---
title: DBMS — Previous Year Question Paper 3
tags:
  - dbms
  - pyp
---

# DBMS — Previous Year Question Paper 3

*Source: [[prev_yr3.pdf]] — CSE361: Database Management System, End-Semester Exam, V Sem — Max Marks: 100, Max Time: 180 Min.*

*Companion papers: [[pyp]], [[pyp2]].*

| Q | Topic | Marks |
| --- | --- | --- |
| 1 | Normalization — Crime Branch relational schema (3NF/BCNF) | 45 |
| 2 | ERD (with assumptions) + ER → relational mapping | 25 |
| 3 | Nested-loop join cost + which attribute to index | 10 |
| 4 | View vs conflict serializability (5 transactions) | 10 |
| 5 | B+ tree insertion and deletion | 10 |

---

> [!question] Q1: Normalization — Crime Branch relational schema (45M)
> Apply efficient algorithms (Normalization) to generate a relational schema for the following user requirements. The relational schema should be in 3NF/BCNF. All the steps should be clearly illustrated.
>
> **Requirements (condensed from the paper):**
> - Every crime is investigated by the **crime branch**: a **head office** (director, officers, technical / non-technical staff) and **branches** (deputy director, officers, technical / non-technical staff). Staff have name, employee ID, address, contact number, etc.
> - A **victim/user registers a crime** through an online portal with **OTP verification**. Relevant documents (medical reports, call records, …) can be uploaded and are stored. User details: Aadhaar number, DoB, name, address, etc.
> - A **unique complaint ID** is generated; date of registration, branch assigned, etc. are stored. Each document is identified through the complaint. The **head office assigns a branch** within a day.
> - The **branch assigns** **one officer + two technical + one non-technical staff** to the complaint. An officer gets **at most four weeks** per case and is on **at most five cases** at any time.
> - The user can **check progress** and give **suggestions (online/offline)**. If unsatisfied, the user can **appeal** with reasoning; if the **deputy director** finds it convincing, the case is **re-investigated by a new team**. A case is investigated within **eight weeks** (even with re-investigation).
> - After the investigation the case is **filed in the crime branch court**; the court gives the **verdict within four weeks and at most ten hearings**. Each **hearing is logged** and available to the press and user.
> - Every crime branch has **three lawyers** (name, contact details, associated cases, …). The user can give suggestions to / contact the lawyers. The system stores **all suggestions** given to officers and lawyers.
> - Every crime branch has a **PRO** who briefs the press; **every press note** about a crime is stored.
> - An officer/lawyer with a **success rate below 75 %** (w.r.t. court verdict) is **terminated**.
>
> *NOTE: All attributes are not mentioned — identify at least a few with each entity.*

> [!info]- Theory: 3NF synthesis algorithm (click to expand)
> > The "efficient algorithm" for a 3NF, lossless, dependency-preserving schema is **3NF synthesis from a canonical (minimal) cover**:
> >
> > 1. **Collect attributes and functional dependencies (FDs)** from the requirements — this gives the universal relation $U$ and the FD set $F$.
> > 2. **Compute a minimal (canonical) cover** $F_c$ of $F$:
> >    - (i) every FD has a **single attribute** on the right-hand side;
> >    - (ii) remove **extraneous attributes** from left-hand sides ($A$ in $X\to B$ is extraneous if $(X-A)\to B$ already follows from $F$);
> >    - (iii) remove **redundant FDs** (an FD derivable from the others).
> > 3. **Group** the FDs of $F_c$ by identical left-hand side: each group $X \to A_1,\dots,A_k$ becomes a relation $R_X(X, A_1,\dots,A_k)$ with key $X$.
> > 4. If **no relation contains a candidate key** of $U$, add one relation consisting of a candidate key (this guarantees the **lossless join**).
> > 5. **Drop** any relation whose attributes are a subset of another relation.
> >
> > **Guarantees:** every relation is in **3NF**, the decomposition is **dependency preserving** (every FD of $F_c$ sits inside one relation) and **lossless**.
> >
> > **BCNF test:** $R$ is in BCNF iff for every non-trivial FD $X\to A$ holding in $R$, $X$ is a superkey of $R$. 3NF relaxes this by allowing $A$ to be a *prime* attribute. If every relation produced has **only candidate keys as determinants**, the result is already in BCNF.

> [!success]- Solution (click to expand)
> > ### Step 1 — Attributes (universal relation $U$)
> >
> > | Group | Attributes |
> > | --- | --- |
> > | **Office** (head office / branch) | `OID`, `OName`, `OType` (HEAD/BRANCH), `OAddr`, `OPhone`, `MgrEID` (director / deputy director), `ProEID` (PRO of the branch) |
> > | **Employee** (director, deputy director, officer, technical, non-technical, PRO) | `EID`, `ENm`, `EAddr`, `EPhone`, `EDoB`, `ERole`, `EStatus` (ACTIVE/TERMINATED), `OID` |
> > | **User** (victim) | `AAD` (Aadhaar), `UNm`, `UDoB`, `UAddr`, `UMob`, `UVerified` (OTP done) |
> > | **Complaint** | `CID`, `CDate`, `CDesc`, `CStatus`, `AAD`, `BrID` (assigned branch), `BrAsgDate` |
> > | **Document** | `DNo`, `DType`, `DFile`, `DDate` |
> > | **Investigation round** | `INo` (1 = first, 2 = re-investigation), `IStart`, `IDue`, `IEnd`, `IProgress`, `LeadEID` (lead officer) |
> > | **Team member** | `TRole` (OFFICER/TECH/NONTECH) |
> > | **Appeal** | `AppID`, `ApReason`, `ApDate`, `ApDecision`, `DecEID` (deputy director who decided) |
> > | **Suggestion** | `SgID`, `SgMode` (ONLINE/OFFLINE), `SgText`, `SgDate`, `SgEID` (officer recipient), `SgLID` (lawyer recipient) |
> > | **Court case** | `FileDate`, `CrtID`, `Verdict` (CONVICTED/ACQUITTED), `VerdictDate` |
> > | **Court** | `CrtName`, `CrtAddr`, `CrtPhone` |
> > | **Hearing** | `HNo`, `HDate`, `HLog` |
> > | **Lawyer** | `LID`, `LNm`, `LDoB`, `LAddr`, `LPhone`, `LEmail`, `LStatus` |
> > | **Case–lawyer** | `LAsgDate` |
> > | **Press note** | `PNID`, `PNDate`, `PNText`, `PNEID` (PRO who wrote it) |
> >
> > *Role-named attributes* (`MgrEID`, `ProEID`, `LeadEID`, `DecEID`, `SgEID`, `PNEID`, `BrID`) are **copies of `EID` / `OID` in a particular role**. They are carried as plain attributes in $U$ and become **foreign keys** at the end (Step 8).
> >
> > *Derived (not stored): success rate of an officer/lawyer = convictions ÷ cases decided. It is computed by a view, and the 75 % rule is applied to it to set `EStatus` / `LStatus`.*
> >
> > ### Step 2 — Functional dependencies $F$ (from the requirements)
> >
> > | # | FD | Source in the requirements |
> > | --- | --- | --- |
> > | F1 | $OID \to OName, OType, OAddr, OPhone, MgrEID, ProEID$ | every office has one head (director / deputy director) and each branch one PRO |
> > | F2 | $EID \to ENm, EAddr, EPhone, EDoB, ERole, EStatus, OID$ | an employee works in exactly one office |
> > | F3 | $AAD \to UNm, UDoB, UAddr, UMob, UVerified$ | user details recorded once |
> > | F4 | $CID \to CDate, CDesc, CStatus, AAD, BrID, BrAsgDate$ | unique ID generated per complaint; one user, one branch |
> > | F5 | $CID, DNo \to DType, DFile, DDate$ | a document is identified *through the complaint* (weak) |
> > | F6 | $CID, INo \to IStart, IDue, IEnd, IProgress, LeadEID$ | one lead officer per round; ≤ 4 weeks per round |
> > | F7 | $CID, INo, EID \to TRole$ | role of a member in a team |
> > | F8 | $AppID \to CID, INo, ApReason, ApDate, ApDecision, DecEID$ | an appeal is against one round of one complaint |
> > | F9 | $SgID \to CID, SgMode, SgText, SgDate, SgEID, SgLID$ | each suggestion has one complaint and one recipient |
> > | F10 | $CID \to FileDate, CrtID, Verdict, VerdictDate$ | a complaint is filed in court once, one verdict |
> > | F11 | $CrtID \to CrtName, CrtAddr, CrtPhone$ | court details |
> > | F12 | $CID, HNo \to HDate, HLog$ | hearings numbered within a case (≤ 10) |
> > | F13 | $LID \to LNm, LDoB, LAddr, LPhone, LEmail, LStatus, BrID$ | a lawyer belongs to one crime branch |
> > | F14 | $CID, LID \to LAsgDate$ | lawyer representing a case |
> > | F15 | $PNID \to CID, PNEID, PNDate, PNText$ | each press note is about one case, written by one PRO |
> >
> > Rules that are **not FDs** (cardinality / time limits) are listed in Q2 as constraints enforced by triggers/`CHECK`: team = 1 officer + 2 technical + 1 non-technical; officer ≤ 5 open cases; round ≤ 4 weeks; whole case ≤ 8 weeks; verdict ≤ 4 weeks and ≤ 10 hearings; 3 lawyers per branch; success-rate ≥ 75 %.
> >
> > ### Step 3 — Minimal (canonical) cover
> >
> > **(i) Single attribute on the RHS.** Each FD above splits into one FD per RHS attribute (e.g. F4 → $CID\to CDate$, $CID\to CDesc$, …). This gives about 80 elementary FDs; they are kept *grouped by LHS* below for readability.
> >
> > **(ii) Extraneous LHS attributes.** Only the FDs with composite LHS need checking:
> >
> > | FD | Test | Result |
> > | --- | --- | --- |
> > | F5: $CID, DNo \to DType\ldots$ | $CID^+$ gives no document attribute; $DNo^+=\{DNo\}$ | nothing extraneous |
> > | F6: $CID, INo \to \ldots$ | $CID^+$ does not contain `IStart`…; $INo^+=\{INo\}$ | nothing extraneous |
> > | F7: $CID, INo, EID \to TRole$ | $\{CID,INo\}^+$, $\{CID,EID\}^+$, $\{INo,EID\}^+$ do **not** contain `TRole` (several members per round; a person can be on rounds 1 and 2 in different roles) | nothing extraneous |
> > | F12: $CID, HNo \to HDate, HLog$ | $CID^+$ lacks `HDate`; $HNo^+=\{HNo\}$ | nothing extraneous |
> > | F14: $CID, LID \to LAsgDate$ | $CID^+$, $LID^+$ lack `LAsgDate` | nothing extraneous |
> >
> > **(iii) Redundant FDs.** For each FD, remove it and recompute the closure of its LHS: no FD is re-derivable from the others. (E.g. $CID \to AAD$ and $AAD\to UNm$ give $CID\to UNm$, but $CID\to UNm$ was **never listed**, so no listed FD is redundant. `CrtID` appears only in F10/F11 and `OID` only in F2/F13 as a foreign-key style attribute, so there is no second route to derive them.)
> >
> > $\therefore$ the minimal cover $F_c$ = F1 … F15 (RHS split, grouping kept).
> >
> > ### Step 4 — Candidate key of $U$
> >
> > Attributes that **never appear on any RHS**: `DNo`, `HNo`, `EID` (as team member), `LID` (as case lawyer), `AppID`, `SgID`, `PNID`. Every other attribute is derivable from them:
> > - $AppID \to CID, INo, \ldots$ (F8); $SgID\to CID$ (F9); $PNID\to CID$ (F15) — so `CID`, `INo` come for free;
> > - from `CID`: $AAD$, `BrID`, document/investigation/case-file/hearing/lawyer facts (F4–F6, F10, F12, F14), then `CrtID`, `AAD`'s user data, etc.
> >
> > $$ K = \{AppID,\ SgID,\ PNID,\ DNo,\ HNo,\ EID,\ LID\} $$
> >
> > $K$ is long because $U$ glues many **independent 1:N / M:N facts** about one complaint into one table. This is exactly why $U$ would be a terrible table (it is not even in 4NF — massive multivalued redundancy). Synthesis breaks it apart.
> >
> > ### Step 5 — Group FDs by LHS → relations (3NF synthesis)
> >
> > | Rel. | Schema (key underlined by position — first attribute(s)) | Key |
> > | --- | --- | --- |
> > | R1 `OFFICE` | (**OID**, OName, OType, OAddr, OPhone, MgrEID, ProEID) | OID |
> > | R2 `EMPLOYEE` | (**EID**, ENm, EAddr, EPhone, EDoB, ERole, EStatus, OID) | EID |
> > | R3 `APP_USER` | (**AAD**, UNm, UDoB, UAddr, UMob, UVerified) | AAD |
> > | R4 `COMPLAINT` | (**CID**, CDate, CDesc, CStatus, AAD, BrID, BrAsgDate) | CID |
> > | R5 `DOCUMENT` | (**CID, DNo**, DType, DFile, DDate) | CID, DNo |
> > | R6 `INVESTIGATION` | (**CID, INo**, IStart, IDue, IEnd, IProgress, LeadEID) | CID, INo |
> > | R7 `TEAM_MEMBER` | (**CID, INo, EID**, TRole) | CID, INo, EID |
> > | R8 `APPEAL` | (**AppID**, CID, INo, ApReason, ApDate, ApDecision, DecEID) | AppID |
> > | R9 `SUGGESTION` | (**SgID**, CID, SgMode, SgText, SgDate, SgEID, SgLID) | SgID |
> > | R10 `CASE_FILE` | (**CID**, FileDate, CrtID, Verdict, VerdictDate) | CID |
> > | R11 `COURT` | (**CrtID**, CrtName, CrtAddr, CrtPhone) | CrtID |
> > | R12 `HEARING` | (**CID, HNo**, HDate, HLog) | CID, HNo |
> > | R13 `LAWYER` | (**LID**, LNm, LDoB, LAddr, LPhone, LEmail, LStatus, BrID) | LID |
> > | R14 `CASE_LAWYER` | (**CID, LID**, LAsgDate) | CID, LID |
> > | R15 `PRESS_NOTE` | (**PNID**, CID, PNEID, PNDate, PNText) | PNID |
> >
> > *Note on R4 vs R10:* F4 and F10 have the **same LHS** (`CID`), so pure synthesis would merge them into one relation. We deliberately **keep `CASE_FILE` separate** — a 1:1 *optional* extension of `COMPLAINT` (most complaints are not yet filed in court, so merging would fill many columns with NULL). Splitting a relation along its own key is always lossless and keeps both parts in BCNF.
> >
> > ### Step 6 — Key relation (lossless-join guarantee)
> >
> > Step 4 of the algorithm demands that some relation contains a candidate key of $U$. None of R1–R15 contains all of $K=\{AppID,SgID,PNID,DNo,HNo,EID,LID\}$, so the algorithm would add
> > $$ R_K(AppID, SgID, PNID, DNo, HNo, EID, LID). $$
> > $R_K$ only stores **meaningless cross-combinations** (e.g. one appeal × one press note × one hearing × one lawyer), because those facts are mutually independent. In practice it is **omitted**: instead we verify losslessness directly with the binary test — the relations are linked in a tree through foreign keys, and **at every join the common attribute is the key of one side**:
> >
> > | Join | Common attribute | Key of |
> > | --- | --- | --- |
> > | `COMPLAINT` ⋈ `APP_USER` | AAD | `APP_USER` |
> > | `COMPLAINT` ⋈ `OFFICE` (BrID = OID) | OID | `OFFICE` |
> > | `COMPLAINT` ⋈ {`DOCUMENT`, `INVESTIGATION`, `APPEAL`, `SUGGESTION`, `CASE_FILE`, `HEARING`, `CASE_LAWYER`, `PRESS_NOTE`} | CID | `COMPLAINT` (and a prefix of the child key) |
> > | `INVESTIGATION` ⋈ `TEAM_MEMBER` | CID, INo | `INVESTIGATION` |
> > | `TEAM_MEMBER` ⋈ `EMPLOYEE` | EID | `EMPLOYEE` |
> > | `EMPLOYEE` ⋈ `OFFICE` | OID | `OFFICE` |
> > | `CASE_FILE` ⋈ `COURT` | CrtID | `COURT` |
> > | `CASE_LAWYER` ⋈ `LAWYER` | LID | `LAWYER` |
> >
> > Every step satisfies $(R_i\cap R_j)\to R_i$ or $R_j$, so the **join is lossless**.
> >
> > ### Step 7 — Check 3NF / BCNF for every relation
> >
> > Within each relation, the only non-trivial FDs that hold are the grouped FDs whose LHS is the **primary key** (derived from F1–F15; the closure of a key adds nothing new inside a single relation because no relation contains two independent determinants).
> >
> > | Relation | Every determinant is a (candidate) key? | Normal form |
> > | --- | --- | --- |
> > | R1 `OFFICE` | OID (and `MgrEID`, if one person manages only one office, is a second candidate key — still a superkey) | **BCNF** |
> > | R2 `EMPLOYEE` | EID | **BCNF** |
> > | R3 `APP_USER` | AAD | **BCNF** |
> > | R4 `COMPLAINT` | CID (no FD like $AAD\to BrID$ exists) | **BCNF** |
> > | R5 `DOCUMENT` | (CID, DNo) | **BCNF** |
> > | R6 `INVESTIGATION` | (CID, INo) | **BCNF** |
> > | R7 `TEAM_MEMBER` | (CID, INo, EID) | **BCNF** |
> > | R8 `APPEAL` | AppID (no FD from `CID` alone to the other columns) | **BCNF** |
> > | R9 `SUGGESTION` | SgID | **BCNF** |
> > | R10 `CASE_FILE` | CID | **BCNF** |
> > | R11 `COURT` | CrtID | **BCNF** |
> > | R12 `HEARING` | (CID, HNo) | **BCNF** |
> > | R13 `LAWYER` | LID | **BCNF** |
> > | R14 `CASE_LAWYER` | (CID, LID) | **BCNF** |
> > | R15 `PRESS_NOTE` | PNID | **BCNF** |
> >
> > No transitive dependency of a non-prime attribute on a key remains: the would-be transitive chains ($CID\to AAD\to UNm$, $CID\to BrID\to OName$, $CID\to CrtID\to CrtName$, $EID\to OID\to OName$) were **broken by placing `AAD`, `OID`, `CrtID` as foreign keys** and the dependent attributes in their own relations (R3, R1, R11).
> >
> > **Dependency preservation:** every FD F1–F15 lies entirely inside one of R1–R15 ⇒ $(\bigcup F_i)^+=F^+$ ✔.
> >
> > ### Step 8 — Foreign keys (referential integrity)
> >
> > | Relation.attribute | References |
> > | --- | --- |
> > | `OFFICE.MgrEID`, `OFFICE.ProEID` | `EMPLOYEE.EID` |
> > | `EMPLOYEE.OID` | `OFFICE.OID` |
> > | `COMPLAINT.AAD` | `APP_USER.AAD` |
> > | `COMPLAINT.BrID` | `OFFICE.OID` (must be a BRANCH) |
> > | `DOCUMENT.CID` | `COMPLAINT.CID` |
> > | `INVESTIGATION.CID`, `INVESTIGATION.LeadEID` | `COMPLAINT.CID`, `EMPLOYEE.EID` |
> > | `TEAM_MEMBER.(CID,INo)`, `TEAM_MEMBER.EID` | `INVESTIGATION.(CID,INo)`, `EMPLOYEE.EID` |
> > | `APPEAL.(CID,INo)`, `APPEAL.DecEID` | `INVESTIGATION.(CID,INo)`, `EMPLOYEE.EID` (deputy director) |
> > | `SUGGESTION.CID`, `SUGGESTION.SgEID`, `SUGGESTION.SgLID` | `COMPLAINT.CID`, `EMPLOYEE.EID`, `LAWYER.LID` |
> > | `CASE_FILE.CID`, `CASE_FILE.CrtID` | `COMPLAINT.CID`, `COURT.CrtID` |
> > | `HEARING.CID` | `CASE_FILE.CID` |
> > | `LAWYER.BrID` | `OFFICE.OID` |
> > | `CASE_LAWYER.CID`, `CASE_LAWYER.LID` | `CASE_FILE.CID`, `LAWYER.LID` |
> > | `PRESS_NOTE.CID`, `PRESS_NOTE.PNEID` | `COMPLAINT.CID`, `EMPLOYEE.EID` (a PRO) |
> >
> > ### Final answer
> >
> > The 15 relations R1–R15 above are the **3NF-synthesised schema, and in fact in BCNF**, lossless and dependency preserving.
>
> > [!tip] Exam pointer
> > "All the steps" = (1) attributes → (2) FDs → (3) **minimal cover** (show the three sub-steps, even if nothing changes) → (4) candidate key → (5) group by LHS → (6) key-relation / lossless argument → (7) BCNF check → foreign keys. Do not skip the **BCNF check** — the question says "3NF/BCNF". Also state the non-FD business rules (team size 4, ≤ 5 cases, 4/8 weeks, ≤ 10 hearings, 75 %) separately: they are *constraints*, not FDs, and examiners look for them.

---

> [!question] Q2: ERD and conversion to the relational schema (25M)
> Give an ERD for the above requirements (assumptions should be stated) and convert your ERD to a relational schema.

> [!info]- Theory: ER → relational mapping rules (click to expand)
> > 1. **Strong entity** → a table; simple attributes become columns; the key becomes the PK. Composite attributes → their simple components. Multivalued attributes → a separate table.
> > 2. **Weak entity** → a table with PK = (owner's PK + partial key) and an FK to the owner (`ON DELETE CASCADE`).
> > 3. **1:N relationship** → put the FK of the "1" side into the **"N" side** table (the side with $(\cdot,1)$).
> > 4. **1:1 relationship** → FK (+ `UNIQUE`) on the side with total participation, or merge.
> > 5. **M:N relationship** → a **separate table** with PK = both FKs (+ relationship attributes).
> > 6. **(min, max)**: min 0 → nullable FK; min 1 on the FK side → `NOT NULL`; bounded max $>1$ and min on the referenced side cannot be expressed by keys → **trigger / assertion** (see [[pyp2]] Q10).

> [!success]- Solution (click to expand)
> > ### Assumptions
> >
> > 1. `OFFICE` is one entity type with `OType` ∈ {HEAD, BRANCH}; exactly one head office. Each office has one **head** (`MgrEID`: director for HEAD, deputy director for BRANCH); each branch has one **PRO**.
> > 2. All staff (director, deputy director, officer, technical, non-technical, PRO) are `EMPLOYEE`s distinguished by `ERole`; an employee works in exactly one office.
> > 3. A user is identified by **Aadhaar**; registration needs OTP (`UVerified`). A user files many complaints.
> > 4. One complaint = one case. The **head office** (an office of type HEAD) assigns it to a **branch** within one day (`BrAsgDate − CDate ≤ 1 day`).
> > 5. `INVESTIGATION` is a **weak entity** of `COMPLAINT` (round 1 = first investigation; round 2 = re-investigation by a **new team**). At most 2 rounds, total time ≤ 8 weeks.
> > 6. A **team** for a round = exactly **1 officer + 2 technical + 1 non-technical** staff; the officer leads it. An officer can be on at most **5 open cases**; a round lasts ≤ **4 weeks**.
> > 7. An `APPEAL` is raised by the user against one round; the **deputy director** accepts/rejects it. Accepted ⇒ a new round is created.
> > 8. `SUGGESTION`s are given by the user on a complaint to **one** recipient (an officer *or* a lawyer).
> > 9. A case is filed in the **crime branch court** after the user accepts the report; the case file records filing date, verdict and verdict date (verdict ≤ 4 weeks after filing). `HEARING` is a **weak entity** of the case (≤ 10 per case, numbered `HNo`).
> > 10. Each branch has **exactly 3 lawyers**; a lawyer can represent many cases and a case can have several lawyers (M:N).
> > 11. `PRESS_NOTE`s are written by the PRO of the branch for a complaint.
> > 12. Success rate is a **derived** attribute (not stored); `EStatus`/`LStatus` = TERMINATED when it falls below 75 %.
> >
> > ### ER diagram
> >
> > Notation: rectangle = entity, double rectangle `[[ ]]` = weak entity, `<...>` = relationship, **(min,max)** next to the entity it applies to, `{M:N}` = many-to-many. Attributes are listed under each entity; **underline = PK**, *dashed = partial key* (shown with `~`).
> >
> > ```
> >                                 headed by (1,1)           (0,1)
> >            ┌──────────────────────── <HEADS> ─────────────────────────┐
> >            │                                                           │
> >      ┌─────┴───────┐   (1,N)  <WORKS_IN>  (1,1)             ┌──────────┴────────┐
> >      │   OFFICE    │◄─────────────────────────────────────  │     EMPLOYEE      │
> >      │ OID  OType  │                                        │ EID ENm EAddr     │
> >      │ OName OAddr │──── <HAS_PRO> (1,1)── PRO (0,1) ──────►│ EPhone EDoB ERole │
> >      │ OPhone      │                                        │ EStatus           │
> >      └──┬───────┬──┘                                        └───┬───────────┬───┘
> >         │(0,N)  │(3,3)                                         │(0,N)      │(4,4)
> >    <ASSIGNED_TO>│<EMPLOYS_LAWYER>                              │           │
> >         │(1,1)  │(1,1)                           <LEADS/ASSIGNED>     <TEAM_MEMBER>{M:N}
> >         │       ▼                                (0,N)  │ TRole         │(1,N)
> >         │   ┌───────────┐                               │               ▼
> >         │   │  LAWYER   │             ┌─────────────────┘      ╔═══════════════════╗
> >         │   │ LID LNm   │             │                         ║  INVESTIGATION    ║
> >         │   │ LDoB LAddr│             │                         ║ ~INo IStart IDue  ║
> >         │   │ LPhone    │             └────────────────────────►║ IEnd IProgress    ║
> >         │   │ LEmail    │                  (LeadEID)            ╚═════════╤═════════╝
> >         │   │ LStatus   │                                            (1,1) │ <ROUND_OF> (identifying)
> >         │   └──┬────────┘                                                  │ (0,N)
> >         │      │(0,N)                                                      │
> >         │  <REPRESENTS>{M:N, LAsgDate}                                     │
> >         │      │(1,N)                                                      │
> >         ▼      ▼                                                           ▼
> >   ┌───────────────────────────────────────────────────────────────────────────────┐
> >   │                              COMPLAINT                                        │
> >   │  CID  CDate  CDesc  CStatus  BrAsgDate                                        │
> >   └──┬───────────────┬──────────────┬─────────────┬────────────────┬──────────────┘
> >      │(1,1)          │(0,N)         │(0,N)        │(0,N)           │(0,1)
> >  <FILED_BY>      <HAS_DOC>      <HAS_SUGG>   <PRESS_ABOUT>      <FILED_IN_COURT>
> >      │(0,N)          │(1,1)         │(1,1)        │(1,1)           │(1,1)
> >  ┌───┴─────┐   ╔═════╧══════╗   ┌───┴──────┐   ┌──┴──────────┐   ┌──┴─────────────┐   (N,1)   ┌─────────┐
> >  │APP_USER │   ║  DOCUMENT  ║   │SUGGESTION│   │ PRESS_NOTE  │   │   CASE_FILE    │──────────►│  COURT  │
> >  │AAD UNm  │   ║ ~DNo DType ║   │SgID SgMode│  │PNID PNDate  │   │FileDate Verdict│  <IN>     │CrtID    │
> >  │UDoB UAddr│  ║ DFile DDate║   │SgText    │   │PNText       │   │VerdictDate     │           │CrtName  │
> >  │UMob     │   ╚════════════╝   │SgDate    │   └─────────────┘   └──┬─────────────┘           │CrtAddr  │
> >  │UVerified│                    └──────────┘                      (1,1)│ <HEARD_IN>(identifying)│CrtPhone │
> >  └─────────┘                    (also: SgEID → EMPLOYEE, SgLID → LAWYER)    (0,10)│            └─────────┘
> >                                                                              ╔═════╧═══════╗
> >                                                                              ║   HEARING   ║
> >                                                                              ║ ~HNo HDate  ║
> >                                                                              ║ HLog        ║
> >                                                                              ╚═════════════╝
> >    APPEAL(AppID, ApReason, ApDate, ApDecision) — <APPEALS_AGAINST>(1,1) INVESTIGATION (0,1); <DECIDED_BY> (1,1) EMPLOYEE (deputy director)
> >    PRESS_NOTE is also <WRITTEN_BY> (1,1) EMPLOYEE (PRO)
> > ```
> >
> > **Relationship summary (with (min,max) and mapping):**
> >
> > | Relationship | Entities (min,max) | Type | Relational mapping |
> > | --- | --- | --- | --- |
> > | WORKS_IN | EMPLOYEE (1,1) — OFFICE (1,N) | 1:N | `EMPLOYEE.OID` FK, `NOT NULL` |
> > | HEADS | OFFICE (1,1) — EMPLOYEE (0,1) | 1:1 | `OFFICE.MgrEID` FK, `NOT NULL`, `UNIQUE` |
> > | HAS_PRO | OFFICE (0,1) — EMPLOYEE (0,1) | 1:1 | `OFFICE.ProEID` FK, nullable (head office has no PRO), `UNIQUE` |
> > | FILED_BY | COMPLAINT (1,1) — APP_USER (0,N) | 1:N | `COMPLAINT.AAD` FK, `NOT NULL` |
> > | ASSIGNED_TO | COMPLAINT (0,1) — OFFICE/branch (0,N) | 1:N | `COMPLAINT.BrID` FK, nullable until assigned (≤ 1 day) |
> > | HAS_DOC | COMPLAINT (0,N) — DOCUMENT (1,1) weak | identifying 1:N | `DOCUMENT(CID, DNo)` PK, FK CASCADE |
> > | ROUND_OF | COMPLAINT (1,2) — INVESTIGATION (1,1) weak | identifying 1:N | `INVESTIGATION(CID, INo)` PK, FK CASCADE |
> > | LEADS | INVESTIGATION (1,1) — EMPLOYEE (0,N) | N:1 | `INVESTIGATION.LeadEID` FK, `NOT NULL` |
> > | TEAM_MEMBER | INVESTIGATION (4,4) — EMPLOYEE (0,N) | **M:N** with attr `TRole` | table `TEAM_MEMBER(CID, INo, EID, TRole)` |
> > | APPEALS_AGAINST | APPEAL (1,1) — INVESTIGATION (0,1) | N:1 (≤ 1 appeal per round) | `APPEAL.(CID,INo)` FK, `NOT NULL` |
> > | DECIDED_BY | APPEAL (0,1) — EMPLOYEE (0,N) | N:1 | `APPEAL.DecEID` FK, nullable until decided |
> > | HAS_SUGG | COMPLAINT (0,N) — SUGGESTION (1,1) | 1:N | `SUGGESTION.CID` FK, `NOT NULL` |
> > | SUGG_TO | SUGGESTION (1,1) — EMPLOYEE or LAWYER | N:1 (exactly one of the two) | `SgEID`, `SgLID` nullable FKs + `CHECK` exactly one is non-null |
> > | PRESS_ABOUT / WRITTEN_BY | PRESS_NOTE (1,1) — COMPLAINT (0,N); PRESS_NOTE (1,1) — EMPLOYEE/PRO (0,N) | N:1, N:1 | `PRESS_NOTE.CID`, `PRESS_NOTE.PNEID` FKs `NOT NULL` |
> > | FILED_IN_COURT | COMPLAINT (0,1) — CASE_FILE (1,1) | 1:1 | `CASE_FILE.CID` is PK **and** FK to `COMPLAINT` |
> > | IN | CASE_FILE (1,1) — COURT (0,N) | N:1 | `CASE_FILE.CrtID` FK, `NOT NULL` |
> > | HEARD_IN | CASE_FILE (0,10) — HEARING (1,1) weak | identifying 1:N | `HEARING(CID, HNo)` PK, FK CASCADE |
> > | EMPLOYS_LAWYER | OFFICE (3,3) — LAWYER (1,1) | 1:N | `LAWYER.BrID` FK, `NOT NULL` |
> > | REPRESENTS | LAWYER (0,N) — CASE_FILE (1,N) | **M:N** with attr `LAsgDate` | table `CASE_LAWYER(CID, LID, LAsgDate)` |
> >
> > ### Relational schema (the conversion)
> >
> > Applying the rules gives the **same 15 relations** obtained by normalization in Q1 — the ER design and the synthesis agree (which is the point of a good ERD):
> >
> > ```sql
> > OFFICE      (OID PK, OName, OType, OAddr, OPhone,
> >              MgrEID NOT NULL UNIQUE  FK→EMPLOYEE, ProEID UNIQUE FK→EMPLOYEE)
> > EMPLOYEE    (EID PK, ENm, EAddr, EPhone, EDoB, ERole, EStatus,
> >              OID NOT NULL FK→OFFICE)
> > APP_USER    (AAD PK, UNm, UDoB, UAddr, UMob, UVerified)
> > COMPLAINT   (CID PK, CDate, CDesc, CStatus, BrAsgDate,
> >              AAD NOT NULL FK→APP_USER, BrID FK→OFFICE)
> > DOCUMENT    (CID FK→COMPLAINT, DNo, DType, DFile, DDate,   PK(CID, DNo))
> > INVESTIGATION(CID FK→COMPLAINT, INo, IStart, IDue, IEnd, IProgress,
> >              LeadEID NOT NULL FK→EMPLOYEE,                 PK(CID, INo))
> > TEAM_MEMBER (CID, INo, EID FK→EMPLOYEE, TRole,             PK(CID, INo, EID),
> >              FK(CID, INo)→INVESTIGATION)
> > APPEAL      (AppID PK, CID, INo, ApReason, ApDate, ApDecision,
> >              DecEID FK→EMPLOYEE,  FK(CID, INo)→INVESTIGATION)
> > SUGGESTION  (SgID PK, CID NOT NULL FK→COMPLAINT, SgMode, SgText, SgDate,
> >              SgEID FK→EMPLOYEE, SgLID FK→LAWYER,  CHECK exactly one of SgEID/SgLID non-null)
> > COURT       (CrtID PK, CrtName, CrtAddr, CrtPhone)
> > CASE_FILE   (CID PK FK→COMPLAINT, FileDate, Verdict, VerdictDate,
> >              CrtID NOT NULL FK→COURT)
> > HEARING     (CID FK→CASE_FILE, HNo, HDate, HLog,           PK(CID, HNo))
> > LAWYER      (LID PK, LNm, LDoB, LAddr, LPhone, LEmail, LStatus,
> >              BrID NOT NULL FK→OFFICE)
> > CASE_LAWYER (CID FK→CASE_FILE, LID FK→LAWYER, LAsgDate,    PK(CID, LID))
> > PRESS_NOTE  (PNID PK, CID NOT NULL FK→COMPLAINT, PNEID NOT NULL FK→EMPLOYEE,
> >              PNDate, PNText)
> > ```
> >
> > ### Constraints that the model cannot express by keys alone (triggers / `CHECK`)
> >
> > | Business rule | Why not a plain key / FK | Enforcement |
> > | --- | --- | --- |
> > | Team = exactly 1 officer + 2 technical + 1 non-technical | bounded max with min > 1 on a M:N | trigger on `TEAM_MEMBER` (count per role, per `(CID,INo)`) |
> > | Officer on ≤ 5 open cases | bounded max across rows | trigger on `TEAM_MEMBER` insert: count rows of that `EID` with role OFFICER in open cases |
> > | Round ≤ 4 weeks; whole case ≤ 8 weeks | arithmetic on dates | `CHECK (IDue ≤ IStart + 28 days)`; trigger/deferred check on `SUM` over rounds |
> > | Head office assigns branch within 1 day | date arithmetic | `CHECK (BrAsgDate ≤ CDate + 1 day)` |
> > | Branch has exactly 3 lawyers | (3,3) cardinality | deferred trigger on `LAWYER` per `BrID` |
> > | ≤ 10 hearings, verdict ≤ 4 weeks | bounded max, date arithmetic | trigger on `HEARING` (count ≤ 10), `CHECK (VerdictDate ≤ FileDate + 28 days)` |
> > | Appeal decided only by a **deputy director**; lead is an **officer**; PRO writes press notes | role of the referenced row | trigger / `CHECK` via `ERole` lookup |
> > | Success rate < 75 % ⇒ terminated | derived attribute | view computing convictions ÷ cases + trigger/job that sets `EStatus`/`LStatus` |
>
> > [!tip] Exam pointer
> > Marks are for (i) **stated assumptions** (especially: one case = one complaint, weak entities `INVESTIGATION`, `DOCUMENT`, `HEARING`; team size 4; 3 lawyers per branch), (ii) a **neat diagram with (min,max)**, and (iii) the mapping step by type — M:N tables (`TEAM_MEMBER`, `CASE_LAWYER`), weak-entity composite keys, 1:N foreign keys. Mention that rules like 5 cases/officer or 3 lawyers/branch are **not expressible by keys** and need triggers.

---

> [!question] Q3: Nested loop join cost and choice of index (10M)
> You are given 3 data files (tables): Course, Instructor and Department. Every Course and Instructor has an associated Department, and a few departments may not offer courses. Every Course has one Instructor. Record sizes: Course 0.5 KB, Instructor 0.75 KB, Department 1 KB. Records: Course 300000, Instructor 120000, Department 10000. Block size 10 KB, buffer 50 KB.
> a) To perform a nested loop join on these three files, compute the approximate number of disk operations for at least two possible scenarios.
> b) If you may generate only **one index** (assume an equi-join is possible on one attribute of the relations) to apply a **single loop join** (on the result of the nested loop join of two relations), will you index an attribute of Department, Instructor or Course? Justify with the selection factor and block accesses.

> [!info]- Theory: block nested-loop join and index (single-loop) join (click to expand)
> > **Blocking factor** $bfr=\lfloor B/R\rfloor$ records per block; **blocks** $b=\lceil r/bfr\rceil$.
> >
> > **Block nested-loop join** of outer $R$ and inner $S$ with $M$ buffer blocks: read $M-2$ blocks of the outer relation at a time (one buffer block for the inner relation, one for the output), then scan the whole inner relation once per outer chunk:
> > $$ \text{cost} = b_R + \left\lceil \frac{b_R}{M-2}\right\rceil \cdot b_S $$
> > It is cheapest when the **smaller relation is the outer**.
> >
> > **Selection factor (selectivity)** of attribute $A$ in relation $r$: $SC(A,r) = r/V(A,r)$ — the **average number of records** matching one value of $A$ ($V$ = number of distinct values). Key attribute ⇒ $SC=1$.
> >
> > **Single-loop (indexed) join:** for each tuple of the outer (the nested-loop result) probe the index on the join attribute of the inner relation:
> > $$ \text{cost} = b_{outer} + r_{outer}\cdot (h + SC) $$
> > with $h$ = index height (block reads to reach the leaf) and $SC$ = data-block reads per probe (secondary index worst case: one block per matching record).

> [!success]- Solution (click to expand)
> > ### Setup: blocking factors, block counts, buffer
> >
> > Using $10\text{ KB}$ blocks:
> >
> > | File | Record size | $bfr=\lfloor 10/R\rfloor$ | Records $r$ | Blocks $b=\lceil r/bfr\rceil$ |
> > | --- | --- | --- | --- | --- |
> > | Course | 0.5 KB | 20 | 300000 | $b_C = 15000$ |
> > | Instructor | 0.75 KB | $\lfloor 13.33\rfloor = 13$ | 120000 | $b_I = \lceil 9230.77\rceil = 9231$ |
> > | Department | 1 KB | 10 | 10000 | $b_D = 1000$ |
> >
> > Buffer $=50\text{ KB}/10\text{ KB} = M = 5$ blocks ⇒ **$M-2 = 3$ blocks** for the outer relation (1 for the inner, 1 for output).
> >
> > Join attributes (assumption): Course.`instructorId` = Instructor.`instructorId`; Course.`deptId` = Department.`deptId`; Instructor.`deptId` = Department.`deptId`.
> >
> > ### (a) Nested-loop join costs — all six pairings (cost in block transfers)
> >
> > $$ \text{cost}(R\ \text{outer},S\ \text{inner}) = b_R + \lceil b_R/3\rceil\cdot b_S $$
> >
> > | Scenario | Outer | Inner | $\lceil b_{outer}/3\rceil$ | Cost |
> > | --- | --- | --- | --- | --- |
> > | **1a** Course ⋈ Instructor | Course | Instructor | 5000 | $15000 + 5000\cdot9231 = \mathbf{46{,}170{,}000}$ |
> > | **1b** Course ⋈ Instructor | Instructor | Course | 3077 | $9231 + 3077\cdot15000 = \mathbf{46{,}164{,}231}$ |
> > | **2a** Course ⋈ Department | Course | Department | 5000 | $15000 + 5000\cdot1000 = \mathbf{5{,}015{,}000}$ |
> > | **2b** Course ⋈ Department | Department | Course | 334 | $1000 + 334\cdot15000 = \mathbf{5{,}011{,}000}$ |
> > | **3a** Instructor ⋈ Department | Instructor | Department | 3077 | $9231 + 3077\cdot1000 = \mathbf{3{,}086{,}231}$ |
> > | **3b** Instructor ⋈ Department | Department | Instructor | 334 | $1000 + 334\cdot9231 = \mathbf{3{,}084{,}154}$ |
> >
> > **Observations:** (1) in every pair the cheaper order puts the **smaller relation as outer** (1b, 2b, 3b); (2) the join of Course with Instructor is by far the most expensive (≈ 46 M) because both files are large, whereas pairing with the small Department file costs only 3–5 M. *(For comparison, a plain tuple-at-a-time nested loop would need $r_{outer}\cdot b_{inner}+b_{outer}$ — e.g. $300000\times9231+15000\approx 2.77\times10^9$ — which shows why block-nested loop with the 5-block buffer is used.)*
> >
> > ### (b) Which single attribute to index? — nested loop on two relations, indexed loop with the third
> >
> > The three possible plans (best outer/inner order from (a) used for the nested-loop part):
> >
> > | Plan | Nested-loop part | Result tuples $r_{res}$ | Third relation probed via index |
> > | --- | --- | --- | --- |
> > | **A** | Course ⋈ Instructor (1b) = 46,164,231 | 300000 (each course has one instructor) | index on **Department.deptId** |
> > | **B** | Course ⋈ Department (2b) = 5,011,000 | 300000 | index on **Instructor.instructorId** |
> > | **C** | Instructor ⋈ Department (3b) = 3,084,154 | 120000 (each instructor has a department) | index on **Course.instructorId** |
> >
> > **Selection factors:**
> >
> > $$ SC(deptId, Department)=\frac{10000}{10000}=1,\qquad SC(instructorId, Instructor)=\frac{120000}{120000}=1,\qquad SC(instructorId, Course)=\frac{300000}{120000}=2.5 $$
> >
> > The `Department` and `Instructor` indexes are on **keys** (≤ 1 matching record per probe); the `Course.instructorId` index is a **secondary, non-unique index** (on average 2.5 matching records per instructor, worst case 3 block reads, as the courses of one instructor are scattered).
> >
> > **Index height (assumption):** with ≈ 8-byte key + 8-byte pointer per entry, a 10 KB block holds ≈ 600 entries (fan-out). Department: $\lceil10000/600\rceil=17$ leaves ⇒ root + leaf, $h=2$. Instructor: 200 leaves ⇒ $h=2$. Course.instructorId: 120000 distinct values ⇒ 200 leaves ⇒ $h=2$.
> >
> > **Block accesses of the index (single-loop) part**, $r_{res}\cdot(h+SC)$:
> >
> > | Plan | Probes | Per-probe cost | Index-join cost | **Total** |
> > | --- | --- | --- | --- | --- |
> > | **A** (Dept index) | 300000 | $2+1=3$ | 900,000 | $46{,}164{,}231+900{,}000 = \mathbf{47{,}064{,}231}$ |
> > | **B** (Instructor index) | 300000 | $2+1=3$ | 900,000 | $5{,}011{,}000+900{,}000 = \mathbf{5{,}911{,}000}$ |
> > | **C** (Course index) | 120000 | $2+2.5=4.5$ | 540,000 | $3{,}084{,}154+540{,}000 = \mathbf{3{,}624{,}154}$ |
> >
> > **Decision: index an attribute of Course (`Course.instructorId`) — Plan C, ≈ 3.6 million block accesses.**
> >
> > **Justification:**
> > - The per-probe cost of the Course index is higher ($h+SC=4.5$ vs 3), because its selection factor is 2.5 (non-key) versus 1 for Department/Instructor.
> > - But the **number of probes** is what dominates: Plan C probes once per *instructor–department* tuple (120000), while A and B probe once per *course* tuple (300000). $120000\times4.5 = 540{,}000 < 300000\times3 = 900{,}000$.
> > - More importantly, indexing the **largest** relation lets the nested-loop step run on the **two smaller** files (Instructor, Department), which costs only 3.08 M instead of 5.0 M (Plan B) or 46.2 M (Plan A). The expensive full scan of Course (15000 blocks × many passes) is **avoided altogether**.
> > - Indexing Department (Plan A) is the worst: it forces the 46 M Course ⋈ Instructor nested loop, and the index only saves a scan of a 1000-block file. Indexing Instructor (Plan B) is second-best but still scans Course in the nested loop and probes 300000 times.
> >
> > ### Summary
> >
> > | Part | Answer |
> > | --- | --- |
> > | (a) best nested loop per pair | Course⋈Instructor ≈ 46.16 M; Course⋈Department ≈ 5.01 M; Instructor⋈Department ≈ 3.08 M block transfers (Department / smaller relation as outer) |
> > | (b) index choice | **Course** (secondary index on `instructorId`), total ≈ **3.62 M** vs 5.91 M (Instructor index) and 47.06 M (Department index) |
> >
> > *Note: if only a **key**-based index (SC = 1) were permitted, the best choice would be the `Instructor` index (Plan B, 5.91 M). The answer above follows the cost computation, with the selection factor used to quantify the per-probe cost.*
>
> > [!tip] Exam pointer
> > Show the **blocking-factor floor** for Instructor (13, not 13.33) — that is the one number students get wrong. State the formula $b_R+\lceil b_R/(M-2)\rceil b_S$ with $M=5$. In (b) the examiner wants the comparison *selection factor × number of probes*, not just "index the smallest table".

---

> [!question] Q4: View and conflict serializability — view serializable but not conflict serializable (10M)
> Explain View and Conflict Serializability with the help of five transactions (each with at least three valid instructions) on two data items (X and Y), and by using the same requirements, give a schedule that is **view serializable but not conflict serializable** (with justification).

> [!info]- Theory: conflict and view serializability (click to expand)
> > **Conflicting instructions.** $I_i$ (of $T_i$) and $I_j$ (of $T_j$, $i\ne j$) conflict iff they access the **same data item** and **at least one is a write**. Read–read never conflicts.
> >
> > **Conflict serializable:** $S$ can be turned into a serial schedule by swapping consecutive non-conflicting instructions of different transactions. **Test:** build the **precedence graph** (edge $T_i\to T_j$ if a conflicting instruction of $T_i$ precedes one of $T_j$); $S$ is conflict serializable **iff the graph is acyclic**.
> >
> > **View serializable:** $S$ is view-equivalent to a serial schedule $S'$ iff for every data item $Q$:
> > 1. if $T_i$ reads the **initial** value of $Q$ in $S$, it does so in $S'$;
> > 2. if $T_i$ reads the value of $Q$ **written by** $T_j$ in $S$, the same holds in $S'$;
> > 3. the transaction doing the **final write** of $Q$ in $S$ also does it in $S'$.
> >
> > Every conflict-serializable schedule is view serializable, **not conversely**. The gap consists of schedules with **blind writes** (a write with no earlier read of the same item by that transaction) that are **overwritten** later: such useless writes create precedence-graph cycles but do not change any read or final write.

> [!success]- Solution (click to expand)
> > **Setup — five transactions on $X, Y$ (3 instructions each):**
> >
> > | Transaction | Instructions (program order) |
> > | --- | --- |
> > | $T_1$ | read($X$); write($X$); write($Y$) |
> > | $T_2$ | write($X$); write($Y$); write($X$) |
> > | $T_3$ | write($X$); write($Y$); write($Y$) |
> > | $T_4$ | read($X$); read($Y$); write($X$) |
> > | $T_5$ | read($X$); read($Y$); write($Y$) |
> >
> > **Schedule $S$** (view serializable, not conflict serializable):
> >
> > | Step | $T_1$ | $T_2$ | $T_3$ | $T_4$ | $T_5$ |
> > | --- | --- | --- | --- | --- | --- |
> > | 1 | read($X$) | | | | |
> > | 2 | | write($X$) | | | |
> > | 3 | write($X$) | | | | |
> > | 4 | write($Y$) | | | | |
> > | 5 | | write($Y$) | | | |
> > | 6 | | write($X$) | | | |
> > | 7 | | | write($X$) | | |
> > | 8 | | | write($Y$) | | |
> > | 9 | | | write($Y$) | | |
> > | 10 | | | | read($X$) | |
> > | 11 | | | | read($Y$) | |
> > | 12 | | | | write($X$) | |
> > | 13 | | | | | read($X$) |
> > | 14 | | | | | read($Y$) |
> > | 15 | | | | | write($Y$) |
> >
> > ### Step 1 — $S$ is NOT conflict serializable
> >
> > Key conflicting pairs:
> > - $T_1.\text{read}(X)$ (step 1) before $T_2.\text{write}(X)$ (step 2) $\Rightarrow T_1\to T_2$ (also $T_1.\text{write}(Y)$ step 4 before $T_2.\text{write}(Y)$ step 5).
> > - $T_2.\text{write}(X)$ (step 2) before $T_1.\text{write}(X)$ (step 3) $\Rightarrow T_2\to T_1$.
> > - $T_1,T_2$ both precede $T_3$ ($W_1(X)/W_2(X)$ before $W_3(X)$; $W_1(Y)/W_2(Y)$ before $W_3(Y)$) $\Rightarrow T_1\to T_3,\ T_2\to T_3$.
> > - $T_3$ precedes $T_4$ and $T_5$ ($W_3(X)$ before $R_4(X)$, $R_5(X)$; $W_3(Y)$ before $R_4(Y)$, $R_5(Y)$) $\Rightarrow T_3\to T_4,\ T_3\to T_5$.
> > - $T_4.\text{write}(X)$ (step 12) before $T_5.\text{read}(X)$ (step 13) $\Rightarrow T_4\to T_5$.
> > - $T_1,T_2$ also precede $T_4,T_5$ (transitively covered by the above).
> >
> > **Precedence graph:** edges $T_1\to T_2,\ T_2\to T_1,\ T_1\to T_3,\ T_2\to T_3,\ T_3\to T_4,\ T_3\to T_5,\ T_4\to T_5$ (plus $T_1,T_2\to T_4,T_5$):
> >
> > ```
> >          ┌────────────┐
> >          ▼            │
> >         T1 ──────────► T2        ← cycle  T1 ⇄ T2
> >          │             │
> >          └──► T3 ◄─────┘
> >                │
> >                ├──► T4 ──► T5
> >                └──────────►┘
> > ```
> >
> > The graph contains the **cycle $T_1\to T_2\to T_1$** ⇒ **$S$ is not conflict serializable** (no serial order can put $T_1$ both before and after $T_2$).
> >
> > ### Step 2 — $S$ IS view serializable (view equivalent to the serial schedule $\langle T_1,T_2,T_3,T_4,T_5\rangle$)
> >
> > | Condition | In $S$ | In serial $T_1T_2T_3T_4T_5$ | Match |
> > | --- | --- | --- | --- |
> > | $T_1$ reads **initial** $X$ | step 1 — no write on $X$ before it | $T_1$ runs first | ✔ |
> > | $T_4$ reads $X$ **from** | $T_3$ (last write of $X$ before step 10 is $W_3(X)$ at step 7) | $T_3$ is the last writer of $X$ before $T_4$ | ✔ |
> > | $T_4$ reads $Y$ **from** | $T_3$ (last write of $Y$ before step 11 is step 9) | $T_3$ | ✔ |
> > | $T_5$ reads $X$ **from** | $T_4$ ($W_4(X)$ at step 12) | $T_4$ | ✔ |
> > | $T_5$ reads $Y$ **from** | $T_3$ (only $W_3(Y)$ precedes it; $T_4$ writes no $Y$) | $T_3$ | ✔ |
> > | **Final write** of $X$ | $T_4$ (step 12) | $T_4$ | ✔ |
> > | **Final write** of $Y$ | $T_5$ (step 15) | $T_5$ | ✔ |
> >
> > All three view-equivalence conditions hold for every data item ⇒ **$S$ is view serializable**.
> >
> > ### Why the two tests disagree
> >
> > $T_2$'s writes ($W_2(X)$, $W_2(Y)$, $W_2(X)$) and $T_1$'s writes are **blind** or **overwritten**: $T_3$ overwrites both items right afterwards, and nobody reads the values written by $T_1$ or $T_2$ (the only reader of an early value, $T_1.R(X)$, reads the initial value). These useless writes create the conflict edges $T_1\leftrightarrow T_2$ (a cycle) but have **no effect** on any read or on the final database state.
> >
> > $\therefore$ $S$ is **view serializable but not conflict serializable**.
>
> > [!tip] Exam pointer
> > The standard recipe: take a classic 3-transaction pattern — $R_1(X)\ W_2(X)\ W_1(X)\ W_3(X)$ — where $T_2$ and $T_3$ do **blind writes** and $T_3$ writes last, then pad with extra transactions that run serially afterwards ($T_4$, $T_5$). The cycle $T_1\leftrightarrow T_2$ kills conflict serializability, but $T_3$'s final write masks everything, giving view equivalence to $T_1T_2T_3\ldots$. Always show **both** the cycle *and* the 3-condition view check.

---

> [!question] Q5: B+ tree insertion and deletion (10M)
> Given that block and record pointers are the same size, order $m$ is 3 and $m_{leaf}$ is 2. Insert the following elements into a B+ tree (one illustration for each insertion): 7, 9, 2, 3, 19, 17, 23, 33, 11, 39, 94, 67, 61. Followed by deleting the elements 19, 7, 94 and 61 (one illustration for each deletion).

> [!info]- Theory: B+ tree rules used here (click to expand)
> > **Capacities** ($m=3$, $m_{leaf}=2$):
> > - **Leaf:** at most 2 keys, at least 1 key.
> > - **Internal node:** at most $m-1=2$ keys (3 children), at least $\lceil m/2\rceil-1=1$ key (2 children).
> >
> > **Insertion.** *Leaf overflow* (3 keys): split — left keeps the 2 smaller keys, right keeps the largest 1; the **smallest key of the right leaf is copied up** into the parent. *Internal overflow* (3 keys): split into 1 key + 1 key, the **middle key moves up** (not kept below). Root overflow ⇒ new root, **height + 1**.
> >
> > **Deletion.** Remove the key from its leaf. On **underflow** (0 keys): (1) **borrow** from an adjacent sibling that has more than the minimum (rotate through the parent, update the separator); (2) otherwise **merge** with a sibling (pull the parent separator down for an internal merge, discard it for a leaf merge); (3) the parent may underflow ⇒ repeat upward; (4) root with 0 keys and 1 child ⇒ child becomes root, **height − 1**.
> >
> > *Conventions used:* on underflow, **try the left sibling first, then the right**; separators that stay valid for routing are not rewritten unless a borrow/merge requires it. There are **no duplicate keys** in this paper's insertion list.

> [!success]- Solution (click to expand)
> > ### Insertions — state after every step
> >
> > Insert sequence: 7, 9, 2, 3, 19, 17, 23, 33, 11, 39, 94, 67, 61.
> >
> > **1. Insert 7.** Empty tree ⇒ single leaf (also the root).
> > ```
> > [7]
> > ```
> >
> > **2. Insert 9.** Fits (1 < 2 keys).
> > ```
> > [7, 9]
> > ```
> >
> > **3. Insert 2.** Leaf becomes [2, 7, 9] — overflow. **Split:** [2, 7] | [9]; copy up **9** into a new root.
> > ```
> >        [9]
> >       /    \
> >  [2,7]      [9]
> > ```
> >
> > **4. Insert 3.** 3 < 9 ⇒ leaf [2,7] → [2,3,7], overflow. **Split:** [2,3] | [7]; copy up **7**. Root becomes [7, 9] (fits).
> > ```
> >           [7, 9]
> >         /    |    \
> >    [2,3]    [7]    [9]
> > ```
> >
> > **5. Insert 19.** 19 ≥ 9 ⇒ last leaf [9] → [9, 19] (fits).
> > ```
> >           [7, 9]
> >         /    |    \
> >    [2,3]    [7]   [9,19]
> > ```
> >
> > **6. Insert 17.** 17 ≥ 9 ⇒ leaf [9,19] → [9,17,19], overflow. **Split:** [9,17] | [19]; copy up **19**. Root would be [7, 9, 19] — 3 keys, overflow. **Root splits:** left [7] (children [2,3], [7]), right [19] (children [9,17], [19]); middle **9 moves up** into a new root. Height = 3.
> > ```
> >                    [9]
> >              /            \
> >          [7]                [19]
> >         /    \             /     \
> >    [2,3]     [7]     [9,17]      [19]
> > ```
> >
> > **7. Insert 23.** 23 ≥ 9 ⇒ right; 23 ≥ 19 ⇒ leaf [19] → [19, 23] (fits).
> > ```
> >                    [9]
> >              /            \
> >          [7]                [19]
> >         /    \             /     \
> >    [2,3]     [7]     [9,17]     [19,23]
> > ```
> >
> > **8. Insert 33.** 33 ≥ 19 ⇒ leaf [19,23] → [19,23,33], overflow. **Split:** [19,23] | [33]; copy up **33**. Internal [19] → [19, 33] (fits).
> > ```
> >                    [9]
> >              /            \
> >          [7]                [19, 33]
> >         /    \             /    |     \
> >    [2,3]     [7]     [9,17]  [19,23]  [33]
> > ```
> >
> > **9. Insert 11.** 11 ≥ 9 ⇒ right subtree [19,33]; 11 < 19 ⇒ first leaf [9,17] → [9,11,17], overflow. **Split:** [9,11] | [17]; copy up **17**. Internal [19,33] → [17,19,33], overflow. **Internal split:** left [17] (children [9,11], [17]), right [33] (children [19,23], [33]); middle **19 moves up**. Root [9] → [9, 19] (fits).
> > ```
> >                      [9, 19]
> >               /        |         \
> >           [7]        [17]        [33]
> >          /   \      /    \      /     \
> >     [2,3]   [7] [9,11]  [17] [19,23]  [33]
> > ```
> >
> > **10. Insert 39.** 39 ≥ 19 ⇒ internal [33]; 39 ≥ 33 ⇒ leaf [33] → [33, 39] (fits).
> > ```
> >                      [9, 19]
> >               /        |         \
> >           [7]        [17]        [33]
> >          /   \      /    \      /     \
> >     [2,3]   [7] [9,11]  [17] [19,23]  [33,39]
> > ```
> >
> > **11. Insert 94.** 94 ≥ 19 ⇒ internal [33]; leaf [33,39] → [33,39,94], overflow. **Split:** [33,39] | [94]; copy up **94**. Internal [33] → [33, 94] (fits).
> > ```
> >                      [9, 19]
> >               /        |            \
> >           [7]        [17]          [33, 94]
> >          /   \      /    \        /    |     \
> >     [2,3]   [7] [9,11]  [17]  [19,23] [33,39] [94]
> > ```
> >
> > **12. Insert 67.** 67 ≥ 19 ⇒ internal [33,94]; 33 ≤ 67 < 94 ⇒ middle leaf [33,39] → [33,39,67], overflow. **Split:** [33,39] | [67]; copy up **67**. Internal [33,94] → [33,67,94], overflow. **Internal split:** left [33] (children [19,23], [33,39]), right [94] (children [67], [94]); middle **67 moves up**. Root [9,19] → [9,19,67], overflow. **Root splits:** left [9] (children [7], [17]), right [67] (children [33], [94]); middle **19 moves up** into a new root. Height = 4.
> > ```
> >                                  [19]
> >                    /                              \
> >                [9]                                  [67]
> >            /          \                         /            \
> >         [7]           [17]                   [33]             [94]
> >        /   \         /    \                 /     \          /     \
> >   [2,3]    [7]   [9,11]   [17]        [19,23]  [33,39]    [67]    [94]
> > ```
> >
> > **13. Insert 61.** 61 ≥ 19 ⇒ right; 61 < 67 ⇒ internal [33]; 61 ≥ 33 ⇒ leaf [33,39] → [33,39,61], overflow. **Split:** [33,39] | [61]; copy up **61**. Internal [33] → [33, 61] (fits, no further split).
> >
> > **Final tree after all 13 insertions (4 levels):**
> > ```
> >                                  [19]                                  ← Root
> >                    /                              \
> >                [9]                                  [67]               ← Level 2
> >            /          \                         /            \
> >         [7]           [17]                  [33, 61]          [94]     ← Level 3
> >        /   \         /    \                /    |    \        /    \
> >   [2,3]    [7]   [9,11]   [17]      [19,23] [33,39] [61]    [67]    [94]   ← Leaves
> > ```
> > Leaf chain: [2,3] → [7] → [9,11] → [17] → [19,23] → [33,39] → [61] → [67] → [94].
> >
> > ---
> >
> > ### Deletions — state after every step
> >
> > Delete 19, 7, 94 and 61 in this order, starting from the final tree above.
> >
> > **D1. Delete 19.** 19 is in leaf [19,23] ⇒ becomes **[23]** (1 key = minimum, no underflow). The key 19 in the root is only a routing separator and still routes correctly ($23\ge19$), so it is left unchanged.
> > ```
> >                                  [19]
> >                    /                              \
> >                [9]                                  [67]
> >            /          \                         /            \
> >         [7]           [17]                  [33, 61]          [94]
> >        /   \         /    \                /    |    \        /    \
> >   [2,3]    [7]   [9,11]   [17]         [23]  [33,39] [61]   [67]    [94]
> > ```
> >
> > **D2. Delete 7.** 7 is in leaf [7] ⇒ empty, **underflow**. Left sibling leaf [2,3] has 2 keys (> minimum) ⇒ **borrow 3**: the leaf becomes [3], the left sibling [2]. The parent separator changes from 7 to **3**.
> > ```
> >                                  [19]
> >                    /                              \
> >                [9]                                  [67]
> >            /          \                         /            \
> >         [3]           [17]                  [33, 61]          [94]
> >        /   \         /    \                /    |    \        /    \
> >      [2]   [3]   [9,11]   [17]         [23]  [33,39] [61]   [67]    [94]
> > ```
> >
> > **D3. Delete 94.** 94 is in leaf [94] ⇒ empty, **underflow**. Its left sibling leaf [67] has only 1 key ⇒ cannot lend ⇒ **merge:** the empty leaf is merged into [67]; separator 94 is discarded. Parent internal [94] loses its only key ⇒ **0 keys, 1 child — underflow**.
> > - Its left sibling internal [33,61] has 2 keys (> minimum) ⇒ **borrow through the parent:** separator **67** comes down into the underflowing node, the sibling's last key **61** moves up to the parent, and the sibling's last child (leaf [61]) is handed over.
> > - Result: parent becomes [61]; left child internal **[33]** (leaves [23], [33,39]); right child internal **[67]** (leaves [61], [67]). No further underflow — stop.
> > ```
> >                                  [19]
> >                    /                              \
> >                [9]                                  [61]
> >            /          \                         /            \
> >         [3]           [17]                    [33]           [67]
> >        /   \         /    \                  /     \        /    \
> >      [2]   [3]   [9,11]   [17]            [23]  [33,39]   [61]   [67]
> > ```
> >
> > **D4. Delete 61.** 61 is in leaf [61] (first child of internal [67]) ⇒ empty, **underflow**. No left sibling under this parent; the right sibling leaf [67] has 1 key ⇒ cannot lend ⇒ **merge** into [67] (separator 67 discarded). Internal [67] now has **0 keys, 1 child — underflow**.
> > - Left sibling internal [33] has only 1 key ⇒ cannot lend ⇒ **merge:** pull the parent separator **61** down: new internal node **[33, 61]** with children [23], [33,39], [67]. The parent [61] now has **0 keys, 1 child — underflow**.
> > - Its left sibling internal [9] has only 1 key ⇒ cannot lend ⇒ **merge:** pull the root separator **19** down: new internal node **[9, 19]** with children [3], [17], [33,61]. The root now has **0 keys and exactly 1 child**.
> > - **The root is removed and its only child [9, 19] becomes the new root ⇒ LEVEL DROP (height 4 → 3).**
> > ```
> >                         [9, 19]                                  ← New root (height dropped to 3)
> >                /           |             \
> >            [3]           [17]          [33, 61]                  ← Level 2
> >           /   \         /    \        /    |    \
> >         [2]   [3]   [9,11]   [17]  [23]  [33,39]  [67]           ← Leaves
> > ```
> > Leaf chain: [2] → [3] → [9,11] → [17] → [23] → [33,39] → [67].
> >
> > **Summary of deletions:**
> >
> > | Step | Key | Leaf effect | Cascade |
> > | --- | --- | --- | --- |
> > | D1 | 19 | [19,23] → [23] | none |
> > | D2 | 7 | [7] empty | **borrow** 3 from left leaf, separator 7 → 3 |
> > | D3 | 94 | [94] empty | leaf **merge** → internal underflow → **borrow** (61) from left internal sibling |
> > | D4 | 61 | [61] empty | leaf **merge** → internal **merge** → internal **merge** → root empty → **level drop** |
>
> > [!tip] Exam pointer
> > Two things to show explicitly: (1) at every underflow, the order **borrow if the sibling has a spare key, merge only otherwise**; (2) after every merge re-check the **parent's key count** and continue upward — in D3 the cascade stops after a borrow, in D4 it runs all the way to the root and the tree loses a level. Leaf-split copies the key up; internal-split moves it up.
