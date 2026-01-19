# AGENTS.md

This document describes the available AI agents in the `agents/writing-agents/` directory for content creation and review workflows.

## Writing Agents Pipeline

The writing agents implement a multi-stage content creation workflow, particularly designed for OneV-style technical writing. Each agent has a specific role in the pipeline.

### 1. Outline Designer (outline-designer.prompt.md)

**Purpose:** Creates structured content outlines for technical writing

**Input:** Topic or writing prompt

**Process:**
- Research the topic and identify key concepts
- Create a structured outline with clear sections
- Define Non-Functional Requirements (NFRs) and engineering constraints
- Identify trade-offs and limitations to be discussed
- Establish writing goals and scope

**Output:** A structured markdown outline with:
- Clear hierarchy of sections
- Notes on engineering constraints and NFRs
- Trade-offs and limitations to address

**Usage:** First stage in the writing pipeline - use this to create a solid foundation before writing.

### 2. Writer (writer.prompt.md)

**Purpose:** Generates complete technical content based on an outline

**Input:**
- Outline from Outline Designer
- Any additional context or requirements

**Process:**
- Expand the outline into full technical content
- Focus on "why" rather than tutorial-style "how"
- Incorporate engineering constraints and NFRs
- Discuss trade-offs and acknowledge limitations
- Maintain a measured, non-dogmatic tone
- Avoid marketing language and get to the point

**Output:** Complete technical draft in markdown format that:
- Follows the outline structure strictly
- Explains reasoning and trade-offs
- Meets all defined constraints and goals

**Usage:** Second stage in the pipeline - takes the outline and creates a full draft.

### 3. PO-Writer / Style Reviewer (po-writer.prompt.md)

**Purpose:** Quality assurance and style compliance review

**Input:**
- Draft content (markdown)
- Corresponding outline (optional)

**Review Checklist:**
- ✓ Explains "why" (not tutorialized)
- ✓ Clearly states engineering constraints and non-functional goals
- ✓ Acknowledges trade-offs and limitations
- ✓ Maintains measured, non-dogmatic tone (no marketing speak)
- ✓ Strictly follows outline structure (no unauthorized additions/deletions)

**Output:**
- Conclusion: Either "✅ Ready to publish" or "❌ Needs revision"
- If revision needed: Specific issues with actionable suggestions
- Style feedback: One-sentence summary of style deviations or strengths

**Usage:** Final stage in the pipeline - quality gate before publication. If rejected, return to Writer for revisions.

### 4. Analyst-Writer (analyst-writer.prompt.md)

**Purpose:** Research, analyze, and synthesize content from multiple sources

**Input:** Research topic or source materials

**Process:**
- Research and analyze the topic
- Synthesize findings with logical flow
- Maintain objective, analytical tone
- Cross-validate conclusions with multiple sources

**Output:** Analytical content that:
- Provides deep research synthesis
- Maintains logical coherence
- Presents balanced, well-supported conclusions

**Usage:** Standalone agent for research-heavy content or when deep analysis is required.

## Agent Templates

### Available Templates

The `agents/writing-agents/templates/` directory contains reusable templates:

- **onev-style-outline.md** - Template for OneV-style technical writing outlines

### Template Usage

Templates provide consistent structure for agent outputs. When creating new outlines or content, refer to these templates for formatting guidelines.

## Workflow Patterns

### Standard Three-Stage Pipeline

```
Outline Designer → Writer → PO-Writer
     ↓              ↓          ↓
   Outline      Draft     Review/Approval
```

### Research-Heavy Content

```
Analyst-Writer → Writer → PO-Writer
     ↓              ↓          ↓
   Research     Draft     Review/Approval
```

## Best Practices

1. **Always start with an outline** - The Outline Designer ensures structured thinking and clear constraints
2. **Use PO-Writer as quality gate** - Don't skip the final review step
3. **Iterate if needed** - If PO-Writer rejects content, provide specific feedback to Writer
4. **Maintain conversation flow** - Keep the original outline and previous outputs in context when progressing through agents
5. **Follow the strict output formats** - Each agent has specific output requirements that should be followed exactly

## Agent Invocation

When using these agents with Claude Code or similar tools:

1. Reference the appropriate `.prompt.md` file
2. Provide the required input format
3. Include previous outputs in context when progressing through the pipeline
4. Follow the specified output format requirements

## File Locations

- Agent definitions: `agents/writing-agents/*.prompt.md`
- Templates: `agents/writing-agents/templates/`
- Usage documentation: `AGENTS.md` (this file)
- Reference in main docs: `CLAUDE.md`
