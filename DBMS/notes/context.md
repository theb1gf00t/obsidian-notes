---
title: DBMS — Notes Format & Generation Rules
aliases:
  - DBMS context
  - DBMS notes rules
course: DBMS
tags:
  - dbms
  - DBMS
  - context
---

# DBMS — Notes Format & Generation Rules

This file is the **authoritative schema** for how notes are formed in the `DBMS` course folder. Read it before adding, extending or reformatting anything here — the formatting contract does not need to be re-specified in chat. It is modeled on [[CG_context]] and on the established convention of [[Post-Midsem-Notes]]; keep new material consistent with it.

---

## 1. Role & Objective

Act as an expert database tutor and technical writer for an engineering undergraduate. Convert the lecture decks in `pdfs/` into **one continuous, exam-ready study note** for the post-midsem / end-semester block that is:

- **Faithful** — grounded strictly in the lecture PDFs. Every definition, formula, worked numeric example, table, figure, convention and caveat from the deck is kept. No invented syllabus, no external padding presented as lecture content.
- **Complete** — **zero omission**. Worked examples are reproduced step by step with their exact numbers (bucket splits, block-access counts, $B^+$ tree traces), not paraphrased into "and so on".
- **Structured** — the reader can navigate syllabus → topic → section → figure → formula without searching.
- **Visual** — every geometric or structural idea a figure carries gets a figure: an original Excalidraw reconstruction for **schematic** diagrams, or a page render lifted from the deck for figures that are already drawn there.
- **Explained** — prose says *why* a structure exists and *what problem* it fixes, in plain language, before the formal definition. The book is consulted for clarity, never as a second source of exam facts.

One note file holds the whole block:

| File | Block | Source decks |
| --- | --- | --- |
| [[Post-Midsem-Notes]] | **Post-midsem / end-sem** — file management, query algorithms, transactions | [[file-management.pdf]], [[algos.pdf]], [[transactions.pdf]] |

> [!warning] Naming trap
> The DBMS note is **[[Post-Midsem-Notes]]** in `DBMS/notes/`. Do not write DBMS material into the Computer Graphics, Phase Diagrams or Graph Theory folders. The rulebook is **[[context]]** here, not [[CG_context]].

---

## 2. Sources

| Source | Role |
| --- | --- |
| [[Syllabus]] | **Authority** for the topic list, the topic order and the checkboxes. Never reorder, rename or renumber topics against it. |
| `pdfs/*.pdf` — one deck per topic | Primary content: theory, formulas, worked examples, figures, conventions. The **topic number equals the deck's position in [[Syllabus]]**. |
| `pdfs/silberschatz_dbms.pdf` | **Explanation only.** Silberschatz *Database System Concepts*, 7th ed. Ch. 13 (Data Storage Structures), Ch. 14 (Indexing), §24.5 (Hash Indices) clarify the deck. Never present book-only material as deck content, and never replace the deck's convention with the book's (e.g. trailing bits vs prefix bits in extendible hashing). |
| Vault-root `Excalidraw/` (prefix `DBMS - `) | Original schematic reconstructions of the deck's diagrams. |
| `DBMS/images/` (prefix `DBMS - `) | Figures / diagrams lifted from the decks as PNG page renders. |

The compilation line at the top of each H2 topic states which deck built it, with the wikilink and slide count, e.g.:

> *Deck: [[file-management.pdf|file-management deck]] — 60 slides, Prof. P. Sreenivasa Kumar, IIT Madras.*

> [!note] The decks are lecture slides, not clean textbook chapters
> - Text extraction (`pdftotext -layout`) recovers the printed text; hand-drawn annotations, arrows and tree drawings are **images** and must be reconstructed as Excalidraw or described in prose.
> - A slide may repeat while it is being annotated. Use the **most complete copy**; do not duplicate repeats.
> - Some pages extract with scrambled layout. Read the readable neighbours and reconstruct only what they support; **never invent a number** that no page shows.
> - Keep the deck's own numbers even when a textbook would use a tidier example ($C = rM$, 9500 → 49 blocks, $m \le 37$, $m_{leaf} \le 33$, 90000 → 484 blocks, the insertion/deletion traces).

---

## 3. File & Folder Map

- **One note file per block, not one per topic** — everything accumulates in topic order.
- `DBMS/notes/` — `Post-Midsem-Notes.md` (the note), `Syllabus.md` (tracker), `context.md` (this rulebook).
- `DBMS/pdfs/` — the lecture decks and the Silberschatz book.
- `DBMS/images/` — PNG figures, named `DBMS - Descriptive Title (deck pN).png`.
- Vault-root `Excalidraw/` — `.excalidraw.md` drawings named `DBMS - Descriptive Title.excalidraw.md`.

All embeds are written **by bare filename** (`![[DBMS - Bplus Tree Structure.excalidraw]]`, `![[DBMS - Primary Index.excalidraw]]`) so that moving folders never breaks a link.

---

## 4. Document Skeleton

### 4.1 YAML frontmatter

```yaml
---
title: DBMS — Post-Midsem Notes (File Organization, Query Algorithms, Transactions)
tags:
  - dbms
  - DBMS
  - file-management
  - indexing
  - post-midsem
---
```

Add a tag for each new topic when it is written.

### 4.2 Heading hierarchy

| Level | Means | Example |
| --- | --- | --- |
| `#` H1 | The **course block** (one per note) | `# Post-Midsem — File Organization and Indexing · Query Algorithms · Transactions` |
| `##` H2 | **Exactly one syllabus topic**, numbered in syllabus order | `## 1. File Organization and Indexing` |
| `###` H3 | A **numbered section** inside the topic, in the deck's slide order | `### 1.34 Order calculation — worked example` |
| `####` H4 | An **enrichment subsection** — depth that stays on the topic | `#### Why one entry per block is enough` |

Rules:

- The **H2 number is the deck's position in [[Syllabus]]**; it never restarts.
- The **H3 number is `H2.section-counter`** (`1.1`, `1.2`, …), counting continuously inside that topic.
- H4 headings are unnumbered and descriptive. No `#####`.
- Use an **em dash** in titles, not a hyphen, for the break between the number and the name.

### 4.3 Order of a completed topic

1. `## N. <Topic>` — one italic line naming the deck, its slide count and its source.
2. A `> [!abstract] Roadmap of this topic — read it as one story` callout linking the sections into one narrative.
3. Numbered H3 sections in **deck slide order** (figure → prose → definition → derivation → table → worked example).
4. `> [!tip] Exam pointer` callouts at the natural checkpoints and as the last element of a major subsection.
5. `## Formula Summary` at the end of the whole note (one table for the block).
6. A `> [!note] Source images` provenance callout at the very end.

`---` horizontal rules separate the H1 block and `##` topics only — not every section.

---

## 5. What Goes Inside a Section

Order of parts within an H3 section (use what is needed, in this order):

1. **Figure** (Excalidraw or extracted PNG) on its own line at the top if the section is carried by a diagram.
2. **Short prose** — what the thing is and *why* it matters, written as continuous prose, not bullets.
3. **Definition callout** (`[!important]`) — **term** — definition, one per paragraph.
4. **Derivation** — the assumption in a sentence, numbered steps, then display math. Wrap a key derivation in `[!important]` with a title such as `Nature of the hash functions`.
5. **Table** for any comparison, classification or catalogue of values.
6. **Worked example** — reproduce **every** step with its numbers, as a table plus the arithmetic that produced each row (block-access counts, bucket splits, tree traces). Show the intermediate arithmetic before the result.
7. **H4 enrichment** — the *why* behind a convention, a pitfall, a complexity remark.
8. **Callout** — insight (`[!note]`), trap (`[!warning]`) or relation (`[!tip]`) where the reader needs it.

Style of prose:

- **Key terms in bold on first use**, then plain.
- *Italics* for the operative word of a definition and for emphasis.
- Concrete numbers over abstraction: this course's marks sit on traces and block counts.
- Keep the lecturer's conventions **exactly** (trailing-bit suffix in extendible hashing, $C = rM$, the deck's split-pointer labels, the deck's reported block-access counts) and state each once, explicitly, in a callout.

---

## 6. Callout Taxonomy (fixed meanings)

| Callout | Reserved for | Example header |
| --- | --- | --- |
| `[!info]` | Orientation — how the parts of a block fit together (once per H1) | `> [!info] How the block is organised` |
| `[!important]` | Definitions, algorithm statements, key derivations, decisive rules | `> [!important] The decisive rule` |
| `[!warning]` | Traps, convention errors, misconceptions, "do not do this" | `> [!warning] Replicate vs move` |
| `[!note]` | The *why* — an insight, a mechanism, a book connection | `> [!note] Why one entry per block is enough` |
| `[!tip]` | Relations worth remembering and the per-topic exam pointers | `> [!tip] Exam pointer — extendible hashing` |
| `[!abstract]` | The one roadmap callout at the top of each H2 topic | `> [!abstract] Roadmap of this topic` |
| plain `>` quote | A quoted problem statement from the deck | `> *Predict the result.*` |

**Strict callout syntax** (breaks rendering if violated):

- The header (`> [!type] Title`) must be the **first non-empty line** of the block — never preceded by a bare `>`.
- Every line inside the callout starts with `>`; blank lines inside are a single `>`.
- Titles are short, sentence case, no trailing punctuation.
- A wikilink with a display pipe inside a callout **table** must escape the pipe: `[[file-management.pdf\|deck]]`. Outside a table, use a normal `|`.

---

## 7. Worked Traces, Splits and Block-Count Examples

This is the part that makes DBMS notes exam-ready.

### 7.1 Which items get a full trace

Every one of the following is reproduced step by step, never summarized:

- **File layout numbers** — blocking factor, index entry size, number of index blocks.
- **Block-access comparisons** — with index vs without, single-level vs multilevel.
- **Extendible hashing** — every insertion from the deck's example (45, 22, 12, 11, 15, 10) with *when* the directory doubles and *when* it does not; deletion's merge and halve rules.
- **Linear hashing** — every insertion (12, 11, 14, 13, 9, 10, 18) with the active hash functions and the split pointer.
- **$B^+$ order calculation** — the inequalities solved to $m \le 37$, $m_{leaf} \le 33$.
- **$B^+$ insertion and deletion** — the deck's whole sequence, including replicated vs moved keys, sibling redistribution and the level drop.

### 7.2 Shape of a trace

1. A `### N.k <Name> — worked example` section (or a subsection of the algorithm section).
2. A one-line **setup** listing every given number with its symbol.
3. A **table** with one row per step/pixel/pass; short column headers ($i$, value, effect, result).
4. The **arithmetic** that produced each row, shown in display math when it is a formula.
5. A `[!note]` or `[!warning]` naming the one trap the deck flags.

> [!note] No interactive widgets by default
> The CG notes ship JS-Engine widgets because their decks are algorithms with a natural animation. The DBMS decks do not: their "traces" are bucket splits and tree rebalances, which are taught as **tables plus Excalidraw before/after diagrams**. Add a widget only if a future deck explicitly calls for one; if added, follow [[CG_context]] §7's contract (single `js-engine` block, Play/Pause/Next Step/Reset, narration line, theme variables with fallbacks, no external dependency).

---

## 8. Figures, Embeds & Naming

### 8.1 Two kinds of figure

| Kind | Where it lives | Naming | Embed |
| --- | --- | --- | --- |
| **Extracted figure** — a diagram or annotated drawing lifted from a deck | `DBMS/images/` | `DBMS - Descriptive Title (deck pN).png` | with a width `440`–`520` |
| **Reconstructed schematic** — redrawn as Excalidraw | vault-root `Excalidraw/` | `DBMS - Descriptive Title.excalidraw.md` | no width parameter |

Rules: **anything schematic is an Excalidraw drawing** (not Mermaid, not ASCII art in a code block); **anything already drawn in a deck is extracted as a page render**, not redrawn. Equations are never images — they are LaTeX. Use **Mermaid only if the user explicitly asks for it**.

Create every drawing with the Copilot Excalidraw tool (never hand-write the `.excalidraw.md` file — a hand-written file garbles labels and detaches arrows), then render it once to confirm it exists. Give each shape a local id and put text **inside** shapes via `label`, not in a free text element stacked on top.

### 8.2 Embed syntax

On its own line, immediately after the paragraph that introduces it, before the caption:

- Excalidraw: `![[DBMS - Bplus Tree Structure.excalidraw]]`
- PNG: `![[DBMS - Primary Index.excalidraw]]` and `![[DBMS - Disk Structure (deck p2).png|470]]`

### 8.3 Captions

Every extracted PNG gets an italic caption opening `*Figure — ` that says what it shows **and** what it demonstrates:

> *Figure — the deck's directory, global depth $d=3$, with local depths marked (deck p. 18).*

Excalidraw reconstructions are self-labelled and need no caption, though a short italic line naming the idea is welcome.

### 8.4 Provenance note

The note ends with:

> [!note] Source images
> All `DBMS - …excalidraw` drawings are original reconstructions … The PNG figures are page renders of the deck … All numbers come from the deck; the book was used for explanation only.

### 8.5 Prefix convention

One prefix for the whole course — `DBMS - ` — because figures are traceable through the caption's deck reference. Add a row here when a new naming family appears.

---

## 9. Mathematics & Notation

- **Inline**: single dollars — $B$, $b = B/r$, $C = rM$, $h_i(x) = x \bmod 2^i M$, $m_{leaf}$, $\lceil \log_2 b_i\rceil$.
- **Display**: `$$ … $$` on its own lines, blank line above and below.
- The one result a section leaves behind is boxed: $$ \boxed{\ \mathrm{BF}_i = B/(V+P)\ } $$
- Sets and functions in italics: $h$, $K_i$, $P_j$, $V_i$. Bit strings in code font: `000`, `110`, `10`.
- Inequalities in display math when they are derived: $mP + (m-1)V \le B$.
- **Never use double backslashes** outside a LaTeX environment.
- In a table, a pipe inside math must be written `\lvert`/`\rvert`, or the cell breaks.
- Percentages and derived counts keep the deck's exact numbers (49 blocks, 484 blocks, $m\le37$, $7$ vs $14$ accesses).

---

## 10. Tables

Tables are the default for classifications and traces:

- One row per **step / insert / pass / case**.
- Columns short — `Insert | Bit string | Effect | State`.
- The header row and `| --- |` separator are always present.
- Prose remarks about a table go **after** it as bullets or a callout, never inside cells.
- **`## Formula Summary`** closes the note: `| Quantity | Expression | Notes / validity |`. The Notes column always states the convention or validity limit.

---

## 11. Typography & Cross-references

- **Em dash** `—` for breaks and definition separators; **en dash** `–` inside names (Cohen–Sutherland is CG, but e.g. Sreenivasa–Kumar style names if they appear); hyphen only inside words.
- Arrows `→` for "leads to", `↔` for correspondences, `≤`, `≥`, `≠` for relations.
- Section cross-references `§1.34`, `§1.35–§1.38` always point at an existing H3 number; renumber every reference when sections move.
- Source citations are real wikilinks to the decks: [[file-management.pdf]], [[algos.pdf]], [[transactions.pdf]], and to the book [[silberschatz_dbms.pdf]].
- Slide numbers may be cited in prose (`deck p. 22`) and in figure captions (`deck p. 18`).

---

## 12. Content Rules

1. **Zero omission.** Every definition, formula, worked number, table, convention and caveat from the deck survives. Worked examples keep every step.
2. **No hallucination, no padding.** Do not add topics the deck does not cover; do not restate a paragraph in other words. Enrichment (H4) stays on the topic and is plainly depth, not new syllabus.
3. **Preserve the lecturer's conventions** — trailing-bit suffix, $C=rM$, split-pointer labels, the deck's block-access counts. These are examinable.
4. **Numbers are sacred.** If a slide's layout is scrambled, reconstruct only what readable neighbours support; never silently change a digit.
5. **Non-destructive edits.** Extend with targeted inline edits; never rewrite a finished block from scratch.
6. **Status tracking.** Tick the topic's checkbox (`- [x]`) on its line in [[Syllabus]] in the *same pass* as writing the topic, and add the section index rows for that topic.

---

## 13. Adding a New Topic — Workflow

1. **Read the syllabus row.** Take the deck's exact topic name and number from [[Syllabus]].
2. **Mine the deck.** `pdftotext -layout` the PDF, walk the slides in order, note repeated annotation slides, the lecturer's own worked example and every convention callout.
3. **Consult the book** on the matching section (Ch. 13–14 or §24.5) for explanation only — record where the book's convention differs from the deck's, and keep the deck's.
4. **Extract figures.** Render the pages whose printed text proves what the picture is into `DBMS/images/` as `DBMS - Title (deck pN).png`; write the caption from that text.
5. **Reconstruct schematics.** Draw the structural set-ups as Excalidraw (`DBMS - Title.excalidraw.md`), then render once to confirm.
6. **Write the H2 topic** with numbered H3 sections in deck order, plus H4 depth and exam pointers.
7. **Close** with the topic's exam pointer, then add its rows to `## Formula Summary`; finish the note with the `[!note] Source images` callout.
8. **Update** the checkbox line, the figure/section-index rows and the open-gaps callout in [[Syllabus]].

### Checklist before finishing

- [ ] H2 number matches the deck's syllabus position; H3 numbers run continuously.
- [ ] Every worked example has setup, a step-by-step table, the arithmetic and the trap.
- [ ] Every schematic is an Excalidraw drawing; every deck figure is a PNG with a width and italic caption.
- [ ] Every callout header is the first line of its block; every inner line is `>`-prefixed.
- [ ] Every formula appears in the Formula Summary with its convention note.
- [ ] Every `§` reference resolves; every deck has a wikilink; the book is cited as explanation only.
- [ ] Nothing from the source deck was dropped.
