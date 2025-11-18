---
name: optimize
description: Optimize existing content for quality, SEO, voice, and platform performance
---

# Optimize Command

Analyzes and optimizes existing content using all available skills to improve quality, SEO, voice consistency, and engagement potential.

## Usage
```
/optimize [file-path]
/optimize [file-path] --focus=seo
/optimize [file-path] --focus=voice
/optimize [file-path] --focus=readability
```

## What This Command Does

### 1. Comprehensive Analysis
Runs all analysis skills on the content:
- **content-analyzer**: Overall quality, readability, structure
- **seo-optimizer**: Search engine optimization
- **voice-matcher**: Voice and brand consistency
- **engagement-predictor**: Estimated performance (if available)

### 2. Generate Optimization Report
Creates detailed report with:
- Current scores (quality, SEO, voice, engagement)
- Specific issues identified
- Prioritized recommendations
- Before/after examples
- Estimated impact of changes

### 3. Apply Optimizations (Optional)
Can automatically apply non-destructive optimizations:
- Fix grammar and spelling
- Improve sentence structure
- Optimize keyword placement
- Adjust header hierarchy
- Add missing elements (meta description, etc.)

### 4. Save Optimized Version
- Save optimized version as new file
- OR overwrite existing file (with backup)
- Create optimization report for reference

## Process

### Step 1: Read Target Content
- Load file from specified path
- Identify content type (article, LinkedIn, newsletter, etc.)
- Extract metadata

### Step 2: Run All Analysis Skills

**Content Analysis**:
```
Using content-analyzer skill...
- Readability: X/100
- Structure: X/100
- Grammar: X/100
- Engagement: X/100
```

**SEO Analysis**:
```
Using seo-optimizer skill...
- Keyword optimization: X/100
- On-page SEO: X/100
- Meta data: X/100
```

**Voice Analysis**:
```
Using voice-matcher skill...
- Voice consistency: X/100
- Tone match: X/100
- Vocabulary match: X/100
```

### Step 3: Prioritize Recommendations

**Critical** (Must fix, high impact):
1. [Issue and solution]
2. [Issue and solution]

**Important** (Should fix, medium impact):
1. [Improvement and solution]
2. [Improvement and solution]

**Optimization** (Nice to have, polish):
1. [Enhancement]
2. [Enhancement]

### Step 4: User Decision

Present options:
```
Found 12 optimization opportunities:
- 3 critical (avg impact: +15 points)
- 5 important (avg impact: +8 points)
- 4 nice-to-have (avg impact: +3 points)

Estimated score improvement: 52/100 → 78/100

Options:
1. Apply all safe optimizations automatically
2. Review and approve each change
3. Generate report only (no changes)
4. Focus on specific area (seo, voice, readability)

What would you like to do?
```

### Step 5: Apply Changes (if approved)

For each optimization:
- Show before/after
- Explain the change
- Apply if approved
- Track cumulative impact

### Step 6: Save and Report

- Save optimized content
- Create optimization report
- Show final scores
- Recommend next steps

## Focus Modes

### SEO Focus
```
/optimize [file] --focus=seo
```
- Keyword optimization
- Meta data creation
- Header structure
- Link optimization
- Featured snippet opportunities

### Voice Focus
```
/optimize [file] --focus=voice
```
- Tone adjustments
- Vocabulary alignment
- Sentence pattern matching
- Brand consistency
- Platform appropriateness

### Readability Focus
```
/optimize [file] --focus=readability
```
- Simplify complex sentences
- Reduce grade level
- Improve paragraph structure
- Add transitions
- Enhance scanability

### Engagement Focus
```
/optimize [file] --focus=engagement
```
- Strengthen hook
- Add engagement prompts
- Improve CTA clarity
- Increase shareability
- Optimize for platform algorithm

## Output Structure

```markdown
# Optimization Report: [Title]

## Summary
**Original Score**: 62/100
**Optimized Score**: 84/100 (estimated)
**Improvement**: +22 points

**Changes Applied**: 8 of 12 recommendations
**Focus Areas**: SEO (+12), Voice (+6), Readability (+4)

## Scores Breakdown

### Before Optimization
- Overall: 62/100
- Readability: 58/100
- SEO: 55/100
- Voice: 72/100
- Structure: 68/100

### After Optimization
- Overall: 84/100
- Readability: 82/100 (+24)
- SEO: 88/100 (+33)
- Voice: 85/100 (+13)
- Structure: 80/100 (+12)

## Changes Applied

### Critical Fixes (3)
1. **SEO: Added primary keyword to title**
   - Before: "Tips for Better Productivity"
   - After: "Remote Work Productivity: 7 Tips That Actually Work"
   - Impact: +12 SEO points

2. **Readability: Simplified complex sentences**
   - Before: "The implementation of asynchronous communication methodologies..."
   - After: "Using async communication helps teams work better..."
   - Impact: +8 readability points

3. **Structure: Added clear introduction hook**
   - Before: Started directly with point 1
   - After: Added compelling opening paragraph
   - Impact: +6 engagement points

### Important Improvements (5)
[List of 5 improvements with before/after]

## Recommendations Not Applied

### Manual Review Needed (4)
1. **Voice: Adjust tone in section 3**
   - Current tone more formal than brand voice
   - Suggested rewrite: [example]
   - Reason not auto-applied: Requires creative judgment

2. [Additional recommendations...]

## SEO Optimization Details

**Primary Keyword**: "remote work productivity"
**Keyword Density**: 0.8% → 1.5% (optimal)
**Meta Description**: Added (158 characters)
**Alt Text**: Added to 3 images
**Internal Links**: Added 2 relevant links
**Header Hierarchy**: Fixed H2/H3 structure

## Voice Alignment Details

**Tone Adjustment**: More conversational
**Vocabulary Updates**: 7 terms aligned with brand voice
**Sentence Structure**: Varied length for better flow
**Personal Elements**: Added 2 personal touches

## File Management

**Original File**: [Backed up to]
**Optimized File**: [Saved to]
**Report**: [Saved to]

## Next Steps
1. Review changes in optimized version
2. Consider manual recommendations
3. Run final quality check before publishing
4. Schedule for publication

## Performance Prediction
Based on optimized content:
- Estimated engagement rate: 7-9% (vs. 4-5% original)
- Estimated read time: 4 minutes
- Shareability score: High
- SEO ranking potential: Good for target keywords
```

## Integration Points

### Skills Used
- `content-analyzer` - Quality analysis
- `seo-optimizer` - SEO recommendations
- `voice-matcher` - Voice consistency
- `engagement-predictor` - Performance estimation

### Related Commands
- `/write` - Creates content that can be optimized
- `/research` - Provides content for optimization
- `/analyze-performance` - Review results

### Related Hooks
- `quality-check` - Validates final optimized version
- `post-optimize` - Can trigger after optimization

## Examples

### Example 1: Full Optimization
```
/optimize content/drafts/article-productivity-2024-11-18.md

Analyzing content...

✓ Content analyzed
  Current score: 67/100

Found 15 optimization opportunities:
  Critical: 4 (high impact)
  Important: 7 (medium impact)
  Polish: 4 (low impact)

Applying all safe optimizations...

✓ 11 changes applied automatically
→ 4 require manual review

Optimized score: 86/100 (+19 points)

Files saved:
- Optimized: content/ready/article-productivity-2024-11-18-optimized.md
- Report: analytics/reports/optimization-productivity-2024-11-18.md
- Backup: content/archive/article-productivity-2024-11-18-original.md
```

### Example 2: SEO Focus
```
/optimize content/drafts/article-remote-work.md --focus=seo

Running SEO optimization...

SEO Analysis:
- Current SEO score: 52/100
- Primary keyword: "remote work tips"
- Keyword density: 0.3% (too low)

Optimizations:
✓ Optimized title with keyword
✓ Created meta description (155 chars)
✓ Added keyword to H1, 2 H2s
✓ Increased keyword density to 1.2%
✓ Added 3 internal links
✓ Optimized 2 image alt texts

SEO score: 52 → 89/100 (+37 points)

Ready for publication with strong SEO.
```

## Configuration

```yaml
optimization:
  auto_apply_safe: true      # Auto-apply non-destructive changes
  create_backup: true        # Backup original before changes
  min_improvement: 10        # Only apply if +10 points minimum
  focus_areas:
    - readability
    - seo
    - voice
    - engagement
```

## Best Practices

1. **Always Backup**: Keep original version
2. **Review Changes**: Don't blindly accept all optimizations
3. **Iterative**: May need multiple optimization passes
4. **Context Matters**: Optimization depends on audience and platform
5. **Preserve Voice**: Never sacrifice authenticity for metrics

## Troubleshooting

**Issue**: Score not improving much
**Solution**: Focus on specific area with --focus flag

**Issue**: Too many suggestions overwhelming
**Solution**: Use focus mode to tackle one area at a time

**Issue**: Voice being changed too much
**Solution**: Check @context/writing-examples.md has good samples
