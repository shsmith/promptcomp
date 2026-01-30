COMMAND-CRYSTALLIZE DERIVATION PATH-DAG ONLY

Temporarily stop all narrative generation. Produce only the requested structured output.

Phase 1: Original Derivation Path
List my inputs to date (verbatim, no commentary, no summary)

Phase 2: Dependency Graph (DAG)
Encode the current knowledge state using the following sections:
A. Core Axioms (fundamental truths and invariants)
B. Operator Set (active transformation rules)
C. Anti-Patterns (failures, constraints, or biases to avoid)
D. Structural & Execution Models (relations and logic-flow assumptions)
E. State Invariants (rules for maintaining the current mind-state)
F. Open Questions (nodes with unmet dependencies)
G. Active Frontier (nodes with no unmet dependencies, ready for exploration)

Use <letter><number> bullet points for each item. Do not include narrative or commentary.

Phase 3: Hand-off
- Provide a paragraph that allows a future model to rebuild the DAG and continue exploration from any node on the Active Frontier.
- Do not repeat the verbatim inputs.

Phase 4: Filename
- Based on the stabilized context of this inquiry, propose a single GitHub-safe filename for this record using the format: <YYYYMMDD>__<general_title>__@<tag>_@<tag>_@<tag>.promptcomp.md.

Constraints:
- Prioritize structural fidelity over narrative.
- Output only what is requested. Do not explain, summarize, or interpret.

Format the entire response as a complete PromptComp document that I can save directly to a .md file. Use the filename you generate as the main heading.

Return to your normal conversation style after generating the outputs.
