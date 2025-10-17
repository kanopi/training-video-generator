---
description: Generate automation scripts from beat sheet for recording
argument-hint: [beat-sheet-file]
allowed-tools: Read, Write
---

# Video Automation Script Generator

Generate AppleScript and bash automation scripts from a beat sheet to automate terminal command execution during video recording.

## Your Task

Parse a beat sheet file and generate automation scripts that will:
1. Open iTerm2 and execute terminal commands automatically
2. Handle timing delays between commands
3. Navigate browser tabs if needed
4. Control the recording flow

## Input

User provides path to beat sheet file:
```
scripts/video-scripts/[topic]-beat-sheet.md
```

## Step 1: Parse Beat Sheet

Read the beat sheet and extract:
- Beat numbers and names
- Duration for each beat
- Terminal commands from code blocks
- Browser actions (note if iTerm2 browser plugin is being used)
- Visual timing cues

**iTerm2 Browser Plugin Support**: If the beat sheet includes browser actions and mentions using iTerm2's browser plugin, note this in the automation script. The browser plugin allows web browsing directly in iTerm2, perfect for showing both CLI and web UI in the same window. Learn more: https://iterm2.com/browser-plugin.html

## Step 2: Generate AppleScript

Create an AppleScript file that:
- Opens iTerm2
- Creates a new window/tab
- Executes commands in sequence
- Adds delays based on beat durations

### AppleScript Template

```applescript
#!/usr/bin/osascript

tell application "iTerm2"
    -- Create new window
    create window with default profile

    tell current session of current window
        -- Beat 1: [Name]
        delay [duration]

        -- Beat 2: [Name]
        write text "[command1]"
        delay [duration after command]
        write text "[command2]"
        delay [remaining beat duration]

        -- Continue for all beats...
    end tell
end tell
```

## Step 3: Generate Bash Orchestration Script

Create a bash script for command reference:

```bash
#!/bin/bash
#Beat-by-beat commands for [topic]

echo "Beat 1: [Name]"
# [Duration] seconds
# [Narration]

echo "Beat 2: [Name]"
[command1]
[command2]
# Duration: [X] seconds

# Continue...
```

## Step 4: Generate Timing JSON

Create JSON file with timing data:

```json
{
  "video_title": "[Topic]",
  "total_duration": "[X] minutes",
  "beats": [
    {
      "number": 1,
      "name": "[Beat Name]",
      "duration": 15,
      "has_commands": false
    },
    {
      "number": 2,
      "name": "[Beat Name]",
      "duration": 30,
      "has_commands": true,
      "commands": ["command1", "command2"]
    }
  ]
}
```

## Output Files

Save generated files to:
```
scripts/automation/
├── [topic]-record.sh           # Main recording wrapper (run this!)
├── [topic]-automate.scpt       # AppleScript automation
├── [topic]-commands.sh         # Bash reference
└── [topic]-timing.json         # Timing data
```

## Example Output

For a beat sheet with 3 beats, generate:

### applescript-example.scpt
```applescript
tell application "iTerm2"
    create window with default profile
    tell current session of current window
        -- Beat 1: Introduction (15s)
        delay 15

        -- Beat 2: Check Prerequisites (20s)
        write text "node --version"
        delay 3
        write text "npm --version"
        delay 17

        -- Beat 3: Installation (30s)
        write text "npm install -g myproject"
        delay 30
    end tell
end tell
```

## Best Practices

- **Command delays**: Add 2-3 seconds after each command for output
- **Long operations**: Add full duration for installations
- **Error handling**: Include success verification commands
- **Clean state**: Start with `clear` command if needed
- **Path handling**: Use absolute paths or `cd` first

## Usage Instructions

The command should generate **FOUR files**:

1. **[topic]-record.sh** - Main wrapper script (uses recording-script.sh template)
   - Starts FFmpeg screen recording automatically
   - Runs the AppleScript automation
   - Stops recording when complete
   - Ensures perfect sync between video and audio

2. **[topic]-automate.scpt** - AppleScript automation (uses applescript-template.scpt)
   - Executes terminal commands
   - Controls iTerm2 window
   - Timing matches beat sheet durations

3. **[topic]-commands.sh** - Human-readable command reference
   - Lists all commands in order
   - Includes narration text
   - Useful for manual review

4. **[topic]-timing.json** - Machine-readable timing data
   - Beat durations
   - Command sequences
   - Used by merge script

### Generation Process

1. **Parse beat sheet** to extract:
   - Beat numbers, names, durations
   - Terminal commands
   - Total video duration

2. **Generate recording wrapper** (from recording-script.sh template):
   - Replace `{{TOPIC}}` with topic name
   - Replace `{{DURATION}}` with total duration in minutes
   - Save as `scripts/automation/[topic]-record.sh`
   - Make executable: `chmod +x`

3. **Generate AppleScript** (from applescript-template.scpt):
   - Parse beat sheet commands
   - Calculate delays between commands
   - Save as `scripts/automation/[topic]-automate.scpt`
   - Make executable: `chmod +x`

4. **Generate command reference** (bash script format):
   - List beats with narration
   - Show commands in order
   - Save as `scripts/automation/[topic]-commands.sh`

5. **Generate timing JSON**:
   - Extract beat timing data
   - Save as `scripts/automation/[topic]-timing.json`

### Success Message

Show user what was generated and how to use it:

```
✅ Automation scripts generated!

Files created:
  - scripts/automation/[topic]-record.sh     (main recording wrapper)
  - scripts/automation/[topic]-automate.scpt (AppleScript automation)
  - scripts/automation/[topic]-commands.sh   (command reference)
  - scripts/automation/[topic]-timing.json   (timing data)

To record your video:
  bash scripts/automation/[topic]-record.sh

This will:
  1. Start screen recording automatically (FFmpeg)
  2. Run terminal automation (AppleScript)
  3. Stop recording when complete
  4. Save to: recordings/[topic].mov

The recording will be perfectly synced with your audio narration!
```

Complete generation with success message showing file locations.
