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
> All `DBMS - …excalidraw` drawings are original schematic reconstructions of the deck's diagrams and live in the vault-root `Excalidraw/` folder. The explanatory drawings *Index Types Compared*, *Extendible Hashing Trace*, *Linear Hashing Trace* and *Bplus Replicate vs Move* are teaching aids built from the deck's own numbers. Callouts titled "Illustrative example (not from the deck)" and the "Intuition" subsections are explanatory additions and are not lecture content. The `DBMS - … (deck pN).png` figures are page renders of [[file-management.pdf]], stored in `DBMS/images/`, and each is captioned with the slide it came from. All numbers, conventions and worked traces come from the deck; the Silberschatz textbook ([[silberschatz_dbms.pdf]], Ch. 13–14 and §24.5) was used for explanation only.
