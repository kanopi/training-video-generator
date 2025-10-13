# Installation

Training Video Generator can be installed globally for all projects or per-project for team collaboration.

---

## Prerequisites

Before installing Training Video Generator, ensure you have:

### Required

- **Claude Code CLI** installed and configured
- **Git** for version control
- **FFmpeg** for video/audio processing
  - macOS: `brew install ffmpeg`
  - Linux: `sudo apt-get install ffmpeg`
  - Windows: [Download from ffmpeg.org](https://ffmpeg.org/download.html)

### Optional

- **iTerm2** (macOS) - Better terminal automation than Terminal.app
- **ElevenLabs API Key** - For premium TTS (recommended)
- **OpenAI API Key** - For high-quality TTS
- **ScreenFlow** - For advanced screen recording features
- **Python 3.x & MkDocs** - For building/contributing to documentation

---

## Installation Methods

### Method 1: Via Marketplace (Recommended)

This is the easiest method and enables automatic updates. **Installs globally for all projects.**

#### Step 1: Add the Marketplace

```bash
claude plugins marketplace add thejimbirch-plugins https://github.com/thejimbirch/claude-plugins
```

#### Step 2: Install Training Video Generator

```bash
claude plugins install thejimbirch-plugins/training-video-generator
```

#### Step 3: Verify Installation

```bash
claude plugins list
```

You should see `training-video-generator` in the list of installed plugins.

#### Updating Via Marketplace

```bash
claude plugins update thejimbirch-plugins/training-video-generator
```

---

### Method 2: Direct from GitHub

Install directly without adding a marketplace. **Installs globally for all projects.**

```bash
claude plugins install https://github.com/thejimbirch/training-video-generator
```

#### Updating Direct Installation

```bash
claude plugins update training-video-generator
```

---

### Method 3: Manual Installation (Development)

For plugin development or testing local changes. **Installs globally for all projects.**

#### Step 1: Clone the Repository

```bash
cd ~/.claude/plugins
git clone https://github.com/thejimbirch/training-video-generator.git
```

!!! note "Plugin Directory Location"
    The plugins directory is typically `~/.claude/plugins/`. Some systems may use `~/.config/claude/plugins/`. Check your system:
    ```bash
    ls -la ~/.claude/plugins/ 2>/dev/null || ls -la ~/.config/claude/plugins/
    ```

#### Step 2: Enable the Plugin

```bash
claude plugins enable training-video-generator
```

#### Updating Manual Installation

```bash
cd ~/.claude/plugins/training-video-generator
git pull origin main
claude plugins reload training-video-generator
```

---

## TTS Provider Setup

Training Video Generator supports multiple text-to-speech providers. Configure at least one for narration generation.

### ElevenLabs (Recommended)

**Quality**: Exceptional natural voices
**Cost**: Pay-per-use, free tier available

1. Sign up at [elevenlabs.io](https://elevenlabs.io)
2. Get your API key from the dashboard
3. Set environment variable:

```bash
export ELEVENLABS_API_KEY="your-api-key-here"
```

Add to your shell profile (`~/.zshrc` or `~/.bashrc`):
```bash
echo 'export ELEVENLABS_API_KEY="your-api-key-here"' >> ~/.zshrc
source ~/.zshrc
```

### OpenAI TTS

**Quality**: Very good natural voices
**Cost**: Pay-per-use

1. Get API key from [platform.openai.com](https://platform.openai.com/api-keys)
2. Set environment variable:

```bash
export OPENAI_API_KEY="your-api-key-here"
```

Add to your shell profile:
```bash
echo 'export OPENAI_API_KEY="your-api-key-here"' >> ~/.zshrc
source ~/.zshrc
```

### macOS `say` Command

**Quality**: Good built-in voices
**Cost**: Free

No setup required! The macOS `say` command works out of the box as a fallback.

List available voices:
```bash
say -v ?
```

---

## Project Configuration

Create a configuration file in your project to customize video generation:

### Create `.training-video-generator/config.json`

In your project root:

```bash
mkdir -p .training-video-generator
```

Create `config.json`:

```json
{
  "tts": {
    "provider": "elevenlabs",
    "voice_id": "default",
    "api_key_env": "ELEVENLABS_API_KEY",
    "fallback": "macos-say"
  },
  "recording": {
    "screen_size": "1920x1080",
    "frame_rate": 30,
    "tool": "screenshot-app"
  },
  "output": {
    "video_codec": "h264",
    "audio_codec": "aac",
    "quality": "high"
  },
  "branding": {
    "intro_video": null,
    "outro_video": null
  }
}
```

### Configuration Options

#### TTS Settings

- **provider**: `"elevenlabs"`, `"openai"`, or `"macos-say"`
- **voice_id**: Voice identifier (provider-specific)
- **api_key_env**: Environment variable name for API key
- **fallback**: Fallback provider if primary fails

#### Recording Settings

- **screen_size**: `"1920x1080"`, `"1280x720"`, etc.
- **frame_rate**: `30`, `60` (fps)
- **tool**: `"screenshot-app"`, `"screenflow"`, `"quicktime"`

#### Output Settings

- **video_codec**: `"h264"`, `"h265"`, `"vp9"`
- **audio_codec**: `"aac"`, `"mp3"`
- **quality**: `"high"`, `"medium"`, `"low"`

#### Branding

- **intro_video**: Path to intro video file (optional)
- **outro_video**: Path to outro video file (optional)

---

## Verifying Installation

### Test a Command

Open Claude Code in any project and try:

```bash
/video-topics
```

You should see an analysis of your project with suggested video topics.

### List Available Commands

In Claude Code, type `/` to see all available commands. You should see:

- `/video-topics`
- `/video-script`
- `/video-automate`
- `/video-narrate`
- `/video-merge`

---

## Optional: iTerm2 Setup (macOS)

For better terminal automation, install iTerm2:

```bash
brew install --cask iterm2
```

Set iTerm2 as your default terminal in macOS System Settings.

Enable Python API in iTerm2:
1. Open iTerm2 > Preferences
2. Go to "General" > "Magic"
3. Enable "Python API"

---

## Optional: ScreenFlow Setup (macOS)

For advanced screen recording features:

1. Download from [screenflow.com](https://www.telestream.net/screenflow/)
2. Install and activate
3. Configure keyboard shortcuts for start/stop recording

---

## Troubleshooting

### Commands Not Showing Up

```bash
# Check plugin status
claude plugins list

# Verify plugin is enabled
claude plugins enable training-video-generator

# Reload plugin
claude plugins reload training-video-generator
```

### FFmpeg Not Found

Verify FFmpeg is installed:

```bash
ffmpeg -version
```

If not found:

=== "macOS"

    ```bash
    brew install ffmpeg
    ```

=== "Linux"

    ```bash
    sudo apt-get install ffmpeg
    ```

=== "Windows"

    Download from [ffmpeg.org](https://ffmpeg.org/download.html) and add to PATH

### TTS API Errors

Check environment variables:

```bash
# ElevenLabs
echo $ELEVENLABS_API_KEY

# OpenAI
echo $OPENAI_API_KEY
```

If empty, add to shell profile:

```bash
export ELEVENLABS_API_KEY="your-key"
export OPENAI_API_KEY="your-key"
```

### Permission Denied

```bash
# Ensure the plugins directory exists
mkdir -p ~/.claude/plugins

# Check ownership
ls -la ~/.claude/plugins/

# Fix permissions if needed
chmod -R 755 ~/.claude/plugins/training-video-generator
```

### Plugin Not Loading

```bash
# Check for errors in plugin.json
cat ~/.claude/plugins/training-video-generator/.claude-plugin/plugin.json

# Verify directory structure
ls ~/.claude/plugins/training-video-generator/commands/

# Check plugin integrity
cd ~/.claude/plugins/training-video-generator
git status
```

---

## Uninstalling

### Remove from Marketplace

```bash
claude plugins uninstall thejimbirch-plugins/training-video-generator
```

### Remove Manual Installation

```bash
claude plugins disable training-video-generator
rm -rf ~/.claude/plugins/training-video-generator
```

### Remove Project Configuration

```bash
rm -rf .training-video-generator
```

---

## Next Steps

- **[Quick Start Guide](quick-start.md)** - Create your first video
- **[Commands Overview](commands/overview.md)** - Learn all 5 commands
- **[Workflow Guide](guides/workflow.md)** - Master the complete workflow
- **[Customization Guide](guides/customization.md)** - Adapt to your needs

---

**Installation Support:**
- **Issues**: [GitHub Issues](https://github.com/thejimbirch/training-video-generator/issues)
- **Repository**: [GitHub](https://github.com/thejimbirch/training-video-generator)
