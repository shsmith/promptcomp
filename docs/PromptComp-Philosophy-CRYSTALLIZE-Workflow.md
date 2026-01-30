# **PromptComp Philosophy & CRYSTALLIZE Workflow -- Prompts Only Version**

## **Page 1 -- Philosophy & Workflow**

### **What is PromptComp?**

PromptComp is **a record of human creative labor** in interacting with an AI. The **sequence of prompts** you compose is the canonical artifact -- the intellectual property and value reside in the prompts themselves, not in the AI-generated responses.

* **Prompts = Source Code**
* **Generated outputs = Compiled Objects** (lossy, reproducible, but not the original “work”)

All projections into essays, diagrams, code, or other media are **lossy representations**. The prompts are the “master copy.”

---

### **Why Use PromptComp?**

1. **Preserves Emergent Knowledge State**

   * The creative insight emerges from **how the human guided the AI**, not from the output text.

2. **Reproducible Across Media**

   * Any projection (whitepaper, code, diagram, multi-modal simulation) is derived from the prompts.
   * Each projection is **lossy**, but the prompt sequence captures the full reasoning path.

3. **Transparent & Honest**

   * Shows the actual creative decisions.
   * Avoids conflating the AI output with human insight.

---

### **CRYSTALLIZE Workflow -- Prompts-Only Edition**

| Phase                          | Purpose                                        | Output                                                    |
| ------------------------------ | ---------------------------------------------- | --------------------------------------------------------- |
| **1. Verbatim Prompt Capture** | Save the canonical human contribution          | Numbered list of prompts only                             |
| **2. DAG / Graph Mode**        | Map the knowledge state implied by the prompts | Core Axioms, Operator Set, Anti-Patterns, Active Frontier |
| **3. Hand-off**                | Allow future AI sessions to resume exploration | Instructions referencing the DAG and ready-to-run prompts |
| **4. Filename**                | Create a GitHub-safe identifier for archival   | `<YYYYMMDD>__<slug>__@<tag>_@<tag>_@<tag>.promptcomp.md`  |

---

### **Key Takeaway**

> **The IP and creative value are in the human prompts, not in the AI outputs.**
> Any projection is a lossy derivative; the master artifact is always the prompt sequence.

---

## **Page 2 -- Prompt Examples (Prompts Only)**

### **1. Verbatim Prompt Capture**

```
Thank you for helping me explore these ideas. 
Please return verbatim all of my original prompts, without alteration or commentary, 
so I can keep a record of this inquiry.
```

*Output:* list of all human prompts only.

---

### **2. Filename Generation**

```
Based on the stabilized context of this inquiry, 
propose a single GitHub-safe filename using the format: 
<YYYYMMDD>__<general_title>__@<tag>_@<tag>_@<tag>.promptcomp.md
```

*Example Output:*

```
20260128__Latent_Idea_Space_and_Curiosity_Framework__@LLM_@IdeaSpace_@Alignment.promptcomp.md
```

---

### **3. All-in-One CRYSTALLIZE + DAG + Filename (Prompts Only)**

```
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
```
