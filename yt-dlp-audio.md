#### Download a Youtube playlist with the bestaudio only then convert it to another lossless format.

To download a YouTube playlist with the best audio quality and convert it to a lossless format (like FLAC), follow these steps using `yt-dlp`:

### 1. **Install Prerequisites**
   - **yt-dlp**: [Installation guide](https://github.com/yt-dlp/yt-dlp#installation)
   - **FFmpeg** (required for conversion):  
     - Linux: `sudo apt install ffmpeg`  
     - macOS: `brew install ffmpeg`  
     - Windows: [Download FFmpeg](https://ffmpeg.org/download.html) and add to `PATH`.

---

### 2. **Download & Convert Command**
Run this in your terminal (replace `PLAYLIST_URL` with your playlist link):
```bash
yt-dlp -x --audio-format flac --audio-quality 0 --embed-thumbnail --embed-metadata -o "%(title)s.%(ext)s" "PLAYLIST_URL"
```

#### Explanation:
- `-x` (or `--extract-audio`):  
  Extracts audio from the video (discards video stream).
- `--audio-format flac`:  
  Converts audio to **lossless FLAC** (alternatives: `wav`, `alac`).
- `--audio-quality 0`:  
  Ensures highest bitrate (not needed for lossless, but harmless).
- `--embed-thumbnail`:  
  Embeds YouTube thumbnail in the audio file.
- `--embed-metadata`:  
  Adds metadata (title, artist, etc.).
- `-o "%(title)s.%(ext)s"`:  
  Names files using the video title.

---

### 3. **Key Notes**
- **Lossless Caveat**:  
  YouTube audio is **not lossless** (typically 128-256kbps Opus/AAC). Converting to FLAC preserves the *downloaded quality* without further loss, but won't improve it.
- **Best Audio Source**:  
  Uses `bestaudio` format by default (usually 160kbps Opus). To force higher bitrates:
  ```bash
  yt-dlp -x --audio-format flac -f "ba" -S "acodec:opus" --embed-thumbnail --embed-metadata "PLAYLIST_URL"
  ```
- **Thumbnail/Metadata**:  
  Requires `ffmpeg` and `mutagen`/`pillow` for embedding. Install with:  
  ```bash
  pip install mutagen pillow
  ```

---

### 4. **Verify Audio Quality**
To check available audio formats for a video:
```bash
yt-dlp -F "VIDEO_URL"
```
Look for `audio only` sections with the highest bitrate (e.g., `251` for Opus at ~160kbps).

---

### Example Output
```bash
[ExtractAudio] Destination: Song Title.flac
[EmbedThumbnail] Embedding thumbnail in "Song Title.flac"
[Metadata] Embedding metadata to "Song Title.flac"
```

### Alternative Workflow (2-Step Process)
If you want to keep original audio files **and** convert to FLAC:
```bash
# Step 1: Download best audio in original format
yt-dlp -x -k --audio-quality 0 -o "orig/%(title)s.%(ext)s" "PLAYLIST_URL"

# Step 2: Convert all to FLAC (run in same directory)
for f in orig/*; do ffmpeg -i "$f" -c:a flac -compression_level 12 "${f%.*}.flac"; done
```

This preserves original downloads while creating FLAC copies. Adjust paths as needed.
