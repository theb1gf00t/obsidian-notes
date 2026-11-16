---
epoch: 1794828704796
mode: agent
backendId: opencode
sessionId: "ses_e1be02538ffenBYD5zxoPAiukE"
tags:
  - copilot-conversation
agentLabel: "Fixing CG notes links and discrepancies"
usage: '{"usedTokens":30333,"contextWindow":200000,"updatedAt":1794829556994}'
---

**user**: go through all the notes for CG and the syllabus and the context files.
fix any discrepencies there might be in links or any other form.
[Timestamp: 2026/11/16 17:01:44]

**ai**: I'll start by exploring the Computer Graphics folder structure to understand what we're working with.Now I have a clear picture. Let me start fixing. First, the two unembedded figures:Now the pseudo-code and the deck-style iterative bullet that contradicted it:Now the connectivity table, whose "leaks" cell contradicts its own paragraph:Now the syllabus Figures table — it lists only the Excalidraw reconstructions, not the seven page renders:Audit complete. Everything now resolves, and every figure the syllabus lists is embedded exactly once in the note.

## What was actually wrong, and what I changed

**`Computer Graphics/notes/CG_Endsem_Notes.md`** (the substantive fixes)

| # | Location | Problem | Fix |
|---|---|---|---|
| 1 | §1.3 | `CG - Camera Frame and View Volume.excalidraw` was listed in the syllabus but embedded nowhere — an orphan drawing | Embedded at the head of §1.3, where the six planes are introduced |
| 2 | §3.2 → §3.9 | `CG - Concave Subject Split.png` was sitting in §3.2 ("why polygon clipping is not line clipping"), which is about the *four cases*, while the picture illustrates the concave-split limitation discussed in §3.9 | Moved to §3.9 with `\|460` and an italic caption naming the doubled edge |
| 3 | §5.4 → §5.7 | `CG - BSP Tree Traversal.excalidraw` was in §5.4 (the plane function), but its content is the eye-dependent traversal rule — syllabus says "§5.7" | Moved to §5.7, right after the OUT/IN table |
| 4 | §5.8 | `CG - BSP Traversal Order.png` existed in `images/` and in the syllabus table but was embedded in **no** note | Embedded after the draw-order formula with `\|480` and a caption |
| 5 | §4.6 | Edge-pixel depth was stated as $z-A/C-B/(mC)$ with a bogus "equivalently" clause — wrong signs, and it contradicted the algorithm box | Now $z' = z + B/C + A/(mC)$, plus a numeric check ($m=2 \Rightarrow z'=4.0$, direct evaluation agrees) |
| 6 | §4.7 | Pseudo-code step 9 dropped the $x$-shift term the preceding section had just derived | Step 9 now reads `z_left = z_left + B/C - (A/C)(x'_left - x_left)` |
| 7 | §4.8 | The z-buffer widget initialised `DB` to `1` while the scene's depths are ~2–5.5 — nothing was ever painted, and the narration reported a stale value | `const FAR = 99`, `∞` display, `step()` records `before`/`win`, narration reads those; a tip sentence reconciles `∞` with the algorithm box's "1 (far)" |
| 8 | §6.10 | The connectivity table put "leaks" on the *4-connected fill / 4-connected boundary* cell, contradicting its own paragraph two lines above | "leaks" moved to 8-connected fill with 8-connected boundary |
| 9 | §5.5 | Subscript typo `f_q(v)` in pseudo-code (the plane function is $f_p$) | `f_p(v)` |
| 10 | Source-images callout | Claimed provenance from "depth-buffer frames" that do not exist in `images/` | Reworded to the actual PNG/Excalidraw provenance |

**`CG_Syllabus.md`**
- Intro + tracker bullet now say plainly that `CG_Endsem_Notes` is the note written against this syllabus and that each "Notes" link jumps to the file holding that block (previously it implied both blocks live in that one file).
- The single "Figures" table mixed 10 Excalidraw reconstructions with 7 PNG page renders under one heading; split into **Excalidraw** and **Page renders** tables, with the "(every one is embedded with a width and an italic caption)" qualifier attached only to the PNG table where it's true.

**`CG_context.md`**
- §4.3 said widgets are "the interactive widget section" without naming it; now names the `### N.k Interactive dry run` convention and says it follows the algorithm box *and its trace*.
- §12.6 and §13.8 referred to a "Syllabus Map" and a `✅ noted` marker that don't exist in the tracker; both now describe the actual workflow — tick `- [x]` on the topic's line, and update the Dataview counter / widget / figure / section-index rows in the same pass.

## Verified clean (no change needed)

- **Links:** 0 unresolved wikilinks and 0 unresolved heading anchors across all four notes (the only three regex hits are placeholders inside code templates — `[[<deck>.pdf]]`, `[[CG - <Schematic>.excalidraw]]` — and `[[3, 3]]`, which is a JS array inside a fence). All 20 deck PDFs resolve.
- **Section index:** every `[[CG_Endsem_Notes#…]]` target matches a real H2/H3 verbatim, and the "(N sections)" counters (7, 11, 17, 9, 11, 16, 13, 13) match the actual heading counts.
- **Widgets:** all 8 IDs (`w-cs`, `w-sh`, `w-zb`, `w-bsp`, `w-sl`, `w-ff`, `w-gs`, `w-tween`) match the syllabus table one-for-one, sit in the right `### N.k Interactive dry run` sections, and all 8 extracted scripts pass `node --check`.
- **Figures:** 10/10 Excalidraw + 7/7 PNG embedded exactly once each; no orphans, no duplicates. Re-ran the z-buffer simulation: 49 steps, 34 writes, 15 rejects — it paints.

## Deliberately left alone

- `CG_Midsem_notes.md` is 0 bytes — that's consistent with the syllabus ("not yet written") and the Open-gaps callout, not a bug.
- §8.4's beat sheet (frames 9–12 anticipation, 13–20 jump) vs §8.6's key poses (K3 push-off at frame 9, K4 apex at 13) use different frame vocabularies. That looks like a deck-level quirk, and "numbers are sacred" — changing digits to force agreement would be exactly the wrong fix. Flagging it as a known ambiguity rather than silently reconciling it.

Note: a scheduled *vault backup* commit swept these edits up at 17:14, so the working tree shows clean — the changes are in `d97f8b2`.
[Timestamp: 2026/11/16 17:01:44]