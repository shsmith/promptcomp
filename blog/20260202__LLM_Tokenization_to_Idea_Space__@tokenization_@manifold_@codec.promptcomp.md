# 20260202__LLM_Tokenization_to_Idea_Space__@tokenization_@manifold_@codec.promptcomp.md

## Phase 1: Original Derivation Path
1. "Are you familiar with the tokenizing process used by LLMs?"
2. "Have there been attempts to use ASCII or UTF-32 to represent characters? (i.e. no word tokenization)."
3. "Tokens are not used directly by the LLM, instead they are expanded into vectors. And those vectors are not 1:1 they vary depending on context and attention."
4. "So the root problem with ASCII or UTF-32 tokens are they don't offer many opportunities for different vector states compared to word or phoneme level tokens."
5. "Also a character model would not have a vocabulary of outputs, but only possible characters, which seems to shift the work to the sequencing and ordering of outputs. I wonder if this could scale down to a single bit input. Probably leads nowhere, just a thought experiment."
6. "I read somewhere that some NN models use "spiking" neurons where the signal is encoded by the frequency of spikes not presence or absence or amplitude."
7. "But of course in the brain there no single spike input, there are billions. So this probably won't scale either."
8. "How do non-text models work? Do they also tokenize and then use tokens to look up embedding vectors?"
9. "The LLM architecture seems kind of rube goldberg with an output for each word in the vocabulary (or each token). Consider continuous models like VJ-JEPA. Do those still use tokens? (i suspect not)."
10. "So in a JEPA model the input-to-vectors and vectors-to-output seems nearly universal. Back to LLM where we have vectors-as-inputs (via tokens via text). But the output is one per token. What if LLM output vectors and used a codec for that final vector-to-vocabulary step."
11. "Idea space is not the same as language space--most thought is non-verbal.  Consider that LLMs can quite easily translate between languages with human-level nuance. 
That makes me think that your core knowledge space is *not* in the form of any specific language, but rather in *ideas* that can later be serialized to language.   Language isn't just lossy compression; it's **lossy compression with reconstruction cues**. The serialized output is deliberately sparse *because* it's designed to trigger reconstruction in a recipient who shares the same cultural/contextual manifold."
12. "It all boils down to navigation within the vector space. If you permute all vector combinations it would produce such a large space it could represent all human knowledge and way more (maybe many orders of magnitude more)."
13. "The enumeration provides the "directory" or places within this space, and as you have pointed out, human knowledge is a tiny crystal relative to the galaxy of possible knowledge. The insight is that once we have trained the "shape" of this manifold into the model, we can extrapolate beyond the actual training, following the shape to a frontier of possible discoveries."

## Phase 2: Dependency Graph (DAG)
### A. Core Axioms
* A1. Thought is non-verbal; language serializes pre-verbal ideas.
* A2. Vector spaces have astronomical representational capacity (10^19,000+ points for 4096D float16).
* A3. Human knowledge occupies a tiny, structured manifold within the vast vector space.
* A4. Language is lossy compression with reconstruction cues, not the substance of thought.
* A5. Training learns manifold geometry, not just point memorization.
* A6. The shared cultural/contextual manifold enables reconstruction from sparse cues.

### B. Operator Set
* B1. Tokenization: Text → discrete tokens (subword, character, byte).
* B2. Embedding lookup: Token ID → continuous vector (static initial representation).
* B3. Self-attention: Contextual transformation of vectors (dynamic representation).
* B4. Manifold navigation: Extrapolation along learned curvature of idea space.
* B5. Codec-based generation: Separate idea formation (continuous) from expression (discrete).
* B6. Cross-modal tokenization: Patches (vision), spectrograms (audio), graphs, tabular data.

### C. Anti-Patterns
* C1. Conflating tokenization with thought (language as substrate rather than interface).
* C2. Fixed vocabulary output layers (O(vocab_size) scaling bottleneck).
* C3. Assuming discrete tokens are fundamental rather than compression artifacts.
* C4. Treating all modalities through text tokenization (losing modality-specific structure).
* C5. Equating sequence length explosion with lack of vector state capacity (misdiagnosis).
* C6. Ignoring the energy/compute scaling advantages of biological sparsity.

### D. Structural & Execution Models
* D1. Current LLM: Tokenization → Embedding → Transformer → Vocabulary projection → Token.
* D2. JEPA-style: Continuous latent space prediction without tokenization.
* D3. Codec-based LLM: Idea formation (continuous) → Codec decoder → Expression.
* D4. Manifold exploration: Training defines curvature, inference navigates geodesics.
* D5. Spiking Neural Networks: Event-driven, temporal coding, energy-efficient but scaling challenges.
* D6. Multi-level tokenization: Bits → bytes → characters → subwords → concepts.

### E. State Invariants
* E1. Idea space is continuous, high-dimensional, and compositional.
* E2. The learned manifold must remain smooth and traversable.
* E3. Separation between idea formation and expression must be maintained.
* E4. Navigation must respect manifold topology (avoid off-manifold hallucinations).
* E5. The reconstruction process assumes shared manifold between sender and receiver.

### F. Open Questions
* F1. How to explicitly train an "idea space" model without language as crutch? (Depends on B5, D3)
* F2. What codec architecture optimally maps idea vectors to text? (Depends on B5, D3)
* F3. Can SNNs scale to language tasks with brain-like efficiency? (Depends on C6, D5)
* F4. How to quantify uncertainty in manifold extrapolation? (Depends on B4, D4)
* F5. What manifold regularization prevents harmful extrapolation? (Depends on E4, D4)
* F6. How to align multi-modal manifolds (text, vision, audio)? (Depends on B6, D4)

### G. Active Frontier
* G1. Codec-based LLM architectures (decoupled idea formation and expression).
* G2. Continuous output spaces for language (avoiding vocabulary bottleneck).
* G3. Manifold extrapolation for scientific discovery.
* G4. Biological plausibility of SNNs for efficient navigation.
* G5. Cross-modal idea spaces (unified representation across modalities).
* G6. Sparse communication protocols optimized for different contexts.

## Phase 3: Hand-off
The current exploration has established that tokenization is an arbitrary compression layer atop a continuous idea space of vast representational capacity. The core insight positions language as lossy compression with reconstruction cues designed for a shared cultural manifold, not as the substrate of thought. The dependency graph reveals active frontiers in codec-based architectures that separate idea formation from expression, manifold extrapolation for discovery, and biologically-plausible efficient navigation. Continue from any Active Frontier node (G1-G6) by implementing the structural models (D1-D6) while adhering to core axioms (A1-A6) and avoiding anti-patterns (C1-C6). Maintain state invariants (E1-E5) while resolving open questions (F1-F6) through targeted experimentation.

