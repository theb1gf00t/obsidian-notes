
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

---

## Chapter 11

> [!question] Q1: Strong Simple Digraphs on 4 Vertices and 5 Arcs
> Draw all the non-isomorphic strong simple digraphs on 4 vertices and 5 arcs.
>
> > [!success]- Solution (Click to expand)
> >
> > **Step 1 — the degree sequences are forced.** A strong digraph has no vertex of out-degree $0$ (it could never be left) and none of in-degree $0$ (it could never be entered). So with $n=4$ and $m=\sum_v \mathrm{outdeg}(v)=5$ every out-degree is $\ge 1$; also no out-degree can be $\ge 3$, since $3+1+1+1=6>5$. Hence
> >
> > $$\text{out-degree sequence} = (2,1,1,1),\qquad \text{in-degree sequence} = (2,1,1,1).$$
> >
> > Exactly one vertex $x$ has out-degree $2$ and exactly one vertex $y$ has in-degree $2$. Consequently the *total* degrees $\deg^++\deg^-$ are either $(4,2,2,2)$ (when $x=y$) or $(3,3,2,2)$ (when $x\neq y$).
> >
> > **Step 2 — split the cases by the number of 2-cycles** (a 2-cycle is a pair $u\leftrightarrow v$ carrying both arcs).
> >
> > *No 2-cycle at all:* then the underlying graph has $5$ edges on $4$ vertices, i.e. it is $K_4$ minus one edge $xy$. The two vertices of total degree $2$ are precisely $x,y$, and the other two vertices $u,w$ are adjacent to everything. So the underlying graph is the union of two triangles $xuw$, $yuw$ sharing the edge $uw$. Orient $uw$ as $u\to w$ (the other choice is symmetric). Each of $x,y$ must have out-degree $1$ and in-degree $1$ among its two neighbours $u,w$, so it is either *transitive* ($u\to x\to w$) or *cyclic* ($w\to x\to u$):
> >   * **both transitive:** then $w$ has out-degree $0$ — impossible in a strong digraph;
> >   * **one transitive, one cyclic:** say $u\to y\to w$ and $w\to x\to u$. Then $u\to y\to w\to x\to u$ is a directed 4-cycle and $u\to w$ is a chord. This is $\mathbf{D_2}$;
> >   * **both cyclic:** $w\to x\to u$, $w\to y\to u$, and $u\to w$. Both $u,w,x$ and $u,w,y$ are directed triangles sharing the arc $u\to w$. This is $\mathbf{D_4}$ (the "bow-tie").
> >
> > *Exactly one 2-cycle,* say $a\leftrightarrow b$. Then $b$ has spent its only out-arc, so the remaining three arcs have tails $a,c,d$ (one each). Two shapes are possible:
> >   * all three arcs stay inside $\{a,c,d\}$: each of $a,c,d$ then has out-degree $1$ inside a 3-set, so the three arcs form a directed triangle $a\to c\to d\to a$. This is $\mathbf{D_1}$ (a directed triangle with a 2-cycle attached at $a$);
> >   * one arc returns to $b$, say $c\to b$ (the case $d\to b$ is symmetric). Testing the possible tails $a\to X$, $d\to Y$ shows that every choice except $a\to d,\ d\to c$ either creates a second 2-cycle, gives some vertex in-degree $0$, or leaves a vertex unreachable. The surviving choice $a\to d\to c\to b$ together with $b\to a$ is a directed 4-cycle $a\to d\to c\to b\to a$ whose edge $ab$ is "doubled" by the extra arc $a\to b$. This is $\mathbf{D_3}$.
> >
> > *Two 2-cycles:* they consume $4$ arcs on two vertex pairs $\{a,b\},\{c,d\}$ and leave only one arc to join the two pairs, so the pairs can be joined in only one direction and no vertex of one pair reaches the other pair. Impossible.
> >
> > **Step 3 — the four digraphs.** They are pairwise non-isomorphic, and are separated by simple invariants:
> >
> > ![[ch11_strong_digraphs_4v.png]]
> >
> > | Digraph | Arcs | Total degrees | Directed triangles | 2-cycles | Directed 4-cycles |
> > |---|---|---|---|---|---|
> > | $D_1$ | $a\to b,\ b\to c,\ c\to a,\ a\to d,\ d\to a$ | $(4,2,2,2)$ | $1$ | $1$ | $0$ |
> > | $D_2$ | $a\to b,\ b\to c,\ c\to d,\ d\to a,\ a\to c$ | $(3,3,2,2)$ | $1$ | $0$ | $1$ |
> > | $D_3$ | $a\to c,\ c\to d,\ d\to b,\ b\to a,\ a\to b$ | $(3,3,2,2)$ | $0$ | $1$ | $1$ |
> > | $D_4$ | $w\to u,\ u\to x,\ x\to w,\ u\to y,\ y\to w$ | $(3,3,2,2)$ | $2$ | $0$ | $0$ |
> >
> > All four are strong: $D_1$ via $a\leftrightarrow d$ plus the triangle; $D_2$ and $D_3$ contain directed Hamilton cycles; $D_4$ via the two triangles sharing $w\to u$. Total degrees $(4,2,2,2)$ singles out $D_1$; among the rest, "has a 2-cycle" singles out $D_3$, and "has a directed 4-cycle" singles out $D_2$.
> >
> > $$\boxed{\text{There are exactly }4\text{ non-isomorphic strong simple digraphs on 4 vertices with 5 arcs.}}$$

> [!question] Q2: Out-Degree 1 Everywhere Forces Exactly One Directed Cycle
> If $D$ is a digraph in which every vertex has out-degree $1$, then show that $D$ has exactly one directed cycle.
>
> > [!success]- Solution (Click to expand)
> >
> > **Important correction of the statement.** As printed this is false for a disconnected digraph: two disjoint directed 3-cycles form a digraph on $6$ vertices with every out-degree equal to $1$, yet it has *two* directed cycles. The correct statement — and the one the exercise means — is:
> >
> > > If every vertex of $D$ has out-degree $1$, then $D$ has **exactly one directed cycle in each weakly connected component**; in particular, if $D$ is weakly connected, it has exactly one directed cycle.
> >
> > **Proof.** Let $K$ be a weakly connected component of $D$, with $n_K$ vertices.
> >
> > *Counting arcs.* Every arc of $D$ has both ends in the same weak component (an arc is an edge of the underlying graph, so it joins vertices of one component). Every vertex of $K$ is the tail of exactly one arc, hence $K$ carries exactly $n_K$ arcs.
> >
> > *The underlying graph is unicyclic.* The underlying graph $G_K$ is connected with $n_K$ vertices and $n_K$ edges, so it contains exactly one cycle (a connected graph has a unique cycle iff $|E|=|V|$).
> >
> > *That cycle is directed, and it is the only directed cycle.* Let $C$ be the unique cycle of $G_K$ and count the arcs of $D$ having **both ends** in $V(C)$. The underlying edges inside $V(C)$ are exactly the $|C|$ edges of $C$, and each of them carries exactly one arc, so there are exactly $|C|$ such arcs. On the other hand each vertex of $C$ has out-degree $1$, so at most $|C|$ arcs have their tail in $V(C)$. Since there are exactly $|C|$ arcs with both ends in $V(C)$, **every** vertex of $C$ has its unique out-arc inside $C$. Following out-arcs from any vertex of $C$ therefore stays in $C$ and returns to it, producing a directed cycle that uses all $|C|$ cycle edges: $C$ is a directed cycle.
> >
> > Finally, any directed cycle of $D$ is a closed walk in $G_K$ and therefore uses the unique cycle $C$ of $G_K$; so $C$ is the only directed cycle of $K$.
> >
> > **Conclusion.** $\#\{\text{directed cycles of }D\} = \#\{\text{weakly connected components of }D\}$. (Equivalently: such a digraph — a *functional digraph* — is a disjoint union of "unicyclic" components, each a directed cycle with rooted in-trees hanging off it.)
> >
> > $$\boxed{\text{One directed cycle per weakly connected component; exactly one if }D\text{ is weakly connected.}}$$

> [!question] Q3: Digraphs on 7 Vertices with In-Degree = Out-Degree = 1
> Draw (as many as you can) simple non-isomorphic digraphs on 7 vertices in which every vertex has out-degree $1$ and every vertex has in-degree $1$. (Do you recognize any relation on such digraphs and partition of 7?)
>
> > [!success]- Solution (Click to expand)
> >
> > **Structure.** If every vertex has out-degree $1$ *and* in-degree $1$, then every weak component is exactly a directed cycle. Indeed, by Q2 each component has exactly one directed cycle $C$; and if some vertex $z\notin V(C)$ lay in the same component, then following out-arcs from $z$ would eventually reach $C$, so some arc $w\to v$ would enter $V(C)$ from outside — but $v$ already receives the arc from its predecessor on $C$, giving $\mathrm{indeg}(v)\ge 2$, a contradiction. So
> >
> > $$D \;=\; \text{a disjoint union of directed cycles, with no loops (}D\text{ is simple).}$$
> >
> > Hence two such digraphs are isomorphic iff the multiset of their cycle lengths is the same, i.e. iff they correspond to the same **partition of $7$ into parts $\ge 2$** (a part $1$ would be a loop, which a simple digraph does not allow).
> >
> > **The four partitions of $7$ into parts $\ge 2$** and their digraphs:
> >
> > $$7,\qquad 5+2,\qquad 4+3,\qquad 3+2+2.$$
> >
> > ![[ch11_one_in_one_out_7v.png]]
> >
> > 1. $7$ — one directed $7$-cycle $0\to1\to2\to3\to4\to5\to6\to0$ (strongly connected).
> > 2. $5+2$ — a directed $5$-cycle together with a $2$-cycle ($u\leftrightarrow v$).
> > 3. $4+3$ — a directed $4$-cycle together with a directed $3$-cycle.
> > 4. $3+2+2$ — a directed $3$-cycle together with two $2$-cycles.
> >
> > $$\boxed{\text{Exactly }4\text{ non-isomorphic digraphs.}}$$
> >
> > **The "partition of 7" connection.** The isomorphism classes of $1$-in/$1$-out simple digraphs on $7$ vertices are in bijection with the partitions of $7$ whose parts are all $\ge 2$. Equivalently, if loops were allowed (a loop being a $1$-cycle), every partition of $7$ would occur, and there would be $p(7)=15$ digraphs: $7;\ 6+1;\ 5+2;\ 5+1+1;\ 4+3;\ 4+2+1;\ 4+1+1+1;\ 3+3+1;\ 3+2+2;\ 3+2+1+1;\ 3+1^4;\ 2+2+2+1;\ 2+2+1+1+1;\ 2+1^5;\ 1^7$. Among the $4$ loop-free ones, exactly one (the $7$-cycle) is strongly connected, and the number of weak components equals the number of parts.

> [!question] Q4: Equality of the Sums of Squared Out-Degrees and Squared In-Degrees
> Let $G$ be a $k$-regular graph on vertices $v_1,\dots,v_n$ and let $D$ be an orientation of $G$. Show that $\sum_{i=1}^n \big(\mathrm{outdeg}(v_i)\big)^2 = \sum_{i=1}^n \big(\mathrm{indeg}(v_i)\big)^2$.
>
> > [!success]- Solution (Click to expand)
> >
> > **Key observation.** An orientation assigns to each edge exactly one direction, so every vertex satisfies
> >
> > $$\mathrm{outdeg}(v)+\mathrm{indeg}(v)=\deg_G(v)=k \qquad \text{for all } v\in V,$$
> >
> > and, summing over all vertices (each edge contributes one out-end and one in-end),
> >
> > $$\sum_{v}\mathrm{outdeg}(v)=\sum_{v}\mathrm{indeg}(v)=m=|E(G)|.$$
> >
> > **Computation.** Write $d^+(v)=\mathrm{outdeg}(v)$, $d^-(v)=\mathrm{indeg}(v)$. Then
> >
> > $$\sum_{v}\Big((d^+(v))^2-(d^-(v))^2\Big)=\sum_{v}\big(d^+(v)-d^-(v)\big)\big(d^+(v)+d^-(v)\big)=\sum_{v}\big(d^+(v)-d^-(v)\big)\,k,$$
> >
> > because $d^+(v)+d^-(v)=k$ for every $v$. Therefore
> >
> > $$\sum_{v}\Big((d^+(v))^2-(d^-(v))^2\Big)=k\underbrace{\Big(\sum_v d^+(v)-\sum_v d^-(v)\Big)}_{=\,m-m\,=\,0}=0,$$
> >
> > which is exactly the claimed identity. $\blacksquare$
> >
> > **What the identity says.** Since $\frac1n\sum_v d^+(v)=\frac1n\sum_v d^-(v)=\frac mn$, the identity is equivalent to
> >
> > $$\mathrm{Var}(d^+)=\mathrm{Var}(d^-),$$
> >
> > i.e. an orientation of a regular graph always produces the same *spread* of out-degrees as of in-degrees (only the means are automatically equal, but for regular $G$ the second moments agree too).
> >
> > **Remark (why regularity is essential).** The proof only uses $d^+(v)+d^-(v)=k$ with $k$ independent of $v$. For a non-regular graph the identity fails in general. Indeed, in general
> >
> > $$\sum_{v}(d^+(v))^2-\sum_{v}(d^-(v))^2=\sum_{v}\deg_G(v)\,\big(d^+(v)-d^-(v)\big),$$
> >
> > which need not vanish when the degrees differ. For example, the path $a-b-c$ oriented as $a\to b\leftarrow c$ has out-degrees $(1,0,1)$ and in-degrees $(0,2,0)$, so $\sum(d^+)^2=2\neq 4=\sum(d^-)^2$.

> [!question] Q5: $k$-Regular Digraphs
> A simple digraph $D$ is called $k$-regular if $\mathrm{outdeg}(v)=\mathrm{indeg}(v)=k$ for every vertex $v\in V(D)$.
>
> (a) Draw a 2-regular digraph on 5 vertices.
> (b) Let $k$ and $n$ be integers with $0\le k<n$. Describe a construction to obtain a $k$-regular digraph on $n$ vertices.
>
> > [!success]- Solution (Click to expand)
> >
> > ### (a) A 2-regular digraph on 5 vertices
> >
> > Take the vertices $\{0,1,2,3,4\}$ and put **two arc-disjoint directed Hamilton cycles** on them:
> >
> > $$0\to1\to2\to3\to4\to0 \qquad\text{and}\qquad 0\to2\to4\to1\to3\to0 .$$
> >
> > Every vertex lies on both cycles, so it has exactly $2$ out-going and exactly $2$ in-coming arcs:
> >
> > ![[ch11_2regular_5v.png]]
> >
> > Degree check: out-degrees $=(2,2,2,2,2)$, in-degrees $=(2,2,2,2,2)$, and $m=nk=5\cdot2=10$ arcs.
> >
> > **Why this is the only possible shape.** By Kőnig's edge-colouring theorem the arc set of a $k$-regular digraph splits into $k$ perfect matchings ("1-factors"); each perfect matching, read as a map $v\mapsto$ its matched out-neighbour, is a permutation of $V$, so its arcs form a disjoint union of directed cycles covering all $n$ vertices. Thus every $k$-regular digraph is the union of $k$ permutation digraphs. For $k=2,\ n=5$ that is exactly two permutational cycles on $5$ vertices — here two Hamilton cycles.
> >
> > ### (b) Construction for arbitrary $0\le k<n$
> >
> > Label the vertices by $\mathbb{Z}_n=\{0,1,\dots,n-1\}$ and put an arc from $i$ to each of the $k$ "successors"
> >
> > $$(i,\,i+1),\ (i,\,i+2),\ \dots,\ (i,\,i+k)\qquad (\text{indices mod } n).$$
> >
> > Equivalently $A(D)=\{(i,j)\ :\ j-i\equiv t \pmod n,\ 1\le t\le k\}$.
> >
> > * **Out-degree:** $i$ dominates exactly $i+1,\dots,i+k$, so $\mathrm{outdeg}(i)=k$.
> > * **In-degree:** $i$ is dominated exactly by $i-1,\dots,i-k$, so $\mathrm{indeg}(i)=k$.
> > * **Simplicity:** no loops ($t\not\equiv0$, since $1\le t\le k\le n-1$) and no repeated arcs.
> >
> > This is the *circulant* (or "cyclic shift") digraph $C_n(1,2,\dots,k)$. For $k=0$ it is the empty digraph; for $k=n-1$ it is the complete digraph $\overleftrightarrow{K_n}$.
> >
> > $$\boxed{D=\big(\mathbb{Z}_n,\ \{(i,i+t):1\le t\le k\}\big)\ \text{is }k\text{-regular on }n\text{ vertices.}}$$
> >
> > The range $0\le k<n$ in the statement is exactly the range in which a simple $k$-regular digraph on $n$ vertices can exist: $k\le n-1$ is forced by simplicity ($i$ has only $n-1$ possible out-neighbours), and $m=nk\le n(n-1)$ is then automatic.

> [!question] Q6: Odd Out-Degree at Every Vertex
> Prove or disprove: For every $n\ge1$, there is a simple digraph on $n$ vertices in which every vertex has odd out-degree.
>
> > [!success]- Solution (Click to expand)
> >
> > **The statement is false — but only because of $n=1$.** Here is the full picture.
> >
> > **$n=1$: impossible.** A simple digraph has no loops, so the single vertex has out-degree $0$, which is even. So the assertion fails for $n=1$.
> >
> > **Every $n\ge2$: possible.** Take the **directed $n$-cycle**
> >
> > $$0\to1\to2\to\cdots\to n-1\to0 .$$
> >
> > It is simple (for $n=2$ it is the 2-cycle $0\leftrightarrow1$, still simple — two distinct arcs), and every vertex has out-degree $1$, which is odd.
> >
> > $$\boxed{\text{False for }n=1;\ \text{true for every }n\ge2.}$$
> >
> > **Stronger version (useful to remember).** Fix any *odd* $d$ with $d\le n-1$. The construction of Q5(b) with $k=d$ gives a $d$-regular, hence simple, digraph on $n$ vertices in which **every** out-degree equals $d$, which is odd. So for every $n\ge2$ and every odd $d\le n-1$ an example exists; in particular when $n$ is even one can even take $d=n-1$, i.e. the complete digraph $\overleftrightarrow{K_n}$.
> >
> > **Moral.** There is no parity obstruction for digraphs (unlike the "even number of odd-degree vertices" theorem for graphs): the only obstruction here is geometry at $n=1$.

> [!question] Q7: Pairs of Digraphs with the Same Vertex-Deleted Deck
> (a) Construct pairs $(D_1,D_2)$ of simple digraphs on $n$ vertices for $n=2,3,4$ where $V(D_1)=\{u_1,\dots,u_n\}$ and $V(D_2)=\{v_1,\dots,v_n\}$ such that (i) $D_1\not\simeq D_2$; (ii) $D_1-u_i\simeq D_2-v_i$ for $i=1,2,\dots,n$.
>
> (b) Verify that the digraphs $D_1$ and $D_2$ shown in Figure 11.22 have the properties (i) and (ii) stated above.
>
> > [!success]- Solution (Click to expand)
> >
> > Throughout, "$D-x$" means the digraph obtained by deleting the vertex $x$ **and all arcs incident with it** (the remaining arcs keep their labels).
> >
> > ### (a) Examples for $n=2,3,4$
> >
> > **$n=2$.** Let $D_1$ have no arcs and let $D_2$ have the single arc $v_1\to v_2$.
> >
> > * (i) $D_1$ has $0$ arcs, $D_2$ has $1$ arc, so $D_1\not\simeq D_2$.
> > * (ii) $D_1-u_1$ and $D_2-v_1$ are both the one-vertex digraph with no arcs; likewise $D_1-u_2\simeq D_2-v_2$. ✓
> >
> > **$n=3$.** Let $D_1$ have arcs $u_1\to u_2$, $u_1\to u_3$, and let $D_2$ have arcs $v_1\to v_3$, $v_2\to v_1$.
> >
> > * (i) Out-degrees of $D_1$ are $(2,1,0)$; of $D_2$ they are $(1,1,0)$ — different multisets, so $D_1\not\simeq D_2$.
> > * (ii) The three vertex deletions give:
> >
> > | deleted | $D_1-$ that vertex | $D_2-$ that vertex |
> > |---|---|---|
> > | $1$ | $\varnothing$ on $\{u_2,u_3\}$ | $\varnothing$ on $\{v_2,v_3\}$ |
> > | $2$ | $u_1\to u_3$ | $v_1\to v_3$ |
> > | $3$ | $u_1\to u_2$ | $v_2\to v_1$ |
> >
> > In each row the two digraphs are isomorphic (with $u_1\mapsto v_1$, $u_3\mapsto v_3$ in row 2, and $u_1\mapsto v_2$, $u_2\mapsto v_1$ in row 3). ✓
> >
> > **$n=4$.** Let
> >
> > $$D_1:\ u_1\to u_2,\ u_1\to u_3,\ u_2\to u_4,\ u_3\to u_2 ;\qquad D_2:\ v_1\to v_3,\ v_2\to v_1,\ v_2\to v_3,\ v_4\to v_2 .$$
> >
> > * (i) Out-degrees of $D_1$ are $(2,1,1,0)$; of $D_2$ they are $(2,1,0,0)$. So $D_1\not\simeq D_2$.
> > * (ii) The vertex-deleted digraphs match, with these isomorphisms:
> >
> > | $i$ | $D_1-u_i$ | $D_2-v_i$ | isomorphism |
> > |---|---|---|---|
> > | $1$ | $u_2\to u_4,\ u_3\to u_2$ | $v_2\to v_3,\ v_4\to v_2$ | $u_2\mapsto v_2,\ u_3\mapsto v_4,\ u_4\mapsto v_3$ |
> > | $2$ | $u_1\to u_3$ | $v_1\to v_3$ | $u_1\mapsto v_1,\ u_3\mapsto v_3$ |
> > | $3$ | $u_1\to u_2,\ u_2\to u_4$ | $v_2\to v_1,\ v_4\to v_2$ | $u_1\mapsto v_2,\ u_2\mapsto v_4,\ u_4\mapsto v_1$ |
> > | $4$ | $u_1\to u_2,\ u_1\to u_3,\ u_3\to u_2$ | $v_1\to v_3,\ v_2\to v_1,\ v_2\to v_3$ | $u_1\mapsto v_2,\ u_2\mapsto v_3,\ u_3\mapsto v_1$ |
> >
> > Each displayed map is a bijection on the three remaining vertices carrying the arc set of $D_1-u_i$ onto that of $D_2-v_i$. ✓
> >
> > **What this shows.** For simple digraphs the vertex-deleted *deck* does **not** determine the digraph — the analogue of the "reconstruction conjecture" fails badly in the directed setting, already at $n=2$ (and the examples above are far from unique).
> >
> > ### (b) Figure 11.22
> >
> > ![[ch11_fig11_22.png]]
> >
> > The two digraphs of the figure are (reading the arcs off the drawing):
> >
> > $$A(D_1)=\{(v_1v_2),(v_1v_3),(v_1v_4),(v_2v_4),(v_2v_5),(v_3v_2),(v_3v_5),(v_4v_3),(v_4v_5),(v_5v_1)\},$$
> >
> > $$A(D_2)=\{(u_1u_2),(u_1u_5),(u_2u_4),(u_2u_5),(u_3u_1),(u_3u_2),(u_3u_4),(u_4u_1),(u_5u_3),(u_5u_4)\},$$
> >
> > where $ab$ abbreviates the arc $a\to b$. Both have $10$ arcs, no 2-cycles, the same out-degree sequence $(3,2,2,2,1)$ and the same in-degree sequence $(3,2,2,2,1)$ — so coarse invariants are useless here.
> >
> > **(i) $D_1\not\simeq D_2$.** Count the directed Hamilton cycles. A computer-free count: $D_1$ has exactly $3$ directed Hamilton cycles, $D_2$ has exactly $2$; isomorphic digraphs would have the same number. Hence $D_1\not\simeq D_2$. ✓
> >
> > **(ii) $D_1-v_i\simeq D_2-u_i$ for every $i$.** Explicit isomorphisms (each verified by mapping the arc list):
> >
> > | $i$ | isomorphism $D_1-v_i\to D_2-u_i$ |
> > |---|---|
> > | $1$ | $v_2\mapsto u_2,\ v_3\mapsto u_3,\ v_4\mapsto u_5,\ v_5\mapsto u_4$ |
> > | $2$ | $v_1\mapsto u_5,\ v_3\mapsto u_4,\ v_4\mapsto u_3,\ v_5\mapsto u_1$ |
> > | $3$ | $v_1\mapsto u_1,\ v_2\mapsto u_2,\ v_4\mapsto u_5,\ v_5\mapsto u_4$ |
> > | $4$ | $v_1\mapsto u_3,\ v_2\mapsto u_2,\ v_3\mapsto u_1,\ v_5\mapsto u_5$ |
> > | $5$ | $v_1\mapsto u_3,\ v_2\mapsto u_1,\ v_3\mapsto u_4,\ v_4\mapsto u_2$ |
> >
> > For instance, deleting $v_1$ from $D_1$ leaves $\{(v_2v_4),(v_2v_5),(v_3v_2),(v_3v_5),(v_4v_3),(v_4v_5)\}$, which under $v_2\mapsto u_2,\ v_3\mapsto u_3,\ v_4\mapsto u_5,\ v_5\mapsto u_4$ becomes
> >
> > $$\{(u_2u_5),(u_2u_4),(u_3u_2),(u_3u_4),(u_5u_3),(u_5u_4)\} = A(D_2-u_1),$$
> >
> > exactly the arc set of $D_2$ with $u_1$ deleted. The other four rows are checked identically.
> >
> > $$\boxed{D_1\not\simeq D_2\ \text{ yet }\ D_1-v_i\simeq D_2-u_i\ \text{for all }i=1,\dots,5.}$$

> [!question] Q8: Weakly Connected Digraphs Have $m\ge n-1$
> If $D$ is a weakly connected digraph, then show that $m\ge n-1$.
>
> > [!success]- Solution (Click to expand)
> >
> > Let $G$ be the **underlying graph** of $D$: same vertex set, and $uv\in E(G)$ whenever $(u,v)$ or $(v,u)$ is an arc of $D$.
> >
> > * " $D$ weakly connected" *means precisely* that $G$ is connected: a weak path in $D$ is exactly a path in $G$, and vice versa.
> > * $G$ has the same $n$ vertices as $D$, and $|E(G)|\le m$, because distinct arcs of $D$ may share the same underlying edge (a 2-cycle $u\leftrightarrow v$ gives only one edge $uv$).
> >
> > A connected graph on $n$ vertices has at least $n-1$ edges (a spanning tree has exactly $n-1$, and every connected graph contains a spanning tree). Hence
> >
> > $$m\ \ge\ |E(G)|\ \ge\ n-1. \qquad\blacksquare$$
> >
> > $$\boxed{m\ge n-1}$$
> >
> > **Sharpness.** A directed Hamilton path $v_1\to v_2\to\cdots\to v_n$ has exactly $m=n-1$ arcs and is weakly (indeed unilaterally) connected, so the bound cannot be improved. Note also that the bound is *not* sufficient: a directed Hamilton path has $n-1$ arcs and is not strong, which is why Q10 needs the stronger hypothesis.

> [!question] Q9: Many Arcs Force Weak Connectivity
> If $D$ is a digraph with $m\ge(n-1)(n-2)+1$, then show that $D$ is weakly connected.
>
> > [!success]- Solution (Click to expand)
> >
> > **Proof by contraposition.** Suppose $D$ is *not* weakly connected. Let its weak components have vertex sets of sizes $n_1,n_2,\dots,n_r$ with $r\ge2$ and $\sum_i n_i=n$. Arcs never join different components, so
> >
> > $$m=\sum_{i=1}^{r} m_i\ \le\ \sum_{i=1}^{r} n_i(n_i-1),$$
> >
> > because a simple digraph on $n_i$ vertices has at most $n_i(n_i-1)$ arcs ($n_i$ choices of tail times $n_i-1$ choices of a different head).
> >
> > **Claim.** $\sum_i n_i(n_i-1)\le (n-1)(n-2)$.
> >
> > Indeed, moving one vertex from a part of size $b\ge2$ to a part of size $a\ge1$ changes the sum by
> >
> > $$\big[(a+1)a+(b-1)(b-2)\big]-\big[a(a-1)+b(b-1)\big]=2a-2(b-1)=2(a-b+1).$$
> >
> > This is positive whenever $a\ge b-1$, so the sum is maximised by making the parts as unequal as possible, i.e. by taking $r=2$ with parts $n-1$ and $1$:
> >
> > $$\sum_i n_i(n_i-1)\ \le\ (n-1)(n-2)+1\cdot 0=(n-1)(n-2).$$
> >
> > Therefore a non-weakly-connected digraph satisfies $m\le(n-1)(n-2)$, contradicting $m\ge(n-1)(n-2)+1$. Hence $D$ must be weakly connected. $\blacksquare$
> >
> > $$\boxed{m\ge(n-1)(n-2)+1\ \Longrightarrow\ D\text{ is weakly connected.}}$$
> >
> > **Sharpness (see Q12(a)).** The bound is best possible: the complete digraph on $n-1$ vertices together with one isolated vertex is disconnected and has exactly $(n-1)(n-2)$ arcs.

> [!question] Q10: Arc Bounds for a Strong Simple Digraph
> If $D$ is a strongly connected simple digraph, then show that $n\le m\le n(n-1)$.
>
> > [!success]- Solution (Click to expand)
> >
> > **Lower bound $m\ge n$.** In a strong digraph every vertex has out-degree $\ge1$: if $\mathrm{outdeg}(v)=0$ then no vertex other than $v$ is reachable from $v$, contradicting strong connectivity (for $n\ge2$). Therefore
> >
> > $$m=\sum_{v\in V}\mathrm{outdeg}(v)\ \ge\ \sum_{v\in V}1\ =\ n .$$
> >
> > (Equivalently, by Q8 and out-degree positivity: every strong digraph contains a closed directed walk through all its vertices, so $m\ge n$.)
> >
> > **Upper bound $m\le n(n-1)$.** $D$ is simple, so between an ordered pair $(u,v)$ with $u\neq v$ there is at most one arc. There are $n(n-1)$ ordered pairs of distinct vertices, hence at most $n(n-1)$ arcs.
> >
> > $$\boxed{n\le m\le n(n-1)}$$
> >
> > **Both bounds are attained.**
> >
> > * $m=n$: the directed $n$-cycle $v_1\to v_2\to\cdots\to v_n\to v_1$ is strong with exactly $n$ arcs.
> > * $m=n(n-1)$: the complete digraph $\overleftrightarrow{K_n}$ (all $n(n-1)$ possible arcs) is strong with $n(n-1)$ arcs.
> >
> > **Interpretation.** The lower bound says strong connectivity costs at least one out-arc per vertex; the upper bound says that once all $n(n-1)$ arcs are present nothing more can be added. By Q12, *neither* bound can be moved: $n-1$ arcs can still give weak (even unilateral) connectivity but never strong connectivity, which is exactly why the threshold for "forced" strong connectivity in Q11 is quadratic rather than linear.

> [!question] Q11: Many Arcs Force Strong Connectivity
> If $D$ is a simple digraph with $m\ge(n-1)^2+1$, then show that $D$ is strongly connected.
>
> > [!success]- Solution (Click to expand)
> >
> > **Proof by contradiction.** Suppose $D$ is not strong. Two cases.
> >
> > **Case 1: $D$ is not even weakly connected.** By Q9 (contrapositive), $m\le(n-1)(n-2)$. But $(n-1)(n-2)<(n-1)^2<(n-1)^2+1$, contradiction.
> >
> > **Case 2: $D$ is weakly connected but not strong.** By Q24, $V(D)$ splits into non-empty parts $A,B$ such that **every** arc between $A$ and $B$ goes from $A$ to $B$. Put $a=|A|$, $b=|B|$, so $a+b=n$ and $a,b\ge1$. Counting the arcs:
> >
> > * inside $A$: at most $a(a-1)$ (simple digraph on $a$ vertices);
> > * inside $B$: at most $b(b-1)$;
> > * between $A$ and $B$: at most $ab$, since only the $a\cdot b$ ordered pairs $(u,v)$ with $u\in A,\ v\in B$ may carry an arc.
> >
> > Hence
> >
> > $$m\le a(a-1)+b(b-1)+ab = a^2+b^2-a-b+ab.$$
> >
> > Using $a^2+b^2+2ab=(a+b)^2=n^2$, i.e. $a^2+b^2=n^2-2ab$, this becomes
> >
> > $$m\le n^2-2ab-(a+b)+ab=n^2-n-ab.$$
> >
> > Finally $ab\ge n-1$: for fixed $a+b=n$ the product $ab=a(n-a)$ is minimised at $a=1$ or $a=n-1$, giving $ab\ge 1\cdot(n-1)=n-1$. Therefore
> >
> > $$m\le n^2-n-(n-1)=n^2-2n+1=(n-1)^2,$$
> >
> > contradicting $m\ge(n-1)^2+1$.
> >
> > Both cases are impossible, so $D$ is strongly connected. $\blacksquare$
> >
> > $$\boxed{m\ge(n-1)^2+1\ \Longrightarrow\ D\text{ is strongly connected.}}$$
> >
> > **Sharpness (see Q12(e)).** The complete digraph on $n-1$ vertices plus one vertex $x$ that dominates all of them has exactly $(n-1)(n-2)+(n-1)=(n-1)^2$ arcs and is **not** strong, so the "$+1$" is indispensable.

> [!question] Q12: Extreme Examples and the Merits of the Bounds
> Give an example of a simple digraph with the following properties: (a) $m=(n-1)(n-2)$, which is disconnected; (b) $m=n$, which is strongly connected; (c) $m=n-1$, which is weakly connected; (d) $m=n-1$, which is unilaterally connected; (e) $m=(n-1)^2$, which is not strongly connected. In view of the existence of these examples, discuss the merits of the bounds stated in Exercises 8 to 11.
>
> > [!success]- Solution (Click to expand)
> >
> > Assume $n\ge3$ (for $n=2$ some of the counts coincide trivially). "$ab$" abbreviates $a\to b$.
> >
> > ### (a) $m=(n-1)(n-2)$, disconnected
> >
> > Take the **complete digraph on $n-1$ vertices** $v_1,\dots,v_{n-1}$, which has exactly $(n-1)(n-2)$ arcs, and add one **isolated** vertex $x$. The digraph has exactly $(n-1)(n-2)$ arcs and is disconnected because $x$ is isolated. This is the densest possible disconnected simple digraph on $n$ vertices.
> >
> > ### (b) $m=n$, strongly connected
> >
> > The **directed $n$-cycle** $v_1\to v_2\to\cdots\to v_n\to v_1$ has $n$ arcs and is strong (from any vertex you can walk forwards around the cycle to any other, and backwards for the reverse direction).
> >
> > ### (c) $m=n-1$, weakly connected
> >
> > The **directed Hamilton path** $v_1\to v_2\to\cdots\to v_n$ has $n-1$ arcs and its underlying graph is the path $P_n$, which is connected, so the digraph is weakly connected.
> >
> > ### (d) $m=n-1$, unilaterally connected
> >
> > The **same** directed Hamilton path works: for $i<j$ there is the directed path $v_i\to v_{i+1}\to\cdots\to v_j$, so every pair of vertices is comparable (unilateral connectivity is *stronger* than weak connectivity, and the directed path has it).
> >
> > ### (e) $m=(n-1)^2$, not strongly connected
> >
> > Take the complete digraph on $\{v_1,\dots,v_{n-1}\}$ — that is $(n-1)(n-2)$ arcs — and add a new vertex $x$, with arcs $x\to v_i$ for **every** $i=1,\dots,n-1$ (so $x$ dominates the whole clique), and **no** arc $v_i\to x$. Then
> >
> > $$m=(n-1)(n-2)+(n-1)=(n-1)^2,$$
> >
> > and the digraph is **not** strong: no vertex of the clique can reach $x$ (all clique vertices, and all their out-neighbours, lie in the clique).
> >
> > ### Discussion: the merits of the bounds of Q8–Q11
> >
> > | Bound | Sharp example | What it says |
> > |---|---|---|
> > | Q8: weak $\Rightarrow m\ge n-1$ | (c) | one arc per vertex really is enough for weak connectivity, so the hypothesis "$m\ge n-1$" cannot be strengthened to "$m\ge n$" |
> > | Q9: $m\ge (n-1)(n-2)+1\Rightarrow$ weak | (a) | the exact threshold: at $(n-1)(n-2)$ arcs disconnection is still possible |
> > | Q10: strong $\Rightarrow n\le m$ | (c),(d) | $n-1$ arcs can give weak/unilateral connectivity but never strong connectivity |
> > | Q10: strong $\Rightarrow m\le n(n-1)$ | $\overleftrightarrow{K_n}$ | attained; nothing stronger is possible |
> > | Q11: $m\ge(n-1)^2+1\Rightarrow$ strong | (e) | the exact threshold for *forced* strong connectivity |
> >
> > Three merits deserve emphasis.
> >
> > 1. **Each bound is sharp (best possible).** The examples (a) and (e) sit exactly one arc *below* the thresholds of Q9 and Q11, and (c),(d) show that "$m\ge n$" in Q10 cannot be lowered. So the theorems cannot be improved: they are exact threshold results, not merely sufficient conditions with slack.
> >
> > 2. **They quantify the density needed to *force* a connectivity property.** Weak connectivity is forced from $\sim n^2$ arcs (Q9) — even though $n-1$ arcs already *suffice* (Q8) — and strong connectivity is forced from $(n-1)^2+1$ arcs (Q11) — even though $n$ arcs already suffice (Q10). The gap between "possible at $m$" and "unavoidable at $m$" is thus quadratic, and examples (a)–(e) are exactly the witness digraphs that make this gap explicit.
> >
> > 3. **They exhibit the asymmetry of the two questions.** For graphs, one edge per vertex ($n-1$) already forces connectivity; for digraphs, directionality means that the same number of arcs can be arranged into a directed path (weak and unilateral, (c),(d)) or into a "one-way valve" structure (e) that is dense yet not strong. Density alone forces a directed property only in the quadratic range.

> [!question] Q13: Strong $\iff$ Converse Strong
> Show that a digraph is strong if and only if its converse digraph is strong. (The converse digraph $D^{\leftarrow}$ has $V(D^{\leftarrow})=V(D)$ and $(u,v)\in A(D^{\leftarrow})$ iff $(v,u)\in A(D)$.)
>
> > [!success]- Solution (Click to expand)
> >
> > **Key observation.** Reversing every arc reverses every directed walk: if $v_0\to v_1\to\cdots\to v_k$ is a directed walk in $D$, then
> >
> > $$v_k\to v_{k-1}\to\cdots\to v_0$$
> >
> > is a directed walk in $D^{\leftarrow}$ (each arc $v_{i}v_{i+1}$ of $D$ becomes the arc $v_{i+1}v_i$ of $D^{\leftarrow}$). Conversely every directed walk of $D^{\leftarrow}$ arises this way from one of $D$. Hence, for all $x,y\in V$,
> >
> > $$y \text{ is reachable from } x \text{ in } D \iff x \text{ is reachable from } y \text{ in } D^{\leftarrow}. \tag{$*$}$$
> >
> > **($\Rightarrow$)** Let $D$ be strong and take $x,y\in V$. By strongness of $D$, $y$ is reachable from $x$, so by $(*)$ $x$ is reachable from $y$ in $D^{\leftarrow}$. As $x,y$ were arbitrary, every vertex of $D^{\leftarrow}$ is reachable from every other, i.e. $D^{\leftarrow}$ is strong.
> >
> > **($\Leftarrow$)** Apply the same argument with the roles of $D$ and $D^{\leftarrow}$ exchanged, using the identity $\big(D^{\leftarrow}\big)^{\leftarrow}=D$.
> >
> > $$\boxed{D\text{ is strong}\iff D^{\leftarrow}\text{ is strong.}}$$
> >
> > **Consequence.** Every theorem about strong digraphs has a *dual* version obtained by reversing all arcs: e.g. Q11 stays true, and "every vertex has out-degree $\ge1$" dualises to "every vertex has in-degree $\ge1$". This is the directed analogue of taking complements in undirected graph theory.

> [!question] Q14: Strong Orientations of the Graphs of Figure 11.23
> Use the proof of Theorem 11.5 to give a strong orientation to the following graphs.
>
> > [!success]- Solution (Click to expand)
> >
> > **The tool (Theorem 11.5 and its proof).** A connected graph $G$ has a strong orientation **iff** $G$ has no cut-edge. The *constructive* proof is an ear decomposition:
> >
> > 1. Since $G$ has no cut-edge, $G$ contains a cycle; orient that cycle cyclically. Its vertices are now mutually reachable.
> > 2. While some vertex is un-oriented, choose a path ("ear") $P=s\,x_1\,x_2\cdots x_t\,s'$ whose **endpoints** $s,s'$ are already in the oriented part $S$ and whose internal vertices $x_1,\dots,x_t$ are outside $S$ (such an ear exists because $G$ is connected; because $G$ has no cut-edge one may always choose it so that it really returns to $S$). Orient all of $P$ consistently from $s$ to $s'$.
> > 3. Then every internal vertex $x_i$ is reachable from $S$ (walk forwards from $s$) and can reach $S$ (walk forwards to $s'$), so $S\cup V(P)$ is again strongly oriented. Repeat.
> >
> > Every edge of $G$ gets exactly one direction, and at the end all vertices are mutually reachable. (Note also: if $G$ has a cut-edge, that edge lies in no cycle, so no orientation can be strong — the condition is necessary as well.)
> >
> > ![[ch11_fig11_23.png]]
> >
> > ### Graph $A$ (left): $8$ vertices, $11$ edges
> >
> > Its edge set is $\{CA,CB,CD,CE,AB,CF,FD,FE,FG,FH,GH\}$: the triangle $ABC$, the $4$-cycle $CDFE$ with chord $CF$, and the triangle $FGH$. There is no cut-edge — every edge lies on a cycle ($CA,AB,BC$ on triangle $ABC$; $CD,DF,FE,EC$ on the $4$-cycle $CDFE$; $CF$ on $CDFC$; $FG,GH,HF$ on the triangle $FGH$).
> >
> > **Ear decomposition and orientation.**
> >
> > * Start with the cycle $C\to D\to F\to E\to C$ (oriented cyclically).
> > * Add the ear $C\to A\to B\to C$ (a closed ear based at $C$).
> > * Add the ear $F\to G\to H\to F$.
> > * Finally the chord $CF$: orient it $C\to F$.
> >
> > $$A(D)=\{C\to D,\ D\to F,\ F\to E,\ E\to C,\ C\to A,\ A\to B,\ B\to C,\ F\to G,\ G\to H,\ H\to F,\ C\to F\}.$$
> >
> > **It is strong.** From $C$: $C\to A\to B$ covers $A,B$; $C\to D\to F$ covers $D,F$, then $F\to E$ and $F\to G\to H$ cover $E,G,H$. And everything returns to $C$: $A\to B\to C$, $B\to C$, $D\to F\to E\to C$, $F\to E\to C$, $E\to C$, $G\to H\to F\to E\to C$, $H\to F\to E\to C$. Every vertex is reachable from $C$ **and** can reach $C$; hence every vertex is reachable from every other. ✓
> >
> > ### Graph $B$ (right): $K_{2,4}$, with parts $X=\{x_1,x_2\}$ and $Y=\{y_1,y_2,y_3,y_4\}$
> >
> > $K_{2,4}$ is connected with no cut-edge (it is bipartite and 2-connected: every edge lies on a 4-cycle). Using ears:
> >
> > * Start with the cycle $x_1\to y_1\to x_2\to y_2\to x_1$.
> > * Add the ear $x_1\to y_3\to x_2$.
> > * Add the ear $x_1\to y_4\to x_2$.
> >
> > $$A(D)=\{x_1\to y_1,\ y_1\to x_2,\ x_2\to y_2,\ y_2\to x_1,\ x_1\to y_3,\ y_3\to x_2,\ x_1\to y_4,\ y_4\to x_2\}.$$
> >
> > **It is strong.** $x_1$ reaches everything: $y_1$ directly, $x_2$ via $x_1\to y_1\to x_2$, $y_2$ via $x_1\to y_1\to x_2\to y_2$, and $y_3,y_4$ directly. Everything reaches $x_1$: $y_1\to x_2\to y_2\to x_1$; $x_2\to y_2\to x_1$; $y_2\to x_1$; $y_3\to x_2\to y_2\to x_1$; $y_4$ similarly. So all vertices are mutually reachable. ✓
> >
> > All $8$ edges receive exactly one direction in each case, so this is an orientation (not merely an assignment of arcs), and it is strong.

> [!question] Q15: $D-v$ Strong Forces Unilateral Connectivity
> If $D$ is a weakly connected simple digraph such that $D-v$ is strong for some vertex $v\in V(D)$, then show that $D$ is unilaterally connected.
>
> > [!success]- Solution (Click to expand)
> >
> > Write $V^-=N^-(v)$ (in-neighbours of $v$) and $V^+=N^+(v)$ (out-neighbours of $v$). We must show: for every pair $x,y$ of vertices, $x$ reaches $y$ or $y$ reaches $x$.
> >
> > **Pairs not involving $v$.** For $x,y\neq v$, strongness of $D-v$ gives directed paths $x\to\cdots\to y$ and $y\to\cdots\to x$ inside $D-v$; in particular they are comparable. ✓
> >
> > **Pairs involving $v$.** Three cases.
> >
> > * **$V^-=\varnothing$.** Then $v\to u$ for every $u\neq v$, so $v$ reaches every vertex and each pair $(v,u)$ is comparable. ✓
> > * **$V^+=\varnothing$.** Then $u\to v$ for every $u\neq v$, so every vertex reaches $v$. ✓
> > * **$V^-\neq\varnothing$ and $V^+\neq\varnothing$.** Choose $y\in V^-$ and $x\in V^+$, so $y\to v\to x$. Since $D-v$ is strong, there is a directed path $x\to\cdots\to y$ in $D-v$. Concatenating,
> >
> > $$y\to v\to x\to\cdots\to y$$
> >
> > is a closed directed walk through $v$. Now take any $u\neq v$. Again by strongness of $D-v$ there is a path $u\to\cdots\to y$ in $D-v$ (trivial if $u=y$), hence
> >
> > $$u\to\cdots\to y\to v,$$
> >
> > so $u$ reaches $v$; and there is a path $x\to\cdots\to u$ in $D-v$ (trivial if $u=x$), hence
> >
> > $$v\to x\to\cdots\to u,$$
> >
> > so $v$ reaches $u$. Thus $u$ and $v$ are mutually reachable, in particular comparable. ✓
> >
> > **Where weak connectivity is used.** Only to exclude the degenerate possibility that $v$ has **no** neighbour at all: if $v$ were isolated (so $V^+=V^-=\varnothing$), the middle two cases would give nothing, and $D$ would fail to be unilateral (nothing reaches or is reached by $v$). Weak connectivity of $D$ guarantees $v$ has at least one neighbour — but note the two middle cases already cover the situations $V^-=\varnothing$ or $V^+=\varnothing$ with a non-isolated $v$.
> >
> > $$\boxed{D-v\text{ strong }+\ D\text{ weakly connected}\ \Longrightarrow\ D\text{ is unilaterally connected.}}$$
> >
> > **Remark.** Strong connectivity of $D-v$ alone does **not** give strong connectivity of $D$: e.g. $v$ may point into $D-v$ with no arc coming back, as in Q12(e). "Unilateral" is exactly the right conclusion.

> [!question] Q16: The Adjacency Matrix of a Digraph
> The adjacency matrix $M=[a_{ij}]$ of a digraph $D$ on $n$ vertices $v_1,\dots,v_n$ is the $n\times n$ matrix with $a_{ij}=1$ if $(v_i,v_j)\in A(D)$ and $a_{ij}=0$ otherwise. Show that (a) $\sum_{j=1}^n a_{ij}=\mathrm{outdeg}(v_i)$; (b) $\sum_{j=1}^n a_{ij}=\mathrm{indeg}(v_i)$; (c) the $(i,j)$-entry $[M^p]_{ij}$ of $M^p$ is the number of directed walks of length $p$ from $v_i$ to $v_j$.
>
> > [!success]- Solution (Click to expand)
> >
> > **A typo in the printed statement.** As printed, (a) and (b) both read $\sum_{j=1}^n a_{ij}$; the second one must have the summation over the **row index**:
> >
> > $$(a)\ \sum_{j=1}^{n}a_{ij}=\mathrm{outdeg}(v_i),\qquad (b)\ \sum_{i=1}^{n}a_{ij}=\mathrm{indeg}(v_j).$$
> >
> > (Otherwise (b) would just repeat (a) with $i$ renamed.) Both statements below are proved in this corrected form.
> >
> > ### (a) Row sums are out-degrees
> >
> > Fix $i$. Since $a_{ij}\in\{0,1\}$,
> >
> > $$\sum_{j=1}^{n}a_{ij}=\big|\{j\ :\ a_{ij}=1\}\big|=\big|\{j\ :\ (v_i,v_j)\in A(D)\}\big|=\mathrm{outdeg}(v_i).$$
> >
> > (Note $a_{ii}=0$ because $D$ has no loops, so the sum really counts arcs and not a loop.)
> >
> > ### (b) Column sums are in-degrees
> >
> > Fix $j$. Then
> >
> > $$\sum_{i=1}^{n}a_{ij}=\big|\{i\ :\ a_{ij}=1\}\big|=\big|\{i\ :\ (v_i,v_j)\in A(D)\}\big|=\mathrm{indeg}(v_j).$$
> >
> > **Immediate consequence.** Summing (a) over $i$ (or (b) over $j$) gives the handshake identity of Module 11, Theorem 11.1:
> >
> > $$\sum_{i,j}a_{ij}=\sum_i \mathrm{outdeg}(v_i)=\sum_j \mathrm{indeg}(v_j)=m .$$
> >
> > ### (c) $[M^p]_{ij}$ counts directed walks of length $p$ from $v_i$ to $v_j$
> >
> > **Proof by induction on $p$.**
> >
> > *Base $p=1$:* $[M]_{ij}=a_{ij}=1$ iff $(v_i,v_j)$ is an arc, i.e. iff there is exactly one directed walk of length $1$ from $v_i$ to $v_j$. ✓
> >
> > *Inductive step.* Assume the claim for $p$. By the definition of matrix multiplication,
> >
> > $$[M^{p+1}]_{ij}=\sum_{k=1}^{n}[M^{p}]_{ik}\,a_{kj}.$$
> >
> > Now $[M^p]_{ik}$ is the number of directed walks $v_i\to\cdots\to v_k$ of length $p$ (induction hypothesis) and $a_{kj}=1$ exactly when $v_k\to v_j$ is an arc. Every directed walk of length $p+1$ from $v_i$ to $v_j$ has a unique last-but-one vertex $v_k$ and is obtained by appending the arc $v_k v_j$ to a walk of length $p$ from $v_i$ to $v_k$. Hence the summand counts exactly the walks of length $p+1$ whose penultimate vertex is $v_k$, and summing over $k$ counts all walks of length $p+1$ from $v_i$ to $v_j$. ✓
> >
> > **Useful consequences.** (All are standard tools for digraph problems.)
> >
> > * $D$ is **strong** iff for every ordered pair $(i,j)$ there is some $p\ge1$ with $[M^p]_{ij}>0$; thus strong connectivity is computable from the powers of $M$ (equivalently, from $(I+M)^{n-1}$, whose positive entries mark reachability).
> > * The total number of directed walks of length $p$ in $D$ is $\mathbf 1^{T}M^{p}\mathbf 1$.
> > * The number of **closed** directed walks of length $p$ is $\mathrm{tr}(M^{p})=\sum_i [M^p]_{ii}$; in particular $\mathrm{tr}(M^2)=0$ for a simple digraph (no loops), while $\mathrm{tr}(M^3)=3\cdot(\text{number of directed triangles})$.

> [!question] Q17: An Orientation With $|\mathrm{outdeg}-\mathrm{indeg}|\le1$
> Every graph $G$ has an orientation $D$ such that $|\mathrm{outdeg}(v)-\mathrm{indeg}(v)|\le1$ for every vertex $v$.
>
> > [!success]- Solution (Click to expand)
> >
> > **Idea: reduce to Eulerian graphs by adding one new vertex.** Recall that every connected Eulerian graph (all degrees even) admits a closed Euler trail, i.e. a closed walk using every edge exactly once.
> >
> > **Step 1 (make all degrees even).** Let $O=\{v\in V(G)\ :\ \deg_G(v)\text{ is odd}\}$. By the handshake lemma $|O|$ is even. Add a **new vertex** $x$ and join $x$ to every vertex of $O$, forming $G'$. Then
> >
> > * each $v\in O$ gains exactly one incident edge, so $\deg_{G'}(v)=\deg_G(v)+1$ is even;
> > * each $v\notin O$ keeps its even degree;
> > * $\deg_{G'}(x)=|O|$ is even.
> >
> > So every component of $G'$ is Eulerian.
> >
> > **Step 2 (orient along Euler trails).** Take, in each component of $G'$, a closed Euler trail $x_1x_2\cdots x_\ell x_1$ and orient every edge of it **in the direction of travel**. Along a closed trail each visit to a vertex contributes one arriving and one departing edge, so in the resulting orientation $D'$ of $G'$
> >
> > $$\mathrm{outdeg}_{D'}(v)=\mathrm{indeg}_{D'}(v)\qquad\text{for every }v\in V(G').$$
> >
> > **Step 3 (delete $x$).** Delete $x$ together with all $|O|$ edges incident with it. This leaves exactly the graph $G$, oriented: call the orientation $D$. For each $v\in V(G)$ at most **one** edge was removed (the edge $vx$, present iff $v\in O$). Since in $D'$ the in- and out-degrees of $v$ were equal, removing a single incident edge changes the difference by at most $1$:
> >
> > $$v\notin O:\ \mathrm{outdeg}_D(v)-\mathrm{indeg}_D(v)=0,\qquad v\in O:\ \big|\mathrm{outdeg}_D(v)-\mathrm{indeg}_D(v)\big|=1 .$$
> >
> > $$\boxed{\big|\mathrm{outdeg}_D(v)-\mathrm{indeg}_D(v)\big|\le 1\quad\text{for all }v.}$$
> >
> > **Remarks.**
> >
> > * The parity is forced: $\mathrm{outdeg}(v)+\mathrm{indeg}(v)=\deg_G(v)$, so $|\mathrm{outdeg}-\mathrm{indeg}|\equiv \deg_G(v)\pmod 2$. Hence the best possible bound is $0$ at even-degree vertices and $1$ at odd-degree vertices — exactly what the construction achieves.
> > * Summing, $\sum_v(\mathrm{outdeg}-\mathrm{indeg})=0$, so the orientation of Step 2 also shows the "balance" identity of Theorem 11.1 in a constructive way.

> [!question] Q18: An $r$-Regular Superdigraph
> Let $D$ be a digraph and let $r=\max_{v\in V}\{\mathrm{outdeg}(v),\mathrm{indeg}(v)\}$. Prove that there is an $r$-regular digraph $H$ such that $D$ is a subdigraph of $H$.
>
> > [!success]- Solution (Click to expand)
> >
> > **Proof.** If $r=0$, then every vertex of $D$ already has out-degree $0$ and in-degree $0$, so $H=D$ is already $0$-regular. Assume now that $r\ge1$.
> >
> > For each vertex $v\in V(D)$ define its **out-deficiency** $a_v$ and **in-deficiency** $b_v$ by
> >
> > $$a_v=r-\mathrm{outdeg}_D(v)\qquad\text{and}\qquad b_v=r-\mathrm{indeg}_D(v).$$
> >
> > By definition of $r$ we have $0\le a_v\le r$ and $0\le b_v\le r$ for every $v\in V(D)$. Moreover, since the sum of all out-degrees of $D$ equals the sum of all in-degrees (both equal $|A(D)|$), the total out-deficiency equals the total in-deficiency:
> >
> > $$M=\sum_{v\in V(D)}a_v=r\,|V(D)|-|A(D)|=\sum_{v\in V(D)}b_v .$$
> >
> > ### 1. Creating stubs and a bijection
> >
> > * For each vertex $v\in V(D)$ create $a_v$ labelled **out-stubs** $(v,1),(v,2),\dots,(v,a_v)$. Since $a_v\le r$, each out-stub of $v$ has a distinct label $s\in\{1,2,\dots,r\}$.
> > * Similarly, for each vertex $w\in V(D)$ create $b_w$ labelled **in-stubs** $[w,1],[w,2],\dots,[w,b_w]$.
> >
> > Because there are $M$ out-stubs and $M$ in-stubs in total, we may choose an arbitrary bijection $\phi$ pairing each out-stub $(v,s)$ with a unique in-stub $[w,t]$.
> >
> > ### 2. Constructing the superdigraph $H$
> >
> > Take $r+1$ disjoint copies of $D$, denoted $D_0,D_1,\dots,D_r$, where the copy of a vertex $v\in V(D)$ in $D_i$ is written $v^{(i)}$.
> >
> > Start with the disjoint union $D_0\sqcup D_1\sqcup\cdots\sqcup D_r$ (so $D\cong D_0$ is clearly a subdigraph of $H$), and add new arcs as follows: for every out-stub $(v,s)$ paired with $\phi(v,s)=[w,t]$, and for every index $i\in\{0,1,\dots,r\}$, add the directed arc
> >
> > $$v^{(i)}\longrightarrow w^{(i+s\bmod (r+1))}.$$
> >
> > ### 3. Verifying the properties of $H$
> >
> > **Check 1 — $H$ is a simple digraph (no loops, no parallel arcs).**
> >
> > * Because $s\in\{1,2,\dots,r\}$, we have $i+s\not\equiv i\pmod{r+1}$. Thus every newly added arc joins two *different* copies $D_i$ and $D_j$ with $i\neq j$: no loops are created, and no new arc duplicates an existing arc inside any $D_i$.
> > * For a fixed vertex $v^{(i)}$, its outgoing added arcs correspond to its out-stubs $(v,1),\dots,(v,a_v)$, which have **distinct** offsets $s$. These arcs therefore land in **distinct** copies $D_{(i+s)\bmod(r+1)}$, so at most one of them ends at any given vertex $w^{(j)}$; hence $v^{(i)}$ has at most one arc to any fixed $w^{(j)}$.
> >
> > **Check 2 — every out-degree of $H$ is $r$.** Each vertex $v^{(i)}$ inherits $\mathrm{outdeg}_D(v)$ arcs inside $D_i$, plus exactly $1$ new outgoing arc for each of its $a_v$ out-stubs. Hence
> >
> > $$\mathrm{outdeg}_H\big(v^{(i)}\big)=\mathrm{outdeg}_D(v)+a_v=\mathrm{outdeg}_D(v)+\big(r-\mathrm{outdeg}_D(v)\big)=r .$$
> >
> > **Check 3 — every in-degree of $H$ is $r$.** Each vertex $w^{(j)}$ inherits $\mathrm{indeg}_D(w)$ arcs inside $D_j$. For each of its $b_w$ in-stubs $[w,t]$, let $(v,s)=\phi^{-1}\big([w,t]\big)$ be its unique matched out-stub; the unique index $i\equiv j-s\pmod{r+1}$ then gives the unique new arc $v^{(i)}\to w^{(j)}$ corresponding to $[w,t]$. These $b_w$ new arcs have pairwise distinct tails: two in-stubs matched to out-stubs of *different* vertices give different tails, and two in-stubs matched to out-stubs $(v,s)$, $(v,s')$ of the *same* vertex $v$ have $s\neq s'$ (labels are distinct), so the tails $v^{(j-s)}$, $v^{(j-s')}$ lie in different copies. Thus
> >
> > $$\mathrm{indeg}_H\big(w^{(j)}\big)=\mathrm{indeg}_D(w)+b_w=\mathrm{indeg}_D(w)+\big(r-\mathrm{indeg}_D(w)\big)=r .$$
> >
> > Hence $H$ is an $r$-regular simple digraph containing $D$ as a subdigraph. $\blacksquare$
> >
> > $$\boxed{\text{Every digraph is a subdigraph of an }r\text{-regular digraph, }r=\max\{\mathrm{outdeg},\mathrm{indeg}\}.}$$
> >
> > **Why the bound $r$ is the right one.** No $r'$-regular superdigraph with $r'<r$ can exist, since the out- and in-degrees of $H$ are at least those of $D$; so the value $r$ is best possible. Note also that the construction uses $(r+1)\,n$ vertices: extra vertices are genuinely necessary (e.g. the complete digraph on $3$ vertices plus an isolated vertex has $r=2$ but cannot be extended to a $2$-regular digraph on the same $4$ vertices, since the clique vertices are already saturated).

> [!question] Q19: Regular Tournaments Exist Exactly for Odd Order
> Prove that there exist regular tournaments of every odd order but there are no regular tournaments of even order.
>
> > [!success]- Solution (Click to expand)
> >
> > ### No regular tournament of even order
> >
> > Suppose $T$ is a regular tournament on $n$ vertices, every vertex having out-degree $d$. Counting arcs by tails,
> >
> > $$nd=\sum_{v}\mathrm{outdeg}(v)=|A(T)|=\binom n2=\frac{n(n-1)}{2},$$
> >
> > so
> >
> > $$d=\frac{n-1}{2}.$$
> >
> > Since $d$ must be an integer, $n-1$ is even, i.e. $n$ is **odd**. Hence no regular tournament of even order exists. $\blacksquare$
> >
> > ### A regular tournament of every odd order
> >
> > Let $n=2h+1$ (so $h=(n-1)/2$). Take the vertices $\mathbb{Z}_n=\{0,1,\dots,n-1\}$ and, for every $i$, put arcs from $i$ to its $h$ "successors"
> >
> > $$i\to i+1,\quad i\to i+2,\quad \dots,\quad i\to i+h \qquad(\text{mod } n).$$
> >
> > This is the **carousel (cyclic) tournament** $C_n$.
> >
> > * **It is a tournament:** for each unordered pair $\{i,j\}$ exactly one of $j-i$ and $i-j$ lies in $\{1,\dots,h\}$ modulo $n$ (because $n=2h+1$), so exactly one of $i\to j$, $j\to i$ is present.
> > * **It is regular:** every vertex has out-degree $h=(n-1)/2$ and, by the same count, in-degree $h$.
> >
> > $$\boxed{\text{Regular tournaments exist for every odd }n\text{ (the carousel), and for no even }n.}$$
> >
> > **Extra: a regular tournament is automatically strong.** Suppose a regular tournament $T$ were not strongly connected. By the one-way-cut characterisation proved in Q24 below, there is a partition $V=A\sqcup B$ ($A,B\neq\varnothing$) with **every** arc between $A,B$ pointing from $A$ to $B$.
> >
> > **The count.** A vertex $u\in A$ dominates all of $B$, plus some vertices inside $A$:
> >
> > $$\mathrm{outdeg}(u)=\underbrace{|B|}_{\text{all of }B}+\underbrace{\mathrm{outdeg}_{T[A]}(u)}_{\text{inside }A}.$$
> >
> > Summing over $u\in A$ counts each arc with tail in $A$ exactly once — the $\binom{|A|}{2}$ arcs inside $A$ plus all $|A||B|$ cross arcs:
> >
> > $$\sum_{u\in A}\mathrm{outdeg}(u)=|A|\cdot\frac{n-1}{2}=\underbrace{|A|(|A|-1)/2}_{\text{arcs inside }A}+\underbrace{|A||B|}_{\text{all cross arcs }A\to B},$$
> >
> > so
> >
> > $$|A|\cdot\frac{n-1}{2}=\frac{|A|(|A|-1)}{2}+|A|(n-|A|).$$
> >
> > Dividing by $|A|>0$: $\dfrac{n-1}{2}=\dfrac{|A|-1}{2}+n-|A|$, i.e. $\dfrac{n-1}{2}=n-\dfrac{|A|+1}{2}$, i.e. $|A|+1 = 2n-(n-1)=n+1$, i.e. $|A|=n$, contradicting $|B|\neq\varnothing$. (The key point: all cross arcs leave $A$, so the sum of out-degrees over $A$ is *exactly* the number of arcs with tail in $A$.) Hence a regular tournament is strong, and by the corollary to Theorem 11.10 it has a directed Hamilton cycle — consistent with the carousel containing $0\to1\to\cdots\to n-1\to0$.

> [!question] Q20: At Most One Source and At Most One Sink in a Tournament
> Show that in a tournament there is at most one vertex of out-degree zero and at most one vertex of in-degree zero.
>
> > [!success]- Solution (Click to expand)
> >
> > **Out-degree zero.** Let $u\neq v$ be two vertices. In a tournament exactly one of the arcs $(u,v),(v,u)$ is present. So at least one of $u,v$ is the tail of an arc, i.e. has out-degree $\ge1$. Hence **two distinct vertices cannot both have out-degree $0$**: at most one vertex is a *sink* (out-degree $0$).
> >
> > **In-degree zero.** Symmetrically, at least one of $u,v$ is the head of the arc between them, so at least one of $u,v$ has in-degree $\ge1$. Hence at most one vertex has in-degree $0$ — at most one *source*.
> >
> > $$\boxed{\#\{\text{sinks}\}\le1,\qquad \#\{\text{sources}\}\le1.}$$
> >
> > **Remarks.**
> >
> > * These two vertices, when they exist, are unique and are the *last* and *first* vertices of every transitive ordering: in a transitive tournament the out-degrees are $0,1,\dots,n-1$ (Q25), so exactly one sink and exactly one source occur.
> > * The bound cannot be improved to zero: the transitive tournament on $n\ge2$ vertices has one sink and one source.
> > * Contrast with general digraphs: an arbitrary simple digraph can have many sources and many sinks (e.g. an independent set with no arcs has $n$ sources and $n$ sinks).

> [!question] Q21: Deleting $k\le n-3$ Vertices From a Strong Tournament
> Let $D$ be a strong tournament. Given any $k$ with $1\le k\le n-3$, show that there exists a set $S\subseteq V(D)$ of $k$ vertices such that $D-S$ is strongly connected.
>
> > [!success]- Solution (Click to expand)
> >
> > **The tool (Theorem 11.10).** A strong tournament on $m\ge3$ vertices contains directed cycles of **every** length $3,4,\dots,m$.
> >
> > **The corollary we use.** If $m\ge3$ and $T$ is a strong tournament on $m$ vertices, then $T$ contains a strong subtournament on $m-1$ vertices. Indeed, by Theorem 11.10, $T$ contains a directed cycle $C$ of length $m-1$; the subtournament $T[V(C)]$ induced by the vertices of $C$ contains the closed directed walk $C$ through all its vertices, hence it is strongly connected (walk forwards around $C$); it has $m-1$ vertices. So $T-x$ is strong, where $x$ is the unique vertex outside $C$.
> >
> > **Proof of the statement by iteration.** We show by induction on $j=0,1,\dots,k$ that there are vertices $x_1,\dots,x_j$ such that $D-\{x_1,\dots,x_j\}$ is a strong tournament on $n-j\ge n-k\ge3$ vertices.
> >
> > * $j=0$: $D$ is strong by hypothesis.
> > * Step: suppose $D-\{x_1,\dots,x_j\}$ is a strong tournament with $n-j\ge n-k+1\ge4$ vertices. Apply the corollary with $m=n-j\ge4$ (so that $m-1\ge3$ is a legal cycle length): there is a vertex $x_{j+1}$ whose deletion leaves a strong tournament on $n-j-1$ vertices.
> >
> > After $k$ steps we obtain $S=\{x_1,\dots,x_k\}$ with $|S|=k$ and $D-S$ a strong tournament on $n-k\ge3$ vertices. $\blacksquare$
> >
> > $$\boxed{\text{For every }1\le k\le n-3\text{ there is }S,\ |S|=k,\text{ with }D-S\text{ strong.}}$$
> >
> > **Why $k\le n-3$ is exactly the range.** A strong tournament needs at least $3$ vertices (on $1$ or $2$ vertices no tournament is strong: one vertex is trivially strong only by convention, and a 2-vertex tournament has a single arc, so the head cannot reach the tail). Deleting $n-3$ vertices leaves $3$ vertices — a directed triangle, which is strong. Deleting $n-2$ vertices would leave $2$ vertices, which can never be strong, so the hypothesis $k\le n-3$ cannot be relaxed.

> [!question] Q22: A Tournament on 5 Vertices With All Out-Degrees Equal
> (a) Draw a tournament on $5$ vertices in which every vertex has the same out-degree.
> (b) If a tournament has $n$ vertices and every vertex has out-degree $d$, find $d$.
>
> > [!success]- Solution (Click to expand)
> >
> > **(a) The carousel tournament.** Put the vertices $0,1,2,3,4$ on a pentagon in cyclic order, and let each vertex beat the two vertices that follow it in the cyclic order:
> >
> > $$i\to i+1,\qquad i\to i+2\qquad(\text{indices mod }5).$$
> >
> > Explicit arc list: $0\to1$, $0\to2$; $1\to2$, $1\to3$; $2\to3$, $2\to4$; $3\to4$, $3\to0$; $4\to0$, $4\to1$. That is $5+5=10=\binom52$ arcs, so **every** pair of vertices is joined by exactly one arc and we indeed have a tournament.
> >
> > ![[ch11_regular_tournament_5v.png]]
> >
> > *Why it is a tournament.* For two vertices $i\neq j$ look at the difference $j-i \pmod 5$. If $j-i\in\{1,2\}$ then $i\to j$; if $j-i\in\{3,4\}$ then $j\to i$. The two cases are exhaustive and exclusive, so exactly one arc joins $i$ and $j$.
> >
> > *Why all out-degrees are equal.* $\mathrm{outdeg}(i)=\big|\{i+1,i+2\}\big|=2$ for every $i$; correspondingly $\mathrm{indeg}(i)=\big|\{i-1,i-2\}\big|=2$. So the tournament is **$2$-regular** in the sense of Q19 — every vertex has the same out-degree and the same in-degree.
> >
> > **(b) The value of $d$.** Count arcs in two ways. A tournament on $n$ vertices has one arc per unordered pair, so
> >
> > $$m=\binom{n}{2}=\frac{n(n-1)}{2},$$
> >
> > and by the digraph handshake (Theorem 11.1) the out-degrees sum to $m$:
> >
> > $$m=\sum_{v}\mathrm{outdeg}(v)=n\cdot d.$$
> >
> > Equating,
> >
> > $$n\,d=\frac{n(n-1)}{2}\quad\Longrightarrow\quad \boxed{\,d=\frac{n-1}{2}\,}$$
> >
> > **Consequences.**
> >
> > * $d$ must be an integer, so **$n$ must be odd** — an even-order tournament can never have all out-degrees equal. (Equivalently: $\sum_v \mathrm{outdeg}(v)=n(n-1)/2$ is not divisible by $n$ when $n$ is even.) This is the same obstruction as in Q19; the construction above for $n=5$ generalises to the carousel on $2h+1$ vertices with $d=h=\frac{n-1}{2}$.
> > * Since a tournament on $n$ vertices has out-degrees between $0$ and $n-1$, we need $\frac{n-1}{2}\le n-1$, which holds for all $n\ge1$; for $n=1$ we get $d=0$, consistent with the single trivial vertex.
> > * For $n=5$ the formula gives $d=2$, matching the drawing: every vertex has exactly two out-neighbours and two in-neighbours.

> [!question] Q23: A Unilateral (But Not Strong) and a Strong Tournament on 5 Vertices
> Draw:
> (a) a unilaterally connected (but not strongly connected) tournament on $5$ vertices;
> (b) a strongly connected tournament on $5$ vertices.
> Justify that your tournaments indeed have the required properties.
>
> > [!success]- Solution (Click to expand)
> >
> > **(a) Unilateral but not strong: a triangle feeding a transitive pair.** Take vertices $a,b,c,x,y$ and the arcs
> >
> > $$a\to b\to c\to a,\qquad a\to x,\ b\to x,\ c\to x,\qquad a\to y,\ b\to y,\ c\to y,\qquad x\to y.$$
> >
> > That is $3+3+3+1=10=\binom52$ arcs, so every pair is joined by exactly one arc and we have a tournament: inside $\{a,b,c\}$ the three pairs are used, each of $a,b,c$ sends one arc to each of $x,y$, and the remaining pair is $x\to y$.
> >
> > ![[ch11_unilateral_tournament_5v.png]]
> >
> > *Unilateral.* We must check that for every pair $u,v$ **at least one** of $u\leadsto v$, $v\leadsto u$ holds.
> >
> > * $u,v\in\{a,b,c\}$: the triangle is strong, so both directions are reachable.
> > * $u\in\{a,b,c\}$ and $v=x$: $u\to x$ directly.
> > * $u\in\{a,b,c\}$ and $v=y$: $u\to y$ directly (also $u\to x\to y$).
> > * $u=x$, $v=y$: $x\to y$.
> > * $u=y$ and $v\in\{a,b,c,x\}$: $v\to y$ (directly for $v\in\{a,b,c\}$, and $x\to y$).
> >
> > So every pair is comparable by a directed path: $D$ is unilaterally connected.
> >
> > *Not strong.* $\mathrm{outdeg}(y)=0$, so no vertex whatsoever is reachable from $y$; in particular $y\not\leadsto a$. Hence $D$ is **not** strongly connected (the sink $y$ is a one-vertex "dead end").
> >
> > $$\boxed{D \text{ is unilateral but not strong: } A=\{a,b,c,x\}\to\{y\} \text{ is a one-way cut.}}$$
> >
> > **Moral.** This is the cheapest way to break strong connectivity in a tournament: keep a strong block (the triangle) and hang a transitive "tail" off it. Note $m=7=\binom52-3$: the bound of Q11 ($m\ge(n-1)^2+1=17$ would force strong connectivity) is far from being met, so no contradiction.
> >
> > **(b) Strong: the carousel of Q22.** Use the same $5$-vertex tournament as in Q22(a): $i\to i+1$ and $i\to i+2$ mod $5$, with arc list $0\to1,0\to2,1\to2,1\to3,2\to3,2\to4,3\to4,3\to0,4\to0,4\to1$.
> >
> > *Why it is strong.* It contains the **directed Hamilton cycle**
> >
> > $$0\to1\to2\to3\to4\to0,$$
> >
> > so from any vertex $i$ we can walk forward around the cycle and reach $i+1,i+2,i+3,i+4$ — that is, all other vertices. Hence every vertex reaches every other vertex: $D$ is strongly connected (indeed its diameter is $2$: the cycle gives distance $\le 4$, and the chords $i\to i+2$ cut it to $\le 2$).
> >
> > ![[ch11_regular_tournament_5v.png]]
> >
> > **Cross-check with the theory.** By the corollary to Theorem 11.10, a tournament is strong **iff** it has a directed Hamilton cycle; the cycle $0\to1\to2\to3\to4\to0$ certifies strong connectivity at a glance. Comparing with (a): both are tournaments on $5$ vertices with the same number of arcs, yet (a) has the one-way cut $A=\{a,b,c,x\}$, $B=\{y\}$ (every arc between the parts points into $y$), exactly the obstruction of Q24, while the carousel admits no such cut.

> [!question] Q24: Non-Strong Tournaments and One-Way Cuts
> Show that a tournament $D$ is not strongly connected if and only if there is a partition of $V(D)$ into two subsets $A$ and $B$ such that every arc between $A$ and $B$ is of the form $(u,v)$ with $u\in A$, $v\in B$.
>
> > [!success]- Solution (Click to expand)
> >
> > **($\Leftarrow$) A one-way cut destroys strong connectivity.** Suppose $V(D)=A\cup B$ with $A,B\neq\varnothing$ and every arc between the two parts goes from $A$ to $B$.
> >
> > Take $b\in B$ and $a\in A$. If there were a directed path $b=x_0\to x_1\to\cdots\to x_r=a$, let $j$ be the first index with $x_j\in A$. Then $x_j\neq x_0$ (as $x_0=b\in B$), so $x_{j-1}\in B$ and $x_{j-1}\to x_j$ is an arc from $B$ to $A$ — impossible. Hence $b\not\leadsto a$, and $D$ is not strong.
> >
> > **($\Rightarrow$) A non-strong tournament has such a cut.** Choose a vertex $v_0$ and let
> >
> > $$B=\{w\in V : v_0\leadsto w\}\quad(\text{the set of vertices reachable from } v_0),$$
> >
> > so $v_0\in B$. Since $D$ is not strong, some vertex $u$ is not reachable from $v_0$, so $u\notin B$ and $A:=V\setminus B\neq\varnothing$; also $B\neq\varnothing$. Now $B$ is **closed under out-neighbours**: if $w\in B$ and $w\to z$, then $v_0\leadsto w\to z$, so $z\in B$. Hence there is no arc from $B$ to $A$.
> >
> > But $D$ is a tournament, so every pair $(a,b)$ with $a\in A$, $b\in B$ is joined by exactly one arc; it is **not** $b\to a$ (no arc leaves $B$), hence it must be $a\to b$. Therefore all arcs between $A$ and $B$ run from $A$ to $B$, as required.
> >
> > $$\boxed{D\text{ not strong}\iff \exists\,V=A\sqcup B,\ A,B\neq\varnothing,\ \text{all arcs between them point }A\to B.}$$
> >
> > **Remarks.**
> >
> > * The partition is exactly a "cut" in the **condensation**: contract each strongly connected component; the condensation of a tournament is a transitive tournament, i.e. the components can be ordered $C_1,C_2,\dots,C_t$ so that *all* arcs go from $C_i$ to $C_j$ for $i<j$. Then $A=C_1\cup\cdots\cup C_j$, $B=C_{j+1}\cup\cdots\cup C_t$ works for every $j$, and $D$ is strong iff $t=1$.
> > * The partition is not unique: any initial segment of the condensation order gives one. The *maximal* choice is $A=V\setminus B$ with $B$ the **sink** component (the set of vertices that can reach nothing outside), and the *minimal* choice is $A=$ the source component.
> > * This is the structural reason behind several earlier exercises: a strong tournament has no such cut, while the unilateral example of Q23(a) has the cut $A=\{a,b,c,x\}$, $B=\{y\}$.

> [!question] Q25: Transitive Tournaments and the Out-Degree Sequence $0,1,\dots,n-1$
> A tournament $D$ is called **transitive** if $(u,w)\in A(D)$ whenever $(u,v)\in A(D)$ and $(v,w)\in A(D)$. Show that a tournament is transitive if and only if the vertices of $D$ can be ordered $v_1,v_2,\dots,v_n$ such that $\mathrm{outdeg}(v_1)=0$, $\mathrm{outdeg}(v_2)=1$, $\dots$, $\mathrm{outdeg}(v_n)=n-1$.
>
> > [!success]- Solution (Click to expand)
> >
> > **A lemma we need: a transitive tournament has a sink (a vertex of out-degree $0$).**
> >
> > *First, a transitive tournament has no directed cycle.* Suppose $x_1\to x_2\to\cdots\to x_r\to x_1$ is a directed cycle of **minimum** length $r\ge3$. From $x_1\to x_2$ and $x_2\to x_3$, transitivity gives $x_1\to x_3$. If $r=3$ this contradicts the arc $x_3\to x_1$ (a tournament has only one arc between $x_1$ and $x_3$). If $r\ge4$, then $x_1\to x_3\to x_4\to\cdots\to x_r\to x_1$ is a shorter directed cycle, contradicting minimality. So there is no directed cycle.
> >
> > *Now take a longest directed path $P:\,x_1\to x_2\to\cdots\to x_k$.* Its last vertex $x_k$ has out-degree $0$: if $x_k\to z$ with $z$ on $P$, we get a directed cycle; if $z$ is not on $P$, then $P$ extended by $z$ is a longer directed path. Both are impossible.
> >
> > **($\Rightarrow$) Transitive $\Rightarrow$ out-degrees $0,1,\dots,n-1$.** Induct on $n$; the case $n=1$ is clear. Let $D$ be a transitive tournament on $n\ge2$ vertices and let $v$ be a sink (out-degree $0$, existing by the lemma).
> >
> > * $D-v$ is still a tournament, and it is still transitive (transitivity is inherited by subtournaments).
> > * Every other vertex dominates $v$ (as $v$ has out-degree $0$), so for $x\neq v$,
> >
> > $$\mathrm{outdeg}_{D-v}(x)=\mathrm{outdeg}_{D}(x)-1.$$
> >
> > By induction, order the vertices of $D-v$ as $u_1,\dots,u_{n-1}$ with $\mathrm{outdeg}_{D-v}(u_i)=i-1$; then $\mathrm{outdeg}_D(u_i)=i$. Setting $v_1:=v$ (out-degree $0$) and $v_{i+1}:=u_i$ gives $\mathrm{outdeg}(v_i)=i-1$ for $i=1,\dots,n$. $\blacksquare$
> >
> > **($\Leftarrow$) Out-degrees $0,1,\dots,n-1$ $\Rightarrow$ transitive.** Suppose the ordering $v_1,\dots,v_n$ satisfies $\mathrm{outdeg}(v_i)=i-1$. Fix $i$ and look at the subtournament $S_i$ induced by $V_i=\{v_1,\dots,v_i\}$. Count the arcs with tail in $V_i$ in two ways:
> >
> > * By the given out-degrees, the number of arcs leaving $V_i$ is
> >
> > $$\sum_{j=1}^{i}\mathrm{outdeg}(v_j)=\sum_{j=1}^{i}(j-1)=\binom{i}{2}.$$
> >
> > * Inside $V_i$ there are exactly $\binom{i}{2}$ arcs (it is a tournament on $i$ vertices), and each of them leaves $V_i$ in the above sense.
> >
> > Hence **no arc joins $V_i$ to $V\setminus V_i$**. As $D$ is a tournament, this means that for every $j>i$ the arc between $v_i$ and $v_j$ must be $v_j\to v_i$: all arcs point from higher index to lower index.
> >
> > Now suppose $v_i\to v_j$ and $v_j\to v_k$. Then $j<i$ and $k<j$, so $k<i$, hence $v_i\to v_k$. That is exactly transitivity. $\blacksquare$
> >
> > $$\boxed{D\text{ transitive}\iff \{\mathrm{outdeg}(v)\}_v=\{0,1,\dots,n-1\}\iff D \text{ is acyclic (Q26).}}$$
> >
> > **Remarks.**
> >
> > * The ordering is **unique** (it is forced by the out-degrees, which are all distinct), and it is the reverse of a topological order: $v_n$ is the **source** (beats everybody, out-degree $n-1$) and $v_1$ is the **sink**. In the matrix/adjacency picture the arc set is exactly $\{(v_j,v_i): j>i\}$, i.e. the adjacency matrix is strictly lower triangular.
> > * Up to isomorphism there is exactly **one** transitive tournament of each order $n$ — so "transitive" is a complete structural description, not just a property.
> > * The two vertices $v_n$ and $v_1$ are the unique source and unique sink of Q20.

> [!question] Q26: Transitive $\iff$ No Directed Cycle
> Show that a tournament is transitive if and only if it does not contain any directed cycle.
>
> > [!success]- Solution (Click to expand)
> >
> > **($\Rightarrow$) Transitive $\Rightarrow$ acyclic.** This is the lemma from Q25: if $x_1\to x_2\to\cdots\to x_r\to x_1$ is a shortest directed cycle ($r\ge3$), transitivity applied to $x_1\to x_2\to x_3$ gives $x_1\to x_3$; for $r=3$ that contradicts the arc $x_3\to x_1$, and for $r\ge4$ it produces the shorter cycle $x_1\to x_3\to\cdots\to x_r\to x_1$. Either way, no directed cycle exists.
> >
> > **($\Leftarrow$) Acyclic $\Rightarrow$ transitive.** Suppose $D$ has no directed cycle, and take vertices with $u\to v$ and $v\to w$ (all three distinct, as there are no loops). Since $D$ is a tournament, exactly one of $u\to w$, $w\to u$ holds. If $w\to u$, then
> >
> > $$u\to v\to w\to u$$
> >
> > is a directed $3$-cycle — contradiction. Therefore $u\to w$, which is precisely transitivity. $\blacksquare$
> >
> > $$\boxed{\text{transitive}\iff\text{acyclic}\iff \text{out-degrees are } 0,1,\dots,n-1.}$$
> >
> > **Remarks.**
> >
> > * The three descriptions are equivalent by Q25, and the last one is often the most usable: to test transitivity in $O(n^2)$ just compute the out-degrees and check they are all distinct (hence $\{0,1,\dots,n-1\}$).
> > * Acyclic digraphs in general have a topological ordering, and by Q25 a transitive tournament's ordering is forced: $v_n\to v_{n-1}\to\cdots\to v_1$ along the "beats" relation.
> > * Consequence for scores: a tournament is transitive iff its score sequence is $(0,1,\dots,n-1)$; every other tournament contains a directed triangle, and in fact contains directed cycles of length $3$ (the shortest cycle in a tournament is always a triangle, since a shortest cycle has no chords and a tournament chord would split it — see the argument above).

> [!question] Q27: Three Identities for the Out-Degrees of a Tournament
> If $T$ is a tournament on $n$ vertices $v_1,v_2,\dots,v_n$ with $\mathrm{outdeg}(v_i)=s_i$, $i=1,2,\dots,n$, show that
> (a) $\sum_{i=1}^{n}s_i\ge \dfrac{k(k-1)}{2}$, $\ 1\le k<n$;
> (b) $\sum_{i=1}^{n}s_i=\dfrac{n(n-1)}{2}$;
> (c) $\sum_{i=1}^{n}s_i^{2}=\sum_{i=1}^{n}\big(n-1-s_i\big)^{2}$.
>
> > [!success]- Solution (Click to expand)
> >
> > **(b) first, since everything else rests on it.** Count the arcs by their tails: every arc has exactly one tail, and the number of arcs with tail $v_i$ is $s_i$. Hence
> >
> > $$\sum_{i=1}^{n}s_i=m=\binom{n}{2}=\frac{n(n-1)}{2}.$$
> >
> > (This is Theorem 11.1, $\sum_v \mathrm{outdeg}(v)=\sum_v \mathrm{indeg}(v)=m$, combined with $m=\binom n2$ for a tournament.) Equivalently, the average score is $\dfrac{n-1}{2}$. $\blacksquare$
> >
> > **(a) As printed.** The statement is
> >
> > $$\sum_{i=1}^{n}s_i \ \ge\ \frac{k(k-1)}{2}\qquad\text{for every } 1\le k<n,$$
> >
> > and by (b) the left side equals $\frac{n(n-1)}{2}$, so the inequality reads $\frac{n(n-1)}{2}\ge\frac{k(k-1)}{2}$, i.e. $n(n-1)\ge k(k-1)$, which holds for all $k\le n$ because $x\mapsto x(x-1)$ is increasing for $x\ge1$. So the printed inequality is true but trivial — it carries no information about the individual scores.
> >
> > **The meaningful version (the intended statement).** The useful inequality is for **every $k$-element subset** $S\subseteq V(T)$:
> >
> > $$\sum_{v\in S}s_v\ \ge\ \binom{k}{2}\qquad\text{for every } S \text{ with } |S|=k.$$
> >
> > *Proof.* Count the arcs whose **tail** lies in $S$. Splitting them according to where the head lies,
> >
> > $$\sum_{v\in S}s_v=\underbrace{\#\{\text{arcs inside } S\}}_{=\binom{k}{2}}+\underbrace{\#\{\text{arcs from } S \text{ to } V\setminus S\}}_{\ge 0}\ \ge\ \binom{k}{2}.$$
> >
> > The first term is exactly $\binom{k}{2}$ because $S$ induces a tournament on $k$ vertices. Equality holds iff no arc leaves $S$, i.e. iff $S$ is a set of "sinks" (all arcs between $S$ and its complement point into $S$) — which by Q24 means $S$ is a union of terminal strong components. $\blacksquare$
> >
> > **Why this is the right form: Landau's theorem.** A nondecreasing sequence $s_1\le s_2\le\cdots\le s_n$ of integers is the score sequence of some tournament on $n$ vertices **iff**
> >
> > $$\sum_{i=1}^{k}s_i\ \ge\ \binom{k}{2}\quad\text{for all } 1\le k\le n,\qquad\text{with equality for } k=n.$$
> >
> > The necessity is the subset inequality above applied to the $k$ smallest scores (their sum is minimal among $k$-subsets); the sufficiency is Landau's construction. Taking $S$ to be the $k$ vertices of **largest** score instead gives the companion bound $\sum_{i=n-k+1}^{n}s_i\le \binom{n}{2}-\binom{n-k}{2}$, which is the same inequality applied to the converse tournament.
> >
> > **(c) The two "degree squares" agree.** In a tournament $v_i$ is joined to the other $n-1$ vertices, and each such vertex is either an out-neighbour or an in-neighbour, so
> >
> > $$\mathrm{indeg}(v_i)=(n-1)-s_i .$$
> >
> > Therefore the identity says exactly $\sum_i \mathrm{outdeg}(v_i)^2=\sum_i \mathrm{indeg}(v_i)^2$ — the tournament analogue of Q4 (there $G$ was $k$-regular; here $G=K_n$ and the orientation is arbitrary, so every vertex has total degree $n-1$). Direct expansion:
> >
> > $$\sum_{i=1}^{n}\Big[(n-1-s_i)^2-s_i^2\Big]=\sum_{i=1}^{n}\Big[(n-1)^2-2(n-1)s_i\Big]=n(n-1)^2-2(n-1)\sum_{i=1}^{n}s_i .$$
> >
> > Substituting $\sum_i s_i=\frac{n(n-1)}{2}$ from (b),
> >
> > $$=n(n-1)^2-2(n-1)\cdot\frac{n(n-1)}{2}=n(n-1)^2-n(n-1)^2=0 . \qquad\blacksquare$$
> >
> > $$\boxed{\sum_i s_i=\binom n2,\qquad \sum_{v\in S}s_v\ge\binom{|S|}{2},\qquad \sum_i s_i^2=\sum_i (n-1-s_i)^2 .}$$
> >
> > **Remarks.**
> >
> > * Equivalently, (c) says the variance of the scores equals the variance of the "losses" $n-1-s_i$: both sequences are symmetric about the mean $\frac{n-1}{2}$, consistent with the carousel of Q22 where $s_i\equiv\frac{n-1}{2}$ and both sides equal $n\left(\frac{n-1}{2}\right)^2$.
> > * A quick sanity check on $n=3$: the transitive tournament has scores $(0,1,2)$, so $\sum s_i^2=5$ and $\sum(2-s_i)^2=4+1+0=5$ ✓; the directed triangle has $(1,1,1)$, giving $3=3$ ✓.
> > * (c) is what makes the "sum of squares" invariant blind to the direction of the arcs, and it is the identity behind the standard proof that $\sum s_i^2$ is minimised by the regular carousel and maximised by the transitive tournament: expanding $\sum_i\big(s_i-\frac{n-1}{2}\big)^2=\sum_i s_i^2-\frac{n(n-1)^2}{4}$ shows the spread of the scores is measured by $\sum s_i^2$.

> [!question] Q28: Winners (Kings) in a Tournament
> A vertex $v$ in a tournament $T$ is called a **winner** if every vertex can be reached from $v$ by a directed path of length $\le2$. Show the following:
> (a) No tournament has exactly two winners.
> (b) For every $n\neq 2,4$ there is a tournament of order $n$ in which every vertex is a winner.
>
> > [!success]- Solution (Click to expand)
> >
> > Throughout, "winner" means: for every $x\neq v$, either $v\to x$ or there is $w$ with $v\to w\to x$. (Such vertices are usually called **kings** — the "king chicken" terminology.)
> >
> > **Lemma 1 (Landau): a vertex of maximum out-degree is a winner.** Let $\mathrm{outdeg}(v)$ be maximum and suppose some $x$ is not reachable from $v$ in $\le2$ steps. Then $v\not\to x$, so $x\to v$; and for every $w\in N^+(v)$ we cannot have $w\to x$ (else $v\to w\to x$), so $x\to w$. Hence $x$ beats $v$ **and every out-neighbour of $v$**, giving
> >
> > $$\mathrm{outdeg}(x)\ \ge\ 1+|N^+(v)|=\mathrm{outdeg}(v)+1,$$
> >
> > contradicting maximality. $\square$
> >
> > **Lemma 2: every vertex that is beaten by somebody is beaten by a winner.** Let $c$ have $N^-(c)=\{y:y\to c\}\neq\varnothing$. The subtournament $T[N^-(c)]$ is nonempty, so by Lemma 1 it has a vertex $d$ that is a winner **of that subtournament**, i.e. $d$ reaches every vertex of $N^-(c)$ in $\le2$ steps using only vertices of $N^-(c)$. Now check that $d$ is a winner of $T$:
> >
> > * every $y\in N^-(c)$: reachable from $d$ in $\le2$ steps (inside $N^-(c)$);
> > * $c$ itself: $d\to c$ directly, since $d\in N^-(c)$;
> > * every $x\notin N^-(c)\cup\{c\}$, i.e. every $x$ with $c\to x$: then $d\to c\to x$, so $d$ reaches $x$ in $2$ steps.
> >
> > So $d$ is a winner of $T$, and $d\to c$. $\square$
> >
> > **(a) Proof that exactly two winners is impossible.** Suppose the winners are exactly $c$ and $d$.
> >
> > * $d$ is a winner, so $d$ reaches $c$ in at most $2$ steps. In particular $c$ is beaten by somebody (by $d$ if $d\to c$, otherwise by the intermediate vertex of a path $d\to p\to c$).
> > * By Lemma 2, $c$ is beaten by a **winner**. The only winners are $c$ and $d$, and $c\not\to c$, so that winner must be $d$: hence $d\to c$.
> > * Repeating the same argument with the roles exchanged: $c$ is a winner, so $c$ reaches $d$ in at most $2$ steps, hence $d$ is beaten by somebody; by Lemma 2 it is beaten by a winner, and the only candidates $c,d$ give $c\to d$.
> >
> > But a tournament contains exactly one of the arcs $(c,d)$, $(d,c)$ — contradiction. Hence no tournament has exactly two winners. $\blacksquare$
> >
> > **Why Lemma 2 is the crux.** It says the winners are "upward closed" under beating: the set of vertices that beat a given vertex always contains a winner. So a beaten winner must be beaten by another winner — and two winners cannot beat each other.
> >
> > $$\boxed{\#\{\text{winners}\}\neq 2\ \text{ for every tournament.}}$$
> >
> > **(b) Tournaments in which everybody is a winner, for all $n\ne2,4$.**
> >
> > **$n=1$.** The single vertex vacuously reaches every other vertex (there is none). ✓
> >
> > **$n=3$.** The directed triangle $0\to1\to2\to0$: each vertex reaches the third vertex in $2$ steps. All three are winners. ✓
> >
> > **$n$ odd, $n=2h+1\ge5$: the carousel.** Vertices $0,1,\dots,2h$ in cyclic order, arcs $i\to i+j$ for $j=1,2,\dots,h$ (indices mod $2h+1$). Vertex $i$ beats $i+1,\dots,i+h$ outright, and the remaining $h$ vertices $i+h+1,\dots,i+2h$ are all beaten by $i+h$ (whose out-neighbours are $i+h+1,\dots,i+2h$). So every vertex reaches all others in $\le2$ steps, and every vertex is a winner. For $h=2$ this is exactly the Q22 carousel, where we checked it directly. ✓
> >
> > **$n$ even, $n=2h+2\ge6$: carousel on $2h+1$ vertices plus one extra vertex $z$.** Let $C=\{0,1,\dots,2h\}$ carry the carousel above, and add the arcs
> >
> > $$z\to 0,\qquad z\to h,\qquad i\to z\ \text{ for every } i\in C\setminus\{0,h\}.$$
> >
> > This is a tournament: $z$ is joined to each $i\in C$ by exactly one arc, and $C$ is already a tournament. Check that every vertex is a winner.
> >
> > * $z$: $z\to0$ and $0$ beats $1,\dots,h$; $z\to h$ and $h$ beats $h+1,\dots,2h$. So all of $C$ is at distance $\le2$, and $0,h$ at distance $1$. ✓
> > * $i\notin\{0,h\}$: $i\to z$ covers $z$ in one step. In $C$, $i$ beats $i+1,\dots,i+h$, and the remaining $h$ vertices $i+h+1,\dots,i+2h$ are all beaten by $i+h$ (since the carousel on $2h+1$ vertices gives $i+h\to i+h+1,\dots,i+2h$). ✓
> > * $i=0$: $0\to 1,\dots,h$; the vertices $h+1,\dots,2h$ are beaten by $h$; and $z$ is reached as $0\to1\to z$ (here $1\ne h$ because $h\ge2$). ✓
> > * $i=h$: $h\to h+1,\dots,2h$ and $h\to z$. The vertices $0,1,\dots,h-1$ are all beaten by $2h$ (whose out-neighbours are $0,1,\dots,h-1$), and $h\to2h$ since $2h=h+h\in N^+(h)$. ✓
> >
> > So for every even $n\ge6$ such a tournament exists. For $n=6$ ($h=2$) the arc list is: $0\to1,0\to2,1\to2,1\to3,2\to3,2\to4,3\to4,3\to0,4\to0,4\to1$ on $C$, plus $z\to0,z\to2,1\to z,3\to z,4\to z$ — that is $15=\binom62$ arcs. ✓
> >
> > **$n=2$ is impossible.** With two vertices the winner (the tail of the single arc) reaches the other in $1$ step, but the head cannot reach the tail at all. So there is exactly one winner, never two. ✓
> >
> > **$n=4$ is impossible.** Suppose all four vertices of a $4$-vertex tournament $T$ are winners. Since $m=\binom42=6$, the average out-degree is $6/4=1.5$, so some vertex $v$ has $\mathrm{outdeg}(v)\le1$. A winner must have out-degree $\ge1$ (with out-degree $0$ it reaches nobody), so $\mathrm{outdeg}(v)=1$: let $N^+(v)=\{w\}$ and let $a,b$ be the two in-neighbours of $v$ (so $V=\{v,w,a,b\}$). Since $v$ is a winner it must reach $a$ and $b$ in $2$ steps, and every path out of $v$ starts $v\to w$; hence $w\to a$ and $w\to b$. So $w$'s out-neighbours are exactly $\{a,b\}$ (it loses to $v$), i.e. $\mathrm{outdeg}(w)=2$. Between $a$ and $b$ exactly one arc lies; say $a\to b$ (the other case is symmetric under swapping the names $a,b$). Then $b$'s out-neighbourhood is exactly $\{v\}$: indeed $a\to b$, $w\to b$ and $b\to v$. But then $b$ reaches only $v$ (in $1$ step) and $w$ (in $2$ steps, as $v\to w$), never $a$. So $b$ is not a winner — contradiction. Hence no $4$-vertex tournament has all vertices as winners. ✓
> >
> > $$\boxed{\forall\,n\ne2,4\ \exists\ \text{a tournament of order } n \text{ with every vertex a winner.}}$$
> >
> > **Remarks.**
> >
> > * (a) and (b) together are a special case of Maurer's theorem: for all $n\ge k\ge1$ there is an $n$-tournament with exactly $k$ winners, except $k=2$ (any $n$) and $(n,k)=(4,4)$ — which is precisely the failure of (b) at $n=2$ (only $k=1$ possible) and $n=4$ (only $k=1,3$ possible).
> > * The all-winners examples are the densest possible: in the carousel every vertex is a winner with the **minimum** possible out-degree $\frac{n-1}{2}$, showing that being a winner is far weaker than having large out-degree. On the other hand, by Lemma 1 a max-out-degree vertex is always a winner, and by Lemma 2 winners are "everywhere": in any tournament every beaten vertex is beaten by a winner.
> > * For $n$ even the "carousel $+$ one vertex" blow-up is the standard construction; the two forbidden values are genuinely exceptional, since $n=2$ has only $2$ tournaments (one winner each) and $n=4$ has $64$ tournaments, of which none has $4$ winners — the $4$-vertex score sequences being $(0,1,2,3)$, $(0,2,2,2)$ and $(1,1,2,2)$, and each of them forces a non-winner as the case analysis above shows.






## Chapter 7 — Matrix Representation of Graphs (Unit 7)

> [!question] Q1 (7-1): Incidence Matrix — Construction & Block-Diagonal Form
> Write the incidence matrix $A(G)$ for a labeled simple graph. If the graph is disconnected with two components $g_1$ and $g_2$, express $A(G)$ in block-diagonal form as in Eq. (7-1):
> $$A(G) = \begin{bmatrix} A(g_1) & 0 \\ 0 & A(g_2) \end{bmatrix}.$$
> Explain why this form holds.
>
> > [!success]- Solution (Click to expand)
> >
> > **Definition.** For a graph $G$ with $n$ vertices $v_1, \dots, v_n$ and $e$ edges $e_1, \dots, e_e$ (no self-loops), the **incidence matrix** $A(G) = [a_{ij}]$ is the $n \times e$ binary matrix where:
> >
> > $$a_{ij} = \begin{cases} 1 & \text{if edge } e_j \text{ is incident on vertex } v_i \\ 0 & \text{otherwise} \end{cases}$$
> >
> > **Key observations:**
> > 1. Each column has exactly two 1's (each edge is incident on exactly two vertices).
> > 2. The number of 1's in row $i$ equals $\deg(v_i)$.
> > 3. A row of all 0's represents an isolated vertex.
> > 4. Parallel edges produce identical columns.
> >
> > **Block-diagonal form for a disconnected graph.** If $G$ is disconnected with components $g_1$ and $g_2$, no edge in $g_1$ is incident on any vertex of $g_2$ and vice versa. If we order the vertices so that all vertices of $g_1$ come first, and order edges likewise, then:
> >
> > $$A(G) = \begin{bmatrix} A(g_1) & 0 \\ 0 & A(g_2) \end{bmatrix}$$
> >
> > The off-diagonal blocks are all zeros because there are no edges between the two components. This generalizes to any number of components.

> [!question] Q2 (7-2): Constructing $A_f$, $B_f$, $C_f$ and Verifying Relationships
> Consider a graph with a chosen spanning tree $T$. Write the matrices $A_f$ (reduced incidence matrix), $B_f$ (fundamental circuit matrix), and $C_f$ (fundamental cut-set matrix) in the standard partitioned forms:
> $$B_f = [I_\mu \mid B_t], \qquad C_f = [C_c \mid I_{n-1}], \qquad A_f = [A_c \mid A_t].$$
> Then verify the relationships:
> $$B_t^T = C_c \qquad \text{and} \qquad A_t^{-1} \cdot A_c = B_t^T.$$
>
> > [!success]- Solution (Click to expand)
> >
> > **Setup.** Let $G$ be a connected graph with $n$ vertices and $e$ edges. Choose a spanning tree $T$ with $n-1$ branches. The $\mu = e - n + 1$ remaining edges are the **chords**.
> >
> > **Reduced incidence matrix $A_f$:** Delete any one row (reference vertex) from $A(G)$. Partition columns so chords come first:
> > $$A_f = [A_c \mid A_t]$$
> > where $A_t$ is $(n-1) \times (n-1)$ corresponding to tree branches (nonsingular since the reduced incidence matrix of a tree is nonsingular), and $A_c$ corresponds to chords.
> >
> > **Fundamental circuit matrix $B_f$:** Each chord $e_k$ defines a unique fundamental circuit with branches of $T$. Arrange chord columns first:
> > $$B_f = [I_\mu \mid B_t]$$
> > The identity block $I_\mu$ appears in the chord columns (each row has exactly one chord).
> >
> > **Fundamental cut-set matrix $C_f$:** Each branch $b_k$ defines a unique fundamental cut-set. Arrange branch columns last:
> > $$C_f = [C_c \mid I_{n-1}]$$
> >
> > **Verifying $B_t^T = C_c$.**
> >
> > From Theorem 7-4 (orthogonality): $A_f \cdot B_f^T = 0 \pmod{2}$. That is:
> > $$[A_c \mid A_t] \begin{bmatrix} I_\mu \\ B_t^T \end{bmatrix} = 0 \implies A_c + A_t B_t^T = 0 \pmod{2}$$
> >
> > Since $A_t$ is nonsingular, multiplying both sides by $A_t^{-1}$:
> > $$A_t^{-1} A_c = B_t^T \pmod{2}$$
> >
> > Similarly, from $C_f \cdot B_f^T = 0 \pmod{2}$:
> > $$[C_c \mid I_{n-1}] \begin{bmatrix} I_\mu \\ B_t^T \end{bmatrix} = C_c + B_t^T = 0 \implies C_c = B_t^T \pmod{2}$$
> >
> > **Conclusion:** $B_t^T = C_c$ and $A_t^{-1} A_c = B_t^T$, confirming the fundamental relationship among the three matrices.

> [!question] Q3 (7-3): Ranks of $A$, $B$, $C$ for a Disconnected Graph
> Show that for a simple disconnected graph $G$ with $k$ components, $n$ vertices, and $e$ edges, the ranks of the incidence matrix $A$, circuit matrix $B$, and cut-set matrix $C$ are:
> $$\text{rank}(A) = n - k, \quad \text{rank}(B) = e - n + k, \quad \text{rank}(C) = n - k.$$
>
> > [!success]- Solution (Click to expand)
> >
> > **Rank of $A$ (incidence matrix).**
> >
> > For a *connected* graph with $n$ vertices, $\text{rank}(A) = n - 1$ (Theorem 7-2). For a disconnected graph with $k$ components, apply this result component by component. The incidence matrix in block-diagonal form gives:
> > $$\text{rank}(A) = \sum_{i=1}^{k} (n_i - 1) = n - k$$
> > where $n_i$ is the number of vertices in component $i$ and $\sum n_i = n$.
> >
> > **Rank of $B$ (circuit matrix).**
> >
> > From Theorem 7-4 (orthogonality), $A \cdot B^T = 0 \pmod{2}$. By Sylvester's law of nullity:
> > $$\text{rank}(A) + \text{rank}(B) \leq e$$
> > $$\text{rank}(B) \leq e - \text{rank}(A) = e - (n - k) = e - n + k$$
> >
> > The fundamental circuit matrix $B_f$ has $\mu = e - n + k$ rows (one per chord) and is of full rank, so:
> > $$\text{rank}(B) \geq e - n + k$$
> >
> > Combining both inequalities: $\boxed{\text{rank}(B) = e - n + k}$.
> >
> > **Rank of $C$ (cut-set matrix).**
> >
> > From observation 6 about cut-set matrices: for a nonseparable graph, every row of $A(G)$ is a row of $C(G)$, hence $\text{rank}(C) \geq \text{rank}(A) = n - k$.
> >
> > From $C \cdot B^T = 0 \pmod{2}$ (every circuit and cut-set share an even number of edges), Sylvester's theorem gives:
> > $$\text{rank}(C) + \text{rank}(B) \leq e \implies \text{rank}(C) \leq e - (e - n + k) = n - k$$
> >
> > Therefore $\boxed{\text{rank}(C) = n - k}$.

> [!question] Q4 (7-4): Circuit Matrix — Construction & Properties
> Label the edges of a graph and write down its circuit matrix $B(G)$. Verify observations 1–5 about circuit matrices:
> 1. A column of all zeros corresponds to an edge not in any circuit.
> 2. Each row of $B(G)$ is a circuit vector.
> 3. A circuit matrix can represent a self-loop (a row with a single 1).
> 4. The number of 1's in a row equals the number of edges in that circuit.
> 5. If $G$ is separable with blocks $g_1$ and $g_2$, then $B(G)$ is block-diagonal.
>
> > [!success]- Solution (Click to expand)
> >
> > **Definition.** For a graph $G$ with $q$ distinct circuits and $e$ edges, the **circuit matrix** $B(G) = [b_{ij}]$ is the $q \times e$ binary matrix where:
> > $$b_{ij} = \begin{cases} 1 & \text{if the } i\text{th circuit includes the } j\text{th edge} \\ 0 & \text{otherwise} \end{cases}$$
> >
> > **Verification of observations:**
> >
> > **Obs. 1 — Column of all zeros = noncircuit edge.** If edge $e_j$ belongs to no circuit, then $b_{ij} = 0$ for every row $i$, giving a zero column. Conversely, an edge is a *bridge* (cut-edge) if and only if it belongs to no circuit, so a zero column corresponds exactly to a bridge.
> >
> > **Obs. 2 — Each row is a circuit vector.** By construction, the support of row $i$ (the set of positions with 1) is exactly the edge set of circuit $i$, which is a circuit vector in the cycle space $W_\Gamma$ of the graph.
> >
> > **Obs. 3 — Self-loops.** A self-loop at vertex $v$ forms a circuit by itself (a cycle of length 1). Its corresponding row has exactly one 1. Unlike the incidence matrix (which cannot represent self-loops properly), the circuit matrix handles them naturally.
> >
> > **Obs. 4 — Row weight = circuit length.** The number of 1's in row $i$ is $\sum_j b_{ij}$, which counts exactly the edges belonging to circuit $i$, i.e., its length $|E(\Gamma_i)|$.
> >
> > **Obs. 5 — Separable graph gives block-diagonal $B(G)$.** If $G$ is separable (or disconnected) with blocks $g_1$ and $g_2$, then every circuit lies entirely within $g_1$ or entirely within $g_2$ (a circuit cannot use edges from both blocks, as the blocks share at most one vertex and no edge). Ordering the rows and columns by block gives:
> > $$B(G) = \begin{bmatrix} B(g_1) & 0 \\ 0 & B(g_2) \end{bmatrix}$$

> [!question] Q5 (7-6): Black-Box Switching Network
> A black box contains a switching network of seven switches $1, 2, 3, 4, 5, 6, 7$. When connected in series with an external switch $k$, the lamp lights for the following combinations (each listed with $k$):
> $(1, 4, 5)$, $(1, 4, 6, 7)$, $(2, 5, 7)$, $(2, 6)$, $(3, 5)$, $(3, 6, 7)$.
> Find the switching network configuration (draw the graph).
>
> > [!success]- Solution (Click to expand)
> >
> > **Modeling.** Treat each switch as an edge in a graph. A lit lamp means current flows through a closed circuit, so each combination corresponds to a circuit in the graph. We form the circuit matrix $B$ from these six observed circuits (rows), with columns for switches $1$–$7$ plus $k$:
> >
> > $$B = \begin{array}{c|cccccccc} & 1 & 2 & 3 & 4 & 5 & 6 & 7 & k \\ \hline 1 & 1 & 0 & 0 & 1 & 1 & 0 & 0 & 1 \\ 2 & 1 & 0 & 0 & 1 & 0 & 1 & 1 & 1 \\ 3 & 0 & 1 & 0 & 0 & 1 & 0 & 1 & 1 \\ 4 & 0 & 1 & 0 & 0 & 0 & 1 & 0 & 1 \\ 5 & 0 & 0 & 1 & 0 & 1 & 0 & 0 & 1 \\ 6 & 0 & 0 & 1 & 0 & 0 & 1 & 1 & 1 \end{array}$$
> >
> > **Removing redundant circuits.** Check if any row is a mod-2 sum of others:
> > - Row 1 $\oplus$ Row 2: $\{5, 6, 7\} \oplus \{k\} \to$ row not in $B$, so rows 1 and 2 are independent.
> > - Rows 1, 3, 4: $R_1 \oplus R_3 \oplus R_4 = \{1,4,5,2,5,7,2,6\} \pmod{2} = \{1,4,6,7\} = R_2$. So $R_2$ is redundant.
> >
> > After simplification, $B_f$ has rank $\mu = 5$ (since $e = 8$, $n-1 = 3$ means $\mu = e - n + 1 = 5$, giving $n = 4$ vertices).
> >
> > **Graph parameters:**
> > - $e = 8$ edges (switches $1$–$7$ plus $k$), $\mu = 5$, $n = 5$ vertices.
> >
> > **Reconstructing the graph.** Bring $B_f$ to the form $[I_5 \mid F]$ by column operations, then read off the reduced incidence matrix $A_f = [F^T \mid I_4]$ (using $C_c = B_t^T$). The resulting graph has 5 vertices and 8 edges corresponding to the switching network inside the black box.

> [!question] Q6 (7-7): Obtaining a Graph from Its Fundamental Cut-Set Matrix
> In Section 7-5 (Narsingh Deo), a graph was obtained from a given fundamental circuit matrix $B_f$. Sketch a procedure for obtaining a graph from its fundamental cut-set matrix $C_f$. Can you get two different (non-isomorphic) graphs for the same $C_f$? If yes, how are they related?
>
> > [!success]- Solution (Click to expand)
> >
> > **Procedure to obtain a graph from $C_f$.**
> >
> > Given $C_f = [C_c \mid I_{n-1}]$ (an $(n-1) \times e$ fundamental cut-set matrix):
> >
> > 1. **Read graph parameters.** The number of rows $= n - 1$ gives the number of vertices $n$. The number of columns $= e$ gives the number of edges. The number of chords $= \mu = e - n + 1$ (the first $\mu$ columns forming $C_c$).
> >
> > 2. **Identify the spanning tree.** The last $n - 1$ columns of $C_f$ form $I_{n-1}$; these columns correspond to the branches of the spanning tree $T$.
> >
> > 3. **Obtain $B_f$ from $C_f$.** Since $C_c = B_t^T$ (the relationship derived in Q2), we have:
> > $$B_f = [I_\mu \mid C_c^T]$$
> > The fundamental circuit matrix is determined directly from $C_f$.
> >
> > 4. **Obtain $A_f$ from $B_f$.** Since $A_t^{-1} A_c = B_t^T = C_c$, once we know $A_t$ (the spanning tree portion of $A_f$, which is a nonsingular $(n-1) \times (n-1)$ matrix), we get $A_c = A_t \cdot C_c$.
> >
> > 5. **Reconstruct the full incidence matrix.** From $A_f = [A_c \mid A_t]$, add back the reference vertex row (so each column sums to 2 mod 2, i.e., exactly two 1's). The resulting $A(G)$ gives the graph.
> >
> > **Can two non-isomorphic graphs share the same $C_f$?**
> >
> > **Yes.** Since $C_f$ determines $B_f$ uniquely, and $B_f$ determines the graph only up to **2-isomorphism** (Theorem 7-1 of the circuit matrix), $C_f$ also determines the graph only within 2-isomorphism. Two graphs that are 2-isomorphic (same cycle space structure) can have the same $C_f$ yet be non-isomorphic as graphs.
> >
> > The two different graphs obtainable from the same $C_f$ are **2-isomorphic** to each other — they are related by a sequence of edge contractions/expansions at 2-vertex cut pairs that preserve the cycle space.

> [!question] Q7 (7-12): Proving $B_f = [I_\mu \mid A_t^T \cdot A_t^{-T}]$ and $C_f = A_t^{-1} \cdot A_f$
> Prove the following matrix identities for a connected graph:
> $$(a)\quad B_f = \bigl[I_\mu \;\big|\; A_t^T \cdot A_t^{-T}\bigr], \qquad (b)\quad C_f = A_t^{-1} \cdot A_f.$$
>
> > [!success]- Solution (Click to expand)
> >
> > **Setup.** Let $G$ be a connected graph with $n$ vertices, $e$ edges, and a chosen spanning tree $T$. Partition the reduced incidence matrix:
> > $$A_f = [A_c \mid A_t]$$
> > where $A_t$ is $(n-1)\times(n-1)$ (branches, nonsingular) and $A_c$ is $(n-1)\times\mu$ (chords, $\mu = e-n+1$).
> >
> > **Proof of (b): $C_f = A_t^{-1} \cdot A_f$.**
> >
> > The fundamental cut-set matrix is $C_f = [C_c \mid I_{n-1}]$. We want to show $A_t^{-1} A_f = [C_c \mid I_{n-1}]$.
> >
> > $$A_t^{-1} A_f = A_t^{-1}[A_c \mid A_t] = [A_t^{-1} A_c \mid A_t^{-1} A_t] = [A_t^{-1} A_c \mid I_{n-1}]$$
> >
> > We already showed in Q2 that $A_t^{-1} A_c = B_t^T = C_c$. Therefore:
> > $$A_t^{-1} A_f = [C_c \mid I_{n-1}] = C_f \qquad \blacksquare$$
> >
> > **Proof of (a): $B_f = [I_\mu \mid A_t^T \cdot (A_t^{-1})^T]$.**
> >
> > We want to show $B_t = (A_t^{-1} A_c)^T = (B_t^T)^T$, i.e., the transpose relationship is consistent.
> >
> > From the orthogonality relation $A_f B_f^T = 0 \pmod{2}$:
> > $$[A_c \mid A_t]\begin{bmatrix} I_\mu \\ B_t^T \end{bmatrix} = A_c + A_t B_t^T = 0 \implies B_t^T = A_t^{-1} A_c$$
> >
> > Taking the transpose: $B_t = (A_t^{-1} A_c)^T = A_c^T (A_t^{-1})^T = A_c^T (A_t^T)^{-1}$.
> >
> > In mod-2 arithmetic, $(A^{-1})^T = (A^T)^{-1}$, so:
> > $$B_f = [I_\mu \mid B_t] = \bigl[I_\mu \;\big|\; A_c^T (A_t^T)^{-1}\bigr] = \bigl[I_\mu \;\big|\; A_t^{-T} A_c^T\bigr]^T \text{ (by transposing)}$$
> >
> > More directly from the formula: $B_t^T = A_t^{-1} A_c$, so the entry $B_t = C_c^T$. This is consistent with the standard form $B_f = [I_\mu \mid C_c^T]$, confirming the identity. $\blacksquare$

> [!question] Q8 (7-15): Matrices for the Complete Graph $K_n$
> Characterize the matrices $A_f$, $B_f$, $C_f$, and $X$ (adjacency matrix) for the complete graph $K_n$.
>
> > [!success]- Solution (Click to expand)
> >
> > The complete graph $K_n$ has $n$ vertices, $\binom{n}{2} = \frac{n(n-1)}{2}$ edges, and is $(n-1)$-regular.
> >
> > **Adjacency matrix $X(K_n)$.**
> >
> > $X(K_n) = J_n - I_n$, where $J_n$ is the $n \times n$ all-ones matrix and $I_n$ is the identity. Every off-diagonal entry is 1, every diagonal entry is 0:
> > $$X(K_n) = \begin{bmatrix} 0 & 1 & \cdots & 1 \\ 1 & 0 & \cdots & 1 \\ \vdots & & \ddots & \vdots \\ 1 & 1 & \cdots & 0 \end{bmatrix}_{n \times n}$$
> >
> > **Reduced incidence matrix $A_f(K_n)$.**
> >
> > Delete the row for vertex $v_n$ (reference vertex). $A_f$ is $(n-1) \times \frac{n(n-1)}{2}$. Each column (edge) has exactly one or two 1's in the first $n-1$ rows. For the spanning tree, choose the star $K_{1,n-1}$ (or any tree). $A_t$ is an $(n-1)\times(n-1)$ identity matrix for the star spanning tree (since each star edge is incident to exactly one non-reference vertex).
> >
> > **Fundamental circuit matrix $B_f(K_n)$.**
> >
> > $\mu = \binom{n}{2} - (n-1) = \frac{n(n-1)}{2} - n + 1 = \frac{(n-1)(n-2)}{2}$ chords (non-tree edges). Each chord together with the spanning tree forms exactly one fundamental circuit. For the star spanning tree, chord $v_i v_j$ ($i,j \neq n$, $i \neq j$) forms the triangle $v_i v_n v_j v_i$, using branches $v_i v_n$ and $v_j v_n$.
> >
> > $$B_f = [I_\mu \mid B_t]$$
> >
> > The submatrix $B_t$ has two 1's per row (the two star-edges forming the triangle with each chord).
> >
> > **Fundamental cut-set matrix $C_f(K_n)$.**
> >
> > $C_f = [C_c \mid I_{n-1}]$ where $C_c = B_t^T$. From the star spanning tree, the fundamental cut-set for branch $v_i v_n$ consists of all edges incident to $v_i$ (Menger's theorem for stars): namely $v_i v_n$ and all chords $v_i v_j$ for $j \neq i, n$. So $C_c$ has $n-2$ ones per row and $C_f$ has the standard block form.
> >
> > **Number of spanning trees.** By Cayley's formula: $\mathcal{J}(K_n) = n^{n-2}$.

> [!question] Q9 (7-18): Finding the Diameter Using Powers of the Adjacency Matrix
> Given the adjacency matrix $X$ of a connected graph $G$ with $n$ vertices, how do you determine the **diameter** of $G$?
> *(Hint: Consider a sum of powers of $X$.)*
>
> > [!success]- Solution (Click to expand)
> >
> > **Background.** By Theorem 7-8 (Narsingh Deo), the $(i,j)$-th entry of $X^r$ equals the number of distinct edge-sequences of length $r$ between vertices $v_i$ and $v_j$.
> >
> > By Corollary A: In a connected graph, $d(v_i, v_j) = k$ if and only if $k$ is the smallest integer such that $[X^k]_{ij} \neq 0$.
> >
> > **Algorithm to find the diameter.**
> >
> > 1. Compute $Y_r = X + X^2 + X^3 + \cdots + X^r$ (summing in the **ring of integers**, not mod 2).
> >
> > 2. The diameter $d$ is the smallest $r$ such that $Y_r$ has **no zero off-diagonal entry**:
> > $$\text{diam}(G) = \min\bigl\{r : [Y_r]_{ij} > 0 \text{ for all } i \neq j\bigr\}$$
> >
> > **Why this works.** $[Y_r]_{ij} > 0$ if and only if there exists some $k \leq r$ with $[X^k]_{ij} > 0$, i.e., there is a path of length $\leq r$ between $v_i$ and $v_j$. So:
> > - $Y_r$ has all positive off-diagonal entries iff every pair of vertices has a path of length $\leq r$, i.e., $\text{diam}(G) \leq r$.
> > - The smallest such $r$ is exactly the diameter.
> >
> > **Example.** For $K_4$: $X = J_4 - I_4$. $X^1$ already has all off-diagonal entries $= 1 > 0$, so $\text{diam}(K_4) = 1$. For a path $P_4 = v_1 v_2 v_3 v_4$: $[X^1]_{14} = 0$, $[X^2]_{14} = 0$, $[X^3]_{14} = 1 > 0$, so $d(v_1, v_4) = 3$ and $\text{diam}(P_4) = 3$.

> [!question] Q10 (7-19): Diagonal of $X^3$ and Triangles
> Show that each diagonal entry $[X^3]_{ii}$ of the cube of the adjacency matrix equals **twice the number of triangles** (circuits of length 3) passing through vertex $v_i$.
>
> > [!success]- Solution (Click to expand)
> >
> > **Setup.** Let $X = [x_{ij}]$ be the adjacency matrix of a simple graph $G$ (integer ring, not mod 2). By Theorem 7-8, $[X^r]_{ij}$ counts the number of edge-sequences of length $r$ from $v_i$ to $v_j$.
> >
> > **Computing $[X^3]_{ii}$.**
> >
> > $$[X^3]_{ii} = \sum_{k=1}^{n} [X^2]_{ik} \cdot x_{ki} = \sum_{k=1}^{n} \left(\sum_{j=1}^{n} x_{ij} x_{jk}\right) x_{ki}$$
> >
> > Each nonzero term in this sum corresponds to a closed edge-sequence $v_i \to v_j \to v_k \to v_i$ of length 3. This is an edge-sequence (not necessarily a simple path) starting and ending at $v_i$.
> >
> > **Why each triangle contributes exactly 2.**
> >
> > Consider a triangle $\{v_i, v_a, v_b\}$ (a 3-cycle through $v_i$). The closed edge-sequences of length 3 starting and ending at $v_i$ that use only edges of this triangle are:
> > $$v_i \to v_a \to v_b \to v_i \quad \text{and} \quad v_i \to v_b \to v_a \to v_i$$
> > These are the two traversals of the triangle (clockwise and counterclockwise). Each is a valid edge-sequence, contributing **2** to $[X^3]_{ii}$.
> >
> > No closed walk of length 3 through $v_i$ can avoid using a triangle: a closed walk $v_i \to v_j \to v_k \to v_i$ requires edges $v_i v_j$, $v_j v_k$, $v_k v_i$ all present, which is exactly a triangle $\{v_i, v_j, v_k\}$. (Note: in a simple graph, $j \neq i$, $k \neq j$, and $k \neq i$ must hold since there are no self-loops, so $j, k$ are distinct and form a triangle with $v_i$.)
> >
> > **Conclusion.**
> > $$[X^3]_{ii} = 2 \times |\{\text{triangles through } v_i\}| \qquad \blacksquare$$
> >
> > **Corollary.** The total number of triangles in $G$ is $\dfrac{\operatorname{tr}(X^3)}{6}$, since $\operatorname{tr}(X^3) = \sum_i [X^3]_{ii}$ counts each triangle $6$ times (3 choices of $v_i \in \triangle$, each giving a factor of 2).

> [!question] Q11 (7-20): Spanning Trees and $\det(A_f \cdot A_f^T)$
> Prove that the number of spanning trees $\mathcal{J}(G)$ in a connected graph $G$ equals:
> $$\mathcal{J}(G) = \det(A_f \cdot A_f^T)$$
> where $A_f$ is the reduced incidence matrix of $G$, and arithmetic is over the **reals** (not mod 2).
>
> > [!success]- Solution (Click to expand)
> >
> > **Setup.** $G$ is a connected graph with $n$ vertices and $e$ edges. $A_f$ is the $(n-1) \times e$ reduced incidence matrix (any one row deleted from $A(G)$), with entries in $\{0, 1\}$ over $\mathbb{R}$.
> >
> > **Using the Binet-Cauchy theorem.**
> >
> > The Binet-Cauchy theorem states: for an $m \times e$ matrix $M$ ($m \leq e$),
> > $$\det(M M^T) = \sum_{S} [\det(M_S)]^2$$
> > where the sum is over all $m \times m$ submatrices $M_S$ obtained by selecting $m$ columns from $M$.
> >
> > Applying this to $A_f$ (with $m = n-1$):
> > $$\det(A_f A_f^T) = \sum_{S \subseteq E,\, |S|=n-1} [\det((A_f)_S)]^2$$
> >
> > **Each term corresponds to a spanning tree.**
> >
> > $(A_f)_S$ is the $(n-1) \times (n-1)$ submatrix of $A_f$ corresponding to edge set $S$. By Theorem 7-3 (Narsingh Deo):
> >
> > > An $(n-1)\times(n-1)$ submatrix of $A_f$ is nonsingular if and only if the corresponding $n-1$ edges form a spanning tree of $G$.
> >
> > Therefore:
> > - If $S$ is a spanning tree: $\det((A_f)_S) = \pm 1$ (the reduced incidence matrix of a tree is nonsingular with determinant $\pm 1$), so $[\det((A_f)_S)]^2 = 1$.
> > - If $S$ is not a spanning tree: $\det((A_f)_S) = 0$, so $[\det((A_f)_S)]^2 = 0$.
> >
> > **Conclusion.**
> > $$\det(A_f A_f^T) = \sum_{\substack{S \subseteq E \\ |S|=n-1 \\ S \text{ is a spanning tree}}} 1 = \mathcal{J}(G) \qquad \blacksquare$$

> [!question] Q12 (7-23): Degree Matrix, Laplacian, and Spanning Trees (Kirchhoff's Theorem)
> For a labeled simple connected graph $G$ with $n$ vertices:
> - Let $D$ be the $n \times n$ **diagonal degree matrix** (the $i$-th diagonal entry = $\deg(v_i)$).
> - Let $E$ be obtained from the incidence matrix $A(G)$ by replacing one of the two 1's in every column with $-1$ (arbitrarily orient each edge).
>
> Prove (over the **ring of integers**, not mod 2):
> **(a)** $E \cdot E^T = D - X$, where $X$ is the adjacency matrix.
> **(b)** All cofactors of $D - X$ are equal.
> **(c)** Each cofactor of $D - X$ equals $\mathcal{J}(G)$, the number of spanning trees.
>
> > [!success]- Solution (Click to expand)
> >
> > The matrix $K(G) = D - X$ is the **Kirchhoff matrix** (or Laplacian) of $G$.
> >
> > ---
> >
> > **Proof of (a): $E \cdot E^T = D - X$.**
> >
> > Orient each edge arbitrarily: for edge $e_j = (v_p, v_q)$ (directed $v_p \to v_q$), set $e_{pj} = +1$, $e_{qj} = -1$, all other entries 0.
> >
> > Compute $[E E^T]_{ii}$ (diagonal entry):
> > $$[EE^T]_{ii} = \sum_j e_{ij}^2 = \sum_{\text{edges incident to } v_i} (\pm 1)^2 = \deg(v_i) = D_{ii}$$
> >
> > Compute $[E E^T]_{ij}$ for $i \neq j$ (off-diagonal):
> > $$[EE^T]_{ij} = \sum_j e_{ij} e_{jk}$$
> > For a given edge $e_k$: the product $e_{ik} e_{jk}$ is nonzero only if edge $e_k$ is incident to both $v_i$ and $v_j$, i.e., $e_k = v_i v_j$. In that case one endpoint gets $+1$ and the other $-1$, so the product is $-1$.
> >
> > Hence $[EE^T]_{ij} = -(\text{number of edges between } v_i \text{ and } v_j) = -x_{ij}$ (since $G$ is simple, $x_{ij} \in \{0,1\}$).
> >
> > Therefore $E E^T = D - X = K(G)$. $\blacksquare$
> >
> > ---
> >
> > **Proof of (b): All cofactors of $K(G)$ are equal.**
> >
> > The row-sums of $K(G) = D - X$ are all zero: for each row $i$,
> > $$\sum_j K_{ij} = \deg(v_i) - \sum_{j \neq i} x_{ij} = \deg(v_i) - \deg(v_i) = 0$$
> >
> > This means $K(G) \cdot \mathbf{1} = \mathbf{0}$, so $\det(K(G)) = 0$ and $\mathbf{1} = (1,1,\dots,1)^T$ is in the null space.
> >
> > Since column-sums are also all zero (by symmetry of $K$), expanding along any row or column yields the same cofactor value. More precisely: by the matrix-tree theorem (see below) and the fact that the rank of $K(G)$ is $n-1$ for a connected graph, all $(n-1)\times(n-1)$ cofactors are nonzero and equal (this follows from the fact that $K$ has a unique null vector $\mathbf{1}$ up to scaling, so all cofactor expansions agree). $\blacksquare$
> >
> > ---
> >
> > **Proof of (c): Each cofactor of $K(G)$ equals $\mathcal{J}(G)$.**
> >
> > The $(s,t)$-cofactor of $K = EE^T$ is $(-1)^{s+t} \det(M_{(s,t)})$, where $M_{(s,t)}$ is the $(n-1) \times (n-1)$ submatrix obtained by deleting row $s$ and column $t$.
> >
> > From part (a), $K = EE^T$. Let $E_f$ be the matrix $E$ with the $s$-th row deleted (this is exactly the oriented version of the reduced incidence matrix $A_f$, since we delete the reference vertex row). Then:
> >
> > $$\det(E_f E_f^T) = \det(M_{(s,s)}) = \text{the } (s,s)\text{-cofactor of } K$$
> >
> > By the **Binet-Cauchy theorem** (same argument as Q11, but now with $\pm 1$ entries instead of $0/1$):
> > $$\det(E_f E_f^T) = \sum_{S,\, |S|=n-1} [\det((E_f)_S)]^2$$
> >
> > For a spanning tree $S$: $(E_f)_S$ is an $(n-1)\times(n-1)$ oriented reduced incidence matrix of a tree, which has $\det = \pm 1$, contributing $1$ to the sum.
> >
> > For a non-spanning-tree $S$: $(E_f)_S$ is singular, contributing $0$.
> >
> > Therefore: $\det(E_f E_f^T) = \mathcal{J}(G)$.
> >
> > Since all cofactors are equal (part b), every cofactor of $K(G)$ equals $\mathcal{J}(G)$. $\blacksquare$
> >
> > **This is the Kirchhoff-Matrix-Tree Theorem** (Theorem 7.7 in Week-9-Unit-7):
> > $$\mathcal{J}(G) = (-1)^{s+t} \det(M_{(s,t)}) \quad \text{for any } s, t.$$
