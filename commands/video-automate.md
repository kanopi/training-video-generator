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
- Browser actions
- Visual timing cues

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
├── [topic]-automate.scpt       # Main AppleScript
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

Generate usage instructions in the automation script comments:

```applescript
-- USAGE INSTRUCTIONS
-- 1. Start screen recording (Cmd+Shift+5)
-- 2. Run this script: osascript [topic]-automate.scpt
-- 3. Script will execute all commands automatically
-- 4. Stop recording when complete
-- 5. Save as: recordings/[topic].mov
```

Complete generation with success message showing file locations.
