---
title: Computer Graphics — Post-Midsem Notes
tags:
  - computer-graphics
  - CG
  - projection
  - clipping
  - hidden-surfaces
  - rasterization
---

# Post-Midsem — 3D Viewing, Clipping, Hidden Surfaces, Rasterization and Animation

This block carries the course from a scene described in three dimensions to the pixels that finally appear on the screen. Every deck in it is one **stage of the viewing pipeline**: build the camera frame and the view volume (§1), clip what falls outside it — lines first, then filled polygons and 3D faces (§2–§3), decide which of the surviving surfaces is actually seen (§4–§5), convert the surviving areas into pixels (§6), and then repair the damage that discretisation does to those pixels (§7). The last deck leaves the geometry behind and animates it (§8).

> [!info] How the block is organised
> | Topic | Deck | Slides | Question it answers |
> | --- | --- | --- | --- |
> | 1 | [[CG_29_Sep.pdf]] | 78 | Where is the camera, what can it see, and how does 3D become a 2D coordinate? |
> | 2 | [[CG_Oct_1.pdf]] | 97 | How is the 2D image placed on the screen, and how is a line trimmed to the window? |
> | 3 | [[CG_Oct_5.pdf]] | 89 | How is a *filled* polygon clipped, and how is a 3D face clipped? |
> | 4 | [[CG_Oct_8.pdf]] | 106 | Which faces point away, and which surface is nearest at each pixel? |
> | 5 | [[CG_26_Oct.pdf]] | 80 | How do we order whole polygons, and what if no order exists? |
> | 6 | [[CG-29th_Oct.pdf]] | 116 | How is the interior of a polygon filled, and how are characters drawn? |
> | 7 | [[CG_Nov-2.pdf]] | 70 | How is a jagged line made smooth? |
> | 8 | [[CG_Nov_Animation.pdf]] | 55 | How is motion produced from still drawings? |

> [!warning] The four conventions this block uses everywhere
> - **Right-handed** coordinates; **the viewer looks along $-z$** in the camera frame, so visible points have $z<0$.
> - **Depth grows inward**: a larger $z$ (or larger $|z|$, as the deck states it) means *farther from the eye*.
> - **Clip order** for polygons is **left → right → top → bottom**; for outcodes the bit order is **Far Near Top Bottom Right Left** (bit 5 … bit 0).
> - **Ties count as inside**: a point exactly on a clip boundary is retained, and a midpoint exactly on the line chooses E. Both are examinable choices, not accidents.

---

## 1. 3D Viewing, Camera and Projection Fundamentals

*Deck: [[CG_29_Sep.pdf]] — 78 slides. Compiles the pipeline overview, the world-to-view transform, the canonical view volume, the projection matrices and the viewport transform.*

### 1.1 The six stages in one picture

The deck opens by fixing the vocabulary for everything that follows: a renderer is a fixed sequence of six stages, and each stage changes either *what an object is* or *which coordinate system it lives in*.

![[CG - 3D Graphics Pipeline.excalidraw]]

| Stage | Operation | Coordinate change | What it decides |
| --- | --- | --- | --- |
| 1 · **Represent** | object representation | — | what geometry exists (mesh, implicit surface, particles) |
| 2 · **Model** | modelling transform | local → world | where each object sits in the shared scene |
| 3 · **Illuminate** | lighting + shading | — (world) | the colour of each surface point |
| 4 · **View** | viewing pipeline | world → camera → view plane → viewport | what the camera sees |
| 5 · **Rasterize** | scan conversion | continuous device → discrete pixels | which pixels are lit, and how brightly |
| 6 · **Display** | frame-buffer output | — | the image |

Two clarifications the deck insists on:

- **Lighting ≠ shading.** Lighting computes the colour at a *point* from the light source and material properties; shading *interpolates* those point results across a surface. Lighting is expensive and sparse, shading is cheap and dense.
- **Modelling ≠ viewing.** Both are affine transforms on the same points, but modelling builds the scene while viewing changes the observer. The scene is identical from every camera.

### 1.2 World-to-view: building the camera frame

The camera is specified in world coordinates by its position $\mathbf{o}$ and the direction it looks along. The viewing transform moves the world so that the camera sits at the origin looking down $-z$ — it changes the **coordinate frame**, and nothing else.

$$ \mathbf{n} = \frac{\mathbf{o}-\mathbf{l}}{\lVert \mathbf{o}-\mathbf{l}\rVert}, \qquad
   \mathbf{u} = \frac{\mathbf{v}_{up}\times\mathbf{n}}{\lVert \mathbf{v}_{up}\times\mathbf{n}\rVert}, \qquad
   \mathbf{v} = \mathbf{n}\times\mathbf{u} $$

The deck builds the matrix in three named steps — **translate**, **rotate**, **compose** — and then applies it:

1. **Translate** the camera position to the world origin with $T(-\mathbf{o})$.
2. **Rotate** so that the camera basis $\mathbf{u},\mathbf{v},\mathbf{n}$ coincides with the world axes; the rotation matrix has the basis vectors as its rows.
3. **Compose.** For column vectors, translation acts first, so the product is $\mathbf{R}\,T$:

$$ \boxed{\ M_{view} = \mathbf{R}\,T(-\mathbf{o}) =
\begin{bmatrix}
u_x & u_y & u_z & -\mathbf{u}\cdot\mathbf{o}\\
v_x & v_y & v_z & -\mathbf{v}\cdot\mathbf{o}\\
n_x & n_y & n_z & -\mathbf{n}\cdot\mathbf{o}\\
0 & 0 & 0 & 1
\end{bmatrix}\ } $$

> [!warning] The camera is not projected yet
> This is the single most common confusion in the block. $M_{view}$ only re-expresses points in the camera frame; it does not flatten anything, and a point behind the camera still gets coordinates. **Projection is a separate matrix applied afterwards**, and clipping is a separate operation again.

### 1.3 The view volume

After the viewing transform, the part of space the camera can record is a **view volume** bounded by six planes $x_{\min},x_{\max},y_{\min},y_{\max},z_{near},z_{far}$.

| Projection | Shape of the view volume | Parallel edges? | Object size with depth |
| --- | --- | --- | --- |
| **Parallel / orthographic** | parallelepiped (a box) | yes | constant |
| **Perspective** | frustum (truncated pyramid) | no | falls as $1/|z|$ |

Anything wholly outside the volume is **clipped away**; anything crossing a boundary is **trimmed**. Clipping is a pure efficiency device: every primitive that survives is cheaper than the ones that do not, because all later stages — projection divide, hidden-surface tests, scan conversion — only ever see the survivors.

### 1.4 Why normalise the volume to a canonical cube

The deck pauses on this question explicitly, because the answer explains half the matrices in the course.

> [!note] Why transform the view volume to a canonical cube
> - **One set of clip tests.** After normalisation every boundary is $x=\pm1$, $y=\pm1$, $z=\pm1$, so clipping and inside/outside tests are six comparisons against constants, with no per-scene parameters.
> - **One projection-independent pipeline.** Orthographic and perspective scenes reduce to the same cube, so everything downstream (clipping, hidden-surface removal, scan conversion) is written once.
> - **A fixed depth range.** $z\in[-1,1]$ gives the depth buffer a known range, so depth precision and the near/far mapping are decided in one place.
> - **Device independence.** The cube is dimensionless; resolution and aspect ratio are chosen later, at viewport mapping (§1.6).
> - **Hardware.** A fixed-function pipeline can hard-wire the comparisons.

The cost is a **non-uniform scale**: normalising a wide, shallow frustum squeezes it, and the perspective divide has already distorted distances. That is why depth must be interpolated *after* the divide, not before (the z-buffer section, §4.7, relies on this).

### 1.5 The projection matrices

Both projections are $4\times4$ matrices applied to homogeneous points $[x\;y\;z\;1]^{T}$; they differ only in what happens to $w$.

**Orthographic (parallel) projection** maps the box $[x_{\min},x_{\max}]\times[y_{\min},y_{\max}]\times[z_{near},z_{far}]$ onto $[-1,1]^{3}$ by scaling and translating each axis independently:

$$ M_{ortho} =
\begin{bmatrix}
\dfrac{2}{x_{\max}-x_{\min}} & 0 & 0 & -\dfrac{x_{\max}+x_{\min}}{x_{\max}-x_{\min}}\\[8pt]
0 & \dfrac{2}{y_{\max}-y_{\min}} & 0 & -\dfrac{y_{\max}+y_{\min}}{y_{\max}-y_{\min}}\\[8pt]
0 & 0 & \dfrac{-2}{z_{far}-z_{near}} & -\dfrac{z_{far}+z_{near}}{z_{far}-z_{near}}\\[8pt]
0 & 0 & 0 & 1
\end{bmatrix} $$

The third row carries the minus sign because the camera looks along $-z$: the near plane has the *larger* (less negative) $z$, and it must land on $-1$.

**Perspective projection** cannot be affine — equal world lengths must project to unequal screen lengths — so the matrix keeps $w$ alive and lets the homogeneous divide do the work:

$$ M_{persp} =
\begin{bmatrix}
\dfrac{2n}{r-l} & 0 & \dfrac{r+l}{r-l} & 0\\[6pt]
0 & \dfrac{2n}{t-b} & \dfrac{t+b}{t-b} & 0\\[6pt]
0 & 0 & -\dfrac{f+n}{f-n} & -\dfrac{2fn}{f-n}\\[6pt]
0 & 0 & -1 & 0
\end{bmatrix},
\qquad
\begin{aligned}
x_{ndc} &= \frac{x_{cam}}{-z_{cam}}\cdot\frac{2n}{r-l}+\dots\\
w &= -z_{cam}
\end{aligned} $$

The fourth row is the whole trick: it sets $w=-z_{cam}$, so dividing by $w$ multiplies $x$ and $y$ by $1/|z|$ — objects shrink with distance, and the frustum becomes a cube. Points at $z=0$ would divide by zero, which is exactly why the **near plane must be strictly in front of the eye**.

| Property | Orthographic | Perspective |
| --- | --- | --- |
| View volume | box | frustum |
| $w$ after transform | 1 | $-z_{cam}$ |
| Divide needed | no | yes |
| Parallel lines | stay parallel | converge at a vanishing point |
| Size vs depth | constant | $\propto 1/|z|$ |
| Typical use | CAD, architectural, 2D-style views | realistic rendering, games |

#### Why the matrix is not "just a divide"

Writing $x_{ndc}=x_{cam}/(-z_{cam})$ directly would be a per-vertex division with no matrix. Packing it into the fourth row means the *same* pipeline — multiply by a $4\times4$, then divide by $w$ — handles both projections, and clipping can be done in homogeneous space *before* the divide. That ordering matters: clipping after the divide would need special handling for points at or behind the eye.

### 1.6 Viewport mapping

The canonical cube (or the 2D window that survives clipping) is dimensionless. The **viewport** is the rectangle on the actual display, in device coordinates, where the image is drawn. Window-to-viewport mapping is the affine map between the two, and the deck derives it by solving one equation per axis.

> [!important] The viewport transformation, derived
> Match the two intervals proportionally — the window edge $W_{x1}$ must land on the viewport edge $V_{x1}$, and $W_{x2}$ on $V_{x2}$:
> $$ \frac{W_x-W_{x1}}{W_{x2}-W_{x1}} = \frac{V_x-V_{x1}}{V_{x2}-V_{x1}} $$
> Multiply by $(V_{x2}-V_{x1})$ and add $V_{x1}$:
> $$ V_x = \underbrace{\frac{V_{x2}-V_{x1}}{W_{x2}-W_{x1}}}_{s_x}\,W_x + \underbrace{(V_{x1}-s_xW_{x1})}_{t_x} $$
> Repeat on $y$ with $s_y=(V_{y2}-V_{y1})/(W_{y2}-W_{y1})$ and $t_y=V_{y1}-s_yW_{y1}$.

$$ \boxed{\ V_x = s_xW_x+t_x,\qquad V_y=s_yW_y+t_y\ } $$

In matrix form, with the third column free for depth:

$$ M_{wv} = \begin{bmatrix} s_x & 0 & 0 & t_x\\ 0 & s_y & 0 & t_y\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix} $$

**Worked example.** Map the window $[-1,1]^{2}$ onto a $640\times480$ viewport whose lower-left corner is the origin. Then $s_x=640/2=320$, $t_x=0-320(-1)=320$, and $s_y=480/2=240$, $t_y=240$. A point in the middle of the window, $(0,0)$, lands at $(320,240)$ — the centre of the screen; the window corner $(-1,-1)$ lands at $(0,0)$; and $(0.5,-0.5)$ lands at $(480,120)$. Because the map is affine, straight lines stay straight and the midpoint of a segment stays the midpoint — which is what makes the transform safe to apply to vertices only.

> [!warning] The y-flip trap
> Window coordinates grow **upward**, device coordinates usually grow **downward**. When the viewport's origin is top-left, the correct scale is
> $$ s_y = -\frac{V_{y2}-V_{y1}}{W_{y2}-W_{y1}}, $$
> and everything else follows from the same two-point derivation. Applying the un-flipped formula produces a vertically mirrored image — a classic lab error that looks like a modelling mistake.

> [!warning] Aspect-ratio distortion
> $s_x$ and $s_y$ are independent, so a square window mapped onto a non-square viewport becomes a rectangle. A circle becomes an ellipse. Guard against it by choosing the viewport aspect to equal the window aspect, or by scaling both axes with the same factor and letter-boxing the remainder.

### 1.7 Exam pointer

> [!tip] Exam pointer — viewing and projection
> - Write $M_{view}=\mathbf{R}\,T(-\mathbf{o})$ and say what each factor does; be ready to explain why translation comes first.
> - State the two view-volume shapes and which projection produces which.
> - Give three reasons for the canonical cube, and the one cost (non-uniform scale).
> - Know which matrix needs the divide and why: $w=-z_{cam}$ in the perspective matrix.
> - Derive $V_x=s_xW_x+t_x$ from the proportion; quote $s_x,t_x,s_y,t_y$; then apply them to a numeric window and viewport.
> - Name the two traps: the $y$-flip and the aspect ratio.

---

## 2. Viewport Mapping and Cohen–Sutherland Clipping

*Deck: [[CG_Oct_1.pdf]] — 97 slides. Point clipping, the 4-bit region code, trivial accept/reject, iterative boundary intersection, then the same algorithm in 3D with six planes.*

### 2.1 Point clipping

A point $(x,y)$ is inside the window exactly when both intervals hold:

$$ x_{\min}\le x\le x_{\max} \quad\text{AND}\quad y_{\min}\le y\le y_{\max} $$

Equality counts as inside — a point on the boundary is retained. One violated interval is enough to reject.

### 2.2 Region codes

Instead of testing four inequalities per endpoint, the four results are packed into a single **4-bit region code** (outcode).

| Bit | Meaning | Set to 1 when | Computed as |
| --- | --- | --- | --- |
| 3 | above the window | $y>y_{\max}$ | $\operatorname{sign}(y-y_{\max})$ |
| 2 | below the window | $y<y_{\min}$ | $\operatorname{sign}(y_{\min}-y)$ |
| 1 | right of the window | $x>x_{\max}$ | $\operatorname{sign}(x-x_{\max})$ |
| 0 | left of the window | $x<x_{\min}$ | $\operatorname{sign}(x_{\min}-x)$ |

![[CG - Cohen Sutherland Region Codes.excalidraw]]

The nine regions of the plane therefore carry the codes $1001,1000,1010$ (top row), $0001,0000,0010$ (middle), $0101,0100,0110$ (bottom). The window is the only region with code `0000`, and a point may set **several** bits at once — the corner regions set two.

> [!important] Definitions
> **Region code (outcode)** — a bit vector recording, for one endpoint, which of the clipping boundaries that endpoint lies outside of.
> **Trivial accept** — a decision that the whole segment is visible, taken without computing any intersection.
> **Trivial reject** — a decision that the whole segment is invisible, taken without computing any intersection.

### 2.3 Trivial accept and trivial reject

Compute $C_0$ for $P_0$ and $C_1$ for $P_1$, then combine the two codes bitwise.

| Test | Result | Meaning |
| --- | --- | --- |
| $C_0 \;\text{OR}\; C_1 = 0000$ | **accept** | neither endpoint is outside any boundary |
| $C_0 \;\text{AND}\; C_1 \neq 0000$ | **reject** | both endpoints lie outside the *same* boundary |
| otherwise | **clip** | part of the segment may be visible |

The AND test works because a shared set bit means both endpoints are on the outer side of one boundary line. If $P$ and $Q$ are both left of $x=x_{\min}$ then $C_P=0001$ and $C_Q=0001$, so $C_P\;\text{AND}\;C_Q=0001\neq0000$: the segment cannot cross into the window, because the window lies entirely on the other side of that line. The same argument holds for *any* same-side combination — both above (bit 3), both below (bit 2), both right (bit 1), both left (bit 0).

> [!warning] AND = 0 is not a promise of visibility
> $C_0\;\text{AND}\;C_1=0000$ only says the shortcut *cannot reject yet*. The two endpoints may still be outside on *different* sides, so the segment can miss the window entirely. A later pass can reject it. Never report "visible" from the AND test — only "not yet rejected".

### 2.4 Clipping one boundary at a time

When neither shortcut applies, one outside endpoint is moved onto a boundary:

1. **Choose the endpoint.** Take the first endpoint whose code is nonzero; a code of `0000` is never clipped.
2. **Choose the plane.** Any set bit works and the answer is the same; the deck takes the **lowest set bit**, in the fixed order Left, Right, Bottom, Top, Near, Far.
3. **Solve for the intersection**, set that coordinate exactly to the boundary value.
4. **Recode** the new endpoint and **retest** from step 1.

The segment is parameterised once, $P(t)=P_0+t(P_1-P_0)$ with $0\le t\le 1$, and every clipped endpoint remains a point of the same line. The working interval therefore only ever shrinks: $[t_{start},t_{end}]\subseteq[0,1]$, with each pass moving one end inward. That is why the algorithm terminates — each pass strictly removes a piece of the segment.

### 2.5 The line-equation view

For 2D work the deck also clips with the line's Cartesian equation, which is often quicker by hand. From two points, get $y=mx+c$, then convert to general form $ax+by+c=0$; substituting a boundary value gives the other coordinate directly.

**Worked example 1 — $P(3,3)$, $Q(5,2)$.**

$$ m=\frac{2-3}{5-3}=-\frac{1}{2}, \qquad 3=-\frac{1}{2}(3)+c \Rightarrow c=\frac{9}{2} $$
$$ y=-\frac{1}{2}x+\frac{9}{2} \quad\Longleftrightarrow\quad \boxed{\,x+2y-9=0\,} $$

**Worked example 2 — $M(1,3)$, $N(5,2)$.**

$$ m=\frac{2-3}{5-1}=-\frac{1}{4}, \qquad 3=-\frac{1}{4}(1)+c \Rightarrow c=\frac{13}{4} $$
$$ y=-\frac{1}{4}x+\frac{13}{4} \quad\Longleftrightarrow\quad \boxed{\,x+4y-13=0\,} $$

With $x+2y-9=0$ and a left boundary $x=0$, the intersection is $y=9/2$; with a top boundary $y=6$ it is $x=9-12=-3$. The Cartesian form is convenient when the boundary is axis-aligned, which it always is in this algorithm.

### 2.6 The three-dimensional extension

The window becomes a **box** $[x_{\min},x_{\max}]\times[y_{\min},y_{\max}]\times[z_{\min},z_{\max}]$ — six boundary planes instead of four — so each endpoint needs a **6-bit** code.

| Bit | Plane | Set to 1 when | Mask |
| --- | --- | --- | --- |
| 5 | Far | $z>z_{\max}$ | `100000` |
| 4 | Near | $z<z_{\min}$ | `010000` |
| 3 | Top | $y>y_{\max}$ | `001000` |
| 2 | Bottom | $y<y_{\min}$ | `000100` |
| 1 | Right | $x>x_{\max}$ | `000010` |
| 0 | Left | $x<x_{\min}$ | `000001` |

`000000` means inside or on the boundary. The accept/reject logic is **identical** to 2D — OR for accept, AND for reject — and a point can set several bits at once: Far + Top + Right is `101010`.

### 2.7 Intersection formulas for all six planes

$$ P(t)=P_0+t(P_1-P_0),\qquad 0\le t\le 1 $$

| Bit | Plane | Boundary | Solve for $t$ | Then substitute |
| --- | --- | --- | --- | --- |
| 0 | Left | $x=x_{\min}$ | $t=(x_{\min}-x_0)/(x_1-x_0)$ | $y=y_0+t(y_1-y_0)$, $z=z_0+t(z_1-z_0)$ |
| 1 | Right | $x=x_{\max}$ | $t=(x_{\max}-x_0)/(x_1-x_0)$ | same |
| 2 | Bottom | $y=y_{\min}$ | $t=(y_{\min}-y_0)/(y_1-y_0)$ | $x,z$ from $t$ |
| 3 | Top | $y=y_{\max}$ | $t=(y_{\max}-y_0)/(y_1-y_0)$ | $x,z$ from $t$ |
| 4 | Near | $z=z_{\min}$ | $t=(z_{\min}-z_0)/(z_1-z_0)$ | $x,y$ from $t$ |
| 5 | Far | $z=z_{\max}$ | $t=(z_{\max}-z_0)/(z_1-z_0)$ | $x,y$ from $t$ |

> [!note] Why the denominator is never zero
> Clipping happens only at a bit that is **set for one endpoint and clear for the other**, so that coordinate differs between $P_0$ and $P_1$ — the denominator cannot vanish. This is the numerical reason the algorithm is robust, and the reason it must pick a plane from the *outside* endpoint's set bits rather than testing planes blindly.

### 2.8 Worked example in 3D

Clip the segment from $A=(-4,2,-2)$ to $B=(8,8,10)$ against the box $0\le x\le 6$, $0\le y\le 6$, $0\le z\le 8$.

**Step 1 — outcodes.**

| Bit | Plane | Test | $A$ value | $A$ result | $A$ bit | $B$ value | $B$ result | $B$ bit |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 5 | Far | $z>8$ | $-2$ | inside | 0 | 10 | outside | 1 |
| 4 | Near | $z<0$ | $-2$ | outside | 1 | 10 | inside | 0 |
| 3 | Top | $y>6$ | 2 | inside | 0 | 8 | outside | 1 |
| 2 | Bottom | $y<0$ | 2 | inside | 0 | 8 | inside | 0 |
| 1 | Right | $x>6$ | $-4$ | inside | 0 | 8 | outside | 1 |
| 0 | Left | $x<0$ | $-4$ | outside | 1 | 8 | inside | 0 |

Reading bit 5 → bit 0:

$$ C(A)=010001,\qquad C(B)=101010 $$

$A$ is near-clipped and left-clipped (two violations, two 1s); $B$ is far, top and right (three violations, three 1s).

**Step 2 — combine and decide.**

| | Far | Near | Top | Bottom | Right | Left |
| --- | --- | --- | --- | --- | --- | --- |
| $C(A)$ | 0 | 1 | 0 | 0 | 0 | 1 |
| $C(B)$ | 1 | 0 | 1 | 0 | 1 | 0 |
| **OR** | 1 | 1 | 1 | 0 | 1 | 1 |
| **AND** | 0 | 0 | 0 | 0 | 0 | 0 |

OR $=111011\neq000000$ ⇒ not a trivial accept. AND $=000000$ ⇒ not a trivial reject. **Clip.** $A$ and $B$ never fail the same plane, so the segment genuinely crosses the box.

**Step 3 — the line, written once.**

$$ d=B-A=(12,6,12),\qquad x(t)=-4+12t,\quad y(t)=2+6t,\quad z(t)=-2+12t $$
Check $t=0$: $(-4,2,-2)=A$ ✓  $t=1$: $(8,8,10)=B$ ✓  Current segment $t\in[0,1]$.

**Pass 1 — clip $A$ at Left, $x=0$.** $C(A)\neq0$, its set bits are Near(4) and Left(0); lowest is bit 0.

$$ -4+12t=0 \Rightarrow t=\frac13,\quad y=2+6\cdot\tfrac13=4,\quad z=-2+12\cdot\tfrac13=2 $$
$$ A'=(0,4,2),\qquad C(A')=000000 $$

The Left-plane intersection also cleared Near: $z=2$ is inside $[0,8]$. Segment is now $t\in[\tfrac13,1]$, OR $=101010$, AND $=000000$ ⇒ clip again.

**Pass 2 — clip $B$ at Right, $x=6$.** $B$'s set bits are Far(5), Top(3), Right(1); lowest is bit 1.

$$ -4+12t=6 \Rightarrow t=\frac56,\quad y=2+6\cdot\tfrac56=7,\quad z=-2+12\cdot\tfrac56=8 $$
$$ Q=(6,7,8),\qquad C(Q)=001000 $$

$Q$ is on $x=6$ and on $z=8$ but $y=7>6$ — **a plane intersection can still lie outside the box**, which is why recoding is mandatory. Segment $t\in[\tfrac13,\tfrac56]$.

**Pass 3 — clip $Q$ at Top, $y=6$.** Only bit 3 is set.

$$ 2+6t=6 \Rightarrow t=\frac23,\quad x=-4+12\cdot\tfrac23=4,\quad z=-2+12\cdot\tfrac23=6 $$
$$ B'=(4,6,6),\qquad C(B')=000000 $$

OR $=000000$ ⇒ **accept**. The visible segment is $A'B'=(0,4,2)\to(4,6,6)$, i.e. $t\in[\tfrac13,\tfrac23]$ of the original line.

| Pass | Endpoint | Code | Plane | $t$ | New point | New code |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | $A$ | `010001` | Left $x=0$ | $1/3$ | $A'=(0,4,2)$ | `000000` |
| 2 | $B$ | `101010` | Right $x=6$ | $5/6$ | $Q=(6,7,8)$ | `001000` |
| 3 | $Q$ | `001000` | Top $y=6$ | $2/3$ | $B'=(4,6,6)$ | `000000` |

Check the result: $0\le4\le6$, $0\le6\le6$, $0\le6\le8$ for $A'$; and $0\le4\le6$, $0\le6\le6$, $0\le6\le8$ for $B'$. Both endpoints are inside or on the boundary.

### 2.9 The algorithm

> [!important] Cohen–Sutherland line clipping — statement
> ```text
> 1: C0 = code(P0); C1 = code(P1)
> 2: loop
> 3:   if C0 OR C1 = 0      -> ACCEPT, stop
> 4:   if C0 AND C1 != 0    -> REJECT, stop
> 5:   pick the endpoint whose code is non-zero (P0 if C0 != 0, else P1)
> 6:   pick its lowest set bit k  -> boundary plane b
> 7:   t = (b - Pstart[axis]) / (Pend[axis] - Pstart[axis])
> 8:   new point = Pstart + t (Pend - Pstart); set the axis coordinate exactly to b
> 9:   replace the chosen endpoint by the new point; recompute its code
> 10: end loop
> ```
> **Cost.** Each pass costs one division and a handful of multiplications; at most one pass per boundary, so at most six passes per segment (four in 2D). Trivial accept/reject is $O(1)$ with no arithmetic.

### 2.10 Interactive dry run

> [!tip] How to use the widget
> `Next Step` advances one *pass* (one endpoint moved onto one plane). The left panel is the geometry; the right panel is the working state: both codes, the OR/AND decision, and the surviving $t$ interval. The $z$ coordinate is checked in the table, not drawn — the sketch is an $xy$ projection.

```html
<div id="w-cs" style="border:1px solid var(--background-modifier-border,#ccc);border-radius:10px;padding:12px;background:var(--background-primary,#fff);color:var(--text-normal,#222);font:14px/1.45 var(--font-interface,system-ui,sans-serif)">
  <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px">
    <button id="cs-play" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--interactive-accent,#4a7fd4);color:var(--text-on-accent,#fff);cursor:pointer">▶ Play</button>
    <button id="cs-pause" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--background-secondary,#eee);color:var(--text-normal,#222);cursor:pointer">⏸ Pause</button>
    <button id="cs-next" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--background-secondary,#eee);color:var(--text-normal,#222);cursor:pointer">⏭ Next Step</button>
    <button id="cs-reset" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--background-secondary,#eee);color:var(--text-normal,#222);cursor:pointer">↺ Reset</button>
  </div>
  <div id="cs-say" style="min-height:40px;color:var(--text-muted,#555);margin-bottom:8px">Ready. Segment A(−4,2,−2) → B(8,8,10) against the box 0≤x≤6, 0≤y≤6, 0≤z≤8.</div>
  <div style="display:flex;gap:12px;flex-wrap:wrap">
    <svg id="cs-stage" viewBox="0 0 460 360" style="flex:1 1 420px;max-width:100%;background:var(--background-secondary,#f7f7f7);border-radius:8px"></svg>
    <div style="flex:1 1 240px;min-width:220px">
      <table id="cs-table" style="width:100%;border-collapse:collapse;font-size:13px">
        <thead><tr style="color:var(--text-muted,#666)">
          <th style="text-align:left;padding:3px 4px;border-bottom:1px solid var(--background-modifier-border,#ddd)">Pass</th>
          <th style="text-align:left;padding:3px 4px;border-bottom:1px solid var(--background-modifier-border,#ddd)">Plane</th>
          <th style="text-align:left;padding:3px 4px;border-bottom:1px solid var(--background-modifier-border,#ddd)">t</th>
          <th style="text-align:left;padding:3px 4px;border-bottom:1px solid var(--background-modifier-border,#ddd)">Point</th>
        </tr></thead>
        <tbody></tbody>
      </table>
      <div id="cs-state" style="margin-top:10px;font:13px/1.6 ui-monospace,monospace;color:var(--text-normal,#222)"></div>
    </div>
  </div>
</div>
<script>
(() => {
  const B = { xmin: 0, xmax: 6, ymin: 0, ymax: 6, zmin: 0, zmax: 8 };
  const A0 = [-4, 2, -2], B0 = [8, 8, 10];
  const PLANES = [
    { bit: 0, name: "Left", axis: 0, bound: B.xmin },
    { bit: 1, name: "Right", axis: 0, bound: B.xmax },
    { bit: 2, name: "Bottom", axis: 1, bound: B.ymin },
    { bit: 3, name: "Top", axis: 1, bound: B.ymax },
    { bit: 4, name: "Near", axis: 2, bound: B.zmin },
    { bit: 5, name: "Far", axis: 2, bound: B.zmax }
  ];
  const code = (p) => {
    let c = 0;
    if (p[0] < B.xmin) c |= 1;
    if (p[0] > B.xmax) c |= 2;
    if (p[1] < B.ymin) c |= 4;
    if (p[1] > B.ymax) c |= 8;
    if (p[2] < B.zmin) c |= 16;
    if (p[2] > B.zmax) c |= 32;
    return c;
  };
  const bits = (c) => c.toString(2).padStart(6, "0");
  const lerp = (a, b, t) => [0, 1, 2].map(i => +(a[i] + t * (b[i] - a[i])).toFixed(4));

  function build() {
    const steps = [];
    let P = A0.slice(), Q = B0.slice(), t0 = 0, t1 = 1;
    steps.push({ P: P.slice(), Q: Q.slice(), t0, t1, done: false, kind: "init", log: "Initial segment: both outcodes are computed." });
    for (let g = 0; g < 8; g++) {
      const cP = code(P), cQ = code(Q);
      if ((cP | cQ) === 0) { steps.push({ P: P.slice(), Q: Q.slice(), t0, t1, done: true, kind: "accept", log: "OR = 000000 → ACCEPT. Both endpoints are inside or on the boundary." }); break; }
      if ((cP & cQ) !== 0) { steps.push({ P: P.slice(), Q: Q.slice(), t0, t1, done: true, kind: "reject", log: "AND ≠ 000000 → REJECT. Both endpoints lie outside the same plane." }); break; }
      const useP = cP !== 0;
      const c = useP ? cP : cQ;
      let pl = PLANES.find(p => c & (1 << p.bit));
      const axis = pl.axis;
      const t = (pl.bound - A0[axis]) / (B0[axis] - A0[axis]);
      let np = lerp(A0, B0, t);
      np[axis] = pl.bound;
      if (useP) { P = np; t0 = t; } else { Q = np; t1 = t; }
      steps.push({
        P: P.slice(), Q: Q.slice(), t0, t1, done: false, kind: "pass",
        plane: pl.name, t: t, pt: np.slice(),
        log: "Pass " + (steps.filter(s => s.kind === "pass").length + 1) + ": clip " + (useP ? "A" : "B") +
             " at " + pl.name + " (" + (axis === 0 ? "x" : axis === 1 ? "y" : "z") + " = " + pl.bound + "), t = " +
             t.toFixed(3) + " → (" + np.map(v => +v.toFixed(2)).join(", ") + "). New code " + bits(code(np)) + "."
      });
    }
    return steps;
  }

  const steps = build();
  let i = 0, timer = null;
  const stage = document.getElementById("cs-stage");
  const say = document.getElementById("cs-say");
  const tbody = document.querySelector("#cs-table tbody");
  const state = document.getElementById("cs-state");
  const NS = "http://www.w3.org/2000/svg";
  const el = (n, a) => { const e = document.createElementNS(NS, n); for (const k in a) e.setAttribute(k, a[k]); return e; };

  const X = x => 40 + (x + 6) * (380 / 18);
  const Y = y => 320 - (y + 3) * (300 / 15);

  function draw(s) {
    stage.innerHTML = "";
    stage.appendChild(el("rect", { x: 0, y: 0, width: 460, height: 360, fill: "none" }));
    stage.appendChild(el("rect", { x: X(B.xmin), y: Y(B.ymax), width: X(B.xmax) - X(B.xmin), height: Y(B.ymin) - Y(B.ymax),
      fill: "rgba(47,158,68,0.10)", stroke: "#2f9e44", "stroke-width": 1.5 }));
    stage.appendChild(el("text", { x: X(B.xmin) + 3, y: Y(B.ymax) - 6, fill: "#2f9e44", "font-size": 11 })).textContent = "clip box (z checked in table)";
    stage.appendChild(el("line", { x1: X(A0[0]), y1: Y(A0[1]), x2: X(B0[0]), y2: Y(B0[1]),
      stroke: "#adb5bd", "stroke-width": 1.5, "stroke-dasharray": "5 4" }));
    stage.appendChild(el("line", { x1: X(s.P[0]), y1: Y(s.P[1]), x2: X(s.Q[0]), y2: Y(s.Q[1]),
      stroke: s.kind === "reject" ? "#e03131" : "#1971c2", "stroke-width": 3 }));
    [[s.P, "P", "#1971c2"], [s.Q, "Q", "#1971c2"]].forEach(([p, lab, col]) => {
      stage.appendChild(el("circle", { cx: X(p[0]), cy: Y(p[1]), r: 4.5, fill: col }));
      const tx = el("text", { x: X(p[0]) + 7, y: Y(p[1]) - 7, fill: col, "font-size": 11 });
      tx.textContent = lab + bits(code(p));
      stage.appendChild(tx);
    });
    if (s.pt) {
      stage.appendChild(el("circle", { cx: X(s.pt[0]), cy: Y(s.pt[1]), r: 5, fill: "none", stroke: "#e8590c", "stroke-width": 2 }));
    }
    const ax = (y, txt) => { const t = el("text", { x: 4, y: y, fill: "var(--text-faint,#888)", "font-size": 10 }); t.textContent = txt; stage.appendChild(t); };
    ax(352, "x: −6 … 12   ·   y: −3 … 12   ·   z is not drawn");
    const band = el("text", { x: 40, y: 22, fill: "var(--text-muted,#555)", "font-size": 12 });
    band.textContent = s.kind === "accept" ? "ACCEPT" : s.kind === "reject" ? "REJECT" : s.kind === "init" ? "initial" : s.kind.toUpperCase();
    stage.appendChild(band);
  }

  function paint() {
    const s = steps[i];
    draw(s);
    say.textContent = s.log + (s.kind === "pass" ? "  Segment now t ∈ [" + s.t0.toFixed(3) + ", " + s.t1.toFixed(3) + "]." : "");
    tbody.innerHTML = "";
    steps.slice(1, i + 1).filter(x => x.kind === "pass").forEach((x, k) => {
      const tr = document.createElement("tr");
      tr.innerHTML = "<td style='padding:3px 4px;border-bottom:1px solid var(--background-modifier-border,#eee)'>" + (k + 1) +
        "</td><td style='padding:3px 4px;border-bottom:1px solid var(--background-modifier-border,#eee)'>" + x.plane +
        "</td><td style='padding:3px 4px;border-bottom:1px solid var(--background-modifier-border,#eee)'>" + x.t.toFixed(3) +
        "</td><td style='padding:3px 4px;border-bottom:1px solid var(--background-modifier-border,#eee)'>(" +
        x.pt.map(v => +v.toFixed(2)).join(", ") + ")</td>";
      tbody.appendChild(tr);
    });
    state.textContent =
      "C(P) = " + bits(code(s.P)) + "\n" +
      "C(Q) = " + bits(code(s.Q)) + "\n" +
      "OR   = " + bits(code(s.P) | code(s.Q)) + "\n" +
      "AND  = " + bits(code(s.P) & code(s.Q)) + "\n" +
      "t ∈ [" + s.t0.toFixed(3) + ", " + s.t1.toFixed(3) + "]";
    state.style.whiteSpace = "pre";
  }

  const stop = () => { if (timer) { clearInterval(timer); timer = null; } };
  document.getElementById("cs-next").onclick = () => { stop(); if (i < steps.length - 1) i++; paint(); };
  document.getElementById("cs-reset").onclick = () => { stop(); i = 0; paint(); };
  document.getElementById("cs-pause").onclick = stop;
  document.getElementById("cs-play").onclick = () => {
    stop();
    timer = setInterval(() => { if (i < steps.length - 1) { i++; paint(); } else { stop(); } }, 1200);
  };
  paint();
})();
</script>
```

### 2.11 Exam pointer

> [!tip] Exam pointer — Cohen–Sutherland
> - Write the 4-bit table with its sign functions, and the 6-bit table with its mask values (`100000` … `000001`).
> - Justify both shortcuts in one sentence each; state that AND = 0 does not prove visibility.
> - Reproduce the 3D worked example end to end: codes, OR/AND, three passes, final segment $(0,4,2)$–$(4,6,6)$ at $t\in[1/3,2/3]$.
> - Explain why the denominator in $t$ is never zero, and why the intersection must be recoded.
> - State the worst-case pass count (one per boundary) and the cost per pass.

---

## 3. Polygon and 3D Fill-Area Clipping

*Deck: [[CG_Oct_5.pdf]] — 89 slides. Fill-area clipping, Sutherland–Hodgman with its four cases and full numeric trace, Weiler–Atherton boundary traversal, 3D point/face clipping, and the visibility problem that the next two topics solve.*

### 3.1 Polygons as ordered, closed vertex lists

A polygon enters the clipper as an **ordered list**, not a set:

$$ V=[v_1,v_2,\dots,v_n] $$

- Edges are $(v_1,v_2),(v_2,v_3),\dots,(v_{n-1},v_n)$ **and the closing edge** $(v_n,v_1)$.
- The closing edge is processed even though $v_1$ is not repeated at the end of the list.
- Clockwise or anticlockwise order is both valid, provided it is consistent.
- Square brackets emphasise that the order carries meaning: $[v_1,v_2,v_3]$ and $[v_2,v_3,v_1]$ are the same polygon (a cyclic rotation), but $[v_1,v_3,v_2]$ is the mirror traversal.
- The output must be a **closed, ordered boundary** too — that closure is exactly what clipping each edge independently cannot guarantee.

### 3.2 Why polygon clipping is not line clipping

> [!important] Why a separate algorithm is needed
> Clipping the four edges of a polygon as four independent segments produces a set of disjoint visible pieces, plus the parts of the window boundary that now form the outline of the visible region. Those boundary pieces belong to no original edge, so the result is **not a closed polygon**. Polygon clipping must therefore invent vertices and edges:
> - **new vertices** — edge/ boundary intersections, and sometimes window corners;
> - **new edges** — segments that run *along* the window boundary.

![[CG - Concave Subject Split.png]]

*Figure — the concave-subject limitation: one clip boundary cuts the U-shape into two lobes, and Sutherland–Hodgman stores both in a single vertex list, producing a polygon whose boundary walks along the clip edge twice.*

### 3.3 The window as four half-planes

A rectangular window is the intersection of four half-planes, so a polygon can be clipped by four independent half-plane passes. Each pass needs only one test:

| Clipper | Inside test | Outside test |
| --- | --- | --- |
| Left | $x\ge x_{\min}$ | $x<x_{\min}$ |
| Right | $x\le x_{\max}$ | $x>x_{\max}$ |
| Bottom | $y\ge y_{\min}$ | $y<y_{\min}$ |
| Top | $y\le y_{\max}$ | $y>y_{\max}$ |

### 3.4 The four edge cases

For one clip boundary, classify the current vertex $S$ and the next vertex $E$. There are exactly four combinations, and each dictates what enters the output list.

![[CG - Sutherland Hodgman Four Cases.excalidraw]]

| $S$ (current) | $E$ (next) | Append to output | Reason |
| --- | --- | --- | --- |
| Inside | Inside | $E$ | whole edge is retained |
| Inside | Outside | $I$ (the crossing) | edge leaves at $I$ |
| Outside | Inside | $I$, then $E$ | edge enters at $I$ |
| Outside | Outside | nothing | whole edge lies outside this half-plane |

> [!note] Why outside–outside appends nothing
> Both endpoints lie strictly beyond the same boundary, so the entire edge lies beyond it as well (the half-plane is convex). No part of that edge can be inside, and no crossing exists — an intersection would have to be *between* the endpoints, which would make one of them inside.

### 3.5 Computing the intersection

Parameterise the edge and solve for the crossing:

$$ P(t)=S+t(E-S),\qquad 0\le t\le 1 $$

| Clip boundary | Parameter | Other coordinate |
| --- | --- | --- |
| $x=b$ (left/right) | $t=(b-S_x)/(E_x-S_x)$ | $y=S_y+t(E_y-S_y)$ |
| $y=b$ (bottom/top) | $t=(b-S_y)/(E_y-S_y)$ | $x=S_x+t(E_x-S_x)$ |

- For an inside→outside transition the denominator is non-zero (the endpoints straddle the boundary).
- A crossing exactly at an endpoint gives $t=0$ or $t=1$: the point duplicates a vertex, so **merge duplicates** before emitting.
- Use a consistent endpoint order and consistent arithmetic to keep numerically coincident points identical; otherwise the output list contains hairline degenerate edges.

### 3.6 The procedure

> [!important] Sutherland–Hodgman — statement
> ```text
> for b in [left, right, top, bottom]:
>     out = []                          # fresh list for this boundary
>     n = length(V)
>     for i in 0 .. n-1:                # includes the closing edge
>         S = V[i]; E = V[(i+1) mod n]
>         if in(S) and in(E): out.append(E)
>         elif in(S):         out.append(I(S,E,b))        # in -> out
>         elif in(E):         out.append(I(S,E,b)); out.append(E)   # out -> in
>         # out -> out: append nothing
>     V = out
>     if V is empty: return []
> return V
> ```
> **Cost.** One pass over $n$ vertices per boundary, four boundaries ⇒ $O(n)$ per clipper, and the list can grow (each pass can add at most two vertices per crossing). An empty list stays empty: **once the polygon is clipped away, later passes cannot restore it** — the early exit is an optimisation, not a change of result.

The order of the four passes does not change the final region, only the vertex order and the number of temporary vertices. The book order — left, right, top, bottom — makes the working predictable.

### 3.7 Pictorial worked example

Take $V=[1,2,3]$ anticlockwise, with vertex 1 above the window, vertex 2 inside and vertex 3 to its right. Read inside/outside off the picture and track the list after every pass:

| Pass | Clipper | Inside | Outside | Result |
| --- | --- | --- | --- | --- |
| 1 | left $x\ge x_{\min}$ | 1,2,3 | none | $[2,3,1]$ — all edges In→In, the triangle is unchanged, the list is a cyclic rotation |
| 2 | right $x\le x_{\max}$ | 1,2 | 3 | $[2',3',1,2]$ — two new points; the new edge $2'\to3'$ runs along the right side |
| 3 | top $y\le y_{\max}$ | $2',3',2$ | 1 | $[3',3'',1',2,2']$ — $3''$ is a *second* crossing on the original edge $3\to1$, left of the corner |
| 4 | bottom $y\ge y_{\min}$ | all five | none | $[3'',1',2,2',3']$ — nothing changes but the starting vertex |

Five vertices survive: $2',3',3'',1'$ are new, and only vertex 2 comes from the original triangle.

### 3.8 Numerical trace

Clip the triangle $1=(-1,0)$, $2=(3,0)$, $3=(1,3)$ against $0\le x\le 2$, $0\le y\le 2$, in the order left, right, top, bottom. Predict first: how many vertices will the result have?

**Pass 1 — left clipper, $x\ge0$.** Classify: $1$ outside ($-1\ge0$ ✗), $2,3$ inside.

$i=0$: $1\to2$ is Out→In.
$$ t=\frac{0-(-1)}{3-(-1)}=\frac14,\qquad y=0+\tfrac14(0-0)=0,\qquad I=1'=(0,0) $$
$i=2$: $3\to1$ is In→Out (closing edge).
$$ t=\frac{0-1}{-1-1}=\frac12,\qquad y=3+\tfrac12(0-3)=\frac32,\qquad I=2'=\left(0,\tfrac32\right) $$

| $i$ | $S\to E$ | Case | Append | out |
| --- | --- | --- | --- | --- |
| 0 | $1\to2$ | Out→In | $1'$, then 2 | $[(0,0),(3,0)]$ |
| 1 | $2\to3$ | In→In | 3 | $[(0,0),(3,0),(1,3)]$ |
| 2 | $3\to1$ | In→Out | $2'$ | $[(0,0),(3,0),(1,3),(0,\tfrac32)]$ |

The clipper creates the new closing edge $2'\to1'$ on $x=0$: that edge exists in no input edge.

**Pass 2 — right clipper, $x\le2$.** Input $[1',2,3,2']$; only $2=(3,0)$ is outside.

$i=0$: $1'\to2$ In→Out, $t=(2-0)/(3-0)=\tfrac23$, $y=0+\tfrac23(0)=0$, so $I=3'=(2,0)$.
$i=1$: $2\to3$ Out→In, $t=(2-3)/(1-3)=\tfrac12$, $y=0+\tfrac12(3)=\tfrac32$, so $I=4'=(2,\tfrac32)$.

| $i$ | $S\to E$ | Case | Append | out |
| --- | --- | --- | --- | --- |
| 0 | $1'\to2$ | In→Out | $3'$ | $[(2,0)]$ |
| 1 | $2\to3$ | Out→In | $4'$, then 3 | $[(2,0),(2,\tfrac32),(1,3)]$ |
| 2 | $3\to2'$ | In→In | $2'$ | $[(2,0),(2,\tfrac32),(1,3),(0,\tfrac32)]$ |
| 3 | $2'\to1'$ | In→In | $1'$ | $[(2,0),(2,\tfrac32),(1,3),(0,\tfrac32),(0,0)]$ |

**Pass 3 — top clipper, $y\le2$.** Only $3=(1,3)$ is outside.

$i=1$: $4'\to3$ In→Out, $t=(2-\tfrac32)/(3-\tfrac32)=\tfrac13$, $x=2+\tfrac13(1-2)=\tfrac53$, so $I=5'=(\tfrac53,2)$.
$i=2$: $3\to2'$ Out→In, $t=(2-3)/(\tfrac32-3)=\tfrac23$, $x=1+\tfrac23(0-1)=\tfrac13$, so $I=6'=(\tfrac13,2)$.

| $i$ | $S\to E$ | Case | Append | out |
| --- | --- | --- | --- | --- |
| 0 | $3'\to4'$ | In→In | $4'$ | $[(2,\tfrac32)]$ |
| 1 | $4'\to3$ | In→Out | $5'$ | $[(2,\tfrac32),(\tfrac53,2)]$ |
| 2 | $3\to2'$ | Out→In | $6'$, then $2'$ | $[(2,\tfrac32),(\tfrac53,2),(\tfrac13,2),(0,\tfrac32)]$ |
| 3 | $2'\to1'$ | In→In | $1'$ | $[\dots,(0,0)]$ |
| 4 | $1'\to3'$ | In→In | $3'$ | $[(2,\tfrac32),(\tfrac53,2),(\tfrac13,2),(0,\tfrac32),(0,0),(2,0)]$ |

**Pass 4 — bottom clipper, $y\ge0$.** All six vertices satisfy it (the two at $y=0$ are *on* the boundary, and boundary counts as inside), so every edge is In→In and the list is only rotated.

| $i$ | $S\to E$ | Case | Append |
| --- | --- | --- | --- |
| 0 | $4'\to5'$ | In→In | $5'$ |
| 1 | $5'\to6'$ | In→In | $6'$ |
| 2 | $6'\to2'$ | In→In | $2'$ |
| 3 | $2'\to1'$ | In→In | $1'$ |
| 4 | $1'\to3'$ | In→In | $3'$ |
| 5 | $3'\to4'$ | In→In | $4'$ |

$$ V'=[\,(2,\tfrac32),\,(\tfrac53,2),\,(\tfrac13,2),\,(0,\tfrac32),\,(0,0),\,(2,0)\,] $$

| Stage | List |
| --- | --- |
| input | $[1,2,3]$ |
| after left | $[1',2,3,2']$ |
| after right | $[3',4',3,2',1']$ |
| after top | $[4',5',6',2',1',3']$ |
| after bottom | $[5',6',2',1',3',4']$ |

Three vertices in, six out: $1,2,3$ are all removed and $1'$–$6'$ are all new.

### 3.9 The limitation: a concave subject can split

Take a concave U-shaped subject $V=[1,\dots,8]$ against one clipper, keeping $y\ge y_{\min}$:

| $i$ | $S\to E$ | Case | Append |
| --- | --- | --- | --- |
| 0 | $1\to2$ | Out→Out | nothing |
| 1 | $2\to3$ | Out→In | $2'$, then 3 |
| 2 | $3\to4$ | In→In | 4 |
| 3 | $4\to5$ | In→Out | $4'$ |
| 4 | $5\to6$ | Out→Out | nothing |
| 5 | $6\to7$ | Out→In | $6'$, then 7 |
| 6 | $7\to8$ | In→In | 8 |
| 7 | $8\to1$ | In→Out | $8'$ |

$$ out=[2',3,4,4',6',7,8,8'] $$

That is **two disconnected pieces stored as one vertex list**. Rendered as a single polygon, the boundary walks from $4'$ to $6'$ along the clip edge and from $8'$ to $2'$ along it again — the degenerate connector is drawn twice. Sutherland–Hodgman is therefore correct only for **convex subjects** (or when the two pieces are allowed to be joined by a doubled edge).

### 3.10 Weiler–Atherton

The alternative walks the boundaries themselves and switches between subject and window at every crossing.

> [!important] Weiler–Atherton — traversal rules
> - Trace the **subject** boundary in its stored orientation.
> - At an **exit** intersection, switch to the **window** boundary, same orientation.
> - At an **entry** intersection, switch back to the **subject**.
> - When the walk returns to the contour's start, close and output that contour.
> - Repeat from any unvisited entry intersection.
> **Assumption:** proper crossings only. Tangencies, shared edges and coincident vertices need extra rules.

**Worked example.** Subject $[1,2,3,4,5,6]$ anticlockwise, vertices 3 and 6 left of the window, concave notch at 6 separating an upper and a lower lobe; the left boundary cuts four edges.

| Subject edge | Direction | Crossing | Type |
| --- | --- | --- | --- |
| $(2,3)$ | inside → outside | $2'$ | exit |
| $(3,4)$ | outside → inside | $3'$ | entry |
| $(5,6)$ | inside → outside | $6'$ | exit |
| $(6,1)$ | outside → inside | $1'$ | entry |

Ordered down the window's left edge (anticlockwise ⇒ downward): $2'$ exit, $1'$ entry, $6'$ exit, $3'$ entry. Exits and entries alternate, so each exit leads to the next entry.

![[CG - Weiler Atherton Crossings.png|460]]

*Figure — the concave subject and the four crossings on the window's left edge, labelled exit/entry; the alternation of the two labels is what makes a single boundary walk possible.*

**Contour 1 (upper region):** subject $1\to2$, exit at $2'$; window $2'\downarrow$ to entry $1'$; subject $1'\to1$, back at the start. Output $[1,2,2',1']$.

**Contour 2 (lower region):** skip the outside part through 3, find entry $3'$; subject $3'\to4\to5$, exit at $6'$; window $6'\downarrow$ back to $3'$. Output $[3',4,5,6']$.

| Region | Vertex list | Window edge used |
| --- | --- | --- |
| upper | $[1,2,2',1']$ | $2'\to1'$ |
| lower | $[3',4,5,6']$ | $6'\to3'$ |

Together the two contours are exactly subject ∩ window. Sutherland–Hodgman on the same input gives $[2,2',3',4,5,6',1',1]$, whose edges $2'\to3'$ and $6'\to1'$ lie on the window boundary — the doubled connector again.

### 3.11 Comparison

| Aspect | Sutherland–Hodgman | Weiler–Atherton |
| --- | --- | --- |
| Operation | successive half-plane passes | linked boundary traversal |
| Subject polygon | convex or concave | convex or concave |
| Output | one vertex list | one list per visible region |
| Bookkeeping | four inside/outside cases | crossings, entry/exit labels, links |
| Failure mode | concave subject ⇒ spurious connecting edges | tangencies and shared edges need special rules |

### 3.12 3D point clipping

After normalisation the volume is the cube $C=[-1,1]^{3}$, bounded by six planes $x=\pm1$, $y=\pm1$, $z=\pm1$. A point is kept **iff all three intervals hold**:

$$ -1\le x\le1 \quad\text{AND}\quad -1\le y\le1 \quad\text{AND}\quad -1\le z\le1 $$

One violated interval rejects the point.

> [!question] Which of these points are kept?
> | Point | $x$ | $y$ | $z$ | Decision | Reason |
> | --- | --- | --- | --- | --- | --- |
> | A | 0.4 | $-0.8$ | 0.2 | keep | all coordinates in $[-1,1]$ |
> | B | 1 | 0 | $-1$ | keep | $x=1$ and $z=-1$ are allowed: B lies on a cube edge |
> | C | 1.2 | 0.3 | 0 | reject | $x=1.2>1$ |
> | D | 0 | $-1.1$ | 1.3 | reject | $y<-1$ and $z>1$ |

### 3.13 Bounding boxes before exact clipping

A face may contain many vertices, and exact clipping examines every edge. Its **bounding box** uses only the coordinate extremes, so comparing boxes is far cheaper. The box test has three outcomes and one non-outcome:

| Object bounding box | Decision | Reason |
| --- | --- | --- |
| $x\in[1.2,2]$, $y,z\in[-0.5,0.5]$ | reject | $a_x=1.2>1$ |
| $x\in[0.5,1.5]$, same $y,z$ | continue | partial overlap: clip the faces |
| $x\in[1,2]$, same $y,z$ | continue | touches $x=1$; $a_x=1$ is **not** $>1$ |
| all intervals inside $[-1,1]$ | accept all | object lies in its box, box lies in the cube |

> [!warning] Overlap is not intersection
> Box overlap only says the boxes share points. The box also contains empty space, and a face may occupy none of the shared part. **Box overlap is inconclusive** — only exact face clipping answers it. Conversely, disjoint boxes *do* guarantee disjoint objects, so rejection is safe.

### 3.14 3D face clipping, worked

Clip the filled triangle $A=(2,0.5,0)$, $B=(0.5,2,0)$, $C=(2,2,0)$ to the cube $-1\le x,y,z\le1$.

1. **A 2D picture is exact here.** All three vertices have $z=0$ and every point of the triangle has $z=0$, so the applicable cross-section of the cube is the square $-1\le x,y\le1$; the two $z$ bounds already hold.
2. **Bounding box:** $x\in[0.5,2]$, $y\in[0.5,2]$, $z=0$ ⇒ partial overlap, so clip.
3. **Pass $x\le1$:** $A$ outside ($2>1$), $B$ inside, $C$ outside.
4. **Edge $A\to B$** (out→in) crosses $x=1$ at $J$: $t=(1-2)/(0.5-2)=\tfrac23$, $y=0.5+1.5\cdot\tfrac23=1.5$ ⇒ $J=(1,1.5,0)$. Append $J$, then $B$.
5. **Edge $B\to C$** (in→out) crosses at $K$: $C-B=(1.5,0,0)$, $t=(1-0.5)/(2-0.5)=\tfrac13$, $y=2$ ⇒ $K=(1,2,0)$. Append $K$. ($B$ is already in the list.)
6. **Edge $C\to A$** is out→out ($x=2$ throughout): append nothing. Output polygon after the $x$ pass: $[J,B,K]$, closed by the new edge $K\to J$.
7. **Pass $y\le1$:** $J$ has $y=1.5>1$, $B$ has $y=2>1$, $K$ has $y=2>1$ — **all three outside**, so every edge is out→out and the output is empty.
8. **Result:** the triangle–cube intersection is empty; the triangle is completely outside the cube. The $x$ pass gave $[J,B,K]$, the $y$ pass gave $[]$, and an empty list cannot be restored.

> [!note] What the example teaches
> - A plane intersection can satisfy the plane it was computed on and still violate another ($K$ is on $x=1$ but $y=2$).
> - A bounding-box overlap may sit entirely in empty box space — the box test said "continue", the exact test said "nothing".
> - The parameters $\tfrac23$ and $\tfrac13$ belong to **different directed edges**; reusing one for the other is the classic error.

### 3.15 Clipping versus occlusion

> [!important] The distinction the rest of the block is built on
> **Clipping** removes geometry wholly or partly *outside the view volume*; every test is against the volume's six boundaries.
> **Hidden-surface removal** (visible-surface detection) removes surfaces *inside* the volume that are blocked by nearer surfaces; every test compares depths along a projector.

Inside the volume there are four cases: object 1 completely outside (clipped away), object 2 crossing a boundary (trimmed), object 3 inside and nearest (kept, visible), object 4 inside but behind 3 (its occluded part must be found by hidden-surface removal). Objects 3 and 4 pass *every* clipping test; only a comparison along the projectors separates them.

Two consequences:

- **Visibility is view-dependent.** Two objects seen end-on may hide one another completely; from the side both are visible. Every hidden-surface answer is for one viewing specification.
- **Visibility is per sample.** A projector passes through each image sample; several surfaces may intersect it. Only surfaces whose projected polygon *covers* the sample compete, and for opaque surfaces the nearest covered intersection wins. No covering surface ⇒ background colour.

| | Object-space methods | Image-space methods |
| --- | --- | --- |
| Unit of work | object / face | pixel / sample |
| Output | exact geometry, device independent | sampled image |
| Advantage | valid at any resolution | simple per-candidate tests, easy in hardware |
| Cost | comparisons, intersections, splitting | one or more tests per pixel; cost grows with resolution |

**Resolution and sampling rule.** One sample per pixel, at the pixel centre; a pixel is covered if its centre is covered; a centre exactly on an edge counts as covered (closed triangle). At $4\times4$ that gives 10 of 16 pixels; at $8\times8$, 21 of 64. The object-space answer does not change with resolution; the image-space answer is recomputed at every resolution.

### 3.16 Interactive dry run

> [!tip] How to use the widget
> The polygon $[(-1,0),(3,0),(1,3)]$ is clipped against $[0,2]^{2}$ in the book order left → right → top → bottom. Each step processes **one edge** and names its case. The right-hand column is the output list *growing*, which is the part that exam questions ask you to reproduce.

```html
<div id="w-sh" style="border:1px solid var(--background-modifier-border,#ccc);border-radius:10px;padding:12px;background:var(--background-primary,#fff);color:var(--text-normal,#222);font:14px/1.45 var(--font-interface,system-ui,sans-serif)">
  <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px">
    <button id="sh-play" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--interactive-accent,#4a7fd4);color:var(--text-on-accent,#fff);cursor:pointer">▶ Play</button>
    <button id="sh-pause" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--background-secondary,#eee);color:var(--text-normal,#222);cursor:pointer">⏸ Pause</button>
    <button id="sh-next" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--background-secondary,#eee);color:var(--text-normal,#222);cursor:pointer">⏭ Next Step</button>
    <button id="sh-reset" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--background-secondary,#eee);color:var(--text-normal,#222);cursor:pointer">↺ Reset</button>
  </div>
  <div id="sh-say" style="min-height:40px;color:var(--text-muted,#555);margin-bottom:8px">Ready. Triangle (−1,0), (3,0), (1,3); window 0≤x≤2, 0≤y≤2.</div>
  <div style="display:flex;gap:12px;flex-wrap:wrap">
    <svg id="sh-stage" viewBox="0 0 360 330" style="flex:1 1 330px;max-width:100%;background:var(--background-secondary,#f7f7f7);border-radius:8px"></svg>
    <div style="flex:1 1 260px;min-width:230px">
      <div id="sh-pass" style="font-weight:600;margin-bottom:6px"></div>
      <div id="sh-out" style="font:13px/1.7 ui-monospace,monospace;color:var(--text-normal,#222)"></div>
      <div id="sh-log" style="margin-top:8px;font-size:12px;color:var(--text-muted,#666)"></div>
    </div>
  </div>
</div>
<script>
(() => {
  const W = { xmin: 0, xmax: 2, ymin: 0, ymax: 2 };
  const start = [[-1, 0], [3, 0], [1, 3]];
  const passes = [
    { name: "left  x ≥ 0", axis: 0, b: 0, inside: p => p[0] >= 0 },
    { name: "right  x ≤ 2", axis: 0, b: 2, inside: p => p[0] <= 2 },
    { name: "top  y ≤ 2", axis: 1, b: 2, inside: p => p[1] <= 2 },
    { name: "bottom  y ≥ 0", axis: 1, b: 0, inside: p => p[1] >= 0 }
  ];
  const steps = [];
  let V = start.map(p => p.slice());
  passes.forEach((ps, pi) => {
    const out = [];
    const n = V.length;
    steps.push({ pi, ps, phase: "pass-start", input: V.map(p => p.slice()), out: [], log: "── " + ps.name + ": input list of " + n + " vertices" });
    for (let i = 0; i < n; i++) {
      const S = V[i], E = V[(i + 1) % n];
      const inS = ps.inside(S), inE = ps.inside(E);
      let kase, added = [], I = null;
      if (inS && inE) { kase = "In → In"; out.push(E.slice()); added = [E]; }
      else if (inS && !inE) {
        const t = (ps.b - S[ps.axis]) / (E[ps.axis] - S[ps.axis]);
        I = ps.axis === 0 ? [ps.b, S[1] + t * (E[1] - S[1])] : [S[0] + t * (E[0] - S[0]), ps.b];
        kase = "In → Out"; out.push(I.slice()); added = [I];
      } else if (!inS && inE) {
        const t = (ps.b - S[ps.axis]) / (E[ps.axis] - S[ps.axis]);
        I = ps.axis === 0 ? [ps.b, S[1] + t * (E[1] - S[1])] : [S[0] + t * (E[0] - S[0]), ps.b];
        kase = "Out → In"; out.push(I.slice()); out.push(E.slice()); added = [I, E];
      } else { kase = "Out → Out"; }
      steps.push({ pi, ps, phase: "edge", S: S.slice(), E: E.slice(), kase, I, added, input: V.map(p => p.slice()), out: out.map(p => p.slice()),
        log: "edge " + fmt(S) + " → " + fmt(E) + " : " + kase + " · append " + (added.length ? added.map(fmt).join(", then ") : "nothing") });
    }
    V = out;
    steps.push({ pi, ps, phase: "pass-end", input: V.map(p => p.slice()), out: V.map(p => p.slice()), log: "── result after " + ps.name + ": " + (V.length ? V.map(fmt).join(" , ") : "empty") });
  });
  steps.push({ pi: passes.length - 1, ps: passes[passes.length - 1], phase: "done", input: V.map(p => p.slice()), out: V.map(p => p.slice()), log: "Final clipped polygon V′ with " + V.length + " vertices." });

  function fmt(p) { return "(" + p.map(v => +v.toFixed(2)).join(", ") + ")"; }
  const X = x => 30 + (x + 1.6) * (300 / 5.2);
  const Y = y => 290 - (y + 0.6) * (260 / 4.2);
  const NS = "http://www.w3.org/2000/svg";
  const el = (n, a) => { const e = document.createElementNS(NS, n); for (const k in a) e.setAttribute(k, a[k]); return e; };
  let i = 0, timer = null;

  function poly(pts, attrs) {
    return el("polyline", Object.assign({ points: pts.map(p => X(p[0]) + "," + Y(p[1])).join(" "), fill: "none" }, attrs));
  }
  function draw(s) {
    const st = document.getElementById("sh-stage");
    st.innerHTML = "";
    st.appendChild(el("rect", { x: X(W.xmin), y: Y(W.ymax), width: X(W.xmax) - X(W.xmin), height: Y(W.ymin) - Y(W.ymax), fill: "rgba(47,158,68,0.10)", stroke: "#2f9e44", "stroke-width": 2 }));
    st.appendChild(el("text", { x: X(W.xmin) + 4, y: Y(W.ymax) - 6, "font-size": 11, fill: "#2f9e44" })).textContent = "window 0…2";
    if (s.input && s.input.length > 1) st.appendChild(poly(s.input.concat([s.input[0]]), { stroke: "#adb5bd", "stroke-width": 1.5, "stroke-dasharray": "4 4" }));
    if (s.out && s.out.length > 1) {
      st.appendChild(poly(s.out.concat([s.out[0]]), { stroke: "#1971c2", "stroke-width": 2.5, fill: "rgba(25,113,194,0.16)" }));
      s.out.forEach(p => st.appendChild(el("circle", { cx: X(p[0]), cy: Y(p[1]), r: 3.5, fill: "#1971c2" })));
    }
    if (s.S && s.E) {
      st.appendChild(el("line", { x1: X(s.S[0]), y1: Y(s.S[1]), x2: X(s.E[0]), y2: Y(s.E[1]), stroke: "#e8590c", "stroke-width": 3 }));
      if (s.I) st.appendChild(el("circle", { cx: X(s.I[0]), cy: Y(s.I[1]), r: 5, fill: "none", stroke: "#e8590c", "stroke-width": 2 }));
    }
    const ax = el("text", { x: 8, y: 318, "font-size": 10, fill: "var(--text-faint,#888)" });
    ax.textContent = "grey dashed = input polygon · orange = edge being processed · blue = output list so far";
    st.appendChild(ax);
  }
  function paint() {
    const s = steps[i];
    draw(s);
    document.getElementById("sh-say").textContent = s.log;
    document.getElementById("sh-pass").textContent = "Pass " + Math.min(s.pi + 1, 4) + " of 4 — " + s.ps.name;
    const o = document.getElementById("sh-out");
    o.innerHTML = "<b>out list</b><br>" + (s.out.length ? s.out.map((p, k) => k + ": " + fmt(p)).join("<br>") : "<i>empty</i>");
    const keep = steps.slice(0, i + 1).filter(x => x.phase === "edge").slice(-4);
    document.getElementById("sh-log").innerHTML = keep.map(x => "· " + x.log).join("<br>");
  }
  const stop = () => { if (timer) { clearInterval(timer); timer = null; } };
  document.getElementById("sh-next").onclick = () => { stop(); if (i < steps.length - 1) i++; paint(); };
  document.getElementById("sh-reset").onclick = () => { stop(); i = 0; paint(); };
  document.getElementById("sh-pause").onclick = stop;
  document.getElementById("sh-play").onclick = () => { stop(); timer = setInterval(() => { if (i < steps.length - 1) { i++; paint(); } else stop(); }, 900); };
  paint();
})();
</script>
```

### 3.17 Exam pointer

> [!tip] Exam pointer — polygon clipping
> - State why per-edge clipping fails (no closed boundary; needs new vertices *and* new edges).
> - Reproduce the four-case table and the intersection formulas; explain why outside–outside appends nothing.
> - Run the numeric trace for $(-1,0),(3,0),(1,3)$ to the six-vertex result, pass by pass.
> - Give the concave U failure with the list $[2',3,4,4',6',7,8,8']$ and say what it renders wrongly.
> - Contrast Weiler–Atherton: entry/exit labels, alternation, one contour per region.
> - Know the 3D point test, the three bounding-box outcomes, and that overlap is inconclusive.
> - Distinguish clipping from occlusion in one sentence, and give one object-space and one image-space advantage.

---

## 4. Hidden Surface Removal I — Back-Face Elimination and the Z-Buffer

*Deck: [[CG_Oct_8.pdf]] — 106 slides. The two first-line defences: throw away faces that point away from the eye, then resolve the rest pixel by pixel with a depth buffer.*

### 4.1 Back-face elimination

For a closed polyhedron, every face has an **outward normal**. A face whose normal turns away from the viewer cannot be seen from this viewpoint, so it can be discarded before any pixel work.

The normal is obtained from the vertex order by a cross product — the order encodes the orientation:

$$ \mathbf{N} = (B-A)\times(C-A) \quad\text{for the face } A\to B\to C\to A $$

For the view vector $\mathbf{v}$ (pointing from the eye into the scene, here $\mathbf{v}=(0,0,-1)$):

$$ \mathbf{N}\cdot\mathbf{v} = -N_z \qquad
\begin{cases}
<0 & \text{front-facing: retain}\\
>0 & \text{back-facing: eliminate}\\
=0 & \text{edge-on: degenerate, no area}
\end{cases} $$

> [!important] Definitions
> **Outward normal** — the normal computed from a face's counter-clockwise (seen from outside) vertex order; it points out of the solid.
> **Front-facing** — the face's normal has a negative component along the view direction, i.e. the face turns towards the eye.
> **Back-face elimination** — discarding all back-facing polygons before rendering. Also called back-face culling.

> [!note] Why counter-clockwise seen from outside
> The right-hand rule ties the cross product to the vertex order: reversing the order reverses $\mathbf{N}$. A consistent outward convention therefore turns a purely combinatorial fact (the order the vertices were stored in) into a geometric one (which side is outside). Get the convention backwards and the algorithm culls exactly the visible faces.

### 4.2 Worked example: a tetrahedron viewed along $-z$

Given $A=(4,5,4)$, $B=(2,3,6)$, $C=(6,1,4)$, $D=(3,2,2)$, viewing vector $\mathbf{v}=(0,0,-1)$, and the outward face list $ABC$, $ADB$, $DCB$, $ACD$.

**Face $ABC$ — retain.**

$$ AB=B-A=(-2,-2,2),\qquad AC=C-A=(2,-4,0) $$
$$ N_x=(-2)(0)-(2)(-4)=8,\quad N_y=(2)(2)-(-2)(0)=4,\quad N_z=(-2)(-4)-(-2)(2)=12 $$
$$ \mathbf{N}=(8,4,12),\qquad \mathbf{N}\cdot\mathbf{v}=-N_z=-12<0 \;\Rightarrow\; \text{front-facing} $$

Outward check against the fourth vertex: $\mathbf{N}\cdot AD = 8(-1)+4(-3)+12(-2)=-44<0$, so $D$ lies behind the face — the normal does point out.

**Face $ADB$ — eliminate.**

$$ AD=(-1,-3,-2),\qquad AB=(-2,-2,2) $$
$$ N_x=(-3)(2)-(-2)(-2)=-10,\quad N_y=(-2)(-2)-(-1)(2)=6,\quad N_z=(-1)(-2)-(-3)(-2)=-4 $$
$$ \mathbf{N}=(-10,6,-4),\qquad \mathbf{N}\cdot\mathbf{v}=4>0 \;\Rightarrow\; \text{back-facing} $$

**Face $DCB$ — retain.**

$$ DC=(3,-1,2),\qquad DB=(-1,1,4) $$
$$ N_x=(-1)(4)-(2)(1)=-6,\quad N_y=(2)(-1)-(3)(4)=-14,\quad N_z=(3)(1)-(-1)(-1)=2 $$
$$ \mathbf{N}=(-6,-14,2),\qquad \mathbf{N}\cdot\mathbf{v}=-2<0 \;\Rightarrow\; \text{front-facing} $$

**Face $ACD$ — eliminate.**

$$ AC=(2,-4,0),\qquad AD=(-1,-3,-2) $$
$$ N_x=(-4)(-2)-(0)(-3)=8,\quad N_y=(0)(-1)-(2)(-2)=4,\quad N_z=(2)(-3)-(-4)(-1)=-10 $$
$$ \mathbf{N}=(8,4,-10),\qquad \mathbf{N}\cdot\mathbf{v}=10>0 \;\Rightarrow\; \text{back-facing} $$

| Face | Normal $\mathbf{N}$ | $\mathbf{N}\cdot\mathbf{v}$ | Result |
| --- | --- | --- | --- |
| $ABC$ | $(8,4,12)$ | $-12$ | retain |
| $ADB$ | $(-10,6,-4)$ | $4$ | eliminate |
| $DCB$ | $(-6,-14,2)$ | $-2$ | retain |
| $ACD$ | $(8,4,-10)$ | $10$ | eliminate |

![[CG - Tetrahedron Back Face Result.png|480]]

*Figure — the tetrahedron from an oblique viewpoint with the two retained faces $ABC$ and $DCB$ shaded; the hidden edge $AD$ is dashed. The on-screen winding matches the sign test: retained faces wind counter-clockwise, eliminated faces clockwise.*

Two independent checks the deck performs:

- $\mathbf{N}\cdot(\text{opposite vertex} - \text{face vertex}) = -44 < 0$ for **every** face — the normals are outward, consistently.
- $\mathbf{N}_{ABC}+\mathbf{N}_{ADB}+\mathbf{N}_{DCB}+\mathbf{N}_{ACD}=(0,0,0)$ — the normals of a closed surface sum to zero.

### 4.3 Why back-face elimination is not enough

Back-face elimination compares a face with **its own** solid only. It cannot answer:

- whether face $X$ of object 1 is hidden by face $Y$ of object 2 (inter-object occlusion);
- whether two front-facing faces overlap on screen and which is nearer;
- anything about an open surface (a single sheet has no "outside", so the sign is meaningless);
- anything about a concave solid, where one front-facing part can hide another front-facing part.

What survives culling still needs a depth comparison per pixel or per object. That is the job of the next two methods.

### 4.4 The depth (z) buffer: the idea

The z-buffer is an **image-space** method: two buffers of the same size as the screen, one storing the nearest depth found so far at each pixel, one storing the colour that produced it.

| Buffer | Symbol | Content | Initial value |
| --- | --- | --- | --- |
| Depth buffer | $DB[x][y]$ | depth of the nearest surface seen at pixel $(x,y)$ | $1$ (the far limit) |
| Frame buffer | $FB[x][y]$ | colour of that surface | background colour |

For every surface, and every pixel its projection covers, compute the surface's depth $z$ at that pixel and compare with the stored value:

$$ \text{if } z < DB[x][y] \text{ then } DB[x][y]=z,\; FB[x][y]=\text{colour of the surface} $$

Because the comparison is per pixel, the surfaces may be processed in **any order** — the result is identical, which is what makes the method hardware-friendly and immune to the cyclic-overlap problem that defeats the painter's algorithm (§5.2).

![[CG - Z Buffer.excalidraw]]

### 4.5 Depth from the plane equation

Every planar surface satisfies

$$ Ax+By+Cz+D=0 \quad\Longrightarrow\quad z=\frac{-D-Ax-By}{C},\qquad C\neq0 $$

so one division per *surface*, and then a linear expression per pixel. The constants come from the surface normal and one known point:

$$ \mathbf{N}=(A,B,C)=(P_2-P_1)\times(P_3-P_1),\qquad D=-Ax_1-By_1-Cz_1 $$

> [!important] Deriving the plane of a surface — the three steps
> 1. **Two vectors in the plane:** $\mathbf{u}=P_2-P_1$, $\mathbf{v}=P_3-P_1$.
> 2. **Normal by cross product:** $\mathbf{N}=\mathbf{u}\times\mathbf{v}=(A,B,C)$.
> 3. **Form the equation:** substitute $\mathbf{N}$ and any one vertex into $Ax+By+Cz+D=0$ and solve for $D$.

### 4.6 Incremental depth: never evaluate the plane twice

Evaluating $z=(-D-Ax-By)/C$ at every pixel costs a multiply and a divide per pixel. Because $z$ is linear in $x$ and $y$, each step across a scan line changes $z$ by a **constant**:

$$ z(x+1,y)=z(x,y)-\frac{A}{C} \qquad\text{(one pixel right)} $$
$$ z(x,y-1)=z(x,y)+\frac{B}{C} \qquad\text{(one scan line down)} $$
$$ z(x+1,y-1)=z(x,y)-\frac{A}{C}+\frac{B}{C} \qquad\text{(right and down in one step)} $$

> [!note] Where the constants come from
> Write $z=(-D-Ax-By)/C$. Increasing $x$ by 1 subtracts $A/C$; decreasing $y$ by 1 adds $B/C$. Both are independent of position, so they are computed **once per surface** and then only added. No divide appears inside the pixel loop.

**Edge pixels.** When the next scan line is reached, the leftmost covered pixel moves in $x$ as well. For an edge of slope $m$, the new $x$-coordinate is

$$ x' = x-\frac{1}{m} $$

so the depth at the first pixel of the new scan line is

$$ z' = z - \frac{A}{C} - \frac{B}{mC} \quad\text{equivalently}\quad z' = z - \frac{A}{C}\left(1-\frac{1}{m}\right)\text{ only when } x \text{ is unchanged} $$

The two terms account, respectively, for the change of $x$ across scan lines and the change of $y$ between them. This is **scan-line coherence**: neighbouring pixels on a surface have neighbouring depths, so the buffer is filled by addition.

**Worked numeric check.** Take a surface with $A=2$, $B=1$, $C=2$, $D=-10$, i.e. $z=(10-2x-y)/2$.

- At pixel $(1,2)$: $z=(10-2-2)/2=3.0$.
- One pixel right, $(2,2)$: $z=3.0-A/C=3.0-1.0=2.0$; direct check gives $(10-4-2)/2=2.0$ ✓.
- One scan line down, $(1,1)$: $z=3.0+B/C=3.5$; direct check gives $(10-2-1)/2=3.5$ ✓.
- Right and down, $(2,1)$: $z=3.0-1.0+0.5=2.5$; direct check gives $(10-4-1)/2=2.5$ ✓.

### 4.7 The algorithm

> [!important] Depth-buffer algorithm — statement
> ```text
> 1: for every pixel: DB[x][y] = 1 (far), FB[x][y] = background
> 2: for each surface:
> 3:     derive A, B, C, D from its plane
> 4:     for each scan line y the surface covers:
> 5:         compute the leftmost covered x and its depth z
> 6:         for each pixel x across the span:
> 7:             if z < DB[x][y] then DB[x][y] = z; FB[x][y] = surface colour
> 8:             z = z - A/C            # step right
> 9:         z_next_line = z_at_left_edge - A/C + B/C
> 10: end for
> ```
> **Cost.** $O(nN)$ for $n$ surfaces overlapping $N$ pixels in total — one comparison per covered pixel, no sorting, no pairwise surface tests.

The deck's simplified form states the same loop with the buffers named $DV[\;][\;]$ and the depth written per scan line:

> [!important] Iterative depth calculation
> - Initialise $x$ to the leftmost pixel of the surface, $y$ to its top scan line, and $z$ to the depth at that leftmost edge point.
> - Set the constants $\Delta z_x=-A/C$ (change along the scan line) and $\Delta z_y=B/C$ (change between scan lines).
> - For each pixel across the scan line: store $z$ in $DV[x][y]$, then $z\mathrel{+}=\Delta z_x$.
> - At the end of a scan line: move the edge $x$ by $-1/m$, and update $z$ by $-A/C+B/C$ for the next scan line.

> [!warning] The three classic z-buffer errors
> - **Wrong depth direction.** If depth grows *inward*, the test is $z<DB$, and initialisation is the far value. Flip the convention without flipping the test and the farthest surface wins.
> - **Divide by zero.** $C=0$ means a surface parallel to the view plane's depth axis — the plane equation must be solved for $z$ from a different coefficient, or the surface rejected.
> - **Depth precision.** $z$ is interpolated after the perspective divide, so its spacing in screen space is non-linear; a small far plane range and a deep scene still collide in the buffer (z-fighting).

### 4.8 Interactive dry run

> [!tip] How to use the widget
> Two triangles are scan-converted in order, first the near one, then the far one. Each step is one covered pixel of one surface: the widget compares the new $z$ against $DB$ and shows the outcome. Watch the near surface win the overlap region, and watch the far one still paint the pixels the near one never covered.

```html
<div id="w-zb" style="border:1px solid var(--background-modifier-border,#ccc);border-radius:10px;padding:12px;background:var(--background-primary,#fff);color:var(--text-normal,#222);font:14px/1.45 var(--font-interface,system-ui,sans-serif)">
  <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px">
    <button id="zb-play" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--interactive-accent,#4a7fd4);color:var(--text-on-accent,#fff);cursor:pointer">▶ Play</button>
    <button id="zb-pause" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--background-secondary,#eee);color:var(--text-normal,#222);cursor:pointer">⏸ Pause</button>
    <button id="zb-next" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--background-secondary,#eee);color:var(--text-normal,#222);cursor:pointer">⏭ Next Step</button>
    <button id="zb-reset" style="padding:5px 12px;border-radius:6px;border:1px solid var(--background-modifier-border,#bbb);background:var(--background-secondary,#eee);color:var(--text-normal,#222);cursor:pointer">↺ Reset</button>
  </div>
  <div id="zb-say" style="min-height:40px;color:var(--text-muted,#555);margin-bottom:8px">Ready. Surface A (near, z≈2) is processed first, then surface B (far, z≈5).</div>
  <div style="display:flex;gap:14px;flex-wrap:wrap;align-items:flex-start">
    <div>
      <div style="font-size:12px;color:var(--text-muted,#666);margin-bottom:4px">frame buffer</div>
      <svg id="zb-fb" viewBox="0 0 300 240" style="width:300px;max-width:100%;background:var(--background-secondary,#f7f7f7);border-radius:8px"></svg>
    </div>
    <div>
      <div style="font-size:12px;color:var(--text-muted,#666);margin-bottom:4px">depth buffer</div>
      <svg id="zb-db" viewBox="0 0 300 240" style="width:300px;max-width:100%;background:var(--background-secondary,#f7f7f7);border-radius:8px"></svg>
    </div>
  </div>
</div>
<script>
(() => {
  const COLS = 10, ROWS = 8, CELL = 28;
  const triA = { pts: [[1, 1], [9, 2], [5, 7]], plane: (x, y) => 2 + 0.05 * x + 0.03 * y, colour: "#1971c2", name: "A" };
  const triB = { pts: [[0, 5], [7, 7], [9, 0]], plane: (x, y) => 5 + 0.05 * x + 0.03 * y, colour: "#e8590c", name: "B" };
  function inside(t, x, y) {
    const [a, b, c] = t.pts;
    const d1 = (x - b[0]) * (a[1] - b[1]) - (a[0] - b[0]) * (y - b[1]);
    const d2 = (x - c[0]) * (b[1] - c[1]) - (b[0] - c[0]) * (y - c[1]);
    const d3 = (x - a[0]) * (c[1] - a[1]) - (c[0] - a[0]) * (y - a[1]);
    const neg = d1 < 0 || d2 < 0 || d3 < 0, pos = d1 > 0 || d2 > 0 || d3 > 0;
    return !(neg && pos);
  }
  const steps = [];
  [triA, triB].forEach(t => {
    for (let y = 0; y < ROWS; y++) for (let x = 0; x < COLS; x++) {
      if (inside(t, x + 0.5, y + 0.5)) steps.push({ t, x, y, z: +t.plane(x, y).toFixed(2) });
    }
  });
  let db, fb, cur = -1, timer = null;
  const init = () => { db = Array.from({ length: ROWS }, () => Array(COLS).fill(1)); fb = Array.from({ length: ROWS }, () => Array(COLS).fill("")); cur = -1; };
  const NS = "http://www.w3.org/2000/svg";
  const el = (n, a) => { const e = document.createElementNS(NS, n); for (const k in a) e.setAttribute(k, a[k]); return e; };
  const tc = v => v >= 1 ? "1" : v.toFixed(2);

  function paint() {
    const s = cur >= 0 ? steps[cur] : null;
    const fbSvg = document.getElementById("zb-fb"), dbSvg = document.getElementById("zb-db");
    fbSvg.innerHTML = ""; dbSvg.innerHTML = "";
    for (let y = 0; y < ROWS; y++) for (let x = 0; x < COLS; x++) {
      const bg = fb[y][x] || "none";
      fbSvg.appendChild(el("rect", { x: x * CELL, y: y * CELL, width: CELL, height: CELL, fill: bg, stroke: "#ced4da", "stroke-width": 0.8 }));
      const d = el("text", { x: x * CELL + CELL / 2, y: y * CELL + CELL / 2 + 4, "font-size": 9, "text-anchor": "middle", fill: "var(--text-normal,#333)" });
      d.textContent = tc(db[y][x]);
      dbSvg.appendChild(el("rect", { x: x * CELL, y: y * CELL, width: CELL, height: CELL, fill: "none", stroke: "#ced4da", "stroke-width": 0.8 }));
      dbSvg.appendChild(d);
    }
    if (s) {
      fbSvg.appendChild(el("rect", { x: s.x * CELL + 1, y: s.y * CELL + 1, width: CELL - 2, height: CELL - 2, fill: "none", stroke: "#2f9e44", "stroke-width": 2.5 }));
      dbSvg.appendChild(el("rect", { x: s.x * CELL + 1, y: s.y * CELL + 1, width: CELL - 2, height: CELL - 2, fill: "none", stroke: "#2f9e44", "stroke-width": 2.5 }));
    }
    if (!s) { document.getElementById("zb-say").textContent = "Ready. Depth buffer = 1 everywhere; frame buffer empty."; return; }
    const px = db[s.y][s.x];
    const win = s.z < px;
    document.getElementById("zb-say").textContent =
      "Surface " + s.t.name + " at pixel (" + s.x + ", " + s.y + "): z = " + s.z.toFixed(2) +
      " · stored DB = " + (cur === 0 ? "1" : tc(px)) + " → " + (win ? "z < DB: write depth and colour" : "z ≥ DB: reject, nearer surface stays") +
      (win && s.z < 100 ? "" : "");
  }
  function step() {
    if (cur >= steps.length - 1) { if (timer) { clearInterval(timer); timer = null; } return; }
    cur++;
    const s = steps[cur];
    const win = s.z < db[s.y][s.x];
    if (win) { db[s.y][s.x] = s.z; fb[s.y][s.x] = s.t.colour; }
    paint();
  }
  document.getElementById("zb-next").onclick = () => { if (timer) { clearInterval(timer); timer = null; } step(); };
  document.getElementById("zb-reset").onclick = () => { if (timer) { clearInterval(timer); timer = null; } init(); paint(); };
  document.getElementById("zb-pause").onclick = () => { if (timer) { clearInterval(timer); timer = null; } };
  document.getElementById("zb-play").onclick = () => { if (timer) clearInterval(timer); timer = setInterval(step, 240); };
  init(); paint();
})();
</script>
```

### 4.9 Exam pointer

> [!tip] Exam pointer — back-face and z-buffer
> - Compute $\mathbf{N}=(B-A)\times(C-A)$ and classify by the sign of $\mathbf{N}\cdot\mathbf{v}$; know that $\mathbf{N}\cdot\mathbf{v}=-N_z$ for $\mathbf{v}=(0,0,-1)$.
> - Reproduce the tetrahedron table with all four normals, and the two checks (opposite-vertex dot product, normals summing to zero).
> - Say precisely what back-face elimination cannot do (inter-object, concave, open surfaces).
> - Write $z=(-D-Ax-By)/C$, then $\Delta z_x=-A/C$ and $\Delta z_y=+B/C$; derive both from the plane equation.
> - State the cost $O(nN)$, the arbitrary processing order, and the three failure modes (depth direction, $C=0$, precision).

---

<!-- §NEXT§ -->
