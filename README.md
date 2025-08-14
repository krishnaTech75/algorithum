Of course. This is a great evolution for the script, making it a flexible, interactive tool rather than a hardcoded one.

This rewritten code will now:

1.  **Ask for the URL** of the media you want to post.
2.  **Automatically convert** a standard GitHub link into the raw content link that the API needs.
3.  **Ask if the URL is an image or a video.**
4.  Execute the correct API calls for the specified media type to post to **both Instagram and Facebook**.
5.  Include the robust video upload process, which involves creating a container, waiting for it to be processed, and then publishing.

### Fully Rewritten `instapost.py` Code

Copy this entire code block and replace the content of your `instapost.py` file. The only thing you need to edit is the `ACCESS_TOKEN`.

```python
import requests
import sys
import time

# --- Configuration (ONLY EDIT THE ACCESS TOKEN) ---
# PASTE YOUR ACCESS TOKEN WITH `pages_manage_posts` PERMISSION HERE.
ACCESS_TOKEN = "PASTE_YOUR_NEW_TOKEN_WITH_PAGES_MANAGE_POSTS_PERMISSION_HERE"

# This is your Facebook Page ID.
FACEBOOK_PAGE_ID = "628072577066270"

# --- End of Configuration ---


# --- Script Internals (No changes needed below) ---
GRAPH_API_VERSION = "v18.0"
BASE_API_URL = f"https://graph.facebook.com/{GRAPH_API_VERSION}"

def convert_github_url(url):
    """Converts a standard GitHub file URL to its raw content URL."""
    if "github.com" in url and "/blob/" in url:
        new_url = url.replace("github.com", "raw.githubusercontent.com").replace("/blob/", "/")
        print(f"  -> Converted GitHub URL to raw format: {new_url}")
        return new_url
    return url

def get_account_ids(page_id, access_token):
    """Fetches the Facebook Page and linked Instagram Business Account details."""
    print("\nStep 1: Fetching account details from Facebook...")
    url = f"{BASE_API_URL}/{page_id}"
    params = {'fields': 'name,instagram_business_account{id,username}', 'access_token': access_token}
    try:
        response = requests.get(url, params=params)
        response.raise_for_status()
        data = response.json()
        if 'instagram_business_account' not in data:
            print("  -> ERROR: No Instagram Business Account is linked to this Facebook Page.")
            return None
        accounts = {
            'page_id': page_id, 'page_name': data.get('name'),
            'instagram_id': data['instagram_business_account'].get('id'),
            'instagram_username': data['instagram_business_account'].get('username')
        }
        print("  -> Details successfully fetched.")
        return accounts
    except requests.exceptions.RequestException as e:
        print(f"  -> FATAL ERROR fetching details: {e.response.text}")
        return None

# --- Photo Posting Functions ---
def post_instagram_photo(instagram_id, image_url, caption, access_token):
    """Publishes a photo to the specified Instagram Business Account."""
    print("\n--- Posting to Instagram ---")
    container_url = f"{BASE_API_URL}/{instagram_id}/media"
    container_params = {'image_url': image_url, 'caption': caption, 'access_token': access_token}
    try:
        container_response = requests.post(container_url, params=container_params).json()
        creation_id = container_response['id']
        publish_url = f"{BASE_API_URL}/{instagram_id}/media_publish"
        publish_params = {'creation_id': creation_id, 'access_token': access_token}
        requests.post(publish_url, params=publish_params).raise_for_status()
        print("  -> Successfully published photo to Instagram.")
    except Exception as e:
        print(f"  -> FAILED to post to Instagram. Reason: {e}")

def post_facebook_photo(page_id, image_url, caption, access_token):
    """Publishes a photo to the specified Facebook Page."""
    print("\n--- Posting to Facebook ---")
    url = f"{BASE_API_URL}/{page_id}/photos"
    params = {'url': image_url, 'caption': caption, 'access_token': access_token}
    try:
        requests.post(url, params=params).raise_for_status()
        print("  -> Successfully published photo to Facebook.")
    except Exception as e:
        print(f"  -> FAILED to post to Facebook. Reason: {e}")

# --- Video Posting Functions ---
def post_instagram_video(instagram_id, video_url, caption, access_token):
    """Publishes a video (Reel) to the specified Instagram Business Account."""
    print("\n--- Posting Reel to Instagram (this may take a minute) ---")
    try:
        # Step 1: Create Media Container
        print("  -> Step A: Creating video container...")
        container_url = f"{BASE_API_URL}/{instagram_id}/media"
        container_params = {'media_type': 'REELS', 'video_url': video_url, 'caption': caption, 'access_token': access_token}
        container_response = requests.post(container_url, params=container_params).json()
        creation_id = container_response['id']
        
        # Step 2: Poll for Status
        print(f"  -> Step B: Waiting for video to process (Container ID: {creation_id})...")
        for _ in range(20): # Poll for up to 100 seconds
            status_url = f"{BASE_API_URL}/{creation_id}"
            status_params = {'fields': 'status_code', 'access_token': access_token}
            status_response = requests.get(status_url, params=status_params).json()
            status_code = status_response.get('status_code')
            print(f"     Status: {status_code}")
            if status_code == 'FINISHED':
                break
            if status_code == 'ERROR':
                raise Exception("Video processing failed.")
            time.sleep(5)
        else:
            raise Exception("Timed out waiting for video processing.")
            
        # Step 3: Publish
        print("  -> Step C: Publishing video...")
        publish_url = f"{BASE_API_URL}/{instagram_id}/media_publish"
        publish_params = {'creation_id': creation_id, 'access_token': access_token}
        requests.post(publish_url, params=publish_params).raise_for_status()
        print("  -> Successfully published video to Instagram.")
    except Exception as e:
        print(f"  -> FAILED to post video to Instagram. Reason: {e}")

def post_facebook_video(page_id, video_url, caption, access_token):
    """Publishes a video to the specified Facebook Page."""
    print("\n--- Posting Video to Facebook ---")
    url = f"{BASE_API_URL}/{page_id}/videos"
    params = {'file_url': video_url, 'description': caption, 'access_token': access_token}
    try:
        requests.post(url, params=params).raise_for_status()
        print("  -> Successfully published video to Facebook.")
    except Exception as e:
        print(f"  -> FAILED to post video to Facebook. Reason: {e}")


def main():
    """Main execution flow: Ask user for input and post accordingly."""
    if "PASTE_YOUR_NEW_TOKEN" in ACCESS_TOKEN:
        print("CRITICAL ERROR: You must edit the script and add your Access Token.")
        sys.exit(1)

    # --- Get User Input ---
    media_url = input("Enter the URL of the image or video to post:\n> ")
    media_url = convert_github_url(media_url.strip())

    media_type = ""
    while media_type not in ['image', 'video']:
        media_type = input("Is this an 'image' or a 'video'?\n> ").lower().strip()
    
    caption = input("Enter a caption for your post:\n> ")

    # --- Fetch Account Details ---
    accounts = get_account_ids(FACEBOOK_PAGE_ID, ACCESS_TOKEN)
    if not accounts:
        sys.exit(1)

    print("\n--- Account Info ---")
    print(f"  Facebook Page:      '{accounts['page_name']}' (ID: {accounts['page_id']})")
    print(f"  Instagram Account:  '@{accounts['instagram_username']}' (ID: {accounts['instagram_id']})")

    # --- Execute Posting Logic ---
    if media_type == 'image':
        post_instagram_photo(accounts['instagram_id'], media_url, caption, ACCESS_TOKEN)
        post_facebook_photo(accounts['page_id'], media_url, caption, ACCESS_TOKEN)
    elif media_type == 'video':
        post_instagram_video(accounts['instagram_id'], media_url, caption, ACCESS_TOKEN)
        post_facebook_video(accounts['page_id'], media_url, caption, ACCESS_TOKEN)

    print("\n--- Script Finished ---")

if __name__ == "__main__":
    main()
```

### How to Use the New Script

1.  **Save the Code:** Paste the entire script into your `instapost.py` file.
2.  **Add Your Access Token:** Make sure you replace `"PASTE_YOUR_NEW_TOKEN_..._HERE"` with your actual, valid Access Token that has the `pages_manage_posts` permission.
3.  **Run the script:**
    ```bash
    python3 instapost.py
    ```
4.  **Follow the Prompts:** The script will now ask you for the URL, the type of media, and the caption directly in your terminal.

**Example Interaction:**

```bash
krishna_tech_guru_30oct@cloudshell:~/insta$ python3 instapost.py
Enter the URL of the image or video to post:
> https://github.com/krishnaTech75/algorithum/blob/main/video.mp4
  -> Converted GitHub URL to raw format: https://raw.githubusercontent.com/krishnaTech75/algorithum/main/video.mp4
Is this an 'image' or a 'video'?
> video
Enter a caption for your post:
> This is a test video posted by my awesome Python script! #Python #Automation #API

Step 1: Fetching account details from Facebook...
  -> Details successfully fetched.

--- Account Info ---
  Facebook Page:      'Moneyloot' (ID: 628072577066270)
  Instagram Account:  '@paisa.lootlo' (ID: 17841474889920887)

--- Posting Reel to Instagram (this may take a minute) ---
  -> Step A: Creating video container...
  -> Step B: Waiting for video to process (Container ID: 179...)...
     Status: IN_PROGRESS
     Status: IN_PROGRESS
     Status: FINISHED
  -> Step C: Publishing video...
  -> Successfully published video to Instagram.

--- Posting Video to Facebook ---
  -> Successfully published video to Facebook.

--- Script Finished ---
```
