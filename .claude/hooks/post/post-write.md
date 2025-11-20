---
name: post-write
description: Automatically executes after /write command completes - repurposes content to all platforms
type: post
trigger: write_command_complete
enabled: true
priority: 1
---

# Post-Write Hook

This hook automatically executes after the `/write` command completes, orchestrating the entire multi-platform repurposing workflow.

## Trigger Event
Activated when `/write` command successfully saves an article to the drafts folder.

## What This Hook Does

### 1. Validate Article Creation
- Confirm article file was created successfully
- Extract article metadata (title, topic, date)
- Verify minimum quality thresholds met
- Check that article meets length requirements (800+ words)

### 2. Auto-Repurpose to All Platforms
Execute all three repurposing agents in parallel:

#### LinkedIn Repurposing
- Invoke `linkedin-repurposer` agent
- Pass full article content
- Save output to: `content/drafts/linkedin-[topic-slug]-[date].md`
- Extract LinkedIn-specific metadata (hashtags, posting time)

#### Newsletter Repurposing
- Invoke `newsletter-repurposer` agent
- Pass full article content
- Save output to: `content/drafts/newsletter-[topic-slug]-[date].md`
- Extract newsletter metadata (subject line, preview text)

#### Social Media & Podcast Repurposing
- Invoke `conversational-repurposer` agent
- Pass full article content
- Save output to: `content/drafts/social-[topic-slug]-[date].md`
- Extract social media posts and podcast Q&A scripts

### 3. Run Quality Checks
- Invoke `content-analyzer` skill on main article
- Generate quality report
- Save to: `content/drafts/quality-report-[topic-slug]-[date].md`
- Flag any critical issues (score < 60)

### 4. SEO Optimization
- Invoke `seo-optimizer` skill on main article
- Generate SEO recommendations
- Save to: `content/drafts/seo-report-[topic-slug]-[date].md`
- Create optimized meta data

### 5. Voice Validation
- Invoke `voice-matcher` skill on main article
- Validate voice consistency
- Save report to: `content/drafts/voice-report-[topic-slug]-[date].md`
- Flag significant deviations (score < 70)

### 6. Generate Asset Suggestions
- Suggest relevant images for article
- Propose graphics for social media posts
- Recommend thumbnail options
- Save suggestions to: `content/drafts/assets-[topic-slug]-[date].md`

### 7. Create Content Summary
Generate comprehensive summary document:
- Article title and summary
- All platform versions created
- Quality scores
- SEO scores
- Voice match scores
- Recommended publish schedule
- Asset suggestions
- Next steps

Save to: `content/drafts/summary-[topic-slug]-[date].md`

### 8. Update Content Calendar
- Add article to content calendar
- Suggest optimal publishing schedule for each platform
- Mark as "Ready for Review"

### 9. Generate Notifications
Create notification summary:
```
✓ Article created: [title]
✓ LinkedIn version: content/drafts/linkedin-[slug]-[date].md
✓ Newsletter version: content/drafts/newsletter-[slug]-[date].md
✓ Social version: content/drafts/social-[slug]-[date].md

Quality Scores:
- Overall: X/100
- SEO: X/100
- Voice Match: X/100

Next Steps:
1. Review all platform versions
2. Address any quality issues flagged
3. Schedule for publication
4. Prepare assets

All files ready in content/drafts/
```

## Execution Flow

```mermaid
graph TD
    A[/write command completes] --> B[Validate article created]
    B --> C{Valid article?}
    C -->|No| D[Report error and exit]
    C -->|Yes| E[Parallel: Repurpose to all platforms]
    E --> F[LinkedIn Agent]
    E --> G[Newsletter Agent]
    E --> H[Social/Podcast Agent]
    F --> I[All agents complete]
    G --> I
    H --> I
    I --> J[Run quality checks]
    J --> K[SEO optimization]
    K --> L[Voice validation]
    L --> M[Generate asset suggestions]
    M --> N[Create content summary]
    N --> O[Update calendar]
    O --> P[Generate notification]
    P --> Q[Display to user]
```

## Configuration

Controlled by these config settings:

```yaml
workflow_automation:
  post_write_repurpose: true    # Enable auto-repurposing
  auto_quality_check: true       # Run quality checks
  auto_seo_optimize: true        # Run SEO optimization

hooks:
  post_write:
    - auto-repurpose-all
    - seo-optimize
    - generate-thumbnails
    - schedule-suggestions
```

## File Naming Convention

All generated files use consistent naming:
- **Main article**: `article-[topic-slug]-[YYYY-MM-DD].md`
- **LinkedIn**: `linkedin-[topic-slug]-[YYYY-MM-DD].md`
- **Newsletter**: `newsletter-[topic-slug]-[YYYY-MM-DD].md`
- **Social**: `social-[topic-slug]-[YYYY-MM-DD].md`
- **Quality Report**: `quality-report-[topic-slug]-[YYYY-MM-DD].md`
- **SEO Report**: `seo-report-[topic-slug]-[YYYY-MM-DD].md`
- **Voice Report**: `voice-report-[topic-slug]-[YYYY-MM-DD].md`
- **Assets**: `assets-[topic-slug]-[YYYY-MM-DD].md`
- **Summary**: `summary-[topic-slug]-[YYYY-MM-DD].md`

Where:
- `[topic-slug]`: Lowercase, hyphenated version of title
- `[YYYY-MM-DD]`: Current date

## Error Handling

If any step fails:
1. Log the error with context
2. Continue with remaining steps
3. Report all errors in final notification
4. Provide recovery suggestions

Example error handling:
```
⚠ Warning: LinkedIn repurposing failed
   Error: [error details]
   Impact: LinkedIn version not created
   Action: Run manually: Use linkedin-repurposer agent on article

✓ Newsletter repurposing completed
✓ Social repurposing completed
```

## Performance Optimization

- Execute repurposing agents in **parallel** (not sequential)
- Cache article content to avoid re-reading
- Reuse quality analysis results across different checks
- Generate all file names upfront to avoid recalculation

## Disable Hook

To disable this hook:

```yaml
# In .claudecode-writer/config.yml
workflow_automation:
  post_write_repurpose: false
```

Or temporarily:
```
/write [topic] --no-hooks
```

## Manual Trigger

To manually trigger this hook on an existing article:
```
/run-hook post-write --file content/drafts/article-[name].md
```

## Success Criteria

Hook succeeds when:
- ✓ Main article exists and is valid
- ✓ At least 2 of 3 platform versions created
- ✓ Quality analysis completed (even if score is low)
- ✓ Summary file created
- ✓ User notification displayed

## Related Hooks

- `pre-write`: Runs before /write command
- `post-repurpose`: Runs after each repurposing completes
- `quality-check`: Validates content quality

## Related Skills

- `content-analyzer`: Quality analysis
- `seo-optimizer`: SEO recommendations
- `voice-matcher`: Voice consistency check

## Related Agents

- `linkedin-repurposer`: LinkedIn optimization
- `newsletter-repurposer`: Email optimization
- `conversational-repurposer`: Social media and podcast

## Examples

### Example Execution Output

```
Running post-write hook...

✓ Article validated: "Why Productivity Advice is Failing Remote Workers"
✓ Starting parallel repurposing...

  → LinkedIn repurposing... ✓ Done (2.3s)
  → Newsletter repurposing... ✓ Done (2.1s)
  → Social/Podcast repurposing... ✓ Done (1.9s)

✓ Quality analysis complete: 87/100
✓ SEO optimization complete: 82/100
✓ Voice validation complete: 91/100
✓ Asset suggestions generated
✓ Content summary created
✓ Calendar updated

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Content Suite Created Successfully!
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📄 Main Article
   content/drafts/article-productivity-advice-failing-remote-workers-2024-11-18.md

📱 Platform Versions
   LinkedIn: content/drafts/linkedin-productivity-advice-failing-remote-workers-2024-11-18.md
   Newsletter: content/drafts/newsletter-productivity-advice-failing-remote-workers-2024-11-18.md
   Social: content/drafts/social-productivity-advice-failing-remote-workers-2024-11-18.md

📊 Reports
   Quality: 87/100 - Excellent
   SEO: 82/100 - Good, minor optimizations suggested
   Voice: 91/100 - Strong match

📅 Recommended Schedule
   LinkedIn: Thursday, 10:00 AM
   Newsletter: Tuesday, 8:00 AM
   Twitter: Wednesday, 3:00 PM

Next Steps:
1. Review platform versions in content/drafts/
2. Check quality-report for any suggested improvements
3. Review seo-report for optimization opportunities
4. Schedule publications when ready

Total execution time: 6.7s
```

## Best Practices

1. **Review Before Publishing**: Always review repurposed versions
2. **Check Quality Scores**: Address any scores below 70
3. **Customize Platform Versions**: Use repurposed content as starting point
4. **Track Performance**: Use generated versions to test what works
5. **Iterate**: Update voice and style based on what performs best

## Troubleshooting

**Issue**: Hook not running after /write
**Solution**: Check `workflow_automation.post_write_repurpose` in config

**Issue**: Repurposing agents failing
**Solution**: Verify agents exist in `.claude/agents/` directory

**Issue**: Files not saving to correct location
**Solution**: Check `paths.drafts` in config.yml

**Issue**: Slow execution
**Solution**: Ensure parallel execution is enabled in config
