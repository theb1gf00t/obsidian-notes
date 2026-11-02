
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
>
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

> [!question] Q3: Bounds on the Chromatic Number
> **For every graph $G$, show that:**
>
> $$\frac{n(G)}{\alpha_0(G)} \le \chi(G) \le n(G) + 1 - \alpha_0(G)$$

> [!question] Q4: Graphs with $\chi(G) = k$
> **Show that every graph with $\chi(G) = k$ contains:**
>
> 1. At least $\frac{k(k - 1)}{2}$ edges.
> 2. A cycle of length at least $k$.

> [!question] Q5: Number of Vertices in Mycielski Graphs
> **Find $n(G_k)$, where $G_k$ is the $k$-vertex-chromatic, triangle-free graph constructed using Mycielski’s method**.

> [!question] Q6: Maximum Edges in a 4-Chromatic Graph
> **Draw a graph having maximum number of edges with $\chi(G) = 4$ and $n(G) = 10$**.

> [!question] Q7: Greedy Coloring of the $P_2 \square P_4$ Ladder Graph
> **Let $G$ be the graph shown in the text ($P_2 \square P_4$ ladder graph). Order the vertices of $G$ in 3 different ways, say $S_1, S_2,$ and $S_3$, so that the greedy algorithm:**
>
> 1. Uses 2 colors, if $S_1$ is the input.
> 2. Uses 3 colors, if $S_2$ is the input.
> 3. Uses 4 colors, if $S_3$ is the input.

> [!question] Q8: Greedy Coloring of the Crown Graph $K_{4,4} - 4e$
> **Order the vertices of the graph shown in the text (crown graph $K_{4,4} - 4e$) in such a way that the greedy algorithm uses 4 colors**.

> [!question] Q9: Greedy Coloring of $k$-Degenerate Graphs
> **Let $G$ be a simple graph such that $\delta(H) \le k$, for every subgraph $H$ of $G$ (such a graph is called a $k$-degenerate graph). Order the vertices of $G$ so that if one applies the greedy algorithm to color the vertices of $G$, then it uses at most $k + 1$ colors**.

> [!question] Q10: Chemical Storage Problem
> **There are 7 chemicals $A, B, C, D, E, F, G$. For safety reasons, the following pairs of chemicals cannot be stored in one room:** $A\&B, A\&C, A\&G, B\&C, B\&D, C\&D, D\&E, D\&F, E\&F, E\&G, F\&G$. **If the problem is to find the minimum number of rooms (say $k$) required to store all the chemicals, how would you model it as a graph theoretical problem and find $k$?**

_(Note: A graph $G$ is said to be $k$-critical if $\chi(G) = k$, and $\chi(H) < k$ for every proper subgraph $H$ of $G$.)_

> [!question] Q11: Properties of $k$-Critical Graphs
> **If $G$ is $k$-critical, then show that $G$ is connected and that $\delta(G) \ge k - 1$**.

> [!question] Q12: Chromatic Number of $G - S$
> **If $S$ is a set of independent vertices in a $k$-critical graph, then what is the chromatic number of $G - S$?**

> [!question] Q13: Critical Graphs and Joins
> **If $G_1$ and $G_2$ are simple graphs, show that $G_1 + G_2$ is a critical graph iff $G_1$ and $G_2$ are critical**.

_(Note: A partition $(V_1, V_2, \dots, V_p)$ of $V(G)$ is called a clique partition of $G$ if every induced subgraph $[V_i]$, $1 \le i \le p$, is a clique in $G$. The minimum integer $k$ such that $G$ admits a clique partition is called the clique partition number of $G$, denoted by $\theta_0(G)$.)_

> [!question] Q14: Clique Partition Number
> **Show that:**
>
> 1. $\theta_0(G) = \chi(G^c)$.
> 2. $\theta_0(G_1 + G_2) = \max{\theta_0(G_1), \theta_0(G_2)}$.
> 3. $\theta_0(G) \ge \alpha_0(G)$.

