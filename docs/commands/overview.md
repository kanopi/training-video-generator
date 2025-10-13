# Commands Overview

Training Video Generator provides 5 powerful commands that work together to automate video creation. Each command can be used independently or as part of the complete workflow.

---

## Complete Workflow

```mermaid
graph LR
    A[/video-topics] --> B[/video-script]
    B --> C[/video-automate]
    B --> D[/video-narrate]
    C --> E[Record Video]
    E --> F[/video-merge]
    D --> F
    F --> G[Final Video]
```

---

## Commands Quick Reference

| Command | Purpose | Input | Output |
|---------|---------|-------|--------|
| [`/video-topics`](#video-topics) | Analyze project, suggest topics | Project docs | Topic list with details |
| [`/video-script`](#video-script) | Generate beat-by-beat script | Topic name | Beat sheet markdown file |
| [`/video-automate`](#video-automate) | Create automation scripts | Beat sheet file | AppleScript + bash scripts |
| [`/video-narrate`](#video-narrate) | Generate TTS audio | Beat sheet file | Audio files (MP3) |
| [`/video-merge`](#video-merge) | Merge video + audio | Topic name | Final MP4 video |

---

## /video-topics

**Analyzes your project documentation and suggests relevant video topics.**

### Usage

```bash
/video-topics                    # Analyze entire project
/video-topics installation       # Focus on installation topics
/video-topics features          # Focus on feature topics
/video-topics workflows         # Focus on workflow topics
/video-topics api               # Focus on API topics
/video-topics advanced          # Focus on advanced topics
```

### What It Does

- Reads README.md, docs/, and other documentation
- Identifies key features, workflows, and use cases
- Suggests 5-10 video topics with:
  - Clear title
  - Target audience level
  - Estimated duration
  - Key points to cover
  - Required demo materials

### Example Output

See full details in [Video Topics Command](video-topics.md)

---

## /video-script

**Generates a detailed beat-by-beat video script from a topic.**

### Usage

```bash
/video-script "Installation and Setup"
/video-script "Getting Started"
/video-script "Advanced Configuration"
```

### What It Does

- Takes topic title as argument
- Analyzes relevant documentation
- Generates screenplay-style beat sheet with:
  - Narration text (word-for-word)
  - Terminal commands (exact syntax)
  - Browser actions (URLs, clicks)
  - Visual cues (camera positioning)
  - Timing (duration per beat)

### Output Location

```
scripts/video-scripts/
└── [topic-name]-beat-sheet.md
```

### Example Output

See full details in [Video Script Command](video-script.md)

---

## /video-automate

**Creates automation scripts from a beat sheet for recording.**

### Usage

```bash
/video-automate scripts/video-scripts/installation-beat-sheet.md
/video-automate scripts/video-scripts/getting-started-beat-sheet.md
```

### What It Does

- Parses the beat sheet markdown file
- Generates automation scripts:
  - **AppleScript** for iTerm2 terminal automation
  - **Bash script** for command orchestration
  - **Browser automation** for Safari/Chrome
  - **Recording control** for start/stop

### Output Location

```
scripts/automation/
├── [topic-name]-automate.scpt         # Main AppleScript
├── [topic-name]-commands.sh           # Bash commands
├── [topic-name]-timing.json           # Timing data
└── [topic-name]-browser.scpt          # Browser automation
```

### Example Output

See full details in [Video Automate Command](video-automate.md)

---

## /video-narrate

**Generates text-to-speech audio narration from beat sheet.**

### Usage

```bash
/video-narrate scripts/video-scripts/installation-beat-sheet.md
/video-narrate scripts/video-scripts/getting-started-beat-sheet.md
```

### What It Does

- Extracts narration text from each beat
- Calls configured TTS provider:
  - **ElevenLabs** (premium quality)
  - **OpenAI TTS** (high quality)
  - **macOS `say`** (free fallback)
- Generates individual audio clips per beat
- Creates master audio file with timing

### Output Location

```
audio/[topic-name]/
├── beat-01-narration.mp3
├── beat-02-narration.mp3
├── beat-03-narration.mp3
├── ...
└── narration.mp3                     # Master file
```

### Example Output

See full details in [Video Narrate Command](video-narrate.md)

---

## /video-merge

**Merges video recording with audio narration into final MP4.**

### Usage

```bash
/video-merge installation
/video-merge getting-started
/video-merge "advanced-configuration"
```

### What It Does

- Finds video file in `recordings/[topic-name].mov`
- Finds audio file in `audio/[topic-name]/narration.mp3`
- Uses FFmpeg to merge and encode:
  - Video codec: h264
  - Audio codec: aac
  - Resolution: 1920x1080 (or source)
  - Frame rate: 30fps (or source)
- Adds intro/outro if configured
- Optimizes for web playback

### Output Location

```
output/
└── [topic-name]-final.mp4
```

### Example Output

See full details in [Video Merge Command](video-merge.md)

---

## Typical Workflow

### 1. Discovery Phase

```bash
# Analyze project and get topic suggestions
/video-topics
```

Review suggested topics and choose one.

### 2. Script Generation

```bash
# Generate detailed beat-by-beat script
/video-script "Your Chosen Topic"
```

Review and edit `scripts/video-scripts/your-topic-beat-sheet.md` if needed.

### 3. Automation Setup

```bash
# Generate automation scripts
/video-automate scripts/video-scripts/your-topic-beat-sheet.md
```

### 4. Recording

```bash
# Start screen recording (manual)
# Then run automation script:
osascript scripts/automation/your-topic-automate.scpt

# Stop recording and save as:
# recordings/your-topic.mov
```

### 5. Audio Generation

```bash
# Generate TTS narration
/video-narrate scripts/video-scripts/your-topic-beat-sheet.md
```

### 6. Final Production

```bash
# Merge video and audio
/video-merge your-topic
```

Your final video will be at: `output/your-topic-final.mp4`

---

## Command Chaining

While commands don't automatically chain, you can create a simple script to run multiple steps:

```bash
#!/bin/bash

TOPIC="installation-and-setup"

# Generate script
claude /video-script "$TOPIC"

# Generate automation
claude /video-automate "scripts/video-scripts/${TOPIC}-beat-sheet.md"

# Note: Recording must be done manually
echo "Now record video using: osascript scripts/automation/${TOPIC}-automate.scpt"
echo "Save as: recordings/${TOPIC}.mov"
echo "Press Enter when done..."
read

# Generate narration
claude /video-narrate "scripts/video-scripts/${TOPIC}-beat-sheet.md"

# Merge final video
claude /video-merge "$TOPIC"

echo "Done! Video at: output/${TOPIC}-final.mp4"
```

---

## Best Practices

### Topic Selection
- Start with beginner-friendly topics
- Keep videos under 10 minutes
- One concept per video

### Script Review
- Always review generated beat sheets
- Adjust timing if needed
- Test commands manually first

### Recording Quality
- Use 1920x1080 resolution
- Record at 30fps minimum
- Close unnecessary applications
- Clean terminal history

### Audio Quality
- Use ElevenLabs or OpenAI for best quality
- Choose appropriate voice
- Ensure API keys are configured

### File Organization
- Follow the generated directory structure
- Use descriptive topic names
- Keep source files for editing

---

## Next Steps

Learn more about each command:

- [Video Topics Command](video-topics.md) - Detailed usage and examples
- [Video Script Command](video-script.md) - Beat sheet generation
- [Video Automate Command](video-automate.md) - Automation scripts
- [Video Narrate Command](video-narrate.md) - TTS audio generation
- [Video Merge Command](video-merge.md) - Final video production

Or explore guides:

- [Complete Workflow Guide](../guides/workflow.md)
- [Writing Beat Sheets](../guides/beat-sheets.md)
- [Customization Options](../guides/customization.md)
