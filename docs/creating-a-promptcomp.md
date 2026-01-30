# Creating a PromptComp

This guide walks through the practical process of extracting PromptComps from your LLM conversations.

## The Basic Flow

1. **Explore**: Have a productive conversation with an LLM
2. **Recognize**: Notice when you've reached an interesting knowledge state
3. **Extract**: Request verbatim prompts from the conversation
4. **Name**: Generate an appropriate filename with tags
5. **Archive**: Save as a `.promptcomp.md` file

## Step 1: Recognizing PromptComp Moments

Not every conversation is worth preserving. Look for these signals:

### Good Indicators
- You've solved a problem through iterative refinement
- You've reached a novel synthesis of ideas
- You've constructed a complex mental model step-by-step
- You want to show someone else your reasoning process
- You might want to branch from this point to explore variations

### Poor Indicators
- You got a simple factual answer
- The conversation wandered without clear direction
- You abandoned the thread before reaching resolution
- The knowledge state depends heavily on the AI's specific responses
- It's highly context-specific (debugging your unique setup)

**Rule of thumb**: If you'd struggle to explain what you learned without the full conversation, it's probably a good PromptComp candidate.

## Step 2: Extraction Prompts

### Basic Extraction

Use this prompt to get your inputs back:

```
Thank you for helping me explore these ideas. Please give back verbatim 
all of my original inputs (my prompts only) from this entire conversation, 
numbered in chronological order. Do not include your responses, commentary, 
or formatting--just my exact prompts as I wrote them.
```

### What You'll Get

The AI will return something like:

```
1. [Your first prompt]
2. [Your second prompt]
3. [Your third prompt]
...
```

**Important**: Review this list. Sometimes the AI includes clarifications or reformulations. Edit to keep only your actual inputs.

In a long conversation, some of your prompts may have already "windowed out". In that case, you should scroll back in the chat and manually copy paste them into the document.

### Advanced: Combined Extraction

If you want both prompts and a filename in one go:

```
CRYSTALLIZE this conversation into a PromptComp artifact.

Please provide:

1. **Verbatim Prompts**: All of my original inputs from this conversation, 
   numbered in order.

2. **Filename**: Generate a filename using format: 
   YYYYMMDD__Title__@Tag1_@Tag2.promptcomp.md

Format the response as a complete PromptComp document.
```

## Step 3: Filename Generation

### The Standard Format

```
YYYYMMDD__Brief_Descriptive_Title__@Tag1_@Tag2_@Tag3.promptcomp.md
```

**Components**:
- **Date**: When you crystallized this (YYYYMMDD format, like `20260128`)
- **Title**: Brief description, underscores instead of spaces
- **Tags**: 1-3 key concepts, each prefixed with `@`
- **Extension**: Always `.promptcomp.md`

### Choosing Tags

Tags should represent **concepts**, not just topics:

**Good tags** (abstract, reusable):
- `@architecture` - System design concepts
- `@ethics` - Ethical considerations
- `@optimization` - Performance/efficiency
- `@emergence` - Emergent behaviors
- `@alignment` - AI alignment concepts

**Poor tags** (too specific):
- `@my_project` - Not useful to others
- `@tuesday` - Too temporal
- `@gpt4` - Too implementation-specific
- `@question` - Too generic

### Filename Examples

```
20260128__Recursive_Self_Improvement__@safety_@capabilities.promptcomp.md
20260127__Token_Optimization_Patterns__@performance_@architecture.promptcomp.md
20260126__Value_Loading_Problem__@ethics_@alignment.promptcomp.md
```

### Generating Filenames Automatically

Ask the LLM:

```
Based on our conversation, propose a filename for this PromptComp 
using format: YYYYMMDD__Title__@Tag1_@Tag2.promptcomp.md

Use today's date (YYYYMMDD format), create a brief descriptive title 
with underscores, and choose 1-3 tags that represent key concepts 
from our discussion. Tags should be abstract and reusable, not 
conversation-specific.
```

## Step 4: Structuring the File

### Minimal Structure

The simplest PromptComp is just the numbered prompts:

```markdown
# 20260128__Example__@demo.promptcomp.md

1. [First prompt]
2. [Second prompt]
3. [Third prompt]
...
```

### Standard Structure

For better archival value, use this format:

```markdown
# 20260128__Example__@demo_@tutorial.promptcomp.md

## Context
[Optional 1-2 sentence description of what knowledge state this reaches]

## Prompts

1. [First prompt]
2. [Second prompt]
3. [Third prompt]
...

## Notes
[Optional: Branch points, alternative paths, projection suggestions]
```

### Advanced: DAG Structure

For complex PromptComps, you can include a dependency graph:

```markdown
# 20260128__Example__@demo_@tutorial.promptcomp.md

## Phase 1: Original Prompts

1. [First prompt]
2. [Second prompt]
...

## Phase 2: Dependency Graph (DAG)

### Axioms
- A1: [Core assumption established]
- A2: [Another foundational truth]

### Operators
- O1: [Key transformation or action]
- O2: [Another operation]

### Anti-patterns
- AP1: [Approach to avoid]
- AP2: [Another pitfall]

### Frontier
- F1: [Open question or next direction]
- F2: [Another unexplored area]

## Phase 3: Hand-off

[Instructions for how to resume or branch from this PromptComp]
```

**When to use DAG structure**: Only for PromptComps that establish formal frameworks or methodologies. Most PromptComps don't need this.

## Step 5: Archiving and Organization

### File Organization

Keep it simple:

```
my-promptcomps/
├── 20260128__topic_one__@tag1_@tag2.promptcomp.md
├── 20260128__topic_two__@tag3.promptcomp.md
├── 20260127__earlier_topic__@tag1_@tag4.promptcomp.md
└── ...
```

**Flat structure**: All files in one directory. Search by:
- Date: Sort alphabetically
- Topic: Read filename
- Tag: Grep for `@tagname`

**Avoid nested folders**: They impose false hierarchies. Tags are more flexible.

### Searching Your Collection

Find files by tag:

```bash
# All files about ethics
ls *@ethics*.promptcomp.md

# All files about both ethics and architecture
ls *@ethics*@architecture*.promptcomp.md

# On Unix/Linux
grep -l "@ethics" *.promptcomp.md
```

## Common Patterns

### Pattern 1: The Distillation

**Use case**: Long rambling conversation → extract the core insight

1. Have the messy conversation
2. Request verbatim prompts
3. **Edit ruthlessly**: Keep only the prompts that build the core path
4. Remove false starts, repetitions, clarifications
5. The result should be 30-50% of the original prompt count

**Example**: 20-prompt conversation → 8-prompt PromptComp

### Pattern 2: The Incremental Build

**Use case**: Step-by-step construction of something complex

1. Start with high-level concept
2. Each prompt adds detail or refinement
3. Maintain clear progression
4. Extract without editing (the build process is the point)

**Example**: 15-prompt sequence building a mental model

### Pattern 3: The Fork

**Use case**: Exploring alternative framings of the same problem

1. Establish base understanding (prompts 1-5)
2. Add note: "Branch point: Alternative framings below"
3. Path A (prompts 6-10)
4. Add note: "Alternative: Path B"
5. Path B (prompts 6-10 with different framing)

**Example**: Two approaches to the same design problem

### Pattern 4: The Meta-Composition

**Use case**: Building on previous PromptComps

1. Reference prior PromptComp: "Consider the approach in [filename]"
2. Build on that foundation with new prompts
3. In notes, link to the prior PromptComp
4. Can duplicate the prior content for self-containment, or keep it as reference

**Example**: Series of PromptComps building a framework

## Quality Checklist

Before archiving, verify:

- [ ] Contains only human prompts (no AI responses)
- [ ] Prompts are in chronological order
- [ ] Sequence is replayable (someone else could follow it)
- [ ] Filename follows convention (date, title, tags, extension)
- [ ] Tags are conceptual, not conversation-specific
- [ ] Any necessary context is in notes, not inline
- [ ] File is self-contained (or clearly references dependencies)

## Tips and Tricks

### Tip 1: Prepare for Extraction

As you're having the conversation, pause periodically and note where you are:
- "Let's checkpoint here. We've established X and Y."
- "This seems like a natural branch point."

These become navigation aids when extracting.

### Tip 2: Clean Up False Starts

Your actual conversation probably had backtracking:
- "Actually, forget that. Let me try again..."
- "Wait, I misunderstood..."

Remove these during extraction. Keep only the path that worked.

### Tip 3: Multiple Extractions

For very long conversations, you might extract multiple PromptComps:
- One for the main thread
- One for each major tangent that reached its own knowledge state

### Tip 4: Don't Over-Edit

Resist the urge to "improve" your prompts during extraction. The raw inputs are canonical for a reason--they show actual thinking process, not polished prose.

Exception: Fix obvious typos or formatting that would confuse replay.

### Tip 5: Date in Filename Matters

Use the date you crystallized the PromptComp, not when you had the conversation. If you extract and refine over several days, use the final date. This makes the filename reflect "when this knowledge state was stable," not "when I started exploring."

## Troubleshooting

### "The AI won't give me just my prompts"

Try being more explicit:

```
Please extract ONLY the text that I wrote, not your responses. 
Number each of my inputs from 1 to N. Do not paraphrase or 
summarize--give me my exact words.
```

### "The sequence doesn't make sense out of context"

Add a brief context note at the top:

```markdown
## Context
This exploration assumes basic familiarity with [concept]. 
It builds toward [goal] by establishing [approach].
```

### "I want to preserve some AI responses"

Then you're creating a different artifact (a conversation transcript, not a PromptComp). That's fine, but it's not the same thing. PromptComps preserve **derivation paths**, not complete conversations.

### "My prompts reference uploaded documents"

Add a note:

```markdown
## Note
Prompts 5-8 assume a document containing [description]. 
The full document is not included but is available at [link/location].
```

Or include the document content in an appendix if it's short.

## Next Steps

Once you have a PromptComp:

- **Replay it**: Feed it back into an LLM to verify it works
- **Branch it**: Start from any point and explore variations
- **Project it**: Ask for different format renderings (code, diagram, etc.)
- **Share it**: Contribute to this repo or share in your own collection
- **Build on it**: Reference it in future conversations

Remember: The PromptComp is the seed. Everything else grows from it.
