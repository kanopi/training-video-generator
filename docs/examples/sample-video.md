# Example: Installation Video

This is a complete example of a training video beat sheet for an installation tutorial.

## Video Overview

**Topic**: Installing MyProject
**Duration**: 5 minutes
**Target Audience**: Beginner
**Prerequisites**: macOS, Linux, or Windows computer with terminal access

This example demonstrates:
- Clear beat structure
- Natural narration style
- Realistic command sequences
- Proper timing estimates
- Visual notes for production
- Post-production guidance

## The Complete Beat Sheet

For the full beat sheet, see: [`examples/sample-beat-sheet.md`](https://github.com/kanopi/training-video-generator/blob/main/examples/sample-beat-sheet.md) in the repository.

## Beat Breakdown Analysis

Let's analyze each beat to understand the structure:

### Beat 1: Introduction (15 seconds)

```markdown
## Beat 1: Introduction
**Duration**: 15 seconds
**Visual**: Terminal - Clean iTerm2 window
**Browser Tab**: N/A

**Narration**:
"Welcome to MyProject! In this video, we'll walk through the complete
installation and setup process. By the end, you'll have MyProject up
and running on your machine. Let's get started!"
```

**Why it works**:
- Short and welcoming (15 seconds)
- Clear outcome ("up and running")
- Sets expectations ("complete installation and setup")
- Friendly, conversational tone
- No commands in intro (keeps it simple)

### Beat 2: Check Prerequisites (25 seconds)

```markdown
## Beat 2: Check Prerequisites
**Duration**: 25 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"First, let's verify you have the required prerequisites. You'll need
Node.js version 18 or higher, and npm version 9 or higher. Let's check
what you have installed."

**Terminal Commands**:
```bash
node --version
npm --version
```

**Visual Notes**:
- Show version output clearly
- Highlight the version numbers
- Pause on output for 2 seconds
```

**Why it works**:
- Explains "why" (checking prerequisites)
- States requirements clearly (Node 18+, npm 9+)
- Commands are simple and safe
- Visual notes ensure viewers see important info
- Timing allows for command execution + comprehension

### Beat 4: Install MyProject (45 seconds)

```markdown
## Beat 4: Install MyProject
**Duration**: 45 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"Now comes the main installation. We'll use npm to install MyProject
globally, which makes it available anywhere on your system. This might
take about 30 seconds, so I'll speed up this part in the video."

**Terminal Commands**:
```bash
npm install -g myproject
```

**Visual Notes**:
- Show npm install command
- Display progress bar and download activity
- Show completion message
- **Post-production**: Speed up this section 2x
```

**Why it works**:
- Explains the command ("install globally")
- Provides context ("available anywhere")
- Sets time expectation ("30 seconds")
- Acknowledges it's boring ("I'll speed up")
- Post-production note ensures video stays engaging
- Longer duration accounts for install time

### Beat 7: Start Development Server (35 seconds)

```markdown
## Beat 7: Start Development Server
**Duration**: 35 seconds
**Visual**: Terminal + Browser (split screen or switch)
**Browser Tab**: http://localhost:3000

**Narration**:
"Excellent! Now let's start the development server. This will launch
your project locally on port 3000. Once it's running, we'll open it in
a browser to see our project live."

**Terminal Commands**:
```bash
myproject serve
```

**Browser Actions**:
- Wait 5 seconds for server to start
- Navigate to http://localhost:3000
- Show the running application

**Visual Notes**:
- Show server starting messages
- Switch to browser when server is ready
- Show the welcome page
- Highlight key UI elements
```

**Why it works**:
- Transitions from terminal to browser
- Explains what will happen ("launch locally on port 3000")
- Browser actions are detailed ("wait 5 seconds")
- Visual notes guide the production
- Duration accounts for server startup + browser demo

### Beat 9: Conclusion (20 seconds)

```markdown
## Beat 9: Stop Server and Conclusion
**Duration**: 20 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"To stop the server, simply press Control+C in your terminal. Great job!
You've successfully installed MyProject, initialized a new project, and
verified everything works. Check out the next video where we'll explore
the core features. Thanks for watching!"

**Terminal Commands**:
```bash
# Press Ctrl+C to stop server
```

**Visual Notes**:
- Show Ctrl+C stopping the server
- Return to clean terminal prompt
- End on a positive, encouraging note
```

**Why it works**:
- Practical tip (how to stop server)
- Celebrates accomplishment ("Great job!")
- Recaps what was covered
- Previews next video (keeps engagement)
- Ends positively ("Thanks for watching!")
- Clean ending visually

## Production Flow

### 1. Script Generation

```bash
cd ~/Projects/myproject
/video-topics
# Review suggested topics
/video-script installation-and-setup
# Review and edit: scripts/video-scripts/installation-and-setup-beat-sheet.md
```

### 2. Automation Setup

```bash
/video-automate installation-and-setup
# Test: osascript scripts/automation/installation-and-setup-automate.scpt
# Adjust timing if needed
```

### 3. Audio Creation

```bash
# Ensure TTS configured
export ELEVENLABS_API_KEY="your_key"

/video-narrate installation-and-setup
# Listen: open audio/installation-and-setup/narration.mp3
```

### 4. Recording

```bash
# Start recording (Cmd+Shift+5 on macOS)
# Select terminal window
# Click Record
# Wait 3 seconds

# Run automation
osascript scripts/automation/installation-and-setup-automate.scpt

# Stop recording when complete
# Save as: recordings/installation-and-setup.mov
```

### 5. Merge

```bash
/video-merge installation-and-setup
# Wait for processing
# Review: output/installation-and-setup-final.mp4
```

## Timing Breakdown

| Beat | Duration | Cumulative | Purpose |
|------|----------|------------|---------|
| 1. Introduction | 15s | 0:15 | Welcome, set expectations |
| 2. Check Prerequisites | 25s | 0:40 | Verify environment |
| 3. Create Directory | 20s | 1:00 | Setup workspace |
| 4. Install MyProject | 45s | 1:45 | Main installation |
| 5. Verify Installation | 20s | 2:05 | Confirm success |
| 6. Initialize Project | 30s | 2:35 | Create new project |
| 7. Start Dev Server | 35s | 3:10 | Launch application |
| 8. Verify in Browser | 25s | 3:35 | Show running app |
| 9. Conclusion | 20s | 3:55 | Recap, next steps |
| **Buffer** | +65s | **5:00** | **Target duration** |

**Note**: 3:55 of scripted beats + 65s buffer = 5:00 target (13% buffer)

## Key Takeaways

### What Makes This Beat Sheet Effective

1. **Clear Structure**
   - Logical flow from prerequisites → installation → verification
   - Each beat has a single clear purpose
   - Natural progression

2. **Conversational Narration**
   - Sounds like a friendly teacher, not a manual
   - Explains "why" not just "what"
   - Sets expectations and provides context

3. **Realistic Timing**
   - Commands have time to execute
   - Viewers have time to read output
   - Boring parts are noted for speed-up

4. **Production Guidance**
   - Visual notes for recording
   - Post-production notes for editing
   - Specific browser actions
   - Highlighting instructions

5. **Safe, Tested Commands**
   - All commands actually work
   - No destructive operations
   - Realistic examples (not foo/bar)
   - Clear working directory

6. **Good Pacing**
   - Not too fast (viewers can follow)
   - Not too slow (stays engaging)
   - Acknowledges boring parts
   - Buffer time for flexibility

## Customization Ideas

### For Different Projects

**API Documentation Video**:
- More browser action beats
- Show Postman or curl examples
- Include API response examples

**CLI Tool Video**:
- More terminal command beats
- Show various command options
- Include troubleshooting beat

**Web App Video**:
- Balance terminal and browser
- Show UI interactions
- Include feature walkthrough beats

### For Different Audiences

**Complete Beginners**:
- Longer beats with more explanation
- More verification beats
- Slower pace overall
- More encouragement

**Advanced Users**:
- Faster pace
- Fewer explanation beats
- More advanced features
- Less hand-holding

### For Different Lengths

**2-3 Minute Quick Start**:
- Fewer beats (5-6 total)
- Faster pace
- Skip optional steps
- Focus on essentials

**10-15 Minute Deep Dive**:
- More beats (12-15 total)
- Include troubleshooting
- Show advanced options
- Multiple examples

## Related Examples

- [Beat Sheet Writing Guide](../guides/beat-sheets.md) - How to write great scripts
- [Workflow Guide](../guides/workflow.md) - Complete production process
- [Command Reference](../commands/overview.md) - All available commands

## Try It Yourself

Use this example as a template:

1. **Copy the structure**: 9-beat format works well for installations
2. **Adapt narration**: Write in your own voice, for your project
3. **Test commands**: Verify everything works in clean environment
4. **Adjust timing**: Read narration aloud to estimate duration
5. **Add visual notes**: Think about what viewers need to see
6. **Generate and iterate**: Use plugin commands, then refine

Good luck with your training videos!
