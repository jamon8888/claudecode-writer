---
name: quality-check
description: Validates content quality before saving - runs on all content creation
type: quality
trigger: before_content_save
enabled: true
priority: 10
---

# Quality Check Hook

This hook automatically validates content quality before any file is saved, ensuring all content meets minimum standards.

## Trigger Events
Activated before:
- `/write` command saves article
- Repurposing agents save platform versions
- `/optimize` command saves changes
- Manual content edits are saved

## What This Hook Does

### 1. Content Analysis
Run quick quality checks on content:

#### Readability Check
- Flesch Reading Ease score > 60
- Grade level appropriate for audience
- Average sentence length < 25 words
- Paragraph length reasonable (< 6 sentences)

#### Grammar & Spelling
- No critical grammar errors
- No spelling mistakes
- Proper punctuation
- Consistent capitalization

#### Structure Check
- Has clear title/headline
- Has introduction
- Has conclusion or call-to-action
- Proper heading hierarchy
- Minimum length requirements met

#### Voice Consistency (if enabled)
- Matches voice profile from examples
- Tone appropriate for platform
- Vocabulary consistent with brand

### 2. Platform-Specific Validation

#### For Articles (800+ words)
- ✓ Title exists and is compelling (50-70 characters)
- ✓ Introduction hooks reader
- ✓ Has 3+ main sections with headers
- ✓ Conclusion with takeaway/CTA
- ✓ 800-2500 words
- ✓ Readability score > 60

#### For LinkedIn Posts (900-1300 characters)
- ✓ Hook in first 2 lines
- ✓ Value clear by paragraph 2
- ✓ 900-1300 characters (optimal)
- ✓ Line breaks for mobile readability
- ✓ Has engagement prompt
- ✓ Hashtags included (3-5)

#### For Newsletter Sections
- ✓ Subject line exists (30-50 characters)
- ✓ Preview text exists (35-90 characters)
- ✓ Personal opening
- ✓ Clear value proposition
- ✓ Single CTA
- ✓ Personal sign-off
- ✓ No spam trigger words

#### For Social Posts
- ✓ Within platform limits (280 for X, etc.)
- ✓ Hook in first 7 words
- ✓ Shareable insight
- ✓ Clear point or question

### 3. Quality Scoring

Generate quick quality scores:
- **Readability**: 0-100
- **Grammar**: 0-100 (based on error count)
- **Structure**: 0-100
- **Voice Match**: 0-100 (if enabled)
- **Overall**: Average

### 4. Decision Logic

Based on overall score:

#### Score 80-100: PASS ✓
- Save content normally
- Display success message
- No intervention needed

#### Score 60-79: WARN ⚠
- Save content with warnings
- Display specific issues
- Recommend (but don't require) fixes
- Allow user to proceed

#### Score < 60: BLOCK ✗
- **Do NOT save** if `quality.strict_mode: true`
- Display critical issues
- Require fixes before saving
- If strict mode disabled, save with prominent warnings

### 5. Reporting

Display results to user:

**PASS Example**:
```
✓ Quality Check Passed (Score: 87/100)
  Readability: 85/100
  Grammar: 95/100
  Structure: 90/100
  Voice Match: 88/100

Content saved successfully.
```

**WARN Example**:
```
⚠ Quality Check: Needs Improvement (Score: 72/100)
  Readability: 65/100 - Sentences averaging 28 words
  Grammar: 88/100 - 3 minor issues
  Structure: 80/100 - Missing clear CTA
  Voice Match: 55/100 - Tone more formal than usual

Suggestions:
- Break up longer sentences in paragraphs 2-4
- Add clear call-to-action in conclusion
- Adjust tone to match examples (more conversational)

Content saved with warnings. Consider addressing suggestions.
```

**BLOCK Example** (strict mode):
```
✗ Quality Check Failed (Score: 52/100)
  Readability: 45/100 - Average sentence: 35 words, Grade 14
  Grammar: 70/100 - 8 errors found
  Structure: 55/100 - No clear introduction hook
  Voice Match: 38/100 - Significant deviation from brand voice

CRITICAL ISSUES - Content NOT saved:
1. Readability too low - simplify sentence structure
2. Introduction missing hook - readers won't engage
3. Voice deviation - doesn't match your established style

Fix these issues and try again.
```

## Execution Flow

```
Content ready to save
  ↓
Run quality checks (parallel)
  ├→ Readability analysis
  ├→ Grammar check
  ├→ Structure validation
  └→ Voice matching
  ↓
Calculate scores
  ↓
Determine action (pass/warn/block)
  ↓
├─ Pass (80-100)
│  └→ Save content + success message
│
├─ Warn (60-79)
│  └→ Save content + warnings + suggestions
│
└─ Block (< 60)
   └→ Don't save + critical issues + required fixes
```

## Configuration

```yaml
# In .claudecode-writer/config.yml

quality:
  readability:
    target_grade_level: 8
    min_score: 60

  grammar:
    enabled: true
    auto_fix: false        # Auto-fix minor issues

  voice:
    strict_mode: false     # Require voice match
    similarity_threshold: 0.7

  strict_mode: false       # Block saves if score < 60
```

## Thresholds

### Readability
- **Excellent** (80-100): Easy to read, clear, concise
- **Good** (60-79): Acceptable, minor improvements possible
- **Poor** (< 60): Too complex, requires simplification

### Grammar
- **Excellent** (90-100): 0-2 minor errors
- **Good** (70-89): 3-5 minor errors
- **Poor** (< 70): 6+ errors or any critical errors

### Structure
- **Excellent** (80-100): All elements present, well-organized
- **Good** (60-79): Missing 1-2 optional elements
- **Poor** (< 60): Missing critical elements (intro, conclusion)

### Voice Match
- **Excellent** (80-100): Strong match to voice profile
- **Good** (60-79): Recognizable but some deviations
- **Poor** (< 60): Significant deviation from brand voice

## Quick Check vs. Full Analysis

This hook runs **quick checks** (< 2 seconds) to not slow down workflow.

For full detailed analysis, use:
```
/optimize [file]  # Runs content-analyzer skill
```

## Bypass Quality Check

Sometimes you need to save work-in-progress:

### Temporary Bypass
```
/write [topic] --skip-quality-check
```

### Disable Hook
```yaml
# config.yml
hooks:
  quality_check:
    enabled: false
```

### Disable Strict Mode (warnings only)
```yaml
quality:
  strict_mode: false  # Never block, only warn
```

## Auto-Fix Minor Issues

Enable auto-fixing of minor issues:

```yaml
quality:
  grammar:
    auto_fix: true  # Fix obvious typos, punctuation
```

Auto-fix handles:
- Common typos
- Double spaces
- Missing punctuation
- Capitalization errors
- Smart quote conversion

Does NOT auto-fix:
- Sentence structure
- Word choice
- Voice issues
- Complex grammar

## Integration Points

### Skills Used
- `content-analyzer` (quick mode)
- `voice-matcher` (quick mode)

### Related Hooks
- `pre-write` - Runs before this
- `post-write` - Runs after this
- `voice-validation` - Detailed voice check

### Related Commands
- `/optimize` - Full quality analysis and fixes
- `/write` - Creates content that gets checked

## Error Handling

If quality check itself fails:
1. Log the error
2. Display warning to user
3. Allow save to proceed
4. Suggest manual review

```
⚠ Quality check encountered an error
  Error: [details]

Content saved, but could not validate quality.
Please review manually before publishing.
```

## Performance

- **Target execution time**: < 2 seconds
- **Parallel execution**: All checks run simultaneously
- **Caching**: Results cached for 5 minutes
- **Incremental**: Only check changed content if possible

## Analytics

Track quality scores over time:
- Average score per content type
- Improvement trends
- Common issues
- Voice consistency trends

Save to: `analytics/quality-trends.json`

## Examples

### Example 1: Article Quality Check
```
/write "How to improve remote productivity"

[Article is created...]

Running quality check...

✓ Quality Check Passed (Score: 89/100)
  Readability: 88/100 - Clear and accessible
  Grammar: 98/100 - Excellent
  Structure: 85/100 - Well organized
  Voice Match: 92/100 - Strong authentic voice

Article saved: content/drafts/article-improve-remote-productivity-2024-11-18.md
```

### Example 2: LinkedIn Post Warning
```
[LinkedIn post being saved...]

⚠ Quality Check: Needs Review (Score: 68/100)
  Length: 1450 characters (optimal: 900-1300)
  Hook: Weak - value not clear in first 2 lines
  Engagement: Missing call-to-action question

Suggestions:
1. Trim by ~150 characters for optimal engagement
2. Strengthen opening hook to grab attention
3. End with specific question to drive comments

Post saved with warnings: content/drafts/linkedin-post-2024-11-18.md
```

### Example 3: Blocked Save (Strict Mode)
```
/write "Technical analysis of distributed systems"

[Article created...]

✗ Quality Check Failed (Score: 42/100)
  Readability: 28/100 - Grade 16, avg sentence 42 words
  Voice Match: 35/100 - Too technical, formal tone

CRITICAL: Content NOT saved

Required fixes:
1. Simplify sentence structure (target: grade 8-10)
2. Break up complex paragraphs
3. Add relatable examples and analogies
4. Adjust tone to match conversational style from examples

Review @context/writing-examples.md for voice guidance.
```

## Best Practices

1. **Set Appropriate Thresholds**: Match your quality standards
2. **Use Warnings, Not Blocks**: In most cases, warnings > blocking
3. **Review Suggestions**: Quality check learns from your patterns
4. **Update Voice Examples**: Keep examples current
5. **Monitor Trends**: Track quality improvements over time
6. **Platform-Specific**: Different standards for different platforms

## Troubleshooting

**Issue**: Quality check too strict
**Solution**: Lower thresholds or disable strict_mode

**Issue**: Quality check too lenient
**Solution**: Raise thresholds or enable strict_mode

**Issue**: Voice check failing consistently
**Solution**: Update @context/writing-examples.md with more/better examples

**Issue**: Slow execution
**Solution**: Disable some checks or use quick mode only

**Issue**: False positives on grammar
**Solution**: Adjust grammar sensitivity or disable
