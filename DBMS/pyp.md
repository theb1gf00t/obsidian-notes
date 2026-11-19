---
title: DBMS — Previous Year Question Paper
tags:
  - dbms
  - pyp
---

# DBMS — Previous Year Question Paper

*Source: [[prev_year.pdf]] — Max Marks: 100, Max Time: 180 Min.*

> [!question] Q1: Normalization — relational schema design (40M)
> Apply efficient algorithms (Normalization) to the following user requirements to generate a relational schema from a universal relation for the following requirements — Governor of a fictional state wanted a portal for a crime management system with the clearly illustrated. The relational schema should be in 3NF/BCNF. All the steps should be followed.
>
> Every police officer will be listed in the portal along with the details like empid, name, designation, DoJ, DoB, office address, latest photo etc. Every district will have a Deputy Commissioner of Police responsible for completing all the investigations within the district. All the Deputy Commissioners will report to the Commissioner of Police, who is responsible for completing all the investigations in the state.
>
> A user can register in the portal with details like name, mobile number, address, etc. After registration, a user can file a complaint, and the complaint will be assigned by the Deputy Commissioner to a Team of 2 to 5 Police officers, depending on the gravity of the complaint/crime. The senior officer will lead the Team. Every Team is identified with an ID, and it has a contact no, email, etc. The Team will resolve every complaint within 15 days. Every case/complaint will have a unique case file maintained by the Team with the details of the complainant, accused and progress. The details (name, age, gender, DoB, Biometrics, etc.) of every accused are stored, and an accused is uniquely identifiable. Every Police officer is assigned at most ten cases in a month.
>
> All the Police officers within a district report to the senior officer in the Deputy Commissioner of Police. The Deputy Commissioner will monitor every case filed by the user. The senior officer will finalize the investigation report after he/she is satisfied with it. During this stage, if it is felt that the investigation is lacking in a few aspects, then a larger team will be constituted by the Deputy Commissioner to reinvestigate the complaint. After a satisfactory report from the Team, the Deputy Commissioner will approve the report, and it will be available for the user. If the user is satisfied with the report, the Team will file the case in court, and the court will give the final judgment within 15 days.
>
> The court will hear the case on a daily basis. Each court is uniquely identified and has an address, phone number, etc. Both the parties will be represented by the lawyers. A lawyer has a name, DoB, address, etc., stored in the portal. A lawyer can be associated with many courts. If the court convicts the accused as reported by the Team, then the entire Team will be rewarded for conducting a foolproof investigation in accordance with the law.
>
> *NOTE: All the attributes are not mentioned in the description — you are expected to identify at least a few of them.*

> [!question] Q2: Lossless vs. dependency-preserving decomposition (10M)
> Prove or disprove the following statements:
> a) If a decomposition is lossless then it will always preserve the dependencies.
> b) If a decomposition is dependency preserving then it will always be lossless.
>
> > [!info]- Theory: lossless-join and dependency-preserving tests (click to expand)
> > **Lossless-join test** (for a binary decomposition of $R$ into $R_1, R_2$ with FD set $F$): the decomposition is lossless iff
> > $$ (R_1 \cap R_2) \to R_1 \quad \text{or} \quad (R_1 \cap R_2) \to R_2 $$
> > i.e. the common attributes must functionally determine *all* attributes of at least one of the two pieces (the common attributes form a superkey of one side).
> >
> > **Dependency preservation test**: let $F_i$ be the projection of $F$ onto $R_i$ (every FD in $F^+$ that uses only attributes of $R_i$). The decomposition is dependency-preserving iff
> > $$ (F_1 \cup F_2 \cup \dots \cup F_n)^+ = F^+ $$
> > i.e. every original FD can be verified from the projected FDs alone, without needing a join. If some FD in $F$ is not implied by the union of the projected sets, the decomposition is **not** dependency-preserving — enforcing that FD would require joining the relations back together at write time, which is expensive.
> >
> > These two properties are **independent** of each other — a decomposition can have either, both, or neither.
>
> **(a) Disproof — lossless does NOT always imply dependency-preserving.**
>
> Counterexample: $R(A,B,C)$ with $F = \{AB \to C,\ C \to B\}$. Decompose into $R_1(A,C)$ and $R_2(B,C)$.
>
> *Lossless-join check*: $R_1 \cap R_2 = \{C\}$. Since $C \to B$ is given, $C \to BC$ (trivially adding $C$), so $C$ functionally determines all of $R_2$. Hence $(R_1\cap R_2) \to R_2$ holds — **the decomposition is lossless**.
>
> *Dependency-preservation check*: project $F$ onto each piece.
> - $F_1$ (on $\{A,C\}$): no non-trivial FD of $F$ involves only $A,C$, so $F_1 = \varnothing$.
> - $F_2$ (on $\{B,C\}$): $C \to B$ survives, so $F_2 = \{C \to B\}$.
>
> Take the closure of $AB$ under $F_1 \cup F_2 = \{C \to B\}$: $AB^+ = \{A,B\}$ (the rule $C\to B$ cannot fire since $C$ is not yet known). So $AB \to C$ is **not** derivable from $F_1 \cup F_2$, even though it was a dependency of the original $F$. The original FD $AB\to C$ is lost — it can only be checked by joining $R_1$ and $R_2$ back together.
>
> $\therefore$ this decomposition is lossless but **not** dependency-preserving. **Statement (a) is disproved.**
>
> **(b) Disproof — dependency-preserving does NOT always imply lossless.**
>
> Counterexample: $R(A,B,C,D)$ with $F = \{A \to B,\ C \to D\}$ (two FDs on disjoint attribute sets). Decompose into $R_1(A,B)$ and $R_2(C,D)$.
>
> *Dependency-preservation check*: $F_1$ (on $\{A,B\}$) $= \{A\to B\}$, $F_2$ (on $\{C,D\}$) $= \{C \to D\}$. $F_1 \cup F_2 = \{A\to B,\ C\to D\} = F$ exactly, so trivially $(F_1\cup F_2)^+ = F^+$ — **the decomposition is dependency-preserving**.
>
> *Lossless-join check*: $R_1 \cap R_2 = \varnothing$. An empty attribute set can never be a superkey of anything (it would have to functionally determine every attribute of $R_1$ or $R_2$, which is impossible for $\varnothing$ unless the relation is trivial). So neither $(R_1\cap R_2)\to R_1$ nor $(R_1\cap R_2)\to R_2$ holds — **the lossless-join test fails**. Concretely, $R_1 \bowtie R_2$ degenerates to a Cartesian product, which reintroduces spurious tuples not present in the original $R$ (e.g. every $A,B$ pairs with every $C,D$ regardless of which tuples actually co-occurred).
>
> $\therefore$ this decomposition is dependency-preserving but **not** lossless. **Statement (b) is disproved.**
>
> > [!tip] Exam pointer
> > Both directions fail — lossless-join and dependency-preservation are **independent properties**. A good decomposition algorithm (e.g. 3NF synthesis) aims to guarantee *both simultaneously*, but BCNF decomposition can sacrifice dependency preservation to guarantee losslessness.

> [!question] Q3: Query optimization — relational algebra steps (12M)
> Apply query optimization on the following expression and illustrate **all the steps**:
>
> `<select p.empId, p.name, p.phone from professor p, teaching t, enrollment e where e.rollNo = "CS22B999" and e.year = 2024 and e.courseId = t.courseId and e.sem = "even" and e.empId = t.empId> (2024 and t.sem = "even")`
>
> *(Note: expression as printed in the paper — condition clauses split across the line break: `e.rollNo = "CS22B999"` and `e.year = 2024` and `e.courseId = t.courseId` and `e.sem = "even"` and `t.sem = "even"` and `t.year = 2024` and `p.empId = t.empId`.)*
>
> > [!info]- Theory: heuristic query optimization rules (click to expand)
> > Heuristic (rule-based) optimization rewrites a relational-algebra expression tree using algebraic equivalences that are *always* beneficial, without needing cost estimates. The standard rule set:
> >
> > 1. **Split conjunctive selections**: $\sigma_{\theta_1 \land \theta_2}(E) \equiv \sigma_{\theta_1}(\sigma_{\theta_2}(E))$ — break one big filter into independent selections so each can move separately.
> > 2. **Selection pushdown**: commute $\sigma$ with $\bowtie$, $\times$, $\cup$ to move each selection as close to its source relation (leaf) as possible — $\sigma_\theta(E_1 \bowtie E_2) \equiv \sigma_\theta(E_1) \bowtie E_2$ when $\theta$ only references $E_1$'s attributes. This shrinks relations before any join.
> > 3. **Reorder joins**: use commutativity ($E_1\bowtie E_2 \equiv E_2\bowtie E_1$) and associativity of $\bowtie$ so the most restrictive join/selection executes first, minimizing intermediate result sizes.
> > 4. **Combine Cartesian product + selection into a join**: $\sigma_\theta(E_1\times E_2) \equiv E_1\bowtie_\theta E_2$, since a join is evaluated far more efficiently than a blind Cartesian product followed by a filter.
> > 5. **Projection pushdown**: push $\Pi$ down as far as possible, and split it like selections, keeping at each step only the attributes needed by an operation above it.
> > 6. **Common subexpression elimination**: identify repeated subexpressions and evaluate once, reusing the result.
> >
> > The goal at every step is the same: **reduce the size of intermediate relations as early as possible**, since join/product cost scales with the sizes of its operands.
>
> **Step 0 — write the initial expression as a relational-algebra tree.**
>
> The query (plain English): "Phone numbers, names, employee IDs of professors who teach a course that a specific student (CS22B999) is enrolled in, during the even semester of 2024."
>
> $$ \Pi_{p.empId,\ p.name,\ p.phone}\Big(\sigma_{\theta}\big(professor \times teaching \times enrollment\big)\Big) $$
>
> where $\theta$ is the full conjunction:
> $$ e.rollNo = \text{"CS22B999"} \land e.year = 2024 \land e.sem = \text{"even"} \land t.year = 2024 \land t.sem = \text{"even"} \land e.courseId = t.courseId \land p.empId = t.empId $$
>
> **Step 1 — split the conjunctive selection** into individual selections (rule 1), one per atomic condition:
>
> $$ \sigma_{e.rollNo = \text{"CS22B999"}}, \quad \sigma_{e.year=2024}, \quad \sigma_{e.sem=\text{"even"}}, \quad \sigma_{t.year=2024}, \quad \sigma_{t.sem=\text{"even"}}, \quad \sigma_{e.courseId=t.courseId}, \quad \sigma_{p.empId=t.empId} $$
>
> **Step 2 — classify each selection by which relation(s) it touches:**
>
> | Condition | Relation(s) touched | Type |
> | --- | --- | --- |
> | $e.rollNo = \text{"CS22B999"}$ | `enrollment` only | single-relation → push to leaf |
> | $e.year = 2024$ | `enrollment` only | single-relation → push to leaf |
> | $e.sem = \text{"even"}$ | `enrollment` only | single-relation → push to leaf |
> | $t.year = 2024$ | `teaching` only | single-relation → push to leaf |
> | $t.sem = \text{"even"}$ | `teaching` only | single-relation → push to leaf |
> | $e.courseId = t.courseId$ | `enrollment`, `teaching` | join condition |
> | $p.empId = t.empId$ | `professor`, `teaching` | join condition |
>
> **Step 3 — push single-relation selections down to their source leaf** (rule 2). Each lands directly on the relation it filters, shrinking it before any join:
>
> $$ \sigma_{rollNo=\text{"CS22B999"} \,\land\, year=2024 \,\land\, sem=\text{"even"}}(enrollment) \rightarrow \text{call this } E' $$
> $$ \sigma_{year=2024 \,\land\, sem=\text{"even"}}(teaching) \rightarrow \text{call this } T' $$
> $$ professor \rightarrow \text{no applicable selection, stays as-is} $$
>
> $E'$ is now a tiny relation — at most one row, since `rollNo` is a key-like filter on a single student's enrollment in one semester/year.
>
> **Step 4 — combine the remaining Cartesian products with their selections into joins** (rule 4). The two join conditions become natural joins:
>
> $$ E' \bowtie_{e.courseId = t.courseId} T' \quad\longrightarrow\quad \text{call this } ET $$
> $$ ET \bowtie_{p.empId = t.empId} professor $$
>
> **Step 5 — reorder the joins so the smallest relation is joined first** (rule 3). Since $E'$ is already filtered down to (at most) one tuple, join $E'$ with $T'$ **before** bringing in `professor` — this keeps every intermediate relation as small as possible, which is exactly what the tree above already does (join order: $E' \bowtie T'$ first, result joined with `professor` last).
>
> **Step 6 — push the final projection down** (rule 5). We only need $p.empId, p.name, p.phone$ at the very end, but the join conditions need $t.empId, t.courseId, e.courseId$ along the way. Push partial projections onto each branch so only the columns needed downstream are carried:
>
> $$ \Pi_{e.courseId}(E') \quad\quad \Pi_{t.courseId,\ t.empId}(T') \quad\quad \Pi_{p.empId,\ p.name,\ p.phone}(professor) $$
>
> and apply the final $\Pi_{p.empId, p.name, p.phone}$ only at the very top, after the last join.
>
> **Final optimized expression tree** (leaves at the bottom, most restrictive filter applied earliest):
>
> ```
>                         Π p.empId, p.name, p.phone
>                                    |
>                         ⋈ (p.empId = t.empId)
>                        /                        \
>              ⋈ (e.courseId = t.courseId)      professor
>             /                            \
>   σ rollNo="CS22B999"              σ year=2024 ∧ sem="even"
>   ∧ year=2024 ∧ sem="even"                   |
>             |                             teaching
>        enrollment
> ```
>
> > [!tip] Exam pointer
> > The two things examiners check: (1) did you **split** the conjunction before pushing (never push a multi-relation condition as one block), and (2) did you push every single-relation filter all the way to its own leaf *before* any join, not after. The join order (smallest/most-filtered relation first) is the secondary optimization — mention it but the selection/projection pushdown is the core of the "all the steps" instruction.

> [!question] Q4: View and conflict serializability (12M)
> Explain View and Conflict Serializability with the help of four transactions (each with at least three valid instructions) on two data items (X and Y), and by using the same requirements, answer the following questions:
> a) Give a schedule that is conflict serializable (justify using precedence graph).
> b) Give a schedule that is not conflict serializable (justify using precedence graph).
>
> > [!info]- Theory: conflicting instructions, conflict serializability, view serializability (click to expand)
> > **Conflicting instructions.** Two instructions $I_i$ (from $T_i$) and $I_j$ (from $T_j$, $i\ne j$) **conflict** iff they operate on the **same data item** and **at least one of them is a write**. Two reads never conflict (reading never changes anything, so their relative order is irrelevant).
> >
> > **Conflict equivalence.** Schedule $S$ is conflict-equivalent to schedule $S'$ (same transactions, same instructions) if $S$ can be transformed into $S'$ by repeatedly swapping two *consecutive, non-conflicting* instructions belonging to different transactions. Swapping non-conflicting instructions never changes the final result or the value any instruction reads, so conflict-equivalent schedules are guaranteed to behave identically.
> >
> > **Conflict serializable.** $S$ is conflict serializable iff it is conflict-equivalent to *some* serial schedule.
> >
> > **Precedence graph test.** Build a graph with one node per transaction. Draw $T_i \to T_j$ whenever some instruction of $T_i$ conflicts with, and comes *before*, some instruction of $T_j$ in $S$. **$S$ is conflict serializable iff this graph is acyclic**; any topological sort of the acyclic graph gives an equivalent serial order.
> >
> > **View serializability** (strictly weaker — a superset of conflict-serializable schedules). $S$ is view-equivalent to serial schedule $S'$ iff, for every data item $Q$:
> > 1. If $T_i$ reads the *initial* value of $Q$ in $S$, $T_i$ must also read the initial value of $Q$ in $S'$.
> > 2. If $T_i$ reads the value of $Q$ *written by* $T_j$ in $S$, the same must hold in $S'$.
> > 3. The transaction that performs the **final write** on $Q$ in $S$ must also perform the final write on $Q$ in $S'$.
> >
> > $S$ is view serializable iff it's view-equivalent to some serial schedule. Every conflict-serializable schedule is view-serializable, but not every view-serializable schedule is conflict-serializable — the gap is schedules containing **blind writes** (a write not preceded by a read of the same item in that transaction), which can satisfy the three view conditions while still producing a cyclic precedence graph under the conflict test.
>
> **Setup — four transactions on data items $X, Y$:**
>
> | Transaction | Instructions (in program order) |
> | --- | --- |
> | $T_1$ | read($X$); write($X$); write($Y$) |
> | $T_2$ | read($Y$); read($X$); write($Y$) |
> | $T_3$ | write($X$); read($Y$); write($Y$) |
> | $T_4$ | read($X$); read($Y$); write($X$) |
>
> **(a) A conflict serializable schedule $S_1$:**
>
> | Step | $T_1$ | $T_2$ | $T_3$ | $T_4$ |
> | --- | --- | --- | --- | --- |
> | 1 | read($X$) | | | |
> | 2 | | read($Y$) | | |
> | 3 | write($X$) | | | |
> | 4 | | read($X$) | | |
> | 5 | | | write($X$) | |
> | 6 | write($Y$) | | | |
> | 7 | | write($Y$) | | |
> | 8 | | | read($Y$) | |
> | 9 | | | write($Y$) | |
> | 10 | | | | read($X$) |
> | 11 | | | | read($Y$) |
> | 12 | | | | write($X$) |
>
> *Conflict pairs present in $S_1$ (same item, $\ge1$ write, different transactions):*
> - $T_1.\text{write}(X)$ (step 3) before $T_2.\text{read}(X)$ (step 4) $\Rightarrow T_1 \to T_2$
> - $T_1.\text{write}(X)$ (step 3) before $T_3.\text{write}(X)$ (step 5) $\Rightarrow T_1 \to T_3$
> - $T_2.\text{read}(X)$ (step 4) before $T_3.\text{write}(X)$ (step 5) $\Rightarrow T_2 \to T_3$
> - $T_1.\text{write}(Y)$ (step 6) before $T_2.\text{write}(Y)$ (step 7) $\Rightarrow T_1 \to T_2$ (duplicate edge, already have it)
> - $T_2.\text{write}(Y)$ (step 7) before $T_3.\text{write}(Y)$ (step 9) $\Rightarrow T_2 \to T_3$ (duplicate)
> - $T_3.\text{write}(X)$ (step 5) before $T_4.\text{read}(X)$ (step 10) $\Rightarrow T_3 \to T_4$
> - $T_3.\text{write}(Y)$ (step 9) before $T_4.\text{read}(Y)$ (step 11) $\Rightarrow T_3 \to T_4$ (duplicate)
> - $T_3.\text{write}(X)$ (step 5) before $T_4.\text{write}(X)$ (step 12) $\Rightarrow T_3 \to T_4$ (duplicate)
>
> **Precedence graph for $S_1$:** edges $T_1\to T_2$, $T_1 \to T_3$, $T_2 \to T_3$, $T_3 \to T_4$ — draw this as a DAG:
>
> ```
>   T1 ──► T2
>    │      │
>    ▼      ▼
>   T3 ────►
>    │
>    ▼
>   T4
> ```
>
> No cycle exists (all edges point "forward": $T_1\to T_2\to T_3\to T_4$ with the extra $T_1\to T_3$ shortcut consistent with the same order). **The graph is acyclic ⇒ $S_1$ is conflict serializable**, equivalent to the serial order $T_1, T_2, T_3, T_4$ (one valid topological sort).
>
> **(b) A schedule that is NOT conflict serializable, $S_2$:**
>
> | Step | $T_1$ | $T_2$ | $T_3$ | $T_4$ |
> | --- | --- | --- | --- | --- |
> | 1 | read($X$) | | | |
> | 2 | | | write($X$) | |
> | 3 | write($X$) | | | |
> | 4 | | read($Y$) | | |
> | 5 | | | | read($X$) |
> | 6 | write($Y$) | | | |
> | 7 | | | | read($Y$) |
> | 8 | | read($X$) | | |
> | 9 | | | read($Y$) | |
> | 10 | | write($Y$) | | |
> | 11 | | | write($Y$) | |
> | 12 | | | | write($X$) |
>
> *Conflict pairs present in $S_2$:*
> - $T_3.\text{write}(X)$ (step 2) before $T_1.\text{write}(X)$ (step 3) $\Rightarrow T_3 \to T_1$
> - $T_1.\text{write}(X)$ (step 3) before $T_4.\text{read}(X)$ (step 5) $\Rightarrow T_1 \to T_4$
> - $T_1.\text{write}(X)$ (step 3) before $T_2.\text{read}(X)$ (step 8) $\Rightarrow T_1 \to T_2$
> - $T_1.\text{write}(X)$ (step 3) before $T_4.\text{write}(X)$ (step 12) $\Rightarrow T_1 \to T_4$ (duplicate)
> - $T_1.\text{write}(Y)$ (step 6) before $T_2.\text{write}(Y)$ (step 10) $\Rightarrow T_1 \to T_2$ (duplicate)
> - $T_1.\text{write}(Y)$ (step 6) before $T_3.\text{read}(Y)$ (step 9) $\Rightarrow T_1 \to T_3$
> - $T_1.\text{write}(Y)$ (step 6) before $T_4.\text{read}(Y)$ (step 7) $\Rightarrow T_1 \to T_4$ (duplicate)
> - $T_1.\text{write}(Y)$ (step 6) before $T_3.\text{write}(Y)$ (step 11) $\Rightarrow T_1 \to T_3$ (duplicate)
> - $T_4.\text{read}(X)$ (step 5) before $T_4.\text{write}(X)$... same transaction, not counted.
> - $T_2.\text{read}(X)$ (step 8) before $T_4.\text{write}(X)$ (step 12) $\Rightarrow T_2 \to T_4$
> - $T_2.\text{write}(Y)$ (step 10) before $T_3.\text{write}(Y)$ (step 11) $\Rightarrow T_2 \to T_3$
>
> **Precedence graph for $S_2$:** edges $T_3\to T_1$, $T_1\to T_4$, $T_1\to T_2$, $T_1\to T_3$, $T_2\to T_4$, $T_2 \to T_3$.
>
> Notice **both** $T_3 \to T_1$ **and** $T_1 \to T_3$ are present (the first from $T_3.\text{write}(X)$ step 2 preceding $T_1.\text{write}(X)$ step 3; the second from $T_1.\text{write}(Y)$ step 6 preceding $T_3.\text{read}(Y)$/$\text{write}(Y)$ steps 9/11) — a direct **2-cycle** between $T_1$ and $T_3$:
>
> ```
>   T1 ──► T3
>    ▲      │
>    └──────┘
> ```
>
> **The graph has a cycle ($T_1 \to T_3 \to T_1$) ⇒ $S_2$ is NOT conflict serializable.** No topological order can satisfy both edges simultaneously — $T_1$ would need to run both before and after $T_3$, which is impossible in any serial schedule.
>
> > [!tip] Exam pointer
> > To *construct* a non-conflict-serializable schedule quickly: pick two transactions that both write the same item, and interleave them so each one's write happens before the other's conflicting access on a *different* shared item — that guarantees opposite-direction edges and a 2-cycle, the simplest possible violation. For the conflict-serializable schedule, the safest construction is to keep every transaction's own instructions in order and ensure all cross-transaction conflicts happen to line up consistently in one direction (here, $T_1\to T_2\to T_3\to T_4$).

> [!question] Q5: B+ tree insertion and deletion (14M)
> Assume that block pointer and record pointer are of the same size, order $m$ is 3 and $m_{leaf}$ is 2. Insert the following elements into a B+ tree (one illustration for each insertion): 70, 19, 22, 3, 19, 17, 2, 83, 11, 39, 94, 69 and 61.
>
> Followed by delete the elements till a **level drop** (one illustration for each deletion).

> [!question] Q6: Weak entity vs. composite multi-valued attribute (10M)
> Discuss with an illustration the design choice between a weak entity and a composite multi-valued attribute.
>
> *(Marginal note in paper: "Go with illustration. ERD should be given pictorially.")*
>
> > [!info]- Theory: weak entities and multivalued attributes (click to expand)
> > **Weak entity type.** An entity type with **no key attribute of its own** sufficient to uniquely identify its instances. It is *existence-dependent* on another entity type, called the **identifying (owner) entity**, through an **identifying relationship** — typically 1:N from owner to weak entity, with **total participation** of the weak entity (it cannot exist in the database without its owner). It has a **partial key (discriminator)**: an attribute that is unique only *among the entities owned by the same owner*, not globally unique.
> >
> > *Chen notation*: a weak entity is a **double-outlined rectangle**; its identifying relationship is a **double-outlined diamond**; its partial key is **underlined with a dashed line** (vs. a solid underline for a normal key).
> >
> > **Composite multivalued attribute.** An attribute of an entity that is simultaneously:
> > - **multivalued** — a single entity instance can have several values of it (drawn as a double-outlined oval), and
> > - **composite** — it decomposes further into sub-attributes (e.g. an address breaking into Street, City, State).
> >
> > It remains purely descriptive data belonging to its owning entity: it has no independent key of its own that matters to the schema, and nothing else in the database ever needs to reference *one specific instance* of it directly.
> >
> > **The design question.** Both model "a set of records, each with several fields, that belong to one owner entity" — e.g. the dependents of an employee. The choice depends on whether that sub-data has **significance and connections of its own**, or is **purely descriptive**.
>
> **Standard example: Dependents of an Employee**
>
> Scenario: each `EMPLOYEE` can have several dependents, each with a `Name`, `BirthDate`, and `Relationship` (spouse, child, etc.).
>
> **Option A — model `DEPENDENT` as a weak entity.**
>
> ```
> ┌──────────────┐        ┌═══════════════┐       ╔═══════════════╗
> │   EMPLOYEE   │        ║ DEPENDENTS_OF ║══════▶║   DEPENDENT    ║
> │ ssn (key)    │───────▶║  (identifying ║  1    ║ name (partial  ║
> │ name         │   1    ║  relationship)║   N   ║  key, dashed-  ║
> │ salary       │        ╚═══════════════╝       ║  underlined)   ║
> └──────────────┘                                 ║ birthdate      ║
>                                                   ║ relationship   ║
>                                                   ╚═══════════════╝
> ```
> *(Double-outlined rectangle = weak entity `DEPENDENT`; double-outlined diamond = identifying relationship `DEPENDENTS_OF`; `name` is dashed-underlined as the partial key — unique only within one employee's dependents, e.g. two different employees can each have a dependent named "Alex", but one employee cannot have two dependents both named "Alex".)*
>
> Chosen when dependents need to be **individually referenced or related elsewhere** — e.g. an `INSURANCE_CLAIM` entity that references a *specific* dependent, dependents who themselves enroll in a benefits plan, or reports that query dependents independently of employees. The relational mapping gives `DEPENDENT` its own table: `DEPENDENT(EmployeeSSN, Name, BirthDate, Relationship)` with `(EmployeeSSN, Name)` as its composite primary key (owner key + partial key) and `EmployeeSSN` as a foreign key to `EMPLOYEE`.
>
> **Option B — model dependents as a composite multivalued attribute of `EMPLOYEE`.**
>
> ```
>                         ╭──────────────╮
>                         │  Dependents   │  (composite, multivalued —
> ┌──────────────┐        ╰──────┬───────╯   double-outlined oval)
> │   EMPLOYEE   │               │
> │ ssn (key)    │───────────────┤
> │ name         │        ┌──────┴──────┬─────────────┐
> │ salary       │        │             │             │
> └──────────────┘      Name        BirthDate     Relationship
>                     (sub-attr)    (sub-attr)      (sub-attr)
> ```
> *(The oval `Dependents` is double-outlined for multivalued, and itself branches into three single-valued sub-attribute ovals — composite. No identifying relationship, no discriminator: this is pure attribute structure on `EMPLOYEE`, not a separate entity.)*
>
> Chosen when dependent data is **purely descriptive** — recorded only for reference on the employee's record (e.g. for tax forms), never queried or related to independently. At the relational level this still ends up materialized as a separate table (multivalued composite attributes cannot sit inside a single 1NF row), but conceptually and in the ER diagram it carries no independent identity or discriminator — it's "data about the employee," not "a thing in its own right."
>
> **Trade-off summary**
>
> | Criterion | Weak entity | Composite multivalued attribute |
> | --- | --- | --- |
> | Needs its own relationships to other entities | Yes → weak entity | No → attribute |
> | Has several attributes with independent semantic weight | Yes → weak entity | No, just descriptive fields |
> | Needs a discriminator to disambiguate individual instances | Yes → weak entity | Not modeled explicitly |
> | Purely descriptive, self-contained, never referenced elsewhere | — | Yes → attribute |
> | Relational mapping | Separate table, owner-key + partial-key as PK, FK to owner | Separate table anyway (1NF), but no explicit discriminator concept at ER level |
>
> > [!tip] Exam pointer
> > The decisive question to lead the answer with: *"does anything else in the schema need to point at one specific instance of this sub-data?"* If yes → weak entity (it needs its own identity, even if only a partial one). If no, and it's just a descriptive bundle of fields → composite multivalued attribute. Always mention that both converge to a similar table under relational mapping — the real difference is **conceptual modeling intent**, not final storage.

> [!question] Q7: Unsafe TRC expression (2M)
> Give an example of an unsafe TRC expression.
