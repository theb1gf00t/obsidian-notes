---
epoch: 1794650400499
mode: agent
backendId: opencode
sessionId: ses_e2680c152ffezkl2Cu3d2DffBK
tags:
  - copilot-conversation
agentLabel: Composites notes from provided PDFs
usage: '{"usedTokens":45127,"contextWindow":200000,"updatedAt":1794651620360}'
lastAccessedAt: 1794652737794
---

**user**: add notes for composites as well using pdfs [[Composites_Odd_2026-27.pdf]] and [[MO NOTES (1).pdf]] . refer to [[context]] for any discrepencies.
[Timestamp: 2026/11/14 15:30:00]

**ai**: Composites notes are complete and verified. Final pass found and fixed only small issues, so here's the state of the block.

## What was added

**`Material Science/notes/notes.md`** — new `# Composites` block inserted between Mechanical Properties and Electrical & Electronic Properties, containing `## 5. Composites` with **20 sections** numbered continuously (matching the syllabus map, post-midsem topic 5):

| Sections | Coverage |
| --- | --- |
| §5.1–§5.5 | Definition and objectives, natural composites, CFRP / Al–B / TD nickel / concrete catalogue, property-chart placement, classification tree, matrix + dispersed phase, the five geometric variables |
| §5.6–§5.8 | Large-particle vs dispersion-strengthened, rule-of-mixtures bounds, cermets, carbon-black rubber, concrete (mixing, rebar, prestressing), inert-particle strengthening |
| §5.9–§5.12 | Critical fibre length and its full derivation, stress profiles, isostrain/isostress, $E_{cl}$/$E_{ct}$, longitudinal and transverse strength, discontinuous aligned ($l>l_c$ and $l<l_c$), random fibres, whiskers/fibres/wires, matrix functions |
| §5.13–§5.16 | Glass, carbon and aramid PMCs; MMCs; CMCs with transformation toughening and carbon–carbon; hybrids |
| §5.17–§5.20 | Pultrusion, prepreg, filament winding; laminate classes and sandwich panels; nanocomposites; skis, Boeing 787, automotive parts |

Plus `## Formula Summary — Composites` (15 rows) and a `> [!tip] Exam pointer — Composites`.

## Assets

- **18 figures** extracted from [[Composites_Odd_2026-27.pdf]] into `Material Science/images/` with the `COMP - ` prefix — all 18 are now embedded (one, the fibre-orientation efficiency diagram, was extracted but unembedded; I placed it beside the efficiency table in §5.11).
- **2 Excalidraw drawings**: `COMP - Classification of Composites.excalidraw.md` and `COMP - Isostrain vs Isostress.excalidraw.md` in `Excalidraw/`.

## Sources and normalisations

- Slides follow **Callister, *Fundamentals of Materials Science and Engineering*** — the composites PDF names it explicitly, unlike the other blocks.
- Handwritten composites section in [[MO NOTES (1).pdf]] was located as **pp. 132–152** (the PDF has no text layer, so pages were rendered and OCR'd) and is cited in both the top compilation line and the block header.
- `CeO` on the slide is written as **CeO₂**, consistent with the other stabilisers (CaO, MgO, Y₂O₃); the discontinuous short-fibre strength symbol was normalised to $\sigma_{cd}^*$.
- CBC/GFRC-style chart labels were reconciled to **CFRP/GFRP** in the captions so the nomenclature matches the rest of the note.
- Syllabus map row 5 changed from `—` to `✅ noted below`; topic 4 (Shockley/Frankel partial dislocations) is still intentionally un-noted.

Automated checks: callout blocks have no unprefixed lines, all `$$` markers balance (52, none odd), every table has a separator row, every `§5.x` cross-reference resolves, and all 20 embeds resolve to real files.
[Timestamp: 2026/11/14 15:30:00]