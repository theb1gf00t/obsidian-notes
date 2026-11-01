
## Chapter 7

> [!question] Q1: Simple Bipartite Graph Edge Bound
> Let $G$ be a simple bipartite graph. Show: (a) $\vert{}E(G)\vert{} \le \alpha_0(G)\beta_0(G)$. (b) If $\vert{}E(G)\vert{} = \alpha_0(G)\beta_0(G)$, then $G$ is a complete bipartite graph.
>
> > [!success]- Solution (Click to expand)
> >
> > ### (a) Proof that $\vert{}E(G)\vert{} \le \alpha_0(G)\beta_0(G)$
> >
> > Let $K$ be a minimum vertex cover of $G$. By definition, $\vert{}K\vert{} = \beta_0(G)$.
> >
> > 1. **Edge-sum over the vertex cover:** Because $K$ is a vertex cover, every edge in $E(G)$ has at least one of its endpoints in $K$. Summing the degrees of all vertices in $K$:
> >
> >    $$\sum_{v \in K} \deg(v) = \vert{}E(G)\vert{} + \vert{}E([K])\vert{}$$
> >
> >    where $E([K])$ denotes the set of edges with both endpoints in $K$. Since $\vert{}E([K])\vert{} \ge 0$, we have:
> >
> >    $$\vert{}E(G)\vert{} \le \sum_{v \in K} \deg(v)$$
> >
> > 2. **Bounding the degree of each vertex:** Because $G$ is a bipartite graph, the vertex set partitions into two independent sets $X$ and $Y$. If $v \in X$, all of its neighbors lie in $Y$. Since $Y$ is an independent set, the neighborhood $N(v) \subseteq Y$ contains no edges between its vertices, making $N(v)$ an independent set in $G$.
> >
> >    By definition of the independence number $\alpha_0(G)$:
> >
> >    $$\deg(v) = \vert{}N(v)\vert{} \le \alpha_0(G) \quad \text{for every } v \in V(G)$$
> >
> > 3. **Combining the inequalities:**
> >
> >    Substituting this degree bound into the edge summation:
> >
> >    $$\vert{}E(G)\vert{} \le \sum_{v \in K} \deg(v) \le \sum_{v \in K} \alpha_0(G) = \vert{}K\vert{} \cdot \alpha_0(G) = \beta_0(G)\alpha_0(G)$$
> >
> > ### (b) Proof that if $\vert{}E(G)\vert{} = \alpha_0(G)\beta_0(G)$, then $G$ is a complete bipartite graph
> >
> > Suppose $\vert{}E(G)\vert{} = \alpha_0(G)\beta_0(G)$. For this equality to hold, both inequalities in part (a) must hold with equality:
> >
> > 1. **$K$ is an independent set:**
> >
> >    $$\vert{}E(G)\vert{} = \sum_{v \in K} \deg(v) \implies \vert{}E([K])\vert{} = 0$$
> >
> >    Thus, no two vertices in $K$ are adjacent, so $K$ is an independent set.
> >
> > 2. **Every vertex in $K$ achieves the maximum possible degree:**
> >
> >    $$\deg(v) = \alpha_0(G) \quad \text{for every } v \in K$$
> >
> > 3. **Structure of the bipartition:**
> >
> >    Let $I = V(G) \setminus K$.
> >
> >    - Since $K$ is a vertex cover, $I$ is an independent set (Theorem 7.1).
> >    - By the Gallai identity, $\vert{}I\vert{} = \vert{}V(G)\vert{} - \vert{}K\vert{} = n - \beta_0(G) = \alpha_0(G)$.
> >    - Since both $K$ and $I$ are independent sets and partition $V(G)$, $[K, I]$ is a valid bipartition of $G$.
> >
> > 4. **Completeness of the bipartite graph:**
> >
> >    Because $K$ is an independent set, all neighbors of any vertex $v \in K$ must lie in $I$, meaning $N(v) \subseteq I$.
> >
> >    We have:
> >
> >    - $\vert{}N(v)\vert{} = \deg(v) = \alpha_0(G)$
> >    - $\vert{}I\vert{} = \alpha_0(G)$
> >
> >    Since $N(v) \subseteq I$ and both finite sets have cardinality $\alpha_0(G)$, it follows that:
> >
> >    $$N(v) = I \quad \text{for every } v \in K$$
> >
> > Every vertex in $K$ is adjacent to every vertex in $I$, and no edges exist within $K$ or within $I$. Therefore, $G$ is the complete bipartite graph $K_{\vert{}K\vert{}, \vert{}I\vert{}} = K_{\beta_0(G), \alpha_0(G)}$.

> [!question] Q2: Equivalent Inequalities Involving $\alpha_0$, $\beta_0$, and $\omega$
> Prove that for any graph $G$, the following inequalities are equivalent. (a) $\beta_0(G) + \beta_0(G^c) \ge \vert{}V(G)\vert{}$. (b) $\alpha_0(G) + \alpha_0(G^c) \le \vert{}V(G)\vert{}$. (c) $\beta_0(G) + \beta_0(G^c) \ge \alpha_0(G) + \alpha_0(G^c)$. (d) $\beta_0(G) \ge \omega(G)$, where $\omega(G) = \max\{\vert{}V(H)\vert{} : H \text{ is a complete subgraph of } G\}$.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G$ be a graph on $n = \vert{}V(G)\vert{}$ vertices, and let $G^c$ denote its complement graph.
> >
> > The proof relies on two fundamental identities:
> >
> > 1. **Gallai's Identity (Corollary to Theorem 7.1):**
> >
> >    For any graph $G$ and its complement $G^c$:
> >
> >    $$\alpha_0(G) + \beta_0(G) = n \implies \beta_0(G) = n - \alpha_0(G) \quad \text{and} \quad \alpha_0(G) = n - \beta_0(G)$$
> >
> >    $$\alpha_0(G^c) + \beta_0(G^c) = n \implies \beta_0(G^c) = n - \alpha_0(G^c) \quad \text{and} \quad \alpha_0(G^c) = n - \beta_0(G^c)$$
> >
> > 2. **Duality between Cliques and Independent Sets:**
> >
> >    A set of vertices $S \subseteq V(G)$ forms a complete subgraph (clique) in $G$ if and only if no two vertices of $S$ are adjacent in $G^c$, meaning $S$ is an independent set in $G^c$. Consequently:
> >
> >    $$\omega(G) = \alpha_0(G^c)$$
> >
> > ### Equivalence of (a) and (b)
> >
> > Statement (a) is:
> >
> > $$\beta_0(G) + \beta_0(G^c) \ge n$$
> >
> > Substituting $\beta_0(G) = n - \alpha_0(G)$ and $\beta_0(G^c) = n - \alpha_0(G^c)$:
> >
> > $$(n - \alpha_0(G)) + (n - \alpha_0(G^c)) \ge n$$
> >
> > $$2n - (\alpha_0(G) + \alpha_0(G^c)) \ge n$$
> >
> > $$\alpha_0(G) + \alpha_0(G^c) \le n$$
> >
> > This is statement (b). Reversing the steps shows that (b) implies (a), so **(a) $\iff$ (b)**.
> >
> > ### Equivalence of (b) and (c)
> >
> > Summing the Gallai identities for $G$ and $G^c$ gives:
> >
> > $$(\alpha_0(G) + \beta_0(G)) + (\alpha_0(G^c) + \beta_0(G^c)) = 2n$$
> >
> > $$\beta_0(G) + \beta_0(G^c) = 2n - (\alpha_0(G) + \alpha_0(G^c))$$
> >
> > Now consider statement (c):
> >
> > $$\beta_0(G) + \beta_0(G^c) \ge \alpha_0(G) + \alpha_0(G^c)$$
> >
> > Substitute the expression for $\beta_0(G) + \beta_0(G^c)$:
> >
> > $$2n - (\alpha_0(G) + \alpha_0(G^c)) \ge \alpha_0(G) + \alpha_0(G^c)$$
> >
> > $$2n \ge 2\big(\alpha_0(G) + \alpha_0(G^c)\big)$$
> >
> > $$\alpha_0(G) + \alpha_0(G^c) \le n$$
> >
> > This matches statement (b). Reversing the steps gives (b) implies (c), so **(b) $\iff$ (c)**.
> >
> > ### Equivalence of (a) and (d)
> >
> > Using $\beta_0(G^c) = n - \alpha_0(G^c)$ from Gallai's identity and substituting $\alpha_0(G^c) = \omega(G)$:
> >
> > $$\beta_0(G^c) = n - \omega(G)$$
> >
> > Substitute this directly into statement (a):
> >
> > $$\beta_0(G) + \beta_0(G^c) \ge n$$
> >
> > $$\beta_0(G) + (n - \omega(G)) \ge n$$
> >
> > $$\beta_0(G) - \omega(G) \ge 0$$
> >
> > $$\beta_0(G) \ge \omega(G)$$
> >
> > This is statement (d). Reversing the steps proves that (d) implies (a), so **(a) $\iff$ (d)**.
> >
> > Since $(a) \iff (b)$, $(b) \iff (c)$, and $(a) \iff (d)$, all four inequalities are mutually equivalent for any graph $G$:
> >
> > $$(a) \iff (b) \iff (c) \iff (d)$$

> [!question] Q3: Maximal Independent Set Containing All Degree-One Vertices in a Tree
> Prove or disprove: In any tree there is a maximal independent set of vertices containing all the vertices of degree one.
>
> > [!success]- Solution (Click to expand)
> >
> > The statement is **FALSE** in general.
> >
> > ### Counterexample (Disproof)
> >
> > Consider the tree $T = K_2$ (the path $P_2$ on $2$ vertices):
> >
> > - Let $V(T) = \{u, v\}$ and $E(T) = \{(u, v)\}$.
> > - $T$ is connected and acyclic, so it is a tree.
> > - The degrees of the vertices are $\deg(u) = 1$ and $\deg(v) = 1$.
> > - Therefore, the set of all vertices of degree one is:
> >
> >   $$L = \{u, v\}$$
> >
> > - Since $u$ and $v$ are adjacent, no independent set can contain both $u$ and $v$.
> > - The only independent sets of $K_2$ are $\emptyset$, $\{u\}$, and $\{v\}$.
> >
> > Neither maximal independent set ($\{u\}$ or $\{v\}$) contains all vertices of degree one. Hence, the statement does not hold for $n = 2$.
> >
> > ### Behavior for Trees with $n \ge 3$ (Proof under $n \ge 3$)
> >
> > If the statement is restricted to trees with at least $3$ vertices ($n \ge 3$), the statement is **TRUE**.
> >
> > #### 1. The set of all leaves is an independent set
> >
> > Let $T$ be a tree on $n \ge 3$ vertices, and let $L = \{v \in V(T) : \deg(v) = 1\}$ be the set of all vertices of degree one.
> >
> > - Suppose, for the sake of contradiction, that two vertices $u, v \in L$ are adjacent.
> > - Since $\deg(u) = 1$ and $\deg(v) = 1$, neither $u$ nor $v$ has any other neighbors in $T$.
> > - Thus, the edge $(u, v)$ forms an entire connected component of $T$.
> > - Since $T$ is connected, the entire vertex set is $V(T) = \{u, v\}$, which implies $n = 2$.
> > - This contradicts the assumption that $n \ge 3$.
> >
> > Therefore, no two vertices in $L$ are adjacent, which proves that **$L$ is an independent set**.
> >
> > #### 2. Extension to a maximal independent set
> >
> > - By definition, an independent set $I$ is maximal if no other independent set properly contains it.
> > - In any finite graph, any independent set $S$ can be extended to a maximal independent set:
> >   1. Start with $I = L$.
> >   2. If there exists a vertex $w \in V(T) \setminus I$ such that no vertex in $I$ is adjacent to $w$, update $I \leftarrow I \cup \{w\}$.
> >   3. Since $V(T)$ is finite, this process terminates in finitely many steps.
> > - When no additional vertices can be added, the resulting set $I$ is a **maximal independent set containing all vertices of degree one**.
> >
> > (Note: In fact, a stronger result holds for $n \ge 3$—there always exists a **maximum** independent set containing all vertices of degree one, since any support vertex present in a maximum independent set can be swapped for its corresponding leaf without reducing the size of the independent set.)

> [!question] Q4: Vertex-Covering Number of $K_{1,t} + K_{1,t}$
> Find the vertex-covering number of $K_{1,t} + K_{1,t}$ $(t > 1)$.
>
> > [!success]- Solution (Click to expand)
> >
> > ### 1. Definitions & Preliminaries
> >
> > 1. **Components of the Graph:** Let $G_1 = K_{1,t}$ and $G_2 = K_{1,t}$ be two disjoint star graphs.
> >
> >    - The star graph $G_1 = K_{1,t}$ consists of $1$ center vertex $c_1$ and $t$ leaf (pendant) vertices $L_1 = \{u_1, u_2, \dots, u_t\}$. Thus, $|V(G_1)| = t + 1$.
> >    - Similarly, $G_2 = K_{1,t}$ consists of $1$ center vertex $c_2$ and $t$ leaf vertices $L_2 = \{v_1, v_2, \dots, v_t\}$. Thus, $|V(G_2)| = t + 1$.
> >
> > 2. **Graph Sum (Join) $G = G_1 + G_2$:** The join $G = G_1 + G_2$ is formed by taking $G_1 \cup G_2$ and adding an edge between **every** vertex of $G_1$ and **every** vertex of $G_2$.
> >
> >    - **Total number of vertices:** $$n(G) = |V(G_1)| + |V(G_2)| = (t + 1) + (t + 1) = 2t + 2$$
> >
> > 3. **Vertex-Covering Number ($\beta_0$) and Independence Number ($\alpha_0$):**
> >
> >    - A subset $K \subseteq V(G)$ is a **vertex cover** if every edge of $G$ has at least one endpoint in $K$. The **vertex-covering number** $\beta_0(G)$ is the minimum size of a vertex cover.
> >    - A subset $I \subseteq V(G)$ is an **independent set** if no two vertices in $I$ are adjacent. The **independence number** $\alpha_0(G)$ is the maximum size of an independent set.
> >    - **Gallai's Identity:** For any graph $G$, $K$ is a vertex cover if and only if $V(G) \setminus K$ is an independent set. Consequently: $$\alpha_0(G) + \beta_0(G) = n(G)$$
> >
> > ### 2. Determining the Independence Number $\alpha_0(G_1 + G_2)$
> >
> > Let $I$ be an independent set of $G = G_1 + G_2$:
> >
> > - By definition of the join $G_1 + G_2$, **every vertex in $V(G_1)$ is adjacent to every vertex in $V(G_2)$**.
> > - Therefore, if $I$ contained a vertex $x \in V(G_1)$ and a vertex $y \in V(G_2)$, the edge $(x, y)$ would exist in $G$, violating the definition of an independent set.
> > - Thus, $I$ must be contained **entirely in $V(G_1)$** or **entirely in $V(G_2)$**.
> >
> > Hence: $$\alpha_0(G_1 + G_2) = \max\{ \alpha_0(G_1), \alpha_0(G_2) \}$$
> >
> > For a star graph $G_1 = K_{1,t}$ with $t > 1$:
> >
> > - The set of leaves $L_1 = \{u_1, u_2, \dots, u_t\}$ forms an independent set of size $t$.
> > - Any independent set containing the center vertex $c_1$ can contain at most $c_1$ itself (size 1), because $c_1$ is adjacent to all leaves.
> > - Since $t > 1$, the maximum independent set of $K_{1,t}$ is $L_1$, so $\alpha_0(K_{1,t}) = t$.
> >
> > Therefore: $$\alpha_0(K_{1,t} + K_{1,t}) = \max(t, t) = t$$
> >
> > ### 3. Calculating the Vertex-Covering Number $\beta_0(K_{1,t} + K_{1,t})$
> >
> > Applying Gallai's identity: $$\beta_0(G) = n(G) - \alpha_0(G)$$ $$\beta_0(K_{1,t} + K_{1,t}) = (2t + 2) - t = t + 2$$
> >
> > ### 4. Direct Structural Construction & Proof
> >
> > We can also directly exhibit a minimum vertex cover $K$:
> >
> > - Choose $K = \{c_1, c_2\} \cup L_1 = \{c_1, c_2, u_1, u_2, \dots, u_t\}$.
> > - The size of $K$ is $|K| = 1 + 1 + t = t + 2$.
> > - The remaining unchosen vertices are $V(G) \setminus K = L_2 = \{v_1, v_2, \dots, v_t\}$.
> > - Since $L_2$ consists solely of the leaves of $G_2$, no two vertices in $L_2$ share an edge. Hence, $V(G) \setminus K$ is an independent set.
> > - By Gallai's Theorem, since $V(G) \setminus K$ is an independent set, $K$ is a valid vertex cover.
> > - Since no independent set in $G$ can exceed size $t$, no vertex cover can have size smaller than $(2t + 2) - t = t + 2$.
> >
> > ### Final Answer
> >
> > $$\beta_0(K_{1,t} + K_{1,t}) = t + 2 \quad \text{for } t > 1.$$

> [!question] Q5: Minimum Edge Covering Number of the $d$-Cube
> Find the minimum edge covering number $\beta_1$ of the d-cube $Q_d$. Justify your answer. And give an example of a minimum edge covering set of $Q_d$.
>
> > [!success]- Solution (Click to expand)
> >
> > ### 1. Definitions & Preliminaries
> >
> > 1. **The $d$-Cube Hypercube ($Q_d$):**
> >
> >    - **Vertex Set:** $V(Q_d) = \{(x_1, x_2, \dots, x_d) : x_i \in \{0, 1\}\}$.
> >    - **Number of Vertices:** $n(Q_d) = |V(Q_d)| = 2^d$.
> >    - **Adjacency:** Two vertices are adjacent if and only if their binary coordinates differ in exactly one position.
> >    - **Regularity & Minimum Degree:** $Q_d$ is $d$-regular, so $\delta(Q_d) = d \ge 1$ for $d \ge 1$.
> >
> > 2. **Edge Cover & Edge Covering Number ($\beta_1$):**
> >
> >    - A subset of edges $F \subseteq E(G)$ is an **edge cover** if every vertex $v \in V(G)$ is incident with at least one edge in $F$.
> >    - Since $\delta(Q_d) \ge 1$, an edge cover exists for $Q_d$.
> >    - The **minimum edge covering number** $\beta_1(G)$ is the minimum size of an edge cover in $G$.
> >
> > ### 2. Justification & Proof
> >
> > We present two rigorous mathematical proofs establishing that $\beta_1(Q_d) = 2^{d-1}$.
> >
> > #### Method 1: Direct Bound Argument
> >
> > - **Lower Bound ($\beta_1(Q_d) \ge 2^{d-1}$):** Each edge $e = (u, v)$ in $Q_d$ covers at most $2$ distinct vertices ($u$ and $v$). To cover all $n(Q_d) = 2^d$ vertices, any edge cover $F$ must satisfy:
> >
> >   $$2 \cdot |F| \ge |V(Q_d)| = 2^d \implies |F| \ge \frac{2^d}{2} = 2^{d-1}$$
> >
> >   Therefore, $\beta_1(Q_d) \ge 2^{d-1}$.
> >
> > - **Upper Bound ($\beta_1(Q_d) \le 2^{d-1}$):** A **perfect matching** $M$ in $Q_d$ is a set of disjoint edges that covers every vertex of $Q_d$ exactly once. Since $Q_d$ is a $d$-regular bipartite graph ($d \ge 1$), by Hall's Marriage Theorem, its edges can be partitioned into $d$ disjoint perfect matchings. A perfect matching $M$ contains exactly $\frac{|V(Q_d)|}{2} = 2^{d-1}$ edges. Since $M$ covers all $2^d$ vertices, $M$ is a valid edge cover of size $2^{d-1}$. Therefore, $\beta_1(Q_d) \le |M| = 2^{d-1}$.
> >
> > Combining both inequalities yields:
> >
> > $$\beta_1(Q_d) = 2^{d-1}$$
> >
> > #### Method 2: Gallai's Theorem for Edge Parameters
> >
> > By **Gallai's Theorem**, for any graph $G$ with minimum degree $\delta(G) > 0$:
> >
> > $$\alpha_1(G) + \beta_1(G) = n(G)$$
> >
> > where $\alpha_1(G)$ is the maximum matching number of $G$.
> >
> > - For $Q_d$, the total number of vertices is $n(Q_d) = 2^d$.
> > - Since $Q_d$ contains a perfect matching, the maximum matching number is:
> >
> >   $$\alpha_1(Q_d) = \frac{n(Q_d)}{2} = 2^{d-1}$$
> >
> > - Applying Gallai's Theorem:
> >
> >   $$\beta_1(Q_d) = n(Q_d) - \alpha_1(Q_d) = 2^d - 2^{d-1} = 2^{d-1}$$
> >
> > ### 3. Explicit Example of a Minimum Edge Covering Set
> >
> > #### General Construction for $Q_d$:
> >
> > Choose any fixed coordinate dimension, say $k = d$. Define $F_d \subseteq E(Q_d)$ as the set of all $2^{d-1}$ edges extending along the $d$-th dimension:
> >
> > $$F_d = \Big\{ \{(x_1, x_2, \dots, x_{d-1}, 0),\, (x_1, x_2, \dots, x_{d-1}, 1)\} : x_i \in \{0, 1\} \text{ for } 1 \le i \le d-1 \Big\}$$
> >
> > - **Size:** $|F_d| = 2^{d-1}$.
> > - **Coverage:** Every vertex $(x_1, x_2, \dots, x_d)$ belongs to exactly one edge in $F_d$ (the edge connecting it to the vertex differing only in the $d$-th bit).
> > - Hence, $F_d$ is a minimum edge cover.
> >
> > #### Concrete Example for $Q_3$ ($d = 3$):
> >
> > - **Vertices ($2^3 = 8$):** $V = \{000, 001, 010, 011, 100, 101, 110, 111\}$.
> > - **Minimum Edge Covering Number:** $\beta_1(Q_3) = 2^{3-1} = 4$.
> > - **Minimum Edge Cover Set $F_3$:**
> >
> >   $$F_3 = \Big\{ (000, 001),\, (010, 011),\, (100, 101),\, (110, 111) \Big\}$$
> >
> > ### Final Answer
> >
> > $$\beta_1(Q_d) = 2^{d-1} \quad \text{for } d \ge 1.$$

> [!question] Q6: $\alpha_0$ and $\beta_1$ of Joins
> Find $\alpha_0$ and $\beta_1$ of $C_{2m+1} + C_{2n}$ and $K_n + C_{2m+1}$.
>
> > [!success]- Solution (Click to expand)
> >
> > ### 1. Key Preliminaries & Properties
> >
> > 1. **Graph Join Property:** For any two graphs $G_1$ and $G_2$, every vertex in $V(G_1)$ is adjacent to every vertex in $V(G_2)$. Therefore, an independent set $I$ in $G_1 + G_2$ **cannot** contain vertices from both $G_1$ and $G_2$. Consequently:
> >
> >    $$\alpha_0(G_1 + G_2) = \max\{\alpha_0(G_1), \alpha_0(G_2)\}$$
> >
> > 2. **Gallai's Identity for Edge Parameters:** For any graph without isolated vertices:
> >
> >    $$\alpha_1(G) + \beta_1(G) = n(G)$$
> >
> >    where $n(G)$ is the total number of vertices and $\alpha_1(G)$ is the maximum matching number.
> >
> > ### 2. Part 1: Parameters for $G = C_{2m+1} + C_{2n}$
> >
> > #### Vertex Count:
> >
> > - $n(G) = |V(C_{2m+1})| + |V(C_{2n})| = (2m + 1) + 2n = 2m + 2n + 1$ (an **odd** integer).
> >
> > #### A. Vertex Independence Number $\alpha_0(G)$:
> >
> > - For the odd cycle $C_{2m+1}$: $\alpha_0(C_{2m+1}) = \lfloor \frac{2m+1}{2} \rfloor = m$.
> > - For the even cycle $C_{2n}$: $\alpha_0(C_{2n}) = \frac{2n}{2} = n$.
> > - Using the join independence property:
> >
> >   $$\alpha_0(C_{2m+1} + C_{2n}) = \max(m, n)$$
> >
> > #### B. Minimum Edge-Covering Number $\beta_1(G)$:
> >
> > - Since total vertices $n(G) = 2m + 2n + 1$ is odd, no matching can cover all vertices. The maximum matching size is bounded by:
> >
> >   $$\alpha_1(G) \le \left\lfloor \frac{2m + 2n + 1}{2} \right\rfloor = m + n$$
> >
> > - **Matching Construction:**
> >   - Pick $m$ independent edges inside $C_{2m+1}$ (covering $2m$ vertices, leaving $1$ vertex unmatched).
> >   - Pick $n$ independent edges inside $C_{2n}$ (covering all $2n$ vertices).
> >   - This yields a set of $m + n$ disjoint edges. Thus, $\alpha_1(G) = m + n$.
> > - **Applying Gallai's Identity:**
> >
> >   $$\beta_1(G) = n(G) - \alpha_1(G) = (2m + 2n + 1) - (m + n) = m + n + 1$$
> >
> > ### 3. Part 2: Parameters for $H = K_n + C_{2m+1}$
> >
> > #### Vertex Count:
> >
> > - $n(H) = |V(K_n)| + |V(C_{2m+1})| = n + 2m + 1$.
> >
> > #### A. Vertex Independence Number $\alpha_0(H)$:
> >
> > - For the complete graph $K_n$: $\alpha_0(K_n) = 1$.
> > - For the odd cycle $C_{2m+1}$: $\alpha_0(C_{2m+1}) = m$.
> > - Using the join independence property (for $m \ge 1$):
> >
> >   $$\alpha_0(K_n + C_{2m+1}) = \max(1, m) = m$$
> >
> > #### B. Minimum Edge-Covering Number $\beta_1(H)$:
> >
> > We analyze by the parity of $n$:
> >
> > - **Case 1: $n$ is odd** (Total vertices $n(H) = n + 2m + 1$ is **even**):
> >
> >   - Pick $m$ edges inside $C_{2m+1}$ (leaving $1$ vertex $u \in V(C_{2m+1})$ unmatched).
> >   - Pick $\frac{n-1}{2}$ edges inside $K_n$ (leaving $1$ vertex $w \in V(K_n)$ unmatched).
> >   - Join $u$ and $w$ via the inter-graph edge $(u, w)$.
> >   - Total matching edges $\alpha_1(H) = m + \frac{n-1}{2} + 1 = m + \frac{n+1}{2}$, which forms a **perfect matching**.
> >   - By Gallai's Identity:
> >
> >     $$\beta_1(H) = n(H) - \alpha_1(H) = (n + 2m + 1) - \left(m + \frac{n+1}{2}\right) = m + \frac{n+1}{2}$$
> >
> > - **Case 2: $n$ is even** (Total vertices $n(H) = n + 2m + 1$ is **odd**):
> >
> >   - Maximum possible matching is $\alpha_1(H) = \frac{n(H)-1}{2} = m + \frac{n}{2}$ (achieved by picking $m$ edges in $C_{2m+1}$ and $\frac{n}{2}$ edges in $K_n$).
> >   - By Gallai's Identity:
> >
> >     $$\beta_1(H) = n(H) - \alpha_1(H) = (n + 2m + 1) - \left(m + \frac{n}{2}\right) = m + \frac{n}{2} + 1$$
> >
> > - **Unified Expression for All $n$:**
> >
> >   $$\beta_1(K_n + C_{2m+1}) = m + \left\lceil \frac{n+1}{2} \right\rceil = \left\lceil \frac{n + 2m + 1}{2} \right\rceil$$
> >
> > ### Summary of Results
> >
> > | Graph | Vertex Count $n(G)$ | $\alpha_0$ (Independence No.) | $\beta_1$ (Edge Cover No.) |
> > |:--|:-:|:-:|:-:|
> > | **$C_{2m+1} + C_{2n}$** | $2m + 2n + 1$ | $\max(m, n)$ | $m + n + 1$ |
> > | **$K_n + C_{2m+1}$** | $n + 2m + 1$ | $m$ | $m + \left\lceil \frac{n+1}{2} \right\rceil$ |

> [!question] Q7: Parameters of $K_{1,2,...,n}$
> Find $\alpha_0$, $\beta_0$, $\alpha_1$ and $\beta_1$ of $K_{1,2,...,n}$.

> [!question] Q8: Disjoint Matchings Exchange
> Let $M$, $N$ be disjoint matchings of a graph $G$ with $\vert{}M\vert{} > \vert{}N\vert{}$. Show that there are disjoint matchings $M_0$ and $N_0$ of $G$ such that $\vert{}M_0\vert{} = \vert{}M\vert{} - 1$ and $\vert{}N_0\vert{} = \vert{}N\vert{} + 1$ and $M_0 \cup N_0 = M \cup N$.

> [!question] Q9: Connected 4-Regular Graph with No Perfect Matching
> Draw a connected 4-regular graph with no perfect matching on $n$-vertices where $n$ is an even integer. What is the minimum value of $n$. Justify your graph indeed has no perfect matching.

> [!question] Q10: $k$-Regular Graph with No Perfect Matching
> For each $k \ge 2$, find an example of a k-regular simple graph which has no perfect matching.

> [!question] Q11: Perfect Matching in Trees
> A tree $T$ has a perfect matching iff $O(T - v) = 1$, for every vertex $v$.

> [!question] Q12: No Perfect Matching in Degree-1-or-3 Trees
> Show that no tree ($n \ge 3$) with every vertex of degree 1 or 3 has a perfect matching.

> [!question] Q13: Perfect Matching in $K_{n,n,n}$
> Let $n > 1$ be an integer. Prove or disprove: (a) If $n$ is even, $K_{n,n,n}$ has a perfect matching. (b) If $n$ is odd, $K_{n,n,n}$ has no perfect matching.

> [!question] Q14: Matching Saturating $X$ in Bipartite Graph
> Prove or disprove: If $G[X, Y]$ is a simple connected bipartite graph such that the degree of every vertex in $X$ is at least 3 and the degree of every vertex in $Y$ is at most 3, then $G$ has a matching saturating every vertex in $X$.

> [!question] Q15: $\beta_0$ and $\beta_1$ of $K_{2,4,6,\dots,2k}$
> Find $\beta_0$ and $\beta_1$ of $K_{2,4,6,\dots,2k}$.
>
> > [!success]- Solution (Click to expand)
> >
> > ### 1. Graph Definitions & Setup
> >
> > Let $G = K_{2, 4, 6, \dots, 2k}$ be a complete $k$-partite graph with $k \ge 1$ partition sets $V_1, V_2, \dots, V_k$.
> >
> > 1. **Part Sizes:** The size of the $i$-th partition set is $|V_i| = 2i$ for $i = 1, 2, \dots, k$.
> >
> > 2. **Total Number of Vertices $n(G)$:**
> >
> >    $$n(G) = \sum_{i=1}^k |V_i| = \sum_{i=1}^k 2i = 2 \cdot \frac{k(k+1)}{2} = k(k+1)$$
> >
> >    Note that $k(k+1)$ is always an **even integer** for all $k \ge 1$.
> >
> > 3. **Adjacency Rule:** Two vertices are adjacent if and only if they belong to **different** partition sets $V_i$ and $V_j$ ($i \neq j$). There are no edges within any single set $V_i$.
> >
> > ### 2. Vertex-Covering Number $\beta_0(G)$
> >
> > #### Step A: Finding the Independence Number $\alpha_0(G)$
> >
> > - An **independent set** $I \subseteq V(G)$ is a subset of vertices with no edges between them.
> > - Since every vertex in $V_i$ is connected to every vertex in $V_j$ for all $i \neq j$, an independent set $I$ can contain vertices from **at most one** partition set $V_i$.
> > - To maximize $|I|$, we select the largest partition set $V_k$, which has size $|V_k| = 2k$.
> > - Thus:
> >
> >   $$\alpha_0(G) = \max_{1 \le i \le k} |V_i| = 2k$$
> >
> > #### Step B: Applying Gallai’s Identity
> >
> > By **Gallai’s Theorem** for vertex parameters:
> >
> > $$\alpha_0(G) + \beta_0(G) = n(G)$$
> >
> > Substituting $n(G) = k(k+1)$ and $\alpha_0(G) = 2k$:
> >
> > $$\beta_0(G) = k(k+1) - 2k = k^2 + k - 2k = k(k-1)$$
> >
> > - **Direct Cover Construction:** The set $K = V_1 \cup V_2 \cup \dots \cup V_{k-1}$ of size $\sum_{i=1}^{k-1} 2i = k(k-1)$ leaves $V \setminus K = V_k$ as an independent set, covering every edge in $G$.
> >
> > ### 3. Minimum Edge-Covering Number $\beta_1(G)$
> >
> > By **Gallai’s Theorem** for edge parameters (for graphs with no isolated vertices):
> >
> > $$\alpha_1(G) + \beta_1(G) = n(G)$$
> >
> > where $\alpha_1(G)$ is the maximum matching number of $G$.
> >
> > We evaluate $\alpha_1(G)$ and $\beta_1(G)$ by analyzing the number of parts $k$:
> >
> > #### Case 1: $k = 1$ ($K_2$ with no edges / empty graph on 2 vertices)
> >
> > - For $k = 1$, $G$ consists of 2 isolated vertices ($E(G) = \emptyset$).
> > - Since there are no edges to cover the vertices, an edge cover **does not exist** (or $\beta_1$ is undefined).
> >
> > #### Case 2: $k = 2$ ($G = K_{2,4}$)
> >
> > - $n(G) = 2(3) = 6$ vertices.
> > - In $K_{2,4}$, edges only exist between $V_1$ (size 2) and $V_2$ (size 4).
> > - Any matching can pick at most $|V_1| = 2$ edges, so $\alpha_1(K_{2,4}) = 2$.
> > - By Gallai’s Identity:
> >
> >   $$\beta_1(K_{2,4}) = n(G) - \alpha_1(G) = 6 - 2 = 4$$
> >
> > #### Case 3: $k \ge 3$
> >
> > To determine if $G$ has a **perfect matching** (meaning $\alpha_1(G) = \frac{n(G)}{2}$), we apply **Tutte’s 1-Factor Theorem**:
> >
> > A complete multipartite graph $G$ with an even number of vertices $n$ has a perfect matching if and only if no single partition set has size strictly greater than $\frac{n}{2}$:
> >
> > $$\max_{1 \le i \le k} |V_i| \le \frac{n(G)}{2}$$
> >
> > Verifying this condition for $k \ge 3$:
> >
> > - Largest part size: $|V_k| = 2k$.
> > - Half of total vertices: $\frac{n(G)}{2} = \frac{k(k+1)}{2}$.
> >
> > We check if $2k \le \frac{k(k+1)}{2}$:
> >
> > $$4k \le k(k+1) \implies 4 \le k+1 \implies k \ge 3$$
> >
> > Since $|V_k| \le \frac{n(G)}{2}$ holds for all $k \ge 3$, **$G$ contains a perfect matching!**
> >
> > - **Matching Number:**
> >
> >   $$\alpha_1(G) = \frac{n(G)}{2} = \frac{k(k+1)}{2}$$
> >
> > - **Edge Covering Number:**
> >
> >   $$\beta_1(G) = n(G) - \alpha_1(G) = k(k+1) - \frac{k(k+1)}{2} = \frac{k(k+1)}{2}$$
> >
> > ### Summary of Results
> >
> > | Parameter | $k = 1$ | $k = 2$ ($K_{2,4}$) | $k \ge 3$ ($K_{2,4,\dots,2k}$) |
> > |:--|:-:|:-:|:-:|
> > | **Vertex-Covering Number $\beta_0$** | $0$ | $2$ | $k(k-1)$ |
> > | **Edge-Covering Number $\beta_1$** | Undefined | $4$ | $\frac{k(k+1)}{2}$ |
> 


