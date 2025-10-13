# Writing Effective Beat Sheets

Beat sheets are the foundation of great training videos. This guide teaches you how to write compelling, clear, and professional scripts.

## What is a Beat Sheet?

A **beat sheet** is a detailed script that breaks down your video into discrete segments called "beats." Each beat represents a single concept, action, or teaching moment.

Think of it like a screenplay for your training video.

### Beat Sheet Structure

```markdown
# Video: [Title]
**Duration**: [X] minutes
**Target Audience**: [Beginner/Intermediate/Advanced]
**Prerequisites**: [What viewers need to know]

---

## Beat 1: [Name]
**Duration**: [X] seconds
**Visual**: [Terminal/Browser/Split]
**Browser Tab**: [URL or N/A]

**Narration**:
"[What you'll say]"

**Terminal Commands**:
```bash
# Commands to execute
```

**Browser Actions**:
- [What to do in browser]

**Visual Notes**:
- [Highlighting, pauses, speed adjustments]
```

## Beat Anatomy

### Beat Header

```markdown
## Beat 3: Create Project Directory
**Duration**: 20 seconds
```

**Purpose**: Identifies the beat and sets timing expectations

**Guidelines**:
- Use descriptive, action-oriented names
- Keep duration realistic (15-60 seconds typical)
- Sum of all beats should match target video length

### Visual Specification

```markdown
**Visual**: Terminal
**Browser Tab**: N/A
```

**Purpose**: Defines what's shown on screen

**Options**:
- `Terminal` - Command line only
- `Browser` - Web browser only
- `Split` - Both terminal and browser
- `Terminal + Browser (switch)` - Alternate between them

### Narration Text

```markdown
**Narration**:
"Great! Now let's create a directory for our project. We'll create a folder
called my-project in your Projects directory and navigate into it."
```

**Purpose**: Exact words spoken in the video (or sent to TTS)

**Guidelines**:
- Write conversationally, as if teaching a friend
- Read aloud to check natural flow
- Include "why" context, not just "what" steps
- Match speaking duration to beat duration
- Use punctuation for natural pauses

### Terminal Commands

```markdown
**Terminal Commands**:
```bash
cd ~/Projects
mkdir my-project
cd my-project
```
```

**Purpose**: Exact commands to execute (automated or manual)

**Guidelines**:
- Use working, tested commands
- Include only necessary commands
- Use realistic examples (avoid `foo`, `bar`)
- Add comments for complex commands
- Ensure commands are safe (no destructive operations)

### Browser Actions

```markdown
**Browser Actions**:
- Navigate to http://localhost:3000
- Wait for page to load (5 seconds)
- Click "Getting Started" button
- Scroll down to show features
```

**Purpose**: Specific actions to perform in web browser

**Guidelines**:
- Be explicit about every action
- Include wait times for page loads
- Note what to click, hover, or scroll to
- Describe expected results

### Visual Notes

```markdown
**Visual Notes**:
- Show version output clearly
- Highlight the version numbers
- Pause on output for 2 seconds
- Speed up in post-production (2x)
```

**Purpose**: Guidance for recording and editing

**Types**:
- **Highlighting**: Draw attention to important parts
- **Pauses**: Give viewers time to read
- **Speed adjustments**: Fast-forward boring parts
- **Scene transitions**: Smooth switches between views

## Writing Great Narration

### Principle 1: Be Conversational

❌ **Bad** (Too formal):
> "The subsequent step requires the execution of the installation command."

✅ **Good** (Conversational):
> "Great! Now let's install the package. This will take about 30 seconds."

### Principle 2: Explain Why

❌ **Bad** (Just what):
> "Now run npm install dash g my-project."

✅ **Good** (Why + what):
> "We'll use npm to install My Project globally, which makes it available from anywhere on your system."

### Principle 3: Set Expectations

❌ **Bad** (No context):
> "Run the server."

✅ **Good** (With context):
> "Now let's start the development server. This will launch your project locally on port 3000, and we'll see it running in just a moment."

### Principle 4: Provide Context

❌ **Bad** (Assuming knowledge):
> "Check your Node version."

✅ **Good** (Explaining why):
> "First, let's verify you have Node.js version 18 or higher, which My Project requires to run."

### Principle 5: Use Transitions

❌ **Bad** (Abrupt):
> Beat 3: "Install the package."
> Beat 4: "Run the server."

✅ **Good** (Smooth):
> Beat 3: "...and the installation is complete!"
> Beat 4: "Perfect! Now that it's installed, let's start the development server."

### Principle 6: Match Timing

Narration should fill the beat duration naturally.

**20-second beat**:
> "Now let's create a directory for our project. [3s]
> We'll make a folder called my-project in your Projects directory [5s]
> and navigate into it. [2s]
> [Commands execute: 7s]
> Perfect, we're now in our new project directory. [3s]"

**Estimate**: ~140-160 words per minute for natural speech

## Timing Guidelines

### Beat Duration Ranges

- **Introduction**: 10-20 seconds
- **Simple command**: 15-30 seconds
- **Complex command**: 30-60 seconds
- **Installation/compilation**: 30-90 seconds (speed up in editing)
- **Browser interaction**: 20-40 seconds
- **Conclusion**: 15-30 seconds

### Total Video Length

- **Quick tip**: 2-3 minutes
- **Feature overview**: 5-8 minutes
- **Complete tutorial**: 10-15 minutes
- **Deep dive**: 15-25 minutes

### Buffer Time

Always add 10-15% buffer:
- Planning: 5 minutes → 5.5 minutes of beats
- Allows for natural pauses
- Accounts for unexpected delays
- Room for slight timing variations

## Command Writing Best Practices

### 1. Test Everything

```bash
# Bad - untested, might fail
npm install -g myproject

# Good - tested in clean environment
npm install -g myproject
# ✓ Verified on macOS, Linux, Windows
# ✓ Works with npm 9+
```

### 2. Use Real Examples

```bash
# Bad - placeholder names
cd /path/to/your/project

# Good - realistic path
cd ~/Projects/my-awesome-project
```

### 3. Show Output

```bash
# Bad - no context for output
node --version

# Good - explain what to expect
node --version
# Output: v18.17.0 (or higher)
```

### 4. Handle Prerequisites

```bash
# Bad - assumes directory exists
cd ~/Projects/myproject

# Good - creates if needed
mkdir -p ~/Projects/myproject
cd ~/Projects/myproject
```

### 5. Be Safe

```bash
# Bad - destructive without warning
rm -rf node_modules

# Good - clear intent and safe
# Clean install by removing node_modules
rm -rf node_modules
npm install
```

## Visual Notes Best Practices

### Highlighting

```markdown
**Visual Notes**:
- Highlight version number in output (yellow circle)
- Draw attention to success message (green checkmark)
- Point out new directory in file tree
```

### Pauses

```markdown
**Visual Notes**:
- Pause on command output for 3 seconds
- Give viewers time to read error message
- Hold on final result before moving on
```

### Speed Adjustments

```markdown
**Visual Notes**:
- Speed up npm install to 2x (takes 30 seconds real-time)
- Fast-forward compilation (boring to watch)
- Return to normal speed when complete
```

### Scene Transitions

```markdown
**Visual Notes**:
- Smooth fade from terminal to browser
- Use wipe transition when switching contexts
- Maintain consistency throughout video
```

## Common Beat Patterns

### Introduction Beat

```markdown
## Beat 1: Introduction
**Duration**: 15 seconds
**Visual**: Terminal - Clean iTerm2 window
**Browser Tab**: N/A

**Narration**:
"Welcome to [Project Name]! In this video, we'll [objective].
By the end, you'll [outcome]. Let's get started!"

**Terminal Commands**:
```bash
# No commands in intro
```

**Visual Notes**:
- Show clean terminal
- Display project logo/name
- Keep it simple and welcoming
```

### Command Execution Beat

```markdown
## Beat 3: Install Dependencies
**Duration**: 45 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"Now let's install our dependencies. We'll run npm install,
which will download all required packages. This takes about
30 seconds, so I'll speed this up in the video."

**Terminal Commands**:
```bash
npm install
```

**Visual Notes**:
- Show npm install progress
- Speed up to 2x in post-production
- Highlight completion message
```

### Browser Interaction Beat

```markdown
## Beat 7: View Running Application
**Duration**: 30 seconds
**Visual**: Browser
**Browser Tab**: http://localhost:3000

**Narration**:
"Let's open a browser and navigate to localhost port 3000.
You should see the welcome page load. Notice the navigation
menu at the top and the getting started guide in the center."

**Browser Actions**:
- Navigate to http://localhost:3000
- Wait for page to load (5 seconds)
- Scroll down slowly to show content
- Hover over navigation items

**Visual Notes**:
- Highlight key UI elements
- Pause to let viewers read
- Smooth scrolling, not jarring
```

### Verification Beat

```markdown
## Beat 5: Verify Installation
**Duration**: 20 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"Perfect! Let's verify the installation was successful by
checking the version. If you see a version number, you're all set!"

**Terminal Commands**:
```bash
myproject --version
```

**Visual Notes**:
- Show version output clearly
- Highlight the version number
- Pause for 2 seconds on output
```

### Conclusion Beat

```markdown
## Beat 9: Conclusion
**Duration**: 20 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"Great job! You've successfully [achievement]. You're now ready to
[next steps]. Check out the next video where we'll [preview].
Thanks for watching!"

**Terminal Commands**:
```bash
# No commands in conclusion
```

**Visual Notes**:
- Return to clean terminal
- Show final success state
- End on positive, encouraging note
```

## Post-Production Notes

Include guidance for video editing:

```markdown
## Post-Production Notes

**Editing**:
- Speed up Beat 4 (npm install) to 2x speed
- Add smooth transitions between terminal and browser
- Trim any long pauses (>3 seconds)

**B-Roll Suggestions**:
- Project logo during introduction (2 seconds)
- Architecture diagram during explanation (5 seconds)
- Feature highlights during conclusion (3 seconds)

**Music** (optional):
- Light, upbeat background music at 10% volume
- Only during intro and outro
- No music during technical steps (distracting)

**Captions/Subtitles**:
- Add subtitles for all narration
- Use monospace font for terminal commands
- Include URLs and version numbers in captions
```

## Examples

### Complete Beat Sheet Example

See: [Sample Beat Sheet](../examples/sample-video.md) - Full 9-beat installation video

### Beat Sheet Templates

#### Quick Tip Video (2-3 minutes)

```markdown
# Video: [Tip Title]
**Duration**: 2-3 minutes
**Target Audience**: [Level]
**Prerequisites**: [Requirements]

## Beat 1: Introduction (10 seconds)
## Beat 2: Setup (20 seconds)
## Beat 3: Main Tip (60 seconds)
## Beat 4: Example (40 seconds)
## Beat 5: Conclusion (10 seconds)
```

#### Feature Tutorial (5-8 minutes)

```markdown
# Video: [Feature Name]
**Duration**: 5-8 minutes
**Target Audience**: [Level]
**Prerequisites**: [Requirements]

## Beat 1: Introduction (15 seconds)
## Beat 2: Overview (30 seconds)
## Beat 3: Setup (45 seconds)
## Beat 4: Basic Usage (60 seconds)
## Beat 5: Advanced Options (60 seconds)
## Beat 6: Real Example (90 seconds)
## Beat 7: Conclusion (20 seconds)
```

## Tips for Success

1. **Start Simple**: First video should be beginner-level installation
2. **Read Aloud**: Always read narration aloud before recording
3. **Test Commands**: Run every command in a clean environment
4. **Be Realistic**: Don't underestimate beat durations
5. **Add Buffer**: Include 10-15% extra time
6. **Think Visual**: Consider what viewers see, not just hear
7. **Natural Flow**: Transitions should feel smooth and logical
8. **Explain Why**: Context makes better training videos
9. **Review Examples**: Study successful training videos
10. **Iterate**: First beat sheet won't be perfect—refine it

## Common Mistakes to Avoid

❌ **Too Fast**: Cramming too much into short beats
❌ **Too Formal**: Using corporate/academic language
❌ **No Context**: Just showing commands without explaining why
❌ **Untested**: Commands that don't actually work
❌ **Poor Timing**: Narration too long/short for beat duration
❌ **Missing Pauses**: Not giving viewers time to comprehend
❌ **Assumption Heavy**: Assuming prerequisite knowledge
❌ **No Transitions**: Abrupt jumps between beats
❌ **Boring Narration**: Reading docs verbatim
❌ **Unclear Actions**: Vague browser/terminal instructions

## Next Steps

- [Workflow Guide](workflow.md) - Complete production process
- [Command Reference](../commands/overview.md) - All available commands
- [Examples](../examples/sample-video.md) - See complete beat sheets
- [Customization](customization.md) - Tailor to your needs

## Resources

- **Style Guide**: [Google Developer Documentation Style Guide](https://developers.google.com/style)
- **Video Examples**: Search YouTube for "installation tutorial" to see structure
- **Narration Practice**: Record yourself reading narration, play it back
- **Timing Tool**: Use a stopwatch to time yourself reading narration aloud
