---
epoch: 1795124945040
mode: agent
backendId: claude
sessionId: "98925b6d-7583-440b-bb8c-fd2fc7cf7a90"
agentLabel: "i have attached a prev_yr2 paper in {DBMS/sources} folder. m…"
tags:
  - copilot-conversation
usage: '{"usedTokens":100861,"contextWindow":1000000,"inputTokens":2,"outputTokens":779,"cacheReadTokens":99486,"cacheWriteTokens":594,"updatedAt":1795125279011}'
---

**user**: i have attached a prev_yr2 paper in {DBMS/sources} folder.
make a separate file for it and solve it in high detail like [[pyp]] was solved.
[Timestamp: 2026/11/20 03:19:05]

**ai**: I have the format of `pyp.md` and the questions from the image. I'm writing the solved paper now.I created `DBMS/pyp2.md` with all 11 questions solved in the same style as [[pyp]]. I haven't previewed it in Obsidian, so check how the callouts and the ASCII diagrams render.

Each question is an outer `[!question]` card. Where it helps, there's a collapsible theory block, then the worked answer and an exam pointer.

I wrote the answers from the question paper image and my own knowledge. I didn't cross-check them against your lecture PDFs (`algos.pdf`, `file-management.pdf`, `transactions.pdf`).

Notes on a few answers:
- **Q1 (3NF equivalence):** the two definitions are "2NF plus no transitive dependency" and "superkey or prime". I proved both directions with a split on whether the left side is inside a key.
- **Q2 (dependency preserving ⇒ lossless):** the statement is false. The counterexample is $R(A,B,C)$ with $F=\{A\to B\}$ split into $R_1(A,B)$ and $R_2(B,C)$. I included a concrete instance showing the spurious tuples.
- **Q3 (hash set operations):** I covered partitioning, then build and probe for union, intersection and difference. It has a worked example and the cost formulas.
- **Q4 (serializability):** I defined five transactions of three instructions each.
  - $S_1$ is conflict serializable.
  - $S_2$ is not conflict serializable; it has a 2-cycle between $T_4$ and $T_5$.
  - I also added a third schedule, $S_3$, that is view serializable but not conflict serializable.
- **Q8 (minimal cover):** the answer is yes. I gave three counterexamples: an extraneous attribute on the right of an FD, one on the left, and a redundant FD. The first two end up with a relation that isn't in 3NF. There's also a full worked run of the algorithm.
- **Q9 (index block accesses):** I assumed the data file is ordered on the key. I took 5 KB as 5120 bytes, which gives 7, 14 and 3 accesses for parts (a), (b) and (c). Using 5000 bytes gives the same answers, and I noted that.
- **Q5, Q10 and Q11:** I used a fresh example for Q5 (student and qualifications). I also gave Q10 a table of what translates declaratively and what needs triggers. The Q11 proofs use only the three basic Armstrong rules.

The ER diagrams in Q5 are ASCII, not Excalidraw. I can redo them as Excalidraw drawings if you'd like.
[Timestamp: 2026/11/20 03:19:05]