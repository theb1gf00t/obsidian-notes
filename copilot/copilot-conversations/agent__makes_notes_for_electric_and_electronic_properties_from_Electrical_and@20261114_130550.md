---
epoch: 1794641750150
mode: agent
backendId: opencode
sessionId: "ses_e27043bcaffebB93Ps7y5FuJWJ"
tags:
  - copilot-conversation
agentLabel: "Notes: electrical, dielectric & optical properties"
usage: '{"usedTokens":106238,"contextWindow":200000,"updatedAt":1794642457205}'
---

**user**: makes notes for electric and electronic properties from [[Electrical and Electronic Properties - Part 2_Odd_2026-27.pdf]] [[Electrical and Electronic Properties - Part 1_Odd_2026-27.pdf]] and for Dielectric materials and polarization optical properties. from [[MP - Yoffee Diagram DBTT.excalidraw]] according to [[context]] .
[Timestamp: 2026/11/14 13:05:50]

**ai**: I'll start by reading the context file and the existing notes structure, then the PDFs.Now I'll write the electrical block into [[Material Science/notes.md]], inserting it in syllabus order before the magnetic block.Now the dielectric and optical block, appended after the magnetic block:The note is complete. I'll add one original synthesis flowchart (classification by band structure), since every *existing* figure was extracted rather than redrawn:Done. Everything was appended to [[notes]] in syllabus order, following `Material Science/context.md` (the Phase Diagrams `context.md` is a different rulebook and does not apply here).

**What was added**

| Block | Location | Content |
| --- | --- | --- |
| `# Electrical & Electronic Properties` | §6, inserted before the magnetic block | 12 sections: resistivity spectrum → free electron model → de Broglie/parabola → box quantisation → Fermi–Dirac → drift & conductivity → superconductors → Meissner → type I/II + pinning → failure of the model → Bragg/standing waves → 3-D forbidden gap |
| | §7 | 14 sections: overlapping bands → Brillouin zones → valence/conduction bands → metals → column-IV gap sequence → semiconductor/insulator divide → intrinsic carriers → mobility → donors/n-type → acceptors/p-type → three regions of $\log\sigma$ vs $1/T$ → doping practice → p–n equilibrium → forward/reverse bias |
| `# Dielectric Materials, Polarization & Optical Properties` | §9, after the magnetic block | 12 sections: dielectric definition → capacitance → the four polarization mechanisms → speed ranking → ferroelectrics → BaTiO₃/Cutie temperature → metals' optics → refraction → reflection/absorption → the $1.8$–$3.1\ \text{eV}$ colour window |

Each block closes with an exam pointer, a `## Formula Summary` table (every formula with its validity note) and a `[!note] Source images` provenance callout, per the schema.

**Figures** — 28 captioned figures extracted straight from the PDFs into `attachments/`: 13 with `EP1 - ` (Figs. 1–12 plus the resistivity-range chart), 9 with `EP2 - ` (Figs. 13–19 plus the forward/reverse-bias diagrams), 6 with `DIE - ` (Figs. 1–6).

**One original reconstruction** — `Excalidraw/EP - Band structure classification.excalidraw.md`, a decision flowchart (half-filled → metal; full → overlap test; no overlap → gap size) embedded in §7.6, since no such summary diagram exists in the slides.

**Two deliberate flags**
- §6.9 carries a `[!warning]` that the slide's "M = −H up to $T_c$" is a typo for "up to $H_c$" — the $M$–$H$ curve exists only *below* $T_c$.
- The Shockley diode equation in §7.14 is marked *added depth beyond the slides*, because the slides only argue the barrier qualitatively.

**Housekeeping** — Syllabus Map rows 6, 7 and 9 now read ✅, and the compilation line at the top cites all seven post-midsem PDFs.

One note on your request: the dielectric material came from [[Dielectric materials_Polarization_Optical properties_Odd_2026-27.pdf]], not from [[MP - Yoffee Diagram DBTT.excalidraw]] (that drawing is the mechanical-properties Yoffee diagram and has no dielectric content) — I assumed the PDF was intended. Also, [[MO NOTES (1).pdf]] is a scanned handwriting PDF with no text layer, so it is cited at block level rather than by page range.
[Timestamp: 2026/11/14 13:05:50]