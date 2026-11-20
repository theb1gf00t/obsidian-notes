# Computer Graphics – Revision Notes (Posts 1–6)

Nov 21, 2026 · @Prabhav Sunia

## Post 1 – 3D viewing transformation and camera setup

Viewing changes the coordinate description of the scene, not the scene itself. Taking a photo means describing the world in the camera's own frame, set by camera position and orientation.

**Pipeline of spaces**

1. Object space (local coordinates) → *model transform* (translate, rotate, scale) →
2. World space → *view transform* (camera to origin, axes aligned) →
3. Camera / view / eye space → *projection + clipping* →
4. Canonical view volume (CVV, normalized cube −1 ≤ x, y, z ≤ 1) → *viewport transform* (scale and translate) →
5. Screen space (2D pixel coordinates).

In the full pipeline, the viewing stage covers: viewing transformation → clipping → hidden surface removal → projection transformation → window-to-viewport transformation. Scan conversion comes after it.

| Stage | Coordinates | Purpose |
| --- | --- | --- |
| Camera | World → camera | Put the camera at the origin and align the viewing axes |
| Projection | Camera → canonical | Map the visible 3D volume to a normalized volume |
| Viewport | Canonical → screen | Scale and translate to the display window |

After the camera transform, objects are still 3D and still have perspective depth. Projection comes next and works on camera-space coordinates.

**Setting up the view coordinate system (VC)**

Given: camera position **o**, look-at point **p**, and a view-up point **p\_up**. The VC basis vectors are called **u, v, n**.

1. n points opposite to the looking direction. Compute n = o − p, then normalize it.
2. eThe view-up vector is V\_up = p\_up − o. Normalize it to get v. (The up direction can instead be given directly as a vector.)
3. u is perpendicular to the plane spanned by v and n, so u = v × n. Both inputs are unit vectors, so no further normalization is needed.

```latex
\hat n = \frac{o - p}{|o - p|}, \qquad \hat v = \frac{V_{up}}{|V_{up}|}, \qquad \hat u = \hat v \times \hat n
```

**World-to-view matrix**

Goal: P' = M\_w2v · P. Two steps align VC with the world frame:

1. Translate the camera to the origin with T(−o), which subtracts o from every point. Orientation is unchanged.
2. Rotate with R, whose rows are u, v, n. Each row is a dot product with one camera axis. The axes are orthonormal, so lengths and angles are preserved.

With column vectors the translation acts first, so the composite is M\_w2v = R · T(−o).

```latex
T(-o)=\begin{bmatrix}1&0&0&-o_x\\0&1&0&-o_y\\0&0&1&-o_z\\0&0&0&1\end{bmatrix},\quad
R=\begin{bmatrix}u_x&u_y&u_z&0\\v_x&v_y&v_z&0\\n_x&n_y&n_z&0\\0&0&0&1\end{bmatrix}
```

```latex
M_{w2v}=R\,T(-o)=\begin{bmatrix}u_x&u_y&u_z&-\,u\cdot o\\v_x&v_y&v_z&-\,v\cdot o\\n_x&n_y&n_z&-\,n\cdot o\\0&0&0&1\end{bmatrix}
```

Each translation term is the negative projection of the camera position onto one camera axis. For example, m14 = u\_x(−o\_x) + u\_y(−o\_y) + u\_z(−o\_z) = −u·o.

**Worked example**

Square object with A(2,1,0), B(2,3,0), C(2,3,3), D(2,1,3). Camera o = (1,2,2). Look-at point p = (2,2,2), the object's centre. Up direction is +z.

- n = o − p = (−1, 0, 0).
- Up gives v = (0, 0, 1) directly. The slides then compute u = a × n = (0, −1, 0), where a is the up vector, and recheck v = n × u = (0, 0, 1).
- T uses o = (1,2,2), so its last column is (−1, −2, −2).
- R has rows u, v, n.

```latex
R=\begin{bmatrix}0&-1&0&0\\0&0&1&0\\-1&0&0&0\\0&0&0&1\end{bmatrix},\quad
M_{w2v}=R\,T=\begin{bmatrix}0&-1&0&2\\0&0&1&-2\\-1&0&0&1\\0&0&0&1\end{bmatrix}
```

Check: the look-at point P\_world = \[2,2,2,1\]ᵀ maps to P\_view = \[0, 0, −1, 1\]ᵀ. It sits one unit in front of the camera along −n.

**Projection: the idea**

- Projection maps n dimensions to n−1 dimensions. Here it is 3D to 2D.
- Objects are projected onto the **view plane**. The rectangular area on it that holds the projected objects is the **clipping window**.
- A 3D **view volume** is also defined. Objects inside it are projected, and everything else is discarded by clipping. The whole scene is not projected, which gives flexibility to synthesize images as wanted.
- **Projectors** are straight lines from each surface point to the view plane. Their intersections with the plane form the projected image.

|  | Parallel projection | Perspective projection |
| --- | --- | --- |
| Projectors | Stay parallel | Meet at the camera (centre of projection) |
| Size vs depth | Does not change with depth | Distant objects appear smaller (foreshortening) |
| Use | Measurement, CAD | Realistic depth cues |

The next step is deriving each projection matrix separately.

## Post 2 – 3D viewing: camera and projection fundamentals

**View volumes**

The projection model decides the shape of the 3D view volume. Both types have six clipping planes: left, right, bottom, top, near, far. The same camera position and direction can use either model.

|  | Orthographic / parallel | Perspective |
| --- | --- | --- |
| Volume | Rectangular box (parallelepiped) | Pyramid frustum; the tip is excluded, and near and far planes cut a section |
| Viewing rays | Parallel | Pass through one eye (centre of projection) |
| Effect | Width and height are constant with depth | Distant objects appear smaller |

The near plane is the view plane that holds the clipping window.

**Canonical view volume (CVV)**

- Clipping removes everything outside the view volume. Intersecting object surfaces with an arbitrary volume's boundaries is expensive.
- Instead, transform every view volume into one standard cube, −1 ≤ x′, y′, z′ ≤ 1, and clip against fixed planes: x′ = ±1, y′ = ±1, z′ = ±1 (all six faces).
- Normalization preserves inside versus outside.
- Parallel view volume → CVV: **scaling** only.
- Perspective frustum → parallel CVV: **shearing + scaling**, which is more complicated.

Projection of a world point P onto the view plane runs in this order: world → VC (T\_vc), then view volume → CVV (T\_cvv), then projection (T\_proj).

```latex
P' = T_{proj}\,T_{cvv}\,T_{vc}\,P
```

The original z (depth) of each point is kept in a separate **z-buffer** (depth buffer). It is needed later for hidden surface removal.

In this textbook, the camera looks along −z and the near/view plane is at z = −d with d > 0 (far plane at z = −f, f > d > 0). The clipping window sits on the near face. Window points are then mapped to the viewport. Projection is also done by matrix multiplication, in homogeneous coordinates.

**Parallel projection matrix**

A point P(x, y, z) projects to P′ on the near plane: x′ = x, y′ = y, z′ = −d.

```latex
T_{par}=\begin{bmatrix}1&0&0&0\\0&1&0&0\\0&0&0&-d\\0&0&0&1\end{bmatrix},\qquad
\begin{bmatrix}x''\\y''\\z''\\w\end{bmatrix}=T_{par}\begin{bmatrix}x\\y\\z\\1\end{bmatrix},\qquad x'=\tfrac{x''}{w},\ y'=\tfrac{y''}{w},\ z'=\tfrac{z''}{w}
```

For parallel projection w = 1, so the division changes nothing.

*Example 6.2.* The point from Post 1 is at (0, 0, −1) in view coordinates. Projecting on the plane z = −0.5 (d = 0.5) gives T\_par · \[0, 0, −1, 1\]ᵀ = \[0, 0, −0.5, 1\]ᵀ. The point lands at (0, 0, −0.5).

**Perspective projection matrix (similar triangles)**

P and P′ lie on the same ray from the eye. The distances are d and −z (note z < 0).

```latex
\frac{y}{y'}=\frac{-z}{d}\ \Rightarrow\ y'=\frac{-d\,y}{z},\qquad x'=\frac{-d\,x}{z},\qquad z'=-d
```

Check: a point on the view plane (z = −d) stays fixed, since x′ = x and y′ = y.

To write this as a matrix, put the division by z in the homogeneous factor, w = −z/d. Then divide by w.

```latex
T_{psp}=\begin{bmatrix}1&0&0&0\\0&1&0&0\\0&0&1&0\\0&0&-\tfrac1d&0\end{bmatrix},\qquad w=-\frac{z}{d},\qquad x'=\frac{x''}{w}=\frac{-dx}{z},\ \ y'=\frac{-dy}{z},\ \ z'=\frac{z''}{w}=-d
```

*Example 6.3.* Same point (0, 0, −1) with the view-coordinate origin as centre of projection and d = 0.5. Then T\_psp has −1/0.5 in row 4. T\_psp · \[0, 0, −1, 1\]ᵀ = \[0, 0, −1, 2\]ᵀ, so the homogeneous factor is w = 2. Dividing gives (0/2, 0/2, −1/2) = (0, 0, −0.5) on the view plane.

**Window and viewport**

- The clipping window is an abstract, intermediate concept. It is the (normalized) window in viewing space, and projected world-coordinate objects land on it.
- The viewport is defined in device (screen) space, with a position and size relative to the screen origin. The scene may not fill the whole screen.
- One more transformation moves points from window (VC) to viewport (DC). Window = what to show. Viewport = where and how large to show it.

**Window-to-viewport (W-V) transformation**

Keep the relative position of the point inside both rectangles. The window corners are (Wx1, Wy1) and (Wx2, Wy2). The viewport corners are (Vx1, Vy1) and (Vx2, Vy2).

```latex
\frac{W_x-W_{x1}}{W_{x2}-W_{x1}}=\frac{V_x-V_{x1}}{V_{x2}-V_{x1}}\ \Rightarrow\ V_x=s_xW_x+t_x,\quad s_x=\frac{V_{x2}-V_{x1}}{W_{x2}-W_{x1}},\ \ t_x=V_{x1}-s_xW_{x1}
```

```latex
V_y=s_yW_y+t_y,\quad s_y=\frac{V_{y2}-V_{y1}}{W_{y2}-W_{y1}},\ \ t_y=V_{y1}-s_yW_{y1}\qquad
T_{vp}=\begin{bmatrix}s_x&0&t_x\\0&s_y&t_y\\0&0&1\end{bmatrix}
```

Apply it as \[x″, y″, w\]ᵀ = T\_vp · \[x, y, 1\]ᵀ, then x′ = x″/w and y′ = y″/w. Each scale factor is viewport size divided by window size.

*Example.* The normalized window is \[−1, 1\] × \[−1, 1\] and the viewport corners are (4, 4) and (6, 8).

- s\_x = (6−4)/(1−(−1)) = 1 and t\_x = 4 − 1·(−1) = 5.
- s\_y = (8−4)/2 = 2 and t\_y = 4 − 2·(−1) = 6. Width stays the same and height doubles.
- The window centre (0, 0) maps to (5, 6), the viewport centre, which is ((4+6)/2, (4+8)/2).
- Corner checks: (−1, −1) → (4, 4) and (1, 1) → (6, 8).

## Post 3 – Clipping fundamentals and Cohen–Sutherland (2D and 3D)

**Point and line clipping basics**

- Point clipping: keep (x, y) if Wx\_min ≤ x ≤ Wx\_max **and** Wy\_min ≤ y ≤ Wy\_max. Otherwise clip it out.
- Line clipping is harder. Represent the segment by its endpoints and check their positions. Three cases arise:
  1. Both endpoints inside the window: don't clip.
  2. One endpoint inside, one outside: must clip.
  3. Both endpoints outside: can't tell whether the line is wholly or partly outside, so line–boundary intersections are needed.
- Computing line–boundary intersections for every line is expensive and may be impractical. Cohen–Sutherland is the better solution.

**2D Cohen–Sutherland**

The window and its surroundings are divided into **nine regions** by extending the window boundaries. Each region gets a unique 4-bit code, bit order Above, Below, Right, Left (bit 3 → bit 0). For example 1001 means above-left.

| Bit | Region | Set when | Function (1 if positive) | Value |
| --- | --- | --- | --- | --- |
| 3 | Above | y > ymax | sign(y − ymax) | 1000 |
| 2 | Below | y < ymin | sign(ymin − y) | 0100 |
| 1 | Right | x > xmax | sign(x − xmax) | 0010 |
| 0 | Left | x < xmin | sign(xmin − x) | 0001 |

An inside point has code 0000. Corner regions combine two bits (1001, 1010, 0101, 0110).

| Outcome | Outcode test | Action |
| --- | --- | --- |
| Trivial accept | code(P) = 0000 and code(Q) = 0000 | Keep the whole segment |
| Trivial reject | code(P) AND code(Q) ≠ 0000 (bitwise) | Discard the whole segment |
| Potential intersection | Neither succeeds | Clip an outside endpoint and repeat |

Why AND ≠ 0 rejects: a shared set bit means both points are outside the same boundary, on the same side (both above, both below, both right, or both left), so the line cannot touch the window. AND = 0 does not prove visibility. It only means the shortcut cannot reject yet.

**Algorithm (iterative)**

1. Compute the 4-bit codes of both endpoints.
2. Accept if both are 0000. Reject if the bitwise AND is nonzero.
3. Otherwise choose an endpoint whose code is nonzero.
4. Pick a boundary from one set bit of that code. The 2D examples test in the order above, below, right, left.
5. Find the intersection with that boundary, replace the endpoint by it, and recompute its code. Only one endpoint changes per iteration.
6. Repeat until the segment is accepted or rejected.

**2D examples** (window x, y ∈ \[2, 4\]; line equation from the two endpoints, y = mx + c)

- **Example 1: A(5,3), B(6,2).** A = 0010 and B = 0010. The first check fails (not both 0000). The AND is 0010 ≠ 0, so reject: both are right of the window.
- **Example 2: P(3,3), Q(5,2).** P = 0000, Q = 0010. The AND is 0000, so intersections are needed. The line is y = −0.5x + 4.5 (x + 2y − 9 = 0). Right boundary x = 4 gives Q′(4, 2.5), code 0000. Both codes are now 0000, so accept PQ′.
- **Example 3: M(1,3), N(5,2).** M = 0001, N = 0010. Both checks fail. The line is y = −x/4 + 13/4 (x + 4y − 13 = 0). Bits 3 and 2 agree, so there is no crossing of the above or below boundaries. Bit 1 differs, so the line crosses the right boundary. x = 4 gives N′(4, 9/4), code 0000. Discard N′N, so the segment becomes MN′. M still has code 0001, so check the left boundary: x = 2 gives M′(2, 11/4), code 0000. Discard MM′. Both ends are now 0000, so return M′N′ and stop.

**3D clipping**

- 2D clipping algorithms work in 3D with few modifications. Clipping is done against the normalized view volume, usually the symmetric cube with each coordinate in \[−1, 1\].
- 3D point clipping: keep (x, y, z) if −1 ≤ x ≤ 1 and −1 ≤ y ≤ 1 and −1 ≤ z ≤ 1.
- 3D Cohen–Sutherland has **27 regions** around the clipping box (near, middle and far layers of 3×3), so each endpoint gets a **6-bit outcode**. 000000 means inside or on the boundary. Convention here: depth z increases from near to far, with clipping volume xmin ≤ x ≤ xmax, ymin ≤ y ≤ ymax, zmin ≤ z ≤ zmax.

| Bit | Plane | Set when | Mask |
| --- | --- | --- | --- |
| 5 | Far | z > zmax | 100000 |
| 4 | Near | z < zmin | 010000 |
| 3 | Top | y > ymax | 001000 |
| 2 | Bottom | y < ymin | 000100 |
| 1 | Right | x > xmax | 000010 |
| 0 | Left | x < xmin | 000001 |

Order: Far Near Top Bottom Right Left. A point can set several bits, for example Far + Top + Right = 101010. Accept, reject and clip tests use bitwise OR and AND:

- C0 OR C1 = 000000 → **accept**.
- C0 AND C1 ≠ 000000 → **reject** (both outside the same plane).
- Otherwise **clip**. Choose an endpoint with a nonzero code and clip to one plane named by a set bit. Then recompute the code and repeat.

Parametric line and intersections: P(t) = P0 + t(P1 − P0), 0 ≤ t ≤ 1. Use the same t to update x, y and z. Set the clipped coordinate to the boundary value exactly.

| Bit | Plane | Boundary | t |
| --- | --- | --- | --- |
| 0 | Left | x = xmin | (xmin − x0)/(x1 − x0) |
| 1 | Right | x = xmax | (xmax − x0)/(x1 − x0) |
| 2 | Bottom | y = ymin | (ymin − y0)/(y1 − y0) |
| 3 | Top | y = ymax | (ymax − y0)/(y1 − y0) |
| 4 | Near | z = zmin | (zmin − z0)/(z1 − z0) |
| 5 | Far | z = zmax | (zmax − z0)/(z1 − z0) |

The denominator is never zero. We clip only at a bit set for one endpoint and clear for the other, so that coordinate differs between P0 and P1. The current segment is always an interval \[t\_start, t\_end\] ⊆ \[0, 1\] on the original line. Each pass moves one end inward. The plane order is arbitrary (the slides take the lowest set bit, bit 0 → bit 5, Left, Right, Bottom, Top, Near, Far). Any order gives the same answer, and a fixed order keeps the working predictable. A plane intersection can still lie outside the box, as pass 2 below shows.

**3D worked example.** Volume 0 ≤ x ≤ 6, 0 ≤ y ≤ 6, 0 ≤ z ≤ 8. A = (−4, 2, −2) and B = (8, 8, 10).

- C(A) = 010001 (Near, Left). C(B) = 101010 (Far, Top, Right).
- OR = 111011 ≠ 0 and AND = 000000, so clip. The direction is d = B − A = (12, 6, 12), so x = −4 + 12t, y = 2 + 6t, z = −2 + 12t.

| Pass | Endpoint (code) | Plane | t | New point | New code |
| --- | --- | --- | --- | --- | --- |
| 1 | A (010001) | Left x = 0 | 1/3 | A′ = (0, 4, 2) | 000000 |
| 2 | B (101010) | Right x = 6 | 5/6 | Q = (6, 7, 8) | 001000 |
| 3 | Q (001000) | Top y = 6 | 2/3 | B′ = (4, 6, 6) | 000000 |

After pass 3 both codes are 000000, so accept. The visible segment is (0, 4, 2) to (4, 6, 6), which is 1/3 ≤ t ≤ 2/3 on the original line. The Left clip also cleared Near, because z = 2 is inside \[0, 8\].

## Post 4 – Polygon and 3D fill-area clipping

Covers Sutherland–Hodgman, Weiler–Atherton, 3D point and face clipping, and an introduction to visibility. Theme: clip the region, not just its edges.

**Fill-area clipping basics**

- A polygon is an **ordered, closed vertex list** V = \[v1, v2, …, vn\]. Its edges are (v1,v2), …, (v(n−1),vn) plus the closing edge (vn,v1), which is processed even though v1 is not repeated.
- Clockwise or anticlockwise order is valid but must be consistent. A cyclic rotation is the same polygon.
- Clipping the edges separately cannot build the filled boundary. Input: a closed polygon and a window. Output: the part of the filled area inside the window, as closed ordered boundary(ies).
- New vertices are edge–boundary intersections, and sometimes window corners. New edges run along the window boundary.
- A rectangular window is the intersection of four half-planes:

| Clipper | Inside | Outside |
| --- | --- | --- |
| Left | x ≥ xmin | x < xmin |
| Right | x ≤ xmax | x > xmax |
| Bottom | y ≥ ymin | y < ymin |
| Top | y ≤ ymax | y > ymax |

**Sutherland–Hodgman (S–H)**

Clip the polygon against one boundary at a time. Each clipper's output list is the next clipper's input. For each edge S (current) → E (next), against one boundary:

| S | E | Append to output | Reason |
| --- | --- | --- | --- |
| Inside | Inside | E | Whole edge retained |
| Inside | Outside | I | Edge leaves at I |
| Outside | Inside | I, then E | Edge enters at I |
| Outside | Outside | nothing | Whole edge outside this half-plane |

Intersection: P(t) = S + t(E − S), 0 ≤ t ≤ 1.

- Vertical boundary x = b: t = (b − Sx)/(Ex − Sx), then y = Sy + t(Ey − Sy).
- Horizontal boundary y = b: t = (b − Sy)/(Ey − Sy), then x = Sx + t(Ex − Sx).
- I is computed only for an inside–outside transition, so the denominator is non-zero.
- A boundary endpoint gives t = 0 or 1, so merge duplicate vertices. Use consistent endpoint order and arithmetic to limit numerical discrepancies.

```python
for b in [left, right, top, bottom]:        # book order; result does not depend on it
    out = []                                 # fresh list each pass
    n = len(V)
    for i in range(n):                       # includes closing edge
        S = V[i]; E = V[(i+1) % n]
        if inside(S) and inside(E):   out.append(E)
        elif inside(S):               out.append(I(S, E, b))            # in -> out
        elif inside(E):               out.append(I(S, E, b)); out.append(E)  # out -> in
        # out -> out: append nothing
    V = out
    if not V: return []                      # empty stays empty
return V
```

*Symbolic example.* Triangle V = \[1, 2, 3\] anticlockwise. Vertex 1 is above the window, 2 is inside, 3 is to the right. Clip order: left, right, top, bottom.

- Left: every edge is in→in, so V = \[2, 3, 1\] ≡ \[1, 2, 3\], unchanged apart from a cyclic rotation.
- Right: 2→3 is in→out (I = 2′), 3→1 is out→in (I = 3′, then 1), 1→2 is in→in. V = \[2′, 3′, 1, 2\]. The new edge 2′→3′ lies on the window's right side.
- Top: 3′→1 is in→out (3″), 1→2 is out→in (1′, then 2). V = \[3′, 3″, 1′, 2, 2′\]. Note 3″ lies on the top edge, left of the corner. It is not the corner itself.
- Bottom: all vertices satisfy y ≥ ymin, so no change.
- Result: **five vertices**. 2′, 3′, 3″, 1′ are new and only vertex 2 survives from the original triangle.

*Numerical example.* Window 0 ≤ x ≤ 2 and 0 ≤ y ≤ 2. Subject 1 = (−1, 0), 2 = (3, 0), 3 = (1, 3), anticlockwise.

| Pass | Edges that cross | Intersections | Output list |
| --- | --- | --- | --- |
| Left (x ≥ 0) | 1→2 out→in; 3→1 in→out | 1′ = (0, 0) at t = 1/4; 2′ = (0, 3/2) at t = 1/2 | \[1′, 2, 3, 2′\] |
| Right (x ≤ 2) | 1′→2 in→out; 2→3 out→in | 3′ = (2, 0) at t = 2/3; 4′ = (2, 3/2) at t = 1/2 | \[3′, 4′, 3, 2′, 1′\] |
| Top (y ≤ 2) | 4′→3 in→out; 3→2′ out→in | 5′ = (5/3, 2) at t = 1/3; 6′ = (1/3, 2) at t = 2/3 | \[4′, 5′, 6′, 2′, 1′, 3′\] |
| Bottom (y ≥ 0) | none (1′ and 3′ lie on y = 0, which counts as inside) | none | \[5′, 6′, 2′, 1′, 3′, 4′\] |

Final V′ = \[1′, 3′, 4′, 5′, 6′, 2′\]. Three vertices in, six out. Vertices 1, 2, 3 are all removed and 1′ to 6′ are all new.

**S–H limitation.** A concave subject can split into pieces, but S–H returns one list. For a U-shaped polygon V = \[1..8\] clipped against y ≥ ymin, the output is \[2′, 3, 4, 4′, 6′, 7, 8, 8′\]. That is two separate pieces stored as one list, with overlapping boundary edges.

**Weiler–Atherton (W–A)**

Idea: walk the boundaries themselves. Trace the subject in its stored orientation. At an **exit** intersection switch to the window boundary. At an **entry** intersection switch back to the subject. Return to the start, then close and output the contour. Repeat from any unvisited entry. Each visible region becomes its own closed polygon, and it works for concave subjects and concave windows.

| Current event | Next boundary to follow |
| --- | --- |
| Start | Any unvisited entry intersection (or an inside subject vertex) |
| Exit intersection | Window boundary, same orientation |
| Entry intersection | Subject polygon boundary |
| Back at the contour's start | Close and output the contour |
| Unvisited entry remains | Begin another contour from it |

Window corners met while following the window boundary are output vertices too. Assumption: proper crossings only. Tangencies, shared edges and coincident vertices need extra rules.

*Example.* Subject \[1,2,3,4,5,6\] anticlockwise, with vertices 3 and 6 left of the window and a concave notch at 6 separating an upper and a lower lobe. The left boundary cuts four edges:

- (2,3) inside→outside: crossing 2′ is an exit.
- (3,4) outside→inside: 3′ is an entry.
- (5,6) inside→outside: 6′ is an exit.
- (6,1) outside→inside: 1′ is an entry.

Order along the window's left edge (anticlockwise ⇒ downward): 2′ exit, 1′ entry, 6′ exit, 3′ entry. Exits and entries alternate, so each exit leads to the next entry.

- Contour 1 (upper): subject 1 → 2 → exit 2′; window 2′ ↓ entry 1′; subject back to 1. Output \[1, 2, 2′, 1′\].
- Contour 2 (lower): search for the entry 3′; subject 3′ → 4 → 5 → exit 6′; window 6′ ↓ back to 3′. Output \[3′, 4, 5, 6′\].
- Together the two polygons are exactly subject ∩ window. S–H would give \[2, 2′, 3′, 4, 5, 6′, 1′, 1\], whose edges 2′→3′ and 6′→1′ overlap along the boundary.

| Aspect | Sutherland–Hodgman | Weiler–Atherton |
| --- | --- | --- |
| Operation | Successive half-plane passes | Linked boundary traversal |
| Subject polygon | Convex or concave | Convex or concave |
| Output | One vertex list | One list per visible region |
| Bookkeeping | Four inside/outside cases | Crossings, entry/exit labels, links |

**3D point and face clipping**

- The book's normalized volume is C = \[−1, 1\]³, bounded by six planes x = ±1, y = ±1, z = ±1. It is applied after the view volume has been normalized.
- A point is kept only if −1 ≤ x ≤ 1 **and** −1 ≤ y ≤ 1 **and** −1 ≤ z ≤ 1. One violated interval rejects it, and equalities are allowed.
- Exercise: A(0.4, −0.8, 0.2) is kept. B(1, 0, −1) is kept (it lies on a cube edge). C(1.2, 0.3, 0) is rejected (x > 1). D(0, −1.1, 1.3) is rejected (y < −1 and z > 1).
- A **polyhedron** is a 3D solid enclosed by flat polygonal faces. Clip it in three stages: a **bounding-box test** against the cube, then, if needed, **clip each face against the 6 planes** with the same half-space procedure (S–H).
  - Box entirely outside the cube: reject the whole object.
  - Box entirely inside: accept all faces, with no clipping.
  - Box overlap or touching is inconclusive, so clip each face. The box contains empty space, so overlap does not guarantee that the face overlaps.
- The bounding-box test is cheap because it compares coordinate bounds, so it may avoid exact clipping.

| Bounding box | Decision | Reason |
| --- | --- | --- |
| x ∈ \[1.2, 2\], y, z ∈ \[−0.5, 0.5\] | Reject | xmin = 1.2 > 1 |
| x ∈ \[0.5, 1.5\], y, z ∈ \[−0.5, 0.5\] | Continue | Partial overlap: clip faces |
| x ∈ \[1, 2\], y, z ∈ \[−0.5, 0.5\] | Continue | Touches x = 1 (xmin = 1 is not > 1) |
| All intervals inside \[−1, 1\] | Accept all | Object lies in its box, box lies in cube |

*3D face-clipping example.* Triangle A = (2, 0.5, 0), B = (0.5, 2, 0), C = (2, 2, 0) against the cube. All z = 0, so the cube section is the square −1 ≤ x, y ≤ 1 and a 2D picture is exact. The bounding box is x ∈ \[0.5, 2\], y ∈ \[0.5, 2\], z = 0. It overlaps the cube, so clip.

- Clip x ≤ 1: A is outside, B is inside, C is outside. A→B (out→in): t = 2/3, J = (1, 1.5, 0), append J, B. B→C (in→out): t = 1/3, K = (1, 2, 0), append K. C→A (out→out): nothing. Result \[J, B, K\]. The parameters 2/3 and 1/3 belong to different directed edges.
- Clip y ≤ 1: J (y = 1.5), B (y = 2) and K (y = 2) are all outside. Every edge is out→out, so the output is empty. Once empty, later planes cannot restore it.
- Answer: the triangle is completely outside the cube. The boxes overlapped only in empty box space, so disjoint boxes guarantee disjoint objects but overlapping boxes need a finer test.

**Visibility (intro to hidden surface removal)**

- **Clipping** removes geometry fully or partly outside the view volume. **Hidden surface removal (HSR)**, also called visible surface detection, removes surfaces inside the volume that are blocked by nearer surfaces.
- Two kinds of hiding: a face hidden by its own object (back faces) or by another object (A partly blocked by B).
- Objects that pass every clipping test can still be occluded. Only a comparison along the projectors finds the occluded part.
- Visibility is view dependent. A surface hidden from one viewpoint may be visible from another, so every answer assumes one viewing specification. The chapter fixes it: right-handed coordinates, viewer looking along −Z. Move the camera and the answer must be recomputed.
- At one image sample, a projector (ray) passes through it. Several surfaces may intersect that ray. Only surfaces whose projected polygon contains the sample compete (coverage). For opaque surfaces the nearest covered intersection wins (depth). If nothing covers it, the pixel gets the background colour. Example: with depths d = 2, 4, 7 for A, B, C, pixel p takes A's colour.

|  | Object space | Image space |
| --- | --- | --- |
| Works per | Geometric unit (object or face) | Pixel or sample |
| Method | For each object, find the parts not obstructed by itself or others, then render them | For each pixel, find the nearest object pierced by the projector, then draw that colour |
| Pros | Answer is geometry, device independent, valid at any resolution | Simple tests per candidate surface, easy to build in hardware |
| Cons | Comparisons, intersections and splitting are costly, suited to simpler scenes | Several surfaces may compete per sample, more pixels mean more sample tests |

Resolution: object-space output is an exact boundary, valid at any resolution. Image-space output is recomputed for every sample when resolution changes. In the slide example (one sample at each pixel centre, and a centre exactly on an edge counts as covered), a triangle covers 10 of 16 pixels at 4 × 4 and 21 of 64 at 8 × 8. With an open edge rule the counts would be 1 and 15 instead (the slide's figures for the two grids).

## Post 5 – Hidden surface removal I: back-face elimination and Z-buffer

**Why HSR?** Clipping removes things *outside* the view volume. Sometimes we must also remove things *inside* it that are blocked by other objects (object B partly hidden behind A). Clipping can't do this, so we use **hidden surface removal (HSR) / visible surface detection** methods. Visibility depends on the viewing direction. Assumptions: right-handed system, viewer looks along **−z**, objects have polygonal surfaces.

**Two families of HSR methods**

|  | Object-space | Image-space |
| --- | --- | --- |
| Idea | Compare objects / parts of objects with each other to find visible parts, then render them in object colour | For each pixel, find the closest object pierced by the projector through it, then colour the pixel |
| Works | **Before** projection (3D object level) | **After** projection and rasterisation (pixel level) |
| Pros | Device-independent, works at any resolution | Fewer computations |
| Cons | Step 1 is computation-heavy; can become infeasible for complex scenes; suits simple scenes with few objects | Depends on display resolution; changing resolution means recomputing pixel colours |

**Coherence** (reduces HSR cost by reusing results from nearby parts of the scene or image):

- **Object** – compare objects via simple circumscribing solids (sphere, cube); process further only if the solids overlap.
- **Face** – properties of one part of a surface apply to adjacent parts (a small surface with one invisible part is wholly invisible).
- **Edge** – an edge's visibility changes only where it crosses another edge; if one segment of a non-intersecting edge is visible, the whole edge is.
- **Scan line** – a segment visible on one scan line is likely visible on adjacent scan lines.
- **Depth** – depths of adjacent parts of the same surface are similar.
- **Frame** – pictures of the same scene at successive times are similar, except near edges of moving objects.

### Back-face elimination (object-space)

The simplest way to remove many hidden surfaces of polyhedra: detect and discard faces on the **back** side of an object with respect to the viewer. Culling back faces does not change what the viewer sees.

**Test.** With outward normal **N** and viewing vector **v** (viewer → object):

```latex
\mathbf{N}\cdot\mathbf{v}=|\mathbf{N}||\mathbf{v}|\cos\theta,\qquad \text{front-facing} \iff \mathbf{N}\cdot\mathbf{v}<0
```

**Shortcut for parallel viewing along −z:** v = (0, 0, −1). For N = (a, b, c), N·v = −c, where c = N\_z.

| c | N·v | Meaning | Action |
| --- | --- | --- | --- |
| c > 0 | < 0 | Front-facing | **RETAIN** |
| c < 0 | > 0 | Back-facing | **ELIMINATE** |
| c = 0 | = 0 | Edge-on (zero projected area) | – |

Repeat for every face. The c-shortcut only applies when viewing along −z. Roughly **half** of the faces of a scene are removed this way.

**Limitation.** It only handles self-hiding of faces. It ignores one object obscuring another, so other algorithms must be used alongside it.

**Example 1 – two triangles.** A(1,1,1), B(2,1,1), C(1,2,1); D(1,1,−1), E(1,2,−1), F(2,1,−1); v = (0,0,−1).

- Surface 1: AB = (1,0,0), AC = (0,1,0), **n₁ = AB × AC = (0,0,1)**, n₁·v = −1 < 0 → front-facing, **retain**.
- Surface 2: DE = (0,1,0), DF = (1,0,0), **n₂ = DE × DF = (0,0,−1)**, n₂·v = +1 > 0 → back-facing, **eliminate**.

**Example 2 – tetrahedron.** A(4,5,4), B(2,3,6), C(6,1,4), D(3,2,2); v = (0,0,−1). Outward (counter-clockwise from outside) face order: ABC, ADB, DCB, ACD. For each face N = (first edge) × (second edge), then N·v = −N\_z.

| Face | Edge vectors | N | N·v = −N\_z | Result |
| --- | --- | --- | --- | --- |
| ABC | AB = (−2,−2,2), AC = (2,−4,0) | (8, 4, 12) | −12 | **Retain** |
| ADB | AD = (−1,−3,−2), AB = (−2,−2,2) | (−10, 6, −4) | 4 | Eliminate |
| DCB | DC = (3,−1,2), DB = (−1,1,4) | (−6, −14, 2) | −2 | **Retain** |
| ACD | AC = (2,−4,0), AD = (−1,−3,−2) | (8, 4, −10) | 10 | Eliminate |

Visible surface: triangles **ABC** and **DCB**. Sanity check: N points outward if N·(vector from the face to the opposite vertex) < 0 (all four give −44).

### Depth (Z) buffer algorithm (image-space)

Resolves visibility by comparing depths **per pixel**. It handles overlapping objects (nearer surfaces hide farther ones) and does not depend on rendering order. It assumes canonical volumes, so depth lies in a normalised range, which lets the depth-buffer size (bits per pixel) be fixed.

**Buffers**

- **Depth buffer DB\[i\]\[j\]**: stores depth for each pixel. It is initialised to the maximum depth (**∞**, or 1.0 in normalised units).
- **Frame buffer FB\[i\]\[j\]**: stores colour. It is initialised to the **background colour**.

**Algorithm**

```
Initialise DB = max depth, FB = background colour
for each surface S:
    for each projected pixel (i, j) of S (from top-left):
        d = depth of S at (i, j)
        if d < DB[i][j]:           # nearer than what is stored
            DB[i][j] = d
            FB[i][j] = colour of S
```

**Depth from the plane equation.** Each surface lies on a plane:

```latex
ax+by+cz+d=0 \;\Rightarrow\; z=\frac{-ax-by-d}{c}
```

First pixel (i, j) on a scan line: z = (−ai − bj − d)/c.

**Iterative (incremental) depth – avoids recomputing the plane equation**

- **Along a scan line**, next pixel (x+1, y): z′ = z − a/c. The constant c₁ = −a/c is the depth change per pixel.
- **Down to the next scan line**, the left-edge x changes to x′ = x − 1/m for an edge of slope m (m ≠ 0). Substituting into the plane equation:

```latex
z'=\frac{-a\left(x-\tfrac{1}{m}\right)-b(y-1)-d}{c}=\;z+\frac{\tfrac{a}{m}+b}{c}
```

Constant c₂ = a/(c·m) + b/c is the depth change between scan lines at the edge. The a/(cm) term accounts for the x shift, and b/c accounts for the y shift. For a vertical edge (m = ∞) this reduces to z′ = z + b/c.

- **Moving diagonally** (next pixel on the next scan line): z″ = z′ − a/c.

**Iterative algorithm (simplified).** Input a, b, c, d. Start at the leftmost edge pixel on the top scan line with its z. For each scan line: set DB\[leftmost\]\[y\] = z, then for each pixel across the scan line do z = z + c₁ and store. After finishing the scan line, set the new left-edge z = z + c₂.

**Worked example.** Two triangles in a parallel-projected (CVV) view; projection just drops z.

- s₁: (0,0,6), (6,0,0), (0,6,0) → projected (0,0), (6,0), (0,6).
- s₂: (2,0,6), (6,0,6), (4,4,0) → projected (2,0), (6,0), (4,4).
- Colours: cl₁ for s₁, cl₂ for s₂, bg for background. s₁ is processed first, then s₂. Pixel of interest: **(3, 1)**. Initially DB\[3\]\[1\] = ∞ and FB\[3\]\[1\] = bg.

**Plane of s₁.** v₁ = (6,0,−6), v₂ = (0,6,−6), so n = v₁ × v₂ = (36, 36, 36). Using n·(P − P₀) = 0 with P₀ = (0,0,6): 36x + 36y + 36(z−6) = 0, which gives **x + y + z = 6** (a = b = c = 1).

**Plane of s₂.** v₁ = (4,0,0), v₂ = (2,4,−6), so n = (0, 24, 16). With P₀ = (2,0,6): 24y + 16(z−6) = 0, which gives **3y + 2z = 12**.

**Processing s₁**

- Topmost pixel (0,6): z = 0 (check: 0 + 6 + z = 6).
- Moving down scan lines is skipped for brevity. Go straight to y = 1.
- Leftmost pixel on y = 1 is (0,1): 0 + 1 + z = 6, so z = 5.
- Along y = 1, each step decreases z by a/c = 1: (1,1) → 4, (2,1) → 3, **(3,1) → 2**.
- 2 < DB\[3\]\[1\] = ∞, so **DB\[3\]\[1\] = 2 and FB\[3\]\[1\] = cl₁**.

**Processing s₂**

- Topmost pixel (4,4): z = 0. Leftmost pixel on y = 1 is (2.5, 1): z = 4.5.
- At (3,1): 3(1) + 2z = 12, so z = 4.5.
- Compare: 4.5 > DB\[3\]\[1\] = 2, so s₂ is **behind** s₁. DB stays 2 and FB stays cl₁.
- **Pixel (3,1) has colour cl₁.**

**Limitations.**

- Each pixel holds only **one** surface colour and one depth value, so it is fine for **opaque** surfaces only.
- With transparent surfaces the pixel colour should combine the surface colour with contributions from the surfaces behind it. The Z-buffer has a single depth slot per pixel and cannot store all contributing surfaces.
- The **A-buffer** method was developed to overcome this.

## Post 6 – Hidden surface removal II: Painter's algorithm, BSP trees, Warnock

### Depth sorting (Painter's algorithm)

Works in **both object and image space**. It simulates an oil painter who paints the background first and the foreground last, so nearer surfaces **overwrite** farther ones. It resolves visibility by **polygon order**, not by a per-pixel depth comparison (unlike the Z-buffer), so it only works when a consistent visibility order can be established.

**Two basic steps**

1. **Sort** the surfaces by depth from the view plane. Find each surface's z\_max and z\_min and build the list S = {s₁, s₂, …, sₙ}, sorted on max depth.
2. **Render** one surface at a time, starting with the maximum depth (sₙ, the farthest) and ending with the lowest depth (nearest).

**Example 1 – three overlapping rectangles** (view along +z, larger z = farther).

- A: x∈\[0,6\], y∈\[0,4\], z=9. B: x∈\[1,5\], y∈\[1,4\], z=6. C: x∈\[3,6\], y∈\[2,5\], z=3. Pixel of interest p = (3.5, 2.5).
- Sort by decreasing z: 9 > 6 > 3, so the draw order is **A → B → C**.
- p lies inside all three footprints, so it receives three writes. The last write is C, so **C is visible at p**. C is the nearest (z = 3).

**Overlap checks.** While rendering, compare the surface Sₙ with every other surface in S. If min depth of one surface > max depth of the other, there is **no depth overlap**: render the surface and remove it from S. Otherwise run these four tests **in order**. As soon as one is true, move to the next surface in the list:

| # | Test (S = current surface, S′ = overlapping surface) | Level |
| --- | --- | --- |
| 1 | **Bounding rectangles** of the two surfaces on the view plane do not overlap. True if there is no overlap in the x extents or no overlap in the y extents; if both overlap, the test fails | Image |
| 2 | S is **completely behind** S′ relative to the viewer. Get the plane equation of S′ (normal toward the viewer) and substitute all vertices of S. If **all** give a value < 0, S is behind S′; otherwise the test fails | Object |
| 3 | S′ is **completely in front of** S. Use the plane equation of S and the vertices of S′. For **all** vertices the value should be > 0 | Object |
| 4 | The **projections (boundary edges) of the two surfaces onto the view plane do not overlap**. Compare the sets of projected pixels for common pixels | Image |

Tests 1 and 4 are done at pixel/image level, and tests 2 and 3 at object level. Example: two triangles whose bounding boxes overlap fail test 1. If their actual projections still do not overlap, test 4 passes.

**If all four tests fail**, swap the two surfaces in the list (**reordering**) and restart the process.

**Failure cases**

- **Cyclic overlap**: each polygon hides another (three strips woven over/under each other), so no single drawing order works.
- **Intersecting surfaces**: part of surface 1 is deeper than surface 2 and part is nearer. All tests fail, so we reorder. They fail again, so we reorder again, and we get an **infinite loop**.
- **Fixes**: keep a Boolean **flag** per surface, set *on* when it is reordered. If it needs reordering a second time, **divide the surface along the intersection line** and **add the two new surfaces** to the sorted list at the appropriate positions.

### Space subdivision: BSP trees

**Idea.** Divide the scene with a plane. The eye and polygon T₂ are tested against the plane of polygon T₁. Planes split space into **Outside (Front)**, the side the normal points to, and **Inside (Back)**.

**Side test.** Let r be a point in space, p a point on the plane and **n** the plane's normal:

```latex
f(\mathbf r)=(\mathbf r-\mathbf p)\cdot\mathbf n=\|\mathbf r-\mathbf p\|\|\mathbf n\|\cos\theta
```

| f(r) | Angle | Position of r |
| --- | --- | --- |
| > 0 | θ < 90° | Outside / front (normal side) |
| = 0 | θ = 90° | On the plane |
| < 0 | θ > 90° | Inside / back |

**Drawing order for two polygons** (q is a point of T₂, e is the eye; T₁ is the dividing polygon):

- **f(q)·f(e) > 0**: same side, so the eye and T₂ are on the same side of T₁. Draw **T₁ first, then T₂**.
- **f(q)·f(e) < 0**: opposite sides. Draw **T₂ first, then T₁**.

The rule is always **far before near**, drawing the polygon on the opposite side from the eye first.

**BSP tree** = efficient structure for quickly finding the inside/outside relation between polygons and the camera position. Two phases:

| Phase | When | What |
| --- | --- | --- |
| **Preprocessing**: build the tree | Once for a given scene | Test polygon vertices against the plane. Group polygons by side (IN / OUT). **Split** polygons that cross the plane. |
| **Rendering**: traverse the tree | Whenever the eye position changes | Test the **eye** against the same planes, then visit the opposite subtree, then the node, then the eye-side subtree. |

The tree stores the partition. The eye selects the traversal order.

**Construction (example scene with polygons 1–11)**

- Pick polygon 1 as the root, extend its plane, and classify the others: IN = {2, 3, 4}, OUT = {5, 6, 7, 8, 9, 10, 11}.
- Repeat inside each subtree. IN side: 2 → {3, 4}, then 3 → 4. OUT side: root 5 puts {6, 7, 10, 11, 9a} IN and {8, 9b} OUT.
- **Polygon splitting.** The plane of polygon 5 cuts polygon 9 (endpoints have f₅(u) < 0 and f₅(v) > 0, different signs, so it crosses the plane). Split at s, where f₅(s) = 0, giving **9a** (IN side) and **9b** (OUT side), each placed in its own subtree.
- Final tree: 1 → (IN: 2 → 3 → 4; OUT: 5 → (IN: 6 → 7 → 9a → 10 → 11; OUT: 8 → 9b)).

**Rendering (traversal).** At each node i, test the **same eye e** with fᵢ(e) = (e − pᵢ)·nᵢ:

- **Eye OUT** (fᵢ(e) > 0): **IN subtree → i → OUT subtree**.
- **Eye IN** (fᵢ(e) < 0): **OUT subtree → i → IN subtree**.

Entering a node does not mean drawing it immediately: the opposite-side subtree is finished first. The rule is applied recursively, and IN/OUT mean whole subtrees.

**Worked traversal for the marked eye position**

| Node | Eye side | Local traversal |
| --- | --- | --- |
| 1 | OUT | IN → 1 → OUT |
| 2 | IN | OUT → 2 → IN |
| 3 | OUT | IN → 3 → OUT |
| 5 | IN | OUT → 5 → IN |
| 8 | IN | OUT → 8 → IN |
| 6 | IN | OUT → 6 → IN |
| 7 | OUT | IN → 7 → OUT (its normal points downward and the eye is below its plane) |
| 9a | IN | OUT → 9a → IN |
| 10 | IN | OUT → 10 → IN |

Leaves 4, 9b and 11 are drawn directly. Sequence: Render(1) = Render(2), **1**, Render(5), where Render(2) = 2, 3, 4; Render(5) = Render(8), **5**, Render(6); Render(8) = 8, 9b; Render(6) = 6, 7, 9a, 10, 11.

**Final drawing order: 2, 3, 4, 1, 8, 9b, 5, 6, 7, 9a, 10, 11.**

Note that the tree is built once, and only the traversal is redone when the eye moves.

### Area subdivision: Warnock's algorithm

**Area subdivision** is a group of HSR methods with the same general idea. Consider an **area** of the projected image. If you can determine which (polygonal) surfaces are visible in the area, assign those surface colours to it. Otherwise **recursively subdivide** the area into smaller regions and apply the same decision logic to the sub-regions.

**Warnock's algorithm** is one of the earliest subdivision methods. It subdivides a screen area into **four equal squares** and checks visibility in each square to decide the pixel colours. Three cases:

| Case | Condition | Action |
| --- | --- | --- |
| 1 | The current square contains **no surface** | Stop subdividing, assign the **background colour** to its pixels |
| 2 | The **nearest surface completely overlaps** the region | Stop subdividing, assign that **surface colour** to the region |
| 3 | None of the above | **Recursively divide** into four sub-regions and repeat the checks |

Recursion stops when Case 1 or Case 2 is met, **or** when the region size equals the pixel size. The slides' example subdivides P₃ → P₃₁ → P₃₁₁…P₃₁₄ around a curved surface.

**Octree method**: another object-space (subdivision) method. It is only mentioned in the slides and not covered.

**Recap of HSR (Posts 5–6).** HSR is an important operation in the 4th stage and is a complex task. Coherence principles are exploited to reduce the complexity.

## Quick-fire formula and comparison cheat sheet

**Pipeline (Posts 1–2):** object → world → view/camera (VC) → canonical view volume (CVV, \[−1,1\]³) → clip → project → window→viewport → screen. The z value is kept for HSR (z-buffer).

| Topic | Key formula / fact |
| --- | --- |
| View basis | n from eye and look-at point, u ∝ p\_up × n (normalised), v = n × u. Camera looks along −z. |
| World → view | M\_w2v = R · T(−o). Rows of R are u, v, n. The translation column is (−u·o, −v·o, −n·o). |
| Parallel projection | x′ = x, y′ = y, z′ = −d. w = 1, so the homogeneous division changes nothing. |
| Perspective projection | x′ = x·d/(−z), y′ = y·d/(−z) (similar triangles). Matrix form uses w = −z/d (row 4 of T\_psp is \[0, 0, −1/d, 0\]); divide by w. |
| View volume | Parallel = box. Perspective = frustum. |
| To CVV | Parallel: scale (and translate). Perspective: shear + scale, so the frustum becomes a box. |
| Window → viewport | s\_x = (Vx2−Vx1)/(Wx2−Wx1), s\_y likewise. V\_x = s\_x(W\_x−Wx1) + Vx1, V\_y = s\_y(W\_y−Wy1) + Vy1. 3×3 homogeneous T\_vp. Each scale is viewport size / window size. |
| 2D Cohen–Sutherland | 4-bit outcode (above, below, right, left). Both codes 0000 → **trivial accept**. Bitwise **AND ≠ 0** → **trivial reject**. Otherwise clip against one crossed edge, replace the outside endpoint by the intersection, recompute the code and repeat. AND = 0 does not imply accept. |
| 3D Cohen–Sutherland | 6-bit outcode (adds near and far). Parametric line P(t) = P₁ + t(P₂−P₁). Intersect with a plane: t = (boundary − coordinate₁)/(coordinate₂ − coordinate₁). |
| Sutherland–Hodgman | Clip the polygon against one window edge at a time, in a fixed order. Per edge, four cases: in→in output P₂; in→out output intersection; out→out nothing; out→in output intersection and P₂. Fails on concave polygons (spurious connecting edges). |
| Weiler–Atherton | Handles concave polygons. Walk along the subject polygon and window boundary, switching at intersections: follow subject at an **entry**, follow window at an **exit**. Gives separate polygons. |
| 3D fill-area clipping | Clip each face of a polyhedron against the CVV planes. Bounding-box tests give quick accept or reject. |
| Back-face test | N·v < 0 → front-facing (retain). Viewing along −z: N·v = −N\_z, so **N\_z > 0** retains. Removes about half of the faces. |
| Z-buffer depth | z = (−ax − by − d)/c. Along a scan line z′ = z − a/c. Across scan lines at the edge z′ = z + (a/m + b)/c, with x′ = x − 1/m. |
| Painter's | Sort by max depth (far first), paint far → near. If depth ranges overlap, run 4 tests in order (bounding rectangles, S behind S′, S′ in front of S, projections do not overlap). If all fail, reorder, then split once the flag is set. |
| Plane side test | f(r) = (r − p)·n. > 0 front/OUT, = 0 on the plane, < 0 back/IN. |
| BSP render | Eye OUT: IN → node → OUT. Eye IN: OUT → node → IN. This draws far to near. Build once, traverse per eye position. |
| Warnock | Subdivide into 4 squares. Stop when empty (background), when the nearest surface covers the square (surface colour), or when the region is one pixel. |

**Comparison of HSR methods**

| Method | Space | Idea | Strength / weakness |
| --- | --- | --- | --- |
| Back-face elimination | Object | N·v test per face | Cheap and removes about half the faces, but ignores one object hiding another |
| Z-buffer | Image | Per-pixel depth compare with depth and frame buffers | Simple, any order, but only opaque surfaces and one colour per pixel (A-buffer for transparency) |
| Painter's (depth sort) | Both | Sort far → near, overwrite | Needs a consistent order. Fails on cyclic or intersecting surfaces and needs splitting |
| BSP tree | Object | Split space with planes. Traverse by eye side | Tree is built once, rendering is a fast traversal, but polygons may be split |
| Warnock | Image (area subdivision) | Recursively subdivide the area | Stops at trivial cases or pixel size |

**Object-space vs image-space:** object-space is device-independent but computation-heavy and suits simple scenes. Image-space is cheaper but depends on resolution.

**Clipping vs HSR:** clipping removes geometry outside the view volume. HSR removes geometry inside it that is blocked by other geometry.
