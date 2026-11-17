---
title: DBMS — Post-Midsem Notes (File Organization, Query Algorithms, Transactions)
tags:
  - dbms
  - DBMS
  - file-management
  - indexing
  - post-midsem
---

# Post-Midsem — File Organization and Indexing · Query Algorithms · Transactions

This block is the storage-and-retrieval half of the DBMS course. It starts at the physical bottom — a disk is a stack of spinning platters, and the only unit it can move is a **block** — and works upward: records must be packed into those blocks (§1.1–§1.6), a **file organization** decides how the records are placed (§1.7–§1.11), and when the file grows or shrinks the placement must change without breaking access (§1.12–§1.20). The other half of the story is the **index**: an auxiliary structure that turns a full-file scan into a handful of block reads, first as a simple ordered file (§1.21–§1.31) and finally as a self-balancing $B^+$ tree (§1.32–§1.39). Topics 2 (query algorithms) and 3 (transactions) are listed in [[Syllabus]] and will be appended here in syllabus order.

*Topic list and progress: [[Syllabus]] · formatting rules: [[context]] · book: [[silberschatz_dbms.pdf]] (Ch. 13 "Data Storage Structures", Ch. 14 "Indexing", §24.5 "Hash Indices").*

> [!info] How the block is organised
> | Topic | Deck | Slides | Question it answers |
> | --- | --- | --- | --- |
> | 1 | [[file-management.pdf\|file-management deck]] | 60 | How are records placed on disk, and how do indexes make them findable? |
> | 2 | [[algos.pdf\|algos deck]] | — | How does the DBMS execute a query (sorting, joining, selecting)? |
> | 3 | [[transactions.pdf\|transactions deck]] | — | How are concurrent, failure-prone updates kept correct? |
>
> Only topic 1 is written so far; the other two rows are placeholders in [[Syllabus]].

> [!warning] The conventions this topic uses everywhere
> - $B$ = **block size** (bytes); $r$ = **record length**; $b$ = **blocking factor** $= B/r$; $b$ is also reused for the *number of data-file blocks* in the index section — the deck does this, so read the local definition each time.
> - $V$ = size of the indexing/ordering field; $P$ = size of a **block pointer**; $P_r$ = size of a **record pointer**.
> - An **index entry** is a pair $\langle \text{key value},\ \text{pointer}\rangle$; a **bucket** is one block or a few consecutive blocks.
> - In extendible hashing the deck uses the **trailing (suffix) $k$ bits** of the hash value. The textbook instead describes leading bits (a *prefix*); the two are equivalent with a reversed bit string, but use the **deck's trailing-bit convention** in exam answers.
> - Order $m$ of an internal node = **maximum number of tree pointers**; it can hold at most $m-1$ keys. Order $m_{leaf}$ of a leaf = **maximum number of record pointers** = number of keys.

---

## 1. File Organization and Indexing

*Deck: [[file-management.pdf|file-management deck]] — 60 slides, Prof. P. Sreenivasa Kumar, IIT Madras. The Silberschatz textbook (Ch. 13–14, §24.5) is used only to explain the deck's ideas more clearly; every number and convention below comes from the deck.*

> [!abstract] Roadmap of this topic — read it as one story
> **The question:** a relation is a set of records, but a disk only moves blocks. How does a record become a byte position, and how is it found again?
> **The answer is a stack of decisions**, each one narrowing the search:
> 1. **§1.1–§1.6 — the physical layer:** who manages the disk, how a block is addressed, what a seek costs, how records are packed and how file blocks land on disk blocks.
> 2. **§1.7–§1.11 — the placement policy:** heap (append), sorted (order), hashed (compute the address). Every organization makes some operations fast and others slow.
> 3. **§1.12–§1.20 — growth:** static hashing breaks when the file changes size; extendible and linear hashing let the structure grow one bucket at a time.
> 4. **§1.21–§1.31 — the index:** rather than reorder the file, build a small sorted side-structure; binary search it, then make it multilevel, and learn the three flavours (primary / clustering / secondary).
> 5. **§1.32–§1.39 — $B^+$ trees:** a multilevel index that repairs itself after every insertion and deletion, so it never needs a full reorganization.
>
> **The idea to carry through:** a database pays for **block accesses**, not for comparisons. Almost every design choice in this topic trades *space* and *update cost* for fewer block reads.

### 1.1 Disk space management — who owns the disk?

The data of a relational database is ultimately stored in **disk files**. The first design question is whether those files are managed by the operating system or by the DBMS itself.

- **Option A — use OS file services.** Simple, but the OS decides *when* a block that the DBMS has modified in its main-memory buffer is written back to disk.
- **Option B — the RDBMS manages disk space itself.** This is the **preferred** option, because the DBMS requires **complete control over when a block or page in the main-memory buffer is written to the disk**. That control is what makes **recovery after a system crash** possible: the write-ahead log and the buffer manager must agree about which disk image is authoritative.

> [!note] Why this matters beyond file management
> The same decision resurfaces in the transactions topic: a commit cannot be honest unless the DBMS can force specific blocks to disk in a specific order. "Let the OS flush it later" is not acceptable.

### 1.2 Structure of disks and the cost of a block access

![[DBMS - Disk Structure.excalidraw]]

*Figure — the disk anatomy: platters on a spindle, one read/write head per surface, tracks and sectors; a cylinder is track $i$ on every platter (deck p. 2).*

A disk is **several platters stacked on a rotating spindle** (7000–10000 rpm). Each platter surface has its **own read/write head**, so a head never has to move between surfaces — only between tracks. A platter carries several **tracks** (about 10,000 per inch); each track is divided into **sectors**, and each sector into **blocks**. The **block is the unit of data transfer** — the smallest amount the disk and the DBMS exchange in one I/O.

**Cylinder $i$** means track $i$ on *all* platters. Because all heads move together, every track in a cylinder is reachable **without a new seek**, which is why cylinder-adjacent blocks are cheap to read together.

> [!important] Definitions — block address and access time
> **Address of a block** = (Surface No, Cylinder No, Block No).
> To transfer a block:
> 1. Move the read/write head to the right track → **seek time**, about $12$–$14\ \text{ms}$.
> 2. Wait for the required block to rotate under the head → **rotational delay**, about $3$–$4\ \text{ms}$ on average.
>
> $$ \boxed{\ \text{access time} = \text{seek time} + \text{rotational delay}\ } $$

Blocks on the **same cylinder** are roughly close to each other in access time — cylinders $i$, $i+1$, $i+2$, … — so placing a file's consecutive blocks on one cylinder (or adjacent cylinders) is the physical reason contiguous allocation is fast.

*Figure — the deck's own disk diagram (deck p. 2).*

![[DBMS - Disk Structure (deck p2).png|470]]

> [!tip] Exam pointer — the cost model
> Know the two components and their numbers: seek $12$–$14$ ms, rotational delay $3$–$4$ ms. Every later "this is faster" claim (binary search on an index, contiguous scanning, multilevel index) is really a claim about **fewer random block accesses**.

### 1.3 Data records and files — fixed length vs variable length

A file is a sequence of records; the *shape* of a record determines how simply it can be located.

**Fixed-length record type.** Every field has a fixed length. Because every record occupies the same number of bytes, **the record number can be used to locate a specific record** by direct arithmetic. The **file header** stores the number of records and the length of each field.

**Variable-length record type.** These arise from (i) **missing fields**, (ii) **repeating fields**, and (iii) **intrinsically variable-length fields**. **Special separator symbols** mark field boundaries and record boundaries; the file header records the number of records and which separator symbols are in use.

> [!warning] The trade-off
> Fixed-length records are easier to implement and allow direct positioning by record number; variable-length records are compact but need separators or offset tables, and a deleted slot may not fit the next inserted record. The textbook calls out the same issue: a free-list of deleted slots works perfectly only when every record is the same size.

### 1.4 Packing records into blocks — blocking factor and spanned records

![[DBMS - Blocking and Spanned Records.excalidraw]]

*Figure — unspanned records fit wholly inside a block; a spanned record continues into the next block.*

**Case 1 — record length much less than block size (the usual case).** Several records share one block. The **blocking factor**

$$ \boxed{\ b = \frac{B}{r}\ } \qquad (B = \text{block size in bytes},\ r = \text{record length in bytes}) $$

is the **maximum number of records that can be stored in a block**; the fractional part is discarded because a record may not straddle a block boundary.

**Case 2 — record length greater than block size.** A **spanned organization** is used: one logical record occupies the remainder of one block and continues at the start of the next. This is the exception, not the rule — it costs an extra block access per spanned record.

A **file block sequence** is the sequence of blocks containing all the records of the file.

> [!note] Book connection
> Silberschatz (§13.2) assumes for most discussion that no record is larger than a block and that each record lies entirely in one block — exactly the deck's Case 1. It also describes the **file header free list**: deleted records are linked together so an insertion can reuse a slot without moving later records.

### 1.5 Mapping file blocks onto disk blocks

Having cut the file into blocks, we must decide where on the disk each file block lives.

![[DBMS - File Block Allocation.excalidraw]]

*Figure — contiguous allocation keeps file blocks together; linked allocation scatters them and chains them with pointers; mixed allocation is the compromise.*

| Scheme | Rule | Advantage | Cost |
| --- | --- | --- | --- |
| **Contiguous allocation** | Consecutive file blocks go into consecutive disk blocks | Fast file scanning, especially with **double buffering** | Expanding the file by inserting a block *in the middle* is difficult |
| **Linked allocation** | Each file block is assigned some disk block; every disk block carries a **pointer to the next block** of the sequence | File expansion is easy | Scanning is slow (the next block may be anywhere → random I/O) |
| **Mixed allocation** | A hybrid — runs of contiguous blocks linked together | Balances the two | More bookkeeping |

> [!note] Why double buffering helps contiguous scanning
> While the CPU processes the block already in memory, the disk transfers the *next* (physically adjacent) block into the other buffer. Sequential disk I/O needs no seek per block, so the pipeline stays full. Linked allocation destroys that locality.

### 1.6 Operations on files and the role of file organization

The operations a DBMS performs on a file are:

| Operation | What it involves |
| --- | --- |
| **Insert a new record** | May involve searching for the appropriate location for the new record |
| **Delete a record** | Locating the record may involve search; deleting it may involve moving other records |
| **Update field(s)** | Equivalent to a **delete followed by an insert** |
| **Search for a record** | Given the value of a **key** or **non-key** field |
| **Range search** | Given a range of values for a key or non-key field |

How successfully these are carried out depends on two things: **the organization of the file** and **the availability of indexes**. That is the whole justification for the rest of this topic — there is no universally best organization, only a best one for a given pattern of operations.

### 1.7 The three primary file organizations — an overview

> [!important] Definition — primary file organization
> **Primary file organization** is the logical policy / method used for **placing records into file blocks**.

Example: a student file may be organized so that student records are sorted in increasing order of `rollNo`.

The **goal** is to make the *frequently executed* operations fast. **Conflicting demands** are normal: on the student file, access by `rollNo` and access by `name` may both be frequent. We choose to make `rollNo` access fast; to make `name` access fast we need an **additional access structure** — an index (§1.21 onward).

The three organizations studied next are **heap files**, **sorted (sequential) files**, and **hashed files**.

### 1.8 Heap files

A **heap file** appends records to the file in insertion order — the simplest organization.

- **Insertion:** read the last file block, append the record, write the block back — **easy**.
- **Locating a record given any attribute:** requires **scanning the entire file** — very costly.

Because lookup is so weak, heap files are **often used only together with other access structures** (an index supplies the lookup; the heap just stores rows compactly).

### 1.9 Sorted (sequential) files

> [!important] Definitions — ordering field and ordering key
> **Ordering field** — the field whose values are used to sort the records of the data file.
> **Ordering key field (OKF)** — an ordering field that is also a key.
> **Sorted / sequential file** — a data file whose records are arranged so the ordering field values are in **ascending order**.

**Search is efficient.** Given the value $X$ of the ordering field, perform **binary search**: the address of the $n$-th file block comes from the file header, so only $O(\log N)$ disk accesses are needed to reach the required block. **Range search is also efficient**, because matching records are physically adjacent.

**Insertion is costly.** It disturbs the ordering: all blocks *following* the insertion block may have to be modified. The deck's remedy is therefore **not to insert directly into the main file**:

1. Keep all newly inserted records in an **auxiliary file**.
2. **Periodically reorganize** — merge the auxiliary file and the main file.
3. A lookup searches the **auxiliary file first**, then the main file.

**Deletion** uses **deletion markers**, so the physical ordering (and therefore the binary search) is not disturbed.

> [!warning] The recurring pattern
> "Keep the main structure still; absorb changes in a small side structure; merge later" appears again for ISAM (§1.31) and, in a smarter incremental form, in $B^+$ trees (§1.32). It is the standard way to make an ordered file writable.

### 1.10 Hashed files — buckets and overflow chains

**Use case:** very useful when quick access to a record is needed given the value of a **single attribute**.

> [!important] Definitions
> **Hashing field** — the attribute on which quick access is needed and on which hashing is performed.
> **Bucket** — a block, or a few consecutive blocks; the data file is organized as buckets numbered $0,1,\dots,M-1$.
> **Hash function $h$** — maps values from the domain of the hashing attribute to bucket numbers.

![[DBMS - Hashed File and Overflow Chains.excalidraw]]

*Figure — main buckets $0\ldots M-1$ with an overflow chain hanging off bucket 1.*

**Insertion of record $R$:** apply $h$ to the hashing-attribute value to get bucket number $r$. If bucket $r$ has space, place $R$ there; otherwise place $R$ in the **overflow chain** of bucket $r$. The overflow chains of *all* buckets are kept together in the **overflow buckets**.

**Deletion:** locate $R$ by applying $h$; remove it from its bucket or overflow chain; **if possible bring a record from the overflow chain back into the bucket** (so future searches need not follow the chain).

**Search for key value $k$:** compute $r = h(k)$, fetch bucket $r$ and search it; if the record is not found, follow the **overflow chain** of bucket $r$.

*Figure — the deck's bucket-and-overflow picture (deck p. 13).*

![[DBMS - Hashed File Buckets (deck p13).png|470]]

> [!note] Book terminology
> Silberschatz calls this **overflow chaining** or **closed addressing**, and contrasts it with **open addressing** (probing another bucket in the fixed set), which it rejects for databases because deletion is troublesome. The book also notes a hash index answers **equality** queries efficiently but **not range** queries — hashing destroys order.

### 1.11 Performance of static hashing

**Static hashing** is the scheme just described: the number of main buckets is **fixed**.

- Locating a record given the hashing-attribute value takes, **most often, one block access** — the ideal case.
- The capacity of the hash file is

$$ \boxed{\ C = r \cdot M\ } \qquad (r = \text{records per bucket},\ M = \text{number of main buckets}) $$

**Disadvantages**, both consequences of $M$ being frozen:

- If actual records $\ll C$ → **wastage of disk space** (many empty buckets).
- If actual records $\gg C$ → **long overflow chains** → degraded performance (a lookup becomes a walk down a chain).

> [!tip] Exam pointer — static hashing
> State $C = rM$ and both failure directions. Then say what dynamic hashing fixes: it lets the bucket set grow/shrink incrementally instead of being chosen once at creation time.

### 1.12 Dynamic file organization — why hashing must grow

**Dynamic files** are files where insertions and deletions happen frequently, so the file **keeps growing and shrinking**. Static hashing cannot serve them well.

The clever observation is that **bucket numbers are integers**, so their **binary representation** can be exploited to devise dynamic schemes. The deck names two:

1. **Extendible hashing** (§1.13–§1.16).
2. **Linear hashing** (§1.17–§1.20).

The book frames the same choice as three bad options for static hashing — pick a function for today's size (performance degrades), pick one for tomorrow's size (space wasted today), or periodically rebuild everything (a massive, disruptive reorganization) — and then presents extendible and linear hashing as the incremental answers.

### 1.13 Extendible hashing — structure

For a record $R$, form its **$k$-bit sequence** as follows:

1. Apply the hash function to the value of the hashing field of $R$ → bucket number $r$.
2. Convert $r$ into its **binary representation** → a bit sequence.
3. Take the **trailing $k$ bits**.

Two depths govern the structure:

> [!important] Definitions — global and local depth
> **Global depth $d$** — the number of trailing bits used in the directory. The directory has $2^d$ entries.
> **Local depth** — the number of bits in the **common suffix** of the bit sequences corresponding to the records in a bucket.

![[DBMS - Extendible Hashing.excalidraw]]

*Figure — a $d=3$ directory (000…111) pointing to buckets whose local depth is written beside them; several directory entries may share one bucket.*

**Locating a record:** match the $d$-bit suffix of $h(k)$ against an entry in the **directory** and follow its pointer to the bucket, then search that bucket. The directory is small (one pointer per entry), so it is cheap to keep in memory; the extra hop is the price of not having to rebuild the file.

*Figure — the deck's directory, global depth $d=3$, with local depths marked (deck p. 18).*

![[DBMS - Extendible Hashing Directory (deck p18).png|470]]

### 1.14 Insertion in extendible hashing

Apply $h$ to the new record, take its $d$-bit suffix, and go to the addressed bucket:

- **Bucket not full** → put the record there. **No change to the directory.**
- **Bucket full** → **split the bucket**. Redistribute its records by one more trailing bit: records whose $(d'+1)$-bit suffix differs go to a **new bucket**; the rest stay. Then:
  - if the bucket's **local depth $<$ global depth** → the directory already has the extra entries; just re-point them. **Directory size unchanged.**
  - if the bucket's **local depth $=$ global depth** → there is no spare directory entry, so **the directory is doubled** ($d \leftarrow d+1$) and every entry is duplicated.

> [!important] The decisive rule
> **If the local depth of the bucket to be split equals the global depth, the directory is doubled.** Otherwise a split image is created without doubling the directory.

The deck's first illustration inserts a record whose 2-bit suffix is `00` into a full bucket $b_0$: $b_0$ is split, records with 2-bit sequence `10` go to the new bucket $b_3$, the others stay in $b_0$, and the directory is modified. Its second illustration inserts suffix `10` into a full $b_3$ with local depth 2 = global depth 2: $b_3$ splits, the directory doubles to $d=3$, and records with 3-bit sequence `110` go to the new $b_4$.

### 1.15 Deletion in extendible hashing

Deletion nearly reverses insertion, but with a **less-than-half-full** test rather than an overflow test:

> [!important] Definitions and rules
> **Matching pair of data buckets** — two buckets whose $k$-bit suffixes have a common $(k-1)$-bit suffix (e.g. $b_3$ and $b_4$).
> 1. If, after deletions, a matching pair becomes **less than half full**, **try to merge them into one bucket**.
> 2. If the **local depth of all buckets is one less than the global depth**, **reduce the directory to half its size** ($d \leftarrow d-1$).

> [!warning] Merge is conditional
> Merging is attempted only for a *matching* pair — two buckets that differ only in the bit that was added at their last split. Merging arbitrary buckets would break the suffix-to-directory mapping.

### 1.16 Extendible hashing — the full worked example

**Setup (deck p. 22–23):** bucket capacity $= 2$, initial buckets $= 1$. The deck shows the binary string of each key beside it. Reproduce every step:

| Insert | Deck's bit string | Effect on the structure |
| --- | --- | --- |
| 45 | `101101` | First record in the single initial bucket (global depth 0, local depth 0) |
| 22 | `10110` | Same bucket — now full (2 records) |
| 12 | `1100` | **Overflow.** Local depth = global depth ⇒ **directory doubles** and a split image is created; directory now 0 / 1, each bucket local depth 1 |
| 11 | `1011` | Goes into the bucket with 45 — that bucket becomes full |
| 15 | `1111` | **Overflow.** Global depth = local depth ⇒ **directory doubles** and a split occurs; directory now 00 / 01 / 10 / 11 |
| 10 | `1010` | **Overflow**, but **local depth < global depth** ⇒ split image created, **directory is NOT doubled** |

> [!note] How to read the last two steps
> After the second doubling the directory has four entries, but not every bucket needed to split. When a bucket whose local depth is already below the global depth overflows, the directory already contains a free entry pointing at it, so we only split the bucket and re-point that entry — exactly the "directory not doubled" line in the deck.

> [!tip] Exam pointer — extendible hashing
> Have ready: the definition of global depth (directory bits) and local depth (common suffix); "full + local = global ⇒ double"; "full + local < global ⇒ split only"; deletion merge when less than half full, halve the directory when every local depth is one below global.

### 1.17 Linear hashing — structure and the hash-function family

Linear hashing **does not require a separate directory structure** — the price of extendible hashing's extra indirection is avoided.

It uses a **family of hash functions** $h_0, h_1, h_2,\dots$, where the range of $h_i$ is **double** the range of $h_{i-1}$:

$$ h_i(x) = x \bmod (2^i M), \qquad h_0(x) = x \bmod M,\quad h_1(x) = x \bmod 2M $$

where $M$ is the **initial number of buckets** and the hashing field is assumed to be an integer.

![[DBMS - Linear Hashing.excalidraw]]

*Figure — main buckets $0\ldots M-1$, the new split images $M, M+1$, the split pointer $N$, and an overflow chain.*

### 1.18 Insertion in linear hashing

**Initially:** $M$ main buckets $(0,\dots,M-1)$ plus a few overflow buckets. To insert a record with hash-field value $x$, place it in bucket $h_0(x)$.

**On the first overflow (say it occurs in bucket $s$):**

1. Insert the overflowing record into the **overflow chain of bucket $s$**.
2. **Create a new bucket $M$**.
3. **Split bucket $0$** using $h_1$ — irrespective of where the overflow occurred. Some records stay in bucket $0$, some go to bucket $M$ (the **split image**).

**On subsequent overflows:** buckets $1, 2, 3,\dots$ are split **in that order** — hence the name **linear hashing**. Let $N$ be the **next bucket to be split**.

**After $M$ overflows:** all original $M$ buckets have been split. Switch to the pair $h_1, h_2$ and **reset $N = 0$**; the process repeats with the next pair $h_i, h_{i+1}$.

| Phase | Hash functions in use | Split pointer |
| --- | --- | --- |
| Start | $h_0$ | $N = 0$ |
| First $M$ overflows | $h_0,\ h_1$ | $N = 0,1,\dots,M-1$ |
| Next $M$ overflows | $h_1,\ h_2$ | $N = 0,1,\dots$ |
| Later | $h_i,\ h_{i+1}$ | reset to 0 each time the round completes |

### 1.19 Nature of the hash functions

This is the arithmetic that makes the split predictable. Let $M' = 2^i M$ be the **current number of original buckets** and $h_i(x) = x \bmod M'$.

If $h_i(x) = k$, then $x = M'r + k$ with $k < M'$. Applying the next function:

$$ h_{i+1}(x) = (M'r + k) \bmod 2M' = \begin{cases} k, & r \text{ even} \\ M' + k, & r \text{ odd}\end{cases} $$

because for even $r = 2s$, $(M'\cdot 2s + k) \bmod 2M' = k$, and for odd $r = 2s+1$, $(M'(2s+1)+k) \bmod 2M' = M' + k$.

So a record in original bucket $k$ has exactly two possible homes under the next function: **$k$ itself or $k + M'$**. That is precisely why splitting one bucket creates **one** new bucket $k+M'$ and never needs a directory.

### 1.20 Linear hashing — the full worked example

**Setup (deck p. 29–30):** initial buckets $=1$, capacity $=2$, $h_0 = x \bmod 1$, $h_1 = x \bmod 2$, $N=0$.

| Step | Deck's annotation | Resulting state |
| --- | --- | --- |
| Insert 12, 11 | — | bucket 0 = {12, 11}, $N=0$ |
| Insert 14 | **B0 overflows**; bucket pointed to by $N$ is split; hash functions are changed | $h_0 = x\bmod 2,\ h_1 = x\bmod 4$; bucket 0 = {12, 14}, bucket 1 = {11} |
| Insert 13 | inserted at leaf value $h_0(13)=1$ | bucket 1 = {11, 13} |
| Insert 9 | **B1 overflows**; a bucket is split using $h_1$ and a split image is created | bucket 0 = {12}, bucket 1 = {11, 9, 13}, new bucket 2 = {14} |
| Insert 10 | $h_1$ applied here | bucket 2 = {14, 10} |
| Insert 18 | **overflow at B2**; split at the split pointer with $h_1$ | $h_0 = x\bmod 4,\ h_1 = x\bmod 8$; buckets: 0 = {12}, 1 = {9, 13}, 2 = {14, 18, 10}, 3 = {11} |

*Figure — the deck's split picture at the first overflow (deck p. 29).*

![[DBMS - Linear Hashing Split (deck p29).png|470]]

> [!warning] Read the example as the deck prints it
> The split-pointer labels in this hand-annotated example are terse (the "B1 overflows / split using $h_1$" step is printed as a split of the bucket at the pointer, producing bucket 2). Trust the **rule** from §1.18 — buckets split in the order $0,1,2,\dots$, $N$ is the next to split, reset after a full round — over trying to re-derive every pointer label.

> [!tip] Exam pointer — extendible vs linear
> **Extendible:** directory + global/local depth; doubling is sudden but lookup is one directory hop + one bucket. **Linear:** no directory, buckets split one at a time in order; more overflow chains, but no doubling event and no indirection. The book makes the same comparison and adds that mostDBMSs prefer $B^+$ trees for disk data because splits are low-cost and range queries work.

### 1.21 Index structures — the three kinds

> [!important] Definition — index
> An **index** is a **disk data structure** that enables efficient retrieval of a record given the value(s) of certain attributes, called the **indexing attributes**.

| Index | Built on | File requirement |
| --- | --- | --- |
| **Primary index** | the **ordering key field** of a file | file must be ordered on that key field |
| **Clustering index** | an **ordering non-key field** | file must be ordered on that non-key field |
| **Secondary index** | **any non-ordering field** | works on any file, ordered or not |

The book uses slightly different wording — *clustering index* = index whose search key defines the file's sequential order (also called primary), and *secondary / nonclustering* = an order different from the file's — but the three-way split above is the deck's exam vocabulary.

### 1.22 Primary index — structure

A **primary index** can be built on ordered / sorted files.

- **Index attribute:** the ordering key field (OKF).
- **Index entry:** the value of the OKF for the **first record of a block $B_j$**, together with the **disk address of $B_j$**.
- **Index file:** an ordered file, sorted on the OKF; its size is the **number of blocks in the data file** (one entry per data block, not per record).

![[DBMS - Primary Index.excalidraw]]

*Figure — index entries point at data blocks; there is one entry per block and it carries that block's first OKF value.*

Because an index entry is smaller than a data record, its blocking factor is larger:

$$ \boxed{\ \mathrm{BF}_i = \frac{B}{V+P}\ },\qquad b_i = \frac{b}{\mathrm{BF}_i} $$

where $B$ is block size, $V$ the OKF size, $P$ the block-pointer size, $b$ the number of data blocks. The index blocking factor is **generally more than the data-file blocking factor**.

### 1.23 Record access using the primary index

Given an OKF value $x$:

1. Carry out **binary search on the index file**. Let $m$ be the OKF value of the first record in the **middle block $k$** of the index file.
2. If $x < m$: continue binary search on blocks $0,\dots,k-1$ of the index file.
3. If $x \ge m$: check whether block $k$ contains an index entry with OKF value exactly $x$.
   - **Yes** → use its block pointer, fetch the data block, and search that block for the record with value $x$.
   - **No** → binary-search blocks $k+1,\dots,b_i$ of the index file.

$$ \text{maximum block accesses (index search)} = \lceil \log_2 b_i \rceil $$

plus **one** access to the data block that holds the record.

> [!note] Why one entry per block is enough
> In a sorted file, all records with OKF values between the first value of block $B_j$ and the first value of block $B_{j+1}$ must live in $B_j$. The index entry is a *sparse* index: it brackets a whole block, so it is small yet still finds any record.

### 1.24 Primary index — worked example (9,500 blocks)

**Data file:** $b = 9500$ blocks, $B = 4\ \text{KB}$, OKF length $V = 15$ bytes, block pointer $p = 6$ bytes.

**Index file:** $r_i = 9500$ entries, each of length $V+P = 21$ bytes.

$$ \mathrm{BF}_i = \frac{4096}{21} = 195,\qquad b_i = \frac{9500}{195} = 49 $$

| Method | Block accesses |
| --- | --- |
| With primary index | $1 + \log_2 b_i = 1 + \log_2 49 \approx 7$ |
| Without primary index | $\log_2 b = \log_2 9500 \approx 14$ |

A **halving** of disk accesses just by adding a 49-block index file.

### 1.25 Making the index multilevel

An index file is itself an ordered file, so **another level of index can be built on it**. Keep adding levels until the **top level has one block**.

- **height** = number of index levels.
- **block accesses** = $\text{height} + 1$ — and **no binary search is required** at each level, because the top level is small enough to stay in memory and each lower level is entered through a pointer.

![[DBMS - Multilevel Index.excalidraw]]

*Figure — top: 1 block; first level: 49 blocks; data file: 9500 blocks.*

For the 9,500-block data file of §1.24:

| Method | Block accesses |
| --- | --- |
| Multilevel primary index | $3$ (top + first level + data) |
| No index at all | $14$ |

> [!note] Book numbers, same idea
> Silberschatz (§14.2.2) gives a 10,000-block index needing $\lceil \log_2 10000\rceil = 14$ random reads, versus 1 index-block read with a two-level sparse index — "14 times as many index searches per second". That is exactly the deck's point expressed as throughput.

### 1.26 Range search, insertion and deletion on the primary index

**Range search on the OKF** (get records with OKF value in $[x_1,x_2]$, inclusive):

1. Use the index to locate the record with OKF value $x_1$.
2. Read **succeeding records** until the OKF value exceeds $x_2$.
3. Very efficient, because the data file is sorted on that field.

**Insertion:** keep **25% of the space in each block free** to absorb future insertions — then the index does not change. Alternatively, use **overflow chains** for blocks that overflow.

**Deletion:** use **deletion markers** so the index is not affected.

> [!important] The governing principle
> **Basically, avoid changes to the index.** Every technique here exists so that inserting or deleting a data record does not force a rewrite of the (sorted, carefully packed) index file.

### 1.27 Clustering index

Built on an **ordered file whose ordering field is not a key**.

- **Index attribute:** the ordering field (OF).
- **Index entry:** a **distinct value $V_i$** of the OF together with the **address of the first block that has a record with OF value $V_i$**.
- **Index file:** ordered (sorted on OF); its size is the **number of distinct values of OF** — not the number of blocks and not the number of records.

> [!note] Why one entry per distinct value
> With a non-key ordering field, many consecutive records share the same OF value. One entry per *distinct* value points at the start of that run; all the records of the run are then found sequentially. Compare: primary index → one entry per **block**; clustering index → one entry per **distinct value**.

### 1.28 Secondary index — the two cases

A **secondary index** is built on any **non-ordering field (NOF)** of a data file.

**Case I — the NOF is also a key (a secondary key).**

$$\text{index entry} = \langle \text{NOF value } V_i,\ \text{pointer to the record with } V_i \rangle$$

**Case II — the NOF is not a key.** Two options:

1. $\langle V_i,\ \text{pointer(s) to all records with } V_i\rangle$ — an index entry of **variable length**.
2. $\langle V_i,\ \text{pointer to a block that holds pointers to the records with } V_i\rangle$ — an index entry of **fixed length**, at the cost of **one more level of indirection**.

![[DBMS - Secondary Index.excalidraw]]

*Figure — from left to right: secondary key; non-key with a list of record pointers; non-key with a block of pointers.*

> [!note] Why variable length is undesirable on disk
> A variable-length index entry makes it hard to pack entries densely and to binary-search by position. Option 2 keeps every entry the same size by inserting one extra block pointer — the classic space-for-regularity trade.

### 1.29 Secondary index on a key — worked example

A secondary index on a key can be built on ordered **and** other types of files.

- **Index attribute:** non-ordering key field.
- **Index entry:** NOF value $V_i$ + pointer to the record with $V_i$.
- **Index file:** ordered (sorted on NOF), with as many entries as there are **records** in the data file (unlike the primary index, which has one entry per **block**).

$$ \mathrm{BF}_i = \frac{B}{V+P_r},\qquad \text{index blocks} = \left\lceil \frac{r}{\mathrm{BF}_i} \right\rceil $$

($P_r$ = record-pointer length, $r$ = number of data records.)

**Example (deck p. 40).** Data file: $r = 90{,}000$, $B = 4\ \text{KB}$, record length $R = 100$ bytes ⇒ $\mathrm{BF} = 4096/100 = 40$, $b = 90000/40 = 2250$. NOF length $V = 15$, record pointer $P_r = 7$.

$$ \mathrm{BF}_i = \frac{4096}{22} = 186,\qquad b_i = \frac{90000}{186} = 484 $$

| Method | Block accesses |
| --- | --- |
| With secondary index | $1 + \log_2 b_i \approx 10$ |
| Without secondary index | $b/2 = 1125$ (average sequential scan) |

> "A very significant improvement" — the deck's own conclusion. This is the number that justifies building indexes at all.

### 1.30 Multilevel secondary index — worked example

1. The **first level** has as many entries as there are records in the data file (90,000).
2. The first level is an ordered file, so the **second level** has one entry per **block of the first level** (484) rather than per record.
3. Higher levels follow the same rule.

Block accesses with a multilevel index = **height + 1**.

For the deck's example: a multilevel secondary index needs **4** block accesses, versus **10** for a single-level secondary index (and 1125 for no index). The top of the tree is 1 block; the first level spans 484 blocks; the data file spans 2250 blocks.

### 1.31 ISAM files

**ISAM (Index Sequential Access Method) files** are ordered files with a **multilevel primary / clustering index**.

- **Insertions:** handled with **overflow chains** at the data file blocks.
- **Deletions:** handled with **deletion markers**.
- **Best for** files that are **relatively static**.

If the files are **dynamic**, we need a dynamic multilevel index structure based on **$B^+$ trees** — the bridge to the rest of the topic.

### 1.32 $B^+$ trees — the idea and the properties

A $B^+$ tree is a **balanced search tree**: all leaves are at the same level.

> [!important] Properties (deck p. 44)
> - **Balanced:** every root-to-leaf path has the same length.
> - **Leaves** hold entries pointing to the actual data records, and **all leaf nodes are chained together as a list** → sequential access is possible.
> - **Internal nodes carry only index information.** In a **B-tree**, internal nodes carry data records too, so their **fan-out is less** (a shorter, busier tree).
> - Blocks are always **at least half filled**.
> - Supports **both random and sequential access**.

![[DBMS - Bplus Tree Structure.excalidraw]]

*Figure — the deck's tree with $m=3$, $m_{leaf}=2$: root `3 | 7`, internal nodes `2 | –`, `4 | –`, `9 | –`, and the leaf chain at the bottom.*

*Figure — the deck's own $B^+$ tree drawing (deck p. 51).*

![[DBMS - Bplus Tree Example (deck p51).png|470]]

> [!note] How a lookup works (book §14.3.2)
> Start at the root; at each internal node take the pointer whose key interval contains the search value ($x \le K_1$, $K_{i-1} < x \le K_i$, or $x > K_{j-1}$). At the leaf, if a key equals the value, its record pointer is returned. A **range query** descends once to the first leaf and then follows the leaf chain — this is why the linked leaves matter.

### 1.33 Order of internal and leaf nodes

> [!important] Definitions
> **Order $m$ of an internal node** = the **maximum number of tree pointers** it can hold. It can therefore hold at most $m-1$ keys.
> **Order $m_{leaf}$ of a leaf node** = the **maximum number of record pointers** it can hold. This **equals the number of keys** in the leaf.

An internal node of order $m$ obeys:

- At least **2 pointers**, except when it is the root.
- At most **$m$ pointers**.
- With pointers $P_1,\dots,P_j$ and keys $K_1 < \dots < K_{j-1}$, where $\lceil m/2\rceil \le j \le m$:
  - $P_1 \to$ subtree with records having $x \le K_1$.
  - $P_i\ (1<i<j) \to$ subtree with $K_{i-1} < x \le K_i$.
  - $P_j \to$ records with $x > K_{j-1}$.

A leaf node of order $m_{leaf}$ obeys:

- One block pointer $P$ to the **next leaf node**.
- At least $\lceil m_{leaf}/2\rceil$ and at most $m_{leaf}$ record-pointer/key pairs.
- $P_{r_i}$ points to the record whose key is $K_i$; $P$ points to the next leaf block.

![[DBMS - Bplus Tree Node Format.excalidraw]]

*Figure — the internal-node layout $P_1 K_1 P_2 \dots K_{j-1} P_j$ and the leaf-node layout $K_1 P_{r1} K_2 P_{r2} \dots K_j P_j\ P$.*

### 1.34 Order calculation — worked example

Each node must fit in one block of size $B$:

$$ \boxed{\ mP + (m-1)V \le B\ } \quad\text{(internal)},\qquad \boxed{\ m_{leaf}(P_r + V) + P \le B\ } \quad\text{(leaf)} $$

where $V$ = indexing-field size, $P$ = block-pointer size, $P_r$ = record-pointer size.

**Deck example:** $B = 512$, $V = 8$, $P = 6$, $P_r = 7$.

$$ \text{Internal: } 6m + 8(m-1) \le 512 \;\Rightarrow\; 14m \le 520 \;\Rightarrow\; m \le 37 $$
$$ \text{Leaf: } 15\,m_{leaf} + 6 \le 512 \;\Rightarrow\; 15\,m_{leaf} \le 506 \;\Rightarrow\; m_{leaf} \le 33 $$

> [!tip] Exam pointer — order
> The internal node has one more pointer than keys, hence the $(m-1)V$; the leaf has exactly as many keys as record pointers **plus** one next-leaf block pointer, hence $m_{leaf}(P_r+V)+P$. Getting these two equations right is a common mark-scorer.

### 1.35 Insertion into $B^+$ trees

**Every record is inserted at the leaf level.**

**If the leaf overflows:**

1. Split at $j = \lceil (m_{leaf}+1)/2\rceil$.
2. Keep the first $j$ entries in the original node.
3. Move entries from $j+1$ onward into the new node.
4. **Replicate** the $j$-th key value in the parent of the leaf.

**If an internal node overflows:**

1. Split at $j = \lceil (m+1)/2\rceil$.
2. Keep values and pointers **up to $P_j$** in the original node.
3. **Move** the $j$-th key value up into the parent of the internal node.
4. Move $P_{j+1}$ and the rest of the entries into the new node.

![[DBMS - Bplus Tree Insertion Split.excalidraw]]

*Figure — a full leaf splits at $j$, the right half moves to a new leaf, and the $j$-th key is replicated in the parent.*

> [!warning] Replicate vs move
> **Leaf split → the $j$-th key is replicated** (it still appears as the first key of the new leaf, and a copy goes up). **Internal split → the $j$-th key is moved** up (it no longer stays in either internal node). Swapping these two is the classic error in a trace.

### 1.36 $B^+$ tree insertion — worked example

Continuing the deck's tree with $m = 3$, $m_{leaf} = 2$:

| Insert | Effect (deck p. 53–55) |
| --- | --- |
| 20, 11 | Both go into a leaf; when it overflows the leaf is split at $j = \lceil(2+1)/2\rceil = 2$ and key **14 is replicated** to the upper level |
| 14 | Inserted at the leaf level into the left leaf |
| 25 | Inserted at the leaf level |
| 30 | Leaf overflows; split at 25; **25 is moved up**; a new leaf is created |
| 12 | Leaf overflow → **triggers overflow at the internal node** → split occurs at the internal node too: split at 14 and **14 is moved up**; the tree grows a new root level |
| 22 | Inserted at the leaf level |
| 23, 24 | Inserted at the leaf level; the leaf now holds 20, 22, 23, 24 |

*Figure — the deck's insertion sequence (deck p. 53).*

![[DBMS - Bplus Tree Insertion Example (deck p53).png|470]]

### 1.37 Deletion in $B^+$ trees

1. **Delete the entry from the leaf node.**
2. **Delete the entry from the internal node too if it is present there**, and replace it with the entry to its **left** in that position.
3. If **underflow** occurs after deletion, repair in this order:
   1. **Distribute entries from the left sibling** (if it has spare entries).
   2. Else **distribute entries from the right sibling**.
   3. Else **merge the node with its left and right sibling**.

> [!note] Why "the entry to its left"
> An internal key $K_i$ is the separator between the subtree with $x \le K_i$ and the one with $x > K_i$. If the smallest key of the right subtree is deleted, the separator must become the next smaller key — the entry immediately to its left in the leaf chain.

### 1.38 $B^+$ tree deletion — worked example

Continuing from §1.36 (deck p. 57–59):

| Delete | Effect |
| --- | --- |
| 20 | Removed from the **leaf only**; it is not a separator in an internal node |
| 22 | Removed from the **leaf and the internal node**; entries from the **right sibling are distributed** to the left |
| 24 | Leaf entry removed; the tree now has separators 12 and 23, 25 |
| 14 | Internal separator 14 is replaced by 12 (the entry to its left) |
| 12 | **Level drop has occurred** — the root loses its last pointer and the tree becomes shallower |

*Figure — the deck's deletion drawings (deck p. 57).*

![[DBMS - Bplus Tree Deletion Example (deck p57).png|470]]

> [!tip] Exam pointer — insertion and deletion
> Be ready to (i) compute $m$ and $m_{leaf}$ from $B, V, P, P_r$; (ii) trace a split and say whether the promoted key is **replicated** (leaf) or **moved** (internal); (iii) apply the three-step underflow repair in order; (iv) recognise a **level drop** at deletion.

### 1.39 Advantages and disadvantages of $B^+$ trees

**Advantages**

1. **Any record can be fetched in an equal number of disk accesses** (balanced tree).
2. **Range queries are easy**, because the leaves are linked.
3. **The height is less** — only keys are used for indexing, so fan-out is high (unlike a B-tree, whose internal nodes also hold records).
4. Supports **both random and sequential access**.

**Disadvantages**

1. **Insert and delete operations are complicated** (split, redistribute, merge, level changes).
2. **The root node becomes a hotspot** — every lookup starts there, so it is constantly needed.

> [!note] Book's comparison
> Silberschatz (§24.5.3) adds that most DBMSs use $B^+$ trees for disk data: they support range queries, handle growth through **low-cost node splits** (unlike the sudden doubling of extendible hashing), and give good worst-case deletion bounds with duplicate keys. Hash indices survive mainly for in-memory work such as hash joins.

---

## Formula Summary

| Quantity | Expression | Notes / validity |
| --- | --- | --- |
| Access time | $\text{seek} + \text{rotational delay}$ | seek $12$–$14$ ms, rotation $3$–$4$ ms avg |
| Blocking factor | $b = B/r$ | max whole records per block; discard fraction |
| Static hash capacity | $C = r\cdot M$ | $r$ records/bucket, $M$ main buckets |
| Extendible hash | directory size $= 2^d$ | $d$ = global depth (trailing bits) |
| Extendible split | double directory iff local depth $=$ global depth | else split image only |
| Linear hash function | $h_i(x) = x \bmod 2^i M$ | $h_0=x\bmod M$, $h_1=x\bmod 2M$ |
| Linear split destinations | $k$ or $k+M'$, $M'=2^i M$ | $r$ even → $k$; $r$ odd → $k+M'$ |
| Primary index blocking factor | $\mathrm{BF}_i = B/(V+P)$ | one entry per data block |
| Primary index size | $b_i = b/\mathrm{BF}_i$ | $b$ = number of data blocks |
| Primary index search | $\lceil \log_2 b_i\rceil + 1$ | binary search + one data block |
| Multilevel search | $\text{height} + 1$ | no binary search at each level |
| Secondary index (key) | $\mathrm{BF}_i = B/(V+P_r)$, blocks $=\lceil r/\mathrm{BF}_i\rceil$ | one entry per record |
| $B^+$ internal order | $mP + (m-1)V \le B$ | max $m$ pointers, $m-1$ keys |
| $B^+$ leaf order | $m_{leaf}(P_r+V) + P \le B$ | plus one next-leaf pointer |
| $B^+$ split point | $j=\lceil(m_{leaf}+1)/2\rceil$ (leaf), $j=\lceil(m+1)/2\rceil$ (internal) | leaf key replicated, internal key moved |

> [!note] Source images
> All `DBMS - …excalidraw` drawings are original schematic reconstructions of the deck's diagrams and live in the vault-root `Excalidraw/` folder. The `DBMS - … (deck pN).png` figures are page renders of [[file-management.pdf]], stored in `DBMS/images/`, and each is captioned with the slide it came from. All numbers, conventions and worked traces come from the deck; the Silberschatz textbook ([[silberschatz_dbms.pdf]], Ch. 13–14 and §24.5) was used for explanation only.
