# Quick Start Guide - ClaudeCode Writer v2.0

Get up and running with ClaudeCode Writer in 5 minutes.

## Prerequisites

- ✅ Claude Code installed ([install here](https://claude.ai/code))
- ✅ Git installed
- ✅ Basic familiarity with command line

## Step 1: Get the Plugin (2 minutes)

### Option A: Use as GitHub Template (Recommended)

1. Go to https://github.com/jamon8888/claudecode-writer
2. Click the green **"Use this template"** button
3. Name your repository (e.g., `my-content-workspace`)
4. Click **"Create repository"**
5. Clone your new repository:
   ```bash
   git clone https://github.com/YOUR-USERNAME/my-content-workspace.git
   cd my-content-workspace
   ```

### Option B: Clone Directly

```bash
git clone https://github.com/jamon8888/claudecode-writer.git my-content-workspace
cd my-content-workspace

# Remove the original remote (optional)
git remote remove origin

# Add your own remote (if you have one)
git remote add origin https://github.com/YOUR-USERNAME/my-content-workspace.git
```

## Step 2: Customize Your Workspace (3 minutes)

### 2.1 Add Your Writing Examples (Essential!)

Open `context/writing-examples.md` and add real examples of your writing:

```bash
# Edit the file
nano context/writing-examples.md
# or use your preferred editor
code context/writing-examples.md
```

**Add:**
- 2-3 LinkedIn posts you've written
- 1-2 newsletter sections
- 2-3 social media posts (Twitter/X, etc.)

**Example:**
```markdown
## LinkedIn Examples

### Post 1: Remote Work Productivity
Most productivity advice for remote workers is stuck in 2019.

Here's what actually works:
❌ Time blocking (ignores energy rhythms)
✅ Energy blocking (work with your natural peaks)
...

Performance: 450 likes, 87 comments
Notes: Strong opening hook, practical tips, ended with question
```

### 2.2 Add Your Research Sources

Open `context/research-sources.md` and add your favorite sources:

```bash
nano context/research-sources.md
```

**Add:**
- Your favorite newsletters (Morning Brew, The Hustle, etc.)
- Industry publications
- Expert blogs
- News sources

**Example:**
```markdown
## Priority Newsletters
- [Morning Brew](https://morningbrew.com) - Business and tech news
- [The Hustle](https://thehustle.co) - Entrepreneurship insights
- [Your favorite newsletter] - [What they cover]
```

### 2.3 (Optional) Customize Configuration

Review and adjust `.claudecode-writer/config.yml`:

```bash
nano .claudecode-writer/config.yml
```

**Key settings to review:**
- `workflow_automation.post_write_repurpose: true` - Auto-repurpose?
- `quality.readability.min_score: 60` - Quality threshold
- `features.enabled` - Which features to enable

**For first use, leave defaults!** They're designed to work well out of the box.

## Step 3: Start Claude Code

```bash
# From your workspace directory
claude
```

This starts Claude Code in your workspace. You'll see a prompt where you can chat with Claude.

## Step 4: Your First Content (1 minute)

### Test the System

```bash
# In Claude Code, type:
/write "why remote work productivity advice fails"
```

**What happens:**
1. Claude creates a comprehensive article
2. AUTO-generates LinkedIn version
3. AUTO-generates newsletter version
4. AUTO-generates social media version
5. Runs quality analysis
6. Performs SEO optimization
7. Validates voice consistency

**All files saved to `content/drafts/` with timestamp!**

### Review the Output

```bash
# List the generated files
ls content/drafts/

# You should see:
# - article-[topic]-2024-11-18.md
# - linkedin-[topic]-2024-11-18.md
# - newsletter-[topic]-2024-11-18.md
# - social-[topic]-2024-11-18.md
# - quality-report-[topic]-2024-11-18.md
# - seo-report-[topic]-2024-11-18.md
# - summary-[topic]-2024-11-18.md
```

## Step 5: Explore Commands

### Try More Commands

```bash
# Extract themes from raw notes
/extract-themes

# Research a topic
/research "future of remote work"

# Create a quick LinkedIn post
/quick-post linkedin "Time blocking doesn't work for remote workers"

# Optimize existing content
/optimize content/drafts/article-[your-file].md
```

### Common Workflow

```bash
# 1. Add ideas to content/rawnotes/
#    (Create .md files with your thoughts)

# 2. Extract themes
/extract-themes

# 3. Research the best theme
/research "[theme from extraction]"

# 4. Write the article
/write "[topic based on research]"

# 5. Review all generated files in content/drafts/

# 6. Publish when ready!
```

## Next Steps

### Improve Voice Matching

The more examples you add to `context/writing-examples.md`, the better Claude matches your voice. Add examples as you create good content!

### Customize Your Brand

Edit `context/brand-guidelines.md` to define:
- Your brand voice attributes
- Content standards
- Vocabulary preferences
- Formatting guidelines

### Define SEO Strategy

Edit `context/seo-keywords.md` to set:
- Primary keywords
- Topic clusters
- SEO strategy

### Explore Advanced Features

- **Workflows**: Check `.claude/workflows/` for orchestration examples
- **Skills**: Review `.claude/skills/core/` to understand capabilities
- **Hooks**: See `.claude/hooks/` for automation options

## Troubleshooting

### "Command not found: /write"
**Solution**: Make sure you're in Claude Code (`claude` command), not your regular terminal.

### "Content doesn't match my voice"
**Solution**: Add more diverse examples to `context/writing-examples.md`. Quality > quantity, but 5-10 good examples is ideal.

### "Quality check failed"
**Solution**: This is normal for first attempts! Review the quality report and adjust. You can also lower thresholds in config.yml.

### "Files not being created"
**Solution**: Check that:
1. You're in the correct directory (`pwd`)
2. `content/drafts/` folder exists
3. You have write permissions

### "Hooks not running"
**Solution**: Verify in `.claudecode-writer/config.yml`:
```yaml
features:
  enabled:
    - hooks
workflow_automation:
  post_write_repurpose: true
```

## Tips for Success

1. **Start Simple**: Use `/write` with a simple topic first
2. **Add Examples Gradually**: Start with 3-5 examples, add more as you create content
3. **Review Generated Content**: Check the quality reports to understand what's being analyzed
4. **Customize Over Time**: Don't overwhelm yourself with configuration initially
5. **Use Version Control**: Commit your content regularly with git
6. **Experiment**: Try different commands and workflows to find what works for you

## Getting Help

- **Documentation**: [ARCHITECTURE.md](ARCHITECTURE.md) for complete details
- **Migration**: [MIGRATION.md](MIGRATION.md) if upgrading from v1.0
- **Issues**: [GitHub Issues](https://github.com/jamon8888/claudecode-writer/issues)
- **Discussions**: [Community forum](https://github.com/jamon8888/claudecode-writer/discussions)

## What's Next?

Once you're comfortable:
- ✅ Experiment with custom workflows
- ✅ Create your own skills
- ✅ Add custom hooks for automation
- ✅ Integrate with your publishing platforms
- ✅ Track performance with analytics

## Congratulations! 🎉

You're now set up with a complete content workflow engine. Happy writing!

---

**Questions?** Open an issue or start a discussion on GitHub.

**Working great?** Consider starring the repository ⭐ and sharing with other content creators!
