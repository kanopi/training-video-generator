# Troubleshooting Guide

Common issues and their solutions when creating training videos.

## Installation Issues

### Plugin Not Found

**Problem**: Claude Code doesn't recognize `/video-*` commands

**Symptoms**:
```
Unknown command: /video-topics
```

**Solutions**:

1. **Verify installation**:
   ```bash
   ls -la ~/.claude/plugins/training-video-generator
   ```

2. **Check plugin.json exists**:
   ```bash
   cat ~/.claude/plugins/training-video-generator/.claude-plugin/plugin.json
   ```

3. **Restart Claude Code**: Close and reopen after installing

4. **Check project settings** (for project-specific install):
   ```json
   // .claude/settings.json
   {
     "enabledPlugins": ["training-video-generator"]
   }
   ```

### FFmpeg Not Found

**Problem**: Commands fail with "ffmpeg: command not found"

**Solutions**:

```bash
# macOS
brew install ffmpeg

# Linux (Ubuntu/Debian)
sudo apt-get update
sudo apt-get install ffmpeg

# Linux (Fedora)
sudo dnf install ffmpeg

# Windows
# Download from https://ffmpeg.org/download.html
# Add to PATH environment variable

# Verify installation
ffmpeg -version
```

### iTerm2 Not Found (macOS)

**Problem**: AppleScript errors about iTerm2

**Solution**:
```bash
# Check if installed
ls /Applications/iTerm.app

# Install if missing
brew install --cask iterm2

# Grant permissions
# System Preferences → Security & Privacy → Privacy → Automation
# Enable iTerm2 → System Events
```

## TTS Issues

### API Key Not Set

**Problem**: "API key not found" or authentication errors

**Symptoms**:
```
Error: ELEVENLABS_API_KEY environment variable not set
```

**Solutions**:

1. **Check if key is set**:
   ```bash
   echo $ELEVENLABS_API_KEY
   echo $OPENAI_API_KEY
   ```

2. **Set temporarily** (current session):
   ```bash
   export ELEVENLABS_API_KEY="your_key_here"
   export OPENAI_API_KEY="your_key_here"
   ```

3. **Set permanently**:
   ```bash
   # Bash
   echo 'export ELEVENLABS_API_KEY="your_key"' >> ~/.bashrc
   source ~/.bashrc

   # Zsh (macOS default)
   echo 'export ELEVENLABS_API_KEY="your_key"' >> ~/.zshrc
   source ~/.zshrc

   # Fish
   set -Ux ELEVENLABS_API_KEY "your_key"
   ```

### Voice Sounds Robotic

**Problem**: TTS narration sounds unnatural or mechanical

**Solutions**:

**ElevenLabs**:
```json
{
  "tts": {
    "settings": {
      "stability": 0.4,        // Lower = more expressive
      "similarity_boost": 0.75,
      "style": 0.2,            // Add slight personality
      "use_speaker_boost": true
    }
  }
}
```

**OpenAI**:
- Try different voices: `nova`, `shimmer` are more expressive
- Adjust speed: `"speed": 0.95` for slightly slower

**macOS**:
- Use premium voices: `Samantha`, `Alex`
- Adjust rate: `"rate": 170` for slightly slower

### API Rate Limit Exceeded

**Problem**: "429 Too Many Requests" error

**Symptoms**:
```
Error 429: Rate limit exceeded
```

**Solutions**:

1. **Wait and retry**: Rate limits reset after time
2. **Batch generation**: Generate all narration at once, not beat-by-beat
3. **Upgrade plan**: Consider paid tier with higher limits
4. **Use fallback**: Configure fallback to different provider

### TTS Generation Fails

**Problem**: Narration files not created

**Solutions**:

1. **Check audio directory exists**:
   ```bash
   mkdir -p audio/[topic]
   ```

2. **Verify API key is valid**:
   ```bash
   # ElevenLabs
   curl https://api.elevenlabs.io/v1/user \
     -H "xi-api-key: $ELEVENLABS_API_KEY"

   # OpenAI
   curl https://api.openai.com/v1/models \
     -H "Authorization: Bearer $OPENAI_API_KEY"
   ```

3. **Check network connection**:
   ```bash
   ping api.elevenlabs.io
   ping api.openai.com
   ```

4. **Review error logs**: Check terminal output for specific errors

## Recording Issues

### Automation Runs Too Fast

**Problem**: Commands execute before narration finishes

**Solution**:

Edit `.scpt` file to increase delays:

```applescript
-- Before
delay 2

-- After (increase by 2-3x)
delay 5
```

Calculate delays:
- Read narration aloud, time it
- Add command execution time
- Add 2-3 second buffer

### Automation Runs Too Slow

**Problem**: Long pauses between commands

**Solution**:

Decrease delays in `.scpt` file:

```applescript
-- Before
delay 10

-- After
delay 5
```

### Commands Fail During Recording

**Problem**: Commands error out or don't execute

**Common Causes & Solutions**:

1. **Wrong directory**:
   ```applescript
   -- Add explicit directory change
   write text "cd ~/Projects/my-project"
   delay 2
   ```

2. **Missing prerequisites**:
   ```bash
   # Test all commands manually first
   node --version
   npm --version
   ```

3. **Environment not clean**:
   - Start with fresh terminal
   - Clear history: `history -c`
   - Remove existing directories
   - Close other applications

4. **Permissions issues**:
   ```bash
   # Check file permissions
   ls -la

   # Fix if needed
   chmod +x script.sh
   ```

### Screen Recording Stops Unexpectedly

**Problem**: macOS stops recording during automation

**Solution**:

Grant screen recording permission:
1. **System Preferences** → **Security & Privacy**
2. **Privacy** tab → **Screen Recording**
3. Enable **iTerm2** (or your terminal app)
4. Restart terminal app

### Terminal Not Visible in Recording

**Problem**: Recorded video shows wrong window or blank screen

**Solutions**:

1. **Bring terminal to front**: Click terminal before starting automation
2. **Full screen mode**: Use terminal in full screen (Cmd+Ctrl+F)
3. **Record specific window**: Use screen recording tool's window selection
4. **Check display settings**: Ensure correct display is being recorded

## Video Issues

### Audio/Video Out of Sync

**Problem**: Narration doesn't match video actions

**Symptoms**:
- Audio ahead of video
- Audio behind video
- Drift over time

**Solutions**:

1. **Check beat sheet timing**:
   - Read narration aloud, time it
   - Ensure matches beat duration
   - Add/remove pauses as needed

2. **Adjust automation delays**:
   ```applescript
   -- Match beat sheet timing
   delay {{BEAT_DURATION}}
   ```

3. **Manual sync adjustment** (FFmpeg):
   ```bash
   # Audio 1.5 seconds behind
   ffmpeg -i video.mov -itsoffset 1.5 -i audio.mp3 \
          -c:v libx264 -c:a aac output.mp4 -y

   # Audio 1.5 seconds ahead
   ffmpeg -itsoffset 1.5 -i video.mov -i audio.mp3 \
          -c:v libx264 -c:a aac output.mp4 -y
   ```

4. **Re-record with corrected timing**: Fix beat sheet, regenerate automation

### Video Quality Poor

**Problem**: Final video looks blurry or pixelated

**Solutions**:

1. **Increase recording resolution**:
   ```json
   {"recording": {"resolution": "1920x1080"}}
   ```

2. **Lower CRF** (higher quality):
   ```json
   {"encoding": {"crf": 20}}  // was 22
   ```

3. **Use slower preset** (better compression):
   ```json
   {"encoding": {"preset": "slow"}}  // was medium
   ```

4. **Check source recording**: Ensure original recording is high quality

### File Size Too Large

**Problem**: Final video is hundreds of MB or GB

**Solutions**:

1. **Increase CRF** (lower quality, smaller file):
   ```json
   {"encoding": {"crf": 26}}  // was 22
   ```

2. **Use faster preset**:
   ```json
   {"encoding": {"preset": "medium"}}  // was slow
   ```

3. **Reduce resolution**:
   ```json
   {"recording": {"resolution": "1280x720"}}  // was 1920x1080
   ```

4. **Lower framerate**:
   ```json
   {"recording": {"framerate": 30}}  // was 60
   ```

5. **Two-pass encoding** (better compression):
   ```bash
   # Pass 1
   ffmpeg -i input.mov -c:v libx264 -preset slow -crf 22 \
          -pass 1 -f null /dev/null

   # Pass 2
   ffmpeg -i input.mov -i audio.mp3 \
          -c:v libx264 -preset slow -crf 22 -pass 2 \
          -c:a aac -b:a 192k output.mp4 -y
   ```

### No Audio in Final Video

**Problem**: Video plays but has no sound

**Solutions**:

1. **Check audio file exists**:
   ```bash
   ls -lh audio/[topic]/narration.mp3
   ```

2. **Test audio file**:
   ```bash
   ffplay audio/[topic]/narration.mp3
   ```

3. **Verify audio stream in output**:
   ```bash
   ffprobe output/[topic]-final.mp4
   ```

4. **Force audio stream**:
   ```bash
   ffmpeg -i video.mov -i audio.mp3 \
          -c:v copy -c:a aac \
          -map 0:v:0 -map 1:a:0 \
          output.mp4 -y
   ```

### FFmpeg Encoding Very Slow

**Problem**: Merge takes 10+ minutes for 5-minute video

**Solutions**:

1. **Use faster preset**:
   ```json
   {"encoding": {"preset": "fast"}}  // was slow
   ```

2. **Hardware acceleration**:
   ```bash
   ffmpeg -hwaccel auto -i video.mov -i audio.mp3 \
          -c:v h264_videotoolbox -c:a aac output.mp4 -y
   ```

3. **Lower resolution during encoding**:
   ```bash
   ffmpeg -i video.mov -i audio.mp3 \
          -vf "scale=1280:720" \
          -c:v libx264 -preset medium -crf 24 \
          -c:a aac output.mp4 -y
   ```

## Beat Sheet Issues

### Beat Sheet Generation Fails

**Problem**: `/video-script` doesn't create beat sheet

**Solutions**:

1. **Check project has documentation**:
   ```bash
   ls -la README.md
   ls -la docs/
   ```

2. **Verify output directory**:
   ```bash
   mkdir -p scripts/video-scripts
   ```

3. **Check for errors**: Review Claude Code output for specific errors

4. **Try simpler topic**: Start with "installation" or "getting-started"

### Timing Doesn't Add Up

**Problem**: Beat durations don't match target video length

**Solution**:

1. **Calculate total**:
   ```bash
   # In beat sheet, sum all beat durations
   # Should equal target duration ± 10%
   ```

2. **Adjust individual beats**:
   - Increase intro/conclusion if too short
   - Break long beats into multiple shorter ones
   - Remove unnecessary beats if too long

3. **Read aloud**: Time narration by reading out loud

### Commands Don't Work

**Problem**: Terminal commands in beat sheet fail when executed

**Solutions**:

1. **Test in clean environment**:
   ```bash
   # New terminal window, clean state
   cd /tmp
   mkdir test-video-commands
   cd test-video-commands
   # Test each command
   ```

2. **Check prerequisites**:
   - Required software installed?
   - Correct working directory?
   - Environment variables set?

3. **Use absolute paths**:
   ```bash
   # Instead of
   cd my-project

   # Use
   cd ~/Projects/my-project
   ```

## Platform-Specific Issues

### macOS: Automation Permission Denied

**Problem**: "Operation not permitted" when running automation

**Solution**:

Grant automation permissions:
1. **System Preferences** → **Security & Privacy**
2. **Privacy** tab → **Automation**
3. Enable:
   - **iTerm2** → **System Events**
   - **Script Editor** → **System Events**
4. Restart affected applications

### macOS: say Command Not Working

**Problem**: `say` command fails or has no output

**Solutions**:

1. **Test say command**:
   ```bash
   say "Hello world"
   ```

2. **List available voices**:
   ```bash
   say -v '?'
   ```

3. **Check audio output**:
   - Ensure speakers/headphones connected
   - Check system volume
   - Test with other audio apps

4. **Install voices** (if missing):
   - **System Preferences** → **Accessibility**
   - **Spoken Content** → **System Voice**
   - Download additional voices

### Linux: Terminal Automation Alternatives

**Problem**: No iTerm2 on Linux, AppleScript doesn't work

**Solutions**:

1. **Use xdotool**:
   ```bash
   sudo apt-get install xdotool

   # Type command
   xdotool type "npm install"
   xdotool key Return

   # Wait
   sleep 5
   ```

2. **Use tmux with scripting**:
   ```bash
   tmux new-session -d -s recording
   tmux send-keys -t recording "cd ~/Projects" C-m
   sleep 2
   tmux send-keys -t recording "npm install" C-m
   ```

3. **Record manually**: Type commands yourself, no automation

### Windows: Automation Challenges

**Problem**: Windows doesn't have AppleScript or Unix tools

**Solutions**:

1. **Use PowerShell**:
   ```powershell
   # Type commands programmatically
   $wshell = New-Object -ComObject wscript.shell
   $wshell.SendKeys("npm install{ENTER}")
   Start-Sleep -Seconds 5
   ```

2. **Use AutoHotkey**:
   ```autohotkey
   Send npm install{Enter}
   Sleep 5000
   ```

3. **WSL for Unix tools**: Run automation in Windows Subsystem for Linux

## Getting Help

If you're still stuck after trying these solutions:

### 1. Check Documentation

- [Installation Guide](../installation.md)
- [Quick Start](../quick-start.md)
- [Command Reference](../commands/overview.md)
- [Workflow Guide](workflow.md)

### 2. Search GitHub Issues

Visit [GitHub Issues](https://github.com/thejimbirch/training-video-generator/issues) and search for your problem.

### 3. Create New Issue

If your problem isn't documented:

1. Go to [GitHub Issues](https://github.com/thejimbirch/training-video-generator/issues/new)
2. Include:
   - Operating system and version
   - Plugin version
   - Exact error message
   - Steps to reproduce
   - What you've tried

### 4. Enable Debug Mode

Get more detailed error information:

```bash
export TVG_DEBUG=1
export TVG_FFMPEG_VERBOSE=1

# Re-run failing command
/video-merge my-topic
```

Share debug output in your issue report.

## Common Error Messages

### "Beat sheet not found"

**Meaning**: `/video-automate` or `/video-narrate` can't find beat sheet

**Solution**:
```bash
# Check file exists
ls scripts/video-scripts/[topic]-beat-sheet.md

# Generate if missing
/video-script [topic]
```

### "Recording file not found"

**Meaning**: `/video-merge` can't find screen recording

**Solution**:
```bash
# Check file exists
ls recordings/[topic].mov

# Check for different extension
ls recordings/[topic].*

# Move file if named differently
mv recordings/my-video.mov recordings/[topic].mov
```

### "Invalid JSON configuration"

**Meaning**: `.training-video-generator/config.json` has syntax error

**Solution**:
```bash
# Validate JSON
cat .training-video-generator/config.json | jq

# If jq not installed
python3 -m json.tool .training-video-generator/config.json
```

### "Voice ID not found"

**Meaning**: ElevenLabs voice ID doesn't exist

**Solution**:
- Visit [ElevenLabs Voices](https://elevenlabs.io/voices)
- Copy correct voice ID
- Update config.json

## Prevention Tips

1. **Test in isolation**: Try commands in clean environment first
2. **Start simple**: Begin with basic videos before advanced features
3. **Save configs**: Commit working configuration to git
4. **Document changes**: Note what you customized and why
5. **Regular backups**: Keep copies of working beat sheets
6. **Version control**: Track all scripts and configs in git

## Related Resources

- [Workflow Guide](workflow.md) - Complete production process
- [Customization Guide](customization.md) - Configuration options
- [Beat Sheets Guide](beat-sheets.md) - Writing better scripts
- [Command Reference](../commands/overview.md) - All commands
