# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Homebrew Hackers Club college template repository. It's a content-only repository using MDX files to create courses and guides for a learning platform. When committed and pushed, the platform automatically syncs and publishes the content.

## Architecture

This is a **content-only repository** with no build system, tests, or backend code. The platform consumes MDX files directly through git integration.

```
/
├── home.mdx              # Landing page for the college
├── courses/              # Course content with chapters
│   └── [course-name]/
│       ├── index.mdx     # Course overview (required)
│       └── *.mdx         # Individual chapters
├── guides/               # Standalone tutorial guides
│   └── *.mdx
├── assets/               # Images and media files
└── .cursor/              # Cursor AI configuration rules
    ├── general.mdc       # Structure and frontmatter rules
    ├── style.mdc         # Writing style guidelines
    └── create-video.mdc  # Video creation workflow
```

## Content Types & Frontmatter Requirements

### Course Index (`courses/[name]/index.mdx`)
**Required fields:**
- `title`: Course name
- `description`: What students will learn

**Optional fields:**
- `banner`: Path to 16:9 aspect ratio image (relative from assets/ or absolute URL)

### Guide (`guides/[name].mdx`)
Same as course index: requires `title` and `description`, optional `banner`.

### Chapter Files
Only requires `title` in frontmatter.

## Course Organization Patterns

**Simple course** (chapters directly in folder):
```
courses/intro-to-python/
  ├── index.mdx
  ├── 1-basics.mdx
  └── 2-variables.mdx
```

**Modular course** (chapters grouped in module folders):
```
courses/web-development/
  ├── index.mdx
  ├── 1-html-basics/
  │   ├── index.mdx
  │   ├── 1-structure.mdx
  │   └── 2-elements.mdx
  └── 2-css-styling/
      ├── 3-selectors.mdx
      └── 4-layout.mdx
```

## File Naming Conventions

- Use lowercase with hyphens: `intro-to-python`, `awesome-mac-terminal-setup`
- Number chapters for ordering: `1-intro.mdx`, `2-advanced.mdx`
- Be descriptive but concise: `setting-up-environment.mdx` not `setup.mdx`

## Guide Creation Workflow

When creating new guides, the Cursor rules define a structured 4-step process:

1. **Brainstorming**: Present 5 possible guide ideas covering different angles/skill levels
2. **Discovery**: Ask 3-5 questions to refine scope (audience, learning outcomes, length, prerequisites)
3. **Planning**: Create detailed outline with sections, key concepts, code examples
4. **Writing**: Write complete guide in one go after approval

Reference: `.cursor/general.mdc:93-158`

## Special MDX Components

### Woz Component (Interactive Learning)
Used for knowledge checks and interactive prompts:

```mdx
<Woz
  title="Recap"
  description="Make sure you really understand 🙃"
  prompt="Ask me 3 questions about this chapter to test my understanding."
/>
```

With custom placeholder:
```mdx
<Woz
  title="Context"
  description="Apply what you learned"
  context="User is learning about web basics"
  prompt=""
  placeholder="Describe your understanding here"
/>
```

## Writing Style Guidelines

From `.cursor/style.mdc`:
- Use simple, concise English for students learning new concepts
- Be encouraging and supportive
- Add emojis where appropriate (but don't overdo it)
- Avoid excessive **bold** or *italic* emphasis
- Break long content into digestible sections
- Always specify language in code blocks for syntax highlighting
- Use proper heading hierarchy (# once per page, then ##, ###, ####)
- Explain concepts before using technical terms
- Use real-world examples and analogies

## Banner Images

- **Aspect ratio**: 16:9 (displayed on feed page)
- **Formats**: png, jpg, jpeg, webp
- **Reference in frontmatter**:
  - Relative: `../assets/filename.png` or `assets/filename.jpg`
  - Absolute URL: `https://example.com/image.png`
- Must exist in `/assets/` directory if using relative path

## Publishing Workflow

This repository has no build step. Changes are published by:
1. Commit changes to MDX files
2. Push to GitHub
3. Platform automatically syncs and updates the college

From CONTRIBUTING.md:
- Use branch naming: `content/<your-slug>`
- Commit message format: `"content: add guide on AI workflows"`
- Open pull request with clear title

## Quality Checklist

Before committing new content:
- [ ] Frontmatter includes all required fields (`title`, `description`)
- [ ] Banner image exists if referenced
- [ ] File naming follows kebab-case conventions
- [ ] Content starts with `#` heading
- [ ] Code blocks have language specified
- [ ] Relative paths are correct
- [ ] Following style guide (simple English, appropriate emojis)
- [ ] Working links and proper formatting
