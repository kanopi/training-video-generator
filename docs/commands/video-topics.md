# /video-topics Command

The `/video-topics` command analyzes your project's documentation and suggests relevant training video topics with detailed metadata.

## Overview

This command is the first step in the video creation workflow. It intelligently scans your project to identify topics that would make good training videos.

**Command**: `/video-topics`

**Allowed Tools**: `Read`, `Glob`, `Grep`

## What It Does

1. **Scans Project Documentation**
   - Reads README.md
   - Analyzes docs/ directory
   - Reviews API documentation
   - Examines package files (package.json, composer.json, etc.)

2. **Identifies Topics**
   - Installation & Setup procedures
   - Core Features & Functionality
   - Common Workflows
   - Advanced Usage scenarios
   - API Reference content

3. **Provides Metadata**
   - Target audience level (Beginner, Intermediate, Advanced)
   - Estimated video duration
   - Required prerequisites
   - Topic category

## Usage

```bash
/video-topics
```

Simply run the command in any project directory where you have documentation.

## Example Output

```markdown
# Suggested Training Video Topics

## Installation & Setup
### Installing MyProject
- **Audience**: Beginner
- **Duration**: 5 minutes
- **Prerequisites**: Node.js 18+, npm 9+
- **Coverage**: Installation process, system requirements, verification

## Core Features
### Using the Plugin System
- **Audience**: Intermediate
- **Duration**: 8 minutes
- **Prerequisites**: MyProject installed, basic command line knowledge
- **Coverage**: Installing plugins, configuration, custom plugins

## Workflows
### Building a Complete Application
- **Audience**: Intermediate
- **Duration**: 12 minutes
- **Prerequisites**: MyProject basics, understanding of project structure
- **Coverage**: Project initialization, development workflow, deployment
```

## When to Use

- **Starting a new video series**: Get a comprehensive list of potential topics
- **Planning documentation**: Identify gaps in your current documentation
- **Content strategy**: Organize topics by difficulty and dependencies
- **Project onboarding**: Discover all the areas that need video coverage

## Tips

1. **Review suggestions**: Not every suggested topic needs a video - prioritize based on your audience
2. **Check prerequisites**: Topics are ordered with dependencies in mind
3. **Combine topics**: Some related topics can be merged into a longer video
4. **Update documentation first**: Better docs lead to better topic suggestions

## Output

The command generates a markdown file at:
```
scripts/video-scripts/suggested-topics.md
```

This file contains all suggested topics with metadata, ready for you to review and select from.

## Next Steps

After reviewing suggested topics:

1. Choose a topic to create
2. Run `/video-script <topic>` to generate the beat sheet
3. Continue with the workflow

## Configuration

The command respects your project's `.training-video-generator/config.json` if it exists:

```json
{
  "defaultDuration": 7,
  "targetAudience": ["beginner", "intermediate"],
  "includeCategories": ["installation", "features", "workflows"]
}
```

## Troubleshooting

### "No documentation found"

**Problem**: Command can't find any documentation to analyze

**Solution**: Ensure you have at least one of:
- README.md in project root
- docs/ directory with markdown files
- API documentation files

### "Topics seem generic"

**Problem**: Suggested topics are too broad or vague

**Solution**:
- Improve your project documentation with more specific examples
- Add more detailed feature descriptions
- Include workflow documentation

### "Missing key topics"

**Problem**: Expected topics aren't suggested

**Solution**:
- Check if those topics are documented
- Add explicit sections in your README or docs
- Use clear headings for features and workflows

## Related Commands

- [`/video-script`](video-script.md) - Generate beat sheet for a topic
- [Quick Start Guide](../quick-start.md) - Complete workflow example
- [Workflow Guide](../guides/workflow.md) - Detailed production workflow
