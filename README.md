# Training Video Generator

![Maintained](https://img.shields.io/maintenance/yes/2025.svg)
[![Documentation](https://img.shields.io/badge/docs-mkdocs-blue.svg)](https://thejimbirch.github.io/training-video-generator/)

**Training Video Generator** is a Claude Code plugin that automates the creation of professional training videos from project documentation. Generate AI-powered scripts, automate screen recordings, create TTS narration, and merge everything into polished training videos for any project.

---

## 📚 Documentation

**Complete documentation is available at:** **[https://thejimbirch.github.io/training-video-generator/](https://thejimbirch.github.io/training-video-generator/)**

### Quick Links

| Resource | Description |
|----------|-------------|
| **[Installation](https://thejimbirch.github.io/training-video-generator/installation/)** | Get started in minutes |
| **[Quick Start](https://thejimbirch.github.io/training-video-generator/quick-start/)** | Your first video walkthrough |
| **[Commands](https://thejimbirch.github.io/training-video-generator/commands/overview/)** | Complete command reference (5 commands) |
| **[Guides](https://thejimbirch.github.io/training-video-generator/guides/workflow/)** | Workflows, beat sheets, customization |

---

## ✨ Features

- **🤖 AI-Generated Scripts** - Beat-by-beat video scripts from documentation
- **🎬 Automated Recording** - Terminal command automation with iTerm2 + AppleScript
- **🗣️ Text-to-Speech** - Multiple TTS providers (ElevenLabs, OpenAI, macOS)
- **🎥 Video Production** - FFmpeg merging with professional encoding
- **📋 Professional Format** - Screenplay-style beat sheets with timing
- **🔄 Project-Agnostic** - Works with any project documentation
- **⚙️ Fully Customizable** - Templates, branding, and configurations

---

## 🚀 Quick Install

**Recommended: Via Marketplace**
```bash
# Add the marketplace
claude plugins marketplace add thejimbirch-plugins https://github.com/thejimbirch/claude-plugins

# Install Training Video Generator
claude plugins install thejimbirch-plugins/training-video-generator
```

**Alternative: Direct Install**
```bash
claude plugins install https://github.com/thejimbirch/training-video-generator
```

**Manual Installation (Development)**
```bash
cd ~/.claude/plugins
git clone https://github.com/thejimbirch/training-video-generator.git
claude plugins enable training-video-generator
```

See [Installation Guide](https://thejimbirch.github.io/training-video-generator/installation/) for detailed setup including TTS API configuration.

---

## 💡 Quick Example

```bash
# 1. Analyze your project for video topics
/video-topics

# 2. Generate a beat-by-beat script
/video-script "Getting Started with Installation"

# 3. Generate automation scripts for recording
/video-automate scripts/video-scripts/installation-beat-sheet.md

# 4. Record video (run generated AppleScript)
# (Execute the generated automation script)

# 5. Generate TTS narration
/video-narrate scripts/video-scripts/installation-beat-sheet.md

# 6. Merge video + audio
/video-merge installation

# Output: output/installation-final.mp4
```

---

## 🎯 Commands Overview

| Command | Purpose |
|---------|---------|
| `/video-topics` | Analyze project and suggest video topics |
| `/video-script` | Generate beat-by-beat video script |
| `/video-automate` | Create automation scripts from beat sheet |
| `/video-narrate` | Generate TTS audio narration |
| `/video-merge` | Merge video recording with audio |

---

## 🛠 What Gets Generated

### Beat-by-Beat Script
```markdown
## Beat 1: Introduction
**Duration**: 10 seconds
**Visual**: Terminal - iTerm2
**Narration**: "Welcome to Project Name..."
**Terminal Commands**:
```bash
cd ~/Projects/example
```
**Browser Actions**: Navigate to localhost:3000
```

### Automation Scripts
- **AppleScript** for iTerm2 terminal automation
- **Bash scripts** for command orchestration
- **Browser automation** for Safari/Chrome
- **Recording control** scripts

### TTS Audio
- Individual audio clips per beat
- Master audio file with proper timing
- Support for multiple TTS providers

### Final Video
- Professional MP4 with h264 encoding
- Synced audio and video
- Optional intro/outro branding
- Optimized for web playback

---

## 📋 Requirements

### Required

- **Claude Code CLI** - To run the plugin commands
- **Git** - For version control
- **FFmpeg** - For video/audio processing
  - macOS: `brew install ffmpeg`
  - Linux: `sudo apt-get install ffmpeg`

### Optional

- **iTerm2** - For better terminal automation (macOS)
- **ElevenLabs API Key** - For premium TTS (recommended)
- **OpenAI API Key** - For OpenAI TTS
- **ScreenFlow** - For advanced screen recording features
- **Python 3.x & MkDocs** - For building/contributing to documentation

---

## 🎬 Use Cases

- **Open Source Projects** - Tutorial videos for contributors
- **Product Documentation** - Feature demo videos
- **API Documentation** - Code walkthrough videos
- **Internal Tools** - Team training videos
- **Workshops & Training** - Educational content
- **Client Deliverables** - Professional demo videos

---

## 🔧 TTS Providers

Training Video Generator supports multiple TTS providers:

### ElevenLabs (Recommended)
- **Quality**: Exceptional natural voices
- **Setup**: Requires API key
- **Cost**: Pay-per-use
- **Best for**: Professional videos

### OpenAI TTS
- **Quality**: Very good natural voices
- **Setup**: Requires API key
- **Cost**: Pay-per-use
- **Best for**: High-quality at scale

### macOS `say` Command
- **Quality**: Good built-in voices
- **Setup**: No configuration needed
- **Cost**: Free
- **Best for**: Testing and quick videos

---

## 📖 Learn More

Visit the **[complete documentation](https://thejimbirch.github.io/training-video-generator/)** for:

- Detailed command reference
- Step-by-step workflows
- Beat sheet writing guide
- Customization options
- Troubleshooting tips
- Example videos

---

## 🤝 Contributing

Contributions welcome! See [Contributing Guide](https://thejimbirch.github.io/training-video-generator/contributing/) for details.

---

## 📄 License

GPL-2.0-or-later - see [LICENSE.md](LICENSE.md) file for details.

---

## 💬 Support

- **Issues**: [GitHub Issues](https://github.com/thejimbirch/training-video-generator/issues)
- **Documentation**: [https://thejimbirch.github.io/training-video-generator/](https://thejimbirch.github.io/training-video-generator/)

---

**Created and maintained by [Jim Birch](https://thejimbirch.com)**
