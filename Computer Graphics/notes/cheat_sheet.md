---
title: Computer Graphics — Formula Cheat Sheet
tags:
  - computer-graphics
  - CG
  - cheat-sheet
  - formulas
---

# Computer Graphics — Formula Cheat Sheet

> [!info] What this sheet is
> A one-stop revision sheet for **every deck in `pdfs/`** — Pre 1–8, the bridge deck (Intensity Quantization), and Post 1–9. Each topic keeps its syllabus number and gives the formulas, the matrices and the convention notes, with no worked traces. For full definitions, derivations and numeric traces see [[CG_Midsem_notes]] (pre-midsem) and [[CG_Endsem_Notes]] (post-midsem); the authority for topic order is [[CG_Syllabus]]. Notation follows [[CG_context]] §9: inline `$...$`, display `$$...$$`, matrices in `\begin{bmatrix}...\end{bmatrix}`, homogeneous points as $[x\;y\;z\;1]^T$.

---

## Pre-Midsem — 8 topics + bridge

### 1. Introduction to Computer Graphics

*Deck: [[Pre 1 - Introduction to Computer Graphics.pdf|Pre 1]].*

| Quantity | Expression | Notes |
| --- | --- | --- |
| Camera-relative point | $\mathbf{p}=\mathbf{A}-\mathbf{c}$ | subtract the camera position from the world point |
| Perspective divide (this deck) | $u=\dfrac{x}{z},\quad v=\dfrac{y}{z}$ | camera at $\mathbf{c}=(2,3,5)$; here $z<0$, so the result is positive |
| Worked value | $\mathbf{A}=(1,1,1),\ \mathbf{c}=(2,3,5)\Rightarrow \mathbf{p}=(-1,-2,-4)\Rightarrow \mathbf{q}=\left(\tfrac14,\tfrac12\right)$ | the projection is repeated for all eight cube vertices |

### 2. Digital Information and Digital Images

*Deck: [[Pre 2 - Digital Information and Digital Images.pdf|Pre 2]].*

| Quantity | Expression | Notes |
| --- | --- | --- |
| Camera space, aligned axes | $\mathbf{p}=V-\mathbf{c}$ | valid only because camera axes are parallel to world axes |
| Camera space, rotated camera | $\mathbf{p}=R\,(V-\mathbf{c})$ | apply the rotation $R$ **before** the perspective divide |
| Normalized perspective projection | $u=-\dfrac{x}{z},\quad v=-\dfrac{y}{z}$ | camera looks down $-z$; $-z$ viewing convention |
| Worked value | $C=(1,0,1),\ \mathbf{c}=(2,-1,5)\Rightarrow\mathbf{p}=(-1,1,-4)\Rightarrow\mathbf{q}=(-0.25,0.25)$ | larger $\lvert z\rvert$ projects closer to the image centre |

> [!warning] Two projection sign conventions
> Pre 1 uses $u=x/z,\ v=y/z$ with the camera at $(2,3,5)$; Pre 2 uses $u=-x/z,\ v=-y/z$ with the camera looking along $-z$. Both give the correct picture — keep the deck's convention when reproducing its numbers.

### 3. Line Drawing Algorithms

*Decks: [[Pre 3 - Line Drawing Algorithms (6 Aug).pdf|Pre 3 (6 Aug)]] and [[Pre 3 - Line Drawing Algorithms (10 Aug).pdf|Pre 3 (10 Aug)]].*

| Quantity | Expression | Notes |
| --- | --- | --- |
| Line slope | $m=\dfrac{\Delta y}{\Delta x}=\dfrac{y_1-y_0}{x_1-x_0}$ | the dominant axis is the one with the larger absolute change |
| DDA, $\lvert m\rvert\le 1$ | $x\leftarrow x+1,\quad y\leftarrow y+m$ | advance $x$ by one pixel; avoids gaps along $x$ |
| DDA, $\lvert m\rvert>1$ | $y\leftarrow y+1,\quad x\leftarrow x+\dfrac{1}{m}$ | advance $y$ by one pixel; avoids gaps along $y$ |
| Circle function | $f(x,y)=x^2+y^2-r^2$ | sign of $f$ decides inside/outside |
| Midpoint test point | $(x_k+1,\;y_k-\tfrac12)$ | midpoint between the two candidate pixels $(x_k+1,y_k)$ and $(x_k+1,y_k-1)$ |
| Decision variable | $p_k=f(x_k+1,\;y_k-\tfrac12)=(x_k+1)^2+(y_k-\tfrac12)^2-r^2$ | $p_k<0$ → midpoint inside → choose upper; $p_k\ge0$ → lower |
| Midpoint circle — start | $x_0=0,\quad y_0=\mathrm{round}(r),\quad p_0=\dfrac54-r$ | the centre is assumed at the origin |
| Midpoint circle — update | $p<0:\ p_{k+1}=p_k+2x_k+3$ · $p\ge0:\ p_{k+1}=p_k+2(x_k-y_k)+5,\ y\leftarrow y-1$ | always $x\leftarrow x+1$ |
| Stop condition | $x\ge y$ | only the octant $x\le y$ is computed |
| Eight-way symmetry | $(x,y),(y,x),(y,-x),(x,-y),(-x,-y),(-y,-x),(-y,x),(-x,y)$ | mirror the one octant into all eight |
| Off-centre circle | plot $(x_c+x,\;y_c+y)$ | translate **at plot time**; $p_0,p_1,\dots$ never change |
| Midpoint line — start | $d_0=2a+b=2\Delta y-\Delta x$, with $a=\Delta y,\ b=-\Delta x$ | used again in the Gupta–Sproull deck (§Post 8) |
| Midpoint line — update | E: $d\mathrel{+}=2a=2\Delta y$ · NE: $d\mathrel{+}=2(a+b)=2(\Delta y-\Delta x)$ | $d>0$ ⇒ NE; $d\le0$ ⇒ E |

> [!note] The deck's own numeric caution
> For $r=2.7$, $p_0=\tfrac54-r=1.25-2.7=-1.45$ (the deck explicitly warns it is **not** $-1.05$); the trace then runs $p_0=-1.45,\ p_1=1.55,\ p_2=2.55$.

### 4. Object Representation

*Deck: [[Pre 4 - Object Representation.pdf|Pre 4]].*

| Quantity | Expression | Notes |
| --- | --- | --- |
| Implicit surface | $f(x,y,z)=0$ | $f=0$ on the boundary; $f<0$ and $f>0$ classify the two sides |
| Sphere (implicit) | $x^2+y^2+z^2-r^2=0$ | a quadric = second-degree implicit surface |
| Parametric surface | $Q(u,v)=(x(u,v),\,y(u,v),\,z(u,v))$ | two parameters; generates surface points directly |
| Parametric curve | $P(t)=(x(t),\,y(t),\,z(t))$ | $t$ is a parameter, not necessarily arc length |
| Tangent vector | $P'(t)=\dfrac{dP}{dt}$ | derivative gives the local direction of the curve |
| Straight line (linear blend) | $P(t)=(1-t)P_0+tP_1,\quad 0\le t\le1$ | the simplest blending equation |
| Cubic polynomial curve | $f(u)=a_0+a_1u+a_2u^2+a_3u^3,\quad 0\le u\le1$ | four coefficients, four constraints |
| Power/matrix form | $P(t)=T\,A,\quad T=[\,1\;t\;t^2\;t^3\,],\quad A=[\,a_0\;a_1\;a_2\;a_3\,]^T$ | one $A$ per coordinate $x,y,z$ |
| General spline matrix form | $P(t)=T\,M\,G$ | $T$ = parameter powers, $M$ = basis matrix (chooses Hermite/Bézier/B-spline), $G$ = geometry/control vector |
| Blending functions | $B=T\,M,\qquad P(t)=\sum_i B_i(t)P_i$ | $B_i(t)$ is how much control point $P_i$ contributes |
| Hermite geometry vector | $G=[\,p_0\;p_1\;p_2\;p_3\,]^T$ | $p_0$ start position, $p_1$ start tangent, $p_2$ end position, $p_3$ end tangent |
| Hermite constraints | $f(0)=p_0,\ f'(0)=p_1,\ f(1)=p_2,\ f'(1)=p_3$ | positions decide where; tangents decide how |
| Hermite constraint matrix | $C_H=\begin{bmatrix}1&0&0&0\\0&1&0&0\\1&1&1&1\\0&1&2&3\end{bmatrix},\quad P=C_H A\Rightarrow A=C_H^{-1}P$ | rows are the four constraints in order |
| Hermite coefficients | $a_0=p_0,\ a_1=p_1,\ a_2=-3p_0-2p_1+3p_2-p_3,\ a_3=2p_0+p_1-2p_2+p_3$ | solve the easy two first, then the $2\times2$ system |
| Hermite basis matrix | $B_H=\begin{bmatrix}1&0&0&0\\0&1&0&0\\-3&-2&3&-1\\2&1&-2&1\end{bmatrix},\quad f(u)=U B_H P$ | $U=[\,1\;u\;u^2\;u^3\,]$; $B_H$ is fixed for every segment |
| Hermite blending functions | $h_0=2u^3-3u^2+1,\ h_1=u^3-2u^2+u,\ h_2=-2u^3+3u^2,\ h_3=u^3-u^2$ | $f=h_0p_0+h_1p_1+h_2p_2+h_3p_3$; $h_1,h_3$ vanish at both ends |
| Cardinal tangent scale | $S=\dfrac{1-\tau}{2},\qquad 0\le\tau\le1$ | $\tau$ = tension; larger $\tau$ ⇒ smaller tangents |
| Cardinal tangents | $f'(0)=S(p_2-p_0),\qquad f'(1)=S(p_3-p_1)$ | segment runs $p_1\to p_2$; $p_0,p_3$ estimate tangents only |
| Cardinal coefficients | $a_0=p_1,\ a_1=-Sp_0+Sp_2,\ a_2=2Sp_0+(S-3)p_1+(3-2S)p_2-Sp_3,\ a_3=-Sp_0+(2-S)p_1+(S-2)p_2+Sp_3$ | Hermite coefficients with the tangents substituted |
| Cardinal basis matrix | $B_C=\begin{bmatrix}0&1&0&0\\-S&0&S&0\\2S&S-3&3-2S&-S\\-S&2-S&S-2&S\end{bmatrix}$ | $f(u)=U B_C P$, $P=[\,p_0\;p_1\;p_2\;p_3\,]^T$ |
| Catmull–Rom special case | $\tau=0\Rightarrow S=\tfrac12$ | centred-difference tangents; no manual tangent input |

**Continuity at a join** (C = parametric, G = geometric):

| Level | Condition |
| --- | --- |
| $C^0$ | segments meet: end of first = start of second; no gap, possible corner |
| $C^1$ | first derivatives (tangent vectors) equal — direction **and** magnitude |
| $C^2$ | first and second derivatives equal; natural cubic splines enforce this at interior knots |
| $G^0$ | segments meet (same as $C^0$) |
| $G^1$ | tangent **directions** match; magnitudes may differ |
| $G^2$ | tangent directions and curvature match |

> [!tip] Family recall
> Interpolating (passes through points): natural cubic, Hermite, Cardinal, Catmull–Rom. Approximating (guided by control points): Bézier, B-spline, NURBS.

### 5. B-Splines

*Deck: [[Pre 5 - B-Splines.pdf|Pre 5]].*

| Quantity | Expression | Notes |
| --- | --- | --- |
| B-spline curve | $C(t)=\sum_{i=0}^{n} P_i N_{i,p}(t)$ | $P_i$ control points, $N_{i,p}$ basis functions, $p$ degree |
| Order vs degree | $k=p+1$ | $p=0$ step, $p=1$ linear, $p=2$ quadratic, $p=3$ cubic (used throughout) |
| Knot count | highest index $m=n+p+1$; number of knots $=n+p+2$ | for $n+1$ control points and degree $p$ |
| Local support | $N_{i,p}(t)\ne0$ only on $[\,t_i,\;t_{i+p+1}\,)$ | outside it $N_{i,p}=0$, giving local control |
| Curve domain (non-clamped) | $t\in[\,t_p,\;t_{n+1}\,)$ | largest region where $p+1$ basis functions overlap |
| Partition of unity | $\sum_i N_{i,p}(t)=1$ | keeps $C(t)$ a genuine weighted average inside the convex hull |
| Cox–de Boor, degree 0 | $N_{i,0}(t)=\begin{cases}1,&t_i\le t<t_{i+1}\\0,&\text{otherwise}\end{cases}$ | half-open interval avoids double-counting at knots |
| Cox–de Boor, degree $p\ge1$ | $N_{i,p}(t)=\dfrac{t-t_i}{t_{i+p}-t_i}N_{i,p-1}(t)+\dfrac{t_{i+p+1}-t}{t_{i+p+1}-t_{i+1}}N_{i+1,p-1}(t)$ | rising weight on the left term, falling weight on the right; $0/0:=0$ |
| Linear uniform basis | $N_{i,1}$ triangular support $[\,t_i,t_{i+2}\,)$, peak $1$ at $t_{i+1}$ | e.g. $t_i=i+1$: $N_{0,1}$ on $[1,3)$ peaks at $2$ |
| Linear curve piece | on $[\,2,3):\ C(t)=P_0(3-t)+P_1(t-2)$ | each piece blends exactly two neighbouring points |
| NURBS curve | $C(t)=\dfrac{\sum_i P_i w_i N_{i,p}(t)}{\sum_i w_i N_{i,p}(t)},\qquad w_i>0$ | rational form; equal weights reduce it to an ordinary B-spline; enables exact conics |
| Spline surface | $S(u,v)=\sum_i\sum_j P_{ij}\,b_i(u)\,b_j(v)$ | tensor product; $P_{ij}$ is the control net |
| Bézier surface | $S(u,v)=U\,M\,P\,M^T V^T$ | $U=[\,u^2\;u\;1\,]$, $V=[\,v^2\;v\;1\,]^T$, $M$ the quadratic Bernstein basis matrix; repeat per coordinate $x,y,z$ |
| Quadratic Bernstein functions | $B_{0,2}=(1-u)^2,\quad B_{1,2}=2u(1-u),\quad B_{2,2}=u^2$ | same functions in $u$ and $v$ |

> [!note] The three well-behaved properties
> **Local support** (distant points have no effect), **non-negativity** ($N_{i,p}(t)\ge0$), **partition of unity** ($\sum_i N_{i,p}=1$). Bézier has *global* control and no knot vector; B-spline/NURBS have *local* control and a knot vector.

### 6. 2D Modelling and Composite Transformations

*Decks: [[Pre 6 - 2D Modelling and Composite Transformations (31 Aug).pdf|Pre 6 (31 Aug)]] (2D) and [[Pre 6 - 2D Modelling and Composite Transformations (3 Sep).pdf|Pre 6 (3 Sep)]] (3D).*

**2D linear maps** — point as a column vector, $P'=MP$:

| Quantity | Expression | Notes |
| --- | --- | --- |
| General linear map | $\begin{bmatrix}x'\\y'\end{bmatrix}=\begin{bmatrix}a_{11}&a_{12}\\a_{21}&a_{22}\end{bmatrix}\begin{bmatrix}x\\y\end{bmatrix}$ | rotation, scaling, shear, reflection; **not** translation |
| Scaling | $x'=s_xx,\ y'=s_yy$; $S=\begin{bmatrix}s_x&0\\0&s_y\end{bmatrix}$ | about the origin unless a fixed point is given |
| Reflection | $s_x=-1$ (about $y$-axis), $s_y=-1$ (about $x$-axis), $(-1,-1)$ (origin) | negative scaling |
| Rotation | $x'=x\cos\theta-y\sin\theta,\ y'=x\sin\theta+y\cos\theta$; $R=\begin{bmatrix}\cos\theta&-\sin\theta\\\sin\theta&\cos\theta\end{bmatrix}$ | $\cos^2\theta+\sin^2\theta=1$ ⇒ rigid; $\theta>0$ CCW |
| Special angles | $90^\circ:(x,y)\to(-y,x)$ · $180^\circ:(-x,-y)$ · $270^\circ:(y,-x)$ | no trig needed |
| Shear | $x'=x+sh_xy,\ y'=y$ (horizontal); $x'=x,\ y'=y+sh_yx$ (vertical); $Sh=\begin{bmatrix}1&sh_x\\sh_y&1\end{bmatrix}$ | diagonal stays $1$; $sh=\tan\theta$ of the tilt angle |

**Homogeneous form** — one $3\times3$ matrix for every affine map:

| Quantity | Expression | Notes |
| --- | --- | --- |
| Homogeneous point | $P_h=(x_h,y_h,h)$, usually $h=1$ | recover $(x'_h/h',\,y'_h/h')$; $h=0$ is a direction vector |
| Translation | $T=\begin{bmatrix}1&0&t_x\\0&1&t_y\\0&0&1\end{bmatrix}$ | bottom row keeps $h=1$ |
| Scaling | $S=\begin{bmatrix}s_x&0&0\\0&s_y&0\\0&0&1\end{bmatrix}$ | — |
| Rotation | $R=\begin{bmatrix}\cos\theta&-\sin\theta&0\\\sin\theta&\cos\theta&0\\0&0&1\end{bmatrix}$ | — |
| Shear | $Sh=\begin{bmatrix}1&sh_x&0\\sh_y&1&0\\0&0&1\end{bmatrix}$ | — |
| Composite | $M=M_k\cdots M_2M_1$ | rightmost acts first (column vectors); $M_1M_2\ne M_2M_1$ |
| About a fixed point $F$ | $M=T(F)\cdot(\text{transform})\cdot T(-F)$ | check $M\cdot F=F$ |
| Dimension rule | $N\times N\to(N+1)\times(N+1)$ | 3D therefore uses $4\times4$ matrices |

**3D extension** — $P=[\,x\;y\;z\;1\,]^T$:

| Quantity | Expression | Notes |
| --- | --- | --- |
| Translation / Scaling | $T=\begin{bmatrix}1&0&0&t_x\\0&1&0&t_y\\0&0&1&t_z\\0&0&0&1\end{bmatrix}$, $S=\operatorname{diag}(s_x,s_y,s_z,1)$ | the $z$-row and $t_z$ column are the only new parts |
| General shear | $\begin{aligned}x'&=x+sh_{xy}y+sh_{xz}z\\ y'&=sh_{yx}x+y+sh_{yz}z\\ z'&=sh_{zx}x+sh_{zy}y+z\end{aligned}$ | six shear factors; subscript $sh_{\text{changed},\text{source}}$ |
| Rotation about $x$ | $R_x=\begin{bmatrix}1&0&0&0\\0&\cos\theta&-\sin\theta&0\\0&\sin\theta&\cos\theta&0\\0&0&0&1\end{bmatrix}$ | $y'=y\cos\theta-z\sin\theta$, $z'=y\sin\theta+z\cos\theta$ |
| Rotation about $y$ | $R_y=\begin{bmatrix}\cos\theta&0&\sin\theta&0\\0&1&0&0\\-\sin\theta&0&\cos\theta&0\\0&0&0&1\end{bmatrix}$ | $x'=x\cos\theta+z\sin\theta$, $z'=-x\sin\theta+z\cos\theta$ (uses the pair $(z,x)$) |
| Rotation about $z$ | $R_z=\begin{bmatrix}\cos\theta&-\sin\theta&0&0\\\sin\theta&\cos\theta&0&0\\0&0&1&0\\0&0&0&1\end{bmatrix}$ | the 2D matrix lifted into 3D |
| Inverse rotation | $R^{-1}(\phi)=R(-\phi)=R^T(\phi)$ | transpose = inverse for rotations |
| Arbitrary-axis alignment | $d=\sqrt{b^2+c^2},\ L=\sqrt{a^2+b^2+c^2}$; $\cos\alpha=\tfrac{c}{d},\ \sin\alpha=\tfrac{b}{d}$; $\cos\beta=\tfrac{d}{L},\ \sin\beta=-\tfrac{a}{L}$ | $(a,b,c)$ is the axis direction after moving $P_2$ to the origin |
| Arbitrary-axis rotation | $M=T(P_2)\,R_x(-\alpha)\,R_y(-\beta)\,R_z(\theta)\,R_y(\beta)\,R_x(\alpha)\,T(-P_2)$ | transform → operate → inverse transform (conjugation) |

> [!warning] Right-hand rule
> Point the right thumb along the positive axis; curled fingers give the positive rotation direction. Right-handed frame: $x\times y=z$.

### 7. Reflection Models and Phong Illumination

*Deck: [[Pre 7 - Reflection Models and Phong Illumination.pdf|Pre 7]].*

| Quantity | Expression | Notes |
| --- | --- | --- |
| Unit vectors | $\mathbf{N}$ normal, $\mathbf{L}=\dfrac{S-P}{\lVert S-P\rVert}$ to light, $\mathbf{V}=\dfrac{E-P}{\lVert E-P\rVert}$ to eye, $\mathbf{R}=2(\mathbf{N}\cdot\mathbf{L})\mathbf{N}-\mathbf{L}$ | $P$ surface point, $S$ light, $E$ eye |
| Lambert factor | $\cos\theta=\mathbf{N}\cdot\mathbf{L}$ | unit vectors; $\theta=90^\circ$ ⇒ zero diffuse |
| Ambient | $I_{amb}=k_aI_a$ | independent of light/viewer direction; never attenuated |
| Diffuse (Lambert) | $I_{diff}=k_d I_L\,\max(0,\mathbf{N}\cdot\mathbf{L})$ | clamp stops negative "light" when the source is behind |
| Specular (Phong) | $I_{spec}=k_s I_L\,[\max(0,\mathbf{R}\cdot\mathbf{V})]^{n_s}$ | $\cos\alpha=\mathbf{R}\cdot\mathbf{V}$; $n_s$ = shininess |
| Full Phong, one light | $I_P=k_aI_a+k_dI_L(\mathbf{N}\cdot\mathbf{L})+k_sI_L(\mathbf{R}\cdot\mathbf{V})^{n_s}$ | evaluate direct terms only when $\mathbf{N}\cdot\mathbf{L}>0$; empirical — $k_a+k_d+k_s$ need not equal $1$ |
| Shininess effect | $0<x<1:\ x^{n_s}$ shrinks as $n_s\uparrow$ | narrows the highlight, does not change its peak |
| Radial attenuation | $AF_{rad}(d)=\dfrac{1}{a_0+a_1d+a_2d^2},\qquad d=\lVert S-P\rVert$ | $a_2=1,a_0=a_1=0$ gives pure inverse-square |
| Spot angle | $\cos\phi=\mathbf{D}\cdot\mathbf{Q},\quad \mathbf{Q}=\dfrac{P-S}{\lVert P-S\rVert}=-\mathbf{L}$ | $\mathbf{D}$ = spotlight central direction |
| Angular attenuation | $AF_{ang}=(\cos\phi)^m$ if $\phi\le\phi_c$, else $0$ | $\phi_c$ decides *if* lit; $m$ decides *how brightly* |
| Light-type factors | Ambient $(—,—)$; Directional $(1,1)$; Point $\left(\tfrac{1}{a_0+a_1d+a_2d^2},1\right)$; Spotlight $\left(\tfrac{1}{a_0+a_1d+a_2d^2},(\cos\phi)^m\right)$ | $(AF_{rad},AF_{ang})$ |
| Coloured light | $\mathbf{I}=(I_R,I_G,I_B),\quad \mathbf{k}=(k_R,k_G,k_B)$ | evaluate the equation independently per channel |
| Hadamard product | $\mathbf{k}\odot\mathbf{I}=(k_RI_R,\ k_GI_G,\ k_BI_B)$ | component-wise; result is an RGB vector, **not** a dot product |
| Multi-light coloured | $\mathbf{I}_P=k_a\odot I_a+\sum_j AF_j\Big[(\mathbf{k}_d\odot\mathbf{I}_{L,j})c_{d,j}+(\mathbf{k}_s\odot\mathbf{I}_{L,j})c_{s,j}\Big]$ | $AF_j=AF_{rad,j}AF_{ang,j}$; ambient added once; $c_{d,j}=\max(0,\mathbf{N}\cdot\mathbf{L}_j)$; $c_{s,j}=[\max(0,\mathbf{R}_j\cdot\mathbf{V})]^{n_s}$; $c_{s,j}=0$ when $\mathbf{N}\cdot\mathbf{L}_j\le0$ |

### 8. Practice Problems

*Deck: [[Pre 8 - Practice Problems.pdf|Pre 8]] — Phong / Gouraud / flat shading drills.*

| Quantity | Expression | Notes |
| --- | --- | --- |
| Linear interpolation of intensity | $I(t)=(1-t)I_A+tI_B$ | $t$ = fraction from $B$ toward $A$; nearer endpoint gets more weight |
| Deck example | point $40\%$ of the way from $V_2$ to $V_1$: $I_4=0.6I_2+0.4I_1$ | — |
| Gouraud shading | two interpolation stages: **along edges**, then **across scanlines** | vertex intensities only |
| Incremental interpolation | $I_{\text{next}}=I_{\text{prev}}+\Delta I$, with $\Delta I$ precomputed per edge/scanline | replaces per-pixel multiplication/division with one addition |
| Flat shading | one intensity for the whole face | lighting evaluated once per polygon |
| Phong shading | interpolate $\mathbf{N}$ per pixel, then evaluate illumination there | smooth highlights; heavier than Gouraud |

> [!warning] Gouraud limitations
> A narrow specular highlight inside a face can be missed entirely; interpolation dims and blurs it, and can create **Mach bands** (stripes where the rate of intensity change shifts).

### Bridge — Intensity Quantization (17 Sep)

*Deck: [[Between - Intensity Quantization (17 Sep).pdf|Between]].*

| Quantity | Expression | Notes |
| --- | --- | --- |
| Number of codes | $M=2^b$ | $b$ bits ⇒ codes indexed $0$ to $M-1$ |
| Quantization error | $\text{error}=\text{computed intensity}-\text{selected device level}$ | choose the nearest supported level when storing a pixel |
| Texture domain | projected: 2D image · texture mapping: $(u,v)$ parameter space · solid texturing: 3D $(u,v,w)$ | methods differ by where the texture is defined |

---

## Post-Midsem — 9 topics

*These rows are the curated Formula Summary of [[CG_Endsem_Notes]], regrouped by topic. Full derivations and traces live in that note.*

### 1. 3D Viewing Transformation and Camera Setup

| Quantity | Expression | Notes |
| --- | --- | --- |
| Camera basis | $\mathbf{n}=\dfrac{\mathbf{o}-\mathbf{l}}{\lVert\mathbf{o}-\mathbf{l}\rVert},\ \mathbf{u}=\dfrac{\mathbf{v}_{up}\times\mathbf{n}}{\lVert\cdot\rVert},\ \mathbf{v}=\mathbf{n}\times\mathbf{u}$ | right-handed; $\mathbf{n}$ points *behind* the camera |
| View matrix | $M_{view}=\mathbf{R}\,T(-\mathbf{o})$ | translation first for column vectors |

### 2. 3D Viewing, Camera and Projection Fundamentals

| Quantity | Expression | Notes |
| --- | --- | --- |
| Orthographic matrix | $M_{ortho}$ with $\dfrac{2}{x_{\max}-x_{\min}}$ and $\dfrac{-2}{z_{far}-z_{near}}$ | $z$ row negated because the camera looks down $-z$ |
| Perspective matrix | $M_{persp}$, fourth row $(0,0,-1,0)$ | sets $w=-z_{cam}$; requires $z<0$ |
| Viewport map | $V_x=s_xW_x+t_x,\quad V_y=s_yW_y+t_y$ | $s=\Delta V/\Delta W$; $y$-flip needs $s_y<0$ |

### 3. Viewport Mapping and Cohen–Sutherland Clipping

| Quantity | Expression | Notes |
| --- | --- | --- |
| Point inside window | $x_{\min}\le x\le x_{\max}$ AND $y_{\min}\le y\le y_{\max}$ | ties count as inside |
| Line parametric form | $P(t)=P_0+t(P_1-P_0),\quad 0\le t\le1$ | all clipping solves for $t$ |
| Intersection with $x=x_{\min}$ | $t=\dfrac{x_{\min}-x_0}{x_1-x_0}$ | denominator $0$ ⇒ parallel to the plane; same pattern for all six planes |
| Outcode order | `Far Near Top Bottom Right Left` | bit 5 … bit 0 |
| Trivial decisions | OR $=0$ accept · AND $\ne0$ reject | otherwise clip |

### 4. Polygon and 3D Fill-Area Clipping

| Quantity | Expression | Notes |
| --- | --- | --- |
| Edge–plane intersection | $t=\dfrac{x_{plane}-x_0}{x_1-x_0}$ (or the $y$/$z$ analogue) | one of the four Sutherland–Hodgman cases decides whether to append |
| Half-plane test | inside if $x\ge x_{\min}$ etc. | window as four half-planes; ties inside |
| Bounding-box reject | reject before exact clipping when bboxes do not overlap | cheap first rejection test |

### 5. Hidden Surface Removal I — Back-Face Elimination and the Z-Buffer

| Quantity | Expression | Notes |
| --- | --- | --- |
| Face normal | $\mathbf{N}=(B-A)\times(C-A)$ | outward if vertices are counterclockwise seen from outside |
| Front/back test | $\mathbf{N}\cdot\mathbf{v}<0$ front, $>0$ back | for $\mathbf{v}=(0,0,-1)$: $\mathbf{N}\cdot\mathbf{v}=-N_z$ |
| Plane from a face | $Ax+By+Cz+D=0,\ \mathbf{N}=(A,B,C),\ D=-Ax_1-By_1-Cz_1$ | $C\ne0$ required for the depth solve |
| Depth from the plane | $z=\dfrac{-D-Ax-By}{C}$ | $z$ grows inward (farther) |
| Incremental depth | $\Delta z_x=-\dfrac{A}{C},\quad \Delta z_y=+\dfrac{B}{C}$ | one add per pixel |

### 6. Hidden Surface Removal II — Painter's Algorithm and BSP Trees

| Quantity | Expression | Notes |
| --- | --- | --- |
| Plane side function | $f(\mathbf{r})=(\mathbf{r}-\mathbf{p})\cdot\mathbf{n}$ | $>0$ OUT, $<0$ IN, $=0$ on the plane |
| Split parameter | $t=\dfrac{f(\mathbf{u})}{f(\mathbf{u})-f(\mathbf{v})}$ | requires opposite signs, so $t\in(0,1)$ |
| BSP traversal | eye OUT: IN → node → OUT; eye IN: OUT → node → IN | one dot product per node |

### 7. Fill-Area Algorithms, Scan Conversion and the 3D Pipeline

| Quantity | Expression | Notes |
| --- | --- | --- |
| Edge slope reciprocal | $\dfrac{1}{m}=\dfrac{\Delta x}{\Delta y}=\dfrac{x_2-x_1}{y_2-y_1}$ | horizontal edges never enter the AET |
| Scan-line update | $x\leftarrow x+\dfrac{1}{m}$ | edge active for $y\in[\,y_{\min},y_{\max})$ |
| Span fill | fill $\lceil x_1\rceil\ldots\lfloor x_2\rfloor$ for sorted pairs | pairs 1–2, 3–4, … |
| Fill test | boundary fill: colour ≠ boundary AND ≠ fill; flood fill: colour = interior | mark on **push** |
| Bitmap storage | $5\times7=35$ bits → $10\times14=140$ at $\times2$ | on-pixels $11\to44$ |
| Outline area | $1\times7+5\times1-1=11$ units² | scales by $2^2=4$; area ≠ pixel count |

### 8. Anti-Aliasing I — The Gupta–Sproull Algorithm

| Quantity | Expression | Notes |
| --- | --- | --- |
| Midpoint start | $d_0=2a+b=2\Delta y-\Delta x$ | $a=\Delta y$, $b=-\Delta x$ |
| Midpoint updates | E: $d\mathrel{+}=2a$ · NE: $d\mathrel{+}=2(a+b)$ | $d>0$ ⇒ NE; $d\le0$ ⇒ E |
| Line length | $L=\sqrt{\Delta x^2+\Delta y^2}$ | computed once per line |
| Signed distance | $s=\dfrac{d+\Delta x}{2L}$ (E), $s=\dfrac{d-\Delta x}{2L}$ (NE) | use $d$ **before** the update |
| Neighbour distances | $D_{upper}=\left\lvert s-\dfrac{\Delta x}{L}\right\rvert,\quad D_{lower}=\left\lvert s+\dfrac{\Delta x}{L}\right\rvert$ | same for E and NE; only $s$ changes |
| Blend | $C=\alpha C_{line}+(1-\alpha)C_{bg}$ | $\alpha=\mathrm{Filter}(\lvert s\rvert)$, cone $=1-D$ |

### 9. Animation — The 2D Production Process

| Quantity | Expression | Notes |
| --- | --- | --- |
| In-between | $\mathbf{P}(t)=(1-t)\mathbf{K}_1+t\mathbf{K}_2$ | two keys, $t\in[0,1]$ |
| Eased in-between | $t'=3t^2-2t^3$ | pins $t'=0.5$ at $t=0.5$ |
| Jump height | $h(t)=4H\,t(1-t)$ | symmetric arc; apex at $t=0.5$ |

---

> [!tip] Last-minute recall
> Know the **assumptions** as well as the algebra: right-handed camera frame with the viewer on $-z$; ties counted as inside; $z$ increasing inward for the depth buffer; E chosen on $d\le0$ in the midpoint rules; $t\in(0,1)$ for a BSP split. The exam marks sit on the traces built from these formulas, not on the formulas alone.
