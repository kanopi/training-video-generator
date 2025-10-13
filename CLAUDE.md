# Claude Context for Training Video Generator Development

This file provides context for Claude (or other AI assistants) when working on this project.

## Project Overview

**Training Video Generator** is a Claude Code plugin that automates the creation of professional training videos from project documentation. It provides 5 slash commands that work together to generate scripts, automate recordings, create narration, and produce final videos.

## Key Architectural Decisions

### 1. Project-Agnostic Design

The plugin must work with ANY project, not just specific ones. This means:
- Commands analyze documentation dynamically
- No hardcoded project names or paths
- Templates are generic and reusable
- Configuration is project-specific (in user's project, not in plugin)

### 2. Modular Workflow

Each command is independent and can be run standalone:
- `/video-topics` - Analyzes docs, suggests topics
- `/video-script` - Generates beat sheet from topic
- `/video-automate` - Creates automation scripts from beat sheet
- `/video-narrate` - Generates TTS audio from beat sheet
- `/video-merge` - Combines video + audio

Users can run the full pipeline or just specific steps.

### 3. Beat Sheet Format

The beat sheet is the core artifact. It's a markdown file with:
```markdown
## Beat N: [Scene Name]
**Duration**: X seconds
**Visual**: [What's on screen]
**Browser Tab**: [URL or N/A]
**Narration**: "Exact words for TTS..."
**Terminal Commands**:
```bash
command here
```
**Browser Actions**: [What to click/navigate]
**Visual Notes**: [Camera positioning, etc.]
```

This format is:
- Human-readable (markdown)
- Machine-parseable (structured)
- Professional (screenplay-style)
- Complete (all info needed for automation)

### 4. Multi-Provider TTS Support

Support multiple TTS providers with fallback:
1. **ElevenLabs** (best quality, requires API key)
2. **OpenAI TTS** (good quality, requires API key)
3. **macOS `say`** (free, always available)

Configuration in user's project determines provider.

### 5. Template-Based Generation

All generated files (AppleScript, bash scripts, etc.) come from templates in `templates/` directory. This allows:
- Easy customization
- Consistent output
- Maintainable code generation
- Version control of templates

## File Organization

```
training-video-generator/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata (version, name, etc.)
├── commands/                # 5 slash command files
│   ├── video-topics.md      # Analyze project, suggest topics
│   ├── video-script.md      # Generate beat sheet
│   ├── video-automate.md    # Generate automation scripts
│   ├── video-narrate.md     # Generate TTS audio
│   └── video-merge.md       # Merge video + audio
├── templates/               # Generation templates
│   ├── beat-sheet.md        # Beat sheet structure
│   ├── applescript-template.scpt
│   ├── recording-script.sh
│   ├── narration-script.sh
│   └── merge-script.sh
├── docs/                    # MkDocs documentation
│   ├── index.md            # Home page
│   ├── installation.md     # Setup guide
│   ├── quick-start.md      # First video walkthrough
│   ├── commands/           # Detailed command docs
│   ├── guides/             # Workflow & customization guides
│   └── examples/           # Example beat sheets & videos
├── examples/               # Sample outputs
│   └── sample-beat-sheet.md
├── .github/workflows/      # CI/CD
│   └── docs.yml           # MkDocs deployment
├── mkdocs.yml             # MkDocs configuration
├── README.md              # Project overview
├── CHANGELOG.md           # Version history
├── CLAUDE.md              # This file
└── LICENSE.md             # GPL-2.0-or-later
```

## Development Workflow

### Adding a New Command

1. **Create command file** in `commands/[name].md`
2. **Add YAML frontmatter**:
```yaml
---
description: Brief description of what command does
argument-hint: [optional-arg]
allowed-tools: Bash(git:*), Read, Glob, Grep, Write
---
```
3. **Write command logic** in markdown (what Claude should do)
4. **Update `docs/commands/overview.md`** to list new command
5. **Create detailed docs** in `docs/commands/[name].md`
6. **Update mkdocs.yml** navigation
7. **Update README.md** command count

### Updating Command Logic

When updating command files:
- Preserve the frontmatter
- Maintain project-agnostic language
- Include examples for multiple scenarios
- Test with different project types
- Update corresponding documentation

### Creating Templates

Templates in `templates/` use placeholders like:
- `{{TOPIC}}` - Video topic name
- `{{PROJECT_NAME}}` - Project name from documentation
- `{{BEAT_N}}` - Beat number
- `{{DURATION}}` - Beat duration
- `{{NARRATION}}` - Narration text
- `{{COMMAND}}` - Terminal command

When generating from templates, replace all placeholders.

### Documentation Updates

1. **Edit files** in `docs/`
2. **Test locally**: `mkdocs serve`
3. **Build**: `mkdocs build --strict` (catches broken links)
4. **Commit**: Auto-deploys to GitHub Pages on push to main

## Important Files to NOT Modify

- **LICENSE.md** - GPL-2.0-or-later license (legal document)
- **GitHub Actions** - `.github/workflows/docs.yml` (stable deployment)

## Code Conventions

### Command Files

- Use `##` for major sections
- Use `###` for subsections
- Include code examples with proper syntax highlighting
- Provide multiple examples (simple → complex)
- Document all arguments and focus options
- Include expected output examples

### Documentation

- Write in active voice
- Use admonitions for warnings/tips/notes
- Include "Quick Start" sections at the top
- Link between related docs
- Use emoji sparingly (only in headings for visual navigation)

### Frontmatter Standards

**Description**: Brief imperative statement (e.g., "Generate beat-by-beat video script")

**Argument-hint**: Show optional args in square brackets: `[topic]`, `[beat-sheet-file]`

**Allowed-tools**: List all tools the command needs:
- Git operations: `Bash(git:*)`
- File operations: `Read, Glob, Grep, Write, Edit`
- FFmpeg: `Bash(ffmpeg:*)`
- AppleScript: `Bash(osascript:*)`

## Testing Approach

### Manual Testing

1. **Install locally**: `ln -s $(pwd) ~/.claude/plugins/training-video-generator`
2. **Enable**: `claude plugins enable training-video-generator`
3. **Test each command** in a sample project
4. **Verify outputs**:
   - Beat sheets are well-formatted
   - Automation scripts work
   - TTS audio generates correctly
   - Videos merge properly

### Documentation Testing

```bash
mkdocs build --strict  # Catches broken links, missing pages
mkdocs serve          # Preview at http://localhost:8000
```

### Cross-Project Testing

Test commands with different project types:
- Node.js project
- Python project
- Static site
- Claude Code plugin
- Web application

## Common Patterns

### Analyzing Project Documentation

Commands should look for documentation in common locations:
- `README.md`
- `docs/` directory
- `CONTRIBUTING.md`
- `API.md` or similar
- Package files (`package.json`, `pyproject.toml`, etc.)

### Generating Beat Sheets

Beat sheets should:
- Start with introduction beat
- Have logical progression
- Include realistic timing (10-30 seconds per beat)
- Total 3-10 minutes for most videos
- End with conclusion/next steps beat

### Creating Automation Scripts

Automation scripts should:
- Have clear comments
- Include error handling
- Use `sleep` commands for timing
- Be idempotent (can run multiple times)
- Clean up after themselves

## Dependencies

### Runtime Dependencies (User's Machine)

- Claude Code CLI
- Git
- FFmpeg
- Optional: iTerm2 (better than Terminal.app)
- Optional: ElevenLabs API key
- Optional: OpenAI API key

### Documentation Build Dependencies

- Python 3.x
- mkdocs-material
- mkdocs-git-revision-date-localized-plugin

Install: `pip install mkdocs-material mkdocs-git-revision-date-localized-plugin`

## Resources

### External Documentation

- [Claude Code Documentation](https://docs.claude.com/en/docs/claude-code)
- [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)
- [iTerm2 Scripting](https://iterm2.com/documentation-scripting.html)
- [FFmpeg Documentation](https://ffmpeg.org/documentation.html)
- [ElevenLabs API](https://elevenlabs.io/docs)
- [OpenAI TTS API](https://platform.openai.com/docs/guides/text-to-speech)

### Internal References

- [Commands Overview](docs/commands/overview.md)
- [Workflow Guide](docs/guides/workflow.md)
- [Beat Sheet Guide](docs/guides/beat-sheets.md)

## Troubleshooting for AI Assistants

### When generating beat sheets

1. Analyze the project first (read README, docs)
2. Identify key features/workflows
3. Create logical beat progression
4. Include realistic terminal commands
5. Write natural narration text
6. Estimate timing based on content

### When creating automation scripts

1. Parse beat sheet structure carefully
2. Extract commands in order
3. Add timing delays between commands
4. Handle window/tab switching
5. Include error checking
6. Test script idempotency

### When TTS generation fails

1. Check API key configuration
2. Verify API quota/limits
3. Fall back to macOS `say` command
4. Check narration text for special characters
5. Validate audio file output

### When documentation builds fail

1. Run `mkdocs build --strict` to see errors
2. Check for broken links in navigation (`mkdocs.yml`)
3. Verify all referenced files exist in `docs/`
4. Check markdown syntax
5. Validate YAML frontmatter

## Future Enhancements

Ideas for future development:

1. **Multi-platform Support**: Linux and Windows automation
2. **Additional TTS Providers**: Azure, Google Cloud, AWS Polly
3. **Video Editing**: Trim, splice, add overlays
4. **Subtitle Generation**: Auto-generate captions/subtitles
5. **Batch Processing**: Generate multiple videos at once
6. **Cloud Rendering**: Offload video processing to cloud
7. **Analytics**: Track video engagement
8. **Interactive Elements**: Add clickable elements in videos
9. **Template Library**: Pre-built beat sheets for common scenarios
10. **Visual Effects**: Transitions, zoom effects, highlights

---

Last updated: 2025-10-13
