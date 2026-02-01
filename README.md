# PromptComp

**Save your prompts.**
LLM outputs are fungible. Your prompts, your derivation paths, are not.
PromptComp is a way to preserve, replay, and share the actual creative work.

**A new form of writing for the LLM era**

PromptComp (Prompt Composition) treats sequences of human prompts as first-class artifacts—executable prose that encodes knowledge states and can be replayed, shared, and projected into multiple formats.

## What is PromptComp?

Traditional writing assumes a static document. PromptComp recognizes that conversations with LLMs create **derivation paths**—specific sequences of prompts that lead to particular knowledge states. These sequences are:

- **Executable**: Feed them back into an LLM to reconstruct the knowledge state
- **Canonical**: The human prompts are the real artifact, not the AI responses
- **Projectable**: Once stabilized, they can render as code, diagrams, whitepapers, music, 3D worlds
- **Preservational**: The creative process itself is captured, not just its outputs

Think of it as musical notation for thought—a score that can be performed by any capable interpreter.

## Why This Matters

Most people use LLMs through long, rambling conversations that disappear into chat history. PromptComp extracts the **signal**—your actual creative inputs—from the noise. 

The result is:
- **Reproducible**: Anyone can replay your derivation path
- **Remixable**: Others can branch from any point in your sequence
- **Multi-modal**: The same prompt sequence can project into text, code, diagrams, or beyond
- **Archival**: Your intellectual labor is preserved in its purest form

## Repository Structure

```
promptcomp/
├── README.md              # You are here
│
├── blog/                  # Daily PromptComp entries
│   ├── 20260128__example__@demo_@tutorial.promptcomp.md
│   └── ...
│
├── contrib/               # Community contributions
│   └── README.md
│
├── docs/                  # Background and guides
│   ├── what-is-promptcomp.md
│   ├── creating-a-promptcomp.md
│   └── replaying-a-promptcomp.md
│
└── prompts/               # Ready-to-use prompts
    ├── all-in-one-prompt.md
    ├── request-DAG-prompt.md
    ├── request-filename-prompt.md
    └── request-inputs-verbatim-prompt.md
```

## Quick Start

### Reading PromptComps

Browse the `blog/` directory. Each file is a self-contained prompt sequence. Open any `.promptcomp.md` file and read the prompts—these are the canonical inputs that created a particular knowledge state.

### Creating Your Own

1. Have a productive conversation with an LLM

2. When you reach an interesting knowledge state, request verbatim extraction:

```
"Thank you for helping me explore these ideas. Please give back verbatim 
all of my original inputs (prompts only) from this conversation,  
in order. Do not include your responses."
```

3. Generate a filename:

```
"Based on our conversation, propose a filename using format: 
YYYYMMDD__Topic__@Tag1_@Tag2.promptcomp.md"
```

4. Save as a `.promptcomp.md` file in your own collection

### Contributing

See `contrib/CONTRIB_README.md` for guidelines. In brief:
- Submit complete PromptComp files (prompts only, self-contained)
- Use the standard filename format with `@tags`
- Refinements should be new files, not overwrites
- Include a brief context note if the derivation path needs it

## Filename Convention

```
YYYYMMDD__Descriptive_Title__@PrimaryTag_@SecondaryTag.promptcomp.md
```

- **Date**: When the knowledge state was crystallized (YYYYMMDD format)
- **Title**: Brief description using underscores instead of spaces
- **Tags**: Key concepts prefixed with `@`, separated by underscores
- **Extension**: `.promptcomp.md` for Markdown format

**Example**: `20260128__AI_Ethics_Framework__@alignment_@value_loading.promptcomp.md`

**Why `@` instead of `#`?** GitHub URLs stop parsing at `#`, but `@` works as both a filesystem tag character and in URLs.

## What PromptComps Are NOT

- **Not summaries**: PromptComps preserve the full derivation path, not just conclusions
- **Not essays**: They're executable sequences, not static narratives
- **Not prompt lists**: Random prompts don't create PromptComps; the sequence and order matter
- **Not AI outputs**: The AI responses are projections; prompts are the canonical form

## Philosophy

A PromptComp embodies these principles:

1. **Prompts-as-artifacts**: Human creative labor deserves preservation
2. **Derivational thinking**: The path to an idea is as important as the idea itself
3. **Projection-not-reduction**: One knowledge state, many representations
4. **Executable prose**: Writing that can be run, not just read
5. **Model-agnostic**: Any sufficiently capable LLM can replay the sequence

## Learn More

- [What is PromptComp?](docs/what-is-promptcomp.md) - Deep dive into the concept
- [Creating a PromptComp](docs/creating-a-promptcomp.md) - Step-by-step guide with examples
- [Replaying a PromptComp](docs/replaying-a-promptcomp.md) - How to use existing PromptComps

## The Blog

The `blog/` directory contains day-to-day PromptComp entries exploring various topics. These are not polished articles—they're raw derivation paths, preserved as they emerged from conversation.

Topics range from technical explorations of LLM behavior to philosophical inquiries about knowledge representation to practical problem-solving. Each file is tagged for searchability at the filesystem level.

Think of it as a lab notebook made public.

## License

This work is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). 
You may use, adapt, and build upon this material for any purpose, even commercially, as long as you give appropriate credit.

The PromptComp methodology itself is public domain—use it however you like.

---

**Status**: Active research preview. This repository evolves as the methodology crystallizes.

**Contact**: Submit issues or pull requests, or find me at [@shsmith](https://github.com/shsmith)
