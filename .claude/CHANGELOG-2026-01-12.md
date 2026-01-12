# Changelog - January 12, 2026

## Summary

Critical updates to content quality and Red Hat style compliance. This release adds:
1. AsciiDoc formatting fixes (list spacing)
2. Clickable image requirements
3. **Plagiarism prevention validation**
4. **Em dash removal enforcement**

All changes enforce Red Hat Corporate Style Guide standards and protect against copyright issues.

---

## Key Changes

### 1. AsciiDoc List Formatting Rules (CRITICAL FIX)

**Problem**: Lists without proper blank lines cause text to run together when rendered in Showroom, making content unreadable.

**What Changed**:
- Added mandatory blank line requirements for all lists
- Updated verification prompts to actively scan for formatting violations
- Fixed demo template with proper spacing
- Added comprehensive examples in SKILL-COMMON-RULES.md

**Required blank lines**:
1. **Blank line BEFORE every list**
2. **Blank line AFTER every list** (before next content)
3. **Blank line after bold text or headings before lists**

**Before (broken rendering)**:
```asciidoc
**Benefits:**
* Cost reduction
* Faster deployment
Next section...
```

**After (correct rendering)**:
```asciidoc
**Benefits:**

* Cost reduction
* Faster deployment

Next section...
```

**Impact**:
- Prevents unprofessional rendering issues
- Improves readability for learners and presenters
- Reduces support burden from formatting confusion
- Maintains Red Hat brand quality standards

---

### 2. Clickable Images Requirement (ALL IMAGES)

**Problem**: Images in workshops/demos were not clickable, forcing users to lose their place to see details.

**What Changed**:
- ALL images must now include `link=self,window=blank`
- Updated both create-lab and create-demo skills with requirement
- Fixed all example code to show correct syntax
- Made it explicit in SKILL-COMMON-RULES.md

**Required syntax**:
```asciidoc
image::diagram.png[Description,link=self,window=blank,width=700,title="My Diagram"]
```

**Optional - Center alignment**:
```asciidoc
image::architecture.png[Architecture,link=self,window=blank,align="center",width=800,title="System Architecture"]
```

**Impact**:
- Learners can click images to see full resolution
- Opens in new tab - doesn't lose place in workshop
- Better user experience for detailed screenshots
- Consistent with team feedback from Nate Stephany

---

### 3. Verification Enhancements

**What Changed**:
- Both verification prompts now actively scan for list formatting issues
- Specific violations checked:
  - Bold text (`**Text:**`) immediately followed by list markers
  - Colons immediately followed by lists
  - Lists without blank lines before/after
  - Lists directly followed by paragraphs
- Detailed before/after examples in error reports
- Business/learning impact explanations

**Files Updated**:
- `.claude/prompts/enhanced_verification_demo.txt` (lines 160-232)
- `.claude/prompts/enhanced_verification_workshop.txt` (lines 170-244)

---

### 4. Template Fixes

**Demo Template** (.claude/templates/demo/02-details.adoc):
- Added blank lines after all section headings
- Fixed blank lines around all lists
- Fixed typos:
  - "introduct" → "introduce"
  - "interationss" → "interactions"

**Workshop Templates**:
- Verified all templates already have correct formatting
- No changes needed

---

### 5. Plagiarism Prevention and Content Originality (NEW REQUIREMENT)

**Problem**: Content copied from external sources creates copyright issues and damages Red Hat's reputation for thought leadership.

**What Changed**:
- Added Section 7 to SKILL-COMMON-RULES.md: Content Originality and Plagiarism Prevention
- Added Section 8 to redhat_style_guide_validation.txt: Plagiarism Prevention
- Updated both verification prompts with plagiarism detection
- Skills now actively check for copied content

**Prohibited Practices**:
- ❌ Copying documentation verbatim from external sources
- ❌ Slightly rewording existing tutorials or blog posts
- ❌ Copy/pasting from Stack Overflow, forums, or vendor docs
- ❌ Using AI-generated content without significant review
- ❌ Presenting others' examples as original work

**Required Practices**:
- ✅ Write original content in your own words
- ✅ Add Red Hat-specific context and implementation details
- ✅ Use proper attribution with quotes and citations
- ✅ Paraphrase completely, don't just rearrange words
- ✅ Add unique value beyond the original source

**Example Violation**:
```asciidoc
❌ WRONG - Copied from kubernetes.io:
Kubernetes is an open-source system for automating deployment, scaling,
and management of containerized applications.

✅ CORRECT - Original with attribution:
According to link:https://kubernetes.io/docs/...[Kubernetes documentation^],
Kubernetes is "an open-source system for automating deployment, scaling,
and management of containerized applications." Red Hat OpenShift extends
Kubernetes with enterprise features including integrated CI/CD, developer
tools, and enhanced security policies.
```

**Impact**:
- Protects Red Hat from copyright infringement
- Maintains Red Hat's thought leadership credibility
- Ensures authentic Red Hat expertise
- Builds customer trust through original content

---

### 6. Em Dash Removal - Red Hat Style Compliance (NEW REQUIREMENT)

**Problem**: Em dashes (—) don't follow Red Hat Corporate Style Guide and create inconsistent formatting.

**What Changed**:
- Added Section 8 to SKILL-COMMON-RULES.md: Punctuation Standards - No Em Dashes
- Added em dash rules to redhat_style_guide_validation.txt
- Updated both verification prompts to scan for em dash character (—)
- Skills now actively flag all em dash usage

**Required Replacements**:

| Use Case | Instead of Em Dash | Use This |
|----------|-------------------|----------|
| Parenthetical remark | "Platform—features—benefits" | "Platform, features, benefits" or "Platform (features and benefits)" |
| Break in thought | "Simple—just do this" | "Simple. Just do this." |
| Emphasis/list intro | "Three things—speed, scale, security" | "Three things: speed, scale, and security" |
| Range | "2020—2025" | "2020–2025" (en dash –) |

**Example Violations**:
```asciidoc
❌ WRONG - Em dash for parenthetical:
OpenShift—Red Hat's Kubernetes platform—simplifies deployments.

✅ CORRECT - Use commas:
OpenShift, Red Hat's Kubernetes platform, simplifies deployments.

✅ CORRECT - Use parentheses:
OpenShift (Red Hat's Kubernetes platform) simplifies deployments.

❌ WRONG - Em dash as separator:
The process is simple—just follow these 3 steps.

✅ CORRECT - Use period:
The process is simple. Just follow these 3 steps.

✅ CORRECT - Use colon:
The process is simple: just follow these 3 steps.
```

**Acceptable Dash Usage**:
- ✅ **En dashes (–)** for ranges: "2020–2025", "pages 10–15"
- ✅ **Hyphens (-)** for compound words: "multi-cloud", "real-time"
- ✅ **Regular dashes** in CLI commands: `--namespace`, `--output`

**Impact**:
- Follows Red Hat Corporate Style Guide
- Clearer punctuation improves readability
- Consistent formatting maintains quality standards
- Better translation for global audiences

---

## Files Changed

**Documentation**:
```
.claude/docs/SKILL-COMMON-RULES.md                              (+293 lines, sections 4, 7, 8 added)
.claude/prompts/enhanced_verification_demo.txt                  (+187 lines, 4 validation sections)
.claude/prompts/enhanced_verification_workshop.txt              (+193 lines, 4 validation sections)
.claude/prompts/redhat_style_guide_validation.txt               (+38 lines, sections 3, 8 added)
.claude/CHANGELOG-2026-01-12.md                                 (updated with 6 sections)
.claude/INTERNAL-DEVELOPER-GUIDE.adoc                           (+60 lines, quality standards)
CLAUDE-SKILLS-GUIDE.adoc                                        (+70 lines, formatting issues)
```

**Skills**:
```
.claude/skills/create-lab/SKILL.md                              (+11, -6)
.claude/skills/create-demo/SKILL.md                             (+10, -5)
```

**Templates**:
```
.claude/templates/demo/02-details.adoc                          (+9, -3)
```

**Global User Docs**:
```
~/.claude/showroom-skill-2026-01-12.md                          (created with full update summary)
```

**Total**: 11 files changed, 871 insertions(+), 14 deletions(-)

**Deployed to Repositories**:
- ✅ showroom-generative-ai-rag
- ✅ showroom-vllm-playground
- ✅ aap-selfserv-intro-showroom

---

## What This Means For Content Creators

### When Creating New Content

**Using /create-lab or /create-demo**:
- Skills automatically generate properly formatted lists
- All images will be clickable by default
- No action needed - it's built in

### When Verifying Existing Content

**Using /verify-content**:
Now checks for:
- ✅ Blank lines before/after all lists
- ✅ Blank lines after bold headings before lists
- ✅ All images include `link=self,window=blank`
- ⚠️ Provides specific fix instructions with examples

### When Fixing Existing Content

**List Formatting**:
1. Find lists in your content
2. Ensure blank line before first item
3. Ensure blank line after last item
4. Ensure blank line after bold headings

**Image Links**:
1. Find all `image::` macros
2. Add `link=self,window=blank` after alt text
3. Verify in Showroom preview

---

## Common Violations and Fixes

### Violation 1: Missing Blank Line Before List

❌ **WRONG**:
```asciidoc
Follow these steps:
. Step 1
. Step 2
```

✅ **CORRECT**:
```asciidoc
Follow these steps:

. Step 1
. Step 2
```

---

### Violation 2: Missing Blank Line After Bold Heading

❌ **WRONG**:
```asciidoc
**Prerequisites:**
* OpenShift installed
* Admin access
```

✅ **CORRECT**:
```asciidoc
**Prerequisites:**

* OpenShift installed
* Admin access
```

---

### Violation 3: Missing Blank Line After List

❌ **WRONG**:
```asciidoc
* First item
* Second item
Next section starts here
```

✅ **CORRECT**:
```asciidoc
* First item
* Second item

Next section starts here
```

---

### Violation 4: Non-Clickable Images

❌ **WRONG**:
```asciidoc
image::diagram.png[My Diagram,width=700,title="Architecture"]
```

✅ **CORRECT**:
```asciidoc
image::diagram.png[My Diagram,link=self,window=blank,width=700,title="Architecture"]
```

---

## Migration Guide

### For Existing Workshops/Demos

If you have content created before today:

1. **Run /verify-content** on your existing modules
2. Review formatting issues reported
3. Fix list formatting:
   - Add blank lines before/after lists
   - Add blank lines after headings
4. Fix image links:
   - Add `link=self,window=blank` to all images
5. Test rendering in Showroom preview
6. Commit changes

### For New Content

All new content automatically follows these standards - no action needed!

---

## Technical Details

### Verification Scanning Logic

The verification agents now use pattern matching to detect:
- `\*\*.*:\*` - Bold text immediately followed by list marker
- `:\n\.` or `:\n\*` - Colon immediately followed by list
- `\*.*\n[A-Z]` - List item followed by paragraph (no blank line)
- `image::[^\[]*\[[^\]]*\]` without `link=self,window=blank`

### AsciiDoc Rendering Behavior

AsciiDoc processors require blank lines to:
- Delimit block boundaries
- Separate lists from surrounding content
- Properly parse list markers vs plain text

Without blank lines, the renderer treats list markers as inline text, causing formatting collapse.

---

## References

**SKILL-COMMON-RULES.md Section 4**: Complete AsciiDoc list formatting guide
**SKILL-COMMON-RULES.md Section 5**: Image path conventions and clickable images
**Team Feedback**: Nate Stephany - clickable images requirement

---

**Last Updated**: January 12, 2026
**Repository**: showroom_template_nookbag (main branch)
**Status**: ✅ Committed
