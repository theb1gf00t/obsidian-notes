---
title: DBMS Syllabus Tracker
aliases:
  - DBMS Syllabus
course: DBMS
tags:
  - dbms
  - syllabus
---

# DBMS — Syllabus

This file is the **authority** for the topic list, the topic order and the post-midsem / end-semester split. The note [[DBMS_Notes]] is written against it topic by topic; every topic below names its lecture deck and jumps straight to the matching heading in the note. The authoritative formatting rules live in [[context]].

| Block | Topics | Note file |
| --- | --- | --- |
| Pre-midsem | 1, 2, 3, 3.1, 4, 6 | *(not yet written)* |
| Post-midsem / end-sem | 1–3 | [[DBMS_Notes]] |

> [!warning] Scope of the examination
> This block covers all three post-midsem topics — file management, query algorithms and transactions. **All three topics are written**; topic 1's checkbox is still open for revision.

> [!warning] Pre-midsem topic numbering has a gap
> The six pre-midsem decks are numbered **1, 2, 3, 3.1, 4, 6** by the lecturer — there is no deck numbered **5** among the files provided in `pdfs/`. The numbering below keeps the lecturer's own numbers exactly as given (per [[context]] §2: "the topic number equals the deck's position"); it is **not** a typo to be renumbered 1–6. If a topic 5 deck surfaces later, insert it in place without renumbering the others.

> [!info] How to use this tracker
> - Tick the box on a topic line when the topic is **revised and recallable**, not merely read once. Untick it if a revision pass exposes a hole.
> - **PDF** opens the lecture deck; **Notes** jumps to the topic's heading in [[DBMS_Notes]]. The section index at the bottom gives a one-click jump to every written section.
> - The counter below is live (Dataview) — it reads the checkboxes in this file, so nothing needs counting by hand.
> - `§` numbers are the H2/H3 section numbers used inside [[DBMS_Notes]] (e.g. §1.24 is a real heading there).

## Progress

```dataview
TABLE WITHOUT ID
  string(length(filter(file.tasks, (t) => t.completed))) + " / " + string(length(file.tasks)) AS "Topics ticked",
  string(round(100 * length(filter(file.tasks, (t) => t.completed)) / length(file.tasks))) + " %" AS "Coverage",
  length(filter(file.tasks, (t) => !t.completed)) AS "Still open"
WHERE file.path = this.file.path
```

---

## Pre-Midsem — 6 topics

- [ ] **1 · Introduction** — [[1_Introduction.pdf|PDF]] · *(Notes not yet written)* (24 slides)
- [ ] **2 · Entity-Relationship (E/R) Model** — [[2_Entity_Relationship_Model.pdf|PDF]] · *(Notes not yet written)* (36 slides)
- [ ] **3 · Relational Model** — [[3_Relational_Model.pdf|PDF]] · *(Notes not yet written)* (62 slides)
- [ ] **3.1 · Tuple Relational Calculus (TRC)** — [[3.1_Tuple_Relational_Calculus.pdf|PDF]] · *(Notes not yet written)* (14 slides)
- [ ] **4 · The SQL Standard** — [[4_The_SQL_Standard.pdf|PDF]] · *(Notes not yet written)* (73 slides)
- [ ] **6 · Database Design and Normal Forms (Relational Schema Design)** — [[6_Relational_Schema_Design.pdf|PDF]] · *(Notes not yet written)* (52 slides)

> [!note] No note file yet
> None of the pre-midsem topics have a compiled study note yet — only the syllabus row exists. When a pre-midsem note file is created (one file for the whole block, per [[context]] §3), link its heading here in place of each *(Notes not yet written)* placeholder and add a `§` section index for it below, mirroring the post-midsem section below.

---

## Post-Midsem — 3 topics

- [x] **1 · File Organization and Indexing** — [[file-management.pdf|PDF]] · [[DBMS_Notes#1. File Organization and Indexing|Notes → §1]] (39 sections) ✅ 2026-11-19
- [x] **2 · Query / Join Algorithms (algos)** — [[algos.pdf|PDF]] · [[DBMS_Notes#2. Query / Join Algorithms (algos)|Notes → §2]] (22 sections)
- [x] **3 · Transactions** — [[transactions.pdf|PDF]] · [[DBMS_Notes#3. Transactions|Notes → §3]] (16 sections)

> [!tip] Exam pointer
> Topic 1's marks sit on the **numbers and traces**, not the definitions: block-access arithmetic and $b = B/r$, the 9500-record primary index giving 49 blocks and $\lceil\log_2 49\rceil + 1 = 7$ accesses, the extendible-hashing directory doubling on a full local depth, the linear-hashing split deciding between $k$ and $k + M'$ from the parity of $r$, and the $B^+$ tree order $m$ / $m_{\text{leaf}}$ with the leaf-key-replicated-versus-internal-key-moved split rule. Topic 2's marks sit on **block-access cost formulas**: selectivity (450/8000 = 0.056), the external-sort cost $2n+2n\lceil\log_d r\rceil$, nested loop join (19040 with $R$ outer vs 16920 with $S$ outer), single loop join with the join selection factor, partition hash join $3(\lvert R\rvert+\lvert S\rvert)+\lvert result\rvert$, and the five-step rewrite of the professor–teaching–enrollment query. Topic 3's marks sit on **applying the rules to schedules**: ACID via the fund-transfer example, state transitions (including restart/kill from Aborted), conflict identification and precedence-graph acyclicity, recoverable vs cascadeless commit/read ordering, and the SQL-92 isolation levels with the snapshot-isolation warning.

---

## Section index of the notes

Every written section of [[DBMS_Notes]], grouped by topic, so a topic can be opened at the exact sub-heading.

### §1 · File Organization and Indexing

| § | Section |
| --- | --- |
| 1.1 | [[DBMS_Notes#1.1 Disk space management — who owns the disk?\|Disk space management — who owns the disk?]] |
| 1.2 | [[DBMS_Notes#1.2 Structure of disks and the cost of a block access\|Structure of disks and the cost of a block access]] |
| 1.3 | [[DBMS_Notes#1.3 Data records and files — fixed length vs variable length\|Data records and files — fixed length vs variable length]] |
| 1.4 | [[DBMS_Notes#1.4 Packing records into blocks — blocking factor and spanned records\|Packing records into blocks — blocking factor and spanned records]] |
| 1.5 | [[DBMS_Notes#1.5 Mapping file blocks onto disk blocks\|Mapping file blocks onto disk blocks]] |
| 1.6 | [[DBMS_Notes#1.6 Operations on files and the role of file organization\|Operations on files and the role of file organization]] |
| 1.7 | [[DBMS_Notes#1.7 The three primary file organizations — an overview\|The three primary file organizations — an overview]] |
| 1.8 | [[DBMS_Notes#1.8 Heap files\|Heap files]] |
| 1.9 | [[DBMS_Notes#1.9 Sorted (sequential) files\|Sorted (sequential) files]] |
| 1.10 | [[DBMS_Notes#1.10 Hashed files — buckets and overflow chains\|Hashed files — buckets and overflow chains]] |
| 1.11 | [[DBMS_Notes#1.11 Performance of static hashing\|Performance of static hashing]] |
| 1.12 | [[DBMS_Notes#1.12 Dynamic file organization — why hashing must grow\|Dynamic file organization — why hashing must grow]] |
| 1.13 | [[DBMS_Notes#1.13 Extendible hashing — structure\|Extendible hashing — structure]] |
| 1.14 | [[DBMS_Notes#1.14 Insertion in extendible hashing\|Insertion in extendible hashing]] |
| 1.15 | [[DBMS_Notes#1.15 Deletion in extendible hashing\|Deletion in extendible hashing]] |
| 1.16 | [[DBMS_Notes#1.16 Extendible hashing — the full worked example\|Extendible hashing — the full worked example]] |
| 1.17 | [[DBMS_Notes#1.17 Linear hashing — structure and the hash-function family\|Linear hashing — structure and the hash-function family]] |
| 1.18 | [[DBMS_Notes#1.18 Insertion in linear hashing\|Insertion in linear hashing]] |
| 1.19 | [[DBMS_Notes#1.19 Nature of the hash functions\|Nature of the hash functions]] |
| 1.20 | [[DBMS_Notes#1.20 Linear hashing — the full worked example\|Linear hashing — the full worked example]] |
| 1.21 | [[DBMS_Notes#1.21 Index structures — the three kinds\|Index structures — the three kinds]] |
| 1.22 | [[DBMS_Notes#1.22 Primary index — structure\|Primary index — structure]] |
| 1.23 | [[DBMS_Notes#1.23 Record access using the primary index\|Record access using the primary index]] |
| 1.24 | [[DBMS_Notes#1.24 Primary index — worked example (9,500 blocks)\|Primary index — worked example (9,500 blocks)]] |
| 1.25 | [[DBMS_Notes#1.25 Making the index multilevel\|Making the index multilevel]] |
| 1.26 | [[DBMS_Notes#1.26 Range search, insertion and deletion on the primary index\|Range search, insertion and deletion on the primary index]] |
| 1.27 | [[DBMS_Notes#1.27 Clustering index\|Clustering index]] |
| 1.28 | [[DBMS_Notes#1.28 Secondary index — the two cases\|Secondary index — the two cases]] |
| 1.29 | [[DBMS_Notes#1.29 Secondary index on a key — worked example\|Secondary index on a key — worked example]] |
| 1.30 | [[DBMS_Notes#1.30 Multilevel secondary index — worked example\|Multilevel secondary index — worked example]] |
| 1.31 | [[DBMS_Notes#1.31 ISAM files\|ISAM files]] |
| 1.32 | [[DBMS_Notes#1.32 $B^+$ trees — the idea and the properties\|$B^+$ trees — the idea and the properties]] |
| 1.33 | [[DBMS_Notes#1.33 Order of internal and leaf nodes\|Order of internal and leaf nodes]] |
| 1.34 | [[DBMS_Notes#1.34 Order calculation — worked example\|Order calculation — worked example]] |
| 1.35 | [[DBMS_Notes#1.35 Insertion into $B^+$ trees\|Insertion into $B^+$ trees]] |
| 1.36 | [[DBMS_Notes#1.36 $B^+$ tree insertion — worked example\|$B^+$ tree insertion — worked example]] |
| 1.37 | [[DBMS_Notes#1.37 Deletion in $B^+$ trees\|Deletion in $B^+$ trees]] |
| 1.38 | [[DBMS_Notes#1.38 $B^+$ tree deletion — worked example\|$B^+$ tree deletion — worked example]] |
| 1.39 | [[DBMS_Notes#1.39 Advantages and disadvantages of $B^+$ trees\|Advantages and disadvantages of $B^+$ trees]] |

### §2 · Query / Join Algorithms (algos)

| § | Section |
| --- | --- |
| 2.1 | [[DBMS_Notes#2.1 Relational query evaluation — the operators\|Relational query evaluation — the operators]] |
| 2.2 | [[DBMS_Notes#2.2 Selection with equality conditions\|Selection with equality conditions]] |
| 2.3 | [[DBMS_Notes#2.3 Predicate selectivity\|Predicate selectivity]] |
| 2.4 | [[DBMS_Notes#2.4 Selectivity estimation\|Selectivity estimation]] |
| 2.5 | [[DBMS_Notes#2.5 Project operation\|Project operation]] |
| 2.6 | [[DBMS_Notes#2.6 External sorting — the idea\|External sorting — the idea]] |
| 2.7 | [[DBMS_Notes#2.7 Algorithm — sort phase\|Algorithm — sort phase]] |
| 2.8 | [[DBMS_Notes#2.8 Algorithm — merge phase\|Algorithm — merge phase]] |
| 2.9 | [[DBMS_Notes#2.9 Join processing\|Join processing]] |
| 2.10 | [[DBMS_Notes#2.10 Nested loop join (block nested loop join)\|Nested loop join]] |
| 2.11 | [[DBMS_Notes#2.11 Nested loop join — time taken\|Nested loop join — time taken]] |
| 2.12 | [[DBMS_Notes#2.12 Nested loop join — worked example\|Nested loop join — worked example]] |
| 2.13 | [[DBMS_Notes#2.13 Single loop join (index loop join)\|Single loop join]] |
| 2.14 | [[DBMS_Notes#2.14 Join selection factor\|Join selection factor]] |
| 2.15 | [[DBMS_Notes#2.15 Hash join\|Hash join]] |
| 2.16 | [[DBMS_Notes#2.16 Partition hash join\|Partition hash join]] |
| 2.17 | [[DBMS_Notes#2.17 Sort-merge join\|Sort-merge join]] |
| 2.18 | [[DBMS_Notes#2.18 Set operations\|Set operations]] |
| 2.19 | [[DBMS_Notes#2.19 Query optimization — overview\|Query optimization — overview]] |
| 2.20 | [[DBMS_Notes#2.20 Heuristic optimization\|Heuristic optimization]] |
| 2.21 | [[DBMS_Notes#2.21 Cost-based optimization\|Cost-based optimization]] |
| 2.22 | [[DBMS_Notes#2.22 Query optimization — worked example\|Query optimization — worked example]] |

### §3 · Transactions

| § | Section |
| --- | --- |
| 3.1 | [[DBMS_Notes#3.1 Transaction concept and the fund-transfer example\|Transaction concept and the fund-transfer example]] |
| 3.2 | [[DBMS_Notes#3.2 The ACID properties\|The ACID properties]] |
| 3.3 | [[DBMS_Notes#3.3 Transaction states\|Transaction states]] |
| 3.4 | [[DBMS_Notes#3.4 Concurrent executions\|Concurrent executions]] |
| 3.5 | [[DBMS_Notes#3.5 Schedules and the serial/concurrent examples\|Schedules and the serial/concurrent examples]] |
| 3.6 | [[DBMS_Notes#3.6 Serializability\|Serializability]] |
| 3.7 | [[DBMS_Notes#3.7 Conflicting instructions and conflict equivalence\|Conflicting instructions and conflict equivalence]] |
| 3.8 | [[DBMS_Notes#3.8 Conflict serializability — examples\|Conflict serializability — examples]] |
| 3.9 | [[DBMS_Notes#3.9 Testing for conflict serializability — the precedence graph\|Testing for conflict serializability — the precedence graph]] |
| 3.10 | [[DBMS_Notes#3.10 Recoverable schedules\|Recoverable schedules]] |
| 3.11 | [[DBMS_Notes#3.11 Cascading rollbacks and cascadeless schedules\|Cascading rollbacks and cascadeless schedules]] |
| 3.12 | [[DBMS_Notes#3.12 Concurrency control\|Concurrency control]] |
| 3.13 | [[DBMS_Notes#3.13 Weak levels of consistency and SQL isolation levels\|Weak levels of consistency and SQL isolation levels]] |
| 3.14 | [[DBMS_Notes#3.14 Transaction definition in SQL\|Transaction definition in SQL]] |
| 3.15 | [[DBMS_Notes#3.15 View serializability\|View serializability]] |
| 3.16 | [[DBMS_Notes#3.16 More complex notions of serializability\|More complex notions of serializability]] |

---

## Figures

The topic's diagrams are either page renders lifted from the deck (`DBMS/images/`) or original Excalidraw reconstructions (vault-root `Excalidraw/`, prefix `DBMS - `). Both are embedded by bare filename, so the note survives a folder move.

| Figure | Carries |
| --- | --- |
| [[DBMS - Disk Structure.excalidraw\|Disk Structure]] | Platter / track / sector geometry and the seek + rotational-delay cost of §1.2 |
| [[DBMS - Blocking and Spanned Records.excalidraw\|Blocking and Spanned Records]] | Blocking factor $b = B/r$ and unspanned versus spanned records of §1.4 |
| [[DBMS - File Block Allocation.excalidraw\|File Block Allocation]] | Contiguous, linked and mixed allocation of file blocks of §1.5 |
| [[DBMS - Hashed File and Overflow Chains.excalidraw\|Hashed File and Overflow Chains]] | Main buckets plus overflow chains of §1.10 |
| [[DBMS - Extendible Hashing.excalidraw\|Extendible Hashing]] | Global/local depth, the directory and a bucket split of §§1.13–1.15 |
| [[DBMS - Linear Hashing.excalidraw\|Linear Hashing]] | The split pointer, $h_0$ / $h_1$ and the round-by-round growth of §§1.17–1.20 |
| [[DBMS - Primary Index.excalidraw\|Primary Index]] | One sparse index entry per data block of §1.22 |
| [[DBMS - Multilevel Index.excalidraw\|Multilevel Index]] | The index-of-an-index tree of §1.25 |
| [[DBMS - Secondary Index.excalidraw\|Secondary Index]] | Dense entries for a key versus non-unique values of §1.28 |
| [[DBMS - Bplus Tree Structure.excalidraw\|Bplus Tree Structure]] | Root / internal / leaf levels and the leaf chain of §1.32 |
| [[DBMS - Bplus Tree Node Format.excalidraw\|Bplus Tree Node Format]] | $m$ pointers and $m-1$ keys inside an internal node of §1.33 |
| [[DBMS - Bplus Tree Insertion Split.excalidraw\|Bplus Tree Insertion Split]] | Leaf and internal split with key replication versus key move of §1.35 |
| [[DBMS - Bplus Replicate vs Move.excalidraw\|Bplus Replicate vs Move]] | The deck's numbers (14 replicated at a leaf split, 14 moved at an internal split), §1.35 |
| [[DBMS - Extendible Hashing Trace.excalidraw\|Extendible Hashing Trace]] | Snapshots of the 45, 22, 12, 11, 15, 10 example with doublings marked, §1.16 |
| [[DBMS - Linear Hashing Trace.excalidraw\|Linear Hashing Trace]] | Snapshots of the 12, 11, 14, 13, 9, 10, 18 example with $h_i$ and $N$, §1.20 |
| [[DBMS - Index Types Compared.excalidraw\|Index Types Compared]] | Primary vs clustering vs secondary entries and sizes, §1.21 |

Page renders lifted from the deck (every one is embedded with a width and an italic caption):

| Figure | Carries |
| --- | --- |
| [[DBMS - Disk Structure (deck p2).png\|Disk Structure (deck p2)]] | The deck's disk-structure figure, §1.2 |
| [[DBMS - Hashed File Buckets (deck p13).png\|Hashed File Buckets (deck p13)]] | The deck's bucket-and-overflow figure, §1.10 |
| [[DBMS - Extendible Hashing Directory (deck p18).png\|Extendible Hashing Directory (deck p18)]] | The deck's directory with trailing-bit suffixes, §1.13 |
| [[DBMS - Linear Hashing Split (deck p29).png\|Linear Hashing Split (deck p29)]] | The deck's linear-hashing split example, §1.20 |
| [[DBMS - Bplus Tree Example (deck p51).png\|Bplus Tree Example (deck p51)]] | The deck's $B^+$ tree example, §1.32 |
| [[DBMS - Bplus Tree Insertion Example (deck p53).png\|Bplus Tree Insertion Example (deck p53)]] | The deck's insertion trace, §1.36 |
| [[DBMS - Bplus Tree Deletion Example (deck p57).png\|Bplus Tree Deletion Example (deck p57)]] | The deck's deletion trace, §1.38 |

---

## Open gaps

> [!warning] What is still missing
> - **The entire pre-midsem block has no note file yet** — topics 1, 2, 3, 3.1, 4 and 6 above have only a syllabus row and a PDF link. No figures, section index or formula summary exist for them until that note is written.
> - **Topic 2 diagrams** — [[algos.pdf]] is written as [[DBMS_Notes#2. Query / Join Algorithms (algos)|§2]]; only the merge-phase figure (deck p. 10) is embedded as a page render. The deck leaves set-operation details to the student (slide 22), so §2.18 records only what the slide states.
> - **Topic 3 diagrams** — the [[transactions.pdf]] deck presents several schedules, the transaction-state diagram and precedence-graph examples as slide graphics; where text extraction did not recover the exact step layout, [[DBMS_Notes#3. Transactions|§3]] records the deck's stated definitions, facts and outcomes rather than inventing diagram bodies.
> - The Silberschatz textbook ([[silberschatz_dbms.pdf]]) was used only to explain topic 1; the worked numbers and conventions in the notes come from the respective decks ([[file-management.pdf]], [[transactions.pdf]]), not the book.

> [!question] Self-check before you tick a topic
> - Can you state the topic's **key formula** from memory and say what it assumes — $b = B/r$, $\mathrm{BF}_i = B/(V+P)$, the $B^+$ internal and leaf order inequalities?
> - Can you draw the **figure** that carries the topic — the disk geometry, the overflow chain, the extendible-hashing directory, the linear split pointer, the primary index, the $B^+$ tree?
> - Can you run the **trace** end to end with the deck's own numbers, and name the **one trap** the lecturer flagged (trailing bits, local-depth doubling, leaf-key replication)?
> - For topic 3, can you state **ACID** with the fund-transfer example, trace the **transaction states** (including restart/kill from Aborted), test a schedule for **conflict serializability** with the precedence graph, and distinguish **recoverable**, **cascadeless** and **cascading rollback** by their commit/read ordering? Can you order the SQL-92 isolation levels and recall the snapshot-isolation warning?
