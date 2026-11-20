---
epoch: 1795204900851
mode: agent
backendId: opencode
sessionId: "ses_e0573cd8bffeHDtk2pgjaALJZN"
tags:
  - copilot-conversation
agentLabel: "Computer Graphics formula sheet in cheat_sheet.md"
usage: '{"usedTokens":34173,"contextWindow":200000,"updatedAt":1795206828398}'
---

**user**: make a formula sheet/cheat sheet for all the pdfs in {Computer Graphics/pdfs} .
basically a formula revision sheet type thing.
make it in a separate file in {Computer Graphics/notes} named cheat_sheet.md
[Timestamp: 2026/11/21 01:31:40]

**ai**: I'll start by exploring the relevant folders and checking for any context conventions. Let me also load the PDF skill since I'll need to read PDFs.There's a `CG_context.md` — I should treat it as authoritative styling. Let me read it along with the syllabus and existing notes to understand conventions and avoid duplication.Let me check the existing notes' state and sizes, then extract text from all the PDFs.The post-midsem block already has a curated 34-row Formula Summary I can reuse. The pre-midsem notes are empty, so I need to mine those PDFs directly. Let me extract text from all pre-midsem decks plus the "Between" deck.This Pre 3 deck bundles multiple lectures. Let me search all pre-midsem text for formula-bearing terms to make sure I capture everything.Let me read the Phong illumination, B-splines, and digital images decks.Now the B-splines and digital images decks.Now the digital images deck and the transformation decks.Now the transformation decks — these are formula-heavy. Let me check their size and mine the formula sections.Now object representation and practice problems — let me mine their formula content.Let me check the tail of the object representation deck and mine the practice problems deck for formulas.Let me check the remaining transformation content and confirm the DDA/midpoint line details before writing.I now have everything I need. Let me write the cheat sheet, organized by syllabus topic across all decks, using the vault's formula-table and LaTeX conventions.Let me verify the written file for formatting correctness (table pipes, callout syntax, LaTeX environments).Done. Created [[cheat_sheet]] at `Computer Graphics/notes/cheat_sheet.md` (313 lines).

**What it covers** — every deck in `pdfs/`, in syllabus order:

- **Pre-midsem (§1–8):** perspective projection conventions, DDA + midpoint circle/line recurrence, implicit/parametric surfaces, Hermite/Cardinal/Catmull–Rom spline matrices and continuity, full 2D→3D transformation matrices (including arbitrary-axis rotation), the complete Phong model (vectors, three terms, attenuation, spotlight, Hadamard/RGB multi-light), and Gouraud interpolation. Since [[CG_Midsem_notes]] is empty, I mined these formulas directly from the decks.
- **Bridge:** the 17 Sep intensity-quantization deck ($M=2^b$, quantization error, texture domains).
- **Post-midsem (§1–9):** regrouped the 34-row curated Formula Summary from [[CG_Endsem_Notes]] by topic — camera basis/projection matrices, Cohen–Sutherland, clipping, z-buffer depths, BSP side/split, scan-line/Gupta–Sproull, and animation interpolation.

**Conventions followed:** frontmatter + tags, `| Quantity | Expression | Notes |` tables with validity notes, `$inline$` LaTeX, bmatrix matrices, strict `[!type]` callout syntax, wikilinks to each deck, and the em/en-dash and terminology rules from [[CG_context]]. Validated that every line has balanced `$` and no stray pipes inside inline math, so tables and equations render cleanly.
[Timestamp: 2026/11/21 01:31:40]

**user**: now make a pdf file such that its contents should be exactly the same as [[cheat_sheet]]
[Timestamp: 2026/11/21 01:57:06]

**ai**: I'll generate a PDF that faithfully reproduces the note — including rendered LaTeX, tables, and callouts. First let me see what conversion tools are available.The environment has Electron and a local MathJax install — that can render the note faithfully to PDF. Let me check the details.I found a workable pipeline: convert the note to HTML with a small local script, render math with the local MathJax, then print to PDF with the installed Electron binary. Let me set that up in `/tmp` (keeping scratch out of the vault).Now I'll write the converter and print scripts.HTML looks correct. Now let's print it to PDF with Electron.The PDF rendered (357 equations, 21 tables). A CLI flag got mistaken for the output path — let me fix that and re-run cleanly.The script overwrote itself with the PDF bytes. Let me rewrite it using an environment variable for the output path.9-page PDF generated. Let me verify the rendering visually and check that no content was lost.I can't view images directly in this session, so I'll verify structurally instead — checking that every heading/table made it in and that no raw LaTeX or MathJax errors leaked through.Found a real issue: two math cells contain literal `<`, which the browser parsed as HTML tags. Let me escape math bodies properly and regenerate.All 360 equations now render, with no raw TeX delimiters left. Let me run final completeness and overflow checks.Checks pass — no clipped text, and the two "missing" phrases were just my test strings that aren't in the note. Now let me place the finished PDF next to the note in the vault.Created `[[cheat_sheet.pdf]]` in `Computer Graphics/notes/`, alongside the source note.

**What it contains**
- The full visible content of `cheat_sheet.md` — all 21 topic sections, 21 formula tables, both callouts, and the "Last-minute recall" section.
- 360 LaTeX expressions rendered as real math (via MathJax), including matrices, cases, and aligned equations.
- Wikilinks shown as their display text, matching how they read in Obsidian. The YAML frontmatter is omitted since it isn't visible in reading view.

**Format**
- 9 pages, A4 landscape, with styled headers, table shading, and coloured callouts.

**Verified**
- Every heading from the note appears in the PDF; no raw TeX delimiters or MathJax errors leaked through; no words fall outside the page bounds.

The original `cheat_sheet.md` was left unchanged.
[Timestamp: 2026/11/21 01:57:06]