---
name: daily-digest
description: Daily summary of content activity, performance, and suggested actions
type: workflow
trigger: schedule
schedule: "09:00"
enabled: true
---

# Daily Digest Hook

Automatically generates a daily summary of your content workflow activity, performance metrics, and recommended next actions.

## Trigger
Runs daily at 09:00 (configurable in config.yml)

## What This Hook Does

### 1. Activity Summary (Last 24 Hours)
- Content created (articles, posts)
- Research completed
- Themes extracted
- Content published
- Drafts in progress

### 2. Content Status
- **Ready to Publish**: X pieces
- **In Drafts**: X pieces
- **Needs Review**: X pieces (quality issues)
- **Scheduled**: X pieces

### 3. Performance Highlights (if analytics enabled)
- Top performing content (last 7 days)
- Engagement trends
- Platform performance
- Best posting times validation

### 4. Recommended Actions
- Priority tasks for today
- Content ready for review
- Overdue scheduled posts
- Research topics trending now

### 5. Content Calendar Preview
- What's scheduled for this week
- Gaps in calendar
- Suggested posting schedule

## Output Format

```markdown
# Daily Content Digest - [Day, Date]

## Yesterday's Activity
✓ 1 article written
✓ 3 platform versions created
✓ 2 research briefs completed
→ 4 drafts ready for review

## Content Status

### Ready to Publish (2)
1. "Why Productivity Advice Fails" - LinkedIn, Newsletter, Social versions ready
2. "Remote Work Trends 2024" - All platforms ready

### In Progress (3)
1. "AI and Creativity" - Draft in progress
2. "Future of Work" - Research complete, needs writing
3. "Leadership in Remote Teams" - Theme extracted, needs research

### Needs Attention (1)
1. "Technical SEO Guide" - Quality score 58/100, needs revision

## Performance Highlights (Last 7 Days)

🏆 Top Performer: "Remote Work Productivity"
   LinkedIn: 450 likes, 87 comments, 12% engagement rate

📈 Trending Up: Newsletter open rates (+5%)
📊 Platform Performance:
   - LinkedIn: Avg 8.5% engagement
   - Newsletter: 42% open rate
   - Twitter: 3.2% engagement

## Today's Recommended Actions

Priority:
1. Review and publish "Productivity Advice Fails" (scheduled for 10 AM)
2. Address quality issues in "Technical SEO Guide"
3. Complete draft of "AI and Creativity"

Opportunities:
- "Remote collaboration" trending - good research topic
- Thursday is optimal posting day this week
- 2 LinkedIn posts scheduled - good cadence

## This Week's Calendar

Monday: Newsletter scheduled (8 AM)
Tuesday: LinkedIn post ready
Wednesday: [Gap - suggest content]
Thursday: LinkedIn post ready (10 AM) ← Optimal day
Friday: Social posts ready

## Content Gaps & Suggestions

Gaps Identified:
- No social content scheduled this week
- Only 1 newsletter for the week (typically 2)
- No content on "AI trends" (currently trending)

Suggestions:
1. Create quick social post from "Productivity Advice" article
2. Research "AI collaboration tools" for next newsletter
3. Extract themes from raw notes (last check: 3 days ago)

## Raw Notes Status
- 7 new files in /rawnotes (last 4 days)
- Recommend running /extract-themes to find patterns

## System Health
✓ All agents functioning
✓ Quality checks passing
✓ Platform connections active
→ 142 MB in drafts folder (consider archiving)

---

To disable this digest: Set `hooks.scheduled.daily_digest.enabled: false` in config.yml
```

## Configuration

```yaml
hooks:
  scheduled:
    daily_digest:
      time: "09:00"
      enabled: true
      include_performance: true
      include_recommendations: true
      include_calendar: true
```

## Customization

Choose what to include:
- `include_performance`: Performance metrics
- `include_recommendations`: AI-generated suggestions
- `include_calendar`: Week ahead preview
- `include_system_health`: Storage and system info

## Delivery Options

### Console Display (Default)
Display in Claude Code interface when you start session.

### Email Delivery (Future)
```yaml
daily_digest:
  email: true
  email_address: you@example.com
```

### Saved Report
Always saves to: `analytics/daily-digest-[YYYY-MM-DD].md`

## Related Hooks
- `weekly-planning` - Weekly content strategy
- `performance-sync` - Analytics collection
- `archive-cleanup` - Content archiving

## Disable

```yaml
hooks:
  scheduled:
    daily_digest:
      enabled: false
```
