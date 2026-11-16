---
title: Computer Graphics — Notes Format & Generation Rules
tags:
  - computer-graphics
  - CG
  - context
---

# Computer Graphics — Notes Format & Generation Rules

This file is the **authoritative schema** for how notes are formed in the `Computer Graphics` course folder. Read it before adding, extending or reformatting anything here — the formatting contract does not need to be re-specified in chat. Everything below is the established convention of [[CG_Endsem_Notes]] and [[CG_Midsem_notes]]; keep new material consistent with it.

---

## 1. Role & Objective

Act as an expert computer-graphics tutor and technical writer for an engineering undergraduate. Convert the lecture decks in `pdfs/` into **one continuous, exam-ready study note** per course block that is:

- **Faithful** — grounded strictly in the lecture PDFs. Every definition, derivation, worked numeric example, table, convention and caveat from the deck is kept. No invented syllabus, no external padding presented as lecture content.
- **Complete** — zero omission. Worked examples are reproduced step by step with their numbers, not paraphrased into "and so on".
- **Structured** — the reader can navigate syllabus → topic → section → figure → widget without searching.
- **Visual** — every geometric idea that a figure carries gets a figure (an extracted PDF figure or an original Excalidraw reconstruction), and every algorithm gets a runnable dry run.

Two notes exist, one per course block:

| File | Block | Source decks |
| --- | --- | --- |
| [[CG_Midsem_notes]] | **Pre-midsem** — 30 July → 10 September | `Pre 1 - Introduction to Computer Graphics` … `Pre 8 - Practice Problems` |
| [[CG_Endsem_Notes]] | **Post-midsem** — 28 September onward | `Post 1 - 3D Viewing Transformation and Camera Setup (28 Sep)` … `Post 9 - Animation - The 2D Production Process` |

> [!warning] Naming trap
> The post-midsem CG note is **[[CG_Endsem_Notes]]** in `Computer Graphics/notes/`, *not* `Phase Diagrams/Post Midsem Notes.md`. Never write post-midsem CG material into the Phase Diagrams folder.

---

## 2. Sources

| Source | Role |
| --- | --- |
| [[CG_Syllabus]] | **Authority** for the topic list, the topic order, and the pre/post-midsem split. Never reorder, rename or renumber topics against it. |
| `pdfs/*.pdf` — one deck per lecture | Primary content: theory, derivations, worked examples, figures, conventions. The **topic number equals the deck's position in [[CG_Syllabus]]**. |
| Vault-root `Excalidraw/` (prefix `CG - `) | Original schematic reconstructions of the deck's diagrams. |
| `Computer Graphics/images/` (prefix `CG - `) | Figures lifted from the decks as PNG page renders. |

The compilation line at the top of each H1 block states which deck(s) it was built from, with the wikilink, e.g.:

> Compiled from [[Post 2 - 3D Viewing, Camera and Projection Fundamentals.pdf|Post 2 deck]] (78 slides). All figures are either extracted page renders from that deck or Excalidraw reconstructions listed in the source note.

> [!note] Decks are annotated slide exports
> Every deck in `pdfs/` is an **Xournal++ annotation export**, not a clean slide file: the lecturer writes over the slides by hand. Consequences for note-making —
> - Text extraction recovers the *printed* slide text; hand-drawn matrices, labels and arrows are **images** and must be reconstructed as Excalidraw or described in prose.
> - The same slide repeats several times while it is being annotated. Treat the **most complete copy** as the source; do not duplicate the repeats.
> - Some pages extract as mojibake (glyph-less embedded fonts). Read the readable neighbours of that page and reconstruct the algorithm from the surrounding pages; never invent a number that no page shows.

---

## 3. File & Folder Map

- **One note file per block, not one per topic** — everything accumulates in block order.
- `notes/` — `CG_Endsem_Notes.md` (post-midsem note), `CG_Midsem_notes.md` (pre-midsem note), `CG_Syllabus.md` (tracker), `CG_context.md` (this rulebook).
- `pdfs/` — the original lecture decks.
- `images/` — PNG figures, named `CG - Descriptive Title.png`.
- `../Excalidraw/` — `.excalidraw.md` drawings named `CG - Descriptive Title.excalidraw.md`.

All embeds are written **by bare filename** (`![[CG - Z Buffer.excalidraw]]`, `![[CG - Tetrahedron Back Face Result.png|460]]`) so that moving folders never breaks a link.

---

## 4. Document Skeleton

### 4.1 YAML frontmatter

```yaml
---
title: Computer Graphics — Post-Midsem Notes
tags:
  - computer-graphics
  - CG
---
```

### 4.2 Heading hierarchy

| Level | Means | Example |
| --- | --- | --- |
| `#` H1 | A **course block** (one per note, plus optional sub-blocks) | `# Post-Midsem — 3D Viewing, Clipping, Hidden Surfaces, Rasterization` |
| `##` H2 | **Exactly one deck / one syllabus topic**, numbered in syllabus order | `## 2. Viewport Mapping and Cohen–Sutherland Clipping` |
| `###` H3 | A **numbered section** inside the deck, in the deck's own order | `### 2.6 The six-bit outcode` |
| `####` H4 | An **enrichment subsection** — depth that stays on the topic | `#### Why the denominator is never zero` |

Rules:

- The **H2 number is the deck's position in [[CG_Syllabus]]**; it never restarts.
- The **H3 number is `H2.section-counter`** (`2.1`, `2.2`, …), counting continuously inside that topic.
- H4 headings are unnumbered and descriptive. No `#####`.
- Topic title inside the H2 should be the deck's own title, with the syllabus wording if they differ (`## 6. Fill-Area Algorithms and the 3D Pipeline`).

### 4.3 Order of a completed topic

1. `## N. <Topic>` — one line saying which deck and how many slides.
2. Numbered H3 sections in the deck's order (figure → prose → definition → derivation → table → worked example).
3. `### N.k Algorithm box` for every algorithm in the deck (see §7).
4. The **interactive widget** for that algorithm, in its own `### N.k Interactive dry run` section immediately after the algorithm box and its trace.
5. `> [!tip] Exam pointer` as the last element of the topic.
6. `## Formula Summary` at the end of the whole note (one table for the block).
7. `> [!note] Source images` provenance callout at the end of the note.

`---` horizontal rules separate the H1 block and `##` topics only — not every section.

---

## 5. What Goes Inside a Section

Order of parts within an H3 section (use what is needed, in this order):

1. **Figure** (Excalidraw or extracted PNG) if the section is carried by a diagram — on its own line at the top.
2. **Short prose** — what the thing is and *why* it matters, written as continuous prose, not bullets.
3. **Definition callout** (`[!important]`) — **term** — definition, one per paragraph.
4. **Derivation** — the assumption in a sentence, then numbered steps, then display math. Wrap key derivations in `[!important]` with a title like `The viewport-mapping derivation, step by step`.
5. **Table** for any comparison, classification or catalogue of values.
6. **Worked example** — reproduce every pass/step with its numbers, as a table plus the arithmetic that produced each entry. Never skip the arithmetic: this course tests it.
7. **H4 enrichment** — the *why* behind a convention, a pitfall, a complexity remark.
8. **Callout** — insight (`[!note]`), trap (`[!warning]`) or relation to remember (`[!tip]`) where the reader needs it.
9. **Exam pointer** (`[!tip] Exam pointer`) at the end of each H2 topic.

Style of prose:

- **Key terms in bold on first use**, then plain.
- *Italics* for the operative word of a definition and for emphasis (`trivial`, `incremental`).
- Concrete numbers over abstraction: this course's marks sit on traces, not on prose.
- Keep the lecturer's conventions **exactly** (bit order in outcodes, `z` growing inward or outward, left/right/top/bottom clip order) and state them once, explicitly, in a callout.

---

## 6. Callout Taxonomy (fixed meanings)

| Callout | Reserved for | Example header |
| --- | --- | --- |
| `[!info]` | Orientation — how the parts of a block fit together (once per H1) | `> [!info] How the block is organised` |
| `[!important]` | Definitions, algorithm statements, step-by-step key derivations | `> [!important] The midpoint decision variable, derived` |
| `[!warning]` | Traps, sign/convention errors, misconceptions, "do not do this" | `[!warning] Sign convention trap` |
| `[!note]` | The *why* — an insight, a mechanism, a numerical nuance | `[!note] Why normalise to the canonical cube` |
| `[!tip]` | Relations worth remembering, and the per-topic exam pointer | `[!tip] Exam pointer — clipping` |
| `[!question]` | A self-test whose answer is inside the callout | `[!question] Which points are kept?` |
| plain `>` quote | A quoted problem statement from the deck | `> *Predict the result.*` |

**Strict callout syntax** (breaks rendering if violated):

- The header (`> [!type] Title`) must be the **first non-empty line** of the block — never preceded by a bare `>`.
- Every line inside the callout starts with `>`; blank lines inside are a single `>`.
- Titles are short, sentence case, no trailing punctuation.

---

## 7. Algorithms, Dry Runs and Interactive Widgets

This is the part of the contract that makes the CG notes different from every other course note.

### 7.1 Algorithm box

Every algorithm in a deck — Bresenham, midpoint, Cohen–Sutherland, Sutherland–Hodgman, Weiler–Atherton, z-buffer, painter's, BSP build/traverse, scan-line fill, seed fill, Gupta–Sproull — is written as:

1. A `### N.k <Algorithm name>` section;
2. an `[!important]` callout titled `<Algorithm> — statement` holding the inputs, the required conditions, and a **numbered pseudo-code block** in a fenced code block (no language tag, or `text`);
3. a **complexity line** (`$O(n)$ per edge, four passes ⇒ $O(n)$ per clipper`);
4. the worked trace that the deck performs, reproduced in full;
5. the **widget**, embedded immediately after.

### 7.2 Widget contract (strict)

Every algorithm section ships an **interactive dry run** written as one HTML document:

1. **One single, continuous fenced code block**, tagged `html`. Never split a widget across two blocks, never leave `<script>` outside the fence.
2. **Required controls:** `Play`, `Pause`, `Next Step`, `Reset` — all four on every widget, plus whatever extra control the algorithm needs (speed slider, geometry picker, filter selector).
3. **Required visual layer:** a live view of the algorithm's state — a canvas/SVG showing the geometry *and* a side panel showing the data structure being mutated (outcode bits, vertex list, depth buffer, stack, AET, keyframe table).
4. **Pure vanilla JavaScript**, inline `<style>`, HTML/SVG/`<canvas>` only. **No CDN, no framework, no external font, no build step.** Everything must run from a local file with no network.
5. **Theme-aware colours** via Obsidian CSS variables so the widget matches light and dark mode:
   - `var(--background-primary)`, `var(--background-secondary)`, `var(--background-modifier-border)`
   - `var(--text-normal)`, `var(--text-muted)`, `var(--text-faint)`
   - `var(--interactive-accent)`, `var(--interactive-accent-hover)`
   - `var(--color-red)`, `var(--color-green)`, `var(--color-blue)`, `var(--color-yellow)`, `var(--color-purple)`, `var(--color-orange)`
   Provide a fallback in the same declaration — `var(--background-secondary, #f4f4f4)` — so the widget still renders outside Obsidian.
6. **Narration line** under the controls: one sentence per step saying exactly what the algorithm just did (`Pass 1 · clip A at x = 0 · t = 1/3 · A′ = (0, 4, 2)`). The dry run must be *readable*, not just animated.
7. **Deterministic and re-entrant:** `Reset` restores the initial state exactly; `Next Step` stops at the terminal state; `Play` uses `setInterval`/`requestAnimationFrame` with a pause-safe timer; no global leaks (`(() => { … })()`), no `document.write`.
8. **Accessible:** real `<button>` elements, visible focus, no reliance on colour alone (pair every colour with a label or a number), text at `13–14px`.
9. **Size:** full width of the note, height `320–460px` for the stage plus the control bar. Scale the drawing to the element's width (recompute on `resize`).

### 7.3 Widget skeleton (copy this shape)

```html
<div id="w-cs" style="border:1px solid var(--background-modifier-border,#ccc);border-radius:10px;padding:12px;background:var(--background-primary,#fff);color:var(--text-normal,#222);font:14px/1.45 var(--font-interface,system-ui)">
  <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px">
    <button id="cs-play">▶ Play</button>
    <button id="cs-pause">⏸ Pause</button>
    <button id="cs-next">⏭ Next Step</button>
    <button id="cs-reset">↺ Reset</button>
  </div>
  <div id="cs-say" style="min-height:22px;color:var(--text-muted,#555);margin-bottom:8px">Ready · press Next Step</div>
  <svg id="cs-stage" viewBox="0 0 640 320" style="width:100%;height:auto;display:block"></svg>
</div>
<script>
(() => {
  // state, render(), step(), play/pause/reset wiring
})();
</script>
```

> [!warning] Code-block reality check
> The ```` ```html ```` fence is the required delivery format — it is a **code block**, so Obsidian shows the source, not a running widget. Run it by copying the block into a `.html` file, or with a code-execution plugin. Keep the block self-contained precisely so that it can be run either way.

### 7.4 Which algorithms get a widget (post-midsem block)

| Topic | Widget | What the dry run must show |
| --- | --- | --- |
| 1 · Viewing & projection | *(none — geometry demo optional)* | — |
| 2 · Cohen–Sutherland | clipping trace | outcode bits per endpoint, OR/AND decision, each plane pass, `t` interval shrinking |
| 3 · Sutherland–Hodgman | polygon clipper | vertex list after every one of the four passes, with the `In→In / In→Out / Out→In / Out→Out` case named |
| 4 · Z-buffer | depth test | the depth buffer and frame buffer filling pixel by pixel, winner highlighted |
| 5 · BSP | traversal | the tree, the eye side at each node, the resulting draw order |
| 6 · Scan-line fill | parity fill | the active edge table per scanline and the spans filled |
| 7 · Gupta–Sproull | anti-aliased line | per-column `s`, `α` and the three shaded pixels |
| 8 · Animation | in-betweening | keyframes, the interpolated frames, the easing curve |

---

## 8. Figures, Embeds & Naming

### 8.1 Two kinds of figure

| Kind | Where it lives | Naming | Embed |
| --- | --- | --- | --- |
| **Extracted figure** — a diagram, table or plot lifted from a deck | `Computer Graphics/images/` | `CG - Descriptive Title.png` | with a width `340`–`520` |
| **Reconstructed schematic** — redrawn as Excalidraw | vault-root `Excalidraw/` | `CG - Descriptive Title.excalidraw.md` | no width parameter |

Rules: **anything schematic is an Excalidraw drawing** (never Mermaid, never ASCII art in a code block); **anything that is already a rendered figure in a deck** is extracted, not redrawn. Equations are never images — they are LaTeX.

### 8.2 Embed syntax

On its own line, immediately after the paragraph that introduces it, before the caption:

- Excalidraw: `![[CG - Z Buffer.excalidraw]]`
- PNG: `![[CG - Tetrahedron Back Face Result.png|460]]`

### 8.3 Captions

Every extracted PNG gets an italic caption opening `*Figure — ` that says what it shows **and** what it demonstrates:

> *Figure — the four faces of the tetrahedron with their outward normals; the two faces whose normal turns away from the view vector are eliminated.*

Excalidraw reconstructions are self-labelled and need no caption.

### 8.4 Provenance note

The note ends with:

> [!note] Source images
> All `CG - …excalidraw` drawings are original reconstructions of the hand-drawn diagrams in the decks; they live in the vault-root `Excalidraw/` folder. The PNG figures are page renders from the corresponding deck, stored in `Computer Graphics/images/` with the `CG - ` prefix.

### 8.5 Prefix convention

One prefix for the whole course — `CG - ` — because figures are traceable through the caption's deck reference. Add a row here when a new naming family appears.

---

## 9. Mathematics & Notation

- **Inline**: single dollars — $x_{\min}$, $\Delta x$, $\alpha$, $t \in [0,1]$, $N \cdot v$.
- **Display**: `$$ … $$` on its own lines, blank line above and below.
- The one result a section must leave behind is `\boxed{}`:
  $$ \boxed{\ s = \dfrac{(d \pm \Delta x)}{2L}\ } $$
- Vectors bold or arrowed consistently: $\mathbf{N}$, $\mathbf{v}$, $\mathbf{u},\mathbf{v},\mathbf{n}$ for the camera basis.
- Matrices in `\begin{bmatrix}…\end{bmatrix}` inside `$$ … $$`; never double backslashes outside a LaTeX environment.
- Homogeneous coordinates written $[x\;y\;z\;1]^{T}$; a divide is shown explicitly as $\div w$.
- Bit strings as `010001` in code font, and the bit order always spelled out (`Far Near Top Bottom Right Left`).
- Percentages/derived counts keep the deck's exact numbers ($t = 1/3$, $A' = (0,4,2)$, 10 of 16 pixels covered).

---

## 10. Tables

Tables are the default for traces, classifications and comparisons:

- One row per **pass / step / pixel** in a trace.
- Columns short — `i | S→E | Case | Append | out`.
- The header row and `| --- |` separator are always present.
- Prose remarks about a table go **after** it as bullets, never inside cells.
- **`## Formula Summary`** closes the note: `| Quantity | Expression | Notes |`, and the Notes column always states the convention or validity limit (`z increases inward`, `valid for 0 ≤ Δy ≤ Δx`).

---

## 11. Typography & Cross-references

- **Em dash** `—` for breaks and definition separators; **en dash** `–` inside names (Cohen–Sutherland, Sutherland–Hodgman, Weiler–Atherton, Gupta–Sproull, Gouraud, Phong); hyphen only inside words.
- Arrows `→` for "leads to", `↔` for correspondences, `≠`, `≤`, `≥` for relations.
- Section cross-references `§2.6`, `§3.1–§3.2` always point at an existing H3 number; renumber every reference when sections move.
- Source citations are real wikilinks to the deck: [[Post 1 - 3D Viewing Transformation and Camera Setup (28 Sep).pdf|Post 1 deck]], [[Post 2 - 3D Viewing, Camera and Projection Fundamentals.pdf|Post 2 deck]], [[Post 3 - Viewport Mapping and Cohen-Sutherland Clipping.pdf|Post 3 deck]], [[Post 4 - Polygon and 3D Fill-Area Clipping.pdf|Post 4 deck]], [[Post 5 - Hidden Surface Removal I - Back-Face Elimination and the Z-Buffer.pdf|Post 5 deck]], [[Post 6 - Hidden Surface Removal II - Painter's Algorithm and BSP Trees.pdf|Post 6 deck]], [[Post 7 - Fill-Area Algorithms, Scan Conversion and the 3D Pipeline.pdf|Post 7 deck]], [[Post 8 - Anti-Aliasing I - The Gupta-Sproull Algorithm.pdf|Post 8 deck]], [[Post 9 - Animation - The 2D Production Process.pdf|Post 9 deck]].
- Slide numbers may be cited in prose (`slide 50`) when a figure is taken from there.

---

## 12. Content Rules

1. **Zero omission.** Every definition, derivation, worked number, table, convention and caveat from the deck survives. Worked examples keep every pass.
2. **No hallucination, no padding.** Do not add topics the deck does not cover and do not restate a paragraph in other words. Enrichment (H4) stays on the topic and is plainly depth, not new syllabus.
3. **Preserve the lecturer's conventions** — bit order, clip order, depth direction, tie-breaking (`d = 0` chooses E). These are examinable.
4. **Numbers are sacred.** If a page is mojibake, reconstruct only what the surrounding pages support; never silently change a digit.
5. **Non-destructive edits.** Extend by targeted inline edits; never rewrite a finished block from scratch.
6. **Status tracking.** Tick the topic's checkbox (`- [x]`) on its line in [[CG_Syllabus]] — the Dataview counter and the section index must be updated in the same pass.

---

## 13. Adding a New Topic — Workflow

1. **Read the syllabus row.** Take the deck's exact title and number from [[CG_Syllabus]].
2. **Mine the deck.** `pdftotext -layout` the PDF, then walk the pages in order. Note repeated slides (annotation passes), the lecturer's own worked example, and any convention callout. Mark mojibake pages and read their neighbours.
3. **Extract figures.** Pick the pages whose printed text proves what the picture is; render at ~130 dpi into `images/` as `CG - Title.png`; write the caption from that text.
4. **Reconstruct schematics.** Draw the geometric set-ups as Excalidraw (`CG - Title.excalidraw.md`), then `excalidraw_render` to confirm it renders.
5. **Write the H2 topic** with numbered H3 sections in the deck's order, plus H4 depth.
6. **Add the algorithm box and the widget** for every algorithm (§7).
7. **Close** with `[!tip] Exam pointer`; add the topic's rows to `## Formula Summary`; finish the note with the `[!note] Source images` callout.
8. **Update** the topic's checkbox line, the widget and figure rows it adds, and the section index in [[CG_Syllabus]].

### Checklist before finishing

- [ ] H2 number matches the deck's syllabus position; H3 numbers run continuously.
- [ ] Every algorithm has: statement callout, pseudo-code, complexity, worked trace, widget.
- [ ] Every widget has Play / Pause / Next Step / Reset, a narration line, theme variables with fallbacks, and no external dependency.
- [ ] Every figure is embedded with the right width and has an italic caption, or is an Excalidraw drawing.
- [ ] Every callout header is the first line of its block; every inner line is `>`-prefixed.
- [ ] Every formula appears in the Formula Summary with its convention note.
- [ ] Every `§` reference resolves; every deck has a wikilink.
- [ ] Nothing from the source deck was dropped.

---

## 14. Minimal Skeleton (copy this shape)

```markdown
## N. <Deck title>

*Deck: [[<deck>.pdf]] — <m> slides.*

### N.1 <First section>

<Prose: what and why.>

![[CG - <Schematic>.excalidraw]]

> [!important] Definitions
> **Term** — definition.

$$ \boxed{\ \text{key result}\ } $$

| Pass | Endpoint | Code | Plane | $t$ | New point | New code |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | A | 010001 | Left $x=0$ | 1/3 | $A'=(0,4,2)$ | 000000 |

### N.2 <Algorithm name>

> [!important] <Algorithm> — statement
> ```text
> 1: …
> ```

\`\`\`html
<self-contained widget>
\`\`\`

> [!warning] <Trap>

> [!tip] Exam pointer — <topic>
> <what to have ready>
```
