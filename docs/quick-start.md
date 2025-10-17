# Quick Start

Create your first training video in minutes! This guide walks you through the complete process from analyzing your project to producing a final video.

---

## Prerequisites

Before you begin, make sure you have:

- ✅ Training Video Generator plugin installed
- ✅ FFmpeg installed
- ✅ At least one TTS provider configured (ElevenLabs, OpenAI, or macOS `say`)

See the [Installation Guide](installation.md) if you need help with setup.

---

## Your First Video: 5 Simple Steps

### Step 1: Analyze Your Project

Navigate to your project directory in Claude Code and run:

```bash
/video-topics
```

**What happens:**
- Analyzes README.md, docs/, and other documentation
- Identifies key features and workflows
- Suggests 5-10 video topics with:
  - Topic title
  - Target audience (beginner/intermediate/advanced)
  - Estimated duration
  - Key points to cover

**Example Output:**

```markdown
# Suggested Video Topics for MyProject

## 1. Installation and Setup (Beginner, 5 min)
- Installing dependencies
- Configuration steps
- Running for the first time
- Verifying installation

## 2. Core Features Overview (Beginner, 8 min)
- Feature A walkthrough
- Feature B demonstration
- Feature C usage
- Best practices

## 3. Advanced Configuration (Intermediate, 10 min)
...
```

**Choose a topic** - Pick one that matches your needs. For your first video, choose a beginner-friendly topic like "Installation" or "Getting Started".

---

### Step 2: Generate Beat-by-Beat Script

Generate a detailed video script for your chosen topic:

```bash
/video-script "Installation and Setup"
```

**What happens:**
- Creates a screenplay-style beat sheet
- Includes narration text, terminal commands, browser actions
- Estimates timing for each scene
- Saves to `scripts/video-scripts/installation-and-setup-beat-sheet.md`

**Example Beat Sheet:**

````markdown
# Video: Installation and Setup
**Duration**: 5 minutes
**Target Audience**: Beginner
**Prerequisites**: None

---

## Beat 1: Introduction
**Duration**: 15 seconds
**Visual**: Terminal - iTerm2
**Browser Tab**: N/A

**Narration**:
"Welcome to MyProject! In this video, we'll walk through the complete installation and setup process. By the end, you'll have MyProject up and running on your machine."

**Terminal Commands**:
```bash
# No commands in intro
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show clean terminal
- Display project logo

---

## Beat 2: Prerequisites Check
**Duration**: 20 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"First, let's verify you have the required prerequisites. You'll need Node.js version 18 or higher, and npm version 9 or higher."

**Terminal Commands**:
```bash
node --version
npm --version
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show version output clearly

---

## Beat 3: Installation
**Duration**: 30 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"Now let's install MyProject. We'll use npm to install it globally so it's available anywhere on your system."

**Terminal Commands**:
```bash
npm install -g myproject
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show installation progress
- Wait for completion

---

[More beats continue...]
````

**Review the script** - Read through the generated beat sheet and make any necessary adjustments.

---

### Step 3: Generate Automation Scripts

Create automation scripts that will execute the terminal commands automatically during recording:

```bash
/video-automate scripts/video-scripts/installation-and-setup-beat-sheet.md
```

**What happens:**
- Parses the beat sheet
- Generates AppleScript for iTerm2
- Creates bash orchestration scripts
- Includes timing delays
- Saves to `scripts/automation/installation-and-setup-automate.scpt`

**Generated Files:**

```
scripts/automation/
├── installation-and-setup-automate.scpt    # Main AppleScript
├── installation-and-setup-commands.sh      # Bash commands
└── installation-and-setup-timing.json      # Timing data
```

**Example AppleScript Output:**

```applescript
tell application "iTerm2"
    -- Beat 1: Introduction (15 seconds)
    create window with default profile
    tell current session of current window
        delay 15
    end tell

    -- Beat 2: Prerequisites Check (20 seconds)
    tell current session of current window
        write text "node --version"
        delay 3
        write text "npm --version"
        delay 17
    end tell

    -- Beat 3: Installation (30 seconds)
    tell current session of current window
        write text "npm install -g myproject"
        delay 30
    end tell
end tell
```

---

### Step 4: Record Your Video

Now you'll record the screen while the automation scripts run the commands.

#### Option A: Manual Recording (Recommended for First Time)

1. **Start screen recording:**
   - macOS: Press `Shift + Command + 5`
   - Select "Record Entire Screen" or "Record Selected Portion"
   - Click "Record"

2. **Run the automation script:**
   ```bash
   osascript scripts/automation/installation-and-setup-automate.scpt
   ```

3. **Let it run:** The script will automatically execute all commands with proper timing

4. **Stop recording:**
   - macOS: Click stop button in menu bar
   - Save video as `recordings/installation-and-setup.mov`

#### Option B: Automated Recording (Advanced)

For fully automated recording, the generated scripts include recording control. See [Advanced Recording Guide](guides/workflow.md).

---

### Step 5: Generate Narration Audio

Generate the voice-over narration from the beat sheet:

```bash
/video-narrate scripts/video-scripts/installation-and-setup-beat-sheet.md
```

**What happens:**
- Extracts narration text from each beat
- Calls your configured TTS provider (ElevenLabs, OpenAI, or macOS)
- Generates individual audio clips per beat
- Creates master audio file with proper timing
- Saves to `audio/installation-and-setup/`

**Generated Files:**

```
audio/installation-and-setup/
├── beat-01-narration.mp3
├── beat-02-narration.mp3
├── beat-03-narration.mp3
├── ...
└── narration.mp3              # Master audio file
```

**Example Output:**

```
✅ Generated audio for Beat 1 (15 seconds)
✅ Generated audio for Beat 2 (20 seconds)
✅ Generated audio for Beat 3 (30 seconds)
...
✅ Master audio file created: audio/installation-and-setup/narration.mp3
   Total duration: 5:00
```

---

### Step 6: Merge Video and Audio

Combine your screen recording with the narration audio:

```bash
/video-merge installation-and-setup
```

**What happens:**
- Finds video file: `recordings/installation-and-setup.mov`
- Finds audio file: `audio/installation-and-setup/narration.mp3`
- Merges using FFmpeg
- Encodes to h264/aac
- Adds intro/outro if configured
- Saves to `output/installation-and-setup-final.mp4`

**Example Output:**

```
🎬 Merging video and audio...
   Video: recordings/installation-and-setup.mov (1920x1080, 30fps)
   Audio: audio/installation-and-setup/narration.mp3 (5:00)

✅ Processing with FFmpeg...
✅ Encoding video (h264)...
✅ Encoding audio (aac)...
✅ Synchronizing...
✅ Finalizing...

🎉 Video created successfully!
   Location: output/installation-and-setup-final.mp4
   Size: 87.3 MB
   Duration: 5:00
   Resolution: 1920x1080
   Format: MP4 (h264/aac)
```

---

## 🎉 Congratulations!

You've created your first training video! Your final video is at:

```
output/installation-and-setup-final.mp4
```

You can now:
- ✅ Upload to YouTube, Vimeo, or your video platform
- ✅ Embed in documentation
- ✅ Share with your team
- ✅ Include in courses or tutorials

---

## Complete Workflow Example

Here's the full command sequence:

```bash
# 1. Analyze project
/video-topics

# 2. Generate script
/video-script "Installation and Setup"

# 3. Generate automation
/video-automate scripts/video-scripts/installation-and-setup-beat-sheet.md

# 4. Record video (manual step)
# - Start screen recording
# - Run: osascript scripts/automation/installation-and-setup-automate.scpt
# - Stop recording and save as recordings/installation-and-setup.mov

# 5. Generate narration
/video-narrate scripts/video-scripts/installation-and-setup-beat-sheet.md

# 6. Merge final video
/video-merge installation-and-setup

# Done! Video at: output/installation-and-setup-final.mp4
```

---

## Tips for Better Videos

### 1. Keep Videos Short
- Aim for 3-10 minutes per video
- Break complex topics into multiple videos
- One concept per video works best

### 2. Test Commands First
- Run all terminal commands manually before recording
- Verify they work in a clean environment
- Document any prerequisites

### 3. Review Beat Sheets
- Read through generated scripts before recording
- Adjust timing if needed
- Ensure commands are correct

### 4. Good Audio Quality
- Use ElevenLabs or OpenAI for best results
- Choose appropriate voice and speed
- Test audio output before merging

### 5. Clean Environment
- Close unnecessary applications
- Hide personal information
- Use a fresh terminal window
- Clear command history if needed

---

## Next Steps

Now that you've created your first video, explore more:

- **[All Commands](commands/overview.md)** - Learn what each command can do
- **[Workflow Guide](guides/workflow.md)** - Advanced workflows and automation
- **[Beat Sheet Guide](guides/beat-sheets.md)** - Write better video scripts
- **[Customization](guides/customization.md)** - Adapt to your style

---

## Troubleshooting Quick Start

### Video Topic Generation Failed

**Problem**: `/video-topics` returns no suggestions

**Solutions**:
1. Ensure you have a README.md or docs/ in your project
2. Check that Claude Code can read project files
3. Try running from project root directory

### Automation Script Doesn't Work

**Problem**: AppleScript fails to run

**Solutions**:
1. Verify iTerm2 is installed and running
2. Grant automation permissions in System Settings
3. Test script manually: `osascript script.scpt`

### Audio Generation Failed

**Problem**: TTS generation fails

**Solutions**:
1. Check API key is set: `echo $ELEVENLABS_API_KEY`
2. Verify API quota hasn't been exceeded
3. Try fallback provider (macOS `say`)

### Video Sync Issues

**Problem**: Audio and video are out of sync

**Solutions**:
1. Ensure video duration matches script timing
2. Check that recording captured all commands
3. Adjust timing in beat sheet if needed
4. Re-record with corrected timing

---

**Need Help?** [Check Troubleshooting Guide](guides/troubleshooting.md) or [Open an Issue](https://github.com/kanopi/training-video-generator/issues)
