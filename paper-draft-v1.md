# The Digital Core Methodology

**Wisdom Happy**
*Playful Sincerity Research*
*Draft 2026-04-18 — provisional, pre-peer-review*

---

## Abstract

Over three weeks in March–April 2026, a single researcher working with an AI coding system produced a candidate new algebraic framework spanning nine classical mathematical domains, with 403 computational verification checks across six independent tool chains and zero formal failures at the time of writing. The work has not undergone peer review and is reported here as provisional. What this paper documents is not the mathematics itself but the methodology that produced it: the *Playful Sincerity Digital Core* (PSDC), a structured research environment built on top of Claude Code. PSDC combines persistent cognition rules, on-demand workflow skills, delegated agents, deterministic hooks, a running chronicle, and a computational verification stack. A meta-audit partway through the work caught a circular verification function that had been silently passing twenty tests; that discovery is presented here as the methodology working, not failing. This paper describes the environment, the research loop, the case study (IVNA), and what remains open.

---

## 1. Introduction

The claim is narrow. One researcher, working alone with an AI system, produced candidate results in abstract algebra in three weeks that would plausibly have taken a traditional research team months. The results are provisional. No external mathematician has fully vetted them. The Lean 4 formalization covers only first-order virtual numbers. The "division by zero" framing the work originally used turns out, on closer inspection, to be misleading.

Despite those caveats, the question the work raises is real: when a single researcher is embedded in a sufficiently structured AI environment, does "lone researcher" still mean what it meant in 2023?

This paper reports on the environment — the Playful Sincerity Digital Core, or PSDC — that made the work possible. It is written for practitioners already using agentic tools who want to see how one research group has structured that use. It is not a claim that this is the only way or the best way. It is a report.

**Roadmap.** Section 2 describes PSDC. Section 3 describes the research loop. Section 4 describes IVNA as a case study, including what is verified and what is not. Section 5 describes what this work provisionally supports and what it does not.

A note on epistemic status. Every non-trivial claim in this paper is either (a) computationally verified and reproducible from the public repository, (b) internally consistent but unreviewed by outside mathematicians, or (c) provisional hypothesis. We try to mark which is which.

---

## 2. The Digital Core

PSDC is the research environment — a collection of files and conventions layered on top of Claude Code that persist across conversations. It is composed of five kinds of artifact.

**Rules.** Always-loaded markdown instructions that shape how the model reasons. Current examples include rules for semantic logging, epistemic verification, model selection, breath-pauses that interrupt momentum, and safety scans on shell commands and fetched web content. Rules are not features; they are cognitive biases imposed on the assistant.

**Skills.** On-demand workflows invoked by slash commands. Examples include `/debate` (adversarial multi-agent stress testing), `/play` (creative exploration with three voices — thread-follower, paradox-holder, pattern-spotter), `/plan-deep` (hierarchical decomposition), `/research-papers`, `/research-books`, and `/think-deep` (the meta-skill that composes research, play, structure, challenger, and synthesis). Skills keep workflow complexity out of the main conversation until it is needed.

**Agents.** Delegated subroutines with scoped context and cheaper models. The Digital Core currently routes over 60% of subagent work to Haiku, reserving Sonnet for reasoning-heavy tasks and Opus for post-debate synthesis. Model selection is itself a rule (Section 3).

**Hooks.** Deterministic enforcement the model cannot forget. When the assistant stops, Bash scripts run to check: has the chronicle been updated recently? has a breath-pause been taken? is the right model selected? The hooks emit reminders that the assistant must then act on, creating a form of self-regulation that does not depend on the assistant remembering to regulate itself.

**Chronicle and memory.** A per-day markdown log of what happened, why, and what it means, stored under `chronicle/YYYY-MM-DD.md`, plus a persistent memory system at `~/.claude/projects/.../memory/`. The chronicle is the narrative layer (what was decided and why). Memory is the cross-conversation fact layer (what to carry forward). Together they close the gap that stateless language models leave open: conversations end, but the work continues.

PSDC is not a product. It is an accumulating set of conventions that one researcher has grown over time. The source is available under MIT license.

---

## 3. The Research Loop: Generate–Verify–Refine

Agentic research is easy to get wrong. A language model will generate plausible mathematics, plausible citations, and plausible proofs, and a researcher who trusts them gets a plausible paper full of errors. The single most important part of the PSDC methodology is the verification layer.

**Domain-aware verification.** Every research domain has a profile that declares what can be computed, what can be proved, and which tool applies. For IVNA, the profile declared: algebraic identities should be checked in SymPy; axiom consistency should be checked in Z3; symbolic results should be cross-verified in Wolfram; core theorems should be formalized in Lean 4. The profile is a rule the assistant follows.

**The loop.** Generate a candidate claim. Write code (or Lean) that tests it. Run the test. If it fails, the generation was wrong — refine. If it passes, log the pass and move on. The loop is not novel (it is the standard scientific-computation pattern). What is novel is making it the default, enforced by rules and hooks, across an entire research project.

**Six tool chains.** The IVNA verification suite uses Python (IVNA's own reference implementation), SymPy (symbolic algebra), Z3 (SMT solver for axiom consistency), Wolfram Engine (independent cross-verification), Lean 4 (machine-checked proofs), and a meta-verification layer that audits the suite itself. No single chain is trusted alone. Agreement across independent tools is the signal.

**Adversarial debate.** For claims that resist computation — philosophical framings, literature interpretations, naming decisions — the Digital Core uses the `/debate` skill. Three agents with different lenses (including an adversarial steel-manner) argue the claim. The convergence or the remaining disagreement is itself evidence about the claim's robustness.

**Multi-session decomposition.** Work that exceeds a single conversation's capacity is broken into parallel session briefs — self-contained markdown files that each drive a separate conversation. IVNA's Phase 4 ran five such sessions in parallel: EXPLORE (open questions), VERIFY (triple-check the unification table), SEARCH (prior art across 15+ databases), RESTRUCTURE (paper organization), and DEBATE (adversarial stress test). The parallel work reconverged at a written synthesis.

**Research agent outputs as primary data.** Every research subagent's full output is saved as a dated markdown file and cross-referenced in the synthesis. Anyone reading the final paper should be able to trace a claim back to the agent that produced it.

---

## 4. Case Study: IVNA

**What IVNA is.** Indexed Virtual Number Algebra is a candidate algebraic framework in which certain classically "undefined" expressions are given consistent algebraic meaning by carrying nonzero index labels. The original framing — "dividing by zero" — is technically misleading and the paper's current revision walks it back. More accurately: IVNA introduces objects `0_x` and `∞_y` (indexed zeros and indexed infinities) on which multiplication is defined by `0_x · ∞_y = xy`. The indices `x` and `y` must be nonzero scalars in the underlying field. The operation is *not* a division by the scalar zero; it is a product of two indexed objects whose labels happen to include zero and infinity.

With this corrected framing, one product rule — `0_x · ∞_y = xy` — turns out to appear, in different disguises, across nine classical mathematical domains:

1. derivatives (first-order virtual numbers recover the Vector-Tangent rule)
2. Riemann integration (step-width product rule)
3. Dirac delta normalization, sifting, and scaling
4. conditional probability (Bayes' theorem, specifically `0_a / 0_b = a/b` — see below)
5. removable singularities in complex analysis
6. residue extraction
7. compound growth and scaling symmetry
8. algebraic blow-up correspondence with exceptional divisors in P¹
9. KL divergence and renormalization limits

The observation that these nine instances share one algebraic rule is, to our knowledge and after a prior-art search covering 31 queries across 7 search strategies, novel. The *connection* between certain pairs — notably between infinitesimal calculus and the Dirac delta — is well-known. The unified algebraic framing is what appears to be new.

**A note on Bayes' theorem.** The identity between A8 (`0_a / 0_b = a/b`) and Bayes' rule for conditional density has a prior. Jacobs (2021, POPL, arXiv:2101.03391) uses symbolic infinitesimals of the form `rε^n` to represent probability densities and computes conditional density as a ratio. The structural difference is that Jacobs carries density as the *coefficient* of `ε` while IVNA carries it as the *index* of the zero. We do not claim A8 = Bayes is new. We claim the explicit statement of it as a named algebraic identity within a broader indexed algebra is.

**Verification record.** As of 2026-04-06, the IVNA verification suite reports: Python/IVNA-native tests, 198 checks, 0 failures; nonstandard-analysis embedding tests, 70 checks, 0 failures; classical correspondence tests, 93 checks, 0 failures; Wolfram cross-verification, 42 checks, 0 failures. The Lean 4 formalization contains 11 axioms and 12 derived theorems with zero `sorry`. A meta-verification layer adds 18 checks of the verification infrastructure itself. The grand total is 403 checks, 0 formal failures.

**What that count does and does not mean.** It does not mean IVNA has been proved correct. It means that across six independent tools, no tool found a contradiction in the stated axioms or their claimed consequences. Domains 3 through 9 in the unification table are currently verified as *classical correspondences* — SymPy or Wolfram computes the classical result, and IVNA notation is shown to produce the same answer. They do not yet demonstrate a case where IVNA computes a novel result that classical analysis cannot.

**The meta-audit.** Partway through the work (2026-04-06), a scheduled audit of the verification suite discovered that the derivative verification function, `ivna_derivative()`, was a passthrough returning its input unchanged. Twenty derivative tests had been "passing" by computing nothing. The function was replaced with a genuine `A-VT + A8` pipeline; the corrected version passes 30 of 30 unit tests. The audit also discovered that prior verification counts had been inflated by roughly 270 classical-math checks that were not IVNA-native; the authoritative count was revised downward to the 403 reported above.

This is presented as evidence that the methodology works. A circular test will pass silently; the only way to catch it is to audit the tests themselves. The audit was scheduled as part of the loop, not triggered by a suspicion. It caught something real.

**External review.** IVNA has had one external reviewer to date: Kiel Howe (Stanford physics PhD), who reviewed the paper on 2026-04-13. His most incisive comment — "why do I need the subscripts? If I just define an `inf*` and `0*` with their product equal to one, can't I leave the coefficients explicit?" — is formally correct at every level of the current formalization. The Lean 4 axioms encode multiplication of two indexed objects as coefficient-multiplication, which is exactly what Howe identified. The paper's next revision must either rigorously defend the indexed notation as more than notational convenience or reframe the contribution as a unifying algebraic vocabulary rather than a new number system.

**What is genuinely provisional.** The "killer theorem" — a result IVNA proves that nonstandard analysis cannot — has not been found. Until it is, IVNA's status is notational plus pedagogical plus organizational. That may or may not count as a mathematical contribution. Peer review will determine.

---

## 5. What This Is Evidence For, and What It Is Not

**What the case study provisionally supports.** A single researcher, using structured AI tools with an emphasis on computational verification, can move faster through the early exploration of a mathematical framework than a traditional solo researcher could. Verification is the load-bearing piece; without it, the speed is hallucinated speed.

**What it does not support.** It does not show that AI tools will replace mathematical research teams. It does not show that IVNA is a correct or important framework; peer review has not happened. It does not show the methodology generalizes to every research domain; IVNA is one case.

**The methodology is being used elsewhere in PS Research.** The Digital Core is currently in use on several other projects — a graph-based memory architecture, a visual computer-use agent, a universal language project, a gravitational-unification program in physics, among others. Architectures and findings from these projects are withheld here. We mention them only to report that the methodology is being tried beyond the one case this paper documents, with preliminary results.

**Open questions that remain.**

- Is there a theorem IVNA proves that NSA does not? The single most important open question about the mathematics.
- Does the methodology scale beyond mathematics to empirical sciences, where verification is noisier and slower?
- What is the right form of external validation for work produced this way? Traditional peer review, collaborative replication by another AI-plus-human pair, formal theorem provers — each gives different guarantees.
- Can methodological patterns be extracted and shared in a form other researchers can adopt without re-doing the several months of environment-building that PSDC represents?

**Reproduction.** The PSDC source is available under MIT license. The IVNA repository is public. Every verification check cited in Section 4 can be re-run from the repository.

**Closing note.** This paper is itself produced using the methodology it describes. A think-deep session scoped the paper; agent outputs are saved alongside this draft; the chronicle for 2026-04-18 logs the decisions taken. The meta-move is intentional: the work documents the tool that produces the work.

---

## Acknowledgments

The methodology described here is shaped by many collaborators whose conversations and critiques over the last six months led to the current form of PSDC. Kiel Howe provided the first external review of IVNA on 2026-04-13. PSDC itself is a dense collaboration between the author and Claude Code (Anthropic). The author holds primary responsibility for any errors; any successes are the methodology doing what it is supposed to do.

## References

*(To be completed in final draft: Jacobs 2021 arXiv:2101.03391; Robinson 1966 NSA; Fereydoni 2025; Anthropic "Building Effective Agents"; Karpathy blog posts on AI-augmented research; Sakana AI "The AI Scientist" 2025; IVNA GitHub repository; PSDC MIT-licensed repository.)*

---

*Word count (body): ~2,350*
