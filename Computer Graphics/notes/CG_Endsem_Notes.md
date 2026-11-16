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

This block carries the course from a scene described in three dimensions to the pixels that finally appear on the screen. Every deck in it is one **stage of the viewing pipeline**: re-describe the scene from the camera (§1), build the view volume and the projection (§2), clip what falls outside it — lines first, then filled polygons and 3D faces (§3–§4), decide which of the surviving surfaces is actually seen (§5–§6), convert the surviving areas into pixels (§7), and then repair the damage that discretisation does to those pixels (§8). The last deck leaves the geometry behind and animates it (§9).

*Topic list and progress: [[CG_Syllabus]] · formatting rules: [[CG_context]] · the earlier block: [[CG_Midsem_notes]].*

> [!info] How the block is organised
> | Topic | Deck | Slides | Question it answers |
> | --- | --- | --- | --- |
> | 1 | [[Post 1 - 3D Viewing Transformation and Camera Setup (28 Sep).pdf|Post 1 deck]] | 76 | How is the world re-described from the camera's point of view, and why must it then be projected? |
> | 2 | [[Post 2 - 3D Viewing, Camera and Projection Fundamentals.pdf|Post 2 deck]] | 78 | Where is the camera, what can it see, and how does 3D become a 2D coordinate? |
> | 3 | [[Post 3 - Viewport Mapping and Cohen-Sutherland Clipping.pdf|Post 3 deck]] | 97 | How is the 2D image placed on the screen, and how is a line trimmed to the window? |
> | 4 | [[Post 4 - Polygon and 3D Fill-Area Clipping.pdf|Post 4 deck]] | 89 | How is a *filled* polygon clipped, and how is a 3D face clipped? |
> | 5 | [[Post 5 - Hidden Surface Removal I - Back-Face Elimination and the Z-Buffer.pdf|Post 5 deck]] | 106 | Which faces point away, and which surface is nearest at each pixel? |
> | 6 | [[Post 6 - Hidden Surface Removal II - Painter's Algorithm and BSP Trees.pdf|Post 6 deck]] | 80 | How do we order whole polygons, and what if no order exists? |
> | 7 | [[Post 7 - Fill-Area Algorithms, Scan Conversion and the 3D Pipeline.pdf|Post 7 deck]] | 116 | How is the interior of a polygon filled, and how are characters drawn? |
> | 8 | [[Post 8 - Anti-Aliasing I - The Gupta-Sproull Algorithm.pdf|Post 8 deck]] | 70 | How is a jagged line made smooth? |
> | 9 | [[Post 9 - Animation - The 2D Production Process.pdf|Post 9 deck]] | 55 | How is motion produced from still drawings? |

> [!warning] The four conventions this block uses everywhere
> - **Right-handed** coordinates; **the viewer looks along $-z$** in the camera frame, so visible points have $z<0$.
> - **Depth grows inward**: a larger $z$ (or larger $|z|$, as the deck states it) means *farther from the eye*.
> - **Clip order** for polygons is **left → right → top → bottom**; for outcodes the bit order is **Far Near Top Bottom Right Left** (bit 5 … bit 0).
> - **Ties count as inside**: a point exactly on a clip boundary is retained, and a midpoint exactly on the line chooses E. Both are examinable choices, not accidents.

---

## 1. 3D Viewing Transformation and Camera Setup

*Deck: [[Post 1 - 3D Viewing Transformation and Camera Setup (28 Sep).pdf|Post 1 deck]] — 76 slides (28 September). The camera analogy, the view coordinate system $\mathbf u,\mathbf v,\mathbf n$, the world-to-view matrix with a full numeric example, and the motivation for projection.*

### 1.1 Viewing as taking a photograph

The 28 September lecture ([[Post 1 - 3D Viewing Transformation and Camera Setup (28 Sep).pdf|Post 1 deck]], 76 pages) opens the post-midsem block. It builds the viewing transformation from scratch — a camera analogy, the view coordinate system and a fully numeric example — and then motivates projection. The next lecture, [[Post 2 - 3D Viewing, Camera and Projection Fundamentals.pdf|Post 2 deck]], recaps it and goes on to the canonical cube, the projection matrices and viewport mapping (§2). It opens with the whole chain on one slide:

![[CG - Object to Screen Space Pipeline.png|760]]
*Object space → world space → camera space → canonical view volume → screen space (Post 1 deck, p. 59). Transformations change the coordinate description; the scene geometry stays the same until projection.*

| Space | Meaning | Obtained by |
| --- | --- | --- |
| **Object space** | the object's local coordinates | — |
| **World space** | objects positioned in the shared scene | model transform |
| **Camera / view space** | coordinates relative to the camera's position and orientation (camera at origin) | view (camera) transformation |
| **Canonical view volume** | normalised cube $-1\le x,y,z\le 1$ after projection and clipping | projection transformation (perspective or orthographic) |
| **Screen space** | final 2D pixel coordinates | viewport transformation |

#### Why a viewing transformation exists

The deck argues from photography. To take a photograph we point the camera in a direction with an orientation, set the focus, and click. We never look at the scene directly — we look **through the camera**, and focusing tells us the quality and coverage of the picture.

- **First case — looking directly at the scene:** we see it in the **world coordinate system**.
- **Second case — looking through the camera:** we see a *different scene*, one that is **changed** by the arrangement of lenses in the camera, to aid our estimation.
- So taking a photograph means **transforming the 3D world-coordinate scene into a description in another coordinate system**, characterised by the camera parameters (position and orientation).
- That new system is called the **view coordinate system (VC)**; the transformation is the **viewing transformation**.
- To simulate it: first define the view coordinate system, then perform the transformation.

#### Setting up the view coordinate system

![[CG - View Coordinate Setup.png|520]]
*The camera basis, the view-up vector and the view plane (Post 1 deck, p. 27).*

The basis vectors of VC are written $\mathbf{u},\mathbf{v},\mathbf{n}$ (rather than $x,y,z$ — the deck says it uses this notation from here on). The deck determines them in this order:

1. **Origin.** The camera is represented as a point in the 3D world coordinate system; that point is the origin of VC, denoted $\mathbf{o}$.
2. **$\hat{\mathbf{n}}$.** With a *look-at point* $\mathbf{p}$ (the centre of interest), simple vector algebra gives $\mathbf{n}=\mathbf{o}-\mathbf{p}$, normalised: $\hat{\mathbf{n}}=\mathbf{n}/\lVert\mathbf{n}\rVert$. So $\hat{\mathbf n}$ points **opposite to the looking direction**.
3. **$\hat{\mathbf{v}}$.** Specify an arbitrary point $\mathbf{p}_{up}$ in the direction of the head while looking through the camera — the **view-up** direction. Then $\vec V_{up}=\mathbf{p}_{up}-\mathbf{o}$ and $\hat{\mathbf v}=\vec V_{up}/\lVert\vec V_{up}\rVert$.
4. **$\hat{\mathbf{u}}$.** $\mathbf u$ is perpendicular to the plane spanned by $\mathbf n$ and $\mathbf v$, hence $\mathbf u=\mathbf v\times\mathbf n$. Since $\mathbf n$ and $\mathbf v$ are unit vectors, **no further normalisation is required**.

> [!important] Summary of the VC construction (deck's summary slide)
> Given the camera position $\bar o$ (origin of the coordinate system), the view-up point $\bar p_{up}$ and the centre of interest / look-at point $\bar p$:
> 1. $\hat n$ — unit basis vector opposite to the looking direction: $\bar n=\bar o-\bar p$, $\hat n=\bar n/|\bar n|$.
> 2. $\hat v$ — unit basis vector along the view-up direction: $\vec V_{up}=\bar p_{up}-\bar o$, $\hat v=\vec V_{up}/|\vec V_{up}|$.
> 3. $\hat u$ — the third unit basis vector: $\hat u=\hat v\times\hat n$.

> [!warning] Two conventions for the same frame
> §2.2 writes $\mathbf u=\mathbf v_{up}\times\mathbf n$ and $\mathbf v=\mathbf n\times\mathbf u$, which *re-orthogonalises* $\mathbf v$ and so works for any up-vector. The 28 September deck takes $\hat{\mathbf v}$ directly from the view-up vector and then $\hat{\mathbf u}=\hat{\mathbf v}\times\hat{\mathbf n}$; this is exact only when the view-up vector is already perpendicular to $\mathbf n$, which is true in its example. Both give the same frame in that case — use the deck's form when solving its numericals.

#### The transformation $M_{w2v}$

Let $P$ be an arbitrary point in world coordinates. We need a matrix $M_{w2v}$ such that $P'=M_{w2v}\,P$ is the point in VC. Assume the VC origin (the camera position) is $(o_{vx},o_{vy},o_{vz})$ and the three basis vectors are $\mathbf u(u_x,u_y,u_z)$, $\mathbf v(v_x,v_y,v_z)$, $\mathbf n(n_x,n_y,n_z)$. To align VC with WC we need a **sequence of transformations**, achieved by two operations — **translation** and **rotation**.

The deck builds the matrix in four named steps (translate, rotate, compose, transform), with the translation written out as

$$ T=\begin{bmatrix}1&0&0&-o_{vx}\\0&1&0&-o_{vy}\\0&0&1&-o_{vz}\\0&0&0&1\end{bmatrix},\qquad
R=\begin{bmatrix}u_x&u_y&u_z&0\\v_x&v_y&v_z&0\\n_x&n_y&n_z&0\\0&0&0&1\end{bmatrix},\qquad M_{w2v}=R\,T $$

- **Step 1 — translation.** Subtract the camera position from each point; the camera maps to the origin; orientation does not change.
- **Step 2 — rotation.** Rows are the camera basis vectors; each row gives one view coordinate. *Why this is correct:* each row computes one dot product with $\mathbf u$, $\mathbf v$ or $\mathbf n$, and orthonormal rows preserve lengths and angles.
- **Step 3 — compose.** Translation acts first for column vectors, so $M_{w2v}=RT$, applied once to every point.
- **Compact form.** Each translation term is the *negative projection of the camera position onto one camera axis* ($-\mathbf u\cdot\mathbf o$, $-\mathbf v\cdot\mathbf o$, $-\mathbf n\cdot\mathbf o$); rows 1–3 give the camera-axis coordinates, the last column accounts for the camera position, the last row preserves homogeneous form (this is the matrix of §2.2).
- The camera is **not projected yet**; projection is a separate transformation applied after points are expressed in view coordinates.

### 1.2 Worked example: the square object

![[CG - Camera Basis Example Scene.png|520]]
*The scene (Post 1 deck, p. 46): square object with $A(2,1,0)$, $B(2,3,0)$, $C(2,3,3)$, $D(2,1,3)$; camera at $(1,2,2)$ looking at the object centre $(2,2,2)$.*

> *We are looking at the square object with vertices $A(2,1,0)$, $B(2,3,0)$, $C(2,3,3)$, $D(2,1,3)$. The camera is located at the point $(1,2,2)$. The look-at point is the centre of the object $(2,2,2)$. The up direction is parallel to the positive $z$ direction. What is the coordinate of the centre of the object, after its transformation to the viewing coordinate system?*

**Step 1 — the three basis vectors.**

- Camera position $\mathbf o=(1,2,2)$, look-at point $\mathbf p=(2,2,2)$.
- $\mathbf n=\mathbf o-\mathbf p=(-1,0,0)$, already unit length, so $\hat{\mathbf n}=(-1,0,0)$.
- The up direction is parallel to $+z$, so directly $\hat{\mathbf v}=(0,0,1)$ without any further calculation. (Another way of specifying the up vector, instead of a point in the up direction, is to give the direction itself.)
- $\hat{\mathbf u}=\hat{\mathbf v}\times\hat{\mathbf n}=(0,0,1)\times(-1,0,0)=(0,-1,0)$.

So the deck's basis is $\hat n(-1,0,0)$, $\hat u(0,-1,0)$, $\hat v(0,0,1)$ — this follows the cross-product order the deck fixed in Part 1.

**Step 2 — the matrices.** With the basis vectors as rows and the camera position negated:

$$ R=\begin{bmatrix}0&-1&0&0\\0&0&1&0\\-1&0&0&0\\0&0&0&1\end{bmatrix},\qquad
T=\begin{bmatrix}1&0&0&-1\\0&1&0&-2\\0&0&1&-2\\0&0&0&1\end{bmatrix} $$

**Step 3 — compose** $M_{W2V}=RT$:

$$ \begin{bmatrix}0&-1&0&0\\0&0&1&0\\-1&0&0&0\\0&0&0&1\end{bmatrix}
\begin{bmatrix}1&0&0&-1\\0&1&0&-2\\0&0&1&-2\\0&0&0&1\end{bmatrix}
=\begin{bmatrix}0&-1&0&2\\0&0&1&-2\\-1&0&0&1\\0&0&0&1\end{bmatrix} $$

![[CG - Composite View Matrix Example.png|560]]
*The composite view matrix as printed in the deck (Post 1 deck, p. 56).*

Check of the last column with the compact form: $-\mathbf u\cdot\mathbf o=-(0\cdot1-1\cdot2+0)=2$; $-\mathbf v\cdot\mathbf o=-(2)=-2$; $-\mathbf n\cdot\mathbf o=-(-1)=1$. ✓

**Step 4 — transform the look-at point / object centre.** $P_{world}=[2,2,2,1]^{T}$:

$$ P_{view}=M_{W2V}P_{world}=\begin{bmatrix}-2+2\\2-2\\-2+1\\1\end{bmatrix}=[0,\,0,\,-1,\,1]^{T} $$

![[CG - Look-at Point Transform.png|560]]
*The look-at point lands at $P(0,0,-1)$ (Post 1 deck, p. 58).*

> [!note] Reading the answer
> The object centre is at $(0,0,-1)$: **one unit in front of the camera along $-\mathbf n$**. The camera is at the origin looking down the viewing axis, as required.

> [!note] Camera space, after the camera transformation
> **Input:** coordinates in world space. **Operation:** apply the view (camera) transformation so the camera is at the origin looking down its viewing axis. **Output:** coordinates in camera space (eye space). At this stage objects are still in 3D coordinates relative to the camera — they still have perspective depth, with no "squashing" yet.

### 1.3 Why projection is needed

The deck then re-enters the chain at the *projection* box, marking it "why projection needed" (Post 1 deck, p. 59).

- **The scene in the view coordinate system is 3D.** To get a 2D image we need a way to **transform** a 3D scene into a 2D one; the technique is **projection**.
- In general, projection transforms objects from $n$ dimensions to $(n-1)$ dimensions; the discussion is restricted to 3D → 2D.
- **Basic idea:** project a 3D object onto a 2D **view plane**. From each point of the surface we generate **straight lines towards the view plane**, known as **projectors**; the intersection points of the projectors with the view plane together give the projected image.
- A usually rectangular area on the view plane that contains the projected objects is the **clipping window**.
- A 3D **view volume** is also defined in the scene: objects inside it are projected onto the view plane; others are discarded through **clipping** (discussed later). The entire scene is *not* projected — only the portion enclosed by the view volume — which gives flexibility to synthesise images as we want.
- We therefore must choose an **appropriate view volume**, which requires an understanding of the different projection types.

| Projection | Projectors | Size vs depth | Typical use |
| --- | --- | --- | --- |
| **Parallel** | remain parallel | does not change with depth | measurement and CAD |
| **Perspective** | meet at the camera | distant objects appear smaller | realistic depth cues |

![[CG - Perspective Foreshortening.png|560]]
*Discussion slide "Why does perspective look natural?" — perspective foreshortening: apparent size decreases with distance (Post 1 deck, p. 75).*

The deck closes the section with the question *how to derive the projection matrix?*, and promises to derive each transformation separately before comparing their equations — that derivation is §2.5.

> [!note] Coverage of this deck
> The deck's final slides about the projection types (p. 62) are exported with unreadable fonts (mojibake); the table above was taken from the readable slide 74 and the figures. Slides 1–10 are blank title slides.

### 1.4 Exam pointer

> [!tip] Exam pointer — the viewing transformation
> - Build $\hat n=(\mathbf o-\mathbf p)/\lVert\mathbf o-\mathbf p\rVert$, then $\hat v$ from the view-up direction, then $\hat u=\hat v\times\hat n$ — in that order.
> - Write $M_{w2v}=R\,T$ with the basis vectors as the rows of $R$ and $-\mathbf o$ in $T$; know why translation acts first.
> - Reproduce the square-object example: $\hat n(-1,0,0)$, $\hat u(0,-1,0)$, $\hat v(0,0,1)$, the composite matrix, and $P_{view}=(0,0,-1)$.
> - Say that the camera transformation does not project; projection is the next, separate step.

---

## 2. 3D Viewing, Camera and Projection Fundamentals

*Deck: [[Post 2 - 3D Viewing, Camera and Projection Fundamentals.pdf|Post 2 deck]] — 78 slides. Compiles the pipeline overview, the world-to-view transform, the canonical view volume, the projection matrices and the viewport transform.*

### 2.1 The six stages in one picture

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

### 2.2 World-to-view: building the camera frame

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

### 2.3 The view volume

After the viewing transform, the part of space the camera can record is a **view volume** bounded by six planes $x_{\min},x_{\max},y_{\min},y_{\max},z_{near},z_{far}$.

![[CG - Camera Frame and View Volume.excalidraw]]

| Projection | Shape of the view volume | Parallel edges? | Object size with depth |
| --- | --- | --- | --- |
| **Parallel / orthographic** | parallelepiped (a box) | yes | constant |
| **Perspective** | frustum (truncated pyramid) | no | falls as $1/|z|$ |

Anything wholly outside the volume is **clipped away**; anything crossing a boundary is **trimmed**. Clipping is a pure efficiency device: every primitive that survives is cheaper than the ones that do not, because all later stages — projection divide, hidden-surface tests, scan conversion — only ever see the survivors.

### 2.4 Why normalise the volume to a canonical cube

The deck pauses on this question explicitly, because the answer explains half the matrices in the course.

> [!note] Why transform the view volume to a canonical cube
> - **One set of clip tests.** After normalisation every boundary is $x=\pm1$, $y=\pm1$, $z=\pm1$, so clipping and inside/outside tests are six comparisons against constants, with no per-scene parameters.
> - **One projection-independent pipeline.** Orthographic and perspective scenes reduce to the same cube, so everything downstream (clipping, hidden-surface removal, scan conversion) is written once.
> - **A fixed depth range.** $z\in[-1,1]$ gives the depth buffer a known range, so depth precision and the near/far mapping are decided in one place.
> - **Device independence.** The cube is dimensionless; resolution and aspect ratio are chosen later, at viewport mapping (§2.6).
> - **Hardware.** A fixed-function pipeline can hard-wire the comparisons.

The cost is a **non-uniform scale**: normalising a wide, shallow frustum squeezes it, and the perspective divide has already distorted distances. That is why depth must be interpolated *after* the divide, not before (the z-buffer section, §5.7, relies on this).

### 2.5 The projection matrices

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

### 2.6 Viewport mapping

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

### 2.7 Exam pointer


> [!tip] Exam pointer — viewing and projection
> - Write $M_{view}=\mathbf{R}\,T(-\mathbf{o})$ and say what each factor does; be ready to explain why translation comes first.
> - State the two view-volume shapes and which projection produces which.
> - Give three reasons for the canonical cube, and the one cost (non-uniform scale).
> - Know which matrix needs the divide and why: $w=-z_{cam}$ in the perspective matrix.
> - Derive $V_x=s_xW_x+t_x$ from the proportion; quote $s_x,t_x,s_y,t_y$; then apply them to a numeric window and viewport.
> - Name the two traps: the $y$-flip and the aspect ratio.

---

## 3. Viewport Mapping and Cohen–Sutherland Clipping

*Deck: [[Post 3 - Viewport Mapping and Cohen-Sutherland Clipping.pdf|Post 3 deck]] — 97 slides. Point clipping, the 4-bit region code, trivial accept/reject, iterative boundary intersection, then the same algorithm in 3D with six planes.*

### 3.1 Point clipping

A point $(x,y)$ is inside the window exactly when both intervals hold:

$$ x_{\min}\le x\le x_{\max} \quad\text{AND}\quad y_{\min}\le y\le y_{\max} $$

Equality counts as inside — a point on the boundary is retained. One violated interval is enough to reject.

### 3.2 Region codes

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

### 3.3 Trivial accept and trivial reject

Compute $C_0$ for $P_0$ and $C_1$ for $P_1$, then combine the two codes bitwise.

| Test | Result | Meaning |
| --- | --- | --- |
| $C_0 \;\text{OR}\; C_1 = 0000$ | **accept** | neither endpoint is outside any boundary |
| $C_0 \;\text{AND}\; C_1 \neq 0000$ | **reject** | both endpoints lie outside the *same* boundary |
| otherwise | **clip** | part of the segment may be visible |

The AND test works because a shared set bit means both endpoints are on the outer side of one boundary line. If $P$ and $Q$ are both left of $x=x_{\min}$ then $C_P=0001$ and $C_Q=0001$, so $C_P\;\text{AND}\;C_Q=0001\neq0000$: the segment cannot cross into the window, because the window lies entirely on the other side of that line. The same argument holds for *any* same-side combination — both above (bit 3), both below (bit 2), both right (bit 1), both left (bit 0).

> [!warning] AND = 0 is not a promise of visibility
> $C_0\;\text{AND}\;C_1=0000$ only says the shortcut *cannot reject yet*. The two endpoints may still be outside on *different* sides, so the segment can miss the window entirely. A later pass can reject it. Never report "visible" from the AND test — only "not yet rejected".

### 3.4 Clipping one boundary at a time

When neither shortcut applies, one outside endpoint is moved onto a boundary:

1. **Choose the endpoint.** Take the first endpoint whose code is nonzero; a code of `0000` is never clipped.
2. **Choose the plane.** Any set bit works and the answer is the same; the deck takes the **lowest set bit**, in the fixed order Left, Right, Bottom, Top, Near, Far.
3. **Solve for the intersection**, set that coordinate exactly to the boundary value.
4. **Recode** the new endpoint and **retest** from step 1.

The segment is parameterised once, $P(t)=P_0+t(P_1-P_0)$ with $0\le t\le 1$, and every clipped endpoint remains a point of the same line. The working interval therefore only ever shrinks: $[t_{start},t_{end}]\subseteq[0,1]$, with each pass moving one end inward. That is why the algorithm terminates — each pass strictly removes a piece of the segment.

### 3.5 The line-equation view

For 2D work the deck also clips with the line's Cartesian equation, which is often quicker by hand. From two points, get $y=mx+c$, then convert to general form $ax+by+c=0$; substituting a boundary value gives the other coordinate directly.

**Worked example 1 — $P(3,3)$, $Q(5,2)$.**

$$ m=\frac{2-3}{5-3}=-\frac{1}{2}, \qquad 3=-\frac{1}{2}(3)+c \Rightarrow c=\frac{9}{2} $$
$$ y=-\frac{1}{2}x+\frac{9}{2} \quad\Longleftrightarrow\quad \boxed{\,x+2y-9=0\,} $$

**Worked example 2 — $M(1,3)$, $N(5,2)$.**

$$ m=\frac{2-3}{5-1}=-\frac{1}{4}, \qquad 3=-\frac{1}{4}(1)+c \Rightarrow c=\frac{13}{4} $$
$$ y=-\frac{1}{4}x+\frac{13}{4} \quad\Longleftrightarrow\quad \boxed{\,x+4y-13=0\,} $$

With $x+2y-9=0$ and a left boundary $x=0$, the intersection is $y=9/2$; with a top boundary $y=6$ it is $x=9-12=-3$. The Cartesian form is convenient when the boundary is axis-aligned, which it always is in this algorithm.

### 3.6 The three-dimensional extension

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

### 3.7 Intersection formulas for all six planes

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

### 3.8 Worked example in 3D

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

### 3.9 The algorithm

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

### 3.10 Interactive dry run

> [!tip] How to use the widget
> `Next Step` advances one *pass* (one endpoint moved onto one plane). The left panel is the geometry; the right panel is the working state: both codes, the OR/AND decision, and the surviving $t$ interval. The $z$ coordinate is checked in the table, not drawn — the sketch is an $xy$ projection.

```js-engine
// Rendered by the JS Engine plugin: `container` is this block's output element.
container.innerHTML = `
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
`;
const $ = (id) => container.querySelector("#" + id);
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
  const stage = $("cs-stage");
  const say = $("cs-say");
  const tbody = container.querySelector("#cs-table tbody");
  const state = $("cs-state");
  const NS = "http://www.w3.org/2000/svg";
  const el = (n, a) => { const e = document.createElementNS(NS, n); for (const k in a) e.setAttribute(k, a[k]); return e; };

  const X = x => 40 + (x + 6) * (380 / 18);
  const Y = y => 320 - (y + 3) * (300 / 15);

  function draw(s) {
    stage.innerHTML = "";
    stage.appendChild(el("rect", { x: 0, y: 0, width: 460, height: 360, fill: "none" }));
    stage.appendChild(el("rect", { x: X(B.xmin), y: Y(B.ymax), width: X(B.xmax) - X(B.xmin), height: Y(B.ymin) - Y(B.ymax),
      fill: "rgba(47,158,68,0.10)", stroke: "var(--color-green,#2f9e44)", "stroke-width": 1.5 }));
    stage.appendChild(el("text", { x: X(B.xmin) + 3, y: Y(B.ymax) - 6, fill: "var(--color-green,#2f9e44)", "font-size": 11 })).textContent = "clip box (z checked in table)";
    stage.appendChild(el("line", { x1: X(A0[0]), y1: Y(A0[1]), x2: X(B0[0]), y2: Y(B0[1]),
      stroke: "var(--background-modifier-border,#adb5bd)", "stroke-width": 1.5, "stroke-dasharray": "5 4" }));
    stage.appendChild(el("line", { x1: X(s.P[0]), y1: Y(s.P[1]), x2: X(s.Q[0]), y2: Y(s.Q[1]),
      stroke: s.kind === "reject" ? "var(--color-red,#e03131)" : "var(--color-blue,#1971c2)", "stroke-width": 3 }));
    [[s.P, "P", "var(--color-blue,#1971c2)"], [s.Q, "Q", "var(--color-blue,#1971c2)"]].forEach(([p, lab, col]) => {
      stage.appendChild(el("circle", { cx: X(p[0]), cy: Y(p[1]), r: 4.5, fill: col }));
      const tx = el("text", { x: X(p[0]) + 7, y: Y(p[1]) - 7, fill: col, "font-size": 11 });
      tx.textContent = lab + bits(code(p));
      stage.appendChild(tx);
    });
    if (s.pt) {
      stage.appendChild(el("circle", { cx: X(s.pt[0]), cy: Y(s.pt[1]), r: 5, fill: "none", stroke: "var(--color-orange,#e8590c)", "stroke-width": 2 }));
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
  $("cs-next").onclick = () => { stop(); if (i < steps.length - 1) i++; paint(); };
  $("cs-reset").onclick = () => { stop(); i = 0; paint(); };
  $("cs-pause").onclick = stop;
  $("cs-play").onclick = () => {
    stop();
    timer = setInterval(() => { if (i < steps.length - 1) { i++; paint(); } else { stop(); } }, 1200);
  };
  paint();
})();
```

### 3.11 Exam pointer

> [!tip] Exam pointer — Cohen–Sutherland
> - Write the 4-bit table with its sign functions, and the 6-bit table with its mask values (`100000` … `000001`).
> - Justify both shortcuts in one sentence each; state that AND = 0 does not prove visibility.
> - Reproduce the 3D worked example end to end: codes, OR/AND, three passes, final segment $(0,4,2)$–$(4,6,6)$ at $t\in[1/3,2/3]$.
> - Explain why the denominator in $t$ is never zero, and why the intersection must be recoded.
> - State the worst-case pass count (one per boundary) and the cost per pass.

---

## 4. Polygon and 3D Fill-Area Clipping

*Deck: [[Post 4 - Polygon and 3D Fill-Area Clipping.pdf|Post 4 deck]] — 89 slides. Fill-area clipping, Sutherland–Hodgman with its four cases and full numeric trace, Weiler–Atherton boundary traversal, 3D point/face clipping, and the visibility problem that the next two topics solve.*

### 4.1 Polygons as ordered, closed vertex lists

A polygon enters the clipper as an **ordered list**, not a set:

$$ V=[v_1,v_2,\dots,v_n] $$

- Edges are $(v_1,v_2),(v_2,v_3),\dots,(v_{n-1},v_n)$ **and the closing edge** $(v_n,v_1)$.
- The closing edge is processed even though $v_1$ is not repeated at the end of the list.
- Clockwise or anticlockwise order is both valid, provided it is consistent.
- Square brackets emphasise that the order carries meaning: $[v_1,v_2,v_3]$ and $[v_2,v_3,v_1]$ are the same polygon (a cyclic rotation), but $[v_1,v_3,v_2]$ is the mirror traversal.
- The output must be a **closed, ordered boundary** too — that closure is exactly what clipping each edge independently cannot guarantee.

### 4.2 Why polygon clipping is not line clipping

> [!important] Why a separate algorithm is needed
> Clipping the four edges of a polygon as four independent segments produces a set of disjoint visible pieces, plus the parts of the window boundary that now form the outline of the visible region. Those boundary pieces belong to no original edge, so the result is **not a closed polygon**. Polygon clipping must therefore invent vertices and edges:
> - **new vertices** — edge/ boundary intersections, and sometimes window corners;
> - **new edges** — segments that run *along* the window boundary.

### 4.3 The window as four half-planes

A rectangular window is the intersection of four half-planes, so a polygon can be clipped by four independent half-plane passes. Each pass needs only one test:

| Clipper | Inside test | Outside test |
| --- | --- | --- |
| Left | $x\ge x_{\min}$ | $x<x_{\min}$ |
| Right | $x\le x_{\max}$ | $x>x_{\max}$ |
| Bottom | $y\ge y_{\min}$ | $y<y_{\min}$ |
| Top | $y\le y_{\max}$ | $y>y_{\max}$ |

### 4.4 The four edge cases

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

### 4.5 Computing the intersection

Parameterise the edge and solve for the crossing:

$$ P(t)=S+t(E-S),\qquad 0\le t\le 1 $$

| Clip boundary | Parameter | Other coordinate |
| --- | --- | --- |
| $x=b$ (left/right) | $t=(b-S_x)/(E_x-S_x)$ | $y=S_y+t(E_y-S_y)$ |
| $y=b$ (bottom/top) | $t=(b-S_y)/(E_y-S_y)$ | $x=S_x+t(E_x-S_x)$ |

- For an inside→outside transition the denominator is non-zero (the endpoints straddle the boundary).
- A crossing exactly at an endpoint gives $t=0$ or $t=1$: the point duplicates a vertex, so **merge duplicates** before emitting.
- Use a consistent endpoint order and consistent arithmetic to keep numerically coincident points identical; otherwise the output list contains hairline degenerate edges.

### 4.6 The procedure

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

### 4.7 Pictorial worked example

Take $V=[1,2,3]$ anticlockwise, with vertex 1 above the window, vertex 2 inside and vertex 3 to its right. Read inside/outside off the picture and track the list after every pass:

| Pass | Clipper | Inside | Outside | Result |
| --- | --- | --- | --- | --- |
| 1 | left $x\ge x_{\min}$ | 1,2,3 | none | $[2,3,1]$ — all edges In→In, the triangle is unchanged, the list is a cyclic rotation |
| 2 | right $x\le x_{\max}$ | 1,2 | 3 | $[2',3',1,2]$ — two new points; the new edge $2'\to3'$ runs along the right side |
| 3 | top $y\le y_{\max}$ | $2',3',2$ | 1 | $[3',3'',1',2,2']$ — $3''$ is a *second* crossing on the original edge $3\to1$, left of the corner |
| 4 | bottom $y\ge y_{\min}$ | all five | none | $[3'',1',2,2',3']$ — nothing changes but the starting vertex |

Five vertices survive: $2',3',3'',1'$ are new, and only vertex 2 comes from the original triangle.

### 4.8 Numerical trace

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

### 4.9 The limitation: a concave subject can split

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

![[CG - Concave Subject Split.png|460]]

*Figure — the concave-subject limitation: one clip boundary cuts the U-shape into two lobes, and Sutherland–Hodgman stores both in a single vertex list, producing a polygon whose boundary walks along the clip edge twice.*

That is **two disconnected pieces stored as one vertex list**. Rendered as a single polygon, the boundary walks from $4'$ to $6'$ along the clip edge and from $8'$ to $2'$ along it again — the degenerate connector is drawn twice. Sutherland–Hodgman is therefore correct only for **convex subjects** (or when the two pieces are allowed to be joined by a doubled edge).

### 4.10 Weiler–Atherton

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

### 4.11 Comparison

| Aspect | Sutherland–Hodgman | Weiler–Atherton |
| --- | --- | --- |
| Operation | successive half-plane passes | linked boundary traversal |
| Subject polygon | convex or concave | convex or concave |
| Output | one vertex list | one list per visible region |
| Bookkeeping | four inside/outside cases | crossings, entry/exit labels, links |
| Failure mode | concave subject ⇒ spurious connecting edges | tangencies and shared edges need special rules |

### 4.12 3D point clipping

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

### 4.13 Bounding boxes before exact clipping

A face may contain many vertices, and exact clipping examines every edge. Its **bounding box** uses only the coordinate extremes, so comparing boxes is far cheaper. The box test has three outcomes and one non-outcome:

| Object bounding box | Decision | Reason |
| --- | --- | --- |
| $x\in[1.2,2]$, $y,z\in[-0.5,0.5]$ | reject | $a_x=1.2>1$ |
| $x\in[0.5,1.5]$, same $y,z$ | continue | partial overlap: clip the faces |
| $x\in[1,2]$, same $y,z$ | continue | touches $x=1$; $a_x=1$ is **not** $>1$ |
| all intervals inside $[-1,1]$ | accept all | object lies in its box, box lies in the cube |

> [!warning] Overlap is not intersection
> Box overlap only says the boxes share points. The box also contains empty space, and a face may occupy none of the shared part. **Box overlap is inconclusive** — only exact face clipping answers it. Conversely, disjoint boxes *do* guarantee disjoint objects, so rejection is safe.

### 4.14 3D face clipping, worked

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

### 4.15 Clipping versus occlusion

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

### 4.16 Interactive dry run

> [!tip] How to use the widget
> The polygon $[(-1,0),(3,0),(1,3)]$ is clipped against $[0,2]^{2}$ in the book order left → right → top → bottom. Each step processes **one edge** and names its case. The right-hand column is the output list *growing*, which is the part that exam questions ask you to reproduce.

```js-engine
// Rendered by the JS Engine plugin: `container` is this block's output element.
container.innerHTML = `
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
`;
const $ = (id) => container.querySelector("#" + id);
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
    const st = $("sh-stage");
    st.innerHTML = "";
    st.appendChild(el("rect", { x: X(W.xmin), y: Y(W.ymax), width: X(W.xmax) - X(W.xmin), height: Y(W.ymin) - Y(W.ymax), fill: "rgba(47,158,68,0.10)", stroke: "var(--color-green,#2f9e44)", "stroke-width": 2 }));
    st.appendChild(el("text", { x: X(W.xmin) + 4, y: Y(W.ymax) - 6, "font-size": 11, fill: "var(--color-green,#2f9e44)" })).textContent = "window 0…2";
    if (s.input && s.input.length > 1) st.appendChild(poly(s.input.concat([s.input[0]]), { stroke: "var(--background-modifier-border,#adb5bd)", "stroke-width": 1.5, "stroke-dasharray": "4 4" }));
    if (s.out && s.out.length > 1) {
      st.appendChild(poly(s.out.concat([s.out[0]]), { stroke: "var(--color-blue,#1971c2)", "stroke-width": 2.5, fill: "rgba(25,113,194,0.16)" }));
      s.out.forEach(p => st.appendChild(el("circle", { cx: X(p[0]), cy: Y(p[1]), r: 3.5, fill: "var(--color-blue,#1971c2)" })));
    }
    if (s.S && s.E) {
      st.appendChild(el("line", { x1: X(s.S[0]), y1: Y(s.S[1]), x2: X(s.E[0]), y2: Y(s.E[1]), stroke: "var(--color-orange,#e8590c)", "stroke-width": 3 }));
      if (s.I) st.appendChild(el("circle", { cx: X(s.I[0]), cy: Y(s.I[1]), r: 5, fill: "none", stroke: "var(--color-orange,#e8590c)", "stroke-width": 2 }));
    }
    const ax = el("text", { x: 8, y: 318, "font-size": 10, fill: "var(--text-faint,#888)" });
    ax.textContent = "grey dashed = input polygon · orange = edge being processed · blue = output list so far";
    st.appendChild(ax);
  }
  function paint() {
    const s = steps[i];
    draw(s);
    $("sh-say").textContent = s.log;
    $("sh-pass").textContent = "Pass " + Math.min(s.pi + 1, 4) + " of 4 — " + s.ps.name;
    const o = $("sh-out");
    o.innerHTML = "<b>out list</b><br>" + (s.out.length ? s.out.map((p, k) => k + ": " + fmt(p)).join("<br>") : "<i>empty</i>");
    const keep = steps.slice(0, i + 1).filter(x => x.phase === "edge").slice(-4);
    $("sh-log").innerHTML = keep.map(x => "· " + x.log).join("<br>");
  }
  const stop = () => { if (timer) { clearInterval(timer); timer = null; } };
  $("sh-next").onclick = () => { stop(); if (i < steps.length - 1) i++; paint(); };
  $("sh-reset").onclick = () => { stop(); i = 0; paint(); };
  $("sh-pause").onclick = stop;
  $("sh-play").onclick = () => { stop(); timer = setInterval(() => { if (i < steps.length - 1) { i++; paint(); } else stop(); }, 900); };
  paint();
})();
```

### 4.17 Exam pointer

> [!tip] Exam pointer — polygon clipping
> - State why per-edge clipping fails (no closed boundary; needs new vertices *and* new edges).
> - Reproduce the four-case table and the intersection formulas; explain why outside–outside appends nothing.
> - Run the numeric trace for $(-1,0),(3,0),(1,3)$ to the six-vertex result, pass by pass.
> - Give the concave U failure with the list $[2',3,4,4',6',7,8,8']$ and say what it renders wrongly.
> - Contrast Weiler–Atherton: entry/exit labels, alternation, one contour per region.
> - Know the 3D point test, the three bounding-box outcomes, and that overlap is inconclusive.
> - Distinguish clipping from occlusion in one sentence, and give one object-space and one image-space advantage.

---

## 5. Hidden Surface Removal I — Back-Face Elimination and the Z-Buffer

*Deck: [[Post 5 - Hidden Surface Removal I - Back-Face Elimination and the Z-Buffer.pdf|Post 5 deck]] — 106 slides. The two first-line defences: throw away faces that point away from the eye, then resolve the rest pixel by pixel with a depth buffer.*

### 5.1 Back-face elimination

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

### 5.2 Worked example: a tetrahedron viewed along the negative z-axis

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

### 5.3 Why back-face elimination is not enough

Back-face elimination compares a face with **its own** solid only. It cannot answer:

- whether face $X$ of object 1 is hidden by face $Y$ of object 2 (inter-object occlusion);
- whether two front-facing faces overlap on screen and which is nearer;
- anything about an open surface (a single sheet has no "outside", so the sign is meaningless);
- anything about a concave solid, where one front-facing part can hide another front-facing part.

What survives culling still needs a depth comparison per pixel or per object. That is the job of the next two methods.

### 5.4 The depth (z) buffer: the idea

The z-buffer is an **image-space** method: two buffers of the same size as the screen, one storing the nearest depth found so far at each pixel, one storing the colour that produced it.

| Buffer | Symbol | Content | Initial value |
| --- | --- | --- | --- |
| Depth buffer | $DB[x][y]$ | depth of the nearest surface seen at pixel $(x,y)$ | $1$ (the far limit) |
| Frame buffer | $FB[x][y]$ | colour of that surface | background colour |

For every surface, and every pixel its projection covers, compute the surface's depth $z$ at that pixel and compare with the stored value:

$$ \text{if } z < DB[x][y] \text{ then } DB[x][y]=z,\; FB[x][y]=\text{colour of the surface} $$

Because the comparison is per pixel, the surfaces may be processed in **any order** — the result is identical, which is what makes the method hardware-friendly and immune to the cyclic-overlap problem that defeats the painter's algorithm (§6.2).

![[CG - Z Buffer.excalidraw]]

### 5.5 Depth from the plane equation

Every planar surface satisfies

$$ Ax+By+Cz+D=0 \quad\Longrightarrow\quad z=\frac{-D-Ax-By}{C},\qquad C\neq0 $$

so one division per *surface*, and then a linear expression per pixel. The constants come from the surface normal and one known point:

$$ \mathbf{N}=(A,B,C)=(P_2-P_1)\times(P_3-P_1),\qquad D=-Ax_1-By_1-Cz_1 $$

> [!important] Deriving the plane of a surface — the three steps
> 1. **Two vectors in the plane:** $\mathbf{u}=P_2-P_1$, $\mathbf{v}=P_3-P_1$.
> 2. **Normal by cross product:** $\mathbf{N}=\mathbf{u}\times\mathbf{v}=(A,B,C)$.
> 3. **Form the equation:** substitute $\mathbf{N}$ and any one vertex into $Ax+By+Cz+D=0$ and solve for $D$.

### 5.6 Incremental depth: never evaluate the plane twice

Evaluating $z=(-D-Ax-By)/C$ at every pixel costs a multiply and a divide per pixel. Because $z$ is linear in $x$ and $y$, each step across a scan line changes $z$ by a **constant**:

$$ z(x+1,y)=z(x,y)-\frac{A}{C} \qquad\text{(one pixel right)} $$
$$ z(x,y-1)=z(x,y)+\frac{B}{C} \qquad\text{(one scan line down)} $$
$$ z(x+1,y-1)=z(x,y)-\frac{A}{C}+\frac{B}{C} \qquad\text{(right and down in one step)} $$

> [!note] Where the constants come from
> Write $z=(-D-Ax-By)/C$. Increasing $x$ by 1 subtracts $A/C$; decreasing $y$ by 1 adds $B/C$. Both are independent of position, so they are computed **once per surface** and then only added. No divide appears inside the pixel loop.

**Edge pixels.** When the next scan line is reached, the leftmost covered pixel moves in $x$ as well. For an edge of slope $m$, the new $x$-coordinate is

$$ x' = x-\frac{1}{m} $$

so the depth at the first pixel of the new scan line is the old depth plus the one-line drop ($+B/C$) plus one step of $-A/C$ for every unit the edge moved in $x$:

$$ z' = z + \frac{B}{C} - \frac{A}{C}\,(x'-x) = z + \frac{B}{C} + \frac{A}{mC} $$

The two terms account, respectively, for the change of $y$ between the scan lines and the change of $x$ along the edge. This is **scan-line coherence**: neighbouring pixels on a surface have neighbouring depths, so the buffer is filled by addition.

**Worked numeric check.** Take a surface with $A=2$, $B=1$, $C=2$, $D=-10$, i.e. $z=(10-2x-y)/2$.

- At pixel $(1,2)$: $z=(10-2-2)/2=3.0$.
- One pixel right, $(2,2)$: $z=3.0-A/C=3.0-1.0=2.0$; direct check gives $(10-4-2)/2=2.0$ ✓.
- One scan line down, $(1,1)$: $z=3.0+B/C=3.5$; direct check gives $(10-2-1)/2=3.5$ ✓.
- Right and down, $(2,1)$: $z=3.0-1.0+0.5=2.5$; direct check gives $(10-4-1)/2=2.5$ ✓.
- Next scan line from the edge, $m=2$: the leftmost pixel moves to $x'=1-\tfrac12=0.5$ and $z'=3.0+0.5+2/(2\cdot2)=4.0$; direct check gives $(10-1-1)/2=4.0$ ✓ — the edge term is not optional.

### 5.7 The algorithm

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
> 9:         z_left = z_left + B/C - (A/C)(x'_left - x_left)   # next line, x'_left = x_left - 1/m
> 10: end for
> ```
> **Cost.** $O(nN)$ for $n$ surfaces overlapping $N$ pixels in total — one comparison per covered pixel, no sorting, no pairwise surface tests.

The deck's simplified form states the same loop with the buffers named $DV[\;][\;]$ and the depth written per scan line:

> [!important] Iterative depth calculation
> - Initialise $x$ to the leftmost pixel of the surface, $y$ to its top scan line, and $z$ to the depth at that leftmost edge point.
> - Set the constants $\Delta z_x=-A/C$ (change along the scan line) and $\Delta z_y=B/C$ (change between scan lines).
> - For each pixel across the scan line: store $z$ in $DV[x][y]$, then $z\mathrel{+}=\Delta z_x$.
> - At the end of a scan line: move the edge by $-1/m$ in $x$, add $\Delta z_y=B/C$ for the drop to the next line, and add $\Delta z_x$ once per unit the edge moved.

> [!warning] The three classic z-buffer errors
> - **Wrong depth direction.** If depth grows *inward*, the test is $z<DB$, and initialisation is the far value. Flip the convention without flipping the test and the farthest surface wins.
> - **Divide by zero.** $C=0$ means a surface parallel to the view plane's depth axis — the plane equation must be solved for $z$ from a different coefficient, or the surface rejected.
> - **Depth precision.** $z$ is interpolated after the perspective divide, so its spacing in screen space is non-linear; a small far plane range and a deep scene still collide in the buffer (z-fighting).

### 5.8 Interactive dry run

> [!tip] How to use the widget
> Two triangles are scan-converted in order, first the near one, then the far one. Each step is one covered pixel of one surface: the widget compares the new $z$ against $DB$ and shows the outcome. Watch the near surface win the overlap region, and watch the far one still paint the pixels the near one never covered. The depths here are in an arbitrary unit, so the buffer is initialised to $\infty$ — the same "far value" as the algorithm box's $1$, since every real depth is nearer than it.

```js-engine
// Rendered by the JS Engine plugin: `container` is this block's output element.
container.innerHTML = `
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
`;
const $ = (id) => container.querySelector("#" + id);
(() => {
  const COLS = 10, ROWS = 8, CELL = 28;
  const triA = { pts: [[1, 1], [9, 2], [5, 7]], plane: (x, y) => 2 + 0.05 * x + 0.03 * y, colour: "var(--color-blue,#1971c2)", name: "A" };
  const triB = { pts: [[0, 5], [7, 7], [9, 0]], plane: (x, y) => 5 + 0.05 * x + 0.03 * y, colour: "var(--color-orange,#e8590c)", name: "B" };
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
  const FAR = 99;
  const init = () => { db = Array.from({ length: ROWS }, () => Array(COLS).fill(FAR)); fb = Array.from({ length: ROWS }, () => Array(COLS).fill("")); cur = -1; };
  const NS = "http://www.w3.org/2000/svg";
  const el = (n, a) => { const e = document.createElementNS(NS, n); for (const k in a) e.setAttribute(k, a[k]); return e; };
  const tc = v => v >= FAR ? "∞" : v.toFixed(2);

  function paint() {
    const s = cur >= 0 ? steps[cur] : null;
    const fbSvg = $("zb-fb"), dbSvg = $("zb-db");
    fbSvg.innerHTML = ""; dbSvg.innerHTML = "";
    for (let y = 0; y < ROWS; y++) for (let x = 0; x < COLS; x++) {
      const bg = fb[y][x] || "none";
      fbSvg.appendChild(el("rect", { x: x * CELL, y: y * CELL, width: CELL, height: CELL, fill: bg, stroke: "var(--background-modifier-border,#ced4da)", "stroke-width": 0.8 }));
      const d = el("text", { x: x * CELL + CELL / 2, y: y * CELL + CELL / 2 + 4, "font-size": 9, "text-anchor": "middle", fill: "var(--text-normal,#333)" });
      d.textContent = tc(db[y][x]);
      dbSvg.appendChild(el("rect", { x: x * CELL, y: y * CELL, width: CELL, height: CELL, fill: "none", stroke: "var(--background-modifier-border,#ced4da)", "stroke-width": 0.8 }));
      dbSvg.appendChild(d);
    }
    if (s) {
      fbSvg.appendChild(el("rect", { x: s.x * CELL + 1, y: s.y * CELL + 1, width: CELL - 2, height: CELL - 2, fill: "none", stroke: "var(--color-green,#2f9e44)", "stroke-width": 2.5 }));
      dbSvg.appendChild(el("rect", { x: s.x * CELL + 1, y: s.y * CELL + 1, width: CELL - 2, height: CELL - 2, fill: "none", stroke: "var(--color-green,#2f9e44)", "stroke-width": 2.5 }));
    }
    if (!s) { $("zb-say").textContent = "Ready. Depth buffer = ∞ everywhere; frame buffer empty."; return; }
    $("zb-say").textContent =
      "Surface " + s.t.name + " at pixel (" + s.x + ", " + s.y + "): z = " + s.z.toFixed(2) +
      " · stored DB = " + tc(s.before) + " → " + (s.win ? "z < DB: write depth and colour" : "z ≥ DB: reject, nearer surface stays");
  }
  function step() {
    if (cur >= steps.length - 1) { if (timer) { clearInterval(timer); timer = null; } return; }
    cur++;
    const s = steps[cur];
    s.before = db[s.y][s.x];
    s.win = s.z < s.before;
    if (s.win) { db[s.y][s.x] = s.z; fb[s.y][s.x] = s.t.colour; }
    paint();
  }
  $("zb-next").onclick = () => { if (timer) { clearInterval(timer); timer = null; } step(); };
  $("zb-reset").onclick = () => { if (timer) { clearInterval(timer); timer = null; } init(); paint(); };
  $("zb-pause").onclick = () => { if (timer) { clearInterval(timer); timer = null; } };
  $("zb-play").onclick = () => { if (timer) clearInterval(timer); timer = setInterval(step, 240); };
  init(); paint();
})();
```

### 5.9 Exam pointer

> [!tip] Exam pointer — back-face and z-buffer
> - Compute $\mathbf{N}=(B-A)\times(C-A)$ and classify by the sign of $\mathbf{N}\cdot\mathbf{v}$; know that $\mathbf{N}\cdot\mathbf{v}=-N_z$ for $\mathbf{v}=(0,0,-1)$.
> - Reproduce the tetrahedron table with all four normals, and the two checks (opposite-vertex dot product, normals summing to zero).
> - Say precisely what back-face elimination cannot do (inter-object, concave, open surfaces).
> - Write $z=(-D-Ax-By)/C$, then $\Delta z_x=-A/C$ and $\Delta z_y=+B/C$; derive both from the plane equation.
> - State the cost $O(nN)$, the arbitrary processing order, and the three failure modes (depth direction, $C=0$, precision).

---

## 6. Hidden Surface Removal II — Painter's Algorithm and BSP Trees

*Deck: [[Post 6 - Hidden Surface Removal II - Painter's Algorithm and BSP Trees.pdf|Post 6 deck]] — 80 slides. Compiles the depth-sort (painter's) algorithm, the cyclic overlap that breaks it, the plane function $f(\mathbf{r})$, and the BSP tree that replaces a per-frame sort with a precomputed partition.*

### 6.1 Painting back to front

The painter's algorithm is the oldest hidden-surface method and the one that matches intuition: an artist paints the distant hills first and the near tree last, and the tree simply covers part of the hills. Nothing is tested per pixel — **the drawing order itself is the visibility computation**. If every polygon is painted in order of *decreasing* distance from the eye, each new polygon overwrites only what should be hidden behind it, and the final frame buffer holds the visible surface of every pixel.

The whole method therefore reduces to one question: *can the polygons be put in a total order by depth?* The naive answer — sort by the $z$ of the centroid, or by the farthest vertex — is a heuristic, not a proof, and the deck spends most of its slides on the cases where the heuristic has no correct answer.

> [!important] Depth-sort (painter's) — statement
> ```text
> 1: compute a depth key for every polygon   (e.g. smallest z, or centroid z)
> 2: sort the polygons by decreasing depth   (farthest first)
> 3: for each adjacent pair (P, Q) in that order, apply the four tests
> 4:     if a test succeeds, the order P then Q is correct — keep it
> 5:     if all four fail, swap P and Q and re-test (at most n times)
> 6:     if the swap returns to the starting order, a cycle exists
> 7:         split one polygon by the other's plane, and restart
> 8: paint the resulting list from farthest to nearest
> ```
>
> **Input:** a set of polygons with their planes and a viewpoint.
> **Output:** a paint order, or a split polygon set that admits one.
> **Cost:** $O(n\log n)$ for the sort, plus the pairwise tests in the worst case $O(n^2)$; the whole cost is paid **again for every new viewpoint**.

> [!note] Why painting works at all
> The frame buffer is destructive: writing a pixel replaces what was there. That is normally a bug, but here it is the mechanism. Because a nearer surface is guaranteed to be painted later, "last write wins" *is* the depth test — at the price of painting the hidden surfaces first and then covering them up. The overdraw is the cost of never storing a depth per pixel.

### 6.2 The four tests that decide a pair

Sorting produces a candidate order; the tests certify that a *particular adjacent pair* $P$ (farther) and $Q$ (nearer) is safe. They go from cheapest and most decisive to most expensive.

| # | Test | If it succeeds | Cost |
| --- | --- | --- | --- |
| 1 | the $x$-extents of $P$ and $Q$ do not overlap | the pair cannot hide each other; order is free | $O(1)$ |
| 2 | the $y$-extents of $P$ and $Q$ do not overlap | same — disjoint in screen space | $O(1)$ |
| 3 | every vertex of $P$ lies behind the plane of $Q$ | $P$ is wholly farther, so $P$ then $Q$ is correct | $O(v_P)$ |
| 4 | every vertex of $Q$ lies in front of the plane of $P$ | again $P$ then $Q$ is correct | $O(v_Q)$ |
| — | all four fail | swap and retest; a persistent cycle means **split** | $O(n)$ retests |

The deck's slides are titled **"Step 4 passes"** and **"Step 4 fails"**: the first shows a configuration where the plane test certifies the order, the second the configuration where it cannot, and the caption on the failing slide is the sentence to remember —

> *Cyclic overlap makes each polygon hide another, so no single drawing order works.*

Test 4 is the load-bearing one because tests 1–2 only prove *irrelevance*: two polygons whose screen rectangles are disjoint can be painted in any order. Tests 3–4 are the only ones that prove an *order*, and they are exactly the tests that a cycle defeats.

> [!warning] "Sort by depth" is not "sort by centroid z"
> A single scalar key cannot represent a polygon that spans a range of depths. A long ground plane whose centroid is far away can still pass in front of a small nearby object, and a polygon seen almost edge-on has a centroid that says nothing about where its surface is. The four tests exist because **no scalar key is a valid sort for arbitrary polygons** — when they all fail, the geometry, not the key, must be cut.

### 6.3 The failure cases

| Case | What goes wrong | Cure |
| --- | --- | --- |
| **Cyclic overlap** (the deck's headline) | $P_1$ hides $P_2$, $P_2$ hides $P_3$, $P_3$ hides $P_1$ — a cycle in the "must be painted after" relation | split one polygon of the cycle |
| **Intersecting polygons** | neither is wholly in front of the other; the correct order changes across the line of intersection | split along the intersection |
| **Polygon straddling the eye plane** | parts of it are behind the eye; depth keys become meaningless or infinite | clip against the near plane first |
| **Coincident / tied surfaces** | equal keys, order undefined, flicker between frames | nudge, or use a depth buffer |
| **Many small vs one huge polygon** | a huge polygon's key is a poor summary of its extent | split the huge polygon |

Cyclic overlap is worth a picture in words because it is easy to draw and easy to state in an exam. Take three long thin triangles lying nearly in the same plane, arranged like the three blades of a pinwheel, each overlapping the next and being overlapped by the previous one. Looked at from the common side:

- along the first overlap, $P_1$ is nearer than $P_2$;
- along the second, $P_2$ is nearer than $P_3$;
- along the third, $P_3$ is nearer than $P_1$.

Three pairwise truths, no global order. The relation "nearer than" is not transitive here, so no sorting algorithm can succeed; the only escape is to **cut one polygon** so that the cycle becomes a chain.

### 6.4 The plane function

Everything that follows — building the tree, splitting a polygon, choosing the traversal — uses one scalar function.

$$ f(\mathbf{r}) = (\mathbf{r} - \mathbf{p}) \cdot \mathbf{n} $$

where $\mathbf{p}$ is any point on the dividing plane and $\mathbf{n}$ its normal. With $\lVert \mathbf{n}\rVert = 1$, $f(\mathbf{r})$ is the **signed perpendicular distance** from the plane to $\mathbf{r}$; with an unnormalised $\mathbf{n}$ it is that distance scaled by $\lVert \mathbf{n} \rVert$, which is harmless because only the *sign* is used.

| Value | Meaning | Deck's label |
| --- | --- | --- |
| $f(\mathbf{r}) > 0$ | on the side the normal points to | **OUT** |
| $f(\mathbf{r}) = 0$ | on the plane | boundary — the deck's ties count as inside |
| $f(\mathbf{r}) < 0$ | on the opposite side | **IN** |

The deck's convention is fixed by the sentence: *the arrow $\mathbf{n}_i$ points toward OUT*. So a polygon entirely on the normal side of the dividing plane goes to the OUT subtree, one entirely on the other side goes to IN, and one with **vertices of both signs** crosses the plane and must be split. The same function, evaluated at the eye instead of at a vertex, tells the renderer which side the viewer is on — and that single bit decides the traversal order.

> [!note] The same test builds and traverses
> > *"The same test builds and traverses the BSP tree."*
>
> Building asks $f(\text{vertex})$ for every polygon vertex; rendering asks $f(\text{eye})$ once per node. The build answer is fixed forever; the render answer changes with the camera. This is the whole economy of a BSP tree: the expensive geometric work (classification and splitting) is done once, and each new frame costs only one dot product per node.

### 6.5 Building the tree

> [!important] BSP construction — statement
> ```text
> 1: BUILD(list S)
> 2:     if S is empty: return an empty leaf
> 3:     choose a polygon p from S            (the root of this subtree)
> 4:     node  ← p, node.plane ← plane of p
> 5:     IN ← {}, OUT ← {}
> 6:     for every other polygon q in S:
> 7:         classify every vertex v of q by sign of f_p(v) = (v − p) · n
> 8:         if all signs < 0:  put q in IN
> 9:         else if all signs > 0: put q in OUT
> 10:        else: split q at the plane into q_IN and q_OUT, put both
> 11:    node.IN  ← BUILD(IN)
> 12:    node.OUT ← BUILD(OUT)
> 13:    return node
> ```
>
> **Invariant:** at every node, all polygons in the IN subtree lie on the non-normal side of that node's plane, and all polygons in the OUT subtree lie on the normal side. The node's own polygon lies in the plane itself.
> **Cost:** one plane test per polygon per level — $O(n\log n)$ for a balanced tree, $O(n^2)$ if the splits degenerate into a chain, and every split adds a polygon, so the output can be larger than the input.

The deck builds the tree in exactly this order and stops at three checkpoints, which are worth reproducing because each one shows a different feature of the build.

**First partition — polygon 1 becomes the root.** Extend the plane of polygon 1, classify the remaining polygons by side, and recurse. With the deck's geometry:

| Node | IN subtree | OUT subtree |
| --- | --- | --- |
| 1 | 2, 3, 4 | 5, 6, 7, 8, 9, 10, 11 |

**The prompt "nodes considering 5?"** — the OUT subtree of 1 still needs a root, and the deck picks polygon 5. Its plane cuts the set into:

| Node | IN subtree | OUT subtree |
| --- | --- | --- |
| 5 | 6, 7, 9a, 10, 11 | 8, 9b |

**The prompt "nodes considering 3, 6, 8?"** — the remaining subtrees each get a root: 3 for the IN branch of 2, 6 for the IN branch of 5, 8 for the OUT branch of 5. Continuing the same rule to the leaves produces the tree the deck draws:

```text
                  1
          2               5
      3               6       8
          4       7       9b
                      9a
                          10
                              11
```

Read the shape, not the x-positions: **2 and 3 are chains of single-child nodes**, because after removing polygon 1 and polygon 5's partition, those subtrees contained only polygons that all lay on one side. A BSP tree is not balanced and is not a search tree — its shape is whatever the chosen splitting planes produce.

### 6.6 Splitting a polygon: cutting 9 into 9a and 9b

The deck's split is the one place where a polygon is created rather than merely classified. Polygon 9 straddles the plane of polygon 5, so one copy of 9 goes to each side under new names:

> *"The plane of polygon 5 cuts polygon 9 into two pieces. Different signs at the endpoints mean that polygon 9 crosses the plane. Split at $s$, where $f_5(s) = 0$. Place each piece in its corresponding subtree."*

The split is a one-dimensional root find along an edge. For an edge from $\mathbf{u}$ to $\mathbf{v}$ with $f(\mathbf{u})$ and $f(\mathbf{v})$ of opposite signs, write $\mathbf{s} = \mathbf{u} + t(\mathbf{v} - \mathbf{u})$ and solve $f(\mathbf{s}) = 0$:

$$ f(\mathbf{u}) + t\big(f(\mathbf{v}) - f(\mathbf{u})\big) = 0
\quad\Longrightarrow\quad
\boxed{\ t = \frac{f(\mathbf{u})}{f(\mathbf{u}) - f(\mathbf{v})}\ } $$

Because the signs differ, the denominator cannot vanish, and $t \in (0,1)$ — the crossing is strictly inside the edge. The new vertex $\mathbf{s}$ is inserted into both copies of the polygon; the vertices before the crossing go to one piece, those after to the other, and each piece is closed along the cut.

#### The split parameter in numbers

Take an edge with $f(\mathbf{u}) = -2$ and $f(\mathbf{v}) = +6$. Then $t = (-2)/((-2) - 6) = 1/4$, so the crossing sits a quarter of the way from $\mathbf{u}$ to $\mathbf{v}$; check: $f$ at that point is $-2 + \tfrac14(8) = 0$. This is the same interpolation the clipper uses in §4.5, applied to a signed plane function instead of to a coordinate — the arithmetic is identical, only the quantity being interpolated changes.

> [!warning] Splitting is not free
> Each split adds vertices and polygons, so a scene built from many mutually crossing polygons can grow substantially, and the tree's memory is proportional to the *split* polygon count, not the input count. The deck's example happens to split exactly one polygon; in the worst case every polygon crosses every plane it meets.

### 6.7 Rendering: the eye selects the traversal order

> [!important] BSP rendering — statement
> ```text
> 1: RENDER(node, eye)
> 2:     if node is empty: return
> 3:     s ← f_node(eye) = (eye − p_node) · n_node
> 4:     if s > 0:                       // eye on the OUT side
> 5:         RENDER(node.IN, eye)        // far subtree first
> 6:         draw node.polygon
> 7:         RENDER(node.OUT, eye)       // near subtree last
> 8:     else:                           // eye on the IN side
> 9:         RENDER(node.OUT, eye)       // far subtree first
> 10:        draw node.polygon
> 11:        RENDER(node.IN, eye)        // near subtree last
> ```
>
> **Invariant:** at the moment a node's polygon is drawn, everything behind it has already been painted and everything in front of it is still to come — which is precisely the painter's order.
> **Cost:** $O(n)$ per frame, one dot product and two recursive calls per node, **no sorting and no per-pixel test**.

| Eye side | Local order | Why it is the painter's order |
| --- | --- | --- |
| **OUT** ($f > 0$) | IN subtree → node → OUT subtree | the whole IN side is on the far side of the plane |
| **IN** ($f < 0$) | OUT subtree → node → IN subtree | the whole OUT side is on the far side of the plane |

> [!important] Why the rule is correct
> The node's plane divides space into two half-spaces, and every polygon in the IN subtree lies entirely in one of them while every polygon in the OUT subtree lies entirely in the other. A viewer standing on the OUT side sees the plane's IN half-space *through* the plane: everything there is farther away than the plane itself. So the far subtree must be painted first, then the plane's own polygon, then the near subtree. The recursion applies the same argument at every level, which is why a single eye test per node is enough.

![[CG - BSP Tree Traversal.excalidraw]]

The deck's own eye is on the OUT side of plane 1 and supplies a per-node table. *The eye stays fixed; each node supplies a different plane*, so each row can differ:

| Node | Eye side | Local traversal |
| --- | --- | --- |
| 1 | OUT | IN → 1 → OUT |
| 2 | IN | OUT → 2 → IN |
| 3 | OUT | IN → 3 → OUT |
| 5 | IN | OUT → 5 → IN |
| 8 | IN | OUT → 8 → IN |
| 6 | IN | OUT → 6 → IN |
| 7 | OUT | IN → 7 → OUT |
| 9a | IN | OUT → 9a → IN |
| 10 | IN | OUT → 10 → IN |
| 4, 9b, 11 | leaves | draw directly |

The row that always causes trouble in the deck is **node 7**: the eye is *below* its plane, i.e. on the IN side, because polygon 7's normal points downward. The traversal order at a node is a property of that node's own orientation, not of the tree's drawing on the page.

### 6.8 The complete trace

Walking the recursion with the eye fixed gives the deck's annotated trace (slides 1/8 → 8/8). The pending nodes form a call stack; a node is drawn only when its far subtree has returned.

| Step | At node | Eye side | Action | Drawn so far |
| --- | --- | --- | --- | --- |
| 1 | 1 | OUT | enter; visit the IN subtree rooted at 2 before drawing 1 | — |
| 2 | 2 | IN | OUT empty → draw 2 → visit 3 | 2 |
| 3 | 3 | OUT | IN empty → draw 3 → visit leaf 4 | 2, 3 |
| 4 | 4 | leaf | draw 4; subtree of 2 complete → draw 1 | 2, 3, 4, 1 |
| 5 | 5 | IN | visit the OUT subtree rooted at 8 first | 2, 3, 4, 1 |
| 6 | 8 | IN | OUT empty → draw 8 → visit leaf 9b | 2, 3, 4, 1, 8, 9b |
| 7 | 5 | IN | OUT subtree done → draw 5 → visit 6 | …, 5 |
| 8 | 6 | IN | OUT empty → draw 6 → visit 7 | …, 6 |
| 9 | 7 | OUT | IN empty → draw 7 → visit 9a | …, 7 |
| 10 | 9a | IN | OUT empty → draw 9a → visit 10 | …, 9a |
| 11 | 10 | IN | OUT empty → draw 10 → visit 11 | …, 10 |
| 12 | 11 | leaf | draw 11; every pending visit is complete | 2, 3, 4, 1, 8, 9b, 5, 6, 7, 9a, 10, 11 |

$$ \text{draw order} = 2,\ 3,\ 4,\ 1,\ 8,\ 9b,\ 5,\ 6,\ 7,\ 9a,\ 10,\ 11 $$

![[CG - BSP Traversal Order.png|480]]

*Figure — the deck's annotated traversal: the tree with each node's eye side marked and the polygons numbered in the order they are painted, ending at $2,3,4,1,8,9b,5,6,7,9a,10,11$.*

Two observations that make the order memorable:

- **1 is drawn fourth, not first.** Entering the root does not mean drawing it — the whole IN subtree must be finished first, and that subtree is where the near polygons 2, 3, 4 live.
- **5 is drawn after 8 and 9b but before 6, 7, 9a, 10, 11.** The eye is on 5's IN side, so its OUT side (8, 9b) is far and goes first, and its IN side (6, 7, 9a, 10, 11) is near and goes last.

### 6.9 Why a BSP tree is worth the build

| Property | Painter's with sort | BSP tree |
| --- | --- | --- |
| Work per frame | $O(n\log n)$ sort + pairwise tests + overdraw | $O(n)$ traversal, no sort |
| Reuse across viewpoints | none — the order is recomputed | the partition is fixed; only the eye tests change |
| Correctness with cyclic overlap | fails | succeeds, because splitting removed the cycles |
| Geometry cost | none | splits add polygons; build is $O(n\log n)$ to $O(n^2)$ |
| Static scenes | fine | ideal (walls, rooms, terrain) |
| Degenerate/coincident planes | fragile | fragile — choose splitting planes carefully |

> [!note] Where the depth ordering went
> Notice that no z-buffer is involved and no pixel is ever compared. The BSP tree *precomputes* the visibility order for **all** viewpoints at once, because the order only depends on which side of each plane the eye happens to be — a finite amount of information. That is why a BSP renderer is cheap per frame and why the structure must be rebuilt whenever the geometry moves.

> [!warning] The classic BSP pitfalls
> - A **badly chosen splitting plane** (a polygon that crosses many others) causes a split explosion; heuristics pick the plane that minimises splits and balances the tree.
> - Polygons lying **in the same plane** must be handled as a special case, or they end up in both subtrees and are drawn twice (harmless with opaque paint, wrong with transparency).
> - BSP gives a **per-polygon** order; polygons that interpenetrate after the build (moving objects) invalidate it.

### 6.10 Interactive dry run

The widget below walks the deck's twelve-step trace on the deck's tree. Watch the *draw order* strip grow: it should end at `2 3 4 1 8 9b 5 6 7 9a 10 11`, and the panel shows each node's eye test as it is evaluated.

```js-engine
// Rendered by the JS Engine plugin: `container` is this block's output element.
container.innerHTML = `
<div id="w-bsp" style="border:1px solid var(--background-modifier-border,#ccc);border-radius:10px;padding:12px;background:var(--background-primary,#fff);color:var(--text-normal,#222);font:14px/1.45 var(--font-interface,system-ui)">
  <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px">
    <button id="bsp-play">▶ Play</button>
    <button id="bsp-pause">⏸ Pause</button>
    <button id="bsp-next">⏭ Next Step</button>
    <button id="bsp-reset">↺ Reset</button>
  </div>
  <div id="bsp-say" style="min-height:44px;color:var(--text-muted,#555);margin-bottom:8px">Ready · the eye is fixed, the tree is built · press Next Step</div>
  <svg id="bsp-stage" viewBox="0 0 760 400" style="width:100%;height:auto;display:block"></svg>
  <div style="margin-top:8px;font-size:13px;color:var(--text-muted,#555)">Painted so far</div>
  <div id="bsp-order" style="display:flex;gap:6px;flex-wrap:wrap;min-height:26px;margin-top:4px"></div>
  <div id="bsp-legend" style="margin-top:8px;font-size:13px;color:var(--text-faint,#777)">
    green = painted · accent = current node · grey = not yet visited · IN / OUT is the eye's side of that node's plane
  </div>
</div>
`;
const $ = (id) => container.querySelector("#" + id);
(() => {
  const NODES = {
    "1":  { x: 380, y: 40,  side: "OUT", kids: ["2", "5"] },
    "2":  { x: 180, y: 110, side: "IN",  kids: ["3", ""] },
    "3":  { x: 110, y: 185, side: "OUT", kids: ["", "4"] },
    "4":  { x: 250, y: 185, side: "",    kids: [] },
    "5":  { x: 560, y: 110, side: "IN",  kids: ["6", "8"] },
    "6":  { x: 480, y: 185, side: "IN",  kids: ["7", ""] },
    "7":  { x: 420, y: 255, side: "OUT", kids: ["", "9a"] },
    "8":  { x: 650, y: 185, side: "IN",  kids: ["9b", ""] },
    "9a": { x: 520, y: 255, side: "IN",  kids: ["10", ""] },
    "9b": { x: 700, y: 255, side: "",    kids: [] },
    "10": { x: 560, y: 320, side: "IN",  kids: ["11", ""] },
    "11": { x: 600, y: 380, side: "",    kids: [] }
  };
  const EDGES = [["1","2"],["1","5"],["2","3"],["3","4"],["5","6"],["5","8"],
                 ["6","7"],["7","9a"],["8","9b"],["9a","10"],["10","11"]];
  const STEPS = [
    { n: "1",  d: [],        s: "Node 1: the eye is OUT (f₁(e) > 0), so the order is IN → 1 → OUT. Descend into the IN subtree at 2; polygon 1 waits." },
    { n: "2",  d: ["2"],     s: "Node 2: eye IN → OUT → 2 → IN. Its OUT child is empty, so draw 2 now and descend to 3." },
    { n: "3",  d: ["3"],     s: "Node 3: eye OUT → IN → 3 → OUT. Its IN child is empty, so draw 3 and descend to leaf 4." },
    { n: "4",  d: ["4","1"], s: "Leaf 4 draws directly. Subtree of 2 is complete, so the waiting polygon 1 is drawn — fourth, not first." },
    { n: "5",  d: [],        s: "Node 5: eye IN → OUT → 5 → IN. Its OUT subtree (rooted at 8) is farther, so visit it before drawing 5." },
    { n: "8",  d: ["8","9b"],s: "Node 8: eye IN, OUT child empty. Draw 8, then its IN leaf 9b. Subtree of 8 is complete." },
    { n: "5",  d: ["5"],     s: "Back at 5 with its OUT side done: draw 5, then descend into its IN subtree at 6." },
    { n: "6",  d: ["6"],     s: "Node 6: eye IN, OUT child empty. Draw 6, then its IN child 7." },
    { n: "7",  d: ["7"],     s: "Node 7: the normal points down, the eye is below the plane → eye OUT → IN → 7 → OUT. IN empty: draw 7, descend to 9a." },
    { n: "9a", d: ["9a"],    s: "Node 9a: eye IN, OUT child empty. Draw 9a, then its IN child 10." },
    { n: "10", d: ["10"],    s: "Node 10: eye IN, OUT child empty. Draw 10, then leaf 11." },
    { n: "11", d: ["11"],    s: "Leaf 11 draws. Every pending subtree has returned: the frame is complete." }
  ];
  const NS = "http://www.w3.org/2000/svg";
  const svg = $("bsp-stage");
  const say = $("bsp-say");
  const orderBox = $("bsp-order");
  const el = (t, a) => { const e = document.createElementNS(NS, t); for (const k in a) e.setAttribute(k, a[k]); return e; };
  const refs = {};
  let cur = -1, timer = null, drawn = [];

  EDGES.forEach(([a, b]) => {
    const A = NODES[a], B = NODES[b];
    svg.appendChild(el("line", { x1: A.x, y1: A.y, x2: B.x, y2: B.y, stroke: "var(--background-modifier-border,#adb5bd)", "stroke-width": 2 }));
  });
  Object.keys(NODES).forEach(id => {
    const n = NODES[id];
    const g = el("g", {});
    const c = el("circle", { cx: n.x, cy: n.y, r: 15, "stroke-width": 2 });
    const t = el("text", { x: n.x, y: n.y + 5, "text-anchor": "middle", "font-size": 13, "font-family": "var(--font-interface,system-ui)", "font-weight": 600 });
    t.textContent = id;
    const tag = el("text", { x: n.x, y: n.y - 22, "text-anchor": "middle", "font-size": 10, "font-family": "var(--font-interface,system-ui)" });
    tag.textContent = n.side;
    g.appendChild(c); g.appendChild(t); g.appendChild(tag);
    svg.appendChild(g);
    refs[id] = { c, t, tag };
  });
  const note = el("text", { x: 20, y: 30, "font-size": 12, "font-family": "var(--font-interface,system-ui)" });
  note.textContent = "BSP tree (left = IN, right = OUT)";
  note.setAttribute("fill", "var(--text-faint,#777)");
  svg.appendChild(note);

  function paint() {
    Object.keys(refs).forEach(id => {
      const r = refs[id];
      const isCur = cur >= 0 && STEPS[cur].n === id;
      const done = drawn.indexOf(id) >= 0;
      r.c.style.fill = isCur ? "var(--interactive-accent,#4c6ef5)" : (done ? "var(--color-green,#2f9e44)" : "var(--background-secondary,#f1f3f5)");
      r.c.style.stroke = isCur ? "var(--interactive-accent,#4c6ef5)" : (done ? "var(--color-green,#2f9e44)" : "var(--background-modifier-border,#adb5bd)");
      r.t.style.fill = (isCur || done) ? "#fff" : "var(--text-normal,#222)";
      r.tag.style.fill = "var(--text-muted,#666)";
    });
    orderBox.innerHTML = "";
    if (drawn.length === 0) {
      const s = document.createElement("span");
      s.textContent = "—";
      s.style.color = "var(--text-faint,#888)";
      orderBox.appendChild(s);
    }
    drawn.forEach((id, i) => {
      const chip = document.createElement("span");
      chip.textContent = (i + 1) + ". " + id;
      chip.style.cssText = "padding:2px 8px;border-radius:6px;font-size:13px;background:var(--color-green,#2f9e44);color:#fff";
      orderBox.appendChild(chip);
    });
  }
  function init() {
    cur = -1; drawn = [];
    say.textContent = "Ready · the eye is fixed, the tree is built · press Next Step";
    paint();
  }
  function step() {
    if (cur >= STEPS.length - 1) { if (timer) { clearInterval(timer); timer = null; } return; }
    cur++;
    const st = STEPS[cur];
    st.d.forEach(id => { if (drawn.indexOf(id) < 0) drawn.push(id); });
    say.textContent = "Step " + (cur + 1) + "/" + STEPS.length + " · " + st.s;
    paint();
  }
  $("bsp-next").onclick = () => { if (timer) { clearInterval(timer); timer = null; } step(); };
  $("bsp-play").onclick = () => { if (timer) clearInterval(timer); timer = setInterval(step, 1100); };
  $("bsp-pause").onclick = () => { if (timer) { clearInterval(timer); timer = null; } };
  $("bsp-reset").onclick = () => { if (timer) { clearInterval(timer); timer = null; } init(); };
  init();
})();
```

### 6.11 Exam pointer

> [!tip] Exam pointer — painter's algorithm and BSP
> - State the painter's idea in one sentence, then the four tests in order, then say **which test fails** in cyclic overlap (the plane-side test).
> - Be able to draw three polygons in a cycle and argue that no order exists — "each polygon hides another" is the deck's own wording.
> - Write $f(\mathbf{r}) = (\mathbf{r}-\mathbf{p})\cdot\mathbf{n}$ and give the sign table: $>0$ OUT, $<0$ IN, $=0$ on the plane.
> - Reproduce the first partition (root 1: IN 2,3,4 · OUT 5…11) and the second (root 5: IN 6,7,9a,10,11 · OUT 8,9b).
> - Split formula $t = f(u)/(f(u)-f(v))$ with $f(u)$, $f(v)$ of opposite signs.
> - Write the two traversal rules and the eye-side table (1 OUT, 2 IN, 3 OUT, 5 IN, 8 IN, 6 IN, 7 OUT, 9a IN, 10 IN), then the draw order $2,3,4,1,8,9b,5,6,7,9a,10,11$.
> - Compare costs: build $O(n\log n)$–$O(n^2)$ once, traversal $O(n)$ per frame, versus a per-frame sort for the painter.

---

## 7. Fill-Area Algorithms, Scan Conversion and the 3D Pipeline

*Deck: [[Post 7 - Fill-Area Algorithms, Scan Conversion and the 3D Pipeline.pdf|Post 7 deck]] — 116 slides. Compiles the six-stage pipeline in the deck's own words, lighting versus shading, the inside–outside tests, scan-line polygon fill, seed/boundary/flood fill with the deck's stack traces, and the two ways of storing a character.*

### 7.1 The six stages

The deck restates the pipeline that §2.1 introduced, but this time stage by stage and with the vocabulary that the rest of the lecture uses. Each stage either changes **what an object is** or **which coordinate system it lives in**.

| Stage | Operation | Coordinate change | The deck's own description |
| --- | --- | --- | --- |
| 1 · **Represent** | object representation | — | geometry as polygon meshes, implicit surfaces or particle systems; independent of where the object will sit |
| 2 · **Model** | modelling (geometric) transformation | local → world | places every independently defined object into one shared world frame |
| 3 · **Illuminate** | lighting and shading | — (world) | assigns colour by simulating how light interacts with a surface and its material |
| 4 · **View** | viewing pipeline | world → camera → view plane → viewport | decides *what part of the scene the camera actually sees* |
| 5 · **Rasterize** | scan conversion | continuous device → discrete pixels | converts the viewport to the pixel grid; introduces aliasing |
| 6 · **Display** | frame-buffer output | — | the image on the device |

> [!note] Representation is independent of placement
> The deck is explicit that stage 1 does not know where the object will be. A mesh, an implicit surface or a particle cloud is a description in its *own* coordinates; stage 2 is what attaches a position, orientation and scale. This separation is why one representation can be instanced many times in one scene and why the viewing transform can be changed without touching the geometry.

Two stage-level facts the deck states outright:

- **Stage 4 is the largest.** It contains **three transformations** — world → camera, camera → view plane (projection), window → viewport — and **two operations** — clipping and hidden-surface removal.
- **Stage 5 is where quality is lost.** Device coordinates are continuous, the display is a grid, and the conversion introduces *alias* — visible as jagged edges. Anti-aliasing is applied here, which is exactly the subject of §8.

### 7.2 Lighting versus shading

The deck separates two words that are routinely conflated, and the separation is examinable as a two-column comparison.

| | **Lighting** | **Shading** |
| --- | --- | --- |
| Computes | colour / intensity **at a point** | how those values **vary across a surface** |
| Inputs | light source, material, surface normal, viewing direction | the lighting results at a small set of points |
| Method | a lighting model simulating optical phenomena | interpolation between the computed points |
| Cost | extensive computation per point | much cheaper — far fewer lighting evaluations |
| Question answered | *what colour should this surface point have?* | *how should that value change across the visible surface?* |

> [!important] Definitions
> **Lighting (illumination)** — evaluation of a lighting model at a point, using the light's properties, the surface's material and normal, and the viewing direction.
> **Shading** — the interpolation-based process of colouring the pixels of a surface from the lighting values computed at a few points.

### 7.3 The three shading models

| Model | What is interpolated | Look | Cost |
| --- | --- | --- | --- |
| **Flat** | nothing — one colour per polygon | faceted; each facet a constant tone | cheapest; one lighting evaluation per polygon |
| **Gouraud** (1971) | **colours** at the vertices, linearly across the polygon | smooth on curved objects; highlights can be missed or smeared | one lighting evaluation per vertex, then interpolation |
| **Phong** (1973) | **surface normals** at the vertices, re-lighting per pixel | the most realistic highlights; the normals bend across the facet | one normal interpolation and one lighting evaluation **per pixel** |

> [!note] Why Gouraud loses highlights
> A highlight is a *narrow* peak of the lighting function. Gouraud evaluates the lighting only at the vertices and interpolates the results, so a highlight that falls between two vertices has no vertex value to be interpolated from — it disappears, or smears into a broad patch. Phong interpolates the *normal* instead and evaluates the lighting at every pixel, so the peak is found wherever the interpolated normal happens to point at the light. The price is a lighting evaluation per pixel rather than per vertex.

The deck's summary line is the one to quote: all three models solve the same problem — *how light behaves per polygon* — at increasing computational cost.

### 7.4 Aliasing at the raster stage

Scan conversion maps a continuous viewport onto a discrete grid. A line that is one pixel wide in continuous space has no exact pixel representation: at each column the rasterizer must choose one row, and the chosen rows step, producing the **staircase**. That staircase is aliasing, and it is not an error in the line algorithm — it is the unavoidable consequence of sampling.

> [!warning] Aliasing is not a bug in Bresenham
> Any algorithm that writes one pixel per column produces a staircase. Bresenham/midpoint choose the *nearest* pixel, which is optimal for a one-pixel line, yet the result still staircases. Removing the staircase requires changing the *number of samples per pixel* — either by shading several pixels per column (pre-filtering, §8) or by supersampling. Do not answer "use a better line algorithm" to an aliasing question.

### 7.5 Inside–outside tests

Filling a polygon requires deciding, for every pixel, whether it is inside. The deck presents the two standard rules.

> [!important] Definitions
> **Even–odd (parity) rule** — cast a ray from the test point to infinity and count the polygon edges it crosses; the point is inside if the count is odd. Equivalently, sort the scan line's crossings by $x$ and fill between pairs: 1–2, 3–4, …
> **Nonzero winding rule** — sum the signed crossings of the ray (an edge crossing upward counts $+1$, downward $-1$); the point is inside if the sum is nonzero.

| | Even–odd | Nonzero winding |
| --- | --- | --- |
| Counts | number of crossings | signed sum of crossings |
| A doubly-wound region | **outside** (even) | **inside** (sum $=2$) |
| Self-overlapping polygon | shows a hole where the polygon overlaps itself | filled solid |
| Implementation | parity bit flipped at each crossing | integer accumulator |
| Typical use | simple polygons, general-purpose fill | font outlines, PostScript-style fills |

The two rules agree on every simple polygon and disagree only where the boundary overlaps itself, which is why the choice is invisible in the deck's triangle and decisive for a self-intersecting outline.

For a pixel's neighbourhood the deck writes the eight neighbours as offsets, with $+y$ up:

| Direction | Offset | Direction | Offset |
| --- | --- | --- | --- |
| T (top) | $(0,+1)$ | TL | $(-1,+1)$ |
| B (bottom) | $(0,-1)$ | TR | $(+1,+1)$ |
| L (left) | $(-1,0)$ | BL | $(-1,-1)$ |
| R (right) | $(+1,0)$ | BR | $(+1,-1)$ |

The four orthogonal offsets define **4-connectivity**; all eight define **8-connectivity**. That single choice changes which regions a fill can reach (§7.10).

### 7.6 The scan-line idea

A scan-line fill turns the two-dimensional inside test into a one-dimensional one, once per row of pixels. For a fixed $y$, the polygon's boundary is crossed at a finite set of $x$ values; sorting them and filling between alternate pairs fills the row exactly.

![[CG - Scan Line Fill.excalidraw]]

Three data structures carry the work:

> [!important] Definitions
> **Edge table (ET)** — every non-horizontal edge, bucketed by its lower $y$ endpoint, storing $y_{\max}$, the $x$ at that lower endpoint, and the slope reciprocal $1/m = \Delta x/\Delta y$.
> **Active edge table (AET)** — the edges that currently cross the scan line, kept sorted by their current $x$. An edge enters the AET at its lower endpoint and leaves just after its upper endpoint.
> **Span** — a pair of consecutive $x$ crossings in the sorted AET; the pixels between them are interior.

Two implementation facts make the algorithm fast and correct:

- **Incremental $x$.** The intersection of an edge with the next scan line is not recomputed from the line equation; it is advanced by the constant $1/m$:
$$ x_{y+1} = x_y + \frac{1}{m} = x_y + \frac{\Delta x}{\Delta y} $$
- **Half-open edges.** An edge is active for $y \in [y_{\min}, y_{\max})$. A vertex shared by two edges is then counted once at a local minimum and zero times at a local maximum, which keeps the parity correct without any special-case code.

> [!warning] Horizontal edges never enter the AET
> A horizontal edge has $\Delta y = 0$, so $1/m$ is infinite and it never crosses a scan line transversally. It is simply omitted from the edge table; the vertices at its ends are handled by the half-open rule of the two non-horizontal edges that meet there.

### 7.7 Worked trace: a triangle, row by row

Take the triangle $A(10,10)$, $B(50,20)$, $C(30,60)$ in a coordinate system with $y$ increasing upward, and fill it by scan lines.

| Edge | $y_{\min}$ | $y_{\max}$ | $x$ at $y_{\min}$ | $1/m = \Delta x/\Delta y$ |
| --- | --- | --- | --- | --- |
| $AB$ | 10 | 20 | 10 | $(50-10)/(20-10) = 4$ |
| $AC$ | 10 | 60 | 10 | $(30-10)/(60-10) = 0.4$ |
| $BC$ | 20 | 60 | 50 | $(30-50)/(60-20) = -0.5$ |

| Scan line $y$ | AET after insertion (sorted by $x$) | Span | Pixels |
| --- | --- | --- | --- |
| 10 | $AB:10,\ AC:10$ | 10 → 10 | 1 (the apex $A$) |
| 15 | $AB:30,\ AC:12$ | 12 → 30 | 19 |
| 20 | $AC:14,\ BC:50$ (AB leaves: $y = y_{\max}$) | 14 → 50 | 37 |
| 30 | $AC:18,\ BC:45$ | 18 → 45 | 28 |
| 40 | $AC:22,\ BC:40$ | 22 → 40 | 19 |
| 50 | $AC:26,\ BC:35$ | 26 → 35 | 10 |
| 55 | $AC:28,\ BC:32.5$ | 28 → 32 | 5 |

Check two entries by hand. At $y=30$, edge $AC$ is $x = 10 + 0.4(30-10) = 18$ and edge $BC$ is $x = 50 - 0.5(30-20) = 45$; the two crossings bracket the interior, so the span is $18 \to 45$. At $y=40$ the same formulas give $22$ and $40$. The number of pixels in a span $x_1 \to x_2$ on integer rows is $\lfloor x_2 \rfloor - \lceil x_1 \rceil + 1$, which is where the counts above come from.

> [!note] What the trace demonstrates
> - The AET **gains** an edge exactly at its lower endpoint ($BC$ appears at $y=20$) and **loses** one just after its upper endpoint ($AB$ disappears at $y=20$).
> - Between consecutive rows nothing is recomputed: $AC$ moves $18 \to 18.4 \to 18.8$ by adding $0.4$, and $BC$ moves $45 \to 44.5 \to 44$ by adding $-0.5$.
> - The span never needs the polygon's interior — only the sorted crossings. That is what makes the method $O(\text{edges})$ per row instead of $O(\text{pixels} \times \text{edges})$.

### 7.8 Scan-line polygon fill — algorithm

> [!important] Scan-line polygon fill — statement
> ```text
> 1: build the edge table: for each non-horizontal edge store (ymax, x_at_ymin, 1/m)
> 2: bucket each edge by floor(ymin);  y ← the smallest occupied bucket
> 3: AET ← empty
> 4: while AET is not empty or edges remain:
> 5:     move every edge whose ymin = y from the ET into the AET
> 6:     remove from the AET every edge with ymax ≤ y         // half-open rule
> 7:     sort the AET by current x
> 8:     for each consecutive pair (x1, x2) in the AET:
> 9:         fill pixels from ceil(x1) to floor(x2) on row y
> 10:    for every edge in the AET: x ← x + 1/m            // incremental update
> 11:    y ← y + 1
> ```
>
> **Input:** an ordered vertex list of a polygon (the deck's closing line is literally *"Input: Set of Vertices of the Polygon"*).
> **Output:** the set of interior pixels.
> **Cost:** $O(E)$ per scan line for the AET update, plus the sort; with an insertion-sorted AET the total is $O(E + S)$ amortised for $E$ edges and $S$ spans, because the AET order changes only when edges cross.

### 7.9 Interactive dry run

The widget fills the triangle of §7.7 one scan line at a time. The left panel is the raster; the right panel is the live AET, with each edge's current $x$ and slope, the sorted crossings, and the resulting span. Step until $y = 60$ and the triangle is complete.

```js-engine
// Rendered by the JS Engine plugin: `container` is this block's output element.
container.innerHTML = `
<div id="w-sl" style="border:1px solid var(--background-modifier-border,#ccc);border-radius:10px;padding:12px;background:var(--background-primary,#fff);color:var(--text-normal,#222);font:14px/1.45 var(--font-interface,system-ui)">
  <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px">
    <button id="sl-play">▶ Play</button>
    <button id="sl-pause">⏸ Pause</button>
    <button id="sl-next">⏭ Next Step</button>
    <button id="sl-reset">↺ Reset</button>
  </div>
  <div id="sl-say" style="min-height:40px;color:var(--text-muted,#555);margin-bottom:8px">Ready · triangle A(10,10) B(50,20) C(30,60) · press Next Step</div>
  <div style="display:flex;gap:12px;flex-wrap:wrap;align-items:flex-start">
    <svg id="sl-stage" viewBox="0 0 420 400" style="flex:1 1 300px;min-width:260px;height:auto;display:block;background:var(--background-secondary,#f8f9fa);border-radius:8px"></svg>
    <div style="flex:1 1 220px;min-width:200px">
      <div style="font-size:13px;color:var(--text-faint,#777);margin-bottom:4px">Active edge table</div>
      <div id="sl-aet" style="font-family:var(--font-monospace,monospace);font-size:13px;line-height:1.7;min-height:90px"></div>
      <div style="font-size:13px;color:var(--text-faint,#777);margin:10px 0 4px">Sorted crossings</div>
      <div id="sl-xs" style="font-family:var(--font-monospace,monospace);font-size:13px"></div>
      <div style="font-size:13px;color:var(--text-faint,#777);margin:10px 0 4px">Pixels filled</div>
      <div id="sl-total" style="font-family:var(--font-monospace,monospace);font-size:13px">0</div>
    </div>
  </div>
</div>
`;
const $ = (id) => container.querySelector("#" + id);
(() => {
  const S = 5, OX = 40, OY = 20, H = 400;
  const A = { x: 10, y: 10 }, B = { x: 50, y: 20 }, C = { x: 30, y: 60 };
  const EDGES = [
    { name: "AB", y0: 10, y1: 20, x0: 10, dx: 4 },
    { name: "AC", y0: 10, y1: 60, x0: 10, dx: 0.4 },
    { name: "BC", y0: 20, y1: 60, x0: 50, dx: -0.5 }
  ];
  const px = x => OX + x * S;
  const py = y => H - OY - y * S;
  const NS = "http://www.w3.org/2000/svg";
  const svg = $("sl-stage");
  const el = (t, a) => { const e = document.createElementNS(NS, t); for (const k in a) e.setAttribute(k, a[k]); return e; };
  const fillLayer = el("g", {});
  const lineLayer = el("g", {});
  let steps = [], cur = -1, timer = null, total = 0;

  // static grid + polygon
  for (let g = 0; g <= 70; g += 10) {
    svg.appendChild(el("line", { x1: px(0), y1: py(g), x2: px(70), y2: py(g), stroke: "var(--background-modifier-border,#e9ecef)", "stroke-width": 1 }));
    svg.appendChild(el("line", { x1: px(g), y1: py(0), x2: px(g), y2: py(70), stroke: "var(--background-modifier-border,#e9ecef)", "stroke-width": 1 }));
    const ty = el("text", { x: px(0) - 8, y: py(g) + 4, "text-anchor": "end", "font-size": 10, fill: "var(--text-faint,#888)" });
    ty.textContent = g; svg.appendChild(ty);
    const tx = el("text", { x: px(g), y: py(0) + 16, "text-anchor": "middle", "font-size": 10, fill: "var(--text-faint,#888)" });
    tx.textContent = g; svg.appendChild(tx);
  }
  svg.appendChild(fillLayer);
  svg.appendChild(el("polygon", { points: px(A.x) + "," + py(A.y) + " " + px(B.x) + "," + py(B.y) + " " + px(C.x) + "," + py(C.y), fill: "none", stroke: "var(--text-normal,#222)", "stroke-width": 2 }));
  [["A", A], ["B", B], ["C", C]].forEach(([n, p]) => {
    const t = el("text", { x: px(p.x) - 14, y: py(p.y) - 6, "font-size": 11, fill: "var(--text-muted,#666)" });
    t.textContent = n; svg.appendChild(t);
  });
  svg.appendChild(lineLayer);

  function activeAt(y) {
    return EDGES.filter(e => y >= e.y0 && y < e.y1).map(e => ({
      name: e.name, x: e.x0 + (y - e.y0) * e.dx, dx: e.dx
    })).sort((p, q) => p.x - q.x);
  }
  for (let y = 10; y <= 60; y++) steps.push(y);
  let fills = [];

  function reset() {
    cur = -1; total = 0; fills = [];
    fillLayer.innerHTML = ""; lineLayer.innerHTML = "";
    $("sl-aet").textContent = "—";
    $("sl-xs").textContent = "—";
    $("sl-total").textContent = "0";
    $("sl-say").textContent = "Ready · triangle A(10,10) B(50,20) C(30,60) · press Next Step";
  }
  function step() {
    if (cur >= steps.length - 1) { if (timer) { clearInterval(timer); timer = null; } return; }
    cur++;
    const y = steps[cur];
    const act = activeAt(y);
    lineLayer.innerHTML = "";
    $("sl-aet").innerHTML = act.length
      ? act.map(e => e.name + "  x = " + e.x.toFixed(2) + "  (" + (e.dx >= 0 ? "+" : "") + e.dx.toFixed(2) + "/line)").join("<br>")
      : "empty";
    const xs = act.map(e => e.x);
    $("sl-xs").textContent = xs.length ? xs.map(v => v.toFixed(2)).join("  ") : "—";

    const ln = el("line", { x1: px(0), y1: py(y), x2: px(70), y2: py(y), stroke: "var(--color-red,#e03131)", "stroke-width": 1.5, "stroke-dasharray": "4 3" });
    lineLayer.appendChild(ln);

    let say = "y = " + y + " · AET: ";
    if (act.length === 0) {
      say += "empty → nothing to fill";
    } else {
      say += act.map(e => e.name + " at " + e.x.toFixed(2)).join(", ");
      for (let i = 0; i + 1 < act.length; i += 2) {
        const x1 = act[i].x, x2 = act[i + 1].x;
        const c1 = Math.ceil(x1), c2 = Math.floor(x2);
        const n = Math.max(0, c2 - c1 + 1);
        total += n;
        if (n > 0) fills.push({ y, x1: c1, x2: c2 });
        say += " · fill " + x1.toFixed(1) + " → " + x2.toFixed(1) + " (" + n + " px)";
      }
    }
    fillLayer.innerHTML = "";
    fills.forEach(f => {
      fillLayer.appendChild(el("rect", { x: px(f.x1), y: py(f.y) - 2, width: (f.x2 - f.x1 + 1) * S, height: 4, fill: "var(--interactive-accent,#4c6ef5)", opacity: 0.75 }));
    });
    act.forEach(e => {
      fillLayer.appendChild(el("circle", { cx: px(e.x), cy: py(y), r: 3.5, fill: "var(--color-red,#e03131)" }));
    });
    $("sl-total").textContent = total + " pixels";
    $("sl-say").textContent = say;
  }
  $("sl-next").onclick = () => { if (timer) { clearInterval(timer); timer = null; } step(); };
  $("sl-play").onclick = () => { if (timer) clearInterval(timer); timer = setInterval(step, 320); };
  $("sl-pause").onclick = () => { if (timer) { clearInterval(timer); timer = null; } };
  $("sl-reset").onclick = () => { if (timer) { clearInterval(timer); timer = null; } reset(); };
  reset();
})();
```

### 7.10 Seed fill, boundary fill, flood fill

The scan-line algorithm fills *one polygon* whose vertices are known. The seed-fill family fills *a connected region of pixels* whose extent is discovered as it goes — the natural method for interactive paint programs and for regions defined by their colour rather than by geometry.

> [!important] Definitions
> **Seed fill** — start from one interior pixel (the seed) and colour its connected neighbours, stopping where the region ends.
> **Boundary fill** — the region is bounded by a known boundary colour; a pixel is filled only if its colour is neither the boundary colour nor the fill colour. This is the deck's test: *colour ≠ boundary **and** ≠ specified colour*.
> **Flood fill** — the region is defined by a uniform interior colour; a pixel is filled only if its colour equals the original interior colour (the one under the seed).
> **4-connected** — neighbours are the four orthogonal pixels $T, B, L, R$; the fill cannot cross a diagonal.
> **8-connected** — neighbours are all eight pixels $T, B, L, R, TL, TR, BL, BR$; the fill can slip through a diagonal gap.

| | Boundary fill | Flood fill |
| --- | --- | --- |
| Test on a candidate pixel | colour ≠ boundary **and** colour ≠ fill | colour = original interior colour |
| Region known by | its wall | its interior colour |
| Filling a multi-coloured interior | works (everything not the wall is fair game) | fails — only the one colour is replaced |
| Typical use | paint-bucket with an outline | background replacement, magic wand |

#### 4- versus 8-connectivity

The choice is not cosmetic. A boundary that is **8-connected** (its pixels touch only at corners in places) is *impermeable to a 4-connected fill* but *permeable to an 8-connected fill*, because the diagonal step is exactly the move that slips through the corner contact.

| Fill | Boundary 4-connected | Boundary 8-connected |
| --- | --- | --- |
| **4-connected** | contained | contained — a diagonal gap is still a wall |
| **8-connected** | contained — the wall has no corner contact to slip through | **leaks** through a diagonal gap |

So the safe pairing for a closed region is *8-connected boundary with 4-connected fill*, or *4-connected boundary with 8-connected fill*. This is why paint programs expose the connectivity as a fill option: the wrong pair floods the whole canvas.

### 7.11 The deck's stack traces

The deck runs the same stack-based pseudo-code three times and prints the stack size after every pop. The numbers are the algorithm's fingerprint: a pop either pushes some new neighbours or pushes none.

| Demo | Stack-size sequence | Pops | Reading |
| --- | --- | --- | --- |
| 4-connected region | $1\to4$, $4\to5$, $5\to4$, $4\to3$, $3\to4$, $4\to3$, $3\to2$, $2\to1$, $1\to0$ | 9 | the seed pushes 4 neighbours; later pops push 0 or 1 because most neighbours are already filled |
| 8-connected region | $1\to8$ (8 pushed), then $8\to7$, $7\to6$, $6\to5$, $5\to4$, $4\to3$, $3\to2$, $2\to1$, $1\to0$ (0 pushed each time) | 9 | the seed pushes all 8 neighbours; every later pop finds nothing new |
| boundary fill | $1\to3$ (3 pushed), $3\to2$, $2\to1$, $1\to0$ | 4 | only three neighbours pass the boundary test |

> [!note] Reading a stack trace
> The pair "$a \to b$ (k pushed)" is a complete statement about one iteration: $a$ pixels were on the stack, one was popped ($a-1$ remain), $k$ new ones were pushed, and the result is $b = a - 1 + k$. Check the 8-connected line: $8 - 1 + 0 = 7$; then $7 - 1 + 0 = 6$; and so on to $1 - 1 + 0 = 0$. The trace terminates when the stack is empty, and the number of pops equals the number of pixels filled — 9 for the first two demos, 4 for the boundary demo.

### 7.12 Seed fill — algorithm

> [!important] Seed / flood fill — statement
> ```text
> 1: push the seed pixel; mark it as filled
> 2: while the stack is not empty:
> 3:     p ← pop()
> 4:     set the pixel p to the fill colour
> 5:     for each neighbour q of p (4 or 8 of them, in a fixed order):
> 6:         if q is inside the region test and q is not already marked:
> 7:             mark q; push q
> 8: (recursion is the same algorithm with the call stack in place of the explicit stack)
> ```
>
> **Input:** a seed pixel, a region test (boundary colour or interior colour), and a connectivity.
> **Output:** the filled region.
> **Cost:** $O(\text{pixels in the region})$ pops, each doing 4 or 8 constant-time neighbour tests; the stack holds at most $O(\text{perimeter})$ entries. Marking **on push**, not on pop, is what prevents the same pixel being queued many times.

> [!warning] Mark on push, or the stack explodes
> If a pixel is marked only when it is popped, a pixel with several already-queued neighbours is pushed once per neighbour, and the stack can grow far beyond the region's perimeter. The deck's traces are consistent with marking on push: every stack size stays small and the pop count equals the pixel count exactly.

### 7.13 Interactive dry run

The widget below runs both connectivities on the same closed boundary. The boundary has **diagonal corner contacts** — it is 8-connected but not 4-connected. Choose 4-connectivity and the fill stays inside; choose 8-connectivity and it escapes through the corner and floods the canvas. Watch the stack counter and the "pushed" figure in the narration.

```js-engine
// Rendered by the JS Engine plugin: `container` is this block's output element.
container.innerHTML = `
<div id="w-ff" style="border:1px solid var(--background-modifier-border,#ccc);border-radius:10px;padding:12px;background:var(--background-primary,#fff);color:var(--text-normal,#222);font:14px/1.45 var(--font-interface,system-ui)">
  <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px;align-items:center">
    <button id="ff-play">▶ Play</button>
    <button id="ff-pause">⏸ Pause</button>
    <button id="ff-next">⏭ Next Step</button>
    <button id="ff-reset">↺ Reset</button>
    <label style="margin-left:6px;font-size:13px;color:var(--text-muted,#555)">
      <input type="radio" name="ffc" id="ff-c4" checked> 4-connected
    </label>
    <label style="font-size:13px;color:var(--text-muted,#555)">
      <input type="radio" name="ffc" id="ff-c8"> 8-connected
    </label>
  </div>
  <div id="ff-say" style="min-height:40px;color:var(--text-muted,#555);margin-bottom:8px">Ready · seed at (3,3) · 4-connected · press Next Step</div>
  <div style="display:flex;gap:12px;flex-wrap:wrap;align-items:flex-start">
    <svg id="ff-stage" viewBox="0 0 470 300" style="flex:1 1 320px;min-width:280px;height:auto;display:block;background:var(--background-secondary,#f8f9fa);border-radius:8px"></svg>
    <div style="flex:1 1 170px;min-width:160px;font-family:var(--font-monospace,monospace);font-size:13px;line-height:1.7">
      <div style="color:var(--text-faint,#777);font-family:var(--font-interface,system-ui)">Stack</div>
      <div id="ff-size">1</div>
      <div style="color:var(--text-faint,#777);font-family:var(--font-interface,system-ui);margin-top:8px">Pixels filled</div>
      <div id="ff-count">0</div>
      <div style="color:var(--text-faint,#777);font-family:var(--font-interface,system-ui);margin-top:8px">Top of stack</div>
      <div id="ff-top">(3,3)</div>
    </div>
  </div>
</div>
`;
const $ = (id) => container.querySelector("#" + id);
(() => {
  const MAP = [
    "..................",
    ".######...........",
    ".#....#...........",
    ".#....#...........",
    ".#....#...........",
    ".#.....#..........",
    ".#......#.........",
    ".#.....#..........",
    ".#....#...........",
    ".######...........",
    ".................."
  ];
  const COLS = 18, ROWS = MAP.length, CELL = 26;
  const NS = "http://www.w3.org/2000/svg";
  const svg = $("ff-stage");
  const el = (t, a) => { const e = document.createElementNS(NS, t); for (const k in a) e.setAttribute(k, a[k]); return e; };
  const cells = {};
  for (let r = 0; r < ROWS; r++) {
    for (let c = 0; c < COLS; c++) {
      const rect = el("rect", { x: c * CELL + 1, y: r * CELL + 1, width: CELL - 2, height: CELL - 2, rx: 3, stroke: "var(--background-modifier-border,#dee2e6)", "stroke-width": 0.5 });
      rect.style.fill = MAP[r][c] === "#" ? "var(--text-faint,#495057)" : "var(--background-primary,#fff)";
      svg.appendChild(rect);
      cells[c + "," + r] = rect;
    }
  }
  const seedMark = el("circle", { cx: 3 * CELL + CELL / 2, cy: 3 * CELL + CELL / 2, r: 4, fill: "var(--color-red,#e03131)" });
  svg.appendChild(seedMark);

  let stack = [], filled = new Set(), timer = null, connected = 4;
  const say = $("ff-say");

  function blocked(c, r) {
    return c < 0 || r < 0 || c >= COLS || r >= ROWS || MAP[r][c] === "#";
  }
  function neighbours(c, r) {
    const out = [[c, r - 1], [c - 1, r], [c + 1, r], [c, r + 1]];
    if (connected === 8) out.push([c - 1, r - 1], [c + 1, r - 1], [c - 1, r + 1], [c + 1, r + 1]);
    return out;
  }
  function reset() {
    if (timer) { clearInterval(timer); timer = null; }
    stack = [[3, 3]];
    filled = new Set(["3,3"]);
    Object.keys(cells).forEach(k => {
      const [c, r] = k.split(",").map(Number);
      cells[k].style.fill = MAP[r][c] === "#" ? "var(--text-faint,#495057)" : "var(--background-primary,#fff)";
      cells[k].style.opacity = 1;
    });
    seedMark.setAttribute("visibility", "visible");
    $("ff-size").textContent = "1";
    $("ff-count").textContent = "0";
    $("ff-top").textContent = "(3,3)";
    say.textContent = "Ready · seed at (3,3) · " + connected + "-connected · press Next Step";
  }
  function step() {
    if (stack.length === 0) { if (timer) { clearInterval(timer); timer = null; } say.textContent = "Stack empty · region complete · " + filled.size + " pixels"; return; }
    const before = stack.length;
    const [c, r] = stack.pop();
    cells[c + "," + r].style.fill = "var(--interactive-accent,#4c6ef5)";
    let pushed = 0;
    neighbours(c, r).forEach(([nc, nr]) => {
      if (blocked(nc, nr)) return;
      const k = nc + "," + nr;
      if (filled.has(k)) return;
      filled.add(k); stack.push([nc, nr]);
      cells[k].style.fill = "var(--color-yellow,#f08c00)"; pushed++;
    });
    if (c === 3 && r === 3) seedMark.setAttribute("visibility", "hidden");
    $("ff-size").textContent = stack.length;
    $("ff-count").textContent = filled.size;
    $("ff-top").textContent = stack.length ? "(" + stack[stack.length - 1][0] + "," + stack[stack.length - 1][1] + ")" : "empty";
    say.textContent = "pop (" + c + "," + r + ") · stack " + before + " → " + stack.length + " (" + pushed + " pushed) · filled " + filled.size;
  }
  $("ff-next").onclick = () => { if (timer) { clearInterval(timer); timer = null; } step(); };
  $("ff-play").onclick = () => { if (timer) clearInterval(timer); timer = setInterval(step, 90); };
  $("ff-pause").onclick = () => { if (timer) { clearInterval(timer); timer = null; } };
  $("ff-reset").onclick = reset;
  $("ff-c4").onchange = () => { connected = 4; reset(); };
  $("ff-c8").onchange = () => { connected = 8; reset(); };
  reset();
})();
```

> [!warning] What to conclude from the leak
> The boundary in the widget is closed in the 8-connected sense — you cannot walk from inside to outside without touching a boundary pixel along an 8-neighbour step. A 4-connected fill still cannot escape, because its only moves are orthogonal and every orthogonal route is blocked. Switch the fill to 8-connected and it steps diagonally through the corner contact immediately. **The topology of the fill must be at least as strict as the topology of the boundary**, which is the general statement behind the table in §7.10.

### 7.14 Character generation: the bitmapped font

There are two ways to put a character on a raster, and the deck builds the same letter $L$ both ways.

A **bitmapped font** stores the character as a small binary image: one bit per pixel, $1$ = on, $0$ = off. For the deck's $5\times7$ letter:

![[CG - Bitmapped Font L.png|300]]

*Figure — the $5\times7$ bitmap of `L`: six upper rows `10000`, bottom row `11111`.*

| Quantity | Value | Arithmetic |
| --- | --- | --- |
| Grid | $5 \times 7$ | — |
| Stored samples | 35 bits | $5 \times 7$ |
| On pixels | 11 | vertical stroke 7 + foot 5 − shared corner 1 |
| Enlarged grid | $10 \times 14$ | each dimension $\times 2$ |
| Enlarged storage | 140 bits | $10 \times 14$ |
| Enlarged on pixels | 44 | $11 \times 4$ — each original pixel becomes a $2\times2$ block |

> [!note] Why enlargement multiplies the on-pixels by four
> Nearest-neighbour replication replaces every original pixel by a $2\times2$ block, so area (and the count of on-pixels) scales by $2^2 = 4$ while the *pattern* is unchanged. The deck's conclusion is the important part: *replication preserves the block pattern; it does not recover a smoother character outline.* A magnified bitmap is a blocky bitmap, not a better letter.

### 7.15 Character generation: the outlined font

An **outlined font** stores the character as geometry: points and line segments that describe the boundary. The deck's `L` is a six-vertex counterclockwise polygon.

![[CG - Outlined Font L.png|300]]

*Figure — the same `L` as a polygon with vertices $(0,0),(5,0),(5,1),(1,1),(1,7),(0,7)$; the outline is scaled and then scan-converted.*

| Quantity | Value | Note |
| --- | --- | --- |
| Vertices (CCW) | $(0,0),(5,0),(5,1),(1,1),(1,7),(0,7)$ | six points, closed |
| Raster extent | $[0,5]\times[0,7]$ | vertices describe **cell boundaries**, pixel centres at $(i+\tfrac12, j+\tfrac12)$ |
| Geometric area | 11 square units | vertical stroke $1\times7$ plus foot $5\times1$ minus the shared $1\times1$ corner |
| After scaling by 2 | vertices doubled, area 44 | area scales by $2^2$ |
| Rasterized on-pixels at $2\times$ | 44 for this axis-aligned outline | the deck's lucky coincidence |

> [!warning] Area is not a pixel count
> The deck ends the section with the sentence to remember: *geometric area and the number of rasterized pixels are different quantities in general.* They coincide here (11 and 44) only because the outline is axis-aligned, one unit thick, and sits exactly on cell boundaries. A slanted or curved outline has a raster pixel count that differs from its area, which is why fonts are designed in outline and *then* hinted/rasterized rather than stored as bitmaps.

| | Bitmapped font | Outlined font |
| --- | --- | --- |
| Storage | one bit per pixel of every size | points + segments, one master |
| Scaling | replicate blocks — quality lost | transform the geometry, re-rasterize — quality kept |
| Rotation | degrades badly | exact (a transform on the points) |
| Rendering cost | trivial — copy bits | needs a polygon fill per glyph |
| Small sizes | crisp, hand-tuned | needs hinting to stay legible |
| The deck's example | $5\times7 = 35$ bits, 11 on | 6 vertices, area 11 |

### 7.16 Exam pointer

> [!tip] Exam pointer — fill areas and the pipeline
> - Six stages with their coordinate changes, and stage 4's **3 transformations + 2 operations**.
> - Lighting versus shading in two columns, then flat / Gouraud / Phong with what each interpolates and why Gouraud loses highlights.
> - Even–odd versus nonzero winding, including a doubly-wound region.
> - ET / AET definitions, the half-open rule, $x \leftarrow x + 1/m$, and the triangle trace of §7.7.
> - Seed vs boundary vs flood fill, the deck's test `colour ≠ boundary AND ≠ fill`, and the 4/8-connectivity leak table.
> - Reproduce the stack traces: $1\to4 \ldots 1\to0$ (4-connected), $1\to8$ then all $(0\text{ pushed})$ (8-connected), $1\to3 \ldots$ (boundary).
> - Bitmap $5\times7$: 35 bits, 11 on; doubled: 140 bits, 44 on. Outline: six vertices, area 11, and the warning that area ≠ pixel count.

---

## 8. Anti-Aliasing I — The Gupta–Sproull Algorithm

*Deck: [[Post 8 - Anti-Aliasing I - The Gupta-Sproull Algorithm.pdf|Post 8 deck]] — 70 slides. Two parts: the midpoint line algorithm that decides **which** pixel, then the Gupta–Sproull extension that decides **how bright** each of the three pixels in the column should be.*

### 8.1 What the algorithm is

The midpoint algorithm answers one question per step and answers it with a sign: E or NE. That produces the nearest pixel but says nothing about *how much* of the pixel the line actually covers — the staircase survives. Gupta–Sproull keeps the midpoint choice untouched and adds a **pre-filtering** step: the chosen pixel and its two vertical neighbours in the same column are all shaded, with weights taken from their perpendicular distance to the line.

| What it is | How it works | What it builds on |
| --- | --- | --- |
| a **pre-filtering** technique for anti-aliased line drawing | the weight of a pixel depends on the perpendicular distance from the pixel centre to the line's centreline | the **midpoint** line-drawing algorithm |

The deck fixes the working octant once and never revisits it:

> [!warning] Assumptions for the whole topic
> Integer endpoints · $x_0 < x_1$ · $0 \le \Delta y \le \Delta x$ · $y$ increases upward · $a = \Delta y$, $b = -\Delta x$.
> **Other octants are handled by coordinate transformations** (swap $x$ and $y$, or negate an axis) applied before and after the algorithm — never by changing the decision rule.

![[CG - Gupta Sproull Coverage.excalidraw]]

### 8.2 Part 1 — two candidates and a midpoint

Having just chosen $(x_k, y_k)$, the next pixel is one of two, because $x$ always advances by exactly one:

| Candidate | Position | Meaning |
| --- | --- | --- |
| **E** | $(x_k+1,\ y_k)$ | same row — "east" |
| **NE** | $(x_k+1,\ y_k+1)$ | one row up — "north-east" |

The decision is made at the **midpoint** $M(x_k+1,\ y_k+\tfrac12)$. If $M$ lies below the line, the line passes above the midpoint and NE is closer; if $M$ lies on or above the line, E is at least as close.

Represent the line by

$$ f(x,y) = ax + by + c = 0, \qquad a = \Delta y,\quad b = -\Delta x,\quad c = \Delta x\,y_0 - \Delta y\,x_0 $$

and use the **scaled** version $F(x,y) = 2(ax+by+c)$. The factor 2 is not cosmetic: the midpoint has a $\tfrac12$ in it, and doubling clears the fraction so that every value in the algorithm stays an integer.

| $F$ at a point | Meaning |
| --- | --- |
| $F > 0$ | below the line |
| $F = 0$ | on the line |
| $F < 0$ | above the line |

The deck's sign convention is worth fixing in memory: **positive is below**, because $b = -\Delta x < 0$ and increasing $y$ makes $F$ decrease.

### 8.3 The decision variable and its update

$$ d_k = F(M) = F\!\left(x_k+1,\ y_k+\tfrac12\right) = 2\left[a(x_k+1) + b\left(y_k+\tfrac12\right) + c\right] $$

> [!important] The decision rule
> **$d_k > 0$** — the midpoint is below the line → choose **NE**.
> **$d_k \le 0$** — the midpoint is on or above the line → choose **E**.
> The tie $d_k = 0$ chooses **E**, exactly as in the clipping ties of §3. This is a convention, not a derivation, and the deck states it explicitly.

The update comes from moving the *midpoint*, not the pixel. After E the next midpoint is one step right; after NE it is one step right and one up:

$$ \begin{aligned}
\text{after E: } & d_{k+1} = d_k + 2a \\
\text{after NE: } & d_{k+1} = d_k + 2(a+b)
\end{aligned} $$

Both constants are computed once. The derivation of the NE case in full, as the deck writes it:

$$ \begin{aligned}
d_{k+1} &= F\!\left(x_k+2,\ y_k+1+\tfrac12\right) \\
&= 2\left[a(x_k+2) + b\left(y_k+\tfrac32\right) + c\right] \\
&= 2\left[a(x_k+1) + b\left(y_k+\tfrac12\right) + c\right] + 2(a+b) \\
&= d_k + 2(a+b)
\end{aligned} $$

The reasoning in one line: the bracket is $F$ at the old midpoint, and the extra terms are the cost of moving one right ($2a$) and one up ($2b$). With $a = \Delta y$ and $b = -\Delta x$, $2(a+b)$ is usually negative — the decision variable drifts back toward zero after every upward step, which is why the line alternates between E and NE.

### 8.4 The starting value

The first midpoint is at $(x_0+1,\ y_0+\tfrac12)$, and $(x_0,y_0)$ lies on the line, so $f(x_0,y_0) = 0$:

$$ \begin{aligned}
d_0 &= F\!\left(x_0+1,\ y_0+\tfrac12\right) \\
&= 2(ax_0 + by_0 + c) + 2a + b \\
&= 2a + b \qquad\text{since } f(x_0,y_0)=0
\end{aligned} $$

$$ \boxed{\ d_0 = 2a + b = 2\Delta y - \Delta x\ } $$

> [!note] Why $d_0$ can be negative
> For a shallow line ($\Delta y < \Delta x/2$) the start value is negative and the first step is E; for a steep line inside the octant ($\Delta y > \Delta x/2$) it is positive and the first step is NE. Nothing is special about either case — the same update rules carry on from whatever sign $d_0$ has.

### 8.5 The complete midpoint algorithm

> [!important] Midpoint line drawing — statement
> ```text
> 1: input integer endpoints (x0,y0), (x1,y1)
> 2: require x0 < x1 and 0 ≤ Δy ≤ Δx
> 3: Δx = x1 − x0;  Δy = y1 − y0
> 4: a = Δy;  b = −Δx;  c = Δx·y0 − Δy·x0
> 5: d = 2a + b                       // = 2Δy − Δx
> 6: x = x0;  y = y0;  P = {(x,y)}
> 7: while x < x1 do
> 8:     if d > 0 then  y = y + 1;  d = d + 2(a+b)
> 9:     else          d = d + 2a
> 10:    x = x + 1;  add (x,y) to P
> 11: end while
> 12: return P
> ```
>
> **Cost:** one comparison and one addition per column — $O(\Delta x)$, all integer arithmetic, no division and no floating point.

### 8.6 Worked midpoint trace: from (0,0) to (8,5)

Here $\Delta x = 8$, $\Delta y = 5$, so $a = 5$, $b = -8$, $d_0 = 2(5) - 8 = 2$, and the two constants are

$$ 2a = 10, \qquad 2(a+b) = 2(5-8) = -6 $$

| Step | $d$ before | Test | Pixel chosen | $d$ after | $x$ |
| --- | --- | --- | --- | --- | --- |
| 0 | $2$ | $>0$ → NE | $(1,1)$ | $2-6=-4$ | 1 |
| 1 | $-4$ | $\le 0$ → E | $(2,1)$ | $-4+10=6$ | 2 |
| 2 | $6$ | $>0$ → NE | $(3,2)$ | $6-6=0$ | 3 |
| 3 | $0$ | tie → E | $(4,2)$ | $0+10=10$ | 4 |
| 4 | $10$ | $>0$ → NE | $(5,3)$ | $10-6=4$ | 5 |
| 5 | $4$ | $>0$ → NE | $(6,4)$ | $4-6=-2$ | 6 |
| 6 | $-2$ | $\le 0$ → E | $(7,4)$ | $-2+10=8$ | 7 |
| 7 | $8$ | $>0$ → NE | $(8,5)$ | $8-6=2$ | 8 |

The pixel set is $(0,0),(1,1),(2,1),(3,2),(4,2),(5,3),(6,4),(7,4),(8,5)$. Check against the true line $y = 5x/8$: at $x=3$ the line is at $1.875$ and the chosen row is 2; at $x=4$ the line is exactly $2.5$ — the tie — and the rule takes the lower row 2. Both are the nearest choice; the tie is broken downwards by convention.

### 8.7 Part 2 — from a vertical gap to a perpendicular distance

The intensity must reflect **how much of the pixel the line covers**, which is governed by the perpendicular distance from the pixel centre to the line — not by the vertical gap. The two are related by the line's slope.

Let $v$ be the vertical offset of the line from the selected pixel centre in that column:

$$ v = y_{\text{line}}(x_{\text{selected}}) - y_{\text{selected}}, \qquad -\tfrac12 \le v \le \tfrac12 $$

because the selected pixel is the nearest one. Consider the small right triangle with vertical side $v$ and perpendicular side $s$, and the slope triangle of the line with sides $\Delta x$, $\Delta y$ and hypotenuse $L = \sqrt{\Delta x^2 + \Delta y^2}$. The two triangles are similar (both right-angled and tilted by the line's slope), so

$$ \frac{s}{v} = \frac{\Delta x}{L} \quad\Longrightarrow\quad \boxed{\ s = v\,\frac{\Delta x}{L}\ } $$

> [!note] The factor is a constant for the whole line
> $\Delta x / L = \cos\theta$, where $\theta$ is the angle between the line and the $x$-axis. It is computed once and reused for every pixel: the perpendicular distance is always the vertical distance times the same cosine. This is why the algorithm needs no trigonometry per pixel.

The algorithm never computes $v$ or $s$ geometrically; it converts the decision variable instead, in three short steps.

**Step 5a — $F$ measures the vertical gap.** Pick $Q$ on the line directly above or below $P$ (same $x$), so $F(Q) = 0$, and let $v_P = y_Q - y_P$. Only $y$ changes between $P$ and $Q$:

$$ F(P) - F(Q) = 2b\,(y_P - y_Q) = 2(-\Delta x)(-v_P) = 2\Delta x\,v_P $$

so $F(P) = 2\Delta x\,v_P$ — the signed vertical gap scaled by $2\Delta x$, positive below the line and negative above it.

**Step 5b — $F$ also measures the perpendicular distance.** Substituting $v_P = (L/\Delta x)s_P$ from the similarity above gives

$$ F(P) = 2\Delta x \cdot \frac{L}{\Delta x}s_P = 2L\,s_P \quad\Longrightarrow\quad \boxed{\ s_P = \frac{F(P)}{2L}\ } $$

In particular, at the midpoint, $d = F(M) = 2L\,s_M$, so the decision variable *is* the midpoint's signed distance up to the constant $2L$.

**Step 5c — half a pixel up or down.** Within one column only the $2by$ term changes, so moving half a pixel up subtracts $\Delta x$ and half a pixel down adds it:

$$ F(x, y+\tfrac12) = F(x,y) + 2b\cdot\tfrac12 = F(x,y) - \Delta x $$

$E$ is half a pixel *below* $M$, and $NE$ is half a pixel *above* it:

$$ F(E) = F(M) + \Delta x = d + \Delta x, \qquad F(NE) = F(M) - \Delta x = d - \Delta x $$

**Step 5d — the signed distance of the selected pixel.**

$$ \boxed{\ s = \frac{F(\text{selected})}{2L} =
\begin{cases}
\dfrac{d + \Delta x}{2L}, & \text{E chosen } (d \le 0)\\[6pt]
\dfrac{d - \Delta x}{2L}, & \text{NE chosen } (d > 0)
\end{cases}\ } $$

Three practical consequences, all stated by the deck:

- $L = \sqrt{\Delta x^2 + \Delta y^2}$ is fixed for the whole line and computed **once**.
- Use $d$ **before** it is updated by the midpoint step — the distance describes the pixel about to be shaded, not the next decision.
- Keep the **sign** of $s$: it tells which side of the line the pixel is on, and the neighbours' distances depend on it.

### 8.8 The filter and the blend

The distance becomes a weight through a **filter**, and the weight becomes a colour through a linear blend:

$$ \alpha = \text{Filter}(|s|), \qquad C = \alpha\,C_{\text{line}} + (1-\alpha)\,C_{\text{background}} $$

| $\alpha$ | Result |
| --- | --- |
| $\alpha \to 1$ | the pixel is fully the line colour |
| $\alpha \to 0$ | the pixel is unchanged background |
| black background | $C = \alpha\,C_{\text{line}}$ — intensity is proportional to $\alpha$ |

The deck's filter curve rises to a peak $\alpha(0)$ at zero distance and falls to zero at a distance of one pixel, which is the standard **cone** filter:

$$ \text{Filter}(D) = \max(0,\ 1 - D) $$

![[CG - Gupta Sproull E vs NE Case.png|440]]

*Figure — the E case and the NE case: the same three pixels per column, only the identity of the middle one and the sign of $s$ change.*

### 8.9 The two vertical neighbours

Selecting a pixel also shades the pixels directly above and below it in the same column, at distances $\Delta x/L$ apart in perpendicular terms.

| | E chosen ($d \le 0$) | NE chosen ($d > 0$) |
| --- | --- | --- |
| Signed distance $s$ | $(d + \Delta x)/(2L)$ | $(d - \Delta x)/(2L)$ |
| Upper neighbour | $(x_k+1,\ y_k+1)$, distance $D_{\text{upper}}$ | $(x_k+1,\ y_k+2)$, distance $D_{\text{upper}}$ |
| Lower neighbour | $(x_k+1,\ y_k-1)$, distance $D_{\text{lower}}$ | $E = (x_k+1,\ y_k)$, distance $D_{\text{lower}}$ |
| Both cases | $D_{\text{upper}} = \left|s - \Delta x/L\right|$ | $D_{\text{lower}} = \left|s + \Delta x/L\right|$ |

The asymmetry in the coordinates is not a typo: when NE is selected, the "lower neighbour" *is* E, the pixel just below NE. The neighbour formulas themselves never change — only $s$ does, by $+\Delta x$ for E and $-\Delta x$ for NE.

> [!warning] Do not move the selected pixel to the neighbour's place
> The three pixels are shaded **in the same column** $x_k+1$. The selected pixel gets $\alpha = \text{Filter}(|s|)$; the pixel above gets $\text{Filter}(D_{\text{upper}})$; the pixel below gets $\text{Filter}(D_{\text{lower}})$. When the selected pixel is NE, the pixel below it is E — it does **not** get the selected pixel's $\alpha$.

### 8.10 Worked shading trace: the same line from (0,0) to (8,5)

With $\Delta x = 8$, $\Delta y = 5$: $L = \sqrt{89} = 9.4340$, $2L = 18.8680$, and $\Delta x/L = 0.8480$. The $\alpha$ column applies the cone filter $\max(0, 1-D)$.

| Column $x$ | $d$ before | Pixel | $s$ | $\alpha$ | $D_{\text{upper}}$ | $\alpha_{\text{upper}}$ | $D_{\text{lower}}$ | $\alpha_{\text{lower}}$ |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 2 | NE | $-0.318$ | 0.682 | 1.166 | 0 | 0.530 | 0.470 |
| 2 | $-4$ | E | $0.212$ | 0.788 | 0.636 | 0.364 | 1.060 | 0 |
| 3 | 6 | NE | $-0.106$ | 0.894 | 0.954 | 0.046 | 0.742 | 0.258 |
| 4 | 0 | E | $0.424$ | 0.576 | 0.424 | 0.576 | 1.272 | 0 |
| 5 | 10 | NE | $0.106$ | 0.894 | 0.742 | 0.258 | 0.954 | 0.046 |
| 6 | 4 | NE | $-0.212$ | 0.788 | 1.060 | 0 | 0.636 | 0.364 |
| 7 | $-2$ | E | $0.318$ | 0.682 | 0.530 | 0.470 | 1.166 | 0 |
| 8 | 8 | NE | $0.000$ | 1.000 | 0.848 | 0.152 | 0.848 | 0.152 |

Check column 3 by hand. The choice is NE because $d = 6 > 0$, so

$$ s = \frac{6 - 8}{18.868} = -0.1060, \qquad \alpha = 1 - 0.1060 = 0.894 $$
$$ D_{\text{upper}} = \left|-0.1060 - 0.8480\right| = 0.9540 \Rightarrow \alpha = 0.046, \qquad
   D_{\text{lower}} = \left|-0.1060 + 0.8480\right| = 0.7420 \Rightarrow \alpha = 0.258 $$

The shaded band therefore spans three rows in every column, with the centre pixel darkest. The trace also shows the symmetry of the line: columns 1 and 7, 2 and 6, 3 and 5 have mirror-image values, and column 4 — the exact midpoint of the line — is shaded symmetrically above and below.

> [!note] What the eye sees
> Three gray levels per column, summing roughly to the coverage of the ideal line, look like a smooth stroke at viewing distance. This is *pre-filtering*: the weight is computed before sampling, from the geometry, instead of averaging samples afterwards. That is why the method needs no supersampling buffer — and why it is cheap, and why its quality is limited to the filter's three-pixel footprint.

### 8.11 Gupta–Sproull — algorithm

> [!important] Gupta–Sproull — statement
> ```text
> 1: input (x0,y0),(x1,y1); require x0<x1 and 0 ≤ Δy ≤ Δx
> 2: Δx = x1−x0;  Δy = y1−y0;  a = Δy;  b = −Δx
> 3: d = 2a + b;  x = x0;  y = y0
> 4: L = sqrt(Δx² + Δy²);  k = Δx/L
> 5: plot(x,y)                                  // first pixel, full intensity
> 6: while x < x1 do
> 7:     if d > 0 then  s = (d − Δx)/(2L);  x' = x+1;  y' = y+1
> 8:     else          s = (d + Δx)/(2L);  x' = x+1;  y' = y
> 9:     α = Filter(|s|);  blend(x', y', α)
> 10:    Du = |s − k|;  Dl = |s + k|
> 11:    blend(x', y'+1, Filter(Du));  blend(x', y'−1, Filter(Dl))
> 12:    if d > 0 then  y = y+1;  d = d + 2(a+b)
> 13:    else          d = d + 2a
> 14:    x = x + 1
> ```
>
> **Input:** integer endpoints in the working octant, a line colour, a background colour, and a filter.
> **Output:** a line drawn with three shaded pixels per column.
> **Cost:** $O(\Delta x)$ — the same integer loop as midpoint plus three blends and two absolute values per column; $O(1)$ extra memory. No division inside the loop ($k$ and $2L$ are computed once), no trigonometry.

| Step in the loop | Midpoint alone | Gupta–Sproull adds |
| --- | --- | --- |
| decide the pixel | $d > 0$ → NE, else E | unchanged |
| distance | — | $s = (d \pm \Delta x)/(2L)$, using $d$ **before** the update |
| shade | one pixel, full intensity | $\alpha = \text{Filter}(|s|)$ and a blend |
| neighbours | — | $D_u$, $D_l$ and two more blends |
| update | $d \mathrel{+}= 2a$ or $2(a+b)$ | unchanged |

### 8.12 Interactive dry run

The widget walks the eight columns of §8.10. Each step shades the selected pixel and its two vertical neighbours, and the table records $d$, the choice, $s$ and the three weights. Watch column 4 — the exact midpoint — where the pixel above and the pixel below receive the same $\alpha$.

```js-engine
// Rendered by the JS Engine plugin: `container` is this block's output element.
container.innerHTML = `
<div id="w-gs" style="border:1px solid var(--background-modifier-border,#ccc);border-radius:10px;padding:12px;background:var(--background-primary,#fff);color:var(--text-normal,#222);font:14px/1.45 var(--font-interface,system-ui)">
  <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px">
    <button id="gs-play">▶ Play</button>
    <button id="gs-pause">⏸ Pause</button>
    <button id="gs-next">⏭ Next Step</button>
    <button id="gs-reset">↺ Reset</button>
  </div>
  <div id="gs-say" style="min-height:40px;color:var(--text-muted,#555);margin-bottom:8px">Ready · line (0,0) → (8,5) · L = √89 = 9.434 · press Next Step</div>
  <div style="display:flex;gap:12px;flex-wrap:wrap;align-items:flex-start">
    <svg id="gs-stage" viewBox="0 0 430 330" style="flex:1 1 300px;min-width:270px;height:auto;display:block;background:var(--background-secondary,#f8f9fa);border-radius:8px"></svg>
    <div style="flex:1 1 230px;min-width:210px">
      <div style="font-size:13px;color:var(--text-faint,#777);margin-bottom:4px">Shaded columns</div>
      <div id="gs-table" style="font-family:var(--font-monospace,monospace);font-size:12px;line-height:1.7"></div>
    </div>
  </div>
</div>
`;
const $ = (id) => container.querySelector("#" + id);
(() => {
  const CELL = 40, OX = 20, OY = 20, XMAX = 9, YMAX = 7;
  const DX = 8, DY = 5, L = Math.sqrt(DX * DX + DY * DY), TWOL = 2 * L, K = DX / L;
  const NS = "http://www.w3.org/2000/svg";
  const svg = $("gs-stage");
  const el = (t, a) => { const e = document.createElementNS(NS, t); for (const k in a) e.setAttribute(k, a[k]); return e; };
  const px = x => OX + x * CELL, py = y => OY + (YMAX - y) * CELL;
  const pixelLayer = el("g", {}), gridLayer = el("g", {}), markLayer = el("g", {});

  for (let y = 0; y < YMAX; y++) for (let x = 0; x < XMAX; x++) {
    gridLayer.appendChild(el("rect", { x: px(x) + 1, y: py(y) + 1, width: CELL - 2, height: CELL - 2, fill: "none", stroke: "var(--background-modifier-border,#dee2e6)", "stroke-width": 0.7 }));
  }
  svg.appendChild(pixelLayer);
  svg.appendChild(gridLayer);
  svg.appendChild(el("line", { x1: px(0), y1: py(0), x2: px(8), y2: py(5), stroke: "var(--color-red,#e03131)", "stroke-width": 1.5, "stroke-dasharray": "5 4", opacity: 0.85 }));
  for (let x = 0; x < XMAX; x++) {
    const t = el("text", { x: px(x) + CELL / 2, y: py(0) + CELL + 12, "text-anchor": "middle", "font-size": 10, fill: "var(--text-faint,#888)" });
    t.textContent = x; svg.appendChild(t);
  }
  for (let y = 0; y < YMAX; y++) {
    const t = el("text", { x: OX - 6, y: py(y) + CELL / 2 + 4, "text-anchor": "end", "font-size": 10, fill: "var(--text-faint,#888)" });
    t.textContent = y; svg.appendChild(t);
  }
  svg.appendChild(markLayer);

  const a_const = DY, b_const = -DX;
  let x, y, d, cur, timer, rows;
  const say = $("gs-say");
  const table = $("gs-table");

  function reset() {
    if (timer) { clearInterval(timer); timer = null; }
    x = 0; y = 0; d = 2 * a_const + b_const; cur = 0; rows = [];
    pixelLayer.innerHTML = ""; markLayer.innerHTML = "";
    pixelLayer.appendChild(el("rect", { x: px(0) + 1, y: py(0) + 1, width: CELL - 2, height: CELL - 2, fill: "var(--interactive-accent,#4c6ef5)" }));
    table.innerHTML = "<span style='color:var(--text-faint,#888)'>—</span>";
    say.textContent = "Ready · pixel (0,0) drawn at full intensity · d₀ = 2Δy − Δx = 2 · press Next Step";
  }
  function shade(cx, cy, alpha) {
    if (cx >= XMAX || cy < 0 || cy >= YMAX) return;
    pixelLayer.appendChild(el("rect", { x: px(cx) + 1, y: py(cy) + 1, width: CELL - 2, height: CELL - 2, fill: "var(--interactive-accent,#4c6ef5)", opacity: Math.max(0.04, alpha) }));
  }
  function step() {
    if (cur >= 8) { if (timer) { clearInterval(timer); timer = null; } return; }
    const dBefore = d;
    const ne = d > 0;
    const s = ne ? (d - DX) / TWOL : (d + DX) / TWOL;
    const aSel = Math.max(0, 1 - Math.abs(s));
    const du = Math.abs(s - K), dl = Math.abs(s + K);
    const au = Math.max(0, 1 - du), al = Math.max(0, 1 - dl);
    const nx = x + 1, ny = ne ? y + 1 : y;

    pixelLayer.innerHTML = "";
    pixelLayer.appendChild(el("rect", { x: px(0) + 1, y: py(0) + 1, width: CELL - 2, height: CELL - 2, fill: "var(--interactive-accent,#4c6ef5)" }));
    rows.forEach(r => {
      shade(r.nx, r.ny, r.aSel); shade(r.nx, r.ny + 1, r.au); shade(r.nx, r.ny - 1, r.al);
    });
    shade(nx, ny, aSel); shade(nx, ny + 1, au); shade(nx, ny - 1, al);
    markLayer.innerHTML = "";
    markLayer.appendChild(el("rect", { x: px(nx), y: py(ny), width: CELL, height: CELL, fill: "none", stroke: "var(--color-blue,#1971c2)", "stroke-width": 2.5 }));

    rows.push({ nx, ny, aSel, au, al, x: nx, d: dBefore, choice: ne ? "NE" : "E", s });
    d = ne ? d + 2 * (a_const + b_const) : d + 2 * a_const;
    x = nx; y = ny; cur++;

    table.innerHTML = rows.map(r =>
      "x=" + r.x + "  d=" + r.d + "  " + r.choice + "<br>&nbsp;&nbsp;s=" + r.s.toFixed(3) +
      "  α=" + r.aSel.toFixed(3) + "<br>&nbsp;&nbsp;αu=" + r.au.toFixed(3) + "  αl=" + r.al.toFixed(3)
    ).join("<br>");
    say.textContent = "Column " + nx + " · d = " + dBefore + " → " + (dBefore > 0 ? "NE" : "E") +
      " · s = (" + dBefore + (dBefore > 0 ? " − 8" : " + 8") + ")/18.868 = " + s.toFixed(3) +
      " · α = " + aSel.toFixed(3) + " · αu = " + au.toFixed(3) + " · αl = " + al.toFixed(3);
  }
  $("gs-next").onclick = () => { if (timer) { clearInterval(timer); timer = null; } step(); };
  $("gs-play").onclick = () => { if (timer) clearInterval(timer); timer = setInterval(step, 900); };
  $("gs-pause").onclick = () => { if (timer) { clearInterval(timer); timer = null; } };
  $("gs-reset").onclick = reset;
  reset();
})();
```

### 8.13 Exam pointer

> [!tip] Exam pointer — Gupta–Sproull
> - State the two-part structure: **which pixel** (midpoint) then **how bright** (distance filter).
> - Write $f = ax+by+c$, $F = 2f$, and the sign table ($F>0$ below, $F<0$ above); justify the factor 2 by the midpoint's $\tfrac12$.
> - Derive $d_0 = 2a+b = 2\Delta y - \Delta x$ and the two updates $2a$, $2(a+b)$; reproduce the $(0,0)$–$(8,5)$ trace with $d = 2, -4, 6, 0, 10, 4, -2, 8$.
> - Derive $s = v\Delta x/L$ from similar triangles, then $s = F/(2L)$, then $s = (d \pm \Delta x)/(2L)$ — plus for E, minus for NE, using $d$ **before** the update.
> - Neighbours: $D_u = |s - \Delta x/L|$, $D_l = |s + \Delta x/L|$; the blend $C = \alpha C_{\text{line}} + (1-\alpha)C_{\text{bg}}$.
> - Say why it is $O(\Delta x)$ with integer arithmetic, and why it is a *pre*-filter rather than supersampling.

---

## 9. Animation — The 2D Production Process

*Deck: [[Post 9 - Animation - The 2D Production Process.pdf|Post 9 deck]] — 55 handwritten slides. The deck carries one exam question, quoted below; this topic answers it in the order the question implies, using the character jumping over a puddle as the running example.*

### 9.1 The question

> *Explain the 2D animation production process using a character jumping over a puddle as an example, with suitable illustrations.*

The question asks for three things at once, and the marks are distributed across them:

1. **The process** — the ordered stages from an idea to a finished shot, with what each stage produces.
2. **The worked example** — every stage instantiated on one jump: which drawings exist, at which frames, in which order.
3. **Illustrations** — the pose sheet, the arc, and the timing chart, because a process described without drawings is not an animation answer.

### 9.2 What a 2D animation is

> [!important] Definitions
> **Frame** — one still image. **Frame rate** — frames per second; at **24 fps** one second of motion is 24 frames.
> **Keyframe (extreme)** — a drawing made by the animator that defines a pose the action must pass through.
> **In-between** — a drawing produced between two keys, either by an assistant or by interpolation, that carries the pose from one key to the next.
> **Timing** — the number of frames between keys. **Spacing** — where the in-betweens sit inside that interval.

Two facts organise everything else. First, **motion is an illusion produced by discrete samples**: the character does not move, 24 drawings per second are shown and the eye integrates them. Second, **the number of drawings is a budget**. A one-second jump is 24 drawings at "full animation" (one drawing per frame, *on ones*), or 12 drawings if each is shot twice (*on twos*) — and the choice is visible: on twos looks steppier and is the standard for economical TV animation.

### 9.3 The production pipeline

![[CG - 2D Animation Pipeline.excalidraw]]

The pipeline has three phases. **Pre-production** decides what will happen (story, timing, design); **production** makes the drawings; **post-production** assembles them with the background, camera and effects.

| Stage | Produces | For the puddle jump |
| --- | --- | --- |
| 1 · **Story & storyboard** | beat sheet, thumbnails, shot timing | "character walks, sees puddle, jumps, lands, walks on" — 2 seconds of screen time |
| 2 · **Character design** | model sheet: proportions, views, palette, construction | the character's height in heads, limb lengths, the shape language |
| 3 · **Keyframes (extremes)** | the poses the action must hit | crouch, push-off, rise, apex, fall, contact, recover |
| 4 · **In-betweens & timing** | the drawings between keys, plus the timing chart | 6 in-betweens per gap, spaced by the arc and the easing |
| 5 · **Clean-up & colour** | clean line, ink and paint, background layer | consistent line weight, flat colours, the puddle painted once |
| 6 · **Compositing** | camera move, effects, render and export | the character layer over the background, exported at 24 fps |

> [!note] Why the order is not negotiable
> Each stage consumes the previous stage's output as its *specification*. In-betweening requires finished keys — an in-between between two unresolved poses is wasted work. Clean-up requires a locked timing chart, because the number of drawings is decided there. Compositing requires painted cels and a background. Reordering the pipeline does not merely cost time; it makes the output undefined.

### 9.4 Stage 1 — storyboard and beat sheet

A storyboard fixes **what happens** and **how long it takes**, before any drawing is animated. Each panel carries a beat and a duration in frames.

| Beat | Frames | Content |
| --- | --- | --- |
| 1 | 1–4 | the character walks in from the left, head down |
| 2 | 5–8 | sees the puddle, stops, looks down |
| 3 | 9–12 | anticipation: crouch, arms back |
| 4 | 13–20 | the jump: push-off → apex → descent |
| 5 | 21–24 | landing, squash, recover, walk on |

The beat sheet is where the **frame budget** is spent. Two seconds of screen time is 48 frames at 24 fps; the storyboard decides that the jump gets 8 of them and the anticipation 4, and that decision constrains every later stage.

### 9.5 Stage 2 — the model sheet

The model sheet is the character's specification: proportions, construction shapes, the front/side/three-quarter views, and the colour palette. Its purpose is **consistency across drawings made by different people on different days**. For the jump it also fixes the *line of action* — the curve through the body that gives the pose its energy — and the character's height in heads, which the squash and stretch will preserve in volume.

> [!important] Volume preservation
> Squash and stretch change the character's *proportions*, not its *volume*. A crouch that is $1.2\times$ wider should be about $1/1.2 = 0.83\times$ shorter. This is the rule that keeps a squashed character from looking deflated, and it is why the model sheet fixes the construction shapes rather than only the silhouette.

### 9.6 Stage 3 — the seven key poses

![[CG - Jump Arc Keyframes.excalidraw]]

| Key | Frame | Pose | What it establishes |
| --- | --- | --- | --- |
| **K1** | 1 | standing at the edge, weight forward | the start of the action |
| **K2** | 5 | crouch: knees bent, arms back, body compressed (**squash**) | **anticipation** — the audience reads the jump before it happens |
| **K3** | 9 | push-off: legs extended, arms up, body elongated (**stretch**) | the impulse; the fastest part of the motion |
| **K4** | 13 | apex: body gathered, legs tucked, arms out | the top of the arc, where motion is slowest |
| **K5** | 17 | descent: legs reaching down, arms forward | preparation for contact |
| **K6** | 21 | contact: knees absorb, body compressed again (**squash**) | impact and weight |
| **K7** | 24 | recover: back to standing, settle | the action ends, ready to walk on |

The keys are drawn as **extremes**: they are the poses where the action changes direction or meaning. Everything between them is interpolation, and interpolation is only as good as the extremes it connects.

### 9.7 Stage 4 — timing, spacing and the in-betweens

Between K1 and K2, and so on, the assistant draws the in-betweens. Two decisions are being made at once:

- **Timing** — how many frames the gap gets. A short gap is fast, a long gap is slow.
- **Spacing** — where inside the gap each in-between sits. Even spacing gives constant speed; bunched spacing near a key gives **slow in / slow out** around that key.

For the jump, the arc is a parabola, and the speed along it is not constant: the character lingers near the apex and moves fastest near the ground. The timing chart encodes exactly that.

| Key | Frame | Height above ground $h$ (units) | Gap to next key |
| --- | --- | --- | --- |
| K1 | 1 | 0 | 4 frames — slow start (anticipation holds) |
| K2 | 5 | 0 (crouched) | 4 frames — explosive, wide spacing |
| K3 | 9 | 163 | 4 frames — decelerating toward the apex |
| K4 | 13 | 180 | 4 frames — accelerating away from the apex |
| K5 | 17 | 152 | 4 frames |
| K6 | 21 | 0 (compressed) | 3 frames — the shortest gap, the snap of recovery |
| K7 | 24 | 0 | — |

Heights follow $h(t) = 4H\,t(1-t)$ with $H = 180$ units over the 23-frame span, which is why the apex sits at $t = 0.522$ and $h = 179.6$ rather than exactly 180: the apex falls between two frames, and the drawing at frame 13 is one frame off the mathematical peak.

> [!note] The arc is the path, the spacing is the speed
> These are separate pieces of information and they are drawn separately. The **arc** is a curve through space that every drawing must lie on; the **timing chart** is a set of marks along that curve saying which drawing happens on which frame. A common beginner error is to space the drawings evenly along a correctly drawn arc, which produces a jump that floats: constant speed along a ballistic path looks weightless, because real gravity decelerates on the way up and accelerates on the way down.

### 9.8 Stage 5 — clean-up, ink and paint

The animator's rough keys and in-betweens go to clean-up, where the lines are redrawn consistently, then to ink and paint, where each cel is filled with flat colour. The background is painted **once**, separately, and the character is composited over it — which is the economic reason 2D animation separates the layers at all: the background does not need to be redrawn for every frame.

### 9.9 Stage 6 — compositing and post

The painted cels are photographed or scanned over the background at the frame rate, with any camera move (a pan, a truck-in) applied at this stage rather than drawn. Effects — dust at the landing, splash from the puddle, motion smear on the fastest frames — are added here. The shot is exported at 24 fps for film or 25/30 fps for broadcast, and the timing chart is what guarantees that the exported frame count matches the board's intent.

### 9.10 The principles the example forces

| Principle | Where it appears in the jump | What it fixes |
| --- | --- | --- |
| **Squash and stretch** | K2 and K6 compressed, K3 elongated | weight and elasticity; preserves volume |
| **Anticipation** | K2 crouch before the push-off | the audience reads the action before it happens |
| **Arcs** | the parabolic path K1 → K7 | natural motion; nothing in nature moves in a straight line |
| **Slow in / slow out** | bunched spacing near K4 apex, wide spacing near K3 | the effect of gravity and inertia |
| **Follow-through** | arms and head continue after the body stops at K6 | the body is a chain, not a rigid block |
| **Secondary action** | the puddle splash, the dust | supports the main action without competing with it |
| **Staging** | the silhouette of each key reads clearly | the pose is legible at a glance |

> [!warning] The jump fails if any one of these is missing
> Remove the anticipation and the jump looks teleported. Remove the arc and it looks like an elevator. Space it evenly and it floats. Skip the squash and the character looks rigid. The exam answer should name each principle **and point at the frame where it is used** — the example is what earns the marks, not the list.

### 9.11 Interpolation: the arithmetic of an in-between

An in-between can be computed rather than drawn, and the computation is the same linear interpolation used everywhere else in the course. For two keys $\mathbf{K}_1, \mathbf{K}_2$ and a parameter $t \in [0,1]$:

$$ \mathbf{P}(t) = (1-t)\,\mathbf{K}_1 + t\,\mathbf{K}_2 $$

With a jump the keys are only two of the seven poses; between any two consecutive keys the same formula applies, and the *path* (the arc) is a separate constraint that the interpolated positions must satisfy.

Linear interpolation gives constant speed. To get slow-in/slow-out, the parameter is eased before it is used:

$$ t' = 3t^2 - 2t^3 \qquad\text{(smoothstep)}, \qquad \mathbf{P}(t') = (1-t')\mathbf{K}_1 + t'\mathbf{K}_2 $$

Easing changes **where** the in-betweens sit, not the path: at $t = 0.25$ the eased parameter is $t' = 0.156$, so the drawing is closer to the first key than a linear in-between would be — it leaves slowly. At $t = 0.75$, $t' = 0.844$ — it arrives slowly.

Worked numbers for a gap of four frames from $x = 100$ to $x = 260$ ($\Delta x = 160$):

| In-between | $t$ | linear $x$ | eased $t'$ | eased $x$ |
| --- | --- | --- | --- | --- |
| 1st | 0.25 | 140 | 0.156 | 125.0 |
| 2nd | 0.50 | 180 | 0.500 | 180.0 |
| 3rd | 0.75 | 220 | 0.844 | 235.0 |

The middle in-between is identical in both columns — easing always pins the halfway point — while the outer two move toward the keys. The spacing is now **wide in the middle, narrow at the ends**, which is exactly the spacing chart an animator would draw by hand.

> [!important] In-betweening — statement
> ```text
> 1: input two keys K1, K2 and the number of frames n in the gap
> 2: for f = 1 to n:
> 3:     t  = (f − 1) / (n − 1)
> 4:     t' = ease(t)                  // identity for linear, 3t² − 2t³ for smooth
> 5:     P  = (1 − t')·K1 + t'·K2
> 6:     if the action is a jump: project P onto the arc, i.e. use P.x and
> 7:        set P.y = 4H·t'·(1 − t')
> 8:     draw P
> ```
>
> **Input:** two key poses, the frame count, and the easing function.
> **Output:** $n$ drawings, the first and last of which are the keys themselves.
> **Cost:** $O(n)$ per gap, one interpolation and possibly one evaluation of the arc per frame.

### 9.12 Interactive dry run

The widget tweens the character between the takeoff key and the landing key across 13 frames. Switch between **linear** and **eased** spacing and watch the dots on the timing track: linear spacing is uniform, eased spacing bunches at both ends. The panel shows $t$, $t'$ and the position actually drawn.

```js-engine
// Rendered by the JS Engine plugin: `container` is this block's output element.
container.innerHTML = `
<div id="w-tween" style="border:1px solid var(--background-modifier-border,#ccc);border-radius:10px;padding:12px;background:var(--background-primary,#fff);color:var(--text-normal,#222);font:14px/1.45 var(--font-interface,system-ui)">
  <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px;align-items:center">
    <button id="tw-play">▶ Play</button>
    <button id="tw-pause">⏸ Pause</button>
    <button id="tw-next">⏭ Next Step</button>
    <button id="tw-reset">↺ Reset</button>
    <label style="margin-left:6px;font-size:13px;color:var(--text-muted,#555)">
      <input type="radio" name="twe" id="tw-linear" checked> linear
    </label>
    <label style="font-size:13px;color:var(--text-muted,#555)">
      <input type="radio" name="twe" id="tw-ease"> smoothstep
    </label>
  </div>
  <div id="tw-say" style="min-height:40px;color:var(--text-muted,#555);margin-bottom:8px">Ready · 13 frames from takeoff to landing · linear spacing · press Next Step</div>
  <svg id="tw-stage" viewBox="0 0 560 300" style="width:100%;height:auto;display:block;background:var(--background-secondary,#f8f9fa);border-radius:8px"></svg>
  <div id="tw-table" style="margin-top:8px;font-family:var(--font-monospace,monospace);font-size:12px;line-height:1.6;max-height:110px;overflow:auto"></div>
</div>
`;
const $ = (id) => container.querySelector("#" + id);
(() => {
  const NS = "http://www.w3.org/2000/svg";
  const svg = $("tw-stage");
  const el = (t, a) => { const e = document.createElementNS(NS, t); for (const k in a) e.setAttribute(k, a[k]); return e; };
  const GROUND = 226, X0 = 60, X1 = 500, H = 130, N = 13;
  const say = $("tw-say");
  let frame = 0, timer = null, eased = false, drawn = [];

  // static scene
  svg.appendChild(el("rect", { x: 0, y: GROUND, width: 560, height: 300 - GROUND, fill: "var(--background-modifier-border,#e9ecef)" }));
  svg.appendChild(el("line", { x1: 0, y1: GROUND, x2: 560, y2: GROUND, stroke: "var(--text-faint,#868e96)", "stroke-width": 2 }));
  svg.appendChild(el("ellipse", { cx: 280, cy: GROUND + 6, rx: 70, ry: 8, fill: "var(--color-blue,#a5d8ff)", opacity: 0.55 }));
  const pl = el("text", { x: 252, y: GROUND + 26, "font-size": 11, fill: "var(--color-blue,#1971c2)" });
  pl.textContent = "puddle"; svg.appendChild(pl);
  const dots = el("g", {}); svg.appendChild(dots);
  const ghosts = el("g", {}); svg.appendChild(ghosts);
  const figure = el("g", {}); svg.appendChild(figure);
  const frameLabel = el("text", { x: 14, y: 24, "font-size": 13, fill: "var(--text-muted,#666)" });
  svg.appendChild(frameLabel);
  const axisLabel = el("text", { x: 14, y: 44, "font-size": 11, fill: "var(--text-faint,#888)" });
  axisLabel.textContent = "frames 1 → 13   (keys at 1 and 13)";
  svg.appendChild(axisLabel);

  // timing track
  const TRACK_Y = 258;
  svg.appendChild(el("line", { x1: X0, y1: TRACK_Y, x2: X1, y2: TRACK_Y, stroke: "var(--background-modifier-border,#ced4da)", "stroke-width": 2 }));

  function pose(t) {
    const tt = eased ? (3 * t * t - 2 * t * t * t) : t;
    const x = X0 + (X1 - X0) * tt;
    const y = GROUND - 4 * H * tt * (1 - tt);
    return { x, y, tt };
  }
  function drawFigure(g, x, y, scale) {
    g.innerHTML = "";
    const s = scale || 1;
    g.appendChild(el("circle", { cx: x, cy: y - 34 * s, r: 7 * s, fill: "none", stroke: "var(--text-normal,#222)", "stroke-width": 2 }));
    g.appendChild(el("line", { x1: x, y1: y - 27 * s, x2: x, y2: y - 12 * s, stroke: "var(--text-normal,#222)", "stroke-width": 2.5 }));
    g.appendChild(el("line", { x1: x, y1: y - 12 * s, x2: x - 7 * s, y2: y, stroke: "var(--text-normal,#222)", "stroke-width": 2.5 }));
    g.appendChild(el("line", { x1: x, y1: y - 12 * s, x2: x + 7 * s, y2: y, stroke: "var(--text-normal,#222)", "stroke-width": 2.5 }));
    g.appendChild(el("line", { x1: x - 8 * s, y1: y - 22 * s, x2: x + 8 * s, y2: y - 18 * s, stroke: "var(--text-normal,#222)", "stroke-width": 2 }));
  }
  function reset() {
    if (timer) { clearInterval(timer); timer = null; }
    frame = 0; drawn = [];
    dots.innerHTML = ""; ghosts.innerHTML = "";
    const p = pose(0);
    drawFigure(figure, p.x, p.y, 1);
    frameLabel.textContent = "frame 1 / 13";
    $("tw-table").innerHTML = "<span style='color:var(--text-faint,#888)'>—</span>";
    say.textContent = "Ready · 13 frames from takeoff to landing · " + (eased ? "smoothstep" : "linear") + " spacing · press Next Step";
  }
  function step() {
    if (frame >= N - 1) { if (timer) { clearInterval(timer); timer = null; } return; }
    frame++;
    const t = frame / (N - 1);
    const p = pose(t);
    ghosts.innerHTML = "";
    drawn.slice(-3).forEach((q, i) => {
      const g = el("g", { opacity: 0.25 + i * 0.15 });
      ghosts.appendChild(g);
      drawFigure(g, q.x, q.y, 1);
    });
    drawFigure(figure, p.x, p.y, 1);
    dots.appendChild(el("circle", { cx: p.x, cy: TRACK_Y, r: 4, fill: "var(--interactive-accent,#4c6ef5)" }));
    drawn.push(p);
    frameLabel.textContent = "frame " + (frame + 1) + " / 13";
    const gap = drawn.length > 1 ? Math.abs(drawn[drawn.length - 1].x - drawn[drawn.length - 2].x).toFixed(1) : "—";
    say.textContent = "frame " + (frame + 1) + " · t = " + t.toFixed(3) + " · t′ = " + p.tt.toFixed(3) +
      " · x = " + p.x.toFixed(1) + " · height = " + (GROUND - p.y).toFixed(0) + " · spacing from previous = " + gap;
    const rows = drawn.map((q, i) => {
      const tt = (i + 1) / (N - 1);
      return "f" + (i + 2) + "  t=" + tt.toFixed(2) + "  t′=" + q.tt.toFixed(3) + "  x=" + q.x.toFixed(0) + "  h=" + (GROUND - q.y).toFixed(0);
    });
    $("tw-table").innerHTML = rows.join("<br>");
  }
  $("tw-next").onclick = () => { if (timer) { clearInterval(timer); timer = null; } step(); };
  $("tw-play").onclick = () => { if (timer) clearInterval(timer); timer = setInterval(step, 420); };
  $("tw-pause").onclick = () => { if (timer) { clearInterval(timer); timer = null; } };
  $("tw-reset").onclick = reset;
  $("tw-linear").onchange = () => { eased = false; reset(); };
  $("tw-ease").onchange = () => { eased = true; reset(); };
  reset();
})();
```

### 9.13 Exam pointer

> [!tip] Exam pointer — 2D animation
> - Draw the pipeline in three phases with six stages, and say what each stage *produces* (not just its name).
> - Answer the question's example explicitly: **seven keys** (K1 crouch … K7 recover), the frame numbers 1, 5, 9, 13, 17, 21, 24, and the arc through them.
> - Draw the arc and the timing chart **separately**, and say that the arc is the path while the timing chart is the speed.
> - Name the principles against specific frames: anticipation at K2, squash at K2/K6, stretch at K3, slow in/out at K4, follow-through after K6.
> - Give the in-between formula $\mathbf{P}(t) = (1-t)\mathbf{K}_1 + t\mathbf{K}_2$ and the eased version $t' = 3t^2 - 2t^3$; the four-frame gap example (125 / 180 / 235 against 140 / 180 / 220) shows the spacing change numerically.
> - Close with the frame budget: 24 fps, one second = 24 drawings, on ones versus on twos.

---

## Formula Summary

| Quantity | Expression | Notes |
| --- | --- | --- |
| Camera basis | $\mathbf{n}=\dfrac{\mathbf{o}-\mathbf{l}}{\lVert\mathbf{o}-\mathbf{l}\rVert},\ \mathbf{u}=\dfrac{\mathbf{v}_{up}\times\mathbf{n}}{\lVert\cdot\rVert},\ \mathbf{v}=\mathbf{n}\times\mathbf{u}$ | right-handed; $\mathbf{n}$ points *behind* the camera |
| View matrix | $M_{view}=\mathbf{R}\,T(-\mathbf{o})$ | translation first for column vectors |
| Orthographic matrix | $M_{ortho}$ with $2/(x_{\max}-x_{\min})$ and $-2/(z_{far}-z_{near})$ | $z$ row negated because the camera looks down $-z$ |
| Perspective matrix | $M_{persp}$, fourth row $(0,0,-1,0)$ | sets $w=-z_{cam}$; requires $z<0$ |
| Viewport map | $V_x=s_xW_x+t_x,\ V_y=s_yW_y+t_y$ | $s=\Delta V/\Delta W$; $y$-flip needs $s_y<0$ |
| Point inside window | $x_{\min}\le x\le x_{\max}$ AND $y_{\min}\le y\le y_{\max}$ | ties count as inside |
| Line parametric form | $P(t)=P_0+t(P_1-P_0),\ 0\le t\le 1$ | all clipping solves for $t$ |
| Intersection with $x=x_{\min}$ | $t=\dfrac{x_{\min}-x_0}{x_1-x_0}$ | denominator $0$ ⇒ parallel to the plane |
| Outcode order | `Far Near Top Bottom Right Left` | bit 5 … bit 0 |
| Trivial decisions | OR $=0$ accept · AND $\neq0$ reject | otherwise clip |
| Face normal | $\mathbf{N}=(B-A)\times(C-A)$ | outward if vertices are counterclockwise when seen from outside |
| Front/back test | $\mathbf{N}\cdot\mathbf{v}<0$ front, $>0$ back | for $\mathbf{v}=(0,0,-1)$: $\mathbf{N}\cdot\mathbf{v}=-N_z$ |
| Plane from a face | $Ax+By+Cz+D=0$, $\mathbf{N}=(A,B,C)$, $D=-Ax_1-By_1-Cz_1$ | $C\neq0$ required for the depth solve |
| Depth from the plane | $z=\dfrac{-D-Ax-By}{C}$ | $z$ grows inward (farther) |
| Incremental depth | $\Delta z_x=-\dfrac{A}{C},\quad \Delta z_y=+\dfrac{B}{C}$ | one add per pixel |
| Plane side function | $f(\mathbf{r})=(\mathbf{r}-\mathbf{p})\cdot\mathbf{n}$ | $>0$ OUT, $<0$ IN, $=0$ on the plane |
| Split parameter | $t=\dfrac{f(\mathbf{u})}{f(\mathbf{u})-f(\mathbf{v})}$ | requires opposite signs, so $t\in(0,1)$ |
| BSP traversal | eye OUT: IN → node → OUT; eye IN: OUT → node → IN | one dot product per node |
| Edge slope reciprocal | $\dfrac{1}{m}=\dfrac{\Delta x}{\Delta y}=\dfrac{x_2-x_1}{y_2-y_1}$ | horizontal edges never enter the AET |
| Scan-line update | $x\leftarrow x+\dfrac{1}{m}$ | edge active for $y\in[y_{\min},y_{\max})$ |
| Span fill | fill $\lceil x_1\rceil \ldots \lfloor x_2\rfloor$ for sorted pairs | pairs 1–2, 3–4, … |
| Fill test | boundary fill: colour ≠ boundary AND ≠ fill; flood fill: colour = interior | mark on **push** |
| Midpoint start | $d_0=2a+b=2\Delta y-\Delta x$ | $a=\Delta y$, $b=-\Delta x$ |
| Midpoint updates | E: $d\mathrel{+}=2a$ · NE: $d\mathrel{+}=2(a+b)$ | $d>0$ ⇒ NE; $d\le0$ ⇒ E |
| Line length | $L=\sqrt{\Delta x^2+\Delta y^2}$ | computed once per line |
| Signed distance | $s=\dfrac{d+\Delta x}{2L}$ (E), $s=\dfrac{d-\Delta x}{2L}$ (NE) | use $d$ **before** the update |
| Neighbour distances | $D_{upper}=\left|s-\dfrac{\Delta x}{L}\right|,\ D_{lower}=\left|s+\dfrac{\Delta x}{L}\right|$ | same for E and NE; only $s$ changes |
| Blend | $C=\alpha C_{line}+(1-\alpha)C_{bg}$ | $\alpha=\mathrm{Filter}(|s|)$, cone $=1-D$ |
| In-between | $\mathbf{P}(t)=(1-t)\mathbf{K}_1+t\mathbf{K}_2$ | two keys, $t\in[0,1]$ |
| Eased in-between | $t'=3t^2-2t^3$ | pins $t'=0.5$ at $t=0.5$ |
| Jump height | $h(t)=4H\,t(1-t)$ | symmetric arc; apex at $t=0.5$ |
| Bitmap storage | $5\times7=35$ bits → $10\times14=140$ at $\times2$ | on-pixels $11\to44$ |
| Outline area | $1\times7+5\times1-1=11$ units² | scales by $2^2=4$; area ≠ pixel count |

> [!note] Source images
> All `CG - …excalidraw` drawings are original reconstructions of the hand-drawn diagrams in the decks; they live in the vault-root `Excalidraw/` folder. The PNG figures are page renders from the corresponding deck, stored in `Computer Graphics/images/` with the `CG - ` prefix: the tetrahedron back-face result from [[Post 5 - Hidden Surface Removal I - Back-Face Elimination and the Z-Buffer.pdf|Post 5 deck]], the Weiler–Atherton crossings and the concave-subject split from [[Post 4 - Polygon and 3D Fill-Area Clipping.pdf|Post 4 deck]], the BSP traversal order from [[Post 6 - Hidden Surface Removal II - Painter's Algorithm and BSP Trees.pdf|Post 6 deck]], the E/NE case of Gupta–Sproull from [[Post 8 - Anti-Aliasing I - The Gupta-Sproull Algorithm.pdf|Post 8 deck]], and the bitmapped and outlined letter `L` from [[Post 7 - Fill-Area Algorithms, Scan Conversion and the 3D Pipeline.pdf|Post 7 deck]].
