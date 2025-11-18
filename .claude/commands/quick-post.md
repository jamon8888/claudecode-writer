---
name: quick-post
description: Rapidly create a single platform post without full article workflow
---

# Quick Post Command

Quickly create optimized content for a specific platform without going through the full research → write → repurpose workflow.

## Usage
```
/quick-post linkedin [idea/topic]
/quick-post newsletter [idea/topic]
/quick-post twitter [idea/topic]
/quick-post social [idea/topic]
```

## What This Command Does

1. Takes your raw idea or topic
2. Develops it into platform-optimized content
3. Uses appropriate repurposing agent
4. Runs quality checks
5. Predicts engagement
6. Saves ready-to-publish version

Perfect for:
- Timely reactions to news/trends
- Quick insights you want to share
- Repurposing a single idea without full article
- Testing content ideas before full development

## Process

### Step 1: Idea Development
- Expand the core idea
- Add context and value
- Find supporting angle
- Identify hook potential

### Step 2: Platform-Specific Creation
Routes to appropriate agent:
- `linkedin` → linkedin-repurposer agent
- `newsletter` → newsletter-repurposer agent
- `twitter/social` → conversational-repurposer agent

### Step 3: Quality Check
- Voice consistency check
- Platform requirements met
- Engagement potential assessment

### Step 4: Prediction & Suggestions
- Estimated engagement rate
- Optimal posting time
- Hashtag suggestions (if applicable)
- A/B test variants (if applicable)

## Examples

### LinkedIn Quick Post
```
/quick-post linkedin "Most productivity advice assumes you work in an office"

Developing LinkedIn post...

✓ Core insight identified
✓ Professional angle developed
✓ Engagement hook crafted

Generated Post:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Most productivity advice assumes you work in an office.

Time blocking? Assumes stable environment.
Focus hours? Assumes you control interruptions.
Pomodoro? Assumes consistent energy levels.

Remote work needs different strategies:

✓ Energy blocking (not time blocking)
✓ Transition rituals (not separate spaces)
✓ Async depth work (not scheduled focus time)

The shift: Productivity isn't about managing time anymore.
It's about managing energy in a distributed world.

What's your best remote productivity hack?

#RemoteWork #Productivity #FutureOfWork
━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Post Stats:
- Length: 1,124 characters (optimal range)
- Readability: Excellent
- Voice match: 89/100
- Predicted engagement: 6-8%

Optimal posting: Thursday 10:00 AM

Saved to: content/ready/linkedin-productivity-advice-2024-11-18.md

Ready to publish!
```

### Newsletter Quick Section
```
/quick-post newsletter "Why most remote teams are over-meeting"

Creating newsletter section...

✓ Email-optimized structure
✓ Engaging subject line created
✓ Personal tone applied

Generated Content:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Subject: You're probably in too many meetings
Preview: Here's how to know (and what to do about it)...

Hey [Name],

Quick question: How many meetings did you have yesterday?

If you're like most remote workers I talk to, the answer is somewhere between "too many" and "way too many."

Here's the thing everyone gets wrong about remote meetings...

[Full newsletter section with value, examples, actionable advice]

Talk soon,
[Your name]

P.S. Hit reply and tell me your meeting count yesterday. I'm curious.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Email Stats:
- Read time: 90 seconds
- Subject score: 82/100
- Personal touch: High
- Spam score: Safe

Best send time: Tuesday 8:00 AM

Saved to: content/ready/newsletter-meetings-2024-11-18.md
```

### Twitter/X Quick Post
```
/quick-post twitter "Energy management beats time management for remote workers"

Creating Twitter post...

✓ Punchy delivery
✓ Shareable insight
✓ Within character limit

Generated Tweet:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Hot take: Time blocking doesn't work for remote workers.

Try "energy blocking" instead.

Schedule deep work when YOU naturally focus best, not when your calendar says you should.

Game changer.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Tweet Stats:
- Length: 178 characters
- Hook quality: Strong
- Shareability: High
- Predicted engagement: 4-6%

Alternative version (thread):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Time blocking doesn't work for remote workers.

Here's why (and what to do instead): 🧵

1/ Traditional productivity advice assumes...
[Full thread provided]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Saved to: content/ready/social-energy-blocking-2024-11-18.md
```

## Options

### With Reference Content
```
/quick-post linkedin --from=content/drafts/article-productivity.md

Pull key insight from existing article and create LinkedIn post.
```

### With A/B Testing
```
/quick-post linkedin [topic] --variants=3

Generate 3 different versions to A/B test.
```

### Skip Quality Check
```
/quick-post twitter [topic] --quick

Skip quality checks for truly rapid posting.
```

## File Management

Saves to: `content/ready/[platform]-[slug]-[date].md`

Includes metadata:
- Creation date/time
- Platform target
- Predicted metrics
- Optimal posting time
- Quality scores

## Integration Points

### Agents Used
- Platform-specific repurposing agents
- Voice-matcher skill
- Engagement predictor

### Related Commands
- `/write` - Full article workflow
- `/research` - Deeper topic development
- `/optimize` - Enhance quick post further

### Related Hooks
- `quality-check` - Validates post
- `post-repurpose` - If you want to expand to other platforms later

## Best Practices

1. **Keep It Focused**: One clear idea per post
2. **Know Your Platform**: Different platforms need different approaches
3. **Test Ideas**: Use quick posts to test before full articles
4. **Engage Fast**: Best for timely content
5. **Quality Still Matters**: Quick doesn't mean low-quality

## When to Use

✓ **Use Quick Post When**:
- Reacting to trending news
- Sharing a single insight
- Testing content idea viability
- Time-sensitive post needed
- Simple idea, no research needed

✗ **Use Full Workflow When**:
- Complex topic needing research
- Multi-platform content suite needed
- Building thought leadership piece
- SEO-focused article
- In-depth analysis required
