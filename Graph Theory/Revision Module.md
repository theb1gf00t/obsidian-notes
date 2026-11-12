# Graph Theory — Revision Module

## Chapter 7: Matchings, Covers, and Independent Sets

---

### Definitions

> [!note] Independent Set
> A subset $I \subseteq V(G)$ is an **independent set** if no two vertices in $I$ are adjacent. The **independence number** $\alpha_0(G)$ is the maximum size of an independent set in $G$.

> [!note] Vertex Cover
> A subset $K \subseteq V(G)$ is a **vertex cover** if every edge of $G$ has at least one endpoint in $K$. The **vertex-covering number** $\beta_0(G)$ is the minimum size of a vertex cover.

> [!note] Matching
> A **matching** $M$ in $G$ is a set of pairwise non-adjacent edges (no two edges share a vertex). The **matching number** $\alpha_1(G)$ is the maximum size of a matching.

> [!note] Perfect Matching
> A matching $M$ is a **perfect matching** if every vertex of $G$ is incident to exactly one edge of $M$.

> [!note] Edge Cover
> A subset $F \subseteq E(G)$ is an **edge cover** if every vertex $v \in V(G)$ is incident with at least one edge in $F$. The **minimum edge covering number** $\beta_1(G)$ is the minimum size of an edge cover. (Requires $\delta(G) \ge 1$.)

> [!note] Clique Number
> $\omega(G) = \max\{|V(H)| : H \text{ is a complete subgraph of } G\}$ is the **clique number** of $G$.

> [!note] Saturated / Unsaturated Vertex
> A vertex $v$ is **$M$-saturated** if it is an endpoint of some edge in matching $M$; otherwise it is **$M$-unsaturated**.

> [!note] Alternating and Augmenting Paths
> Given a matching $M$, a path is **$M$-alternating** if its edges alternate between $M$ and $E(G)\setminus M$. An alternating path is **$M$-augmenting** if both endpoints are $M$-unsaturated.

> [!note] System of Distinct Representatives (SDR)
> Given a family of sets $\mathcal{F} = (A_1, A_2, \ldots, A_n)$, a **system of distinct representatives** is a set of distinct elements $\{a_1, a_2, \ldots, a_n\}$ with $a_i \in A_i$ for each $i$.

---

### Theorems

> [!abstract] Theorem 7.1 — Gallai's Theorem (Vertex Parameters)
> For any graph $G$ without isolated vertices:
> $$\alpha_0(G) + \beta_0(G) = n(G)$$
> A set $K \subseteq V(G)$ is a vertex cover if and only if $V(G) \setminus K$ is an independent set.

> [!abstract] Theorem 7.2 — Gallai's Theorem (Edge Parameters)
> For any graph $G$ with $\delta(G) \ge 1$:
> $$\alpha_1(G) + \beta_1(G) = n(G)$$

> [!abstract] Theorem 7.3 — Berge's Theorem
> A matching $M$ in $G$ is a maximum matching if and only if $G$ contains no $M$-augmenting path.

> [!abstract] Theorem 7.4 — König's Theorem
> In a bipartite graph $G$:
> $$\alpha_1(G) = \beta_0(G)$$
> That is, the maximum matching number equals the minimum vertex cover number.

> [!abstract] Theorem 7.5 — König's Edge Theorem
> In a bipartite graph $G$:
> $$\alpha_0(G) = \beta_1(G)$$
> That is, the maximum independence number equals the minimum edge cover number.

> [!abstract] Theorem 7.6 — Hall's Marriage Theorem
> A bipartite graph $G[X, Y]$ has a matching that saturates every vertex of $X$ if and only if for every $S \subseteq X$:
> $$|N(S)| \ge |S|$$
> (Hall's condition)

> [!abstract] Theorem 7.7 — Hall's Theorem for SDR
> A family of finite sets $\mathcal{F} = (A_1, A_2, \ldots, A_n)$ has an SDR if and only if for every $k$ and every choice of $k$ sets from $\mathcal{F}$, their union contains at least $k$ elements.

> [!abstract] Theorem 7.8 — Perfect Matching in Regular Bipartite Graphs
> Every $k$-regular bipartite graph ($k \ge 1$) has a perfect matching.

> [!abstract] Theorem 7.9 — Tutte's Theorem
> A graph $G$ has a perfect matching if and only if for every $S \subseteq V(G)$:
> $$o(G - S) \le |S|$$
> where $o(H)$ denotes the number of odd components of $H$.

---

### Corollaries

> [!tip] Corollary to Theorem 7.1 (Gallai Identity for Complement)
> For any graph $G$ on $n$ vertices:
> $$\beta_0(G) = n - \alpha_0(G), \qquad \alpha_0(G) = n - \beta_0(G)$$

> [!tip] Corollary — Clique-Independence Duality
> For any graph $G$:
> $$\omega(G) = \alpha_0(G^c)$$
> A clique in $G$ is an independent set in its complement $G^c$.

> [!tip] Corollary to König's Theorem
> In a bipartite graph $G$ on $n$ vertices with $\delta(G) \ge 1$:
> $$\alpha_0(G) = \beta_1(G) = n - \alpha_1(G) = n - \beta_0(G)$$

> [!tip] Corollary to Hall's Theorem — Deficiency Version
> If Hall's condition fails, the maximum matching saturating $X$ has size $|X| - \text{def}(G)$, where the **deficiency** is:
> $$\text{def}(G) = \max_{S \subseteq X}\{|S| - |N(S)|\}$$

> [!tip] Corollary — Perfect Matching from Hall's Condition
> A bipartite graph $G[X, Y]$ with $|X| = |Y|$ has a perfect matching if and only if Hall's condition holds for $X$ (equivalently, for $Y$).

---

### Important Results and Remarks

> [!important] Result — Lower Bound on Vertex Cover
> For any graph $G$:
> $$\beta_0(G) \ge \delta(G)$$
> *Proof sketch:* In a minimum vertex cover, at least one vertex $v$ lies outside. All $\deg(v)$ neighbours must be in the cover.

> [!important] Result — Vertex Cover and Clique
> For any graph $G$:
> $$\beta_0(G) \ge \omega(G) - 1$$

> [!important] Result — Independent Set in Join
> For graphs $G_1$ and $G_2$, every independent set in $G_1 + G_2$ lies entirely in $V(G_1)$ or entirely in $V(G_2)$. Hence:
> $$\alpha_0(G_1 + G_2) = \max\{\alpha_0(G_1), \alpha_0(G_2)\}$$

> [!important] Result — Matching Number in Join
> $$\alpha_1(G_1 + G_2) = \alpha_1(G_1) + \alpha_1(G_2) + \min\{r_1, r_2\}$$
> where $r_i$ is the number of $M_i$-unsaturated vertices in $G_i$ for a maximum matching $M_i$.

> [!important] Result — Equivalences via Gallai
> For any graph $G$ on $n$ vertices, the following are equivalent:
> - (a) $\beta_0(G) + \beta_0(G^c) \ge n$
> - (b) $\alpha_0(G) + \alpha_0(G^c) \le n$
> - (c) $\beta_0(G) + \beta_0(G^c) \ge \alpha_0(G) + \alpha_0(G^c)$
> - (d) $\beta_0(G) \ge \omega(G)$

> [!important] Result — Perfect Matching in $d$-Cube
> The hypercube $Q_d$ ($d \ge 1$) has a perfect matching. Its edges can be partitioned into $d$ perfect matchings.
> $$\alpha_1(Q_d) = 2^{d-1}, \qquad \beta_1(Q_d) = 2^{d-1}$$

> [!important] Result — Edge Cover and Matching Relation
> If $M$ is a maximum matching of $G$ with $\delta(G) \ge 1$, a minimum edge cover can be constructed by extending $M$ to cover all unsaturated vertices with one edge each.

> [!important] Remark — Augmenting Path Structure
> The symmetric difference $M \oplus M^*$ of two matchings decomposes into paths and even cycles that alternate between edges of $M$ and $M^*$. Augmenting paths in $M \oplus M^*$ certify that $M$ is not maximum when $|M| < |M^*|$.

> [!important] Remark — Alternating Components
> Given two disjoint matchings $M$ and $N$, every component of the subgraph $M \cup N$ is either:
> - an **alternating even cycle** (equal number of $M$- and $N$-edges), or
> - an **alternating path** (differs by at most one edge between $M$ and $N$).
> This structure is used to exchange edges between matchings and adjust their sizes.

> [!important] Remark — Bipartite Graphs are Class 1
> Every bipartite graph $G$ satisfies $\chi_1(G) = \Delta(G)$ (Class 1). This follows from König's theorem applied to edge coloring.

> [!important] Remark — Leaves in Trees
> For any tree $T$ with $n \ge 3$ vertices, the set of all leaves (degree-1 vertices) is an independent set and can be extended to a maximal independent set.

---

## Chapter 8: Vertex Colorings

---

### Definitions

> [!note] Proper Vertex Coloring
> A **proper vertex coloring** of $G$ is an assignment of colors to the vertices of $G$ such that no two adjacent vertices receive the same color.

> [!note] Chromatic Number
> The **chromatic number** $\chi(G)$ is the minimum number of colors required for a proper vertex coloring of $G$.

> [!note] $k$-Colorable
> $G$ is **$k$-colorable** if $\chi(G) \le k$.

> [!note] $k$-Chromatic
> $G$ is **$k$-chromatic** if $\chi(G) = k$.

> [!note] Color Class
> In a proper $k$-coloring, the vertices of each color form an independent set called a **color class**.

> [!note] $k$-Critical Graph
> A graph $G$ is **$k$-critical** if $\chi(G) = k$ and $\chi(H) < k$ for every proper subgraph $H \subsetneq G$.

> [!note] Clique Partition
> A **clique partition** of $G$ is a partition $(V_1, V_2, \ldots, V_p)$ of $V(G)$ such that each induced subgraph $G[V_i]$ is a clique. The **clique partition number** $\theta_0(G)$ is the minimum number of parts in any clique partition.

> [!note] $k$-Degenerate Graph
> A graph $G$ is **$k$-degenerate** if $\delta(H) \le k$ for every subgraph $H$ of $G$.

> [!note] Mycielski Graph
> The **Mycielskian** $G_k$ is a triangle-free graph with $\chi(G_k) = k$, constructed recursively: given $G_{k-1}$ on vertices $\{u_1, \ldots, u_m\}$, add shadow vertices $v_1, \ldots, v_m$ (where $v_i$ is joined to all neighbours of $u_i$) and an apex $z$ joined to all $v_i$.

---

### Theorems

> [!abstract] Theorem 8.1 — König's Bipartite Characterization
> A graph $G$ is $2$-colorable (bipartite) if and only if $G$ contains no odd cycle.

> [!abstract] Theorem 8.2 — Chromatic Number of a Join
> For any two graphs $G_1$ and $G_2$:
> $$\chi(G_1 + G_2) = \chi(G_1) + \chi(G_2)$$

> [!abstract] Theorem 8.3 — Bounds on $\chi(G)$
> For every graph $G$:
> $$\frac{n(G)}{\alpha_0(G)} \le \chi(G) \le n(G) + 1 - \alpha_0(G)$$

> [!abstract] Theorem 8.4 — Mycielski's Theorem
> For every $k \ge 2$, there exists a triangle-free graph with chromatic number $k$.
> The Mycielski graph $G_k$ is triangle-free and satisfies $\chi(G_k) = k$.

> [!abstract] Theorem 8.5 — Properties of $k$-Critical Graphs
> If $G$ is $k$-critical, then:
> 1. $G$ is connected.
> 2. $\delta(G) \ge k - 1$.

> [!abstract] Theorem 8.6 — Chromatic Number of $G - S$ in Critical Graphs
> If $S$ is an independent set in a $k$-critical graph $G$, then:
> $$\chi(G - S) = k - 1$$

> [!abstract] Theorem 8.7 — Critical Graphs and Joins
> For simple graphs $G_1$ and $G_2$:
> $$G_1 + G_2 \text{ is critical} \iff G_1 \text{ and } G_2 \text{ are both critical}$$

> [!abstract] Theorem 8.8 — Greedy Coloring of $k$-Degenerate Graphs
> If $G$ is $k$-degenerate, then there exists a vertex ordering (degeneracy ordering) such that the greedy algorithm uses at most $k + 1$ colors.
> $$\chi(G) \le k + 1$$

---

### Corollaries

> [!tip] Corollary — Chromatic Numbers of Basic Graphs
> - $\chi(K_n) = n$
> - $\chi(C_{2k}) = 2$ (even cycle)
> - $\chi(C_{2k+1}) = 3$ (odd cycle)
> - $\chi(T) = 2$ for any tree $T$ with $n \ge 2$ (trivially $1$ for $n = 1$)
> - $\chi(K_{n_1, n_2, \ldots, n_s}) = s$

> [!tip] Corollary — Chromatic Number of Complement of a Cycle
> $$\chi(C_n^c) = \begin{cases} 1 & n = 3 \\ \left\lceil \dfrac{n}{2} \right\rceil & n \ge 4 \end{cases}$$

> [!tip] Corollary — Minimum Edges in $k$-Chromatic Graphs
> Every graph $G$ with $\chi(G) = k$ satisfies:
> $$|E(G)| \ge \frac{k(k-1)}{2}$$

> [!tip] Corollary — Long Cycle in $k$-Chromatic Graphs
> Every graph $G$ with $\chi(G) = k \ge 3$ contains a cycle of length at least $k$.

> [!tip] Corollary — Clique Partition and Complement
> $$\theta_0(G) = \chi(G^c)$$

> [!tip] Corollary — Clique Partition of a Join
> $$\theta_0(G_1 + G_2) = \max\{\theta_0(G_1), \theta_0(G_2)\}$$

> [!tip] Corollary — Clique Partition vs Independence Number
> $$\theta_0(G) \ge \alpha_0(G)$$

> [!tip] Corollary — Mycielski Graph Vertex Count
> $$n(G_k) = 3 \cdot 2^{k-2} - 1 \quad (k \ge 2)$$

---

### Important Results and Remarks

> [!important] Result — Clique Lower Bound
> For any graph $G$:
> $$\chi(G) \ge \omega(G)$$
> The chromatic number is at least the clique number; however equality does not always hold (e.g., Mycielski graphs have $\omega = 2$ but arbitrarily large $\chi$).

> [!important] Result — Maximum Edges in a $k$-Chromatic Graph on $n$ Vertices
> Among all graphs on $n$ vertices with $\chi(G) = k$, the one with the maximum number of edges is the complete $k$-partite graph with part sizes as equal as possible (Turán-type). For $k$ parts summing to $n$, the edge count is maximized by the balanced partition.

> [!important] Remark — Greedy Algorithm and Vertex Ordering
> The greedy algorithm does **not** always achieve $\chi(G)$; its output depends on the vertex ordering. For a bipartite graph $G$, orderings exist that force the greedy algorithm to use $2$, $3$, or even $4$ colors.

> [!important] Remark — Mycielski Construction Preserves Triangle-Freeness
> The Mycielski construction $G_{k-1} \mapsto G_k$ preserves triangle-freeness and raises $\chi$ by exactly $1$. This shows $\chi$ and $\omega$ are completely independent parameters.

> [!important] Remark — $k$-Critical Subgraph
> Every graph $G$ with $\chi(G) = k$ contains a $k$-critical subgraph. In a $k$-critical graph, every vertex deletion strictly reduces the chromatic number.

> [!important] Remark — Chromatic Number of Unicyclic Graph
> A graph with exactly one cycle (unicyclic graph) has:
> $$\chi(G) = \begin{cases} 2 & \text{if the unique cycle is even} \\ 3 & \text{if the unique cycle is odd} \end{cases}$$

> [!important] Result — Petersen Graph Chromatic Number
> $\chi(\text{Petersen graph}) = 3$. The Petersen graph contains an odd cycle (so $\chi \ge 3$) and admits an explicit proper $3$-coloring.

> [!important] Result — Chemical Storage / Conflict Graph Modeling
> The minimum number of storage rooms for chemicals with pairwise conflicts equals $\chi(G)$, where $G$ is the **conflict graph** (vertices = chemicals, edges = incompatible pairs).

---

## Chapter 9: Edge Colorings

---

### Definitions

> [!note] Proper Edge Coloring
> A **proper edge coloring** of $G$ is an assignment of colors to edges such that no two adjacent edges (sharing a common vertex) receive the same color.

> [!note] Edge-Chromatic Number (Chromatic Index)
> The **edge-chromatic number** (or **chromatic index**) $\chi_1(G)$ is the minimum number of colors required for a proper edge coloring of $G$.

> [!note] Class 1 and Class 2
> A graph $G$ is **Class 1** if $\chi_1(G) = \Delta(G)$, and **Class 2** if $\chi_1(G) = \Delta(G) + 1$.

> [!note] Color Class (Edge Coloring)
> Each color class in a proper edge coloring is a **matching** (a set of pairwise non-adjacent edges).

> [!note] Total Deficiency
> The **total deficiency** of $G$ is:
> $$td(G) = \sum_{v \in V(G)} \big(\Delta(G) - \deg(v)\big)$$

> [!note] Overfull Graph
> A graph $G$ is **overfull** if $m(G) > \Delta(G) \cdot \lfloor n(G)/2 \rfloor$. Every overfull graph is Class 2.

> [!note] $1$-Factorable
> A graph is **$1$-factorable** (or **perfectly edge-colorable**) if its edges can be partitioned into perfect matchings (i.e., it is Class 1 and regular).

---

### Theorems

> [!abstract] Theorem 9.1 — Vizing's Theorem (Gupta–Vizing)
> For every simple graph $G$:
> $$\Delta(G) \le \chi_1(G) \le \Delta(G) + 1$$
> Every simple graph is either Class 1 or Class 2.

> [!abstract] Theorem 9.2 — Edge-Chromatic Number of Complete Graphs
> $$\chi_1(K_n) = \begin{cases} n - 1 & \text{if } n \text{ is even} \\ n & \text{if } n \text{ is odd} \end{cases}$$

> [!abstract] Theorem 9.3 — König's Edge-Coloring Theorem
> Every bipartite graph $G$ is Class 1:
> $$\chi_1(G) = \Delta(G)$$

> [!abstract] Theorem 9.4 — Class 2 Criterion (Overfull Condition)
> If $m(G) > \Delta(G) \cdot \alpha_1(G)$, then $G$ is Class 2.

> [!abstract] Theorem 9.5 — Hamiltonian 3-Regular Graphs are Class 1
> If $G$ is simple, 3-regular, and Hamiltonian, then $\chi_1(G) = 3$.

> [!abstract] Theorem 9.6 — Equitable Edge-Coloring Theorem
> If a graph $G$ has a proper $k$-edge-coloring, then it also has an **equitable** $k$-edge-coloring (one where all color classes differ in size by at most 1).

---

### Corollaries

> [!tip] Corollary — Regular Graphs on Odd Vertices are Class 2
> Every regular simple graph $G$ with $n(G)$ odd and $m(G) > 0$ is Class 2:
> $$\chi_1(G) = \Delta(G) + 1$$

> [!tip] Corollary — Odd Vertex Count and Total Deficiency
> If $G$ is a simple graph with $n(G)$ odd and $td(G) < \Delta(G)$, then $G$ is Class 2.

> [!tip] Corollary — Edge Count Class 2 Criterion
> If $G$ is a loopless graph with $n$ odd and $m(G) \ge n \cdot \Delta(G) / 2$, in particular if $m(G) > \Delta(G) \cdot \alpha_1(G)$, then $\chi_1(G) = \Delta(G) + 1$.

> [!tip] Corollary — Degree Sum on a Class 2 Edge
> Let $\chi_1(G) = \Delta(G) + 1$ and let $e = uv$ be an edge with $\chi_1(G - e) = \Delta(G)$. Then:
> $$\deg(u) + \deg(v) \ge \Delta(G) + 2$$

> [!tip] Corollary — Iterations to Regularize a Bipartite Graph
> In König's proof of Theorem 9.3, the number of iterations needed to raise a bipartite graph $G$ to a $\Delta(G)$-regular bipartite graph is:
> $$t = \Delta(G) - \delta(G)$$

> [!tip] Corollary — $\chi_1$ of Prism Graph
> For any simple graph $G$:
> $$\chi_1(G \,\square\, 2K_2) = \Delta(G \,\square\, 2K_2)$$
> i.e., $G \,\square\, 2K_2$ is always Class 1.

---

### Important Results and Remarks

> [!important] Result — Edge-Chromatic Numbers of Specific Graphs
> | Graph | $\chi_1$ |
> |:--|:--|
> | $K_n$, $n$ even | $n-1$ |
> | $K_n$, $n$ odd | $n$ |
> | Bipartite graph $G$ | $\Delta(G)$ |
> | $d$-regular bipartite graph | $d$ |
> | $d$-cube $Q_d$ | $d$ |
> | Petersen graph | $4$ |
> | $K_5 - e$ | $5$ |
> | $T + T$, $T$ a tree on $n \ge 3$ vertices | $n + \Delta(T)$ |
> | $T_k + C_{2k+1}$ | $2k + 1 + \Delta(T_k)$ |
> | $C_5 + C_5$ | $7$ |
> | $C_{2s} + C_{2t}$ | $2\max(s,t) + 2$ |
> | $K_{5,5,5,5,5}$ | $21$ |

> [!important] Remark — Join of Class 1 Graphs Need Not Be Class 1
> The join of two Class 1 graphs can be Class 2. Counterexample: $K_1 + K_4 = K_5$, both $K_1$ and $K_4$ are Class 1, but $K_5$ is Class 2 (odd regular).

> [!important] Remark — Bipartite Multigraph Scheduling
> For a bipartite multigraph $G$ modeling a teacher–class schedule (edges = required meetings), the minimum number of periods is $\chi_1(G) = \Delta(G)$ by König's theorem. The number of classrooms needed per period equals the size of the largest color class; by the Equitable Edge-Coloring Theorem, this can be made $\lceil m(G)/\chi_1(G) \rceil$.

> [!important] Remark — Conflict Graph for Course Scheduling
> The minimum number of time slots for scheduling courses is $\chi(H)$, where $H$ is the **conflict graph** (vertices = courses, edges join courses sharing at least one student). The minimum number of rooms needed simultaneously equals the largest color class size in an optimal coloring of $H$.

> [!important] Result — Edge Deletion Preserves Class 2 (Near-Regular Odd Graphs)
> Let $G$ be a $d$-regular simple graph with $n(G)$ odd and $d \ge 2$. Any graph $H$ obtained from $G$ by deleting at most $\lfloor(d-1)/2\rfloor$ edges satisfies $\chi_1(H) = \Delta(H) + 1$ (Class 2).

---

## Chapter 10: Planar Graphs

---

### Definitions

> [!note] Planar Graph / Plane Graph
> A graph $G$ is **planar** if it can be drawn in the plane with no edge crossings. A specific such drawing is called a **plane graph**.

> [!note] Face
> A **face** of a plane graph is a connected region of the plane formed by removing the drawing. One face is always unbounded (the **exterior** or **outer** face).

> [!note] Degree of a Face
> The **degree** of a face $f$, written $\deg(f)$, is the number of edges on its boundary (edges traversed twice count twice).

> [!note] Girth
> The **girth** $g(G)$ of a graph is the length of a shortest cycle. For acyclic graphs, girth is undefined.

> [!note] Maximal Planar Graph / Triangulation
> A simple planar graph is **maximal planar** (a **triangulation**) if adding any edge between non-adjacent vertices destroys planarity. Equivalently, every face (including the exterior) has degree exactly 3.

> [!note] Platonic Graphs
> The five **Platonic graphs** are the vertex-edge skeletons of the Platonic solids: tetrahedron ($K_4$), cube ($Q_3$), octahedron ($K_{2,2,2}$), dodecahedron, and icosahedron.

> [!note] Subdivision
> A **subdivision** of a graph $G$ (written $S(G)$) is obtained by replacing each edge of $G$ with a path (inserting degree-2 vertices along edges). A subdivision preserves the cyclomatic number $\mu = m - n + c$.

> [!note] Minor
> A graph $H$ is a **minor** of $G$ if $H$ can be obtained from a subgraph of $G$ by contracting edges. "$G$ contains an $H$-minor" means $H$ is a minor of $G$.

> [!note] Cyclomatic Number (Circuit Rank)
> $$\mu(G) = m(G) - n(G) + c(G)$$
> where $c(G)$ is the number of components. This is the dimension of the cycle space of $G$.

> [!note] $k$-Regular Planar Graphs
> A $k$-regular simple planar graph exists if and only if $k \in \{0,1,2,3,4,5\}$.

---

### Theorems

> [!abstract] Theorem 10.1 — Euler's Formula (Connected Plane Graph)
> For any connected plane graph:
> $$n - m + r = 2$$
> where $n$ = vertices, $m$ = edges, $r$ = faces.

> [!abstract] Theorem 10.2 — Sum of Face Degrees
> For any plane graph:
> $$\sum_{f} \deg(f) = 2m$$
> Every edge is on the boundary of exactly two faces.

> [!abstract] Theorem 10.3 — Planarity Edge Bound
> For any simple planar graph with $n \ge 3$:
> $$m \le 3n - 6$$
> For bipartite simple planar graphs with $n \ge 3$:
> $$m \le 2n - 4$$

> [!abstract] Theorem 10.3 (Girth Form) — Girth-Refined Edge Bound
> For a simple planar graph with $n \ge 3$ and girth $g \ge 3$:
> $$m \le \frac{g}{g-2}(n-2)$$

> [!abstract] Theorem 10.4 — Kuratowski's Theorem
> A graph $G$ is planar if and only if it contains no subdivision of $K_5$ or $K_{3,3}$ as a subgraph.

> [!abstract] Theorem 10.5 — Wagner's Theorem
> A graph $G$ is planar if and only if it contains neither $K_5$ nor $K_{3,3}$ as a minor.

> [!abstract] Theorem 10.6 — Fáry's Theorem
> Every simple planar graph can be drawn as a plane graph in which all edges are straight line segments.

> [!abstract] Theorem 10.7 — Generalized Euler's Formula
> For any plane graph with $c$ components:
> $$n - m + r = c + 1$$

---

### Corollaries

> [!tip] Corollary — Triangulation Edge Count
> A maximal planar graph (triangulation) on $n \ge 3$ vertices satisfies:
> $$m = 3n - 6, \qquad r = 2n - 4$$

> [!tip] Corollary — Minimum Degree in Planar Graphs
> Every simple planar graph satisfies $\delta(G) \le 5$. In particular, every simple planar graph has at least one vertex of degree $\le 5$.

> [!tip] Corollary — At Least 4 Low-Degree Vertices
> Every simple planar graph with $\delta(G) \ge 3$ and $n \ge 4$ has at least **4** vertices of degree $\le 5$.

> [!tip] Corollary — Petersen Graph is Nonplanar
> The Petersen graph ($n=10$, $m=15$, girth 5) is nonplanar since $15 > \frac{5}{3}(10-2) = \frac{40}{3} \approx 13.3$.

> [!tip] Corollary — $K_5$ and $K_{3,3}$ are Nonplanar
> $K_5$: $m=10 > 3(5)-6=9$. $\quad K_{3,3}$: $m=9 > 2(6)-4=8$.

> [!tip] Corollary — Face-Degree Identity for 3-Regular Plane Graphs
> For a connected plane 3-regular graph, with $n_k$ faces of degree $k$:
> $$\sum_{k \ge 3} (k-6)\,n_k + 12 = 0$$
> If further bipartite: $n_4 \ge 6$ (at least 6 quadrilateral faces).

> [!tip] Corollary — Vertex-Degree Identity for Maximal Planar Graphs
> For a simple maximal planar graph with $\Delta(G) = 7$ and $n_k$ vertices of degree $k$:
> $$n_7 = 3n_3 + 2n_4 + n_5 - 12$$
> (The $n_6$ term cancels entirely.)

> [!tip] Corollary — Graphs with $\mu(G) \le 3$ are Planar
> Any graph with cyclomatic number $\mu(G) \le 3$ is planar.
> ($\mu(K_5) = 6$, $\mu(K_{3,3}) = 4$, and subdivisions preserve $\mu$.)

> [!tip] Corollary — $G$ or $G^c$ Nonplanar for $n \ge 11$
> If $n(G) \ge 11$, then at least one of $G$, $G^c$ is nonplanar.

> [!tip] Corollary — No Maximal Planar Graph with Planar Complement
> There is no simple maximal planar graph whose complement is also maximal planar.

---

### Important Results and Remarks

> [!important] Result — Euler's Formula for Disconnected Plane Graphs
> For a plane graph with $c$ components: $n + r = m + c + 1$.

> [!important] Result — Platonic Graphs are All Hamiltonian
> All five Platonic graphs (tetrahedron, cube, octahedron, dodecahedron, icosahedron) are Hamiltonian.

> [!important] Result — Regularity and Planarity
> - $k$-regular simple planar graphs exist iff $k \le 5$.
> - The unique simple 4-regular maximal planar graph is the **octahedron** ($n = 6$, forced by $2n = 3n-6$).
> - The icosahedron is the unique 5-regular planar triangulation on 12 vertices.

> [!important] Result — Faces of $K_{1,1,n}$ (Book Graph)
> The complete tripartite graph $K_{1,1,n}$ (parts of size 1, 1, $n$) is planar with $r = n+1$ faces.

> [!important] Result — Planarity of $K_{a,b,c}$ ($1 \le a \le b \le c$)
> $K_{a,b,c}$ is planar if and only if $a = b = 1$ (any $c$), or $(a,b,c) = (1,2,2)$.

> [!important] Result — Planarity of $K_{1,2,\ldots,n}$
> $K_{1,2,\ldots,n}$ is planar if and only if $n \le 2$.

> [!important] Result — Tree Whose Complement is Maximal Planar
> If a tree $T$ on $n \ge 3$ vertices has $T^c$ maximal planar, then $n = 7$.

> [!important] Result — Degree-5 Vertices When $\delta = 5$
> If $G$ is a simple planar graph with $\delta(G) = 5$, then $G$ has at least 12 vertices of degree exactly 5. The icosahedron achieves this bound with equality.

> [!important] Remark — Any Face Can Become the Outer Face
> Any face of any plane graph can be made the exterior face by a sphere-inversion (stereographic re-projection). This means the combinatorial embedding has no "special" outer face.

> [!important] Remark — Kuratowski's Theorem in Practice
> To prove nonplanarity: exhibit a subgraph that is a subdivision of $K_5$ or $K_{3,3}$.
> To prove planarity: use Euler's formula / edge-count bounds, or direct planar drawing.

> [!important] Remark — Discharging Identity
> For any simple planar graph: $\displaystyle\sum_{v}(6 - \deg(v)) \ge 12$. This identity drives many degree-distribution results (e.g., $\ge 4$ vertices of degree $\le 5$, $\ge 12$ degree-5 vertices when $\delta = 5$).

> [!important] Remark — Nonplanar Degree Conditions (Kuratowski Witness)
> If $G$ is nonplanar, then either: (i) $G$ has at least 5 vertices of degree $\ge 4$ (from $S(K_5)$), or (ii) $G$ has at least 6 vertices of degree $\ge 3$ (from $S(K_{3,3})$).

> [!important] Result — 3-Regular Planar Girth Constraints (on 10 vertices)
> - No 3-regular simple planar graph on 10 vertices has girth 5.
> - The pentagonal prism is the unique 3-regular planar graph on 10 vertices with girth 4.
> - Girth-3 examples on 10 vertices exist (e.g. the prism with a rung replaced by a triangle gadget).

> [!important] Result — Trees and Kuratowski
> For a connected graph $G$, the following are equivalent: (a) $G$ is a tree; (b) $G$ contains no $S(K_3)$; (c) $G$ contains no $K_3$-minor.


---

## Chapter 11: Directed Graphs

---

### Definitions

> [!note] Directed Graph (Digraph)
> A **directed graph** $D$ is a triple $(V, A, I_D)$ where $V$ and $A$ are disjoint sets and $I_D : A \to V \times V$ is a function. An element of $V$ is a **vertex**; an element of $A$ is an **arc**. $|V| = n$, $|A| = m$.

> [!note] Tail, Head, Simple Digraph
> If $I_D(x) = (u, v)$, then $x$ is denoted $x(u, v)$, $u$ is the **tail** of $x$, and $v$ is the **head** of $x$; $x$ is an arc from $u$ to $v$. A loop $x(u,u)$ has $u$ as both its head and tail. A digraph with no multiple arcs and no loops is a **simple digraph**.

> [!note] Underlying Graph
> The **underlying graph** $G(D)$ of a digraph $D(V, A, I_D)$ is obtained by ignoring the direction of arcs: $V(G) = V$, $E(G) = A$, and $I_G(a) = (u,v)$ if $I_D(a) = (u,v)$ or $(v,u)$.

> [!note] Out-degree, In-degree, Out/In-Neighbors
> The **out-degree** $\text{outdeg}_D(v)$ is the number of arcs with $v$ as tail; $N_{\text{out}}(v) = \{x \in V(D) : (v,x) \in A(D)\}$. The **in-degree** $\text{indeg}_D(v)$ is the number of arcs with $v$ as head; $N_{\text{in}}(v) = \{x \in V(D) : (x,v) \in A(D)\}$. If $D$ is simple, $|N_{\text{out}}(v)| = \text{outdeg}(v)$ and $|N_{\text{in}}(v)| = \text{indeg}(v)$.

> [!note] Digraph Isomorphism
> Two digraphs $D_1(V_1, A_1, I_{D_1})$ and $D_2(V_2, A_2, I_{D_2})$ are **isomorphic** ($D_1 \simeq D_2$) if there exist bijections $f: V_1 \to V_2$ and $g: A_1 \to A_2$ such that $x$ is an arc from $u$ to $v$ in $D_1$ iff $g(x)$ is an arc from $f(u)$ to $f(v)$ in $D_2$.

> [!note] Directed Walk, Trail, Path, Cycle
> A **directed walk** $W(v_0, v_t) = (v_0, a_1, v_1, a_2, v_2, \ldots, v_{t-1}, a_t, v_t)$ has $a_i$ as an arc from $v_{i-1}$ to $v_i$; $v_0$ is the **origin**, $v_t$ the **terminus**, and its **length** is $t$. A walk is a **directed trail** if all arcs are distinct, and a **directed path** if all vertices (hence arcs) are distinct. A walk is **closed** if $v_0 = v_t$. A closed walk with all vertices distinct except $v_0 = v_t$ is a **directed cycle**.

> [!note] Weakly, Unilaterally, Strongly Connected
> A digraph is **weakly connected** if its underlying graph is connected. It is **unilaterally connected** if for every pair $u, v$, there is a directed path from $u$ to $v$ or from $v$ to $u$. It is **strongly connected (strong)** if for every pair $u, v$, there is a directed path from $u$ to $v$ **and** from $v$ to $u$.
> $$\text{Strong} \implies \text{Unilateral} \implies \text{Weak}$$
> (converses do not hold).

> [!note] Orientation of a Graph
> If $G$ is a graph, an **orientation** of $G$ is a digraph $D(G)$ obtained by orienting each edge $(x,y)$ of $G$ from $x$ to $y$ or $y$ to $x$ (not both). A loopless graph $G$ has $2^m$ orientations (some possibly isomorphic).

> [!note] Strong Orientation, Strongly Orientable
> An orientation $D(G)$ is a **strong orientation** if $D(G)$ is strong. A graph $G$ is **strongly orientable** if some orientation of it is strongly connected.

> [!note] Eulerian Trail / Eulerian Digraph
> A directed trail containing all arcs of $D$ is an **Eulerian trail** (open or closed). $D$ is an **Eulerian digraph** if it contains a closed Eulerian trail.

> [!note] Hamilton Directed Path / Cycle / Digraph
> A directed path containing all vertices of $D$ is a **Hamilton directed path**. A directed cycle containing all vertices is a **Hamilton directed cycle**. $D$ is a **Hamilton digraph** if it contains a directed Hamilton cycle.

> [!note] Reachability
> A vertex $v$ is **reachable** from $u$ if there is a directed path from $u$ to $v$.

> [!note] Tournament
> An orientation of a complete graph is called a **tournament**. In a tournament $D$, for every pair of distinct vertices $u, v$, exactly one of $(u,v) \in A(D)$ or $(v,u) \in A(D)$ holds.

> [!note] Converse Digraph
> The **converse digraph** $\overleftarrow{D}$ of $D$ has $V(\overleftarrow{D}) = V(D)$, and $(u,v) \in A(\overleftarrow{D})$ iff $(v,u) \in A(D)$.

---

### Theorems

> [!abstract] Theorem 11.1 — Sum of Degrees
> For every digraph $D$:
> $$\sum_{v \in V(D)} \text{outdeg}(v) = \sum_{v \in V(D)} \text{indeg}(v) = m$$

> [!abstract] Theorem 11.2 — Characterization of Strong Digraphs
> A digraph $D$ is strong if and only if it contains a closed directed walk which contains all its vertices.

> [!abstract] Theorem 11.3 — Characterization of Unilaterally Connected Digraphs
> A digraph $D$ is unilaterally connected if and only if it contains a directed walk (not necessarily closed) containing all the vertices of $D$.

> [!abstract] Theorem 11.4 — Directed Cycle from Degree Bound
> Let $D$ be a simple digraph satisfying, for some integer $p$, either:
> (1) $\text{outdeg}(v) \ge p \ge 1$ for every vertex $v$, or
> (2) $\text{indeg}(v) \ge p \ge 1$ for every vertex $v$.
> Then $D$ contains a directed cycle of length $\ge p+1$.

> [!abstract] Theorem 11.5 — Strong Orientability Characterization
> A connected graph $G$ is strongly orientable if and only if $G$ has no cut-edges.

> [!abstract] Theorem 11.6 — Characterization of Eulerian Digraphs
> A digraph $D$ is Eulerian if and only if:
> (i) $D$ is weakly connected, and
> (ii) $\text{outdeg}(v) = \text{indeg}(v)$ for every vertex $v$.

> [!abstract] Theorem 11.7 — Ghouila-Houri's Theorem (1960)
> If $D$ is a simple digraph such that:
> (i) $n \ge 3$,
> (ii) $\text{outdeg}(v) \ge \dfrac{n}{2}$ for every vertex $v$, and
> (iii) $\text{indeg}(v) \ge \dfrac{n}{2}$ for every vertex $v$,
> then $D$ contains a directed Hamilton cycle.

> [!abstract] Theorem 11.8 — Reachability from Maximum Out-Degree Vertex
> If $u$ is a vertex of maximum out-degree in a tournament $D$, then every vertex is reachable from $u$ by a directed path of length at most $2$.

> [!abstract] Theorem 11.9 — Hamilton Path in Tournaments
> Every tournament $D$ contains a directed Hamilton path.

> [!abstract] Theorem 11.10 — Cycles of Every Length in Strong Tournaments
> Every strong tournament $D$ on $n \ge 3$ vertices contains a directed cycle of length $k$, for every $k$, $3 \le k \le n$.

---

### Corollaries

> [!tip] Corollary to Theorem 11.4
> If $D$ is a digraph satisfying any of the conditions stated in Theorem 11.4, then $D$ contains a directed cycle.

> [!tip] Corollary to Theorem 11.3 — Tournaments are Unilaterally Connected
> Every tournament is unilaterally connected.

> [!tip] Corollary to Theorems 11.2 and 11.10 — Strong Tournament Characterization
> A tournament is strong if and only if it contains a directed Hamilton cycle.

---

### Important Results and Remarks

> [!important] Remark — Dropping "Directed"
> In walk/trail/path/cycle definitions, the adjective "directed" can be dropped if it is clear from context that digraphs are under discussion.

> [!important] Remark — Walks Do Not Reverse
> If there exists a $(v_0, v_t)$-directed walk, it is **not** necessary that a $(v_t, v_0)$-directed walk exists.

> [!important] Remark — Walk Implies Path
> If there exists a $(v_0, v_t)$-directed walk, there exists a $(v_0, v_t)$-directed path (obtained by shortcutting repeated vertices).

> [!important] Remark — Connectivity Hierarchy is Strict
> Strongly connected $\implies$ unilaterally connected $\implies$ weakly connected, but none of the converse implications hold in general.

> [!important] Remark — One-Way Traffic Problem
> The strong-orientability question models: *when is it possible to make the roads of a city one-way so that every corner is reachable from every other corner?* Theorem 11.5 answers this: exactly when the road network (as a graph) has no cut-edges.

> [!important] Remark — $P_3$ is Not Strongly Orientable; $K_3$ Is
> $P_3$ (path on 3 vertices) does not admit a strong orientation, since its middle edge is a cut-edge. $K_3$ admits a strong orientation (orient it as a directed triangle).

> [!important] Remark — Hamilton Digraph Implications
> - $D$ contains a directed Hamilton cycle $\implies$ $D$ contains a directed Hamilton path.
> - $D$ contains a directed Hamilton path $\;\not\Rightarrow\;$ $D$ contains a directed Hamilton cycle.
> - $D$ contains a directed Hamilton path $\implies$ $D$ is unilaterally connected (Theorem 11.3).
> - $D$ is Hamilton $\implies$ $D$ is strong (Theorem 11.2).

> [!important] Remark — No Full Characterization of Hamilton Digraphs
> As with Hamilton graphs (Chapter 6), there is no known full characterization of Hamilton digraphs. Theorem 11.7 (Ghouila-Houri) gives only a sufficient condition, analogous to Dirac's condition for Hamilton graphs.

> [!important] Remark — Tournaments Need Not Be Hamiltonian
> A tournament need not contain a directed Hamilton cycle (e.g., a non-strong tournament). However, every **strong** tournament on $\ge 3$ vertices contains a directed Hamilton cycle (Theorem 11.10 / its corollary).

> [!important] Remark — Proof Technique for Theorem 11.4 (Analogy)
> The proof of Theorem 11.4 is similar to that of Theorem 2.2: choose a directed path of maximum length $P(x,y)$; if condition (1) holds, examine $N_{\text{out}}(y)$; if condition (2) holds, examine $N_{\text{in}}(x)$.

> [!important] Remark — Proof Technique for Theorem 11.6 (Analogy)
> The proof of Theorem 11.6 (Eulerian digraph characterization) is similar to the proof of Theorem 5.1 (Eulerian graph characterization).

---

## Chapter 7 (Matrix): Matrix Representation of Graphs

---

### Definitions

> [!note] Adjacency Matrix
> Let $G$ be a graph with vertices $v_1, v_2, \ldots, v_n$ and edges $e_1, e_2, \ldots, e_m$. The **adjacency matrix** $A(G) = [a_{ij}]$ is the $n \times n$ matrix where
> $$a_{ij} = \begin{cases} \text{number of edges joining } v_i \text{ and } v_j, & i \neq j \\ 2 \times (\text{number of loops at } v_i), & i = j \end{cases}$$
> $A(G)$ is a symmetric matrix. For a simple graph, every entry is 0 or 1 and every diagonal entry is 0 (a **binary** or **zero-one** matrix).

> [!note] Incidence Matrix
> The **incidence matrix** $B(G) = [b_{ij}]$ is the $n \times m$ matrix where
> $$b_{ij} = \begin{cases} 0, & v_i \text{ is not incident with } e_j \\ 1, & v_i \text{ is incident with } e_j \text{ and } e_j \text{ is not a loop} \\ 2, & v_i \text{ is incident with } e_j \text{ and } e_j \text{ is a loop} \end{cases}$$
> For a simple graph, $B(G)$ is a zero-one matrix. Each column has exactly two 1's (one per endpoint); the row sum equals $\deg(v_i)$.

> [!note] Circuit Matrix
> Let the number of distinct circuits in $G$ be $q$ and the number of edges be $m$. The **circuit matrix** $C_c(G) = [c_{ij}]$ is the $q \times m$ zero-one matrix where
> $$c_{ij} = \begin{cases} 1, & \text{if the } i\text{th circuit includes the } j\text{th edge} \\ 0, & \text{otherwise} \end{cases}$$

> [!note] Fundamental Circuit Matrix
> A **fundamental circuit matrix** $C_c^f$ is the submatrix of $C_c$ whose rows correspond to the set of fundamental circuits with respect to some spanning tree. If $\mu = m - n + 1$ is the nullity (number of fundamental circuits), then $C_c^f$ is a $\mu \times m$ matrix. With columns arranged so that the $\mu$ chords come first:
> $$C_c^f = [I_\mu \mid C_c^t]$$
> where $I_\mu$ is the $\mu \times \mu$ identity and $C_c^t$ is the $\mu \times (n-1)$ submatrix for the spanning-tree branches.

> [!note] Cut-Set Matrix
> The **cut-set matrix** $C_s(G) = [s_{ij}]$ has rows corresponding to cut-sets and columns to edges:
> $$s_{ij} = \begin{cases} 1, & \text{if the } i\text{th cut-set contains the } j\text{th edge} \\ 0, & \text{otherwise} \end{cases}$$

> [!note] Fundamental Cut-Set Matrix
> The **fundamental cut-set matrix** $C_s^f$ of a connected graph $G$ with $m$ edges and $n$ vertices is an $(n-1) \times m$ submatrix of $C_s$ whose rows correspond to fundamental cut-sets with respect to some spanning tree. With columns arranged so that the $n-1$ branches come last:
> $$C_s^f = [C_s^c \mid I_{n-1}]$$
> where $C_s^c$ is the $(n-1) \times (m-n+1)$ submatrix for the chords.

> [!note] Reduced Incidence Matrix
> Removing any one row from the incidence matrix $B(G)$ of a connected graph gives an $(n-1) \times m$ submatrix $B_f$ called the **reduced incidence matrix**. The deleted vertex is the **reference vertex**. $B_f$ has rank $n-1$.

> [!note] Laplacian (Kirchhoff) Matrix
> The **Laplacian** (or **Kirchhoff matrix**) $K(G)$ is the $n \times n$ matrix obtained from $A(G)$ by:
> 1. Changing the sign of every off-diagonal entry (from $+$ to $-$).
> 2. Replacing the $i$-th diagonal entry by $\deg(v_i)$.
>
> Equivalently, $K(G) = D(G) - A(G)$ where $D(G)$ is the diagonal degree matrix.

> [!note] Number of Spanning Trees $\mathcal{J}(G)$
> $\mathcal{J}(G)$ denotes the number of distinct spanning trees of $G$ (two trees are distinct if their edge sets differ). Key facts:
> - $\mathcal{J}(G) = 0$ iff $G$ is disconnected.
> - $\mathcal{J}(G) = 1$ iff $G$ is a tree.
> - $\mathcal{J}(K_n) = n^{n-2}$ (Cayley's formula).

---

### Theorems

> [!abstract] Theorem 7.1 — Powers of the Adjacency Matrix
> Let $A = [a_{ij}]$ be the adjacency matrix of a simple graph $G$. Then the $(i,j)$-th entry $[A^p]_{ij}$ of $A^p$ is the number of walks of length $p$ from $v_i$ to $v_j$.

> [!abstract] Theorem 7.2 — Distance via Adjacency Matrix
> If $G$ is a connected simple graph, then the distance $d(v_i, v_j)$ is the smallest integer $p \ge 0$ such that $[A^p]_{ij} \neq 0$.

> [!abstract] Theorem 7.3 — Rank of the Incidence Matrix
> If $B(G)$ is the incidence matrix of a connected graph $G$ with $n$ vertices, then $\operatorname{rank}(B(G)) = n - 1$.

> [!abstract] Theorem 7.4 — Orthogonality of $C_c$ and $B$
> Let $C_c$ and $B$ be, respectively, the circuit matrix and the incidence matrix of a self-loop-free graph, with columns arranged in the same edge order. Then every row of $C_c$ is orthogonal to every row of $B$ over $GF(2)$:
> $$B C_c^T = C_c B^T = 0 \pmod{2}$$

> [!abstract] Theorem 7.5 — Rank of the Circuit Matrix
> If $C_c$ is the circuit matrix of a connected graph $G$ with $m$ edges and $n$ vertices, then $\operatorname{rank}(C_c) = m - n + 1$.

> [!abstract] Theorem 7.6 — Rank of the Cut-Set Matrix
> The rank of the cut-set matrix $C_s(G)$ equals the rank of the incidence matrix $B(G)$, which equals the rank of the graph $G$ (i.e., $n - 1$ for a connected graph).

> [!abstract] Theorem 7.7 — Kirchhoff-Matrix-Tree Theorem
> Let $G$ be a loopless graph, $A(G)$ its adjacency matrix, and $K(G)$ its Kirchhoff (Laplacian) matrix. All $(n-1) \times (n-1)$ cofactors of $K(G)$ have the same value, equal to $\mathcal{J}(G)$:
> $$\mathcal{J}(G) = (-1)^{s+t} \det(M_{(s,t)})$$
> where $M_{(s,t)}$ is the $(n-1) \times (n-1)$ matrix obtained from $K(G)$ by deleting the $s$-th row and $t$-th column.

---

### Corollaries

> [!tip] Corollary — Rank of $B(G)$ for Disconnected Graphs
> If $B(G)$ is the incidence matrix of a simple graph $G$ with $n$ vertices and $k$ components, then $\operatorname{rank}(B(G)) = n - k$.

> [!tip] Corollary — Reduced Incidence Matrix of a Tree is Nonsingular
> The reduced incidence matrix of a tree is a square matrix of order $n-1$ and rank $n-1$; hence it is nonsingular.

> [!tip] Corollary — Rank of $C_c$ for Disconnected Graphs
> For a disconnected graph with $k$ components, $e$ edges, and $n$ vertices: $\operatorname{rank}(C_c) = m - n + k$.

> [!tip] Corollary — Cayley's Formula from Kirchhoff
> Applying the Kirchhoff-Matrix-Tree Theorem to $K_n$ gives $\mathcal{J}(K_n) = n^{n-2}$.

> [!tip] Corollary — Spanning Trees Under Edge Multiplication
> If $G^{(k)}$ is obtained from a simple graph $G$ by replacing every edge with $k$ parallel edges, then $\mathcal{J}(G^{(k)}) = k^{n-1} \mathcal{J}(G)$.

---

### Important Results and Remarks

> [!important] Remark — Block-Diagonal Structure of $B(G)$
> If $G$ is disconnected with components $G_1$ and $G_2$, the incidence matrix can be written in block-diagonal form:
> $$B(G) = \begin{bmatrix} B(G_1) & 0 \\ 0 & B(G_2) \end{bmatrix}$$
> The same holds for the circuit matrix $C_c(G)$ and the cut-set matrix $C_s(G)$.

> [!important] Remark — Orthogonality of $C_c^f$ and $C_s^f$
> Since every circuit and every cut-set share an even number of edges, every row of $C_s$ is orthogonal to every row of $C_c$ over $GF(2)$:
> $$C_c C_s^T = C_s C_c^T = 0 \pmod{2}$$

> [!important] Result — Relationships among $B_f$, $C_c^f$, and $C_s^f$
> With a common spanning tree and the same edge ordering:
> - $B_f = [B_c \mid B_t]$ (chords | branches)
> - $C_c^f = [I_\mu \mid C_c^t]$ and $C_s^f = [C_s^c \mid I_{n-1}]$
> - From $B_f (C_c^f)^T = 0 \pmod 2$: $\;B_t^{-1} B_c = (C_c^t)^T$ over $GF(2)$
> - $C_s^c = -(C_c^t)^T = (C_c^t)^T$ over $GF(2)$
> - Given $B$ or $B_f$, one can construct $C_c^f$ and $C_s^f$; given either fundamental matrix, one can construct the other; but $B_f$ cannot in general be recovered from $C_c^f$ or $C_s^f$ alone.

> [!important] Remark — Row Interpretations
> - Each column of $B(G)$ has exactly two 1's (one per endpoint of the edge).
> - The number of 1's in row $i$ of $B(G)$ equals $\deg(v_i)$.
> - A row of all 0's in $B(G)$ corresponds to an isolated vertex.
> - Parallel edges produce identical columns in both $B(G)$ and $C_s(G)$.
> - A column of all 0's in $C_c(G)$ corresponds to a bridge (non-circuit edge).
> - A column of all 0's in $C_s(G)$ corresponds to a self-loop.

---

## Miscellaneous

---

### Necessary Theory (Brief Overview)

> [!note] Vertex Coloring — Definition & Key Bounds
> A proper $k$-vertex-coloring of a simple graph $G = (V, E)$ is a function $f: V(G) \to \{1, 2, \dots, k\}$ such that $uv \in E(G) \implies f(u) \ne f(v)$. Equivalently, it partitions $V(G)$ into $k$ disjoint **independent sets** $V_1, V_2, \dots, V_k$.
>
> **Chromatic Number $\chi(G)$:** The minimum $k$ for which $G$ admits a proper $k$-vertex-coloring.
>
> **Key Bounds:**
> 1. **Clique Lower Bound:** $\chi(G) \ge \omega(G)$
> 2. **Independence Lower Bound:** $\chi(G) \ge \dfrac{n(G)}{\alpha_0(G)}$
> 3. **Greedy Upper Bound:** $\chi(G) \le \Delta(G) + 1$
> 4. **Brooks' Theorem:** $\chi(G) \le \Delta(G)$ for any connected $G$ unless $G \cong K_n$ or $G \cong C_{2p+1}$
> 5. **Bipartite (König):** $\chi(G) \le 2 \iff G$ contains no odd cycles

> [!note] Edge Coloring — Definition & Key Bounds
> A proper $k$-edge-coloring of a loopless graph $G = (V, E)$ is a function $C: E(G) \to \{1, 2, \dots, k\}$ such that adjacent edges (sharing a common vertex) receive distinct colors. Equivalently, it partitions $E(G)$ into $k$ disjoint **matchings** $M_1, M_2, \dots, M_k$.
>
> **Chromatic Index $\chi_1(G)$:** The minimum $k$ for which $G$ admits a proper $k$-edge-coloring.
>
> **Key Bounds & Classification:**
> 1. **Trivial Degree Lower Bound:** $\chi_1(G) \ge \Delta(G)$
> 2. **Gupta–Vizing Theorem:** $\Delta(G) \le \chi_1(G) \le \Delta(G) + 1$; graphs are **Class 1** ($\chi_1 = \Delta$) or **Class 2** ($\chi_1 = \Delta + 1$)
> 3. **König's Edge-Coloring Theorem:** Every bipartite graph is Class 1
> 4. **Line Graph Identity:** $\chi_1(G) = \chi(L(G))$

---

### Detailed Comparison: Vertex vs. Edge Coloring Approaches

> [!abstract] Fundamental Units of Partitioning
> **Vertex Coloring:**
> - Partitions $V(G)$ into independent sets; local cliques $K_r$ force $\chi(G) \ge r$.
>
> **Edge Coloring:**
> - Partitions $E(G)$ into matchings; local stars $K_{1,\Delta}$ force $\chi_1(G) \ge \Delta(G)$.

> [!abstract] Bounding Strategy and Decision Gap
> **Vertex Coloring (Unbounded Local–Global Gap):**
> - Local structure ($\omega(G)$ or $\Delta(G)$) does **not** pin down $\chi(G)$ tightly.
> - By Mycielski's Theorem, triangle-free graphs ($\omega = 2$) can have arbitrarily large $\chi(G)$.
> - Proofs must analyze global cycles, topological embeddings, or sequential vertex orderings.
>
> **Edge Coloring (Strict Binary Dichotomy):**
> - $\chi_1(G)$ takes **only one of two values**: $\Delta(G)$ or $\Delta(G) + 1$.
> - To prove Class 2, show edge density exceeds $\Delta(G)$ matchings:
> $$m(G) > \Delta(G) \cdot \alpha_1(G) \implies \chi_1(G) = \Delta(G) + 1$$
> - For a $\Delta$-regular graph on an odd number of vertices $n$:
> $$m(G) = \frac{n \cdot \Delta(G)}{2} > \Delta(G) \cdot \frac{n-1}{2} \implies \chi_1(G) = \Delta(G) + 1$$

> [!abstract] Core Proof Techniques — Vertex Coloring
> **1. Greedy / Sequential Ordering:**
> - Order vertices $v_1, v_2, \dots, v_n$ by a structural strategy (e.g., reverse perfect elimination ordering for chordal graphs, or by distance from a minimum-degree vertex for Brooks' Theorem).
> - Assign the smallest available color to $v_i$ not conflicting with $N(v_i) \cap \{v_1, \dots, v_{i-1}\}$.
>
> **2. Kempe Chains (Color Swapping):**
> - Let $G_{i,j}$ be the subgraph induced by vertices colored $i$ and $j$.
> - If two target vertices lie in **different components** of $G_{i,j}$, swap colors $i \leftrightarrow j$ in one component to free a color — used in the 5-Color Theorem and Brooks' Theorem.
>
> **3. Inductive Constructions (Mycielski):**
> - Build $G_{k+1}$ from $G_k$ by adding shadow vertices $u_1, \dots, u_p$ (duplicating neighborhoods of $v_1, \dots, v_p$) and an apex $z$ joined to all shadow vertices.

> [!abstract] Core Proof Techniques — Edge Coloring
> **1. Missing Colors & Vizing Fan Recoloring:**
> - At any vertex $x$ in a $(\Delta+1)$-edge-coloring of $G - e$, at least one color is missing since $\deg(x) \le \Delta$.
> - Construct a **Vizing Fan** $(u, v_0), (u, v_1), \dots, (u, v_t)$ at pivot $u$, where color $\alpha_{i+1}$ is missing at $v_i$; shift colors along the fan to eliminate conflicts.
>
> **2. Alternating $\alpha$-$\beta$ Paths:**
> - Build a maximal path $P$ from fan vertex $v_t$ alternating between colors $\alpha$ and $\beta$.
> - Swapping $\alpha \leftrightarrow \beta$ along $P$ breaks cyclic dependencies, allowing the uncolored edge $e = (u, v_0)$ to be colored with $\Delta + 1$ colors.
>
> **3. Regularization and Bipartite Matching Extensions:**
> - To prove $\chi_1(G) = \Delta(G)$ for bipartite $G$: embed $G$ into a $\Delta(G)$-regular bipartite supergraph $H$, then partition $E(H)$ into $\Delta(G)$ perfect matchings via Hall's Marriage Theorem.

> [!important] Summary of Methodological Differences
> | Aspect | Vertex Coloring | Edge Coloring |
> |:--|:--|:--|
> | **Problem** | Partition $V(G)$ into $k$ independent sets? | Partition $E(G)$ into $k$ matchings? |
> | **Lower bound** | Clique number $\omega(G)$ | Maximum degree $\Delta(G)$ |
> | **Upper bound** | $\Delta(G) + 1$ (greedy), $\Delta(G)$ (Brooks) | $\Delta(G) + 1$ (Vizing) |
> | **Gap** | Unbounded (Mycielski) | Binary: Class 1 or Class 2 |
> | **Key invariants** | $\omega(G)$, $\alpha_0(G)$, $\Delta(G)$ | $\Delta(G)$, $m(G)$, $\alpha_1(G)$ |
> | **Proof mechanics** | Vertex orderings, Kempe chains, planarity bounds | Vizing fans, alternating 2-color paths, bipartite regularization |

> [!note] Visual Comparison
> The illustration below depicts the structural distinction between vertex coloring and edge coloring on the $5$-cycle $C_5$:
>
> --Image of: --Vertex vs Edge Coloring Comparison