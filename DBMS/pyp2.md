---
title: DBMS — Previous Year Question Paper 2
tags:
  - dbms
  - pyp
---

# DBMS — Previous Year Question Paper 2

*Source: [[prev_yr2.png]] — CSE361: Database Management System, End-Semester Exam, V Sem — Max Marks: 100, Max Time: 180 Min.*

*Companion paper: [[pyp]].*

| Q | Topic | Marks |
| --- | --- | --- |
| 1 | Equivalence of the two 3NF definitions | 10 |
| 2 | Dependency preserving ⇒ lossless? | 8 |
| 3 | Hash-based Union / Intersect / Difference | 15 |
| 4 | View & conflict serializability (5 transactions) | 12 |
| 5 | Weak entity vs composite multivalued attribute | 5 |
| 6 | Unsafe TRC expression | 2 |
| 7 | BCNF but not 4NF (≥ 6 attributes) | 8 |
| 8 | Is a minimal cover needed for 3NF synthesis? | 15 |
| 9 | Primary / multilevel index block accesses | 10 |
| 10 | (min, max) cardinality → relational model | 5 |
| 11 | Armstrong's axioms proofs | 10 |

---

> [!question] Q1: Equivalence of the two definitions of 3NF (8M proof + 2M definitions = 10M)
> Prove that both the definitions of 3NF are equivalent.
>
> > [!info]- Theory: terminology used in the proof (click to expand)
> > Let $R$ be a relation schema with FD set $F$ (all reasoning is over the closure $F^+$).
> >
> > - **Candidate key** $K$: a minimal set of attributes with $K \to R$. A **superkey** is any superset of a candidate key.
> > - **Prime attribute**: an attribute that belongs to *at least one* candidate key. **Non-prime** otherwise.
> > - **Trivial FD**: $X \to A$ with $A \in X$.
> > - **Partial dependency**: a non-prime attribute $A$ is *partially dependent* on candidate key $K$ if $X \to A$ for some **proper subset** $X \subsetneq K$.
> > - **Transitive dependency**: a non-prime attribute $A$ is *transitively dependent* on candidate key $K$ if there is an attribute set $Z$ such that $Z$ is **neither a superkey nor a subset of any candidate key**, $K \to Z$, $Z \to A$ and $A \notin Z$.
> >
> > Since $K$ is a key, $K \to Z$ holds for **every** attribute set $Z$ — so the only real requirements for a transitive dependency are "$Z \to A$, $Z$ is not a superkey, $Z$ is not inside a key".
>
> ### The two definitions (2M)
>
> **Definition 1 — structural / Codd form (generalised to all candidate keys):**
> $R$ is in 3NF iff
> 1. $R$ is in **2NF** (no non-prime attribute is partially dependent on any candidate key), **and**
> 2. **no non-prime attribute is transitively dependent on any candidate key.**
>
> **Definition 2 — "superkey or prime" form (Elmasri–Navathe / Silberschatz):**
> $R$ is in 3NF iff for **every non-trivial FD** $X \to A$ in $F^+$, **at least one** holds:
> - (a) $X$ is a **superkey** of $R$, or
> - (b) $A$ is a **prime attribute**.
>
> *(Silberschatz states (b) as "every attribute in $\beta-\alpha$ is contained in some candidate key" for $\alpha\to\beta$. This is the same thing: $\alpha \to \beta$ holds iff $\alpha\to A$ holds for each $A\in\beta$ by the decomposition rule, so it is enough to argue with single attributes $A$.)*
>
> **Claim:** Definition 1 $\iff$ Definition 2.
>
> ### Part I — Definition 1 $\Rightarrow$ Definition 2 (contrapositive)
>
> Assume $R$ satisfies Definition 1. Take any non-trivial FD $X \to A$ in $F^+$ (so $A \notin X$) with $A$ **non-prime**. We must show $X$ is a superkey. Suppose, for contradiction, that **$X$ is not a superkey**. There are exactly two cases.
>
> **Case 1 — $X$ is a proper subset of some candidate key $K$** ($X \subsetneq K$).
> Then $X \to A$ with $A$ non-prime and $X \subsetneq K$ is, by definition, a **partial dependency** of $A$ on $K$. This violates 2NF, i.e. violates Definition 1(1). **Contradiction.**
>
> **Case 2 — $X$ is not contained in any candidate key.**
> Together with "$X$ is not a superkey" this means $X$ is neither a superkey nor a subset of a key. Pick any candidate key $K$. Because $K$ is a key, $K \to X$. We also have $X \to A$, $A \notin X$, $A$ non-prime (so $A \notin K$). Hence $A$ is **transitively dependent** on $K$ via $Z = X$:
> $$ K \to X \to A $$
> This violates Definition 1(2). **Contradiction.**
>
> (These two cases are exhaustive: if $X$ is contained in a candidate key, either $X$ equals it — then $X$ is a superkey, excluded — or $X$ is a proper subset, which is Case 1.)
>
> So whenever $A$ is non-prime, $X$ must be a superkey. That is exactly Definition 2: for every non-trivial $X\to A$, either $X$ is a superkey or $A$ is prime. $\square$
>
> ### Part II — Definition 2 $\Rightarrow$ Definition 1 (contrapositive)
>
> Assume $R$ satisfies Definition 2. We show both conditions of Definition 1.
>
> **(1) $R$ is in 2NF.** Suppose not: there is a non-prime $A$, a candidate key $K$ and $X \subsetneq K$ with $X \to A$.
> - The FD is non-trivial: $A$ is non-prime but every attribute of $X \subseteq K$ is prime, so $A\notin X$.
> - $X$ is **not a superkey**: a proper subset of a candidate key cannot be a superkey, otherwise $K$ would not be minimal.
> - $A$ is **not prime**.
>
> So $X \to A$ violates Definition 2 (neither (a) nor (b)). **Contradiction.** Hence no partial dependency exists.
>
> **(2) No non-prime attribute is transitively dependent on a key.** Suppose non-prime $A$ is transitively dependent on key $K$ via $Z$: $K \to Z$, $Z \to A$, $A \notin Z$, and $Z$ is neither a superkey nor a subset of a key.
> - $Z \to A$ is non-trivial ($A \notin Z$).
> - $Z$ is **not a superkey**.
> - $A$ is **not prime**.
>
> So $Z \to A$ violates Definition 2. **Contradiction.** Hence no transitive dependency of a non-prime attribute on a key exists.
>
> Both conditions of Definition 1 hold. $\square$
>
> ### Conclusion
>
> Part I and Part II give Definition 1 $\iff$ Definition 2, so the two definitions describe exactly the same set of relation schemas. The only "gap" an examiner will look for is the two-case split (proper subset of a key vs. not inside any key) — it is the bridge between "partial/transitive dependency" language and "superkey-or-prime" language.
>
> > [!tip] Exam pointer
> > Write the two definitions first (2M are for them alone). Then prove the two directions *separately* and name the contradiction in each: partial dependency ⇒ breaks 2NF; transitive dependency ⇒ breaks the "no transitive" clause. The mapping to remember: **$X$ inside a key ↔ partial dependency**, **$X$ outside every key and not a superkey ↔ transitive dependency**, **$A$ prime ↔ the loophole that 3NF (unlike BCNF) allows.**

> [!question] Q2: Dependency preserving ⇒ always lossless? (8M)
> Prove or disprove: if a decomposition is dependency preserving, then it will always be lossless.
>
> > [!info]- Theory: the two tests (click to expand)
> > **Lossless-join (binary decomposition $R \to R_1, R_2$):** lossless iff
> > $$ (R_1 \cap R_2) \to R_1 \quad\text{or}\quad (R_1 \cap R_2) \to R_2 \ \in F^+ $$
> > i.e. the common attributes form a superkey of at least one of the two pieces. Lossless means $r = \Pi_{R_1}(r) \bowtie \Pi_{R_2}(r)$ for every legal instance $r$ — the join returns *exactly* the original tuples, no spurious ones.
> >
> > **Dependency preservation:** let $F_i = \{\,X\to Y \in F^+ : XY \subseteq R_i\,\}$ be the projection of $F$ on $R_i$. The decomposition preserves dependencies iff
> > $$ (F_1 \cup F_2 \cup \dots \cup F_n)^+ = F^+ $$
> > i.e. every FD can be checked inside a single relation, with no join.
> >
> > The first property is about **information** (can we rebuild the data?), the second about **constraint checking** (can we enforce $F$ cheaply?). They talk about different things, so neither implies the other.
>
> **Verdict: the statement is FALSE — disproved by a counterexample.**
>
> **Counterexample.** $R(A,B,C)$, $F = \{A \to B\}$. Decompose into $R_1(A,B)$ and $R_2(B,C)$.
>
> **Step 1 — the decomposition is dependency preserving.**
> - $F_1$ (on $\{A,B\}$) $= \{A \to B\}$.
> - $F_2$ (on $\{B,C\}$) $= \varnothing$ (no non-trivial FD of $F^+$ lives entirely inside $\{B,C\}$).
> - $(F_1\cup F_2)^+ = \{A\to B\}^+ = F^+$. ✔ Every FD of $F$ can be checked inside $R_1$ alone.
>
> **Step 2 — the decomposition is NOT lossless.**
> - $R_1 \cap R_2 = \{B\}$.
> - Is $B \to R_1 = AB$? That needs $B \to A$. Not in $F^+$ ($B^+ = \{B\}$). ✘
> - Is $B \to R_2 = BC$? That needs $B \to C$. Not in $F^+$. ✘
> - Neither holds, so the lossless test fails.
>
> **Step 3 — a concrete instance showing the spurious tuples.** $r$ satisfies $A\to B$:
>
> | $A$ | $B$ | $C$ |
> | --- | --- | --- |
> | $a_1$ | $b_1$ | $c_1$ |
> | $a_2$ | $b_1$ | $c_2$ |
>
> $\Pi_{AB}(r) = \{(a_1,b_1),(a_2,b_1)\}$ and $\Pi_{BC}(r) = \{(b_1,c_1),(b_1,c_2)\}$. Their natural join on $B$:
>
> | $A$ | $B$ | $C$ | in $r$? |
> | --- | --- | --- | --- |
> | $a_1$ | $b_1$ | $c_1$ | yes |
> | $a_1$ | $b_1$ | $c_2$ | **no — spurious** |
> | $a_2$ | $b_1$ | $c_1$ | **no — spurious** |
> | $a_2$ | $b_1$ | $c_2$ | yes |
>
> $r_1 \bowtie r_2 \neq r$ (4 tuples vs 2). **Lossy.**
>
> **Step 4 — (optional) formal check with the chase tableau.** Rows: $R_1=(A,B)$, $R_2=(B,C)$.
>
> | | $A$ | $B$ | $C$ |
> | --- | --- | --- | --- |
> | $R_1$ | $a$ | $a$ | $b_{13}$ |
> | $R_2$ | $b_{21}$ | $a$ | $a$ |
>
> Apply $A \to B$: the two rows have different $A$ values ($a$ vs $b_{21}$), so the FD never fires and nothing changes. No row ever becomes all-$a$'s, so the decomposition is lossy. ✔
>
> **Conclusion.** $\{R_1,R_2\}$ is dependency preserving but not lossless. **The statement is disproved.**
>
> **Why it happens:** an FD that lives entirely inside one fragment ($A\to B \subseteq R_1$) is trivially "preserved", but nothing guarantees the fragments share a key-like connecting attribute. Preservation only looks at FDs *inside* pieces; losslessness looks at the *overlap between* pieces.
>
> **Even simpler (disjoint) counterexample:** $R(A,B,C,D)$, $F=\{A\to B,\ C\to D\}$, $R_1(A,B)$, $R_2(C,D)$. Preserving, yet $R_1\cap R_2=\varnothing$ so the join is a Cartesian product — lossy.
>
> > [!tip] Exam pointer
> > Also state the converse to show you understand independence: **lossless ⇏ dependency preserving** ($R(A,B,C)$, $F=\{AB\to C, C\to B\}$, $R_1(A,C)$, $R_2(B,C)$ is lossless but loses $AB\to C$) — see [[pyp]] Q2(a). The practical moral: BCNF decomposition guarantees lossless but may lose dependencies, 3NF synthesis guarantees **both** (see Q8).

> [!question] Q3: Union, Intersect and Difference using hash-based methods (15M)
> Explain in detail Union, Intersect and Difference using hash-based join methods.
>
> > [!info]- Theory: why hashing works for set operations (click to expand)
> > The set operations $r\cup s$, $r\cap s$, $r-s$ require **union-compatible** relations (same attributes/domains). Two tuples are "equal" only if **all** attributes are equal. That is exactly an equi-join on *every* attribute — so the same machinery as **hash join** (partition, then build & probe) can be reused.
> >
> > **Key idea:** if the *same hash function $h_1$ (applied to the whole tuple)* splits both relations into $n$ partitions, then identical tuples always land in partitions with the **same index**. So a tuple of $r_i$ can only possibly match a tuple in $s_i$ — never in $s_j$, $j\neq i$. The big problem therefore decomposes into $n$ independent small problems.
> >
> > **Notation:** $b_r, b_s$ = blocks of $r, s$; $M$ = memory buffer blocks; $n$ = number of partitions; $h_1$ = partitioning hash; $h_2$ = a **different** hash used for the in-memory hash index (using $h_1$ again would put every tuple of a partition in one bucket).
>
> ### Phase 1 — Partitioning (common to all three operations)
>
> 1. Choose $n$ so that each partition of the **build relation** $r$ (plus its in-memory hash index) fits in memory: $n \ge \lceil b_r / M \rceil$ (times a small fudge factor for the hash table overhead), and $n \le M-1$ so one output buffer per partition fits.
> 2. Scan $r$; for each tuple $t$ compute $h_1(t)$ and write it to the buffer of partition $r_{h_1(t)}$; flush buffers to disk when full. Result: $r_0,\dots,r_{n-1}$.
> 3. Do the same for $s$ with the **same** $h_1$: $s_0,\dots,s_{n-1}$.
>
> ### Phase 2 — Per-partition build & probe
>
> For each $i = 0,\dots,n-1$:
> - **Build:** read $r_i$ fully into memory and build an in-memory hash index on it using $h_2$ over the entire tuple.
> - **Probe:** stream $s_i$ block by block, and for each tuple $t$ probe the index ($h_2(t)$, then compare within the bucket).
> - What you do on a hit / miss depends on the operation:
>
> | Operation | On probe of $t \in s_i$ | After $s_i$ is exhausted |
> | --- | --- | --- |
> | **Union** $r\cup s$ | **hit** → $t$ already present, discard it. **miss** → insert $t$ into the index. | write **all** tuples now in the index to the result |
> | **Intersection** $r\cap s$ | **hit** → output $t$ to the result (then optionally remove it so duplicates in $s_i$ are not output twice). **miss** → discard. | nothing more to output |
> | **Difference** $r-s$ | **hit** → **delete** that tuple from the index. **miss** → ignore. | output the **remaining** tuples in the index |
>
> **For $s-r$**, just swap the roles: build the hash index on $s_i$ and probe with $r_i$.
>
> **Why each is correct:**
> - *Union:* the index starts with all of $r_i$; each tuple of $s_i$ not already there is added. At the end the index = $r_i \cup s_i$ with duplicates eliminated automatically (a set can't hold a tuple twice).
> - *Intersection:* a tuple is in $r_i\cap s_i$ iff it is in the index (came from $r_i$) **and** appears in the probe stream (from $s_i$).
> - *Difference:* every tuple of $s_i$ that matches something in $r_i$ is knocked out of the index; what survives is exactly the tuples of $r_i$ that never appeared in $s_i$.
>
> ### Worked example
>
> Take single-attribute tuples $r=\{1,2,3,5,8\}$, $s=\{2,3,6,8,9\}$ and $h_1(x) = x \bmod 3$ (so $n=3$).
>
> | Partition | $r_i$ | $s_i$ |
> | --- | --- | --- |
> | 0 | $\{3\}$ | $\{3,6,9\}$ |
> | 1 | $\{1\}$ | $\{\}$ |
> | 2 | $\{2,5,8\}$ | $\{2,8\}$ |
>
> **Union:**
> - $i=0$: index $\{3\}$; probe 3 (hit, skip), 6 (miss, insert), 9 (miss, insert) → $\{3,6,9\}$.
> - $i=1$: index $\{1\}$; nothing to probe → $\{1\}$.
> - $i=2$: index $\{2,5,8\}$; probe 2 (hit), 8 (hit) → $\{2,5,8\}$.
> - Result: $\{1,2,3,5,6,8,9\}$ ✔
>
> **Intersection:**
> - $i=0$: probe 3 (hit → output), 6, 9 (miss). $i=1$: nothing. $i=2$: 2 (hit → output), 8 (hit → output).
> - Result: $\{2,3,8\}$ ✔
>
> **Difference $r-s$:**
> - $i=0$: index $\{3\}$; probe 3 (hit → delete) → $\{\}$.
> - $i=1$: index $\{1\}$, no probes → output 1.
> - $i=2$: index $\{2,5,8\}$; probe 2 (delete), 8 (delete) → $\{5\}$.
> - Result: $\{1,5\}$ ✔
>
> ### Cost analysis
>
> *If every partition of $r$ fits in memory (no recursive partitioning):*
> - Partitioning reads and writes both relations: $2(b_r + b_s)$ block transfers.
> - Build/probe phase reads each partition once: $b_r + b_s$.
> - **Total $\approx 3(b_r+b_s)$ block transfers**, plus about $2\left(\lceil b_r/b_b\rceil+\lceil b_s/b_b\rceil\right) + 2n$ seeks for $b_b$ blocks of buffer per partition (the "+4n" term in the textbook for partially filled blocks).
>
> *Recursive partitioning:* if $n > M-1$ (not enough buffers to partition in one pass), partition in several passes using different hash functions. The number of passes is $\lceil \log_{M-1}(b_s) - 1\rceil$ and the cost becomes
> $$ 2(b_r + b_s)\lceil \log_{M-1}(b_s)-1\rceil + (b_r + b_s). $$
>
> *Overflow handling:* if one partition is skewed so $r_i$ still doesn't fit, either re-partition that partition with a new hash function, or fall back to a block-nested-loop style probe for just that partition.
>
> **Choosing the build relation:** the smaller relation should be the build input so that it fits in memory with the fewest partitions.
>
> ### Comparison with sort-based set operations
>
> | | Hash-based | Sort-based (merge) |
> | --- | --- | --- |
> | Pre-processing | partition with $h_1$ | external sort both inputs |
> | Output order | unordered | sorted |
> | Duplicates | eliminated by the hash index | eliminated while merging |
> | Best when | one input is much smaller; no sort order needed | inputs already sorted or sorted output wanted |
> | Weakness | skewed data → partition overflow | sort cost $\propto b\log b$ |
>
> > [!tip] Exam pointer
> > The three things to state explicitly: (1) **same $h_1$ on both relations** so only matching partitions are compared, (2) a **different $h_2$** for the in-memory index, and (3) the **per-operation rule** (union = insert-if-absent; intersection = output-on-hit; difference = delete-on-hit, output survivors). A worked mini-example like the one above is the fastest way to earn the "in detail" marks.

> [!question] Q4: View and conflict serializability with five transactions (12M)
> Explain View and Conflict Serializability with the help of five transactions (each with at least three valid instructions) on two data items ($X$ and $Y$), and by using the same requirements, answer: a) give a schedule that is conflict serializable (justify using precedence graph); b) give a schedule that is not conflict serializable (justify using precedence graph).
>
> > [!info]- Theory: conflict and view serializability (click to expand)
> > **Conflicting instructions.** $I_i \in T_i$ and $I_j\in T_j$ ($i\ne j$) **conflict** iff they access the **same data item** and **at least one is a write**. Pairs: read–write, write–read, write–write conflict; read–read does **not**.
> >
> > **Conflict equivalence.** Two schedules are conflict equivalent if one can be turned into the other by swapping *adjacent non-conflicting* instructions of different transactions. **Conflict serializable** = conflict equivalent to some serial schedule.
> >
> > **Precedence (serialization) graph.** Node per transaction; edge $T_i\to T_j$ if an instruction of $T_i$ conflicts with and **precedes** an instruction of $T_j$. **Schedule is conflict serializable $\iff$ the graph is acyclic**; a topological order gives the equivalent serial schedule.
> >
> > **View equivalence.** Schedules $S, S'$ (same transactions) are view equivalent iff for every item $Q$:
> > 1. if $T_i$ reads the **initial** value of $Q$ in $S$, it does in $S'$;
> > 2. if $T_i$ reads a value of $Q$ **written by $T_j$** in $S$, the same happens in $S'$ (same "reads-from" pairs);
> > 3. the transaction doing the **final write** of $Q$ is the same in both.
> >
> > **View serializable** = view equivalent to some serial schedule. Every conflict-serializable schedule is view serializable; the converse fails — the difference is **blind writes** (a write with no earlier read of that item by the same transaction).
>
> ### The five transactions (data items $X$, $Y$; every transaction has 3 instructions)
>
> | Txn | Instruction 1 | Instruction 2 | Instruction 3 |
> | --- | --- | --- | --- |
> | $T_1$ | $R_1(X)$ | $W_1(X)$ | $R_1(Y)$ |
> | $T_2$ | $W_2(X)$ | $R_2(Y)$ | $W_2(Y)$ |
> | $T_3$ | $W_3(X)$ | $R_3(Y)$ | $W_3(Y)$ |
> | $T_4$ | $R_4(Y)$ | $W_4(Y)$ | $R_4(X)$ |
> | $T_5$ | $R_5(X)$ | $R_5(Y)$ | $W_5(X)$ |
>
> *(Each schedule below keeps every transaction's own instructions in their program order.)*
>
> ### (a) A conflict serializable schedule $S_1$
>
> | Step | $T_1$ | $T_2$ | $T_3$ | $T_4$ | $T_5$ |
> | --- | --- | --- | --- | --- | --- |
> | 1 | $R(X)$ | | | | |
> | 2 | $W(X)$ | | | | |
> | 3 | | $W(X)$ | | | |
> | 4 | $R(Y)$ | | | | |
> | 5 | | $R(Y)$ | | | |
> | 6 | | $W(Y)$ | | | |
> | 7 | | | $W(X)$ | | |
> | 8 | | | $R(Y)$ | | |
> | 9 | | | | | $R(X)$ |
> | 10 | | | $W(Y)$ | | |
> | 11 | | | | $R(Y)$ | |
> | 12 | | | | $W(Y)$ | |
> | 13 | | | | $R(X)$ | |
> | 14 | | | | | $R(Y)$ |
> | 15 | | | | | $W(X)$ |
>
> **Conflicts on $X$** (operations on $X$ in order: $R_1$(1), $W_1$(2), $W_2$(3), $W_3$(7), $R_5$(9), $R_4$(13), $W_5$(15)):
> - $R_1/W_1$ (steps 1,2) before $W_2$ (3) $\Rightarrow T_1\to T_2$
> - $W_1$/$W_2$ before $W_3$ (7) $\Rightarrow T_1\to T_3,\ T_2\to T_3$
> - $W_1,W_2,W_3$ before $R_5$ (9) $\Rightarrow T_1\to T_5,\ T_2\to T_5,\ T_3\to T_5$
> - $W_1,W_2,W_3$ before $R_4$ (13) $\Rightarrow T_1\to T_4,\ T_2\to T_4,\ T_3\to T_4$
> - $R_4$ (13) before $W_5$ (15) $\Rightarrow T_4\to T_5$
>
> **Conflicts on $Y$** (order: $R_1$(4), $R_2$(5), $W_2$(6), $R_3$(8), $W_3$(10), $R_4$(11), $W_4$(12), $R_5$(14)):
> - $R_1$ (4) before $W_2$ (6), $W_3$ (10), $W_4$ (12) $\Rightarrow T_1\to T_2,\ T_1\to T_3,\ T_1\to T_4$
> - $R_2$/$W_2$ before $W_3$, $R_4$, $W_4$, $R_5$ $\Rightarrow T_2\to T_3,\ T_2\to T_4,\ T_2\to T_5$
> - $R_3$ (8) before $W_4$ (12); $W_3$ (10) before $R_4$, $W_4$, $R_5$ $\Rightarrow T_3\to T_4,\ T_3\to T_5$
> - $W_4$ (12) before $R_5$ (14) $\Rightarrow T_4\to T_5$
>
> **Precedence graph edges of $S_1$:**
> $T_1\to T_2,\ T_1\to T_3,\ T_1\to T_4,\ T_1\to T_5,\ T_2\to T_3,\ T_2\to T_4,\ T_2\to T_5,\ T_3\to T_4,\ T_3\to T_5,\ T_4\to T_5.$
>
> ```
>        ┌──────────────────────────────────────┐
>        │   ┌─────────────────────────┐        │
>        │   │   ┌────────────┐        │        │
>        ▼   ▼   ▼            │        │        │
>   T1 ─► T2 ─► T3 ─► T4 ─► T5          (all edges go left → right;
>   (plus the "long" edges T1→T3, T1→T4, T1→T5,    every edge Ti → Tj has i < j)
>    T2→T4, T2→T5, T3→T5)
> ```
>
> Every edge goes from a lower-numbered to a higher-numbered transaction, so **there is no cycle ⇒ the graph is acyclic ⇒ $S_1$ is conflict serializable.** The (unique) topological order is $T_1, T_2, T_3, T_4, T_5$, so $S_1$ is conflict equivalent to the serial schedule $\langle T_1,T_2,T_3,T_4,T_5\rangle$. (It was built from that serial schedule by swapping only adjacent non-conflicting pairs, e.g. $R_1(Y)$ moved after $W_2(X)$, $R_5(X)$ moved earlier.)
>
> ### (b) A schedule that is NOT conflict serializable, $S_2$
>
> $S_2$ is the serial schedule $T_1T_2T_3T_4T_5$ with just one change: $T_4$'s last instruction $R_4(X)$ is **delayed until after $T_5$ has finished**.
>
> | Step | $T_1$ | $T_2$ | $T_3$ | $T_4$ | $T_5$ |
> | --- | --- | --- | --- | --- | --- |
> | 1 | $R(X)$ | | | | |
> | 2 | $W(X)$ | | | | |
> | 3 | $R(Y)$ | | | | |
> | 4 | | $W(X)$ | | | |
> | 5 | | $R(Y)$ | | | |
> | 6 | | $W(Y)$ | | | |
> | 7 | | | $W(X)$ | | |
> | 8 | | | $R(Y)$ | | |
> | 9 | | | $W(Y)$ | | |
> | 10 | | | | $R(Y)$ | |
> | 11 | | | | $W(Y)$ | |
> | 12 | | | | | $R(X)$ |
> | 13 | | | | | $R(Y)$ |
> | 14 | | | | | $W(X)$ |
> | 15 | | | | $R(X)$ | |
>
> **Edges:**
> - Everything between $T_1,T_2,T_3$ and later transactions goes forward exactly as in $S_1$: $T_1\to T_2,T_3,T_4,T_5$; $T_2\to T_3,T_4,T_5$; $T_3\to T_4,T_5$.
> - **$T_4 \to T_5$** — on $Y$: $W_4(Y)$ (step 11) precedes $R_5(Y)$ (step 13).
> - **$T_5 \to T_4$** — on $X$: $W_5(X)$ (step 14) precedes $R_4(X)$ (step 15).
>
> ```
>        ┌────────────┐
>        ▼            │
>       T4 ─────────► T5        ← 2-cycle T4 → T5 → T4
>        ▲            │
>        └────────────┘
> ```
>
> The graph contains the cycle $T_4\to T_5\to T_4$ ⇒ **$S_2$ is NOT conflict serializable.** No serial order can put $T_4$ both before $T_5$ (needed for $W_4(Y)\to R_5(Y)$) and after $T_5$ (needed for $W_5(X)\to R_4(X)$).
>
> *Bonus: $S_2$ is not even view serializable.* $T_5$ reads $Y$ from $T_4$ (so $T_4$ must precede $T_5$ in any equivalent serial schedule) and $T_4$ reads $X$ from $T_5$ (so $T_5$ must precede $T_4$) — contradictory reads-from requirements.
>
> ### (c) Illustrating View vs Conflict: view serializable but NOT conflict serializable, $S_3$
>
> This is the case that shows why view serializability is strictly weaker. It exploits the **blind writes** $W_2(X)$ and $W_3(X)$ (neither $T_2$ nor $T_3$ read $X$ first):
>
> | Step | $T_1$ | $T_2$ | $T_3$ | $T_4$ | $T_5$ |
> | --- | --- | --- | --- | --- | --- |
> | 1 | $R(X)$ | | | | |
> | 2 | | $W(X)$ | | | |
> | 3 | $W(X)$ | | | | |
> | 4 | $R(Y)$ | | | | |
> | 5 | | $R(Y)$ | | | |
> | 6 | | $W(Y)$ | | | |
> | 7 | | | $W(X)$ | | |
> | 8 | | | $R(Y)$ | | |
> | 9 | | | $W(Y)$ | | |
> | 10 | | | | $R(Y)$ | |
> | 11 | | | | $W(Y)$ | |
> | 12 | | | | $R(X)$ | |
> | 13 | | | | | $R(X)$ |
> | 14 | | | | | $R(Y)$ |
> | 15 | | | | | $W(X)$ |
>
> **Not conflict serializable:** $R_1(X)$ (step 1) precedes $W_2(X)$ (step 2) ⇒ $T_1\to T_2$; and $W_2(X)$ (step 2) precedes $W_1(X)$ (step 3) ⇒ $T_2\to T_1$. Cycle $T_1\rightleftarrows T_2$.
>
> **But view equivalent to the serial schedule $\langle T_1,T_2,T_3,T_4,T_5\rangle$:**
>
> | View condition | In $S_3$ | In serial $T_1T_2T_3T_4T_5$ | Match |
> | --- | --- | --- | --- |
> | Reads initial $X$ | $T_1$ ($R_1(X)$ before any write) | $T_1$ | ✔ |
> | Reads initial $Y$ | $T_1$ ($R_1(Y)$), $T_2$ ($R_2(Y)$) | $T_1$, $T_2$ ($T_1$ never writes $Y$) | ✔ |
> | $T_3$ reads $Y$ from | $T_2$ | $T_2$ | ✔ |
> | $T_4$ reads $Y$ from | $T_3$ | $T_3$ | ✔ |
> | $T_5$ reads $Y$ from | $T_4$ | $T_4$ | ✔ |
> | $T_4$, $T_5$ read $X$ from | $T_3$ (last writer before step 12/13) | $T_3$ | ✔ |
> | Final write of $X$ | $T_5$ | $T_5$ | ✔ |
> | Final write of $Y$ | $T_4$ | $T_4$ | ✔ |
>
> All three view conditions hold ⇒ $S_3$ is **view serializable** even though its precedence graph has a cycle. The writes $W_1(X)$ and $W_2(X)$ are both overwritten by $W_3(X)$ before anyone reads $X$, so their relative order never affects what any transaction sees — the conflict test is too strict here, the view test correctly accepts it.
>
> > [!tip] Exam pointer
> > To build a non-conflict-serializable schedule quickly: take a serial schedule and *delay one transaction's last instruction* past another transaction that conflicts with it on a **different** item than an earlier pair (as in $S_2$) — that forces opposite-direction edges. To show view ≠ conflict, always use **blind writes + a later overwriting write** ($S_3$). Remember: conflict-serializable ⊂ view-serializable ⊂ all schedules.

> [!question] Q5: Weak entity vs composite multivalued attribute (5M)
> Discuss with an illustration the design choice between a weak entity and a composite multi-valued attribute.
>
> > [!info]- Theory: the two modelling constructs (click to expand)
> > **Weak entity.** An entity type with **no key of its own**; it is existence-dependent on an **owner (identifying) entity** via an **identifying relationship** (1:N, with *total* participation of the weak entity). It has a **partial key (discriminator)**, unique only among entities of the same owner. Its full key = owner key + partial key. *Notation:* double rectangle; double diamond for the identifying relationship; dashed underline for the discriminator.
> >
> > **Composite multivalued attribute.** An attribute that is **multivalued** (several values per entity — double ellipse) **and composite** (made of sub-attributes — ellipse tree). It has no identity and cannot take part in relationships.
> >
> > **Design rule:** use an **attribute** when the information only *describes* the owner; use a **weak entity** when the information needs its **own attributes' semantics, identity, or its own relationships**.
>
> **Running example:** a `STUDENT` can have several **qualifications**, each with `Degree`, `Institute`, `Year`.
>
> **Option A — `QUALIFICATION` as a composite multivalued attribute of `STUDENT`:**
>
> ```
>                                   (Degree)   (Institute)   (Year)
>                                        \          |          /
>     ┌───────────┐                       \         |         /
>     │  STUDENT  │───────────────────── ((Qualification))        ← double ellipse
>     └───────────┘                       (multivalued + composite)
>        │      │
>     (roll_no) (name)       roll_no underlined = key
> ```
>
> Chosen when qualifications are just a list printed on the student's record: nobody else in the schema refers to one particular qualification, and it has no relationships of its own.
>
> **Option B — `QUALIFICATION` as a weak entity of `STUDENT`:**
>
> ```
>   ┌───────────┐  1      ╔═════════╗    N   ╔═══════════════╗
>   │  STUDENT  │═════════║  HAS    ║════════║ QUALIFICATION ║──(Institute)
>   │ roll_no   │         ╚═════════╝        ║ degree (- - -)║──(Year)
>   └───────────┘   identifying relationship ╚═══════════════╝
>                   (double diamond)          weak entity (double box)
>                                             degree = partial key (dashed underline)
> ```
>
> Chosen when a qualification is a **thing in its own right**: e.g. it is verified by a `VERIFIER` entity, linked to an `INSTITUTE` entity, or other entities (scholarships, placement eligibility) must reference *that specific* qualification.
>
> **Relational mapping (both end up as a separate table, because a 1NF row cannot hold a set):**
> - Option A: `QUALIFICATION(roll_no, degree, institute, year)` — `roll_no` FK → `STUDENT`; the attribute-table's key is the whole row.
> - Option B: `QUALIFICATION(roll_no, degree, institute, year)` with PK `(roll_no, degree)` = owner key + partial key, `roll_no` FK with `ON DELETE CASCADE`. Other tables can now carry `(roll_no, degree)` as a foreign key.
>
> **Choice summary:**
>
> | Question | Weak entity | Composite multivalued attribute |
> | --- | --- | --- |
> | Does another entity/relationship need to reference one specific instance? | Yes | No |
> | Has its own discriminator / identity concept? | Yes (partial key) | No |
> | Has its own relationships (e.g. with `INSTITUTE`)? | Yes | Not possible |
> | Purely descriptive data of the owner? | No | Yes |
> | Diagram complexity | more symbols | compact |
>
> > [!tip] Exam pointer
> > Lead with the deciding question: *"Does anything else need to point at one specific instance?"* Yes → weak entity; no → composite multivalued attribute. And note that both map to a similar table — the difference is **modelling intent** (and what can be enforced via keys/relationships), not final storage. Draw the ERD with the correct symbols: this is why the paper's marker asks for it pictorially.

> [!question] Q6: Unsafe TRC expression (2M)
> Give an example of an unsafe TRC expression.
>
> > [!info]- Theory: safety of TRC (click to expand)
> > A TRC expression $\{\,t \mid P(t)\,\}$ is **safe** if every tuple in its result is made only of values from $\text{dom}(P)$ — the **active domain**: constants appearing in $P$ plus all values in the relations mentioned in $P$. Safe expressions always give a **finite** relation. An expression that can produce values outside $\text{dom}(P)$ (hence possibly infinitely many tuples) is **unsafe**.
>
> **Example 1 (canonical):**
> $$ \{\, t \mid \lnot (t \in \text{Student}) \,\} $$
> *"All tuples that are not in `Student`."* The tuple variable ranges over **every possible tuple** over the attribute domains (all integers, all strings, …) except the finitely many in `Student`. The result is **infinite** and contains values appearing in no relation — so it is unsafe.
>
> **Example 2 (unbounded comparison):**
> $$ \{\, t \mid t[\text{marks}] > 50 \,\} $$
> No relation restricts $t$; infinitely many values satisfy the condition.
>
> **Example 3 (unguarded quantifier):**
> $$ \{\, t \mid \exists u\,(\lnot(u \in \text{Student}) \land t[\text{name}] = u[\text{name}]) \,\} $$
> $u$ ranges over all tuples *not* in `Student`, so $t[\text{name}]$ takes infinitely many values.
>
> **Contrast (safe):** $\{\,t \mid t\in \text{Student} \land t[\text{marks}]>50\,\}$ — $t$ is drawn from the finite relation `Student`, so the result is finite.
>
> > [!tip] Exam pointer
> > Give the definition of safety in one line, then Example 1. The reason to quote: *"the result is infinite / contains values not in $\text{dom}(P)$."*

> [!question] Q7: A relation with ≥ 6 attributes in BCNF but not in 4NF (8M)
> Give a relation with at least six attributes such that it is in BCNF and not in 4NF (with justification).
>
> > [!info]- Theory: BCNF vs 4NF (click to expand)
> > **BCNF:** for every non-trivial FD $X\to Y$ in $F^+$, $X$ is a superkey.
> >
> > **Multivalued dependency (MVD)** $X \twoheadrightarrow Y$: for every two tuples $t_1,t_2$ with $t_1[X]=t_2[X]$ there exist tuples $t_3,t_4$ with $t_3[X]=t_4[X]=t_1[X]$, $t_3[Y]=t_1[Y]$, $t_3[R-X-Y]=t_2[R-X-Y]$, $t_4[Y]=t_2[Y]$, $t_4[R-X-Y]=t_1[R-X-Y]$ (swapping the $Y$-parts keeps the tuples in the relation). Equivalent: $R$ losslessly decomposes into $R_1(X\cup Y)$ and $R_2(X\cup (R-Y))$.
> >
> > **4NF:** for every **non-trivial** MVD $X\twoheadrightarrow Y$ in $D^+$, $X$ is a superkey. (An MVD is trivial if $Y\subseteq X$ or $X\cup Y=R$.)
> >
> > BCNF only looks at **FDs**; 4NF also looks at **MVDs**. So a relation with *no* non-trivial FD (hence in BCNF vacuously) but with independent multivalued facts about the same key is in BCNF yet not in 4NF.
>
> **The relation.** $\text{STUDENT\_INFO}(\underline{SID,\ Phone,\ Email,\ Hobby,\ Language,\ Club})$ — **6 attributes**.
>
> A student can have several phone numbers, several e-mail addresses, several hobbies, several languages spoken, and be in several clubs, and these facts are **mutually independent**. Constraints:
> - FDs: **none** except the trivial ones (a student has many phones, so $SID\not\to Phone$, etc.). Therefore the only candidate key is the **whole attribute set** $\{SID,Phone,Email,Hobby,Language,Club\}$.
> - MVDs: $SID \twoheadrightarrow Phone,\ SID\twoheadrightarrow Email,\ SID \twoheadrightarrow Hobby,\ SID\twoheadrightarrow Language,\ SID\twoheadrightarrow Club$ (each set is independent of the rest).
>
> **Justification — in BCNF.** There is no non-trivial FD in $F^+$ at all. The BCNF condition ("every non-trivial FD has a superkey on the left") is vacuously true. ✔
>
> **Justification — not in 4NF.** Take the non-trivial MVD $SID \twoheadrightarrow Phone$:
> - It is **non-trivial**: $Phone \not\subseteq \{SID\}$ and $\{SID,Phone\}\ne R$.
> - Its left side $SID$ is **not a superkey** (the key is the whole schema).
>
> So the 4NF condition is violated. ✘
>
> **Why this is a real problem — redundancy.** If student 1 has 2 phones ($p_1,p_2$) and 2 e-mails ($e_1,e_2$) and (to keep it short) one hobby, one language, one club ($h$, $l$, $c$), the MVD forces **all combinations** to be stored:
>
> | SID | Phone | Email | Hobby | Language | Club |
> | --- | --- | --- | --- | --- | --- |
> | 1 | $p_1$ | $e_1$ | $h$ | $l$ | $c$ |
> | 1 | $p_1$ | $e_2$ | $h$ | $l$ | $c$ |
> | 1 | $p_2$ | $e_1$ | $h$ | $l$ | $c$ |
> | 1 | $p_2$ | $e_2$ | $h$ | $l$ | $c$ |
>
> Each phone number is repeated once per e-mail and vice-versa (redundancy). Adding a second e-mail forces inserting a tuple per phone (insertion anomaly); deleting the only remaining e-mail forces handling every phone row (deletion/update anomaly). 4 rows for $2+2$ facts; with $m$ phones, $n$ e-mails, $k$ hobbies, … it becomes $m\cdot n\cdot k\cdots$ rows.
>
> **Fix — decompose into 4NF** (each step splits on a violating MVD and is lossless):
> $$ R_1(SID, Phone),\ R_2(SID, Email),\ R_3(SID, Hobby),\ R_4(SID, Language),\ R_5(SID, Club) $$
> Each $R_i$ has only the trivial MVD $SID\twoheadrightarrow X$ with $SID\cup X=R_i$, so each is in 4NF, and the redundancy disappears.
>
> **Smaller textbook version of the same idea:** $R(\text{Course},\text{Teacher},\text{Book})$ with $\text{Course}\twoheadrightarrow\text{Teacher}\mid\text{Book}$ — padded to six attributes by treating each of Teacher and Book as a pair of attributes (e.g. name+email, title+edition) as long as no FD exists among them.
>
> > [!tip] Exam pointer
> > Template for any such question: choose independent multivalued facts about the same entity ⇒ **no FDs ⇒ whole-row key ⇒ BCNF holds vacuously**, then point at one **non-trivial MVD whose left side is not a superkey** ⇒ not 4NF. Always show the redundant rows and the 4NF decomposition.

> [!question] Q8: Is a minimal form of FDs required in the 3NF decomposition algorithm? (15M)
> In the 3NF decomposition algorithm, is it required to have a minimal form of FDs? Justify your claim.
>
> > [!info]- Theory: canonical (minimal) cover and 3NF synthesis (click to expand)
> > **Canonical / minimal cover $F_c$** of $F$: a set equivalent to $F$ (i.e. $F_c^+=F^+$) such that
> > 1. every FD has a **single attribute on the right** (or, in Silberschatz's form, FDs with the same left side are merged),
> > 2. **no extraneous attribute on any left side** — in $\alpha\to\beta$, $A\in\alpha$ is extraneous if $(F-\{\alpha\to\beta\})\cup\{(\alpha-A)\to\beta\}\equiv F$, i.e. $\beta \subseteq (\alpha-A)^+$ under $F$,
> > 3. **no extraneous attribute on the right** — $B\in\beta$ is extraneous if $\alpha \to B$ is implied by $(F-\{\alpha\to\beta\})\cup\{\alpha\to(\beta-B)\}$,
> > 4. **no redundant FD** — no FD can be derived from the others.
> >
> > **3NF synthesis algorithm (lossless + dependency preserving):**
> > 1. Compute a **canonical cover** $F_c$ of $F$.
> > 2. For each FD $\alpha\to\beta \in F_c$, create the relation schema $R_i=\alpha\cup\beta$ (merging FDs with the same left side).
> > 3. If **no** $R_i$ contains a candidate key of $R$, add a relation $R_{key}$ consisting of one candidate key.
> > 4. Drop any $R_i$ that is a subset of another $R_j$.
>
> **Claim: YES — the minimal (canonical) form is required.** The algorithm's step 1 is not decoration. Skipping it can (i) produce a relation that is **not in 3NF**, and (ii) produce **redundant relations**. Both are shown below.
>
> ### Counterexample 1 — extraneous attribute on the RIGHT breaks 3NF
>
> $R(A,B,C)$, $F=\{A \to BC,\ B \to C\}$. (Here $C$ is extraneous in $A\to BC$, because $A\to B\to C$.) Only candidate key: $A$.
>
> **Without minimal cover** — use $F$ as given:
> - $A\to BC \Rightarrow R_1(A,B,C)$; $B\to C\Rightarrow R_2(B,C)$.
> - $R_2\subseteq R_1$, so it is dropped. Final schema: just $R_1(A,B,C)=R$ itself.
> - But in $R_1$ the FD $B\to C$ holds with $B$ **not a superkey** and $C$ **non-prime** ⇒ **$R_1$ is NOT in 3NF.** ✘ (The algorithm "output" is the original unnormalised relation.)
>
> **With minimal cover** $F_c=\{A\to B,\ B\to C\}$:
> - $R_1(A,B)$, $R_2(B,C)$; $R_1$ contains the key $A$.
> - $R_1$: only $A\to B$, key $A$ ✔; $R_2$: only $B\to C$, key $B$ ✔. **Both in 3NF** (indeed BCNF). ✔
>
> ### Counterexample 2 — extraneous attribute on the LEFT breaks 3NF
>
> $R(A,B,C)$, $F=\{AB\to C,\ B\to C\}$. ($A$ is extraneous in $AB\to C$ since $B\to C$.) Candidate key: $AB$.
>
> **Without minimal cover:** $AB\to C\Rightarrow R_1(A,B,C)$; $B\to C \Rightarrow R_2(B,C)$ (a subset, dropped). Result $R_1(A,B,C)$ contains $B\to C$ with $B$ not a superkey, $C$ non-prime ⇒ **not in 3NF**. ✘
>
> **With minimal cover** $F_c=\{B\to C\}$: $R_1(B,C)$; no relation contains the key $AB$ ⇒ add $R_2(A,B)$. Result $\{(B,C),(A,B)\}$ — both 3NF ✔, lossless ($B$ is a key of $R_1$), dependency preserving ✔.
>
> ### Counterexample 3 — a redundant FD gives a redundant relation
>
> $R(A,B,C)$, $F=\{A\to B,\ B\to C,\ A\to C\}$ ($A\to C$ is redundant — it follows by transitivity).
>
> **Without minimal cover:** $R_1(A,B)$, $R_2(B,C)$, $R_3(A,C)$ — all three are in 3NF, but $R_3$ is **pure redundancy**: $A\to C$ is already enforced by $R_1\bowtie R_2$. Cost: an extra table, duplicated $A$–$C$ data (update anomalies between $R_3$ and the $R_1\bowtie R_2$ path), and extra join/constraint-checking work.
>
> **With minimal cover** $\{A\to B,\ B\to C\}$: just $R_1(A,B)$, $R_2(B,C)$.
>
> ### Full worked example (shows every step)
>
> $R(A,B,C,D)$, $F=\{A\to BC,\ B\to C,\ A\to B,\ AB\to D\}$.
>
> **Step 1 — canonical cover.**
> - *Split right sides:* $A\to B,\ A\to C,\ B\to C,\ A\to B,\ AB\to D$ (the duplicate $A\to B$ is removed): $\{A\to B,\ A\to C,\ B\to C,\ AB\to D\}$.
> - *Left extraneous:* in $AB\to D$, is $B$ extraneous? Compute $A^+$ using the FDs with $AB\to D$ kept as is: $A\to B$ gives $\{A,B\}$, then $AB\to D$ gives $\{A,B,D\}$ (and $B\to C$ gives $C$). $D\in A^+$ ✔, so $B$ is extraneous and $AB\to D$ becomes $A\to D$.
> - *Redundant FDs:* is $A\to C$ derivable from the rest $\{A\to B, B\to C, A\to D\}$? $A^+=\{A,B,C,D\}\ni C$ ✔ ⇒ **remove** $A\to C$.
> - $F_c=\{A\to B,\ B\to C,\ A\to D\}$.
>
> **Step 2 — one relation per FD (merge equal left sides):** $A\to B$ and $A\to D$ ⇒ $R_1(A,B,D)$; $B\to C \Rightarrow R_2(B,C)$.
>
> **Step 3 — contains a candidate key?** $A^+=\{A,B,C,D\}=R$, so $A$ is the key and $R_1\ni A$ ✔ — no extra relation.
>
> **Step 4 — remove subsets:** none.
>
> **Result:** $R_1(A,B,D)$, $R_2(B,C)$ — 3NF (and BCNF), lossless, dependency preserving.
>
> **If we had skipped Step 1** and used $F$ directly: $A\to BC\Rightarrow(A,B,C)$, $B\to C\Rightarrow(B,C)$ [subset, dropped], $AB\to D\Rightarrow(A,B,D)$. The relation $(A,B,C)$ contains $B\to C$ with $B$ not a superkey, $C$ non-prime ⇒ **not in 3NF**. ✘
>
> ### Why exactly minimality matters (the justification)
>
> 1. The algorithm builds each $R_i=\alpha\cup\beta$ from an FD $\alpha\to\beta$ and **assumes $\alpha$ is the key of $R_i$**, with nothing but $\alpha\to\beta$ holding inside it. This is only true if $\alpha$ has no extraneous attributes (else a smaller subset of $\alpha$ already determines $\beta$, and $\alpha$ isn't even a minimal key) and $\beta$ has no extraneous attributes (else part of $\beta$ is determined by a *non-key* part inside $R_i$, creating a transitive dependency inside $R_i$).
> 2. Redundant FDs add relations (and checking cost) without adding any constraint.
> 3. Correctness of **dependency preservation** only needs $F_c^+=F^+$ and one relation per FD; **losslessness** is ensured by the key relation (Step 3). Both properties hold *because* $F_c$ is equivalent to $F$ — so computing $F_c$ costs nothing in correctness and buys 3NF.
>
> **Nuance worth mentioning.** Splitting right sides into single attributes is just a convenience (the same-left-side FDs are merged back in Step 2). The **essential** parts are: *no extraneous attributes* and *no redundant FDs*.
>
> > [!tip] Exam pointer
> > The answer is a firm **yes**. Always attach the counterexample $F=\{A\to BC, B\to C\}$ — it is the shortest one: without the minimal cover the output is $R_1(A,B,C)$ which still has the transitive dependency $A\to B\to C$. Then show the same algorithm on the minimal cover giving $(A,B),(B,C)$.

> [!question] Q9: Index block accesses (10M)
> Given, in a data file: number of blocks $b = 10000$; block size $B = 5\text{ KB}$; ordering key field (OKF) length $V = 20$ bytes; block pointer length $p = 10$ bytes. Find the following:
> a) Max no. of block accesses to retrieve a record using the primary index. (4M)
> b) Max no. of block accesses to retrieve a record without using the primary index. (2M)
> c) Max no. of block accesses to retrieve a record using the multi-level primary index. (4M)
>
> > [!info]- Theory: primary index and multilevel index (click to expand)
> > A **primary index** is built on the **ordering key field** of a file *sorted* on that key. It is a **sparse** (non-dense) index: **one entry per data block**, holding $\langle K(i), P(i)\rangle$ = the key of the *first record* of block $i$ (the "anchor record") and a pointer to that block.
> >
> > - Index entry size: $R_i = V + p$.
> > - Index blocking factor: $bf_i = \lfloor B / (V+p) \rfloor$.
> > - Number of index entries: $r_1 = b$ (one per data block).
> > - Number of index blocks: $b_1 = \lceil r_1 / bf_i\rceil$.
> >
> > **Single-level primary index lookup:** binary search the index file ($\lceil\log_2 b_1\rceil$ block accesses) + 1 access to the data block.
> >
> > **Multilevel primary index:** treat the first-level index (itself a sorted file) as a data file and build a second-level index on it, and so on, until the top level fits in **one block**. Each level $j$ has $r_j=b_{j-1}$ entries and $b_j=\lceil r_j/bf_i\rceil$ blocks. With $x$ levels, a lookup costs **$x$ index block accesses (one per level) + 1 data block** $= x+1$.
>
> **Interpretation used:** the data file is **ordered on the OKF** (that is what makes the primary index possible). $5\text{ KB} = 5\times1024 = 5120$ bytes. *(If $5\text{ KB}=5000$ bytes is meant, see the check at the end — the answers do not change.)*
>
> ### Common computations
>
> - Index entry size $= V + p = 20 + 10 = 30$ bytes.
> - Index blocking factor $bf_i = \lfloor 5120 / 30 \rfloor = \lfloor 170.67\rfloor = 170$ entries per block.
> - First-level index entries $r_1 = b = 10000$ (one per data block).
> - First-level index blocks $b_1 = \lceil 10000/170 \rceil = \lceil 58.82\rceil = 59$.
>
> ### (a) Using the primary index
>
> Binary search in the index file of 59 blocks: $\lceil \log_2 59\rceil = 6$ (since $2^5=32<59\le 2^6=64$). Then 1 access to fetch the data block.
> $$ \text{accesses} = \lceil\log_2 b_1\rceil + 1 = 6+1 = \boxed{7} $$
>
> ### (b) Without using the primary index
>
> The data file is ordered on the key, so we can **binary search the data file directly**:
> $$ \text{accesses} = \lceil\log_2 b\rceil = \lceil\log_2 10000\rceil = \boxed{14}\quad (2^{13}=8192<10000\le 2^{14}=16384) $$
> *(If the file were **not** ordered on that key, only a linear scan is possible and the worst case is $b = 10000$ block accesses. Since a primary index presupposes an ordered file, 14 is the intended answer; mention 10000 as the unordered/linear-scan alternative.)*
>
> ### (c) Using a multilevel primary index
>
> - Level 1: $r_1 = 10000$ entries, $b_1 = 59$ blocks.
> - Level 2: $r_2 = b_1 = 59$ entries, $b_2 = \lceil 59/170\rceil = 1$ block. ← fits in **one** block, stop.
> - So there are $x = 2$ index levels.
> $$ \text{accesses} = x + 1 = 2+1 = \boxed{3} $$
> (one block at each index level — the top block is read straight into memory — then the data block).
>
> ### Summary
>
> | Method | Max block accesses |
> | --- | --- |
> | (a) Single-level primary index | **7** |
> | (b) No index (binary search on ordered data file) | **14** (10000 if only a linear scan is possible) |
> | (c) Multilevel primary index | **3** |
>
> **Check with $5\text{ KB}=5000$ bytes:** $bf_i=\lfloor5000/30\rfloor=166$, $b_1=\lceil 10000/166\rceil=61$, $\lceil\log_2 61\rceil=6\Rightarrow$ (a) $=7$; $b_2=\lceil61/166\rceil=1\Rightarrow$ (c) $=3$; (b) is unchanged $=14$. Same answers ✔.
>
> > [!tip] Exam pointer
> > Remember the primary index is **sparse: one entry per data block**, not per record — that is why $r_1=b$. And in the multilevel case the number of levels is until the top level is **a single block**; cost is $x+1$ (no binary search needed inside a level because each upper-level block is addressed by pointer).

> [!question] Q10: Translating (min, max) cardinality constraints from ERD to the relational model (5M)
> Explain the scenarios under which a (min, max) cardinality constraint in ERD can be translated to the relational model.
>
> > [!info]- Theory: (min, max) notation (click to expand)
> > For entity $E$ and relationship $R$, the pair **(min, max)** written next to $E$ says that each entity of $E$ takes part in **at least min and at most max** relationship instances of $R$.
> > - **min = 0** → *partial* participation (optional); **min ≥ 1** → *total* participation (mandatory; min = 1 is the common case).
> > - **max = 1** → "one side"; **max = N (or $*$)** → "many side"; max = $k>1$ finite is a *bounded* many.
> >
> > The relational model can express only certain constraints **declaratively** — through primary keys, `UNIQUE`, `NOT NULL`, foreign keys and `CHECK`. Whether a (min, max) pair can be translated depends on whether one of these can express it.
>
> **Direct translation (declarative, DBMS-enforced):**
>
> | (min, max) scenario | Relational translation | What enforces it |
> | --- | --- | --- |
> | **max = 1** on $E_1$'s side, $E_2$ is many (1:N) | put FK of $E_2$'s key **in $E_1$'s table** (the "many" side holds the FK) | FK constraint (each $E_1$ row has ≤ 1 partner) |
> | **min = 0**, max = 1 | FK column **nullable** | FK with `NULL` allowed |
> | **min = 1**, max = 1 (total participation on the "one-side-reference" end) | FK column `NOT NULL` | `NOT NULL` + FK |
> | **1:1**, both (·,1) | FK in either table (prefer the side with min=1) **+ `UNIQUE`** on the FK; or merge both tables if both are (1,1) | `UNIQUE` + FK |
> | **M:N**, both max = N (min = 0) | **separate table** for the relationship: $R(\underline{k_1,k_2},\text{attrs})$, both columns FKs, composite PK | PK + two FKs |
> | **Weak entity** (identifying relationship is $(1,1)$ at the weak side, $(0,N)$ at owner) | weak table with PK = owner key + partial key; FK with `ON DELETE CASCADE` | PK + FK + cascade |
>
> **Not directly translatable (needs extra mechanisms):**
>
> | (min, max) scenario | Problem | Workaround |
> | --- | --- | --- |
> | **min ≥ 1 on the "one" side of a 1:N** (e.g. every `DEPARTMENT` must have ≥ 1 `EMPLOYEE`, (1,N)) | the FK lives in the *other* table; a department row can exist with no referencing row, and "at least one referencing row" is not a key/FK constraint | triggers / assertions / application logic, or deferred constraints on insertion order |
> | **min ≥ 1 on either side of M:N** | the junction table cannot say the entity must appear in it | triggers / `CHECK` with a subquery (assertions) |
> | **bounded max = $k>1$** (e.g. a student takes at most 5 courses, (0,5)) | no declarative "at most $k$ rows per key" in plain SQL keys | trigger, `CHECK` with subquery/assertion, or application code |
> | **min and max both > 1, e.g. (2,5)** (a team has 2–5 officers) | neither bound is expressible by keys | trigger / assertion enforcing both bounds; may also require deferred checking |
> | **Ternary or higher-degree** relationships with mixed (min,max) | one table with composite key, but the max-1 side makes the key *smaller* (e.g. (1,1) on one entity ⇒ other two entities' keys form the PK) | PK choice encodes the max=1; min and bounded max again need triggers |
>
> **Example (employee–department):** `WORKS_FOR` with `EMPLOYEE (1,1)` and `DEPARTMENT (0,N)`.
> ```sql
> CREATE TABLE Employee (
>   emp_id  INT PRIMARY KEY,
>   name    VARCHAR(50),
>   dept_id INT NOT NULL,                       -- min = 1  →  NOT NULL
>   FOREIGN KEY (dept_id) REFERENCES Department(dept_id)  -- max = 1  →  single FK column
> );
> ```
> `DEPARTMENT (0,N)` needs nothing at all — no constraint for "0 or more". If it were `DEPARTMENT (1,N)`, we would need a trigger/assertion (every department must have at least one employee).
>
> **Key takeaways:**
> 1. **max = 1** ⇒ FK/`UNIQUE` (declarative); **max = N** ⇒ FK on the many side or a junction table.
> 2. **min = 0** ⇒ nullable (nothing to enforce); **min = 1 on the referencing (FK-holding) side** ⇒ `NOT NULL`.
> 3. **min ≥ 1 on the referenced side** and **bounded max > 1** can't be expressed with keys — use triggers, assertions or the application.
>
> > [!tip] Exam pointer
> > Organise the answer as "*what translates cleanly (0/1/N with FK, NOT NULL, UNIQUE, junction table)* vs *what needs triggers/assertions (min on the referenced side, bounded max)*". The `NOT NULL` for min=1 and nullable for min=0 line is the one markers look for.

> [!question] Q11: Armstrong's axioms proofs (10M)
> Prove the following using the set of sound and complete Armstrong's inference rules:
> a) $\{X\to YZ\}\models\{X\to Y\}$;
> b) $\{X\to Y,\ X\to Z\}\models\{X\to YZ\}$;
> c) $\{X\to Y,\ WY\to Z\}\models\{WX\to Z\}$.
>
> > [!info]- Theory: Armstrong's axioms (click to expand)
> > For attribute sets $X,Y,Z,W$ over a relation $R$:
> >
> > 1. **Reflexivity (IR1):** if $Y\subseteq X$ then $X\to Y$. *(trivial FDs)*
> > 2. **Augmentation (IR2):** if $X\to Y$ then $XZ\to YZ$ for any $Z$.
> > 3. **Transitivity (IR3):** if $X\to Y$ and $Y\to Z$ then $X\to Z$.
> >
> > These are **sound** (they derive only FDs that truly hold in every relation satisfying the given FDs) and **complete** (every FD implied by a set $F$ can be derived using them: $F^+$ is exactly what the rules generate). Derived rules (all provable from the three above): **Union** (the content of (b)), **Decomposition** (the content of (a)), **Pseudotransitivity** (the content of (c)). We prove each from the three basic rules only.
>
> ### (a) $\{X\to YZ\}\models\{X\to Y\}$ — Decomposition
>
> | Step | Statement | Reason |
> | --- | --- | --- |
> | 1 | $X\to YZ$ | Given |
> | 2 | $YZ\to Y$ | Reflexivity ($Y\subseteq YZ$) |
> | 3 | $X\to Y$ | Transitivity on 1 and 2 |
>
> $\square$
>
> ### (b) $\{X\to Y,\ X\to Z\}\models\{X\to YZ\}$ — Union
>
> | Step | Statement | Reason |
> | --- | --- | --- |
> | 1 | $X\to Y$ | Given |
> | 2 | $X\to Z$ | Given |
> | 3 | $XX\to XY$, i.e. $X\to XY$ | Augmentation of 1 with $X$ (note $XX=X$ as a set) |
> | 4 | $XY\to YZ$ | Augmentation of 2 with $Y$ |
> | 5 | $X\to YZ$ | Transitivity on 3 and 4 |
>
> $\square$
>
> ### (c) $\{X\to Y,\ WY\to Z\}\models\{WX\to Z\}$ — Pseudotransitivity
>
> | Step | Statement | Reason |
> | --- | --- | --- |
> | 1 | $X\to Y$ | Given |
> | 2 | $WY\to Z$ | Given |
> | 3 | $WX\to WY$ | Augmentation of 1 with $W$ |
> | 4 | $WX\to Z$ | Transitivity on 3 and 2 |
>
> $\square$
>
> **Sanity check with attribute closure** (an independent verification, not a replacement for the proof): in (c), start with $\{W,X\}^+$ under $F=\{X\to Y,\ WY\to Z\}$: $\{W,X\}\to$ add $Y$ (by $X\to Y$) $\to\{W,X,Y\}\to$ add $Z$ (by $WY\to Z$) $=\{W,X,Y,Z\}\ni Z$ ✔. In (b): $X^+=\{X,Y,Z\}\supseteq YZ$ ✔. In (a): $X^+\supseteq\{Y,Z\}\ni Y$ ✔.
>
> > [!tip] Exam pointer
> > Prove each using **only** the three primitive rules, naming the rule on every line. The standard moves: **(a)** reflexivity then transitivity; **(b)** augment *each* FD by the *other* side's attribute set, then chain with transitivity; **(c)** augment the first FD by $W$ and chain. Don't just cite "union/decomposition/pseudotransitivity" — the question asks you to *prove* them.
