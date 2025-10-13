---
description: Generate TTS audio narration from beat sheet
argument-hint: [beat-sheet-file]
allowed-tools: Read, Write, Bash(curl:*), Bash(say:*)
---

# Video Narration Generator

Generate text-to-speech audio files from a beat sheet's narration text using configured TTS provider.

## Your Task

Extract narration text from a beat sheet and generate high-quality audio files for each beat, plus a master audio file.

## Input

User provides path to beat sheet file:
```
scripts/video-scripts/[topic]-beat-sheet.md
```

## Step 1: Read Configuration

Check for TTS configuration in `.training-video-generator/config.json`:

```json
{
  "tts": {
    "provider": "elevenlabs",
    "voice_id": "default",
    "api_key_env": "ELEVENLABS_API_KEY",
    "fallback": "macos-say"
  }
}
```

If no config exists, use macOS `say` command as default.

## Step 2: Parse Beat Sheet

Extract from each beat:
- Beat number
- Beat name
- Duration
- Narration text

## Step 3: Generate Audio Per Beat

For each beat, generate audio using the configured provider:

### Option A: ElevenLabs API

```bash
curl -X POST https://api.elevenlabs.io/v1/text-to-speech/[voice-id] \
  -H "xi-api-key: $ELEVENLABS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "[narration text]",
    "model_id": "eleven_monolingual_v1",
    "voice_settings": {
      "stability": 0.5,
      "similarity_boost": 0.75
    }
  }' \
  --output "audio/[topic]/beat-[N]-narration.mp3"
```

### Option B: OpenAI TTS API

```bash
curl https://api.openai.com/v1/audio/speech \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "tts-1",
    "input": "[narration text]",
    "voice": "alloy"
  }' \
  --output "audio/[topic]/beat-[N]-narration.mp3"
```

### Option C: macOS say Command

```bash
say -v "Alex" -o "audio/[topic]/beat-[N]-narration.aiff" "[narration text]"
# Convert to MP3
ffmpeg -i "audio/[topic]/beat-[N]-narration.aiff" \
       -acodec libmp3lame -ab 192k \
       "audio/[topic]/beat-[N]-narration.mp3"
rm "audio/[topic]/beat-[N]-narration.aiff"
```

## Step 4: Create Master Audio File

Concatenate all beat audio files with proper timing:

Create FFmpeg concat list file:
```
# audio-concat.txt
file 'beat-01-narration.mp3'
file 'beat-02-narration.mp3'
file 'beat-03-narration.mp3'
...
```

Merge with FFmpeg:
```bash
ffmpeg -f concat -safe 0 -i audio-concat.txt \
       -c copy audio/[topic]/narration.mp3
```

## Output Structure

```
audio/[topic]/
├── beat-01-narration.mp3      # Individual clips
├── beat-02-narration.mp3
├── beat-03-narration.mp3
├── ...
├── narration.mp3              # Master file
└── audio-concat.txt           # FFmpeg concat list
```

## Progress Reporting

Show progress for each beat:
```
✅ Generated audio for Beat 1: Introduction (15 seconds)
✅ Generated audio for Beat 2: Prerequisites (20 seconds)
✅ Generated audio for Beat 3: Installation (30 seconds)
...
✅ Master audio file created: audio/[topic]/narration.mp3
   Total duration: 5:00
```

## Error Handling

If primary TTS provider fails:
1. Log the error with details
2. Fall back to configured fallback provider
3. If all fail, provide clear error message with troubleshooting steps

## TTS Provider Tips

### ElevenLabs
- Best quality, most natural
- Requires API key
- Check rate limits
- Recommended voices: "Adam", "Rachel", "Domi"

### OpenAI TTS
- Very good quality
- Requires API key
- Fast processing
- Available voices: "alloy", "echo", "fable", "onyx", "nova", "shimmer"

### macOS say
- Free, always available
- Good quality
- No API required
- Best voices: "Alex", "Samantha", "Daniel"

## Configuration Example

Provide example for user to customize:

```json
{
  "tts": {
    "provider": "elevenlabs",
    "voice_id": "21m00Tcm4TlvDq8ikWAM",
    "api_key_env": "ELEVENLABS_API_KEY",
    "fallback": "macos-say",
    "macos_voice": "Samantha",
    "speech_rate": 200,
    "pitch": 50
  }
}
```

Complete with success message and audio file locations.
