# Changelog

All notable changes to ClaudeCode Writer will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2024-11-18

### Added - Major Plugin Architecture Revamp

#### Skills System
- **content-analyzer**: Comprehensive quality, readability, structure, and engagement analysis
- **voice-matcher**: Brand voice consistency validation with detailed scoring
- **seo-optimizer**: Complete SEO optimization with keyword strategy and on-page optimization
- **research-aggregator**: Multi-source research with credibility assessment and synthesis

#### Hooks System
- **post-write**: Auto-repurposes content to ALL platforms after `/write` command
- **quality-check**: Validates content quality before saving (configurable thresholds)
- **daily-digest**: Scheduled daily workflow summary and recommendations
- **voice-validation**: Ensures brand voice consistency

#### New Commands
- `/optimize [file]`: Comprehensive content optimization (quality, SEO, voice, readability)
- `/quick-post [platform] [idea]`: Rapid single-platform content creation without full workflow
- `/analyze-performance`: Review published content performance and analytics
- `/schedule [file] [date] [platform]`: Content scheduling and calendar management

#### Workflows
- **article-pipeline**: Complete orchestrated workflow from research to multi-platform publication
- **quick-social**: Rapid social media post creation and optimization
- **weekly-planning**: Automated content planning and gap analysis

#### Configuration System
- Centralized configuration in `.claudecode-writer/config.yml`
- Feature flags for skills, hooks, workflows, analytics
- Workflow automation preferences
- Quality thresholds (readability, SEO, voice)
- Platform connection settings
- Hook scheduling and management

#### Directory Structure
- Reorganized content into `content/` directory with subdirectories:
  - `content/rawnotes/` - Unprocessed ideas
  - `content/research/` - Research briefs
  - `content/drafts/` - Work in progress
  - `content/ready/` - Ready to publish
  - `content/published/` - Published content
  - `content/archive/` - Archived content
- Created `.claudecode-writer/` for plugin configuration and state
- Added `analytics/` for performance tracking
- Added `assets/` for media files

#### Context Files
- `context/brand-guidelines.md` - Comprehensive brand voice and content standards
- `context/seo-keywords.md` - SEO strategy and keyword targeting

#### Documentation
- `ARCHITECTURE.md` - Complete plugin architecture documentation
- `MIGRATION.md` - v1.0 to v2.0 migration guide
- `CHANGELOG.md` - Version history and changes
- Updated `CLAUDE.md` with v2.0 features and workflows
- Updated `README.md` with new capabilities

### Enhanced - Existing Features

#### Commands
- `/extract-themes` - Now uses trend detection and auto-saves results
- `/research` - Now uses research-aggregator skill with fact-checking
- `/write` - Now auto-triggers post-write hook for complete automation

#### Workflow Automation
- `/write` command now automatically:
  - Creates LinkedIn, Newsletter, and Social versions
  - Runs quality analysis
  - Performs SEO optimization
  - Validates voice consistency
  - Generates asset suggestions
  - Provides schedule recommendations
  - Creates comprehensive summary

#### File Management
- Consistent file naming convention across all generated content
- Automatic organization by content type and status
- Metadata tracking for all content

### Changed

#### Directory Structure
- **BREAKING**: Content folders moved from root to `content/` directory
  - `rawnotes/` → `content/rawnotes/`
  - `research/` → `content/research/`
  - `drafts/` → `content/drafts/`

#### Configuration
- **BREAKING**: New centralized configuration system
- Settings previously implicit now explicit in `config.yml`
- All features opt-in via configuration

#### Workflow Behavior
- `/write` command now triggers full automation by default
- Manual repurposing no longer required (but still available)
- Quality gates can block content saves (configurable)

### Deprecated
None (all v1.0 features still supported)

### Removed
None (backward compatible with v1.0)

### Fixed
- Improved error handling in all workflows
- Better file path management
- Consistent naming across all generated files

### Security
- API keys stored in environment variables only
- No credentials in configuration files
- Content stays local by default
- Analytics opt-in only

## [1.0.0] - 2024-11-01

### Added - Initial Release

#### Core Commands
- `/extract-themes` - Analyze raw notes to identify content themes
- `/research [topic]` - Comprehensive research workflow
- `/write` - Create long-form articles

#### Agents
- `linkedin-repurposer` - LinkedIn content optimization
- `newsletter-repurposer` - Email newsletter optimization
- `conversational-repurposer` - Social media and podcast content

#### Context
- `context/writing-examples.md` - Voice and style examples
- `context/research-sources.md` - Priority research sources

#### Documentation
- `README.md` - Getting started guide
- `CLAUDE.md` - System instructions
- `CONTRIBUTING.md` - Contribution guidelines
- `LICENSE` - MIT license

#### Directory Structure
- `rawnotes/` - Raw ideas and notes
- `research/` - Research outputs
- `drafts/` - Content drafts

### Workflow
- Manual workflow: extract themes → research → write → manually repurpose
- Each platform version created by explicitly invoking agents

---

## Migration Guide

For upgrading from v1.0 to v2.0, see [MIGRATION.md](MIGRATION.md).

## Versioning

We use [Semantic Versioning](https://semver.org/):
- **MAJOR** version for incompatible API changes
- **MINOR** version for added functionality (backwards compatible)
- **PATCH** version for backwards compatible bug fixes

## Links

- [Homepage](https://github.com/jamon8888/claudecode-writer)
- [Issue Tracker](https://github.com/jamon8888/claudecode-writer/issues)
- [Documentation](https://github.com/jamon8888/claudecode-writer/blob/main/README.md)
