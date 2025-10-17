# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.1] - 2025-10-17

### Added
- **Automated Screen Recording Wrapper**: New recording wrapper script that handles screen recording automatically
  - Starts FFmpeg screen recording programmatically
  - Runs AppleScript automation with perfect timing
  - Stops recording automatically when complete
  - Ensures perfect A/V sync between video and audio
  - No manual recording timing needed
- **iTerm2 Window Sizing**: AppleScript now sets iTerm2 window to 16:9 aspect ratio (1920x1080)
  - Consistent window size for every recording
  - Professional 16:9 framing for video platforms
- **FFmpeg Cropping**: Recording script crops to exact iTerm2 window area
  - Captures only the terminal window, not entire display
  - Perfect match with window positioning
  - No wasted pixels or post-processing needed
- **Video Topics File Output**: `/video-topics` now saves suggestions to file
  - Saves to `scripts/video-scripts/video-topics-suggestions.md`
  - Enables handoff to `/video-script` command

### Changed
- **Video Duration Targets**: Updated from 3-10 minutes to 3-5 minutes
  - Most videos should be under 5 minutes
  - Complex topics can extend to 8 minutes max
  - Updated all commands and documentation to reflect shorter format
  - Encourages focused, concise content
- **Improved `/video-script` Handoff**: Now reads `/video-topics` output automatically
  - Checks for `video-topics-suggestions.md` file
  - Uses suggested key points as outline
  - Follows estimated duration from analysis
  - Maintains consistency between topic analysis and beat sheet
- **Simplified Configuration**: Reduced example.config.json to minimal working example
  - Only includes options actually used by commands
  - Changed from 280+ lines to 22 lines
  - Removed aspirational/unused configuration options

### Fixed
- **A/V Sync Issues**: Automated recording wrapper ensures perfect synchronization
  - Eliminates human timing delays
  - Video duration matches audio duration exactly
  - Controlled start/stop timing via script

## [0.1.0] - 2025-10-13

### Added
- Initial release of Training Video Generator Claude Code plugin
- **5 Specialized Commands** for automated video creation:
  - `/video-topics` - Analyze project documentation and suggest video topics
  - `/video-script` - Generate beat-by-beat video scripts
  - `/video-automate` - Create automation scripts for screen recording
  - `/video-narrate` - Generate TTS audio narration
  - `/video-merge` - Merge video and audio into final output
- **Beat Sheet Generator**: AI-powered screenplay-style scripts with:
  - Word-for-word narration text
  - Exact terminal commands to execute
  - Browser actions and navigation
  - Visual cues and timing
  - Duration estimates per beat
- **Automation Script Generation**:
  - AppleScript for iTerm2 terminal automation
  - Bash orchestration scripts
  - Browser automation support
  - Screen recording control scripts
- **Multiple TTS Providers**:
  - ElevenLabs API integration (premium quality)
  - OpenAI TTS API integration
  - macOS built-in `say` command (free fallback)
  - Configurable voice selection
- **Video Post-Production**:
  - FFmpeg-based video/audio merging
  - Professional encoding (h264/aac)
  - Intro/outro branding support
  - Optimized web playback settings
- **Project-Agnostic Design**:
  - Analyzes any project's documentation
  - Adapts to project structure
  - No hardcoded project names
  - Reusable templates
- **Professional Templates**:
  - Beat sheet markdown template
  - AppleScript automation template
  - Recording script template
  - Narration script template
  - FFmpeg merge script template
- **Complete Documentation**:
  - MkDocs documentation site
  - Installation guide
  - Quick start guide
  - Detailed command reference
  - Workflow guides
  - Beat sheet writing guide
  - Customization guide
  - Troubleshooting guide
  - Example videos
- **Configuration System**:
  - JSON-based configuration
  - TTS provider settings
  - Recording preferences
  - Output settings
  - Branding options
- **Example Content**:
  - Sample beat sheet
  - Example automation scripts
  - Documentation examples
- **GitHub Integration**:
  - Automated docs deployment
  - GitHub Actions workflows
- **Licensing**:
  - GPL-2.0-or-later license

### Features for Future Releases
- Multi-platform support (Linux, Windows)
- Additional TTS providers
- Video editing capabilities
- Subtitle/caption generation
- Multiple video format exports
- Cloud rendering support
- Batch video generation
- Video analytics

[Unreleased]: https://github.com/kanopi/training-video-generator/compare/v0.1.1...HEAD
[0.1.1]: https://github.com/kanopi/training-video-generator/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/kanopi/training-video-generator/releases/tag/v0.1.0
