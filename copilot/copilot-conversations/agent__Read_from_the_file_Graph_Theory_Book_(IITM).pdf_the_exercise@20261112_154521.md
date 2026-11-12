---
epoch: 1794478521289
mode: agent
backendId: opencode
sessionId: ses_e30c0ce64ffeWd7H15Nnox7gJ3
tags:
  - copilot-conversation
agentLabel: Graph Theory Module 11 exercises and solutions
usage: '{"usedTokens":97084,"contextWindow":200000,"updatedAt":1794500502390}'
lastAccessedAt: 1794506620228
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

**user**: im pasting a solution for question 18 in chapter 11.
check if it is the current one, if it is then do nothing if its a different solution(different method) then replace the current solution with this one.
solution:
**Proof:**

If $r = 0$, then every vertex in $D$ already has out-degree $0$ and in-degree $0$, so $H = D$ is already $0$-regular. Assume now that $r \ge 1$.

For each vertex $v \in V(D)$, define its **out-deficiency** $a_v$ and **in-deficiency** $b_v$ by


$$a_v = r - \text{outdeg}_D(v) \qquad \text{and} \qquad b_v = r - \text{indeg}_D(v).$$


By definition of $r$, we have $0 \le a_v \le r$ and $0 \le b_v \le r$ for every $v \in V(D)$. Moreover, since the sum of all out-degrees in $D$ equals the sum of all in-degrees (both equal $\vert{}A(D)\vert{}$), the total out-deficiency equals the total in-deficiency:


$$M = \sum_{v \in V(D)} a_v = r\vert{}V(D)\vert{} - \vert{}A(D)\vert{} = \sum_{v \in V(D)} b_v.$$

### 1. Creating Stubs and a Bijection

* For each vertex $v \in V(D)$, create $a_v$ labeled **out-stubs** $(v, 1), (v, 2), \dots, (v, a_v)$. Since $a_v \le r$, each out-stub of $v$ has a distinct label $s \in \{1, 2, \dots, r\}$.
* Similarly, for each vertex $w \in V(D)$, create $b_w$ labeled **in-stubs** $[w, 1], [w, 2], \dots, [w, b_w]$.

Because there are $M$ out-stubs in total and $M$ in-stubs in total, we can choose an arbitrary bijection $\phi$ pairing each out-stub $(v, s)$ with a unique in-stub $[w, t]$.

### 2. Constructing the Superdigraph $H$

Take $r + 1$ disjoint copies of $D$, denoted $D_0, D_1, \dots, D_r$, where the copy of a vertex $v \in V(D)$ in $D_i$ is written $v^{(i)}$.

Start with the disjoint union $D_0 \sqcup D_1 \sqcup \dots \sqcup D_r$ (so $D \cong D_0$ is clearly a subdigraph of $H$), and add new arcs as follows: for every out-stub $(v, s)$ paired with $\phi(v, s) = [w, t]$, and for every index $i \in \{0, 1, \dots, r\}$, add the directed arc


$$v^{(i)} \longrightarrow w^{(i + s \bmod (r+1))}.$$

### 3. Verifying the Properties of $H$

1. **$H$ is a simple digraph (no loops or parallel arcs):**
* Because $s \in \{1, 2, \dots, r\}$, we have $i + s \not\equiv i \pmod{r+1}$. Thus every newly added arc connects two *different* copies $D_i$ and $D_j$ ($i \neq j$), meaning no loops are created and no new arc duplicates an existing arc inside any $D_i$.
* For a fixed vertex $v^{(i)}$, its outgoing added arcs correspond to its out-stubs $(v, 1), \dots, (v, a_v)$, which have **distinct** offsets $s$. Consequently, these arcs land in **distinct** copies $D_{(i+s)\bmod(r+1)}$, so $v^{(i)}$ has at most one arc to any given vertex $w^{(j)}$.


2. **$H$ is $r$-regular:**
* **Out-degree:** Each vertex $v^{(i)}$ inherits $\text{outdeg}_D(v)$ arcs inside $D_i$, plus $1$ new outgoing arc for each of its $a_v$ out-stubs. Thus,

$$\text{outdeg}_H(v^{(i)}) = \text{outdeg}_D(v) + a_v = \text{outdeg}_D(v) + \big(r - \text{outdeg}_D(v)\big) = r.$$


* **In-degree:** Each vertex $w^{(j)}$ inherits $\text{indeg}_D(w)$ arcs inside $D_j$. For each of its $b_w$ in-stubs $[w, t]$, let $(v, s) = \phi^{-1}([w, t])$ be its unique matched out-stub; taking the unique $i \equiv j - s \pmod{r+1}$ gives the unique new arc $v^{(i)} \to w^{(j)}$ corresponding to $[w, t]$. Thus,

$$\text{indeg}_H(w^{(j)}) = \text{indeg}_D(w) + b_w = \text{indeg}_D(w) + \big(r - \text{indeg}_D(w)\big) = r.$$





Hence, $H$ is an $r$-regular simple digraph containing $D$ as a subdigraph. $\blacksquare$
[Timestamp: 2026/11/12 21:50:51]

**ai**: Current Q18 uses the König line-colouring + Hall/permutation-layer method. The pasted one is a genuinely different construction ($r+1$ copies with modular offsets), so I'll replace it.**Different solution — replaced.** Current Q18 used König's line-colouring theorem to split $A(D)$ into $r$ partial injections, then completed each to a permutation of $V\cup P$ via Hall's theorem ($|P|=4r+2$). Your version is the modular-copy construction: $r+1$ disjoint copies $D_0,\dots,D_r$ plus stub-matching arcs $v^{(i)}\to w^{(i+s\bmod (r+1))}$. Genuinely different method, so the old proof is gone.

I checked your construction before pasting it:

- deficiencies $a_v,b_v\in[0,r]$ and $\sum a_v=\sum b_v=r|V|-|A(D)|$ ✓ (so a bijection $\phi$ exists)
- no loops: $1\le s\le r\Rightarrow i+s\not\equiv i\pmod{r+1}$ ✓
- no parallel arcs from a fixed tail: distinct labels $s$ give distinct target copies ✓
- out-degree $=\mathrm{outdeg}_D(v)+a_v=r$ ✓
- in-degree $=\mathrm{indeg}_D(w)+b_w=r$ ✓ — I made the *distinct-tails* step explicit, since it is the one place a double arc could sneak in: two in-stubs matched to out-stubs $(v,s),(v,s')$ of the same $v$ must have $s\neq s'$, so $v^{(j-s)}\neq v^{(j-s')}$.

Kept from the old block: the boxed conclusion and the "why $r$ cannot be lowered" remark, plus a note that the construction lives on $(r+1)n$ vertices and that extra vertices are genuinely needed (the $K_3$-digraph + isolated vertex example, $r=2$).

Changed file: `Graph Theory/Question Practice.md` (Q18 solution body only; +25/−21 lines).
[Timestamp: 2026/11/12 21:50:51]