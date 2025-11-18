# ClaudeCode Writer v2.0 - Plugin Architecture

Complete architectural documentation for the ClaudeCode Writer content workflow engine.

## Overview

ClaudeCode Writer v2.0 is a comprehensive plugin system that transforms Claude Code into a full-featured content workflow engine, automating everything from research to multi-platform publication.

### What's New in v2.0

- **Skills System**: Reusable capabilities (content analysis, SEO, voice matching)
- **Hooks System**: Event-driven automation (quality checks, auto-repurposing)
- **Enhanced Commands**: New commands for optimization, quick posting, analytics
- **Workflow Engine**: Orchestrate complex multi-step workflows
- **Configuration System**: Centralized settings and feature flags
- **Analytics & Tracking**: Performance monitoring and insights
- **Enhanced Context**: Brand guidelines, SEO keywords, audience profiles

## System Architecture

```
claudecode-writer/
├── .claudecode-writer/          # Plugin Core
│   ├── config.yml               # Central configuration
│   ├── state.json               # Runtime state
│   └── cache/                   # Performance cache
│
├── .claude/                     # Claude Code Integration
│   ├── skills/                  # Reusable Capabilities
│   │   ├── core/               # Content analysis, voice, SEO, research
│   │   ├── platform/           # Platform-specific optimization
│   │   ├── workflow/           # Workflow management
│   │   └── ai/                 # AI-powered features
│   │
│   ├── commands/               # User-Facing Commands
│   │   ├── extract-themes.md
│   │   ├── research.md
│   │   ├── write.md
│   │   ├── optimize.md        # NEW
│   │   └── quick-post.md      # NEW
│   │
│   ├── agents/                 # Platform Specialists
│   │   ├── linkedin-repurposer.md
│   │   ├── newsletter-repurposer.md
│   │   └── conversational-repurposer.md
│   │
│   ├── hooks/                  # Event Automation
│   │   ├── pre/               # Before-action hooks
│   │   ├── post/              # After-action hooks
│   │   ├── quality/           # Quality assurance
│   │   ├── workflow/          # Scheduled workflows
│   │   └── integrations/      # External integrations
│   │
│   ├── templates/              # Content Templates
│   │   ├── articles/
│   │   ├── posts/
│   │   └── workflows/
│   │
│   └── workflows/              # Workflow Definitions
│       ├── article-pipeline.yml
│       ├── quick-social.yml
│       └── weekly-planning.yml
│
├── context/                    # Knowledge Base
│   ├── writing-examples.md    # Voice samples
│   ├── research-sources.md    # Priority sources
│   ├── brand-guidelines.md    # Brand voice & standards
│   └── seo-keywords.md        # SEO strategy
│
├── content/                    # Content Files
│   ├── rawnotes/              # Unprocessed ideas
│   ├── research/              # Research briefs
│   ├── drafts/                # Work in progress
│   ├── ready/                 # Ready to publish
│   ├── published/             # Published content
│   └── archive/               # Archived content
│
├── analytics/                  # Performance Tracking
│   ├── reports/               # Generated reports
│   ├── insights/              # AI insights
│   └── benchmarks/            # Performance benchmarks
│
└── assets/                     # Media Files
    ├── images/
    ├── videos/
    └── graphics/
```

## Core Systems

### 1. Skills System

Reusable capabilities that power commands, hooks, and workflows.

#### Core Skills
- **content-analyzer**: Quality, readability, structure analysis
- **voice-matcher**: Brand voice consistency validation
- **seo-optimizer**: Search engine optimization
- **research-aggregator**: Multi-source research synthesis

#### Platform Skills
- **platform-formatter**: Dynamic platform formatting
- **hashtag-generator**: Smart hashtag selection
- **image-suggester**: Relevant image recommendations
- **link-optimizer**: Link tracking and optimization

#### Workflow Skills
- **content-scheduler**: Publication scheduling
- **approval-manager**: Review workflows
- **performance-tracker**: Analytics tracking

Skills are invoked by:
- Commands (e.g., /optimize uses seo-optimizer)
- Hooks (e.g., quality-check uses content-analyzer)
- Workflows (e.g., article-pipeline uses multiple skills)

### 2. Hooks System

Event-driven automation that runs at specific points in the workflow.

#### Hook Types

**Pre Hooks** (Before Actions):
- `pre-write`: Validate prerequisites
- `pre-research`: Check sources
- `pre-extract-themes`: Validate raw notes exist

**Post Hooks** (After Actions):
- `post-write`: Auto-repurpose to all platforms
- `post-research`: Save and organize
- `post-repurpose`: Optimize and schedule

**Quality Hooks** (Validation):
- `quality-check`: Content quality validation
- `voice-validation`: Voice consistency
- `seo-check`: SEO validation
- `fact-check`: Claim verification

**Workflow Hooks** (Scheduled):
- `daily-digest`: Daily summary (09:00)
- `weekly-planning`: Content planning (Mon 09:00)
- `performance-sync`: Sync analytics (daily)
- `archive-cleanup`: Archive old content (weekly)

**Integration Hooks** (External):
- `publish-to-linkedin`: Auto-publish
- `publish-to-substack`: Newsletter publishing
- `publish-to-twitter`: Tweet posting
- `sync-analytics`: Platform analytics

#### Hook Configuration

```yaml
hooks:
  post_write:
    - auto-repurpose-all
    - seo-optimize
    - generate-thumbnails

  scheduled:
    daily_digest:
      time: "09:00"
      enabled: true
```

### 3. Commands System

User-facing workflows accessible via `/command`.

#### Existing Commands (Enhanced)

**`/extract-themes`**
- NOW: Uses trend-detector skill
- NOW: Auto-saves to research/
- NOW: Suggests immediate actions

**`/research [topic]`**
- NOW: Uses research-aggregator skill
- NOW: Fact-checking integration
- NOW: Competitive analysis
- NOW: Auto-saves structured brief

**`/write [topic]`**
- NOW: Voice-matcher integration
- NOW: SEO-optimizer integration
- NOW: Auto-repurposes to ALL platforms
- NOW: Quality checks before save

#### New Commands

**`/optimize [file]`**
- Comprehensive content optimization
- SEO, voice, readability improvements
- Before/after comparisons
- Apply changes selectively

**`/quick-post [platform] [idea]`**
- Rapid single-platform posting
- Skip full article workflow
- Optimized for timely content
- Engagement prediction

**`/analyze-performance`**
- Review published content performance
- Platform-specific analytics
- Trend identification
- Recommendations

**`/schedule [file] [date] [platform]`**
- Content scheduling
- Calendar management
- Optimal timing suggestions

### 4. Workflow Engine

Orchestrates multi-step processes.

#### Article Pipeline Workflow

```yaml
Research → Write → Quality Check → SEO → Voice Check →
Repurpose All → Assets → Schedule → Summary
```

**Execution**:
```
/workflow article-pipeline "remote work productivity"
```

**Features**:
- Parallel execution where possible
- Quality gates (must pass thresholds)
- Error handling (continue on non-critical)
- Comprehensive reporting

#### Quick Social Workflow

```yaml
Idea → Platform Agent → Quality Check → Engagement Prediction →
Schedule Suggestion
```

**Execution**:
```
/workflow quick-social linkedin "productivity advice failing"
```

### 5. Configuration System

Centralized settings in `.claudecode-writer/config.yml`.

#### Key Configuration Areas

**Feature Flags**:
```yaml
features:
  enabled:
    - skills
    - hooks
    - workflows
    - analytics
```

**Workflow Automation**:
```yaml
workflow_automation:
  post_write_repurpose: true
  auto_quality_check: true
  auto_seo_optimize: true
```

**Platform Connections**:
```yaml
platforms:
  linkedin:
    enabled: true
    auto_publish: false
```

**Quality Thresholds**:
```yaml
quality:
  readability:
    min_score: 60
  voice:
    similarity_threshold: 0.7
```

## Content Workflow

### Complete Article Creation Flow

1. **Capture Ideas** → Add to `content/rawnotes/`

2. **Extract Themes** → `/extract-themes`
   - Analyzes all raw notes
   - Identifies patterns
   - Saves to `content/research/theme-analysis-[date].md`

3. **Research Topic** → `/research [theme]`
   - Checks priority sources FIRST
   - Broader web research
   - Competitive analysis
   - Saves to `content/research/research-brief-[slug]-[date].md`

4. **Write Article** → `/write [topic]`
   - Creates comprehensive article
   - Saves to `content/drafts/article-[slug]-[date].md`
   - **AUTO-TRIGGERS post-write hook:**
     - Repurposes to LinkedIn, Newsletter, Social
     - Runs quality analysis
     - SEO optimization
     - Voice validation
     - Asset suggestions
     - Schedule recommendations
     - Creates summary

5. **Review & Optimize** → `/optimize [file]`
   - Comprehensive analysis
   - Recommended improvements
   - Apply optimizations

6. **Schedule & Publish** → `/schedule [file] [date] [platform]`
   - Add to content calendar
   - Publish at optimal times
   - Track performance

### Quick Post Flow (Timely Content)

1. **Quick Post** → `/quick-post linkedin [idea]`
   - Develops idea
   - Uses platform agent
   - Quality checks
   - Engagement prediction
   - Saves to `content/ready/`

2. **Review & Publish**
   - Quick review
   - Publish immediately or schedule

## Integration Points

### Skills ↔ Commands
Commands invoke skills for specific capabilities:
- `/optimize` → content-analyzer, seo-optimizer, voice-matcher
- `/write` → voice-matcher, seo-optimizer (via hooks)
- `/research` → research-aggregator, trend-detector

### Hooks ↔ Commands
Hooks trigger automatically around commands:
- **Before** `/write`: quality-check, voice-validation
- **After** `/write`: post-write (repurpose all)
- **After** `/research`: post-research (save and organize)

### Workflows ↔ Everything
Workflows orchestrate commands, skills, hooks:
- Call commands in sequence
- Invoke skills directly
- Respect hook triggers
- Parallel execution

### Agents ↔ Platform Content
Agents specialize in platform optimization:
- `linkedin-repurposer` → Professional posts
- `newsletter-repurposer` → Email content
- `conversational-repurposer` → Social & podcast

## Data Flow

### Content Creation
```
Raw Idea (rawnotes/)
  ↓
Theme Extraction (research/theme-analysis-*.md)
  ↓
Research Brief (research/research-brief-*.md)
  ↓
Article (drafts/article-*.md)
  ↓ [post-write hook]
Platform Versions (drafts/linkedin-*, newsletter-*, social-*)
  ↓
Optimization (via /optimize)
  ↓
Ready to Publish (ready/)
  ↓
Published (published/)
  ↓
Archive (archive/) [after 30 days]
```

### Quality Assurance Flow
```
Content Created
  ↓
Quality Check Hook
  ├→ Readability Analysis
  ├→ Grammar Check
  ├→ Structure Validation
  └→ Voice Matching
  ↓
Score Calculation
  ↓
Decision (Pass/Warn/Block)
  ↓
Save with Status
```

### Workflow Orchestration
```
Workflow Started
  ↓
Step 1: Research
  ↓ [outputs: research brief]
Step 2: Write
  ↓ [outputs: article]
  ├→ Quality Gate (min 70/100)
  ↓
Step 3: Optimization
  ↓ [parallel execution]
  ├→ SEO Optimization
  ├→ Voice Check
  └→ Asset Generation
  ↓
Step 4: Repurposing
  ↓ [parallel execution]
  ├→ LinkedIn Version
  ├→ Newsletter Version
  └→ Social Version
  ↓
Step 5: Summary & Notification
```

## Performance Optimizations

### Parallel Execution
- Repurposing agents run simultaneously
- Multiple quality checks in parallel
- Workflow steps with no dependencies execute together

### Caching
- Voice profile cached (5 min)
- Quality check results cached
- Research sources indexed

### Incremental Operations
- Only analyze changed content
- Reuse previous analysis where applicable
- Smart file watching

## Extension Points

### Adding New Skills
1. Create skill file in `.claude/skills/[category]/`
2. Define capabilities and output format
3. Reference in commands/hooks/workflows
4. Update config if needed

### Adding New Hooks
1. Create hook file in `.claude/hooks/[type]/`
2. Define trigger and actions
3. Add to config.yml hooks section
4. Test with relevant commands

### Adding New Commands
1. Create command file in `.claude/commands/`
2. Define usage and process
3. Integrate skills/agents as needed
4. Document in README

### Adding New Workflows
1. Create workflow YAML in `.claude/workflows/`
2. Define steps and dependencies
3. Set quality gates
4. Test end-to-end

## Security & Privacy

### API Keys
- Stored in environment variables
- Never committed to git
- Referenced in config as `${ENV_VAR}`

### Content Privacy
- All content stays local
- No external sharing without explicit command
- Analytics opt-in only

### Hook Safety
- Hooks can't execute arbitrary code
- Validated against allowed operations
- Can be disabled globally or individually

## Troubleshooting

### Common Issues

**Hooks not running**:
- Check `config.yml` hooks enabled
- Verify hook file in correct directory
- Check hook trigger matches event

**Skills not found**:
- Verify skill file exists in `.claude/skills/`
- Check skill name referenced correctly
- Ensure skill dependencies met

**Quality checks too strict**:
- Adjust thresholds in `config.yml`
- Disable strict_mode
- Update voice examples in `context/`

**Performance slow**:
- Enable caching in config
- Disable unnecessary hooks
- Use quick-post for simple content

## Monitoring & Analytics

### Built-in Analytics
- Content quality scores over time
- Platform performance metrics
- Workflow execution times
- Common failure points

### Reports
- Daily digest (scheduled)
- Weekly performance summary
- Monthly trends analysis
- Quarterly strategy review

## Versioning & Updates

**Current Version**: 2.0.0

**Migration**: See MIGRATION.md for v1→v2 upgrade path

**Backwards Compatibility**: v1 commands still work, new features opt-in

## Best Practices

1. **Start Small**: Enable features gradually
2. **Customize Context**: Update writing-examples.md with your best work
3. **Review Automation**: Don't blindly trust hooks - review outputs
4. **Monitor Quality**: Track quality scores to improve over time
5. **Iterate**: Workflows improve with usage and feedback
6. **Backup**: Git commit regularly, especially before major changes

## Resources

- **Documentation**: Full docs in `/docs` directory
- **Examples**: Example workflows in `.claude/workflows/`
- **Templates**: Content templates in `.claude/templates/`
- **Community**: [Link to community/support]

## License

MIT License - See LICENSE file

## Support

- GitHub Issues: [repo-url/issues]
- Documentation: [docs-url]
- Community: [community-url]
