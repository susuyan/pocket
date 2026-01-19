# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Pocket SKILL workspace for link extraction and content summarization. The repository contains various tools and agents for processing links, particularly from Weibo and other social media platforms.

## Key Commands

### Shell Script
- `scripts/format-daily-links.sh <file>` - Formats daily links markdown files by removing empty sections and normalizing whitespace
  - Default: Uses today's date as `docs/daily-links/$(date +%F).md`
  - Example: `scripts/format-daily-links.sh docs/daily-links/2026-01-16.md`

## Architecture

### Directory Structure

- `agents/` - Contains various AI agent templates and configurations
  - `writing-agents/` - AI agents for content writing and analysis (see AGENTS.md for details)
    - `outline-designer.prompt.md` - Creates structured content outlines
    - `writer.prompt.md` - Generates complete technical content from outlines
    - `po-writer.prompt.md` - Quality assurance and style compliance review
    - `analyst-writer.prompt.md` - Research, analyze, and synthesize content
    - Agent templates in `templates/` directory
  - See AGENTS.md for detailed agent documentation and usage patterns

- `skills/` - Main skill implementations
  - Currently contains `link-extractor/` skill for extracting and processing links
  - `references/` directory contains style examples and documentation

- `docs/daily-links/` - Repository for daily link summaries in markdown format

- `examples/` - Contains markdown best practices documentation

### Link Extractor Skill

The `link-extractor` skill is designed to extract links from content (primarily Weibo posts) and process them into various output formats. The skill references several daily link styles:

- `github-repo` - GitHub repository style
- `official-blog` - Official blog style
- `concept-style` - Concept explanation style
- `icon-single-line` - Icon-based single line style
- `bullets-summary` - Bullet point summary style

These styles provide different ways to format extracted links for daily link documentation.

## Development Guidelines

### Cursor Rules (From .cursorrules)
- For project-level questions, read `.cursorrules.md` for workspace architecture and tool usage
- For skill-specific questions, read the corresponding `README.md` in each skill directory
- Use `ls -R` or `find` to explore directory structure when needed
- Prioritize reading documentation files before exploring code

### Git Configuration
- No commits should be made unless explicitly requested
- All changes must be thoroughly reviewed before committing
- When working with the repository, ensure clean git state (no uncommitted changes)

### File Organization
- Daily link files follow the pattern: `docs/daily-links/YYYY-MM-DD.md`
- Each markdown file uses level-2 headings (##) for link categories
- Sections are separated by horizontal rules (---)
- Empty sections are automatically removed by the formatting script

### Content Processing
The `format-daily-links.sh` script:
1. Removes sections that contain only whitespace or horizontal rules
2. Normalizes blank lines (single blank lines between sections)
3. Maintains the original header line
4. Preserves section structure with separators
5. Trims trailing whitespace from lines

## Writing Agent Workflow

For content creation using the writing agents pipeline:

1. **Start with Outline Designer** - Provide a topic to create a structured outline
2. **Use Writer** - Expand the outline into full content
3. **PO-Writer Review** - Quality gate before publication
4. **Iterate if needed** - Return to Writer with specific feedback if rejected

See AGENTS.md for detailed agent descriptions, workflows, and best practices.

## Key Technologies

- Bash scripting for automation
- AWK for text processing and formatting
- Markdown for documentation
- Git for version control
- Claude/Code AI agents for content creation