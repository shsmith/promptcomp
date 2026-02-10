# `20260208__voting_system_idempotence_mailIn__@cryptography_@verification_@auditability.promptcomp.md`

## Phase 1: Original Derivation Path

- Define idempotent.

- Now consider how these ideas apply to the vote counting process with computerized voting machines.

- One idea that comes to mind is to do the counting in two stages. The first stage creates a journal listing each bag and its contents. If the same bag is presented a second time, the same journal entry is reinforced without introducing duplication. The next stage uses these journal entries to calculate the final total.

- Another aspect: Voting systems need the following properties: 1) each authorized voter can vote only once, 2) the specific votes made by a voter must not be known (if authorities know what a voter voted for it could lead to intimidation), 3) An individual voter desires a mechanism to verify that her specific vote is included in the total.

- It is my understanding that many voting machines record individual votes in an internal memory device. Periodically poll workers will swap these memory devices, moving "filled" memories into a pipeline for final voting. What practical measures exist to avoid a specific memory device being counted more than once?

- The paper voter roll has some virtues compared to fully automated solutions. Each voter is matched to an entry in the roll book (authorization), and that entry is "crossed off" to prevent multiple voting (idempotence at collection point). The real risk seems to be downstream as these collected votes get integrated into the overall grand total.

- In my experience, not only does the poll worker "cross off" the entry for a voter, the voter is also asked to sign the roll. This signature prevents a poll worker from prematurely crossing off certain voters before they ever voted. Which leads to a reconciliation phase at the polling place: does the count of crossed-off entries equal the number of votes actually collected?

- An analogy came to mind: in the bitcoin "memory pool" we face (and solve) similar issues. The "secret ballot" guarantee stems from the disconnect from utxo and a specific individual. But as you pointed out, if a voter can get back a receipt confirming how she voted, then the secrecy requirement is not met.

- That made me think of "zero knowledge proofs" where actor A can prove to actor B that a fact is known without disclosing the fact to actor B.

- But voter A might fear her vote for candidate 1 was actually counted toward candidate 2. Perhaps this is unavoidable while preserving secrecy, but leaves the final count open to skepticism.

- So far this composition does not discuss "mail in voting". I think similar voter role matching could avoid duplication, and signature matching could avoid ballot stuffing. But what is a whole mailbag is never counted? Also the ability to "challenge" a specific mail-in vote seems to break the secrecy requirement.

- Also consider that in many places "sample ballots" are mailed to individuals authorized to vote, and these mail artifacts can be presented at the polling place as a form of identification. But the "didn't vote" vs "vote was lost" vs "vote was counted against the wrong candidate" all seem conflicted.

## Phase 2: Dependency Graph (DAG)

### A. Core Axioms

A1. Idempotence: f(f(x)) = f(x); repeated application yields identical result to single application

A2. Voting integrity trilemma: Authorization (one vote per eligible voter), Anonymity (unlinkable vote to voter), Verifiability (voter confirms inclusion) form mutually tensioned constraints

A3. Receipt-based verification breaks anonymity through coercion potential

A4. Physical chain-of-custody and cryptographic chain-of-custody are dual mechanisms for ensuring integrity

A5. Client-side trust (voting machine interface accuracy) remains irreducible without voter-verified audit trails

A6. Perfect mathematical guarantees for all three trilemma properties simultaneously are impossible

A7. States A (didn't vote), B (vote lost), and C (vote miscounted) are observationally equivalent from different perspectives

A8. Sample ballots used as authentication tokens create interception vulnerability without photo verification

A9. Distributed collection (mail-in) eliminates single reconciliation point present in precinct-based systems

A10. Challenge/cure processes create temporal windows where ballot-identity links exist and can be observed

### B. Operator Set

B1. Journal-aggregation pattern: Stage 1 creates idempotent records by bag/device identifier; Stage 2 sums unique journal entries

B2. Cryptographic hashing: Generate unique fingerprint per vote collection; reject duplicate fingerprints at aggregation

B3. Physical tamper-evidence: Seals with unique serial numbers plus chain-of-custody logging

B4. Reconciliation operator: Compare input count (signed voter roll) with output count (ballots cast) at collection point

B5. Zero-knowledge proof construction: Prove property about encrypted data without revealing plaintext

B6. Homomorphic encryption: Perform arithmetic operations on encrypted votes to yield encrypted totals

B7. Risk-limiting audit: Statistical sampling of paper trail to verify electronic count within confidence bounds

B8. Two-person integrity protocol: Require dual authorization for custody transfers

B9. Voter roll marking: Mark entry when mail-in ballot received (idempotent - duplicate processing doesn't duplicate mark)

B10. Signature verification: Authenticate outer envelope against registration records before ballot acceptance

B11. Two-envelope separation: Outer envelope (identity) separated from inner envelope (ballot) before counting

B12. Chain-of-custody manifest: Each mailbag gets custody log with envelope count at each transfer point

B13. Ballot tracking system: Confirm to voter when ballot mailed, received, signature verified, counted

B14. Statistical anomaly detection: Apply Benford's Law, geographic distributions to detect wholesale fraud patterns

B15. Challenge-response audit: Voter can demand ballot audit instead of casting; machine reveals encryption to prove correctness

B16. Sample ballot distribution: Mail preview ballot to registered voters

### C. Anti-Patterns

C1. Duplicate counting of same memory device/bag without detection mechanism

C2. Receipt systems that enable vote buying or coercion

C3. Premature voter roll invalidation without voter presence

C4. Aggregation without hash-based or serial-number-based deduplication

C5. Pure electronic systems without paper audit trail

C6. Closed-source voting software without public verification

C7. Individual vote decryption in end-to-end verifiable systems

C8. Assuming cryptographic anonymity (Bitcoin UTXO) equals true anonymity (graph analysis vulnerability)

C9. Accepting sample ballots as sole form of polling place identification

C10. Challenge/cure protocols that maintain permanent ballot-identity linkage

C11. Counting challenged ballots before separation from identity information

C12. Mail-in systems without ballot tracking or statistical validation

C13. Wholesale mailbag omission without detection through custody manifests or statistical analysis

C14. Client-side vote recording without voter-verified paper printout

C15. Systematic audit sampling that cannot detect targeted vote flipping

### D. Structural & Execution Models

D1. Two-stage pipeline: Collection → Aggregation, with idempotence enforced at collection boundary

D2. Voter roll as authorization ledger with physical/digital crossing-off operation

D3. Memory device as atomic vote batch with unique identifier

D4. Bitcoin mempool as analogue: UTXO pseudonymity, double-spend prevention, public verification

D5. End-to-end verifiable voting: Client encryption → Public commitment → Homomorphic tallying → Decrypted total

D6. Reconciliation as consistency check: Σ(authorizations) = Σ(ballots)

D7. Trust distribution: Client trust (interface), Process trust (chain-of-custody), Mathematical trust (cryptographic proof), Statistical trust (audit sampling)

D8. Mail-in two-envelope architecture: Outer envelope (signature, identity) → Verification → Separation → Inner envelope (anonymous ballot) → Batching → Counting

D9. Challenge window as temporal attack surface: Ballot-identity link exists until separation occurs

D10. Three-state observational equivalence: Didn't vote, vote lost, vote miscounted produce identical observations without instrumentation

D11. Sample ballot as dual-use artifact: Information channel and authentication token with conflicting security requirements

D12. Precinct-level vs system-level reconciliation: Local discrepancies detectable, distributed losses detectable only through statistical analysis or voter-initiated tracking

D13. Custody manifest chain: Each transfer point increments audit trail with count verification

### E. State Invariants

E1. Maintain distinction between collection-point idempotence and aggregation-point idempotence

E2. Recognize trilemma as constraint space rather than solvable problem

E3. Acknowledge cryptographic solutions address Anonymity-Verifiability tension but not Authorization-Interface trust

E4. Paper trails serve dual purpose: audit substrate and voter verification mechanism

E5. Coercion resistance requires unlinkability between voter action and public record

E6. Mail-in systems trade precinct-level reconciliation for distributed collection convenience

E7. Challenge processes create unavoidable tension between due process and ballot secrecy

E8. Individual vote content verification requires either anonymity violation or client trust assumption

E9. Wholesale omission attacks require different detection mechanisms than duplicate counting

E10. Sample ballots cannot serve authentication function without introducing impersonation vulnerability

### F. Open Questions

F1. Optimal cryptographic scheme balancing computational overhead, security assumptions, and voter comprehensibility

F2. Minimum audit sample size for given confidence level and margin of error

F3. Game-theoretic analysis of collusion scenarios in two-person integrity protocols

F4. Usability requirements for zero-knowledge proof interfaces in general-population voting

F5. Legal and procedural frameworks for dispute resolution when cryptographic and audit results diverge

F6. Quantum-resistant cryptographic primitives for long-term vote record integrity

F7. Mechanisms for voter verification without receipts (e.g., challenge protocols, cut-and-choose)

F8. Formal verification of voting system software against specification

F9. Can wholesale mailbag omission be detected without violating voter privacy?

F10. Is there a challenge/cure protocol that maintains ballot secrecy while providing due process?

F11. What is the minimum information required for a voter to verify ballot inclusion without enabling coercion?

F12. Can individual voter verify vote content correctness without breaking anonymity or enabling coercion?

F13. What audit sampling rate is required to detect targeted (non-systematic) vote flipping with 95% confidence?

F14. How to distinguish legitimate "didn't vote" from "mailbag lost" at scale?

F15. What cryptographic commitment reveals sufficient information for voter verification but insufficient for coercion?

F16. How to design sample ballots that provide information without creating authentication vulnerability?

F17. What observer protocols prevent deanonymization during challenge/cure windows?

F18. Can statistical methods distinguish systematic miscounting from targeted attacks on specific voter subsets?

### G. Active Frontier

G1. Design concrete journal schema for vote bag metadata (bag ID, hash, timestamp, custody chain, reconciliation status)

G2. Specify deduplication algorithm with hash collision handling and contested-bag resolution protocol

G3. Model attack vectors for memory device swapping protocol and corresponding countermeasures

G4. Compare homomorphic encryption schemes (Paillier, ElGamal, lattice-based) for vote tallying performance

G5. Develop voter-facing explanation of zero-knowledge verification process with user studies

G6. Prototype blockchain-based vote commitment system with privacy analysis

G7. Calculate audit sample sizes for various election margins and confidence requirements

G8. Design voter interface for challenge-response verification without coercible receipts

G9. Analyze Bitcoin UTXO graph analysis techniques applicability to voting commitment graph

G10. Specify reconciliation failure handling procedures (recount triggers, dispute escalation)

G11. Design custody manifest system with cryptographic commitments per mailbag

G12. Model statistical fraud detection sensitivity vs. false positive rate for mail-in votes

G13. Specify cryptographic mail-in ballot protocol with coercion resistance analysis

G14. Analyze observer-based deanonymization risk during challenge/cure window

G15. Design challenge-response protocol where voters can audit-instead-of-cast with usability testing

G16. Model impersonation attack surface when sample ballots are accepted as polling place ID

G17. Calculate detection probability for vote-flipping attacks under various audit strategies (random sample vs. risk-limiting vs. precinct-triggered)

G18. Specify voter-facing explanation: "Why you can't get a receipt showing how you voted"

G19. Design ballot tracking system architecture with privacy-preserving verification codes

G20. Formalize three-state observational equivalence detection matrix with instrumentation requirements

G21. Prototype statistical anomaly detection system for distributed mail-in collection with baseline establishment methodology

G22. Design two-envelope separation protocol with minimal challenge/cure window temporal exposure

G23. Specify alternative sample ballot design that provides information without authentication function

G24. Model targeted vote-flipping attack detection limits under various audit sampling strategies with game-theoretic adversary

## Phase 3: Hand-off

The exploration addresses idempotent operations in voting systems across precinct-based and mail-in architectures, identifying the fundamental tension between authorization, anonymity, and verifiability as an irreducible constraint space requiring hybrid cryptographic-procedural solutions. Core insight: precinct systems achieve reconciliation through temporal-spatial concentration (all voters present, immediate count comparison) while mail-in systems sacrifice this for convenience, requiring substitute mechanisms (custody manifests, ballot tracking, statistical validation) that detect different failure modes. The challenge/cure paradox exposes temporal attack surfaces where ballot-identity links necessarily exist. Sample ballots reveal dual-use artifact vulnerabilities when authentication and information functions conflict. Three-state observational equivalence (didn't vote, vote lost, vote miscounted) demonstrates that different failure modes produce identical observations without proper instrumentation checkpoints. Client-side trust remains irreducible: voter cannot verify vote content correctness without either breaking anonymity (linkage) or enabling coercion (receipt) or trusting interface (attack vulnerable). The Active Frontier contains 24 concrete nodes spanning technical implementation (G1-G4, G11, G13, G19, G22), cryptographic analysis (G6, G9, G13, G15), statistical methods (G7, G12, G17, G21, G24), usability design (G5, G8, G18, G23), security modeling (G3, G14, G16, G20), and formal specifications (G2, G10, G22). Mail-in systems introduce distributed collection without single reconciliation point, wholesale omission vulnerability, and challenge-window deanonymization risk as novel attack surfaces beyond precinct-based threats. Future exploration can branch from any G-node toward implementation prototypes, formal proofs, empirical validation, or adversarial analysis.

## Phase 4: Filename

`20260208__voting_system_idempotence_mailIn__@cryptography_@verification_@auditability.promptcomp.md`

---

The updated DAG now incorporates mail-in voting complexities, sample ballot vulnerabilities, and the three-state observational equivalence problem. 
The Active Frontier has expanded to 24 nodes, with several (G19-G24) specifically addressing the distributed collection and challenge/cure issues you identified.
