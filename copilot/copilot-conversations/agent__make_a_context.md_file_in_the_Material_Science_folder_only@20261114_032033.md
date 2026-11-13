---
epoch: 1794606633544
mode: agent
backendId: opencode
sessionId: "ses_e291cd7abffexW6gU7FohJzRAS"
tags:
  - copilot-conversation
agentLabel: "Material Science notes format context file"
usage: '{"usedTokens":55943,"contextWindow":200000,"updatedAt":1794606752202}'
---

**user**: make a context.md file in the Material Science folder only noting down the format in which the notes are formed. so I dont have to specfy details of making notes through pdfs again I just have to refer to that file.
[Timestamp: 2026/11/14 03:20:33]

**ai**: I have the full picture of how `notes.md` is built. Now writing the rulebook.Created [[context]] in the `Material Science/` folder — a self-contained format rulebook for `notes.md`, so you never have to re-specify the layout again. Nothing in `notes.md` was touched.

**What it records (all reverse-engineered from the existing note):**

- **Role & sources** — syllabus.md as the authority for topic order, the lecture PDFs, [[MO NOTES (1).pdf]] with page ranges, and the Raghavan/Callister textbooks.
- **Document skeleton** — YAML frontmatter, and the fixed heading hierarchy: H1 = course block, H2 = one syllabus topic (numbered to match syllabus position), H3 = numbered lecture section (`2.4`), H4 = unnumbered "added depth" subsection. One file, not one per topic.
- **Section anatomy** — Excalidraw figure → prose → `[!important]` definitions → numbered derivation → table → extracted figure with `*Figure — …*` caption → H4 depth → closing exam pointer.
- **Callout taxonomy** — the exact reserved meaning of `[!info]`, `[!important]`, `[!warning]`, `[!note]`, `[!tip]`, `[!question]` and plain blockquotes, plus the strict "header must be the first line / every inner line `>`-prefixed" rule.
- **Figures & naming** — Excalidraw in `Excalidraw/` with `MP - ` prefix (no width param) vs. PDF extracts in `attachments/` with `MP1/MP2/MP3 - ` prefix (width `340`–`520`), plus a prefix table for the remaining topics (SD, COMP, EP1/EP2, MAG, DIE) to extend as you go.
- **Math** — inline `$…$`, display `$$…$$`, `\boxed{}` for the one result a section must leave behind, upright `\text{}` units, no double backslashes outside matrices.
- **Tables** — including the per-block `## Formula Summary` (Quantity | Expression | Notes, Notes never empty) and the closing `[!note] Source images` provenance callout.
- **Content rules** — zero omission, no hallucination/padding, non-destructive inline edits, status tracked in the Syllabus Map.
- **Workflow + checklist** — the 8-step procedure for adding a new topic (including integrating pasted NotebookLM text verbatim under the correct header) and a pre-finish checklist.
- **Minimal skeleton** at the end to copy.

One detail: the two embed-syntax examples in §7.2 are written with a leading backslash (`\![[…]]`) so the reference file itself doesn't render live embeds — the file notes this, and you write them normally in `notes.md`.
[Timestamp: 2026/11/14 03:20:33]