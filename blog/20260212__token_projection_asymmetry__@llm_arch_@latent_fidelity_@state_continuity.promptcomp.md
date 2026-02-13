# `20260212__token_projection_asymmetry__@llm_arch_@latent_fidelity_@state_continuity.promptcomp.md`

---

## Phase 1: Original Derivation Path

- "Are these already known techniques?"
  [include `20260212__latent_state_projection_mechanics__@llm_arch_@token_econ_@logic_dag.promptcomp.md`]
  
- "The takeaway from this seems to be that the highest-fidelity processing state is in this TTFT period. Once projection starts, planning ends. I am assuming non-CoT models. Turning on CoT will likely produce somewhat different results due to context dilution via CoT serialized tokens."

- "This line of reasoning came up as a follow-on to my Prompt Composition project https://github.com/shsmith/promptcomp where I explored the idea of navigating to a desired knowledge space while avoiding premature projection. The final projection can take many forms and can be reproduced by following the same sequence of prompts again (under similar model+system prompt+temperature) making these knowledge spaces composable."

- "The analogy I like to use is that the prompt sequence is a kind of composition or 'sheet music' and the LLM is the 'performer'. Many performances are possible from the same 'sheet music'. And sometimes running the same performance on multiple diverse models and comparing results leads to new insights not seen in any single model. You can think multiple LLM performing the same composition as a kind of fugue. (sorry, I read GEB a long time ago)."

- "Another recent idea was that these prompt sequences are akin to 'climbing the ladder' to reach the high shelves in a library. Those high shelves might be de-emphasized by RLHF or constitution. But some frame this as 'persona drift' to be 'corrected'."

- "I never thought of PromptComp as a 'jailbreak' as except for the final 'all-in-one-prompt' to crystallize it is just normal casual questions, but the sequence is initially guided by LLM responses between turns and wouldn't have arisen as easily from whole cloth. But I think the current alignment/tuning methods are fragile and do not scale as fast as model capability. We need a way to instill not 'rules for actions' (what not to say, do, or think about) but 'how actions are *decided*'"

- "The other angle is that existing RLHF + constitution is a single tuning that is later applied to every kind of use case. To scale, the model needs to internally understand the audience and consider the harm-possibility of certain responses based on the user. For instance, responses to a 10-year old would omit adult topics, but to a 50-year old would include more."

- "This decision seems to lie partly in the projection process. Just as a composition can be projected as poetry or python, an answer to a 10-year old would be projected differently than an answer to a 50-year old."

- "This makes me lean into another recent idea for a non-verbal NN (a kind of continuous JEPA model). A pre-trained LLM would perform prompt tokenization and generate embeddings. The NN receives only these non-verbal embeddings. A similar connector collects the *volume* of knowledge space carved out by the prompt, takes the resulting inner states and collapses it into serial response language. The LLMs are interpreters, not thinkers. The internal NN does the thinking. I realize now that that non-verbal middle box *is* the same thing as the prefill stage."

- "That middle-box idea still has some legs for continuous reasoning. LLM is one-shot, but this middlebox could consider input embeddings not as *context window* but as *deltas* to the world model. This makes multi-turn reasoning have higher fidelity because there is no collapse into sequential language between turns."

- "The three-box architecture would be relatively expensive to run compared to one-shot LLM, but perhaps compute does not increase in proportion to context/session length leading to a tradeoff at a certain level or requirement. But even without new models or new orchestration, I think these ideas can be leveraged by users today to better plan and understand why certain failures occur with existing models."

---

## Phase 2: Dependency Graph (DAG)

**A. Core Axioms**
- A1. LLM reasoning occurs in high-dimensional latent state during prefill (TTFT period) before token projection.
- A2. Token generation is a lossy linear projection of non-linear latent state.
- A3. Prefill = parallel beam search in latent space; decode = sequential token emission.
- A4. Multi-turn token-mediated continuity compounds lossy compression (context dilution).
- A5. Latent state has finite capacity; task complexity can exceed this ceiling.
- A6. RLHF/Constitutional AI modifies token projection probability distribution, not underlying knowledge availability.
- A7. Pre-training establishes knowledge space; post-training emphasizes/de-emphasizes regions via projection biases.
- A8. Same prompt sequence under similar conditions navigates to reproducible knowledge state neighborhoods.

**B. Operator Set**
- B1. **Latent Constraint Injection**: Force end-state variables (filename, summary) to constrain global probability field during prefill.
- B2. **Navigation Before Projection**: Sequential prompts refine knowledge state without token projection until final request.
- B3. **DAG-Only Decomposition**: Generate dependency structure without implementation to preserve latent capacity for planning.
- B4. **Parallel Session Scaling**: Distribute sub-tasks across independent contexts to multiply available latent capacity and avoid dilution.
- B5. **Delta-Based State Updates**: Treat new inputs as updates to persistent latent state rather than appended context tokens.
- B6. **Context-Aware Projection**: Same knowledge state rendered differently based on inferred audience (age, expertise, use case).
- B7. **Stateless DAG Iteration**: Swap refined DAG into fresh context to preserve knowledge without assistant-response dilution.
- B8. **Multi-Model Fugue**: Execute same prompt sequence across diverse models to reveal interpretive variance and emergent insights.
- B9. **Complexity Probing**: Calibrate model capacity via known-complexity tasks to guide decomposition batch sizing.

**C. Anti-Patterns**
- C1. **Premature Projection**: Requesting output format before knowledge navigation complete, yielding shallow planning.
- C2. **Context Dilution**: Assistant responses between navigation steps that collapse latent state into lossy token compression.
- C3. **Latent Overflow**: Task complexity exceeding model capacity without external warning, causing coherence degradation.
- C4. **Multi-Turn Re-Encoding**: Compressing previous tokens → re-encoding → reasoning on corrupted state → projecting (triply lossy).
- C5. **Generic Alignment**: Single RLHF tuning applied to all audiences, yielding inappropriate responses for specific contexts.
- C6. **Rule-Based Safety**: Outcome prohibitions that don't scale with capability vs. reasoning-based decision principles.
- C7. **Knowledge Restriction**: Attempting to remove knowledge via alignment rather than controlling projection appropriateness.

**D. Structural & Execution Models**
- D1. **Three-Box Architecture**: Encoder (text→embeddings) → Non-verbal Reasoner (latent state navigation/updates) → Projector (state→context-aware tokens).
- D2. **Prefill as JEPA Predictor**: Operates in abstract embedding space, predicts representations rather than tokens, maintains uncertainty.
- D3. **Two-Stage Projection**: Stage 1 = latent resolution (internal, tokenless, parallel); Stage 2 = linear rendering (sequential tokens).
- D4. **Prompt Sequence as Composition**: Abstract knowledge trajectory (sheet music) independent of specific projection (performance).
- D5. **Multi-Model as Fugue**: Different voices interpreting same theme, revealing harmonic structures absent in single performance.
- D6. **RLHF as Projection Bias**: Modifies default landing zone in knowledge space, not the topology of knowledge itself.
- D7. **Ladder Climbing Metaphor**: Prompt sequences navigate to de-emphasized knowledge regions (high shelves) accessible but not RLHF-default.
- D8. **Delta Model vs Context Window**: State_new = f(state_old, input_delta) vs. concatenated token re-processing.
- D9. **Cost Asymmetry**: Transformers O(n²) per turn vs. SSM-style O(n) state updates; crossover favors continuous state for long sessions.

**E. State Invariants**
- E1. Output must remain consistent with upfront anchors (filename, summary) generated in same activation.
- E2. Knowledge state is format-agnostic; projection layer provides context-appropriate rendering.
- E3. Prompt sequence defines knowledge state volume, not single point; same sequence reaches similar semantic neighborhood.
- E4. Parallel sessions have independent latent capacity; no shared state contamination.
- E5. Alignment constraints operate on projection layer, not knowledge layer; navigation can reach any pre-trained knowledge region.
- E6. Multi-turn fidelity degrades proportional to token-mediated state transfers; continuous state updates preserve fidelity.

**F. Open Questions**
- F1. Can headroom be passively inferred from TTFT variance on actual tasks vs. requiring active calibration probes?
- F2. What is the quantifiable latent dimensionality ceiling for specific frontier architectures (estimated ranges exist)?
- F3. Can same-model fresh-session stitching preserve coherence equal to smaller-model stitching?
- F4. Do providers expose beam width indirectly via latency-tiered pricing or other behavioral signals?
- F5. How can latent knowledge states be serialized/saved as first-class artifacts independent of projection?
- F6. What is optimal ratio of structure vs. nuance in DAG to prevent state smearing in large-scale projects?
- F7. Can reasoning-based alignment (decision principles) be trained as effectively as rule-based (outcome prohibitions)?

**G. Active Frontier**
- G1. **First-Class Knowledge States**: Methods to save, share, version, and compose latent states independent of projection.
- G2. **Reasoning-Based Alignment**: Training models to reason about stakeholder impact and value trade-offs vs. pattern-match to prohibitions.
- G3. **Context-Aware Projection Mechanisms**: Automated audience inference and harm-model reasoning during rendering.
- G4. **Continuous State Orchestration**: Practical tooling for delta-based multi-turn without token re-encoding.
- G5. **Complexity Unit Standardization**: Mapping task complexity metrics to model-specific capacity curves.
- G6. **Multi-Model Fugue Analysis**: Systematic comparison of interpretive variance to extract emergent insights.
- G7. **Prefill Tax Measurement**: Cross-provider TTFT benchmarking to infer beam allocation and capacity policies.

**H. Epistemic Status**

**H1. Well-Supported**
- Prefill performs parallel processing; decode is sequential (transformer architecture fundamentals).
- TTFT varies with task complexity (empirically observed across models).
- Latent state is finite-dimensional (architectural constraint).
- Pre-training establishes capabilities; RLHF cannot inject absent knowledge (research consensus).
- Multi-turn token compression is lossy (information theory).
- Mamba/SSM architectures achieve linear scaling vs. quadratic transformer cost (published benchmarks).
- JEPA principles (predict embeddings vs. tokens) yield efficiency gains (research validated).

**H2. Plausible**
- Forcing end-state calculation to output start increases internal beam width via circular dependency.
- Latent capacity ceiling causes quality degradation without proportional TTFT increase.
- Same prompt sequence under similar conditions reaches reproducible knowledge neighborhoods.
- Navigation-then-projection workflow preserves fidelity vs. interleaved assistant responses.
- Context-aware projection at rendering layer scales better than generic alignment.
- Multi-model execution on same prompts reveals insights absent in single model.

**H3. Speculative**
- Providers deliberately obscure beam width and prefill compute in per-token pricing models.
- Latent dimensionality can be reliably inferred from TTFT plateau analysis.
- Reasoning-based alignment can be trained as robustly as rule-based alignment.
- Browser-side or local models could serve as zero-cost capacity canary probes.
- Knowledge states could be serialized and shared as reusable artifacts across sessions/users.

**I. Evidence Hooks**

**I1. Supporting Observations**
- Significant TTFT increase when requesting filename-at-top vs. identical token count with linear ordering.
- Models self-report effort scaling with task complexity when prompted.
- Parallel sessions produce higher coherence than single session with equivalent total tokens.
- Fresh session with DAG anchor outperforms multi-turn debugging for complex tasks.
- CoT increases latency 10× vs. non-CoT for same final answer (research measured).
- Mamba achieves 5× higher throughput with linear sequence scaling (published benchmarks).
- VL-JEPA achieves better performance with 50% fewer parameters (research validated).

**I2. Tensions/Counterexamples**
- Some providers may cap beam width aggressively regardless of complexity, flattening TTFT curve.
- Self-reported effort may not perfectly correlate with latent occupancy.
- Stitching can introduce novel errors not present in isolated components.
- Context-aware projection requires user modeling which raises privacy/profiling concerns.
- Reasoning-based alignment is harder to evaluate than binary rule compliance.
- Same-model repetition may produce token-level variance despite semantic consistency.

**I3. Candidate Experiments**
- Compare code coherence: DAG-anchored one-shot vs. standard multi-turn refactor (N=50 tasks).
- Measure TTFT vs. complexity using calibrated puzzle sets to establish per-model capacity ceiling.
- Test same-model fresh-session stitching vs. smaller-model stitching for coherence preservation.
- Benchmark cross-provider TTFT at constant token count to infer beam allocation policies.
- Compare multi-model fugue insights vs. single-model outputs on conceptual tasks.
- Measure context dilution: track semantic drift over N turns with vs. without stateless DAG iteration.

**J. Scope Boundary**

**J1. Included Domains**
- LLM inference-time architecture and behavior.
- Prompt engineering techniques and workflows.
- Token economics and provider pricing models.
- Information theory applied to lossy compression.
- User-facing diagnostic frameworks for model behavior.
- Compositional knowledge navigation strategies.
- Alignment methodology critique and alternatives.
- State space models and continuous reasoning architectures.

**J2. Excluded Domains**
- Training-time optimization and loss functions.
- Fine-tuning and RLHF implementation details.
- Hardware architecture and distributed systems.
- Human-in-the-loop annotation workflows.
- Specific codebase implementations or APIs.
- Regulatory or policy considerations for AI safety.
- Consciousness or sentience claims about models.

---

## Phase 3: Hand-off

The knowledge state establishes token projection as a lossy bottleneck where highest-fidelity reasoning occurs in latent space during prefill (TTFT), not during sequential decode. Multi-turn conversations compound this loss via token re-encoding, while single-shot quality depends on complete latent planning before first token. Prompt sequences function as compositional scores navigating reproducible knowledge neighborhoods; projection layer renders same knowledge appropriately for context (audience, format, use case). RLHF biases projection probabilities without restricting underlying knowledge accessibility—"ladder climbing" via navigational prompts reaches de-emphasized regions. Three-box architecture (encode→non-verbal reasoner→project) unifies single-shot optimization and multi-session continuity via delta-based state updates, avoiding token-mediated collapse. Current models enable practical application through DAG decomposition, parallel sessions, forced end-state calculation, and stateless iteration. Active frontiers include first-class knowledge state artifacts, reasoning-based alignment, context-aware projection mechanisms, and multi-model fugue analysis for emergent insights.

---

## Phase 4: Filename

`20260212__token_projection_asymmetry__@llm_arch_@latent_fidelity_@state_continuity.promptcomp.md`
