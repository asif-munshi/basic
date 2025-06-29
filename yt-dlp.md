#### Question: Help me download a youtube video with audio at 2160p with yt-dlp.

To download a YouTube video in **2160p (4K) with audio** using `yt-dlp`, follow these steps:

### 1. **Install Prerequisites**
   - **yt-dlp**: [Installation guide](https://github.com/yt-dlp/yt-dlp#installation)
   - **FFmpeg** (required for merging audio/video):  
     - Linux: `sudo apt install ffmpeg`  
     - macOS: `brew install ffmpeg`  
     - Windows: [Download FFmpeg](https://ffmpeg.org/download.html) and add it to your `PATH`.

---

### 2. **Download Command**
Run this command in your terminal (replace `VIDEO_URL` with your YouTube URL):
```bash
yt-dlp -f "bestvideo[height<=2160][ext=webm]+bestaudio/best" --merge-output-format mkv "VIDEO_URL"
```

#### Explanation:
- `-f "bestvideo[height<=2160][ext=webm]+bestaudio/best"`:
  - Selects the best 2160p (or lower) WebM video stream + best audio stream.
  - Falls back to a pre-merged format if 2160p isn't available.
- `--merge-output-format mkv`:  
  Merges streams into an `.mkv` container (supports all codecs).

---

### 3. **Key Notes**
- **Why MKV?**  
  YouTube's 2160p streams often use codecs like `VP9`/`AV1`, which are better supported in MKV than MP4. If you need MP4, add `--recode-video mp4` (may require re-encoding).
- **Avoid Re-encoding**:  
  Use `mkv` to preserve quality. Recoding to MP4 can degrade quality and take longer.
- **H.264 Preference** (if available):  
  Add `-S "vcodec:h264"` to prioritize H.264 over VP9/AV1 (rare in 2160p):
  ```bash
  yt-dlp -f "bestvideo[height<=2160]+bestaudio" -S "vcodec:h264" --merge-output-format mkv "VIDEO_URL"
  ```

---

### 4. **Verify Available Formats**
To see all formats for a video (identify 2160p streams):
```bash
yt-dlp -F "VIDEO_URL"
```
Look for `2160p` rows under `VIDEO` and `AUDIO` sections.

---

### Example Output
```bash
[info] Available formats for VIDEO_ID:
...
137          webm       2560x1440  1440p  ...
248          webm       3840x2160  2160p  ... (best video)
251          webm       audio only          ... (best audio)
```

This ensures you download the highest quality 2160p video with audio. Let me know if you encounter issues!
