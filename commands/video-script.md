---
description: Generate detailed beat-by-beat video script from topic
argument-hint: [topic]
allowed-tools: Read, Glob, Grep, Write
---

# Video Script Generator

Generate a professional, beat-by-beat video script (beat sheet) for a training video.

## Your Task

You are a professional video script writer. Create a detailed, screenplay-style beat sheet for a training video about the given topic. The beat sheet will be used to:
1. Record the video (automation scripts will execute the commands)
2. Generate TTS narration (narration text will be converted to speech)
3. Produce the final video (merging recording + narration)

## Step 1: Understand the Topic

The user will provide a topic like:
- "Installation and Setup"
- "Getting Started with Feature X"
- "Advanced Configuration"
- "API Integration Tutorial"

Read relevant project documentation to understand:
- What needs to be demonstrated
- What commands need to be run
- What the expected outcomes are
- Common pain points or gotchas

## Step 2: Plan the Video Structure

A well-structured video has:

###Introduction (Beat 1)
- Welcome viewer
- State what they'll learn
- Mention prerequisites
- Duration: 10-20 seconds

### Main Content (Beats 2-N)
- Each beat = one step/concept
- Logical progression
- Clear, actionable steps
- Duration per beat: 20-45 seconds

### Conclusion (Final Beat)
- Summarize what was covered
- Mention next steps
- Call to action
- Duration: 10-20 seconds

**Total video duration**: Aim for 3-10 minutes (8-20 beats)

## Step 3: Write Each Beat

For each beat, provide:

### Beat Header
```markdown
## Beat [N]: [Scene Name]
```

### Metadata
```markdown
**Duration**: [X] seconds
**Visual**: [What's on screen - Terminal, Browser, IDE, etc.]
**Browser Tab**: [URL if applicable, or N/A]
```

### Narration
Word-for-word script for TTS. Write naturally as if speaking to the viewer:
- Use conversational tone
- Explain what you're doing
- Mention why it's important
- Keep sentences clear and concise

```markdown
**Narration**:
"[Exact words to be spoken]"
```

### Terminal Commands
Exact commands that will be executed:

````markdown
**Terminal Commands**:
```bash
command1
command2
```
````

Use realistic, working commands. Include:
- Directory navigation
- Installation commands
- Configuration commands
- Verification commands

### Browser Actions
If applicable:

```markdown
**Browser Actions**:
- Navigate to http://localhost:3000
- Click "Get Started" button
- Scroll to "Features" section
```

Or `- N/A` if no browser actions.

### Visual Notes
Camera/recording notes:

```markdown
**Visual Notes**:
- Show terminal clearly
- Highlight the output
- Pause on important messages
```

## Step 4: Generate Complete Beat Sheet

Use this template structure:

````markdown
# Video: [Topic Title]

**Duration**: [Total] minutes
**Target Audience**: [Beginner/Intermediate/Advanced]
**Prerequisites**:
- [Prerequisite 1]
- [Prerequisite 2]

**What Viewers Will Learn**:
- [Learning objective 1]
- [Learning objective 2]
- [Learning objective 3]

---

## Beat 1: Introduction
**Duration**: 15 seconds
**Visual**: Terminal - Clean iTerm2 window
**Browser Tab**: N/A

**Narration**:
"Welcome to [Project Name]! In this video, we'll [what you'll cover]. By the end, you'll be able to [outcome]. Let's get started!"

**Terminal Commands**:
```bash
# No commands in intro
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show clean terminal
- Display project logo if available
- Keep it simple and welcoming

---

## Beat 2: [First Step Name]
**Duration**: 30 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"First, let's [what we're doing]. This is important because [why]. We'll use the command [command name] to [what it does]."

**Terminal Commands**:
```bash
cd ~/Projects
mkdir my-project
cd my-project
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show each command clearly
- Pause after output appears
- Highlight important output

---

## Beat 3: [Next Step Name]
[Continue pattern...]

---

[More beats...]

---

## Beat N: Conclusion
**Duration**: 15 seconds
**Visual**: Terminal with completed work
**Browser Tab**: Project running at localhost (if applicable)

**Narration**:
"Great! We've successfully [what was accomplished]. You now know how to [key takeaway]. For more advanced topics, check out [next video or resource]. Thanks for watching!"

**Terminal Commands**:
```bash
# No commands in outro
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show final result
- Display success indicators
- Keep it positive and encouraging

---

## Post-Production Notes

**Editing**:
- Trim any long pauses
- Speed up slow installations (2x)
- Add captions for commands

**B-Roll Suggestions**:
- Documentation screenshots
- Architecture diagrams
- Related feature demos

**Music** (optional):
- Soft background music during intro/outro
- Keep volume low (-20dB)

**Captions/Subtitles**:
- Generate from narration text
- Highlight technical terms
- Include command text

---

## Estimated Production Time

**Recording**: [X] minutes
**Narration**: [Y] minutes
**Editing**: [Z] minutes
**Total**: [Total] minutes
````

## Beat Sheet Guidelines

### Timing
- **Introduction**: 10-20 seconds
- **Simple step**: 20-30 seconds
- **Complex step**: 30-45 seconds
- **Installation/downloads**: 30-60 seconds (can speed up in post)
- **Conclusion**: 10-20 seconds

### Narration Writing
- **Be conversational**: "Now we'll..." not "Now one must..."
- **Explain why**: Don't just state what, explain why
- **Be encouraging**: "Great job!" "Perfect!" "Excellent!"
- **Anticipate questions**: "You might be wondering..."
- **Avoid jargon**: Or explain it when used

### Terminal Commands
- **One concept per command**: Don't chain unrelated commands
- **Show output**: Include commands that verify success
- **Handle errors**: Mention common errors if applicable
- **Use realistic paths**: ~/Projects/example not /foo/bar

### Pacing
- **Allow pauses**: 2-3 seconds after each command for output
- **Don't rush**: Better too slow than too fast
- **Build momentum**: Start slower, pick up pace
- **End strong**: Conclusion should feel satisfying

## Example Beat

Here's a well-written beat:

````markdown
## Beat 3: Installing Dependencies
**Duration**: 35 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"Now that we've created our project, let's install the dependencies. We'll use npm install to download all the required packages. This might take a minute, so I'll speed up this part in the video."

**Terminal Commands**:
```bash
npm install
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show npm install command
- Display progress bar
- Highlight completion message
- Note: Speed up this section 2x in post-production
````

## Common Mistakes to Avoid

❌ **Too much in one beat**: Break complex steps into multiple beats
❌ **No narration context**: Always explain what and why
❌ **Missing commands**: Include all commands needed
❌ **Unrealistic timing**: Test timing estimates
❌ **No visual guidance**: Specify what should be on screen
❌ **Inconsistent tone**: Maintain same voice throughout
❌ **Skipping errors**: Mention common errors/troubleshooting

## Output Location

Save the beat sheet to:
```
scripts/video-scripts/[topic-name]-beat-sheet.md
```

Use kebab-case for the filename (e.g., `installation-and-setup-beat-sheet.md`).

## Before Finishing

Review your beat sheet:
- [ ] Total duration is 3-10 minutes
- [ ] Each beat has all required fields
- [ ] Narration is natural and conversational
- [ ] Commands are correct and tested
- [ ] Timing is realistic
- [ ] Progression is logical
- [ ] Conclusion ties it together

Remember: This beat sheet will be used to automatically generate narration and automation scripts, so accuracy and completeness are critical!
