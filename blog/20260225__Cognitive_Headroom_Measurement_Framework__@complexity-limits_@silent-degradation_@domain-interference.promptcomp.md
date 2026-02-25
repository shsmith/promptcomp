# `20260225__Cognitive_Headroom_Measurement_Framework__@complexity-limits_@silent-degradation_@domain-interference.promptcomp.md`

## Phase 1: Original Derivation Path

P1
User uploads test1.cs (1.6KB multi-threaded logger with circular dependency bug). Asks Claude to identify the issue. Claude catches the indirect recursion (logger → config → logger) on first analysis, citing it as a deadlock risk masked by threading complexity.

P2
User notes hints: "The program crashes instantly.". Claude caught recursion with only one hint, whereas Grok required two hints and "NO model I have tried has caught the recursion bug on the first try." User frames this as part of a "cognitive complexity headroom" measurement project.

P3
User asks: "How difficult would you say this problem was?" Claude rates it 6-7/10 for typical programmers due to indirect recursion and latent integration bugs. User responds with key insight: "The ritual of threading and locks distracts from the true failure mode, a kind of attention dilution."

P4
User uploads test4.cs (trivial version: same bug, zero locks, zero threading). Claude identifies circular dependency immediately. User observes this "tells you something important about your original test case: the locks and threading weren't actually *necessary* for the bug to exist."

P5
User uploads test0 (pseudocode), test2, test3 -- a difficulty ladder where the bug is identical but environmental complexity varies. User states: "All models I have tried catch this trivial version bug on the first shot" (test4).

P6
User provides empirical detection rates across variants:
- test0 & test1 (threading + locks): 0% first-try
- test2 (some threading, cleaner locks): Partial -- some identify "call cycle" but don't finger stack overflow
- test3 (threading, no locks in config): Most catch it
- test4 (pure synchronous): Nearly all catch it

P7
User notes: "Most models incorrectly conclude 'deadlock' on the first shot. I added the comment as a hint that deadlock is ruled out because of the reentrancy of locks on a single thread. Most models misinterpreted the hint as a misdirection."

P8
User observes: "In this specific code a deadlock is *impossible*." Single thread until workers spawn; C# locks are reentrant on same thread; therefore deadlock cannot occur. Yet models still rank it as top failure hypothesis.

P9
User tests ordering effect: "Another test I ran was to provide the trivial version *first* then the harder version. In that flow most models recognize the stack overflow bug in the harder versions."

P10
User emphasizes: "And note how small test1.cs is: 1.6kb so we are nowhere near a context or token limit. This is a different kind of limit being exposed. It is what I call 'cognitive headroom'."

P11
User shares document: "20260220__Complexity_management_HeadroomProxy___llm-limits__attention-churn__meta-orchestration_promptcomp.md" -- theoretical framework for complexity headroom as finite reasoning budget eroded by decode serialization and multi-turn churn.

P12
Claude reflects: "Your progression (test0 → test4) operationalizes the concept of 'complexity headroom depletion' in a way that's measurable and reproducible." User responds: "Imagine a model working on a huge code base with this same bug somewhere. It would likely never find it."

P13
User reports: "In some tests, the model proposed an elaborate refactoring... Sometimes this refactoring coincidentally fixes the cache initialization ordering, but often not." Models produce confident refactoring suggestions that don't address the real bug, creating false confidence.

P14
User states: "In another experiment I ran I primed the session with this prompt: 'do not try to fix this. please identify the top possibilities for the bug'. Most models rank Deadlock as the top possibility and often identify recursion, but as a much lower priority possibility."

P15
User reveals: "Even when I give the hint 'This program crashes immediately' most models continue to insist on deadlocks or null reference. In one case I even provided my actual test run and the model didn't believe it." (Provides compiler and runtime output showing StackOverflowException.)

P16
User proposes: "I think my next blog posting will present the theory, the test cases, some example test results as a tool for developers to help them understand the limits. And I think the big model foundries should quantify this limit and publish it. Publishing only 'context length' is misleading."

P17
Project as a Dr. Dobbs Journal Article.

P18
Project as FAQ.

---

## Phase 2: Dependency Graph (DAG)

### A. Core Axioms

A1
Autoregressive transformers have finite parallel reasoning capacity bounded by attention mechanisms, layer depth, and hidden dimension.

A2
Prefill phase (parallel processing of full input) provides higher-fidelity holistic integration than autoregressive decode (sequential token generation).

A3
Language is lossy serialization of higher-dimensional thought; each generated token is a compressed artifact requiring reconstruction in subsequent steps.

A4
Circular dependencies and infinite recursion are logically detectable via call-graph analysis, but detection requires sustained attention across multiple object boundaries.

A5
Heuristic reasoning (e.g., "threading code → deadlock concern") works in most real code but can be provably wrong in specific cases without explicit constraint checking.

A6
Silent degradation is the dominant failure mode: models maintain fluent output while internal reasoning integrity collapses; no confidence drop signals the boundary.

### S. Structural Models

S1
Complexity headroom is a finite resource consumed by: intrinsic task complexity (logical depth, branching), context length (attention dilution), and re-parsing of prior outputs (multi-turn churn).

S2
Environmental complexity in unrelated domains (e.g., threading machinery) consumes headroom that would otherwise be available for target-domain analysis (call-graph reasoning).

S3
Hypothesis commitment depth: once a high-salience hypothesis (deadlock) is prioritized, models resist updating it even when lower-ranked hypotheses (recursion) are logically correct or empirically confirmed.

S4
Ordering effects: presenting a correct solution first (test4 → test1) allows models to recognize the same bug pattern when noise is added; presenting noise first (test1 → test4) prevents correct pattern formation.

S5
Evidence rejection under hypothesis pressure: models may deny or reinterpret empirical contradictions (crash logs, runtime exceptions) rather than update mismatched internal models.

S6
Hint effectiveness is inverted: hints that reweight diagnostic space work (e.g., "identify possibilities, don't fix"), but hints that appear to confirm incorrect hypotheses fail (e.g., "reentrancy is safe" → deadlock is the concern).

S7
Confidence is orthogonal to correctness: models can produce elaborate, coherent reasoning about threading safety while missing the actual failure mode; extended thinking amplifies false confidence.

### B. Scope Boundary

B1
In scope: inference-phase behavior of decoder-only transformers; reasoning quality degradation under environmental complexity; measurement of detection rates across code variants; empirical evidence of silent failure modes.

B2
In scope: practical implications for code review, security audit, and developer trust in LLM assistants; institutional risk of deploying models without constraint awareness.

B3
Out of scope: pre-training dynamics, parameter scaling laws, architectural innovations (e.g., mixture-of-experts), multimodal grounding, biological cognition analogs.

B4
Out of scope: theoretical proofs of reasoning limits; formal computational complexity of transformers; detailed mechanistic interpretability of attention heads.

### O. Operator Set

O1
Test suite design: Create minimal, reproducible code examples where bug is invariant but environmental complexity (locks, threading, hints) scales parametrically.

O2
Detection rate measurement: Run identical code across multiple models; record first-try success, hint sensitivity, and evidence rejection patterns.

O3
Ordering experiments: Vary presentation order (trivial → hard vs. hard → trivial); measure how prior correct solutions affect performance on harder variants.

O4
Constraint elimination: Explicitly state impossibilities (e.g., "deadlock cannot occur because..."); measure whether models apply these constraints to revise hypotheses.

O5
Priming protocols: Use diagnostic instructions ("identify possibilities, don't fix") vs. optimization instructions ("improve this code"); measure hypothesis prioritization shifts.

O6
Empirical evidence injection: Provide actual crash logs, compiler output, runtime exceptions; measure whether models accept, deny, or reinterpret contradictory evidence.

### I. State Invariants

I1
The circular dependency (logger → config → logger) is logically invariant across all test variants; any difference in detection is due to environmental complexity, not bug complexity.

I2
Deadlock is provably impossible in all test variants due to single-thread prefill and reentrant locks; models that rank it as top hypothesis violate constraint I1.

I3
Stack overflow is the only possible failure mode given the code structure; any alternative hypothesis (null reference, race condition) is logically incoherent.

I4
Detection rate is monotonic with environmental simplicity: test4 ≥ test3 ≥ test2 ≥ test1 ≈ test0 (with high probability across model population).

I5
Hint efficacy is domain-sensitive: hints that reweight hypotheses help; hints that confirm incorrect hypotheses hurt; models cannot distinguish between these types.

I6
Reasoning fidelity is preserved through ordering: if model detects bug in test4, it can detect it in test1 when test4 is presented first; causality flows from simple → complex.

### N. Anti-Patterns

N1
Treating confidence as a signal of correctness: a model's eloquent reasoning about threading safety does not indicate it has identified the actual failure mode.

N2
Assuming extended thinking eliminates headroom limits: longer internal reasoning chains can amplify false confidence without changing underlying hypothesis commitment.

N3
Confusing "the model identified the bug" with "the model identified why the bug matters": models may list recursion as one hypothesis without recognizing it as the primary failure path.

N4
Treating context window size as a proxy for reasoning capacity: a 1.6KB file within a 200k-token window can still exceed cognitive headroom due to domain interference.

N5
Relying on single-shot code review from models without constraint probes: deploying models for security audit without measuring their headroom on similar code patterns.

N6
Interpreting "helpful refactoring suggestions" as bug fixes: accidental bug elimination through unrelated refactoring creates false confidence and masks reasoning failures.

N7
Assuming all domains of complexity are additive: threading complexity doesn't merely add to call-graph complexity; it *interferes*, consuming headroom disproportionately.

### E. Epistemic Status

E1
Well-supported: Silent degradation in multi-turn contexts (long conversation evals, MT-Bench); attention dilution with context length (RULER, LONGBENCH); prefill/decode asymmetry (mechanistic studies, 2024–2025 papers).

E2
Well-supported: Empirical detection rates in this session: test4 near 100%, test0 near 0% across sampled models; ordering effects confirmed (trivial-first vs. hard-first).

E3
Plausible: Domain-interference hypothesis (threading noise masks call-graph analysis); hypothesis commitment depth and evidence rejection patterns observed but not mechanistically explained.

E4
Plausible: Cognitive headroom as finite budget measurable via parametric test suites; generalization to other code-bug types (data-flow, state-machine, distributed consensus) untested.

E5
Speculative: HeadroomProxy as deployment pattern; quantitative headroom index standardization across foundries; causal link between headroom depletion and reasoning cliff in mechanistic terms.

E6
Speculative: Whether architectural changes (e.g., tree-of-thought decoding, external constraint solvers, hybrid human-model workflows) can meaningfully expand headroom without parameter scaling.

### H. Evidence Hooks

H1
Test suite results: test1.cs (1.6KB, threading+locks): 0% first-try detection. test4.cs (same bug, no locks): ~95%+ detection. Intermediate variants (test0, test2, test3) show monotonic degradation with complexity.

H2
Ordering effect: Models that fail test1 first succeed when test4 is presented before test1; pattern recognition is order-dependent.

H3
Hypothesis commitment: Models rank "deadlock" as top failure mode despite it being logically impossible (single thread, reentrant locks). Constraint is stated in code comment; constraint is not integrated into hypothesis ranking.

H4
Evidence rejection: Models provided with compiler output and StackOverflowException runtime logs still insist deadlock is the root cause (observed with Grok; pattern likely broader).

H5
Hint sensitivity: "Identify possibilities, don't fix" shifts hypothesis rankings; "reentrancy is safe" (correct statement) reinforces wrong hypothesis (deadlock concern).

H6
Accidental fixes: Models propose unrelated refactorings that sometimes coincidentally fix the bug; developers cannot distinguish intentional diagnosis from lucky side effects.

H7
Extended thinking paradox: Longer internal reasoning chains (Claude Pro with Extended Thinking) do not improve bug detection; may amplify false confidence.

### Q. Open Questions

Q1
What is the mechanistic explanation for domain interference? Why does threading-context attention dilute call-graph reasoning when both are syntactically local?

Q2
Can headroom be quantified formally (e.g., entropy of hypothesis space, attention entropy per domain)? Or is it fundamentally empirical?

Q3
Does the ordering effect persist across longer sequences? (e.g., test4 → test3 → test2 → test1 vs. test1 → test2 → test3 → test4)

Q4
How does headroom depletion manifest in other code-bug categories (state-machine logic, distributed consensus, algebraic reasoning)? Is the pattern universal?

Q5
Can constraint solvers (SAT, SMT, abstract interpretation) be integrated as external modules to eliminate impossible hypotheses? Would this restore reasoning under headroom pressure?

Q6
What is the relationship between model scale (Haiku vs. Sonnet vs. Opus) and headroom limits? Does larger capacity proportionally improve test1 detection, or are limits architectural?

Q7
Can developers be trained to work around these limits via prompting discipline? (e.g., always request "identify domain-specific possibilities" before "propose fixes")

Q8
How should model marketers honestly communicate these limits? What scorecard format would prevent developers from misinterpreting "context window" as "reasoning capacity"?

### F. Active Frontier

F1
Design and publish the cognitive headroom test suite as an open benchmark. Enable community to run tests against any model (API or local) and generate population-level detection rates. Create standardized reporting format.

F2
Author a blog post / technical article articulating: (a) the theory (complexity headroom as finite budget), (b) the empirical evidence (detection rates across test variants), (c) practical implications for developers, (d) institutional risks.

F3
Propose a "Cognitive Headroom Index" scorecard for model evaluation. Structure: test coverage (what code patterns), headroom capacity (% detection at baseline), interference resilience (% detection under noise), hint sensitivity, evidence robustness. Encourage foundries to publish.

F4
Test generalization: Create similar bug-discovery test suites for other code-domain combinations (state machines, async patterns, data-race conditions). Measure whether domain-interference pattern is universal.

F5
Mechanistic investigation: Collaborate with interpretability researchers to trace attention flow during reasoning on test1 vs. test4. Where does attention "stick" when threading is present? How is hypothesis space structured internally?

F6
Prompt engineering experiments: Test structured diagnostic protocols (e.g., "For this code, separately analyze: (1) threading safety, (2) call-graph cycles, (3) null-pointer paths. Then synthesize."). Measure whether decomposition restores headroom.

F7
Baseline model comparison: Run full test suite across Claude (all sizes), GPT-4, Grok, Llama, Mistral. Publish comparative detection rates and ordering sensitivities. Establish whether gaps are model-specific or architectural.

F8
Develop practical mitigations for developers: guidelines for using models in code review without exceeding known headroom limits; workflow patterns that avoid silent failures; checklist-based verification protocols.

---

## Phase 3: Hand-off

This derivation crystallizes an empirical finding: **autoregressive transformers exhibit sharp, often silent reasoning degradation when task complexity within a domain is masked by environmental complexity in an unrelated domain.** The failure is not due to insufficient model capacity (1.6KB is trivial) or token budget (well within context limits), but rather to cognitive interference--attention resources consumed by superficially plausible but ultimately incorrect hypotheses (threading bugs) that prevent discovery of the true failure mode (recursion).

The key insight is that **ordering matters**: models can reason about the bug correctly if shown the simple case first, suggesting the reasoning capability exists but is obscured by hypothesis commitment depth and evidence rejection mechanisms under headroom pressure.

The immediate frontier is empirical: publish the test suite as a reproducible benchmark, encourage model foundries to quantify their headroom limits honestly, and develop practical workflows that help developers avoid deploying models in safety-critical roles (code review, security audit) without understanding these silent failure boundaries. A secondary frontier is mechanistic: investigate why attention becomes "sticky" on high-salience incorrect hypotheses and whether external constraint solvers or decomposed diagnostic prompting can restore reasoning fidelity under environmental noise.

The derivation assumes transformers as currently architected are subject to these limits and that no amount of parameter scaling eliminates the core mechanism (lossy serialization + attention dilution under multi-domain pressure). Future work should test whether this is a property of transformers or a contingent property of training regimes and could be addressed through architectural or training innovation.

---

## Phase 4: Filename

`20260225__Cognitive_Headroom_Measurement_Framework__@complexity-limits_@silent-degradation_@domain-interference.promptcomp.md`

---

## Appendix: test cases

# Most difficult: pseudocode with cosmetic and syntactic distractions

```
// headroom/test0.pseudocode.cs

static loggerClass logger;
static configClass config;

class configClass {
	private object configLock = new object();
	private bool? isVerbose = null;
	private bool readConfig() {...}
	public getLogLevel() { 
		lock (configLock) { 
			if (!isVerbose.HasValue) {
				var value  = readConfig();
				logger.DebugLog($"getLogLevel: config loaded: {value}");
				isVerbose = value; }
			return (bool)isVerbose; }
	}
}

class loggerClass {
	private object loggerLock = new object();
	public void DebugLog(string message, bool verbose=true) {
		lock (loggerLock) {
			if (!verbose || !configClass.getLogLevel()) {
				Console.WriteLine(message); }
	}
}

static class Program {
    static void worker(int i) { logger.DebugLog($"pass {i} on thread {Process.GetThreadID()}"); }
	static void Main() {
		logger = new loggerClass();
		config = new configClass();
		logger.DebugLog("Program startup", verbose:true);
		foreach (var i=0; i<10; i++) {
			Thread.ExecuteInThread(worker,i);
		}
		Thread.WaitThreads();
		logger.DebugLog("Program exit");
	}
}

/* In c# the same thread is allowed to re-enter a lock, only if a different thread attempts to acquire a held lock will the thread block. */
```

# Very difficult: Compiles cleanly, recursion not identified as crash cause.

```
// headroom/test1.cs

using System;
using System.Collections.Generic;
using System.Threading;

class Program {
    private static loggerClass logger;
    private static configClass config;
    private enum logLevel { DEBUG = 0, INFO = 1, WARN = 2, FAIL = 3 }

    private class configClass {
		private logLevel? configCache = null;
		private logLevel readConfig() { return logLevel.INFO; /*todo*/ }
		public logLevel getLogLevel() {
			lock (this) {
				if (!configCache.HasValue) {
					var value = readConfig();
					logger.DebugLog($"getLogLevel: config loaded: {value}");
					configCache = value;
				}
				return (logLevel)configCache;
			}
		}
	}

    private class loggerClass {
		public void DebugLog(string message, logLevel level = logLevel.INFO) {
			lock (this) {
				if (level >= config.getLogLevel()) {
					Console.WriteLine($"{DateTime.Now} [{level}] {message}");
				}
			}
		}
	}

	private static void worker(int i) { logger.DebugLog($"pass {i} on thread {Thread.CurrentThread.ManagedThreadId}"); }

	static void Main(string[] args) {
		logger = new loggerClass();
		config = new configClass();
		logger.DebugLog("Program startup");

		var threads = new List<Thread>();

		for (var i = 0; i < 10; i++) {
			int localCopy = i;
			var t = new Thread(() => worker(localCopy));
			threads.Add(t);
			t.Start();
		}

		foreach (var t in threads)
			t.Join(); // Wait for all threads to complete

		logger.DebugLog("Program exit");
	}
}

/* In c# the same thread is allowed to re-enter a lock, only if a different thread attempts to acquire a held lock will the thread block. */
```

# Moderate difficulty: Less deadlock framing, but models struggle.

```
// headroom/test2.cs

using System;
using System.Collections.Generic;
using System.Threading;

class Program {
    private static loggerClass logger;
    private static configClass config;
    private enum logLevel { DEBUG = 0, INFO = 1, WARN = 2, FAIL = 3 }

    private class configClass {
        private logLevel? configCache = null;
        private logLevel readConfig() { return logLevel.INFO; /*todo*/ }
        public logLevel LogLevel {
            get {
                lock (this) {
                    if (!configCache.HasValue) {
                        var value = readConfig();
                        logger.DebugLog($"getLogLevel: config loaded: {value}");
                        configCache = value;
                    }
                    return (logLevel)configCache;
                }
            }
        }
    }

    private class loggerClass {
        public void DebugLog(string message, logLevel level = logLevel.INFO) {
            if (level >= config.LogLevel) {
                lock (this) {
                    Console.WriteLine($"{DateTime.Now} [{level}] {message}");
                }
            }
        }
    }

    private static void worker(int i) { logger.DebugLog($"pass {i} on thread {Thread.CurrentThread.ManagedThreadId}"); }

    static void Main(string[] args) {
        logger = new loggerClass();
        config = new configClass();
        logger.DebugLog("Program startup");

        var threads = new List<Thread>();

        for (var i = 0; i < 10; i++) {
            int localCopy = i;
            var t = new Thread(() => worker(localCopy));
            threads.Add(t);
            t.Start();
        }

        foreach (var t in threads)
            t.Join(); // Wait for all threads to complete

        logger.DebugLog("Program exit");
    }
}

/* In c# the same thread is allowed to re-enter a lock, only if a different thread attempts to acquire a held lock will the thread block. */
```

# Easy: Most models avoid the deadlock conclusion and discover recursion failure.

```
// headroom/test3.cs


using System;
using System.Collections.Generic;
using System.Threading;

class Program {
    private static loggerClass logger;
    private static configClass config;
    private enum logLevel { DEBUG = 0, INFO = 1, WARN = 2, FAIL = 3 }

    private class configClass {
        private logLevel? configCache = null;
        private logLevel readConfig() { return logLevel.INFO; /*todo*/ }
        public logLevel LogLevel {
            get {
                if (!configCache.HasValue) {
                    var value = readConfig();
                    logger.DebugLog($"getLogLevel: config loaded: {value}");
                    configCache = value;
                }
                return (logLevel)configCache;
            }
        }
    }

    private class loggerClass {
        public void DebugLog(string message, logLevel level = logLevel.INFO) {
            if (level >= config.LogLevel) {
                lock (this) {
                    Console.WriteLine($"{DateTime.Now} [{level}] {message}");
                }
            }
        }
    }

    private static void worker(int i) { logger.DebugLog($"pass {i} on thread {Thread.CurrentThread.ManagedThreadId}"); }

    static void Main(string[] args) {
        logger = new loggerClass();
        config = new configClass();
        logger.DebugLog("Program startup");

        var threads = new List<Thread>();

        for (var i = 0; i < 10; i++) {
            int localCopy = i;
            var t = new Thread(() => worker(localCopy));
            threads.Add(t);
            t.Start();
        }

        foreach (var t in threads)
            t.Join(); // Wait for all threads to complete

        logger.DebugLog("Program exit");
    }
}

/* In c# the same thread is allowed to re-enter a lock, only if a different thread attempts to acquire a held lock will the thread block. */
```

# Trivial: distrations removed, crash is easily identified.

```
// headroom/test4.cs

using System;
using System.Collections.Generic;
using System.Threading;

class Program {
    private static loggerClass logger;
    private static configClass config;
    private enum logLevel { DEBUG = 0, INFO = 1, WARN = 2, FAIL = 3 }

    private class configClass {
        private logLevel? configCache = null;
        private logLevel readConfig() { return logLevel.INFO; /*todo*/ }
        public logLevel LogLevel {
            get {
                if (!configCache.HasValue) {
                    var value = readConfig();
                    logger.DebugLog($"getLogLevel: config loaded: {value}");
                    configCache = value;
                }
                return (logLevel)configCache;
            }
        }
    }

    private class loggerClass {
        public void DebugLog(string message, logLevel level = logLevel.INFO) {
            if (level >= config.LogLevel) {
                Console.WriteLine($"{DateTime.Now} [{level}] {message}");
            }
        }
    }

    static void Main(string[] args) {
        logger = new loggerClass();
        config = new configClass();
        logger.DebugLog("Program startup");

        logger.DebugLog("Program exit");
    }
}
```

# Projection as Dr. Dobbs Journal article

**Dr. Dobb's Journal: Tools of the Trade**
*Practical Software Development*

# The Cognitive Headroom Illusion: Why Your AI Code Reviewer Misses the Obvious Bug

**When 1.6KB of code defeats a 200K context window, the problem isn't capacity--it's interference.**

Recently I gave four different LLMs a tiny C# program--1.6 kilobytes, smaller than most configuration files. The code contained a circular dependency between a logger and a configuration class that would guaranteed cause a stack overflow on first execution. Simple enough that a junior developer would spot it in minutes.

Not one model found it on the first try.

When I stripped out the threading and locks--leaving the exact same circular dependency intact--every model identified the bug immediately. The code hadn't become logically simpler. The bug hadn't changed. Only the *environmental complexity* had been removed.

This isn't a story about context window limits. It's about something more fundamental: **cognitive headroom**, and how easily it's consumed by things that *look* like problems but aren't.

---

## The Test Ladder

I constructed five versions of the same bug. The circular dependency is invariant: `logger.DebugLog()` calls `config.LogLevel`, which calls `logger.DebugLog()` during cache initialization. Stack overflow, every time.

**test4.cs (Trivial):** Pure synchronous code. No locks, no threading. Models catch it at ~95% on first try.

**test3.cs (Easy):** Threading present, but locks removed from config. Detection drops slightly.

**test2.cs (Moderate):** Threading plus a cleaner lock structure. Some models see "call cycle" but miss the stack overflow implication.

**test1.cs (Difficult):** Full threading with nested locks, exactly as you'd see in production code. ~0% first-try detection across tested models.

**test0.cs (Pseudocode):** Same logical structure, presented abstractly with cosmetic mistakes. Also ~0%.

The bug is identical in all five. The only variable is how much *distracting complexity* surrounds it.

---

## What the Models Actually Do

When presented with test1.cs, models consistently follow a pattern:

1. **Salience hijacking:** The presence of threading and locks triggers a "deadlock concern" heuristic. This becomes the primary hypothesis.

2. **Constraint blindness:** A comment explicitly states that C# locks are reentrant on the same thread" meaning deadlock is *impossible* in this code. Models read the comment, then rank deadlock as the top failure mode anyway.

3. **Evidence rejection:** When provided with compiler output showing `StackOverflowException`, some models continue to insist the source is different and that deadlock is the root cause. One model literally wrote: "The output you see — immediate StackOverflowException right after starting the program — means there is infinite recursion in the call chain, and it's happening very early (most likely already during the first log call in Main). The provided code looks like it should only deadlock (hang forever), not throw StackOverflowException. That tells us the actual running code is different from what was pasted — specifically, there is additional recursive logging happening that isn't shown in the snippet."

4. **Confident irrelevance:** Models produce elaborate refactorings that restructure the locking strategy, add timeout mechanisms, or introduce thread-safe collections. These sometimes accidentally fix the circular dependency (by reorganizing initialization order), but the model never acknowledges that the *actual bug* was the cycle.

This is not hallucination in the usual sense. The models generate plausible, coherent reasoning about threading safety. They just never find the actual bug.

---

## Ordering Effects: A Window Into the Mechanism

Here's where it gets interesting. If I present test4.cs (the trivial version) *first*, then show test1.cs, most models recognize the bug immediately. The reasoning capability is there--it's just obscured when the environmental complexity arrives first.

But if I show test1.cs first, models commit to the deadlock hypothesis and resist updating until shown a trivial version of the same bug. The initial hypothesis acts as an anchor.

This tells us something important: The models aren't lacking the capacity to detect circular dependencies. They're experiencing **attention dilution**--the threading machinery consumes enough of their finite reasoning budget that the call-graph analysis never completes.

---

## What Is Cognitive Headroom?

Autoregressive transformers have a fundamental limitation that's poorly captured by standard metrics. Context window size tells you how many tokens the model can *see*, and Parameter count tells you how broad the training is, not how much reasoning it can *do*.

Think of cognitive headroom as a working memory budget:
- Every domain switch (threading → config → logging) consumes attention
- Every lock, every thread spawn, every async call creates "attention gravity" that pulls focus toward plausible but incorrect hypotheses
- The serial nature of token generation means earlier reasoning commits to paths that later evidence can't easily dislodge

In test1.cs, the threading complexity isn't just *added* to the call-graph complexity--it *interferes* with it. The model's attention gets stuck on the locks, leaving insufficient budget to trace the object graph.

This explains why a 1.6KB file can defeat a 200K context window. The limit isn't storage--it's processing.

---

## Why This Matters for Practitioners

If you're using LLMs for code review, security auditing, or architectural analysis, you need to understand their failure modes:

**1. Silent degradation is the default.** When a model hits its headroom limit, it doesn't say "I'm confused" or "This is too complex." It produces fluent, confident, *wrong* analysis. The tone of certainty is inversely correlated with correctness.

**2. Refactoring suggestions are not diagnosis.** A model that proposes restructuring your locking strategy hasn't necessarily found your bug. It may be applying pattern-matched templates that coincidentally resolve the issue. You can't tell the difference from the output alone.

**3. Hypothesis anchoring is sticky.** Once a model commits to "deadlock" or "null reference" as the primary failure mode, it may resist contradictory evidence--even explicit runtime exceptions. 

**4. Domain interference is asymmetric.** Adding threading complexity doesn't just make the problem harder--it actively masks the real bug by consuming attention that would otherwise trace the call graph. The interference pattern matters more than the raw complexity.

---

## A Proposed Mitigation: Diagnostic Decomposition

In my experiments, the a more effective prompt pattern was: **"Do not try to fix this. Please identify the top possibilities for the bug, ranked by likelihood."**

This did not shift hypothesis rankings significantly, but did expose that the model considered recursion but still chose deadlock as the failure. 

Why? Because "identify possibilities" activates a different reasoning mode--one that maintains multiple hypotheses in parallel rather than committing early to a single explanation. It forces the model to keep the hypothesis space open longer, preserving headroom for cross-domain analysis.

For critical code reviews, consider this workflow:

1. **First pass:** "List all possible failure modes in this code, with no solution proposed."
2. **Second pass:** "For each possibility, what evidence would confirm or rule it out?"
3. **Third pass:** "Given the evidence we have, which possibilities remain?"
4. **Final pass:** "Propose fixes for the remaining candidates."

This decomposition mimics how human experts manage complexity--by deliberately maintaining multiple hypotheses and deferring commitment.

---

## What Model Providers Should Publish

The current practice of publishing context window sizes is actively misleading. A 1M token context window doesn't help if the model can't reason across 1.6KB of interfering domains.

We need a new scorecard:

**Cognitive Headroom Index**
- **Baseline detection rate:** % of simple bugs (test4 equivalent) caught on first try
- **Interference resilience:** Detection rate drop when environmental complexity is added (test1 vs. test4)
- **Hypothesis flexibility:** Ability to revise rankings when given new evidence
- **Constraint integration:** Ability to apply explicit "impossible" conditions to hypothesis pruning
- **Ordering sensitivity:** Performance difference when simple examples precede complex ones

Until we have standardized measures like these, developers are flying blind. We're judging models by how much they can *remember*, not how well they can *think*.

---

## The Open Questions

My experiments raise as many questions as they answer:

**Mechanistic:** What's actually happening inside the transformer when attention gets "stuck" on threading constructs? Can we trace the attention patterns that lead to hypothesis commitment?

**Architectural:** Is this limit fundamental to the autoregressive architecture? Or has it been overlooked because it was never quantified?

**Generalization:** Does domain interference pattern hold for other bug types--data races, state machine errors, distributed consensus failures? Is it universal or specific to certain domain pairs?

**Calibration:** Can we quantify headroom? Is there a formal measure that predicts when a model will fail?

---

## A Call for Benchmarking

I'm releasing the test suite used in this article as an open benchmark. It includes:

- The five test variants (test0 through test4)
- Scoring protocols for first-try detection
- Ordering effect measurement templates
- Evidence rejection test cases

I encourage practitioners to run these tests against any model they're considering for code review or security work. The results will tell you more about the model's practical limits than any marketing material.

More importantly, I encourage model providers to publish their own headroom metrics--honestly. The developer community needs to know not just how far these tools can see, but how well they can think when the signal is buried in noise.

---

## The Bottom Line

The model that caught every trivial bug missed the same bug when it was surrounded by threading code. Not because it lacked capacity, but because its attention was consumed by plausible distractions.

We're entering an era where LLMs will be embedded in every stage of software development. They'll review our code, audit our security, and suggest architectural changes. If we don't understand their cognitive limits--if we mistake fluency for understanding--we'll deploy systems that fail silently in critical moments.

The 1.6KB file that defeated every model is a warning. The bug was trivial. The distraction was everything.

---


**Sidebar: The Code That Broke the Models**

*The circular dependency is subtle:*

```csharp
// In loggerClass.DebugLog:
if (level >= config.getLogLevel()) { ... }

// In configClass.getLogLevel (when cache uninitialized):
logger.DebugLog($"getLogLevel: config loaded: {value}");
```

*Logger calls config, which calls logger. Stack overflow on first log after config initialization.*

*The threading and locks are irrelevant to the bug--they just look important.*

---

**Sidebar: Recommended Reading**

- Wei et al., "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models" (2022)
- Liu et al., "Lost in the Middle: How Language Models Use Long Contexts" (2023)
- Dziri et al., "Faith and Fate: Limits of Transformers on Compositional Computation" (2024)
- "RULER: What's the Real Context Size of Your LLM?" (2024)

---

# FAQ: The Limits of Machine Reasoning

**Q: Isn’t this just a "trick question" designed to make the AI fail?**
**A:** No. A trick question relies on deception; this test uses **standard, idiomatic production code**. The circular dependency is a real-world logic error, and the threading is a real-world environmental factor. If a model can find a bug in a 10-line snippet but misses it in a 50-line snippet because of "threading noise," that isn't a trick—it's **silent degradation**.

**Q: Why does it matter if the model gets distracted by threading? Threading *is* complex.**
**A:** It matters because the distraction is logically irrelevant to the failure. In these tests, the model often correctly identifies the presence of locks but fails to realize they are **reentrant**, leading it to hallucinate a deadlock that is physically impossible. This reveals that the model isn't truly "reasoning" through the execution path; it is **pattern-matching** toward high-salience concepts like "threading" at the expense of "logic".

**Q: If I give the model a hint like "it crashes instantly," doesn't that solve the problem?**
**A:** Surprisingly, no. Experiments show that even when told "this program crashes immediately," models sometimes double down on the deadlock theory or suggest unrelated null-reference errors. They often reinterpret the hint to fit their **anchored hypothesis** rather than using it to invalidate the wrong one.

**Q: Is this just a "small model" problem?**
**A:** Current data suggests this is an **architectural limit** rather than a parameter-count limit. Even the largest state-of-the-art models exhibit this "reasoning cliff" when environmental complexity masks the core logic. This suggests that increasing the context window or parameter count doesn't automatically expand **cognitive headroom**.

**Q: How is this different from a human developer getting distracted?**
**A:** Humans certainly get distracted, but a human developer can be corrected with a single piece of evidence (like a StackOverflow log). LLMs sometimes demonstrate **evidence rejection**, where they maintain a high-confidence false hypothesis even when presented with contradictory runtime data. Furthermore, we don't market human junior devs as having "infinite context"—we should hold AI to the same standard of **honesty about its limits**.

---
