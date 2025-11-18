# Migration Guide: v1.0 → v2.0

Complete guide for upgrading from ClaudeCode Writer v1.0 to v2.0.

## Overview

v2.0 introduces a complete plugin architecture with skills, hooks, workflows, and enhanced automation. This guide helps you migrate smoothly while preserving your existing content and customizations.

## What's Changed

### New in v2.0
✨ **Skills System**: Reusable capabilities (content analysis, SEO, voice matching)
✨ **Hooks System**: Event-driven automation
✨ **Enhanced Commands**: `/optimize`, `/quick-post`, analytics commands
✨ **Workflow Engine**: Multi-step orchestration
✨ **Configuration System**: Centralized settings
✨ **Analytics**: Performance tracking
✨ **Enhanced Context**: Brand guidelines, SEO keywords

### Backwards Compatibility
✓ **All v1 commands still work**: `/extract-themes`, `/research`, `/write`
✓ **All v1 agents still work**: linkedin-repurposer, newsletter-repurposer, conversational-repurposer
✓ **Existing content preserved**: All files in rawnotes/, research/, drafts/ are safe
✓ **Incremental adoption**: New features are opt-in

### Breaking Changes
⚠️ **Directory structure**: Content folders reorganized (automatic migration)
⚠️ **File naming**: New consistent naming convention (backward compatible)
⚠️ **Configuration**: New config file (creates from defaults)

## Pre-Migration Checklist

Before starting migration:

- [ ] **Backup your work**: `git commit -am "Backup before v2 migration"` or copy folder
- [ ] **Note customizations**: Document any custom agents or commands you've added
- [ ] **Export content**: Optional - export any critical content
- [ ] **Review changelog**: Read CHANGELOG.md for full list of changes

## Migration Process

### Automatic Migration (Recommended)

The easiest path - let the migration script handle everything:

```bash
# 1. Pull v2.0 changes
git pull origin main

# 2. Run migration script
/migrate-to-v2

# 3. Review changes
/verify-migration

# 4. Test workflow
/write "test migration" --dry-run
```

The migration script will:
1. Create new directory structure
2. Move existing files to new locations
3. Create default configuration
4. Preserve all customizations
5. Generate migration report

### Manual Migration

If you prefer manual control:

#### Step 1: Backup

```bash
# Create backup branch
git checkout -b pre-v2-backup
git commit -am "Backup before v2 migration"
git checkout main
```

#### Step 2: Pull v2.0

```bash
git pull origin main
```

#### Step 3: Reorganize Content

The new directory structure moves files:

**Old → New**:
```
rawnotes/          → content/rawnotes/
research/          → content/research/
drafts/            → content/drafts/
```

Migration commands:
```bash
# Migrate content folders
mkdir -p content/{rawnotes,research,drafts,ready,published,archive}
mv rawnotes/* content/rawnotes/ 2>/dev/null || true
mv research/* content/research/ 2>/dev/null || true
mv drafts/* content/drafts/ 2>/dev/null || true
rmdir rawnotes research drafts 2>/dev/null || true
```

#### Step 4: Create Configuration

Copy template and customize:

```bash
# Config file is auto-created on first run
# Or copy from template:
cp .claudecode-writer/config.template.yml .claudecode-writer/config.yml
```

Edit `.claudecode-writer/config.yml` to match your preferences.

#### Step 5: Update Context Files

**Add new context files** (optional but recommended):

1. **Brand Guidelines**: `context/brand-guidelines.md`
   - Define your brand voice
   - Content standards
   - Vocabulary preferences

2. **SEO Keywords**: `context/seo-keywords.md`
   - Primary keywords
   - Topic clusters
   - Competitor keywords

**Keep existing** `context/writing-examples.md` and `context/research-sources.md` - these still work!

#### Step 6: Test

```bash
# Test basic workflow
/research "test topic"
/write "test article"

# Test new features
/optimize content/drafts/[latest-article].md
/quick-post linkedin "test idea"
```

## Feature Migration

### Migrating Custom Agents

If you added custom agents in v1:

**v1 Location**: `.claude/agents/my-agent.md`
**v2 Location**: Same! No change needed.

Agents continue to work exactly as before. Optionally enhance them with v2 skills:

```markdown
<!-- In your custom agent -->
You can now use these skills:
- content-analyzer
- seo-optimizer
- voice-matcher
```

### Migrating Custom Commands

If you created custom commands in v1:

**v1 Location**: `.claude/commands/my-command.md`
**v2 Location**: Same! No change needed.

Commands continue to work. Optionally add v2 capabilities:

**Old command** (v1):
```markdown
# My Command
Do something...
```

**Enhanced command** (v2):
```markdown
# My Command

## What This Command Does
[Description]

## Integration Points
Uses skills:
- content-analyzer
- seo-optimizer

Related hooks:
- post-my-command
```

### Enabling New Features

All new features are **opt-in**. Enable in `.claudecode-writer/config.yml`:

```yaml
features:
  enabled:
    - skills           # Enable skill system
    - hooks            # Enable hooks (auto-repurposing, quality checks)
    - workflows        # Enable workflow orchestration
    - analytics        # Enable performance tracking
```

Start with `skills` and `hooks`, add others as you explore.

## Configuration Migration

### v1 (Implicit Configuration)

v1 had no central config - everything was hardcoded.

### v2 (Explicit Configuration)

v2 uses `.claudecode-writer/config.yml` for all settings.

**Key settings to configure**:

```yaml
# Automation preferences
workflow_automation:
  post_write_repurpose: true    # Auto-repurpose after /write?
  auto_quality_check: true      # Run quality checks?
  auto_seo_optimize: true       # Auto SEO optimization?

# Quality thresholds
quality:
  readability:
    min_score: 60              # Minimum readability score
  voice:
    similarity_threshold: 0.7   # Voice match threshold

# Platform connections (all disabled by default)
platforms:
  linkedin:
    enabled: true
    auto_publish: false        # Require manual approval
```

## Workflow Changes

### v1 Workflow

```
/extract-themes → /research → /write
  ↓
Manually use agents on article:
- "Use linkedin-repurposer agent on this article"
- "Use newsletter-repurposer agent on this article"
- "Use conversational-repurposer agent on this article"
```

### v2 Workflow (Default)

```
/extract-themes → /research → /write
  ↓ [AUTO-TRIGGERED by post-write hook]
All platform versions created automatically:
- LinkedIn version saved
- Newsletter version saved
- Social version saved
- Quality reports generated
- SEO optimization applied
```

**To disable auto-repurposing** (keep v1 behavior):
```yaml
workflow_automation:
  post_write_repurpose: false
```

## Common Migration Scenarios

### Scenario 1: "I want v2 features but keep manual control"

**Solution**: Enable features, disable automation

```yaml
features:
  enabled:
    - skills
    - hooks: false    # Disable hooks
    - workflows

workflow_automation:
  post_write_repurpose: false
  auto_quality_check: false
```

Use skills manually:
```
/write "my topic"
/optimize content/drafts/article-my-topic-2024-11-18.md
# Then manually repurpose when ready
```

### Scenario 2: "I want full automation"

**Solution**: Enable everything

```yaml
features:
  enabled:
    - skills
    - hooks
    - workflows
    - analytics

workflow_automation:
  post_write_repurpose: true
  auto_quality_check: true
  auto_seo_optimize: true

hooks:
  scheduled:
    daily_digest:
      enabled: true
    weekly_planning:
      enabled: true
```

### Scenario 3: "I only want specific new features"

**Solution**: Enable selectively

Want only SEO optimization?
```yaml
features:
  enabled:
    - skills

workflow_automation:
  post_write_repurpose: false
  auto_quality_check: false
  auto_seo_optimize: true
```

Then use: `/optimize --focus=seo`

### Scenario 4: "I have custom integrations/scripts"

**Solution**: Wrap in v2 hooks

If you had custom scripts that ran after content creation:

**v1**: Manual execution
```bash
# After /write, manually run:
./my-custom-script.sh article.md
```

**v2**: Hook integration
Create `.claude/hooks/post/custom-integration.md`:
```markdown
---
name: custom-integration
trigger: post_write
---

# Custom Integration Hook

After /write completes:
1. Run custom script
2. Upload to CMS
3. Notify team
```

## Verification

### Post-Migration Checks

Run these checks to ensure successful migration:

```bash
# 1. Verify directory structure
ls -la content/
# Should show: rawnotes/, research/, drafts/, ready/, published/, archive/

# 2. Verify configuration exists
cat .claudecode-writer/config.yml

# 3. Verify skills available
ls .claude/skills/core/
# Should show: content-analyzer.md, voice-matcher.md, seo-optimizer.md, etc.

# 4. Verify hooks available
ls .claude/hooks/post/
# Should show: post-write.md

# 5. Test basic command
/research "test migration"

# 6. Test new command
/quick-post linkedin "test v2 features"

# 7. Check content moved correctly
ls content/rawnotes/
ls content/research/
ls content/drafts/
```

### Expected Results

✓ All content in `content/` subdirectories
✓ Config file created and readable
✓ Skills and hooks directories populated
✓ Commands work (`/research`, `/write`, `/optimize`)
✓ Agents still work (linkedin-repurposer, etc.)

### Troubleshooting

**Issue**: "Content files missing"
**Solution**: Check `content/` subdirectories - files moved there

**Issue**: "Hooks not running"
**Solution**: Check `config.yml` has `hooks: enabled: true`

**Issue**: "Quality check failing everything"
**Solution**: Lower thresholds in config or disable strict mode

**Issue**: "/write not auto-repurposing"
**Solution**: Enable `workflow_automation.post_write_repurpose: true`

**Issue**: "Voice match score very low"
**Solution**: Add more examples to `context/writing-examples.md`

## Rollback Plan

If you need to rollback to v1:

```bash
# 1. Checkout backup branch
git checkout pre-v2-backup

# 2. Or revert commit
git revert HEAD

# 3. Or restore from backup
rm -rf ./* .claudecode-writer/
cp -r /path/to/backup/* ./
```

Your content in `content/` folders is still usable in v1 - just move back:
```bash
mv content/rawnotes/* rawnotes/
mv content/research/* research/
mv content/drafts/* drafts/
```

## Getting Help

**Migration Issues**:
1. Check this guide first
2. Review ARCHITECTURE.md for system understanding
3. Check FAQ in README.md
4. Open GitHub issue with `migration` label

**Feature Questions**:
1. Review ARCHITECTURE.md
2. Check individual skill/command documentation
3. Explore examples in `.claude/workflows/`

## Post-Migration Next Steps

Once migration is complete:

1. **Customize Configuration**
   - Review `.claudecode-writer/config.yml`
   - Set quality thresholds
   - Configure platforms

2. **Update Context Files**
   - Add examples to `context/writing-examples.md`
   - Update `context/research-sources.md`
   - Create `context/brand-guidelines.md`
   - Define `context/seo-keywords.md`

3. **Test New Features**
   - Try `/optimize` on existing content
   - Use `/quick-post` for rapid content
   - Enable hooks and observe automation
   - Run a workflow: `/workflow article-pipeline "test topic"`

4. **Enable Analytics** (optional)
   ```yaml
   analytics:
     tracking_enabled: true
   ```

5. **Schedule Automation** (optional)
   ```yaml
   hooks:
     scheduled:
       daily_digest:
         enabled: true
   ```

## Migration Checklist

Use this checklist to track your migration:

- [ ] Backup created (git commit or copy)
- [ ] v2.0 code pulled
- [ ] Directory structure created
- [ ] Content files moved
- [ ] Configuration file created
- [ ] Configuration customized
- [ ] Context files updated
- [ ] New context files created (optional)
- [ ] Commands tested (`/research`, `/write`)
- [ ] New commands tested (`/optimize`, `/quick-post`)
- [ ] Hooks working (if enabled)
- [ ] Quality checks passing
- [ ] Voice match reasonable
- [ ] Platform integrations configured (if using)
- [ ] Analytics enabled (if desired)
- [ ] Documentation reviewed
- [ ] Migration complete!

## Welcome to v2.0!

You're now running the enhanced ClaudeCode Writer with:
- ✅ Automated multi-platform repurposing
- ✅ Quality checks and SEO optimization
- ✅ Voice consistency validation
- ✅ Performance analytics
- ✅ Workflow orchestration
- ✅ And much more!

Start exploring:
```
/quick-post linkedin "Excited to try ClaudeCode Writer v2.0!"
```

Happy writing! 🚀
