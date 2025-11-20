# ClaudeCode Writer v2.0

**A complete content workflow engine for Claude Code** - Transform ideas into multi-platform content with automated research, writing, optimization, and repurposing.

[![Version](https://img.shields.io/badge/version-2.0.0-blue.svg)](CHANGELOG.md)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-purple.svg)](https://claude.ai/code)

## 🚀 What This Does

ClaudeCode Writer is a **full-featured plugin** that turns Claude Code into your personal content creation system:

- 📝 **One command** creates an article + LinkedIn post + newsletter + social media content
- 🎯 **Skills system** provides reusable capabilities (analysis, SEO, voice matching)
- 🔄 **Hooks system** automates workflows (quality checks, repurposing, scheduling)
- 🤖 **AI-powered** research, optimization, and multi-platform adaptation
- 📊 **Quality gates** ensure consistent brand voice and standards
- 🎨 **Learns your voice** from examples to maintain authenticity

### What's New in v2.0

✨ **Automated repurposing** - `/write` now creates ALL platform versions automatically
✨ **Quality checks** - Auto-validates content before saving
✨ **SEO optimization** - Built-in search engine optimization
✨ **Voice consistency** - Ensures brand voice across all platforms
✨ **Workflow engine** - Orchestrate complex multi-step processes
✨ **Configuration system** - Centralized settings and feature flags

## 🎯 Perfect For

- **Content Creators**: Create once, publish everywhere
- **Thought Leaders**: Build consistent presence across platforms
- **Newsletter Writers**: Repurpose content efficiently
- **Marketing Teams**: Maintain brand voice at scale
- **Solopreneurs**: Maximize content ROI

## ⚡ Quick Start

### 1. Install as GitHub Template

Click the green **"Use this template"** button on GitHub, or:

```bash
# Clone the repository
git clone https://github.com/jamon8888/claudecode-writer.git my-content-workspace
cd my-content-workspace

# Or use as template
gh repo create my-content-workspace --template jamon8888/claudecode-writer
```

### 2. Install Claude Code

If you haven't already:

```bash
# Mac (Homebrew)
brew install anthropics/claude/claude-code

# Or visit https://claude.ai/code for other platforms
```

### 3. Initialize Your Workspace

```bash
# Navigate to your workspace
cd my-content-workspace

# Start Claude Code
claude

# In Claude Code, customize your setup:
# 1. Add your writing examples to context/writing-examples.md
# 2. Add your research sources to context/research-sources.md
# 3. (Optional) Customize .claudecode-writer/config.yml
```

### 4. Start Creating!

```bash
# Create a complete content suite
/write "why remote work productivity advice fails"

# Result: Article + LinkedIn + Newsletter + Social versions
# All saved to content/drafts/ with quality reports
```

## 🎬 The v2.0 Workflow

### Before v2.0 (Manual)
```
/write "topic"
→ Get article
→ Manually repurpose to LinkedIn
→ Manually repurpose to Newsletter
→ Manually repurpose to Social
→ Manually check quality
→ Manually optimize SEO
```

### After v2.0 (Automated)
```
/write "topic"
  ↓ [AUTO-TRIGGERED]
- ✅ Creates article in content/drafts/
- ✅ Generates LinkedIn version
- ✅ Generates newsletter version
- ✅ Generates social media version
- ✅ Runs quality analysis (87/100)
- ✅ Performs SEO optimization
- ✅ Validates voice consistency
- ✅ Suggests assets and schedule
- ✅ Creates comprehensive summary

Done in ~30 seconds!
```

## 📚 Core Commands

### Content Creation
```bash
/write [topic]              # Create article + all platform versions (automated)
/quick-post [platform]      # Rapid single-platform post
/research [topic]           # Comprehensive research with fact-checking
/extract-themes             # Analyze raw notes for content ideas
```

### Content Optimization
```bash
/optimize [file]            # Improve quality, SEO, voice
/analyze-performance        # Review published content metrics
/schedule [file] [date]     # Schedule publication
```

### Full command reference in [ARCHITECTURE.md](ARCHITECTURE.md)

## 🎯 Skills System

Reusable capabilities that power commands and hooks:

- **content-analyzer** - Quality, readability, structure analysis
- **voice-matcher** - Brand voice consistency validation
- **seo-optimizer** - Search engine optimization
- **research-aggregator** - Multi-source research synthesis

Skills are invoked automatically or manually via commands.

## 🔄 Hooks System

Event-driven automation:

- **post-write** - Auto-repurposes to all platforms after `/write`
- **quality-check** - Validates content before saving
- **daily-digest** - Scheduled workflow summary
- **voice-validation** - Ensures brand consistency

Configure hooks in `.claudecode-writer/config.yml`

## ⚙️ Configuration

Customize your workflow in `.claudecode-writer/config.yml`:

```yaml
# Enable/disable features
features:
  enabled:
    - skills
    - hooks
    - workflows
    - analytics

# Workflow automation
workflow_automation:
  post_write_repurpose: true    # Auto-repurpose after /write
  auto_quality_check: true       # Run quality checks
  auto_seo_optimize: true        # Optimize for SEO

# Quality thresholds
quality:
  readability:
    min_score: 60
  voice:
    similarity_threshold: 0.7
```

## 📁 Directory Structure

```
.claudecode-writer/          # Plugin configuration
├── config.yml              # Central settings
└── cache/                  # Performance cache

.claude/
├── skills/                 # Reusable capabilities
│   └── core/              # Analysis, SEO, voice, research
├── hooks/                  # Event automation
│   ├── post/              # After-action hooks
│   ├── quality/           # Quality assurance
│   └── workflow/          # Scheduled tasks
├── commands/               # User-facing commands
├── agents/                 # Platform specialists
└── workflows/              # Multi-step orchestration

content/
├── rawnotes/              # Unprocessed ideas
├── research/              # Research briefs
├── drafts/                # Work in progress
├── ready/                 # Ready to publish
├── published/             # Published content
└── archive/               # Archived content

context/
├── writing-examples.md    # Your voice samples (customize!)
├── research-sources.md    # Priority sources (customize!)
├── brand-guidelines.md    # Brand voice & standards
└── seo-keywords.md        # SEO strategy
```

## 🎓 Examples

### Example 1: Complete Article Pipeline

```bash
# 1. Add raw ideas to content/rawnotes/
# 2. Extract themes
/extract-themes

# 3. Research the topic
/research "energy management for remote workers"

# 4. Write article (automatic repurposing)
/write "energy management for remote workers"

# Result:
# ✓ content/drafts/article-energy-management-2024-11-18.md
# ✓ content/drafts/linkedin-energy-management-2024-11-18.md
# ✓ content/drafts/newsletter-energy-management-2024-11-18.md
# ✓ content/drafts/social-energy-management-2024-11-18.md
# ✓ content/drafts/quality-report-energy-management-2024-11-18.md
# ✓ content/drafts/seo-report-energy-management-2024-11-18.md
# ✓ content/drafts/summary-energy-management-2024-11-18.md
```

### Example 2: Quick Social Post

```bash
/quick-post linkedin "Time blocking doesn't work for remote workers"

# Result: Optimized LinkedIn post ready to publish
# Saved to: content/ready/linkedin-time-blocking-2024-11-18.md
```

### Example 3: Optimize Existing Content

```bash
/optimize content/drafts/article-productivity-2024-11-18.md

# Result: Comprehensive optimization with recommendations
# - Readability improvements
# - SEO enhancements
# - Voice adjustments
# - Structure fixes
```

## 🎨 Customization

### 1. Add Your Voice (Essential!)

Edit `context/writing-examples.md`:
- Add 2-3 examples of your LinkedIn posts
- Add 1-2 examples of your newsletter
- Add examples of your social media posts

The more examples you provide, the better Claude matches your voice.

### 2. Add Your Research Sources

Edit `context/research-sources.md`:
- Add your favorite newsletters
- Add industry publications
- Add expert blogs

Claude will check these sources FIRST during research.

### 3. Define Your Brand

Edit `context/brand-guidelines.md`:
- Define your brand voice attributes
- Set content standards
- Specify vocabulary preferences

### 4. Configure SEO

Edit `context/seo-keywords.md`:
- Add primary keywords
- Define topic clusters
- Set SEO strategy

## 🚀 Advanced Features

### Workflow Orchestration

Create custom workflows in `.claude/workflows/`:

```yaml
name: quick-social
steps:
  - research
  - quick-post
  - schedule
```

### Custom Skills

Add your own skills in `.claude/skills/`:

```markdown
---
name: my-custom-skill
description: Does something amazing
---

# My Custom Skill
[Your skill logic]
```

### Custom Hooks

Add automation in `.claude/hooks/`:

```markdown
---
name: my-hook
trigger: after_write
---

# My Hook
[Your automation logic]
```

## 📖 Documentation

- **[ARCHITECTURE.md](ARCHITECTURE.md)** - Complete plugin architecture
- **[MIGRATION.md](MIGRATION.md)** - Upgrade from v1.0
- **[CHANGELOG.md](CHANGELOG.md)** - Version history
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - Contribution guide

## 🆘 Troubleshooting

### "Content doesn't match my voice"
→ Add more examples to `context/writing-examples.md`

### "Quality checks too strict"
→ Adjust thresholds in `.claudecode-writer/config.yml`

### "Hooks not running"
→ Verify `features.enabled: [hooks]` in config

### "Research feels generic"
→ Add specific sources to `context/research-sources.md`

## 🤝 Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for:
- How to improve skills and workflows
- Testing requirements
- Submission process

## 📜 License

MIT License - See [LICENSE](LICENSE) file

## 🙏 Acknowledgments

Built for the Claude Code community by content creators, for content creators.

## 🔗 Links

- **Documentation**: [Full docs](ARCHITECTURE.md)
- **Issues**: [Report bugs](https://github.com/jamon8888/claudecode-writer/issues)
- **Discussions**: [Community forum](https://github.com/jamon8888/claudecode-writer/discussions)
- **Claude Code**: [Official site](https://claude.ai/code)

---

**Ready to 10x your content creation?** Get started now! 🚀

```bash
# Use this template
gh repo create my-content-workspace --template jamon8888/claudecode-writer
cd my-content-workspace
claude

# Start creating
/write "your first topic"
```
