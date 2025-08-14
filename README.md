# To run this code you need to install the following dependencies:
# pip install google-genai

import base64
import os
from google import genai
from google.genai import types


def generate():
    client = genai.Client(
        api_key=os.environ.get("GEMINI_API_KEY"),
    )

    model = "gemini-2.5-pro"
    contents = [
        types.Content(
            role="user",
            parts=[
                types.Part.from_text(text="""{
  \"data\": [
    {
      \"access_token\": \"EAAPsGDYlGSwBPOjtaesYVFV46E8PcgZAlzcpj5NlUpDK4kkBOYbSpidjHtYJ8L3IuJDfhDQKRBbsqurNeMW7YCkRgRcLAzg8OnpdUPMnZCydbLiEZATMs8pYAZCJgEpuq2NijYqgtFFRGlWH61BeY4VudzQnaVPPXPTbZClZA7ZCULmrXbW5E2rkff9T4UFoYZB4ruVnbSxZBGXEVpZBb4IcU43MmZAVnrY9WnoZCw5pZBlmOlqwZD\",
      \"category\": \"Reel creator\",
      \"category_list\": [
        {
          \"id\": \"1817904601806120\",
          \"name\": \"Video Creator\"
        }
      ],
      \"name\": \"Moneyloot\",
      \"id\": \"628072577066270\",
      \"tasks\": [
        \"ADVERTISE\",
        \"ANALYZE\",
        \"CREATE_CONTENT\",
        \"MESSAGING\",
        \"MODERATE\",
        \"MANAGE\"
      ]
    }
  ],
  \"paging\": {
    \"cursors\": {
      \"before\": \"QVFIU1lyQi12TkFfZAHVnNWJVVWI3YVBhYzlfVFdLVVEzLThaU3dld1FZAc2FKR1ZAxRFF4QzZAqR2lPdWtnSkxpeFU3UTZA0ZAVZAudzQzbVlURVBiUVRDRC0wQjN3\",
      \"after\": \"QVFIU1lyQi12TkFfZAHVnNWJVVWI3YVBhYzlfVFdLVVEzLThaU3dld1FZAc2FKR1ZAxRFF4QzZAqR2lPdWtnSkxpeFU3UTZA0ZAVZAudzQzbVlURVBiUVRDRC0wQjN3\"
    }
  }
} write code inpython which able to post all video as reels over instagram one by one from this path /sdcard/insta/edited_video , using acces token {
  \"data\": [
    {
      \"access_token\": \"EAAPsGDYlGSwBPOjtaesYVFV46E8PcgZAlzcpj5NlUpDK4kkBOYbSpidjHtYJ8L3IuJDfhDQKRBbsqurNeMW7YCkRgRcLAzg8OnpdUPMnZCydbLiEZATMs8pYAZCJgEpuq2NijYqgtFFRGlWH61BeY4VudzQnaVPPXPTbZClZA7ZCULmrXbW5E2rkff9T4UFoYZB4ruVnbSxZBGXEVpZBb4IcU43MmZAVnrY9WnoZCw5pZBlmOlqwZD\",
      \"category\": \"Reel creator\",
      \"category_list\": [
        {
          \"id\": \"1817904601806120\",
          \"name\": \"Video Creator\"
        }
      ],
      \"name\": \"Moneyloot\",
      \"id\": \"628072577066270\",
      \"tasks\": [
        \"ADVERTISE\",
        \"ANALYZE\",
        \"CREATE_CONTENT\",
        \"MESSAGING\",
        \"MODERATE\",
        \"MANAGE\"
      ]
    }
  ],
  \"paging\": {
    \"cursors\": {
      \"before\": \"QVFIU1lyQi12TkFfZAHVnNWJVVWI3YVBhYzlfVFdLVVEzLThaU3dld1FZAc2FKR1ZAxRFF4QzZAqR2lPdWtnSkxpeFU3UTZA0ZAVZAudzQzbVlURVBiUVRDRC0wQjN3\",
      \"after\": \"QVFIU1lyQi12TkFfZAHVnNWJVVWI3YVBhYzlfVFdLVVEzLThaU3dld1FZAc2FKR1ZAxRFF4QzZAqR2lPdWtnSkxpeFU3UTZA0ZAVZAudzQzbVlURVBiUVRDRC0wQjN3\"
    }
  }
}"""),
            ],
        ),
        types.Content(
            role="model",
            parts=[
                types.Part.from_text(text="""**Investigating API Options**

My initial investigation into the Instagram Graph API is underway. I've begun my search using terms like \"Instagram Graph API post video reel python\" and other relevant phrases to get a sense of the technical landscape. I'm aiming to understand the prerequisites for uploading videos and potential publication containers.


**Unpacking the Process**

I'm now diving deeper into the API's nuances. My current focus is dissecting the multi-step process for reel publication: video upload, media container creation, and final publishing. I'm keen to find Python code examples that clarify parameter requirements, specifically focusing on `access_token`, `instagram_user_id`, `video_url`, and `caption`. With this information, my goal is to build a script to automate reel posting from `/sdcard/insta/edited_video`.


**Considering API Implementation**

I've examined the search results and determined that the Instagram Graph API is the most suitable approach. I now have a solid grasp of how to use it to upload videos as Reels, although I still have to figure out all the nuances.


**Clarifying Public Accessibility**

I'm now fully aware of the public URL requirement for video uploads. The provided local path won't work, so I'll need to emphasize the necessity of a publicly accessible host. I've sketched out the two-phase posting process, uploading to a container first and then publishing. I'm also preparing to clarify the necessary permissions and video specifications.


**Developing the Python Script**

I'm now fully immersed in the Python script's structure. I've broken down the script into manageable modules, from authorization and video processing to the core API interactions for container creation, status polling, and publishing. I'm focusing on clarity and error handling, ensuring robust responses to API failures. The current focus is on the crucial public URL handling and how I can help the user integrate it smoothly into their existing workflow.


**Refining Code Implementation**

I'm finalizing the Python script now, focusing on clean modularity and robust error handling for API responses. I'm prioritizing clear instructions for the user to integrate their public video URLs and ensuring the process is as user-friendly as possible. I've also incorporated detailed comments to clarify each API interaction. I am making it as easy as possible to integrate this into any existing workflow.


"""),
                types.Part.from_text(text="""### Automate Instagram Reel Publishing with Python

This guide provides a Python script to automate the process of uploading and publishing videos as Reels to your Instagram account one by one from a specified directory. The script utilizes the Instagram Graph API and requires your videos to be accessible via a public URL.

**Prerequisites:**

Before running the script, ensure you have the following:

*   **Publicly Hosted Videos:** The Instagram Graph API requires a public URL for each video you want to upload. The provided path `/sdcard/insta/edited_video` is a local directory. You will need to upload the videos from this directory to a web server or a cloud storage service (like Amazon S3, Google Cloud Storage, etc.) that provides public URLs for your files.
*   **Video Specifications:** Your videos must adhere to Instagram's requirements for Reels:
    *   **Container:** MOV or MP4
    *   **Audio Codec:** AAC
    *   **Video Codec:** HEVC or H264
    *   **Frame Rate:** 23-60 FPS
    *   **Aspect Ratio:** Recommended 9:16 to avoid cropping.
    *   **Duration:** Between 3 seconds and 15 minutes.
    *   **File Size:** Maximum 1GB.
*   **Python and `requests` library:** Make sure you have Python installed on your system, along with the `requests` library. You can install it using pip:
    ```bash
    pip install requests
    ```

---

### Python Script for Uploading Instagram Reels

Below is the Python script to upload your videos. Remember to replace the placeholder values with your actual information.

```python
import os
import requests
import time

# --- Configuration ---
ACCESS_TOKEN = \"EAAPsGDYlGSwBPOjtaesYVFV46E8PcgZAlzcpj5NlUpDK4kkBOYbSpidjHtYJ8L3IuJDfhDQKRBbsqurNeMW7YCkRgRcLAzg8OnpdUPMnZCydbLiEZATMs8pYAZCJgEpuq2NijYqgtFFRGlWH61BeY4VudzQnaVPPXPTbZClZA7ZCULmrXbW5E2rkff9T4UFoYZB4ruVnbSxZBGXEVpZBb4IcU43MmZAVnrY9WnoZCw5pZBlmOlqwZD\"
INSTAGRAM_USER_ID = \"628072577066270\"
VIDEO_DIRECTORY = \"/sdcard/insta/edited_video\"  # Local directory of your videos
GRAPH_API_VERSION = \"v18.0\"
BASE_URL = f\"https://graph.facebook.com/{GRAPH_API_VERSION}\"

def upload_reel(video_url, caption=\"\"):
    \"\"\"
    Uploads and publishes a single video as an Instagram Reel.
    \"\"\"
    # --- Step 1: Upload the video to a container ---
    print(f\"Starting to upload video from: {video_url}\")
    upload_url = f\"{BASE_URL}/{INSTAGRAM_USER_ID}/media\"
    upload_params = {
        'media_type': 'REELS',
        'video_url': video_url,
        'caption': caption,
        'share_to_feed': True,
        'access_token': ACCESS_TOKEN
    }
    try:
        upload_response = requests.post(upload_url, params=upload_params)
        upload_response.raise_for_status()  # Raise an exception for bad status codes
        creation_id = upload_response.json().get('id')
        if not creation_id:
            print(\"Error: 'id' not found in the upload response.\")
            print(\"Response:\", upload_response.json())
            return None
        print(f\"Video uploaded to container with creation_id: {creation_id}\")
    except requests.exceptions.RequestException as e:
        print(f\"Error uploading video container: {e}\")
        print(\"Response:\", e.response.json() if e.response else \"No response\")
        return None

    # --- Step 2: Check the status of the container ---
    status_url = f\"{BASE_URL}/{creation_id}\"
    status_params = {
        'fields': 'status_code',
        'access_token': ACCESS_TOKEN
    }
    while True:
        try:
            status_response = requests.get(status_url, params=status_params)
            status_response.raise_for_status()
            status_code = status_response.json().get('status_code')
            print(f\"Current upload status: {status_code}\")

            if status_code == 'FINISHED':
                break
            elif status_code == 'ERROR':
                print(\"Error processing the video.\")
                return None
        except requests.exceptions.RequestException as e:
            print(f\"Error checking status: {e}\")
            return None
        time.sleep(5)  # Wait for 5 seconds before checking the status again

    # --- Step 3: Publish the Reel ---
    print(f\"Publishing the reel with creation_id: {creation_id}\")
    publish_url = f\"{BASE_URL}/{INSTAGRAM_USER_ID}/media_publish\"
    publish_params = {
        'creation_id': creation_id,
        'access_token': ACCESS_TOKEN
    }
    try:
        publish_response = requests.post(publish_url, params=publish_params)
        publish_response.raise_for_status()
        media_id = publish_response.json().get('id')
        print(f\"Successfully published Reel with media_id: {media_id}\")
        return media_id
    except requests.exceptions.RequestException as e:
        print(f\"Error publishing the reel: {e}\")
        print(\"Response:\", e.response.json() if e.response else \"No response\")
        return None

def main():
    \"\"\"
    Iterates through videos in a directory, gets their public URLs,
    and uploads them as Reels.
    \"\"\"
    # THIS IS A PLACEHOLDER. You need to implement the logic to get
    # the public URLs for your videos from your local directory.
    # For example, you might upload them to a cloud service and get the URLs back.
    # The following is a conceptual example.

    # Example: A dictionary mapping local file names to their public URLs
    public_video_urls = {
        \"video1.mp4\": \"https://your-public-server.com/videos/video1.mp4\",
        \"video2.mp4\": \"https://your-public-server.com/videos/video2.mp4\",
        # Add all your video mappings here
    }

    for video_file, public_url in public_video_urls.items():
        local_video_path = os.path.join(VIDEO_DIRECTORY, video_file)
        if os.path.exists(local_video_path):
            print(f\"\\nProcessing video: {video_file}\")
            caption = f\"This is my new Reel: {os.path.splitext(video_file)[0]}\"
            upload_reel(public_url, caption)
            print(\"-\" * 30)
            time.sleep(10)  # Add a delay between uploads to avoid rate limiting
        else:
            print(f\"Video file not found: {local_video_path}\")


if __name__ == \"__main__\":
    main()
```

### How to Use the Script:

1.  **Replace Placeholders:**
    *   Update the `ACCESS_TOKEN` and `INSTAGRAM_USER_ID` with the values from your JSON data.
    *   Set the `VIDEO_DIRECTORY` to the path where your videos are stored locally.

2.  **Populate Public URLs:**
    *   The most critical step is to modify the `main` function. The provided `public_video_urls` dictionary is a placeholder. You need to replace this with your own logic to map your local video files to their corresponding public URLs. This might involve a separate script to upload your videos to a server and generate this mapping.

3.  **Run the Script:**
    *   Execute the script from your terminal:
        ```bash
        python your_script_name.py
        ```

The script will then iterate through your list of public video URLs and post each one as a Reel to your Instagram account. The process involves creating a container for the video, checking the upload status until it is finished, and finally publishing the container. A delay is included between each upload to help prevent hitting API rate limits."""),
            ],
        ),
        types.Content(
            role="user",
            parts=[
                types.Part.from_text(text="""       instaurl.py     mediadown.sh                                only__maya_queen_top_reels_20250426_085349.txt
krishna_tech_guru_30oct@cloudshell:~/insta$ python3 instapost.py
Video file not found: /home/krishna_tech_guru_30oct/vid_editor/edited_video/video1.mp4
Video file not found: /home/krishna_tech_guru_30oct/vid_editor/edited_video/video2.mp4
krishna_tech_guru_30oct@cloudshell:~/insta$  rewrite above code toautomatically select video one by one so rewrite for this 
"""),
            ],
        ),
        types.Content(
            role="model",
            parts=[
                types.Part.from_text(text="""**Addressing Video Selection**

I'm currently revising the `instapost.py` script. The original version had a hardcoded placeholder for video URLs. Now, the goal is to automatically select a video, correcting the \"Video file not found\" error. I'm focusing on dynamic video selection instead of a static placeholder.


**Analyzing File Access Issues**

I'm now investigating how to provide public access to video files within the Cloud Shell environment. Simply pointing to the local directory won't suffice; a public URL is essential for the Instagram API. My focus is on determining a viable method to make these files accessible from the web. I'm exploring potential solutions and documenting the inherent limitations of the Cloud Shell environment for direct file uploads.


**Automating Video Upload**

My focus is shifting to implementing a two-step process to handle video uploads. First, the user needs to upload the video files to a publicly accessible location, like cloud storage. Second, my Python script will then iterate through the local files and automatically construct the public URLs using a base URL provided by the user, dynamically building the necessary Instagram API calls. I'm prioritizing simplifying the user's workload through streamlined automation and configuration.


**Designing Automation Workflow**

The fundamental principle is clear: Instagram API requires public URLs for videos. I'm focusing on crafting a reliable, user-friendly automation workflow. This involves guiding the user through setting up a publicly accessible storage location, like Google Cloud Storage, while simplifying the script to dynamically construct the necessary API calls for uploading videos one by one. I'm prioritizing clarity for user configuration and error handling.


**Refining Script Automation**

I'm now revising the `instapost.py` script to address the user's need for automatic video selection. The core change involves iterating through the local video directory, constructing public URLs for each file, and then making the Instagram API calls. I'm focusing on incorporating user-friendly configuration variables, like `BASE_PUBLIC_URL`, for customizing the video hosting location. I'll also add a file to track already-uploaded videos, avoiding redundant actions. My goal is to streamline the upload process and provide more informative feedback to the user.


**Designing Automated Uploads**

I'm now revising my script to handle file selection. The current approach involves the user providing a `BASE_PUBLIC_URL`, ensuring they first upload the videos to cloud storage. Then the script automates the process of selecting files from a local directory, constructing the corresponding URLs using the base provided, and subsequently posting the videos to Instagram. I will include a log file to track uploaded videos for efficiency. My focus is user-friendliness through automation and informative prompts.


"""),
                types.Part.from_text(text="""Of course. The error `Video file not found` occurs because the previous script used a hardcoded, placeholder list of video files and did not actually scan the directory.

The key challenge remains: **The Instagram API cannot access local files on your computer or Cloud Shell instance.** It requires a **publicly accessible URL** for each video.

Therefore, the process must be in two parts:
1.  **You must upload your videos** from `/home/krishna_tech_guru_30oct/vid_editor/edited_video/` to a place on the internet where they get a public URL. A good option when using Google Cloud Shell is to use a **Google Cloud Storage bucket**.
2.  **This rewritten script will then automatically find** your local video files, construct the public URL for each one, and post them one by one.

Here is the rewritten Python script, `instapost.py`. It is now designed to automatically find videos in your specified directory, construct their public URLs, and upload them, while also keeping track of which videos have already been posted.

### **Instructions**

1.  **Make Your Videos Publicly Accessible:**
    *   Create a Google Cloud Storage bucket.
    *   Upload your video files from `/home/krishna_tech_guru_30oct/vid_editor/edited_video/` to this bucket.
    *   **Crucially, make the files publicly readable.** When you do this, each file will have a public URL, typically in the format `https://storage.googleapis.com/your-bucket-name/your-video-filename.mp4`.

2.  **Update and Run the Script:**
    *   Copy the code below into your `instapost.py` file.
    *   **Edit the `Configuration` section** in the script:
        *   `LOCAL_VIDEO_DIRECTORY`: Set this to the path of your local video files.
        *   `BASE_PUBLIC_URL`: Set this to the base URL of your public storage location (e.g., `https://storage.googleapis.com/your-bucket-name/`). **Don't forget the trailing slash `/`!**
    *   Run the script using `python3 instapost.py`.

---

### Rewritten `instapost.py` Code

```python
import os
import requests
import time
import sys

# --- Configuration (EDIT THESE VALUES) ---
ACCESS_TOKEN = \"EAAPsGDYlGSwBPOjtaesYVFV46E8PcgZAlzcpj5NlUpDK4kkBOYbSpidjHtYJ8L3IuJDfhDQKRBbsqurNeMW7YCkRgRcLAzg8OnpdUPMnZCydbLiEZATMs8pYAZCJgEpuq2NijYqgtFFRGlWH61BeY4VudzQnaVPPXPTbZClZA7ZCULmrXbW5E2rkff9T4UFoYZB4ruVnbSxZBGXEVpZBb4IcU43MmZAVnrY9WnoZCw5pZBlmOlqwZD\"
INSTAGRAM_USER_ID = \"628072577066270\"

# The local directory where your edited video files are.
LOCAL_VIDEO_DIRECTORY = \"/home/krishna_tech_guru_30oct/vid_editor/edited_video\"

# !! IMPORTANT !!
# The public base URL where your videos are hosted.
# For Google Cloud Storage, it will look like: \"https://storage.googleapis.com/your-bucket-name/\"
# MAKE SURE to include the trailing slash \"/\" at the end.
BASE_PUBLIC_URL = \"https://your-public-server.com/videos/\" # <-- CHANGE THIS

# --- End of Configuration ---

# --- Script Internals ---
GRAPH_API_VERSION = \"v18.0\"
BASE_API_URL = f\"https://graph.facebook.com/{GRAPH_API_VERSION}\"
UPLOADED_LOG_FILE = \"uploaded_videos.log\"
SUPPORTED_FORMATS = ('.mp4', '.mov')

def load_uploaded_videos():
    \"\"\"Loads the list of already uploaded video filenames from a log file.\"\"\"
    if not os.path.exists(UPLOADED_LOG_FILE):
        return set()
    with open(UPLOADED_LOG_FILE, 'r') as f:
        return set(line.strip() for line in f)

def log_uploaded_video(filename):
    \"\"\"Adds a successfully uploaded video filename to the log file.\"\"\"
    with open(UPLOADED_LOG_FILE, 'a') as f:
        f.write(f\"{filename}\\n\")

def upload_reel(video_url, caption=\"\"):
    \"\"\"Uploads and publishes a single video as an Instagram Reel.\"\"\"
    print(f\"Starting post for video: {video_url}\")
    
    # --- Step 1: Initialize Upload Container ---
    print(\"Step 1: Initializing upload container...\")
    container_url = f\"{BASE_API_URL}/{INSTAGRAM_USER_ID}/media\"
    container_params = {
        'media_type': 'REELS',
        'video_url': video_url,
        'caption': caption,
        'share_to_feed': True,
        'access_token': ACCESS_TOKEN
    }
    try:
        container_response = requests.post(container_url, params=container_params)
        container_response.raise_for_status()
        creation_id = container_response.json().get('id')
        if not creation_id:
            print(f\"Error: Could not get creation_id from response. Full response: {container_response.json()}\")
            return False
        print(f\"  -> Success! Container ID: {creation_id}\")
    except requests.exceptions.RequestException as e:
        print(f\"  -> Error creating upload container: {e}\")
        print(f\"     Response: {e.response.json() if e.response else 'No response'}\")
        return False

    # --- Step 2: Poll Upload Status ---
    print(\"Step 2: Waiting for video to finish processing...\")
    status_url = f\"{BASE_API_URL}/{creation_id}\"
    status_params = {'fields': 'status_code', 'access_token': ACCESS_TOKEN}
    for _ in range(20): # Poll for up to ~100 seconds
        try:
            status_response = requests.get(status_url, params=status_params)
            status_response.raise_for_status()
            status_code = status_response.json().get('status_code')
            print(f\"  -> Upload status: {status_code}\")

            if status_code == 'FINISHED':
                print(\"  -> Success! Video processing finished.\")
                break
            elif status_code == 'ERROR':
                print(\"  -> Error: Instagram reported an error processing the video.\")
                return False
        except requests.exceptions.RequestException as e:
            print(f\"  -> Error checking status: {e}\")
            return False
        time.sleep(5)
    else:
        print(\"  -> Error: Timed out waiting for video to process.\")
        return False

    # --- Step 3: Publish the Reel ---
    print(\"Step 3: Publishing the reel...\")
    publish_url = f\"{BASE_API_URL}/{INSTAGRAM_USER_ID}/media_publish\"
    publish_params = {'creation_id': creation_id, 'access_token': ACCESS_TOKEN}
    try:
        publish_response = requests.post(publish_url, params=publish_params)
        publish_response.raise_for_status()
        media_id = publish_response.json().get('id')
        print(f\"  -> SUCCESS! Reel published with Media ID: {media_id}\")
        return True
    except requests.exceptions.RequestException as e:
        print(f\"  -> Error publishing the reel: {e}\")
        print(f\"     Response: {e.response.json() if e.response else 'No response'}\")
        return False

def main():
    \"\"\"Finds new videos in the local directory and uploads them one by one.\"\"\"
    
    if \"your-public-server.com\" in BASE_PUBLIC_URL:
        print(\"Error: You have not configured the `BASE_PUBLIC_URL` variable in the script.\")
        print(\"Please edit the script and set it to your public hosting URL (e.g., from Google Cloud Storage).\")
        sys.exit(1)

    if not os.path.isdir(LOCAL_VIDEO_DIRECTORY):
        print(f\"Error: The specified directory does not exist: {LOCAL_VIDEO_DIRECTORY}\")
        sys.exit(1)
        
    print(f\"Scanning for new videos in: {LOCAL_VIDEO_DIRECTORY}\")
    
    already_uploaded = load_uploaded_videos()
    print(f\"Found {len(already_uploaded)} previously uploaded videos in the log file.\")
    
    # Get a sorted list of video files from the directory
    try:
        all_files = sorted(os.listdir(LOCAL_VIDEO_DIRECTORY))
        video_files_to_upload = [
            f for f in all_files 
            if f.lower().endswith(SUPPORTED_FORMATS) and f not in already_uploaded
        ]
    except OSError as e:
        print(f\"Error reading directory {LOCAL_VIDEO_DIRECTORY}: {e}\")
        sys.exit(1)

    if not video_files_to_upload:
        print(\"No new videos to upload.\")
        return

    print(f\"Found {len(video_files_to_upload)} new video(s) to upload.\")

    for filename in video_files_to_upload:
        # Construct the full public URL for the video
        public_url = f\"{BASE_PUBLIC_URL}{filename}\"
        caption = f\"Check out this reel! #{os.path.splitext(filename)[0].replace('_', ' ')}\"
        
        print(\"\\n\" + \"=\"*50)
        
        # Upload the reel
        success = upload_reel(public_url, caption)
        
        if success:
            log_uploaded_video(filename)
        
        print(\"=\"*50)
        
        # Wait for a bit before posting the next one to avoid API rate limits
        print(\"\\nWaiting for 30 seconds before next upload...\")
        time.sleep(30)
    
    print(\"\\nAll new videos have been processed.\")

if __name__ == \"__main__\":
    main()
```"""),
            ],
        ),
        types.Content(
            role="user",
            parts=[
                types.Part.from_text(text="""
krishna_tech_guru_30oct@cloudshell:~/insta$ python3 instapost.py
Error: You have not configured the `BASE_PUBLIC_URL` variable in the script.
Please edit the script and set it to your public hosting URL (e.g., from Google Cloud Storage).
"""),
            ],
        ),
        types.Content(
            role="model",
            parts=[
                types.Part.from_text(text="""**Diagnosing the Root Cause**

I've homed in on the explicit error message: \"Error: You have not configured the `BASE_PUBLIC_URL` variable in the script.\" This clearly indicates the central issue. It's a configuration oversight. I'm now exploring how the script handles the absence of this vital variable, and how best to advise the user to resolve it. I need to figure out what's the best next action here.


**Addressing the Configuration Issue**

I'm now zeroing in on the best way to present the solution to the user. Given the explicit nature of the error message, a direct approach is best. I plan to start by acknowledging the error, explaining the underlying need for a public URL, and then clearly outlining the necessary configuration step. I also want to make sure I don't confuse the user by going too far into details or code, as they are not the focus.


**Formulating the Resolution**

I'm finalizing the structure of the resolution I'll present. I plan to start by directly acknowledging the error message. Then, I'll briefly explain *why* the error occurs, reinforcing the need for a public URL.  I'm focusing on providing a clear, step-by-step guide: get the public URL, then edit the script with \"before\" and \"after\" code examples. This will be the clearest way to address the issue. I have an example structure to make the resolution as easy to understand as possible.


**Refining the Response Structure**

I've finalized the structure of the response, focusing on clarity and ease of understanding. I'll begin by directly acknowledging the error message. Then, I'll briefly explain the underlying issue—the need for a public URL. The solution will be presented as a clear, numbered list: obtain the public URL, edit the script with \"before\" and \"after\" examples, and then rerun it. I'll make sure to use bolding and code blocks to make key parts stand out, and end with a sentence prompting the user to re-try. I think this format is most effective in addressing the problem.


**Devising a Clear Outline**

I've crafted a comprehensive, structured response to guide the user. I'll begin by directly acknowledging the error message they encountered. My explanation will cover the core problem: the need for a public URL. Then, I'll provide a concise, step-by-step solution, offering guidance on obtaining a public URL (e.g., via Google Cloud Storage), along with concrete \"before\" and \"after\" code examples within a code block, and clear steps to rerun the script. I'll conclude by prompting the user to re-try.


"""),
                types.Part.from_text(text="""You've encountered the exact safety check that was built into the script. The error message is correct and is there to help you.

`Error: You have not configured the 'BASE_PUBLIC_URL' variable in the script.`

### **What This Error Means**

This error means you have not told the script where your videos are located on the internet.

Remember, the Instagram API **cannot see the files on your Cloud Shell computer**. You must first upload your videos to a public web server, and the `BASE_PUBLIC_URL` is the web address of that location.

The script works by taking the `BASE_PUBLIC_URL` and adding your video's filename to the end of it.

*   **BASE_PUBLIC_URL:** `https://storage.googleapis.com/my-insta-videos/`
*   **Video Filename:** `my_cool_reel_01.mp4`
*   **Resulting URL sent to Instagram:** `https://storage.googleapis.com/my-insta-videos/my_cool_reel_01.mp4`

Without the correct base URL, the script would send a fake link to Instagram, and it would fail.

### **How to Fix It**

You need to complete two steps:

**Step 1: Upload Your Videos and Get Your Public URL**

1.  Go to the [Google Cloud Storage browser](https://console.cloud.google.com/storage/browser).
2.  Create a new bucket (e.g., `krishna-tech-guru-reels-2025`).
3.  Upload the videos from your computer's `/home/krishna_tech_guru_30oct/vid_editor/edited_video/` directory into the bucket you just created.
4.  **Crucially**, you must make the files public. Select all the uploaded videos, click \"Edit Access,\" add a new principal named `allUsers`, and assign it the role of \"Storage Object Viewer.\"
5.  Your public base URL will be: `https://storage.googleapis.com/your-bucket-name/`
    *   For example: `https://storage.googleapis.com/krishna-tech-guru-reels-2025/`

**Step 2: Edit the `instapost.py` Script**

1.  Open your `instapost.py` file for editing.
2.  Find this line:
    ```python
    BASE_PUBLIC_URL = \"https://your-public-server.com/videos/\" # <-- CHANGE THIS
    ```
3.  **Change the placeholder URL** to the actual public URL of your Google Cloud Storage bucket. Make sure it ends with a `/`.

    **Example:**

    ```python
    # Before
    BASE_PUBLIC_URL = \"https://your-public-server.com/videos/\" # <-- CHANGE THIS

    # After
    BASE_PUBLIC_URL = \"https://storage.googleapis.com/krishna-tech-guru-reels-2025/\" # <-- CHANGE THIS
    ```

**Step 3: Save and Run Again**

Save the changes to `instapost.py` and run it again:

```bash
python3 instapost.py
```

Now that the script knows where to find your videos online, it will proceed with the upload process."""),
            ],
        ),
        types.Content(
            role="user",
            parts=[
                types.Part.from_text(text="""INSERT_INPUT_HERE"""),
            ],
        ),
    ]
    tools = [
        types.Tool(googleSearch=types.GoogleSearch(
        )),
    ]
    generate_content_config = types.GenerateContentConfig(
        thinking_config = types.ThinkingConfig(
            thinking_budget=-1,
        ),
        tools=tools,
    )

    for chunk in client.models.generate_content_stream(
        model=model,
        contents=contents,
        config=generate_content_config,
    ):
        print(chunk.text, end="")

if __name__ == "__main__":
    generate()
