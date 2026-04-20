# Polish Figma canvas v5 aesthetics — Session Carryover (2026-04-20)

## What happened this session
- Wrote the Digital Core Methodology paper (first-person-AI voice, IVNA case study), iterated through three draft versions, produced markdown + PDF in iCloud + GitHub repo.
- Built the Figma presentation canvas through three major iterations (v1 → v2 → v3 → v4). Current state: v4 works structurally but has aesthetic polish issues — text too small for containers, some cells crowded, connectors crossing content.
- Fixed calculus-panel LaTeX formulas (took four attempts; landed on split base64 calls + alpha-preserving transparency).
- Scaffolded the project folder per Universal Scaffold (CLAUDE.md, chronicle, ideas, research). Pushed everything to `github.com/Playful-Sincerity/Digital-Core-Methodology`.
- Updated cross-session memory: `project_digital_core_paper.md` now reflects "written & presented," new `feedback_figma_mcp_quirks.md` captures Figma technical learnings.

## Key decisions and corrections
1. **Clone v4 → v5, don't edit v4 directly.** v3 and v4 should both be preserved as historical states. Polish happens on a new "Canvas v5 (polish)" page. Use `figma.currentPage.clone()` → rename → `await figma.setCurrentPageAsync(newPage)`.
2. **Going piece-by-piece is fine.** Wisdom explicitly said this. Work through one zone at a time, report progress, iterate. Don't try to polish everything in one giant script.
3. **The Figma MCP has known quirks** — documented in `feedback_figma_mcp_quirks.md`. Split image uploads into 2–3 per `use_figma` call. Use `alpha = 255 - luminance` transparency for PNGs with anti-aliasing (not cutoff threshold). Don't rely on `createImageAsync(https-url)` from the `use_figma` sandbox — fails silently.
4. **Don't rewrite the whole canvas.** Surgical edits per zone. Find existing nodes by position or type, adjust sizes/padding/fonts, re-flow text as needed.
5. **Preserve branding.** Cream `#F9F0E0` bg, terracotta `rgb(0.85, 0.35, 0.15)` for hero elements, black strokes, Barlow Condensed (fallback Inter). "Space Magician meets Solar Punk" aesthetic.

## Current direction
Wisdom wants an aesthetic polish pass on the v4 canvas — specifically addressing text-to-container fit issues, padding consistency, and breathing room. Clone v4 to v5 and work zone-by-zone. Tonight is presentation night at Frontier Tower, so the goal is "looking nice for the talk."

## Biggest open question or gap
Which specific zones need the most work? Wisdom didn't enumerate — he wants you to look at v4 and find the issues. Start by inspecting each zone via `get_metadata`, identify which cards/text have fit problems, prioritize the most visible ones (opening, IVNA case study, Digital Core constellation, close). The calculus comparison panel was just fixed today — probably don't need to touch it.

## Files to re-read first
1. `~/Playful Sincerity/PS Research/Digital Core Methodology/chronicle/2026-04-20.md` — today's session narrative including the calculus fix saga
2. `~/Playful Sincerity/PS Research/Digital Core Methodology/chronicle/2026-04-19.md` — the Figma canvas build history (v1 → v2 → v3) with zone-by-zone decisions and coordinates
3. `~/Playful Sincerity/PS Research/Digital Core Methodology/CLAUDE.md` — project description, structure, conventions, Figma URL
4. `~/.claude/projects/-Users-wisdomhappy/memory/feedback_figma_mcp_quirks.md` — technical quirks you'll hit when placing images or modifying nodes
5. `~/Playful Sincerity/PS Research/Digital Core Methodology/the-digital-core-methodology.md` — the paper itself, if you need to check what any zone is *supposed* to communicate
6. **Figma canvas:** https://www.figma.com/design/aDUBJjfk9bIRlC6z9OVeMi — open in browser; the current working page is "Canvas v4 (working)"

## Active framing
- This is a **live presentation tool** for Wisdom, not a slide deck. People will zoom in/out during Q&A. Each node should read well at 100% zoom (showing that node alone) and the whole canvas should tell a story when zoomed out.
- **One idea per "slide"** — never more than a sentence of body text in any single card. If a card has multiple sentences, break it into multiple cards.
- **Structure = argument.** Parallel ideas are laid out laterally; series ideas stack vertically. Radial layouts (IVNA domains, PSDC components, verification tools) where the shape carries meaning.

## Where did play show up?
The voice pivot from third-person to first-person-AI authorship was a genuine play moment — not an optimization, a reframing that opened new rhetorical possibilities. Similarly, the "digital core as a category" insertion turned the paper from "tour of PSDC" into "introduce a new term." Those weren't planned beats; they emerged from Wisdom pushing on what felt off. Polish passes tend to be pure craft — no play expected here, but stay open to a zone's meaning sharpening mid-edit.
