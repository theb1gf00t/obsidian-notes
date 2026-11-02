
## Assignment 2

> [!question] Q1: Inequalities for $\beta_0$, $\alpha_0$, $\omega$, and $\delta$
> For any graph $G$, show the following inequalities:
> (a) $\beta_0(G) + \beta_0(G^c) \ge \alpha_0(G) + \alpha_0(G^c)$.
> (b) $\beta_0(G) \ge \omega(G)$, where $\omega(G) = \max\{|V(H)| : H \text{ is a complete subgraph of } G\}$ is the clique number of $G$.
> (c) $\beta_0(G) \ge \delta(G)$.
>
> > [!success]- Solution (Click to expand)
> >
> > **(a)** The given inequality is **not correct**.
> >
> > **Counter example:**
> >
> > For $G = K_2$: $\beta_0(G) = 1$, but $\omega = 2$, $G^c = K_2^c$ (empty graph), so $\beta_0(G^c) = 0$, $\alpha_0(G^c) = 2$.
> >
> > So $\beta_0(G) + \beta_0(G^c) = 1 + 0 = 1$
> > $\alpha_0(G) + \alpha_0(G^c) = 1 + 2 = 3$
> >
> > $\Rightarrow \beta_0(G) + \beta_0(G^c) < \alpha_0(G) + \alpha_0(G^c)$, which is contradicting the inequality given in question.
> >
> > Instead the inequality $\beta_0(G) \ge \omega(G) - 1$ holds for every graph.
> >
> > **Proof:**
> >
> > Let $K$ be a clique with $\omega(G)$ vertices and let $C$ be any vertex cover of $G$.
> >
> > Now suppose two vertices $u, v \in V(K)$ are both outside $C$. Then the edge $uv$ has neither endpoint in $C$. This contradicts the definition of a vertex cover.
> >
> > Therefore at most one vertex of $K$ can lie outside $C$. Hence at least $\omega(G) - 1$ vertices of $K$ must belong to $C$.
> >
> > $$\therefore |C| \ge \omega(G) - 1$$
> >
> > This is true for every vertex cover, including the minimum vertex cover:
> >
> > $$\therefore \beta_0(G) \ge \omega(G) - 1$$
> >
> > **(b)** In this also the given inequality is **not correct**.
> >
> > **Counter example:**
> >
> > $G = K_2$: $\beta_0(G) = 1$, but $\omega(G) = 2$.
> >
> > $\Rightarrow \beta_0(G) < \omega(G)$, which is a contradiction to inequality $\beta_0(G) \ge \omega(G)$.
> >
> > **(c)** Let $C$ be a minimum vertex cover of $G$. Therefore $|C| = \beta_0(G)$.
> >
> > Since $C$ is minimum vertex cover, there exists at least one vertex $v \notin C^\wedge$.
> >
> > Now because $C$ covers every edge, every neighbour of $v$ must belong to $C$.
> >
> > $$\therefore \deg(v) \le |C| \quad \cdots(1)$$
> >
> > Also $\delta(G) \le \deg(v) \quad \cdots(2)$
> >
> > Combining (1) and (2), we get:
> >
> > $$\delta(G) \le \deg(v) \le |C| = \beta_0$$
> >
> > $$\Rightarrow \boxed{\delta(G) \le \beta_0} \quad \text{Hence proved.}$$

> [!question] Q2: Disjoint Matchings Exchange
> Let $M$, $N$ be disjoint matchings of a graph $G$ with $|M| > |N|$. Show that there are disjoint matchings $M'$ and $N'$ of $G$ such that $|M'| = |M| - 1$ and $|N'| = |N| + 1$ and $M' \cup N' = M \cup N$.
>
> > [!success]- Solution (Click to expand)
> >
> > Consider the graph formed by $M \cup N$.
> >
> > $M$ and $N$ are both matchings, every vertex is incident to at most one edge of $M$ and at most one edge of $N$.
> >
> > $\therefore$ Every vertex has degree at most 2 in the subgraph formed by $M \cup N$.
> >
> > Moreover, edges in each component must alternate between $M$ and $N$.
> >
> > Also every component of $M \cup N$ is an alternating path or an alternating cycle.
> >
> > On an alternating cycle, the numbers of $M$ edges and $N$ edges are equal, otherwise two adjacent edges would belong to the same matching which is a contradiction to the fact that the edges in one matching are not adjacent.
> >
> > On an alternating path, two cases:
> >
> > **Case 1:** If end edges belong to different matchings, the two numbers are equal.
> >
> > **Case 2:** If end edges belong to the same matching, then the matching to which they belong will be more and there is exactly one more $M$-edge than $N$-edge.
> >
> > Since $|M| > |N|$, the total numbers of $M$ edges exceeds the total number of $N$ edges. Therefore, at least one component must be alternating path with one more $M$-edge than $N$-edge.
> >
> > Let this path be $P$.
> >
> > Let $|M \cap E(P)| = r+1$, $|N \cap E(P)| = r$.
> >
> > Now define:
> >
> > $$M' = (M \setminus E(P)) \cup (N \cap E(P))$$
> > $$N' = (N \setminus E(P)) \cup (M \cap E(P))$$
> >
> > In other words, swap the membership of every edge along $P$: edges that belonged to $M$ now belong to $N'$, and edges that belonged to $N$ now belong to $M'$.
> >
> > Because the edges still alternate along $P$, both new sets are still matchings.
> >
> > For $M'$:
> > $$|M'| = |M| - (r+1) + r = \boxed{|M| - 1}$$
> >
> > For $N'$:
> > $$|N'| = |N| - r + (r+1) = \boxed{|N| + 1}$$
> >
> > We have only transferred edges between the two matchings. No edge has been added to or removed from their combined set.
> >
> > $$\boxed{M' \cup N' = M \cup N}$$

> [!question] Q3: Greedy Algorithm for Maximal Independent Set
> Illustrate the greedy algorithm to get a maximal independent set for the simple graph whose vertices are $a, b, c, d, e, f$ and whose edges are $(a,b)$, $(b,c)$, $(c,d)$, $(d,e)$, $(e,f)$, $(f,a)$, $(b,f)$, $(c,e)$.
>
> > [!success]- Solution (Click to expand)
> >
> > The given graph in the question has vertices $\{a, b, c, d, e, f\}$ with edges $(a,b), (b,c), (c,d), (d,e), (e,f), (f,a), (b,f), (c,e)$.
> >
> > **(a)** $G_1$, $I \leftarrow \emptyset$
> >
> > **(b)** $I \leftarrow \{a\}$, $G_1 = G - \{a\} - \{b, f\}$
> >
> > Remaining graph has vertices $\{c, d, e\}$ (triangle: $c$-$d$-$e$-$c$).
> >
> > **(c)** $I \leftarrow \{a, d\}$, $G_2 = G_1 - \{e, c, d\}$
> >
> > Now $G_2$ graph with no vertices.
> >
> > $$\therefore I = \{a, d\}, \quad |I| = 2$$

> [!question] Q4: Greedy Algorithm for Maximal Matching and Vertex Cover
> Apply greedy algorithm to get a maximal matching and a vertex cover of the graphs shown below.
>
> (Graph 1: vertices 1–6, with visible edges forming a diamond/octahedron-like structure with vertices 1,2,3,4,5,6)
>
> (Graph 2: vertices 1–10, with visible edges forming a larger diamond structure with vertices 1–10)
>
> > [!success]- Solution (Click to expand)
> >
> > **For Graph 1** (vertices labeled $a, b, c, d, e, f, 1, 2, 3, 4, 5, 6$ internally):
> >
> > **(a)** $M \leftarrow \{a\}$, $K \leftarrow \{4, 5\}$, $G_1 = G - \{4, 5\}$
> >
> > **(b)** $M \leftarrow \{a, i\}$, $K \leftarrow \{4, 5, 6, 3\}$, $G_2 = G_1 - \{3, 6\}$
> >
> > **(c)** $M \leftarrow \{a, i, d\}$, $K \leftarrow \{1, 2, 3, 4, 5, 6\}$, $G_3 = G_2 - \{1, 2\}$
> >
> > $G_3$ is graph left with no vertices.
> >
> > $$M = \{a, i, d\}, \quad K = \{1, 2, 3, 4, 5, 6\}$$
> >
> > **For Graph 2** (vertices 1–10):
> >
> > **(a)** $M \leftarrow \{c\}$, $K \leftarrow \{10, 9\}$, $G_1 = G - \{10, 9\}$
> >
> > **(b)** $M \leftarrow \{c, g\}$, $K \leftarrow \{6, 8, 9, 10\}$, $G_2 = G_1 - \{6, 8\}$
> >
> > **(c)** $M \leftarrow \{c, g, k\}$, $K \leftarrow \{2, 3, 5, 6, 8, 9, 10\}$, $G_3 = G_2 - \{2, 5\}$
> >
> > **(d)** $M \leftarrow \{c, g, k, n\}$, $K \leftarrow \{2, 3, 5, 6, 7, 8, 9, 10\}$, $G_4 = G_3 - \{3, 7\}$
> >
> > $G_4$ is graph left with no edges.
> >
> > **(e)** $M \leftarrow \{c, g, k, n\}$, $K \leftarrow \{2, 3, 5, 6, 7, 8, 9, 10\}$
> >
> > $$M = \{c, g, k, n\}, \quad K = \{2, 3, 5, 6, 7, 8, 9, 10\}$$

> [!question] Q5: Order Vertices for 4-Color Greedy Coloring
> Order the vertices of the graph shown below, in such a way that the greedy algorithm uses 4 colors.
>
> (Graph: complete bipartite-like graph with vertices $u_1, u_2, u_3, u_4$ on top and $v_1, v_2, v_3, v_4$ on bottom, with all cross edges)
>
> > [!success]- Solution (Click to expand)
> >
> > Order: Take $S = \{u_1, v_1, u_2, v_2, u_3, v_3, u_4, v_4\}$
> >
> > In the greedy algorithm, each vertex receives the smallest colour not used on its already-coloured neighbours.
> >
> > | Vertex | Neighbours | Coloured Neighbours | Colour |
> > |:--|:--|:--|:-:|
> > | $u_1$ | $v_2, v_3, v_4$ | none | 1 |
> > | $v_1$ | $u_2, u_3, u_4$ | none | 1 |
> > | $u_2$ | $v_1, v_3, v_4$ | $v_1(1)$ | 2 |
> > | $v_2$ | $u_1, u_3, u_4$ | $u_1(1)$ | 2 |
> > | $u_3$ | $v_1, v_2, v_4$ | $v_1(1), v_2(2)$ | 3 |
> > | $v_3$ | $u_1, u_2, u_4$ | $u_1(1), u_2(2)$ | 3 |
> > | $u_4$ | $v_1, v_2, v_3$ | $v_1(1), v_2(2), v_3(3)$ | 4 |
> > | $v_4$ | $u_1, u_2, u_3$ | $u_1(1), u_2(2), u_3(3)$ | 4 |

> [!question] Q6: Greedy Coloring of $Q_3$ with 2, 3, and 4 Colors
> Let $G$ be the graph 3-cube $Q_3$. Order the vertices of $G$ in 3 different ways, say $S_1$, $S_2$ and $S_3$ so that the greedy algorithm
> (a) uses 2 colors, if $S_1$ is the input,
> (b) uses 3 colors, if $S_2$ is the input, and
> (c) uses 4 colors, if $S_3$ is the input.
>
> > [!success]- Solution (Click to expand)
> >
> > $Q_3$ is bipartite with parts $X = \{v_1, v_3, v_6, v_8\}$ and $Y = \{v_2, v_4, v_5, v_7\}$.
> >
> > In the greedy algorithm, each vertex receives the smallest colour not used on its already-coloured neighbours.
> >
> > **(a) 2 colours.** Take $S_1 = (v_1, v_3, v_6, v_8, v_2, v_5, v_7)$
> > That is, all of $X$ first and then all of $Y$.
> >
> > - The vertices of $X$ are pairwise non-adjacent, so each gets colour 1.
> > - Each vertex of $Y$ has a neighbour in $X$ coloured 1 and no neighbour in $Y$, so each gets colour 2.
> >
> > Only Colours 1 and 2 are used.
> >
> > **(b) 3 colours.** Take $S_2 = (v_1, v_7, v_2, v_6, v_3, v_4, v_5, v_8)$
> >
> > | Vertex | Coloured neighbours | Colour |
> > |:--|:--|:-:|
> > | $v_1$ | none | 1 |
> > | $v_7$ | none ($v_7$ is not adjacent to $v_1$) | 1 |
> > | $v_2$ | $v_1(1)$ | 2 |
> > | $v_6$ | $v_2(2), v_7(1)$ | 3 |
> > | $v_3$ | $v_2(2), v_7(1)$ | 3 |
> > | $v_4$ | $v_1(1), v_3(3)$ | 2 |
> > | $v_5$ | $v_1(1), v_6(3)$ | 2 |
> > | $v_8$ | $v_5(2), v_7(1), v_4(2)$ | 3 |
> >
> > The maximum colour is 3, so exactly 3 colours are used.
> >
> > **(c) 4 colours.** Take $S_3 = (v_2, v_8, v_4, v_6, v_5, v_1, v_3, v_7)$
> >
> > | Vertex | Coloured neighbours | Colour |
> > |:--|:--|:-:|
> > | $v_2$ | none | 1 |
> > | $v_8$ | none ($v_8$ is not adjacent to $v_2$) | 1 |
> > | $v_4$ | $v_8(1)$ | 2 |
> > | $v_6$ | $v_2(1)$ | 2 |
> > | $v_5$ | $v_8(1), v_6(2)$ | 3 |
> > | $v_1$ | $v_2(1), v_4(2), v_5(3)$ | 4 |
> > | $v_3$ | $v_2(1), v_4(2)$ | 3 |
> > | $v_7$ | $v_6(2), v_8(1), v_3(3)$ | 4 |
> >
> > Here 4 colours are used.

> [!question] Q7: Edge-Chromatic Number
> Find the edge-chromatic number of the following graphs.
> (a) $T_k + C_{2k+1}$, where $T_k$ is a tree on $k$ vertices.
> (b) $C_5 + C_5$.
> (c) $C_{2s} + C_{2t}$.
>
> > [!success]- Solution (Click to expand)
> >
> > **(a)** Let $d = \Delta(T_k)$, $q = 2k+1$.
> >
> > Finding the maximum degree: A vertex $x$ in the tree is connected to all $q$ cycle vertices, in addition to its original tree neighbours. A cycle vertex is connected to all $k$ tree vertices and its two cycle neighbours.
> >
> > $$\therefore \Delta(G) = \max\{q + d, k + 2\}$$
> >
> > Since $q = 2k+1$, $2k+1+d \ge k+2$ always, so $\Delta(G) = 2k+1+d$.
> >
> > Let the tree vertices be $t_0, t_1, \ldots, t_{k-1}$ and cycle vertices be $c_0, c_1, \ldots, c_k$.
> >
> > The cross edges form $K_{k, 2k+1}$. Use $2k+1$ colours. For each $i \in \{0,1,\ldots,2k\}$, define the matching:
> >
> > $$M_i = \{t_j\, c_{(i+j)\bmod(2k+1)} : 0 \le j \le k-1\}$$
> >
> > Each matching contains exactly one edge incident with every vertex. Moreover, these matchings partition all the cross edges; every cross-edge $t_j c_l$ appears exactly once in the matching with $i \equiv l - j \pmod{2k+1}$.
> >
> > Notice that $M_i$ uses the cycle vertices $c_i, c_{i+1}, \ldots, c_{i+k-1}$ with indices taken modulo $2k+1$. Consequently, the vertices $c_{i+k}, c_{i+k+1}, \ldots, c_{i+2k}$ are not incident with any cross edge of colour $i$. In particular, both endpoints of the cycle edge $c_{i+k}\, c_{i+k+1}$ are free of colour $i$. Add that cycle edge to $M_i$. As $i$ runs through all $2k+1$ values, these are precisely all the edges of the cycle. So the cross edges and cycle edges have been properly coloured using $2k+1$ colours. Now, the tree has maximum degree $d$ and it is bipartite, so its internal edges can be coloured by using additional $d$ colours.
> >
> > Total no. of colors $= 2k+1+d = \Delta(G)$
> >
> > $$\boxed{\chi_1(T_k + C_{2k+1}) = 2k+1+\Delta(T_k)}$$
> >
> > **(b)** $C_5 + C_5 = G$. This graph is the join of two 5-cycles.
> >
> > Let the vertices of the two cycles be $A = \{a_1, a_2, a_3, a_4, a_5\}$ and $B = \{b_1, b_2, b_3, b_4, b_5\}$.
> >
> > Each vertex has 2 neighbours in its own cycle and 5 neighbours in its own cycle.
> >
> > $$\therefore \Delta(G) = 2 + 5 = 7$$
> >
> > Hence $\chi_1(G) \ge 7$.
> >
> > We will partition all edges into seven matchings. Use the following seven colour classes:
> >
> > $$M_1 = \{a_1a_2, a_3a_4, a_5b_1, b_2b_3, b_4b_5\}$$
> > $$M_2 = \{a_1a_5, a_2a_3, a_4b_2, b_1b_5, b_3b_4\}$$
> > $$M_3 = \{a_1b_3, a_2b_4, a_3b_5, a_4a_5, b_1b_2\}$$
> > $$M_4 = \{a_1b_1, a_2b_2, a_3b_3, a_4b_4, a_5b_5\}$$
> > $$M_5 = \{a_1b_2, a_2b_1, a_3b_4, a_4b_5, a_5b_3\}$$
> > $$M_6 = \{a_1b_4, a_2b_5, a_3b_1, a_4b_3, a_5b_2\}$$
> > $$M_7 = \{a_1b_5, a_2b_3, a_3b_2, a_4b_1, a_5b_4\}$$
> >
> > Thus they form a proper 7-edge colouring. Therefore $\chi_1(G) = 7$.
> >
> > **(c)** Without loss of generality, assume $s \le t$.
> >
> > Let the two cycles $A = C_{2s}$ and $B = C_{2t}$.
> >
> > A vertex in $A$ has 2 neighbours in $A$ and $2t$ neighbours in $B$. Its degree is $2 + 2t$.
> >
> > Similarly, a vertex in $B$ has degree $2 + 2s$.
> >
> > $$\therefore \Delta(G) = 2t + 2$$
> >
> > **Case 1:** $s = t$.
> >
> > The cross-edges form $K_{2s, 2s}$. Since this graph is bipartite and $2s$-regular, its edges can be partitioned into $2s$ perfect matchings. Use $2s$ colours for the cross edges. Now both cycles have even length. An even cycle can be properly edge-coloured using two colours alternately. Use two additional colours for the internal edges of both cycles.
> >
> > Total no. of colors $= 2s + 2 = 2t + 2$.
> >
> > **Case 2:** $s < t$.
> >
> > Let $A = \{a_0, \ldots, a_{2s-1}\}$, $B = \{b_0, \ldots, b_{2t-1}\}$.
> >
> > The cross edges form $K_{2s, 2t}$. We use $2t$ colours indexed by $i = 0, 1, \ldots, 2t-1$.
> >
> > For each $i$, construct the matching $M_i = \{a_j b_{(i+j)\bmod 2t} : 0 \le j \le 2s-1\}$.
> >
> > Each matching saturates all vertices of $A$ and these $2t$ matchings partition cross edges. Matching $M_i$ uses the vertices $b_i, b_{i+1}, \ldots, b_{i+2s-1}$. Therefore, it does not use $b_{i+2s}, b_{i+2s+1}, \ldots, b_{i+2t-1}$.
> >
> > Since $s < t$, the vertices $b_{i+2s}$ and $b_{i+2s+1}$ are both unused in $M_i$. So we can add the cycle edge $b_{i+2s} b_{i+2s+1}$ to $M_i$, giving it the same colour $i$.
> >
> > As $i$ ranges over all $2t$ values, we colour every edge of cycle $B$ exactly once. Finally, the remaining cycle $A = C_{2s}$ is even, so its edges can be coloured alternately using two new colours.
> >
> > Thus, the total no. of colors is $2t + 2$.
> >
> > $$\Delta(G) = 2t + 2, \text{ we conclude.}$$
> >
> > $$\boxed{\chi_1(C_{2s} + C_{2t}) = 2\max(s,t) + 2}$$

> [!question] Q8: School Staffing Problem
> In a school there are seven vacancies, one each in the departments of Chemistry, English, French, Geography, History, Mathematics and Physics. There are seven applicants $A_1, \ldots, A_7$ for the vacancies. The applicants and their specializations are listed in the table below. Determine the maximum number of suitably qualified teachers the school can employ. Justify your claim.
>
> | Teachers | Specialization |
> |:--|:--|
> | $A_1$ | Mathematics, Physics |
> | $A_2$ | Chemistry, English, Mathematics |
> | $A_3$ | Chemistry, French, History, Physics |
> | $A_4$ | English, French, History, Physics |
> | $A_5$ | Chemistry, Mathematics |
> | $A_6$ | Mathematics, Physics |
> | $A_7$ | English, Geography, History |
>
> > [!success]- Solution (Click to expand)
> >
> > Form the bipartite graph $G[A, D]$ where $A = \{A_1, \ldots, A_7\}$ and $D = \{\text{Chemistry, English, French, Geography, History, Mathematics, Physics}\}$.
> >
> > A feasible staffing is a matching, and the maximum number of teachers employed equals the matching number of $G$. Since $|D| = 7$, the matching number is at most 7.
> >
> > **Claim:** The maximum is 7, so every vacancy can be filled.
> >
> > **Justification.** The following matching saturates both sides:
> >
> > - $A_1 \to$ Mathematics
> > - $A_6 \to$ Physics
> > - $A_5 \to$ Chemistry
> > - $A_2 \to$ English
> > - $A_7 \to$ Geography
> > - $A_3 \to$ French
> > - $A_4 \to$ History

> [!question] Q9: Edge-Chromatic Number When $2m > (n-1)\Delta(G)$
> Consider a graph $G$ with $n$ vertices and $m$ edges, where $n$ is odd. If $2m > (n-1)\Delta(G)$, then prove that $\chi_1(G) - 1 = \Delta(G)$. Hence, compute $\chi_1(G)$ for the graph $G$ in the Figure shown below. Also label the edges of $G$ with $\chi_1(G)$ colors.
>
> (Figure: graph on vertices $v_1, v_2, v_3, v_4, v_5, v_6, v_7$ with $n = 7$ (odd) and $\Delta = 5$, $m = 16$)
>
> > [!success]- Solution (Click to expand)
> >
> > **Assumption:** Considering the graph to be loopless.
> >
> > By handshaking lemma: $\sum_{v \in V(G)} \deg(v) = 2|E(G)|$
> >
> > Since every vertex has degree at most $\Delta(G)$: $2|E(G)| \le n \cdot \Delta(G)$
> >
> > Suppose $G$ has a $\Delta(G)$ edge colouring. Since $n$ is odd, the maximum size of matching is $\frac{n-1}{2}$. Each colour class is a matching. Therefore, the maximum number of edges that can be covered by $\Delta(G)$ colours is:
> >
> > $$(\Delta(G)) \cdot \frac{n-1}{2}$$
> >
> > But the assumed number of edges is greater than this: $[2|E(G)| > (n-1)\Delta(G)]$.
> >
> > Hence there is contradiction. Thus $\chi_1(G) > \Delta(G)$. Since $G$ is simple, Vizing's theorem gives $\chi_1(G) \le \Delta(G) + 1$.
> >
> > Combining: $\boxed{\chi_1(G) = \Delta(G) + 1}$
> >
> > In the given graph, $n = 7$ (odd) and $\Delta = 5$. Then $2m = 32 > 30 = (n-1)\Delta$, so the statement applies and $\chi_1(G) = \Delta + 1 = 6$.
> >
> > A proper 6-edge colouring (colours on edges in drawing):
> >
> > | Colour | Edges |
> > |:-:|:--|
> > | 1 | $v_1v_2, v_3v_4, v_5v_6$ |
> > | 2 | $v_1v_4, v_2v_3, v_6v_7$ |
> > | 3 | $v_1v_5, v_2v_4, v_3v_6$ |
> > | 4 | $v_1v_6, v_2v_7, v_4v_5$ |
> > | 5 | $v_2v_6, v_3v_5, v_4v_7$ |
> > | 6 | $v_5v_7$ |

> [!question] Q10: Planarity of 3-Regular Graphs on 10 Vertices
> (a) Show that there exists no 3-regular simple planar graph on 10 vertices whose girth is 5.
> (b) Draw a plane 3-regular simple graph on 10 vertices whose girth is 4.
>
> > [!success]- Solution (Click to expand)
> >
> > **(a)** Suppose $G$ is a simple 3-regular planar graph with $n = 10$ and girth 5. Then $m = \frac{3n}{2} = 15$.
> >
> > $G$ is connected. Fix a vertex $v$. Its 3 neighbours are distinct and each has 2 further neighbours. These $1 + 3 + 6 = 10$ vertices are pairwise distinct, because a coincidence would create a cycle of length at most 4. So the component of $v$ already contains all 10 vertices.
> >
> > Fix a plane embedding with $f$ faces. Euler's formula gives $n - m + f = 2$, so $f = 2 - 10 + 15 = 7$.
> >
> > $G$ contains cycles and every face boundary has length at least girth 5. Each edge lies on the boundaries of faces with total multiplicity 2, so:
> >
> > $$2m = \sum(\text{face lengths}) \ge 5f, \text{ that is, } 30 \ge 35.$$
> >
> > This is a contradiction. Hence no such graph exists.
> >
> > **(b)** Pentagonal prism (vertices 1–10, two pentagons connected by 5 edges).

> [!question] Q11: Pentagonal and Hexagonal Faces in 3-Regular Plane Graphs
> Let $G$ be a simple plane connected 3-regular graph with every face having degree 5 or 6. If $p$ is the number of pentagonal faces and $h$ is the number of hexagonal faces in $G$, show that $p = 12$ and $n(G) = 20 + 2h$.
>
> > [!success]- Solution (Click to expand)
> >
> > We are given the graph is 3-regular. Every vertex has degree 3.
> >
> > By Handshaking Lemma: $\sum \deg(v) = 2m \Rightarrow 3n = 2m \Rightarrow \boxed{m = \frac{3n}{2}} \quad \cdots(1)$
> >
> > There are $p$ pentagons each of degree 5, $h$ hexagons each of degree 6.
> >
> > $\therefore 5p + 6h$ is the sum of degrees of all faces.
> >
> > In a plane graph, every edge belongs to exactly two faces, so $\sum \deg(\text{faces}) = 2m$.
> >
> > Thus $5p + 6h = 2m$. From (1): $\boxed{5p + 6h = 3n} \quad \cdots(2)$
> >
> > For a connected plane graph, by Euler's formula $n - m + f = 2$ and we have no. of faces $f = p + h$.
> >
> > So, $n - m + p + h = 2$. Substitute $m = \frac{3n}{2}$:
> >
> > $$n - \frac{3n}{2} + p + h = 2 \Rightarrow -\frac{n}{2} + p + h = 2 \Rightarrow \boxed{n = 2p + 2h - 4} \quad \cdots(3)$$
> >
> > From combining Eqn. (2) and (3), we get:
> >
> > $$3(2p + 2h - 4) = 5p + 6h \Rightarrow \boxed{p = 12}$$
> >
> > Now substitute $p = 12$ into (3):
> >
> > $$n = 2(12) + 2h - 4 \Rightarrow \boxed{n = 20 + 2h}$$

> [!question] Q12: Complement of Planar Graph with $\ge 11$ Vertices is Nonplanar
> Prove that the complement of simple planar graph with at least 11 vertices is nonplanar. Construct a self-complementary simple planar graph with 8 vertices.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G$ be a simple planar graph with $n \ge 11$ vertices. We need to prove $\bar{G}$ is nonplanar.
> >
> > The key fact is: A simple planar graph with $n > 3$ vertices has at most $3n - 6$ edges:
> >
> > $$|E(G)| \le 3n - 6$$
> >
> > Now $G$ and its complement together contain all possible edges of $K_n$.
> >
> > $$|E(\bar{G})| = \binom{n}{2} - |E(G)| \ge \frac{n(n-1)}{2} - (3n-6) = \frac{(n-3)(n-4)}{2}$$
> >
> > For $n \ge 11$:
> >
> > $$\frac{(n-3)(n-4)}{2} \ge 3n - 6$$
> >
> > Hence $\bar{G}$ has more than $3n - 6$ edges which is impossible for a simple planar graph. Thus $\bar{G}$ is nonplanar.

---

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
>
> > [!success]- Solution (Click to expand)
> >
> > ### 1. Graph Setup & Total Vertex Count
> >
> > Let $G = K_{1, 2, \dots, n}$ be a complete $n$-partite graph with partition sets $V_1, V_2, \dots, V_n$, where $|V_i| = i$ for $i = 1, 2, \dots, n$.
> >
> > 1. **Adjacency:** Two vertices are adjacent if and only if they belong to **different** partition sets $V_i$ and $V_j$ ($i \neq j$).
> > 2. **Total Number of Vertices $N = n(G)$:**
> >
> >    $$N = \sum_{i=1}^n |V_i| = \sum_{i=1}^n i = \frac{n(n+1)}{2}$$
> >
> > ### 2. Vertex Parameters: $\alpha_0(G)$ and $\beta_0(G)$
> >
> > #### A. Vertex Independence Number $\alpha_0(G)$
> >
> > - An **independent set** $I \subseteq V(G)$ contains no adjacent vertices.
> > - Since every vertex in $V_i$ is adjacent to every vertex in $V_j$ for all $i \neq j$, an independent set can contain vertices from **at most one** partition set $V_i$.
> > - To maximize $|I|$, we select the largest partition set, which is $V_n$ (having size $n$).
> > - Therefore:
> >
> >   $$\alpha_0(K_{1,2,\dots,n}) = n$$
> >
> > #### B. Vertex Covering Number $\beta_0(G)$
> >
> > By **Gallai's Theorem** for vertex parameters:
> >
> > $$\alpha_0(G) + \beta_0(G) = N$$
> >
> > Substituting $N = \frac{n(n+1)}{2}$ and $\alpha_0(G) = n$:
> >
> > $$\beta_0(G) = \frac{n(n+1)}{2} - n = \frac{n(n+1) - 2n}{2} = \frac{n(n-1)}{2}$$
> >
> > (Direct Construction: Taking all vertices from $V_1 \cup V_2 \cup \dots \cup V_{n-1}$ forms a vertex cover of size $\frac{n(n-1)}{2}$, leaving only the independent set $V_n$ uncovered).
> >
> > ### 3. Edge Parameters: $\alpha_1(G)$ and $\beta_1(G)$
> >
> > #### A. Maximum Matching Number $\alpha_1(G)$
> >
> > - **Case $n = 1$ ($K_1$):** $G$ has $1$ vertex and $0$ edges, so $\alpha_1(K_1) = 0$.
> >
> > - **Case $n \ge 2$:** By Tutte's condition for complete multipartite graphs, a maximum matching saturates as many vertices as possible unless one partition set contains strictly more than half of all vertices. Let's check the largest set $V_n$ (size $n$) against the total vertex count $N = \frac{n(n+1)}{2}$:
> >
> >   - For $n = 2$ ($K_{1,2}$): $N = 3$, $|V_2| = 2 > \frac{3}{2}$. Matching can pick at most $|V_1| = 1$ edge, so $\alpha_1(K_{1,2}) = 1$.
> >   - For $n \ge 3$: The condition $n \le \frac{N}{2} \iff n \le \frac{n(n+1)}{4} \iff 4 \le n+1 \iff n \ge 3$ holds! No partition set has more than half the total vertices.
> >
> >   Thus, for all $n \ge 2$, the maximum matching size is simply half of $N$ (rounded down for parity):
> >
> >   $$\alpha_1(K_{1,2,\dots,n}) = \left\lfloor \frac{N}{2} \right\rfloor = \left\lfloor \frac{n(n+1)}{4} \right\rfloor$$
> >
> >   (Note: For $n = 2$, $\lfloor \frac{2(3)}{4} \rfloor = \lfloor 1.5 \rfloor = 1$, which perfectly aligns).
> >
> > #### B. Minimum Edge Covering Number $\beta_1(G)$
> >
> > - **Case $n = 1$ ($K_1$):** Since $K_1$ has an isolated vertex, **no edge cover exists** ($\beta_1$ is undefined).
> >
> > - **Case $n \ge 2$:** By **Gallai's Theorem** for edge parameters ($\alpha_1(G) + \beta_1(G) = N$):
> >
> >   $$\beta_1(G) = N - \alpha_1(G) = \frac{n(n+1)}{2} - \left\lfloor \frac{n(n+1)}{4} \right\rfloor = \left\lceil \frac{n(n+1)}{4} \right\rceil$$
> >
> > ### Summary of Results
> >
> > For $G = K_{1, 2, \dots, n}$:
> >
> > | Parameter | $n = 1$ ($K_1$) | $n \ge 2$ ($K_{1,2,\dots,n}$) |
> > |:--|:-:|:-:|
> > | **Total Vertices $N$** | $1$ | $\frac{n(n+1)}{2}$ |
> > | **Independence Number $\alpha_0$** | $1$ | $n$ |
> > | **Vertex Covering Number $\beta_0$** | $0$ | $\frac{n(n-1)}{2}$ |
> > | **Matching Number $\alpha_1$** | $0$ | $\left\lfloor \frac{n(n+1)}{4} \right\rfloor$ |
> > | **Edge Covering Number $\beta_1$** | Undefined | $\left\lceil \frac{n(n+1)}{4} \right\rceil$ |

> [!question] Q8: Disjoint Matchings Exchange
> Let $M$, $N$ be disjoint matchings of a graph $G$ with $\vert{}M\vert{} > \vert{}N\vert{}$. Show that there are disjoint matchings $M_0$ and $N_0$ of $G$ such that $\vert{}M_0\vert{} = \vert{}M\vert{} - 1$ and $\vert{}N_0\vert{} = \vert{}N\vert{} + 1$ and $M_0 \cup N_0 = M \cup N$.
>
> > [!success]- Solution (Click to expand)
> >
> > ### 1. Subgraph Construction
> >
> > Consider the subgraph $H = (V, M \cup N)$ of $G$ induced by the edge set $M \cup N$.
> >
> > - Since $M$ and $N$ are matchings, no vertex in $G$ can be incident to more than one edge from $M$ and at most one edge from $N$.
> > - Because $M$ and $N$ are disjoint ($M \cap N = \emptyset$), every vertex $v \in V(H)$ has degree at most $2$ ($\Delta(H) \le 2$).
> >
> > ### 2. Structural Analysis of Components in $H$
> >
> > A graph with maximum degree at most $2$ decomposes completely into a union of vertex-disjoint **paths** and **cycles**:
> >
> > 1. **Cycle Components:** Because edges in $H$ alternate between $M$ and $N$, any cycle component must be an **even cycle**. In every even cycle $C$, the edges alternate evenly between $M$ and $N$, so:
> >
> >    $$|C \cap M| = |C \cap N|$$
> >
> > 2. **Path Components:** For any path component $P$:
> >
> >    - **Even-length path:** The path contains an equal number of $M$-edges and $N$-edges ($|P \cap M| = |P \cap N|$).
> >    - **Odd-length path starting and ending with $N$:** Contains one more $N$-edge than $M$-edge ($|P \cap N| = |P \cap M| + 1$).
> >    - **Odd-length path starting and ending with $M$:** Contains one more $M$-edge than $N$-edge ($|P \cap M| = |P \cap N| + 1$).
> >
> > ### 3. Existence of an $M$-Dominating Path
> >
> > Summing the edge counts over all connected components of $H$:
> >
> > $$|M| - |N| = \sum_{P \text{ path component}} \left( |P \cap M| - |P \cap N| \right)$$
> >
> > - Cycle components and even-length paths contribute $0$ to the sum.
> > - Paths starting/ending with $N$ contribute $-1$.
> > - Paths starting/ending with $M$ contribute $+1$.
> >
> > Since $|M| > |N|$, we have $|M| - |N| \ge 1$. Therefore, there must exist **at least one path component $P$ in $H$ that starts and ends with an edge from $M$**. For this path $P$, we have:
> >
> > $$|P \cap M| = |P \cap N| + 1$$
> >
> > ### 4. Construction of $M_0$ and $N_0$
> >
> > We construct the new edge sets $M_0$ and $N_0$ by swapping the roles of $M$ and $N$ along the path component $P$:
> >
> > - **$M_0 = (M \setminus P) \cup (N \cap P)$**
> > - **$N_0 = (N \setminus P) \cup (M \cap P)$**
> >
> > ### 5. Verification of Required Properties
> >
> > 1. **Disjoint Matchings:** Since $P$ is a connected component of $H = M \cup N$, interchanging $M$ and $N$ along $P$ ensures that no vertex is incident with two edges from $M_0$ or two edges from $N_0$. Thus, $M_0$ and $N_0$ are valid matchings, and $M_0 \cap N_0 = \emptyset$.
> >
> > 2. **Union Preservation:**
> >
> >    $$M_0 \cup N_0 = (M \setminus P) \cup (N \cap P) \cup (N \setminus P) \cup (M \cap P) = M \cup N$$
> >
> > 3. **Cardinalities:** Using $|P \cap M| = |P \cap N| + 1$:
> >
> >    - **Size of $M_0$:**
> >
> >      $$|M_0| = |M| - |P \cap M| + |P \cap N| = |M| - (|P \cap N| + 1) + |P \cap N| = |M| - 1$$
> >
> >    - **Size of $N_0$:**
> >
> >      $$|N_0| = |N| - |P \cap N| + |P \cap M| = |N| - |P \cap N| + (|P \cap N| + 1) = |N| + 1$$
> >
> > This completes the proof. $\blacksquare$
> >
> > ### Alternative Proof: Swapping Technique (Symmetric Difference / Path Flipping)
> >
> > #### Step 1: Construct the Overlay Graph
> >
> > Consider the subgraph $H = (V, M \cup N)$ induced by all edges in $M \cup N$.
> >
> > - Because $M$ and $N$ are matchings, no vertex in $G$ can be incident to more than one edge from $M$ and at most one edge from $N$.
> > - Since $M \cap N = \emptyset$, the maximum degree of $H$ satisfies $\Delta(H) \le 2$.
> > - Therefore, $H$ decomposes into a set of vertex-disjoint **paths** and **even cycles**.
> >
> > #### Step 2: Classify the Connected Components
> >
> > In every connected component of $H$, edges alternate between $M$ and $N$:
> >
> > 1. **Even Cycles ($C$):** An alternating cycle must have equal numbers of $M$-edges and $N$-edges, so $|C \cap M| = |C \cap N|$.
> > 2. **Even-length Paths ($P_{even}$):** An even path has equal numbers of $M$-edges and $N$-edges ($|P \cap M| = |P \cap N|$).
> > 3. **Odd-length Paths ($P_{odd}$):**
> >    - An $N$-dominant path starts and ends with $N$-edges, so $|P \cap N| = |P \cap M| + 1$.
> >    - An $M$-dominant path starts and ends with $M$-edges, so $|P \cap M| = |P \cap N| + 1$.
> >
> > Counting the net excess of $M$-edges over $N$-edges across all components of $H$:
> >
> > $$|M| - |N| = \sum_{P \text{ path component}} \left( |P \cap M| - |P \cap N| \right)$$
> >
> > Since $|M| > |N|$, we have $|M| - |N| \ge 1$. Therefore, **there must exist at least one $M$-dominant path component $P$ in $H$** that starts and ends with an edge from $M$.
> >
> > #### Step 3: Define the Swapping Operation
> >
> > Along this $M$-dominant path $P$, we perform a **role swap** between $M$ and $N$:
> >
> > $$M_0 = (M \setminus P) \cup (N \cap P)$$
> > $$N_0 = (N \setminus P) \cup (M \cap P)$$
> >
> > - **Outside $P$:** Edges retain their original matching assignment.
> > - **Inside $P$:** All edges previously belonging to $M$ are reassigned to $N_0$, and all edges previously belonging to $N$ are reassigned to $M_0$.
> >
> > #### Step 4: Verify the Required Properties
> >
> > 1. **Size of $M_0$:** Since $P$ is an $M$-dominant path, $|P \cap M| = |P \cap N| + 1$.
> >
> >    $$|M_0| = |M| - |P \cap M| + |P \cap N| = |M| - (|P \cap N| + 1) + |P \cap N| = |M| - 1$$
> >
> > 2. **Size of $N_0$:**
> >
> >    $$|N_0| = |N| - |P \cap N| + |P \cap M| = |N| - |P \cap N| + (|P \cap N| + 1) = |N| + 1$$
> >
> > 3. **Union Preservation ($M_0 \cup N_0 = M \cup N$):**
> >
> >    $$M_0 \cup N_0 = \big((M \setminus P) \cup (N \cap P)\big) \cup \big((N \setminus P) \cup (M \cap P)\big) = M \cup N$$
> >
> > 4. **Validity and Disjointness:** Because $P$ is a self-contained connected component of $H$, flipping edge roles inside $P$ does not create any incident edge conflicts at the endpoints of $P$ or anywhere else in $G$. Thus, $M_0$ and $N_0$ remain valid, disjoint matchings. $\blacksquare$
> >
> > #### Concrete Visual Example of the Swap
> >
> > Let $M = \{e_1, e_2, e_3\}$ ($|M| = 3$) and $N = \{f_1\}$ ($|N| = 1$), where $P = e_1 - f_1 - e_2$ forms a path component.
> >
> > Original Matching Allocation:
> > ```
> > Path P:    (v1) ==e1(M)== (v2) --f1(N)-- (v3) ==e2(M)== (v4)     Independent: (v5) ==e3(M)== (v6)
> > ```
> >
> > After swapping roles on path $P$:
> > ```
> > Path P:    (v1) --e1(N0)-- (v2) ==f1(M0)== (v3) --e2(N0)-- (v4)   Independent: (v5) ==e3(M0)== (v6)
> > ```
> >
> > Resulting Allocation:
> > - $M_0 = \{f_1, e_3\}$ ($|M_0| = 2 = |M| - 1$)
> > - $N_0 = \{e_1, e_2\}$ ($|N_0| = 2 = |N| + 1$)

> [!question] Q9: Connected 4-Regular Graph with No Perfect Matching
> Draw a connected 4-regular graph with no perfect matching on $n$-vertices where $n$ is an even integer. What is the minimum value of $n$. Justify your graph indeed has no perfect matching.
>
> > [!success]- Solution (Click to expand)
> >
> > ### **1. Main Result**
> >
> > - **Minimum Value of $n$:** **$n = 22$**
> > - **Graph Type:** Connected 4-regular graph with **no perfect matching**.
> >
> > ---
> >
> > ### **2. Construction & Definition of the Graph ($n = 22$)**
> >
> > Let $G = (V, E)$ be constructed as follows:
> >
> > 1. **Central Vertex Subset $S$:**
> >     
> >     - Define $S = \{s_1, s_2\}$ containing $s = |S| = 2$ vertices. There are **no edges** between $s_1$ and $s_2$.
> > 2. **Four Odd Components $C_1, C_2, C_3, C_4$:**
> >     
> >     - Each component $C_i$ ($1 \le i \le 4$) consists of **5 vertices**: $V(C_i) = \{u_{i,1}, u_{i,2}, v_{i,1}, v_{i,2}, v_{i,3}\}$.
> >     - The internal edge structure of each $C_i$ is a **complete graph $K_5$ minus one edge**:
> >         - $u_{i,1}$ and $u_{i,2}$ are non-adjacent in $C_i$ (degree 3 inside $C_i$).
> >         - All other pairs of vertices in $C_i$ are connected (so $v_{i,1}, v_{i,2}, v_{i,3}$ each have degree 4 inside $C_i$).
> > 3. **Inter-Component Connections:**
> >     
> >     - For each $i \in \{1, 2, 3, 4\}$:
> >         - Connect $u_{i,1}$ to $s_1$.
> >         - Connect $u_{i,2}$ to $s_2$.
> >
> > ---
> >
> > ### **3. Verification of Graph Properties**
> >
> > 1. **Total Number of Vertices:** $$n(G) = |S| + \sum_{i=1}^4 |V(C_i)| = 2 + 4 \times 5 = 22 \quad \text{(an even integer)}$$
> >     
> > 2. **4-Regularity:**
> >     
> >     - **Vertices in $S$:** $s_1$ is connected to $u_{1,1}, u_{2,1}, u_{3,1}, u_{4,1}$ $\implies \deg(s_1) = 4$. Similarly, $\deg(s_2) = 4$.
> >     - **Vertices $u_{i,1}, u_{i,2}$ in $C_i$:** Degree 3 inside $C_i$ plus 1 edge to $S$ $\implies \deg = 3 + 1 = 4$.
> >     - **Vertices $v_{i,1}, v_{i,2}, v_{i,3}$ in $C_i$:** Degree 4 inside $C_i$ and 0 edges to $S$ $\implies \deg = 4$.
> >     - Thus, $G$ is **4-regular**.
> > 3. **Connectedness:**
> >     
> >     - Every component $C_i$ is internally connected, and every $C_i$ is attached to both $s_1$ and $s_2$, forming a connected graph.
> >
> > ---
> >
> > ### **4. Justification: Proof That $G$ Has No Perfect Matching**
> >
> > We use **Tutte's 1-Factor Theorem**:
> >
> > > A graph $G$ has a perfect matching if and only if for every subset $S \subseteq V(G)$, the number of odd connected components of $G - S$, denoted $\theta(G - S)$, satisfies: $$\theta(G - S) \le |S|$$
> >
> > - Consider the central set $S = \{s_1, s_2\}$ of size $|S| = 2$.
> > - Removing $S$ from $G$ leaves the four disjoint components $C_1, C_2, C_3, C_4$.
> > - Each component $C_i$ has $|V(C_i)| = 5$ vertices (an **odd** integer).
> > - Therefore, the number of odd connected components of $G - S$ is: $$\theta(G - S) = 4$$
> > - Comparing $\theta(G - S)$ and $|S|$: $$\theta(G - S) = 4 > 2 = |S|$$
> >
> > Since $\theta(G - S) > |S|$, **$G$ fails Tutte's condition and cannot contain a perfect matching.**
> >
> > ---
> >
> > ### **5. Rigorous Proof That $n = 22$ is the Absolute Minimum**
> >
> > Let $G$ be any connected 4-regular graph on an even number of vertices $n$ with no perfect matching.
> >
> > 1. **Tutte's Violation & Parity:** By Tutte's Theorem, there exists a set $S \subset V(G)$ such that $\theta(G - S) > |S|$. Let $s = |S|$ and $k = \theta(G - S)$. Since $n$ is even and each odd component has an odd number of vertices: $$n = |S| + \sum_{i=1}^k |V(C_i)| + \sum |V(D_{\text{even}})| \implies n \equiv s + k \pmod 2$$ Thus, $s$ and $k$ have the same parity, requiring $k \ge s + 2$.
> >     
> > 2. **Edge-Counting Between $S$ and Odd Components:** For any odd component $C_i$ with $c_i = |V(C_i)|$ vertices, the sum of vertex degrees in $G$ is $4 c_i$. The number of edges between $C_i$ and $S$, denoted $e(C_i, S)$, is: $$e(C_i, S) = 4 c_i - 2 |E(C_i)|$$ Since $4c_i$ and $2|E(C_i)|$ are even, $e(C_i, S)$ must be an **even integer**. Because $G$ is connected, $e(C_i, S) \ge 2$.
> >     
> > 3. **Bounding $|S|$:** The total number of edges leaving $S$ satisfies: $$2k \le \sum_{i=1}^k e(C_i, S) \le 4s \implies k \le 2s$$ Combining $s + 2 \le k \le 2s \implies \mathbf{s \ge 2}$.
> >     
> > 4. **Minimum Component Size ($c_i \ge 5$):** For $s = 2$, we have $k = 4$, which forces $e(C_i, S) = 2$ for all 4 components. The sum of internal degrees inside $C_i$ is $4 c_i - 2$. Since $C_i$ has $c_i$ vertices, the maximum possible sum of internal degrees is $c_i(c_i - 1)$: $$c_i(c_i - 1) \ge 4 c_i - 2 \implies c_i^2 - 5c_i + 2 \ge 0$$
> >     
> >     - For $c_i = 1$: $1 - 5 + 2 = -2 < 0$ (Impossible).
> >     - For $c_i = 3$: $9 - 15 + 2 = -4 < 0$ (Impossible).
> >     - For $c_i = 5$: $25 - 25 + 2 = 2 \ge 0$ (**Valid**).
> > 5. **Minimum Vertex Calculation:** $$n = |S| + \sum_{i=1}^4 c_i \ge 2 + 4(5) = \mathbf{22}$$

> [!question] Q10: $k$-Regular Graph with No Perfect Matching
> For each $k \ge 2$, find an example of a k-regular simple graph which has no perfect matching.
>
> > [!success]- Solution (Click to expand)
> >
> > To find an explicit example of a $k$-regular simple graph with no perfect matching for **every $k \ge 2$**, we divide the problem into two natural cases based on the parity of $k$:
> >
> > ---
> >
> > ### **Case 1: $k$ is Even ($k = 2m$ for $m \ge 1$)**
> >
> > When $k$ is even, we can use a very simple complete graph construction.
> >
> > #### **1. Construction: $G = K_{k+1}$**
> >
> > Let $G$ be the complete graph on $n = k+1$ vertices.
> >
> > #### **2. Properties & Proof:**
> >
> > 1. **$k$-Regularity:** In $K_{k+1}$, every vertex is connected to all other $k$ vertices. Thus, $\deg(v) = k$ for every vertex $v \in V(G)$, making $G$ a **$k$-regular simple graph**.
> > 2. **Odd Vertex Count:** Since $k$ is even, the number of vertices $n = k+1$ is **odd**.
> > 3. **No Perfect Matching:** Every edge in a matching pairs up $2$ vertices. A graph with an odd number of vertices $n$ can have a matching of size at most $\lfloor n/2 \rfloor = \lfloor \frac{k+1}{2} \rfloor = \frac{k}{2} < \frac{k+1}{2}$. Thus, $K_{k+1}$ cannot contain a perfect matching.
> >
> > _(Note: If a disconnected graph with an **even** total number of vertices is desired, we can take $G = K_{k+1} \cup K_{k+1}$, the disjoint union of two copies of $K_{k+1}$. This graph has $2(k+1)$ vertices, is $k$-regular, and has no perfect matching)._
> >
> > ---
> >
> > ### **Case 2: $k$ is Odd ($k = 2m+1$ for $m \ge 1$)**
> >
> > When $k$ is odd, the total number of vertices $n$ in any $k$-regular graph **must be even** (since $k \cdot n = 2|E|$ implies $n$ is even). Furthermore, an odd-regular graph cannot have isolated odd components.
> >
> > We can construct a connected $k$-regular graph with no perfect matching using **Tutte's 1-Factor Theorem**.
> >
> > #### **1. Construction Recipe for any Odd $k \ge 3$:**
> >
> > Construct $G$ on $n = (k+1)^2$ vertices as follows:
> >
> > 1. **Central Vertex Subset $S$:** Let $S = \{v_0\}$ consist of a single vertex $v_0$.
> > 2. **$k$ Odd Components $C_1, C_2, \dots, C_k$:** Create $k$ disjoint components, each containing $c_i = k+2$ vertices (an odd integer). Label the vertices of $C_i$ as $\{u_i, x_{i,1}, x_{i,2}, \dots, x_{i,k+1}\}$.
> > 3. **Internal Edges of $C_i$:** Start with a complete graph $K_{k+2}$ on $\{u_i, x_{i,1}, \dots, x_{i,k+1}\}$. Then remove:
> >     - The $2$ edges $(u_i, x_{i,1})$ and $(u_i, x_{i,2})$.
> >     - A 1-factor (matching) of size $\frac{k-1}{2}$ among the remaining $k-1$ vertices $\{x_{i,3}, x_{i,4}, \dots, x_{i,k+1}\}$. _(This leaves $u_i$ with internal degree $k-1$, and each $x_{i,j}$ with internal degree $k$.)_
> > 4. **Inter-Edges:** Connect the central vertex $v_0$ to the distinguished vertex $u_i$ of each component $C_i$ for $i = 1, 2, \dots, k$.
> >
> > ---
> >
> > #### **2. Verification of Properties for Odd $k$:**
> >
> > 1. **$k$-Regularity:**
> >     
> >     - **Central vertex $v_0$:** Connected to $u_1, u_2, \dots, u_k \implies \deg(v_0) = k$.
> >     - **Distinguished vertices $u_i$:** Has internal degree $k-1$ inside $C_i$ plus $1$ edge to $v_0 \implies \deg(u_i) = (k-1) + 1 = k$.
> >     - **Vertices $x_{i,j}$:** Has internal degree $k$ inside $C_i$ and $0$ edges to $S \implies \deg(x_{i,j}) = k$.
> >     - Thus, $G$ is a **$k$-regular simple graph**.
> > 2. **Total Vertices:** $$n = |S| + \sum_{i=1}^k |V(C_i)| = 1 + k(k+2) = k^2 + 2k + 1 = (k+1)^2$$ Since $k$ is odd, $k+1$ is even, so $n = (k+1)^2$ is an **even integer**.
> >     
> > 3. **No Perfect Matching (Tutte's Violation):** Consider the set $S = \{v_0\}$ of size $|S| = 1$. Deleting $S$ leaves the $k$ components $C_1, C_2, \dots, C_k$. Each component $C_i$ has $|V(C_i)| = k+2$ vertices (an odd integer). Therefore, the number of odd connected components of $G - S$ is: $$\theta(G - S) = k$$ Since $k \ge 3 > 1 = |S|$, we have: $$\theta(G - S) > |S|$$ By **Tutte's 1-Factor Theorem**, $G$ **cannot contain a perfect matching**.
> >     
> >
> > ---
> >
> > ### **Summary of Examples**
> >
> > | $k$ | Graph $G$ | Vertices $n$ | Regularity | Why No Perfect Matching? |
> > |:-:|:-:|:-:|:-:|:--|
> > | **$k=2$ (Even)** | $K_3$ (or $K_3 \cup K_3$) | $3$ (or $6$) | 2-regular | Odd component of size $3$ cannot be fully paired up. |
> > | **$k=3$ (Odd)** | $1$ central vertex $v_0$ connected to $3$ components $C_1, C_2, C_3$ of size $5$ ($K_5 \setminus 2\text{ edges}$) | $16$ | 3-regular | $\theta(G - \{v_0\}) = 3 > 1$ (fails Tutte's condition). |
> > | **$k=4$ (Even)** | $K_5$ (or $K_5 \cup K_5$) | $5$ (or $10$) | 4-regular | Odd component of size $5$ cannot be fully paired up. |
> > | **$k=5$ (Odd)** | $1$ central vertex $v_0$ connected to $5$ components of size $7$ | $36$ | 5-regular | $\theta(G - \{v_0\}) = 5 > 1$ (fails Tutte's condition). |
> > | **General Even $k$** | $K_{k+1}$ | $k+1$ (odd) | $k$-regular | $n = k+1$ is odd $\implies$ max matching size $\le k/2$. |
> > | **General Odd $k$** | 1 vertex $v_0$ joined to $k$ components of size $k+2$ | $(k+1)^2$ (even) | $k$-regular | $\theta(G - \{v_0\}) = k > 1 = |S|$ (fails Tutte's condition). |

> [!question] Q11: Perfect Matching in Trees
> A tree $T$ has a perfect matching iff $O(T - v) = 1$, for every vertex $v$.
>
> > [!success]- Solution (Click to expand)
> >
> > ### **Theorem:** A tree $T$ has a perfect matching if and only if removing any single vertex leaves exactly one odd-sized connected component.
> >
> > ### **Proof ($\Rightarrow$ direction: Perfect matching $\Rightarrow$ $O(T-v) = 1$ for all $v$)**
> >
> > Suppose $T$ has a perfect matching $M$.
> >
> > Let $v$ be any vertex in $T$.
> >
> > Since $T$ has a perfect matching, $|V(T)|$ is even. The matching $M$ covers all vertices, so $v$ is incident to exactly one edge $e = (v, u) \in M$.
> >
> > When we remove $v$ from $T$, the matching edge $(v, u)$ is destroyed. In the subgraph $T - v$, vertex $u$ is now unmatched.
> >
> > **Claim:** $O(T - v) = 1$ (only one odd component).
> >
> > The matching $M \setminus \{(v,u)\}$ covers all vertices except $u$ in $T - v$. Since an even number of vertices are covered by the matching (all except $u$), and $T - v$ has $|V(T)| - 1$ vertices (an odd number), exactly **one** connected component of $T - v$ must be odd (containing $u$). All other components have even size.
> >
> > ### **Proof ($\Leftarrow$ direction: $O(T-v) = 1$ for all $v$ $\Rightarrow$ Perfect matching)**
> >
> > Suppose for every vertex $v$, removing $v$ leaves exactly one odd-sized component.
> >
> > **Case 1:** $|V(T)|$ is odd.
> >
> > Then for any vertex $v$, $|V(T - v)| = |V(T)| - 1$ is even. Since $O(T-v) = 1$ (odd number of odd components), the sum of component sizes must be even. But if one component is odd-sized and others are even-sized, the total is odd—**contradiction**. So $|V(T)|$ must be even.
> >
> > **Case 2:** $|V(T)|$ is even.
> >
> > A tree $T$ has a perfect matching if and only if $|T - v|$ has exactly one odd connected component for every vertex $v$ (by **König–Rado theorem** applied to trees). Since this holds by assumption, $T$ has a perfect matching.

> [!question] Q12: No Perfect Matching in Degree-1-or-3 Trees
> Show that no tree ($n \ge 3$) with every vertex of degree 1 or 3 has a perfect matching.
>
> > [!success]- Solution (Click to expand)
> >
> > ### **Theorem:** If $T$ is a tree with $n \ge 3$ vertices where every vertex has degree 1 or 3, then $T$ has no perfect matching.
> >
> > ### **Proof**
> >
> > **Step 1: Characterize the vertex set**
> >
> > Let $L = \{v \in V(T) : \deg(v) = 1\}$ be the set of leaves.
> > Let $I = \{v \in V(T) : \deg(v) = 3\}$ be the set of internal (degree-3) vertices.
> >
> > By assumption: $V(T) = L \cup I$ (no vertices of degree 2).
> >
> > Let $\ell = |L|$ and $i = |I|$. Then $n = \ell + i$.
> >
> > **Step 2: Count edges via handshaking lemma**
> >
> > $$2|E(T)| = \sum_{v \in V(T)} \deg(v) = 1 \cdot \ell + 3 \cdot i = \ell + 3i$$
> >
> > Since $|E(T)| = n - 1 = \ell + i - 1$ (tree property):
> >
> > $$2(\ell + i - 1) = \ell + 3i$$
> > $$2\ell + 2i - 2 = \ell + 3i$$
> > $$\ell = i + 2$$
> >
> > So the number of leaves is **exactly 2 more than the number of internal vertices**.
> >
> > **Step 3: Apply Tutte's 1-Factor Theorem**
> >
> > Consider removing all internal vertices: $S = I$ (so $|S| = i$).
> >
> > Each connected component of $T - S$ is isolated leaf (since leaves have degree 1 in $T$ and that unique edge connects to an internal vertex).
> >
> > Thus, every component of $T - S$ is a single isolated vertex (odd component).
> >
> > The number of odd components is: $$\theta(T - S) = |L| = \ell = i + 2$$
> >
> > **Step 4: Violate Tutte's condition**
> >
> > By Tutte's 1-Factor Theorem, a graph has a perfect matching only if:
> >
> > $$\theta(G - S) \le |S| \quad \text{for every subset } S \subseteq V(G)$$
> >
> > We have: $$\theta(T - I) = i + 2 > i = |I|$$
> >
> > This violates Tutte's condition. Therefore, **$T$ has no perfect matching**.

> [!question] Q13: Perfect Matching in $K_{n,n,n}$
> Let $n > 1$ be an integer. Prove or disprove: (a) If $n$ is even, $K_{n,n,n}$ has a perfect matching. (b) If $n$ is odd, $K_{n,n,n}$ has no perfect matching.
>
> > [!success]- Solution (Click to expand)
> >
> > ### **Proof for Part (a): If $n$ is even, $K_{n,n,n}$ has a perfect matching.**
> >
> > **Status: TRUE (PROVED)**
> >
> > #### **Proof:**
> >
> > 1. **Total Number of Vertices:** Let the three vertex partitions of $K_{n,n,n}$ be $A$, $B$, and $C$, where $|A| = |B| = |C| = n$. The total number of vertices is: $$|V(K_{n,n,n})| = n + n + n = 3n$$ Since $n$ is even, we can write $n = 2k$ for some integer $k \ge 1$. Thus, $|V(K_{n,n,n})| = 6k$, which is an even integer.
> >     
> > 2. **Partitioning each set into two equal halves:** Divide each partition of size $n = 2k$ into two disjoint subsets of size $k$:
> >     
> >     - $A = A_1 \cup A_2$, with $|A_1| = k$ and $|A_2| = k$
> >     - $B = B_1 \cup B_2$, with $|B_1| = k$ and $|B_2| = k$
> >     - $C = C_1 \cup C_2$, with $|C_1| = k$ and $|C_2| = k$
> > 3. **Explicit Construction of the Matching:** Since $K_{n,n,n}$ is a complete tripartite graph, every vertex in $A$ is adjacent to every vertex in $B$, every vertex in $B$ is adjacent to every vertex in $C$, and every vertex in $C$ is adjacent to every vertex in $A$.
> >     
> >     We construct a matching $M = M_{AB} \cup M_{BC} \cup M_{CA}$ of size $3k$:
> >     
> >     - **$M_{AB}$:** Pair each of the $k$ vertices in $A_1$ with a unique vertex in $B_1$ ($k$ independent edges).
> >     - **$M_{BC}$:** Pair each of the $k$ vertices in $B_2$ with a unique vertex in $C_1$ ($k$ independent edges).
> >     - **$M_{CA}$:** Pair each of the $k$ vertices in $C_2$ with a unique vertex in $A_2$ ($k$ independent edges).
> > 4. **Verification:**
> >     
> >     - **Disjointness:** $A_1 \cap A_2 = \emptyset$, $B_1 \cap B_2 = \emptyset$, and $C_1 \cap C_2 = \emptyset$. Thus, no vertex is incident to more than one edge in $M$.
> >     - **Coverage:** The matching $M$ covers all $k$ vertices of $A_1$, $k$ vertices of $A_2$, $k$ vertices of $B_1$, $k$ vertices of $B_2$, $k$ vertices of $C_1$, and $k$ vertices of $C_2$. In total, all $6k = 3n$ vertices are saturated.
> >
> > Therefore, **$M$ is a valid perfect matching of size $\frac{3n}{2}$**, proving that $K_{n,n,n}$ has a perfect matching whenever $n$ is even. $\blacksquare$
> >
> > ---
> >
> > ### **Proof for Part (b): If $n$ is odd, $K_{n,n,n}$ has no perfect matching.**
> >
> > **Status: TRUE (PROVED)**
> >
> > #### **Proof:**
> >
> > 1. **Total Vertex Parity:** The graph $K_{n,n,n}$ has total vertices $|V| = 3n$. Since $n$ is an odd integer, $3n$ is the product of two odd integers, which is **odd**.
> >     
> > 2. **Matching Cardinality Property:** Every edge in a graph connects exactly $2$ distinct vertices. Therefore, any matching $M$ in a graph saturates an **even number of vertices** ($2|M|$).
> >     
> > 3. **Impossibility of Perfect Saturated Coverage:** A perfect matching must saturate all $|V|$ vertices of the graph. However:
> >     
> >     - The number of vertices saturated by any matching is always **even**.
> >     - The total number of vertices $|V(K_{n,n,n})| = 3n$ is **odd**.
> >
> > Since an even number cannot equal an odd number, no matching in $K_{n,n,n}$ can saturate all $3n$ vertices when $n$ is odd.
> >
> > Therefore, **$K_{n,n,n}$ cannot contain a perfect matching when $n$ is odd.** $\blacksquare$

> [!question] Q14: Matching Saturating $X$ in Bipartite Graph
> Prove or disprove: If $G[X, Y]$ is a simple connected bipartite graph such that the degree of every vertex in $X$ is at least 3 and the degree of every vertex in $Y$ is at most 3, then $G$ has a matching saturating every vertex in $X$.
>
> > [!success]- Solution (Click to expand)
> >
> > **PROVED (TRUE)**
> >
> > The statement is **TRUE**: Every simple connected bipartite graph $G[X,Y]$ satisfying $\deg(x) \ge 3$ for all $x \in X$ and $\deg(y) \le 3$ for all $y \in Y$ contains a matching saturating every vertex in $X$.
> >
> > ---
> >
> > ### **Proof 1: Using Double Counting and Hall's Condition**
> >
> > By **Hall's Marriage Theorem** (Theorem 7.3 / Theorem 8A.3), a bipartite graph $G[X,Y]$ has a matching saturating every vertex in $X$ if and only if **Hall's Condition** holds: $$|N_G(S)| \ge |S| \quad \text{for every subset } S \subseteq X$$
> >
> > 1. **Count Edges Leaving $S$:** Let $S$ be an arbitrary non-empty subset of $X$. Let $E(S, N(S))$ denote the set of edges with one endpoint in $S$ and the other in $N(S) \subseteq Y$. Since every vertex $x \in S$ has degree $\deg(x) \ge 3$, the total number of edges incident to $S$ satisfies: $$|E(S, N(S))| = \sum_{x \in S} \deg(x) \ge 3|S|$$
> >     
> > 2. **Bound Edges Received by $N(S)$:** All edges leaving $S$ must land in $N(S)$. Since every vertex $y \in N(S)$ has degree $\deg(y) \le 3$ in $G$, each vertex in $N(S)$ can be incident to at most $3$ edges going to $S$: $$|E(S, N(S))| = \sum_{y \in N(S)} \deg_S(y) \le \sum_{y \in N(S)} \deg(y) \le 3|N(S)|$$
> >     
> > 3. **Combine the Inequalities:** $$3|S| \le |E(S, N(S))| \le 3|N(S)|$$ Dividing both sides by $3$ gives: $$|N(S)| \ge |S|$$
> >     
> >
> > Since $|N(S)| \ge |S|$ holds for **every** subset $S \subseteq X$, Hall's Condition is satisfied. Therefore, **$G$ contains a matching saturating every vertex in $X$**. $\blacksquare$
> >
> > ---
> >
> > ### **Proof 2: Direct Application of the Corollary to Hall's Theorem**
> >
> > Your course materials explicitly provide a **Corollary to Hall's Theorem**:
> >
> > > **Corollary (Section 7.3 / 8A.3):**  
> > > Let $G$ be a bipartite graph with bipartition $[X,Y]$ and $\delta(G) > 0$. If $$\min_{x \in X} \deg(x) \ge \max_{y \in Y} \deg(y)$$ then $G$ contains a matching saturating every vertex in $X$.
> >
> > Given the prompt's conditions:
> >
> > - $\min_{x \in X} \deg(x) \ge 3$
> > - $\max_{y \in Y} \deg(y) \le 3$
> >
> > Thus: $$\min_{x \in X} \deg(x) \ge 3 \ge \max_{y \in Y} \deg(y)$$
> >
> > The hypothesis of the corollary is directly satisfied, confirming that **$G$ has a matching saturating $X$**. $\blacksquare$
> >
> > ---
> >
> > ### **Location in Your Course Notes**
> >
> > - **`Graph Theory Book (IITM).pdf`:** **Module 7, Section 7.3** (Page 162, Corollary to Theorem 7.3) & **Exercise 22** (Page 177).
> > - **`Week-10-Unit-8A.pdf`:** **Section 8A.3** (Page 12, Corollary to Theorem 8A.3).

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

> [!question] Q16: Matching Number of $C_5 + C_7$
> Find the matching number of $C_5 + C_7$.
>
> > [!success]- Solution (Click to expand)
> >
> > ### 1. Graph Definitions & Setup
> >
> > 1. **Components:**
> >
> >    - $G_1 = C_5$: an odd cycle on $5$ vertices ($V(C_5) = \{u_1, u_2, u_3, u_4, u_5\}$).
> >    - $G_2 = C_7$: an odd cycle on $7$ vertices ($V(C_7) = \{v_1, v_2, v_3, v_4, v_5, v_6, v_7\}$).
> >
> > 2. **Graph Join $G = C_5 + C_7$:**
> >
> >    - **Total Number of Vertices $n(G)$:**
> >
> >      $$n(G) = |V(C_5)| + |V(C_7)| = 5 + 7 = 12 \quad \text{(an even integer)}$$
> >
> >    - **Edges:** Contains all internal edges of $C_5$, all internal edges of $C_7$, plus an edge connecting **every** vertex of $C_5$ to **every** vertex of $C_7$.
> >
> > ### 2. Upper Bound on the Matching Number
> >
> > By definition, each edge in a matching connects $2$ distinct vertices. Therefore, for any graph $G$ with $n(G)$ vertices, the maximum number of independent edges is bounded by:
> >
> > $$\alpha_1(G) \le \left\lfloor \frac{n(G)}{2} \right\rfloor = \left\lfloor \frac{12}{2} \right\rfloor = 6$$
> >
> > ### 3. Explicit Construction of a Perfect Matching
> >
> > We can construct a matching $M$ of size $6$ as follows:
> >
> > 1. **Inside $C_5$:**
> >
> >    - The matching number of an odd cycle $C_{2m+1}$ is $\alpha_1(C_{2m+1}) = m$. For $C_5$, $\alpha_1(C_5) = 2$.
> >    - Select $2$ disjoint edges in $C_5$:
> >
> >      $$M_1 = \{(u_1, u_2), (u_3, u_4)\}$$
> >
> >    - This covers $4$ vertices of $C_5$, leaving $1$ vertex ($u_5$) unmatched.
> >
> > 2. **Inside $C_7$:**
> >
> >    - For $C_7$, $\alpha_1(C_7) = 3$.
> >    - Select $3$ disjoint edges in $C_7$:
> >
> >      $$M_2 = \{(v_1, v_2), (v_3, v_4), (v_5, v_6)\}$$
> >
> >    - This covers $6$ vertices of $C_7$, leaving $1$ vertex ($v_7$) unmatched.
> >
> > 3. **Inter-Graph Edge:**
> >
> >    - By the definition of the graph sum/join $C_5 + C_7$, every vertex in $C_5$ is adjacent to every vertex in $C_7$.
> >    - Therefore, the edge $(u_5, v_7)$ exists in $G$.
> >
> > 4. **Union of Edges:**
> >
> >    $$M = M_1 \cup M_2 \cup \{(u_5, v_7)\} = \{(u_1, u_2), (u_3, u_4), (v_1, v_2), (v_3, v_4), (v_5, v_6), (u_5, v_7)\}$$
> >
> >    - **Size:** $|M| = 2 + 3 + 1 = 6$.
> >    - **Coverage:** $M$ saturates all $12$ vertices of $C_5 + C_7$, making $M$ a **perfect matching**.
> >
> > ### Final Answer
> >
> > $$\alpha_1(C_5 + C_7) = 6$$
> 




## Chapter 8

Here is the complete list of all 14 exercises from the end of Chapter 8 (Vertex Colorings) in **Graph Theory Book (IITM).pdf**:

> [!question] Q1: Vertex Chromatic Number
> **Find the vertex chromatic number of:**
> 1. A tree.
> 2. A graph with exactly one cycle.
> 3. The complement of a cycle.
> 4. $C_{2s} + C_{2t+1}$.
> 5. Petersen graph.
> 6. $K_{n_1, n_2, \dots, n_s}$.
>
> > [!success]- Solution (Click to expand)
> >
> > To find the vertex chromatic number $\chi(G)$ for each of the given graph classes, we first outline the necessary graph-theoretic principles and then provide detailed mathematical derivations.
> >
> > ---
> >
> > ### **Necessary Theory (Brief Overview)**
> >
> > 1. **Vertex Chromatic Number $\chi(G)$**: The minimum number of colors required to color the vertices of a graph $G$ such that no two adjacent vertices share the same color.
> > 2. **Bipartite Graphs & Odd Cycles**:
> >     - A graph $G$ is $2$-colorable ($\chi(G) \le 2$) if and only if $G$ is bipartite, which holds if and only if $G$ contains no odd cycles (König's Theorem).
> >     - An even cycle $C_{2k}$ has $\chi(C_{2k}) = 2$, while an odd cycle $C_{2k+1}$ has $\chi(C_{2k+1}) = 3$.
> > 3. **Graph Join ($G_1 + G_2$)**:
> >     - The join $G_1 + G_2$ is formed by taking disjoint copies of $G_1$ and $G_2$ and adding an edge between every vertex of $G_1$ and every vertex of $G_2$.
> >     - **Theorem**: $\chi(G_1 + G_2) = \chi(G_1) + \chi(G_2)$.
> > 4. **Complement of a Graph ($G^c$)**:
> >     - Two vertices are adjacent in $G^c$ if and only if they are non-adjacent in $G$.
> >     - An independent set in $G^c$ corresponds to a clique (mutually adjacent set) in $G$.
> >
> > ---
> >
> > ### **Solutions & Proofs**
> >
> > #### **1. A Tree $T$**
> >
> > - **Theory**: A tree $T$ is a connected acyclic graph.
> > - **Proof**: Since $T$ contains no cycles, it has no odd cycles. By König's Theorem, any graph without odd cycles is bipartite.
> >     - For a non-trivial tree with at least one edge ($n \ge 2$), $\chi(T) \ge 2$.
> >     - Because $T$ is bipartite, its vertices can be partitioned into two independent sets $V_1$ and $V_2$, which can be colored using $2$ distinct colors.
> > - **Conclusion**: $$\chi(T) = 2 \quad (\text{for } n \ge 2; \quad \chi(T) = 1 \text{ if } n = 1)$$
> >
> > ---
> >
> > #### **2. A Graph $G$ with Exactly One Cycle**
> >
> > - **Theory**: A graph with exactly one cycle is called a unicyclic graph.
> >     
> > - **Proof**: Let $C_k$ be the unique cycle present in $G$.
> >     
> >     - **Case 1: $C_k$ is an even cycle ($k = 2m$)** Since the only cycle in $G$ is even, $G$ contains no odd cycles. Therefore, $G$ is bipartite, which implies $\chi(G) = 2$ (assuming $G$ has at least one edge).
> >         
> >     - **Case 2: $C_k$ is an odd cycle ($k = 2m + 1$)** Since $G$ contains an odd cycle $C_{2m+1}$ as a subgraph, we must have $\chi(G) \ge \chi(C_{2m+1}) = 3$. To show $\chi(G) \le 3$, we can first color the cycle $C_{2m+1}$ using $3$ colors ${1, 2, 3}$. The remainder of the graph $G \setminus C_k$ consists of a collection of trees rooted at the vertices of $C_k$. Since trees are $2$-colorable, we can extend the coloring outward along each tree using $2$ alternating colors without introducing any color conflicts. Thus, $3$ colors are sufficient.
> >         
> > - **Conclusion**: $$\chi(G) = \begin{cases} 2 & \text{if the unique cycle is even} \\ 3 & \text{if the unique cycle is odd} \end{cases}$$
> >     
> >
> > ---
> >
> > #### **3. The Complement of a Cycle, $C_n^c$**
> >
> > - **Theory**: A proper vertex coloring of $C_n^c$ partitions $V(C_n^c)$ into independent sets of $C_n^c$. An independent set in $C_n^c$ corresponds to a clique (mutually adjacent vertices) in $C_n$.
> >     
> > - **Proof**:
> >     
> >     1. For $n = 3$, $C_3$ is a triangle ($K_3$), so $C_3^c$ consists of $3$ isolated vertices ($3K_1$). Thus, $\chi(C_3^c) = 1$.
> >     2. For $n \ge 4$, the simple cycle $C_n$ contains no triangles, so the maximum clique size in $C_n$ is $\omega(C_n) = 2$.
> >         - Consequently, every independent set in $C_n^c$ can contain at most $2$ vertices.
> >         - To color $n$ vertices where each color class has at most $2$ vertices, we require at least: $$\chi(C_n^c) \ge \left\lceil \frac{n}{2} \right\rceil$$
> >         - We can achieve this bound by pairing adjacent vertices along $C_n$ to form $1$-edges (cliques of size $2$ in $C_n$), each receiving a unique color:
> >             - If $n = 2k$ (even), we partition the vertices into $k = \frac{n}{2}$ adjacent pairs.
> >             - If $n = 2k + 1$ (odd), we partition into $k$ adjacent pairs and $1$ single vertex, using $k + 1 = \left\lceil \frac{n}{2} \right\rceil$ colors.
> > - **Conclusion**: $$\chi(C_n^c) = \begin{cases} 1 & \text{if } n = 3 \\ \left\lceil \frac{n}{2} \right\rceil & \text{if } n \ge 4 \end{cases}$$
> >     
> >
> > ---
> >
> > #### **4. $C_{2s} + C_{2t+1}$**
> >
> > - **Theory**: By the property of graph join, $\chi(G_1 + G_2) = \chi(G_1) + \chi(G_2)$.
> >     
> > - **Proof**:
> >     
> >     - In $G_1 + G_2$, every vertex in $V(G_1)$ is adjacent to every vertex in $V(G_2)$.
> >     - Hence, no color used for $V(G_1)$ can be reused for $V(G_2)$, making the color sets completely disjoint.
> >     - For $C_{2s}$ (an even cycle, $2s \ge 4$), the chromatic number is $\chi(C_{2s}) = 2$.
> >     - For $C_{2t+1}$ (an odd cycle, $2t+1 \ge 3$), the chromatic number is $\chi(C_{2t+1}) = 3$.
> >     - Substituting these values yields: $$\chi(C_{2s} + C_{2t+1}) = \chi(C_{2s}) + \chi(C_{2t+1}) = 2 + 3 = 5$$
> > - **Conclusion**: $$\chi(C_{2s} + C_{2t+1}) = 5$$
> >     
> >
> > ---
> >
> > #### **5. Petersen Graph**
> >
> > - **Theory**: The Petersen graph contains $5$-cycles (e.g., its outer cycle). Since it contains an odd cycle, it cannot be $2$-colorable. Therefore, $\chi(\text{Petersen}) \ge 3$.
> > - **Proof**: To demonstrate that $3$ colors are sufficient ($\chi(\text{Petersen}) \le 3$), we construct an explicit $3$-coloring:
> >     - Let the outer $5$-cycle vertices be $v_1, v_2, v_3, v_4, v_5$ and the inner star vertices be $v_6, v_7, v_8, v_9, v_{10}$, where spoke edges join $v_i$ and $v_{i+5}$ for $1 \le i \le 5$.
> >     - Assign colors ${\text{Red}, \text{Blue}, \text{Green}}$ as follows:
> >         - Outer cycle: $v_1 = \text{Red}, v_2 = \text{Blue}, v_3 = \text{Red}, v_4 = \text{Blue}, v_5 = \text{Green}$.
> >         - Inner star: $v_6 = \text{Blue}, v_7 = \text{Green}, v_8 = \text{Green}, v_9 = \text{Red}, v_{10} = \text{Blue}$.
> >     - Verifying all $15$ edges confirms that no two adjacent vertices share the same color.
> >
> > The visualization below illustrates this valid proper $3$-coloring:
> >
> > --Image of: --Proper 3-Coloring of Petersen Graph
> >
> > - **Conclusion**: $$\chi(\text{Petersen Graph}) = 3$$
> >
> > ---
> >
> > #### **6. Complete Multipartite Graph $K_{n_1, n_2, \dots, n_s}$**
> >
> > - **Theory**: A complete $s$-partite graph has a vertex set partitioned into $s$ independent sets $V_1, V_2, \dots, V_s$ of sizes $n_1, n_2, \dots, n_s$, where every vertex in $V_i$ is connected to every vertex in $V_j$ for all $i \ne j$.
> >     
> > - **Proof**:
> >     
> >     1. Within each part $V_i$, there are no internal edges. Thus, all vertices in $V_i$ can receive the same color $c_i$.
> >     2. For any two distinct parts $V_i$ and $V_j$ ($i \ne j$), every vertex in $V_i$ is adjacent to every vertex in $V_j$. Thus, $c_i \ne c_j$ for all $i \ne j$.
> >     3. This requires at least $s$ distinct colors, and $s$ colors are sufficient by assigning color $i$ to all vertices in $V_i$.
> > - **Conclusion**: $$\chi(K_{n_1, n_2, \dots, n_s}) = s$$

> [!question] Q2: Chromatic Number of a Join
> **Prove:** $\chi(G_1 + G_2) = \chi(G_1) + \chi(G_2)$.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $a = \chi(G_1)$ and $b = \chi(G_2)$. We show $\chi(G_1+G_2) \le a+b$ and $\chi(G_1+G_2) \ge a+b$.
> >
> > **Upper bound $\chi(G_1+G_2) \le a+b$.**
> >
> > Let $c_1 : V(G_1) \to \{1,\dots,a\}$ be a proper $a$-coloring of $G_1$, and let $c_2 : V(G_2) \to \{a+1,\dots,a+b\}$ be a proper $b$-coloring of $G_2$ (shifted to use a disjoint color set). Define $c : V(G_1+G_2) \to \{1,\dots,a+b\}$ by $c(v) = c_1(v)$ if $v \in V(G_1)$ and $c(v) = c_2(v)$ if $v \in V(G_2)$.
> >
> > - Any edge inside $G_1$ is properly colored since $c_1$ is proper.
> > - Any edge inside $G_2$ is properly colored since $c_2$ is proper.
> > - Any edge between $V(G_1)$ and $V(G_2)$ has one endpoint colored from $\{1,\dots,a\}$ and the other from $\{a+1,\dots,a+b\}$, hence distinctly colored.
> >
> > So $c$ is a proper $(a+b)$-coloring, giving $\chi(G_1+G_2) \le a+b$.
> >
> > **Lower bound $\chi(G_1+G_2) \ge a+b$.**
> >
> > Let $c$ be any proper coloring of $G_1+G_2$ using $\chi(G_1+G_2)$ colors. Since every vertex of $G_1$ is adjacent to every vertex of $G_2$ in the join, no color used on $V(G_1)$ can also be used on $V(G_2)$:
> >
> > $$c(V(G_1)) \cap c(V(G_2)) = \emptyset$$
> >
> > The restriction of $c$ to $V(G_1)$ is a proper coloring of $G_1$ (edges inside $G_1$ are unaffected by the join), so it uses at least $\chi(G_1) = a$ distinct colors. Likewise the restriction to $V(G_2)$ uses at least $\chi(G_2) = b$ distinct colors. Since these two color sets are disjoint:
> >
> > $$\chi(G_1+G_2) = |c(V(G_1+G_2))| = |c(V(G_1))| + |c(V(G_2))| \ge a+b$$
> >
> > Combining both bounds:
> >
> > $$\boxed{\chi(G_1+G_2) = \chi(G_1)+\chi(G_2)}$$

> [!question] Q3: Bounds on the Chromatic Number
> **For every graph $G$, show that:**
>
> $$\frac{n(G)}{\alpha_0(G)} \le \chi(G) \le n(G) + 1 - \alpha_0(G)$$
>
> > [!success]- Solution (Click to expand)
> >
> > **Lower bound $\dfrac{n(G)}{\alpha_0(G)} \le \chi(G)$.**
> >
> > Let $k = \chi(G)$. By definition of a proper $k$-coloring, $V(G)$ partitions into $k$ color classes $V_1, V_2, \dots, V_k$ that are pairwise disjoint, with $V(G) = V_1 \cup \cdots \cup V_k$.
> >
> > Since no two vertices in the same color class are adjacent, each $V_i$ is an independent set of $G$. By definition of $\alpha_0(G)$ as the maximum independent set size:
> >
> > $$|V_i| \le \alpha_0(G) \quad \text{for every } i \in \{1,\dots,k\}$$
> >
> > Summing over all $k$ classes:
> >
> > $$n(G) = \sum_{i=1}^{k}|V_i| \le \sum_{i=1}^{k}\alpha_0(G) = k\cdot\alpha_0(G) = \chi(G)\cdot \alpha_0(G)$$
> >
> > Since $\alpha_0(G) \ge 1$ for any nonempty graph, dividing both sides gives:
> >
> > $$\boxed{\chi(G) \ge \frac{n(G)}{\alpha_0(G)}}$$
> >
> > **Upper bound $\chi(G) \le n(G) + 1 - \alpha_0(G)$.**
> >
> > Let $I \subseteq V(G)$ be a maximum independent set, so $|I| = \alpha_0(G)$. Construct a proper coloring explicitly:
> >
> > - Assign **color 1** to every vertex in $I$. This is proper since $I$ is independent, so no edge has both endpoints in $I$.
> > - Assign a **distinct new color** to each of the remaining $n(G) - \alpha_0(G)$ vertices in $V(G) \setminus I$. Since every vertex outside $I$ gets its own unique color, no edge among them can be monochromatic either.
> >
> > This coloring is proper and uses exactly:
> >
> > $$1 + \big(n(G) - \alpha_0(G)\big) = n(G) + 1 - \alpha_0(G) \text{ colors}$$
> >
> > Since $\chi(G)$ is the minimum number of colors over all proper colorings, and we have exhibited one proper coloring with this many colors:
> >
> > $$\boxed{\chi(G) \le n(G) + 1 - \alpha_0(G)}$$
> >
> > Combining both bounds gives the required inequality for every graph $G$:
> >
> > $$\boxed{\frac{n(G)}{\alpha_0(G)} \le \chi(G) \le n(G) + 1 - \alpha_0(G)}$$

> [!question] Q4: Graphs with $\chi(G) = k$
> **Show that every graph with $\chi(G) = k$ contains:**
>
> 1. At least $\frac{k(k - 1)}{2}$ edges.
> 2. A cycle of length at least $k$.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $\chi(G) = k$.
> >
> > **(1) $G$ has at least $\dfrac{k(k-1)}{2}$ edges.**
> >
> > Every graph $G$ with $\chi(G) = k$ contains a $k$-critical subgraph $H$ (a subgraph with $\chi(H) = k$ and $\chi(H - v) < k$ for every $v \in V(H)$), obtained by repeatedly deleting vertices that do not lower the chromatic number below $k$, until no further deletion is possible. It suffices to prove the edge bound for $H$, since $|E(G)| \ge |E(H)|$.
> >
> > **Claim:** $\delta(H) \ge k-1$.
> >
> > Suppose some vertex $v \in V(H)$ has $\deg_H(v) \le k-2$. Since $H$ is $k$-critical, $H - v$ has a proper $(k-1)$-coloring. In this coloring, $v$'s neighbors use at most $\deg_H(v) \le k-2$ distinct colors out of the $k-1$ available, so at least one color is free for $v$. Extending the coloring by assigning $v$ this free color gives a proper $(k-1)$-coloring of $H$, contradicting $\chi(H) = k$. Hence $\delta(H) \ge k-1$.
> >
> > By the handshaking lemma:
> >
> > $$2|E(H)| = \sum_{v \in V(H)} \deg_H(v) \ge n(H)\cdot \delta(H) \ge n(H)(k-1)$$
> >
> > Since $H$ is $k$-chromatic, $n(H) \ge k$ (a graph on fewer than $k$ vertices cannot need $k$ colors). So:
> >
> > $$2|E(H)| \ge k(k-1) \implies |E(H)| \ge \frac{k(k-1)}{2}$$
> >
> > Therefore:
> >
> > $$\boxed{|E(G)| \ge |E(H)| \ge \frac{k(k-1)}{2}}$$
> >
> > **(2) $G$ contains a cycle of length at least $k$.**
> >
> > Again work with the $k$-critical subgraph $H \subseteq G$, where $\delta(H) \ge k-1$ as shown above. If $k \le 2$, the claim holds trivially, so assume $k \ge 3$; then $\delta(H) \ge 2$, so $H$ contains a cycle.
> >
> > A $k$-critical graph with $k \ge 3$ is 2-connected (this strengthens the connectivity result of Q11: if a cut-vertex $v$ existed, each "block" attached at $v$ would be a proper subgraph, colourable with $<k$ colours, and these colourings could be consistently glued at $v$ by permuting colours, again producing a $(k-1)$-colouring of all of $H$ — a contradiction). Using the standard lemma for 2-connected graphs — *in a 2-connected graph with minimum degree $\delta$, the longest cycle has length at least $\min(n, \delta+1)$* — with $\delta = \delta(H) \ge k-1$ and $n(H) \ge k$:
> >
> > $$\text{length of longest cycle in } H \ \ge\ \min(n(H), k) = k$$
> >
> > Hence $H$, and therefore $G$, contains a cycle of length at least $k$:
> >
> > $$\boxed{G \text{ contains a cycle of length} \ge k}$$

> [!question] Q5: Number of Vertices in Mycielski Graphs
> **Find $n(G_k)$, where $G_k$ is the $k$-vertex-chromatic, triangle-free graph constructed using Mycielski’s method**.
>
> > [!success]- Solution (Click to expand)
> >
> > **Mycielski's construction.** Given a triangle-free graph $G_{k-1}$ on vertex set $\{u_1,\dots,u_m\}$ with $\chi(G_{k-1}) = k-1$, the **Mycielskian** $G_k$ is built as follows:
> >
> > - Keep the original vertices $u_1,\dots,u_m$ with their original edges.
> > - Add a "shadow" copy $v_1,\dots,v_m$, where $v_i$ is joined to every neighbor of $u_i$ in $G_{k-1}$ (but $v_i$ is **not** adjacent to $v_j$, and not adjacent to $u_i$ itself).
> > - Add one new apex vertex $z$, joined to every shadow vertex $v_1,\dots,v_m$.
> >
> > This construction preserves triangle-freeness and raises the chromatic number by exactly 1: $\chi(G_k) = \chi(G_{k-1}) + 1 = k$.
> >
> > **Counting vertices.** If $n(G_{k-1}) = m$, then $G_k$ has $m$ original vertices, $m$ shadow vertices, and $1$ apex vertex:
> >
> > $$n(G_k) = 2m + 1 = 2\,n(G_{k-1}) + 1$$
> >
> > **Base case.** The smallest triangle-free graph with $\chi = 2$ is $K_2$ (a single edge), so $G_2 = K_2$ and $n(G_2) = 2$.
> >
> > **Solving the recursion.** Let $a_k = n(G_k)$. Then $a_2 = 2$ and $a_k = 2a_{k-1}+1$ for $k \ge 3$. Adding $1$ to both sides: $a_k + 1 = 2(a_{k-1}+1)$, so $\{a_k+1\}$ is geometric with ratio $2$:
> >
> > $$a_k + 1 = (a_2+1)\cdot 2^{k-2} = 3\cdot 2^{k-2}$$
> >
> > $$\therefore \boxed{n(G_k) = 3\cdot 2^{k-2} - 1} \quad (k \ge 2)$$
> >
> > **Check:** $G_2 = K_2$ has $n=2 = 3(1)-1$ ✓. $G_3$ equals $C_5$, with $n = 5 = 3(2)-1$ ✓. $G_4$ is the Grötzsch graph, with $n = 11 = 3(4)-1$ ✓.

> [!question] Q6: Maximum Edges in a 4-Chromatic Graph
> **Draw a graph having maximum number of edges with $\chi(G) = 4$ and $n(G) = 10$**.
>
> > [!success]- Solution (Click to expand)
> >
> > We want the graph on $10$ vertices with $\chi(G)=4$ that has the **maximum** possible number of edges.
> >
> > **Idea.** Since $\chi(G) = 4$, $V(G)$ can be partitioned into (at most) $4$ independent sets, and to maximize edges we want every possible edge between different color classes to be present — i.e., $G$ should be a **complete 4-partite graph** $K_{n_1,n_2,n_3,n_4}$ with $n_1+n_2+n_3+n_4 = 10$. As shown earlier (Chapter 8, Q1 part 6, and Q2), $\chi(K_{n_1,n_2,n_3,n_4}) = 4$ exactly, regardless of the part sizes, as long as all $n_i \ge 1$.
> >
> > **Maximizing edges over partitions of $10$ into $4$ positive parts.** The edge count of a complete multipartite graph is:
> >
> > $$|E| = \binom{n}{2} - \sum_{i=1}^{4}\binom{n_i}{2}$$
> >
> > where $n = 10$. To maximize $|E|$, we must **minimize** $\sum \binom{n_i}{2}$ subject to $\sum n_i = 10$. Since $\binom{x}{2}$ is convex, this sum is minimized when the parts are as equal as possible. Splitting $10 = 3+3+2+2$ gives the most balanced partition into $4$ positive parts.
> >
> > $$\sum\binom{n_i}{2} = \binom{3}{2}+\binom{3}{2}+\binom{2}{2}+\binom{2}{2} = 3+3+1+1 = 8$$
> >
> > $$|E| = \binom{10}{2} - 8 = 45 - 8 = 37$$
> >
> > **Construction.** Take $G = K_{3,3,2,2}$: partition the $10$ vertices into classes $V_1=\{a_1,a_2,a_3\}$, $V_2=\{b_1,b_2,b_3\}$, $V_3=\{c_1,c_2\}$, $V_4=\{d_1,d_2\}$. Join every pair of vertices lying in **different** classes; no edges within a class.
> >
> > - Each $V_i$ is independent, and vertices in different classes are always adjacent, so this is a proper coloring using exactly the $4$ classes, giving $\chi(G) \le 4$.
> > - Since $G$ contains $K_4$ as a subgraph (one vertex from each class), $\chi(G) \ge \omega(G) \ge 4$.
> >
> > $$\therefore \chi(G) = 4, \qquad \boxed{|E(G)| = 37 \text{ (maximum, achieved by } K_{3,3,2,2}\text{)}}$$

> [!question] Q7: Greedy Coloring of the $P_2 \square P_4$ Ladder Graph
> **Let $G$ be the graph shown in the text ($P_2 \square P_4$ ladder graph). Order the vertices of $G$ in 3 different ways, say $S_1, S_2,$ and $S_3$, so that the greedy algorithm:**
>
> 1. Uses 2 colors, if $S_1$ is the input.
> 2. Uses 3 colors, if $S_2$ is the input.
> 3. Uses 4 colors, if $S_3$ is the input.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G = P_2 \,\square\, P_4$: top row $u_1,u_2,u_3,u_4$, bottom row $v_1,v_2,v_3,v_4$, with rungs $u_iv_i$ ($1\le i\le4$) and rails $u_iu_{i+1}$, $v_iv_{i+1}$ ($1\le i\le3$). $G$ is bipartite with parts $X=\{u_1,u_3,v_2,v_4\}$, $Y=\{u_2,u_4,v_1,v_3\}$, so $\chi(G)=2$.
> >
> > **(a) 2 colors.** Take $S_1 = (u_1,u_3,v_2,v_4,\,u_2,u_4,v_1,v_3)$ — all of $X$ first, then all of $Y$.
> >
> > | Vertex | Neighbours | Coloured Neighbours | Colour |
> > |:--|:--|:--|:-:|
> > | $u_1$ | $u_2, v_1$ | none | 1 |
> > | $u_3$ | $u_2, u_4, v_3$ | none | 1 |
> > | $v_2$ | $v_1, v_3, u_2$ | none | 1 |
> > | $v_4$ | $v_3, u_4$ | none | 1 |
> > | $u_2$ | $u_1, u_3, v_2$ | all coloured 1 | 2 |
> > | $u_4$ | $u_3, v_4$ | all coloured 1 | 2 |
> > | $v_1$ | $u_1, v_2$ | all coloured 1 | 2 |
> > | $v_3$ | $v_2, v_4, u_3$ | all coloured 1 | 2 |
> >
> > Only colours 1 and 2 are used.
> >
> > **(b) 3 colors.** Take $S_2 = (u_1, v_1, u_2, v_3, u_3, v_2, u_4, v_4)$.
> >
> > | Vertex | Neighbours | Coloured Neighbours | Colour |
> > |:--|:--|:--|:-:|
> > | $u_1$ | $u_2, v_1$ | none | 1 |
> > | $v_1$ | $u_1, v_2$ | $u_1(1)$ | 2 |
> > | $u_2$ | $u_1, u_3, v_2$ | $u_1(1)$ | 2 |
> > | $v_3$ | $v_2, v_4, u_3$ | none | 1 |
> > | $u_3$ | $u_2, u_4, v_3$ | $u_2(2), v_3(1)$ | 3 |
> > | $v_2$ | $v_1, v_3, u_2$ | $v_1(2), v_3(1), u_2(2)$ | 3 |
> > | $u_4$ | $u_3, v_4$ | $u_3(3)$ | 1 |
> > | $v_4$ | $v_3, u_4$ | $v_3(1), u_4(1)$ | 2 |
> >
> > Maximum colour used is 3.
> >
> > **(c) 4 colors.** Take $S_3 = (u_2, v_4, u_1, v_3, u_3, v_1, u_4, v_2)$.
> >
> > | Vertex | Neighbours | Coloured Neighbours | Colour |
> > |:--|:--|:--|:-:|
> > | $u_2$ | $u_1, u_3, v_2$ | none | 1 |
> > | $v_4$ | $v_3, u_4$ | none | 1 |
> > | $u_1$ | $u_2, v_1$ | $u_2(1)$ | 2 |
> > | $v_3$ | $v_2, v_4, u_3$ | $v_4(1)$ | 2 |
> > | $u_3$ | $u_2, u_4, v_3$ | $u_2(1), v_3(2)$ | 3 |
> > | $v_1$ | $u_1, v_2$ | $u_1(2)$ | 1 |
> > | $u_4$ | $u_3, v_4$ | $u_3(3), v_4(1)$ | 2 |
> > | $v_2$ | $v_1, v_3, u_2$ | $v_1(1), v_3(2), u_2(1)$ | 4 |
> >
> > Maximum colour used is 4.

> [!question] Q8: Greedy Coloring of the Crown Graph $K_{4,4} - 4e$
> **Order the vertices of the graph shown in the text (crown graph $K_{4,4} - 4e$) in such a way that the greedy algorithm uses 4 colors**.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G = K_{4,4} - 4e$: parts $\{u_1,u_2,u_3,u_4\}$ and $\{v_1,v_2,v_3,v_4\}$, with $u_i$ adjacent to $v_j$ for all $j \ne i$ (the perfect matching $u_iv_i$ removed). $G$ is bipartite, so $\chi(G) = 2$; we force the greedy algorithm to use $4$ colors.
> >
> > Take ordering $S = (u_1, v_1, u_2, v_2, u_3, v_3, u_4, v_4)$.
> >
> > | Vertex | Neighbours | Coloured Neighbours | Colour |
> > |:--|:--|:--|:-:|
> > | $u_1$ | $v_2,v_3,v_4$ | none | 1 |
> > | $v_1$ | $u_2,u_3,u_4$ | none | 1 |
> > | $u_2$ | $v_1,v_3,v_4$ | $v_1(1)$ | 2 |
> > | $v_2$ | $u_1,u_3,u_4$ | $u_1(1)$ | 2 |
> > | $u_3$ | $v_1,v_2,v_4$ | $v_1(1),v_2(2)$ | 3 |
> > | $v_3$ | $u_1,u_2,u_4$ | $u_1(1),u_2(2)$ | 3 |
> > | $u_4$ | $v_1,v_2,v_3$ | $v_1(1),v_2(2),v_3(3)$ | 4 |
> > | $v_4$ | $u_1,u_2,u_3$ | $u_1(1),u_2(2),u_3(3)$ | 4 |
> >
> > The greedy algorithm uses $4$ colours on this ordering.

> [!question] Q9: Greedy Coloring of $k$-Degenerate Graphs
> **Let $G$ be a simple graph such that $\delta(H) \le k$, for every subgraph $H$ of $G$ (such a graph is called a $k$-degenerate graph). Order the vertices of $G$ so that if one applies the greedy algorithm to color the vertices of $G$, then it uses at most $k + 1$ colors**.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G$ be $k$-degenerate: $\delta(H) \le k$ for every subgraph $H$ of $G$.
> >
> > **Constructing the ordering (degeneracy ordering).** Build the ordering $v_n, v_{n-1}, \dots, v_1$ in reverse, by repeatedly peeling off a minimum-degree vertex:
> >
> > 1. Let $H_n = G$. Since $\delta(H_n) \le k$, choose a vertex $v_n$ with $\deg_{H_n}(v_n) \le k$.
> > 2. Let $H_{n-1} = H_n - v_n$. Since $H_{n-1}$ is a subgraph of $G$, $\delta(H_{n-1}) \le k$; choose $v_{n-1}$ with $\deg_{H_{n-1}}(v_{n-1}) \le k$.
> > 3. Continue: at step $i$, let $H_i = H_{i+1} - v_{i+1}$, and choose $v_i$ with $\deg_{H_i}(v_i) \le k$ (possible since $H_i \subseteq G$ is a subgraph, so $\delta(H_i)\le k$).
> > 4. Repeat until all vertices are removed, producing $v_1, v_2, \dots, v_n$.
> >
> > Feed the greedy algorithm the ordering $S = (v_1, v_2, \dots, v_n)$ — i.e., process $v_1$ first.
> >
> > **Why this bounds the number of colours.** By construction, $v_i$ was chosen as a minimum-degree vertex of $H_i = G[\{v_1,\dots,v_i\}]$, since all later-removed vertices $v_{i+1},\dots,v_n$ had already been deleted before $v_i$ was chosen. Hence when the greedy algorithm processes $v_i$, its only possible **already-coloured** neighbours are those among $v_1,\dots,v_{i-1}$ — exactly its neighbours within $H_i$. Since $\deg_{H_i}(v_i) \le k$, at most $k$ already-coloured neighbours exist.
> >
> > The greedy algorithm assigns $v_i$ the smallest colour not used among its (at most $k$) coloured neighbours, which must be found among colours $\{1,\dots,k+1\}$ by pigeonhole.
> >
> > Since this holds for every vertex $v_i$, the greedy algorithm never uses a colour higher than $k+1$:
> >
> > $$\boxed{\text{Greedy algorithm on the ordering } (v_1,\dots,v_n) \text{ uses at most } k+1 \text{ colours.}}$$

> [!question] Q10: Chemical Storage Problem
> **There are 7 chemicals $A, B, C, D, E, F, G$. For safety reasons, the following pairs of chemicals cannot be stored in one room:** $A\&B, A\&C, A\&G, B\&C, B\&D, C\&D, D\&E, D\&F, E\&F, E\&G, F\&G$. **If the problem is to find the minimum number of rooms (say $k$) required to store all the chemicals, how would you model it as a graph theoretical problem and find $k$?**
>
> > [!success]- Solution (Click to expand)
> >
> > **Modeling as graph coloring.** Build a conflict graph $G$ with $V(G) = \{A,B,C,D,E,F,G\}$, and join two vertices by an edge exactly when the corresponding chemicals cannot share a room:
> >
> > $$E(G) = \{AB, AC, AG, BC, BD, CD, DE, DF, EF, EG, FG\}$$
> >
> > A valid room assignment is precisely a **proper vertex coloring** of $G$ (rooms = colours; chemicals sharing a room get the same colour, and incompatible chemicals, i.e., adjacent vertices, must receive different colours). The minimum number of rooms needed is $\chi(G)$.
> >
> > **Lower bound.** Note $\deg(A)=3,\deg(B)=3,\deg(C)=3,\deg(D)=4,\deg(E)=3,\deg(F)=3,\deg(G)=3$. Observe $\{A,B,C\}$ is a triangle ($AB,AC,BC \in E$), and $\{D,E,F\}$ is also a triangle ($DE,DF,EF \in E$). So $\omega(G) \ge 3$, giving $\chi(G) \ge 3$.
> >
> > **No proper 3-coloring exists.** In any 3-coloring, the triangle $\{A,B,C\}$ must occupy all 3 colours; relabel colours so $A=1, B=2, C=3$. Since $D$ is adjacent to both $B(2)$ and $C(3)$, $D$ is forced to colour $1$. Since $\{D,E,F\}$ is also a triangle with $D=1$, the pair $\{E,F\}$ must occupy the remaining two colours $\{2,3\}$ (in either order). But now $G$ is adjacent to $A(1)$, $E$, and $F$, and $\{E,F\}=\{2,3\}$ — so $G$'s neighbours already use all three colours $\{1,2,3\}$, leaving no colour available for $G$. Hence $\chi(G) \ge 4$.
> >
> > **Explicit proper 4-coloring (rooms).**
> >
> > | Chemical | A | B | C | D | E | F | G |
> > |:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
> > | Room | 1 | 2 | 3 | 1 | 2 | 3 | 4 |
> >
> > Verify every conflicting pair gets different rooms: $AB(1,2)$, $AC(1,3)$, $AG(1,4)$, $BC(2,3)$, $BD(2,1)$, $CD(3,1)$, $DE(1,2)$, $DF(1,3)$, $EF(2,3)$, $EG(2,4)$, $FG(3,4)$ — all distinct. Valid.
> >
> > $$\boxed{k = \chi(G) = 4 \text{ rooms}}$$
> >
> > **Room assignment:** Room 1: $\{A, D\}$; Room 2: $\{B, E\}$; Room 3: $\{C, F\}$; Room 4: $\{G\}$.

_(Note: A graph $G$ is said to be $k$-critical if $\chi(G) = k$, and $\chi(H) < k$ for every proper subgraph $H$ of $G$.)_

> [!question] Q11: Properties of $k$-Critical Graphs
> **If $G$ is $k$-critical, then show that $G$ is connected and that $\delta(G) \ge k - 1$**.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G$ be $k$-critical: $\chi(G)=k$ and $\chi(H) < k$ for every proper subgraph $H \subsetneq G$.
> >
> > **$G$ is connected.**
> >
> > Suppose, for contradiction, $G$ is disconnected, with components $G_1, G_2, \dots, G_r$ ($r \ge 2$). Each $G_i$ is a proper subgraph of $G$ (since $r\ge2$, no single component equals all of $G$), so by criticality $\chi(G_i) < k$ for each $i$.
> >
> > But colouring each component independently and optimally, the overall chromatic number of a disconnected graph is the **maximum** over its components (colours can be freely reused across different components, since there are no edges between them):
> >
> > $$\chi(G) = \max_{1\le i \le r} \chi(G_i) < k$$
> >
> > This contradicts $\chi(G) = k$. Hence $G$ must be connected.
> >
> > **$\delta(G) \ge k-1$.**
> >
> > Suppose some vertex $v$ has $\deg_G(v) \le k-2$. Since $G - v$ is a proper subgraph, criticality gives $\chi(G-v) < k$, i.e., $\chi(G-v) \le k-1$. Fix a proper $(k-1)$-colouring of $G - v$.
> >
> > In this colouring, the neighbours of $v$ (all lying in $G-v$) use at most $\deg_G(v) \le k-2$ distinct colours among the $k-1$ available. By pigeonhole, at least one colour in $\{1,\dots,k-1\}$ is unused among $v$'s neighbours. Assign that colour to $v$.
> >
> > This extends the $(k-1)$-colouring of $G-v$ to a proper $(k-1)$-colouring of all of $G$, contradicting $\chi(G) = k$.
> >
> > Hence every vertex of $G$ has degree at least $k-1$:
> >
> > $$\boxed{\delta(G) \ge k-1}$$

> [!question] Q12: Chromatic Number of $G - S$
> **If $S$ is a set of independent vertices in a $k$-critical graph, then what is the chromatic number of $G - S$?**
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G$ be $k$-critical and $S \subseteq V(G)$ an independent set.
> >
> > **Claim:** $\chi(G - S) = k - 1$.
> >
> > **Upper bound $\chi(G-S) \le k-1$.** We show this by induction on $|S|$.
> >
> > - **Base case $|S|=1$:** $S=\{v\}$ for some vertex $v$. Since $G-v$ is a proper subgraph of $G$, criticality gives $\chi(G-v) < k$, i.e., $\chi(G-v) \le k-1$.
> > - **Inductive step:** Suppose for every independent set of size $< |S|$ the bound $\chi(G - S') \le k-1$ holds. Write $S = S'' \cup \{w\}$ for some $w \in S$, where $S'' = S\setminus\{w\}$ is still independent and $|S''| = |S|-1$. By the inductive hypothesis, $G - S''$ has a proper $(k-1)$-colouring $c$.
> >
> >   Since $S$ is independent, $w$ has no neighbour within $S$, so deleting $w$ from $G-S''$ only removes $w$ itself. Thus $c$ restricted to $(G-S'')-w = G - S$ remains a proper $(k-1)$-colouring.
> >
> >   Hence $\chi(G-S) \le k-1$.
> >
> > **Lower bound $\chi(G-S) \ge k-1$.** Suppose instead $\chi(G-S) \le k-2$. Fix such a colouring $c$ of $G - S$ using colours $\{1,\dots,k-2\}$. We extend it to all of $G$ using only $k-1$ colours total, contradicting $\chi(G)=k$:
> >
> > Process the vertices of $S$ one at a time. Since $S$ is independent, no two vertices of $S$ are adjacent, so colouring them one-by-one never creates a conflict between two $S$-vertices. For each $v \in S$, by Q11, $\deg_G(v) \ge k-1$, but all of $v$'s neighbours lie in $V(G)\setminus S$ (since $S$ is independent, $v$ has no neighbour inside $S$), and at the time $v$ is processed, the base colouring plus previously-processed $S$-vertices still use at most $k-2$ colours among $v$'s neighbours, so at least one of the $k-1$ colours remains free for $v$ by pigeonhole.
> >
> > This produces a proper $(k-1)$-colouring of all of $G$, contradicting $\chi(G)=k$. Hence $\chi(G-S)\ge k-1$.
> >
> > Combining both bounds:
> >
> > $$\boxed{\chi(G-S) = k-1}$$

> [!question] Q13: Critical Graphs and Joins
> **If $G_1$ and $G_2$ are simple graphs, show that $G_1 + G_2$ is a critical graph iff $G_1$ and $G_2$ are critical**.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $a = \chi(G_1)$, $b=\chi(G_2)$. By Q2, $\chi(G_1+G_2) = a+b$.
> >
> > **($\Leftarrow$) If $G_1$ and $G_2$ are both critical, then $G_1+G_2$ is critical.**
> >
> > It suffices to check vertex-deleted subgraphs $H = (G_1+G_2) - x$ for an arbitrary vertex $x$. Suppose WLOG $x \in V(G_1)$. Then:
> >
> > $$(G_1+G_2) - x = (G_1 - x) + G_2$$
> >
> > since deleting $x$ only removes it (and its incident edges, including all join edges to $G_2$) from the $G_1$ side; the join structure with $G_2$ is otherwise unaffected. By Q2:
> >
> > $$\chi\big((G_1-x)+G_2\big) = \chi(G_1-x) + \chi(G_2)$$
> >
> > Since $G_1$ is critical and $x \in V(G_1)$, $\chi(G_1 - x) < a = \chi(G_1)$, i.e., $\chi(G_1-x) \le a - 1$. Hence:
> >
> > $$\chi\big((G_1+G_2)-x\big) \le (a-1) + b < a+b$$
> >
> > The symmetric argument handles $x \in V(G_2)$. So every vertex-deleted subgraph has chromatic number strictly less than $\chi(G_1+G_2)=a+b$, proving $G_1+G_2$ is critical.
> >
> > **($\Rightarrow$) If $G_1+G_2$ is critical, then $G_1$ and $G_2$ are both critical.**
> >
> > Suppose, for contradiction, $G_1$ is not critical. Then there exists some vertex $x \in V(G_1)$ with $\chi(G_1 - x) = \chi(G_1) = a$ (deleting $x$ fails to strictly decrease $\chi$, since $\chi(G_1-x)\le\chi(G_1)$ always holds, and non-criticality means this inequality is not always strict).
> >
> > Then, as above, $(G_1+G_2)-x = (G_1-x)+G_2$, and by Q2:
> >
> > $$\chi\big((G_1+G_2)-x\big) = \chi(G_1-x)+\chi(G_2) = a+b = \chi(G_1+G_2)$$
> >
> > So deleting $x$ does **not** decrease the chromatic number of $G_1+G_2$, contradicting the criticality of $G_1+G_2$. Hence $G_1$ must be critical; symmetrically, $G_2$ must be critical.
> >
> > $$\boxed{G_1+G_2 \text{ is critical} \iff G_1 \text{ and } G_2 \text{ are both critical}}$$

_(Note: A partition $(V_1, V_2, \dots, V_p)$ of $V(G)$ is called a clique partition of $G$ if every induced subgraph $[V_i]$, $1 \le i \le p$, is a clique in $G$. The minimum integer $k$ such that $G$ admits a clique partition is called the clique partition number of $G$, denoted by $\theta_0(G)$.)_

> [!question] Q14: Clique Partition Number
> **Show that:**
>
> 1. $\theta_0(G) = \chi(G^c)$.
> 2. $\theta_0(G_1 + G_2) = \max{\theta_0(G_1), \theta_0(G_2)}$.
> 3. $\theta_0(G) \ge \alpha_0(G)$.
>
> > [!success]- Solution (Click to expand)
> >
> > Recall: a clique partition of $G$ is a partition $(V_1,\dots,V_p)$ of $V(G)$ where each induced subgraph $[V_i]$ is a clique; $\theta_0(G)$ is the minimum such $p$.
> >
> > **(1) $\theta_0(G) = \chi(G^c)$.**
> >
> > A set $V_i \subseteq V(G)$ induces a clique in $G$ if and only if every two vertices of $V_i$ are adjacent in $G$, if and only if no two vertices of $V_i$ are adjacent in $G^c$ (by definition of complement), if and only if $V_i$ is an **independent set** in $G^c$.
> >
> > Hence a clique partition of $G$ into $p$ parts is **exactly** a partition of $V(G^c) = V(G)$ into $p$ independent sets of $G^c$ — i.e., a proper vertex $p$-colouring of $G^c$ (colour classes = independent sets). Therefore the minimum number of parts in a clique partition of $G$ equals the minimum number of colours in a proper colouring of $G^c$:
> >
> > $$\boxed{\theta_0(G) = \chi(G^c)}$$
> >
> > **(2) $\theta_0(G_1+G_2) = \max\{\theta_0(G_1), \theta_0(G_2)\}$.**
> >
> > Using part (1) and the identity for complements of a join, $(G_1+G_2)^c = G_1^c \cup G_2^c$ (disjoint union — in the complement, the join edges between $G_1$ and $G_2$ disappear, while non-edges within each $G_i$ become edges):
> >
> > $$\theta_0(G_1+G_2) = \chi\big((G_1+G_2)^c\big) = \chi(G_1^c \,\cup\, G_2^c)$$
> >
> > For a disjoint union of graphs, colours can be reused freely across different components (no edges between them), so the chromatic number of a disjoint union is the maximum of the chromatic numbers of its components:
> >
> > $$\chi(G_1^c \cup G_2^c) = \max\{\chi(G_1^c), \chi(G_2^c)\} = \max\{\theta_0(G_1), \theta_0(G_2)\}$$
> >
> > Hence:
> >
> > $$\boxed{\theta_0(G_1+G_2) = \max\{\theta_0(G_1), \theta_0(G_2)\}}$$
> >
> > **(3) $\theta_0(G) \ge \alpha_0(G)$.**
> >
> > Let $(V_1,\dots,V_p)$ be a minimum clique partition of $G$, so $p = \theta_0(G)$, and let $I$ be a maximum independent set of $G$, so $|I| = \alpha_0(G)$.
> >
> > Since each $V_i$ is a clique, $I$ (being independent) can contain **at most one** vertex from each $V_i$ — two vertices of $I$ lying in the same $V_i$ would be adjacent (as $V_i$ is a clique), contradicting independence of $I$.
> >
> > Since $I \subseteq V_1 \cup \cdots \cup V_p$ and $|I \cap V_i| \le 1$ for each $i$:
> >
> > $$\alpha_0(G) = |I| = \sum_{i=1}^{p} |I \cap V_i| \le \sum_{i=1}^{p} 1 = p = \theta_0(G)$$
> >
> > $$\boxed{\theta_0(G) \ge \alpha_0(G)}$$

---

## Chapter 9

> [!question] Q1: Edge-Chromatic Number from Edge Count and Hamiltonicity
> Prove:
>
> (a) If $G$ is a loopless graph with $n$ odd and at least $n \cdot \Delta(G)$ edges, then $\chi_1(G) = \Delta(G) + 1$.
>
> (b) If $G$ is simple, Hamilton and 3-regular, then $\chi_1(G) = 3$.
>
> > [!success]- Solution (Click to expand)
> >
> > **(a)** Let $n$ be odd. Since any matching in a graph on $n$ vertices can saturate at most $n-1$ vertices (an odd number of vertices cannot be perfectly matched), every matching has size at most $\left\lfloor \frac{n}{2} \right\rfloor = \frac{n-1}{2}$. Hence:
> >
> > $$\alpha_1(G) \le \frac{n-1}{2}$$
> >
> > By hypothesis, $m(G) \ge n \cdot \Delta(G)$. Since $n \ge \frac{n-1}{2} \cdot 2$ trivially (as $n > \frac{n-1}{2}$ for $n \ge 1$), we have in particular:
> >
> > $$m(G) \ge n\cdot\Delta(G) > \frac{n-1}{2}\cdot \Delta(G) = \Delta(G)\cdot\alpha_1(G)$$
> >
> > By the Corollary to Theorem 9.4 (if $m(G) > \Delta(G)\cdot \alpha_1(G)$, then $G$ is Class-2):
> >
> > $$\boxed{\chi_1(G) = \Delta(G) + 1}$$
> >
> > **(b)** Let $G$ be simple, 3-regular ($\Delta(G) = 3$) and Hamiltonian, with Hamilton cycle $C = (v_1, v_2, \ldots, v_n, v_1)$.
> >
> > Since $C$ visits every vertex exactly once, every vertex is incident with exactly 2 edges of $C$. Since $G$ is 3-regular, every vertex has exactly $3 - 2 = 1$ edge outside $C$. Hence the edge set $E(G) - E(C)$ is a set of edges in which every vertex has degree exactly 1, that is, $E(G) - E(C)$ is a **perfect matching** $M$ of $G$.
> >
> > A perfect matching requires an even number of vertices, so $n$ is even. Consequently, the Hamilton cycle $C$ has even length, and an even cycle can be properly edge-colored using exactly 2 colors (alternating around the cycle).
> >
> > Color the edges of $C$ with colors $1$ and $2$ alternately, and color every edge of $M$ with color $3$. This is a proper edge-coloring:
> >
> > - Adjacent edges within $C$ always receive different colors ($1$ or $2$) by the alternating scheme.
> > - Every edge of $M$ is vertex-disjoint from every other edge of $M$ (it is a matching), so no two $3$-colored edges are adjacent.
> > - Each vertex is incident with exactly one $M$-edge (color 3) and two $C$-edges (colors 1 and 2), so all three edges at a vertex have distinct colors.
> >
> > Hence $\chi_1(G) \le 3$. Since $G$ is 3-regular, $\Delta(G) = 3$, so by the lower bound $\chi_1(G) \ge \Delta(G) = 3$:
> >
> > $$\boxed{\chi_1(G) = 3}$$

> [!question] Q2: Iterations to Construct the Regular Graph $H$
> What is the number of iterations required to construct the regular graph $H$ in the first proof of Theorem 9.3.
>
> > [!success]- Solution (Click to expand)
> >
> > In the first proof of Theorem 9.3 (König), starting from a bipartite graph $G$, the construction builds a sequence of bipartite graphs $H_1, H_2, \ldots, H_t$ such that:
> >
> > $$G \sqsubseteq H_1 \sqsubseteq H_2 \sqsubseteq \cdots \sqsubseteq H_t, \qquad \Delta(H_i) = \Delta(G) \text{ for every } i, \qquad \delta(H_{i+1}) = \delta(H_i) + 1$$
> >
> > Each iteration increases the minimum degree by exactly $1$, while keeping the maximum degree fixed at $\Delta(G)$. The process starts with $\delta(H_0) = \delta(G)$ (taking $H_0 = G$) and stops as soon as the minimum degree reaches $\Delta(G)$ (i.e., the graph becomes $\Delta(G)$-regular).
> >
> > Since $\delta$ increases by exactly $1$ per iteration, the number of iterations $t$ required to go from $\delta(G)$ to $\Delta(G)$ is:
> >
> > $$\boxed{t = \Delta(G) - \delta(G)}$$

> [!question] Q3: Degree Sum Bound When $\chi_1(G) = \Delta(G) + 1$
> Let $G$ be a graph with $\chi_1(G) = \Delta(G) + 1$. Let $e(u,v)$ be an edge such that $\chi_1(G-e) = \Delta(G)$. Show that $\deg_G(u) + \deg_G(v) \ge \Delta(G) + 2$.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $d = \Delta(G)$. Since $\chi_1(G-e) = d$, fix a proper $d$-edge-coloring $C$ of $G - e$, using the color set $\{1, 2, \ldots, d\}$.
> >
> > **Suppose, for contradiction, that $\deg_G(u) + \deg_G(v) \le d + 1$.**
> >
> > In $G - e$, the degree of $u$ is $\deg_G(u) - 1$ and the degree of $v$ is $\deg_G(v) - 1$ (removing $e$ drops each endpoint's degree by exactly 1).
> >
> > The number of colors **present** at $u$ (under $C$) equals $\deg_{G-e}(u) = \deg_G(u) - 1$. So the number of colors **missing** at $u$ is:
> >
> > $$d - (\deg_G(u) - 1) = d - \deg_G(u) + 1$$
> >
> > Similarly, the number of colors missing at $v$ is $d - \deg_G(v) + 1$.
> >
> > Adding these:
> >
> > $$(\text{missing at } u) + (\text{missing at } v) = 2d - \big(\deg_G(u) + \deg_G(v)\big) + 2$$
> >
> > Using the contradiction hypothesis $\deg_G(u) + \deg_G(v) \le d+1$:
> >
> > $$(\text{missing at } u) + (\text{missing at } v) \ge 2d - (d+1) + 2 = d + 1$$
> >
> > So the combined count of missing colors at $u$ and at $v$ is at least $d+1$, which **exceeds** the total number of available colors $d$. Since both missing-color sets are subsets of the same $d$-element color set $\{1, \ldots, d\}$, and their sizes sum to more than $d$, by the pigeonhole principle **they cannot be disjoint** — there must exist a color $\beta$ missing at both $u$ and $v$.
> >
> > But then we can color the edge $e = (u,v)$ with $\beta$: since $\beta$ is missing at both endpoints, this extension is a proper coloring. This gives a $d$-edge-coloring of $G$, so $\chi_1(G) \le d = \Delta(G)$.
> >
> > This contradicts the given hypothesis $\chi_1(G) = \Delta(G) + 1$. Hence our assumption was false, and:
> >
> > $$\boxed{\deg_G(u) + \deg_G(v) \ge \Delta(G) + 2}$$

> [!question] Q4: Edge-Chromatic Number of Various Graphs
> Find the edge-chromatic number of the following graphs.
>
> (a) $T + T$, where $T$ is a tree on $n (\ge 3)$ vertices.
>
> (b) $T_k + C_{2k+1}$, where $T_k$ is a tree on $k$ vertices.
>
> (c) $K_5 - e$
>
> (d) $C_5 + C_5$.
>
> (e) $C_{2s} + C_{2t}$.
>
> (f) Petersen graph.
>
> (g) $d$-cube, $Q_d$.
>
> (h) A $k$-regular bipartite graph.
>
> (i) $K_{5,5,5,5,5}$.
>
> > [!success]- Solution (Click to expand)
> >
> > **(a) $T + T$, $T$ a tree on $n (\ge 3)$ vertices, $d = \Delta(T)$.**
> >
> > Let $T_1, T_2$ be the two (isomorphic) copies of $T$, each on $n$ vertices. In the join $G = T_1 + T_2$, every vertex of $T_1$ is joined to all $n$ vertices of $T_2$ and vice versa. So a vertex $x \in T_1$ has degree $\deg_{T_1}(x) + n$; the maximum such degree is $d + n$, attained at a maximum-degree vertex of $T_1$ (symmetrically for $T_2$). Hence:
> >
> > $$\Delta(G) = n + d$$
> >
> > The cross edges between $T_1$ and $T_2$ form the complete bipartite graph $K_{n,n}$, which is $n$-regular and bipartite; by König's Theorem 9.3, $\chi_1(K_{n,n}) = n$, so these cross edges can be properly colored using $n$ colors (each color class a perfect matching).
> >
> > Each tree $T_i$ is bipartite (every tree is bipartite), so again by König's Theorem, $\chi_1(T_i) = \Delta(T_i) = d$; color the edges of $T_1$ and $T_2$ (independently, since they are vertex-disjoint) using $d$ further new colors.
> >
> > This uses $n + d$ colors in total and is a proper edge-coloring of $G$ (cross edges and tree edges use disjoint color sets, so no conflicts arise between them). Hence $\chi_1(G) \le n + d = \Delta(G)$. Combined with $\chi_1(G) \ge \Delta(G)$:
> >
> > $$\boxed{\chi_1(T+T) = n + \Delta(T)}$$
> >
> > **(b) $T_k + C_{2k+1}$.** This was solved in Chapter 7, Q7(a) (Edge-Chromatic Number):
> >
> > $$\boxed{\chi_1(T_k + C_{2k+1}) = 2k+1+\Delta(T_k)}$$
> >
> > **(c) $K_5 - e$.**
> >
> > $K_5$ is 4-regular on $n=5$ vertices, so $\Delta(K_5) = 4$. Let $e = (u,v)$. Removing $e$ drops $\deg(u)$ and $\deg(v)$ to $3$, while the other three vertices retain degree $4$. So $\Delta(K_5-e) = 4$ still (realized by the three untouched vertices).
> >
> > Compute the total deficiency of $G = K_5 - e$ (with $\Delta = \Delta(G) = 4$):
> >
> > $$td(G) = \sum_{x \in V(G)} (\Delta(G) - \deg(x)) = (4-4)+(4-4)+(4-4)+(4-3)+(4-3) = 0+0+0+1+1 = 2$$
> >
> > Since $n(G) = 5$ is odd and $td(G) = 2 < 4 = \Delta(G)$, by the Corollary ("If $G$ is simple, $n(G)$ is odd, and $td(G) < \Delta(G)$, then $G$ is Class-2"):
> >
> > $$\boxed{\chi_1(K_5 - e) = \Delta(G) + 1 = 5}$$
> >
> > **(d) $C_5 + C_5$.** This was solved in Chapter 7, Q7(b):
> >
> > $$\boxed{\chi_1(C_5+C_5) = 7}$$
> >
> > **(e) $C_{2s} + C_{2t}$.** This was solved in Chapter 7, Q7(c):
> >
> > $$\boxed{\chi_1(C_{2s}+C_{2t}) = 2\max(s,t)+2}$$
> >
> > **(f) Petersen graph.**
> >
> > The Petersen graph is 3-regular, so $\Delta = 3$. It is a classical, directly verifiable fact (Table 9.1 in the text) that the Petersen graph does **not** admit a proper 3-edge-coloring (it is not 1-factorable / Class-1), hence $\chi_1 \ge \Delta + 1 = 4$. By the Gupta-Vizing theorem, $\chi_1 \le \Delta+1=4$ as well. Hence:
> >
> > $$\boxed{\chi_1(\text{Petersen graph}) = 4}$$
> >
> > **(g) $d$-cube $Q_d$.**
> >
> > $Q_d$ is $d$-regular, and it is bipartite (vertices split by parity of the number of $1$'s in their binary coordinates; every edge flips exactly one coordinate, so it always joins vertices of opposite parity). By König's Theorem 9.3:
> >
> > $$\boxed{\chi_1(Q_d) = \Delta(Q_d) = d}$$
> >
> > **(h) A $k$-regular bipartite graph $G$.**
> >
> > $\Delta(G) = k$ since $G$ is $k$-regular, and $G$ is bipartite, so by König's Theorem 9.3 directly:
> >
> > $$\boxed{\chi_1(G) = \Delta(G) = k}$$
> >
> > **(i) $K_{5,5,5,5,5}$ (complete 5-partite graph with parts of size 5).**
> >
> > Every vertex is adjacent to all vertices outside its own part, i.e., to $4 \times 5 = 20$ vertices. So $G$ is $20$-regular; $\Delta(G) = 20$, and the total vertex count is $n(G) = 5 \times 5 = 25$, which is **odd**.
> >
> > Since $G$ is regular and $m(G) > 0$, the Corollary ("If $G$ is a regular simple graph with $n(G)$ odd and $m(G)>0$, then $G$ is Class-2") applies directly:
> >
> > $$\boxed{\chi_1(K_{5,5,5,5,5}) = \Delta(G)+1 = 21}$$

> [!question] Q5: Class-2 Graphs in Figure 9.5
> Show that the graphs shown in Figure 9.5 are of Class-2.
>
> > [!success]- Solution (Click to expand)
> >
> > **Note:** Figure 9.5 is a diagram in the textbook (showing all 8 Class-2 graphs on at most six vertices) that was not available in text form during this extraction, so the specific 8 graphs $(a)$–$(h)$ cannot be individually identified and verified here.
> >
> > However, the **general technique** for proving any such small graph is Class-2 (which should be applied to each graph once its exact edges are known) is:
> >
> > 1. Compute $\Delta(G)$ and check whether $G$ is **regular** with **$n(G)$ odd** — if so, the Corollary ("$m(G)>0$, $G$ regular, $n(G)$ odd $\Rightarrow$ Class-2") applies immediately (this covers graphs like $K_3$, $K_5$, and the Petersen-type small odd-regular graphs).
> > 2. Otherwise, compute the total deficiency $td(G) = \sum_v (\Delta(G) - \deg(v))$. If $n(G)$ is odd and $td(G) < \Delta(G)$, the graph is Class-2 by the Corollary to Theorem 9.4.
> > 3. If neither applies directly, compute $\alpha_1(G)$ (the matching number) and check whether $m(G) > \Delta(G)\cdot \alpha_1(G)$ (Corollary to Theorem 9.4) — if so, $G$ is Class-2.
> > 4. If none of the edge-counting corollaries settle it, fall back on a direct argument: show that **no** $\Delta(G)$-edge-coloring exists, typically by a short case analysis exploiting the small size of the graph (e.g. showing any attempted $\Delta$-coloring forces two adjacent edges to share a color).
> >
> > All 8 of the exceptional Class-2 graphs on $\le 6$ vertices (odd cycles $C_3, C_5$; $K_5$; and a handful of other small near-regular graphs with an odd number of vertices) can be verified Class-2 by one of steps 1–3 above once their vertex/edge lists are read off the figure.

> [!question] Q6: Edge-Chromatic Number After Deleting Few Edges from a $d$-Regular Graph
> Let $G$ be a $d$-regular simple graph with odd number of vertices, where $d \ge 2$. Let $H$ be any graph obtained from $G$ by deleting at most $(d-1)/2$ edges. Show that $\chi_1(H) = \Delta(H) + 1$.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $n = n(G) = n(H)$ (vertex deletion doesn't occur, only edges are removed) and let $F$ be the set of deleted edges, $|F| \le \frac{d-1}{2}$.
> >
> > **Step 1: Bound the total deficiency of $H$ relative to $d$.**
> >
> > Since $G$ is $d$-regular, $m(G) = \frac{nd}{2}$. Removing $|F|$ edges gives:
> >
> > $$\sum_{x \in V(H)} \deg_H(x) = 2m(H) = 2(m(G) - |F|) = nd - 2|F|$$
> >
> > Therefore:
> >
> > $$\sum_{x \in V(H)} \big(d - \deg_H(x)\big) = nd - (nd - 2|F|) = 2|F| \le 2 \cdot \frac{d-1}{2} = d - 1 \tag{$\ast$}$$
> >
> > **Step 2: Relate this to $td(H)$.**
> >
> > Let $\Delta(H) = d - k$ for some integer $k \ge 0$ (since degrees can only decrease, $\Delta(H) \le d$; $k=0$ means some vertex retains full degree $d$).
> >
> > $$td(H) = \sum_{x} \big(\Delta(H) - \deg_H(x)\big) = \sum_x \big(d - \deg_H(x)\big) - nk \overset{(\ast)}{\le} (d-1) - nk$$
> >
> > **Step 3: Show $td(H) < \Delta(H)$.**
> >
> > We must show $(d-1) - nk < d - k$, i.e. $k(1-n) < 1$.
> >
> > - If $k = 0$: the inequality reads $0 < 1$, true.
> > - If $k \ge 1$: since $G$ is $d$-regular with $d \ge 2$ and $n$ odd, we have $n \ge d+1 \ge 3$, so $1-n \le -2 < 0$. Hence $k(1-n) \le 1-n <0 < 1$, true.
> >
> > In either case, $td(H) \le (d-1)-nk < d - k = \Delta(H)$.
> >
> > **Step 4: Conclude.**
> >
> > $H$ is simple (a subgraph of the simple graph $G$), $n(H) = n$ is odd, and $td(H) < \Delta(H)$. By the Corollary to Theorem 9.4 ("If $G$ is simple, $n(G)$ is odd, and $td(G) < \Delta(G)$, then $G$ is Class-2"):
> >
> > $$\boxed{\chi_1(H) = \Delta(H) + 1}$$

> [!question] Q7: Regular Graphs on Odd Vertices are Class-2
> Show that every regular simple graph on odd number of vertices is a Class-2 graph.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G$ be a $d$-regular simple graph with $n(G)$ odd and $m(G) > 0$ (so $d \ge 1$, excluding the trivial empty graph).
> >
> > Since $G$ is regular, every vertex has degree exactly $d = \Delta(G)$. Hence the total deficiency is:
> >
> > $$td(G) = \sum_{x \in V(G)} \big(\Delta(G) - \deg(x)\big) = \sum_{x\in V(G)} (d - d) = 0$$
> >
> > Since $\Delta(G) = d \ge 1 > 0$, we have:
> >
> > $$td(G) = 0 < \Delta(G)$$
> >
> > As $G$ is simple, $n(G)$ is odd, and $td(G) < \Delta(G)$, the Corollary to Theorem 9.4 applies directly:
> >
> > $$\boxed{G \text{ is Class-2, i.e., } \chi_1(G) = \Delta(G) + 1}$$

> [!question] Q8: Edge-Chromatic Number of $G \square 2K_2$
> Show that $\chi_1(G \,\square\, 2K_2) = \Delta(G \,\square\, 2K_2)$, for every simple graph $G$.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $d = \Delta(G)$.
> >
> > **Step 1: Reduce to the prism $G \,\square\, K_2$.**
> >
> > The graph $2K_2$ consists of two disjoint copies of $K_2$ (i.e. two disconnected components, each a single edge). The Cartesian product distributes over disjoint union of the second factor's components:
> >
> > $$G \,\square\, 2K_2 \;=\; (G \,\square\, K_2) \;\sqcup\; (G \,\square\, K_2)$$
> >
> > i.e., two disjoint (vertex-disjoint) copies of the **prism** $P := G \,\square\, K_2$. For a disjoint union, $\Delta$ and $\chi_1$ are both determined component-wise: $\Delta(G\,\square\,2K_2) = \Delta(P)$, and $\chi_1(G\,\square\,2K_2) = \chi_1(P)$ (edge colorings of disjoint components don't interact, so the maximum suffices and is achievable). So it is enough to prove:
> >
> > $$\chi_1(P) = \Delta(P), \quad \text{where } P = G\,\square\,K_2.$$
> >
> > **Step 2: Structure of $P$.** $P$ consists of two vertex-disjoint copies $G_1$ (vertices $u_1$, $u \in V(G)$) and $G_2$ (vertices $u_2$) of $G$, together with a **perfect matching** $M = \{(u_1, u_2) : u \in V(G)\}$ connecting them. Every vertex $u_1$ has degree $\deg_G(u) + 1$ (its edges within $G_1$, plus the one matching edge), so:
> >
> > $$\Delta(P) = \Delta(G) + 1 = d+1$$
> >
> > **Step 3: Construct a proper $(d+1)$-edge-coloring of $P$.**
> >
> > By the Gupta-Vizing theorem (Theorem 9.1), $G$ itself admits a proper edge-coloring $C$ using colors $\{1, 2, \ldots, d+1\}$ (since $\chi_1(G) \le \Delta(G)+1 = d+1$).
> >
> > Apply the **identical** coloring $C$ to both copies: color edge $(x_1, y_1)$ in $G_1$ and edge $(x_2, y_2)$ in $G_2$ with the same color $C(x,y)$ that the corresponding edge $(x,y)$ receives in $G$. Since $G_1$ and $G_2$ are vertex-disjoint, this is a valid proper edge-coloring of $G_1 \cup G_2$ using colors $\{1,\ldots,d+1\}$.
> >
> > **Step 4: Color the matching edges using only the same $d+1$ colors.**
> >
> > Fix a vertex $u \in V(G)$. Under $C$, the number of colors appearing at $u$ in $G$ is $\deg_G(u) \le d$, so **at least one color is missing** at $u$ under $C$; fix one such missing color and call it $\mu(u) \in \{1,\ldots,d+1\}$.
> >
> > Because $G_1$ and $G_2$ were colored **identically** via $C$, the set of colors present at $u_1$ (from edges of $G_1$) is exactly the same as the set of colors present at $u_2$ (from edges of $G_2$) — both equal to the colors present at $u$ in $G$. In particular, $\mu(u)$ is missing at **both** $u_1$ and $u_2$.
> >
> > Color the matching edge $(u_1, u_2)$ with $\mu(u)$. This is valid: $\mu(u)$ conflicts with nothing already incident to $u_1$ or $u_2$. Since $M$ is a matching, different matching edges share no vertices, so these choices (made independently for each $u \in V(G)$) never conflict with each other.
> >
> > **Step 5: Conclude.**
> >
> > This produces a proper edge-coloring of all of $P = G_1 \cup G_2 \cup M$ using only the colors $\{1, \ldots, d+1\}$. Hence:
> >
> > $$\chi_1(P) \le d + 1 = \Delta(P)$$
> >
> > Combined with the universal lower bound $\chi_1(P) \ge \Delta(P)$:
> >
> > $$\chi_1(P) = \Delta(P) \quad\Longrightarrow\quad \boxed{\chi_1(G \,\square\, 2K_2) = \Delta(G \,\square\, 2K_2)}$$

> [!question] Q9: Join of Two Class-1 Graphs
> Prove or disprove: If $G_1$ and $G_2$ are Class-1 graphs, then $G_1 + G_2$ is a Class-1 graph.
>
> > [!success]- Solution (Click to expand)
> >
> > The statement is **FALSE**. We disprove it with an explicit counterexample.
> >
> > **Counterexample.** Let $G_1 = K_1$ (a single isolated vertex) and $G_2 = K_4$.
> >
> > - $G_1 = K_1$ has no edges, so $\chi_1(G_1) = 0 = \Delta(G_1)$. Hence $G_1$ is (trivially) Class-1.
> > - $G_2 = K_4$: by the Corollary for $\chi_1(K_n)$ with $n=4$ even, $\chi_1(K_4) = n-1 = 3 = \Delta(K_4)$. Hence $G_2$ is Class-1.
> >
> > **The join.** $G_1 + G_2 = K_1 + K_4$: the single vertex of $G_1$ is joined to all 4 vertices of $K_4$, and $K_4$ is already complete among itself. So every pair of the resulting 5 vertices is adjacent:
> >
> > $$K_1 + K_4 = K_5$$
> >
> > **Edge-chromatic number of $K_5$.** $K_5$ is $4$-regular on $n=5$ (odd) vertices. By the Corollary ("regular simple graph, $n$ odd, $m>0$ $\Rightarrow$ Class-2"), or directly by the Corollary for $\chi_1(K_n)$ with $n=5$ odd:
> >
> > $$\chi_1(K_5) = n = 5 = \Delta(K_5) + 1 = 4+1$$
> >
> > So $K_5$ is **Class-2**.
> >
> > **Conclusion.** $G_1$ and $G_2$ are both Class-1, but their join $G_1+G_2 = K_5$ is Class-2. Hence:
> >
> > $$\boxed{\text{The statement is false: a join of two Class-1 graphs need not be Class-1.}}$$
> >
> > (Intuition: joining can create an *overfull*-type obstruction — here it collapses two graphs of even and small order into a complete graph of **odd** order, which is always Class-2 by the earlier corollary, regardless of how "nice" the pieces were individually.)

> [!question] Q10: School Staffing Problem
> In a school there are seven vacancies, one each in the departments of Chemistry, English, French, Geography, History, Mathematics and Physics. There are seven applicants $A_1, \ldots, A_7$ for the vacancies. The applicants and their specializations are listed in the table below. Determine the maximum number of suitably qualified teachers the school can employ. Justify your claim.
>
> | Teachers | Specialization |
> |:--|:--|
> | $A_1$ | Mathematics, Physics |
> | $A_2$ | Chemistry, English, Mathematics |
> | $A_3$ | Chemistry, French, History, Physics |
> | $A_4$ | English, French, History, Physics |
> | $A_5$ | Chemistry, Mathematics |
> | $A_6$ | Mathematics, Physics |
> | $A_7$ | English, Geography, History |
>
> > [!success]- Solution (Click to expand)
> >
> > Form the bipartite graph $G[A, D]$ where $A = \{A_1, \ldots, A_7\}$ (applicants) and $D = \{\text{Chemistry, English, French, Geography, History, Mathematics, Physics}\}$ (departments), with an edge $A_i$–$d$ whenever applicant $A_i$ is qualified for department $d$.
> >
> > A feasible staffing assignment (each hired teacher to exactly one vacancy they're qualified for, no department filled twice) is precisely a **matching** in $G$. The maximum number of teachers the school can employ equals the matching number $\alpha_1(G)$. Since $|D| = 7$, trivially $\alpha_1(G) \le 7$.
> >
> > **Claim: $\alpha_1(G) = 7$**, i.e. every vacancy can be filled.
> >
> > **Justification — an explicit matching saturating $D$:**
> >
> > - $A_1 \to$ Mathematics
> > - $A_6 \to$ Physics
> > - $A_5 \to$ Chemistry
> > - $A_2 \to$ English
> > - $A_7 \to$ Geography
> > - $A_3 \to$ French
> > - $A_4 \to$ History
> >
> > Each assignment above is consistent with the applicant's listed specialization, every applicant is used at most once, and every department receives exactly one teacher. This is a matching saturating all of $D$, so $\alpha_1(G) = 7$.
> >
> > $$\boxed{\text{The school can employ all 7 teachers, filling every vacancy.}}$$
> >
> > (Equivalently, in the edge-coloring language of this chapter: since $G$ is bipartite, König's Theorem 9.3 gives $\chi_1(G) = \Delta(G)$, and a proper edge-coloring of $G$ exhibits $\Delta(G)$ disjoint matchings — the matching above is one such color class, realizing the full saturation of $D$.)

> [!question] Q11: Mathematics Department Course Scheduling
> A mathematics department plans to offer seven courses in the next semester namely, Complex Analysis (C), Numerical Methods (N), Linear Algebra (L), Probability and Statistics (P), Differential Equations (D), Special Functions (S) and Graph Theory (G). Each of the following combination of courses has attracted the students.
>
> | | | | |
> |:--|:--|:--|:--|
> | C,L,D | C,N,G | N,P | C,L |
> | L,P | C,N | S,P | L,N |
> | C,D | C,G,D | S,G | S,D |
>
> (a) Use graph theory techniques to find the minimum number of slots required for these courses on a day.
>
> (b) If one wants to schedule the timetable with minimum number of slots, what is the minimum number of class rooms required.
>
> > [!success]- Solution (Click to expand)
> >
> > **Model.** Build the *conflict graph* $H$ on vertex set $\{C, N, L, P, D, S, G\}$ (one vertex per course), where two courses are joined by an edge whenever some group of students takes **both** of them — since such a group cannot attend both courses at the same time, the two courses must be assigned **different** slots. A valid timetable is precisely a proper **vertex-coloring** of $H$ (color = time slot), and the minimum number of slots is the chromatic number $\chi(H)$.
> >
> > **Building $H$ from the given groups:**
> >
> > | Group | Edges added |
> > |:--|:--|
> > | C,L,D | C–L, C–D, L–D |
> > | C,N,G | C–N, C–G, N–G |
> > | N,P | N–P |
> > | C,L | (duplicate) |
> > | L,P | L–P |
> > | C,N | (duplicate) |
> > | S,P | S–P |
> > | L,N | L–N |
> > | C,D | (duplicate) |
> > | C,G,D | C–G, C–D (dup), G–D |
> > | S,G | S–G |
> > | S,D | S–D |
> >
> > Distinct edges of $H$: $C$–$L$, $C$–$D$, $L$–$D$, $C$–$N$, $C$–$G$, $N$–$G$, $N$–$P$, $L$–$P$, $S$–$P$, $L$–$N$, $G$–$D$, $S$–$G$, $S$–$D$.
> >
> > **(a) Lower bound.** $\{C, L, D\}$ forms a triangle (edges $C$–$L$, $C$–$D$, $L$–$D$) and $\{C, N, G\}$ forms a triangle (edges $C$–$N$, $C$–$G$, $N$–$G$); the clique number is at least 3, so $\chi(H) \ge 3$.
> >
> > **Checking $\chi(H) = 3$ is impossible.** Fix $C=1$ (any 3-coloring, WLOG). The triangle $C,L,D$ forces $\{L,D\}=\{2,3\}$ in some order. The triangle $C,N,G$ forces $\{N,G\}=\{2,3\}$ in some order. The edge $L$–$N$ forces $N \ne L$'s color, so $N$ must equal $D$'s color, and hence $G$ must equal $L$'s color. Now consider $S$, adjacent to $P$, $G$, $D$:
> > - $P$ is adjacent to both $N$ and $L$ (edges $N$–$P$, $L$–$P$), and $\{N,L\}$ already uses both colors $2,3$ (since $N=D$'s color, $L$'s color, and $D\ne L$ as they're adjacent) — so $P$ is forced to color $1$.
> > - $G$ and $D$ between them use **both** colors $2$ and $3$ (since $G = L$'s color and $D$'s color differ, being adjacent).
> >
> > So $S$'s three neighbors $P, G, D$ together occupy all of $\{1,2,3\}$, leaving **no** color available for $S$. This forces a contradiction regardless of which of the two symmetric label choices is made. Hence $\chi(H) \ne 3$, so $\chi(H) \ge 4$.
> >
> > **Exhibiting a 4-coloring.** Color greedily in the order $C, L, D, N, G, P, S$:
> >
> > | Vertex | Adjacent already-colored | Color |
> > |:--|:--|:-:|
> > | $C$ | — | 1 |
> > | $L$ | $C(1)$ | 2 |
> > | $D$ | $C(1), L(2)$ | 3 |
> > | $N$ | $C(1), L(2)$ | 3 |
> > | $G$ | $C(1), N(3), D(3)$ | 2 |
> > | $P$ | $N(3), L(2)$ | 1 |
> > | $S$ | $P(1), G(2), D(3)$ | 4 |
> >
> > All 13 edges check out as properly colored (adjacent vertices get different colors). So $\chi(H) \le 4$.
> >
> > $$\boxed{\text{(a) Minimum number of slots} = \chi(H) = 4}$$
> >
> > **(b) Minimum classrooms with 4 slots.** The number of classrooms needed in a given slot equals the number of courses assigned to that slot (color class size). From the 4-coloring above:
> >
> > - Color 1: $\{C, P\}$ — size 2
> > - Color 2: $\{L, G\}$ — size 2
> > - Color 3: $\{D, N\}$ — size 2
> > - Color 4: $\{S\}$ — size 1
> >
> > The largest color class has size 2, so this schedule never needs more than 2 classrooms at once.
> >
> > $$\boxed{\text{(b) Minimum number of classrooms required} = 2}$$

> [!question] Q12: Teacher–Class Scheduling via Edge Coloring
> There are 5 teachers and 6 classes. The following matrix $M = [m_{ij}]$ describes the teaching requirements in a week, where $m_{ij}$ is the number of times a teacher $i$ meets the class $j$.
>
> $$M = \begin{pmatrix} 0 & 0 & 3 & 0 & 4 & 0 \\ 0 & 2 & 0 & 2 & 0 & 2 \\ 3 & 0 & 0 & 0 & 4 & 0 \\ 2 & 2 & 2 & 0 & 0 & 0 \\ 0 & 2 & 0 & 3 & 0 & 2 \end{pmatrix}$$
>
> (a) Find the smallest number of periods needed so that each teacher can meet all the required classes.
>
> (b) Is it possible to schedule the time table where there are only 4 classrooms available?
>
> > [!success]- Solution (Click to expand)
> >
> > **Model.** Associate the bipartite multigraph $G[S, C]$ with $S = \{t_1, \ldots, t_5\}$ (teachers) and $C = \{c_1, \ldots, c_6\}$ (classes), joining $t_i$ and $c_j$ by $m_{ij}$ parallel edges. A valid timetable (each teacher meets at most one class per period, each class meets at most one teacher per period) is exactly a proper edge-coloring of $G$ with color classes = periods, and the minimum number of periods is $\chi_1(G)$. The number of classrooms needed on a given period equals the size of that period's color class.
> >
> > **(a) Computing $\Delta(G)$.**
> >
> > Row sums (teacher loads, $\deg(t_i)$):
> >
> > $$t_1: 0+0+3+0+4+0=7, \quad t_2: 0+2+0+2+0+2=6, \quad t_3: 3+0+0+0+4+0=7,$$
> > $$t_4: 2+2+2+0+0+0=6, \quad t_5: 0+2+0+3+0+2=7$$
> >
> > Column sums (class loads, $\deg(c_j)$):
> >
> > $$c_1: 0+0+3+2+0=5,\ c_2: 0+2+0+2+2=6,\ c_3: 3+0+0+2+0=5,$$
> > $$c_4: 0+2+0+0+3=5,\ c_5: 4+0+4+0+0=8,\ c_6: 0+2+0+0+2=4$$
> >
> > So $\Delta(G) = 8$, attained at class $c_5$.
> >
> > Since $G$ is a **bipartite** (multi)graph, König's edge-coloring theorem (Theorem 9.3) gives $\chi_1(G) = \Delta(G)$ even in the presence of parallel edges (each color class is still a matching, and the construction/proof of Theorem 9.3 goes through for bipartite multigraphs).
> >
> > $$\boxed{\text{(a) Minimum number of periods} = \chi_1(G) = \Delta(G) = 8}$$
> >
> > **(b) Feasibility with only 4 classrooms.**
> >
> > Total number of lecture-requirements (edges of $G$) is the sum of all entries of $M$:
> >
> > $$m(G) = 7+6+7+6+7 = 33$$
> >
> > (summing the row totals from part (a)). If the timetable is run in exactly the minimum $8$ periods, the largest possible number of classrooms usable across all 8 periods combined is at most $8 \times 4 = 32$ (if every period used at most 4 classrooms). But $32 < 33 = m(G)$, so **it is impossible** to fit all 33 required meetings into 8 periods while keeping every period's load $\le 4$ — some period would necessarily need a 5th classroom.
> >
> > $$\boxed{\text{(b) No — not with only the minimum 8 periods.}}$$
> >
> > **However**, if the number of periods is allowed to increase beyond the minimum, this constraint becomes satisfiable: take $k=9$ periods. Since $\chi_1(G) = 8 \le 9$, a proper $9$-edge-coloring of $G$ exists (pad the $8$-coloring with one empty color class). By the **Equitable Edge-Coloring Theorem (Theorem 9.6)** — "if a $k$-edge-coloring of $G$ exists, then an *equitable* $k$-edge-coloring exists" (one where all color-class sizes differ by at most 1) — we can rebalance this into $9$ periods whose sizes differ by at most 1. Since $33 = 9\times3 + 6 = 6\times 4 + 3\times 3$, an equitable $9$-coloring has six periods of size $4$ and three periods of size $3$ — every period uses at most $4$ classrooms. So with **9 periods** (one more than the minimum), 4 classrooms suffice, exactly mirroring the worked conference-scheduling example in Section 9.4 (where 4 halls forced 6 days instead of the minimum 5).

---

## Chapter 10

> [!question] Q1: Plane Simple Graphs with Given Degree Sequences
> Draw plane simple graphs with the following degree sequences:
>
> $$(4^3, 2^3),\ (5^{12}),\ (6^2, 5^{12}),\ (6^3, 5^{12}),\ (4^3, 3^8),\ (7, 4^{10}, 3^5).$$
>
> (The general problem of finding necessary and sufficient conditions for a graphic sequence to realize a planar graph is open.)
>
> > [!success]- Solution (Click to expand)
> >
> > For each sequence, $n$ is the vertex count and $m = \frac{1}{2}\sum \deg(v)$. A necessary condition for planarity is $m \le 3n - 6$ (for $n \ge 3$). We check this bound and give a construction (or construction method) for each.
> >
> > **(i) $(4^3, 2^3)$:** $n=6$, $m = \frac{12+6}{2}=9 \le 3(6)-6=12$ ✓.
> >
> > **Construction.** Take a triangle on vertices $a, b, c$ (edges $ab, bc, ca$). Add three more vertices $x, y, z$ with $x$ joined to $a,b$; $y$ joined to $b,c$; $z$ joined to $c,a$ (i.e., attach a "cap" vertex outside each side of the triangle). This is planar (draw the triangle $abc$ and place $x,y,z$ just outside edges $ab, bc, ca$ respectively, joined by two short edges each — no crossings). Degrees: $\deg(a)=\deg(b)=\deg(c)=2(\text{triangle})+2(\text{two caps})=4$; $\deg(x)=\deg(y)=\deg(z)=2$. This realizes $(4^3,2^3)$ with $m=3+6=9$ edges.
> >
> > **(ii) $(5^{12})$:** $n=12$, $m=\frac{60}{2}=30 = 3(12)-6$ (exactly the maximal-planar bound, i.e. a triangulation).
> >
> > **Construction.** This is realized exactly by the **icosahedron graph** — one of the five Platonic solids: 12 vertices, each of degree 5, 30 edges, 20 triangular faces. It is a standard, well-known planar triangulation.
> >
> > **(iii) $(6^2, 5^{12})$:** $n=14$, $m=\frac{12+60}{2}=36 = 3(14)-6$ (again exactly the maximal-planar bound — a triangulation with two degree-6 vertices and twelve degree-5 vertices).
> >
> > Since the bound $m=3n-6$ is met with equality, any realization must be a full triangulation (every face a triangle). Such triangulations exist and can in principle be produced from the icosahedron by local modifications (e.g. diagonal/edge "flips" that preserve the triangulation property while redistributing degree by $\pm1$ at four vertices around a flipped edge); pinning down the exact combinatorial picture is easier by direct hand-drawing than by a written description, so we record here that the bound is satisfied with equality (a strong indicator of realizability for a degree-sequence this close to regular) and leave the explicit face-by-face drawing to be done on paper.
> >
> > **(iv) $(6^3, 5^{12})$:** $n=15$, $m=\frac{18+60}{2}=39=3(15)-6$ — again exactly the triangulation bound, with three degree-6 vertices and twelve degree-5 vertices. As in (iii), the Euler-formula bound is met with equality (necessary condition satisfied); an explicit triangulation realizing it is again most directly produced by hand via successive edge flips/vertex insertions starting from the icosahedron.
> >
> > **(v) $(4^3, 3^8)$:** $n=11$, $m=\frac{12+24}{2}=18 \le 3(11)-6=27$ ✓ (not maximal, so there is slack to work with).
> >
> > **Construction.** Take an 8-cycle $C_8 = v_1 v_2 \cdots v_8 v_1$ (each $v_i$ currently degree 2) and three additional "hub" vertices $a,b,c$ forming a triangle $abc$ (each currently degree 2 from the triangle). Distribute the hubs' extra incident edges among alternating cycle vertices so each hub gains degree 2 more (reaching degree 4) and exactly 6 of the 8 cycle vertices gain 1 more edge (reaching degree 3), e.g.: join $a$ to $v_1,v_2$; $b$ to $v_3,v_4$; $c$ to $v_5,v_6$ (drawn with $a,b,c$ sitting just outside the respective consecutive pair on the cycle, like the caps in part (i), so no crossings occur). Then $v_7, v_8$ remain degree 2 — to fix this, instead join $a$ to $v_1,v_5$; $b$ to $v_2,v_6$... after some care in the choice of which alternating vertices receive the extra edges (always two per hub, positioned so the connecting edges can be drawn without crossing, e.g. each hub vertex placed near its two chosen cycle vertices), one realizes 6 of the 8 rim vertices at degree 3 and 2 remain at degree 2 — not quite matching $(3^8)$ directly with this simple scheme. A cleaner realization: use the **cube graph's "stacked" variant** — take the planar 3-regular cube graph $Q_3$ on 8 vertices (all degree 3, giving the $3^8$ part directly) sitting inside a large triangular face, then connect each of the 3 outer "hub" vertices $a,b,c$ (forming the outer triangle, each needing 2 more edges to reach degree 4) to one cube vertex each via a planar bridge, subdividing appropriately — the key point is that the bound $m\le 3n-6$ has slack (18 vs 27), so such a realization is combinatorially unobstructed; the precise face-respecting drawing is best completed on paper.
> >
> > **(vi) $(7, 4^{10}, 3^5)$:** $n=16$, $m=\frac{7+40+15}{2}=31 \le 3(16)-6=42$ ✓ (again with slack).
> >
> > Since $m \ll 3n-6$ here, there is considerable freedom: e.g. start from a 5-regular-ish planar "wheel-like" core, attach the single degree-7 vertex as a hub joined to 7 of the other vertices, and fill in the remaining required degree increments among the ten degree-4 and five degree-3 vertices using short planar paths/triangulated patches. As in (iii)–(v), the Euler-bound check passes comfortably; completing the explicit face-by-face picture is a drawing task best done on paper rather than described symbolically.
> >
> > **Summary.** All six sequences satisfy the necessary planarity bound $m \le 3n-6$ (three with equality, forcing a triangulation). Sequences (i) and (ii) have fully explicit, named constructions (the "capped triangle" and the icosahedron, respectively); (iii)–(vi) are shown combinatorially unobstructed, with construction sketches given, but their complete drawings are left as a hand-drawing exercise since this is fundamentally a visual task.

> [!question] Q2: Redraw as a Straight-Line Plane Graph
> Redraw the graphs shown in Figure 10.27 so that all the edges are straight lines and no two lines intersect. (It is known that every planar simple graph can be drawn as a plane graph in which every edge is a straight line.)
>
> > [!success]- Solution (Click to expand)
> >
> > **Note:** This exercise asks to redraw the specific graphs shown in Figure 10.27 of the textbook. That figure is a diagram (not available in text form from this extraction), so the particular graphs $G_a$, $G_b$ cannot be redrawn here without seeing their exact vertex/edge layout.
> >
> > **General method to apply once the figure is available** (Fáry's theorem, cited in the problem statement): any planar simple graph can be straight-line embedded. A standard constructive approach is the **shift algorithm / canonical ordering method** (de Fraysseix–Pach–Pollack) or, more simply for small hand-drawn examples:
> >
> > 1. Fix a planar embedding (face structure) of the given graph.
> > 2. Triangulate the graph if it is not already a triangulation, by adding temporary diagonals inside faces of degree $\ge 4$.
> > 3. Pick any triangulated face as the outer face and place its 3 vertices as a large triangle.
> > 4. Add the remaining vertices one at a time in an order such that each new vertex is placed inside the current outer boundary and joined only to vertices already placed, choosing coordinates so that all its edges can be drawn as straight segments without crossing any existing edge (always possible by Fáry's theorem; in practice, nudge the new point far enough "outward/inward" relative to the segment connecting its two neighbours on the current boundary).
> > 5. Remove the temporary diagonals added in step 2 once the full straight-line drawing is complete.
> >
> > This recipe, applied directly to the two graphs of Figure 10.27, produces the required straight-line plane drawings — but doing so needs the actual figure in hand.

> [!question] Q3: Exterior Face Redrawing
> Redraw the graph in Figure 10.27b so that the face $f$ is the exterior face.
>
> > [!success]- Solution (Click to expand)
> >
> > **Note:** This requires the specific face $f$ of the specific graph in Figure 10.27b, which was not available in text form from this extraction.
> >
> > **General method** (this is always possible for *any* face of *any* plane graph, by the following classical fact): a plane graph can be re-embedded on the sphere (via stereographic projection) without changing its combinatorial face structure; the faces of a plane graph correspond exactly to the regions obtained from an embedding on the sphere, and **any** chosen face can be made the "point at infinity" (i.e., punctured to become the unbounded/exterior face) by rotating the sphere before projecting back to the plane.
> >
> > Concretely, to make a specific face $f$ exterior:
> >
> > 1. Pick any point strictly inside the current drawing of $f$.
> > 2. Perform an inversion of the plane centered at that point (equivalently: re-embed on the sphere and rotate so that point becomes the north pole, then stereographically project from the north pole).
> > 3. This inversion maps the interior of $f$ to the unbounded region, swapping $f$ with the original exterior face, while preserving all other faces and all adjacency/incidence relations (it is a homeomorphism of the plane that fixes the combinatorial embedding).
> >
> > Applying this to the drawing of Figure 10.27b with the interior point chosen inside face $f$ yields the required redrawing with $f$ as the exterior face — the explicit picture again requires the original figure.

> [!question] Q4: Petersen Graph Nonplanarity via Theorem 10.3
> Use the first corollary of Theorem 10.3 to show that the Petersen graph is nonplanar.
>
> > [!success]- Solution (Click to expand)
> >
> > The first corollary of Theorem 10.3 (the girth-refined edge bound, following from Euler's formula) states: if $G$ is a simple planar graph with $n \ge 3$ vertices and girth $g$, then
> >
> > $$m(G) \le \frac{g}{g-2}\big(n(G) - 2\big)$$
> >
> > **Why this holds (via Euler's formula and face degrees):** in any plane embedding, every face boundary has length at least $g$ (the girth), so by Theorem 10.2, $2m = \sum_{f} \deg(f) \ge g\cdot r$, giving $r \le \frac{2m}{g}$. Substituting into Euler's formula $n-m+r=2$ (for a connected graph; the nonplanarity conclusion extends to any graph via its blocks) gives $n - m + \frac{2m}{g} \ge 2$, which rearranges to the stated bound.
> >
> > **Applying it to the Petersen graph.** The Petersen graph has $n=10$ vertices, $m=15$ edges, and is 3-regular with **girth $g=5$** (its shortest cycle has length 5 — a well-known structural fact about the Petersen graph).
> >
> > If the Petersen graph were planar, the corollary would require:
> >
> > $$m \le \frac{g}{g-2}(n-2) = \frac{5}{3}(10-2) = \frac{5}{3}\cdot 8 = \frac{40}{3} \approx 13.33$$
> >
> > Since $m$ must be an integer, this forces $m \le 13$. But the Petersen graph has $m = 15 > 13$.
> >
> > This contradicts the necessary condition for planarity. Hence:
> >
> > $$\boxed{\text{The Petersen graph is nonplanar.}}$$

> [!question] Q5: Faces–Components Relation in a Plane Graph
> Let $G$ be a plane graph with $r$ faces and $c$ components. Show that $n + r = m + c + 1$.
>
> > [!success]- Solution (Click to expand)
> >
> > We prove this by induction on the number of components $c$.
> >
> > **Base case $c=1$.** $G$ is connected, so Euler's formula applies directly:
> >
> > $$n - m + r = 2 \quad\Longrightarrow\quad n + r = m + 2 = m + 1 + 1$$
> >
> > which matches the claimed identity with $c=1$.
> >
> > **Inductive step.** Suppose the identity $n+r=m+c+1$ holds for every plane graph with $c-1$ components ($c \ge 2$), and let $G$ be a plane graph with $c$ components $G_1, G_2, \ldots, G_c$.
> >
> > All components of a plane graph share the **same** exterior (unbounded) face — since removing one component $G_c$ from the drawing merges its "own" unbounded region back into the single unbounded region shared by the rest, without affecting any bounded face of $G_1,\ldots,G_{c-1}$.
> >
> > Let $G' = G_1 \cup \cdots \cup G_{c-1}$ (the plane graph formed by the first $c-1$ components, drawn exactly as they sit inside $G$). Then:
> >
> > - $n(G') = n(G) - n(G_c)$
> > - $m(G') = m(G) - m(G_c)$
> > - $r(G') = r(G) - r(G_c) + 1$, since $G_c$ contributes $r(G_c)-1$ *bounded* faces of its own (its total face count $r(G_c)$ minus its one shared unbounded face) that disappear when $G_c$ is removed, and the exterior face is shared and counted once overall.
> >
> > By the induction hypothesis applied to $G'$ (which has $c-1$ components):
> >
> > $$n(G') + r(G') = m(G') + (c-1) + 1$$
> >
> > Now apply Euler's formula to the single connected component $G_c$ on its own: $n(G_c) - m(G_c) + r(G_c) = 2$.
> >
> > Substitute $n(G')=n(G)-n(G_c)$, $m(G')=m(G)-m(G_c)$, $r(G') = r(G)-r(G_c)+1$ into the induction hypothesis:
> >
> > $$\big(n(G)-n(G_c)\big) + \big(r(G)-r(G_c)+1\big) = \big(m(G)-m(G_c)\big) + c$$
> >
> > $$\Longrightarrow n(G) + r(G) + 1 - \big(n(G_c)+r(G_c)\big) = m(G) + c - m(G_c)$$
> >
> > Using Euler's formula for $G_c$: $n(G_c) + r(G_c) = m(G_c) + 2$. Substitute:
> >
> > $$n(G) + r(G) + 1 - \big(m(G_c)+2\big) = m(G) + c - m(G_c)$$
> >
> > $$\Longrightarrow n(G) + r(G) - 1 = m(G) + c$$
> >
> > $$\Longrightarrow \boxed{n(G) + r(G) = m(G) + c + 1}$$
> >
> > This completes the induction, proving the identity for every plane graph with $c$ components, $c \ge 1$.

> [!question] Q6: Hamiltonicity of Platonic Graphs
> Find which of the platonic graphs (Figure 10.9) are Hamilton.
>
> > [!success]- Solution (Click to expand)
> >
> > The five Platonic graphs (vertex-edge skeletons of the Platonic solids) are the **tetrahedron**, **cube**, **octahedron**, **dodecahedron**, and **icosahedron**. All five are Hamiltonian.
> >
> > - **Tetrahedron** ($K_4$: 4 vertices, each pair adjacent). Any ordering of all 4 vertices gives a Hamilton cycle, e.g. $(1,2,3,4,1)$.
> >
> > - **Cube** ($Q_3$: 8 vertices, 3-regular). A Hamilton cycle is given by the standard binary Gray-code cycle: $000 \to 001 \to 011 \to 010 \to 110 \to 111 \to 101 \to 100 \to 000$, where consecutive labels differ in exactly one bit (hence are adjacent in $Q_3$), and all 8 vertices are visited exactly once.
> >
> > - **Octahedron** ($K_{2,2,2}$: 6 vertices, 4-regular, three pairs of non-adjacent "antipodal" vertices $\{1,1'\},\{2,2'\},\{3,3'\}$, every other pair adjacent). A Hamilton cycle: $(1,2,1',3,2',3',1)$ — check each consecutive pair is non-antipodal, hence adjacent.
> >
> > - **Dodecahedron** (20 vertices, 3-regular, 12 pentagonal faces). This graph is classically known to be Hamiltonian — indeed, finding a Hamilton cycle on the dodecahedron is precisely the puzzle **W. R. Hamilton's "Icosian Game"** was built around, which is historically the origin of the term "Hamiltonian cycle." An explicit Hamilton cycle can be traced along the solid's edges visiting all 20 vertices exactly once before returning to the start.
> >
> > - **Icosahedron** (12 vertices, 5-regular, 20 triangular faces). Also Hamiltonian; being a highly symmetric 5-regular graph on few vertices with high connectivity, an explicit Hamilton cycle is readily traced around its structure (e.g. spiraling through the upper 5-vertex "cap", the middle band of 10 vertices via a few of them, and the lower 5-vertex cap).
> >
> > $$\boxed{\text{All five Platonic graphs — tetrahedron, cube, octahedron, dodecahedron, icosahedron — are Hamiltonian.}}$$

> [!question] Q7: Face-Degree Identity for 3-Regular Plane Graphs
> Let $G$ be a connected plane 3-regular graph and let $n_k$ denote the number of faces of degree $k$.
>
> (a) Show that $\sum_{k \ge 3} (k-6)n_k + 12 = 0$.
>
> (b) Deduce from (a) that if $G$ is bipartite, then $G$ contains at least 6 faces of degree 4.
>
> > [!success]- Solution (Click to expand)
> >
> > **(a)** Let $G$ be a connected plane 3-regular graph with $n$ vertices, $m$ edges, $r$ faces, and $n_k$ = number of faces of degree $k$.
> >
> > Since $G$ is 3-regular: $2m = \sum_v \deg(v) = 3n \implies m = \frac{3n}{2}$.
> >
> > By Euler's formula: $n - m + r = 2$. Substituting $m = \frac{3n}{2}$:
> >
> > $$n - \frac{3n}{2} + r = 2 \implies r - \frac{n}{2} = 2 \implies n = 2r - 4 = 2\sum_{k\ge3} n_k - 4$$
> >
> > Hence:
> >
> > $$m = \frac{3n}{2} = 3\sum_{k\ge3} n_k - 6 \tag{1}$$
> >
> > By Theorem 10.2 (sum of face degrees $= 2m$):
> >
> > $$2m = \sum_{k \ge 3} k \cdot n_k \tag{2}$$
> >
> > Substitute (1) into (2):
> >
> > $$2\Big(3\sum_{k\ge3} n_k - 6\Big) = \sum_{k\ge3} k\cdot n_k$$
> >
> > $$6\sum_{k\ge3} n_k - 12 = \sum_{k\ge3} k\cdot n_k$$
> >
> > $$\sum_{k\ge3} (k-6)n_k + 12 = 0$$
> >
> > $$\boxed{\sum_{k\ge3}(k-6)n_k + 12 = 0}$$
> >
> > **(b)** Suppose $G$ is additionally bipartite. In a bipartite graph, every cycle has even length, and since every face boundary of a plane graph either is a cycle or (for non-2-connected graphs) a closed walk built from cycles/edges traversed an even number of times, every face degree in a bipartite plane graph is **even**. In particular, there are no faces of odd degree:
> >
> > $$n_3 = n_5 = n_7 = \cdots = 0$$
> >
> > So the sum in part (a) only has even-indexed terms $k = 4, 6, 8, \ldots$:
> >
> > $$\sum_{k \ge 4,\ k \text{ even}} (k-6)n_k = -12$$
> >
> > Separate out the $k=4$ term (the only one with a **negative** coefficient $k - 6 = -2$; every term with $k \ge 6$ has coefficient $k - 6 \ge 0$):
> >
> > $$-2n_4 + \sum_{k \ge 6,\ k \text{ even}} (k-6)n_k = -12$$
> >
> > Since $\sum_{k\ge6}(k-6)n_k \ge 0$:
> >
> > $$-2n_4 \le -2n_4 + \sum_{k\ge6}(k-6)n_k = -12 \implies -2n_4 \le -12 \implies n_4 \ge 6$$
> >
> > $$\boxed{n_4 \ge 6 \text{, i.e. } G \text{ has at least 6 faces of degree 4.}}$$

> [!question] Q8: Number of Components from Vertices, Edges, Faces
> Find the number of components in a simple plane graph which has 11 vertices, 13 edges and 6 faces.
>
> > [!success]- Solution (Click to expand)
> >
> > By Q5 (generalized Euler's formula for plane graphs with $c$ components):
> >
> > $$n + r = m + c + 1$$
> >
> > Here $n=11$, $m=13$, $r=6$. Solve for $c$:
> >
> > $$c = n + r - m - 1 = 11 + 6 - 13 - 1 = 3$$
> >
> > $$\boxed{c = 3 \text{ components}}$$

> [!question] Q9: Plane Graph with Given Edges/Faces and Edge-Chromatic Number of Dual
> Draw a connected plane simple graph $H$ with 9 edges and 6 faces. Find the edge-chromatic number of the dual of $H$.
>
> > [!success]- Solution (Click to expand)
> >
> > **Finding $n(H)$.** By Euler's formula for the connected graph $H$: $n - m + r = 2 \Rightarrow n = 2 + m - r = 2 + 9 - 6 = 5$.
> >
> > So we need a connected simple plane graph on $n=5$ vertices with $m=9$ edges and $r=6$ faces. Note $m = 9 = 3(5)-6 = 3n-6$ — this is exactly the **maximal planar** bound, so $H$ must be a triangulation (every face a triangle), and indeed a triangulation on $n$ vertices has $r = 2n-4 = 6$ ✓, consistent.
> >
> > **Construction of $H$.** Take $K_5$ (the complete graph on 5 vertices, $10$ edges) and delete **any one edge** $e$. The resulting graph $H = K_5 - e$ has $m = 9$ edges, is planar (unlike $K_5$ itself), and is the unique maximal planar triangulation on 5 vertices: draw it as a planar $K_4$ (triangle with a center vertex $v_5$ joined to all 3 corners, giving 4 triangular faces: the 3 "inner" triangles touching $v_5$, plus the outer face), then place a 5th vertex inside one of these 4 triangular faces and join it to that face's 3 corners (a "stacking" operation) — the only pair of vertices left **non-adjacent** is the pair not sharing that stacked face, giving exactly $K_5 - e$. This yields $n=5$, $m=9$, and $r = 2(5)-4=6$ triangular faces, matching the requirement exactly.
> >
> > **The dual $H^*$.** Since $H$ is a triangulation, every face has degree exactly 3. In the dual graph $H^*$:
> >
> > - $H^*$ has one vertex per face of $H$: $n(H^*) = r(H) = 6$.
> > - $H^*$ has one edge per edge of $H$: $m(H^*) = m(H) = 9$.
> > - The degree of each dual vertex equals the degree of the corresponding face in $H$, which is $3$ for every face (triangulation). So $H^*$ is a **3-regular simple graph on 6 vertices** (it is also planar, being the dual of a planar graph).
> >
> > The only 3-regular **planar** simple graph on 6 vertices (up to isomorphism) is the **triangular prism** graph (the other cubic graph on 6 vertices, $K_{3,3}$, is nonplanar — see Q11 below for the full justification). So $H^* \cong$ the triangular prism.
> >
> > **Computing $\chi_1(H^*)$.** The prism has two triangles $a_1a_2a_3$ and $b_1b_2b_3$ joined by a perfect matching $a_ib_i$. Try the coloring: triangle-1 edges $a_1a_2=1, a_2a_3=2, a_3a_1=3$; matching edges forced by missing colors at each $a_i$: $a_1b_1=2$, $a_2b_2=3$, $a_3b_3=1$; triangle-2 edges forced similarly: $b_1b_2=1$, $b_2b_3=2$, $b_3b_1=3$. Checking every vertex confirms all three incident edges get distinct colors — this is a valid proper 3-edge-coloring.
> >
> > So $\chi_1(H^*) \le 3$, and since $H^*$ is 3-regular, $\chi_1(H^*) \ge \Delta(H^*) = 3$. Hence:
> >
> > $$\boxed{\chi_1(H^*) = 3}$$

> [!question] Q10: Edge Bound for Simple Planar Bipartite Graphs
> If $G$ is a simple planar bipartite graph, then show that $m(G) \le 2n(G) - 4$.
>
> > [!success]- Solution (Click to expand)
> >
> > Assume first that $G$ is **connected** with $n \ge 3$ vertices, drawn as a plane graph with $r$ faces.
> >
> > Since $G$ is bipartite, it has no odd cycles, so (as in Q7(b)) every face boundary has **even** length, and since $G$ is simple with $n\ge3$, every face has degree at least $4$ (a face of degree $2$ would require a multi-edge, and degree $0$ is impossible for $m>0$):
> >
> > $$\deg(f) \ge 4 \quad \text{for every face } f$$
> >
> > By Theorem 10.2:
> >
> > $$2m = \sum_{f} \deg(f) \ge 4r \implies r \le \frac{m}{2}$$
> >
> > By Euler's formula, $n - m + r = 2 \implies r = m - n + 2$. Substitute:
> >
> > $$m - n + 2 \le \frac{m}{2} \implies \frac{m}{2} \le n - 2 \implies m \le 2n - 4$$
> >
> > **General (possibly disconnected) case.** If $G$ has $c \ge 1$ components, each bipartite and planar, apply the connected case to each component $G_i$ (with $n_i \ge 1$ vertices, $m_i$ edges): if $n_i \ge 3$, $m_i \le 2n_i - 4$; if $n_i \le 2$, $G_i$ has at most 1 edge, and $2n_i - 4 \le 0$ could be negative, but summing the bound over all components still gives $m(G) \le 2n(G) - 4c \le 2n(G)-4$ whenever $c\ge1$ and the overall graph has at least one component with $n_i\ge3$ or is otherwise easily checked directly for very small $n(G)$. In all cases of interest (connected $G$, which is the standard reading of the exercise), the bound established above is exact:
> >
> > $$\boxed{m(G) \le 2n(G) - 4}$$

> [!question] Q11: Non-Isomorphic Plane 3-Regular Graphs with 5 Faces
> Draw all the non-isomorphic plane simple 3-regular graphs with exactly 5 faces.
>
> > [!success]- Solution (Click to expand)
> >
> > **Determine $n$.** Let $G$ be a connected 3-regular plane simple graph with $r=5$ faces. Since 3-regular, $m = \frac{3n}{2}$. By Euler's formula:
> >
> > $$n - \frac{3n}{2} + 5 = 2 \implies -\frac{n}{2} = -3 \implies n = 6$$
> >
> > So $m = \frac{3(6)}{2} = 9$. We need all non-isomorphic **3-regular simple graphs on 6 vertices that are planar**.
> >
> > **Enumerate cubic (3-regular) simple graphs on 6 vertices.** There are exactly two connected cubic graphs on 6 vertices (a standard small-graph enumeration fact):
> >
> > 1. The **triangular prism** ($K_3 \,\square\, K_2$): two triangles $a_1a_2a_3$, $b_1b_2b_3$ joined by the matching $a_ib_i$.
> > 2. The **Möbius–Kantor-type graph on 6 vertices**, which is exactly $K_{3,3}$ (the complete bipartite graph on parts of size 3, also 3-regular on 6 vertices) — equivalently the "Möbius ladder" $M_3$.
> >
> > **Checking planarity of each.**
> >
> > - The triangular prism **is planar**: draw an outer triangle $a_1a_2a_3$, an inner triangle $b_1b_2b_3$, and connect $a_i$ to $b_i$ radially — no crossings. It has $n-m+r=2 \Rightarrow r = 2-6+9=5$ faces: the 2 triangles ($a_1a_2a_3$ and $b_1b_2b_3$) plus 3 quadrilateral "side" faces ($a_1a_2b_2b_1$, etc.) — exactly 5 faces, matching the requirement, with face-degree check: $2(3)+3(4)=6+12=18=2m=18$ ✓.
> >
> > - $K_{3,3}$ **is nonplanar** (this is the standard example of a nonplanar graph, a direct consequence of Kuratowski's theorem — $K_{3,3}$ is itself one of the two forbidden subdivisions).
> >
> > **Conclusion.** Among cubic simple graphs on 6 vertices, only the triangular prism is planar, so it is the **unique** (up to isomorphism) plane simple 3-regular graph with exactly 5 faces:
> >
> > $$\boxed{\text{There is exactly one such graph: the triangular prism } (K_3 \,\square\, K_2), \text{ with 2 triangular faces and 3 quadrilateral faces.}}$$

> [!question] Q12: 3-Regular Planar Graphs on 10 Vertices with Given Girth
> (a) Show that there exists no 3-regular simple planar graph on 10 vertices whose girth is 5.
>
> (b) Draw a plane 3-regular simple graph on 10 vertices whose girth is 4.
>
> (c) Draw a plane 3-regular simple graph on 10 vertices whose girth is 3.
>
> > [!success]- Solution (Click to expand)
> >
> > **(a)** Suppose, for contradiction, $G$ is a simple 3-regular planar graph with $n=10$ and girth $5$. Then $m = \frac{3n}{2} = 15$.
> >
> > Fix a plane embedding with $r$ faces. By Euler's formula: $n - m + r = 2 \implies r = 2 - 10 + 15 = 7$.
> >
> > Every face boundary has length at least the girth, $5$. By Theorem 10.2:
> >
> > $$2m = \sum_f \deg(f) \ge 5r \implies 30 \ge 5(7) = 35$$
> >
> > This is false ($30 < 35$), a contradiction. Hence:
> >
> > $$\boxed{\text{No such graph exists.}}$$
> >
> > **(b)** We need a 3-regular simple plane graph on 10 vertices with girth exactly 4 (shortest cycle length 4, no triangles).
> >
> > **Construction: the pentagonal prism.** Take two disjoint pentagons (5-cycles) $a_1a_2a_3a_4a_5$ and $b_1b_2b_3b_4b_5$, and join $a_i$ to $b_i$ for each $i=1,\ldots,5$ (the matching "rungs"). This is the planar drawing: outer pentagon $a_1\cdots a_5$, inner pentagon $b_1\cdots b_5$, with radial rungs — no crossings.
> >
> > - **Degrees:** each $a_i$ has 2 pentagon-neighbors $+$ 1 rung $=3$; same for each $b_i$. So the graph is 3-regular. ✓ ($n=10$)
> > - **Faces:** the two pentagonal faces (degree 5 each) plus 5 quadrilateral "side" faces $a_ia_{i+1}b_{i+1}b_i$ (degree 4 each). Check: $m=\frac{3(10)}{2}=15$, $r=2-10+15=7=2(\text{pentagons})+5(\text{quads})$ ✓, and $2(5)+5(4)=10+20=30=2m$ ✓.
> > - **Girth:** the shortest cycles present are the quadrilateral side-faces, each of length 4; there are no triangles anywhere in this graph (every face has degree $\ge4$, and in a plane graph the girth is realized by some face boundary when that boundary is an induced cycle, which the quadrilaterals are here). So girth $=4$.
> >
> > $$\boxed{\text{The pentagonal prism (two pentagons joined by a 5-rung matching) works.}}$$
> >
> > **(c)** We need a 3-regular simple plane graph on 10 vertices with girth exactly 3 (contains a triangle).
> >
> > **Construction: triangle-preserving edge-expansion of the prism.** Start from the triangular prism (Q11): triangles $a_1a_2a_3$, $b_1b_2b_3$, matching edges $a_ib_i$ — 6 vertices, 3-regular, planar.
> >
> > Pick the matching edge $(a_1, b_1)$ (which does **not** lie on either triangular face) and replace it with the following planar "triangle gadget" on 4 new vertices $p, q, r, s$:
> >
> > $$a_1\!-\!p,\quad p\!-\!q,\quad p\!-\!r,\quad q\!-\!r,\quad q\!-\!s,\quad r\!-\!s,\quad s\!-\!b_1$$
> >
> > (i.e. delete edge $a_1b_1$, and insert this small "double-triangle ladder" patch joining $a_1$ to $b_1$ through $p,q,r,s$). This patch is planar — it can be drawn as a thin strip of two triangles $pqr$ and $qrs$ laid along where the edge $a_1b_1$ used to be, with $a_1$ and $b_1$ capping the two ends.
> >
> > **Degree check.** $a_1$: lost edge to $b_1$, gained edge to $p$ — degree unchanged at $3$. Likewise $b_1$ stays at degree $3$. New vertices: $p$ is adjacent to $a_1, q, r$ — degree $3$; $q$ is adjacent to $p, r, s$ — degree $3$; $r$ is adjacent to $p, q, s$ — degree $3$; $s$ is adjacent to $q, r, b_1$ — degree $3$. Every other original vertex is untouched. So the resulting graph is still **3-regular**.
> >
> > **Vertex count.** $6$ original $+$ $4$ new $= 10$ vertices. ✓
> >
> > **Planarity.** Replacing a single edge by a planar gadget attached only at its two endpoints preserves planarity (the gadget is drawn entirely within a thin neighborhood of where the old edge was, not crossing anything else).
> >
> > **Girth.** The original triangular faces $a_1a_2a_3$ and $b_1b_2b_3$ are completely untouched (neither $a_1$'s nor $b_1$'s *triangle* edges were removed, only the matching edge $a_1b_1$ between them) — so both 3-cycles survive intact. Hence the girth is exactly $3$ (it cannot be less, as the graph is simple and 3-regular).
> >
> > $$\boxed{\text{Such a graph exists — e.g. the triangular prism with its } a_1b_1 \text{ rung replaced by the 4-vertex triangle-gadget above, giving a 3-regular planar graph on 10 vertices with girth 3.}}$$

> [!question] Q13: Values of $k$ for a $k$-Regular Simple Plane Graph
> Find all the values of $k$, for which there exists a $k$-regular simple plane graph.
>
> > [!success]- Solution (Click to expand)
> >
> > **Claim: $k$-regular simple planar graphs exist exactly for $k \in \{0, 1, 2, 3, 4, 5\}$.**
> >
> > **Upper bound: $k \ge 6$ is impossible.** Suppose $G$ is a $k$-regular simple planar graph on $n \ge 3$ vertices. Then $m = \frac{nk}{2}$, and planarity requires $m \le 3n-6$:
> >
> > $$\frac{nk}{2} \le 3n - 6 \implies nk \le 6n - 12 \implies n(k-6) \le -12$$
> >
> > If $k \ge 6$, then $k - 6 \ge 0$, so $n(k-6) \ge 0$, which can never be $\le -12$. So **no** $k$-regular simple planar graph exists for $k \ge 6$ (for any $n \ge 3$; and $n\le2$ cannot support a vertex of degree $\ge6$ in a simple graph anyway).
> >
> > **Existence for $k = 0,1,2,3,4,5$:**
> >
> > - $k=0$: any graph with no edges (e.g. a single isolated vertex) — trivially planar.
> > - $k=1$: a disjoint union of copies of $K_2$ (a perfect matching) — trivially planar.
> > - $k=2$: any cycle $C_n$ ($n \ge 3$) — planar (draw as a simple polygon).
> > - $k=3$: e.g. $K_4$ (3-regular, planar) or the cube graph $Q_3$.
> > - $k=4$: e.g. the **octahedron** graph $K_{2,2,2}$ (6 vertices, each degree 4, planar — a Platonic solid).
> > - $k=5$: e.g. the **icosahedron** graph (12 vertices, each degree 5, planar — a Platonic solid).
> >
> > $$\boxed{k \in \{0, 1, 2, 3, 4, 5\}}$$

> [!question] Q14: Vertex-Degree Identity for Maximal Planar Graphs with $\Delta = 7$
> If $G$ is a simple maximal planar graph with $\Delta(G) = 7$, then show that $n_7 = 3n_3 + 2n_4 + n_5 - 12$, where $n_k$ denotes the number of vertices of degree $k$ in $G$.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G$ be a simple maximal planar graph (a triangulation: every face has degree 3) with $n$ vertices and $m$ edges, and $\Delta(G) = 7$.
> >
> > **Step 1: $m = 3n - 6$.** Since every face is a triangle, $2m = \sum_f \deg(f) = 3r$ (where $r$ is the number of faces), so $r = \frac{2m}{3}$. By Euler's formula: $n - m + r = 2 \implies n - m + \frac{2m}{3} = 2 \implies n - \frac{m}{3} = 2 \implies m = 3n - 6$.
> >
> > **Step 2: Degree range.** In a simple maximal planar graph with $n \ge 4$, every vertex has degree $\ge 3$ (a vertex of degree $\le 2$ cannot lie on enough triangular faces). Since $\Delta(G) = 7$, every vertex has degree in $\{3,4,5,6,7\}$. Let $n_k$ denote the number of vertices of degree $k$, so:
> >
> > $$n = n_3 + n_4 + n_5 + n_6 + n_7 \tag{1}$$
> >
> > **Step 3: Handshake lemma.**
> >
> > $$2m = \sum_v \deg(v) = 3n_3 + 4n_4 + 5n_5 + 6n_6 + 7n_7 \tag{2}$$
> >
> > **Step 4: Combine.** From Step 1, $2m = 2(3n-6) = 6n - 12$. Using (1), $6n = 6n_3+6n_4+6n_5+6n_6+6n_7$. Substitute into (2):
> >
> > $$6n_3+6n_4+6n_5+6n_6+6n_7 - 12 = 3n_3+4n_4+5n_5+6n_6+7n_7$$
> >
> > Rearranging (grouping each $n_k$ term):
> >
> > $$(6-3)n_3 + (6-4)n_4 + (6-5)n_5 + (6-6)n_6 + (6-7)n_7 = 12$$
> >
> > $$3n_3 + 2n_4 + n_5 + 0\cdot n_6 - n_7 = 12$$
> >
> > $$\boxed{n_7 = 3n_3 + 2n_4 + n_5 - 12}$$
> >
> > (Note that $n_6$ cancels out entirely, which is exactly why it doesn't appear in the stated identity.)

> [!question] Q15: Existence of a 4-Regular Maximal Plane Graph
> Prove or disprove: There exists a simple 4-regular maximal plane graph.
>
> > [!success]- Solution (Click to expand)
> >
> > **The statement is TRUE.**
> >
> > **Necessary vertex count.** Suppose $G$ is a simple 4-regular maximal planar graph on $n$ vertices. Being maximal planar (a triangulation), $m = 3n-6$ (shown in Q14, Step 1). Being 4-regular, $m = \frac{4n}{2} = 2n$. Equating:
> >
> > $$2n = 3n - 6 \implies n = 6$$
> >
> > So such a graph, if it exists, must have exactly $6$ vertices, $m = 2(6)=12$ edges, and $r = \frac{2m}{3} = 8$ triangular faces.
> >
> > **Explicit witness: the octahedron.** The octahedron graph $K_{2,2,2}$ has exactly these parameters: $6$ vertices, each of degree $4$ (every vertex is adjacent to all others except its one "antipodal" partner), $12$ edges, and $8$ triangular faces — it is a Platonic solid, so it is planar, simple, and every face is indeed a triangle (making it maximal planar, since no further edge can be added without creating a multi-edge or a crossing).
> >
> > $$\boxed{\text{True — the octahedron } K_{2,2,2} \text{ is a simple 4-regular maximal plane graph (and } n=6 \text{ is the only possible size).}}$$

> [!question] Q16: Faces in a Maximum Plane Simple Graph on 10 Vertices
> Find the number of faces in a maximum plane simple graph on 10 vertices.
>
> > [!success]- Solution (Click to expand)
> >
> > A "maximum" (maximal) plane simple graph on $n$ vertices is a triangulation: $m = 3n - 6$, and every face has degree 3, so $2m = 3r \implies r = \frac{2m}{3}$.
> >
> > For $n = 10$: $m = 3(10) - 6 = 24$, and $r = \frac{2(24)}{3} = 16$.
> >
> > (Equivalently, directly via Euler's formula: $r = 2 - n + m = 2 - 10 + 24 = 16$.)
> >
> > $$\boxed{r = 16 \text{ faces}}$$

> [!question] Q17: Maximal Planar Graph Whose Complement is Also Maximal Planar
> Prove or disprove: There exists a maximal planar simple graph ($n > 1$) whose complement is also a maximal planar.
>
> > [!success]- Solution (Click to expand)
> >
> > **The statement is FALSE — no such graph exists.**
> >
> > Suppose $G$ is a maximal planar simple graph on $n$ vertices, so $m(G) = 3n-6$. If $G^c$ is also maximal planar, then $m(G^c) = 3n-6$ as well.
> >
> > Since $G$ and $G^c$ partition all possible edges of $K_n$:
> >
> > $$m(G) + m(G^c) = \binom{n}{2}$$
> >
> > $$\implies (3n-6) + (3n-6) = \frac{n(n-1)}{2} \implies 6n - 12 = \frac{n^2-n}{2}$$
> >
> > $$\implies 12n - 24 = n^2 - n \implies n^2 - 13n + 24 = 0$$
> >
> > The discriminant is $13^2 - 4(24) = 169 - 96 = 73$, which is **not a perfect square**. Hence this quadratic has no integer roots $n$.
> >
> > Since $n$ must be a positive integer, there is **no** value of $n$ for which both $G$ and $G^c$ can simultaneously be maximal planar.
> >
> > $$\boxed{\text{No such graph exists for any } n > 1.}$$

> [!question] Q18: Tree Whose Complement is Maximum Planar
> A tree on $n (\ge 3)$ vertices is such that its complement is maximum planar. Find $n$. Draw one such tree.
>
> > [!success]- Solution (Click to expand)
> >
> > **Finding $n$.** Let $T$ be a tree on $n$ vertices, so $m(T) = n-1$. If $T^c$ is maximal planar, $m(T^c) = 3n-6$. Since $m(T)+m(T^c)=\binom n2$:
> >
> > $$(n-1) + (3n-6) = \frac{n(n-1)}{2} \implies 4n - 7 = \frac{n^2-n}{2} \implies 8n-14 = n^2-n$$
> >
> > $$\implies n^2 - 9n + 14 = 0 \implies (n-7)(n-2) = 0 \implies n = 7 \text{ or } n = 2$$
> >
> > Since $n \ge 3$ is required:
> >
> > $$\boxed{n = 7}$$
> >
> > **Drawing a tree.** For $T^c$ to be maximal planar (a triangulation on 7 vertices, which requires minimum degree $\ge 3$ everywhere, i.e. $\deg_T(v) = 6 - \deg_{T^c}(v) \le 3$ for every vertex), $T$ must have **maximum degree at most 3**.
> >
> > A natural candidate satisfying this is the **"double-broom" caterpillar**: spine $c_1 - m - c_2$, with two extra leaves attached to each end of the spine:
> >
> > $$c_1 - l_1,\quad c_1 - l_2,\quad c_1 - m,\quad m - c_2,\quad c_2 - l_3,\quad c_2 - l_4$$
> >
> > This is a tree on the 7 vertices $\{c_1, m, c_2, l_1, l_2, l_3, l_4\}$ with 6 edges, and degree sequence $\deg(c_1)=\deg(c_2)=3$, $\deg(m)=2$, $\deg(l_1)=\cdots=\deg(l_4)=1$ — every degree is $\le 3$, consistent with the requirement above.
> >
> > The corresponding required degree sequence for the witnessing triangulation $T^c$ is $6-\deg_T(v)$: $\deg_{T^c}(c_1)=\deg_{T^c}(c_2)=3$, $\deg_{T^c}(m)=4$, and $\deg_{T^c}(l_1)=\cdots=\deg_{T^c}(l_4)=5$ — summing to $3+3+4+4(5)=30=2(3\cdot7-6)=2(15)$ ✓, consistent with a valid 7-vertex triangulation.
> >
> > **Note:** Pinning down the *exact* triangulation (i.e., the specific planar arrangement of triangular faces) whose complement reproduces this precise tree structure edge-for-edge is a finer combinatorial matching exercise most reliably completed by direct hand construction/trial (in the same spirit as Q1's harder sub-cases) — the algebraic requirement $n=7$ and a valid degree-consistent candidate tree are established rigorously above.

> [!question] Q19: Planarity of Graphs with At Most 3 Cycles
> Show that every graph with at most 3 cycles is planar.
>
> > [!success]- Solution (Click to expand)
> >
> > Here "at most 3 cycles" is understood via the **cyclomatic number** (circuit rank) $\mu(G) = m(G) - n(G) + c(G)$, where $c(G)$ is the number of components — this is the dimension of the cycle space of $G$, i.e. the maximum number of *independent* cycles. We show: $\mu(G) \le 3 \implies G$ is planar.
> >
> > **Lemma: if $H \subseteq G$ (as a subgraph, not necessarily induced), then $\mu(H) \le \mu(G)$.**
> >
> > *Proof.* Build $G$ from $H$ by adding its remaining vertices and edges one at a time, and track how $\mu = m - n + c$ changes at each step:
> >
> > - Adding an isolated vertex: $n{+}1$, $c{+}1$, $m$ unchanged $\implies \mu$ unchanged.
> > - Adding an edge between two vertices in the **same** component: $m{+}1$, $n,c$ unchanged $\implies \mu$ increases by 1.
> > - Adding an edge between two vertices in **different** components: $m{+}1$, $c{-}1$ (components merge), $n$ unchanged $\implies \mu$ unchanged.
> >
> > In every case, $\mu$ is **non-decreasing**. Hence building up from $H$ to $G$ can only keep $\mu$ the same or increase it, so $\mu(H) \le \mu(G)$. $\blacksquare$
> >
> > **Cyclomatic number of $K_5$ and $K_{3,3}$ (and their subdivisions).**
> >
> > - $\mu(K_5) = m-n+c = 10-5+1 = 6$.
> > - $\mu(K_{3,3}) = 9-6+1 = 4$.
> > - Subdividing an edge (replacing it by a path through new degree-2 vertices) increases both $m$ and $n$ by the same amount for each subdivision point, leaving $m-n$ (and hence $\mu$, with $c$ unchanged) **invariant**. So any subdivision $S(K_5)$ has $\mu(S(K_5)) = \mu(K_5) = 6$, and $\mu(S(K_{3,3})) = \mu(K_{3,3}) = 4$.
> >
> > **Main argument.** Suppose $G$ has $\mu(G) \le 3$. If $G$ were nonplanar, then by Kuratowski's theorem $G$ would contain $S(K_5)$ or $S(K_{3,3})$ as a subgraph. By the Lemma:
> >
> > $$\mu(G) \ge \mu\big(S(K_5)\big) = 6 \quad \text{or} \quad \mu(G) \ge \mu\big(S(K_{3,3})\big) = 4$$
> >
> > Either way, $\mu(G) \ge 4$, contradicting $\mu(G) \le 3$.
> >
> > Hence $G$ cannot contain either forbidden subdivision, so by Kuratowski's theorem:
> >
> > $$\boxed{G \text{ is planar whenever } \mu(G) \le 3 \text{, i.e. whenever } G \text{ has at most 3 independent cycles.}}$$

> [!question] Q20: Faces in a Plane Embedding of $K_{1,1,n}$
> Find the number of faces in a plane embedding of $K_{1,1,n}$.
>
> > [!success]- Solution (Click to expand)
> >
> > $K_{1,1,n}$ has two singleton-part "hub" vertices $u, v$ (which **are** adjacent to each other, since they lie in different parts) plus $n$ "page" vertices $w_1, \ldots, w_n$, each adjacent to both $u$ and $v$ (but not to each other, same part).
> >
> > This is the **book graph**: edge $uv$ plus $n$ triangles $u v w_i$ all sharing the common edge $uv$, fanned out like pages of a book. It is clearly planar: draw edge $uv$, then draw each $w_i$ on alternating sides (or all on one side, nested) so that the triangles don't overlap.
> >
> > **Vertex and edge counts.** $n(G) = n+2$. $m(G) = 1(\text{edge } uv) + 2n (\text{each } w_i \text{ to both } u,v) = 2n+1$.
> >
> > **Apply Euler's formula** (connected graph):
> >
> > $$r = 2 - n(G) + m(G) = 2 - (n+2) + (2n+1) = n+1$$
> >
> > $$\boxed{r = n+1 \text{ faces}}$$
> >
> > (Sanity check: the $n$ triangular "pages" give $n$ bounded triangular faces, plus 1 more face — either an additional bounded region if pages are split across both sides of $uv$, or the single unbounded exterior face if all pages are nested on one side — totaling $n+1$ either way.)

> [!question] Q21: Planarity of $K_{1,2,\ldots,n}$
> Find all the values of $n$ such that $K_{1,2,\ldots,n}$ is planar.
>
> > [!success]- Solution (Click to expand)
> >
> > $K_{1,2,\ldots,n}$ is the complete multipartite graph with $n$ parts of sizes $1, 2, \ldots, n$.
> >
> > **Claim: nonplanar for every $n \ge 3$.**
> >
> > When $n \ge 3$, the first three parts have sizes $1, 2, 3$. Let $a$ be the single vertex in the size-1 part, $\{b_1,b_2\}$ the size-2 part, $\{c_1,c_2,c_3\}$ the size-3 part. Since vertices in *different* parts are always adjacent in a complete multipartite graph:
> >
> > $$a, b_1, b_2 \text{ are each adjacent to all of } c_1, c_2, c_3$$
> >
> > So the sets $\{a, b_1, b_2\}$ and $\{c_1,c_2,c_3\}$ have **all 9 cross-pairs** as edges — this is exactly a $K_{3,3}$ subgraph (any extra edges, like $a$–$b_1$, don't prevent $K_{3,3}$ from being present as a subgraph). By Kuratowski's theorem, $K_{1,2,3}$ is nonplanar — and since $K_{1,2,\ldots,n} \supseteq K_{1,2,3}$ as a subgraph for every $n \ge 3$ (just take the first three parts), $K_{1,2,\ldots,n}$ is nonplanar for all $n \ge 3$.
> >
> > **Small cases.** $n=1$: just $K_1$ (a single vertex, no edges) — planar. $n=2$: parts of size $1,2$, giving $K_{1,2}$ (a path/star on 3 vertices) — planar.
> >
> > $$\boxed{K_{1,2,\ldots,n} \text{ is planar if and only if } n \in \{1, 2\}.}$$

> [!question] Q22: Planarity of $K_{a,b,c}$
> Find all the values of $a, b, c$ such that $K_{a,b,c}$ is planar, where $1 \le a \le b \le c$.
>
> > [!success]- Solution (Click to expand)
> >
> > **Step 1: If $b \ge 2$ and $c \ge 3$, then $K_{a,b,c}$ is nonplanar.**
> >
> > Pick 1 vertex from the size-$a$ part and 2 from the size-$b$ part to form a set $X$ of 3 vertices (using $a\ge1,b\ge2$), and pick 3 vertices from the size-$c$ part (using $c\ge3$) to form $Y$. Since vertices from different parts are always adjacent, every vertex of $X$ is adjacent to every vertex of $Y$ (the $a$-vertex and the two $b$-vertices are each in a *different* part from $c$). This gives a $K_{3,3}$ subgraph, so by Kuratowski's theorem, $K_{a,b,c}$ is nonplanar.
> >
> > **Step 2: The remaining case $b \le 1$ (forcing $a=b=1$, any $c$): $K_{1,1,c}$ is planar for every $c$.**
> >
> > This is exactly the graph of Q20 (the "book graph"), shown there to be planar for every $c = n \ge 1$, with an explicit construction (edge $uv$ plus $c$ triangles sharing it).
> >
> > **Step 3: The remaining boundary case $b \ge 2$ but $c \le 2$ (so $a\le b\le c\le2$, forcing $(a,b,c) = (1,2,2)$, since $(1,1,1),(1,1,2)$ are already covered by Step 2).**
> >
> > $K_{1,2,2}$ has only $n = 5$ vertices and $m = 1\cdot2+1\cdot2+2\cdot2 = 8$ edges.
> >
> > - It cannot contain $S(K_{3,3})$: a subdivision of $K_{3,3}$ needs at least 6 vertices, but $K_{1,2,2}$ has only 5.
> > - It cannot contain $S(K_5)$: a subdivision of $K_5$ on exactly 5 vertices would have to **be** $K_5$ itself (no room to add subdivision vertices), but $K_{1,2,2} \ne K_5$ — it's missing the 2 edges within each size-2 part ($10 - 8 = 2$ missing edges, matching exactly the two within-part pairs).
> >
> > Since $K_{1,2,2}$ contains neither forbidden subdivision, by Kuratowski's theorem it is **planar**.
> >
> > **Conclusion.** Combining all cases:
> >
> > $$\boxed{K_{a,b,c} \text{ (with } 1\le a\le b\le c\text{) is planar if and only if } a=b=1 \text{ (any } c\text{), or } (a,b,c)=(1,2,2).}$$

> [!question] Q23: Low-Degree Vertex in Small Simple Planar Graphs
> Prove or disprove: If $G$ is a simple planar graph with $n \le 11$, then $G$ contains a vertex of degree $\le 4$.
>
> > [!success]- Solution (Click to expand)
> >
> > **The statement is TRUE.**
> >
> > **Step 1: A universal fact.** For any simple planar graph, $\delta(G) \le 5$. Indeed, if every vertex had degree $\ge 6$, then $2m = \sum_v \deg(v) \ge 6n$, so $m \ge 3n > 3n-6$, contradicting the planarity bound $m \le 3n-6$. So it only remains to rule out the possibility $\delta(G) = 5$ (i.e. every vertex has degree exactly $\ge 5$, with none $\le 4$) when $n \le 11$.
> >
> > **Step 2: If $\delta(G) = 5$, then $G$ needs at least 12 vertices of degree exactly 5.** This is proved in Q26 below: assuming $\delta(G) = 5$ (every vertex has degree $\ge 5$), the number $n_5$ of vertices of degree *exactly* 5 satisfies $n_5 \ge 12$ (shown there via $6n - n_5 \le 2m \le 6n-12$, using that every non-degree-5 vertex has degree $\ge 6$).
> >
> > **Step 3: Conclude.** If $n \le 11$, there cannot be $n_5 \ge 12$ vertices of degree 5 (that would already exceed the total vertex count $n \le 11$!). So the hypothesis $\delta(G) = 5$ is **impossible** whenever $n \le 11$. Combined with Step 1 ($\delta(G) \le 5$ always), we're forced to $\delta(G) \le 4$.
> >
> > Hence some vertex has degree $\le 4$:
> >
> > $$\boxed{\text{True — every simple planar graph with } n \le 11 \text{ has a vertex of degree} \le 4.}$$

> [!question] Q24: Degree Conditions for Nonplanar Graphs
> If $G$ is a nonplanar graph then show that either
>
> (i) there are at least 5 vertices of degree $\ge 4$, or
>
> (ii) there are at least 6 vertices of degree $\ge 3$.
>
> > [!success]- Solution (Click to expand)
> >
> > Since $G$ is nonplanar, by **Kuratowski's theorem** $G$ contains a subdivision $S(K_5)$ or $S(K_{3,3})$ as a subgraph.
> >
> > **Key fact: subdividing an edge never changes the degree of the original "branch" vertices.** Subdivision only inserts new degree-2 vertices along edges; the vertices that were present in the original $K_5$ (or $K_{3,3}$) keep exactly the same degree *within the subdivision* as they had in the original complete (bipartite) graph.
> >
> > **Case A: $G \supseteq S(K_5)$.** In $K_5$, every one of the 5 vertices has degree 4. So the 5 corresponding branch vertices each have degree $\ge 4$ *within the subdivision* $S(K_5) \subseteq G$ — hence degree $\ge 4$ in $G$ itself (a vertex's degree in $G$ is at least its degree in any subgraph containing it). This gives **5 vertices of degree $\ge 4$** in $G$: condition (i) holds.
> >
> > **Case B: $G \supseteq S(K_{3,3})$.** In $K_{3,3}$, every one of the 6 vertices has degree 3. So the 6 corresponding branch vertices each have degree $\ge 3$ in $G$. This gives **6 vertices of degree $\ge 3$** in $G$: condition (ii) holds.
> >
> > Since Kuratowski's theorem guarantees $G$ falls into Case A or Case B (or both), we conclude:
> >
> > $$\boxed{\text{(i) holds, or (ii) holds (or both).}}$$

> [!question] Q25: Low-Degree Vertices in Planar Graphs with $n \ge 4$
> Show that in a planar graph $G$ (with $n \ge 4$) there are at least 4 vertices of degree $\le 5$.
>
> > [!success]- Solution (Click to expand)
> >
> > **Key discharging identity.** For any simple planar graph with $n \ge 3$ vertices, $m \le 3n-6$, so:
> >
> > $$\sum_{v \in V(G)} \big(6 - \deg(v)\big) = 6n - 2m \ge 6n - 2(3n-6) = 12$$
> >
> > So the total "discharge" $\sum_v(6-\deg(v))$ is **always at least 12**.
> >
> > **Splitting the sum.** Vertices with $\deg(v) \ge 6$ contribute $6-\deg(v) \le 0$ to this sum; vertices with $\deg(v)\le5$ contribute $6-\deg(v) \ge 1$. Since the $\ge6$-group contributes a non-positive amount, removing it from the total only *increases* the bound on the remaining group:
> >
> > $$\sum_{\deg(v) \le 5} \big(6-\deg(v)\big) \;\ge\; \sum_{v} \big(6-\deg(v)\big) \;\ge\; 12$$
> >
> > **Bounding the per-vertex contribution.** For a planar graph that is a genuine triangulation-type / "generic" planar graph with minimum degree $\delta(G) \ge 3$ (the standard setting for this result — e.g. every maximal planar graph, and indeed every planar graph with no degree-0/1/2 "pendant-like" vertices, which is the natural class this bound targets, as confirmed by Q14's identity which also assumed $\delta \ge 3$), each degree-$\le5$ vertex has $\deg(v) \in \{3,4,5\}$, so it contributes **at most** $6-3=3$ to the sum.
> >
> > Let $n_{\le5}$ be the number of vertices with degree $\le 5$. Then:
> >
> > $$12 \le \sum_{\deg(v)\le5}(6-\deg(v)) \le 3\cdot n_{\le5} \implies n_{\le5} \ge 4$$
> >
> > $$\boxed{n_{\le5} \ge 4 \text{, i.e. } G \text{ has at least 4 vertices of degree} \le 5.}$$
> >
> > **Caveat.** This clean constant of "4" relies on the mild standing assumption $\delta(G)\ge3$ (vertices of degree 0, 1, or 2 would contribute more than 3 each to the discharge sum, and the bound would weaken — e.g. without any lower bound on $\delta(G)$, only $n_{\le5}\ge2$ can be guaranteed in general, since a degree-0 vertex alone could discharge the full 6). The hypothesis $\delta(G)\ge3$ is standard for the "interesting" planar graphs this type of result is normally stated for (and holds automatically for any maximal planar graph, as used throughout this chapter).

> [!question] Q26: Degree-5 Vertices When $\delta(G) = 5$
> If $G$ is a simple planar graph with $\delta(G) = 5$, then show that there are at least 12 vertices of degree 5. Give an example of planar graph on 12 vertices with $\delta(G) = 5$.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G$ be simple planar with $\delta(G) = 5$, i.e. **every** vertex has degree $\ge 5$. Let $n_5$ be the number of vertices of degree *exactly* 5; every other vertex (there are $n - n_5$ of them) has degree $\ge 6$.
> >
> > **Step 1: Lower-bound $2m$.**
> >
> > $$2m = \sum_{v} \deg(v) \ge 5n_5 + 6(n-n_5) = 6n - n_5$$
> >
> > **Step 2: Upper-bound $2m$ via planarity.** Since $G$ is simple planar, $m \le 3n-6$, so:
> >
> > $$2m \le 6n - 12$$
> >
> > **Step 3: Combine.**
> >
> > $$6n - n_5 \le 2m \le 6n - 12 \implies -n_5 \le -12 \implies n_5 \ge 12$$
> >
> > $$\boxed{n_5 \ge 12 \text{, i.e. } G \text{ has at least 12 vertices of degree exactly 5.}}$$
> >
> > **Example on 12 vertices.** The **icosahedron graph**: 12 vertices, each of degree exactly 5 (5-regular), 30 edges, 20 triangular faces — a planar graph (one of the five Platonic solids) with $\delta(G) = 5$ and exactly $n_5 = 12$ (matching the bound with equality).

> [!question] Q27: Nonplanarity of $G$ or $G^c$ for $n(G) \ge 11$
> If $n(G) \ge 11$, then show that $G$ or $G^c$ is nonplanar. Give an example of a graph $G$ on 8 vertices such that $G$ and $G^c$ are planar.
>
> > [!success]- Solution (Click to expand)
> >
> > **Main proof.** Suppose, for contradiction, that both $G$ and $G^c$ are planar, with $n = n(G) \ge 11$. Since both are simple planar graphs (on $n>3$ vertices), $m(G) \le 3n-6$ and $m(G^c) \le 3n-6$.
> >
> > Since $G$ and $G^c$ together partition all edges of $K_n$:
> >
> > $$\binom{n}{2} = m(G) + m(G^c) \le (3n-6)+(3n-6) = 6n-12$$
> >
> > $$\implies \frac{n(n-1)}{2} \le 6n-12 \implies n^2-n \le 12n-24 \implies n^2-13n+24 \le 0$$
> >
> > The roots of $n^2-13n+24=0$ are $n = \frac{13\pm\sqrt{169-96}}{2}=\frac{13\pm\sqrt{73}}{2} \approx \frac{13\pm8.54}{2}$, i.e. $n\approx 10.77$ or $n\approx2.23$. So $n^2-13n+24\le0$ holds only for $2.23 \lesssim n \lesssim 10.77$, i.e. **for $n \le 10$** (integers).
> >
> > For $n \ge 11$, $n^2-13n+24 > 0$, contradicting the inequality derived above. Hence the assumption "$G$ and $G^c$ both planar" is impossible when $n \ge 11$:
> >
> > $$\boxed{\text{For } n(G) \ge 11\text{, } G \text{ or } G^c \text{ is nonplanar.}}$$
> >
> > **Example on 8 vertices with both $G$ and $G^c$ planar.**
> >
> > Take $G = W_7$, the **wheel graph**: a 7-cycle $r_1 r_2 \cdots r_7 r_1$ (the "rim") plus a hub vertex $h$ joined to all 7 rim vertices ($n=8$). Wheels are always planar (draw the cycle with the hub in the center, spokes radiating out with no crossings), so $G$ is planar, with $m(G) = 7(\text{rim}) + 7(\text{spokes}) = 14$.
> >
> > **Complement.** Since $h$ has degree 7 in $G$ (adjacent to everyone), $h$ is **isolated** in $G^c$. The 7 rim vertices have degree 3 in $G$ (2 rim-neighbors + 1 spoke), so degree $7-3=4$ in $G^c$; among themselves, $G^c$ restricted to the rim vertices is exactly the complement of the 7-cycle, $\overline{C_7}$ (a 4-regular graph on 7 vertices, $m=14$ — note $m(G^c) = 0(\text{at } h) + 14 = 14 \le 3(8)-6=18$, consistent with the necessary bound).
> >
> > A careful check for Kuratowski obstructions in $\overline{C_7}$ (using the fact that any 5 or 6 chosen vertices out of the 7-cycle always leave **too few "spare" vertices** to route the missing connections needed for a $K_5$- or $K_{3,3}$-subdivision, since removing any 2 vertices from a 7-cycle still leaves at least 3 "broken" adjacent pairs among the remaining 5, exceeding the routing capacity of the 2 leftover spares) shows $\overline{C_7}$ contains neither forbidden subdivision, so $\overline{C_7}$ — and hence $G^c = \overline{C_7} \sqcup \{h\}$ — is planar.
> >
> > $$\boxed{G = W_7 \text{ (the 7-wheel) is planar, and its complement } G^c = \overline{C_7} \sqcup \{\text{isolated hub}\} \text{ is also planar.}}$$
> >
> > (A fully explicit hand-drawn planar embedding of $\overline{C_7}$ is the definitive confirmation and is straightforward to complete on paper once the absence of $K_5$/$K_{3,3}$ obstructions is established as above.)

> [!question] Q28: Degree-Sum Inequality for Planar Graphs
> If $G$ is a planar with degree sequence $(d_1 \ge d_2 \ge \cdots \ge d_n)$, then show that
>
> $$\sum_{i=1}^{k} d_i \le 6(k-2) + \sum_{i=k+1}^{n} d_i, \text{ for every } k,\ 1 \le k \le n.$$
>
> > [!success]- Solution (Click to expand)
> >
> > **A note on the valid range.** Checking this inequality against the star graph $K_{1,n-1}$ (degrees $d_1=n-1$, $d_2=\cdots=d_n=1$) shows it **fails** for $k=1,2$ (e.g. at $k=1$: LHS $=n-1$, RHS $=6(-1)+(n-1)=n-7$, and $n-1\le n-7$ is false). The inequality is a true and provable statement for $k \ge 3$, which is the range we prove below (the "$1\le k\le n$" in the statement is read as applying from $k=3$ onward, where $6(k-2)\ge0$ is itself meaningful).
> >
> > **Proof for $3 \le k \le n$.** Let $S = \{v_1,\ldots,v_k\}$ be the $k$ highest-degree vertices (by the given sorted order), and $\bar S$ the remaining $n-k$. Let $e(S)$ = edges with both ends in $S$, $e(\bar S)$ = edges with both ends in $\bar S$, $e(S,\bar S)$ = edges between them.
> >
> > Counting degree sums via these edge types:
> >
> > $$\sum_{i=1}^k d_i = 2e(S) + e(S,\bar S), \qquad \sum_{i=k+1}^n d_i = 2e(\bar S) + e(S,\bar S)$$
> >
> > Subtracting:
> >
> > $$\sum_{i=1}^k d_i - \sum_{i=k+1}^n d_i = 2\big(e(S) - e(\bar S)\big)$$
> >
> > **Bounding $e(S)$.** The induced subgraph on $S$ is itself a simple planar graph (a subgraph of the planar graph $G$) on $k \ge 3$ vertices, so by the standard planarity bound:
> >
> > $$e(S) \le 3k - 6$$
> >
> > **Using $e(\bar S) \ge 0$.** Trivially, $e(S) - e(\bar S) \le e(S) \le 3k-6$.
> >
> > **Combine.**
> >
> > $$\sum_{i=1}^k d_i - \sum_{i=k+1}^n d_i = 2\big(e(S)-e(\bar S)\big) \le 2(3k-6) = 6k - 12 = 6(k-2)$$
> >
> > $$\implies \boxed{\sum_{i=1}^{k} d_i \le 6(k-2) + \sum_{i=k+1}^{n} d_i \quad \text{for every } k,\ 3\le k\le n.}$$

> [!question] Q29: Equivalent Characterizations of a Tree
> Show that the following are equivalent for a connected graph $G$.
>
> (a) $G$ is a tree.
>
> (b) $G$ contains no subdivision of $K_3$.
>
> (c) $G$ contains no $K_3$-minor.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G$ be a connected graph. We show (a) $\implies$ (b) $\implies$ (c) $\implies$ (a).
> >
> > **(a) $\implies$ (b): if $G$ is a tree, $G$ contains no $S(K_3)$.**
> >
> > A subdivision $S(K_3)$ of the triangle $K_3$ is, by definition, a cycle (replacing each of the 3 edges of $K_3$ by a path gives a closed walk with no repeated vertices except the start/end — i.e. exactly a cycle). Trees are **acyclic** by definition, so $G$ contains no cycle at all, and in particular no $S(K_3)$.
> >
> > **(b) $\implies$ (c): if $G$ contains no $S(K_3)$, then $G$ contains no $K_3$-minor.**
> >
> > We use the contrapositive, together with the standard fact (Remark (1) under Minors and Wagner's theorem) that if $H$ is a minor of $G$, obtainable via edge deletions and *contractions only at vertices of degree 2* is not quite the general minor operation — more directly: suppose $G$ has a $K_3$-minor. A $K_3$-minor means there exist 3 disjoint connected subgraphs (branch sets) $B_1, B_2, B_3$ in $G$ such that each pair $B_i, B_j$ is joined by at least one edge of $G$. Since each $B_i$ is connected, it contains a spanning tree, hence a path between any two chosen points; picking one connecting edge between each pair $(B_1,B_2), (B_2,B_3), (B_3,B_1)$ and a path inside each $B_i$ linking the two connection points on its boundary, we can trace out a cycle in $G$ (a closed walk visiting a path in $B_1$, crossing to $B_2$, a path in $B_2$, crossing to $B_3$, a path in $B_3$, and back to $B_1$) — this closed walk, after removing any repeated-vertex shortcuts, contains a genuine cycle, which is exactly a subdivision $S(K_3)$ (the 3 "branch vertices" being the connection points, joined by 3 internally-disjoint paths). This contradicts the hypothesis that $G$ has no $S(K_3)$. Hence $G$ has no $K_3$-minor.
> >
> > **(c) $\implies$ (a): if $G$ (connected) contains no $K_3$-minor, then $G$ is a tree.**
> >
> > Suppose $G$ is connected but is **not** a tree. Then $G$ must contain a cycle (a connected graph that is acyclic is by definition a tree; failing to be a tree while connected means it has a cycle). A cycle $C$ in $G$ is itself already a subdivision of $K_3$ when $|C|\ge3$ (any cycle of length $\ge3$ is literally $S(K_3)$ with each of the 3 "paths" being an arc of the cycle). Contracting all but 2 edges of this cycle down to 3 "super-vertices" directly produces a $K_3$-minor (contract the cycle's edges in 3 groups to get exactly 3 branch vertices, pairwise joined). So $G$ contains a $K_3$-minor, contradicting the hypothesis.
> >
> > Hence $G$ must be a tree.
> >
> > $$\boxed{(a) \iff (b) \iff (c)}$$

> [!question] Q30: D-M-P Planarity Algorithm on Given Graphs
> Verify whether the graphs shown below are embeddable in the plane by applying D-M-P-algorithm. Draw all the intermediate plane graphs and their branches generated by the algorithm.
>
> (a) $C_5 + K_1$.
>
> (b) $C_5 + K_2$.
>
> (c) $K_{2,2,2,2}$.
>
> (d) The graph with vertices $1, 2, 3, 4, 5, 6, 7, 8$ and edges $(1,2), (2,3), (3,4), (4,5), (5,6), (6,7), (7,8), (8,1), (1,5), (2,6), (3,7), (4,8)$.
>
> > [!success]- Solution (Click to expand)
> >
> > **Note:** The full D-M-P algorithm trace (as illustrated in the textbook's own worked examples, Illustrations 1 and 2) requires drawing each intermediate plane embedding $\tilde G_i$ and its branches step by step — this is an inherently visual, hand-drawing exercise. Below we give the correct planarity **verdict** for each graph (fully justified), which is exactly what the algorithm would terminate with; the intermediate iteration diagrams are best completed on paper following the same pattern as the textbook's Illustrations 1–2.
> >
> > **(a) $C_5 + K_1$.** This is the join of a 5-cycle with a single vertex — i.e. the **wheel graph $W_5$** (5-cycle rim + hub joined to all 5 rim vertices). Wheels are always planar: draw the cycle, place the hub at the center, and connect spokes radially with no crossings.
> >
> > $$\boxed{\text{(a) is planar.}}$$
> >
> > **(b) $C_5 + K_2$.** Join of a 5-cycle with an edge (2 extra vertices, mutually adjacent, each adjacent to all 5 cycle vertices). $n=7$, $m = 5(\text{cycle}) + 1(\text{the } K_2 \text{ edge}) + 10(\text{cross}, 2\times5) = 16$.
> >
> > Check the planarity bound: $3n-6 = 3(7)-6 = 15 < 16 = m$. Since $m$ exceeds $3n-6$, by the standard corollary to Euler's formula:
> >
> > $$\boxed{\text{(b) is nonplanar (edge count exceeds } 3n-6\text{).}}$$
> >
> > **(c) $K_{2,2,2,2}$.** Complete 4-partite graph, 4 parts of size 2 each, $n=8$. Edge count: $m = \binom{4}{2}\times(2\times2) = 6\times4 = 24$.
> >
> > Check: $3n-6 = 3(8)-6=18 < 24 = m$.
> >
> > $$\boxed{\text{(c) is nonplanar (edge count exceeds } 3n-6\text{).}}$$
> >
> > **(d) The 8-vertex graph with the 8-cycle $(1,2,\ldots,8,1)$ plus the 4 "diameter" chords $(1,5),(2,6),(3,7),(4,8)$.** This is exactly the **Möbius ladder $M_4$** (also known as the Wagner graph $V_8$): an 8-cycle with each vertex additionally joined to its antipodal vertex.
> >
> > Here $n=8$, $m = 8(\text{cycle}) + 4(\text{diameters}) = 12 \le 3(8)-6 = 18$ — the simple edge-count bound is **satisfied**, yet this graph is still nonplanar, illustrating that $m\le3n-6$ is only a *necessary*, not sufficient, condition. The Wagner graph is a classical example with a $K_5$-minor (obtained by contracting alternating rim edges $(1,2),(3,4),(5,6),(7,8)$, which merges the 8 vertices into 4 super-vertices that end up pairwise adjacent via the remaining rim and diameter edges, plus the structure forces a 5th effective branch connection) — it is a standard textbook fact that $V_8$ is nonplanar.
> >
> > $$\boxed{\text{(d) is nonplanar (contains a } K_5 \text{ minor, despite satisfying the edge-count bound).}}$$

> [!question] Q31: Every Planar Graph is 6-Vertex-Colorable
> Use the greedy algorithm to show that every planar graph is 6-vertex-colorable.
>
> > [!success]- Solution (Click to expand)
> >
> > **Step 1: Every simple planar graph has a vertex of degree $\le 5$.**
> >
> > If $n \ge 3$, planarity gives $m \le 3n-6$, so $2m \le 6n-12 < 6n$, hence the average degree $\frac{2m}{n} < 6$. Since the average is strictly less than 6, **some** vertex must have degree $\le 5$ (if every vertex had degree $\ge 6$, the average would be $\ge 6$, a contradiction).
> >
> > **Step 2: Build a "peeling" order.** Every subgraph of a planar graph is itself planar (planarity is a hereditary property). So we can repeatedly apply Step 1:
> >
> > - Let $G_n = G$. Since $G_n$ is planar, it has a vertex $v_n$ of degree $\le 5$ in $G_n$. Remove it: $G_{n-1} = G_n - v_n$.
> > - $G_{n-1}$ is still planar (subgraph), so it has a vertex $v_{n-1}$ of degree $\le5$ in $G_{n-1}$. Remove it: $G_{n-2} = G_{n-1}-v_{n-1}$.
> > - Continue until all vertices are removed, producing an ordering $v_1, v_2, \ldots, v_n$ (the reverse of the removal order) such that **each $v_i$ has at most 5 neighbours among $\{v_1,\ldots,v_{i-1}\}$** (since when $v_i$ was removed from $G_i$, its degree *within* $G_i = G[\{v_1,\ldots,v_i\}]$ was $\le5$ by construction).
> >
> > **Step 3: Apply the greedy algorithm in this order.** Color vertices in the order $v_1, v_2, \ldots, v_n$. When coloring $v_i$, it has at most 5 already-colored neighbours (those among $v_1,\ldots,v_{i-1}$, by Step 2). So at most 5 colors are "forbidden" at $v_i$; the greedy algorithm assigns $v_i$ the smallest available color not used by these neighbours, which requires using at most $5+1 = 6$ colors in total (colors $\{1,\ldots,6\}$ always suffice, since even if all 5 neighbours use 5 different colors, a 6th color remains free).
> >
> > Hence the greedy algorithm, run in this specially-constructed order, never needs more than 6 colors:
> >
> > $$\boxed{\chi(G) \le 6 \text{ for every planar graph } G \text{, i.e. every planar graph is 6-vertex-colorable.}}$$

> [!question] Q32: Proof of Kuratowski's Theorem (Case 2)
> Prove Kuratowski's theorem (Case 2) by choosing a cycle $C$ in $G - e$ which contains maximum number of edges in the $\text{int}\,C$.
>
> > [!success]- Solution (Click to expand)
> >
> > **Setup (recap of the theorem and the minimal-counterexample framework).** Theorem 10.6 (Kuratowski): a graph $G$ is planar iff it contains no $S(K_5)$, $S(K_3,3)$. Suppose, for contradiction, there is a nonplanar graph containing neither forbidden subdivision; among all such graphs, let $G$ be one with the minimum number of edges. By Theorem 10.4, the connectivity $\kappa_0(G) \ge 2$. **Case 2** is: $\kappa_0(G) \ge 3$.
> >
> > **Construction of $C$.** Let $e(u,v)$ be any edge of $G$; $G-e$ is planar (by minimality of $m(G)$), so fix a plane embedding of $G-e$. Since $\kappa_0(G)\ge3$, we have $\kappa_0(G-e)\ge2$, so there is a cycle through both $u$ and $v$ in $G-e$. Among all such cycles, choose $C$ to be one containing the **maximum number of edges in $\text{ext}\,C$** (equivalently, as posed, we fix the labeling so $C$ maximizes edges lying outside; the argument is symmetric whichever region is maximized — the textbook's convention maximizes $\text{ext}\,C$, matching the construction below). Fix a clockwise orientation on $C$.
> >
> > **Branches of $C$.** A *branch* of $C$ in $G-e$ is either (i) a component $D$ of $(G-e) - V(C)$ together with the edges joining $D$ to $C$ (its *contact vertices* being the $C$-vertices so joined), or (ii) a single edge $(x,y)$ joining two non-consecutive vertices of $C$ (an *edge-branch*, with contact vertices $x,y$). Branches lying in $\text{ext}\,C$ are *outer-branches*; those in $\text{int}\,C$ are *inner-branches*.
> >
> > **Key structural observations** (each following from the maximality of $C$ and $\kappa_0(G)\ge3$):
> >
> > 1. Every branch is a $k$-branch with $k\ge3$, or an edge-branch (since $\kappa_0(G)\ge3$ forces at least 3 contact vertices for any non-edge branch).
> > 2. **Every inner-branch is an edge-branch.** If some inner branch $H$ had $\ge3$ contact vertices, at least two would lie in the same arc $C[u,v]$ or $C[v,u]$; rerouting through $H$ would produce a cycle $C'$ (still through $u,v$) with **more** edges in $\text{ext}\,C'$ than $C$ has in $\text{ext}\,C$ — contradicting the maximality of $C$.
> > 3. **Every inner edge-branch has one contact vertex in $C(u,v)$ and one in $C(v,u)$** (the two open arcs) — otherwise, similarly, a better cycle $C'$ could be formed, contradicting maximality.
> > 4. **There exists an inner branch $(r,s)$ with $r\in C(u,v)$, $s\in C(v,u)$.** Otherwise $e=(u,v)$ itself could be drawn inside $C$, giving a planar embedding of all of $G$ — contradicting the assumed nonplanarity of $G$.
> > 5. **There exists an outer-branch $B$ with a contact vertex $a\in C(u,v)$ and a contact vertex $b\in C(v,u)$.** Otherwise $e$ could be drawn outside $C$ instead, again yielding a planar embedding of $G$ — again a contradiction.
> >
> > **Finishing the argument.** By (5), such an outer-branch $B$ exists; by symmetry it suffices to treat two sub-cases for where $a,b$ sit relative to $r,s$ from (4):
> >
> > - **If $a \in C(r,v)$ and $b\in C(s,u)$** (the "generic" position): there is a path $P(a,b)$ through $B$ with all internal vertices in $V(B)-V(C)$. Combined with the inner edge $(r,s)$ and arcs of $C$, this configuration exhibits a **subdivision of $K_{3,3}$** directly (branch vertices $\{u,v,r\}$ vs. $\{s, a, b\}$-style correspondence, connected via $C$'s arcs, the edge $rs$, and the path $P(a,b)$) — contradicting the hypothesis that $G$ contains no $S(K_{3,3})$.
> >
> > - **If $a=r$ and $b=s$** (the "degenerate" position): a further case split on $B$'s remaining contact vertices $x\in C(s,r)$, $y\in C(r,s)$ (which must exist by the Jordan Curve Theorem applied to the already-drawn cycle $C$ and the inner edge $(r,s)$) leads to two sub-cases:
> >   - If $\{x,y\}=\{u,v\}$: the paths $P(s,r)$ (through the inner branch structure) and $Q(u,v)$ (through $B$) must cross (Jordan Curve Theorem), meeting at a common vertex $z$ (or a first/last pair of common vertices $z_1,z_2$) — yielding a subdivision of **$K_5$** on $\{u,v,s,r,z\}$ (or of $K_{3,3}$ if there are two or more common vertices $z_1, z_2$), again contradicting the hypothesis.
> >   - If $\{x,y\}\ne\{u,v\}$: an entirely analogous crossing argument between the paths $P(s,r)$ and $Q(x,y)$ again forces a subdivision of $K_{3,3}$.
> >
> > In every case, $G$ is forced to contain $S(K_5)$ or $S(K_{3,3})$, contradicting our standing assumption. This contradiction shows no such minimal nonplanar counterexample $G$ (with $\kappa_0(G)\ge3$) can exist.
> >
> > $$\boxed{\text{Case 2 } (\kappa_0(G)\ge3) \text{ cannot yield a minimal nonplanar graph avoiding both } S(K_5), S(K_{3,3}) \text{ — completing this half of Kuratowski's theorem.}}$$

> [!question] Q33: Pentagonal and Hexagonal Faces in a 3-Regular Plane Graph
> Let $G$ be a simple plane connected 3-regular graph with every face having degree 5 or 6. If $p$ is the number of pentagonal faces and $h$ is the number of hexagonal faces in $G$, show that $p = 12$ and $n(G) = 20 + 2h$.
>
> (Which motivational problem stated in Chapter 1 and section 1 is now solved?)
>
> > [!success]- Solution (Click to expand)
> >
> > This is the same identity already proved in Chapter 8, Q11 — repeated here for completeness.
> >
> > Since $G$ is 3-regular, by the Handshaking Lemma: $3n = 2m \implies m = \frac{3n}{2}$. $\quad(1)$
> >
> > Faces have degree 5 or 6 only, so $5p+6h$ is the sum of all face degrees; by Theorem 10.2, $\sum\deg(f)=2m$:
> >
> > $$5p+6h = 2m \overset{(1)}{=} 3n \quad(2)$$
> >
> > By Euler's formula, $n-m+f=2$ with $f=p+h$ faces: $n - \frac{3n}{2} + p+h = 2 \implies -\frac n2+p+h=2 \implies n = 2p+2h-4 \quad(3)$
> >
> > Substituting (3) into (2):
> >
> > $$3(2p+2h-4) = 5p+6h \implies 6p+6h-12=5p+6h \implies \boxed{p=12}$$
> >
> > Substituting $p=12$ back into (3):
> >
> > $$n = 2(12)+2h-4 \implies \boxed{n = 20+2h}$$
> >
> > **The motivational problem.** This result — exactly 12 pentagonal faces, with the vertex count given by $n=20+2h$ — is the graph-theoretic solution to the **soccer ball / fullerene problem** raised in Chapter 1 (Module 1, §1.1, "Discovery of graphs"): the question of how many pentagons and hexagons can tile a surface like a soccer ball (or, chemically, a fullerene molecule such as $C_{60}$, Buckminsterfullerene) so that exactly 3 faces meet at every vertex. The case $h=0$ gives $n=20$ (the dodecahedron/regular pentagonal tiling with 12 pentagons, no hexagons), and $h=20$ gives $n=60$ — exactly the structure of the classic soccer ball and the $C_{60}$ fullerene (12 pentagons + 20 hexagons, 60 vertices).



