# Training Video Generator

Welcome to **Training Video Generator** - the Claude Code plugin that automates professional training video creation from your project documentation.

---

## What is Training Video Generator?

Training Video Generator transforms your project documentation into polished training videos using AI and automation. With 5 powerful slash commands, you can:

1. 🤖 **Generate AI-powered scripts** - Beat-by-beat video scripts from documentation
2. 🎬 **Automate screen recordings** - Terminal commands execute automatically
3. 🗣️ **Create TTS narration** - Professional voice-over with multiple providers
4. 🎥 **Merge into final videos** - Professional MP4s ready to publish
5. 🔄 **Reuse across projects** - Works with any project documentation

---

## Key Features

### 🤖 AI-Generated Scripts

Generate professional beat-by-beat video scripts that include:

- Word-for-word narration text
- Exact terminal commands to execute
- Browser navigation steps
- Visual cues and camera positioning
- Realistic timing estimates

### 🎬 Automated Recording

Create automation scripts that:

- Execute terminal commands automatically via iTerm2
- Navigate browser tabs and URLs
- Control screen recording start/stop
- Handle timing and transitions
- Run without manual intervention

### 🗣️ Text-to-Speech Integration

Generate professional narration with:

- **ElevenLabs** - Premium quality, natural voices
- **OpenAI TTS** - High quality, easy integration
- **macOS `say`** - Free, built-in fallback
- Configurable voices and settings

### 🎥 Professional Video Production

Merge recordings with audio:

- FFmpeg-based processing
- Professional encoding (h264/aac)
- Intro/outro branding support
- Optimized for web playback

### 🔄 Project-Agnostic Design

Works with any project:

- Analyzes documentation automatically
- Adapts to project structure
- No hardcoded names or paths
- Fully reusable templates

---

## Quick Start

Get started in minutes:

```bash
# 1. Install the plugin
claude plugins install https://github.com/kanopi/training-video-generator

# 2. Analyze your project
/video-topics

# 3. Generate a script
/video-script "Getting Started"

# 4. Create your first video!
```

See the [Quick Start Guide](quick-start.md) for a complete walkthrough.

---

## Commands Overview

| Command | Purpose |
|---------|---------|
| [`/video-topics`](commands/video-topics.md) | Analyze project and suggest video topics |
| [`/video-script`](commands/video-script.md) | Generate beat-by-beat video script |
| [`/video-automate`](commands/video-automate.md) | Create automation scripts from beat sheet |
| [`/video-narrate`](commands/video-narrate.md) | Generate TTS audio narration |
| [`/video-merge`](commands/video-merge.md) | Merge video recording with audio |

[View Complete Command Reference →](commands/overview.md)

---

## Use Cases

### Open Source Projects
Create tutorial videos for contributors showing:
- Installation and setup
- Key features and workflows
- API usage examples
- Contributing guidelines

### Product Documentation
Generate demo videos demonstrating:
- Feature walkthroughs
- Configuration options
- Integration examples
- Troubleshooting steps

### Internal Tools
Build training videos for teams covering:
- Onboarding new developers
- Tool usage and best practices
- Deployment procedures
- Troubleshooting guides

### Educational Content
Produce educational videos for:
- Workshops and courses
- Conference talks
- Tutorial series
- Code walkthroughs

---

## How It Works

### 1. Analyze Documentation
```bash
/video-topics
```

The plugin analyzes your project's:
- README.md
- Documentation files
- API docs
- Package files

Then suggests relevant video topics with estimated durations.

### 2. Generate Beat Sheet
```bash
/video-script "Your Topic"
```

Creates a screenplay-style beat sheet with:
- Introduction beat
- Step-by-step instructions
- Terminal commands
- Browser actions
- Conclusion beat

### 3. Automate Recording
```bash
/video-automate scripts/video-scripts/your-topic-beat-sheet.md
```

Generates:
- AppleScript for iTerm2 automation
- Bash orchestration scripts
- Browser automation
- Recording control

### 4. Generate Narration
```bash
/video-narrate scripts/video-scripts/your-topic-beat-sheet.md
```

Creates TTS audio:
- Individual clips per beat
- Master audio file
- Proper timing synchronization

### 5. Merge Final Video
```bash
/video-merge your-topic
```

Produces final MP4:
- Synced video and audio
- Professional encoding
- Ready to publish

---

## Example Output

### Beat Sheet (Markdown)
```markdown
## Beat 1: Introduction
**Duration**: 10 seconds
**Visual**: Terminal - iTerm2
**Narration**: "Welcome to ProjectName..."
**Terminal Commands**:
\`\`\`bash
cd ~/Projects/example
\`\`\`
**Browser Actions**: Navigate to localhost:3000
```

### Automation Script (AppleScript)
```applescript
tell application "iTerm2"
    create window with default profile
    tell current session of current window
        write text "cd ~/Projects/example"
        delay 2
    end tell
end tell
```

### Final Video
- **Format**: MP4 (h264 video, aac audio)
- **Quality**: 1080p, 30fps
- **Duration**: 3-10 minutes (typical)
- **Size**: ~50-100MB (typical)

---

## Requirements

### Required
- Claude Code CLI
- Git
- FFmpeg

### Optional
- iTerm2 (recommended for automation)
- ElevenLabs API key (premium TTS)
- OpenAI API key (high-quality TTS)
- ScreenFlow (advanced recording)

[View Complete Installation Guide →](installation.md)

---

## Get Started

1. **[Installation](installation.md)** - Set up the plugin and dependencies
2. **[Quick Start](quick-start.md)** - Create your first video
3. **[Commands](commands/overview.md)** - Learn all 5 commands
4. **[Guides](guides/workflow.md)** - Master the workflow

---

## Support & Contributing

- **Issues**: [GitHub Issues](https://github.com/kanopi/training-video-generator/issues)
- **Source**: [GitHub Repository](https://github.com/kanopi/training-video-generator)
- **License**: GPL-2.0-or-later

---

**Ready to create amazing training videos?** [Get Started →](quick-start.md)
