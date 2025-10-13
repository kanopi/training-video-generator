# /video-narrate Command

The `/video-narrate` command generates TTS (Text-to-Speech) audio narration from your beat sheet using your choice of TTS provider.

## Overview

This command extracts narration text from your beat sheet and generates high-quality audio files using ElevenLabs, OpenAI TTS, or macOS `say` command.

**Command**: `/video-narrate <topic>`

**Allowed Tools**: `Read`, `Write`, `Bash`

## What It Does

1. **Parses Beat Sheet**
   - Extracts narration text from each beat
   - Maintains beat order and timing

2. **Generates Audio Files**
   - Creates individual MP3 file per beat
   - Uses configured TTS provider
   - Applies voice settings

3. **Creates Master Audio**
   - Concatenates all beat audio files
   - Generates single `narration.mp3`
   - Matches beat sheet timing

## Usage

```bash
/video-narrate installation-and-setup
```

**Parameters**:
- `<topic>`: The topic name (must have existing beat sheet)

**Prerequisites**:
- Beat sheet must exist at `scripts/video-scripts/[topic]-beat-sheet.md`
- TTS provider configured (API keys for ElevenLabs/OpenAI, or macOS for `say`)

## TTS Provider Setup

### Option 1: ElevenLabs (Recommended)

**Quality**: ⭐⭐⭐⭐⭐ (Most natural)
**Cost**: Paid (free tier available)
**Best for**: Professional training videos

1. **Get API Key**:
   - Sign up at [ElevenLabs](https://elevenlabs.io)
   - Go to Profile → API Keys
   - Copy your API key

2. **Set Environment Variable**:
   ```bash
   export ELEVENLABS_API_KEY="your_api_key_here"
   ```

3. **Choose Voice ID**:
   - Browse voices at elevenlabs.io/voices
   - Copy voice ID (e.g., `21m00Tcm4TlvDq8ikWAM` for Rachel)

4. **Configure**:
   ```json
   {
     "tts": {
       "provider": "elevenlabs",
       "voiceId": "21m00Tcm4TlvDq8ikWAM",
       "model": "eleven_monolingual_v1"
     }
   }
   ```

### Option 2: OpenAI TTS

**Quality**: ⭐⭐⭐⭐ (Very good)
**Cost**: Paid ($0.015 per 1K characters)
**Best for**: Cost-effective professional quality

1. **Get API Key**:
   - Sign up at [OpenAI](https://platform.openai.com)
   - Go to API Keys
   - Create new key

2. **Set Environment Variable**:
   ```bash
   export OPENAI_API_KEY="your_api_key_here"
   ```

3. **Choose Voice**:
   Available voices: `alloy`, `echo`, `fable`, `onyx`, `nova`, `shimmer`

4. **Configure**:
   ```json
   {
     "tts": {
       "provider": "openai",
       "voice": "alloy",
       "model": "tts-1"
     }
   }
   ```

### Option 3: macOS Say (Free)

**Quality**: ⭐⭐⭐ (Good for testing)
**Cost**: Free
**Best for**: Testing, internal videos, budget projects

1. **List Available Voices**:
   ```bash
   say -v '?'
   ```

2. **Test Voice**:
   ```bash
   say -v "Samantha" "Hello, this is a test"
   ```

3. **Configure**:
   ```json
   {
     "tts": {
       "provider": "macos",
       "voice": "Samantha"
     }
   }
   ```

**Recommended macOS Voices**:
- **Samantha** (US Female) - Clear, professional
- **Alex** (US Male) - Natural, friendly
- **Daniel** (UK Male) - Authoritative
- **Karen** (Australia Female) - Warm, approachable

## Generated Files

### Individual Beat Audio
**Location**: `audio/[topic]/beat-01-narration.mp3`, `beat-02-narration.mp3`, etc.

Each beat gets its own audio file for flexibility in editing.

### Master Narration
**Location**: `audio/[topic]/narration.mp3`

Single file with all beats concatenated in order.

### Generation Script
**Location**: `scripts/automation/[topic]-narrate.sh`

Bash script that handles the TTS API calls and audio processing.

## Configuration

Configure TTS in `.training-video-generator/config.json`:

```json
{
  "tts": {
    "provider": "elevenlabs",
    "voiceId": "21m00Tcm4TlvDq8ikWAM",
    "model": "eleven_monolingual_v1",
    "settings": {
      "stability": 0.5,
      "similarity_boost": 0.75,
      "style": 0,
      "use_speaker_boost": true
    }
  }
}
```

### ElevenLabs Settings

- **stability** (0-1): Lower = more expressive, Higher = more stable
- **similarity_boost** (0-1): Voice consistency
- **style** (0-1): Exaggeration level (0 for professional)
- **use_speaker_boost**: Enhance voice clarity (recommended: true)

### OpenAI Settings

```json
{
  "tts": {
    "provider": "openai",
    "voice": "alloy",
    "model": "tts-1-hd",
    "speed": 1.0
  }
}
```

- **model**: `tts-1` (faster) or `tts-1-hd` (higher quality)
- **speed** (0.25-4.0): Playback speed (1.0 = normal)

### macOS Say Settings

```json
{
  "tts": {
    "provider": "macos",
    "voice": "Samantha",
    "rate": 175
  }
}
```

- **rate** (90-300): Speaking speed (175 = normal)

## Output Example

```
🗣️  Generating TTS Narration
Topic: installation-and-setup
Provider: elevenlabs
Output: audio/installation-and-setup

🎙️  Generating Beat 01...
  ✅ Created: audio/installation-and-setup/beat-01-narration.mp3
🎙️  Generating Beat 02...
  ✅ Created: audio/installation-and-setup/beat-02-narration.mp3
...

🎵 Creating master audio file...
✅ Master audio: audio/installation-and-setup/narration.mp3

🎉 Narration generation complete!
```

## Audio Processing

### FFmpeg Operations

The command uses FFmpeg to:
1. Convert AIFF to MP3 (for macOS `say`)
2. Concatenate beat audio files
3. Normalize audio levels
4. Apply consistent bitrate (192kbps)

### Audio Quality

**Settings**:
- Codec: MP3 (libmp3lame)
- Bitrate: 192 kbps
- Sample Rate: 44.1 kHz
- Channels: Mono (for narration)

## Tips

1. **Test Your Voice**: Generate a short test narration first
2. **Review Audio**: Listen to individual beats before final merge
3. **Adjust Settings**: Fine-tune stability/speed for your preference
4. **Backup Configuration**: Save your TTS settings for reuse
5. **Cost Management**: Use OpenAI tts-1 (not hd) for drafts

## Troubleshooting

### "API Key not found"

**Problem**: TTS provider API key not set

**Solution**:
```bash
# Check if key is set
echo $ELEVENLABS_API_KEY
echo $OPENAI_API_KEY

# Set key (temporary)
export ELEVENLABS_API_KEY="your_key"

# Set key (permanent)
echo 'export ELEVENLABS_API_KEY="your_key"' >> ~/.zshrc
source ~/.zshrc
```

### "Voice sounds robotic"

**Problem**: TTS sounds unnatural

**Solution**:
- **ElevenLabs**: Increase stability, decrease similarity_boost slightly
- **OpenAI**: Try different voices (nova, shimmer are more expressive)
- **macOS**: Use Samantha, Alex, or premium voices

### "Audio too fast/slow"

**Problem**: Narration pace doesn't match video timing

**Solution**:
- **ElevenLabs**: Edit narration text to be longer/shorter
- **OpenAI**: Adjust `speed` setting (0.9 = slower, 1.1 = faster)
- **macOS**: Adjust `rate` setting (150 = slower, 200 = faster)

### "API request failed"

**Problem**: TTS API returns error

**Solution**:
```bash
# Check API key validity
curl https://api.elevenlabs.io/v1/user \
  -H "xi-api-key: $ELEVENLABS_API_KEY"

# Check OpenAI key
curl https://api.openai.com/v1/models \
  -H "Authorization: Bearer $OPENAI_API_KEY"
```

Common errors:
- **401 Unauthorized**: Invalid API key
- **429 Too Many Requests**: Rate limit exceeded, wait and retry
- **402 Payment Required**: No credits remaining

### "ffmpeg not found"

**Problem**: FFmpeg not installed

**Solution**:
```bash
# macOS
brew install ffmpeg

# Linux (Ubuntu/Debian)
sudo apt-get install ffmpeg

# Linux (Fedora)
sudo dnf install ffmpeg

# Verify installation
ffmpeg -version
```

### "Audio concatenation fails"

**Problem**: Master audio file creation errors

**Solution**:
- Verify all beat audio files exist
- Check file permissions
- Ensure consistent audio format across beats
- Review FFmpeg concat list file

## Advanced Usage

### Custom Audio Processing

Edit generated narration script to add effects:

```bash
# Add background music
ffmpeg -i narration.mp3 -i background.mp3 \
  -filter_complex "[1:a]volume=0.1[bg];[0:a][bg]amix=inputs=2" \
  narration-with-music.mp3

# Normalize audio levels
ffmpeg -i narration.mp3 -af "loudnorm" narration-normalized.mp3

# Add fade in/out
ffmpeg -i narration.mp3 \
  -af "afade=t=in:st=0:d=2,afade=t=out:st=293:d=2" \
  narration-faded.mp3
```

### Regenerate Single Beat

To regenerate just one beat's audio:

```bash
# Edit beat narration in beat sheet
# Then regenerate specific beat
say -v "Samantha" -o audio/topic/beat-03-temp.aiff "Updated narration text"
ffmpeg -i audio/topic/beat-03-temp.aiff -acodec libmp3lame -ab 192k \
  audio/topic/beat-03-narration.mp3 -y
rm audio/topic/beat-03-temp.aiff

# Recreate master audio
cd audio/topic
ffmpeg -f concat -safe 0 -i concat-list.txt -c copy narration.mp3 -y
```

## Cost Estimation

### ElevenLabs
- Free tier: 10,000 characters/month
- Paid: Starts at $5/month for 30,000 characters
- Typical 5-min video: ~750-1000 characters
- **Estimated cost**: $0.15-0.20 per video (paid tier)

### OpenAI
- Cost: $0.015 per 1,000 characters
- Typical 5-min video: ~750-1000 characters
- **Estimated cost**: $0.01-0.02 per video

### macOS Say
- **Cost**: Free

## Next Steps

After generating narration:

1. **Listen** to `narration.mp3` to verify quality
2. **Re-record** any beats that need adjustment
3. **Proceed** to video recording with automation
4. **Run** `/video-merge` to combine video and audio

## Related Commands

- [`/video-script`](video-script.md) - Generate beat sheet (prerequisite)
- [`/video-automate`](video-automate.md) - Generate automation scripts
- [`/video-merge`](video-merge.md) - Merge video and audio
- [Workflow Guide](../guides/workflow.md) - Complete production workflow
