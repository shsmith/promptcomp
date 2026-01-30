# Contributing to PromptComp

Thank you for considering a contribution! This repository grows through community participation.

## What to Contribute

### Good Contributions

**PromptComp files** that:
- Reach interesting knowledge states through clear derivation paths
- Are self-contained (can be replayed without external context)
- Follow the filename and tagging conventions
- Preserve the actual prompts you used (not polished rewrites)
- Could be useful to others learning similar concepts

**Improvements** like:
- Corrections to existing PromptComps (typos, broken sequences)
- Better tags or filenames for existing entries
- Additional context notes that help replay
- New documentation or guides

### Not Suitable for Contribution

- Essays or articles about PromptComp (those go elsewhere)
- AI-generated content without the prompts that created it
- Summarized or paraphrased prompt sequences
- Private/proprietary explorations
- Malicious, harmful, or misleading content

## Contribution Process

### Step 1: Prepare Your PromptComp

1. Follow the [Creating a PromptComp](../docs/creating-a-promptcomp.md) guide
2. Test that it replays successfully
3. Ensure filename follows convention: `YYYYMMDD__Title__@tag1_@tag2.promptcomp.md`
4. Add brief context notes if needed

### Step 2: Choose Location

**Your own PromptComps**: Add to `contrib/[your-username]/`

Structure:
```
contrib/
└── your-username/
    ├── 20260128__topic_one__@tag1.promptcomp.md
    ├── 20260128__topic_two__@tag2.promptcomp.md
    └── README.md (optional: describe your collection)
```

**Improvements to existing files**: Edit the file directly

### Step 3: Submit Pull Request

1. Fork this repository
2. Add your contribution
3. Create a pull request with description:

```
## Contribution Type
- [ ] New PromptComp
- [ ] Improvement to existing file
- [ ] Documentation enhancement

## Description
[Brief description of what this adds or improves]

## Testing
[How you verified this works - e.g., "Replayed successfully with Claude Sonnet 4"]
```

### Step 4: Review Process

Maintainers will check that:
- Follows filename and format conventions
- Contains actual prompts (not AI responses)
- Is self-contained or clearly notes dependencies
- Tags are appropriate and reusable
- Content is valuable to the community

**Timeline**: Most PRs reviewed within a week.

## Style Guide

### Filename Convention

```
YYYYMMDD__Brief_Title__@tag1_@tag2.promptcomp.md
```

- **Date**: YYYYMMDD format, the date you crystallized this
- **Title**: Descriptive, use underscores not spaces
- **Tags**: 1-3 conceptual tags, each with `@` prefix
- **Extension**: `.promptcomp.md`

### File Structure

Minimal acceptable format:

```markdown
# 20260128__Topic__@tag1_@tag2.promptcomp.md

1. [First prompt]
2. [Second prompt]
...
```

Recommended format:

```markdown
# 20260128__Topic__@tag1_@tag2.promptcomp.md

## Context
[1-2 sentences about what this explores]

## Prompts

1. [First prompt]
2. [Second prompt]
...

## Notes
[Optional: Branch points, dependencies, projection suggestions]
```

### Tag Guidelines

**Use abstract, reusable tags**:
- `@architecture` - System design
- `@ethics` - Ethical considerations  
- `@optimization` - Performance/efficiency
- `@emergence` - Emergent behaviors
- `@reasoning` - Logical frameworks

**Avoid over-specific tags**:
- `@my_project` - Too personal
- `@tuesday` - Too temporal
- `@claude` - Too model-specific
- `@broken` - Not a concept

### Content Standards

**Do**:
- Keep only your actual prompts
- Number prompts sequentially
- Preserve the order you used
- Note if prompts reference external files
- Add context if the derivation path needs it

**Don't**:
- Include AI responses in the main sequence
- Paraphrase or "improve" your original prompts
- Add editorial commentary between prompts
- Create fictional "ideal" prompt sequences that weren't actually used

## Quality Standards

Before submitting, verify:

- [ ] File contains only human prompts (no AI outputs)
- [ ] Prompts are numbered sequentially
- [ ] Filename follows convention exactly
- [ ] You've replayed it to confirm it works
- [ ] Any dependencies are noted clearly
- [ ] Tags are conceptual, not conversation-specific
- [ ] Content is appropriate for public sharing

## Types of Contributions

### Type 1: New Original PromptComp

**Best for**: Sharing your explorations with others

Place in: `contrib/[your-username]/`

Include:
- The PromptComp file itself
- Optional: README in your directory explaining your collection's focus

### Type 2: Branch from Existing PromptComp

**Best for**: Building on someone else's work

Place in: `contrib/[your-username]/`

Include in file:
```markdown
## Context
Builds on `20260128__Original__@tag.promptcomp.md` (prompts 1-7),
then branches to explore [your variation].
```

### Type 3: Improved Tagging

**Best for**: Making existing PromptComps more discoverable

Process:
1. Suggest better tags via issue
2. Or submit PR with filename change
3. Explain reasoning in PR description

### Type 4: Context Enhancement

**Best for**: Helping others replay successfully

Process:
1. Replay someone's PromptComp
2. Notice where context would help
3. Submit PR adding brief context notes
4. Don't change the prompts themselves

### Type 5: Documentation

**Best for**: Improving guides, examples, or templates

Place in: `docs/`

Focus on:
- Practical how-to content
- Real examples from the collection
- Patterns you've noticed
- Common troubleshooting

## What Happens After Submission

### Accepted PRs

Merged into the repository. You'll be credited as a contributor.

Your PromptComps remain in `contrib/[your-username]/` unless you request otherwise.

### Requested Changes

Maintainer may ask for:
- Filename adjustments
- Better tags
- Additional context
- Verification that it replays

Please respond within 2 weeks or the PR may be closed.

### Declined PRs

Rare, but might happen if:
- Content violates guidelines
- Not actually a PromptComp (wrong format)
- Too specific/personal to be useful
- Duplicates existing content

## Recognition

Contributors are:
- Listed in commit history
- Credited in their PromptComp files
- Acknowledged in periodic updates
- Invited to help maintain the collection

Significant contributors may be offered direct commit access.

## Code of Conduct

### Expected Behavior

- Share knowledge generously
- Respect others' creative process
- Provide constructive feedback
- Assume good intentions
- Help newcomers

### Unacceptable Behavior

- Harassment or discrimination
- Malicious content
- Spam or self-promotion
- Plagiarism (claiming others' prompts)
- Deliberately misleading content

### Enforcement

Violations result in:
1. Warning and request to fix
2. Temporary ban from contributing
3. Permanent ban for severe/repeated violations

Report issues to repository maintainers.

## Licensing

By submitting, you agree that:
- Your contribution is your original work (or properly attributed)
- You license it under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
- Others can use, adapt, and build upon it (even commercially) with attribution
- You retain copyright to your work

If you need different licensing terms, please discuss before submitting.

## Questions?

- **About PromptComp concept**: Read [docs/what-is-promptcomp.md](../docs/what-is-promptcomp.md)
- **About creating one**: Read [docs/creating-a-promptcomp.md](../docs/creating-a-promptcomp.md)
- **About replaying**: Read [docs/replaying-a-promptcomp.md](../docs/replaying-a-promptcomp.md)
- **Technical issues**: Open an issue
- **General questions**: Open a discussion

## Getting Started

New to contributing?

1. Browse existing PromptComps in `blog/` and `contrib/`
2. Try replaying a few
3. Create your first PromptComp locally
4. Test that it replays successfully
5. Submit it here

Welcome to the community!
