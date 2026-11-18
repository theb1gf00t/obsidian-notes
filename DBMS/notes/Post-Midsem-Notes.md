---
title: DBMS — Post-Midsem Notes (File Organization, Query Algorithms, Transactions)
tags:
  - dbms
  - DBMS
  - file-management
  - indexing
  - transactions
  - query-algorithms
  - joins
  - post-midsem
---
	
# Post-Midsem — File Organization and Indexing · Query Algorithms · Transactions

This block is the storage-and-retrieval half of the DBMS course. It starts at the physical bottom — a disk is a stack of spinning platters, and the only unit it can move is a **block** — and works upward: records must be packed into those blocks (§1.1–§1.6), a **file organization** decides how the records are placed (§1.7–§1.11), and when the file grows or shrinks the placement must change without breaking access (§1.12–§1.20). The other half of the story is the **index**: an auxiliary structure that turns a full-file scan into a handful of block reads, first as a simple ordered file (§1.21–§1.31) and finally as a self-balancing $B^+$ tree (§1.32–§1.39). Topic 2 (query algorithms — selection, external sorting, joins, optimization) is written below as §2; topic 3 (transactions) is written below as §3.

*Topic list and progress: [[Syllabus]] · formatting rules: [[context]] · book: [[silberschatz_dbms.pdf]] (Ch. 13 "Data Storage Structures", Ch. 14 "Indexing", §24.5 "Hash Indices").*

> [!info] How the block is organised
> | Topic | Deck | Slides | Question it answers |
> | --- | --- | --- | --- |
> | 1 | [[file-management.pdf\|file-management deck]] | 60 | How are records placed on disk, and how do indexes make them findable? |
> | 2 | [[algos.pdf\|algos deck]] | 32 | How does the DBMS execute a query (sorting, joining, selecting)? |
> | 3 | [[transactions.pdf\|transactions deck]] | 36 | How are concurrent, failure-prone updates kept correct? |
>
> All three topics are now written; progress is tracked in [[Syllabus]].

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

#### Intuition — a restaurant kitchen and its order book

Think of the **main-memory buffer** as the cook's counter and the **disk** as the permanent order book. If the cook decides *himself* when to copy a finished order into the book, then after a power cut the book always agrees with what the kitchen promised the customer. If a helper (the OS) copies pages "whenever it feels like it", some promises exist only on the counter and are lost. The DBMS therefore insists on being the one who says *"write this page now"*.

> [!example] Illustrative example (not from the deck)
> A bank transfer updates two blocks: *debit A* and *credit B*. If the OS happens to flush the debit block but crashes before the credit block, the money has vanished. Because the DBMS controls the flush order (log first, then data), it can undo or redo the half-finished transfer after the crash.

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

#### Intuition — why only the block counts

A disk is like a **record player with several records stacked on one spindle**. Moving the arm to the right groove (seek) is by far the slowest step; waiting for the groove to spin round (rotational delay) is the second; actually reading the data once the arm is there is tiny. So the DBMS tries hard to *read a lot of useful data per arm movement* — that is why the unit of transfer is a whole block, and why blocks of one file are best kept on the same or neighbouring cylinders.

> [!example] Illustrative example (not from the deck) — random vs sequential
> Take the deck's figures: seek $\approx 13$ ms and rotational delay $\approx 3.5$ ms, so one **random** block access costs about $13 + 3.5 = 16.5$ ms.
> - Reading 100 blocks scattered all over the disk: $100 \times 16.5 = 1650$ ms.
> - Reading 100 blocks that sit on the same cylinder: one seek and one rotational wait, then the blocks stream past the head, so the cost is close to $16.5$ ms plus pure transfer time.
>
> This factor of roughly *tens* is why "contiguous allocation" and "number of **random** block accesses" are the two phrases that dominate the rest of the topic.

> [!tip] Exam pointer — the cost model
> Know the two components and their numbers: seek $12$–$14$ ms, rotational delay $3$–$4$ ms. Every later "this is faster" claim (binary search on an index, contiguous scanning, multilevel index) is really a claim about **fewer random block accesses**.

### 1.3 Data records and files — fixed length vs variable length

A file is a sequence of records; the *shape* of a record determines how simply it can be located.

**Fixed-length record type.** Every field has a fixed length. Because every record occupies the same number of bytes, **the record number can be used to locate a specific record** by direct arithmetic. The **file header** stores the number of records and the length of each field.

**Variable-length record type.** These arise from (i) **missing fields**, (ii) **repeating fields**, and (iii) **intrinsically variable-length fields**. **Special separator symbols** mark field boundaries and record boundaries; the file header records the number of records and which separator symbols are in use.

> [!example] Illustrative example (not from the deck) — the same student table, two ways
> **Fixed length:** `rollNo` (6 bytes) + `name` (20 bytes, padded with blanks) + `cpi` (4 bytes) = **30 bytes for every student**. The 1000th record starts at byte $999 \times 30 = 29970$ — no searching, just multiplication. The price: a student named "Li" still occupies 20 bytes for the name.
>
> **Variable length:** `101,Li,8.5#102,Alexandrina Fernandes,9.1#103,,7.9#` — here `,` separates fields, `#` separates records, and student 103's *missing* name is simply an empty field. Space is saved, but to find the 1000th record you must scan and count `#` symbols (or keep an offset table). The file header records which separator symbols are in use, exactly as the deck says.

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

> [!example] Illustrative example (not from the deck) — computing the blocking factor
> Let $B = 4096$ bytes and $r = 100$ bytes. Then $b = \lfloor 4096/100 \rfloor = 40$ records per block, using $40 \times 100 = 4000$ bytes; the remaining $96$ bytes of every block are **wasted** because a 41st record would not fit and (unspanned) may not straddle a boundary.
> A file of $r_{file} = 90{,}000$ records therefore needs $\lceil 90000/40 \rceil = 2250$ blocks — this is exactly the data file used in the secondary-index example of §1.29.
> If instead $r = 5000$ bytes $> B$, a record cannot fit in one block, so a **spanned** organization stores $4096$ bytes in one block and the remaining $904$ bytes at the start of the next block; reading that record now costs *two* block accesses.

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

> [!example] Illustrative example (not from the deck) — a 5-block file
> The file blocks are $F_1,\dots,F_5$.
> - **Contiguous:** $F_1\ldots F_5$ sit in disk blocks $100,101,102,103,104$. To scan, seek once to block 100 and read onward. To *insert a new block between $F_2$ and $F_3$*, blocks $F_3,F_4,F_5$ would all have to shift by one — hard.
> - **Linked:** $F_1\to 17,\ F_2\to 250,\ F_3\to 42,\ F_4\to 911,\ F_5\to 63$, each disk block storing the number of the next. Inserting a new block between $F_2$ and $F_3$ only changes one pointer — easy. But a scan needs five separate seeks.

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

#### Intuition — three ways to keep a pile of exam answer sheets

- **Heap:** drop each new sheet on top of the pile. Adding is instant; finding "roll no. 57" means going through the pile.
- **Sorted:** keep the pile in roll-number order. Finding 57 is quick (open the middle, go left or right), but a late sheet must be squeezed into the middle, disturbing everything after it.
- **Hashed:** have labelled trays (say, by the last digit of the roll number). Both adding and finding go straight to one tray — but "all sheets between 50 and 60" now means checking *every* tray.

| Organization | Insert | Search on the organizing field | Range search | Weak point |
| --- | --- | --- | --- | --- |
| **Heap** | very cheap (last block) | scan whole file | scan whole file | every lookup |
| **Sorted** | costly (shifts later blocks) → auxiliary file | $O(\log N)$ block accesses | efficient (neighbours adjacent) | insertion |
| **Hashed** | cheap (compute bucket) | typically **1** block access | not supported well (hashing scrambles order) | fixed size, range queries |

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

> [!example] Illustrative example (not from the deck) — binary search over blocks
> A sorted student file has $N = 1000$ blocks. To find roll no. $x$: read block 500 (the middle); if $x$ is smaller, search blocks $1$–$499$, otherwise $501$–$1000$; read the middle of that half, and so on. Each read halves the range, so at most $\lceil \log_2 1000\rceil = 10$ block reads are needed, versus up to $1000$ for a heap file.
> *Insertion cost:* inserting roll no. 50 into block 3 forces later records to slide forward, potentially rewriting blocks $3,4,\dots,1000$ — up to 998 block writes. That is why new records go to the small **auxiliary file** and are merged in during the periodic reorganization.

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

> [!example] Illustrative example (not from the deck) — a tiny hashed file
> Let $M = 5$ buckets, each holding $r = 2$ records, and $h(x) = x \bmod 5$ on `rollNo`. Insert $12, 7, 22, 15, 32, 9$:
>
> | Insert | $h(x)$ | Where it goes |
> | --- | --- | --- |
> | 12 | 2 | bucket 2 |
> | 7 | 2 | bucket 2 (now full: 12, 7) |
> | 22 | 2 | bucket 2 is full → **overflow chain** of bucket 2 |
> | 15 | 0 | bucket 0 |
> | 32 | 2 | overflow chain of bucket 2 (22, 32) |
> | 9 | 4 | bucket 4 |
>
> *Search 32:* $h(32)=2$ → read bucket 2 (12, 7: no) → follow the chain (22, 32: found) = 2 block accesses. *Delete 7:* remove it from bucket 2, then bring 22 from the chain into the freed slot so later searches for 22 take one access.

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

> [!example] Illustrative example (not from the deck) — capacity
> With $r = 40$ records per bucket and $M = 100$ main buckets, $C = rM = 4000$ records. If the file holds only 400 records, about 90% of the space is idle (**wastage**). If it grows to 40,000 records, each bucket receives about 400 records on average, i.e. an overflow chain roughly ten buckets long, so a lookup is no longer "one access" but around ten.

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

#### Intuition — a phone book that adds pages by looking at more digits

Imagine sorting contact cards into boxes by the **last digit** of the phone number: 10 boxes. When one box overflows, instead of re-sorting everything, you only **split that box** using the *second-last digit* as well. Boxes that never overflowed keep being addressed by one digit. The **directory** is the little index card that says "numbers ending in 0 → box A, ending in 1 → box B …". Global depth is how many trailing digits (here bits) the index card currently looks at; local depth is how many digits *that particular box* really needed.

> [!example] Illustrative example (not from the deck) — reading a directory
> With $d = 3$ the directory has $2^3 = 8$ entries `000`…`111`. A bucket with local depth $2$ holds every record whose last two bits are, say, `01`, so the two directory entries `001` and `101` **both point to it**. A bucket with local depth $3$ is pointed to by exactly one entry. Number of directory entries pointing to a bucket $= 2^{d - \text{local depth}}$.

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

![[DBMS - Extendible Hashing Trace.excalidraw]]

*Figure — the six insertions as five snapshots; the colour change marks where the directory doubled (orange) and where only a bucket was split (red).*

#### The same example, bucket contents spelled out

The table above says *what happened*; this one shows *why*, by writing the **trailing bits** of each key explicitly (45 = `101101`, 22 = `10110`, 12 = `1100`, 11 = `1011`, 15 = `1111`, 10 = `1010`).

| Step | Directory ($d$) | Bucket contents (with local depth) | Reason |
| --- | --- | --- | --- |
| after 45, 22 | $d=0$: one entry | $\{45, 22\}$ (0) | everything shares the empty suffix |
| insert 12 | $d=1$: `0`, `1` | `0` → $\{22,12\}$ (1); `1` → $\{45\}$ (1) | last bits: 22→`0`, 12→`0`, 45→`1` |
| insert 11 | $d=1$ | `1` → $\{45, 11\}$ (1), full | last bit of 11 is `1` |
| insert 15 | $d=2$: `00`,`01`,`10`,`11` | `00` and `10` → $\{22,12\}$ (1); `01` → $\{45\}$ (2); `11` → $\{11,15\}$ (2) | bucket `1` overflowed with local = global = 1, so double; 2-bit suffixes: 45→`01`, 11→`11`, 15→`11` |
| insert 10 | $d=2$ (unchanged) | `00` → $\{12\}$ (2); `10` → $\{22,10\}$ (2); `01` → $\{45\}$; `11` → $\{11,15\}$ | 10 has suffix `10` and bucket $\{22,12\}$ is full with local depth $1<2$: split by the 2nd bit — 22→`10`, 10→`10`, 12→`00` |

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

#### Intuition — no index card, just a predictable order of splitting

Extendible hashing needs a directory because the bucket that splits is the one that overflowed, so the system must remember where everything went. Linear hashing removes the directory by making the splitting order **fixed and public**: bucket 0, then 1, then 2, …, no matter who overflowed. Anyone can then work out where a record lives from just two numbers: the current hash functions and the pointer $N$. The cost is that the overflowing bucket may have to wait (using an overflow chain) until its turn to be split.

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

**Where does a record go while a round is in progress?** (deck p. 28, "Insertion (3/3)") Say the hash functions in use are $h_i, h_{i+1}$. To insert a record with hash-field value $x$, compute $h_i(x)$:

- if $h_i(x) < N$, the original bucket $h_i(x)$ **has already been split** in this round, so place the record in bucket $h_{i+1}(x)$;
- otherwise place the record in bucket $h_i(x)$.

> [!example] Illustrative example (not from the deck)
> Suppose $M=4$ (so $h_0 = x \bmod 4$, $h_1 = x \bmod 8$) and buckets $0$ and $1$ have been split, i.e. $N = 2$. Insert $x = 13$: $h_0(13) = 1 < N$, bucket 1 was already split, so use $h_1(13) = 5$ → the split image, bucket 5. Insert $x = 14$: $h_0(14) = 2 \ge N$, bucket 2 has not been split yet → bucket 2.

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

![[DBMS - Linear Hashing Trace.excalidraw]]

*Figure — the example as four snapshots, with the hash functions and $N$ at each stage.*

#### The same example, step by step with the rule of §1.18

| Step | Active functions, $N$ | Computation | Result |
| --- | --- | --- | --- |
| 12, 11 | $h_0 = x \bmod 1$, $N=0$ | both give bucket 0 | $0:\{12, 11\}$ (full) |
| 14 | same | $h_0(14)=0$, bucket full → overflow. Split bucket $N=0$ using $h_1 = x \bmod 2$: $12\to0$, $14\to0$, $11\to1$. All $M=1$ original buckets are now split → round ends | $0:\{12,14\}$, $1:\{11\}$; new functions $h_0 = x\bmod 2$, $h_1 = x \bmod 4$, $N=0$ |
| 13 | $N=0$ | $h_0(13)=1 \ge N$ → bucket 1 | $1:\{11,13\}$ |
| 9 | $N=0$ | $h_0(9)=1$ → bucket 1 is full → overflow chain. Split bucket $N=0$ with $h_1 = x \bmod 4$: $12\to0$, $14\to2$. Then $N=1$ | $0:\{12\}$, $1:\{11,13\}+\{9\}$, $2:\{14\}$ |
| 10 | $N=1$ | $h_0(10)=0 < N$ → already split → use $h_1(10)=2$ | $2:\{14,10\}$ — this is the deck's note "$h_1$ is applied here" |
| 18 | $N=1$ | $h_0(18)=0 < N$ → $h_1(18)=2$ → bucket 2 full → overflow. Split bucket $N=1$ with $h_1 = x \bmod 4$: $11\to3$, $9\to1$, $13\to1$. All 2 original buckets split → round ends | $0:\{12\}$, $1:\{9,13\}$, $2:\{14,18,10\}$ (one in chain), $3:\{11\}$; new $h_0 = x \bmod 4$, $h_1 = x \bmod 8$, $N=0$ |

> [!warning] Two traps in this example
> - **The bucket that splits is the one at $N$, not the one that overflowed.** Inserting 9 overflowed bucket 1, yet bucket 0 was split. Bucket 1's turn came when 18 overflowed bucket 2.
> - **Check $h_i(x) < N$ before placing a record** (the rule above). That is why 10 and 18 are sent to bucket 2 by $h_1$ even though $h_0$ gives bucket 0.

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

![[DBMS - Index Types Compared.excalidraw]]

*Figure — the three index kinds side by side: what the entry contains and how many entries there are.*

#### Intuition — the index at the back of a textbook

A textbook's **subject index** lists a term and the page numbers where it occurs, so you do not read the whole book. A DBMS index is the same: a small sorted list of `<value, pointer>` that is far shorter than the data. The three kinds differ in how the *book itself* is arranged:

- **Primary:** the book is printed in order of the key (like a dictionary). One bookmark per page ("page 40 starts with *kettle*") is enough — that is the entry-per-block idea.
- **Clustering:** the book is in order of a non-key field (say, pages grouped by *department*). One bookmark per department, pointing to where that department's run begins.
- **Secondary:** the book is not in order of the field you care about (say, you want to look up by `name` in a file ordered by `rollNo`). Every record needs its own index entry, because records with neighbouring names are scattered.

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

> [!example] Illustrative example (not from the deck) — a four-block file
> Data blocks (sorted on `rollNo`): $B_0=\{101,104,110\}$, $B_1=\{121,123,127\}$, $B_2=\{129,133,138\}$, $B_3=\{140,145,150\}$.
> The primary index has just four entries: $\langle101,B_0\rangle,\ \langle121,B_1\rangle,\ \langle129,B_2\rangle,\ \langle140,B_3\rangle$.
> *Find 133:* the largest index value $\le 133$ is $129$ → fetch $B_2$ and scan it → found. *Find 125:* the largest value $\le 125$ is $121$ → fetch $B_1$ → not there, so 125 does not exist. We never needed an entry for 123 or 133 themselves.

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

#### Following the arithmetic in plain words

1. Each index entry is a key (15 bytes) plus a block pointer (6 bytes) = **21 bytes**, much smaller than a data record, so one 4096-byte block holds $\lfloor 4096/21 \rfloor = 195$ entries.
2. There is one entry for each of the 9500 data blocks, so the index has $9500/195 \approx 48.7$, rounded up to **49 blocks**.
3. Searching 49 index blocks by binary search needs about $\log_2 49 \approx 5.6 \to 6$ reads, plus one read of the data block: $\approx 7$.
4. Binary search directly on the 9500 data blocks needs $\log_2 9500 \approx 13.2 \to 14$ reads.

The index is "small enough to binary-search cheaply", which is the whole trick.

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

> [!example] Why the top level is one block here
> The first-level index has 49 blocks, so the second level needs one entry per first-level block: **49 entries**, which fit in a single block (195 entries fit per block). Because that top block is one block, the process stops there. A lookup reads **1 top block → 1 first-level block → 1 data block = 3 accesses**, picking the correct block each time by direct comparison with the keys already in memory — no binary search needed.

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

> [!example] Illustrative example (not from the deck) — clustering index on `dept`
> The file is sorted on `dept`: block $B_0=\{\text{CS},\text{CS},\text{CS}\}$, $B_1=\{\text{CS},\text{EE},\text{EE}\}$, $B_2=\{\text{EE},\text{ME},\text{ME}\}$. The index has one entry per **distinct** department: $\langle\text{CS},B_0\rangle,\ \langle\text{EE},B_1\rangle,\ \langle\text{ME},B_2\rangle$ — three entries even though there are nine records and three blocks. To fetch all EE staff: jump to $B_1$, read on through the EE run, and stop at the first non-EE record (in $B_2$).

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

> [!example] Illustrative example (not from the deck) — Case II on `city`
> The file is ordered on `rollNo`; we want fast lookup by `city`. Records with `city = Pune` are rolls 3, 17 and 52.
> - **Option 1:** entry $\langle\text{Pune}, \{p_3, p_{17}, p_{52}\}\rangle$ — as many pointers as there are matches, so entries differ in length.
> - **Option 2:** entry $\langle\text{Pune}, q\rangle$ where $q$ is a block containing $p_3,p_{17},p_{52}$ — every entry is $V + P$ bytes, but lookup needs *one extra block read* (the indirection).

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

#### Following the arithmetic in plain words

1. A data record is 100 bytes, so a 4096-byte block holds 40 records; 90,000 records need $90000/40 = 2250$ blocks.
2. The secondary index needs an entry **per record** (the file is not sorted on this field, so no block-level shortcut exists): 90,000 entries of $15 + 7 = 22$ bytes → $\lfloor 4096/22 \rfloor = 186$ per block → $90000/186 \approx 484$ blocks.
3. With the index: binary search on 484 blocks ($\lceil\log_2 484\rceil = 9$) plus one data block = **10**.
4. Without it: the file is unsorted on this field, so on average half the blocks are scanned: $2250/2 = 1125$.

The index is *bigger* than the primary index above (484 vs 49 blocks) — that is the price of covering every record — yet it is still about **110 times** cheaper than scanning.

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

> [!example] Lookups on the deck's tree ($m=3$, $m_{leaf}=2$)
> The tree: root `3 | 7`; internal nodes `2`, `4`, `9`; leaves `1 2`, `3`, `4`, `6 7`, `8 9`, `12 15`.
> - **Search 7.** At the root, $3 < 7 \le 7$ → middle pointer → internal node `4`: $7 > 4$ → right pointer → leaf `6 7` → key 7 found. Three nodes read (root, internal, leaf) — *every* search reads exactly three nodes, because the tree is balanced.
> - **Range 4 to 9.** Descend once to the leaf `4`; then follow the leaf chain: `4` → `6 7` → `8 9`; the next leaf starts with 12 $> 9$, so stop. No second descent from the root was needed.

#### Intuition — why half-full blocks are a feature

A node that is always at least half full guarantees a minimum fan-out of $\lceil m/2 \rceil$, so the tree can never degenerate into a tall thin chain. Height therefore stays logarithmic with a large base: with the deck's $m = 37$, even a three-level tree can address up to roughly $37^3 \approx 50{,}000$ leaf-level pointers (and more for real, bigger blocks).

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

![[DBMS - Bplus Replicate vs Move.excalidraw]]

*Figure — the same two events with the deck's numbers: a leaf split copies 14 up; an internal split sends 14 up and removes it from both halves.*

**Split points, computed.** For $m_{leaf}=2$: $j=\lceil(2+1)/2\rceil=2$, so an overflowing leaf with 3 keys keeps the first 2 and gives the last 1 to the new leaf. For $m=3$: $j=\lceil(3+1)/2\rceil=2$, so an overflowing internal node (3 keys, 4 pointers) keeps $P_1,K_1,P_2$, sends $K_2$ up, and gives $P_3,K_3,P_4$ to the new node.

*Figure — a full leaf splits at $j$, the right half moves to a new leaf, and the $j$-th key is replicated in the parent.*

> [!warning] Replicate vs move
> **Leaf split → the $j$-th key is replicated** (it still appears as the first key of the new leaf, and a copy goes up). **Internal split → the $j$-th key is moved** up (it no longer stays in either internal node). Swapping these two is the classic error in a trace.

### 1.36 $B^+$ tree insertion — worked example

Continuing the deck's tree with $m = 3$, $m_{leaf} = 2$:

| Insert | Effect (deck p. 53–55) |
| --- | --- |
| 20, 11 | Both go into one leaf, kept sorted: `11 20` (the leaf is full) |
| 14 | Leaf would hold `11 14 20` → **overflow**. Split at $j = \lceil(2+1)/2\rceil = 2$: `11 14` stays, `20` goes to a new leaf, and key **14 is replicated** into a new root |
| 25 | Inserted at the leaf level: right leaf becomes `20 25` |
| 30 | Right leaf would be `20 25 30` → overflow; split at 25: `20 25` stays, `30` moves to a new leaf. The deck says "25 is moved up"; since 25 *also stays in the leaf* this is the leaf-split **replicate** rule. Root becomes `14 25` |
| 12 | Leaf `11 14` would be `11 12 14` → leaf split: `11 12` \| `14`, **12 replicated** into the parent. The parent (the root) would then be `12 14 25` with 4 pointers $>m=3$ → **internal overflow**: split at $j=2$, `14` is **moved up** (it stays in neither half), left internal node `12`, right internal node `25`, and a **new root `14`** — the tree grows one level |
| 22 | Goes to the leaf `20 25`, giving `20 22 25` → overflow; split `20 22` \| `25`, **22 replicated**; the right internal node becomes `22 25` (3 pointers, still legal) |
| 23, 24 | 23 → leaf `25` becomes `23 25`. 24 → `23 24 25` overflows → `23 24` \| `25`, **24 replicated**; right internal node would be `22 24 25` (4 pointers) → internal split: **24 moved up**, giving internal nodes `22` and `25`; root `14 24` |

Final tree after all insertions: root `14 | 24`; internal nodes `12`, `22`, `25`; leaves `11 12`, `14`, `20 22`, `23 24`, `25`, `30` (deck p. 55).

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
| 20 | Removed from the **leaf only**; it is not a separator in an internal node. Leaf `20 22` becomes `22` (still at least half full) |
| 22 | Removed from the **leaf and the internal node** (where it was a separator). The leaf is now empty (underflow), so an entry (23) from the **right sibling is distributed** to it; the internal node's separator becomes `23`. State: root `14 24`; internal `12`, `23`, `25`; leaves `11 12`, `14`, `23`, `24`, `25`, `30` |
| 24 | Leaf `24` is removed; its internal node (`23`) is left with too few pointers, so it is **merged with its right sibling `25`** into one internal node `23 25`, and the root loses key 24. State: root `14`; internal `12` and `23 25`; leaves `11 12`, `14`, `23`, `25`, `30` |
| 14 | Leaf `14` is removed; separator 14 in the root is replaced by 12 (the entry to its left). The left internal node becomes `11`. State: root `12`; internal `11` and `23 25`; leaves `11`, `12`, `23`, `25`, `30` |
| 12 | Leaf `12` is removed and the left part collapses into a single leaf `11 23` shared with the right subtree. The root now has no left subtree of its own: **level drop has occurred** — the old root disappears and the internal node `23 25` becomes the new root, with leaves `11 23`, `25`, `30` |

> [!warning] Reading the last two rows
> The deck shows only the drawings for these steps and no commentary besides "Level drop has occurred". The states above are read directly off slides 58–59; the *reason* for each merge (underflow → borrow from sibling → else merge) follows the rule of §1.37. If a precise node-by-node justification is asked in an exam, redraw from the rule rather than from memory of the pictures.

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

## 2. Query / Join Algorithms (algos)

*Deck: [[algos.pdf|algos deck]] — 32 slides, "Algorithms for Relational Algebra Operators and Query Evaluation", Dr P Sreenivasa Kumar, IIT Madras. Every definition, formula and number below comes from the deck; the book was not needed.*

> [!abstract] Roadmap of this topic — read it as one story
> **The question:** an SQL query is turned into relational-algebra (RA) operators. How does the DBMS actually *execute* each operator on files of blocks, and how does it choose the cheapest way?
> 1. **§2.1–§2.5 — selection and projection:** scan or use an index; **selectivity** decides which condition to use first.
> 2. **§2.6–§2.8 — external sorting:** a sort phase that builds *runs* and a merge phase that combines them; the cost is counted in block accesses. Sorting feeds duplicate elimination, grouping and joins.
> 3. **§2.9–§2.17 — joins:** nested loop, single loop (index), hash, partition hash and sort-merge — each with its block-access cost and the conditions under which it wins.
> 4. **§2.18 — set operations:** adapted from the hash and sort-merge methods.
> 5. **§2.19–§2.22 — query optimization:** rewrite the RA tree with heuristics (algebraic optimization), then pick methods by estimated cost (cost-based optimization), shown on one running example.
>
> **The idea to carry through:** as in topic 1, cost = **number of block accesses**. Every algorithm is a different way of paying fewer of them, given the file sizes, the buffer size $m$, the available indexes and the selectivity.

> [!warning] Notation used in this topic
> - $n$, $b_1$, $b_2$ = number of **blocks** of a file; $m$ = number of **buffer blocks** in memory.
> - $r$ = number of **runs** (external sort); $d$ = **degree of merging**; $h_B(S)$ = block accesses of the index on $B$ for $S$.
> - $\lvert R\rvert$, $\lvert S\rvert$, $\lvert result\rvert$ = sizes **in blocks** in the hash-join costs.
> - $\lceil\ \rceil$ is a ceiling; the deck writes it as $\lceil x\rceil$ around every division in a cost formula.

### 2.1 Relational query evaluation — the operators

The operators whose implementation the deck studies are:

- **Select, Project, Join**
- **Union, Intersect, Difference**

The deck's agenda for the topic is: *how to implement these*, **sorting**, **grouping and aggregation**, *how do indexes help?*, and *any other information that is helpful* (selectivity, file sizes, organization). Each of the following sections answers one of these questions.

### 2.2 Selection with equality conditions

| Condition | Index available? | Method |
| --- | --- | --- |
| Single condition $X = c_1$ | Index on $X$ | **Use the index** |
| Single condition $X = c_1$ | No index on $X$ | **File scan** |
| Conjunction $X_1=c_1$ and $X_2=c_2$ and … and $X_k=c_k$ | Index on **any** $X_i$ | Get the records through that index and **check the other conditions** |
| Conjunction | No index on any $X_i$ | **File scan** |
| Disjunction (several conditions joined by *or*) | Index on any *single* $X_i$ | **Not helpful** — a record may satisfy another disjunct, so the other disjuncts still need a full scan |

> [!note] Why disjunction is harder
> In a conjunction, one indexed condition already narrows the candidates to a superset of the answer, and the rest are filters. In a disjunction, an index on one $X_i$ finds only the records satisfying *that* disjunct; records satisfying the others are missed. The deck's summary: *difficult compared to the conjunctive case*.

### 2.3 Predicate selectivity

> [!important] Definition — selectivity
> **Selectivity $s$ of a condition $C$**, with $0 \le s \le 1$:
>
> $$ \boxed{\ s = \frac{\text{No. of records satisfying } C}{\text{Total no. of records}}\ } $$

The deck's three examples on a student file of $8000$ records:

| Condition | Records satisfying | Selectivity |
| --- | --- | --- |
| $C_1$: `student.dept = "CSE"` | $450$ | $450/8000 = 0.056$ |
| $C_2$: `student.sex = "female"` | $1200$ | $1200/8000 = 0.15$ |
| $C_3$: `student.rollNo = "CS10B032"` | $1$ | $1/8000 = 0.000125$ |

- A **highly selective predicate** has a very *low* selectivity value — $C_3$ is the most selective of the three.
- **Conjunction of conditions:** choose the one that is *most* selective (lowest $s$), get its records, and check the other conditions on them.
- Selectivity values are **estimates, collected offline**.

> [!warning] Low number = highly selective
> The wording is a classic slip: "highly selective" means **small** $s$ (few records survive). In a conjunction, you pick the condition with the *smallest* selectivity value, not the largest.

### 2.4 Selectivity estimation

Selectivity estimates are **maintained in the DB catalog** and **used by the query optimizer**.

| Condition type | Estimate |
| --- | --- |
| Equality on a **key** attribute | $\text{Selectivity} = \dfrac{1}{\text{Total no. of records}}$ |
| Equality on a **non-key** attribute | $\text{Selectivity} = \dfrac{1}{\text{Distinct values of the attribute}}$ |

Sometimes **histograms** are also maintained: for each distinct value or value range, the **number of records**.

> [!example] Illustrative example (not from the deck) — applying the two formulas
> On the 8000-record student file, `rollNo` is a key, so $s = 1/8000 = 0.000125$ — which is exactly the deck's $C_3$. If `dept` has $10$ distinct values, the non-key formula estimates $s = 1/10 = 0.1$ ≈ $800$ records; the *actual* $450/8000 = 0.056$ for CSE differs because values are not uniformly distributed — that gap is what a histogram corrects.

### 2.5 Project operation

For every record in the operand: **access it, take the required attribute values, and construct the result record**.

- **Duplicate elimination** is **costly**; **sort-based or hash-based** methods are used (§2.6–§2.8 for sorting).
- A **file scan becomes essential** — every record must be visited.
- **Apply project after selection, if possible**, to reduce the input to project.

> [!tip] Exam pointer — selection and projection
> Know the three selection cases (single, conjunctive, disjunctive) and why an index helps only the first two; define selectivity with the 450/8000, 1200/8000, 1/8000 numbers; state the two catalog estimates; and say why project follows select.

### 2.6 External sorting — the idea

**Sorting a file** is an often-required operation: duplicate elimination, grouping of records, join, etc. A file is too large for memory, so the **merge-sort principle** is used, with $O(n\log n)$ worst-case complexity for $n$ items. There are **two phases**:

| Phase | What is repeated | Result |
| --- | --- | --- |
| **Sort phase** | read part of the data, sort it, write it | many sorted files called **runs** |
| **Merge phase** | merge some sorted files and write | repeat **till only one sorted file is left** |

### 2.7 Algorithm — sort phase

**Given:** a file of $n$ blocks and buffer memory of $m$ blocks.

1. Repeat the following $\lceil n/m\rceil$ times: **read the next $m$ blocks; sort them in memory; write them to disk as a single file, called a *run*.**
2. The **number of runs** is

$$ \boxed{\ r = \lceil n/m\rceil\ } $$

3. **Complexity:** $n$ block reads and $n$ block writes, i.e. $\boxed{\ 2n \text{ block accesses}\ }$.

### 2.8 Algorithm — merge phase

**Given:** a file of $n$ blocks, memory buffers $m\ (\ge 3)$ blocks, and $r$ runs. The **degree of merging** $d$ is the number of runs merged at a time:

$$ 2 \le d \le (m-1) $$

**Merge phase:** repeat the following $\lceil \log_d r\rceil$ times — **reduce $j$ runs to $\lceil j/d\rceil$ runs** (initially $j = r$) by repeatedly merging $d$ runs at a time into one run:

- use **$d$ buffers, one for each of the next $d$ runs, and one buffer for the result**;
- **get one block at a time** from each run;
- **merge and write** the result to disk, **one block at a time**.

**Complexity.** Each sub-phase reads and writes the entire file, so the merge phase costs $2n\lceil \log_d r\rceil$, and

$$ \boxed{\ \text{Overall} = 2n + 2n\left\lceil \log_d r \right\rceil \text{ block accesses}\ } $$

![[DBMS - External Sort Merge Phase (deck p10).png|520]]

*Figure — the deck's merge-phase picture (deck p. 10): runs $1,2,\dots,d$ merge into one, runs $d+1,\dots,2d$ into the next, and so on, reducing $j$ runs to $\lceil j/d\rceil$; at the bottom, $d$ input buffers (green) each fed from one run file (pink), and one output buffer feeding the merged run.*

> [!note] Why $d \le m-1$
> One buffer per input run plus one for the output needs $d+1 \le m$ buffers, which is the bound $d \le m-1$. The largest allowed $d = m-1$ minimises the number of merge sub-phases $\lceil\log_d r\rceil$, hence the cost.

> [!example] Illustrative example (not from the deck) — a full count
> Take $n = 1000$ blocks and $m = 5$ buffers. **Sort phase:** $r = \lceil 1000/5\rceil = 200$ runs, cost $2n = 2000$. **Merge phase** with $d = m-1 = 4$: $\lceil \log_4 200\rceil = 4$ (since $4^3 = 64 < 200 \le 256 = 4^4$) sub-phases, runs go $200 \to 50 \to 13 \to 4 \to 1$, cost $2n\cdot 4 = 8000$. **Overall** $= 2000 + 8000 = 10000$ block accesses.

> [!tip] Exam pointer — external sorting
> State the two phases, $r=\lceil n/m\rceil$, $2\le d\le m-1$, and the overall cost $2n + 2n\lceil\log_d r\rceil$; remember that every merge sub-phase reads *and* writes the whole file.

### 2.9 Join processing

**Join** is a very important operation. A **2-way join** takes two files of records and a given join condition; a **multi-way join** involves more files. The **choice of algorithm** depends on:

- the **sizes of the files**,
- the **primary organization** of the files,
- the **availability of indices**,
- the **selectivity of the join condition**, etc.

### 2.10 Nested loop join (block nested loop join)

The **brute-force join**:

```
for each record x in R do
   for each record y in S do
      check if x, y join ...
```

**Setup:** two data files $R$ ($b_1$ blocks) and $S$ ($b_2$ blocks), buffer of $m$ blocks.

**Buffer usage:** **one block for the result** of the join; **one for the inner file** (say $S$); **$(m-2)$ for the outer file** ($R$).

For each set of $(m-2)$ blocks of $R$ read in: for each block of $S$, read it in, compute the join and write to the result block; **write the result block to disk whenever it fills up.**

### 2.11 Nested loop join — time taken

- The **outer file** is read once: $b_1$ block accesses.
- The **inner file's blocks are read** $\left\lceil \dfrac{b_1}{m-2}\right\rceil$ times (once per group of $m-2$ outer blocks).

$$ \boxed{\ \text{Overall} = b_1 + \left\lceil \frac{b_1}{m-2}\right\rceil b_2\ } \qquad \text{or, symmetrically,}\quad b_2 + \left\lceil \frac{b_2}{m-2}\right\rceil b_1 $$

the second form when $S$ is in the outer loop and $R$ inside.

> [!important] Which file goes in the outer loop?
> **The one with fewer blocks.**

### 2.12 Nested loop join — worked example

**Setup:** $R$: $b_1 = 5600$ blocks; $S$: $b_2 = 120$ blocks; buffer $m = 52$ blocks, so $m-2 = 50$.

| Outer file | Arithmetic | Disk operations |
| --- | --- | --- |
| $R$ outer | $5600 + \lceil 5600/50\rceil \times 120 = 5600 + 112\times120 = 5600 + 13440$ | $\mathbf{19040}$ |
| $S$ outer | $120 + \lceil 120/50\rceil \times 5600 = 120 + 3\times 5600 = 120 + 16800$ | $\mathbf{16920}$ |

Assuming **10 ms per disk operation**: $19040 \times 10\ \text{ms}\approx 190$ s versus $16920\times10\ \text{ms}\approx 169$ s.

> [!warning] The trap — ceiling, not division
> $\lceil 120/50\rceil = \lceil 2.4\rceil = 3$, not $2.4$. The smaller file in the outer loop wins ($16920 < 19040$), confirming the rule of §2.11 — the saving is $\approx 21$ s here.

### 2.13 Single loop join (index loop join)

**Setup:** files $R$ ($b_1$ blocks) and $S$ ($b_2$ blocks); compute the **equi-join** $R.A = S.B$. We have an **index on one of them**, say on $B$ of $S$.

**Algorithm:** for each record $x$ of $R$ read in, use the index on $B$ of $S$ to get all the matching records (having $B = x.A$).

$$ \boxed{\ \text{Time taken} = b_1 \cdot h_B(S)\ } $$

where $h_B(S)$ is the number of block accesses of the index on $B$ for $S$.

### 2.14 Join selection factor

> [!important] Definition — join selection factor
> **Join selection factor** — the **fraction of records in a file that join with records of the other file** for the given condition.

Consider $\text{professor} \bowtie_{\text{empId} = \text{hod}} \text{department}$: **only 5% of professor rows join** with department rows, while **100% of department rows join** with professor rows.

It impacts the performance of single loop join **when indexes are available on both files**: **loop over the records of the file with the high join selection factor.**

**Deck's example.** Two options:

| Option | Loop over | Probe using | Result |
| --- | --- | --- | --- |
| 1 | professor records | index on `hod` of department | **95% of probes don't give a match** |
| 2 | department records | index on `empId` of professor | **all probes give a match** |

**Option 2 is the right choice.**

### 2.15 Hash join

Consider a 2-way equi-join $R \bowtie_{R.A = S.B} S$ and **assume that $S$ fits into memory.**

1. Use a hash function $h$; **hash the records of $S$ into $M$ buckets using the $B$-values** — called the **partitioning** of $S$.
2. To compute the join result, **hash the records of $R$ one by one using the $A$-values**, with **the same $M$ buckets and the same hash function $h$**.
3. **Matching pairs of records hash to the same bucket**, so each $R$ record is compared only with the records of one bucket.

### 2.16 Partition hash join

Consider $R \bowtie_{R.A=S.B} S$ when **neither $R$ nor $S$ fits into memory**.

**Partition phase** — use a hash function $h$:

- hash the records of $R$ into $m$ buckets using the $A$-values, giving $R_1, R_2,\dots,R_m$ — **written to files**;
- hash the records of $S$ into $m$ buckets using the $B$-values, giving $S_1, S_2,\dots,S_m$ — **written to files**.

**Goals:** the distribution should be **uniform**, and **at least one of $R_i$ or $S_i$ should fit into memory**. To compute the join result, **join $R_i$ with $S_i$ only** — a record of $R_i$ can never match a record of $S_j$, $j\neq i$.

**Probe phase** — join $R_i$ with $S_i$ for all $i$:

| Case | Method | Overall cost |
| --- | --- | --- |
| One of $R_i$, $S_i$ fits into memory | Use the hash-join idea again: **hash the smaller of the two into memory using a different hash function $h_2$**, read the other file, probe and produce result records | $\boxed{\ 3(\lvert R\rvert + \lvert S\rvert) + \lvert result\rvert\ }$ block accesses |
| Neither fits | Use **nested loops join** on the pair | $2(\lvert R\rvert + \lvert S\rvert)$ + cost of the nested loop joins |

> [!note] Where the 3 comes from
> Partitioning reads and writes both files: $2(\lvert R\rvert+\lvert S\rvert)$. The probe phase reads every partition once more: $+(\lvert R\rvert+\lvert S\rvert)$. Writing the result adds $\lvert result\rvert$. Total $3(\lvert R\rvert+\lvert S\rvert)+\lvert result\rvert$. In the "neither fits" case the $2(\lvert R\rvert+\lvert S\rvert)$ is the partitioning cost and the nested loops replace the single probe read.

> [!warning] Use a *different* hash function in the probe
> The partition uses $h$, so all records of $R_i$ already agree on $h$. Rehashing the in-memory partition with $h$ would put them all in one bucket; hence the deck's $h_2$.

### 2.17 Sort-merge join

Consider $R \bowtie_{R.A=S.B} S$.

- If **$R$ is sorted on $A$ and $S$ is sorted on $B$**: **merge $R$ and $S$** to get the join results — called **merge join**, *very efficient, linear*.
- If **only one of them is sorted** on the join attribute: **sorting the other and merging may be cost-effective**.
- Of course, we can **sort $R$ on $A$, sort $S$ on $B$ and use merge** — but the **cost might be high** (the external sort of §2.8 is added).

### 2.18 Set operations

**Union, Intersect and Difference** can be computed by adapting:

- the **hash-based join method**, and
- the **sort-merge method**.

The deck leaves the details to the student: *"Please study the details!"*

> [!tip] Exam pointer — joins and set operations
> Be able to write the four cost formulas: nested loop $b_1+\lceil b_1/(m-2)\rceil b_2$ (smaller file outside), single loop $b_1\cdot h_B(S)$ (loop over the file with the high join selection factor), partition hash $3(\lvert R\rvert+\lvert S\rvert)+\lvert result\rvert$, and sort-merge (linear after sorting). Reproduce the 19040 vs 16920 example.

### 2.19 Query optimization — overview

An **SQL query is converted to an RA expression tree.** Two stages follow:

1. The initial RA expression is **rewritten using heuristic and algebraic transformation rules**; the final RA expression tree is generated. This is called **algebraic optimization**.
2. **Cost-based query optimization:** the **cost estimates of the methods for the RA operators are computed**, and the **execution plan with the least estimated cost is chosen**.

### 2.20 Heuristic optimization

**Main heuristic rule: apply select and project before other operations.** This

- **reduces the size** of intermediate results, and
- **reduces the number of fields** in the intermediate results.

The optimizer makes use of **relational algebraic laws**:

| Law | Operators |
| --- | --- |
| **Commutative** | select, project, join, union, intersect |
| **Associative** | join, union, intersect |

and there are many more.

### 2.21 Cost-based optimization

The initial expression tree is rebuilt using heuristics and algebraic laws. Then, for each operator:

- it **can be carried out using many methods**;
- for a method, a **cost function gives the estimated cost**, taking **file sizes, access-path costs, etc.** into account;
- the **choice made at a node may affect the choices at others**.

**Evaluate different plans based on estimated costs and choose the plan with least cost.**

### 2.22 Query optimization — worked example

**Query:** obtain the name and phone details of professors who taught the courses taken by the student with roll number `CS08B027` in the even semester of 2010.

```sql
select p.empId, p.name, p.phone
from professor p, teaching t, enrollment e
where e.rollNo = "CS08B027" and e.courseId = t.courseId
      and e.sem = "even" and e.year = 2010
      and t.sem = "even" and t.year = 2010
      and p.empId = t.empId
```

Notation: $p$ = professor, $t$ = teaching, $e$ = enrollment.

**Step 0 — initial RA expression.**

$$ \Pi_{p.empId,\,p.name,\,p.phone}\big(\sigma_\theta(p \times t \times e)\big) $$

$$ \theta = \big(e.rollNo=\text{"CS08B027"} \wedge e.courseId = t.courseId \wedge e.sem=\text{"even"} \wedge e.year = 2010 \wedge t.sem=\text{"even"} \wedge t.year=2010 \wedge p.empId = t.empId\big) $$

**Step 1 — push the single-relation selections down.**

$$ \equiv \Pi_{p.empId,\,p.name,\,p.phone}\big(\sigma_{\theta_3}(p \times \sigma_{\theta_2}(t) \times \sigma_{\theta_1}(e))\big) $$

- $\theta_1 = (e.rollNo=\text{"CS08B027"} \wedge e.sem=\text{"even"} \wedge e.year=2010)$
- $\theta_2 = (t.sem=\text{"even"} \wedge t.year=2010)$
- $\theta_3 = (p.empId=t.empId \wedge e.courseId=t.courseId)$

**Step 2 — split the join conditions between the two products.**

$$ \equiv \Pi_{p.empId,\,p.name,\,p.phone}\big(\sigma_{\theta_3}(p \times \sigma_{\theta_4}(\sigma_{\theta_2}(t) \times \sigma_{\theta_1}(e)))\big) $$

with $\theta_3 = (p.empId = t.empId)$ and $\theta_4 = (e.courseId = t.courseId)$.

**Step 3 — turn selection-over-product into joins.**

$$ \equiv \Pi_{p.empId,\,p.name,\,p.phone}\big(p \bowtie_{\theta_3} (\sigma_{\theta_2}(t) \bowtie_{\theta_4} \sigma_{\theta_1}(e))\big) $$

**Step 4 — push projections down** (keep only the fields needed above each node).

$$ \equiv \Big(\Pi_{empId,name,phone}(p) \bowtie_{\theta_3} \Pi_{empId}\big(\Pi_{courseId,\,empId}\,\sigma_{\theta_2}(t) \bowtie_{\theta_4} \Pi_{courseId}\,\sigma_{\theta_1}(e)\big)\Big) $$

with $\theta_3 = (p.empId = empId)$ and $\theta_4 = (t.courseId = e.courseId)$ in the deck's final slide.

**Step 5 — cost-based choice.** Evaluate the costs of using different methods for the **two selections and the two joins**, and **choose the least-cost plan**.

| Step | What was done | Heuristic used |
| --- | --- | --- |
| 0 → 1 | single-relation conditions $\theta_1,\theta_2$ moved onto $e$ and $t$ | apply select early |
| 1 → 2 | join conditions $\theta_3,\theta_4$ separated | algebraic laws |
| 2 → 3 | $\sigma\ \text{over}\ \times$ replaced by $\bowtie$ | join instead of product |
| 3 → 4 | projections on $p$, $t$, $e$ and on the join result | apply project early |
| 4 → 5 | pick method per selection/join using §2.2–§2.17 costs | cost-based |

> [!tip] Exam pointer — query optimization
> Name the two stages (algebraic = heuristic, then cost-based); state the main heuristic (select and project first) and the commutative/associative laws; reproduce the five-line rewrite of the professor–teaching–enrollment query, and say that the last step compares methods for the two selections and two joins.

---

## 3. Transactions

*Deck: [[transactions.pdf|transactions deck]] — 36 slides, Silberschatz, Korth and Sudarshan (*Database System Concepts*, 6th ed., Chapter 14). All definitions, properties, examples and schedule facts below come from the deck.*

> [!abstract] Roadmap of this topic — read it as one story
> **The question:** when many programs read and update the same database, and when hardware or software can fail in the middle, how does the DBMS keep the data correct?
> **The answer is a contract and a theory of interleaving**, built in layers:
> 1. **§3.1–§3.2 — the transaction and ACID:** a transaction is the unit of work the DBMS promises to treat as indivisible, consistent, isolated and durable; the fund-transfer example shows exactly what breaks when each property is missing.
> 2. **§3.3 — the life cycle:** a transaction moves through Active, Partially committed, Committed, Failed and Aborted; commit, abort, restart and kill are the control actions.
> 3. **§3.4–§3.5 — concurrency and schedules:** running transactions together improves throughput and response time, but a schedule (an interleaving of their instructions) must preserve the order inside each transaction and must not destroy correctness.
> 4. **§3.6–§3.9 — serializability:** a concurrent schedule is acceptable if it is equivalent to some serial one; conflict serializability tests this by swapping non-conflicting instructions and, algorithmically, by checking the precedence graph for cycles.
> 5. **§3.10–§3.11 — recoverability:** correctness after failures requires that a transaction not commit after reading uncommitted data (recoverable), and preferably not read uncommitted data at all (cascadeless).
> 6. **§3.12–§3.14 — control and SQL:** the DBMS needs concurrency-control protocols; applications can trade strictness for performance through SQL isolation levels and explicit transaction boundaries.
> 7. **§3.15–§3.16 — beyond conflict serializability:** view serializability is weaker but hard to test; some schedules are correct only when the meaning of operations beyond reads and writes is considered.
>
> **The idea to carry through:** concurrency is valuable, but every relaxation of serial execution must be justified by an equivalence that preserves consistency and by a recovery rule that can undo the right work after a failure.

### 3.1 Transaction concept and the fund-transfer example

A **transaction** is a unit of program execution that accesses and possibly updates various data items.

> [!example] Example (deck) — transfer $50$ from account $A$ to account $B$
> Transaction $T_1$:
> 1. $\texttt{read}(A)$
> 2. $A := A - 50$
> 3. $\texttt{write}(A)$
> 4. $\texttt{read}(B)$
> 5. $B := B + 50$
> 6. $\texttt{write}(B)$

Two main issues must be dealt with:

- **Failures** of various kinds, such as hardware failures and system crashes.
- **Concurrent execution** of multiple transactions.

> [!note] Why a transaction is the right unit
> The database is consistent before $T_1$ starts and must be consistent after $T_1$ finishes, but in the middle (after debiting $A$ and before crediting $B$) the database is temporarily wrong. The DBMS must therefore treat steps 1–6 as one indivisible unit: either all of them take effect, or none do.

### 3.2 The ACID properties

To preserve the integrity of data, the database system must ensure four properties for every transaction.

#### Atomicity

> [!important] **Atomicity** — either all operations of the transaction are properly reflected in the database, or none are.

For the transfer transaction:

- If the transaction fails after step 3 and before step 6, money will be "lost", leading to an inconsistent database state.
- Failure could be due to software or hardware.
- The system should ensure that updates of a partially executed transaction are not reflected in the database.

#### Consistency

> [!important] **Consistency** — execution of a transaction in isolation preserves the consistency of the database.

Consistency requirements for the transfer example:

- The sum $A + B$ is unchanged by the execution of the transaction.

In general, consistency requirements include:

- **Explicitly specified integrity constraints**, such as primary keys and foreign keys.
- **Implicit integrity constraints** — e.g. the sum of balances of all accounts minus the sum of loan amounts must equal the value of cash-in-hand.

A transaction, when starting to execute, must see a consistent database. During transaction execution the database may be temporarily inconsistent. When the transaction completes successfully the database must be consistent.

> [!warning] Erroneous logic
> Erroneous transaction logic can lead to inconsistency. The DBMS can enforce declared constraints, but it cannot make a badly written transaction logically correct.

#### Isolation

> [!important] **Isolation** — although multiple transactions may execute concurrently, each transaction must be unaware of other concurrently executing transactions. Intermediate transaction results must be hidden from other concurrently executed transactions.

That is, for every pair of transactions $T_i$ and $T_j$, it appears to $T_i$ that either $T_j$ finished execution before $T_i$ started, or $T_j$ started execution after $T_i$ finished.

If, between steps 3 and 6 of the fund-transfer transaction $T_1$, another transaction $T_2$ is allowed to access the partially updated database, it will see an inconsistent database (the sum $A + B$ will be less than it should be):

| $T_1$ | $T_2$ |
| --- | --- |
| 1. $\texttt{read}(A)$ | |
| 2. $A := A - 50$ | |
| 3. $\texttt{write}(A)$ | |
| | $\texttt{read}(A),\ \texttt{read}(B),\ \texttt{print}(A+B)$ |
| 4. $\texttt{read}(B)$ | |
| 5. $B := B + 50$ | |
| 6. $\texttt{write}(B)$ | |

Isolation can be ensured trivially by running transactions **serially** — that is, one after the other. However, executing multiple transactions concurrently has significant benefits, as discussed in §3.4.

#### Durability

> [!important] **Durability** — after a transaction completes successfully, the changes it has made to the database persist, even if there are system failures.

Once the user has been notified that the transaction has completed (i.e. the transfer of the $50$ has taken place), the updates to the database by the transaction must persist even if there are software or hardware failures.

> [!note] ACID as one contract
> Atomicity and durability protect against **failures** (nothing half-done survives, and everything committed survives). Isolation protects against **concurrency** (concurrent transactions do not see each other's half-done work). Consistency is the correctness condition the whole contract is meant to preserve.

> [!tip] Exam pointer — ACID
> Be able to state each property precisely, attach it to the fund-transfer example (lost money → atomicity, wrong sum seen by another transaction → isolation, $A+B$ preserved → consistency, completed transfer surviving a crash → durability), and explain why serial execution gives isolation trivially but at a performance cost.

### 3.3 Transaction states

A transaction moves through a fixed set of states during its lifetime.

> [!important] Transaction states
> - **Active** — the initial state; the transaction stays in this state while it is executing.
> - **Partially committed** — after the final statement has been executed.
> - **Failed** — after the discovery that normal execution can no longer proceed.
> - **Aborted** — after the transaction has been rolled back and the database restored to its state prior to the start of the transaction.
> - **Committed** — after successful completion.

After a transaction has been aborted, there are two options:

- **Restart the transaction** — can be done only if there is no internal logical error.
- **Kill the transaction**.

#### State transitions (as shown on the deck's state diagram)

| From | To | Event / condition |
| --- | --- | --- |
| — | Active | Transaction begins |
| Active | Partially committed | Final statement has been executed |
| Partially committed | Committed | Successful completion |
| Active | Failed | Normal execution can no longer proceed |
| Partially committed | Failed | Failure discovered after final statement but before commit completes |
| Failed | Aborted | Transaction rolled back; database restored to pre-transaction state |
| Aborted | Active | Restart (only if no internal logical error) |
| Aborted | — | Kill the transaction |

> [!note] Why Partially committed is distinct from Committed
> After the last statement executes, the transaction's intended updates are known but may not yet be safely durable on stable storage. A failure in this window can still force the transaction to Failed and then Aborted. Only the Committed state carries the durability guarantee.

### 3.4 Concurrent executions

Multiple transactions are allowed to run concurrently in the system.

**Advantages:**

- **Increased processor and disk utilization, leading to better transaction throughput** — e.g. one transaction can be using the CPU while another is reading from or writing to the disk.
- **Reduced average response time for transactions** — short transactions need not wait behind long ones.

**Concurrency control schemes** are mechanisms to achieve isolation — that is, to control the interaction among the concurrent transactions in order to prevent them from destroying the consistency of the database. (The deck notes these are studied in Chapter 15, after the notion of correctness of concurrent executions.)

### 3.5 Schedules and the serial/concurrent examples

> [!important] **Schedule** — a sequence of instructions that specifies the chronological order in which instructions of concurrent transactions are executed.

- A schedule for a set of transactions must consist of **all instructions** of those transactions.
- It must **preserve the order** in which the instructions appear in each individual transaction.
- A transaction that successfully completes its execution will have a **commit** instruction as the last statement (by default a transaction is assumed to execute a commit instruction as its last step).
- A transaction that fails to successfully complete its execution will have an **abort** instruction as the last statement.

#### Running example for schedules: $T_1$ and $T_2$

The deck uses the following pair throughout Schedules 1–4:

- $T_1$: transfer $50$ from $A$ to $B$.
  1. $\texttt{read}(A)$
  2. $A := A - 50$
  3. $\texttt{write}(A)$
  4. $\texttt{read}(B)$
  5. $B := B + 50$
  6. $\texttt{write}(B)$
- $T_2$: transfer $10\%$ of the balance from $A$ to $B$ (as stated by the deck).

#### Schedule 1 — serial, $T_1$ followed by $T_2$

An example of a serial schedule in which $T_1$ is followed by $T_2$. The deck presents this schedule as a slide diagram.

#### Schedule 2 — serial, $T_2$ followed by $T_1$

A serial schedule in which $T_2$ is followed by $T_1$. The deck presents this schedule as a slide diagram.

#### Schedule 3 — concurrent, equivalent to a serial schedule

Let $T_1$ and $T_2$ be the transactions defined previously. The following schedule is not a serial schedule, but it is equivalent to Schedule 1 (as stated on the deck slide introducing Schedule 3). The deck presents the schedule as a slide diagram.

> [!note] Preservation of $A+B$
> In Schedules 1, 2 and 3, the sum $A + B$ is preserved (deck).

#### Schedule 4 — concurrent, incorrect

The following concurrent schedule does not preserve the sum of $A + B$. The deck presents the schedule as a slide diagram.

> [!warning] Serial is safe; concurrent is not automatically safe
> Schedules 1 and 2 are serial, so each sees a consistent database and leaves one behind. Schedule 3 interleaves instructions but still preserves $A+B$; Schedule 4 interleaves in a way that destroys $A+B$. The purpose of serializability theory (§3.6 onward) is to tell Schedule 3 from Schedule 4 without relying on intuition about one example.

### 3.6 Serializability

> [!important] Basic assumption and definition
> **Basic assumption** — each transaction preserves database consistency. Thus, serial execution of a set of transactions preserves database consistency.
>
> A (possibly concurrent) schedule is **serializable** if it is equivalent to a serial schedule.

Different forms of schedule equivalence give rise to different notions:

1. **Conflict serializability**
2. **View serializability**

#### Simplified view of transactions

- We ignore operations other than **read** and **write** instructions.
- We assume that transactions may perform arbitrary computations on data in local buffers in between reads and writes.
- Our simplified schedules consist of only read and write instructions.

### 3.7 Conflicting instructions and conflict equivalence

> [!important] **Conflicting instructions**
> Let $l_i$ and $l_j$ be two instructions of transactions $T_i$ and $T_j$ respectively. Instructions $l_i$ and $l_j$ **conflict** if and only if there exists some item $Q$ accessed by both $l_i$ and $l_j$, and at least one of these instructions wrote $Q$.

| $l_i$ | $l_j$ | Conflict? |
| --- | --- | --- |
| $\texttt{read}(Q)$ | $\texttt{read}(Q)$ | No — $l_i$ and $l_j$ don't conflict |
| $\texttt{read}(Q)$ | $\texttt{write}(Q)$ | Yes — they conflict |
| $\texttt{write}(Q)$ | $\texttt{read}(Q)$ | Yes — they conflict |
| $\texttt{write}(Q)$ | $\texttt{write}(Q)$ | Yes — they conflict |

Intuitively, a conflict between $l_i$ and $l_j$ forces a (logical) temporal order between them. If $l_i$ and $l_j$ are consecutive in a schedule and they do **not** conflict, their results would remain the same even if they had been interchanged in the schedule.

> [!important] **Conflict equivalence and conflict serializability**
> If a schedule $S$ can be transformed into a schedule $S'$ by a series of swaps of non-conflicting instructions, we say that $S$ and $S'$ are **conflict equivalent**.
>
> We say that a schedule $S$ is **conflict serializable** if it is conflict equivalent to a serial schedule.

### 3.8 Conflict serializability — examples

#### Schedule 3 is conflict serializable

Schedule 3 can be transformed into Schedule 6 — a serial schedule where $T_2$ follows $T_1$ — by a series of swaps of non-conflicting instructions. Therefore, Schedule 3 is conflict serializable. (The deck shows Schedule 3 and Schedule 6 side by side as slide diagrams.)

#### A schedule that is not conflict serializable

The deck gives an example involving transactions $T_3$ and $T_4$ (shown as a slide diagram) and states: we are unable to swap instructions in that schedule to obtain either the serial schedule $\langle T_3, T_4 \rangle$ or the serial schedule $\langle T_4, T_3 \rangle$.

> [!note] Why non-conflicting swaps matter
> Swapping non-conflicting instructions does not change the value any transaction reads or writes, so it does not change the final database state. If a concurrent schedule can be "straightened" into a serial order by such swaps, it is behaviourally indistinguishable (with respect to reads/writes) from that serial order.

### 3.9 Testing for conflict serializability — the precedence graph

> [!important] **Precedence graph**
> Consider some schedule of a set of transactions $T_1, T_2, \ldots, T_n$.
> - **Precedence graph** — a directed graph where the vertices are the transactions (names).
> - Draw an arc from $T_i$ to $T_j$ if the two transactions conflict, and $T_i$ accessed the data item on which the conflict arose earlier.
> - We may label the arc by the item that was accessed.

> [!important] **Serializability test**
> A schedule is conflict serializable **if and only if** its precedence graph is **acyclic**.

- **Cycle-detection algorithms** exist which take order $n^2$ time, where $n$ is the number of vertices in the graph.
  - (Better algorithms take order $n + e$ where $e$ is the number of edges.)
- If the precedence graph is acyclic, the serializability order can be obtained by a **topological sorting** of the graph.
  - That is, a linear order consistent with the partial order of the graph.
  - For example, a serializability order for the schedule (a) would be one of either (b) or (c) (as shown on the deck's diagram).

> [!tip] Exam pointer — precedence graph
> To test a schedule: find every pair of conflicting operations on the same item by different transactions, draw an edge from the earlier accessor to the later one (labelled by the item), then check for cycles. No cycle ⇒ conflict serializable, and any topological order is a valid equivalent serial schedule. A cycle ⇒ not conflict serializable.

### 3.10 Recoverable schedules

> [!important] **Recoverable schedule** — if a transaction $T_j$ reads a data item previously written by a transaction $T_i$, then the commit operation of $T_i$ must appear before the commit operation of $T_j$.

The deck gives the following example: the schedule shown is not recoverable if $T_9$ commits immediately after the $\texttt{read}(A)$ operation (schedule diagram on the deck). If $T_8$ should abort, $T_9$ would have read (and possibly shown to the user) an inconsistent database state. Hence, the database must ensure that schedules are recoverable.

> [!warning] Why "commit after read-from" is dangerous
> If $T_9$ commits after reading a value written by uncommitted $T_8$, then $T_8$'s later abort cannot be undone from $T_9$'s point of view — a committed transaction cannot be rolled back. The only safe order is: $T_8$ commits (or aborts) first, and $T_9$ commits only after that.

### 3.11 Cascading rollbacks and cascadeless schedules

#### Cascading rollbacks

> [!important] **Cascading rollback** — a single transaction failure leads to a series of transaction rollbacks.

The deck gives the following example: consider the schedule shown where none of the transactions has yet committed (so the schedule is recoverable). If $T_{10}$ fails, $T_{11}$ and $T_{12}$ must also be rolled back. Cascading rollback can lead to the undoing of a significant amount of work.

#### Cascadeless schedules

> [!important] **Cascadeless schedules** — for each pair of transactions $T_i$ and $T_j$ such that $T_j$ reads a data item previously written by $T_i$, the commit operation of $T_i$ appears before the read operation of $T_j$.

- Every cascadeless schedule is also recoverable.
- It is desirable to restrict the schedules to those that are cascadeless.

The deck includes an example of a schedule that is **not** cascadeless (shown as a slide diagram).

> [!note] Recoverable vs cascadeless
> **Recoverable** allows $T_j$ to read $T_i$'s uncommitted write, but delays $T_j$'s commit until $T_i$ commits/aborts. **Cascadeless** is stricter: $T_j$ cannot even *read* $T_i$'s uncommitted write until $T_i$ has committed, so an abort of $T_i$ can never force $T_j$ to roll back. Every cascadeless schedule is recoverable, but not every recoverable schedule is cascadeless.

### 3.12 Concurrency control

A database must provide a mechanism that will ensure that all possible schedules are both:

- **Conflict serializable.**
- **Recoverable and preferably cascadeless.**

Additional points from the deck:

- A policy in which only one transaction can execute at a time generates serial schedules, but provides a poor degree of concurrency.
- **Concurrency-control schemes** trade off between the amount of concurrency they allow and the amount of overhead that they incur.
- Testing a schedule for serializability after it has executed is a little too late!
  - Tests for serializability help us understand why a concurrency control protocol is correct.
- **Goal** — to develop concurrency control protocols that will assure serializability.

### 3.13 Weak levels of consistency and SQL isolation levels

#### Weak levels of consistency

Some applications are willing to live with weak levels of consistency, allowing schedules that are not serializable:

- E.g. a read-only transaction that wants to get an approximate total balance of all accounts.
- E.g. database statistics computed for query optimization can be approximate (why? — they are used for cost estimation, not for user-visible correctness).
- Such transactions need not be serializable with respect to other transactions.

This is a **tradeoff of accuracy for performance**.

#### Levels of consistency in SQL-92

| Level | Guarantee (deck) |
| --- | --- |
| **Serializable** | Default |
| **Repeatable read** | Only committed records to be read; repeated reads of the same record must return the same value. However, a transaction may not be serializable — it may find some records inserted by a transaction but not find others. |
| **Read committed** | Only committed records can be read, but successive reads of a record may return different (but committed) values. |
| **Read uncommitted** | Even uncommitted records may be read. |

- Lower degrees of consistency are useful for gathering approximate information about the database.
- **Warning:** some database systems do not ensure serializable schedules by default.
  - E.g. Oracle and PostgreSQL by default support a level of consistency called **snapshot isolation** (not part of the SQL standard).

> [!warning] "Serializable" in SQL vs in the system
> The SQL-92 level named *Serializable* is the strongest in that standard, but the deck warns that some systems default to weaker behaviour (e.g. snapshot isolation). Do not assume a system's default matches the SQL-92 serializable guarantee without checking.

### 3.14 Transaction definition in SQL

- Data manipulation language must include a construct for specifying the set of actions that comprise a transaction.
- In SQL, a transaction begins implicitly.
- A transaction in SQL ends by:
  - **`Commit work`** — commits current transaction and begins a new one.
  - **`Rollback work`** — causes current transaction to abort.
- In almost all database systems, by default, every SQL statement also commits implicitly if it executes successfully.
  - Implicit commit can be turned off by a database directive.
  - E.g. in JDBC, `connection.setAutoCommit(false);`

### 3.15 View serializability

> [!important] **View equivalence**
> Let $S$ and $S'$ be two schedules with the same set of transactions. $S$ and $S'$ are **view equivalent** if the following three conditions are met, for each data item $Q$:
> 1. If in schedule $S$, transaction $T_i$ reads the initial value of $Q$, then in schedule $S'$ also transaction $T_i$ must read the initial value of $Q$.
> 2. If in schedule $S$ transaction $T_i$ executes $\texttt{read}(Q)$, and that value was produced by transaction $T_j$ (if any), then in schedule $S'$ also transaction $T_i$ must read the value of $Q$ that was produced by the same $\texttt{write}(Q)$ operation of transaction $T_j$.
> 3. The transaction (if any) that performs the final $\texttt{write}(Q)$ operation in schedule $S$ must also perform the final $\texttt{write}(Q)$ operation in schedule $S'$.

As can be seen, view equivalence is also based purely on reads and writes alone.

> [!important] **View serializability**
> A schedule $S$ is **view serializable** if it is view equivalent to a serial schedule.

Key facts:

- Every conflict serializable schedule is also view serializable.
- The deck shows a schedule which is view-serializable but not conflict serializable (slide diagram) and asks: what serial schedule is it equivalent to?
- Every view serializable schedule that is not conflict serializable has **blind writes**.

#### Testing for view serializability

- The precedence graph test for conflict serializability cannot be used directly to test for view serializability.
  - Extension to test for view serializability has cost **exponential** in the size of the precedence graph.
- The problem of checking if a schedule is view serializable falls in the class of **NP-complete** problems.
  - Thus, existence of an efficient algorithm is extremely unlikely.
- However, practical algorithms that just check some sufficient conditions for view serializability can still be used.

> [!note] Conflict vs view serializability
> Conflict serializability is a sufficient, efficiently testable condition (acyclic precedence graph). View serializability is a more general notion (allows some schedules conflict serializability rejects, typically due to blind writes), but testing it is NP-complete. In practice, concurrency-control protocols target conflict serializability.

### 3.16 More complex notions of serializability

The deck gives a schedule (slide diagram) that produces the same outcome as the serial schedule $\langle T_1, T_5 \rangle$, yet is not conflict equivalent or view equivalent to it.

- If we start with $A = 1000$ and $B = 2000$, the final result is $960$ and $2040$.
- Determining such equivalence requires analysis of operations other than read and write.

> [!note] Beyond reads and writes
> Conflict and view serializability treat transactions as sequences of reads and writes on data items. When the *meaning* of operations matters (e.g. two increments commute even though they both read and write the same item), schedules can be correct in a stronger semantic sense without being conflict- or view-equivalent to a serial schedule. The deck uses this example to show the limits of the read/write model.

> [!tip] Exam pointer — transactions
> Know ACID with the fund-transfer example; draw/trace the state diagram and name the restart/kill options from Aborted; distinguish serial, conflict-serializable and non-serializable schedules; apply the conflict rules and the precedence-graph acyclicity test; distinguish recoverable, cascadeless and cascading rollback with the commit/read ordering; and recall the SQL-92 isolation levels in order with what each allows, plus the warning that some systems default to snapshot isolation.

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
| Selectivity | $s = \dfrac{\text{records satisfying } C}{\text{total records}}$ | $0\le s\le1$; low $s$ = highly selective |
| Selectivity estimate | key: $1/\text{(total records)}$; non-key: $1/\text{(distinct values)}$ | uniform-distribution estimate kept in the catalog |
| External sort — runs | $r=\lceil n/m\rceil$ | $n$ file blocks, $m$ buffer blocks |
| External sort — cost | $2n + 2n\lceil\log_d r\rceil$ | $2\le d\le m-1$; sort phase $2n$, each merge sub-phase $2n$ |
| Nested loop join | $b_1 + \lceil b_1/(m-2)\rceil\, b_2$ | $R$ outer; put the file with fewer blocks outside |
| Single loop join | $b_1\cdot h_B(S)$ | index on $B$ of $S$; loop over the file with high join selection factor |
| Partition hash join | $3(\lvert R\rvert+\lvert S\rvert)+\lvert result\rvert$ | one of $R_i,S_i$ fits in memory; else $2(\lvert R\rvert+\lvert S\rvert)$ + nested loop cost |

> [!note] Source material and figures
> **Topic 1.** All `DBMS - …excalidraw` drawings are original schematic reconstructions of the deck's diagrams and live in the vault-root `Excalidraw/` folder. The explanatory drawings *Index Types Compared*, *Extendible Hashing Trace*, *Linear Hashing Trace* and *Bplus Replicate vs Move* are teaching aids built from the deck's own numbers. Callouts titled "Illustrative example (not from the deck)" and the "Intuition" subsections in §1 are explanatory additions and are not lecture content. The `DBMS - … (deck pN).png` figures are page renders of [[file-management.pdf]], stored in `DBMS/images/`, and each is captioned with the slide it came from.
> **Topic 2.** Content is compiled from [[algos.pdf]] (32 slides). The merge-phase figure *DBMS - External Sort Merge Phase (deck p10).png* is a page render of the deck stored in `DBMS/images/`. The "Illustrative example (not from the deck)" callouts in §2.4 and §2.8 are explanatory additions; all other numbers (8000-record selectivities, 5600/120/52-block join, the query-rewrite chain) come from the deck.
> **Topic 3.** Content is compiled from [[transactions.pdf]] (Silberschatz, Korth and Sudarshan, *Database System Concepts*, 6th ed., Chapter 14). Where the deck presents schedules, state diagrams or graphs as slide diagrams, the notes record every fact, definition, property and result stated on the slides; diagram-only step layouts that were not recoverable from text extraction are described by the deck's stated outcomes and constraints rather than invented.
> **General.** All numbers, conventions and worked traces come from the respective decks; the Silberschatz textbook ([[silberschatz_dbms.pdf]], Ch. 13–14 and §24.5) was used for explanation only in topic 1.
