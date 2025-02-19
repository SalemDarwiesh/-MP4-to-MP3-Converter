# MP4 to MP3 Converter

This Python script converts all MP4 video files in a specified directory to MP3 audio files.  It uses the `moviepy` library to extract the audio track from the video files.

## Features

*   **Batch Conversion:**  Processes all MP4 files within a given directory.
*   **Simple Usage:** Requires only specifying the directory containing the MP4 files.
*   **Automatic Naming:**  Output MP3 files have the same name as the input MP4 files (with the extension changed to `.mp3`).

## Requirements

*   Python 3.x
*   `moviepy` library:

    ```bash
    pip install moviepy
    ```

    **Note:** `moviepy` depends on `ffmpeg`.  In most cases, `moviepy` will automatically download `ffmpeg` when needed.  However, if you encounter issues, you might need to install `ffmpeg` manually:

    *   **Windows:** Download from [https://www.ffmpeg.org/download.html](https://www.ffmpeg.org/download.html) and add the `bin` directory to your system's PATH environment variable.  Alternatively, use a package manager like Chocolatey (`choco install ffmpeg`).
    *   **macOS:** Use Homebrew: `brew install ffmpeg`
    *   **Linux:** Use your distribution's package manager (e.g., `apt install ffmpeg` on Debian/Ubuntu, `yum install ffmpeg` on Fedora/CentOS).

## Usage

1.  **Install `moviepy` (and potentially `ffmpeg`):**

    ```bash
    pip install moviepy
    ```

2.  **Modify the Script:**
    *   Open the Python script (e.g., `mp4_to_mp3.py`).
    *   Replace the empty string in `directory_path = r""` with the *absolute* path to the directory containing your MP4 files.  Use a raw string (prefix with `r`) to avoid issues with backslashes on Windows.

    Example (within the script):

    ```python
    directory_path = r"C:\Users\YourName\Videos\Convert"  # Example: Windows
    # OR
    directory_path = r"/home/user/Videos/Convert"  # Example: Linux/macOS
    ```

3.  **Run the Script:**

    ```bash
    python mp4_to_mp3.py
    ```

    Replace `mp4_to_mp3.py` with the actual name of your script file.

## Script Explanation

*   **`import os`:** Imports the `os` module for interacting with the operating system (listing files, constructing paths).
*   **`from moviepy.video.io.VideoFileClip import VideoFileClip`:** Imports the `VideoFileClip` class from `moviepy`, which is used to load video files.
*   **`directory_path = r""`:**  This variable *must* be set to the directory containing your MP4 files.
*   **`for filename in os.listdir(directory_path):`:**  This loop iterates through all files and directories within `directory_path`.
*   **`if filename.endswith(".mp4"):`:**  Checks if the current file ends with `.mp4`.
*   **`mp4_path = os.path.join(directory_path, filename)`:** Constructs the full path to the MP4 file.
*   **`mp3_path = os.path.join(directory_path, os.path.splitext(filename)[0] + ".mp3")`:** Constructs the full path to the *output* MP3 file.  `os.path.splitext(filename)[0]` gets the filename without the extension.
*   **`video_clip = VideoFileClip(mp4_path)`:** Loads the MP4 video file using `moviepy`.
*   **`video_clip.audio.write_audiofile(mp3_path)`:** Extracts the audio track from the `video_clip` and saves it as an MP3 file at `mp3_path`.
*   **`print("Conversion from MP4 to MP3 completed.")`:**  Prints a message to the console when the process is finished.

## Troubleshooting

*   **`ImportError: No module named 'moviepy'`:**  Make sure `moviepy` is installed (`pip install moviepy`).
*   **`OSError: [Errno 22] Invalid argument` or similar errors:** Double-check that `directory_path` is a valid *absolute* path and that the directory exists. Use raw strings (prefix with `r`) for paths, especially on Windows.
*   **`MoviePy - গলাকাটা ত্রুটি` (MoviePy - গলাকাটা ত্রুটি)** or similar errors in other languages. These are often related to ffmpeg not being available. Check that ffmpeg is correctly installed and is on your PATH if needed.
*   **Slow conversion:** Video processing can be resource-intensive.  Conversion speed depends on your computer's hardware and the size/length of the video files.

This README file provides clear instructions on how to install the requirements, use the script, and troubleshoot common issues.  It's suitable for a GitHub repository, and explains the script's functionality concisely.
