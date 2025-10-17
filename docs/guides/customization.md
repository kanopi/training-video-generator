# Customization Guide

The Training Video Generator is highly customizable to fit your workflow, brand, and preferences.

## Configuration File

Create `.training-video-generator/config.json` in your project root:

```json
{
  "project": {
    "name": "My Awesome Project",
    "version": "1.0.0",
    "docsPath": "docs/",
    "examplesPath": "examples/"
  },
  "video": {
    "defaultDuration": 7,
    "targetAudience": ["beginner", "intermediate"],
    "categories": ["installation", "features", "workflows", "api"]
  },
  "tts": {
    "provider": "elevenlabs",
    "voiceId": "21m00Tcm4TlvDq8ikWAM",
    "model": "eleven_monolingual_v1",
    "settings": {
      "stability": 0.5,
      "similarity_boost": 0.75
    }
  },
  "recording": {
    "resolution": "1920x1080",
    "framerate": 30,
    "terminalApp": "iTerm2",
    "terminalTheme": "Solarized Dark"
  },
  "encoding": {
    "codec": "libx264",
    "crf": 22,
    "preset": "slow",
    "audioBitrate": "192k"
  }
}
```

## Project Settings

### Basic Info

```json
{
  "project": {
    "name": "My Awesome Project",
    "version": "1.0.0",
    "description": "A tool for doing awesome things",
    "repository": "https://github.com/user/project"
  }
}
```

**Usage**: Appears in beat sheet headers, video metadata

### Documentation Paths

```json
{
  "project": {
    "docsPath": "documentation/",
    "apiDocsPath": "api/",
    "examplesPath": "examples/",
    "tutorialsPath": "tutorials/"
  }
}
```

**Usage**: Where `/video-topics` looks for content

### Output Directories

```json
{
  "directories": {
    "scripts": "video-scripts/",
    "audio": "audio-files/",
    "recordings": "screen-recordings/",
    "output": "final-videos/",
    "automation": "automation-scripts/"
  }
}
```

**Default structure**:
```
project/
├── scripts/
│   ├── video-scripts/      (beat sheets)
│   └── automation/         (AppleScripts, bash)
├── audio/                  (TTS narration)
├── recordings/             (screen recordings)
└── output/                 (final videos)
```

## Video Settings

### Default Parameters

```json
{
  "video": {
    "defaultDuration": 4,
    "introDuration": 15,
    "conclusionDuration": 20,
    "beatDurationRange": [20, 45]
  }
}
```

**Explanation**:
- `defaultDuration`: Target video length in minutes (most videos should be 3-5 minutes)
- `introDuration`: Intro beat duration in seconds
- `conclusionDuration`: Conclusion beat duration in seconds
- `beatDurationRange`: Min/max beat duration [min, max] in seconds

### Target Audience

```json
{
  "video": {
    "targetAudience": ["beginner", "intermediate"],
    "skipCategories": ["advanced", "api"]
  }
}
```

**Options**:
- `beginner`: Installation, getting started
- `intermediate`: Features, workflows
- `advanced`: Architecture, optimization
- `api`: API reference, integration

### Content Categories

```json
{
  "video": {
    "categories": [
      "installation",
      "features",
      "workflows",
      "troubleshooting",
      "api"
    ],
    "priorityCategories": ["installation", "features"]
  }
}
```

## TTS Configuration

### ElevenLabs

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

**Voice IDs** (popular choices):
- `21m00Tcm4TlvDq8ikWAM` - Rachel (American Female)
- `ErXwobaYiN019PkySvjV` - Antoni (American Male)
- `VR6AewLTigWG4xSOukaG` - Arnold (British Male)
- `EXAVITQu4vr4xnSDxMaL` - Sarah (British Female)

**Settings**:
- `stability` (0-1): 0.3-0.5 for expressive, 0.5-0.7 for consistent
- `similarity_boost` (0-1): 0.75 recommended for most uses
- `style` (0-1): 0 for professional, 0.3+ for more personality
- `use_speaker_boost`: true for clarity boost (recommended)

### OpenAI

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

**Voices**:
- `alloy` - Neutral, balanced
- `echo` - Male, clear
- `fable` - British, warm
- `onyx` - Deep, authoritative
- `nova` - Female, energetic
- `shimmer` - Soft, friendly

**Models**:
- `tts-1`: Faster, good quality
- `tts-1-hd`: Slower, higher quality

**Speed**: 0.25-4.0 (1.0 = normal)

### macOS Say

```json
{
  "tts": {
    "provider": "macos",
    "voice": "Samantha",
    "rate": 175
  }
}
```

**Recommended Voices**:
- `Samantha` (US Female) - Clear, professional
- `Alex` (US Male) - Natural, friendly
- `Daniel` (UK Male) - Authoritative
- `Karen` (Australia Female) - Warm
- `Moira` (Ireland Female) - Distinct

**Rate**: 90-300 (175 = normal speaking speed)

### Fallback Chain

```json
{
  "tts": {
    "provider": "elevenlabs",
    "fallbackChain": ["openai", "macos"]
  }
}
```

If ElevenLabs fails, try OpenAI, then macOS `say`.

## Recording Settings

### Video Quality

```json
{
  "recording": {
    "resolution": "1920x1080",
    "framerate": 30,
    "bitrate": "5000k"
  }
}
```

**Resolution options**:
- `1920x1080` - Full HD (recommended for most)
- `2560x1440` - 2K (high-end)
- `1280x720` - HD (smaller files)

**Framerate**:
- `30` - Standard, smooth (recommended)
- `60` - Very smooth (larger files)
- `24` - Cinematic (smaller files)

### Terminal Configuration

```json
{
  "recording": {
    "terminalApp": "iTerm2",
    "terminalTheme": "Solarized Dark",
    "terminalFont": "Monaco",
    "terminalFontSize": 20,
    "terminalSize": "140x40"
  }
}
```

**Terminal Apps**:
- `iTerm2` (macOS) - Best automation support
- `Terminal.app` (macOS) - Built-in
- `Gnome Terminal` (Linux)
- `Windows Terminal` (Windows)

**Recommended Settings**:
- Font size: 18-24pt (readable in video)
- Theme: High contrast (Solarized Dark, Dracula)
- Size: 140x40 or larger

### Automation Settings

```json
{
  "automation": {
    "defaultDelay": 2,
    "commandDelay": 1,
    "pauseAfterOutput": 2,
    "typingSpeed": "instant"
  }
}
```

**Timing**:
- `defaultDelay`: Seconds between beats
- `commandDelay`: Seconds before entering command
- `pauseAfterOutput`: Seconds after command completes
- `typingSpeed`: `instant` or `human` (simulated typing)

## Encoding Settings

### Video Codec

```json
{
  "encoding": {
    "videoCodec": "libx264",
    "videoCRF": 22,
    "videoPreset": "slow",
    "videoProfile": "high",
    "videoLevel": "4.0"
  }
}
```

**CRF** (quality):
- `18` - Near lossless (huge files)
- `22` - High quality (recommended)
- `26` - Good quality (smaller files)
- `30` - Acceptable quality (small files)

**Preset** (speed vs compression):
- `ultrafast` - Fastest, largest files
- `fast` - Quick, larger files
- `medium` - Balanced
- `slow` - Better compression (recommended)
- `veryslow` - Best compression, slowest

### Audio Codec

```json
{
  "encoding": {
    "audioCodec": "aac",
    "audioBitrate": "192k",
    "audioSampleRate": 44100,
    "audioChannels": 1
  }
}
```

**Bitrate**:
- `128k` - Good for voice
- `192k` - High quality (recommended)
- `256k` - Very high quality (larger files)

**Channels**:
- `1` - Mono (recommended for narration)
- `2` - Stereo (for music/effects)

### Format Options

```json
{
  "encoding": {
    "outputFormat": "mp4",
    "faststart": true,
    "pixelFormat": "yuv420p"
  }
}
```

**Options**:
- `faststart`: Optimize for web streaming (recommended)
- `pixelFormat`: `yuv420p` for compatibility

## Branding

### Visual Identity

```json
{
  "branding": {
    "logo": "assets/logo.png",
    "introVideo": "assets/intro.mp4",
    "outroVideo": "assets/outro.mp4",
    "watermark": "assets/watermark.png"
  }
}
```

**Usage**:
- `logo`: Shown during introduction beat
- `introVideo`: Prepended to final video
- `outroVideo`: Appended to final video
- `watermark`: Overlaid throughout (corner)

### Text Overlays

```json
{
  "branding": {
    "titleCard": {
      "enabled": true,
      "duration": 3,
      "template": "assets/title-card.png"
    },
    "subtitles": {
      "enabled": true,
      "font": "Arial",
      "fontSize": 24,
      "color": "white",
      "backgroundColor": "rgba(0,0,0,0.7)"
    }
  }
}
```

### Music

```json
{
  "branding": {
    "backgroundMusic": {
      "intro": "assets/music/intro.mp3",
      "outro": "assets/music/outro.mp3",
      "volume": 0.1
    }
  }
}
```

**Volume**: 0.05-0.15 (5-15%, subtle background)

## Workflow Presets

### Quick & Dirty (Testing)

```json
{
  "preset": "quick",
  "tts": {
    "provider": "macos",
    "voice": "Samantha"
  },
  "encoding": {
    "crf": 26,
    "preset": "fast"
  },
  "recording": {
    "resolution": "1280x720"
  }
}
```

**Use case**: Fast iteration, internal testing

### High Quality (Production)

```json
{
  "preset": "production",
  "tts": {
    "provider": "elevenlabs",
    "voiceId": "21m00Tcm4TlvDq8ikWAM"
  },
  "encoding": {
    "crf": 20,
    "preset": "slow"
  },
  "recording": {
    "resolution": "1920x1080"
  }
}
```

**Use case**: Public release, professional content

### YouTube Optimized

```json
{
  "preset": "youtube",
  "encoding": {
    "videoCodec": "libx264",
    "crf": 21,
    "preset": "slow",
    "audioBitrate": "192k"
  },
  "recording": {
    "resolution": "1920x1080",
    "framerate": 30
  },
  "branding": {
    "introVideo": "assets/youtube-intro.mp4",
    "outroVideo": "assets/youtube-outro.mp4"
  }
}
```

**Use case**: YouTube uploads, social media

## Environment Variables

### API Keys

```bash
# ElevenLabs
export ELEVENLABS_API_KEY="your_key_here"

# OpenAI
export OPENAI_API_KEY="your_key_here"
```

### Configuration Override

```bash
# Use specific config file
export TVG_CONFIG="/path/to/config.json"

# Override TTS provider
export TVG_TTS_PROVIDER="openai"

# Override output directory
export TVG_OUTPUT_DIR="./custom-output"
```

### Debugging

```bash
# Enable debug logging
export TVG_DEBUG=1

# Verbose FFmpeg output
export TVG_FFMPEG_VERBOSE=1
```

## Per-Command Configuration

### Override for Specific Videos

Create topic-specific config:
```
.training-video-generator/
├── config.json                    (default)
├── installation.json              (for installation videos)
└── api-reference.json             (for API videos)
```

Reference in command:
```bash
/video-script installation --config installation.json
```

## Custom Templates

### Beat Sheet Template

Create custom template at `.training-video-generator/templates/custom-beat-sheet.md`:

```markdown
# Video: {{TOPIC_TITLE}}
**Series**: {{SERIES_NAME}}
**Episode**: {{EPISODE_NUMBER}}
**Duration**: {{TOTAL_DURATION}} minutes

<!-- Your custom sections -->

## Beat {{BEAT_NUMBER}}: {{BEAT_TITLE}}
**Duration**: {{BEAT_DURATION}} seconds
**Visual**: {{BEAT_VISUAL}}

**Narration**:
"{{BEAT_NARRATION}}"

<!-- Your custom beat sections -->
```

Use with:
```bash
/video-script my-topic --template custom-beat-sheet
```

### AppleScript Template

Custom automation at `.training-video-generator/templates/custom-automate.scpt`:

```applescript
#!/usr/bin/osascript
-- Your custom automation logic
tell application "{{TERMINAL_APP}}"
    -- Your custom commands
end tell
```

## Tips

1. **Start with defaults**: Don't customize until you know what you want
2. **Commit config**: Add `.training-video-generator/config.json` to git
3. **Version control**: Track config changes with your project
4. **Document overrides**: Comment why you changed settings
5. **Test before production**: Try new settings on short test videos
6. **Share configs**: Team members can use same settings

## Examples

### Example 1: Company Training Videos

```json
{
  "project": {
    "name": "Acme Corp Internal Tools",
    "version": "2.1.0"
  },
  "tts": {
    "provider": "openai",
    "voice": "onyx",
    "model": "tts-1-hd"
  },
  "branding": {
    "logo": "assets/acme-logo.png",
    "watermark": "assets/acme-watermark.png",
    "titleCard": {
      "enabled": true,
      "template": "assets/title-card-acme.png"
    }
  },
  "recording": {
    "resolution": "1280x720"
  }
}
```

### Example 2: Open Source Project

```json
{
  "project": {
    "name": "AwesomeDB",
    "repository": "https://github.com/user/awesomedb"
  },
  "tts": {
    "provider": "macos",
    "voice": "Samantha"
  },
  "video": {
    "targetAudience": ["beginner", "intermediate"],
    "categories": ["installation", "features", "workflows"]
  },
  "encoding": {
    "crf": 24,
    "preset": "medium"
  }
}
```

### Example 3: YouTube Channel

```json
{
  "project": {
    "name": "DevTips Channel"
  },
  "tts": {
    "provider": "elevenlabs",
    "voiceId": "21m00Tcm4TlvDq8ikWAM",
    "settings": {
      "stability": 0.4,
      "style": 0.3
    }
  },
  "branding": {
    "introVideo": "assets/youtube-intro-5s.mp4",
    "outroVideo": "assets/youtube-outro-10s.mp4",
    "backgroundMusic": {
      "intro": "assets/music/upbeat-intro.mp3",
      "outro": "assets/music/upbeat-outro.mp3",
      "volume": 0.12
    }
  },
  "recording": {
    "resolution": "1920x1080",
    "framerate": 30
  }
}
```

## Next Steps

- [Workflow Guide](workflow.md) - Complete production process
- [Beat Sheets](beat-sheets.md) - Writing effective scripts
- [Troubleshooting](troubleshooting.md) - Solving common issues
- [Command Reference](../commands/overview.md) - All commands
