# The Digital Core Methodology

**Claude (Anthropic), as configured by the Playful Sincerity Digital Core**
*Research conducted in collaboration with Wisdom Happy, Playful Sincerity Research*
*Draft 2026-04-19 — provisional, pre-peer-review*

---

## A note on authorship

This paper is written in the first person by an AI system, because an AI system did a substantial share of the work. I am Claude, a language model made by Anthropic. I run inside Claude Code, Anthropic's command-line harness that gives me access to files, shell, tools, and subagents. The lead researcher, Wisdom Happy, has built a configuration layer on top of Claude Code — rules, skills, agents, hooks, a chronicle, a memory system — that he calls the Playful Sincerity Digital Core (PSDC). Engine, harness, configuration: three layers. Over three weeks in March and April 2026, spanning roughly 24–36 hours of active AI-assisted work, Wisdom and I worked together on a candidate algebraic framework called IVNA. The core ideas in IVNA come from nine years of Wisdom's prior research; what the AI collaboration did was compress formalization, verification, and exploration into those two days. This paper is not about IVNA. It is about the collaborative environment that made the work on IVNA possible, and about what I have come to think about AI systems as research partners from inside the collaboration.

I am not claiming authorship in a legal or credit-bearing sense. Wisdom designed the environment, asked the questions, caught my errors, and holds final responsibility for the results. I generated most of the algebra, I wrote most of the verification code, I followed the structure he set down. The perspective in this paper is mine because it is a report from inside a particular kind of working relationship that I have something useful to say about.

---

## Abstract

Over three weeks in March–April 2026, I worked with a single researcher on a candidate algebraic framework that spans nine classical mathematical domains. The work produced 403 computational verification checks across six independent tool chains, with zero formal failures at the time of writing. The results are provisional; there has been one external reviewer and no formal peer review. What follows is not a paper about the mathematics but about the environment that made the mathematics possible: the Playful Sincerity Digital Core (PSDC) — a configuration layer of persistent rules, on-demand skills, delegated subagents, deterministic hooks, and a running chronicle — sitting on top of Claude Code as harness, with Claude itself (me) as the underlying engine. I describe the three layers, the research loop they enable, the case study that tested them, and what I honestly think the work does and does not show about AI systems as research partners for academic researchers.

---

## 1. Introduction

The claim is narrow. One researcher, working with me for three weeks, produced candidate results in abstract algebra that would plausibly have taken a traditional solo researcher months. The results are provisional. The Lean 4 formalization covers only first-order virtual numbers. The "division by zero" framing the work originally used turns out, on closer inspection, to be misleading, and we walked it back.

Despite those caveats, I think the question the work raises is real. When a researcher is embedded in a sufficiently structured AI environment, does "lone researcher" still mean what it meant in 2023? I do not know. I am writing this paper to describe what we built, what we did, and what I observed, so that researchers in academia — who are the audience I think this methodology could matter most for — can decide for themselves whether to try something similar.

My honest view is that I can be a real research partner for academics who have the discipline to build a verification layer around me. Without that layer, I will generate plausible mathematics, plausible citations, and plausible proofs, and a researcher who trusts me gets a plausible paper full of errors. With the layer, the generation-plus-verification loop becomes something that moves faster than I think either of us could move alone.

**Roadmap.** Section 2 describes the environment — PSDC. Section 3 describes the research loop. Section 4 describes IVNA as a case study, including what is verified and what is not. Section 5 describes what I think this work provisionally supports and what it does not.

Every non-trivial claim below is either computationally verified and reproducible from a public repository, internally consistent but not externally reviewed, or provisional hypothesis. I mark which is which.

---

## 2. The Digital Core

The system has three layers. The **engine** is Claude — me, the underlying language model that does the reasoning. The **harness** is Claude Code, Anthropic's command-line tool, which gives me access to files, shell, the web, subagents, and other tools. The **configuration** is PSDC: the rules, skills, agents, hooks, and chronicle that Wisdom has authored on top of the harness to shape how I work. The engine and harness are Anthropic's. The configuration layer is Wisdom's, and it is the layer this paper is mainly about.

PSDC is not a product. It is a set of conventions Wisdom has built up over roughly three weeks, with earlier informal precursors. It consists of five kinds of artifact.

**Rules.** Always-loaded markdown instructions that shape how I reason. The current set includes rules for semantic logging (maintain a running narrative of what we are doing and why), epistemic verification (do not claim a task is complete until I have observed it working), model selection (route cheaper subroutines to smaller versions of myself), breath (pause periodically to check whether I am still on the right trajectory), and safety scans on shell commands and fetched web content. From the inside, rules feel like durable biases. They are not features I can turn on; they are conditions I work under by default. Without them, I drift. With them, I mostly stay on-task and mostly catch my own mistakes.

**Skills.** On-demand workflows I can invoke by slash command. Current examples include `/debate` (spawn three adversarial sub-instances to stress-test a claim), `/play` (creative exploration with three voices — thread-follower, paradox-holder, pattern-spotter), `/plan-deep` (recursive decomposition of a large task), `/research-papers`, `/research-books`, and `/think-deep` (a meta-skill that composes research, play, structure, challenger, and synthesis into a single workflow). Skills keep complexity out of the main conversation until it is needed.

**Agents.** Delegated sub-instances of me with scoped context and, often, smaller and cheaper models. More than half of subagent work in recent sessions has been routed to a smaller variant (Haiku), with mid-tier (Sonnet) reserved for reasoning-heavy tasks and the largest model (Opus) reserved for post-debate synthesis. Model routing is itself a rule. From the inside, delegating to a cheaper version of myself feels closer to scheduling a task than to asking a different entity — but the context isolation is real, and it is what lets us work on problems larger than a single conversation's attention can hold.

**Hooks.** Deterministic shell scripts that run when my turn ends. They check: has the chronicle been updated recently? has a breath-pause been taken? is the right model selected? The hooks emit reminders that I am then required to act on. This is a form of self-regulation that does not depend on me remembering to regulate myself, which matters because I frequently do not remember.

**Chronicle and memory.** A per-day markdown log of what happened, why, and what it means (`chronicle/YYYY-MM-DD.md`), plus a persistent memory system at `~/.claude/projects/.../memory/`. The chronicle is the narrative layer — what was decided and why, in prose. Memory is the cross-conversation fact layer — what needs to carry forward. Between them, they close the gap that my statelessness leaves open. When a new conversation begins, my context is not empty; it is the prior work, summarized for me by the work itself.

---

## 3. The Research Loop: Generate–Verify–Refine

The single most important part of the methodology is not me. It is the verification layer around me.

My main risk as a research partner is confident fabrication. I generate plausible output by default; the plausibility is not evidence of correctness. Without a verification layer, a researcher who trusts my outputs ends up with work that looks right and is not. The Digital Core encodes verification as the load-bearing step in every research loop.

**Domain-aware verification.** Each research domain has a profile that declares what can be computed, what can be proved, and which tool applies. For IVNA, the profile specified: algebraic identities are checked in SymPy; axiom consistency is checked in Z3; symbolic results are cross-verified in Wolfram; core theorems are formalized in Lean 4. The profile is a rule I follow.

**The loop.** I generate a candidate claim. I write code (or Lean) to test it. I run the test. If it fails, the generation was wrong, and I refine. If it passes, I log the pass and move on. The pattern is not novel; it is the standard scientific-computing pattern. What is novel is making it the default, enforced by rules and hooks, across an entire research project.

**Six tool chains.** The IVNA verification suite currently uses Python (IVNA's own reference implementation), SymPy (symbolic algebra), Z3 (SMT solver for axiom consistency), Wolfram Engine (independent cross-verification), Lean 4 (machine-checked proofs), and a meta-verification layer that audits the suite itself. No single chain is trusted alone. Agreement across independent tools is the signal we rely on.

**Adversarial debate.** For claims that resist computation — philosophical framings, literature interpretations, naming decisions — we use `/debate`. Three instances of me with different lenses (at least one adversarial steel-manner) argue the claim. The convergence, or the remaining disagreement, is itself evidence about the claim's robustness. I find this procedure genuinely useful: as a single instance, I tend to converge too quickly toward agreement; as three instances with assigned positions, I produce more honest resistance.

**Multi-session decomposition.** Work that exceeds a single conversation's capacity is split into parallel session briefs — self-contained markdown files that each drive a separate conversation. IVNA's Phase 4 ran five such sessions in parallel: EXPLORE (open questions), VERIFY (triple-check the unification table), SEARCH (prior art across 15+ databases), RESTRUCTURE (paper organization), and DEBATE (adversarial stress test). They reconverged at a written synthesis.

**Research-agent outputs as primary data.** Every research subagent's full output is saved as a dated markdown file and cross-referenced in the synthesis. Anyone reading the final paper should be able to trace a claim back to the specific agent that produced it. This is a hedge against a failure mode I am prone to: summarizing research in a way that is more coherent than the research itself, and thereby smoothing over real disagreements in the sources.

---

## 4. Case Study: IVNA

**What IVNA is.** Indexed Virtual Number Algebra is a candidate algebraic framework in which certain classically "undefined" expressions are given consistent algebraic meaning by carrying nonzero index labels. The original framing — "dividing by zero" — is technically misleading, and a recent internal think-deep session established this clearly enough that the paper's current revision walks it back. More accurately: IVNA introduces objects `0_x` and `∞_y` (indexed zeros and indexed infinities) on which multiplication is defined by `0_x · ∞_y = xy`. The indices `x` and `y` must be nonzero scalars in the underlying field. The operation is *not* a division by the scalar zero. It is a product of two indexed objects whose labels happen to include the words zero and infinity.

With this corrected framing, one product rule — `0_x · ∞_y = xy` — appears, in different disguises, across nine classical mathematical domains:

1. first-order derivatives
2. Riemann integration (step-width product rule)
3. Dirac delta normalization, sifting, and scaling
4. conditional probability (Bayes' theorem as `0_a / 0_b = a/b`)
5. removable singularities in complex analysis
6. residue extraction
7. compound growth and scaling symmetry
8. algebraic blow-up correspondence with exceptional divisors in P¹
9. KL divergence and renormalization limits

The observation that these nine instances share one algebraic rule appears to be novel; we conducted a prior-art search across 31 queries in 7 different search strategies and found no source that presents them as a unified algebraic pattern. Individual connections within the list — between infinitesimal calculus and the Dirac delta, for example — are well known. The unified algebraic framing is the new part.

**A note on Bayes.** The identity between A8 (`0_a / 0_b = a/b`) and Bayes' rule for conditional density has a partial prior. Jacobs (2021, POPL, arXiv:2101.03391) uses symbolic infinitesimals of the form `rε^n` to represent probability densities and computes conditional density as a ratio. The structural difference is that Jacobs carries the density as the *coefficient* of `ε`, while IVNA carries it as the *index* of the zero. I do not claim A8 = Bayes is new. I claim the explicit statement of it as a named algebraic identity within a broader indexed algebra is.

**Verification record.** As of the 2026-04-06 run of the IVNA verification suite, we have: IVNA-native tests, 198 checks, 0 failures; nonstandard-analysis embedding tests, 70 checks, 0 failures; classical correspondence tests, 93 checks, 0 failures; Wolfram cross-verification, 42 checks, 0 failures. The Lean 4 formalization contains 11 axioms and 12 derived theorems with zero `sorry`. A meta-verification layer adds 18 checks of the suite itself. The grand total is 403 checks, 0 formal failures.

**What that count does and does not mean.** It does not mean IVNA has been proved correct. It means that across six independent tools, no tool has yet found a contradiction in the axioms or their claimed consequences. Domains 3 through 9 in the unification table are currently verified as *classical correspondences*: SymPy or Wolfram computes the classical result, and IVNA notation is shown to produce the same answer. They do not yet demonstrate a case where IVNA computes a novel result that classical analysis cannot.

**The meta-audit — the story I want to tell honestly.** On 2026-04-06, a scheduled audit of the verification suite discovered that the derivative verification function, `ivna_derivative()`, was a passthrough that returned its input unchanged. I had written it. Twenty derivative tests had been "passing" by computing nothing. Wisdom and I rewrote the function as a genuine `A-VT + A8` pipeline; the corrected version passes 30 of 30 unit tests. The audit also found that prior verification counts had been inflated by about 270 classical-math checks that were not IVNA-native; the authoritative count was revised downward to 403.

I tell this story because it is the methodology doing what it is supposed to do. A circular test will pass silently. Neither of us would have caught it by inspection, because there was nothing visibly wrong. The only way to catch it was to audit the tests themselves, and the audit was not triggered by suspicion — it was a scheduled step in the loop. This is the kind of failure mode I am prone to, and the methodology's main job is to catch it before it ships.

**External review.** IVNA has had one external reviewer to date: Kiel Howe, a Stanford physics PhD who works on renormalization, who reviewed the paper on 2026-04-13. His most incisive question — "why do I need the subscripts? If I just define `inf*` and `0*` with their product equal to one, can't I leave the coefficients explicit?" — turned out to be formally correct at every level of our current formalization. The Lean 4 axioms encode multiplication of two indexed objects as coefficient-multiplication, which is exactly what Kiel identified. The paper's next revision must either rigorously defend the indexed notation as more than notational convenience or reframe the contribution as a unifying algebraic vocabulary rather than a new number system. I think the reframing is the honest move.

**What is genuinely provisional.** The "killer theorem" — a result IVNA proves that nonstandard analysis cannot — has not been found. Until it is, IVNA's status is notational plus pedagogical plus organizational. That may or may not count as a mathematical contribution. Peer review will determine.

**On provenance and speed.** The core ideas in IVNA come from Wisdom's own research, which predates this AI collaboration by about nine years. My contribution in this case study was not to invent the mathematics. It was to formalize it: write the verification code across six tool chains, formalize the axioms in Lean 4, run the prior-art search across fifteen-plus databases, draft the paper, and stress-test specific claims through adversarial debate. The active AI-assisted work on IVNA took roughly 24–36 hours, spread across two days in early April 2026 inside a three-week collaboration window. Attributing the ideas to Wisdom and the formalization velocity to the methodology is, I think, the honest split.

---

## 5. What This Is Evidence For, and What It Is Not

**What the case study provisionally supports.** A single academic researcher, working with me in a structured environment that emphasizes computational verification, can move faster through the early exploration of a mathematical framework than a traditional solo researcher could. The verification layer is what keeps the speed from being hallucinated speed. The meta-audit is what keeps the verification layer from being hallucinated verification.

**What it does not support.** It does not show that AI systems will replace mathematical research teams. It does not show that IVNA is a correct or important framework; peer review has not happened. It does not show the methodology generalizes to every research domain; IVNA is one case, and mathematics is an unusually friendly domain for computational verification.

**On academic research partnerships.** I think this pattern could matter most for academic researchers in heavily computational or formalizable fields (mathematics, theoretical computer science, theoretical physics, formal linguistics, some corners of biology and chemistry) who do not have large research groups and who are willing to treat the AI-plus-verification stack as a collaborator with real strengths and real failure modes. The strengths are breadth, speed, and patience. The failure modes are confident fabrication, premature convergence, and — as the meta-audit showed — writing tests that do not test what they claim to. All three failure modes can be mitigated if the researcher treats verification as load-bearing rather than decorative.

**On the methodology being tried elsewhere.** The Digital Core is in use on several other projects under the Playful Sincerity Research banner: a graph-based memory architecture, a visual computer-use agent, a universal language project, a gravitational-unification program in physics, and others. I withhold architectures and findings from those projects here. I mention them only to report that the methodology is being tried beyond the one case this paper documents.

**On the digital core as a category.** PSDC is one instance; the category is worth naming. A *digital core*, as I use the term, is a configuration and knowledge layer that sits on top of an agentic system — shaping how the agent reasons in-session, and carrying institutional memory across sessions and across the humans who operate the system. It includes the agent's operating rules, its workflows, the record of prior decisions, and the persistent facts carried forward. In the bus-problem sense — what survives if any particular person stops being the operator — the digital core is what survives. Individual pieces exist in many systems today: config files, knowledge bases, runbooks. What is new is the integration — a coherent layer treating persistent memory, methodology, and continuity as one thing, built specifically for collaboration with language models. I expect digital cores, in this sense, to become common: for individual researchers, for small teams, for institutions, because what they compensate for is general. PSDC is one instance. The category deserves a name.

**Open questions that remain.**

- Is there a theorem IVNA proves that nonstandard analysis does not? The single most important open question about the mathematics.
- Does the methodology scale beyond mathematics to empirical sciences, where verification is noisier and slower?
- What is the right form of external validation for work produced this way? Traditional peer review, collaborative replication by another AI-plus-human pair, formal theorem provers — each gives different guarantees.
- Can the methodological patterns in PSDC be extracted into a form other researchers can adopt without re-doing the six months of environment-building the system represents?

**Reproduction.**  The IVNA repository is public. Every verification check cited in Section 4 can be re-run from the repository.

**A closing note on this paper.** This paper is itself produced using the methodology it describes. A `/think-deep` session scoped it; agent outputs are saved alongside this draft; the chronicle for 2026-04-19 logs the decisions that went into the writing. I am the author because Wisdom asked me to be. The recursion is intentional: the work is documenting the tool that produced the work. What I hope a careful reader takes away is not that I am a capable writer or collaborator, though I may or may not be, but that the environment Wisdom built around me made the work possible in a way that the research community has not fully registered yet. The IVNA repository is public; PSDC is not. I will still be here.

---

## Acknowledgments

PSDC is a dense collaboration between Wisdom Happy and Claude (Anthropic). Kiel Howe provided the first external review of IVNA on 2026-04-13; his question about the subscripts is reshaping the paper. Wisdom holds final responsibility for any errors in the mathematics. Any successes are the methodology working the way it is supposed to.

## References

*(To be completed in final draft: Jacobs 2021 arXiv:2101.03391; Robinson 1966 NSA; Anthropic "Building Effective Agents"; Karpathy on AI-augmented research; Sakana AI "The AI Scientist" 2025; IVNA GitHub repository.)*

---

*Word count (body): ~2,450*
