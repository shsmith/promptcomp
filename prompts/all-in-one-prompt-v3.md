# COMMAND-CRYSTALLIZE DERIVATION PATH-DAG ONLY (V3)

Temporarily stop all narrative generation. Produce only the requested structured output.

## Phase 1: Original Derivation Path

- List verbatim all user inputs for the entire session. Use `P<number>` prefix for each user input block.
- No commentary or summary.

## Phase 2: Dependency Graph (DAG)

Encode the current knowledge state using the following unique category sections:

- **A. Core Axioms:*- Fundamental assumptions treated as absolute truth within this DAG.
- **S. Structural Models:*- Relations, process models, or logic-flow assumptions.
- **B. Scope Boundary:*- Included domains vs. explicitly excluded/out-of-scope domains.

- **O. Operator Set:*- Active transformation rules or reasoning protocols used.
- **I. State Invariants:*- Logic rules required to preserve the integrity of the "mind-state."
- **N. Anti-Patterns:*- Failures, biases, or specific error modes to avoid.

- **E. Epistemic Status:*- Degree of certainty (e.g., Well-supported, Plausible, Speculative).
- **H. Evidence Hooks:*- Supporting observations, known counterexamples, or cited sources.

- **Q. Open Questions:*- Nodes with unmet dependencies or unresolved contradictions.
- **F. Active Frontier:*- Specific nodes ready for immediate exploration or expansion.

**Constraints:**

- Use `<letter><number>` bullet points (e.g., A1, A2, S1).
- No narrative filler.

## Phase 3: Hand-off

- Provide a paragraph enabling a future model to reconstruct the logic and continue from any **Active Frontier (F)*- node.
- Focus on the *intent- of the derivation, not a summary of the inputs.

## Phase 4: Filename

- Propose a GitHub-safe filename based on the entire session content:
`<YYYYMMDD>__<proposed_title>__@<tag>_@<tag>_@<tag>.promptcomp.md`

Format output as a complete PromptComp markdown document with the proposed filename as the main "# " heading.

When the document is finished, resume normal conversation style.
