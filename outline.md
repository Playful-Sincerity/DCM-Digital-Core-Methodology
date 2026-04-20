# The Digital Core Methodology — Outline & Writing Plan

## Status
- **Target:** 5-page paper, ~2,500 words
- **Audience:** Frontier Tower AI Reading Club, Monday 2026-04-20
- **Format:** Markdown draft → convert to LaTeX or PDF via `pdf` command before presenting
- **Draft v1:** `paper-draft-v1.md` (complete, 2,350 words)

## Structure (final)

| § | Title | Words | Status |
|---|-------|-------|--------|
| — | Abstract | ~180 | done v1 |
| 1 | Introduction | ~260 | done v1 |
| 2 | The Digital Core | ~380 | done v1 |
| 3 | The Research Loop (GVR) | ~430 | done v1 |
| 4 | Case Study: IVNA | ~750 | done v1 |
| 5 | What This Is & Is Not Evidence For | ~400 | done v1 |
| — | Acknowledgments | ~90 | done v1 |
| — | References | — | needs filling |

## Voice decisions

- **Practitioner-accessible**, not dense mathematical journal style. Karpathy/Willison register.
- **Humble epistemic framing throughout.** Every non-trivial claim marked as verified / unreviewed / provisional.
- **The meta-audit is the headline methodology story** — circular derivative test caught and fixed. That paragraph is load-bearing.
- **Do NOT lead with "division by zero"** — the 2026-04-18 think-deep on "what is indexed zero" established this is misleading. The paper walks it back in Section 4.
- **Do NOT claim IVNA beats NSA.** Until the killer theorem exists, IVNA's status is notational + pedagogical + organizational.
- **Openly acknowledge** A8 = Bayes is partially anticipated by Jacobs 2021. The novelty claim is narrow.

## Facts anchored in IVNA repo (cross-check before final)

- Verification count: **403 checks, 0 failures** (as of 2026-04-06 suite run)
- Breakdown: 198 IVNA-native + 70 NSA-embedding + 93 classical-correspondence + 42 Wolfram + 18 meta-verification
- Lean 4: **11 axioms, 12 theorems, 0 `sorry`**
- Circular `ivna_derivative()` caught 2026-04-06; replaced with A-VT + A8 pipeline; 30/30 unit tests pass
- 9-domain unification table: confirmed NOVEL via prior art search (31 queries, 7 strategies)
- A8 = Bayes: PARTIALLY ANTICIPATED by Jacobs 2021 (POPL, arXiv:2101.03391)
- Kiel Howe reviewed 2026-04-13; his "why subscripts?" comment is formally correct at every level

## Open revision questions

1. **Do we keep the "Mean Girls / limit does exist" hook?** Currently dropped — paper opens straight into the technical claim. Could add as a footnote or talk-only joke. *Recommendation: drop from paper, keep for talk only.*
2. **Should Section 5 list the other PS Research projects by name?** Currently says "graph-based memory architecture, visual computer-use agent, universal language project, gravitational-unification program." No architectures revealed. *Recommendation: keep at current level of disclosure.*
3. **Should the paper include a figure?** A diagram of the PSDC architecture (rules/skills/agents/hooks/chronicle) would help Section 2 considerably. Spatial Workspace v1 could be shown in the talk even if not in the paper. *Recommendation: add one ASCII/SVG figure for the paper; plan Spatial Workspace demo for the talk.*
4. **Does the paper need a "reproducibility" box?** Could be a boxed section listing: (a) PSDC repo URL, (b) IVNA repo URL, (c) how to re-run the verification suite. *Recommendation: yes — add to Section 5.*

## Talk structure (60 min) — separate from paper

| Minute | Segment | Notes |
|-------:|---------|-------|
| 0–5 | Hook + setup | "The limit does exist now" joke, intro PSDC name |
| 5–15 | Digital Core walkthrough | Show actual files — rules/, skills/, hooks/. Live terminal if possible. |
| 15–25 | Research loop demo | Show a GVR cycle in live agent, or prerecorded screencast |
| 25–45 | IVNA case study | Product rule across 3 domains, then the meta-audit story |
| 45–55 | Spatial Workspace demo (if v1 ready) | Visual of the research |
| 55–60 | Q&A setup + open questions | Frame "this is provisional, push back" |

## Writing plan for next ~24h

1. **Tonight** — v1 complete. ✅
2. **Sunday morning** — Read v1 fresh. Tighten. Add one architecture figure. Verify every factual claim by grepping the IVNA repo.
3. **Sunday afternoon** — Fill references section. Cross-check with Jacobs 2021 paper.
4. **Sunday evening** — Send draft to Kiel for quick sanity check if possible. If not, run one more internal adversarial debate on Section 4.
5. **Monday morning** — Final polish. Build slide deck from paper sections. Test Spatial Workspace demo.
6. **Monday evening** — Present.

## Things explicitly NOT in this paper (IP protection)

- Associative Memory architecture details (research hasn't started; only thesis mentioned)
- ULP's 13-tier dimensional ladder or binary run-length encoding specifics
- Gravitationalism's derivation of forces from graviton density gradients
- Phantom's dual-perception / imagination-first architecture
- Companion's permission-as-consciousness meta-architecture
- Convergence Paper's 7 specific ideas
- Autonomous Venture Studio's 6 research streams

Each of these gets at most one noun-phrase mention in Section 5.
