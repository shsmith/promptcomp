# Replaying a PromptComp

This guide explains how to use existing PromptComps to reconstruct knowledge states and branch into your own explorations.

## What Replay Means

When you "replay" a PromptComp, you're:

1. **Reconstructing** the knowledge state by following the same derivation path
2. **Experiencing** the thought process that led to insights
3. **Preparing** to branch off in your own direction

Think of it like following a recipe, learning a dance from notation, or executing code from source. The PromptComp is instructions for reaching a cognitive destination.

## Basic Replay Process

### Step 1: Choose a PromptComp

Browse the collection and find something interesting. The filename tells you:
- **Date**: When it was created (recent = more likely to use current capabilities)
- **Topic**: What it's about
- **Tags**: Key concepts involved

### Step 2: Open Your LLM

Use any capable LLM interface:
- ChatGPT, Claude, or other web interfaces
- API-based tools
- Local models (if they're sophisticated enough)

**Important**: The LLM should be at least as capable as the one used to create the PromptComp. Using a less capable model might not work.

### Step 3: Feed Prompts Sequentially

Copy and paste each prompt, in order, into the LLM:

1. Send prompt #1
2. Read the response
3. Send prompt #2
4. Read the response
5. Continue through the sequence

**Do not skip prompts**. The knowledge state builds incrementally. 

**Do not merge all into one big prompt**. The response points matter to the LLM even if you don't read the intermediate responses.

### Step 4: Observe the Emergence

As you proceed, notice:
- How each prompt builds on the previous state
- Where the key insights crystallize
- Which prompts shift perspective or reframe the problem
- Where you might want to branch off

## Replay Strategies

### Strategy 1: Faithful Reconstruction

**Goal**: Reproduce the original knowledge state 

**Process**:
- Copy prompts verbatim
- Don't add your own commentary between prompts
- Let the derivation path unfold as intended
- Good for understanding the creator's thought process

**When to use**: 
- Learning a new conceptual framework
- Understanding someone else's reasoning
- Verifying that the PromptComp still works with current models

### Strategy 2: Active Exploration

**Goal**: Understand while annotating

**Process**:
- After each response, ask the LLM: "What did this prompt establish?"
- Or: "How does this build on the previous state?"
- Continue with the next prompt
- Good for metacognitive awareness

**When to use**:
- You want to deeply understand the structure
- You're learning how to create good PromptComps
- You're analyzing what makes this derivation path effective

### Strategy 3: Branching Replay

**Goal**: Reach the state, then diverge

**Process**:
- Follow the prompts until you reach an interesting point
- Stop and explore: "What if we approached this differently?"
- Try alternative framings
- Return to the main path or continue your branch

**When to use**:
- You want to build on someone else's work
- You see a different direction worth exploring
- You're remixing ideas

## Advanced Techniques

### Technique 1: Multi-Model Comparison

Run the same PromptComp through different LLMs:
- ChatGPT (GPT-4)
- Claude (Sonnet, Opus)
- Gemini
- Others

**What to notice**:
- Where they agree (robust insights)
- Where they diverge (model-dependent interpretations)
- Which model handles the sequence best

This reveals which parts of the knowledge state are universal vs. model-specific.

### Technique 2: Projection Practice

After replaying to the final state, ask for different projections:

```
Based on the knowledge state we've reached, please project this as:
- A technical whitepaper abstract
- A Python implementation outline
- A system architecture diagram (in text)
- An ELI10 explanation
- A list of potential failure modes
```

This helps you understand the knowledge state's nature and potential applications.

### Technique 3: Checkpoint Resume

For long PromptComps, create checkpoints:

1. Replay prompts 1-10
2. Use all-in-one-prompt.md
3. Save that artifact
4. Later: Start new chat with "Consider this state: [summary]"
5. Continue from prompt 11

This lets you resume long replays without starting over.

### Technique 4: Parallel Paths

If a PromptComp shows branch points, explore both:

1. Replay up to the branch (prompts 1-5)
2. Note the current state
3. Follow path A (prompts 6-10)
4. Start fresh, replay 1-5 again
5. Follow path B (alternative prompts 6-10)
6. Compare the resulting knowledge states

Reveals how different framings lead to different insights.

## Troubleshooting Replays

### Problem: "The LLM gives different responses"

**Expected**: LLMs are non-deterministic. Exact responses will vary.

**What matters**: Does the knowledge state converge to the same place?

**Test**: After finishing the sequence, ask: "What is the core insight we've established?" If this matches across replays, it worked.

### Problem: "A prompt seems to assume context I don't have"

**Solutions**:
1. Check the PromptComp's notes for required background
2. Ask the LLM: "What background knowledge does this prompt assume?"
3. Look for referenced documents or prior PromptComps
4. Add a setup prompt: "I'm replaying a PromptComp about X. Please prepare for a series of prompts building toward Y."

### Problem: "The sequence doesn't work with my model"

**Possible causes**:
- Model not capable enough (too small, too old)
- PromptComp is model-specific (mentions features not available)
- PromptComp is broken or incomplete

**Solutions**:
- Try a more capable model
- Adapt prompts to your model's capabilities
- Report issues to the PromptComp creator

### Problem: "I don't understand what we're building toward"

**This is normal** for your first few prompts. The knowledge state emerges gradually.

**If it persists**:
- Check the filename and tags for hints
- Read any context notes at the top of the file
- Ask the LLM: "What knowledge state are we constructing?"
- Consider that the PromptComp might be exploratory (destination emerged during creation)

## Branching from PromptComps

### When to Branch

Good branch points:
- After establishing foundational concepts
- When you see a different approach worth trying
- Where the PromptComp itself notes alternatives
- When you want to apply the framework to a new domain

### How to Branch

1. Replay up to your branch point
2. Note the knowledge state: "Let's checkpoint. We've established [X, Y, Z]."
3. Introduce your variation: "Instead of [original approach], let's try [your approach]."
4. Continue building your own sequence
5. Eventually extract your branch as a new PromptComp

### Citing the Source

If you create a new PromptComp by branching:

```markdown
## Context
This builds on the foundation from 
`20260128__Original_Topic__@tag1_@tag2.promptcomp.md` 
(prompts 1-7), then diverges to explore [your variation].
```

This maintains the derivation lineage.

## Getting Value Without Full Replay

Not every PromptComp needs full replay. Alternative uses:

### Quick Scan
- Read just the prompts (don't feed to LLM)
- Notice the progression and structure
- Extract the methodology
- Apply the pattern to your own work

**Good for**: Learning composition techniques

### Cherry-Picking
- Identify one or two key prompts
- Use those in your own conversations
- Don't worry about the full sequence

**Good for**: Finding useful framings or questions

### Template Extraction
- Notice recurring patterns across PromptComps
- "Oh, this type of prompt usually appears at this stage"
- Build your own templates

**Good for**: Developing your prompt craft

### Inspiration Mining
- Read to see what kinds of explorations are possible
- "I never thought to approach it that way"
- Adapt the strategy, not the specifics

**Good for**: Breaking out of habitual thinking

## Creating a Replay Library

If you replay PromptComps frequently:

### Organize by Purpose

```
replays/
├── to-learn/          # PromptComps teaching new concepts
├── to-adapt/          # Good templates for reuse
├── to-branch/         # Starting points for your work
└── completed/         # Ones you've fully explored
```

### Take Notes

After each replay, briefly record:
- What knowledge state it reaches
- Key insights or techniques
- Where you might branch
- How well it worked with your model

This builds your own index of "prompts I can start from."

### Share Your Findings

If you discover that a PromptComp:
- Works especially well with a particular model
- Benefits from additional context
- Has an interesting branch point
- Doesn't work as written

Share that via issues or contributions. Help improve the ecosystem.

## Ethical Considerations

### Attribution

When you:
- Branch from someone's PromptComp
- Use their prompts in your work  
- Build on their knowledge state

**Credit them** in your own PromptComp:
```markdown
## Acknowledgments
Prompts 1-5 adapted from [Author's PromptComp] (URL or filename)
```

### Modification

PromptComps are typically CC-BY licensed, meaning:
- You can use them freely
- You can modify them
- You can build on them
- You should attribute

But check the specific license.

### Commercial Use

If you:
- Build a product using insights from PromptComps
- Generate commercial content by replaying sequences
- Package PromptComp replays as a service

This is generally allowed under CC-BY, but **attribution is required**.

## Advanced: Automated Replay

For technically inclined users, you can automate replay:

```python
# Pseudocode - adapt to your API
prompts = parse_promptcomp("filename.promptcomp.md")

conversation = []
for i, prompt in enumerate(prompts):
    conversation.append({"role": "user", "content": prompt})
    response = llm.chat(conversation)
    conversation.append({"role": "assistant", "content": response})
    print(f"Prompt {i+1} response: {response[:100]}...")
```

**Use cases**:
- Testing PromptComps across multiple models
- Batch processing large collections
- Creating automated projection generators

## Next Steps

After replaying PromptComps:

1. **Create your own**: You now understand the structure
2. **Branch and contribute**: Extend existing work
3. **Build patterns**: Notice what makes good sequences
4. **Share learnings**: Help others replay effectively

The more people replay and branch, the richer the ecosystem becomes.

## Further Reading

- [Creating a PromptComp](creating-a-promptcomp.md) - Make your own
- [What is PromptComp?](what-is-promptcomp.md) - Deeper philosophy
- [Blog](../blog/) - Examples to practice with
