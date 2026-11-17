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

This file is the **authority** for the topic list, the topic order and the post-midsem / end-semester split. The note [[Post-Midsem-Notes]] is written against it topic by topic; every topic below names its lecture deck and jumps straight to the matching heading in the note. The authoritative formatting rules live in [[context]].

| Block | Topics | Note file |
| --- | --- | --- |
| Post-midsem / end-sem | 1–3 | [[Post-Midsem-Notes]] |

> [!warning] Scope of the examination
> This block covers all three post-midsem topics — file management, query algorithms and transactions. Only **topic 1 is written** so far; topics 2 and 3 are still open.

> [!info] How to use this tracker
> - Tick the box on a topic line when the topic is **revised and recallable**, not merely read once. Untick it if a revision pass exposes a hole.
> - **PDF** opens the lecture deck; **Notes** jumps to the topic's heading in [[Post-Midsem-Notes]]. The section index at the bottom gives a one-click jump to every written section.
> - The counter below is live (Dataview) — it reads the checkboxes in this file, so nothing needs counting by hand.
> - `§` numbers are the H2/H3 section numbers used inside [[Post-Midsem-Notes]] (e.g. §1.24 is a real heading there).

## Progress

```dataview
TABLE WITHOUT ID
  string(length(filter(file.tasks, (t) => t.completed))) + " / " + string(length(file.tasks)) AS "Topics ticked",
  string(round(100 * length(filter(file.tasks, (t) => t.completed)) / length(file.tasks))) + " %" AS "Coverage",
  length(filter(file.tasks, (t) => !t.completed)) AS "Still open"
WHERE file.path = this.file.path
```

---

## Post-Midsem — 3 topics

- [ ] **1 · File Organization and Indexing** — [[file-management.pdf|PDF]] · [[Post-Midsem-Notes#1. File Organization and Indexing|Notes → §1]] (39 sections)
- [ ] **2 · Query / Join Algorithms (algos)** — [[algos.pdf|PDF]] · [[Post-Midsem-Notes|Notes]] (not yet written)
- [ ] **3 · Transactions** — [[transactions.pdf|PDF]] · [[Post-Midsem-Notes|Notes]] (not yet written)

> [!tip] Exam pointer
> Topic 1's marks sit on the **numbers and traces**, not the definitions: block-access arithmetic and $b = B/r$, the 9500-record primary index giving 49 blocks and $\lceil\log_2 49\rceil + 1 = 7$ accesses, the extendible-hashing directory doubling on a full local depth, the linear-hashing split deciding between $k$ and $k + M'$ from the parity of $r$, and the $B^+$ tree order $m$ / $m_{\text{leaf}}$ with the leaf-key-replicated-versus-internal-key-moved split rule.

---

## Section index of the notes

Every written section of [[Post-Midsem-Notes]], grouped by topic, so a topic can be opened at the exact sub-heading.

### §1 · File Organization and Indexing

| § | Section |
| --- | --- |
| 1.1 | [[Post-Midsem-Notes#1.1 Disk space management — who owns the disk?\|Disk space management — who owns the disk?]] |
| 1.2 | [[Post-Midsem-Notes#1.2 Structure of disks and the cost of a block access\|Structure of disks and the cost of a block access]] |
| 1.3 | [[Post-Midsem-Notes#1.3 Data records and files — fixed length vs variable length\|Data records and files — fixed length vs variable length]] |
| 1.4 | [[Post-Midsem-Notes#1.4 Packing records into blocks — blocking factor and spanned records\|Packing records into blocks — blocking factor and spanned records]] |
| 1.5 | [[Post-Midsem-Notes#1.5 Mapping file blocks onto disk blocks\|Mapping file blocks onto disk blocks]] |
| 1.6 | [[Post-Midsem-Notes#1.6 Operations on files and the role of file organization\|Operations on files and the role of file organization]] |
| 1.7 | [[Post-Midsem-Notes#1.7 The three primary file organizations — an overview\|The three primary file organizations — an overview]] |
| 1.8 | [[Post-Midsem-Notes#1.8 Heap files\|Heap files]] |
| 1.9 | [[Post-Midsem-Notes#1.9 Sorted (sequential) files\|Sorted (sequential) files]] |
| 1.10 | [[Post-Midsem-Notes#1.10 Hashed files — buckets and overflow chains\|Hashed files — buckets and overflow chains]] |
| 1.11 | [[Post-Midsem-Notes#1.11 Performance of static hashing\|Performance of static hashing]] |
| 1.12 | [[Post-Midsem-Notes#1.12 Dynamic file organization — why hashing must grow\|Dynamic file organization — why hashing must grow]] |
| 1.13 | [[Post-Midsem-Notes#1.13 Extendible hashing — structure\|Extendible hashing — structure]] |
| 1.14 | [[Post-Midsem-Notes#1.14 Insertion in extendible hashing\|Insertion in extendible hashing]] |
| 1.15 | [[Post-Midsem-Notes#1.15 Deletion in extendible hashing\|Deletion in extendible hashing]] |
| 1.16 | [[Post-Midsem-Notes#1.16 Extendible hashing — the full worked example\|Extendible hashing — the full worked example]] |
| 1.17 | [[Post-Midsem-Notes#1.17 Linear hashing — structure and the hash-function family\|Linear hashing — structure and the hash-function family]] |
| 1.18 | [[Post-Midsem-Notes#1.18 Insertion in linear hashing\|Insertion in linear hashing]] |
| 1.19 | [[Post-Midsem-Notes#1.19 Nature of the hash functions\|Nature of the hash functions]] |
| 1.20 | [[Post-Midsem-Notes#1.20 Linear hashing — the full worked example\|Linear hashing — the full worked example]] |
| 1.21 | [[Post-Midsem-Notes#1.21 Index structures — the three kinds\|Index structures — the three kinds]] |
| 1.22 | [[Post-Midsem-Notes#1.22 Primary index — structure\|Primary index — structure]] |
| 1.23 | [[Post-Midsem-Notes#1.23 Record access using the primary index\|Record access using the primary index]] |
| 1.24 | [[Post-Midsem-Notes#1.24 Primary index — worked example (9,500 blocks)\|Primary index — worked example (9,500 blocks)]] |
| 1.25 | [[Post-Midsem-Notes#1.25 Making the index multilevel\|Making the index multilevel]] |
| 1.26 | [[Post-Midsem-Notes#1.26 Range search, insertion and deletion on the primary index\|Range search, insertion and deletion on the primary index]] |
| 1.27 | [[Post-Midsem-Notes#1.27 Clustering index\|Clustering index]] |
| 1.28 | [[Post-Midsem-Notes#1.28 Secondary index — the two cases\|Secondary index — the two cases]] |
| 1.29 | [[Post-Midsem-Notes#1.29 Secondary index on a key — worked example\|Secondary index on a key — worked example]] |
| 1.30 | [[Post-Midsem-Notes#1.30 Multilevel secondary index — worked example\|Multilevel secondary index — worked example]] |
| 1.31 | [[Post-Midsem-Notes#1.31 ISAM files\|ISAM files]] |
| 1.32 | [[Post-Midsem-Notes#1.32 $B^+$ trees — the idea and the properties\|$B^+$ trees — the idea and the properties]] |
| 1.33 | [[Post-Midsem-Notes#1.33 Order of internal and leaf nodes\|Order of internal and leaf nodes]] |
| 1.34 | [[Post-Midsem-Notes#1.34 Order calculation — worked example\|Order calculation — worked example]] |
| 1.35 | [[Post-Midsem-Notes#1.35 Insertion into $B^+$ trees\|Insertion into $B^+$ trees]] |
| 1.36 | [[Post-Midsem-Notes#1.36 $B^+$ tree insertion — worked example\|$B^+$ tree insertion — worked example]] |
| 1.37 | [[Post-Midsem-Notes#1.37 Deletion in $B^+$ trees\|Deletion in $B^+$ trees]] |
| 1.38 | [[Post-Midsem-Notes#1.38 $B^+$ tree deletion — worked example\|$B^+$ tree deletion — worked example]] |
| 1.39 | [[Post-Midsem-Notes#1.39 Advantages and disadvantages of $B^+$ trees\|Advantages and disadvantages of $B^+$ trees]] |

### §2 · Query / Join Algorithms (algos)

Not yet written — see the open deck [[algos.pdf]].

### §3 · Transactions

Not yet written — see the open deck [[transactions.pdf]].

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
> - **Topic 2 (query / join algorithms)** — [[algos.pdf]] is not yet mined and [[Post-Midsem-Notes]] has no §2.
> - **Topic 3 (transactions)** — [[transactions.pdf]] is not yet mined and [[Post-Midsem-Notes]] has no §3.
> - The Silberschatz textbook ([[silberschatz_dbms.pdf]]) was used only to explain topic 1; the worked numbers and conventions in the note come from [[file-management.pdf]], not the book.

> [!question] Self-check before you tick a topic
> - Can you state the topic's **key formula** from memory and say what it assumes — $b = B/r$, $\mathrm{BF}_i = B/(V+P)$, the $B^+$ internal and leaf order inequalities?
> - Can you draw the **figure** that carries the topic — the disk geometry, the overflow chain, the extendible-hashing directory, the linear split pointer, the primary index, the $B^+$ tree?
> - Can you run the **trace** end to end with the deck's own numbers, and name the **one trap** the lecturer flagged (trailing bits, local-depth doubling, leaf-key replication)?
