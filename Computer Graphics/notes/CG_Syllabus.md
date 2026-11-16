---
title: Computer Graphics Syllabus Tracker
aliases:
  - CG Syllabus
  - Computer Graphics Syllabus
course: Computer Graphics
tags:
  - computer-graphics
  - CG
  - syllabus
---

# Computer Graphics — Syllabus

This file is the **authority** for the topic list, the topic order and the midsem / post-midsem split. The post-midsem note [[CG_Endsem_Notes]] is written against it section for section; every topic below names its lecture deck and jumps straight to the matching heading in the note file that holds it.

The split is by **date of the deck**, not by subject:

| Block | Decks | Note file |
| --- | --- | --- |
| Pre-midsem | 30 July → 10 September | [[CG_Midsem_notes]] |
| Post-midsem | 29 September → the animation deck | [[CG_Endsem_Notes]] |

> [!warning] Scope of the examination
> **The end-semester examination includes all of the syllabus** — both the pre-midsem block (topics 1–8) and the post-midsem block (topics 1–8). Nothing drops out: the raster algorithms of the post-midsem block are built directly on the line and object representations of the pre-midsem block.

> [!info] How to use this tracker
> - Tick the box on a topic line when the topic is **revised and recallable**, not merely read once. Untick it if a revision pass exposes a hole.
> - **PDF** opens the lecture deck; **Notes** jumps to the topic's heading in the note file that holds it — [[CG_Endsem_Notes]] for the post-midsem block, [[CG_Midsem_notes]] for the pre-midsem one; the section index at the bottom gives a one-click jump to every written section.
> - The counter below is live (Dataview) — it reads the checkboxes in this file, so nothing needs counting by hand.
> - `§` numbers are the H2/H3 section numbers used inside [[CG_Endsem_Notes]] (e.g. §4.5 is a real heading there).
> - Each post-midsem topic that contains an algorithm also carries an **interactive dry-run widget** — the widget column in the table at the bottom says which one.

## Progress

```dataview
TABLE WITHOUT ID
  string(length(filter(file.tasks, (t) => t.completed))) + " / " + string(length(file.tasks)) AS "Topics ticked",
  string(round(100 * length(filter(file.tasks, (t) => t.completed)) / length(file.tasks))) + " %" AS "Coverage",
  length(filter(file.tasks, (t) => !t.completed)) AS "Still open"
WHERE file.path = this.file.path
```

---

## Pre-Midsem — 8 topics

- [ ] **1 · Introduction to Computer Graphics** — [[Pre 1 - Introduction to Computer Graphics.pdf|PDF]] · [[CG_Midsem_notes|Notes]] (not yet written)
- [ ] **2 · Digital Information and Digital Images** — [[Pre 2 - Digital Information and Digital Images.pdf|PDF]] · [[CG_Midsem_notes|Notes]] (not yet written)
- [ ] **3 · Line Drawing Algorithms** — [[Pre 3 - Line Drawing Algorithms (6 Aug).pdf|PDF (6 Aug)]], [[Pre 3 - Line Drawing Algorithms (10 Aug).pdf|PDF (10 Aug)]] · [[CG_Midsem_notes|Notes]] (not yet written)
- [ ] **4 · Object Representation** — [[Pre 4 - Object Representation.pdf|PDF]] · [[CG_Midsem_notes|Notes]] (not yet written)
- [ ] **5 · B-Splines** — [[Pre 5 - B-Splines.pdf|PDF]] · [[CG_Midsem_notes|Notes]] (not yet written)
- [ ] **6 · 2D Modelling and Composite Transformations** — [[Pre 6 - 2D Modelling and Composite Transformations (31 Aug).pdf|PDF (31 Aug)]], [[Pre 6 - 2D Modelling and Composite Transformations (3 Sep).pdf|PDF (3 Sep)]] · [[CG_Midsem_notes|Notes]] (not yet written)
- [ ] **7 · Reflection Models and Phong Illumination** — [[Pre 7 - Reflection Models and Phong Illumination.pdf|PDF]] · [[CG_Midsem_notes|Notes]] (not yet written)
- [ ] **8 · Practice Problems** — [[Pre 8 - Practice Problems.pdf|PDF]] · [[CG_Midsem_notes|Notes]] (not yet written)

> [!note] Between the blocks
> - [[Between - Intensity Quantization (17 Sep).pdf|Intensity Quantization (17 Sep)]] — **intensity quantization**: how a continuous intensity is mapped onto the finite grey levels of a display. Dates between the two blocks, so it belongs to neither list; it is the bridge from the pre-midsem image model to the post-midsem raster stage. Not yet written.
> - [[Post 1 - 3D Viewing, Camera and Projection Fundamentals (28 Sep alt).pdf|28 Sep duplicate]] — a 76-page deck that **repeats the viewing fundamentals** of [[Post 1 - 3D Viewing, Camera and Projection Fundamentals.pdf|Post 1]] (topic 1 below). Treat it as an alternate copy of topic 1, not as a ninth topic. Its content (camera analogy, VC set-up, the numeric worked example, why projection) is written up in [[CG_Endsem_Notes#1.7 The 28 September lecture: viewing as taking a photograph|§1.7–§1.9]].

---

## Post-Midsem — 8 topics

- [x] **1 · 3D Viewing, Camera and Projection Fundamentals** — [[Post 1 - 3D Viewing, Camera and Projection Fundamentals.pdf|PDF]] · [[CG_Endsem_Notes#1. 3D Viewing, Camera and Projection Fundamentals|Notes → §1]] (10 sections, incl. the 28 Sep lecture in §1.7–§1.9)
- [x] **2 · Viewport Mapping and Cohen–Sutherland Clipping** — [[Post 2 - Viewport Mapping and Cohen-Sutherland Clipping.pdf|PDF]] · [[CG_Endsem_Notes#2. Viewport Mapping and Cohen–Sutherland Clipping|Notes → §2]] (11 sections) · widget `#w-cs`
- [x] **3 · Polygon and 3D Fill-Area Clipping** — [[Post 3 - Polygon and 3D Fill-Area Clipping.pdf|PDF]] · [[CG_Endsem_Notes#3. Polygon and 3D Fill-Area Clipping|Notes → §3]] (17 sections) · widget `#w-sh`
- [x] **4 · Hidden Surface Removal I — Back-Face Elimination and the Z-Buffer** — [[Post 4 - Hidden Surface Removal I - Back-Face Elimination and the Z-Buffer.pdf|PDF]] · [[CG_Endsem_Notes#4. Hidden Surface Removal I — Back-Face Elimination and the Z-Buffer|Notes → §4]] (9 sections) · widget `#w-zb`
- [x] **5 · Hidden Surface Removal II — Painter's Algorithm and BSP Trees** — [[Post 5 - Hidden Surface Removal II - Painter's Algorithm and BSP Trees.pdf|PDF]] · [[CG_Endsem_Notes#5. Hidden Surface Removal II — Painter's Algorithm and BSP Trees|Notes → §5]] (11 sections) · widget `#w-bsp`
- [x] **6 · Fill-Area Algorithms, Scan Conversion and the 3D Pipeline** — [[Post 6 - Fill-Area Algorithms, Scan Conversion and the 3D Pipeline.pdf|PDF]] · [[CG_Endsem_Notes#6. Fill-Area Algorithms, Scan Conversion and the 3D Pipeline|Notes → §6]] (16 sections) · widgets `#w-sl`, `#w-ff`
- [x] **7 · Anti-Aliasing I — The Gupta–Sproull Algorithm** — [[Post 7 - Anti-Aliasing I - The Gupta-Sproull Algorithm.pdf|PDF]] · [[CG_Endsem_Notes#7. Anti-Aliasing I — The Gupta–Sproull Algorithm|Notes → §7]] (13 sections) · widget `#w-gs`
- [x] **8 · Animation — The 2D Production Process** — [[Post 8 - Animation - The 2D Production Process.pdf|PDF]] · [[CG_Endsem_Notes#8. Animation — The 2D Production Process|Notes → §8]] (13 sections) · widget `#w-tween`

> [!tip] Exam pointer
> The marks in this block sit on the **traces, not the definitions**: project a point through the camera frame and the canonical cube (§1.2–§1.5), an outcode-by-outcode line clip (§2.4, §2.8), the four-case Sutherland–Hodgman walk (§3.4–§3.8), the tetrahedron normal test (§4.2) and the incremental z recursion (§4.6), the full BSP draw order with the split of polygon 9 (§5.6–§5.8), a row-by-row scan-line trace (§6.7) and a seed-fill stack trace (§6.11), the Gupta–Sproull decision variable together with its eight coverage values (§7.6, §7.10), and the in-between arithmetic $h(t)=4Ht(1-t)$ (§8.11).

---

## Section index of the notes

Every written section of [[CG_Endsem_Notes]], grouped by topic, so a topic can be opened at the exact sub-heading.

### §1 · 3D Viewing, Camera and Projection Fundamentals

| § | Section |
| --- | --- |
| 1.1 | [[CG_Endsem_Notes#1.1 The six stages in one picture\|The six stages in one picture]] |
| 1.2 | [[CG_Endsem_Notes#1.2 World-to-view: building the camera frame\|World-to-view: building the camera frame]] |
| 1.3 | [[CG_Endsem_Notes#1.3 The view volume\|The view volume]] |
| 1.4 | [[CG_Endsem_Notes#1.4 Why normalise the volume to a canonical cube\|Why normalise the volume to a canonical cube]] |
| 1.5 | [[CG_Endsem_Notes#1.5 The projection matrices\|The projection matrices]] |
| 1.6 | [[CG_Endsem_Notes#1.6 Viewport mapping\|Viewport mapping]] |
| 1.7 | [[CG_Endsem_Notes#1.7 The 28 September lecture: viewing as taking a photograph\|The 28 September lecture]] |
| 1.8 | [[CG_Endsem_Notes#1.8 Worked example from the 28 September lecture\|Worked example (28 Sep)]] |
| 1.9 | [[CG_Endsem_Notes#1.9 Why projection is needed\|Why projection is needed]] |
| 1.10 | [[CG_Endsem_Notes#1.10 Exam pointer\|Exam pointer]] |

### §2 · Viewport Mapping and Cohen–Sutherland Clipping

| § | Section |
| --- | --- |
| 2.1 | [[CG_Endsem_Notes#2.1 Point clipping\|Point clipping]] |
| 2.2 | [[CG_Endsem_Notes#2.2 Region codes\|Region codes]] |
| 2.3 | [[CG_Endsem_Notes#2.3 Trivial accept and trivial reject\|Trivial accept and trivial reject]] |
| 2.4 | [[CG_Endsem_Notes#2.4 Clipping one boundary at a time\|Clipping one boundary at a time]] |
| 2.5 | [[CG_Endsem_Notes#2.5 The line-equation view\|The line-equation view]] |
| 2.6 | [[CG_Endsem_Notes#2.6 The three-dimensional extension\|The three-dimensional extension]] |
| 2.7 | [[CG_Endsem_Notes#2.7 Intersection formulas for all six planes\|Intersection formulas for all six planes]] |
| 2.8 | [[CG_Endsem_Notes#2.8 Worked example in 3D\|Worked example in 3D]] |
| 2.9 | [[CG_Endsem_Notes#2.9 The algorithm\|The algorithm]] |
| 2.10 | [[CG_Endsem_Notes#2.10 Interactive dry run\|Interactive dry run]] |
| 2.11 | [[CG_Endsem_Notes#2.11 Exam pointer\|Exam pointer]] |

### §3 · Polygon and 3D Fill-Area Clipping

| § | Section |
| --- | --- |
| 3.1 | [[CG_Endsem_Notes#3.1 Polygons as ordered, closed vertex lists\|Polygons as ordered, closed vertex lists]] |
| 3.2 | [[CG_Endsem_Notes#3.2 Why polygon clipping is not line clipping\|Why polygon clipping is not line clipping]] |
| 3.3 | [[CG_Endsem_Notes#3.3 The window as four half-planes\|The window as four half-planes]] |
| 3.4 | [[CG_Endsem_Notes#3.4 The four edge cases\|The four edge cases]] |
| 3.5 | [[CG_Endsem_Notes#3.5 Computing the intersection\|Computing the intersection]] |
| 3.6 | [[CG_Endsem_Notes#3.6 The procedure\|The procedure]] |
| 3.7 | [[CG_Endsem_Notes#3.7 Pictorial worked example\|Pictorial worked example]] |
| 3.8 | [[CG_Endsem_Notes#3.8 Numerical trace\|Numerical trace]] |
| 3.9 | [[CG_Endsem_Notes#3.9 The limitation: a concave subject can split\|The limitation: a concave subject can split]] |
| 3.10 | [[CG_Endsem_Notes#3.10 Weiler–Atherton\|Weiler–Atherton]] |
| 3.11 | [[CG_Endsem_Notes#3.11 Comparison\|Comparison]] |
| 3.12 | [[CG_Endsem_Notes#3.12 3D point clipping\|3D point clipping]] |
| 3.13 | [[CG_Endsem_Notes#3.13 Bounding boxes before exact clipping\|Bounding boxes before exact clipping]] |
| 3.14 | [[CG_Endsem_Notes#3.14 3D face clipping, worked\|3D face clipping, worked]] |
| 3.15 | [[CG_Endsem_Notes#3.15 Clipping versus occlusion\|Clipping versus occlusion]] |
| 3.16 | [[CG_Endsem_Notes#3.16 Interactive dry run\|Interactive dry run]] |
| 3.17 | [[CG_Endsem_Notes#3.17 Exam pointer\|Exam pointer]] |

### §4 · Hidden Surface Removal I — Back-Face Elimination and the Z-Buffer

| § | Section |
| --- | --- |
| 4.1 | [[CG_Endsem_Notes#4.1 Back-face elimination\|Back-face elimination]] |
| 4.2 | [[CG_Endsem_Notes#4.2 Worked example: a tetrahedron viewed along the negative z-axis\|Worked example: a tetrahedron viewed along the negative z-axis]] |
| 4.3 | [[CG_Endsem_Notes#4.3 Why back-face elimination is not enough\|Why back-face elimination is not enough]] |
| 4.4 | [[CG_Endsem_Notes#4.4 The depth (z) buffer: the idea\|The depth (z) buffer: the idea]] |
| 4.5 | [[CG_Endsem_Notes#4.5 Depth from the plane equation\|Depth from the plane equation]] |
| 4.6 | [[CG_Endsem_Notes#4.6 Incremental depth: never evaluate the plane twice\|Incremental depth: never evaluate the plane twice]] |
| 4.7 | [[CG_Endsem_Notes#4.7 The algorithm\|The algorithm]] |
| 4.8 | [[CG_Endsem_Notes#4.8 Interactive dry run\|Interactive dry run]] |
| 4.9 | [[CG_Endsem_Notes#4.9 Exam pointer\|Exam pointer]] |

### §5 · Hidden Surface Removal II — Painter's Algorithm and BSP Trees

| § | Section |
| --- | --- |
| 5.1 | [[CG_Endsem_Notes#5.1 Painting back to front\|Painting back to front]] |
| 5.2 | [[CG_Endsem_Notes#5.2 The four tests that decide a pair\|The four tests that decide a pair]] |
| 5.3 | [[CG_Endsem_Notes#5.3 The failure cases\|The failure cases]] |
| 5.4 | [[CG_Endsem_Notes#5.4 The plane function\|The plane function]] |
| 5.5 | [[CG_Endsem_Notes#5.5 Building the tree\|Building the tree]] |
| 5.6 | [[CG_Endsem_Notes#5.6 Splitting a polygon: cutting 9 into 9a and 9b\|Splitting a polygon: cutting 9 into 9a and 9b]] |
| 5.7 | [[CG_Endsem_Notes#5.7 Rendering: the eye selects the traversal order\|Rendering: the eye selects the traversal order]] |
| 5.8 | [[CG_Endsem_Notes#5.8 The complete trace\|The complete trace]] |
| 5.9 | [[CG_Endsem_Notes#5.9 Why a BSP tree is worth the build\|Why a BSP tree is worth the build]] |
| 5.10 | [[CG_Endsem_Notes#5.10 Interactive dry run\|Interactive dry run]] |
| 5.11 | [[CG_Endsem_Notes#5.11 Exam pointer\|Exam pointer]] |

### §6 · Fill-Area Algorithms, Scan Conversion and the 3D Pipeline

| § | Section |
| --- | --- |
| 6.1 | [[CG_Endsem_Notes#6.1 The six stages\|The six stages]] |
| 6.2 | [[CG_Endsem_Notes#6.2 Lighting versus shading\|Lighting versus shading]] |
| 6.3 | [[CG_Endsem_Notes#6.3 The three shading models\|The three shading models]] |
| 6.4 | [[CG_Endsem_Notes#6.4 Aliasing at the raster stage\|Aliasing at the raster stage]] |
| 6.5 | [[CG_Endsem_Notes#6.5 Inside–outside tests\|Inside–outside tests]] |
| 6.6 | [[CG_Endsem_Notes#6.6 The scan-line idea\|The scan-line idea]] |
| 6.7 | [[CG_Endsem_Notes#6.7 Worked trace: a triangle, row by row\|Worked trace: a triangle, row by row]] |
| 6.8 | [[CG_Endsem_Notes#6.8 Scan-line polygon fill — algorithm\|Scan-line polygon fill — algorithm]] |
| 6.9 | [[CG_Endsem_Notes#6.9 Interactive dry run\|Interactive dry run]] |
| 6.10 | [[CG_Endsem_Notes#6.10 Seed fill, boundary fill, flood fill\|Seed fill, boundary fill, flood fill]] |
| 6.11 | [[CG_Endsem_Notes#6.11 The deck's stack traces\|The deck's stack traces]] |
| 6.12 | [[CG_Endsem_Notes#6.12 Seed fill — algorithm\|Seed fill — algorithm]] |
| 6.13 | [[CG_Endsem_Notes#6.13 Interactive dry run\|Interactive dry run]] |
| 6.14 | [[CG_Endsem_Notes#6.14 Character generation: the bitmapped font\|Character generation: the bitmapped font]] |
| 6.15 | [[CG_Endsem_Notes#6.15 Character generation: the outlined font\|Character generation: the outlined font]] |
| 6.16 | [[CG_Endsem_Notes#6.16 Exam pointer\|Exam pointer]] |

### §7 · Anti-Aliasing I — The Gupta–Sproull Algorithm

| § | Section |
| --- | --- |
| 7.1 | [[CG_Endsem_Notes#7.1 What the algorithm is\|What the algorithm is]] |
| 7.2 | [[CG_Endsem_Notes#7.2 Part 1 — two candidates and a midpoint\|Part 1 — two candidates and a midpoint]] |
| 7.3 | [[CG_Endsem_Notes#7.3 The decision variable and its update\|The decision variable and its update]] |
| 7.4 | [[CG_Endsem_Notes#7.4 The starting value\|The starting value]] |
| 7.5 | [[CG_Endsem_Notes#7.5 The complete midpoint algorithm\|The complete midpoint algorithm]] |
| 7.6 | [[CG_Endsem_Notes#7.6 Worked midpoint trace: from (0,0) to (8,5)\|Worked midpoint trace: from (0,0) to (8,5)]] |
| 7.7 | [[CG_Endsem_Notes#7.7 Part 2 — from a vertical gap to a perpendicular distance\|Part 2 — from a vertical gap to a perpendicular distance]] |
| 7.8 | [[CG_Endsem_Notes#7.8 The filter and the blend\|The filter and the blend]] |
| 7.9 | [[CG_Endsem_Notes#7.9 The two vertical neighbours\|The two vertical neighbours]] |
| 7.10 | [[CG_Endsem_Notes#7.10 Worked shading trace: the same line from (0,0) to (8,5)\|Worked shading trace: the same line from (0,0) to (8,5)]] |
| 7.11 | [[CG_Endsem_Notes#7.11 Gupta–Sproull — algorithm\|Gupta–Sproull — algorithm]] |
| 7.12 | [[CG_Endsem_Notes#7.12 Interactive dry run\|Interactive dry run]] |
| 7.13 | [[CG_Endsem_Notes#7.13 Exam pointer\|Exam pointer]] |

### §8 · Animation — The 2D Production Process

| § | Section |
| --- | --- |
| 8.1 | [[CG_Endsem_Notes#8.1 The question\|The question]] |
| 8.2 | [[CG_Endsem_Notes#8.2 What a 2D animation is\|What a 2D animation is]] |
| 8.3 | [[CG_Endsem_Notes#8.3 The production pipeline\|The production pipeline]] |
| 8.4 | [[CG_Endsem_Notes#8.4 Stage 1 — storyboard and beat sheet\|Stage 1 — storyboard and beat sheet]] |
| 8.5 | [[CG_Endsem_Notes#8.5 Stage 2 — the model sheet\|Stage 2 — the model sheet]] |
| 8.6 | [[CG_Endsem_Notes#8.6 Stage 3 — the seven key poses\|Stage 3 — the seven key poses]] |
| 8.7 | [[CG_Endsem_Notes#8.7 Stage 4 — timing, spacing and the in-betweens\|Stage 4 — timing, spacing and the in-betweens]] |
| 8.8 | [[CG_Endsem_Notes#8.8 Stage 5 — clean-up, ink and paint\|Stage 5 — clean-up, ink and paint]] |
| 8.9 | [[CG_Endsem_Notes#8.9 Stage 6 — compositing and post\|Stage 6 — compositing and post]] |
| 8.10 | [[CG_Endsem_Notes#8.10 The principles the example forces\|The principles the example forces]] |
| 8.11 | [[CG_Endsem_Notes#8.11 Interpolation: the arithmetic of an in-between\|Interpolation: the arithmetic of an in-between]] |
| 8.12 | [[CG_Endsem_Notes#8.12 Interactive dry run\|Interactive dry run]] |
| 8.13 | [[CG_Endsem_Notes#8.13 Exam pointer\|Exam pointer]] |

---

## Interactive dry runs

Each algorithm in the post-midsem block has one self-contained widget: a `Play` / `Pause` / `Next Step` / `Reset` control bar over a drawing of the algorithm's own data. The code lives in the note as a single `html` block; [[CG_context]] explains how to run it.

| Widget | Where | Algorithm | What to watch |
| --- | --- | --- | --- |
| `#w-cs` | [[CG_Endsem_Notes#2.10 Interactive dry run\|§2.10]] | Cohen–Sutherland line clip | The outcodes recomputed after every boundary; the line shortening from one end at a time |
| `#w-sh` | [[CG_Endsem_Notes#3.16 Interactive dry run\|§3.16]] | Sutherland–Hodgman polygon clip | Inside/outside switching per boundary and the new vertex list growing at each of the four passes |
| `#w-zb` | [[CG_Endsem_Notes#4.8 Interactive dry run\|§4.8]] | Z-buffer | Depth-test winners per pixel, and the z value stepping by a constant along a scan line |
| `#w-bsp` | [[CG_Endsem_Notes#5.10 Interactive dry run\|§5.10]] | BSP tree build and traversal | Which polygon becomes the splitting plane, and the draw order flipping as the eye crosses a plane |
| `#w-sl` | [[CG_Endsem_Notes#6.9 Interactive dry run\|§6.9]] | Scan-line polygon fill | The active edge table as edges enter and leave, and the parity rule turning spans on and off |
| `#w-ff` | [[CG_Endsem_Notes#6.13 Interactive dry run\|§6.13]] | Flood fill | The 4- versus 8-connectivity switch: the same boundary leaks under one and holds under the other |
| `#w-gs` | [[CG_Endsem_Notes#7.12 Interactive dry run\|§7.12]] | Gupta–Sproull anti-aliasing | The midpoint decision variable choosing E or NE, then the two coverage values that sum to one |
| `#w-tween` | [[CG_Endsem_Notes#8.12 Interactive dry run\|§8.12]] | In-between interpolation | Linear versus smoothstep spacing of the same seven keys along the jump arc |

---

## Figures

The block's diagrams are either page renders lifted from the decks (`Computer Graphics/images/`) or original Excalidraw reconstructions (vault-root `Excalidraw/`, prefix `CG - `). Both are embedded by bare filename, so the note survives a folder move.

| Figure | Carries |
| --- | --- |
| [[CG - 3D Graphics Pipeline.excalidraw\|3D Graphics Pipeline]] | The six stages of §1.1 in one picture |
| [[CG - Camera Frame and View Volume.excalidraw\|Camera Frame and View Volume]] | $\mathbf{n}$, $\mathbf{v}$, $\mathbf{u}$ and the frustum of §1.2–§1.3 |
| [[CG - Cohen Sutherland Region Codes.excalidraw\|Cohen Sutherland Region Codes]] | The nine outcoded regions of §2.2 |
| [[CG - Sutherland Hodgman Four Cases.excalidraw\|Sutherland Hodgman Four Cases]] | The in/out vertex dictionary of §3.4 |
| [[CG - Z Buffer.excalidraw\|Z Buffer]] | Per-pixel depth test of §4.4–§4.7 |
| [[CG - BSP Tree Traversal.excalidraw\|BSP Tree Traversal]] | The eye-dependent draw order of §5.7 |
| [[CG - Scan Line Fill.excalidraw\|Scan Line Fill]] | AET / ET bookkeeping of §6.6–§6.8 |
| [[CG - Gupta Sproull Coverage.excalidraw\|Gupta Sproull Coverage]] | The perpendicular distance and the two-neighbour blend of §7.7–§7.9 |
| [[CG - 2D Animation Pipeline.excalidraw\|2D Animation Pipeline]] | The six stages of §8.3 |
| [[CG - Jump Arc Keyframes.excalidraw\|Jump Arc Keyframes]] | The seven keys and the $4Ht(1-t)$ arc of §8.6–§8.11 |

Page renders lifted from the decks (every one is embedded with a width and an italic caption):

| Figure | Carries |
| --- | --- |
| [[CG - Concave Subject Split.png\|Concave Subject Split]] | The two lobes of the concave subject of §3.9 |
| [[CG - Weiler Atherton Crossings.png\|Weiler Atherton Crossings]] | The four exit/entry crossings of §3.10 |
| [[CG - Tetrahedron Back Face Result.png\|Tetrahedron Back Face Result]] | The two retained faces of the tetrahedron of §4.2 |
| [[CG - BSP Traversal Order.png\|BSP Traversal Order]] | The deck's annotated draw order of §5.8 |
| [[CG - Bitmapped Font L.png\|Bitmapped Font L]] | The $5\times7$ bitmap of §6.14 |
| [[CG - Outlined Font L.png\|Outlined Font L]] | The six-vertex outline of §6.15 |
| [[CG - Gupta Sproull E vs NE Case.png\|Gupta Sproull E vs NE Case]] | The E and NE cases and the sign of $s$ of §7.8 |

---

## Open gaps

> [!warning] What is still missing
> - **The whole pre-midsem block (topics 1–8)** has no written note yet — [[CG_Midsem_notes]] is empty. The checkboxes above are the work list.
> - [[Between - Intensity Quantization (17 Sep).pdf|Intensity Quantization (17 Sep)]] (intensity quantization) is unwritten and sits between the two blocks, so it appears in neither list.
> - [[Post 6 - Fill-Area Algorithms, Scan Conversion and the 3D Pipeline.pdf|Post 6]] pages 35–57 and 64–74 export as **mojibake** (embedded fonts with no glyphs). Those sections of §6 were reconstructed from the readable neighbouring pages and from the standard formulation of each algorithm; no number in them is invented, but the deck's own wording for those pages is lost.
> - [[Post 5 - Hidden Surface Removal II - Painter's Algorithm and BSP Trees.pdf|Post 5]] is 80 slides but only about 20 of them are unique — the rest are annotation repeats of the same BSP example. Read the unique pages, not the count.
> - [[Post 8 - Animation - The 2D Production Process.pdf|Post 8]] is handwritten and extracts almost no text (≈186 bytes over 55 pages). §8 answers the one question the deck poses, but nothing else in the deck could be recovered.

> [!question] Self-check before you tick a topic
> - Can you state the topic's **key formula** from memory and say what it assumes — a right-handed frame, the viewer on $-z$, ties counted as inside?
> - Can you draw the **figure** that carries the topic — the frustum, the nine outcode regions, the four clipping cases, the BSP draw order, the scan-line AET, the coverage pair, the jump arc?
> - Can you run the **trace** end to end with real numbers, and name the **one trap** the lecturer flagged?
