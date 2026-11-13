# Material Science (MO-201) — Notes Format & Generation Rules

This file is the **authoritative schema** for how notes are formed in this folder. Read it before adding, extending or reformatting anything here — the format does not need to be re-specified in chat. Everything below is the observed, established convention of [[notes]]; keep new material consistent with it.

---

## 1. Role & Objective

Act as an expert materials-science tutor and technical writer for an engineering undergraduate. Convert the lecture PDFs and the handwritten class notes of this folder into **one continuous, exam-ready study note** (`notes.md`) that is:

- **Faithful** — grounded strictly in the lecture PDFs, the handwritten notes and the prescribed textbooks. No invented content, no external padding.
- **Complete** — every definition, justification, counterexample, derivation, number and caveat from the source is retained. Summarising is *not* the job.
- **Structured** — the reader can navigate from syllabus → topic → section → figure without searching.

---

## 2. Sources

| Source | Role |
| --- | --- |
| `syllabus.md` | **Authority** for topic list, topic order and the midsem/post-midsem split. Never reorder or rename topics against it. |
| Lecture PDFs in this folder (e.g. [[Mechanical Properties part 1_Odd_2026-27.pdf]], [[Phase_Diagrams.pdf]], [[Crystal Defects.pdf]]) | Primary content: theory, figures, tables, worked examples, exam emphasis. |
| [[MO NOTES (1).pdf]] | Handwritten class notes — used for the lecturer's own emphasis, extra derivations and "as taught" points. Always cite the page range. |
| Textbooks — **Raghavan, *Materials Science and Engineering***; **Callister, *Fundamentals of Materials Science and Engineering*** | Used to complete and cross-check the slides; cite by author/table number in prose (e.g. "Callister, Table 7.5"). |
| `attachments/` | Figures extracted from the lecture PDFs. |
| `Excalidraw/` (vault root) | Original schematic reconstructions drawn as Excalidraw files. |

The compilation line at the top of a block states which sources it was built from, with wikilinks and page ranges, e.g.:

> Compiled from the lecture slides ([[Mechanical Properties part 1_Odd_2026-27.pdf]], …) and the handwritten class notes in [[MO NOTES (1).pdf]] (pp. 100–131). Slides follow **Raghavan, *Materials Science and Engineering*** and **Callister, *Fundamentals of Materials Science and Engineering***.

---

## 3. File & Folder Map

- **One note file, not one per topic** — everything accumulates in `notes.md`, in syllabus order.
- `notes.md` — the single growing note.
- `syllabus.md` — the topic list.
- `attachments/` — PNGs extracted from the lecture PDFs (prefix-named, see §7).
- `../Excalidraw/` — `.excalidraw.md` drawings, prefix-named `MP - `, referenced from the note by embed.
- Lecture `.pdf`s and the odd `.mp4`/`.xlsx` stay in this folder and are linked/embedded by filename.

---

## 4. Document Skeleton

### 4.1 YAML frontmatter

```yaml
---
title: Material Science — MO-201 Notes
tags:
  - materials-science
  - MO-201
---
```

### 4.2 Heading hierarchy

| Level | Means | Example |
| --- | --- | --- |
| `#` H1 | A **course block** — a group of related lecture PDFs, or the syllabus map | `# Syllabus Map`, `# Mechanical Properties` |
| `##` H2 | **One syllabus topic / PDF**, numbered in syllabus order | `## 1. Mechanical Properties — I`, `## 2. Mechanical Properties — II` |
| `###` H3 | A **numbered section** inside the topic, following the lecture's own order | `### 2.4 CRSS and the Schmid factor` |
| `####` H4 | An **enrichment subsection** — "added depth" that extends beyond the slides but stays on the topic | `#### Frank's rule — the general criterion` |

Rules:

- The **H2 number is the topic's position in `syllabus.md`** (1…9 for post-midsem). It never restarts or gets reused.
- The **H3 number is `H2.topic-counter`** (`1.1`, `1.2`, … `2.19`, `3.10`). Counters run continuously within the H2 topic.
- H4 subsections are **unnumbered** and titled descriptively (often an em-dash clause: `#### Why Hooke's law works`).
- Do **not** use `#####`. Four levels is the maximum.
- The H3 sections are the lecture's own sequence; the H4 subsections are where the "added depth to be ready with" lives (see the exam pointers).

### 4.3 Order of a completed block

1. `# <Course block>` H1 + a short orientation paragraph on why the topic matters.
2. `---` separator.
3. `## N. <Topic>` — one H2 per lecture PDF, in order.
4. Numbered H3 sections; inside each: figure, prose, definition callout, table, derivation, H4 subsections.
5. `## Formula Summary` — one table collecting every formula of the block (see §9).
6. `> [!note] Source images` — the provenance note (see §7.4).

`---` horizontal rules separate the H1 blocks and the major internal divisions only — not every section.

---

## 5. What Goes Inside a Section

Order of parts within an H3 section (use what is needed, in this order):

1. **Excalidraw figure** (if the section is best introduced by a diagram) — on its own line, at the top of the section.
2. **Short prose paragraph** — what the thing is, and *why it matters*. Written as continuous prose, not bullets.
3. **Definition callout** (`[!important]`) — bold term, em dash, definition. One definition per paragraph inside the callout.
4. **Derivation** — prose sentence stating the assumption, then numbered steps, then display math. Derivations of key results are wrapped in a `[!important]` callout with numbered steps (e.g. "The Frenkel derivation, step by step").
5. **Table** for any comparison, catalogue or set of typical values (see §9).
6. **Extracted figure + italic caption** (`*Figure — …*`) immediately below the prose that references it.
7. **H4 subsections** for enrichment: tensor forms, worked examples, "why it is exactly five", historical notes, practical consequences.
8. **Callout** — insight (`[!note]`), trap (`[!warning]`) or relation-to-remember (`[!tip]`), placed where the reader needs it.
9. **Exam pointer** (`[!tip] Exam pointer`) at the **end of each H2 topic** (the last part), listing the formulas and ideas to have ready.

Style of prose:

- **Key terms in bold on first use**, then plain.
- **Italics for emphasis** and for the operative word of a definition (`permanent`, `non-recoverable`).
- Concrete, physical framing over abstraction — a section normally answers "*why* is this true" before "*what is the formula*".
- Contrasting examples and design consequences are kept, not trimmed.

---

## 6. Callout Taxonomy (fixed meanings)

| Callout | Reserved for | Example header |
| --- | --- | --- |
| `[!info]` | Orientation — how the parts of a block fit together (once per H1 block) | `> [!info] How the three parts fit together` |
| `[!important]` | Definitions and step-by-step derivations of key results | `> [!important] Definitions` / `> [!important] The Frenkel derivation, step by step` |
| `[!warning]` | Traps, corrections, common misconceptions, "do not do this" | `> [!warning] Common exam trap` / `> [!warning] Correct indices for the classic example` |
| `[!note]` | The *why* — an insight, mechanism or nuance worth pausing on | `> [!note] Why $E$ is the least structure-sensitive property` |
| `[!tip]` | Relations worth remembering, and the per-topic exam pointer | `> [!tip] Exam pointer — Part II` |
| `[!question]` | A self-test / "what does X mean" whose answer is inside the callout | `> [!question] What do "brittle" and "ductile" mean?` |
| plain `>` quote | A rhetorical question, a worked-example problem statement, or a quoted statement | `> *How much elastic and plastic deformation can a material accommodate …?*` |

**Strict callout syntax** (breaks rendering if violated):

- The callout header (`> [!type] Title`) must be the **first non-empty line** of the block — never preceded by a bare `>`.
- Every line inside the callout, including blank lines and `$$…$$` blocks, starts with `>` (blank lines inside: a single `>`).
- Nested solutions use doubled prefixes — outer `> [!question] …`, inner `> > [!success]- Solution (Click to expand)`, and every solution line begins with `> > `. Never leave a bare `>` or unquoted line inside a nested callout.
- Titles are short, sentence-case, no trailing punctuation.

---

## 7. Figures, Embeds & Naming

### 7.1 Two kinds of figure

| Kind | Where it lives | Naming | Embed |
| --- | --- | --- | --- |
| **Extracted figure** — a photograph, plot, micrograph or table lifted from the lecture PDF | `attachments/` (PNG) | `PREFIX - Descriptive Title.png` | with a width parameter |
| **Reconstructed schematic** — redrawn by me as an Obsidian Excalidraw drawing | `../Excalidraw/` (`.excalidraw.md`) | `MP - Descriptive Title.excalidraw.md` | no width parameter |

Rules: **any diagram, flowchart or schematic is an Excalidraw drawing** (never Mermaid, never a hand-drawn ASCII figure); **any figure that already exists in the PDF is extracted to `attachments/`** rather than redrawn.

### 7.2 Embed syntax

The embed is written on its own line: an exclamation mark, then double brackets around the **exact filename including extension**. For example, for the file `MP - Types of Loading.excalidraw` the line is written as

\![[MP - Types of Loading.excalidraw]]

and for `MP2 - Yoffee diagram.png` at a display width of 380 px it is

\![[MP2 - Yoffee diagram.png|380]]

*(the leading backslash above only stops this reference file from embedding them — write it without the backslash in `notes.md`)*

- **Excalidraw**: no width parameter — let it render at natural size.
- **PNG**: always give a width between `340` and `520` (most are `420`–`480`), chosen to match the source figure's aspect.
- The embed goes **immediately after the paragraph that introduces it**, before the caption.

### 7.3 Captions

Every extracted PNG is followed by an italic caption on its own line, opening with `*Figure — `, describing what the figure shows *and* the physics it demonstrates:

> *Figure — the Yoffee diagram: yield stress falls with temperature, cleavage fracture stress is nearly temperature-independent, and the intersection defines the DBTT.*

Excalidraw reconstructions do not need a caption (they are self-labelled).

### 7.4 Provenance note

Each course block ends with the `[!note] Source images` callout stating that the Excalidraw figures are original reconstructions and where the extracted figures came from, e.g.:

> All Excalidraw figures in this note are original reconstructions of the diagrams in the three lecture PDFs and the handwritten notes; the vault copies live in the `Excalidraw/` folder with the `MP - ` prefix. The photographs, plots and tables embedded above are the original figures extracted from the three lecture PDFs and stored in `Material Science/attachments/` with the `MP`/`MP2`/`MP3` prefix.

### 7.5 Prefix convention

The attachment prefix encodes **the course block plus the part number**, so that a figure is traceable to its PDF:

| Topic (syllabus order) | Attachment prefix | Excalidraw prefix |
| --- | --- | --- |
| 1–3 Mechanical Properties — I / II / III | `MP1 - ` / `MP2 - ` / `MP3 - ` | `MP - ` |
| 4 Shockley & Frank partial dislocations | `SD - ` | `SD - ` |
| 5 Composites | `COMP - ` | `COMP - ` |
| 6–7 Electrical & Electronic Properties — 1 / 2 | `EP1 - ` / `EP2 - ` | `EP - ` |
| 8 Magnetic Properties | `MAG - ` | `MAG - ` |
| 9 Dielectric Materials, Polarization, Optical Properties | `DIE - ` | `DIE - ` |

Use **spaces and Title Case inside the name, not underscores**. When a new prefix is first used, add its row to this table.

---

## 8. Mathematics & Notation

- **Inline** parameters, variables and short expressions: single dollars — $r^*_{\text{het}}$, $\theta$, $\gamma_{SL}$, $\tau_{CRSS}$, $E$, $\nu$.
- **Display** derivations and standalone results: `$$ … $$` on their own lines, blank line above and below.
- **Never** use double backslashes except inside LaTeX matrix/align environments.
- The **one result a section must leave behind** is wrapped in `\boxed{ }`, e.g.

  $$ \boxed{\ \tau_R = \sigma\, m, \qquad m = \cos\phi_1\cos\phi_2\ } $$

- **Units and words** in math use upright `\text{}`: $\text{N/m}^2$, $\text{MPa}$, $\text{GPa}$; multiple statements on one line are spaced with `\qquad`.
- Use `\tfrac`/`\dfrac` for fractions inside inline or tight contexts, `\frac` in display.
- `$\sim$` (not `~`) for "approximately" inside math; `≈` in prose.
- Numbers keep their significant figures and units exactly as in the source; ranges use an en dash (0.25–0.35).
- Symbols are defined on first use in the section, in the sentence that introduces the equation.

---

## 9. Tables

Tables are the default for **comparisons, catalogues and data**:

- Property comparisons and test catalogues (`| Test | What it measures | Typical use |`).
- Typical values with units in the header (`| Material | $E$ (GPa) | Yield strength (MPa) | UTS (MPa) |`).
- Symmetry/constant counts, model comparisons, historical case tables.
- Prose remarks that apply to a table go **after** it, as bullets.

**Column style:** the header row and the `| --- |` separator row are always present; cells are short phrases (no full sentences); the first column names the item and is bolded when the table is a catalogue.

**Formula Summary** — each course block closes with an H2 `## Formula Summary` table of every formula in the block, with three columns:

| Quantity | Expression | Notes |
| --- | --- | --- |
| True stress / strain | $\sigma_T = \sigma(1+\varepsilon)$, $\varepsilon_T = \ln(1+\varepsilon)$ | Valid to onset of necking only |

The Notes column carries the validity limit, the assumption, or the definition of a symbol — never leave it empty if there is a caveat.

---

## 10. Typography & Cross-references

- **Em dash** `—` for parenthetical breaks and definition separators; **en dash** `–` for ranges and compound names (Hall–Petch, Peierls–Nabarro); hyphen only inside words.
- Arrows `→` and `⟹` for "leads to"; `↔` for correspondences; `⇏`/`≠` for the distinctions being stressed.
- Section cross-references are written `§2.7`, `§1.6`, `§3.1–§3.2` — always pointing at an existing H3 number.
- Source citations are **real wikilinks** to the PDFs, e.g. [[Phase_Diagrams.pdf]], [[MO NOTES (1).pdf]] — with page numbers when they exist.
- Never leave a section number referenced but absent; when sections are renumbered, update every `§` reference.

---

## 11. Content Rules

1. **Zero omission.** Keep 100 % of the technical detail — explanations, derivations, numbers, justifications, counterexamples, historical cases, design consequences. Never truncate or abbreviate unless explicitly asked to summarise.
2. **No hallucination, no padding.** Do not add external theory or background that is not in the sources. Enrichment (H4) is still bound to the topic and must be marked as depth beyond the slides.
3. **No restating.** Do not re-explain in a second way what a paragraph already said; depth means a *new* mechanism, form or consequence.
4. **Preserve the lecturer's emphasis** — anything marked as an exam pointer, a common trap or a worked example in the class notes is kept and flagged with the matching callout.
5. **Non-destructive edits.** When extending an existing note, make targeted inline edits; never overwrite the file from scratch. Nothing already written is deleted or reworded.
6. **Status is tracked** in the Syllabus Map table (`✅ noted below` / `—`), and is updated whenever a topic is added.

---

## 12. Adding a New Topic — Workflow

1. **Read the syllabus row.** Take the topic's exact title and number from [[syllabus]]; confirm the row exists in the Syllabus Map table.
2. **Mine the source PDF.** Work through the lecture slides in order, plus the relevant page range of [[MO NOTES (1).pdf]]; note the lecturer's worked examples and emphasis.
3. **Extract figures.** Pull the photographs, plots and tables out of the PDF into `attachments/` using the correct prefix from §7.5 and a Title Case descriptive name.
4. **Reconstruct schematics.** Draw the diagram-only figures as Excalidraw files in `Excalidraw/` with the block's Excalidraw prefix, then verify each one renders (`excalidraw_render`) before citing it.
5. **Write the H2 topic** with numbered H3 sections in the lecture's own sequence, adding H4 enrichment subsections where the source invites them.
6. **Integrate pasted NotebookLM text** verbatim in detail: format it into the same structure (prose paragraphs, tables, callouts, display math) and place it under the correct H3/H4 header — do not summarise, condense or drop lines.
7. **Close the block** with the `[!tip] Exam pointer`, the `## Formula Summary` table and the `[!note] Source images` provenance note.
8. **Update the Syllabus Map** status column.

### Checklist before finishing

- [ ] H2 number matches the syllabus position; H3 numbers run continuously.
- [ ] Every figure is embedded with the right width and has an italic `*Figure — *` caption (PNGs) or is an Excalidraw file (schematics).
- [ ] Every callout header is the first line of its block and every inner line is `>`-prefixed.
- [ ] Every formula is inline `$…$` or display `$$…$$`; the section's key result is `\boxed{}`.
- [ ] Every new formula appears in the Formula Summary with its validity note.
- [ ] Every `§` reference resolves; every source has a wikilink.
- [ ] Nothing from the source PDF or the pasted text was dropped.

---

## 13. Minimal Skeleton (copy this shape)

```markdown
# <Course block name>

<One paragraph: what this block covers and why it matters.>

---

## N. <Topic title exactly as in syllabus>

### N.1 <First section title>

<Prose paragraph — what and why.>

> [!important] Definitions
> **Term** — definition.
> **Term** — definition.

| A | B | C |
| --- | --- | --- |
| … | … | … |

$$ \boxed{\ \text{key result}\ } $$

#### <Enrichment subsection>

<Added depth.>

> [!tip] Exam pointer
> <What to have ready.>

---

## Formula Summary

| Quantity | Expression | Notes |
| --- | --- | --- |
| … | … | … |

> [!note] Source images
> <Provenance of the figures in this block.>
```
