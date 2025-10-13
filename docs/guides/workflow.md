# Complete Video Production Workflow

This guide walks you through the complete process of creating a training video from start to finish.

## Overview

The Training Video Generator workflow consists of 5 main stages:

1. **Topic Discovery** - Find what to teach
2. **Script Generation** - Plan the video beats
3. **Automation Setup** - Prepare terminal automation
4. **Audio Creation** - Generate TTS narration
5. **Recording & Merge** - Capture and combine

**Total Time**: 30-60 minutes per 5-minute video (after initial setup)

## Prerequisites

Before starting, ensure you have:

- ✅ Plugin installed (see [Installation](../installation.md))
- ✅ FFmpeg installed (`brew install ffmpeg`)
- ✅ iTerm2 installed (macOS) or terminal of choice
- ✅ TTS provider configured (ElevenLabs, OpenAI, or macOS `say`)
- ✅ Screen recording method ready (macOS Cmd+Shift+5, OBS Studio, etc.)

## Stage 1: Topic Discovery

### Goal
Identify the best topics for training videos based on your project's documentation.

### Steps

1. **Navigate to your project**:
   ```bash
   cd /path/to/your/project
   ```

2. **Run topic discovery**:
   ```bash
   /video-topics
   ```

3. **Review suggestions**:
   - Output: `scripts/video-scripts/suggested-topics.md`
   - Topics organized by category and difficulty
   - Each with audience level, duration, prerequisites

4. **Select a topic**:
   - Start with beginner-level topics (Installation, Getting Started)
   - Choose 5-10 minute duration for first videos
   - Pick topics with clear prerequisites

**Time**: 5-10 minutes

**Example Output**:
```markdown
## Installation & Setup
### Installing MyProject
- **Audience**: Beginner
- **Duration**: 5 minutes
- **Prerequisites**: Node.js 18+
```

## Stage 2: Script Generation

### Goal
Create a detailed beat-by-beat script with narration, commands, and timing.

### Steps

1. **Generate beat sheet**:
   ```bash
   /video-script installation-and-setup
   ```

2. **Review the generated script**:
   - Output: `scripts/video-scripts/installation-and-setup-beat-sheet.md`
   - Check narration for natural flow
   - Verify commands are correct
   - Confirm timing is realistic

3. **Edit and refine**:
   - Read narration aloud to check pacing
   - Test terminal commands in clean environment
   - Adjust beat durations if needed
   - Add visual notes for highlighting

4. **Calculate total duration**:
   - Sum all beat durations
   - Add buffer time (10-15%)
   - Ensure matches target length

**Time**: 15-30 minutes

**Tips**:
- Keep narration conversational, not formal
- Include "why" explanations, not just "what"
- Pause after important commands (2-3 seconds)
- Plan browser switches in advance

## Stage 3: Automation Setup

### Goal
Create AppleScript automation to execute terminal commands with proper timing.

### Steps

1. **Generate automation scripts**:
   ```bash
   /video-automate installation-and-setup
   ```

2. **Review generated files**:
   - `scripts/automation/installation-and-setup-automate.scpt` (AppleScript)
   - `scripts/automation/installation-and-setup-record.sh` (Recording wrapper)

3. **Test automation without recording**:
   ```bash
   osascript scripts/automation/installation-and-setup-automate.scpt
   ```

4. **Adjust timing if needed**:
   - Edit `.scpt` file delay values
   - Increase delays if commands need more time
   - Decrease if there are long pauses

5. **Prepare recording environment**:
   - Clean terminal (no history)
   - Increase terminal font size (18-24pt)
   - Hide personal information
   - Close distracting applications
   - Set consistent window dimensions

**Time**: 10-15 minutes

**Common Adjustments**:
```applescript
-- Too fast? Increase delays
delay 5  -- was: delay 2

-- Need more read time? Add pauses
write text "npm install"
delay 3  -- give viewers time to see output
```

## Stage 4: Audio Creation

### Goal
Generate high-quality TTS narration matching your beat sheet.

### Steps

1. **Ensure TTS provider is configured**:
   ```bash
   # ElevenLabs
   echo $ELEVENLABS_API_KEY

   # OpenAI
   echo $OPENAI_API_KEY

   # macOS (always available)
   say -v '?' | grep Samantha
   ```

2. **Generate narration**:
   ```bash
   /video-narrate installation-and-setup
   ```

3. **Review audio files**:
   - Individual beats: `audio/installation-and-setup/beat-01-narration.mp3`, etc.
   - Master file: `audio/installation-and-setup/narration.mp3`

4. **Listen to master narration**:
   ```bash
   # macOS
   open audio/installation-and-setup/narration.mp3

   # Linux
   vlc audio/installation-and-setup/narration.mp3

   # FFmpeg
   ffplay audio/installation-and-setup/narration.mp3
   ```

5. **Regenerate if needed**:
   - Edit beat sheet narration
   - Re-run `/video-narrate`
   - Adjust TTS settings (voice, speed, stability)

**Time**: 5-10 minutes (plus TTS API time)

**Quality Check**:
- [ ] Narration sounds natural
- [ ] No pronunciation errors
- [ ] Volume is consistent
- [ ] Pacing matches beat timing
- [ ] Total duration is correct

## Stage 5: Recording & Merge

### Goal
Record screen with automation, then merge with narration audio.

### Steps

#### A. Recording

1. **Prepare to record**:
   ```bash
   # Run recording wrapper
   bash scripts/automation/installation-and-setup-record.sh
   ```

2. **Start screen recording**:
   - **macOS**: Press `Cmd + Shift + 5`
   - **OBS Studio**: Click "Start Recording"
   - **Other**: Use your preferred tool

3. **Select recording area**:
   - Terminal window + browser if needed
   - Full screen or specific region
   - Recommended: 1920x1080 or 1280x720

4. **Begin recording**:
   - Click "Record" button
   - Wait 2-3 seconds for recording to start
   - Return to terminal

5. **Run automation**:
   ```bash
   osascript scripts/automation/installation-and-setup-automate.scpt
   ```

6. **Let automation complete**:
   - Don't touch mouse/keyboard during automation
   - Watch for completion notification
   - Verify all commands executed successfully

7. **Stop recording**:
   - **macOS**: Click stop button in menu bar
   - **OBS**: Click "Stop Recording"
   - Save as `recordings/installation-and-setup.mov`

**Time**: 5-10 minutes (actual video length + setup)

#### B. Merging

1. **Verify input files exist**:
   ```bash
   ls -lh recordings/installation-and-setup.mov
   ls -lh audio/installation-and-setup/narration.mp3
   ```

2. **Run merge command**:
   ```bash
   /video-merge installation-and-setup
   ```

3. **Wait for processing**:
   - FFmpeg will encode video
   - Time varies by video length and settings
   - Typical 5-min video: 2-5 minutes processing

4. **Verify output**:
   ```bash
   ls -lh output/installation-and-setup-final.mp4
   ```

5. **Review final video**:
   ```bash
   open output/installation-and-setup-final.mp4
   ```

**Time**: 5-15 minutes (depending on video length)

**Quality Check**:
- [ ] Video and audio are synchronized
- [ ] Audio levels are good (not too quiet/loud)
- [ ] Video is clear and readable
- [ ] No unexpected cuts or glitches
- [ ] File size is reasonable

## Complete Workflow Example

Here's a real example from start to finish:

### 1. Topic Discovery (5 minutes)

```bash
cd ~/Projects/my-awesome-project
/video-topics
# Review: scripts/video-scripts/suggested-topics.md
# Choose: "Installing My Awesome Project"
```

### 2. Script Generation (20 minutes)

```bash
/video-script installation-and-setup
# Review: scripts/video-scripts/installation-and-setup-beat-sheet.md
# Edit narration for natural flow
# Test all terminal commands
# Finalize beat sheet
```

### 3. Automation Setup (10 minutes)

```bash
/video-automate installation-and-setup
# Test: osascript scripts/automation/installation-and-setup-automate.scpt
# Adjust timing in .scpt file
# Prepare clean terminal environment
```

### 4. Audio Creation (5 minutes)

```bash
# Verify TTS provider
echo $ELEVENLABS_API_KEY

# Generate narration
/video-narrate installation-and-setup

# Listen to review
open audio/installation-and-setup/narration.mp3
```

### 5. Recording (7 minutes)

```bash
# Start recording wrapper
bash scripts/automation/installation-and-setup-record.sh

# Press Cmd+Shift+5, select area, click Record
# Wait 3 seconds
# Press 'y' to run automation
# Wait for completion notification
# Stop recording
# Save as: recordings/installation-and-setup.mov
```

### 6. Merge (5 minutes)

```bash
/video-merge installation-and-setup
# Wait for FFmpeg processing
# Review: output/installation-and-setup-final.mp4
```

**Total Time**: ~52 minutes for a 5-minute video

## Optimization Tips

### Speed Up Production

After your first video, you'll get faster:

1. **Reuse configurations**: TTS settings, recording setup
2. **Template beat sheets**: Copy structure from previous videos
3. **Batch operations**: Generate multiple scripts, then record all
4. **Keyboard shortcuts**: Save common commands as aliases

### Improve Quality

1. **Professional audio**: Invest in ElevenLabs or OpenAI TTS
2. **Better recording**: Use OBS Studio for more control
3. **Post-processing**: Add intro/outro, captions, b-roll
4. **Consistent branding**: Reuse templates, colors, fonts

### Reduce File Sizes

1. **Lower resolution**: 720p instead of 1080p
2. **Increase CRF**: 26 instead of 22 (smaller files, slightly lower quality)
3. **Use faster preset**: "medium" instead of "slow"
4. **Trim unnecessary footage**: Cut long pauses, errors

## Troubleshooting Common Issues

### Audio/Video Out of Sync

**Cause**: Narration duration doesn't match automation timing

**Solution**:
1. Check beat sheet timing accuracy
2. Verify automation delays match narration
3. Re-record with corrected timing
4. Use FFmpeg `-itsoffset` to adjust sync

### Commands Fail During Recording

**Cause**: Environment not clean or prerequisites missing

**Solution**:
1. Test automation in clean terminal first
2. Verify all prerequisites are met
3. Use absolute paths in commands
4. Add error handling to automation

### TTS Sounds Unnatural

**Cause**: Provider settings or text formatting

**Solution**:
1. Try different voices
2. Adjust stability/speed settings
3. Rewrite narration more conversationally
4. Add punctuation for natural pauses

### Video Quality Poor

**Cause**: Wrong encoding settings or source resolution

**Solution**:
1. Record at higher resolution (1080p)
2. Lower CRF value (22 or lower)
3. Use slower FFmpeg preset
4. Increase bitrate

## Next Steps

- [Beat Sheet Writing Guide](beat-sheets.md) - Write better scripts
- [Customization Guide](customization.md) - Configure for your needs
- [Troubleshooting](troubleshooting.md) - Solve common problems
- [Examples](../examples/sample-video.md) - See complete examples

## Need Help?

- Check [Troubleshooting Guide](troubleshooting.md)
- Review [Command Documentation](../commands/overview.md)
- Visit [GitHub Issues](https://github.com/thejimbirch/training-video-generator/issues)
