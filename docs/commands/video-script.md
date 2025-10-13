# /video-script Command

The `/video-script` command generates a complete beat-by-beat video script with narration, terminal commands, timing, and visual cues.

## Overview

This is the core creative command that transforms a video topic into a production-ready beat sheet. The output is a detailed script that serves as the blueprint for your entire video.

**Command**: `/video-script <topic>`

**Allowed Tools**: `Read`, `Glob`, `Grep`, `Write`

## What It Does

1. **Analyzes Topic Requirements**
   - Reads relevant documentation
   - Identifies key concepts to cover
   - Determines logical flow

2. **Creates Beat-by-Beat Structure**
   - Introduction beat
   - Main content beats (typically 5-8 beats)
   - Conclusion beat

3. **Generates Detailed Beat Information**
   - Duration estimate per beat
   - Narration text (what to say)
   - Terminal commands (what to type)
   - Browser actions (what to click)
   - Visual notes (what to highlight)

## Usage

```bash
/video-script <topic>
```

**Parameters**:
- `<topic>`: The video topic name (from `/video-topics` or your own)

**Example**:
```bash
/video-script installation-and-setup
```

## Beat Sheet Structure

Each generated beat includes:

```markdown
## Beat N: [Beat Name]
**Duration**: [X] seconds
**Visual**: [Terminal/Browser/Split]
**Browser Tab**: [URL or N/A]

**Narration**:
"[Exact text to speak in the video]"

**Terminal Commands**:
```bash
command --to-execute
```

**Browser Actions**:
- [Specific actions to perform]

**Visual Notes**:
- [Highlighting, pauses, speed adjustments]
```

## Example Output

See the complete example: [Sample Beat Sheet](../examples/sample-video.md)

Quick preview:

```markdown
# Video: Installation and Setup

**Duration**: 5 minutes
**Target Audience**: Beginner
**Prerequisites**: macOS, Linux, or Windows computer

---

## Beat 1: Introduction
**Duration**: 15 seconds
**Visual**: Terminal - Clean iTerm2 window
**Browser Tab**: N/A

**Narration**:
"Welcome to MyProject! In this video, we'll walk through the complete
installation and setup process. By the end, you'll have MyProject up
and running on your machine. Let's get started!"

**Terminal Commands**:
```bash
# No commands in intro
```

**Visual Notes**:
- Show clean terminal
- Display project logo or name
```

## Best Practices

### Narration Writing

1. **Conversational Tone**: Write like you're teaching a friend
   - ✅ "Great! Now let's create a directory for our project"
   - ❌ "The next step requires directory creation"

2. **Clear Instructions**: Be explicit about what's happening
   - ✅ "We'll use npm to install globally, which makes it available anywhere"
   - ❌ "Install the package"

3. **Appropriate Pacing**: Match narration to action duration
   - For quick commands: Brief narration
   - For long operations: More explanation

4. **Helpful Context**: Explain why, not just what
   - ✅ "Let's verify you have Node 18+, which MyProject requires"
   - ❌ "Check your Node version"

### Terminal Commands

1. **Executable Commands**: Every command should actually work
2. **Safe Commands**: No destructive operations without warnings
3. **Realistic Output**: Consider what output will appear
4. **Proper Sequencing**: Commands in logical order

### Visual Notes

1. **Highlight Important Output**: Draw attention to key information
2. **Pause for Comprehension**: Give viewers time to read output
3. **Speed Adjustments**: Note when to speed up boring parts
4. **Scene Transitions**: Smooth switches between terminal and browser

## Configuration

Customize beat sheet generation in `.training-video-generator/config.json`:

```json
{
  "videoSettings": {
    "defaultDuration": 7,
    "introDuration": 15,
    "conclusionDuration": 20,
    "beatDurationRange": [20, 60]
  },
  "narrationStyle": "conversational",
  "visualStyle": "clean-terminal",
  "includePostProduction": true
}
```

## Output Location

Beat sheets are saved to:
```
scripts/video-scripts/[topic]-beat-sheet.md
```

## When to Use

- After identifying a topic with `/video-topics`
- When you want to script a video manually
- Before recording to ensure proper flow
- When planning multi-video series

## Tips

1. **Review and Edit**: Generated scripts are starting points - refine them
2. **Test Commands**: Verify all commands work in a clean environment
3. **Time It Out**: Read narration aloud to check pacing
4. **Consider Audience**: Adjust complexity based on target viewers
5. **Plan B-Roll**: Note opportunities for overlays or graphics

## Post-Production Notes

Beat sheets include a section for post-production guidance:

```markdown
## Post-Production Notes

**Editing**:
- Speed up Beat 4 (npm install) to 2x speed
- Trim any long pauses between beats

**B-Roll Suggestions**:
- Project logo during introduction
- Architecture diagram during initialization

**Music** (optional):
- Light, upbeat background music at 10% volume during intro/outro
- No music during technical steps

**Captions/Subtitles**:
- Add subtitles for all narration
- Highlight terminal commands in monospace font
```

## Troubleshooting

### "Beat sheet seems rushed"

**Problem**: Narration is too brief or beats are too short

**Solution**:
- Increase `defaultDuration` in config
- Manually adjust beat durations in the generated file
- Add more explanatory narration

### "Commands don't work together"

**Problem**: Commands assume state from previous beats

**Solution**:
- Review beat sequence for logic
- Add setup commands to earlier beats
- Include verification commands between steps

### "Narration sounds robotic"

**Problem**: Text is too formal or technical

**Solution**:
- Rewrite in conversational style
- Read aloud to check naturalness
- Add transitions and connective phrases

### "Missing visual cues"

**Problem**: Visual notes section is sparse

**Solution**:
- Think about what viewers need to see
- Add highlights for important output
- Note when to pause or speed up
- Include scene transition guidance

## Next Steps

After generating and reviewing your beat sheet:

1. **Edit the beat sheet**: Refine narration, adjust timing
2. **Run `/video-automate`**: Generate automation scripts
3. **Run `/video-narrate`**: Create TTS audio files
4. **Record the video**: Follow the beat sheet timing
5. **Run `/video-merge`**: Combine recording with audio

## Related Commands

- [`/video-topics`](video-topics.md) - Discover video topics
- [`/video-automate`](video-automate.md) - Generate automation scripts
- [`/video-narrate`](video-narrate.md) - Create TTS narration
- [Beat Sheet Guide](../guides/beat-sheets.md) - Writing effective beat sheets
