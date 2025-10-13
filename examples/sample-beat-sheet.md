# Video: Installation and Setup

**Duration**: 5 minutes
**Target Audience**: Beginner
**Prerequisites**:
- macOS, Linux, or Windows computer
- Internet connection
- Basic terminal knowledge

**What Viewers Will Learn**:
- How to check system requirements
- How to install the project
- How to verify installation success
- How to run the project for the first time

---

## Beat 1: Introduction
**Duration**: 15 seconds
**Visual**: Terminal - Clean iTerm2 window
**Browser Tab**: N/A

**Narration**:
"Welcome to MyProject! In this video, we'll walk through the complete installation and setup process. By the end, you'll have MyProject up and running on your machine. Let's get started!"

**Terminal Commands**:
```bash
# No commands in intro
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show clean terminal
- Display project logo or name
- Keep it welcoming and simple

---

## Beat 2: Check Prerequisites
**Duration**: 25 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"First, let's verify you have the required prerequisites. You'll need Node.js version 18 or higher, and npm version 9 or higher. Let's check what you have installed."

**Terminal Commands**:
```bash
node --version
npm --version
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show version output clearly
- Highlight the version numbers
- Pause on output for 2 seconds

---

## Beat 3: Create Project Directory
**Duration**: 20 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"Great! Now let's create a directory for our project. We'll create a folder called my-project in your Projects directory and navigate into it."

**Terminal Commands**:
```bash
cd ~/Projects
mkdir my-project
cd my-project
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show each command execution
- Display pwd output to confirm location

---

## Beat 4: Install MyProject
**Duration**: 45 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"Now comes the main installation. We'll use npm to install MyProject globally, which makes it available anywhere on your system. This might take about 30 seconds, so I'll speed up this part in the video."

**Terminal Commands**:
```bash
npm install -g myproject
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show npm install command
- Display progress bar and download activity
- Show completion message
- **Post-production**: Speed up this section 2x

---

## Beat 5: Verify Installation
**Duration**: 20 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"Perfect! Let's verify the installation was successful by checking the version. If you see a version number, you're all set!"

**Terminal Commands**:
```bash
myproject --version
myproject --help
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show version output
- Show help output to demonstrate it's working
- Highlight key information

---

## Beat 6: Initialize Project
**Duration**: 30 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"Now let's initialize a new project. We'll use the init command which will ask you a few questions. I'll use the defaults for this demo, so I'll just press enter for each prompt."

**Terminal Commands**:
```bash
myproject init
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show interactive prompts
- Press Enter for each prompt
- Show completion message
- Display created files with ls

---

## Beat 7: Start Development Server
**Duration**: 35 seconds
**Visual**: Terminal + Browser (split screen or switch)
**Browser Tab**: http://localhost:3000

**Narration**:
"Excellent! Now let's start the development server. This will launch your project locally on port 3000. Once it's running, we'll open it in a browser to see our project live."

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

---

## Beat 8: Verify Everything Works
**Duration**: 25 seconds
**Visual**: Browser
**Browser Tab**: http://localhost:3000

**Narration**:
"And there we have it! Your project is running successfully. You can see the welcome page here, and everything is working as expected. You're now ready to start developing!"

**Terminal Commands**:
```bash
# No new commands - server still running
```

**Browser Actions**:
- Scroll down the page
- Click on "Getting Started" link
- Show basic functionality

**Visual Notes**:
- Demonstrate the application is interactive
- Show key features briefly
- Keep it high-level

---

## Beat 9: Stop Server and Conclusion
**Duration**: 20 seconds
**Visual**: Terminal
**Browser Tab**: N/A

**Narration**:
"To stop the server, simply press Control+C in your terminal. Great job! You've successfully installed MyProject, initialized a new project, and verified everything works. Check out the next video where we'll explore the core features. Thanks for watching!"

**Terminal Commands**:
```bash
# Press Ctrl+C to stop server
```

**Browser Actions**:
- N/A

**Visual Notes**:
- Show Ctrl+C stopping the server
- Return to clean terminal prompt
- End on a positive, encouraging note

---

## Post-Production Notes

**Editing**:
- Speed up Beat 4 (npm install) to 2x speed
- Add captions for all terminal commands
- Trim any long pauses between beats

**B-Roll Suggestions**:
- MyProject logo during introduction
- Architecture diagram during initialization
- Feature highlights during conclusion

**Music** (optional):
- Light, upbeat background music at 10% volume during intro and outro
- No music during technical steps to avoid distraction

**Captions/Subtitles**:
- Add subtitles for all narration
- Highlight terminal commands in monospace font
- Include URLs and version numbers

---

## Estimated Production Time

**Recording**: 6-7 minutes (includes buffer time)
**Narration**: 3 minutes (TTS generation)
**Editing**: 15-20 minutes (speed adjustments, captions)
**Total**: 25-30 minutes

---

## Notes for Video Generator

- Total of 9 beats
- Realistic timing with buffer
- Includes both terminal and browser scenes
- Commands are executable and safe
- Progression is logical and beginner-friendly
- Conclusion provides next steps
