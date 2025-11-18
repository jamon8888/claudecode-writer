# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# Content Creation System v2.0

## System Overview
This workspace is a complete content workflow engine powered by Claude Code:
1. **Raw notes** → Theme extraction → Research → Long-form article → Multi-platform versions
2. **Skills system** provides reusable capabilities (analysis, SEO, voice matching)
3. **Hooks system** automates workflows (quality checks, repurposing, scheduling)
4. **Agents** handle platform-specific optimization
5. **All content** preserved in organized directory structure

## Architecture
See ARCHITECTURE.md for complete plugin system documentation.

## Workflow Commands

### Core Workflow (Enhanced in v2.0)
- `/extract-themes` - Analyze raw notes to identify patterns (NOW: uses trend detection, auto-saves)
- `/research [topic]` - Comprehensive research (NOW: uses research-aggregator skill, fact-checking)
- `/write [topic]` - Create article (NOW: auto-triggers post-write hook for full automation)

### New Commands in v2.0
- `/optimize [file]` - Comprehensive content optimization (quality, SEO, voice)
- `/quick-post [platform] [idea]` - Rapid single-platform content creation
- `/analyze-performance` - Review published content performance
- `/schedule [file] [date] [platform]` - Schedule publication

## Skills System (NEW in v2.0)
Reusable capabilities invoked by commands and hooks:
- **content-analyzer**: Quality, readability, structure analysis
- **voice-matcher**: Brand voice consistency validation
- **seo-optimizer**: Search engine optimization
- **research-aggregator**: Multi-source research synthesis

## Hooks System (NEW in v2.0)
Event-driven automation:
- **post-write**: Auto-repurposes to ALL platforms after /write command
- **quality-check**: Validates content quality before saving
- **daily-digest**: Daily workflow summary (scheduled)
- **voice-validation**: Ensures brand voice consistency

## Context Architecture
Always reference these for consistency:
- @context/writing-examples.md - Real examples demonstrating voice and style
- @context/research-sources.md - Priority sources to check FIRST during research
- @context/brand-guidelines.md - Brand voice, tone, values, standards (NEW)
- @context/seo-keywords.md - SEO strategy and keyword targets (NEW)

## Agent Specializations
- `linkedin-repurposer`: Professional networking optimization
- `newsletter-repurposer`: Email engagement specialist
- `conversational-repurposer`: Social media posts and podcast Q&A scripts

## Directory Structure
```
content/
├── rawnotes/      # Unprocessed ideas and notes
├── research/      # Research briefs and theme analyses
├── drafts/        # Work in progress
├── ready/         # Ready to publish
├── published/     # Published content
└── archive/       # Archived content
```

## Configuration
Plugin settings in `.claudecode-writer/config.yml`:
- Feature flags (skills, hooks, workflows, analytics)
- Workflow automation preferences
- Quality thresholds
- Platform connections
- Hook scheduling

## Key Workflows

### Complete Article Creation
```
/write "topic"
  ↓ [AUTO-TRIGGERED by post-write hook]
- Creates article in content/drafts/
- Generates LinkedIn version
- Generates newsletter version
- Generates social media version
- Runs quality analysis
- Runs SEO optimization
- Runs voice validation
- Suggests assets and schedule
- Creates comprehensive summary

All outputs saved to content/drafts/ with consistent naming.
```

### Quick Content Creation
```
/quick-post linkedin "idea"
  ↓
- Develops idea into platform-optimized post
- Runs quality checks
- Predicts engagement
- Saves to content/ready/
```

## Development Guidelines
- Never duplicate context information - always reference source files
- Maintain consistency across all generated formats
- Skills are reusable - invoke them rather than duplicating logic
- Hooks automate repetitive tasks - don't manually repeat hook actions
- Content quality gates validate against brand guidelines before output
- All file operations use consistent naming convention
- Workflows orchestrate complex multi-step processes

## Automation Features
When `workflow_automation.post_write_repurpose: true` (default):
- /write command automatically generates ALL platform versions
- Quality checks run automatically
- SEO optimization applied automatically
- Voice validation performed automatically
- Comprehensive reports generated

This eliminates manual repurposing steps from v1.0.

## Migration from v1.0
See MIGRATION.md for complete upgrade guide.
Key changes:
- Content folders moved to `content/` directory
- New configuration system
- Enhanced commands with auto-repurposing
- New skills and hooks systems

## For More Information
- **Complete Architecture**: See ARCHITECTURE.md
- **Migration Guide**: See MIGRATION.md
- **Contributing**: See CONTRIBUTING.md
- **Changelog**: See CHANGELOG.md
