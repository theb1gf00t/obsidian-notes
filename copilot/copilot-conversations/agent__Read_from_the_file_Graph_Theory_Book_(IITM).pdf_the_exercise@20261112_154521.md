---
epoch: 1794478521289
mode: agent
backendId: opencode
sessionId: "ses_e30c0ce64ffeWd7H15Nnox7gJ3"
tags:
  - copilot-conversation
agentLabel: "Graph Theory Module 11 exercises and solutions"
usage: '{"usedTokens":83812,"contextWindow":200000,"updatedAt":1794479637136}'
---

**user**: Read from the file [[Graph Theory Book (IITM).pdf]]  the exercise questions at the end of Module 11. 
and make a section of Modul1 11 in [[Question Practice]] .
Solve those questions in detail according to .
do not interfere with questions from the assignment or chapter 7 to 10 - they are already solved and well formatted.
add a chapter 11 section along with its questions and then solve those questions in detail.
make sure the solution is detailed and understandable.
[Timestamp: 2026/11/12 15:45:21]

**ai**: I'll start by examining the current state of the Question Practice file and locating Module 11 in the PDF.Let me verify a few enumerations computationally so the solutions are exact.I'll continue from where I left off. Let me first verify the file state and run the remaining computations.Now let me generate the figures with graphviz.Now I'll write the Chapter 11 section. Starting with the heading and Q1–Q4:I'll append the final Q22–Q28 batch. Let me first check the current tail of the Chapter 11 section.Now I'll append Q22–Q28 in one edit anchored on the Q21 tail.I need to repair an over-broad replacement. Let me inspect the exact structure first.Q23(a) as written isn't actually a tournament (only 7 of 10 pairs joined). Let me fix the construction, its figure, and two wording issues in Q28.Now the Q23 text fix:Chapter 11 is now complete — Q1 through Q28 — in [[Question Practice]].

**What I appended (Q22–Q28)**

| Q | Topic | Approach taken |
|---|---|---|
| Q22 | Regular tournament on 5 vertices | Carousel $i\to i+1,i+2$; double count $nd=\binom n2$ ⟹ $d=\frac{n-1}{2}$, so $n$ must be odd |
| Q23 | Unilateral vs. strong | (a) triangle + $x,y$ with a one-way cut $A\to\{y\}$; (b) carousel with the Hamilton cycle $0\to1\to2\to3\to4\to0$ |
| Q24 | One-way cuts | Reachable-set argument both ways, plus the condensation picture |
| Q25 | Transitive $\iff$ out-degrees $0..n-1$ | Lemma (sink exists) + induction one way; $\binom i2$ double count the other |
| Q26 | Transitive $\iff$ acyclic | Shortest-cycle argument, then the 3-cycle obstruction to $w\to u$ |
| Q27 | Score identities | (b) first; (a) shown trivial as printed + the real $k$-subset (Landau) form with $C(k,2)+\#(\text{arcs leaving }S)$; (c) expansion using $\mathrm{indeg}=n-1-s$ |
| Q28 | Winners/kings | Landau + "every beaten vertex is beaten by a king" lemmas; all-winner constructions: $n=1$, triangle, carousel (odd), carousel $+z$ (even $\ge6$), with $n=2,4$ impossibilities |

**Corrections made while finalising**

- **Q23(a) was not a tournament** as first drafted (7 of 10 pairs joined — a $y$ left unjoined to $a,b,c$). It now uses the full arc set $a\to b\to c\to a$, $a,b,c\to x$, $a,b,c\to y$, $x\to y$ (10 arcs), and I regenerated the figure accordingly.
- **Q28(a)** had a garbled role-swap bullet; rewritten cleanly (…so $c\to d$, contradicting $d\to c$), and the vague "chain argument" aside replaced by a short note on why Lemma 2 is the crux.
- **Q28(b) $n=4$** case analysis tightened (average out-degree $\Rightarrow$ a vertex of out-degree 1 $\Rightarrow$ some other vertex reachable only to $v,w$).
- **Q19** still contained a drafting artifact ("Wait — more directly… symmetric reasoning gives indeg…"); replaced by the clean "count arcs with tail in $A$" argument that the rest of the paragraph already used.

**Changed files**

- `Graph Theory/Question Practice.md` — Q22–Q28 added after Q21; Q19 and Q23 text repaired.
- `Graph Theory/ch11_unilateral_tournament_5v.png` — redrawn with all 10 arcs (1062×462).

Note: I can't view images in this session, so the redrawn figure was checked only by construction/dimensions; if the $a,b,c\to y$ arcs look cluttered, say the word and I'll re-space it.
[Timestamp: 2026/11/12 15:45:21]