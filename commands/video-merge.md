---
description: Merge video recording with audio narration into final MP4
argument-hint: [topic]
allowed-tools: Bash(ffmpeg:*), Read
---

# Video Merger

Merge screen recording video with TTS audio narration to create the final training video.

## Your Task

Combine a screen recording with generated narration audio using FFmpeg to produce a professional, web-optimized MP4 video.

## Input

User provides topic name (without file extension):
```
/video-merge installation-and-setup
```

## Expected File Locations

### Video Input
```
recordings/[topic].mov
# or
recordings/[topic].mp4
```

### Audio Input
```
audio/[topic]/narration.mp3
```

### Output
```
output/[topic]-final.mp4
```

## Step 1: Verify Input Files

Check that both files exist:
```bash
ls -lh recordings/[topic].*
ls -lh audio/[topic]/narration.mp3
```

If files don't exist, provide clear error message with expected locations.

## Step 2: Read Configuration

Check `.training-video-generator/config.json` for output settings:

```json
{
  "output": {
    "video_codec": "h264",
    "audio_codec": "aac",
    "quality": "high",
    "resolution": "1920x1080",
    "frame_rate": 30
  },
  "branding": {
    "intro_video": null,
    "outro_video": null
  }
}
```

## Step 3: Merge Video and Audio

### Basic Merge (No Intro/Outro)

```bash
ffmpeg -i recordings/[topic].mov \
       -i audio/[topic]/narration.mp3 \
       -c:v libx264 -preset slow -crf 22 \
       -c:a aac -b:a 192k \
       -movflags +faststart \
       output/[topic]-final.mp4
```

### With Intro/Outro (If Configured)

If `intro_video` or `outro_video` are configured:

1. Create concat list:
```
# concat-list.txt
file 'assets/intro.mp4'
file 'recordings/[topic].mov'
file 'assets/outro.mp4'
```

2. Concatenate videos:
```bash
ffmpeg -f concat -safe 0 -i concat-list.txt \
       -i audio/[topic]/narration.mp3 \
       -c:v libx264 -preset slow -crf 22 \
       -c:a aac -b:a 192k \
       -movflags +faststart \
       output/[topic]-final.mp4
```

## FFmpeg Options Explained

- **`-c:v libx264`**: H.264 video codec (widely compatible)
- **`-preset slow`**: Better compression (slower encoding)
- **`-crf 22`**: Quality level (18-28, lower = better)
- **`-c:a aac`**: AAC audio codec
- **`-b:a 192k`**: Audio bitrate (good quality)
- **`-movflags +faststart`**: Enable web streaming

## Quality Presets

### High Quality (Default)
```bash
-crf 18 -preset slow
# Larger files, best quality
```

### Medium Quality
```bash
-crf 23 -preset medium
# Balanced size/quality
```

### Low Quality (Faster Processing)
```bash
-crf 28 -preset fast
# Smaller files, faster encoding
```

## Step 4: Verify Output

After encoding, verify the video:

```bash
# Get video info
ffprobe -v quiet -print_format json -show_format -show_streams \
        output/[topic]-final.mp4

# Extract key info
Duration: [X:XX]
Video codec: h264
Audio codec: aac
Resolution: 1920x1080
Frame rate: 30 fps
File size: [X] MB
```

## Progress Reporting

Show encoding progress:

```
🎬 Merging video and audio...
   Video: recordings/installation-and-setup.mov (1920x1080, 30fps)
   Audio: audio/installation-and-setup/narration.mp3 (5:00)

⏳ Processing with FFmpeg...
   [====================] 100% (ETA: 0:00)

✅ Encoding complete!

📊 Video Information:
   Duration: 5:00
   Resolution: 1920x1080
   Frame Rate: 30 fps
   Video Codec: h264 (CRF 22)
   Audio Codec: aac (192kbps)
   File Size: 87.3 MB

💾 Output: output/installation-and-setup-final.mp4

🎉 Your training video is ready!
```

## Advanced Options

### Add Watermark

If configured in settings:
```bash
ffmpeg -i input.mp4 -i watermark.png \
       -filter_complex "overlay=10:10" \
       output.mp4
```

### Add Subtitles/Captions

Generate from narration text:
```bash
ffmpeg -i input.mp4 -vf subtitles=captions.srt \
       output.mp4
```

### Adjust Audio Level

If audio too quiet/loud:
```bash
ffmpeg -i input.mp4 -af "volume=1.5" output.mp4
```

## Troubleshooting

### Video/Audio Out of Sync

```bash
# Check duration difference
ffprobe -show_format recordings/[topic].mov
ffprobe -show_format audio/[topic]/narration.mp3

# If video longer: trim video to audio length
# If audio longer: extend video or trim audio
```

### File Too Large

```bash
# Increase CRF value (lower quality, smaller file)
-crf 28

# Use faster preset
-preset veryfast

# Lower resolution
-vf scale=1280:720
```

### Encoding Too Slow

```bash
# Use faster preset
-preset ultrafast

# Hardware acceleration (macOS)
-c:v h264_videotoolbox
```

## Output Optimization

### For YouTube
```bash
-c:v libx264 -preset slow -crf 18 \
-pix_fmt yuv420p \
-c:a aac -b:a 192k \
-movflags +faststart
```

### For Web Hosting
```bash
-c:v libx264 -preset medium -crf 23 \
-maxrate 2M -bufsize 4M \
-c:a aac -b:a 128k \
-movflags +faststart
```

### For Email/Sharing
```bash
-vf scale=1280:720 \
-c:v libx264 -preset fast -crf 28 \
-c:a aac -b:a 96k
```

Complete with success message and next steps (uploading, sharing, etc.).
