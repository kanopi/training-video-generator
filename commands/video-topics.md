---
description: Analyze project documentation and suggest video topics
argument-hint: [focus]
allowed-tools: Read, Glob, Grep
---

# Video Topics Generator

Analyze your project's documentation and generate relevant video topic suggestions.

## Your Task

You are helping to plan training videos for a project. Analyze the project documentation and suggest 5-10 video topics that would be valuable for users, developers, or stakeholders.

## Step 1: Analyze Project Documentation

Read and analyze the following files (if they exist):

```bash
# Core documentation
README.md
CONTRIBUTING.md
docs/index.md
docs/README.md

# API/Technical docs
API.md
docs/api/
docs/reference/

# Getting started
docs/installation.md
docs/quick-start.md
docs/getting-started.md

# Configuration
docs/configuration.md
docs/setup.md

# Package files (for understanding project)
package.json
pyproject.toml
composer.json
Cargo.toml
```

Use Glob and Read tools to find and read these files.

## Step 2: Identify Video Topics

Based on the documentation, identify topics in these categories:

### Installation & Setup (Beginner)
- Installation procedures
- Prerequisites and dependencies
- Initial configuration
- First-time setup
- Environment setup
- Troubleshooting installation

### Core Features (Beginner/Intermediate)
- Main features overview
- Feature walkthroughs
- Common use cases
- Basic workflows
- UI/CLI navigation

### Workflows & Best Practices (Intermediate)
- Development workflows
- Best practices
- Common patterns
- Integration examples
- Real-world scenarios

### Advanced Topics (Advanced)
- Advanced configuration
- Performance optimization
- Security considerations
- Custom integrations
- Advanced use cases

### API & Development (Advanced)
- API usage
- SDK integration
- Custom development
- Plugin/extension creation

## Step 3: Generate Topic Suggestions

For each suggested topic, provide:

### 1. Topic Title
Clear, descriptive title (e.g., "Installation and Setup on macOS")

### 2. Target Audience
- **Beginner**: First-time users, no prior knowledge required
- **Intermediate**: Some experience with the project
- **Advanced**: Experienced users, developers

### 3. Estimated Duration
- **Short**: 3-5 minutes
- **Medium**: 5-8 minutes
- **Long**: 8-12 minutes

### 4. Key Points to Cover
List 4-6 main points that should be covered in the video

### 5. Prerequisites
What the viewer needs to know or have installed

### 6. Demo Materials
What files, data, or setup is needed for the demo

## Output Format

```markdown
# Suggested Video Topics for [Project Name]

## Video 1: [Topic Title]

**Target Audience**: [Beginner/Intermediate/Advanced]
**Estimated Duration**: [3-5/5-8/8-12] minutes
**Category**: [Installation/Features/Workflows/Advanced/API]

### Description
[2-3 sentence description of what the video will cover]

### Key Points to Cover
1. [Point 1]
2. [Point 2]
3. [Point 3]
4. [Point 4]
5. [Point 5]

### Prerequisites
- [Prerequisite 1]
- [Prerequisite 2]

### Demo Materials Needed
- [Material 1]
- [Material 2]

### Why This Video Is Valuable
[1-2 sentences explaining the value to viewers]

---

## Video 2: [Next Topic]
[Same format...]

---

[Continue for 5-10 topics...]

---

## Recommended Order

For a complete video series, we recommend creating videos in this order:

1. **[Topic Title]** - Foundation for understanding
2. **[Topic Title]** - Builds on previous video
3. **[Topic Title]** - Natural progression
[etc...]

## Additional Topic Ideas

If you need more content, consider these additional topics:
- [Additional topic 1]
- [Additional topic 2]
- [Additional topic 3]
```

## Focus Parameter

If user provides a focus parameter, filter topics to that category:

- **installation**: Only installation, setup, and configuration topics
- **features**: Only feature walkthrough and demonstration topics
- **workflows**: Only workflow, best practices, and integration topics
- **api**: Only API documentation and development topics
- **advanced**: Only advanced configuration and optimization topics

## Best Practices

### Topic Selection
- Start with fundamental topics (installation, basic features)
- Progress from beginner to advanced
- Each video should have a clear, single focus
- Consider common pain points and questions

### Duration Estimation
- Installation/setup: Usually 5-8 minutes
- Feature demos: Usually 3-5 minutes per feature
- Workflows: Usually 8-12 minutes
- API/advanced: Usually 10-15 minutes

### Key Points
- Limit to 4-6 points per video
- Each point should take 30-90 seconds to demonstrate
- Points should follow a logical progression
- Include troubleshooting tips

### Prerequisites
- Be specific about required knowledge
- List all required software/tools
- Mention any accounts or API keys needed
- Note any project setup required

## Example Analysis

If analyzing a web framework project, you might suggest:

1. **Installation and First App** (Beginner, 5 min)
   - Installing the framework
   - Creating first project
   - Running development server
   - Understanding project structure

2. **Routing and Views** (Beginner, 6 min)
   - Creating routes
   - Defining views
   - Passing data to views
   - URL parameters

3. **Database Integration** (Intermediate, 8 min)
   - Setting up database
   - Creating models
   - Running migrations
   - Basic CRUD operations

[etc...]

## Tips for Quality Suggestions

- Review existing documentation thoroughly
- Look for code examples (good for demos)
- Identify common questions in issues/discussions
- Consider the learning curve
- Think about what would help someone get productive quickly
- Balance breadth (overview) with depth (detailed)

Remember: The goal is to help users understand and use the project effectively. Suggest topics that provide real value and follow a natural learning progression.
