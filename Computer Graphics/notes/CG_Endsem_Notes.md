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

<!-- §NEXT§ -->
