---
title: Material Science — MO-201 End-Sem Solutions (Endsem-1 and Endsem 2)
tags:
  - materials-science
  - MO-201
  - end-sem
  - endsem-1
  - endsem-2
---

# Endsem-1 Solutions — MO 201 Materials Science

Worked solutions to the first End-Sem paper, [[endsem1.pdf]] (IIT (BHU) Varanasi, Odd Sem 2025–26, 3 hours, 50 marks; attempt any 10 of 12 questions, all of equal marks). Every answer is built from [[notes]] (cited by section, e.g. §4.3) and the lecture PDFs behind it — [[Shockley and Frank partial dislocations_Odd_2026-27.pdf]], [[Mechanical Properties part 2_Odd_2026-27.pdf]], [[Mechanical Properties part 3_Odd_2026-27.pdf]], [[Composites_Odd_2026-27.pdf]], [[Phase_Diagrams.pdf]], [[Electrical and Electronic Properties - Part 1_Odd_2026-27.pdf]], [[Electrical and Electronic Properties - Part 2_Odd_2026-27.pdf]], [[Magnetic Properties_Odd_2026-27.pdf]] and [[Dielectric materials_Polarization_Optical properties_Odd_2026-27.pdf]] — following the conventions of [[context]]. Where a point goes beyond the slides it is marked *added depth*.

> [!info] How to use this note
> Each question is a card; click **Solution** to expand it. The marks split printed in the paper is kept in each card header, and each answer is sized to that split. Questions are in paper order; the table below maps each one to its syllabus topic so that a missed question can be traced back to [[notes]].

| Q | Topic | Marks | Where it lives in [[notes]] |
| --- | --- | --- | --- |
| **1** | Shockley and Frank partials (FCC), Shockley partials (HCP) | 2 + 2 + 1 | §4.1–§4.8 |
| **2** | DBTT and Yoffee diagram; sessile dislocation by a reaction | 3 + 2 | §2.7, §2.5 |
| **3** | Brinell, Rockwell, Vickers; 3-point bending | 3 + 2 | §3.1, §3.5–§3.7 |
| **4** | Cermets, hybrid composites, critical fibre length | 2 + 2 + 1 | §5.6, §5.16, §5.9 |
| **5** | Carbon black vs silica; structural composites | 1 + 4 | §5.6, §5.18 |
| **6** | Iron–carbon phase diagram | 5 | [[Phase_Diagrams.pdf]] |
| **7** | Ag–Pt and Pb–Sn diagrams; lever rule | 2 + 2 + 1 | [[Phase_Diagrams.pdf]] |
| **8** | Free electron theory and conduction | 5 | §6.2–§6.6 |
| **9** | Intrinsic, p-type and n-type semiconductors | 1 + 2 + 2 | §7.7–§7.10 |
| **10** | Conductivity vs $T$ (extrinsic); p-n junction bias | 3 + 2 | §7.11, §7.13–§7.14 |
| **11** | Heusler alloys, Zn in NiFe₂O₄, ferrimagnetism | 2 + 2 + 1 | §8.9, §8.11–§8.13 |
| **12** | Polarization mechanisms; ferroelectricity of BaTiO₃ | 3 + 2 | §9.3–§9.9 |

---

## Q1. Shockley and Frank partials

> [!question] Q1: Explain (a) Shockley and (b) Frank partial dislocations in FCC. (c) Write the dislocation reaction for Shockley partial dislocations in HCP. [2 + 2 + 1 = 5]
>
> > [!success]- Solution (Click to expand)
> > **Background — why a perfect dislocation splits.** A dislocation's elastic energy per unit length is $E_{el} \approx \alpha G b^2$, so replacing one long Burgers vector by two shorter ones with the same vector sum lowers the energy. In FCC the perfect dislocation is $\mathbf{b} = \tfrac{a}{2}\langle110\rangle$, with $b^2 = a^2/2$. The close-packed $\{111\}$ planes stack as $\ldots ABCABC\ldots$, and a partial dislocation is one whose Burgers vector is *not* a lattice translation, so it leaves a **stacking fault** behind it (§4.1–§4.2).
> >
> > ![[SD - Dissociation into Shockley partials.excalidraw]]
> >
> > **(a) Shockley partial** [2 marks]
> >
> > - A **Shockley partial** is a partial dislocation with $\mathbf{b} = \tfrac{a}{6}\langle112\rangle$, magnitude $b_p = a/\sqrt6 = 0.408\,a = b/\sqrt3$.
> > - Its Burgers vector lies **in** the $\{111\}$ plane of the fault it bounds, so it is **glissile**: it glides conservatively in that plane. Glide of the leading partial *creates* an intrinsic stacking fault (one wrong layer, $ABC\,A\,|\,C\,A\,B\ldots$); glide of the trailing partial *removes* it.
> > - It is formed by the **dissociation** of a perfect dislocation into two Shockley partials:
> >
> > $$ \frac{a}{2}[1\bar{1}0] \;\longrightarrow\; \frac{a}{6}[2\bar{1}\bar{1}] + \frac{a}{6}[1\bar{2}1] \qquad \text{on the } (111) \text{ plane} $$
> >
> > Checks:
> >
> > 1. **Burgers-vector conservation** — $\tfrac{a}{6}[2\bar{1}\bar{1}] + \tfrac{a}{6}[1\bar{2}1] = \tfrac{a}{6}[3\bar{3}0] = \tfrac{a}{2}[1\bar{1}0]$ ✓.
> > 2. **Frank's rule (energy)** — $b_1^2 + b_2^2 = \tfrac{a^2}{6} + \tfrac{a^2}{6} = \tfrac{a^2}{3} < \tfrac{a^2}{2} = b^2$: a **33 % energy saving**, so dissociation is always favourable in FCC.
> > 3. **Geometry** — the parent and both partials lie in the fault plane $(111)$: $[1\bar{1}0]\cdot[111] = 0$, $[2\bar{1}\bar{1}]\cdot[111] = 0$ and $[1\bar{2}1]\cdot[111] = 0$ ✓. Each partial is $30^\circ$ from the parent vector ($\cos\theta = 3/\sqrt{12} = 0.866$) and the two are $60^\circ$ apart.
> >
> > - The two partials repel; the fault ribbon between them pulls them together. They settle at the **equilibrium separation** where repulsion balances the fault energy $\gamma_{SF}$ — the pair is an **extended dislocation**, with $d \propto G b_p^2/\gamma_{SF}$.
> >
> > $$ \boxed{\ \frac{a}{2}\langle110\rangle \longrightarrow \frac{a}{6}\langle112\rangle + \frac{a}{6}\langle112\rangle, \qquad b^2:\ \frac{a^2}{2} \to \frac{a^2}{3}\ } $$
> >
> > **(b) Frank partial** [2 marks]
> >
> > - A **Frank partial** is a pure **edge** partial dislocation with $\mathbf{b} = \tfrac{a}{3}\langle111\rangle$, with $|\mathbf{b}_F| = a/\sqrt3$, which is exactly the $\{111\}$ interplanar spacing $d_{111}$; $b_F^2 = a^2/3$.
> > - Its Burgers vector is **normal** to the fault plane, not in it. It therefore **cannot glide**: gliding would require dragging the fault disc with it, which is non-conservative. It is **sessile**, and can move only by **climb** (absorbing or emitting vacancies/interstitials).
> > - **Formation:** vacancies supersaturated by quenching or irradiation condense on a $\{111\}$ plane as a flat plate; the plate **collapses** by one plane spacing, leaving an *intrinsic* stacking fault on the plane, and the rim of the faulted disc is a **Frank loop** of vacancy type. Condensation of interstitials gives an *extrinsic* fault bounded by an interstitial-type loop.
> > - **Removal:** by climb (high temperature), or by **unfaulting** when a Shockley partial sweeps the faulted plane and reacts with the Frank partial:
> >
> > $$ \frac{a}{3}[111] + \frac{a}{6}[11\bar{2}] \longrightarrow \frac{a}{2}[110] $$
> >
> > $$ \boxed{\ \mathbf{b}_F = \frac{a}{3}\langle111\rangle,\qquad |\mathbf{b}_F| = \frac{a}{\sqrt3} = d_{111},\qquad \mathbf{b}_F \perp \text{fault plane} \ \Rightarrow\ \text{sessile}\ } $$
> >
> > ![[SD - Frank partial from a vacancy plate.excalidraw]]
> >
> > | | **Shockley partial** | **Frank partial** |
> > | --- | --- | --- |
> > | Burgers vector | $\tfrac{a}{6}\langle112\rangle$ | $\tfrac{a}{3}\langle111\rangle$ |
> > | $b^2$ | $a^2/6$ | $a^2/3$ |
> > | $\mathbf{b}$ vs fault plane | **lies in** the plane | **normal** to the plane |
> > | Character | mixed ($30^\circ$ to parent $\mathbf{b}$) | pure edge |
> > | Mobility | **glissile** | **sessile** (climb only) |
> > | Created by | dissociation of $\tfrac{a}{2}\langle110\rangle$ | collapse of a vacancy / interstitial plate |
> > | Found in | every FCC metal, always | quenched, irradiated, fatigued metals |
> >
> > **(c) Shockley partials in HCP** [1 mark]
> >
> > In HCP the close-packed plane is the **basal plane** $(0001)$, stacked $\ldots ABABAB\ldots$, and the perfect dislocation on it is $\mathbf{b} = \tfrac{a}{3}\langle11\bar{2}0\rangle$ with $b^2 = a^2$. It dissociates into two Shockley partials of type $\tfrac{a}{3}\langle10\bar{1}0\rangle$, lying in the basal plane, with a stacking-fault ribbon between them:
> >
> > $$ \boxed{\ \frac{a}{3}[11\bar{2}0] \;\longrightarrow\; \frac{a}{3}[10\bar{1}0] + \frac{a}{3}[01\bar{1}0]\ } $$
> >
> > Check the vector sum: $[10\bar{1}0] + [01\bar{1}0] = [11\bar{2}0]$ ✓. Check the energy (Frank's rule): $|\tfrac{a}{3}\langle10\bar{1}0\rangle|^2 = a^2/3$ for each partial, so $b_1^2 + b_2^2 = \tfrac{2a^2}{3} < a^2$ ✓ — dissociation is favourable. *Added depth beyond the slides:* the HCP partial vectors are quoted from standard dislocation theory rather than the lecture slides, which treat the FCC case in detail.

> [!tip] Exam pointer — Q1
> Quote the dissociation equation with its **three checks** (vector sum, $a^2/2 \to a^2/3$, partials in the fault plane), state $b_p = a/\sqrt6$ and $b_F = a/\sqrt3 = d_{111}$, and say that the Frank partial is sessile **because $\mathbf{b}$ is normal to the fault plane** — not because it is an edge dislocation (§4.8).

---

## Q2. DBTT, the Yoffee diagram, and a sessile lock

> [!question] Q2: (a) Explain ductile to brittle transition in iron and Yoffee diagram. (b) Explain with diagram the formation of a sessile dislocation in an FCC crystal by a dislocation reaction. [3 + 2 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Ductile-to-brittle transition and the Yoffee diagram** [3 marks]
> >
> > The same material gives quite different tensile curves at different temperatures. For **iron**:
> >
> > | Temperature | Behaviour |
> > | --- | --- |
> > | $-200\ ^\circ\text{C}$ | Very high yield stress, almost no plasticity — **brittle** |
> > | $-100\ ^\circ\text{C}$ | Some ductility, much less than at room temperature — **transition** |
> > | $25\ ^\circ\text{C}$ | Long plastic region and pronounced necking — **ductile** |
> >
> > ![[MP2 - Iron curves at three temperatures.png|440]]
> >
> > *Figure — the same material (iron) tested at $-200$, $-100$ and $25\ ^\circ\text{C}$: the low-temperature curve is almost linear to fracture; the room-temperature curve shows a long plastic region and a neck.*
> >
> > Iron is BCC, so its screw dislocations have non-planar cores and a large Peierls barrier: motion past obstacles needs thermal help, and the yield stress is strongly temperature-dependent.
> >
> > **The Yoffee diagram.** Plot two curves against temperature:
> >
> > 1. the **yield stress** $\sigma_y$ — it *falls* as $T$ rises, because dislocation motion past obstacles is thermally activated;
> > 2. the **cleavage fracture stress** $\sigma_f$ — it is nearly *temperature-independent* (athermal), because breaking bonds across a plane needs no diffusion or thermal activation.
> >
> > ![[MP - Yoffee Diagram DBTT.excalidraw]]
> >
> > ![[MP2 - Yoffee diagram.png|380]]
> >
> > *Figure — the Yoffee diagram: yield stress falls with temperature, cleavage fracture stress is nearly temperature-independent, and the intersection defines the DBTT.*
> >
> > The two curves cross at the **Ductile–Brittle Transition Temperature (DBTT)**:
> >
> > - **Below DBTT:** $\sigma_f < \sigma_y$ — the stress reaches the cleavage value *before* plastic flow can blunt the crack, so the material **fractures before it yields → brittle**.
> > - **Above DBTT:** $\sigma_y < \sigma_f$ — the material **yields first**, the plastic zone blunts the crack tip, and it is **ductile**.
> >
> > $$ \boxed{\ T < T_{\text{DBTT}}:\ \sigma_f < \sigma_y\ (\text{brittle}) \qquad\quad T > T_{\text{DBTT}}:\ \sigma_y < \sigma_f\ (\text{ductile})\ } $$
> >
> > The same transition appears in the Charpy test as an S-shaped energy–temperature curve: *lower shelf* (cleavage, low energy), a steep *transition* region, and *upper shelf* (ductile, high energy).
> >
> > **What raises the DBTT** (makes iron more brittle): lower service temperature; high strain rate or impact loading (less time for thermal activation, so $\sigma_y$ rises); a sharp notch (triaxial stress suppresses shear yielding); coarse grains; and impurities and high carbon. FCC alloys such as austenitic stainless steel, aluminium and nickel alloys have no such transition, which is why they serve at cryogenic temperatures.
> >
> > **(b) A sessile dislocation from a dislocation reaction — the Lomer lock** [2 marks]
> >
> > Dislocations gliding on **non-parallel** $\{111\}$ planes meet along the line where their planes intersect and can **react**. A reaction proceeds if the Burgers vector is conserved and the strain energy ($\propto b^2$) falls (**Frank's rule**): $\mathbf{b}_3 = \mathbf{b}_1 + \mathbf{b}_2$ and $b_3^2 < b_1^2 + b_2^2$.
> >
> > ![[MP - Dislocation Reaction Sessile Lock.excalidraw]]
> >
> > Take $\mathbf{b}_1 = \tfrac{a}{2}[10\bar{1}]$ gliding on $(111)$ and $\mathbf{b}_2 = \tfrac{a}{2}[011]$ gliding on $(11\bar{1})$. (Each lies in its own plane: $[10\bar{1}]\cdot[111] = 0$ and $[011]\cdot[11\bar{1}] = 0$.) The two planes intersect along $[1\bar{1}0]$, and the dislocations react there:
> >
> > $$ \frac{a}{2}[10\bar{1}] + \frac{a}{2}[011] \;\longrightarrow\; \frac{a}{2}[110] $$
> >
> > $$ b_1^2 + b_2^2 = \frac{a^2}{2} + \frac{a^2}{2} = a^2 \;\longrightarrow\; b_3^2 = \frac{a^2}{2} \qquad (50\,\%\ \text{energy decrease}) $$
> >
> > The reaction is therefore favourable. The product $\tfrac{a}{2}[110]$ is perpendicular to the line $[1\bar{1}0]$, so its glide plane (the plane containing both $\mathbf{b}$ and the line) is $(001)$ — a $\{100\}$-type plane, which is **not** a close-packed slip plane of FCC. It cannot glide: it is **sessile** (a *Lomer lock*).
> >
> > ![[MP2 - Lomer sessile lock formation.png|440]]
> >
> > *Figure — two mobile dislocations on non-parallel $\{111\}$ planes meet along the line of intersection and react to form a sessile dislocation; further glide on either plane is blocked and dislocations pile up behind the lock.*
> >
> > **Consequence.** Dislocations on both planes pile up behind the lock, producing a long-range back stress that opposes the applied stress. A higher stress is therefore needed for further deformation — a basic mechanism of **work hardening**.
> >
> > $$ \boxed{\ \tfrac{a}{2}[10\bar{1}] + \tfrac{a}{2}[011] \to \tfrac{a}{2}[110],\qquad a^2 \to \tfrac{a^2}{2},\ \text{product sessile}\ } $$

> [!tip] Exam pointer — Q2
> For (a) draw the two curves and **label the intersection DBTT**, then write the two inequalities — most marks go to *why* the curves have those slopes (yield thermally activated, cleavage athermal). For (b) check the plane normals with dot products before writing the reaction (§2.5).

---

## Q3. Hardness tests and the three-point bend test

> [!question] Q3: Explain (a) Brinell, Rockwell, Vickers hardness tests (b) 3-point bending test. [3 + 2 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Hardness tests** [3 marks]
> >
> > > **Hardness** is the resistance of a material to *localised plastic deformation* — a small dent or scratch. A small indenter is forced into the surface under a specified load and loading rate, and the depth or size of the indent is measured: the softer the material, the larger the indent.
> >
> > ![[MP - Hardness Indenters.excalidraw]]
> >
> > **Brinell test**
> >
> > - A hardened steel or tungsten-carbide **ball of $D = 10\ \text{mm}$** is pressed into the surface; standard loads are 500–3000 kg in 500 kg steps, held for 10–30 s.
> > - The **diameter $d$ of the circular indent** is measured under a microscope. Hardness is the load divided by the *curved surface area* of the spherical cap, whose depth is $h = \tfrac{D - \sqrt{D^2 - d^2}}{2}$:
> >
> > $$ \boxed{\ HB = \frac{2P}{\pi D\left[D - \sqrt{D^2 - d^2}\right]}\ } $$
> >
> > - There is only one Brinell scale, and the load must be quoted with the number. The large indent (about 1–5 mm) averages a coarse microstructure (good for cast iron) but is unsuitable for thin parts.
> >
> > **Rockwell test**
> >
> > - The number comes from the **difference in depth of penetration** between a **minor load** (10 kg — it seats the indenter and removes surface-roughness error) and a **major load**. The depth is read directly from a dial, so the test is fast.
> > - Letter scales combine an indenter and a major load — e.g. **A** (diamond cone, 60 kg), **B** ($\tfrac{1}{16}$ in. ball, 100 kg), **C** (diamond, 150 kg); superficial scales 15N/30N/45N and 15T/30T/45T are for thin specimens.
> > - With $h$ the permanent depth increase in mm (one hardness point per $0.002$ mm):
> >
> > $$ \boxed{\ HR = 100 - \frac{h}{0.002}\ \text{(diamond cone)} \qquad HR = 130 - \frac{h}{0.002}\ \text{(ball)}\ } $$
> >
> > - Readings are unreliable below about 20 and above about 100.
> >
> > **Vickers (microindentation) test**
> >
> > - A **square-based diamond pyramid with a $136^\circ$ included angle** is pressed in with a load of 1–1000 g; the two **diagonals** of the impression are measured under a microscope (after careful grinding and polishing of the surface).
> > - Hardness is load divided by the contact area of the four faces, $A = \dfrac{d^2}{2\sin 68^\circ}$:
> >
> > $$ \boxed{\ HV = \frac{2P\sin 68^\circ}{d^2} = 1.854\,\frac{P}{d^2}\ } $$
> >
> > - Because the pyramid is self-similar, HV is in principle independent of load. The indent is small enough to sit inside a single grain, so Vickers measures individual phases, thin coatings and case depth.
> >
> > | | **Brinell** | **Rockwell** | **Vickers** |
> > | --- | --- | --- | --- |
> > | Indenter | 10 mm steel / WC ball | Diamond cone or steel ball | $136^\circ$ diamond pyramid |
> > | Load | 500–3000 kg | 15–150 kg | 1–1000 g |
> > | Measured | Indent diameter $d$ | Depth increase $h$ | Mean diagonal $d$ |
> > | Speed | Slow (microscope) | Fast (dial) | Slow (microscope) |
> > | Best for | Cast iron, coarse structures | Routine QC of metals | Hard materials, single phases, coatings |
> >
> > ![[MP3 - Hardness testing techniques table.png|480]]
> >
> > *Figure — the lecture table (Callister, Table 7.5) of hardness-testing techniques with indenter shapes, side/top views, formulas and the standard designation of each number.*
> >
> > **(b) Three-point bending test** [2 marks]
> >
> > Ceramics are hard and brittle: a waisted tensile specimen is hard to machine, gripping creates stress concentrations that fracture the specimen prematurely, and the tensile strength is only about one-tenth of the compressive strength. The **three-point bend test** avoids all three problems.
> >
> > ![[MP - Three Point Bending.excalidraw]]
> >
> > - A rectangular (or circular) bar rests on **two support pins** a distance $L$ apart and is loaded at **mid-span** — three contact points.
> > - The **top surface is in compression and the bottom surface in tension**. Ceramics are far weaker in tension, so **fracture starts on the bottom (tensile) face**.
> > - From beam theory $\sigma = Mc/I$ with $M_{\max} = FL/4$; for a rectangular section $I = bd^3/12$ and $c = d/2$, giving
> >
> > $$ \sigma = \frac{(FL/4)(d/2)}{bd^3/12} = \frac{3FL}{2bd^2} $$
> >
> > $$ \boxed{\ \sigma_{fs} = \frac{3F_fL}{2bd^2}\ \text{(rectangular)} \qquad \sigma_{fs} = \frac{F_fL}{\pi r^3}\ \text{(circular)}\ } $$
> >
> > where $F_f$ is the fracture load, $b$ the width, $d$ the depth and $r$ the radius. This stress at fracture is the **flexural strength**, also called the modulus of rupture or bend strength.
> >
> > ![[MP3 - Three point bending test.png|420]]
> >
> > *Figure — the three-point bend arrangement: a bar on two support pins, loaded at mid-span, with the top surface in compression and the bottom surface in tension; the two standard cross-sections (rectangular and circular) are also shown.*

> [!tip] Exam pointer — Q3
> Give **indenter + load + what is measured + formula** for each hardness test, and for bending write the $\sigma = Mc/I$ derivation to $3FL/2bd^2$ (§3.1, §3.5–§3.7). Assumptions: elastic beam, small deflection, negligible shear.

---

## Q4. Cermets, hybrid composites, critical fibre length

> [!question] Q4: What are (a) cermets and (b) hybrid composites? (c) What is the importance of critical fiber length? [2 + 2 + 1 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Cermets** [2 marks]
> >
> > **Cermets** are **ceramic–metal** composites and the classic example of a *large-particle composite*. The most common cermet is **cemented carbide**: extremely hard particles of a refractory carbide ceramic — **tungsten carbide (WC)** or **titanium carbide (TiC)** — embedded in a matrix of a metal such as **cobalt or nickel**.
> >
> > - Used extensively as **cutting tools for hardened steels**.
> > - **Toughness is enhanced** by the ductile metal matrix, which isolates the carbide particles from one another and stops cracks running from particle to particle.
> > - Both matrix and particles are **refractory**, so the material withstands the high temperatures of cutting.
> > - Particle volume fractions are large — often **above 90 vol.%** — and no single material could give this combination of properties.
> >
> > **(b) Hybrid composites** [2 marks]
> >
> > A **hybrid composite** contains **two or more different kinds of fibres in a single matrix**, giving a better all-round combination of properties than a composite with only one fibre type.
> >
> > - The commonest system is **carbon + glass fibres in a polymeric resin**. Carbon fibres are strong, stiff and light but expensive; glass fibres are cheap but less stiff. The **glass–carbon hybrid** is stronger and tougher, has higher impact resistance, and can cost less than either the all-carbon or all-glass composite.
> > - The fibres may be aligned and intimately mixed, or laid up in alternating layers of one type; in virtually all hybrids the properties are **anisotropic**.
> > - Failure in tension is **non-catastrophic**: the carbon fibres fail first and load transfers to the glass fibres; when the glass fails the matrix carries the load; final failure coincides with failure of the matrix.
> > - Applications: lightweight land, water and air transport structures, sporting goods, lightweight orthopaedic components.
> >
> > **(c) Importance of the critical fibre length** [1 mark]
> >
> > The matrix loads a fibre by **shear along the interface**, so the fibre stress is zero at each end and rises towards the centre. The **critical fibre length $l_c$** is the shortest length for which the fibre can be loaded to its ultimate tensile strength $\sigma_f^*$:
> >
> > $$ \sigma_f^*\,\frac{\pi d^2}{4} = \tau_c\,\pi d\,\frac{l_c}{2} \quad\Longrightarrow\quad \boxed{\ l_c = \frac{\sigma_f^* d}{2\tau_c}\ } $$
> >
> > where $d$ is the fibre diameter and $\tau_c$ is the fibre–matrix bond strength or the matrix shear yield strength, whichever is smaller.
> >
> > ![[COMP - Fiber stress profiles at critical length.png|430]]
> >
> > *Figure — stress–position profiles for a fibre-reinforced composite loaded to the fibre tensile strength $\sigma_f^*$: (a) $l=l_c$, where the maximum fibre stress is reached only at the axial centre; (b) $l>l_c$, where the fibre is more effectively loaded; (c) $l<l_c$, where the fibre never reaches its strength and pulls out instead of fracturing.*
> >
> > | Fibre length | What happens |
> > | --- | --- |
> > | $l < l_c$ | Fibre never reaches $\sigma_f^*$ — it **pulls out**; little reinforcement |
> > | $l = l_c$ | Peak stress $\sigma_f^*$ reached only at the centre |
> > | $l > l_c$ | Fibre loaded to its full strength over most of its length — effective reinforcement |
> > | $l > 15\,l_c$ | Treated as **continuous** |
> >
> > For common glass and carbon fibres $l_c \approx 1\ \text{mm}$, i.e. 20–150 times the fibre diameter. $l_c$ therefore tells the designer how long the fibres must be to reinforce effectively.

> [!tip] Exam pointer — Q4
> Memorise $l_c = \sigma_f^* d/2\tau_c$, its force-balance derivation, and the $l<l_c$ / $l>l_c$ / $l>15l_c$ ladder (§5.9).

---

## Q5. Carbon black and structural composites

> [!question] Q5: (a) Why is carbon black used and not silica as particle reinforcement in vulcanized rubber? (b) Explain the types of structural composites. [1 + 4 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Carbon black rather than silica** [1 mark]
> >
> > Carbon black — very small, essentially spherical carbon particles from the combustion of natural gas or oil in limited air — greatly improves **tensile strength, toughness, tear and abrasion resistance** of vulcanised rubber; tyres contain about 15–30 vol.% of it. For significant reinforcement the particles must be extremely small (**20–50 nm**), evenly distributed, and form a **strong adhesive bond** with the rubber matrix. Carbon black does this because of a **special interaction between the rubber molecules and the carbon particle surfaces**; with other particles such as **silica** that special interaction does not exist, so reinforcement is much less effective. It is also extremely inexpensive.
> >
> > **(b) Types of structural composites** [4 marks]
> >
> > A **structural composite** is a multi-layered, normally low-density composite used where structural integrity — high tensile, compressive and torsional strength and stiffness — is needed. Its properties depend on the constituent materials *and* on the **geometrical design** of the structural elements. The two most common types are **laminar composites** and **sandwich panels**.
> >
> > *1. Laminar composites (laminates).* Two-dimensional sheets or **plies** (laminae), each with a preferred high-strength direction (as in continuous aligned fibre polymers), are bonded together. Properties depend on how the high-strength direction changes from ply to ply:
> >
> > | Class | Stacking pattern | Consequence |
> > | --- | --- | --- |
> > | **Unidirectional** | Same high-strength direction in every ply | Maximum axial stiffness and strength; highly anisotropic |
> > | **Cross-ply** | Alternating $0^\circ$ and $90^\circ$ layers | Stiffness in two perpendicular directions; more balanced |
> > | **Angle-ply** | Alternating $+\theta$ and $-\theta$ (e.g. $\pm45^\circ$) | Good shear and torsion resistance |
> > | **Multidirectional** | Several orientations | Most isotropic in-plane response |
> >
> > ![[COMP - Classes of laminar composites.png|360]]
> >
> > *Figure — the four classes of laminar composites: (a) unidirectional, (b) cross-ply, (c) angle-ply and (d) multidirectional. The arrows show the high-strength direction of each ply.*
> >
> > Layers are stacked **symmetrically about the midplane** to prevent out-of-plane twisting or bending. Applications: aircraft fuselage and stabilizers, automobile panels and drive shafts, ship hulls and decks, bridge components and roof structures, the modern ski.
> >
> > *2. Sandwich panels.* A lightweight beam or panel with high stiffness and strength: two outer sheets (**faces** or skins) separated by, and adhesively bonded to, a thicker **core**.
> >
> > - **Faces** are stiff and strong (aluminium alloys, steel, stainless steel, fibre-reinforced plastics, plywood) and carry the **bending loads** — one face in compression, the other in tension.
> > - The **core** is lightweight with a low modulus; it supports the faces continuously, holds them apart, and resists **transverse shear** (it needs adequate shear strength and enough thickness for shear stiffness, to resist buckling).
> > - Panel stiffness depends mainly on **core material and thickness**. Core materials are **rigid polymeric foams, wood, and honeycombs**. Strong face–core bonding is essential, and the panel is cost-effective because cores are cheaper than faces.
> >
> > ![[COMP - Sandwich panel cross section.png|380]]
> >
> > *Figure — cross-section of a sandwich panel: two stiff, strong faces separated by a thick, lightweight core. The faces carry bending stress; the core carries transverse shear and keeps the faces apart.*
> >
> > ![[COMP - Honeycomb core sandwich panel.png|460]]
> >
> > *Figure — construction of a honeycomb-core sandwich panel: face sheets are adhesively bonded to a honeycomb core, giving high bending stiffness at low weight.*

> [!tip] Exam pointer — Q5
> For (b) the answer is "laminates (4 classes) + sandwich panels (faces, core, three core types)"; for (a) say *size 20–50 nm* and *rubber–particle surface interaction absent in silica* (§5.6, §5.18).

---

## Q6. The iron–carbon phase diagram

> [!question] Q6: Draw the iron-carbon phase diagram showing all the phases and invariant reactions. [5]
>
> > [!success]- Solution (Click to expand)
> > ![[PD - Iron Carbon Phase Diagram.png|520]]
> >
> > *Figure — the Fe–Fe₃C phase diagram: temperature (°C) against wt% C from 0 to 6.7, with the peritectic at 1493 °C, the eutectic at 1147 °C (4.30 wt% C), the eutectoid at 727 °C (0.76 wt% C), the critical lines A₁, A₃, A₄ and A$_{cm}$, and the typical microstructures of hypo-eutectoid, eutectoid and hyper-eutectoid steels.*
> >
> > The components are **iron** and **iron carbide (Fe₃C, cementite, 6.7 wt% C)**. Fe₃C is metastable; in the stable system the second component is graphite.
> >
> > **Phases**
> >
> > | Phase | Description | Max. carbon dissolved |
> > | --- | --- | --- |
> > | **L** | Liquid solution of C in Fe | — |
> > | **$\delta$** | High-temperature BCC solid solution (1394–1538 °C) | $\sim$0.09 wt% C at 1493 °C |
> > | **$\gamma$ (austenite)** | FCC solid solution | 2.14 wt% C at 1147 °C |
> > | **$\alpha$ (ferrite)** | BCC solid solution | 0.022 wt% C at 727 °C |
> > | **Fe₃C (cementite)** | Hard, brittle intermetallic compound | 6.7 wt% C (fixed) |
> >
> > Pure iron: melts at 1538 °C; $\delta \leftrightarrow \gamma$ at 1394 °C; $\gamma \leftrightarrow \alpha$ at 912 °C.
> >
> > **Invariant reactions** (three phases in equilibrium; $F = 0$ at fixed pressure)
> >
> > | Reaction | Name | Temperature | Compositions (wt% C) |
> > | --- | --- | --- | --- |
> > | $\delta + L \rightleftharpoons \gamma$ | **Peritectic** | 1493 °C | $\delta \approx 0.09$, $L \approx 0.53$, $\gamma \approx 0.17$ |
> > | $L \rightleftharpoons \gamma + \text{Fe}_3\text{C}$ | **Eutectic** (forms *ledeburite*) | 1147 °C | $L = 4.30$, $\gamma = 2.14$ |
> > | $\gamma \rightleftharpoons \alpha + \text{Fe}_3\text{C}$ | **Eutectoid** (forms *pearlite*) | 727 °C ($A_1$) | $\gamma = 0.76$, $\alpha = 0.022$ |
> >
> > $$ \boxed{\ \delta + L \xrightarrow{1493\,^\circ\text{C}} \gamma \qquad L \xrightarrow{1147\,^\circ\text{C}} \gamma + \text{Fe}_3\text{C} \qquad \gamma \xrightarrow{727\,^\circ\text{C}} \alpha + \text{Fe}_3\text{C}\ } $$
> >
> > **Critical lines and regions**
> >
> > - **$A_1$** — the 727 °C eutectoid horizontal; **$A_3$** — the $\gamma/(\alpha+\gamma)$ boundary falling from 912 °C to 0.76 wt% C; **$A_{cm}$** — the $\gamma/(\gamma + \text{Fe}_3\text{C})$ boundary rising to 2.14 wt% C at 1147 °C; **$A_4$** — the $\delta/\gamma$ boundary at 1394 °C.
> > - **Steels** (up to 2.14 wt% C): *hypo-eutectoid* below 0.76 wt% C (proeutectoid ferrite + pearlite), *eutectoid* at 0.76 wt% C (all pearlite), *hyper-eutectoid* above 0.76 wt% C (proeutectoid cementite + pearlite).
> > - **Cast irons** (2.14–6.7 wt% C): austenite + ledeburite and cementite at 2.14–4.30 wt% C below the eutectic, and cementite + ledeburite above 4.30 wt% C.
> > - Below 727 °C the two-phase field is $\alpha + \text{Fe}_3\text{C}$ throughout.
> >
> > *Added depth beyond the slides:* the invariant-reaction compositions of the peritectic (0.09, 0.53, 0.17 wt% C) are the standard textbook values (Callister) — the lecture figure labels only the temperature 1493 °C.

> [!tip] Exam pointer — Q6
> Draw the diagram, **label the three invariant temperatures and compositions** (1493 °C peritectic; 1147 °C / 4.30 eutectic; 727 °C / 0.76 eutectoid), the single-phase fields L, $\delta$, $\gamma$, $\alpha$, Fe₃C, and write the three reactions.

---

## Q7. Ag–Pt and Pb–Sn diagrams, and the lever rule

> [!question] Q7: Draw the Ag-Pt and Pb-Sn phase diagrams and explain the invariant reactions in each. What is Lever rule? [2 + 2 + 1 = 5]
>
> > [!success]- Solution (Click to expand)
> > **Invariant reactions.** A reaction at which three phases coexist in a binary system, with zero degrees of freedom ($F = C - P + 1 = 2 - 3 + 1 = 0$), is **invariant**: it proceeds isothermally at a fixed temperature and with fixed phase compositions. The four types met in binary diagrams are:
> >
> > | Reaction | On cooling |
> > | --- | --- |
> > | Eutectic | $L \leftrightarrow \alpha + \beta$ |
> > | Eutectoid | $\gamma \leftrightarrow \alpha + \beta$ |
> > | Peritectic | $L + \beta \leftrightarrow \alpha$ |
> > | Peritectoid | $\gamma + \beta \leftrightarrow \alpha$ |
> >
> > **(a) The silver–platinum diagram — a peritectic system** [2 marks]
> >
> > ![[PD - Silver Platinum Phase Diagram.png|380]]
> >
> > *Figure — the Ag–Pt phase diagram: Ag melts at 961 °C and Pt at 1769 °C; the horizontal at 1185 °C is the peritectic, $T_p$, with the peritectic composition $c_p$ marked.*
> >
> > - **When it forms:** the melting points of the components are **vastly different** (961 °C against 1769 °C), and solid solubility is limited — a peritectic diagram results.
> > - **Phases:** liquid $L$; $\alpha$ (Ag-rich solid solution); $\beta$ (Pt-rich solid solution); two-phase fields $L+\alpha$, $L+\beta$, $\alpha+\beta$.
> > - **Invariant reaction — peritectic**, at $T_p = 1185\ ^\circ\text{C}$:
> >
> > $$ \boxed{\ L + \beta \;\underset{\text{heating}}{\overset{\text{cooling}}{\rightleftharpoons}}\; \alpha \qquad (T_p = 1185\,^\circ\text{C})\ } $$
> >
> > - Reading the figure, the three phases at the horizontal are the liquid at about 20 wt% Pt, the $\alpha$ phase at the peritectic composition $c_p$ (about 40 wt% Pt) and $\beta$ at about 78 wt% Pt. On cooling through $T_p$, the liquid **reacts with** the already-formed solid $\beta$ to produce a *new* solid $\alpha$ — the liquid is consumed, not split into two solids as in a eutectic.
> > - The horizontal is a tie-line whose ends give the compositions of the three phases; $F = 0$ there.
> >
> > **(b) The lead–tin diagram — a eutectic system** [2 marks]
> >
> > ![[PD - Lead Tin Phase Diagram.png|380]]
> >
> > *Figure — the Pb–Sn phase diagram: Pb melts at 327 °C and Sn at 232 °C; the eutectic horizontal at $T_e = 183\ ^\circ\text{C}$ has ends $c_{\alpha e}$ and $c_{\beta e}$ and the eutectic composition $c_e$ between them; the solvus lines bound the single-phase $\alpha$ and $\beta$ fields; the sketches on the right show the microstructure evolution for an alloy of composition $c_0$.*
> >
> > - **When it forms:** solid solubility is **limited** and the melting points of the components are **not vastly different**.
> > - **Phases:** liquid $L$; $\alpha$ (Pb-rich solid solution); $\beta$ (Sn-rich solid solution); two-phase fields $L+\alpha$, $L+\beta$ and $\alpha+\beta$. The boundary between $\alpha$ and $\alpha+\beta$ is the **solvus**; the boundary between liquid and the two-phase region is the **liquidus**, and between solid and the two-phase region the **solidus**.
> > - **Invariant reaction — eutectic**, at $T_e = 183\ ^\circ\text{C}$ and $c_e \approx 61.9$ wt% Sn:
> >
> > $$ \boxed{\ L \;\underset{\text{heating}}{\overset{\text{cooling}}{\rightleftharpoons}}\; \alpha + \beta \qquad (T_e = 183\,^\circ\text{C})\ } $$
> >
> > - Slightly above $T_e$ one or both of $\alpha$ and $\beta$ would disappear; slightly below it the liquid has transformed to a mixture of $\alpha$ and $\beta$. The eutectic horizontal is the tie-line whose ends, at $c_{\alpha e}$ ($\approx 19$ wt% Sn) and $c_{\beta e}$ ($\approx 97.5$ wt% Sn), give the compositions of $\alpha$ and $\beta$. The **lowest-melting** alloy in the system is the eutectic.
> >
> > | | **Ag–Pt** | **Pb–Sn** |
> > | --- | --- | --- |
> > | Type | Peritectic | Eutectic |
> > | Condition | Vastly different melting points | Limited solubility, similar melting points |
> > | Reaction on cooling | $L + \beta \to \alpha$ | $L \to \alpha + \beta$ |
> > | Invariant temperature | 1185 °C | 183 °C |
> > | Phases at the invariant line | $L$, $\alpha$, $\beta$ | $L$, $\alpha$, $\beta$ |
> >
> > *Added depth beyond the slides:* the Pb–Sn values $c_e = 61.9$, $c_{\alpha e} = 19$, $c_{\beta e} = 97.5$ wt% Sn are standard handbook values — the lecture figure marks these points only symbolically; the Ag–Pt compositions are read off the diagram.
> >
> > **(c) The lever rule** [1 mark]
> >
> > In a two-phase region the **lever rule**, derived from a mass balance, gives the **relative amounts of the coexisting phases**. Draw the horizontal **tie-line** at the temperature of interest; its ends meet the phase boundaries at the compositions of the two phases. Treat the tie-line as a lever with its **fulcrum at the overall composition $c_0$**: for the arm to balance, the "weight" at each end — the amount of that phase — must be proportional to the arm length **on the other side** of the fulcrum.
> >
> > For liquid (composition $c_l$) and solid (composition $c_s$) at overall composition $c_0$:
> >
> > $$ \boxed{\ f_l = \frac{c_s - c_0}{c_s - c_l} \qquad\qquad f_s = \frac{c_0 - c_l}{c_s - c_l} \qquad f_l + f_s = 1\ } $$
> >
> > ![[PD - Lever Rule Worked Example.png|440]]
> >
> > *Figure — the lecture's lever-rule example: with $c_0 = 73$, $c_l = 57$ and $c_s = 82$, the liquid fraction is $f_l = (82-73)/(82-57) = 0.36$ and the solid fraction $f_s = 0.64$.*
> >
> > **Limits and uses**
> >
> > - The lever rule **cannot be applied at the eutectic or peritectic temperature itself**, where three phases coexist and an isothermal reaction changes their relative amounts.
> > - It *can* be applied just above or just below the invariant temperature, to estimate (i) the fraction of a **proeutectic phase**, (ii) the fraction of the **eutectic mixture**, and (iii) the fraction of a phase that forms **part of the eutectic mixture**.
> >
> > *Example — Pb–40 wt% Sn, just below 183 °C (using $c_{\alpha e} = 19$, $c_e = 61.9$, $c_{\beta e} = 97.5$):*
> >
> > | Quantity | Expression | Value |
> > | --- | --- | --- |
> > | Total $\alpha$ | $\dfrac{97.5-40}{97.5-19}$ | $0.73$ |
> > | Total $\beta$ | $\dfrac{40-19}{97.5-19}$ | $0.27$ |
> > | Proeutectic $\alpha$ | $\dfrac{61.9-40}{61.9-19}$ | $0.51$ |
> > | Eutectic mixture | $\dfrac{40-19}{61.9-19}$ | $0.49$ |

> [!tip] Exam pointer — Q7
> Draw both diagrams with the invariant horizontal labelled by name, temperature and the three coexisting phases; remember **peritectic: $L+\beta\to\alpha$** against **eutectic: $L\to\alpha+\beta$**. Write the lever rule as "opposite arm over whole tie-line".

---

## Q8. Free electron theory and electrical conduction

> [!question] Q8: Explain the free electron theory and on the basis of the same, explain why solids conduct electricity. [5]
>
> > [!success]- Solution (Click to expand)
> > **The free electron theory**
> >
> > Conduction is **not** a function of the total number of electrons in the solid — only the outermost (valence) electrons take part. In the free electron model they are not bound to any atom but are free to move through the whole solid: the **free electron gas** (**Fermi gas**). The basic assumption is that the potential field of the ion cores is **uniform** throughout the solid, so the potential energy can be set to a constant (zero) and only the kinetic energy $E = \tfrac12 mv^2$ matters. That energy is substantially lower than for a bound electron in an isolated atom, because the larger field of motion allows longer wavelengths.
> >
> > *1. Wave nature and the $E$–$k$ parabola.* The de Broglie wavelength is $\lambda = h/mv$, and the wave number is $k = 2\pi/\lambda$. Combining these with $E = \tfrac12 mv^2$:
> >
> > $$ \boxed{\ E = \frac{h^2k^2}{2m}\ } $$
> >
> > Energy rises as $k^2$ — a parabola.
> >
> > ![[EP1 - Parabolic E-k free electron.png|380]]
> >
> > *Figure — the parabolic $E$–$k$ relation of a free electron: energy rises as the square of the wave number, so long waves (small $k$) sit at the bottom of the curve.*
> >
> > *2. Quantization.* For a solid of length $L$ the wave must vanish at both ends, so $\lambda = 2L, L, \tfrac23 L, \ldots$ and $k = \pm n\pi/L$, giving $E = n^2h^2/8mL^2$. In three dimensions
> >
> > $$ E = \frac{h^2}{8m}\left(\frac{n_x^2}{L_x^2} + \frac{n_y^2}{L_y^2} + \frac{n_z^2}{L_z^2}\right) $$
> >
> > Each combination $(n_x, n_y, n_z)$ is a **quantum state** holding two electrons of opposite spin (Pauli exclusion principle); states with equal energy are **degenerate**. The levels are so close that $E$ is practically continuous, and electrons fill them from the bottom up.
> >
> > *3. Fermi energy and Fermi–Dirac statistics.* At $0\ \text{K}$ all levels up to the **Fermi energy $E_F$** are full and all above are empty. The occupation probability at temperature $T$ is
> >
> > $$ \boxed{\ P(E) = \frac{1}{1 + \exp\!\left(\dfrac{E - E_F}{kT}\right)}\ } $$
> >
> > The **Fermi level** is the level with $P = 50\,\%$, at every temperature. At $T > 0$ some electrons just below $E_F$ are excited to levels just above it.
> >
> > ![[EP1 - Fermi-Dirac distribution at three temperatures.png|440]]
> >
> > *Figure — the Fermi–Dirac distribution at three temperatures: the step at $0\ \text{K}$ broadens with temperature but every curve pivots about $P = 0.5$ at $E = E_F$.*
> >
> > **Why solids conduct electricity**
> >
> > 1. In a neutral solid, for every electron with a given speed in one direction there is another with the same speed in the opposite direction — the velocity distribution is symmetric and the net current is zero.
> > 2. An applied electric field **biases** this distribution: electrons moving towards the positive end gain velocity and those moving the other way lose some. The occupied states shift in $k$-space, giving a net velocity in one direction — a current.
> >
> > ![[EP1 - Electron redistribution under field.png|360]]
> >
> > *Figure — the field-induced shift of the occupied states: the whole Fermi sphere is displaced in $k$-space, so the electron gas acquires a net drift velocity.*
> >
> > 3. This redistribution is possible **only if empty states are available immediately above $E_F$** — the basic characteristic of conductors, as opposed to insulators and semiconductors.
> > 4. The accelerated electrons do not speed up indefinitely: they collide with obstacles, and between collisions acquire an average extra velocity — the **drift velocity** — all of which is lost at each collision.
> >
> > ![[EP1 - Extra velocity lost on collision.png|440]]
> >
> > *Figure — the drift velocity: each electron accelerates between collisions and loses the whole increment at the next one, so the steady state is a sawtooth in velocity.*
> >
> > With $n$ free electrons per unit volume, charge $e$, mass $m$ and mean collision time $\tau = l/v$ ($l$ = mean free path):
> >
> > $$ \boxed{\ \sigma = \frac{ne^2\tau}{m}\ } $$
> >
> > 5. **Resistance** arises from the collisions. In a perfect crystal at $0\ \text{K}$ the mean free path is infinite and $\sigma$ would be infinite; real crystals fall short because **solute atoms** (the most effective scatterers), other point defects, dislocations and grain boundaries all decrease $l$ and hence $\sigma$.
> >
> > **Conclusion.** Metals conduct because their valence electrons are free, and because empty states lie immediately above the Fermi level, so a field can shift the electron distribution; the conductivity is limited only by scattering. *(The model cannot explain insulators and semiconductors — it ignores the periodic lattice, whose Bragg reflection opens the energy gaps of §6.11.)*

> [!tip] Exam pointer — Q8
> The five pieces to show: uniform potential, $E = h^2k^2/2m$, quantization with Pauli + $E_F$, Fermi–Dirac $P(E)$, and the field-bias argument that ends in $\sigma = ne^2\tau/m$ (§6.2–§6.6). The phrase "**empty states immediately above $E_F$**" is the key to *why* conduction occurs.

---

## Q9. Intrinsic and extrinsic semiconductors

> [!question] Q9: Explain (a) intrinsic semiconductor (b) p-type extrinsic semiconductor (c) n-type extrinsic semiconductor. [1 + 2 + 2 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Intrinsic semiconductor** [1 mark]
> >
> > In an **intrinsic** semiconductor, conduction is due to processes characteristic of the pure crystal itself — a pure Si or Ge crystal. Thermal energy excites electrons from the top of the **valence band** across the gap $E_g$ into the **conduction band**, leaving **holes** in the valence band; the electron and hole concentrations are equal. The Fermi level lies in the **middle of the gap**, so $E - E_F = E_g/2$ (for Si, $0.55\ \text{eV}$, more than twenty times $kT = 0.026\ \text{eV}$ at room temperature). Using the Fermi–Dirac distribution with the "1" dropped (Boltzmann approximation):
> >
> > $$ \boxed{\ n_e = n_h = N\exp\!\left(-\frac{E_g}{2kT}\right) \qquad\qquad \sigma = e\left(n_e\mu_e + n_h\mu_h\right)\ } $$
> >
> > where $\mu_e$ and $\mu_h$ are the electron and hole mobilities (Si: $0.14$ and $0.05\ \text{m}^2\text{V}^{-1}\text{s}^{-1}$). The carrier number grows exponentially with $T$, so a plot of $\ln\sigma$ against $1/T$ is a straight line of slope $-E_g/2k$.
> >
> > ![[EP2 - Fermi level midgap in intrinsic semiconductor.png|380]]
> >
> > *Figure — the Fermi level of an intrinsic semiconductor sits midgap, so that the energy measured from $E_F$ to either band edge is exactly $E_g/2$.*
> >
> > **(b) p-type extrinsic semiconductor** [2 marks]
> >
> > In an **extrinsic** semiconductor, conduction is due to deliberately added impurities (**doping**). A p-type semiconductor is made by doping Si with a **third-column element** — Al, Ga or In.
> >
> > - The trivalent atom, substituting for Si, has only three outer electrons, so it needs an **extra electron** to complete the four tetrahedral bonds. The electron comes from a neighbouring Si atom, which leaves a **hole**.
> > - The Al atom becomes negatively charged, and the positive hole revolves around it like a hydrogen-like centre — in the dielectric of the crystal, with a very large orbit and small binding energy.
> > - At $0\ \text{K}$ the holes stay bound; as $T$ rises they break away by thermal excitation. The bound-hole levels are **acceptor levels**, lying just **above the valence band**.
> > - By the law of mass action ($n_en_h = n_i^2$) electrons are suppressed: **holes are the majority carriers** and electrons the minority carriers.
> >
> > ![[EP2 - Silicon doped with aluminium p-type.png|470]]
> >
> > *Figure — silicon doped with aluminium: the trivalent atom completes its four bonds by taking an electron from a neighbour, leaving a mobile hole bound to a shallow acceptor level.*
> >
> > **(c) n-type extrinsic semiconductor** [2 marks]
> >
> > An n-type semiconductor is made by doping Si with a **fifth-column element** — P, As or Sb.
> >
> > - The pentavalent atom substitutes for a Si atom; **four** of its five outer electrons form the tetrahedral bonds with the four Si neighbours, and the **fifth is loosely bound** to the parent ion.
> > - Treating it as a hydrogen-like orbit in the crystal's dielectric, the radius is about $80\ \text{\AA}$ (against $0.5\ \text{\AA}$ for hydrogen) — the electron is almost free, at a level close to the conduction band: the **donor level**, just *below* the conduction band.
> > - The **ionization energy** needed to lift it into the conduction band is far smaller than $E_g$, so at room temperature most donor electrons are excited — far more than by the intrinsic process.
> > - Mass action ($n_en_h = n_i^2$) drastically reduces the holes: **electrons are the majority carriers**; the material is called n-type because the dopant donates negative charge.
> >
> > ![[EP2 - Silicon doped with phosphorus n-type.png|450]]
> >
> > *Figure — silicon doped with phosphorus: four of the five outer electrons enter the tetrahedral bonds, and the fifth occupies a shallow donor level just below the conduction band.*
> >
> > | | **n-type** | **p-type** |
> > | --- | --- | --- |
> > | Dopant | Fifth column — P, As, Sb | Third column — Al, Ga, In |
> > | Mechanism | Donates a loosely bound electron | Accepts an electron, leaving a hole |
> > | Impurity level | Donor, just below conduction band | Acceptor, just above valence band |
> > | Majority carrier | Electrons | Holes |
> > | Minority carrier | Holes | Electrons |

> [!tip] Exam pointer — Q9
> Do not forget the $80\ \text{\AA}$ vs $0.5\ \text{\AA}$ orbit (the dielectric constant of the crystal is why the ionization energy is small), the law of mass action, and where each impurity level sits (§7.7–§7.10).

---

## Q10. Conductivity vs temperature, and the p–n junction

> [!question] Q10: Explain (a) variation of conductivity with temperature for an extrinsic semiconductor (b) forward and reverse bias in junction diode. [3 + 2 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Conductivity vs temperature for an extrinsic semiconductor** [3 marks]
> >
> > The conductivity is $\sigma = e(n_e\mu_e + n_h\mu_h)$. A plot of $\log\sigma$ against $1/T$ for an extrinsic semiconductor divides into **three regions**.
> >
> > ![[EP2 - log conductivity versus reciprocal temperature.png|450]]
> >
> > *Figure — $\log\sigma$ against $1/T$: a steep extrinsic (ionization) branch at low temperature, a flat exhaustion plateau near room temperature, and a steeper intrinsic branch above it.*
> >
> > 1. **Extrinsic (ionization) region — low $T$, large $1/T$.** Carriers are excited from the donor level to the conduction band (or created by excitation to the acceptor level), and their number grows exponentially with $T$, so $\log\sigma$ is linear in $1/T$. The slope gives the **ionization energy of the impurity**.
> > 2. **Exhaustion region — intermediate $T$.** The impurities are nearly all ionized and the unexcited ones are exhausted, so the carrier number is constant and the curve is **flat**. The slope can even turn **positive**, because the mobility falls as $T$ rises — higher $T$ shortens the mean free path.
> > 3. **Intrinsic region — high $T$ (above room temperature).** Electrons are now excited across the gap from the valence band; $\log\sigma$ is again linear in $1/T$ with a **steep negative slope** $-E_g/2k$. The difference between the extrinsic and intrinsic slopes reflects the difference between the ionization energy and $E_g$.
> >
> > $$ \boxed{\ \text{slope}_{\text{extrinsic}} \sim -\frac{E_{\text{ionization}}}{k} \ll \text{slope}_{\text{intrinsic}} = -\frac{E_g}{2k}\ } $$
> >
> > *Design use:* the flat exhaustion region is where a device is stable against temperature changes; a thermistor is instead operated on a steep branch for maximum sensitivity.
> >
> > **(b) Forward and reverse bias in a junction diode** [2 marks]
> >
> > A **p–n junction** has n-type material on one side and p-type on the other (made by diffusing dopant through a window in the oxide layer). At equilibrium the Fermi level is constant across the crystal, which forces the conduction band of the n-side to lie **lower** than that of the p-side by the contact potential $eV_0$ — a potential barrier at the junction.
> >
> > ![[EP2 - p-n junction band diagram at equilibrium.png|450]]
> >
> > *Figure — the p-n junction at equilibrium: a single Fermi level runs across both sides, the bands are offset by $eV_0$, and the junction region contains the resulting barrier.*
> >
> > At equilibrium the current from n to p equals that from p to n, both equal to $I_0$, so the net current is zero. (Electrons from the p-side slide *down* the hill with current $I_0$; the many n-side electrons must climb the barrier, and only a small Boltzmann fraction manages it.)
> >
> > - **Forward bias** — the p-side is made **positive** relative to the n-side. The barrier is **lowered by $eV_i$**, so many more n-side electrons cross; the p → n flow is unchanged (still downhill). The result is a **large net current** in the forward direction.
> >
> > ![[EP2 - Forward bias lowered barrier.png|440]]
> >
> > *Figure — forward bias: the barrier is lowered by $eV_i$, so the majority electrons can cross in large numbers and the current rises steeply.*
> >
> > - **Reverse bias** — the voltage is applied the other way. The barrier is **raised by $eV_i$**, drastically reducing the n → p flow, while the reverse flow stays at $I_0$. The net current is only the **small, constant $I_0$** (the reverse saturation current).
> >
> > ![[EP2 - Reverse bias raised barrier.png|440]]
> >
> > *Figure — reverse bias: the barrier is raised by $eV_i$, the n → p current is choked off, and only the small, barrier-independent $I_0$ survives.*
> >
> > $$ \boxed{\ I = I_0\left[\exp\!\left(\frac{eV_i}{kT}\right) - 1\right]\ } $$
> >
> > This is the **rectifying action** of the diode — large current in one direction, almost none in the other. *(The diode equation is added depth beyond the slides.)*

> [!tip] Exam pointer — Q10
> For (a) draw the three-region plot and say **what each slope measures** (impurity ionization energy; none/mobility; $E_g/2$). For (b) draw the band diagram with the barrier before and after bias (§7.11, §7.13–§7.14).

---

## Q11. Heusler alloys, Zn in NiFe₂O₄, ferrimagnetism

> [!question] Q11: (a) Explain ferromagnetism in Heusler alloys although Mn is not ferromagnetic in elemental form. (b) Explain what happens to the magnetization of NiFe₂O₄ upon addition of Zn. (c) What is ferrimagnetism? [2 + 2 + 1 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Ferromagnetism in Heusler alloys** [2 marks]
> >
> > In Fe, Co and Ni the unpaired $3d$ electrons of neighbouring atoms align their spins in parallel and lower their spin-dependent electrostatic energy. The **net energy gain** is the exchange interaction energy, $E_{\text{exchange}} = E_{\text{unmagnetized}} - E_{\text{magnetized}}$, a sensitive function of the ratio of the atomic diameter to the $3d$ orbital diameter. It is positive — parallel spins are favoured — only when
> >
> > $$ \boxed{\ 1.5 < \frac{d_{\text{atom}}}{d_{3d}} < 2.0 \ \Longrightarrow\ E_{\text{exchange}} > 0\ } $$
> >
> > In elemental **Mn** this ratio is outside the window, so the exchange energy is not positive and Mn is not ferromagnetic. On **alloying** the interatomic distance can be changed: in the **Heusler alloys** $\text{Cu}_2\text{MnSn}$ and $\text{Cu}_2\text{MnAl}$ the Mn atoms are separated by Cu and Sn (or Al), which **increases the Mn–Mn distance by the right amount**, so the ratio falls in the range $1.5$–$2.0$, the exchange energy becomes positive, and the Mn spins on neighbouring atoms align. The alloys are ferromagnetic even though none of the constituents is (Cu is diamagnetic; Mn and Sn are not ferromagnetic in elemental form). Ferromagnetism is thus a property of a *ratio* that can be engineered by alloying.
> >
> > **(b) Effect of Zn on the magnetization of NiFe₂O₄** [2 marks]
> >
> > NiFe₂O₄ is a **ferrite** with the **inverse spinel** structure: the $\text{Ni}^{2+}$ ions and half of the $\text{Fe}^{3+}$ ions occupy octahedral (B) sites, and the other half of the $\text{Fe}^{3+}$ ions occupy tetrahedral (A) sites. The two $\text{Fe}^{3+}$ sets ($5\,\mu_B$ each) are coupled **antiparallel**, so they cancel, and the net moment comes from $\text{Ni}^{2+}$ alone ($\approx 2\,\mu_B$ per formula unit) — the same logic as for $\text{Fe}^{2+}$ in magnetite, where the net moment is from the ferrous ions only.
> >
> > $\text{Zn}^{2+}$ ($3d^{10}$) has **no magnetic moment** and strongly prefers **tetrahedral** sites. On adding Zn it therefore **displaces $\text{Fe}^{3+}$ from tetrahedral sites** to octahedral sites. For $\text{Ni}_{1-x}\text{Zn}_x\text{Fe}_2\text{O}_4$:
> >
> > $$ \text{A (tetrahedral)}:\ \text{Zn}_x\text{Fe}_{1-x} \qquad \text{B (octahedral)}:\ \text{Ni}_{1-x}\text{Fe}_{1+x} $$
> >
> > $$ M = M_B - M_A = \left[2(1-x) + 5(1+x)\right] - 5(1-x) = 2 + 8x \ \ (\mu_B\ \text{per formula unit}) $$
> >
> > Each $\text{Zn}^{2+}$ added removes one antiparallel $\text{Fe}^{3+}$ ($5\,\mu_B$) from the A sublattice and puts one more on the B sublattice, so the **magnetization increases** with $x$. *(Added depth beyond the slides, which give only the ferrite formula and magnetite example:)* the linear rise holds only for small $x$; at high Zn content the A–B coupling that holds the lattice ordered is so weakened that the net magnetization and Curie temperature fall again, and for $\text{ZnFe}_2\text{O}_4$ the compound is not ferrimagnetic.
> >
> > **(c) Ferrimagnetism** [1 mark]
> >
> > **Ferrimagnetism** occurs in compounds whose constituent atoms are **antiferromagnetically coupled but have different magnetic moments**. The unequal antiparallel moments do not cancel, so each coupling leaves a **net moment**, and the sum over all the couplings can give a magnetization comparable in order of magnitude to ferromagnetism. Ferrites $\text{Me}^{2+}\text{Fe}_2^{3+}\text{O}_4^{2-}$ are the standard examples; in magnetite $\text{Fe}_3\text{O}_4$ the ferric ions ($5\,\mu_B$) cancel and the net $4\,\mu_B$ per formula unit comes from the ferrous ion.
> >
> > ![[MAG - Ferro antiferro ferrimagnetic coupling.png|460]]
> >
> > *Figure — (a) ferromagnetic, (b) antiferromagnetic and (c) ferrimagnetic coupling of electron spins in atoms, denoted by arrows; the length of an arrow is a measure of the magnetic moment of the atom. In (b) the antiparallel moments are equal and cancel exactly; in (c) they are unequal, so each pair leaves a net moment and the solid is magnetized.*
> >
> > | Coupling | Neighbouring moments | Net moment |
> > | --- | --- | --- |
> > | **Ferromagnetic** | Parallel | Full sum |
> > | **Antiferromagnetic** | Antiparallel, equal | Zero |
> > | **Ferrimagnetic** | Antiparallel, unequal | Difference of sublattice moments |

> [!warning] Part (b) goes beyond the slides
> The slides give the ferrite formula, the inverse-spinel site distribution and the magnetite moment count, but not the Zn substitution itself. The cation-site argument above is the standard textbook explanation — check it against your class notes ([[MO NOTES (1).pdf]]) before relying on the numbers.

> [!tip] Exam pointer — Q11
> Quote the $1.5 < d_{\text{atom}}/d_{3d} < 2.0$ window for (a); for (b) the sites-and-sublattices argument ("non-magnetic Zn takes the A sites, pushing Fe³⁺ to B, so the antiparallel cancellation is reduced"); for (c) "antiparallel + unequal = net moment" (§8.9, §8.11–§8.13).

---

## Q12. Polarization mechanisms and ferroelectricity

> [!question] Q12: (a) Define the various polarization mechanisms. (b) Explain why BaTiO₃ shows ferroelectricity. [3 + 2 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Polarization mechanisms** [3 marks]
> >
> > When a dielectric is placed between capacitor plates it **binds charge** at its surfaces and the capacitance rises from $C = \varepsilon_0A/d$ to $C = \varepsilon_r\varepsilon_0A/d$. The **polarization** $P$ is the dipole moment per unit volume ($\text{C m}^{-2}$). The total polarization is the sum of four contributions:
> >
> > $$ \boxed{\ P = P_e + P_i + P_o + P_s\ } $$
> >
> > ![[DIE - Four polarization mechanisms.png|430]]
> >
> > *Figure — the four polarization processes in one figure: (a) electronic, (b) ionic, (c) orientation and (d) space charge; each panel shows the charge configuration before and after the field is applied.*
> >
> > 1. **Electronic polarization ($P_e$)** — displacement of the positively charged **nucleus and the negative electron cloud of an atom in opposite directions** under a field. The fastest mechanism, and **independent of temperature**.
> > 2. **Ionic polarization ($P_i$)** — in an ionic solid, **cations and anions are displaced in opposite directions**, each relative to its oppositely charged neighbours (not relative to its own nucleus, which is what distinguishes it from electronic polarization). **Independent of $T$**, but **slower** than electronic polarization because whole ions are heavier than an electron cloud.
> > 3. **Orientation polarization ($P_o$)** — molecules with a **permanent dipole moment** (e.g. CH₃Cl, where Cl pulls the bonding electrons more strongly than H; CH₄ has none) **align** with the applied field, like permanent magnetic moments in paramagnetism. It is **temperature dependent**, since thermal energy randomizes the alignment, and slower than ionic.
> > 4. **Space charge polarization ($P_s$)** — **accumulation of charge at electrodes or at interfaces** in a multiphase material, as ions diffuse over appreciable distances in the field and redistribute. It is the **slowest** mechanism, since ions diffuse over several interatomic distances.
> >
> > | Mechanism | What moves | $T$ dependence | Speed |
> > | --- | --- | --- | --- |
> > | **Electronic** | Electron cloud vs its own nucleus | Independent | Fastest |
> > | **Ionic** | Cations vs anions | Independent | Slower than electronic |
> > | **Orientation** | Permanent molecular dipoles align | Dependent | Slower than ionic |
> > | **Space charge** | Ions diffuse to interfaces | Dependent | Slowest |
> >
> > Because each mechanism can follow only a field that alternates slowly enough, the slowest ones drop out first as frequency rises — so $\varepsilon_r$ is a function of frequency.
> >
> > **(b) Ferroelectricity in BaTiO₃** [2 marks]
> >
> > A **ferroelectric** has its electric dipoles **aligned in the same direction even with no applied field** (spontaneous polarization), and its dielectric constant is about two orders of magnitude larger than that of ordinary dielectrics — over **2000** for BaTiO₃, against under 10 for ordinary dielectrics. It is the electric analogue of ferromagnetism.
> >
> > - **Above $120\ ^\circ\text{C}$** BaTiO₃ is **cubic**: the centres of positive and negative charge coincide, so there is no spontaneous dipole.
> > - **Cooling below the ferroelectric Curie temperature of $120\ ^\circ\text{C}$**, the **Ti⁴⁺ ion shifts to one side of the body centre**, with a displacement of the neighbouring oxygen anions. The cell becomes **tetragonal**, with
> >
> > $$ \frac{c}{a} = \frac{4.03\ \text{\AA}}{3.98\ \text{\AA}} = 1.012 $$
> >
> > - The positive and negative charge centres no longer coincide, so each cell carries a **dipole**. The dipoles of neighbouring cells **line up**, giving a large polarization in the solid even without a field — hence ferroelectricity and the very large $\varepsilon_r$.
> > - Ferroelectric crystals always show the **piezoelectric** effect (a charge in response to stress, a shape change in response to a field); BaTiO₃ is used in microphones, strain gauges and sonar, and its high dielectric constant makes it useful for small capacitors.
> >
> > ![[DIE - BaTiO3 cubic and tetragonal cells.png|400]]
> >
> > *Figure — the BaTiO₃ unit cell above and below the Curie temperature: the dashed circle in the front view marks the Ti ion, which shifts off the body centre on cooling, dragging the neighbouring oxygens with it.*

> [!tip] Exam pointer — Q12
> For (a) give *what moves*, *$T$ dependence* and *relative speed* for all four; for (b) say **cubic above 120 °C → Ti shifts off-centre → tetragonal, $c/a = 1.012$ → dipoles align spontaneously** (§9.3–§9.9).

---

## Formula Summary — Endsem-1

| Quantity | Expression | Notes |
| --- | --- | --- |
| Shockley dissociation (FCC) | $\tfrac{a}{2}[1\bar{1}0] \to \tfrac{a}{6}[2\bar{1}\bar{1}] + \tfrac{a}{6}[1\bar{2}1]$, $a^2/2 \to a^2/3$ | Both partials in the fault plane $(111)$; vector sum must close |
| Frank partial | $\mathbf{b}_F = \tfrac{a}{3}\langle111\rangle$, $\lvert\mathbf{b}_F\rvert = a/\sqrt3 = d_{111}$ | Normal to the fault plane; sessile |
| Shockley dissociation (HCP) | $\tfrac{a}{3}[11\bar{2}0] \to \tfrac{a}{3}[10\bar{1}0] + \tfrac{a}{3}[01\bar{1}0]$ | Basal plane; $a^2 \to 2a^2/3$ |
| Frank's rule | $b_3^2 < b_1^2 + b_2^2$ with $\mathbf{b}_3 = \mathbf{b}_1 + \mathbf{b}_2$ | Both conditions required |
| Lomer lock | $\tfrac{a}{2}[10\bar{1}] + \tfrac{a}{2}[011] \to \tfrac{a}{2}[110]$ | $a^2 \to a^2/2$; product not in a slip plane |
| DBTT | $\sigma_y(T) = \sigma_f$ | Brittle below, ductile above |
| Brinell | $HB = \dfrac{2P}{\pi D\left[D - \sqrt{D^2-d^2}\right]}$ | $P$ in kg, $D$, $d$ in mm |
| Rockwell | $HR = 100 - h/0.002$ (cone), $130 - h/0.002$ (ball) | $h$ in mm |
| Vickers | $HV = 1.854\,P/d^2$ | $d$ = mean diagonal |
| Flexural strength | $\sigma_{fs} = 3F_fL/2bd^2$, $F_fL/\pi r^3$ | Elastic beam, small deflection |
| Critical fibre length | $l_c = \sigma_f^* d/2\tau_c$ | $\tau_c$ = smaller of bond strength and matrix shear yield strength |
| Gibbs phase rule | $F = C - P + 2$ ($F = C - P + 1$ at constant $P$) | Invariant reaction: $F = 0$ |
| Lever rule | $f_l = \dfrac{c_s - c_0}{c_s - c_l}$, $f_s = \dfrac{c_0 - c_l}{c_s - c_l}$ | Not at the invariant temperature itself |
| Free electron energy | $E = h^2k^2/2m$; $E = \dfrac{h^2}{8m}\left(\tfrac{n_x^2}{L_x^2}+\tfrac{n_y^2}{L_y^2}+\tfrac{n_z^2}{L_z^2}\right)$ | Uniform potential; Pauli exclusion |
| Fermi–Dirac | $P(E) = \left[1+\exp\!\left(\tfrac{E-E_F}{kT}\right)\right]^{-1}$ | $P(E_F) = 0.5$ at all $T$ |
| Metallic conductivity | $\sigma = ne^2\tau/m$ | $\tau = l/v$ |
| Intrinsic carriers | $n_e = n_h = N\exp(-E_g/2kT)$ | Needs $E_g/2 \gg kT$ |
| Semiconductor conductivity | $\sigma = e(n_e\mu_e + n_h\mu_h)$ | Holds for intrinsic and extrinsic |
| Mass action | $n_en_h = n_i^2$ | Fixes majority/minority carriers |
| Diode current | $I = I_0\left[\exp(eV_i/kT) - 1\right]$ | Added depth beyond the slides |
| Exchange criterion | $1.5 < d_{\text{atom}}/d_{3d} < 2.0$ | $E_{\text{exchange}} > 0$ only in this window |
| Ferrite moment (Zn-substituted NiFe₂O₄) | $M = 2 + 8x\ \mu_B$ | Added depth; valid for small $x$ |
| Total polarization | $P = P_e + P_i + P_o + P_s$ | Four mechanisms, different speeds |
| Capacitance with dielectric | $C = \varepsilon_r\varepsilon_0A/d$ | $\varepsilon_0 = 8.85\times10^{-12}\ \text{F m}^{-1}$ |
| BaTiO₃ tetragonality | $c/a = 4.03/3.98 = 1.012$ | Below the 120 °C Curie temperature |

> [!note] Source images
> The Excalidraw figures in this note (`SD - `, `MP - `) are the original reconstructions already stored in the vault `Excalidraw/` folder. The extracted figures come from the lecture PDFs and are stored in `Material Science/images/` with their topic prefix (`MP2`, `MP3`, `SD`, `COMP`, `EP1`, `EP2`, `MAG`, `DIE`); the four phase-diagram figures (Pb–Sn, Ag–Pt, Fe–C and the lever-rule example) were extracted from [[Phase_Diagrams.pdf]] and are stored with the new `PD - ` prefix.


---

# Endsem 2 Solutions

Worked solutions to the End-Sem paper [[emdsem2.pdf]] (Even Sem 2025–26, MO-201 Materials Science and Engineering, 3 hours, 60 marks, 32 short questions). The answers follow the same method as the Endsem-1 section above: each question is a card with a collapsible solution, built from [[notes]] (cited by section) and the lecture PDFs, with *added depth* marked wherever an answer goes beyond the slides. The questions are grouped by topic in paper order.

> [!info] Map of the paper
> Questions **1–9** are mechanical behaviour, **10–18** are free electrons, conduction, semiconductors and optical response, **19–22** are dielectrics, **23–30** are magnetic materials, and **31–32** return to semiconductors. Several of the numerical questions (3, 11, 16, 18, 22, 25, 26) are worked in full with units; the key results are collected in the Formula Summary at the end of this section.

| Q | Topic | Marks | Where it lives in [[notes]] |
| --- | --- | --- | --- |
| **1** | Strain–time response: elastomer, viscoelastic, viscous | 2 | §2.9 |
| **2** | Engineering stress–strain curve with labels | 2 | §2.8, §2.11 |
| **3** | Elastic strain of Al at 30,000 psi | 2 | §1.4 / Hooke's law |
| **4** | Failures: Titanic, Liberty, Challenger, Columbia | 2 | §1.1, §2.7 |
| **5** | Poisson's ratio: elastic vs plastic | 2 | §2.10 |
| **6** | Slip and slip system | 2 | §2.2–§2.3 |
| **7** | Shear stress parallel to tensile stress and yielding | 2 | §2.4 |
| **8** | Slip vs twinning | 2 | §2.2 |
| **9** | Grain-boundary strengthening | 4 | §2.5 |
| **10** | Fermi–Dirac occupancy limits | 2 | §6.5 |
| **11** | Fermi velocity of potassium | 2 | §6.3–§6.4 |
| **12** | Nichrome vs copper heating element | 1 | §6.6 |
| **13** | Aluminium transmission lines and solid solution | 1 | §6.6 |
| **14** | Pb and Zn as conductors | 2 | §7.1, §7.4–§7.5 |
| **15** | Conductivity vs impurity: semiconductor vs metal | 2 | §6.6, §7.9–§7.10 |
| **16** | Energy gap of Ge from resistance data | 2 | §7.8 |
| **17** | CdTe photoconductor and a cigarette | 1 | §9.12 |
| **18** | Wavelength of a GaAs laser | 2 | §9.12 |
| **19** | Polyethylene vs PVC dielectric constant | 2 | §9.5 |
| **20** | Ice/water vs HCl dielectric constant on melting | 1 | §9.5 |
| **21** | Loss factor: Na⁺ replaced by Rb⁺ in glass | 2 | §9.6–§9.7 |
| **22** | Polarization of BaTiO₃ | 2 | §9.9 |
| **23** | Large moment vs high Curie temperature | 1 | §8.9–§8.10 |
| **24** | Fe–Ni permeability and hysteresis area | 2 | §8.15–§8.17 |
| **25** | Eddy-current and hysteresis loss at 50 Hz | 2 | §8.16 |
| **26** | Eddy loss in Fe–4%Si | 2 | §8.17 |
| **27** | Fe, Co, Ni ferromagnetic: exchange energy | 2 | §8.9 |
| **28** | Heusler alloys | 1 | §8.11 |
| **29** | Zn in nickel ferrite | 2 | §8.12–§8.13 |
| **30** | Fe–4%Si vs ferrites: energy loss | 2 | §8.17 |
| **31** | Conductivity vs temperature, extrinsic semiconductor | 2 | §7.11 |
| **32** | GaAs vs Si in optoelectronic communication | 1 | §9.12 |

---

## E2-A. Mechanical behaviour (Q1–Q9)

> [!question] Q1: Draw strain–time response for the given stress cycle for elastomer, viscoelastic material, and viscous materials. [2]
>
> > [!success]- Solution (Click to expand)
> > The stress cycle in the paper is a **rectangular pulse**: stress is switched **on** at $t_1$, held constant, and switched **off** at $t_2$. The strain–time response of a material to this pulse depends on how much of its deformation is instantaneous, retarded or permanent (§2.9).
> >
> > ![[MP2 - Anelasticity elastic viscous viscoelastic.png|420]]
> >
> > *Figure — the standard four-panel comparison: load–time cycle (top) against strain–time response (bottom) for (a) elastic, (b) anelastic/viscoelastic, (c) viscous and (d) elastomeric behaviour.*
> >
> > | Material | On loading ($t_1$ to $t_2$) | On unloading (after $t_2$) | Net result |
> > | --- | --- | --- | --- |
> > | **Elastomer** | Large strain builds up, with a rapid initial rise followed by a slower approach to a plateau | Strain falls, quickly at first and then slowly | Fully **recovered** — no permanent set |
> > | **Viscoelastic** | Instantaneous elastic jump, then a **time-dependent (retarded) rise**, with some steady flow under constant load | Instantaneous elastic recovery, then **gradual** recovery of the retarded strain | A residual (permanent) strain may remain |
> > | **Viscous** | No instantaneous jump; strain grows **linearly with time** at constant stress | Strain stays **constant** at the value reached | **All** strain is permanent |
> >
> > The ordering of the elastic content is therefore: elastic (all instantaneous, all recovered) $\to$ elastomer/viscoelastic (partly delayed) $\to$ viscous (none recovered). *Check the labels (b) and (d) against your slide, which names the retarded-recovery curve; the shapes above are the ones in the four-panel figure.*

> [!question] Q2: Draw the engineering stress and engineering strain curve for metals, and label the elastic limit, offset yield strength, tensile strength, breaking strength, and strain to failure. [2]
>
> > [!success]- Solution (Click to expand)
> > ![[MP - Engineering Stress Strain Curve.excalidraw]]
> >
> > | Label | Where it is on the curve |
> > | --- | --- |
> > | **Elastic limit** | End of the linear/elastic region (the largest stress after which the specimen still returns to zero strain on unloading); in practice close to the proportional limit |
> > | **Offset yield strength** $\sigma_y$ | Intersection of the curve with a line **parallel to the elastic slope, starting at $\varepsilon = 0.002$** (the 0.2 % offset) |
> > | **Tensile strength** $\sigma_{UTS}$ | The **maximum** of the curve; onset of necking |
> > | **Breaking strength** | The stress at the end of the curve (fracture) — **lower** than $\sigma_{UTS}$ on the engineering curve, because necking reduces the load while $A_0$ is still used |
> > | **Strain to failure** $\varepsilon_f$ | Strain at the fracture point; the elongation measured after fracture is smaller by the recovered elastic part |
> >
> > ![[MP2 - 0.2 percent offset yield strength.png|440]]
> >
> > *Figure — the 0.2 % offset construction (left) and the upper/lower yield points of a low-carbon steel with the 0.2 % offset yield strength marked on the same curve (right).*
> >
> > $$ \boxed{\ \sigma_y:\ \text{curve} \cap \text{line of slope } E \text{ through } \varepsilon = 0.002 \qquad \sigma_{UTS} = \sigma_{\max}\ } $$

> [!question] Q3: Steel and aluminium have Young's moduli of 210 GPa and 70 GPa, respectively. Tensile samples of steel and aluminium are made with identical geometry. In both samples, the yield stress occurs above 40,000 psi. At an engineering stress of 30,000 psi, the steel sample shows an elastic strain of 0.001. Find the elastic strain of the aluminium sample at an engineering stress of 30,000 psi. [2]
>
> > [!success]- Solution (Click to expand)
> > Both samples yield above 40,000 psi, so at 30,000 psi both are still in the **elastic** region and Hooke's law $\sigma = E\varepsilon$ applies. The same stress acts on both (identical geometry, same load), so
> >
> > $$ \sigma = E_{\text{steel}}\,\varepsilon_{\text{steel}} = E_{\text{Al}}\,\varepsilon_{\text{Al}} \quad\Longrightarrow\quad \varepsilon_{\text{Al}} = \varepsilon_{\text{steel}}\,\frac{E_{\text{steel}}}{E_{\text{Al}}} $$
> >
> > $$ \varepsilon_{\text{Al}} = 0.001 \times \frac{210\ \text{GPa}}{70\ \text{GPa}} = 0.003 $$
> >
> > **Check in psi.** $1\ \text{GPa} = 1.450\times10^{5}\ \text{psi}$, so $E_{\text{steel}} = 30.5\times10^{6}\ \text{psi}$ and $E_{\text{Al}} = 10.15\times10^{6}\ \text{psi}$. Then $\sigma_{\text{steel}} = 30.5\times10^{6}\times0.001 = 30{,}500\ \text{psi}\approx 30{,}000\ \text{psi}$ ✓, and
> >
> > $$ \varepsilon_{\text{Al}} = \frac{30{,}000}{10.15\times10^{6}} = 2.96\times10^{-3} \approx 0.003 $$
> >
> > $$ \boxed{\ \varepsilon_{\text{Al}} \approx 0.003\ } $$
> >
> > The aluminium strains three times as much as steel under the same stress because its modulus is one-third as large.

> [!question] Q4: Materials response to external force changes depending on temperature, loading, and strain rate. Name the material behavior phenomenon that led to the failure of a) Titanic in 1912, b) World War II Liberty ship, c) Space Shuttle Challenger in 1986, and d) Space Shuttle Columbia in 2003. [2]
>
> > [!success]- Solution (Click to expand)
> > | Failure | Phenomenon | Explanation |
> > | --- | --- | --- |
> > | **a) Titanic, 1912** | **Ductile-to-brittle transition** (brittle fracture) | Hull steel with a high DBTT, in ice-cold water, under impact loading — service temperature fell *below* the DBTT, so the plate fractured before it yielded (§2.7) |
> > | **b) Liberty ships, 1942–45** | **Ductile-to-brittle transition** (brittle fracture at notches) | All-welded hulls of steel with inadequate notch toughness; low temperature, stress concentration at hatch corners and no crack-arresting seams (§1.1, §2.7) |
> > | **c) Challenger, 1986** | **Loss of elasticity of the elastomer O-ring at low temperature** (rubber → glassy, below its glass transition) | A cold launch stiffened the rubber seals, which could no longer recover and seal the joint |
> > | **d) Columbia, 2003** | **Brittle fracture under high-strain-rate impact** | Impact of a foam fragment on the brittle reinforced carbon–carbon leading edge cracked it, letting hot gas in |
> >
> > The common thread is that the same material behaves very differently when temperature falls or loading rate rises — the Yoffee-diagram argument of Endsem-1 Q2(a). *Added depth beyond the slides:* parts (c) and (d) are not worked in [[notes]], which treats the Titanic and Liberty cases (§1.1, §2.7); the Challenger and Columbia explanations are the standard accounts.

> [!question] Q5: What is Poisson's ratio, and comment on its value for metals in the elastic region and the plastic region. [2]
>
> > [!success]- Solution (Click to expand)
> > Under a tensile stress along $z$ the specimen elongates ($\varepsilon_z > 0$) and **contracts laterally** ($\varepsilon_x = \varepsilon_y < 0$). **Poisson's ratio** is the negative ratio of lateral to axial strain:
> >
> > $$ \boxed{\ \nu = -\frac{\varepsilon_x}{\varepsilon_z} = -\frac{\varepsilon_y}{\varepsilon_z}\ } $$
> >
> > - **Elastic region** — for metals and alloys $\nu \approx 0.25$–$0.35$ (steels 0.27–0.30, aluminium about 0.33, copper 0.33–0.35). The volume *increases* slightly: $\Delta V/V = \varepsilon_z(1-2\nu)$, so for $\nu = 0.3$ a strain of 0.3 % gives a volume increase of only 0.12 %.
> > - **Plastic region** — plastic deformation proceeds by **slip (shear)**, which does not change volume, so volume is conserved. Setting $\Delta V = 0$ gives $1 - 2\nu = 0$, i.e.
> >
> > $$ \nu_{\text{plastic}} = 0.5 $$
> >
> > So $\nu$ **rises from about 0.3 in the elastic range towards 0.5 in the plastic range**, the value of a perfectly incompressible material (the same value as rubber). This is the constant-volume assumption, $A_0l_0 = A_il_i$, behind the true-stress and true-strain conversions.

> [!question] Q6: What is slip and slip system? [2]
>
> > [!success]- Solution (Click to expand)
> > **Slip** is plastic deformation by the shear of one part of a crystal over another along a crystallographic plane, in a crystallographic direction, by a discrete, whole number of lattice spacings. It proceeds by the nucleation, glide and escape of **dislocations**, not by rigid sliding of two half-crystals, so the lattice orientation on both sides of the slip plane is **unchanged** and a **slip step** of height $nb$ appears at the surface.
> >
> > A **slip system** is one **slip plane** together with one **slip direction** in it (and the Burgers vector of the dislocation that glides). The plane is the **close-packed plane** (highest atomic density, widest spacing, lowest shear resistance) and the direction is the **close-packed direction** in that plane (shortest Burgers vector, lowest dislocation energy).
> >
> > | Crystal | Slip plane | Slip direction | Number of systems |
> > | --- | --- | --- | --- |
> > | **FCC** | $\{111\}$ | $\langle110\rangle$ | $4\times3 = 12$ |
> > | **BCC** | $\{110\}$ (also $\{112\}$, $\{123\}$) | $\langle111\rangle$ | $6\times2 = 12$ |
> > | **HCP** | Basal $(0001)$ | $\langle11\bar{2}0\rangle$ | $1\times3 = 3$ |
> >
> > The number of independent slip systems controls ductility: at least **five** are needed for an arbitrary shape change (von Mises), which is why FCC metals are ductile and HCP metals are not.

> [!question] Q7: Can shear stress parallel to tensile stress result in the yielding of a single crystal? Give justification. [2]
>
> > [!success]- Solution (Click to expand)
> > Yes — but only through the component of the stress that is **resolved onto the slip system**. A tensile stress $\sigma$ along an arbitrary axis is not itself a shear stress on the slip plane; slip is driven by the **resolved shear stress** in the slip direction on the slip plane. With $\phi_1$ the angle between the stress axis and the slip-plane normal and $\phi_2$ the angle between the stress axis and the slip direction:
> >
> > $$ \tau_R = \sigma\cos\phi_1\cos\phi_2 = \sigma\,m, \qquad m_{\max} = 0.5\ \ (\phi_1 = \phi_2 = 45^\circ) $$
> >
> > Slip starts when $\tau_R$ reaches the **critical resolved shear stress** $\tau_{CRSS}$, a material property:
> >
> > $$ \boxed{\ \tau_R = \tau_{CRSS} \quad\Longrightarrow\quad \sigma_y = \frac{\tau_{CRSS}}{m}\ } $$
> >
> > - A stress acting **along the tensile axis** produces a non-zero resolved shear stress on every plane that is inclined to the axis, so a single crystal **can yield**, at the stress $\tau_{CRSS}/m$ — lowest when $m = 0.5$.
> > - It **cannot yield on a given system** if $m = 0$: when the stress axis lies *in* the slip plane ($\phi_1 = 90^\circ$), or when the slip direction is perpendicular to the axis ($\phi_2 = 90^\circ$, which includes the case of a slip plane perpendicular to the axis, since the direction then lies in the plane). Then $\tau_R = 0$ however large $\sigma$ is.
> >
> > So the answer is conditional: shear stress on the slip system must be **resolved** and must reach $\tau_{CRSS}$; orientation alone decides whether this occurs (§2.4). *The question's wording is ambiguous; this answer treats it as "does a tensile stress, through its shear component, cause yielding".*

> [!question] Q8: Name two modes through which plastic deformation can take place in metallic samples. Give at least two key differences between the two modes. [2]
>
> > [!success]- Solution (Click to expand)
> > The two modes are **slip** and **twinning**.
> >
> > | | **Slip** | **Twinning** |
> > | --- | --- | --- |
> > | Displacement | Block above the plane shifts by a **whole number of lattice spacings** | Each successive plane shifts by a **fraction** of a spacing, growing with distance from the twin plane |
> > | Lattice orientation | **Unchanged** | **Changed** — the twinned region is a mirror image of the parent |
> > | Surface evidence | A visible **step** (slip line) | A reoriented, tilted region |
> > | Strain produced | Large (repeats indefinitely) | Small and bounded (a few per cent) |
> > | When it dominates | Normal case (FCC, BCC) | When slip is hard: HCP metals, low $T$, high strain rate, low-SFE FCC (brass, TWIP steel) |
> > | Stress needed | Low (reaches CRSS first) | High (often 2–3 times CRSS) |
> >
> > ![[MP2 - Slip and twinning sequence.png|420]]
> >
> > *Figure — (a) before deformation; (b) after slip, the upper block is displaced by a whole number of lattice spacings and the surface shows a step; (c) after twinning, each plane is displaced by a fraction of a spacing, producing a mirror-image (twinned) region.*

> [!question] Q9: Explain the grain boundary strengthening mechanism and the associated relation with neat schematics. [4]
>
> > [!success]- Solution (Click to expand)
> > **Mechanism.** Neighbouring grains have different crystallographic orientations, so a slip plane in one grain does not continue into the next. A moving dislocation therefore **cannot cross the grain boundary**; it **piles up** against it. The more grain boundaries per unit volume (the finer the grain), the more frequently dislocations are stopped, so more stress is needed to keep the metal deforming.
> >
> > ![[MP - Grain Boundary Pile-up.excalidraw]]
> >
> > **Quantitative relation.** A pile-up of $n$ dislocations multiplies the applied stress at its head by about $n$:
> >
> > $$ \tau_{\text{head}} \approx n\,\tau_{\text{applied}}, \qquad n \approx \frac{\pi\,\tau_{\text{applied}}\,L}{Gb} $$
> >
> > where $L$ is the pile-up length ($\approx$ the grain radius, $L = d/2$), $G$ the shear modulus and $b$ the Burgers vector. Yielding of the *next* grain begins when $\tau_{\text{head}}$ reaches that grain's critical value $\tau^{*}$. Setting $\tau_{\text{head}} = \tau^{*}$:
> >
> > $$ \tau_{\text{applied}} \approx \sqrt{\frac{2Gb\,\tau^{*}}{\pi d}} $$
> >
> > so the yield stress varies as the inverse square root of the grain diameter — the **Hall–Petch relation**:
> >
> > $$ \boxed{\ \sigma_y = \sigma_0 + k_y\,d^{-1/2}\ } $$
> >
> > where $\sigma_0$ is the friction stress opposing dislocation motion in the single crystal and $k_y$ is a constant measuring the resistance of the boundary. A **plot of $\sigma_y$ against $d^{-1/2}$ is a straight line** of slope $k_y$ and intercept $\sigma_0$.
> >
> > **Consequences.**
> >
> > - **Finer grains → higher yield strength.** Grain refinement is the only common strengthening mechanism that also *improves* toughness: it lowers the DBTT because it shortens the pile-ups that nucleate cleavage cracks (§2.7).
> > - The same pile-up stress concentration, applied to a crack instead of a boundary, is how a slip band nucleates a cleavage crack.
> >
> > | Grain size | Pile-up length | Stress at head | Yield strength |
> > | --- | --- | --- | --- |
> > | Coarse (large $d$) | Long | Large — next grain yields easily | Low |
> > | Fine (small $d$) | Short | Small — higher applied stress needed | High |

> [!tip] Exam pointer — Endsem 2, mechanical (Q1–Q9)
> Have ready: the four strain–time shapes (elastic, viscoelastic, viscous, elastomer); the labelled stress–strain curve with the 0.2 % offset line; $\varepsilon = \sigma/E$ in the elastic range; the four failures and their phenomena (DBTT for Titanic/Liberty); $\nu \approx 0.3$ (elastic) $\to 0.5$ (plastic); slip system = close-packed plane + direction; $\tau_R = \sigma\cos\phi_1\cos\phi_2$; the slip/twinning table; and Hall–Petch with the pile-up argument (§2.2–§2.5, §2.9–§2.10).

---

## E2-B. Free electrons, conduction, semiconductors and optical response (Q10–Q18)

> [!question] Q10: Show that the probability of occupancy of energy level $E$ by an electron is (i) negligible for $E \gg E_F$, (ii) 0.5 for $E = E_F$, (iii) $\sim 1$ for $E \ll E_F$. [2]
>
> > [!success]- Solution (Click to expand)
> > The probability of occupation of an energy level $E$ is given by the Fermi–Dirac distribution
> >
> > $$ P(E) = \frac{1}{1 + \exp\!\left(\dfrac{E - E_F}{kT}\right)} $$
> >
> > where $k$ is Boltzmann's constant and $T$ the absolute temperature. Define $x = (E - E_F)/kT$, so $P = 1/(1 + e^{x})$.
> >
> > - **(i) $E \gg E_F$.** Then $x \gg 1$, $e^{x} \gg 1$, and the "1" in the denominator can be dropped:
> >
> > $$ P(E) \approx \exp\!\left(-\frac{E - E_F}{kT}\right) \longrightarrow 0 $$
> >
> > The level is **almost always empty** (negligible occupancy).
> >
> > - **(ii) $E = E_F$.** Then $x = 0$, $e^{0} = 1$:
> >
> > $$ P(E_F) = \frac{1}{1 + 1} = 0.5 $$
> >
> > This holds at **every** temperature — this is the definition of the Fermi level.
> >
> > - **(iii) $E \ll E_F$.** Then $x \ll -1$, $e^{x} \to 0$:
> >
> > $$ P(E) = \frac{1}{1 + e^{x}} \longrightarrow 1 $$
> >
> > The level is **almost certainly filled**.
> >
> > $$ \boxed{\ P \to 0\ (E \gg E_F) \qquad P = 0.5\ (E = E_F) \qquad P \to 1\ (E \ll E_F)\ } $$
> >
> > At $0\ \text{K}$ the limits become exact: $P = 1$ below $E_F$ and $P = 0$ above it.

> [!question] Q11: The Fermi level for potassium is 2.1 eV. Calculate the velocity of the electrons at the Fermi level. [2]
>
> > [!success]- Solution (Click to expand)
> > The energy of free electrons is purely kinetic, $E = \tfrac12 mv^2$, so at the Fermi level
> >
> > $$ E_F = \tfrac12 m v_F^2 \quad\Longrightarrow\quad v_F = \sqrt{\frac{2E_F}{m}} $$
> >
> > Convert the energy: $E_F = 2.1\ \text{eV} \times 1.602\times10^{-19}\ \text{J/eV} = 3.364\times10^{-19}\ \text{J}$, and $m = 9.109\times10^{-31}\ \text{kg}$:
> >
> > $$ v_F = \sqrt{\frac{2\,(3.364\times10^{-19})}{9.109\times10^{-31}}} = \sqrt{7.39\times10^{11}}\ \text{m/s} $$
> >
> > $$ \boxed{\ v_F \approx 8.6\times10^{5}\ \text{m/s}\ } $$
> >
> > This is about $0.3\,\%$ of the speed of light, which justifies the classical (non-relativistic) kinetic energy used in the free electron model. Note that $v_F$ is large even at $0\ \text{K}$: the Pauli exclusion principle forces electrons into high-energy states.

> [!question] Q12: Explain why nichrome and not copper is used as a heating element. [1]
>
> > [!success]- Solution (Click to expand)
> > A heating element converts electrical energy into heat by Joule heating, $P = V^2/R$, so it needs a **high resistivity** (a high resistance in a compact wire) and must survive **high temperature in air**.
> >
> > - **Resistivity.** In $\sigma = ne^2\tau/m$, solute atoms are the most effective electron scatterers: they shorten the mean free path and lower $\sigma$. **Nichrome** (Ni–Cr alloy) is a concentrated solid solution, so its resistivity ($\sim10^{-6}\ \Omega\,\text{m}$) is about 60 times that of pure copper ($\sim1.7\times10^{-8}\ \Omega\,\text{m}$).
> > - **Copper** conducts so well that a very long, thin wire would be needed for the same resistance, and it would oxidise and weaken at red heat. *Added depth beyond the slides:* nichrome forms a protective, adherent $\text{Cr}_2\text{O}_3$ film and keeps its strength at high temperature, so it does not burn out.

> [!question] Q13: Explain why aluminium used in long distance transmission lines cannot be strengthened by solid solution. [1]
>
> > [!success]- Solution (Click to expand)
> > Solid-solution strengthening works by adding solute atoms that obstruct dislocations — but those same solute atoms are the **most effective scattering centres for conduction electrons** (§6.6). They shorten the mean free path $l$ and the collision time $\tau = l/v$, so the conductivity $\sigma = ne^2\tau/m$ **falls sharply**. A transmission line must have the highest possible conductivity to minimise $I^2R$ loss over long distances, so aluminium used there is left essentially pure; the strength is supplied instead by a **steel core** (an *added-depth* design remark beyond the slides).

> [!question] Q14: Explain why lead and zinc with an even number of electrons in the outer shell and a full valence band are conductors. [2]
>
> > [!success]- Solution (Click to expand)
> > An even number of valence electrons (Zn: 2, Pb: 4) *would* fill the valence band completely if the bands were separated by a gap, and the material would then be an insulator or semiconductor — no empty states immediately above the top filled level, so no net drift is possible under a field (§6.6).
> >
> > These metals conduct because the **bands overlap**:
> >
> > - **Zinc**, like Mg and Be, has a full valence band that **overlaps in energy with the next (conduction) band**. Electrons spill over from the top of the valence band into the bottom of the next band, leaving *both* bands partially filled, with empty states immediately above the occupied ones.
> > - **Lead** is in the fourth column, but down the series C → Si → Ge → Sn → Pb the gap shrinks ($5.4 \to 1.1 \to 0.7 \to 0.08 \to 0\ \text{eV}$) and disappears at Pb, so the valence and conduction bands meet or overlap.
> >
> > Overlap removes the forbidden gap, so empty states are available just above the Fermi level, the electron distribution can be shifted by a field, and the materials are **metallic conductors**. The criterion is band overlap, not the number of electrons.
> >
> > ![[EP2 - Metals partially filled and overlapping bands.png|440]]
> >
> > *Figure — the two metallic band structures: a partially filled band (left) and overlapping bands (right); both leave empty states directly above the occupied levels.*

> [!question] Q15: Why does the conductivity of a semiconductor change with impurity content? Compare this with the behaviour of metallic conductors. [2]
>
> > [!success]- Solution (Click to expand)
> > **Semiconductor.** The conductivity is $\sigma = e(n_e\mu_e + n_h\mu_h)$, and in a pure semiconductor the carrier concentration is tiny, $n_e = n_h = N\exp(-E_g/2kT)$. Impurities change $n_e$ or $n_h$ dramatically:
> >
> > - **Donors** (fifth-column P, As, Sb) put a loosely bound electron at a level just below the conduction band; **acceptors** (third-column Al, Ga, In) create holes just above the valence band. The ionization energy is far smaller than $E_g$, so at room temperature almost every impurity atom supplies a carrier.
> > - Doping by even a few parts per million raises the carrier concentration by orders of magnitude, so $\sigma$ **increases strongly** with impurity content (and by mass action the opposite carrier is suppressed, $n_en_h = n_i^2$).
> >
> > **Metal.** The carrier concentration $n$ is already very large (about one free electron per atom) and **does not change** on alloying. Impurities act only as **scattering centres** that shorten the mean free path:
> >
> > $$ \sigma = \frac{ne^2\tau}{m}, \qquad \tau = \frac{l}{v}\ \downarrow \ \Rightarrow\ \sigma\ \downarrow $$
> >
> > | | **Semiconductor** | **Metal** |
> > | --- | --- | --- |
> > | Effect of impurity on carriers | Adds many carriers | Adds none |
> > | Effect on mobility / mean free path | Minor | Decreases (scattering) |
> > | Net effect on $\sigma$ | **Increases** (large) | **Decreases** |

> [!question] Q16: The resistance of a sample of pure germanium has the following temperature dependence: Temperature, K 312 354 385 420; Resistance, ohm 11.8 2.33 0.90 0.35. Determine the energy gap in germanium. [2]
>
> > [!success]- Solution (Click to expand)
> > For an intrinsic semiconductor the carrier number is $n = N\exp(-E_g/2kT)$ and the small temperature dependence of mobility is negligible, so
> >
> > $$ \sigma = \sigma_0\exp\!\left(-\frac{E_g}{2kT}\right) \quad\Longrightarrow\quad R \propto \frac{1}{\sigma} \propto \exp\!\left(\frac{E_g}{2kT}\right) $$
> >
> > $$ \ln R = \text{const} + \frac{E_g}{2k}\cdot\frac{1}{T} \qquad\Longrightarrow\qquad \text{slope of } \ln R \text{ vs } 1/T = \frac{E_g}{2k} $$
> >
> > | $T$ (K) | $1/T$ ($10^{-3}\ \text{K}^{-1}$) | $R$ ($\Omega$) | $\ln R$ |
> > | --- | --- | --- | --- |
> > | 312 | 3.205 | 11.8 | 2.468 |
> > | 354 | 2.825 | 2.33 | 0.846 |
> > | 385 | 2.597 | 0.90 | $-0.105$ |
> > | 420 | 2.381 | 0.35 | $-1.050$ |
> >
> > Slope between the end points:
> >
> > $$ \frac{E_g}{2k} = \frac{2.468 - (-1.050)}{(3.205 - 2.381)\times10^{-3}\ \text{K}^{-1}} = \frac{3.518}{0.824\times10^{-3}} = 4.27\times10^{3}\ \text{K} $$
> >
> > (The three successive intervals give $4.27$, $4.18$ and $4.36\times10^{3}\ \text{K}$ — consistent, confirming the straight line.) With $k = 8.617\times10^{-5}\ \text{eV/K}$:
> >
> > $$ E_g = 2k \times 4.27\times10^{3}\ \text{K} = 2\,(8.617\times10^{-5})(4.27\times10^{3}) $$
> >
> > $$ \boxed{\ E_g \approx 0.74\ \text{eV}\ } $$
> >
> > This is close to the accepted value for germanium ($\approx 0.7\ \text{eV}$, as in the gap sequence 5.4 → 1.1 → 0.7 eV for C → Si → Ge).

> [!question] Q17: A CdTe photoconductor responds to a glowing cigarette. Explain why this is so. [1]
>
> > [!success]- Solution (Click to expand)
> > A photon is absorbed in a semiconductor only if $h\nu \ge E_g$, i.e. $\lambda \le hc/E_g$, and it then lifts an electron across the gap, creating an electron–hole pair that **raises the conductivity** (photoconduction). CdTe has a band gap of about $1.5\ \text{eV}$ (*added depth*), so it responds to radiation with $\lambda \lesssim 0.83\ \mu\text{m}$ — the red and near-infrared end of the spectrum. The glowing tip of a cigarette is hot enough ($\sim$1000 K) to emit **red/near-infrared photons** in this range, so they excite electrons across the gap, and the photoconductor's conductivity changes: it "sees" the cigarette.

> [!question] Q18: Determine the wavelength of the light from a GaAs laser, assuming that the radiative transition occurs between the bottom of the conduction band and the top of the valence band. [2]
>
> > [!success]- Solution (Click to expand)
> > A radiative transition between the conduction-band edge and the valence-band edge emits a photon of energy $h\nu = E_g$, so
> >
> > $$ \lambda = \frac{hc}{E_g} $$
> >
> > For GaAs $E_g = 1.43\ \text{eV}$ (*value from standard tables; the slides give only the method*). Using $hc = 1.240\ \text{eV}\,\mu\text{m}$:
> >
> > $$ \lambda = \frac{1.240\ \text{eV}\,\mu\text{m}}{1.43\ \text{eV}} = 0.867\ \mu\text{m} $$
> >
> > Check in SI units: $\lambda = \dfrac{(6.626\times10^{-34})(3.00\times10^{8})}{1.43\times1.602\times10^{-19}} = 8.68\times10^{-7}\ \text{m}$ ✓.
> >
> > $$ \boxed{\ \lambda \approx 0.87\ \mu\text{m} = 870\ \text{nm}\ } $$
> >
> > This lies in the **near-infrared**, just beyond the red edge of the visible spectrum ($\sim0.70\ \mu\text{m}$), consistent with a band gap below the $1.8\ \text{eV}$ visible limit.

> [!tip] Exam pointer — Endsem 2, electronic (Q10–Q18)
> Have ready: the three limits of $P(E)$; $v_F = \sqrt{2E_F/m}$ (convert eV → J first); the rule "solutes scatter electrons so $\sigma$ falls" for Q12, Q13 and Q15; band overlap as the reason for Zn and Pb; the linear fit $\ln R$ vs $1/T$ with slope $E_g/2k$; and $\lambda = hc/E_g = 1.24/E_g(\text{eV})\ \mu\text{m}$ (§6.5, §6.6, §7.4–§7.8, §9.12).

---

## E2-C. Dielectrics (Q19–Q22)

> [!question] Q19: The dielectric constant of polyethylene is independent of temperature, while that of polyvinylchloride is not. Explain this difference in behaviour on the basis of their monomer structures. [2]
>
> > [!success]- Solution (Click to expand)
> > The temperature dependence of a dielectric constant comes only from **orientation polarization**, since electronic and ionic polarization are independent of temperature. Orientation polarization needs **permanent dipoles**, which align with the field while thermal energy tends to randomise them.
> >
> > - **Polyethylene** — monomer $\text{CH}_2{=}\text{CH}_2$ (repeat unit $-\text{CH}_2\text{CH}_2-$). The C–H bonds are practically non-polar and the symmetrical monomer has **no permanent dipole moment**, like $\text{CH}_4$ (the centres of positive and negative charge coincide). Only electronic polarization acts, so $\varepsilon_r$ is **independent of temperature**.
> > - **Polyvinylchloride** — monomer $\text{CH}_2{=}\text{CHCl}$. The C–Cl bond is polar, because Cl has a higher electronegativity than H and pulls the bonding electrons towards itself; the asymmetrical monomer therefore carries a **permanent dipole moment**, like $\text{CH}_3\text{Cl}$. The dipoles align in the field (orientation polarization), but thermal agitation randomises them as $T$ rises, so $\varepsilon_r$ **depends on temperature**.
> >
> > | | **Polyethylene** | **PVC** |
> > | --- | --- | --- |
> > | Monomer | $\text{CH}_2{=}\text{CH}_2$ | $\text{CH}_2{=}\text{CHCl}$ |
> > | Permanent dipole | No (symmetric) | Yes (C–Cl) |
> > | Polarization present | Electronic | Electronic + orientation |
> > | $\varepsilon_r$ vs $T$ | Independent | Temperature dependent |

> [!question] Q20: When ice melts into water, the dielectric constant increases, in contrast to the decrease observed during the melting of HCl. Explain why this is so. [1]
>
> > [!success]- Solution (Click to expand)
> > Both $\text{H}_2\text{O}$ and $\text{HCl}$ are polar molecules, so their dielectric constants are governed by **orientation polarization** — whether the permanent dipoles are free to align with the field.
> >
> > - **Ice → water (increase).** In ice the water molecules are locked into the lattice by hydrogen bonds and **cannot rotate** into the field, so orientation polarization is largely frozen out. On melting, the molecules are free to rotate and the permanent dipoles can align, so $\varepsilon_r$ **rises** (to about 80 for water).
> > - **Solid HCl → liquid HCl (decrease).** The HCl dipoles can already orient in the solid, so orientation polarization is present before melting. On melting, the greater thermal agitation of the liquid **randomises** the alignment, as the temperature dependence of orientation polarization requires, so $\varepsilon_r$ **falls**.
> >
> > *Added depth beyond the slides:* the slides treat orientation polarization and its temperature dependence (§9.5); the specific ice and HCl cases follow from that argument.

> [!question] Q21: What is the variation expected in the loss factor in a sodium silicate glass, when some of the Na⁺ ions are replaced by Rb⁺ ions? Explain. [2]
>
> > [!success]- Solution (Click to expand)
> > In a sodium silicate glass the dielectric loss at low frequencies arises from the **jumping of mobile Na⁺ ions** between sites in the open silicate network in the alternating field — a form of ionic and space-charge relaxation (§9.6–§9.7), in which part of the field energy is dissipated as heat.
> >
> > Replacing some Na⁺ by the **larger Rb⁺** ion makes the ions **less mobile**: Rb⁺ is much bigger than Na⁺ and the sites and channels left by Na⁺ are too small for it to jump readily, and the mixture of two kinds of mobile ion blocks each other's pathways (the mixed-alkali effect). Fewer and slower ion jumps mean less dissipation, so:
> >
> > $$ \boxed{\ \text{loss factor decreases on replacing Na}^+\text{ by Rb}^+\ } $$
> >
> > The loss peak also moves to lower frequencies and the d.c. conductivity of the glass falls. *Added depth beyond the slides:* the slides define the relaxation frequency and loss factor only in the optical context (§9.12); the mechanism above is the standard glass-dielectric explanation.

> [!question] Q22: Calculate the polarization of a BaTiO₃ crystal. The shift of the titanium ion from the body centre is 0.06 Å. The oxygen anions of the side faces shift by 0.06 Å, while the oxygen anions of the top and bottom faces shift by 0.08 Å, all in a direction opposite to that of the titanium ion. [2]
>
> > [!success]- Solution (Click to expand)
> > **Polarization** is the dipole moment per unit volume, $P = \sum q_i d_i / V_{\text{cell}}$. Below the Curie temperature BaTiO₃ is tetragonal with $a = 3.98\ \text{\AA}$ and $c = 4.03\ \text{\AA}$ (§9.9); the $\text{Ba}^{2+}$ ions at the corners are taken as undisplaced.
> >
> > ![[DIE - BaTiO3 cubic and tetragonal cells.png|400]]
> >
> > *Figure — the BaTiO₃ unit cell above and below the Curie temperature: the dashed circle in the front view marks the Ti ion, which shifts off the body centre on cooling, dragging the neighbouring oxygens with it.*
> >
> > **Ions in one cell.** One $\text{Ti}^{4+}$ at the body centre; oxygens ($\text{O}^{2-}$) at the face centres, each shared by two cells: the **4 side faces** contribute $4 \times \tfrac12 = 2$ oxygens, the **top and bottom faces** contribute $2 \times \tfrac12 = 1$ oxygen. Taking the Ti shift as the positive direction:
> >
> > | Ion | Number | Charge | Shift (Å) | Dipole moment ($e\,\text{\AA}$) |
> > | --- | --- | --- | --- | --- |
> > | $\text{Ti}^{4+}$ | 1 | $+4e$ | $+0.06$ | $4(0.06) = +0.24$ |
> > | $\text{O}^{2-}$ (side faces) | 2 | $-2e$ | $-0.06$ | $2(-2)(-0.06) = +0.24$ |
> > | $\text{O}^{2-}$ (top/bottom) | 1 | $-2e$ | $-0.08$ | $1(-2)(-0.08) = +0.16$ |
> > | **Total** | | | | $+0.64$ |
> >
> > The oxygens move opposite to Ti and carry the opposite charge, so all three contributions **add**.
> >
> > $$ p = 0.64\ e\,\text{\AA} = 0.64\,(1.602\times10^{-19}\ \text{C})(10^{-10}\ \text{m}) = 1.03\times10^{-29}\ \text{C\,m} $$
> >
> > Cell volume: $V = a^2c = (3.98)^2(4.03)\ \text{\AA}^3 = 63.8\ \text{\AA}^3 = 6.38\times10^{-29}\ \text{m}^3$.
> >
> > $$ P = \frac{p}{V} = \frac{1.03\times10^{-29}}{6.38\times10^{-29}} $$
> >
> > $$ \boxed{\ P \approx 0.16\ \text{C m}^{-2}\ } $$
> >
> > This large spontaneous polarization, present even without a field, is the signature of a ferroelectric.

> [!tip] Exam pointer — Endsem 2, dielectrics (Q19–Q22)
> Orientation polarization (permanent dipoles, temperature dependent) explains Q19 and Q20; for Q22 list each ion's $q\,d$ with sign and divide by the cell volume $a^2c$ (§9.3–§9.9).

---

## E2-D. Magnetic materials (Q23–Q30)

> [!question] Q23: Does a large magnetic moment per atom mean a high Curie temperature? Explain. [1]
>
> > [!success]- Solution (Click to expand)
> > **No.** The Curie temperature measures the **strength of the exchange coupling** that holds the spins aligned against thermal randomization — the stronger the exchange energy, the higher $T_C$. It is not set by the size of the atomic moment.
> >
> > | Material | Moment per atom ($\mu_B$) | Exchange energy | Curie temperature |
> > | --- | --- | --- | --- |
> > | **Co** | 1.7 | Highest | **1400 K** |
> > | **Fe** | 2.2 | Large | 1041 K |
> > | **Gd** | 7 | Small | **Below room temperature** |
> >
> > Gd has the largest moment but the lowest $T_C$, and Co has a smaller moment than Fe yet a higher $T_C$ (§8.9–§8.10).

> [!question] Q24: Explain how a high initial permeability in Fe–Ni alloys helps to reduce the area under the hysteresis loop. [2]
>
> > [!success]- Solution (Click to expand)
> > The permeability is $\mu = B/H$. A **high initial permeability** means the induction $B$ rises steeply for a very small applied field $H$ — the $B$–$H$ curve is steep near the origin.
> >
> > - This happens when the **domain walls move very easily**: the favourably oriented domains grow at the expense of the others with almost no resistance, so only a small field is needed for magnetization (§8.16). In Fe–Ni alloys the walls are not pinned by strain or inclusions.
> > - A material that magnetizes and demagnetizes with a small field has a **small coercive field $H_c$**, so the loop is **narrow and steep**.
> > - The energy dissipated as heat each cycle equals the **area of the hysteresis loop**, so a narrow loop means a small hysteresis loss.
> >
> > ![[MAG - Soft vs Hard Hysteresis.excalidraw]]
> >
> > $$ \boxed{\ \text{high } \mu_{\text{initial}} \Rightarrow \text{easy wall motion} \Rightarrow \text{small } H_c \Rightarrow \text{narrow loop} \Rightarrow \text{low loss per cycle}\ } $$
> >
> > This is the design rule of a **soft magnetic material** for transformers and other devices with frequent reversals of magnetization.

> [!question] Q25: The total iron loss in a transformer core at normal flux density was measured at 25 Hz and at 50 Hz and was found to be 250 W and 800 W respectively. Calculate (i) the eddy current loss and (ii) the hysteresis loss at 50 Hz. [2]
>
> > [!success]- Solution (Click to expand)
> > Hysteresis loss per cycle is constant (the loop area), so $W_h \propto f$; eddy-current loss $W_e \propto f^2$. At fixed flux density:
> >
> > $$ W = W_h + W_e = A f + B f^2 $$
> >
> > $$ 250 = 25A + 625B \qquad (25\ \text{Hz}) $$
> >
> > $$ 800 = 50A + 2500B \qquad (50\ \text{Hz}) $$
> >
> > Multiply the first equation by 2: $500 = 50A + 1250B$. Subtract it from the second:
> >
> > $$ 300 = 1250B \quad\Longrightarrow\quad B = 0.24\ \text{W/Hz}^2 $$
> >
> > $$ 250 = 25A + 625(0.24) = 25A + 150 \quad\Longrightarrow\quad A = 4\ \text{W/Hz} $$
> >
> > At 50 Hz:
> >
> > $$ \boxed{\ W_e = Bf^2 = 0.24\,(50)^2 = 600\ \text{W} \qquad W_h = Af = 4\,(50) = 200\ \text{W}\ } $$
> >
> > Check: $600 + 200 = 800\ \text{W}$ ✓ — the eddy-current loss dominates at 50 Hz (75 % of the total).

> [!question] Q26: The electrical resistivity of iron increases by a factor of 6, on alloying with 4% silicon. Estimate the decrease in eddy current losses for this change in composition. [2]
>
> > [!success]- Solution (Click to expand)
> > Eddy currents are induced in the core by the changing flux; the larger the resistivity $\rho$, the smaller the current for a given induced emf and the lower the power dissipated:
> >
> > $$ W_e \propto \frac{f^2B^2t^2}{\rho} \quad\Longrightarrow\quad W_e \propto \frac{1}{\rho}\ \ \text{(same } f,\ B,\ \text{sheet thickness } t) $$
> >
> > With $\rho_{\text{Fe-Si}} = 6\rho_{\text{Fe}}$:
> >
> > $$ \frac{W_e(\text{Fe–4\%Si})}{W_e(\text{Fe})} = \frac{\rho_{\text{Fe}}}{\rho_{\text{Fe-Si}}} = \frac{1}{6} = 0.167 $$
> >
> > $$ \boxed{\ \text{eddy loss falls to } 1/6 \text{ of its value} \ \ (\text{a decrease of } \approx 83\,\%)\ } $$
> >
> > This is why silicon is added to iron for transformer cores. *Added depth beyond the slides:* the $1/\rho$ dependence of eddy loss is the standard result; the slides state the benefit only qualitatively (§8.17).

> [!question] Q27: In the 1st transition metal element series only Fe, Co, Ni are ferromagnetic. Explain this observation from exchange energy viewpoint. [2]
>
> > [!success]- Solution (Click to expand)
> > In Fe, Co and Ni the unpaired $3d$ electrons on neighbouring atoms align their spins **parallel**, which lowers their spin-dependent electrostatic energy. This gain is partly offset by a rise in the Fermi level and in the average kinetic energy of the electrons. The net gain is the **exchange interaction energy**:
> >
> > $$ E_{\text{exchange}} = E_{\text{unmagnetized}} - E_{\text{magnetized}} $$
> >
> > It is a sensitive function of the ratio of the atomic diameter to the $3d$ orbital diameter, and is **positive** — parallel spins favoured, spontaneous magnetization — only when
> >
> > $$ \boxed{\ 1.5 < \frac{d_{\text{atom}}}{d_{3d}} < 2.0\ } $$
> >
> > Among the first-series metals only **Fe, Co and Ni** have a ratio inside this window. The rest are outside it: the elements at the left of the series have a ratio below the window (strong overlap, antiferromagnetic coupling), and for the others the $3d$ orbitals overlap too strongly or too weakly for parallel alignment to be favoured. In the higher transition series there is no overlap of the $d$ orbitals at all, because the $d$ electrons are strongly attracted to nuclei of larger charge; the only other elemental ferromagnets are the rare earths Gd, Tb and Dy, where the $4f$ electrons align.
> >
> > | Element | $d_{\text{atom}}/d_{3d}$ | $E_{\text{exchange}}$ | Behaviour |
> > | --- | --- | --- | --- |
> > | Fe, Co, Ni | Within 1.5–2.0 | Positive | **Ferromagnetic** |
> > | Mn (and others in the series) | Outside the window | Not positive | Not ferromagnetic |

> [!question] Q28: None of the constituent elements in Heusler alloys such as Cu₂MnSn and Cu₂MnAl are ferromagnetic yet they show ferromagnetic behaviour. Give reason for this observation. [1]
>
> > [!success]- Solution (Click to expand)
> > Ferromagnetism depends on the **ratio** $d_{\text{atom}}/d_{3d}$ lying between 1.5 and 2.0 (Q27), not on the element itself. In elemental Mn the ratio is outside this window, so the exchange energy is not positive and Mn is not ferromagnetic. **Alloying changes the interatomic distance**: in $\text{Cu}_2\text{MnSn}$ and $\text{Cu}_2\text{MnAl}$ the Mn atoms are separated by Cu and Sn (or Al), which increases the Mn–Mn distance by the right amount, so the ratio falls in the 1.5–2.0 range, the exchange energy becomes positive, and the Mn spins on neighbouring atoms align parallel. The alloy is therefore ferromagnetic although Cu is diamagnetic and Mn and Sn are not ferromagnetic as elements (§8.11).

> [!question] Q29: In nickel ferrite, NiFe₂O₄, the ferric ions are antiferromagnetically coupled. The magnetization is due to the nickel ions. When zinc is added to nickel ferrite, the magnetization of the crystal increases, even though the zinc ions are not ferromagnetic. Explain how this could happen. [2]
>
> > [!success]- Solution (Click to expand)
> > NiFe₂O₄ is an **inverse spinel**: the $\text{Ni}^{2+}$ ions and half of the $\text{Fe}^{3+}$ ions occupy the octahedral (B) sites, and the other half of the $\text{Fe}^{3+}$ ions occupy the tetrahedral (A) sites. The $\text{Fe}^{3+}$ ions on the two sites ($5\,\mu_B$ each) are coupled **antiparallel** and cancel, so the net moment is from $\text{Ni}^{2+}$ alone ($\approx 2\,\mu_B$ per formula unit).
> >
> > $\text{Zn}^{2+}$ ($3d^{10}$) has **no magnetic moment** and strongly prefers **tetrahedral** sites. Added Zn therefore **displaces $\text{Fe}^{3+}$ from the A sites to the B sites**. For $\text{Ni}_{1-x}\text{Zn}_x\text{Fe}_2\text{O}_4$:
> >
> > $$ \text{A}:\ \text{Zn}_x\text{Fe}_{1-x} \qquad \text{B}:\ \text{Ni}_{1-x}\text{Fe}_{1+x} $$
> >
> > $$ M = M_B - M_A = \left[2(1-x) + 5(1+x)\right] - 5(1-x) = 2 + 8x\ \ \mu_B $$
> >
> > Each Zn removes one $5\,\mu_B$ moment from the antiparallel A sublattice and adds one to the B sublattice, so the **cancellation is reduced and the net magnetization rises** — even though Zn itself is non-magnetic. *Added depth beyond the slides:* at high $x$ the A–B coupling weakens so much that $M$ falls again; the linear rise holds for small $x$ (same argument as Endsem-1 Q11(b)).

> [!question] Q30: Fe–4% Si is a preferred material for transformer core whereas Ni–Zn ferrites or other oxide magnetic materials are used for high frequency applications like microwave isolators. Explain the reason behind this choice from energy loss aspect for soft magnetic materials. [2]
>
> > [!success]- Solution (Click to expand)
> > The energy loss in a soft magnetic material has two parts:
> >
> > - **Hysteresis loss** — the loop area per cycle, so $W_h \propto f$. It is kept low by easy domain-wall motion (narrow loop).
> > - **Eddy-current loss** — $W_e \propto f^2B^2t^2/\rho$, growing as the *square* of frequency and falling with the resistivity $\rho$.
> >
> > **Fe–4% Si (power transformers, 50–60 Hz).** Silicon raises the resistivity (Q26) and so cuts the eddy loss; at power frequency the hysteresis loss is low (narrow loop) and, with laminated sheets, the total loss is small. It also keeps the **high saturation induction** of iron, giving a compact core.
> >
> > **Ni–Zn ferrites and other oxides (high frequency, microwave).** At high frequency $f^2$ makes the eddy loss in any metal enormous, because metals have low $\rho$ even when alloyed and laminated. Ferrites are **ceramic oxides with very high electrical resistivity** (they are insulators or poor semiconductors), so eddy currents are essentially suppressed and the total loss stays small up to high frequency. The price is a lower saturation magnetization than iron.
> >
> > | | **Fe–4% Si** | **Ni–Zn ferrite** |
> > | --- | --- | --- |
> > | Resistivity | Low (raised by Si) | Very high (oxide) |
> > | Eddy loss at high $f$ | Large ($\propto f^2$) | Negligible |
> > | Saturation induction | High | Lower |
> > | Use | Power frequency (50 Hz) | High frequency, microwave |
> >
> > The choice is made on the **dominant loss term at the operating frequency**. *Added depth beyond the slides:* the slides describe soft magnets through hysteresis loss only (§8.17); the eddy-current argument is the standard completion.

> [!tip] Exam pointer — Endsem 2, magnetic (Q23–Q30)
> Have ready: Curie temperature set by exchange energy, not moment (Co > Fe, Gd low); loop area = loss per cycle; $W_h \propto f$ and $W_e \propto f^2/\rho$ with the two-equation solve for Q25; the $1.5 < d_{\text{atom}}/d_{3d} < 2.0$ window for Q27 and Q28; and the A/B sublattice count $M = 2 + 8x$ for Q29 (§8.9–§8.17).

---

## E2-E. Semiconductors again (Q31–Q32)

> [!question] Q31: Draw and explain conductivity vs temperature plot for an extrinsic semiconductor. [2]
>
> > [!success]- Solution (Click to expand)
> > ![[EP2 - log conductivity versus reciprocal temperature.png|450]]
> >
> > *Figure — $\log\sigma$ against $1/T$: a steep extrinsic (ionization) branch at low temperature, a flat exhaustion plateau near room temperature, and a steeper intrinsic branch above it.*
> >
> > The plot of $\log\sigma$ against $1/T$ for an extrinsic semiconductor has **three regions** (low $T$ on the right):
> >
> > 1. **Extrinsic (ionization) region — low $T$.** Carriers are excited from the donor level (or into the acceptor level) and their number grows exponentially with $T$, so $\log\sigma$ is linear in $1/T$. The slope gives the **impurity ionization energy**.
> > 2. **Exhaustion region — intermediate $T$.** The impurities are all ionized, so the carrier number is constant and the curve is **flat**; the slope may even turn positive because the mobility falls as $T$ rises (shorter mean free path).
> > 3. **Intrinsic region — high $T$.** Electrons are excited across the gap from the valence band, so $\log\sigma$ is linear again with a **steep negative slope** $-E_g/2k$.
> >
> > $$ \boxed{\ \text{slope}_{\text{extrinsic}} \sim -\frac{E_{\text{ionization}}}{k} \ \ll\ \text{slope}_{\text{intrinsic}} = -\frac{E_g}{2k}\ } $$
> >
> > The flat region is where a device is stable against temperature changes. This is the same answer as Endsem-1 Q10(a).

> [!question] Q32: Why GaAs is preferred over Si in optoelectronic communication? [1]
>
> > [!success]- Solution (Click to expand)
> > GaAs has a **direct band gap**: the conduction-band minimum and valence-band maximum occur at the same wave vector, so an electron falling across the gap can emit a photon directly ($h\nu = E_g$, $\lambda \approx 0.87\ \mu\text{m}$, Q18). Silicon has an **indirect gap**, in which recombination also needs a phonon, and so is mostly non-radiative — it gives off heat, not light, and cannot make efficient LEDs or lasers. GaAs also has a higher electron mobility, so it is suitable for fast devices. *Added depth beyond the slides:* the direct/indirect-gap argument is standard semiconductor physics, not worked in [[notes]]; the slides give only the band-gap absorption and emission relation $h\nu \ge E_g$ (§9.12).

> [!tip] Exam pointer — Endsem 2, semiconductors (Q31–Q32)
> For Q31 draw the three-region plot and say what each slope measures; for Q32 say *direct band gap → efficient radiative recombination* (§7.11, §9.12).

---

## Formula Summary — Endsem 2

| Quantity | Expression | Notes |
| --- | --- | --- |
| Hooke's law (elastic strain) | $\varepsilon = \sigma/E$ | Valid below yield; same $\sigma$ for equal geometry and load |
| Poisson's ratio | $\nu = -\varepsilon_x/\varepsilon_z$; $\nu_{\text{plastic}} = 0.5$ | $\nu \approx 0.25$–$0.35$ elastic for metals; plastic flow conserves volume |
| Volume strain (tension) | $\Delta V/V = \varepsilon_z(1-2\nu)$ | Zero at $\nu = 0.5$ |
| Resolved shear stress | $\tau_R = \sigma\cos\phi_1\cos\phi_2$, $\sigma_y = \tau_{CRSS}/m$ | $m_{\max} = 0.5$; $m = 0$ if either angle is $90^\circ$ |
| Hall–Petch | $\sigma_y = \sigma_0 + k_yd^{-1/2}$ | $d$ = grain diameter; from the pile-up argument |
| Fermi–Dirac | $P(E) = \left[1+\exp\!\left(\tfrac{E-E_F}{kT}\right)\right]^{-1}$ | $P \to 0,\ 0.5,\ 1$ for $E \gg, =, \ll E_F$ |
| Fermi velocity | $v_F = \sqrt{2E_F/m}$ | $E_F$ in J; K: $8.6\times10^5\ \text{m/s}$ |
| Metallic conductivity | $\sigma = ne^2\tau/m$ | Solutes lower $\tau$ and hence $\sigma$ |
| Intrinsic resistance | $\ln R = \text{const} + \dfrac{E_g}{2k}\dfrac{1}{T}$ | Ge: $E_g \approx 0.74\ \text{eV}$ |
| Photon wavelength at the gap | $\lambda = hc/E_g = 1.24/E_g(\text{eV})\ \mu\text{m}$ | GaAs: $0.87\ \mu\text{m}$ |
| Polarization | $P = \sum q_id_i/V$ | BaTiO₃ (Q22): $0.16\ \text{C m}^{-2}$ |
| Total core loss | $W = Af + Bf^2$ | $W_h = Af$, $W_e = Bf^2$; Q25: $A = 4$, $B = 0.24$ |
| Eddy loss | $W_e \propto f^2B^2t^2/\rho$ | Added depth; $\rho \times 6 \Rightarrow W_e/6$ |
| Exchange criterion | $1.5 < d_{\text{atom}}/d_{3d} < 2.0$ | $E_{\text{exchange}} > 0$ only inside this window |
| Zn-substituted NiFe₂O₄ | $M = 2 + 8x\ \mu_B$ | Added depth; small $x$ |

> [!note] Source images
> The Excalidraw figure `MP - Grain Boundary Pile-up.excalidraw` in Q9 is a new original reconstruction (the vault copy lives in the `Excalidraw/` folder with the `MP - ` prefix); the other Excalidraw figures are the existing `MP - ` and `MAG - ` drawings. The extracted figures are the original lecture figures stored in `Material Science/images/` with their topic prefix (`MP2`, `EP2`, `DIE`).

---

# Endsem 3 Solutions

Worked solutions to the third End-Sem paper, [[endsem3.pdf]] (IIT (BHU) Varanasi, Odd Sem 2024–25, MO 201 Materials Science, 3 hours, 60 marks; 18 questions of 5 marks each, attempt any 12, and only the **first 12 answers** are marked). The method is the same as the two sections above: each question is a card with a collapsible solution, built from [[notes]] and the lecture PDFs, with *added depth* marked where an answer goes beyond the slides.

> [!info] How this paper overlaps the others
> Most of this paper repeats questions already solved above, so those answers are carried over in full and are self-contained: **Q1** and **Q3(b)**, **Q5**, **Q6** (plus Knoop), **Q7(a)**, **Q10**, **Q12–Q18** correspond to Endsem-1 Q1–Q12 and parts of Q3–Q5. The questions that are **new** are **Q2** (Schmid factor), **Q3(a)** (slip vs twinning), **Q4** (tensile-test definitions), **Q7(b)** (steel in concrete), **Q8** (composite moduli), **Q9** (fibreglass) and **Q11** (zone refining).

| Q | Topic | Marks | Where it lives in [[notes]] |
| --- | --- | --- | --- |
| **1** | Shockley and Frank partials in FCC | 5 | §4.1–§4.8 |
| **2** | Resolved shear stress, CRSS, Schmid factor and its maximum | 5 | §2.4 |
| **3** | Slip vs twinning; sessile dislocation by a reaction | 2 + 3 | §2.2, §2.5 |
| **4** | Poisson ratio, anelasticity, necking, 0.2 % offset yield stress, modulus of resilience | 1×5 | §2.8–§2.15 |
| **5** | DBTT in iron; Yoffee diagram | 2 + 3 | §2.7 |
| **6** | Brinell, Rockwell, Vickers and Knoop tests | 5 | §3.4–§3.7 |
| **7** | Carbon black vs silica; steel in concrete | 2 + 3 | §5.6, §5.7 |
| **8** | Elastic modulus of aligned-fibre composites (longitudinal, transverse) | 2.5×2 | §5.10 |
| **9** | Fibreglass composite: advantages, limitations, applications | 5 | §5.13 |
| **10** | Iron–carbon phase diagram | 5 | [[Phase_Diagrams.pdf]] |
| **11** | Principle of zone refining | 5 | [[Phase_Diagrams.pdf]] |
| **12** | Free electron theory and conduction | 5 | §6.2–§6.6 |
| **13** | Intrinsic, p-type and n-type semiconductors | 1+2+2 | §7.7–§7.10 |
| **14** | Conductivity vs $T$; forward and reverse bias | 3+2 | §7.11, §7.13–§7.14 |
| **15** | Heusler alloys; Zn in NiFe₂O₄; ferrimagnetism | 2+2+1 | §8.9, §8.11–§8.13 |
| **16** | Polarization mechanisms; BaTiO₃ | 2+3 | §9.3–§9.9 |
| **17** | Cermets, hybrid composites, critical fibre length | 2+2+1 | §5.6, §5.16, §5.9 |
| **18** | Types of structural composites | 5 | §5.18 |

---

## E3-A. Dislocations, mechanical behaviour and particle reinforcement (Q1–Q7)

> [!question] Q1: Explain what are Shockley and Frank partial dislocations in FCC. [5]
>
> > [!success]- Solution (Click to expand)
> > **Background — why a perfect dislocation splits.** A dislocation's elastic energy per unit length is $E_{el} \approx \alpha G b^2$, so replacing one long Burgers vector by two shorter ones with the same vector sum lowers the energy. In FCC the perfect dislocation is $\mathbf{b} = \tfrac{a}{2}\langle110\rangle$, with $b^2 = a^2/2$. The close-packed $\{111\}$ planes stack as $\ldots ABCABC\ldots$, and a partial dislocation is one whose Burgers vector is *not* a lattice translation, so it leaves a **stacking fault** behind it (§4.1–§4.2).
> >
> > ![[SD - Dissociation into Shockley partials.excalidraw]]
> >
> > **(a) Shockley partial**
> >
> > - A **Shockley partial** is a partial dislocation with $\mathbf{b} = \tfrac{a}{6}\langle112\rangle$, magnitude $b_p = a/\sqrt6 = 0.408\,a = b/\sqrt3$.
> > - Its Burgers vector lies **in** the $\{111\}$ plane of the fault it bounds, so it is **glissile**: it glides conservatively in that plane. Glide of the leading partial *creates* an intrinsic stacking fault (one wrong layer, $ABC\,A\,|\,C\,A\,B\ldots$); glide of the trailing partial *removes* it.
> > - It is formed by the **dissociation** of a perfect dislocation into two Shockley partials:
> >
> > $$ \frac{a}{2}[1\bar{1}0] \;\longrightarrow\; \frac{a}{6}[2\bar{1}\bar{1}] + \frac{a}{6}[1\bar{2}1] \qquad \text{on the } (111) \text{ plane} $$
> >
> > Checks:
> >
> > 1. **Burgers-vector conservation** — $\tfrac{a}{6}[2\bar{1}\bar{1}] + \tfrac{a}{6}[1\bar{2}1] = \tfrac{a}{6}[3\bar{3}0] = \tfrac{a}{2}[1\bar{1}0]$ ✓.
> > 2. **Frank's rule (energy)** — $b_1^2 + b_2^2 = \tfrac{a^2}{6} + \tfrac{a^2}{6} = \tfrac{a^2}{3} < \tfrac{a^2}{2} = b^2$: a **33 % energy saving**, so dissociation is always favourable in FCC.
> > 3. **Geometry** — the parent and both partials lie in the fault plane $(111)$: $[1\bar{1}0]\cdot[111] = 0$, $[2\bar{1}\bar{1}]\cdot[111] = 0$ and $[1\bar{2}1]\cdot[111] = 0$ ✓. Each partial is $30^\circ$ from the parent vector ($\cos\theta = 3/\sqrt{12} = 0.866$) and the two are $60^\circ$ apart.
> >
> > - The two partials repel; the fault ribbon between them pulls them together. They settle at the **equilibrium separation** where repulsion balances the fault energy $\gamma_{SF}$ — the pair is an **extended dislocation**, with $d \propto G b_p^2/\gamma_{SF}$.
> >
> > $$ \boxed{\ \frac{a}{2}\langle110\rangle \longrightarrow \frac{a}{6}\langle112\rangle + \frac{a}{6}\langle112\rangle, \qquad b^2:\ \frac{a^2}{2} \to \frac{a^2}{3}\ } $$
> >
> > **(b) Frank partial**
> >
> > - A **Frank partial** is a pure **edge** partial dislocation with $\mathbf{b} = \tfrac{a}{3}\langle111\rangle$, with $|\mathbf{b}_F| = a/\sqrt3$, which is exactly the $\{111\}$ interplanar spacing $d_{111}$; $b_F^2 = a^2/3$.
> > - Its Burgers vector is **normal** to the fault plane, not in it. It therefore **cannot glide**: gliding would require dragging the fault disc with it, which is non-conservative. It is **sessile**, and can move only by **climb** (absorbing or emitting vacancies/interstitials).
> > - **Formation:** vacancies supersaturated by quenching or irradiation condense on a $\{111\}$ plane as a flat plate; the plate **collapses** by one plane spacing, leaving an *intrinsic* stacking fault on the plane, and the rim of the faulted disc is a **Frank loop** of vacancy type. Condensation of interstitials gives an *extrinsic* fault bounded by an interstitial-type loop.
> > - **Removal:** by climb (high temperature), or by **unfaulting** when a Shockley partial sweeps the faulted plane and reacts with the Frank partial:
> >
> > $$ \frac{a}{3}[111] + \frac{a}{6}[11\bar{2}] \longrightarrow \frac{a}{2}[110] $$
> >
> > $$ \boxed{\ \mathbf{b}_F = \frac{a}{3}\langle111\rangle,\qquad |\mathbf{b}_F| = \frac{a}{\sqrt3} = d_{111},\qquad \mathbf{b}_F \perp \text{fault plane} \ \Rightarrow\ \text{sessile}\ } $$
> >
> > ![[SD - Frank partial from a vacancy plate.excalidraw]]
> >
> > | | **Shockley partial** | **Frank partial** |
> > | --- | --- | --- |
> > | Burgers vector | $\tfrac{a}{6}\langle112\rangle$ | $\tfrac{a}{3}\langle111\rangle$ |
> > | $b^2$ | $a^2/6$ | $a^2/3$ |
> > | $\mathbf{b}$ vs fault plane | **lies in** the plane | **normal** to the plane |
> > | Character | mixed ($30^\circ$ to parent $\mathbf{b}$) | pure edge |
> > | Mobility | **glissile** | **sessile** (climb only) |
> > | Created by | dissociation of $\tfrac{a}{2}\langle110\rangle$ | collapse of a vacancy / interstitial plate |
> > | Found in | every FCC metal, always | quenched, irradiated, fatigued metals |

> [!question] Q2: Explain with diagram what is resolved shear stress, critical resolved shear stress and Schmid factor and what is their importance with respect to plastic deformation. What can be the maximum value of Schmid factor and why? [5]
>
> > [!success]- Solution (Click to expand)
> > **Resolved shear stress.** A tensile stress $\sigma$ applied along an arbitrary axis does not act as a shear stress on the slip plane. Only the component resolved *onto the slip plane and along the slip direction* drives glide, and that component is the **resolved shear stress (RSS)** $\tau_R$.
> >
> > ![[MP - Schmid Factor Geometry.excalidraw]]
> >
> > ![[MP2 - Schmid factor geometry.png|420]]
> >
> > *Figure — the tensile axis at angles $\phi_1$ (to the slip-plane normal) and $\phi_2$ (to the slip direction); the resolved shear stress is $\tau = \sigma\cos\phi_1\cos\phi_2$.*
> >
> > **Derivation.** Let the load be $P$ on a cross-section $A$, so $\sigma = P/A$.
> >
> > 1. The area of the slip plane is enlarged by the obliquity: $A_s = A/\cos\phi_1$.
> > 2. The component of the load along the slip direction is $P\cos\phi_2$.
> > 3. Therefore
> > $$ \tau_R = \frac{P\cos\phi_2}{A/\cos\phi_1} = \frac{P}{A}\cos\phi_1\cos\phi_2 = \sigma\cos\phi_1\cos\phi_2 $$
> >
> > **Schmid factor.** The geometric factor $m = \cos\phi_1\cos\phi_2$ is the **Schmid factor**:
> >
> > $$ \boxed{\ \tau_R = \sigma\, m, \qquad m = \cos\phi_1\cos\phi_2\ } $$
> >
> > **Critical resolved shear stress (CRSS).** Slip begins on a system when $\tau_R$ reaches a critical value $\tau_{CRSS}$, a **material property** (to first order independent of orientation; it depends on temperature, impurities and dislocation density):
> >
> > $$ \tau_R = \tau_{CRSS} \quad\Longrightarrow\quad \sigma_y = \frac{\tau_{CRSS}}{m} $$
> >
> > **Maximum value of the Schmid factor.** $m_{\max} = 0.5$, reached when $\phi_1 = \phi_2 = 45^\circ$.
> >
> > *Why:* the slip direction lies *in* the slip plane, so the slip direction $\mathbf{D}$ is perpendicular to the plane normal $\mathbf{N}$. The cosines of the angles between the tensile axis and two perpendicular directions satisfy $\cos^2\phi_1 + \cos^2\phi_2 \le 1$ (with equality when the axis lies in the plane containing $\mathbf{N}$ and $\mathbf{D}$, where $\phi_1 + \phi_2 = 90^\circ$). Then
> >
> > $$ \cos\phi_1\cos\phi_2 \le \frac{\cos^2\phi_1 + \cos^2\phi_2}{2} \le \frac12 $$
> >
> > For the coplanar case $m = \cos\phi_1\sin\phi_1 = \tfrac12\sin2\phi_1$, which is largest at $\phi_1 = 45^\circ$. Equivalently, the applied load is shared between "shear on the plane" ($\propto\cos\phi_1$) and "along the direction" ($\propto\cos\phi_2$), and a $45^\circ/45^\circ$ split is the best compromise. $m = 0$ when the axis lies in the slip plane ($\phi_1 = 90^\circ$) or is perpendicular to the slip direction ($\phi_2 = 90^\circ$): the crystal cannot glide on that system.
> >
> > **Importance for plastic deformation.**
> >
> > - Plastic flow of a single crystal starts on the system with the **largest** Schmid factor, because it is the first to reach $\tau_{CRSS}$ as the load rises.
> > - The **yield stress of a single crystal depends on orientation**: it is lowest ($\sigma_y = 2\tau_{CRSS}$) when $m = 0.5$ and, in principle, infinite when $m = 0$.
> > - It tells which system is active, and hence the direction of slip lines and the crystal rotation during deformation.
> > - In a polycrystal the grains are randomly oriented and constrained by their neighbours, so an average factor, the Taylor factor $M \approx 3.06$ for FCC, relates macroscopic yield to the CRSS: $\sigma_y \approx M\tau_{CRSS}$.

> [!question] Q3: (a) What is the difference between slip and twinning? (b) Explain with diagram the formation of a sessile dislocation in an FCC crystal by a dislocation reaction. [2 + 3 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Slip versus twinning** [2 marks]
> >
> > Both are **shear** processes in which the resolved shear stress on a plane, in a direction, does the work.
> >
> > | | **Slip** | **Twinning** |
> > | --- | --- | --- |
> > | Displacement | Block above the plane shifts by a **whole number of lattice spacings** | Each successive plane shifts by a **fraction** of a spacing, growing with distance from the twin plane |
> > | Lattice orientation | **Unchanged** | **Changed** — the twinned region is a mirror image of the parent |
> > | Surface evidence | A visible **step** (slip line) | A reoriented, tilted region |
> > | Strain produced | Large (repeats indefinitely) | Small and bounded (a few per cent) |
> > | Stress needed | Low (reaches CRSS first) | High (often 2–3 times CRSS) |
> > | When it dominates | Normal case (FCC, BCC) | When slip is hard: HCP metals, low $T$, high strain rate, low-SFE FCC |
> >
> > ![[MP2 - Slip and twinning sequence.png|420]]
> >
> > *Figure — (a) before deformation; (b) after slip, the upper block is displaced by a whole number of lattice spacings and the surface shows a step; (c) after twinning, each plane is displaced by a fraction of a spacing, producing a mirror-image (twinned) region.*
> > **(b) A sessile dislocation from a dislocation reaction — the Lomer lock** [3 marks]
> >
> > Dislocations gliding on **non-parallel** $\{111\}$ planes meet along the line where their planes intersect and can **react**. A reaction proceeds if the Burgers vector is conserved and the strain energy ($\propto b^2$) falls (**Frank's rule**): $\mathbf{b}_3 = \mathbf{b}_1 + \mathbf{b}_2$ and $b_3^2 < b_1^2 + b_2^2$.
> >
> > ![[MP - Dislocation Reaction Sessile Lock.excalidraw]]
> >
> > Take $\mathbf{b}_1 = \tfrac{a}{2}[10\bar{1}]$ gliding on $(111)$ and $\mathbf{b}_2 = \tfrac{a}{2}[011]$ gliding on $(11\bar{1})$. (Each lies in its own plane: $[10\bar{1}]\cdot[111] = 0$ and $[011]\cdot[11\bar{1}] = 0$.) The two planes intersect along $[1\bar{1}0]$, and the dislocations react there:
> >
> > $$ \frac{a}{2}[10\bar{1}] + \frac{a}{2}[011] \;\longrightarrow\; \frac{a}{2}[110] $$
> >
> > $$ b_1^2 + b_2^2 = \frac{a^2}{2} + \frac{a^2}{2} = a^2 \;\longrightarrow\; b_3^2 = \frac{a^2}{2} \qquad (50\,\%\ \text{energy decrease}) $$
> >
> > The reaction is therefore favourable. The product $\tfrac{a}{2}[110]$ is perpendicular to the line $[1\bar{1}0]$, so its glide plane (the plane containing both $\mathbf{b}$ and the line) is $(001)$ — a $\{100\}$-type plane, which is **not** a close-packed slip plane of FCC. It cannot glide: it is **sessile** (a *Lomer lock*).
> >
> > ![[MP2 - Lomer sessile lock formation.png|440]]
> >
> > *Figure — two mobile dislocations on non-parallel $\{111\}$ planes meet along the line of intersection and react to form a sessile dislocation; further glide on either plane is blocked and dislocations pile up behind the lock.*
> >
> > **Consequence.** Dislocations on both planes pile up behind the lock, producing a long-range back stress that opposes the applied stress. A higher stress is therefore needed for further deformation — a basic mechanism of **work hardening**.
> >
> > $$ \boxed{\ \tfrac{a}{2}[10\bar{1}] + \tfrac{a}{2}[011] \to \tfrac{a}{2}[110],\qquad a^2 \to \tfrac{a^2}{2},\ \text{product sessile}\ } $$

> [!question] Q4: Define the following with respect to tensile testing: (a) Poisson ratio (b) Anelasticity (c) Necking (d) 0.2% offset yield stress (e) modulus of resilience. [1×5 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Poisson ratio** [1 mark]
> >
> > Under a tensile stress along $z$ the specimen elongates ($\varepsilon_z > 0$) and contracts laterally ($\varepsilon_x = \varepsilon_y < 0$). **Poisson's ratio** is the negative ratio of lateral to axial strain:
> >
> > $$ \boxed{\ \nu = -\frac{\varepsilon_x}{\varepsilon_z} = -\frac{\varepsilon_y}{\varepsilon_z}\ } $$
> >
> > For metals $\nu \approx 0.25$–$0.35$ in the elastic range, rising to $0.5$ in the plastic range, where volume is conserved; $E = 2G(1+\nu)$ for an isotropic solid.
> >
> > **(b) Anelasticity** [1 mark]
> >
> > In real materials part of the elastic strain is **time-dependent**: deformation continues slowly *after* the stress is applied, and on unloading a finite time is needed for complete recovery. This is **anelasticity**. It arises from time-dependent atomistic processes accompanying deformation (e.g. stress-induced ordering of solute atoms, grain-boundary relaxation). It is small in metals (about 0.1 % of the elastic strain) and large in polymers, where the behaviour is called **viscoelastic**.
> >
> > **(c) Necking** [1 mark]
> >
> > After the tensile strength (UTS) the cross-section decreases locally — a **neck** forms and further deformation is confined to it. The engineering curve falls because it uses $A_0$, although the *true* stress in the neck keeps rising. Necking starts when the load stops increasing, $dP = 0$, which with constant volume gives the **Considère criterion**:
> >
> > $$ \boxed{\ \frac{d\sigma_T}{d\varepsilon_T} = \sigma_T\ } $$
> >
> > It is a geometric instability, not a material failure: the neck begins where the area reduction outruns work hardening. With Hollomon's equation $\sigma_T = K\varepsilon_T^n$ this becomes $\varepsilon_{T,u} = n$.
> >
> > **(d) 0.2 % offset yield stress** [1 mark]
> >
> > Most metals show a gradual elastic-to-plastic transition, so yield strength is defined by convention: draw a line **parallel to the elastic portion starting at $\varepsilon = 0.002$**; its intersection with the stress–strain curve is the **0.2 % offset yield stress** $\sigma_y$, the stress at which the material has accumulated 0.2 % *plastic* strain.
> >
> > ![[MP2 - 0.2 percent offset yield strength.png|440]]
> >
> > *Figure — the 0.2 % offset construction (left) and the upper/lower yield points of a low-carbon steel with the 0.2 % offset yield strength marked on the same curve (right).*
> >
> > **(e) Modulus of resilience** [1 mark]
> >
> > The **modulus of resilience** is the energy absorbed per unit volume in the elastic range — the area under the stress–strain curve **up to yield**, the ability to store energy and spring back:
> >
> > $$ \boxed{\ U_r = \int_0^{\varepsilon_y}\sigma\,d\varepsilon = \tfrac12\sigma_y\varepsilon_y = \frac{\sigma_y^2}{2E}\ } \qquad [\text{J/m}^3] $$
> >
> > It is favoured by a **high yield strength and low modulus**, which is why springs are made of high-yield materials.
> >
> > ![[MP2 - Resilience and toughness areas.png|400]]
> >
> > *Figure — the modulus of resilience is the small triangular area up to yield; the modulus of toughness is the whole area under the curve to fracture.*

> [!question] Q5: (a) What is ductile to brittle transition in iron? (b) What is Yoffee diagram? [2 + 3 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Ductile-to-brittle transition in iron** [2 marks]
> >
> > The same material gives quite different tensile curves at different temperatures. For **iron**:
> >
> > | Temperature | Behaviour |
> > | --- | --- |
> > | $-200\ ^\circ\text{C}$ | Very high yield stress, almost no plasticity — **brittle** |
> > | $-100\ ^\circ\text{C}$ | Some ductility, much less than at room temperature — **transition** |
> > | $25\ ^\circ\text{C}$ | Long plastic region and pronounced necking — **ductile** |
> >
> > ![[MP2 - Iron curves at three temperatures.png|440]]
> >
> > *Figure — the same material (iron) tested at $-200$, $-100$ and $25\ ^\circ\text{C}$: the low-temperature curve is almost linear to fracture; the room-temperature curve shows a long plastic region and a neck.*
> >
> > Iron is BCC, so its screw dislocations have non-planar cores and a large Peierls barrier: motion past obstacles needs thermal help, and the yield stress is strongly temperature-dependent.
> >
> > **(b) The Yoffee diagram** [3 marks]
> >
> > **The Yoffee diagram.** Plot two curves against temperature:
> >
> > 1. the **yield stress** $\sigma_y$ — it *falls* as $T$ rises, because dislocation motion past obstacles is thermally activated;
> > 2. the **cleavage fracture stress** $\sigma_f$ — it is nearly *temperature-independent* (athermal), because breaking bonds across a plane needs no diffusion or thermal activation.
> >
> > ![[MP - Yoffee Diagram DBTT.excalidraw]]
> >
> > ![[MP2 - Yoffee diagram.png|380]]
> >
> > *Figure — the Yoffee diagram: yield stress falls with temperature, cleavage fracture stress is nearly temperature-independent, and the intersection defines the DBTT.*
> >
> > The two curves cross at the **Ductile–Brittle Transition Temperature (DBTT)**:
> >
> > - **Below DBTT:** $\sigma_f < \sigma_y$ — the stress reaches the cleavage value *before* plastic flow can blunt the crack, so the material **fractures before it yields → brittle**.
> > - **Above DBTT:** $\sigma_y < \sigma_f$ — the material **yields first**, the plastic zone blunts the crack tip, and it is **ductile**.
> >
> > $$ \boxed{\ T < T_{\text{DBTT}}:\ \sigma_f < \sigma_y\ (\text{brittle}) \qquad\quad T > T_{\text{DBTT}}:\ \sigma_y < \sigma_f\ (\text{ductile})\ } $$
> >
> > The same transition appears in the Charpy test as an S-shaped energy–temperature curve: *lower shelf* (cleavage, low energy), a steep *transition* region, and *upper shelf* (ductile, high energy).
> >
> > **What raises the DBTT** (makes iron more brittle): lower service temperature; high strain rate or impact loading (less time for thermal activation, so $\sigma_y$ rises); a sharp notch (triaxial stress suppresses shear yielding); coarse grains; and impurities and high carbon. FCC alloys such as austenitic stainless steel, aluminium and nickel alloys have no such transition, which is why they serve at cryogenic temperatures.

> [!question] Q6: Explain the various hardness testing methods Brinell, Rockwell, Vickers and Knoop test. [5]
>
> > [!success]- Solution (Click to expand)
> > > **Hardness** is the resistance of a material to *localised plastic deformation* — a small dent or scratch. A small indenter is forced into the surface under a specified load and loading rate, and the depth or size of the indent is measured: the softer the material, the larger the indent.
> >
> > ![[MP - Hardness Indenters.excalidraw]]
> >
> > **Brinell test**
> >
> > - A hardened steel or tungsten-carbide **ball of $D = 10\ \text{mm}$** is pressed into the surface; standard loads are 500–3000 kg in 500 kg steps, held for 10–30 s.
> > - The **diameter $d$ of the circular indent** is measured under a microscope. Hardness is the load divided by the *curved surface area* of the spherical cap, whose depth is $h = \tfrac{D - \sqrt{D^2 - d^2}}{2}$:
> >
> > $$ \boxed{\ HB = \frac{2P}{\pi D\left[D - \sqrt{D^2 - d^2}\right]}\ } $$
> >
> > - There is only one Brinell scale, and the load must be quoted with the number. The large indent (about 1–5 mm) averages a coarse microstructure (good for cast iron) but is unsuitable for thin parts.
> >
> > **Rockwell test**
> >
> > - The number comes from the **difference in depth of penetration** between a **minor load** (10 kg — it seats the indenter and removes surface-roughness error) and a **major load**. The depth is read directly from a dial, so the test is fast.
> > - Letter scales combine an indenter and a major load — e.g. **A** (diamond cone, 60 kg), **B** ($\tfrac{1}{16}$ in. ball, 100 kg), **C** (diamond, 150 kg); superficial scales 15N/30N/45N and 15T/30T/45T are for thin specimens.
> > - With $h$ the permanent depth increase in mm (one hardness point per $0.002$ mm):
> >
> > $$ \boxed{\ HR = 100 - \frac{h}{0.002}\ \text{(diamond cone)} \qquad HR = 130 - \frac{h}{0.002}\ \text{(ball)}\ } $$
> >
> > - Readings are unreliable below about 20 and above about 100.
> >
> > **Vickers (microindentation) test**
> >
> > - A **square-based diamond pyramid with a $136^\circ$ included angle** is pressed in with a load of 1–1000 g; the two **diagonals** of the impression are measured under a microscope (after careful grinding and polishing of the surface).
> > - Hardness is load divided by the contact area of the four faces, $A = \dfrac{d^2}{2\sin 68^\circ}$:
> >
> > $$ \boxed{\ HV = \frac{2P\sin 68^\circ}{d^2} = 1.854\,\frac{P}{d^2}\ } $$
> >
> > - Because the pyramid is self-similar, HV is in principle independent of load. The indent is small enough to sit inside a single grain, so Vickers measures individual phases, thin coatings and case depth.
> >
> > **Knoop (microindentation) test**
> >
> > - A very small **elongated diamond pyramid** (rhombic base, long-to-short diagonal ratio $l/b = 7.11$, face angles $172.5^\circ$ and $130^\circ$) is pressed in with a load of 1–1000 g; the **long diagonal $l$** of the impression is measured under a microscope after careful grinding and polishing.
> > - Hardness is the load over the projected area:
> >
> > $$ \boxed{\ HK = 14.2\,\frac{P}{l^2}\ } $$
> >
> > - The elongated shape gives a **shallow indent** (depth $\approx l/30$), so Knoop is preferred for **thin coatings, very brittle ceramics and case-depth traverses**: the plastic zone is shallow and does not run through the layer being measured, and cracking is minimised.
> >
> > | | **Brinell** | **Rockwell** | **Vickers** |
> > | --- | --- | --- | --- |
> > | Indenter | 10 mm steel / WC ball | Diamond cone or steel ball | $136^\circ$ diamond pyramid |
> > | Load | 500–3000 kg | 15–150 kg | 1–1000 g |
> > | Measured | Indent diameter $d$ | Depth increase $h$ | Mean diagonal $d$ |
> > | Speed | Slow (microscope) | Fast (dial) | Slow (microscope) |
> > | Best for | Cast iron, coarse structures | Routine QC of metals | Hard materials, single phases, coatings |
> >
> > *Comparison including Knoop:* Brinell and Rockwell are **macro** tests that average over many grains, whereas Vickers and Knoop are **micro** tests that can be placed in a single grain, phase or coating. Brinell and Vickers report a stress-like load/area, Rockwell reports a depth read directly on a dial (fastest), and Knoop uses the long diagonal of its elongated indent.
> >
> > ![[MP3 - Hardness testing techniques table.png|480]]
> >
> > *Figure — the lecture table (Callister, Table 7.5) of hardness-testing techniques with indenter shapes, side/top views, formulas and the standard designation of each number.*

> [!question] Q7: (a) Why is carbon black used and not silica as particle reinforcement in vulcanized rubber? (b) Why is steel a suitable reinforcement material for concrete? [2 + 3 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Carbon black rather than silica** [2 marks]
> >
> > Carbon black — very small, essentially spherical carbon particles from the combustion of natural gas or oil in limited air — greatly improves **tensile strength, toughness, tear and abrasion resistance** of vulcanised rubber; tyres contain about 15–30 vol.% of it. For significant reinforcement the particles must be extremely small (**20–50 nm**), evenly distributed, and form a **strong adhesive bond** with the rubber matrix. Carbon black does this because of a **special interaction between the rubber molecules and the carbon particle surfaces**; with other particles such as **silica** that special interaction does not exist, so reinforcement is much less effective. It is also extremely inexpensive.
> >
> > **(b) Steel as a reinforcement for concrete** [3 marks]
> >
> > Portland cement concrete is a ceramic–ceramic particulate composite (cement paste with sand and gravel aggregate). Like most ceramics it is **relatively weak and extremely brittle**: its **tensile strength is only about 1/15 to 1/10 of its compressive strength**. Its strength is raised by embedding **steel rods, wires, bars (rebar) or mesh** in the fresh concrete, so that the steel carries the tensile load. Steel is a suitable reinforcement because:
> >
> > 1. **Its coefficient of thermal expansion is nearly the same as that of concrete.** Large concrete structures expand and contract considerably with temperature; with matched expansion the steel and concrete move together, so no thermal stresses build up at the interface and the bond is not broken by temperature cycling (the handwritten note on the paper — "same expansion coefficient" — is the key point).
> > 2. **Steel is not rapidly corroded in the cement environment.** The alkaline cement keeps the steel protected.
> > 3. **A relatively strong adhesive bond forms between steel and the cured concrete**, so load is transferred from the concrete to the steel.
> >
> > Steel is also strong and stiff in tension and cheap. The same idea is extended in **prestressed concrete**: high-strength steel wires are stretched, the concrete is poured and hardened, and when the tension is released the wires put the concrete into **compression**, so a service tensile stress must first cancel that compression before a crack can open.

> [!tip] Exam pointer — Endsem 3, Q1–Q7
> Q1: dissociation with its three checks and the Frank partial sessile because $\mathbf{b}$ is normal to the fault plane. Q2: derive $\tau_R = \sigma\cos\phi_1\cos\phi_2$ and prove $m_{\max} = 0.5$ with the direction-cosine inequality. Q4: five one-mark definitions, each with its formula ($\nu$, Considère, offset line, $U_r = \sigma_y^2/2E$). Q5: two curves and the DBTT intersection. Q6: indenter + load + measurement + formula for all four tests. Q7(b): matched thermal expansion, no corrosion in cement, strong bond (§2.4, §2.5, §2.7–§2.15, §3.4–§3.7, §4).

---

## E3-B. Composites (Q8–Q9)

> [!question] Q8: Derive the equations for elastic modulus of composite in longitudinal and transverse direction for continuous and aligned fiber composites. [2.5×2 = 5]
>
> > [!success]- Solution (Click to expand)
> > A continuous, aligned-fibre composite is **highly anisotropic**: its modulus depends on whether the load is applied along or across the fibres. Let $V_f$ and $V_m$ be the volume fractions of fibre and matrix ($V_f + V_m = 1$) and $E_f$, $E_m$ their moduli.
> >
> > ![[COMP - Isostrain vs Isostress.excalidraw]]
> >
> > **(a) Longitudinal modulus $E_{cl}$ — loading parallel to the fibres (isostrain)** [2.5 marks]
> >
> > The fibre–matrix bond is assumed perfect, so the fibres and matrix deform by the **same amount**: the **isostrain** state.
> >
> > 1. The load on the composite is the sum of the loads on the phases: $F_c = F_m + F_f$.
> > 2. With $F = \sigma A$: $\sigma_cA_c = \sigma_mA_m + \sigma_fA_f$.
> > 3. Dividing by $A_c$ and noting that, for equal lengths, area fractions equal volume fractions:
> > $$ \sigma_c = \sigma_mV_m + \sigma_fV_f $$
> > 4. Isostrain: $\varepsilon_c = \varepsilon_m = \varepsilon_f$. Substituting $\sigma = E\varepsilon$ and cancelling the common strain:
> >
> > $$ \boxed{\ E_{cl} = E_mV_m + E_fV_f = E_m(1 - V_f) + E_fV_f\ } $$
> >
> > The load carried by the fibres relative to the matrix is
> >
> > $$ \frac{F_f}{F_m} = \frac{E_fV_f}{E_mV_m} $$
> >
> > so the stiff fibres carry most of the load. $E_{cl}$ is a volume-weighted **arithmetic mean**, the **upper bound** for the composite modulus.
> >
> > **(b) Transverse modulus $E_{ct}$ — loading perpendicular to the fibres (isostress)** [2.5 marks]
> >
> > When the load is applied across the fibres the two phases are in series and carry the **same stress**: the **isostress** state.
> >
> > 1. Isostress: $\sigma_c = \sigma_m = \sigma_f = \sigma$.
> > 2. The composite strain is the volume-weighted sum of the phase strains:
> > $$ \varepsilon_c = \varepsilon_mV_m + \varepsilon_fV_f $$
> > 3. Substituting $\varepsilon = \sigma/E$ and cancelling the common stress:
> > $$ \frac{1}{E_{ct}} = \frac{V_m}{E_m} + \frac{V_f}{E_f} $$
> > 4. Inverting:
> >
> > $$ \boxed{\ E_{ct} = \frac{E_mE_f}{V_mE_f + V_fE_m}\ } $$
> >
> > $E_{ct}$ is the **lower bound**, a harmonic (compliance-weighted) mean.
> >
> > | | **Longitudinal** | **Transverse** |
> > | --- | --- | --- |
> > | Load direction | Parallel to fibres | Perpendicular to fibres |
> > | Condition | Isostrain, $\varepsilon_c = \varepsilon_m = \varepsilon_f$ | Isostress, $\sigma_c = \sigma_m = \sigma_f$ |
> > | Modulus | $E_{cl} = E_mV_m + E_fV_f$ | $E_{ct} = \dfrac{E_mE_f}{V_mE_f + V_fE_m}$ |
> > | Bound | Upper | Lower |
> >
> > For every real composite $E_{cl} > E_{ct}$ (the soft phase dominates the compliance in series), so the composite is stiff along the fibres and compliant across them.

> [!question] Q9: What is fiberglass composite? State its advantages and limitations and typical applications. [5]
>
> > [!success]- Solution (Click to expand)
> > **What it is.** **Fibreglass** (glass fibre-reinforced polymer, GFRP) is a composite consisting of **glass fibres**, either continuous or discontinuous, contained within a **polymer matrix**. It is the polymer-matrix composite produced in the largest quantities. The glass most commonly drawn into fibres is **E-glass**, with fibre diameters of 3–20 µm.
> >
> > **Advantages**
> >
> > 1. Glass is **easily drawn into high-strength fibres** from the molten state.
> > 2. It is **readily available** and can be made into a glass-reinforced plastic **economically**.
> > 3. The fibre is relatively strong, so the composite has a very high **specific strength**.
> > 4. **Chemical inertness**, so the composite is useful in corrosive environments.
> >
> > **Limitations**
> >
> > 1. **Not very stiff** — it lacks the rigidity needed for some applications, such as structural members for aircraft and bridges.
> > 2. **Service temperature limited to below about 200 °C**, because at higher temperatures most polymers begin to flow or deteriorate. High-purity fused silica fibres and high-temperature polymers such as polyimide resins extend the limit to about 300 °C.
> >
> > **Typical applications:** automotive and marine bodies, plastic pipes, storage containers, and industrial floorings; the transportation industry uses increasing amounts of GFRP to reduce vehicle weight and boost fuel efficiency.
> >
> > | | **Fibreglass (E-glass)** |
> > | --- | --- |
> > | Stiffness / strength | Moderate / moderate (high specific strength) |
> > | Weakness | Not stiff; service limit about 200 °C |
> > | Best fit | Marine, automotive, pipes, tanks, floorings |

> [!tip] Exam pointer — Endsem 3, composites (Q8–Q9)
> Q8: write the isostrain and isostress derivations as numbered steps and finish with both boxed equations, noting upper and lower bounds. Q9: four advantages, two limitations, applications (§5.10, §5.13).

---

## E3-C. Phase diagrams (Q10–Q11)

> [!question] Q10: Draw the iron-carbon phase diagram showing all the phases and invariant reactions. [5]
>
> > [!success]- Solution (Click to expand)
> > ![[PD - Iron Carbon Phase Diagram.png|520]]
> >
> > *Figure — the Fe–Fe₃C phase diagram: temperature (°C) against wt% C from 0 to 6.7, with the peritectic at 1493 °C, the eutectic at 1147 °C (4.30 wt% C), the eutectoid at 727 °C (0.76 wt% C), the critical lines A₁, A₃, A₄ and A$_{cm}$, and the typical microstructures of hypo-eutectoid, eutectoid and hyper-eutectoid steels.*
> >
> > The components are **iron** and **iron carbide (Fe₃C, cementite, 6.7 wt% C)**. Fe₃C is metastable; in the stable system the second component is graphite.
> >
> > **Phases**
> >
> > | Phase | Description | Max. carbon dissolved |
> > | --- | --- | --- |
> > | **L** | Liquid solution of C in Fe | — |
> > | **$\delta$** | High-temperature BCC solid solution (1394–1538 °C) | $\sim$0.09 wt% C at 1493 °C |
> > | **$\gamma$ (austenite)** | FCC solid solution | 2.14 wt% C at 1147 °C |
> > | **$\alpha$ (ferrite)** | BCC solid solution | 0.022 wt% C at 727 °C |
> > | **Fe₃C (cementite)** | Hard, brittle intermetallic compound | 6.7 wt% C (fixed) |
> >
> > Pure iron: melts at 1538 °C; $\delta \leftrightarrow \gamma$ at 1394 °C; $\gamma \leftrightarrow \alpha$ at 912 °C.
> >
> > **Invariant reactions** (three phases in equilibrium; $F = 0$ at fixed pressure)
> >
> > | Reaction | Name | Temperature | Compositions (wt% C) |
> > | --- | --- | --- | --- |
> > | $\delta + L \rightleftharpoons \gamma$ | **Peritectic** | 1493 °C | $\delta \approx 0.09$, $L \approx 0.53$, $\gamma \approx 0.17$ |
> > | $L \rightleftharpoons \gamma + \text{Fe}_3\text{C}$ | **Eutectic** (forms *ledeburite*) | 1147 °C | $L = 4.30$, $\gamma = 2.14$ |
> > | $\gamma \rightleftharpoons \alpha + \text{Fe}_3\text{C}$ | **Eutectoid** (forms *pearlite*) | 727 °C ($A_1$) | $\gamma = 0.76$, $\alpha = 0.022$ |
> >
> > $$ \boxed{\ \delta + L \xrightarrow{1493\,^\circ\text{C}} \gamma \qquad L \xrightarrow{1147\,^\circ\text{C}} \gamma + \text{Fe}_3\text{C} \qquad \gamma \xrightarrow{727\,^\circ\text{C}} \alpha + \text{Fe}_3\text{C}\ } $$
> >
> > **Critical lines and regions**
> >
> > - **$A_1$** — the 727 °C eutectoid horizontal; **$A_3$** — the $\gamma/(\alpha+\gamma)$ boundary falling from 912 °C to 0.76 wt% C; **$A_{cm}$** — the $\gamma/(\gamma + \text{Fe}_3\text{C})$ boundary rising to 2.14 wt% C at 1147 °C; **$A_4$** — the $\delta/\gamma$ boundary at 1394 °C.
> > - **Steels** (up to 2.14 wt% C): *hypo-eutectoid* below 0.76 wt% C (proeutectoid ferrite + pearlite), *eutectoid* at 0.76 wt% C (all pearlite), *hyper-eutectoid* above 0.76 wt% C (proeutectoid cementite + pearlite).
> > - **Cast irons** (2.14–6.7 wt% C): austenite + ledeburite and cementite at 2.14–4.30 wt% C below the eutectic, and cementite + ledeburite above 4.30 wt% C.
> > - Below 727 °C the two-phase field is $\alpha + \text{Fe}_3\text{C}$ throughout.
> >
> > *Added depth beyond the slides:* the invariant-reaction compositions of the peritectic (0.09, 0.53, 0.17 wt% C) are the standard textbook values (Callister) — the lecture figure labels only the temperature 1493 °C.

> [!question] Q11: Explain the principle of zone refining from phase diagram. [5]
>
> > [!success]- Solution (Click to expand)
> > **Principle.** Zone refining uses the fact that, when a melt of composition $c_0$ solidifies, the **first solid to crystallise is purer in the solvent than the liquid** from which it forms. Consider purifying a component $A$ that contains $B$ as the impurity, using the phase diagram below, where the liquidus and solidus both fall towards $A$ as $B$ is added.
> >
> > ![[PD - Zone Refining Phase Diagram.png|380]]
> >
> > *Figure — the phase diagram used to explain zone refining: starting at $c_0$, solidification begins at $T_1$ with solid $c_s'$ purer in $A$; remelting that solid and cooling it begins solidification at the higher temperature $T_2$ with solid $c_s''$, purer still.*
> >
> > **Step-by-step from the diagram**
> >
> > 1. Let the starting composition be $c_0$. It starts to solidify at $T_1$, where the tie-line meets the solidus.
> > 2. Just below $T_1$ a small quantity of solid of composition $c_s'$, **purer in $A$ than $c_0$**, separates from the liquid.
> > 3. Imagine cooling is stopped, the liquid is thrown away and the solid is remelted. This small quantity of liquid now has composition $c_s'$ and is purer.
> > 4. It starts to solidify at a **higher temperature $T_2$**, and the first solid to separate has composition $c_s''$, **purer in $A$ than $c_s'$**.
> > 5. Repeating the sequence a few times gives very pure $A$, although the quantity of purified material is extremely small compared with the starting material.
> >
> > **The zone-refining process.** The batch procedure above is replaced by a continuous one:
> >
> > - The material to be purified is a **long rod**. Only a **small length is molten** at any time, melted by an induction coil or electron beam.
> > - The coil or beam is moved **slowly from one end to the other**, continuously solidifying the molten zone behind it and remelting fresh material ahead of it. The solid that freezes behind is purer, and the impurity is carried along in the liquid zone to the far end.
> > - **Surface tension** is usually strong enough to hold the molten zone in place without a container, which could contaminate the melt.
> > - If the zone is passed along the rod **many times in the same direction**, the material at the starting end becomes much purer than the rest of the rod, and the impurity is swept into the end that is cut off.
> > - In a typical case **ten passes** reduce the impurity level to as low as **$10^{-6}$ times** the initial value.
> >
> > $$ \boxed{\ \text{first solid} \ (c_s < c_l) \ \text{is purer in } A \ \Longrightarrow\ \text{repeated melt–freeze passes sweep impurity to one end}\ } $$
> >
> > This technique produces the ultra-high-purity materials needed to control impurity concentration in **semiconductor crystals**.

> [!tip] Exam pointer — Endsem 3, phase diagrams (Q10–Q11)
> Q10: draw the diagram and label the three invariant temperatures and compositions (1493 °C peritectic; 1147 °C / 4.30 eutectic; 727 °C / 0.76 eutectoid). Q11: the sequence "$c_0 \to c_s' \to c_s''$ at rising temperatures" and the moving molten zone, with ten passes giving $10^{-6}$.

---

## E3-D. Electrical and electronic properties (Q12–Q14)

> [!question] Q12: Explain the free electron theory and on the basis of the same, explain why solids conduct electricity. [5]
>
> > [!success]- Solution (Click to expand)
> > **The free electron theory**
> >
> > Conduction is **not** a function of the total number of electrons in the solid — only the outermost (valence) electrons take part. In the free electron model they are not bound to any atom but are free to move through the whole solid: the **free electron gas** (**Fermi gas**). The basic assumption is that the potential field of the ion cores is **uniform** throughout the solid, so the potential energy can be set to a constant (zero) and only the kinetic energy $E = \tfrac12 mv^2$ matters. That energy is substantially lower than for a bound electron in an isolated atom, because the larger field of motion allows longer wavelengths.
> >
> > *1. Wave nature and the $E$–$k$ parabola.* The de Broglie wavelength is $\lambda = h/mv$, and the wave number is $k = 2\pi/\lambda$. Combining these with $E = \tfrac12 mv^2$:
> >
> > $$ \boxed{\ E = \frac{h^2k^2}{2m}\ } $$
> >
> > Energy rises as $k^2$ — a parabola.
> >
> > ![[EP1 - Parabolic E-k free electron.png|380]]
> >
> > *Figure — the parabolic $E$–$k$ relation of a free electron: energy rises as the square of the wave number, so long waves (small $k$) sit at the bottom of the curve.*
> >
> > *2. Quantization.* For a solid of length $L$ the wave must vanish at both ends, so $\lambda = 2L, L, \tfrac23 L, \ldots$ and $k = \pm n\pi/L$, giving $E = n^2h^2/8mL^2$. In three dimensions
> >
> > $$ E = \frac{h^2}{8m}\left(\frac{n_x^2}{L_x^2} + \frac{n_y^2}{L_y^2} + \frac{n_z^2}{L_z^2}\right) $$
> >
> > Each combination $(n_x, n_y, n_z)$ is a **quantum state** holding two electrons of opposite spin (Pauli exclusion principle); states with equal energy are **degenerate**. The levels are so close that $E$ is practically continuous, and electrons fill them from the bottom up.
> >
> > *3. Fermi energy and Fermi–Dirac statistics.* At $0\ \text{K}$ all levels up to the **Fermi energy $E_F$** are full and all above are empty. The occupation probability at temperature $T$ is
> >
> > $$ \boxed{\ P(E) = \frac{1}{1 + \exp\!\left(\dfrac{E - E_F}{kT}\right)}\ } $$
> >
> > The **Fermi level** is the level with $P = 50\,\%$, at every temperature. At $T > 0$ some electrons just below $E_F$ are excited to levels just above it.
> >
> > ![[EP1 - Fermi-Dirac distribution at three temperatures.png|440]]
> >
> > *Figure — the Fermi–Dirac distribution at three temperatures: the step at $0\ \text{K}$ broadens with temperature but every curve pivots about $P = 0.5$ at $E = E_F$.*
> >
> > **Why solids conduct electricity**
> >
> > 1. In a neutral solid, for every electron with a given speed in one direction there is another with the same speed in the opposite direction — the velocity distribution is symmetric and the net current is zero.
> > 2. An applied electric field **biases** this distribution: electrons moving towards the positive end gain velocity and those moving the other way lose some. The occupied states shift in $k$-space, giving a net velocity in one direction — a current.
> >
> > ![[EP1 - Electron redistribution under field.png|360]]
> >
> > *Figure — the field-induced shift of the occupied states: the whole Fermi sphere is displaced in $k$-space, so the electron gas acquires a net drift velocity.*
> >
> > 3. This redistribution is possible **only if empty states are available immediately above $E_F$** — the basic characteristic of conductors, as opposed to insulators and semiconductors.
> > 4. The accelerated electrons do not speed up indefinitely: they collide with obstacles, and between collisions acquire an average extra velocity — the **drift velocity** — all of which is lost at each collision.
> >
> > ![[EP1 - Extra velocity lost on collision.png|440]]
> >
> > *Figure — the drift velocity: each electron accelerates between collisions and loses the whole increment at the next one, so the steady state is a sawtooth in velocity.*
> >
> > With $n$ free electrons per unit volume, charge $e$, mass $m$ and mean collision time $\tau = l/v$ ($l$ = mean free path):
> >
> > $$ \boxed{\ \sigma = \frac{ne^2\tau}{m}\ } $$
> >
> > 5. **Resistance** arises from the collisions. In a perfect crystal at $0\ \text{K}$ the mean free path is infinite and $\sigma$ would be infinite; real crystals fall short because **solute atoms** (the most effective scatterers), other point defects, dislocations and grain boundaries all decrease $l$ and hence $\sigma$.
> >
> > **Conclusion.** Metals conduct because their valence electrons are free, and because empty states lie immediately above the Fermi level, so a field can shift the electron distribution; the conductivity is limited only by scattering. *(The model cannot explain insulators and semiconductors — it ignores the periodic lattice, whose Bragg reflection opens the energy gaps of §6.11.)*

> [!question] Q13: Explain (a) intrinsic semiconductor (b) p-type extrinsic semiconductor (c) n-type extrinsic semiconductor. [1 + 2 + 2 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Intrinsic semiconductor** [1 mark]
> >
> > In an **intrinsic** semiconductor, conduction is due to processes characteristic of the pure crystal itself — a pure Si or Ge crystal. Thermal energy excites electrons from the top of the **valence band** across the gap $E_g$ into the **conduction band**, leaving **holes** in the valence band; the electron and hole concentrations are equal. The Fermi level lies in the **middle of the gap**, so $E - E_F = E_g/2$ (for Si, $0.55\ \text{eV}$, more than twenty times $kT = 0.026\ \text{eV}$ at room temperature). Using the Fermi–Dirac distribution with the "1" dropped (Boltzmann approximation):
> >
> > $$ \boxed{\ n_e = n_h = N\exp\!\left(-\frac{E_g}{2kT}\right) \qquad\qquad \sigma = e\left(n_e\mu_e + n_h\mu_h\right)\ } $$
> >
> > where $\mu_e$ and $\mu_h$ are the electron and hole mobilities (Si: $0.14$ and $0.05\ \text{m}^2\text{V}^{-1}\text{s}^{-1}$). The carrier number grows exponentially with $T$, so a plot of $\ln\sigma$ against $1/T$ is a straight line of slope $-E_g/2k$.
> >
> > ![[EP2 - Fermi level midgap in intrinsic semiconductor.png|380]]
> >
> > *Figure — the Fermi level of an intrinsic semiconductor sits midgap, so that the energy measured from $E_F$ to either band edge is exactly $E_g/2$.*
> >
> > **(b) p-type extrinsic semiconductor** [2 marks]
> >
> > In an **extrinsic** semiconductor, conduction is due to deliberately added impurities (**doping**). A p-type semiconductor is made by doping Si with a **third-column element** — Al, Ga or In.
> >
> > - The trivalent atom, substituting for Si, has only three outer electrons, so it needs an **extra electron** to complete the four tetrahedral bonds. The electron comes from a neighbouring Si atom, which leaves a **hole**.
> > - The Al atom becomes negatively charged, and the positive hole revolves around it like a hydrogen-like centre — in the dielectric of the crystal, with a very large orbit and small binding energy.
> > - At $0\ \text{K}$ the holes stay bound; as $T$ rises they break away by thermal excitation. The bound-hole levels are **acceptor levels**, lying just **above the valence band**.
> > - By the law of mass action ($n_en_h = n_i^2$) electrons are suppressed: **holes are the majority carriers** and electrons the minority carriers.
> >
> > ![[EP2 - Silicon doped with aluminium p-type.png|470]]
> >
> > *Figure — silicon doped with aluminium: the trivalent atom completes its four bonds by taking an electron from a neighbour, leaving a mobile hole bound to a shallow acceptor level.*
> >
> > **(c) n-type extrinsic semiconductor** [2 marks]
> >
> > An n-type semiconductor is made by doping Si with a **fifth-column element** — P, As or Sb.
> >
> > - The pentavalent atom substitutes for a Si atom; **four** of its five outer electrons form the tetrahedral bonds with the four Si neighbours, and the **fifth is loosely bound** to the parent ion.
> > - Treating it as a hydrogen-like orbit in the crystal's dielectric, the radius is about $80\ \text{\AA}$ (against $0.5\ \text{\AA}$ for hydrogen) — the electron is almost free, at a level close to the conduction band: the **donor level**, just *below* the conduction band.
> > - The **ionization energy** needed to lift it into the conduction band is far smaller than $E_g$, so at room temperature most donor electrons are excited — far more than by the intrinsic process.
> > - Mass action ($n_en_h = n_i^2$) drastically reduces the holes: **electrons are the majority carriers**; the material is called n-type because the dopant donates negative charge.
> >
> > ![[EP2 - Silicon doped with phosphorus n-type.png|450]]
> >
> > *Figure — silicon doped with phosphorus: four of the five outer electrons enter the tetrahedral bonds, and the fifth occupies a shallow donor level just below the conduction band.*
> >
> > | | **n-type** | **p-type** |
> > | --- | --- | --- |
> > | Dopant | Fifth column — P, As, Sb | Third column — Al, Ga, In |
> > | Mechanism | Donates a loosely bound electron | Accepts an electron, leaving a hole |
> > | Impurity level | Donor, just below conduction band | Acceptor, just above valence band |
> > | Majority carrier | Electrons | Holes |
> > | Minority carrier | Holes | Electrons |

> [!question] Q14: Explain (a) variation of conductivity with temperature for an extrinsic semiconductor (b) forward and reverse bias in junction diode. [3 + 2 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Conductivity vs temperature for an extrinsic semiconductor** [3 marks]
> >
> > The conductivity is $\sigma = e(n_e\mu_e + n_h\mu_h)$. A plot of $\log\sigma$ against $1/T$ for an extrinsic semiconductor divides into **three regions**.
> >
> > ![[EP2 - log conductivity versus reciprocal temperature.png|450]]
> >
> > *Figure — $\log\sigma$ against $1/T$: a steep extrinsic (ionization) branch at low temperature, a flat exhaustion plateau near room temperature, and a steeper intrinsic branch above it.*
> >
> > 1. **Extrinsic (ionization) region — low $T$, large $1/T$.** Carriers are excited from the donor level to the conduction band (or created by excitation to the acceptor level), and their number grows exponentially with $T$, so $\log\sigma$ is linear in $1/T$. The slope gives the **ionization energy of the impurity**.
> > 2. **Exhaustion region — intermediate $T$.** The impurities are nearly all ionized and the unexcited ones are exhausted, so the carrier number is constant and the curve is **flat**. The slope can even turn **positive**, because the mobility falls as $T$ rises — higher $T$ shortens the mean free path.
> > 3. **Intrinsic region — high $T$ (above room temperature).** Electrons are now excited across the gap from the valence band; $\log\sigma$ is again linear in $1/T$ with a **steep negative slope** $-E_g/2k$. The difference between the extrinsic and intrinsic slopes reflects the difference between the ionization energy and $E_g$.
> >
> > $$ \boxed{\ \text{slope}_{\text{extrinsic}} \sim -\frac{E_{\text{ionization}}}{k} \ll \text{slope}_{\text{intrinsic}} = -\frac{E_g}{2k}\ } $$
> >
> > *Design use:* the flat exhaustion region is where a device is stable against temperature changes; a thermistor is instead operated on a steep branch for maximum sensitivity.
> >
> > **(b) Forward and reverse bias in a junction diode** [2 marks]
> >
> > A **p–n junction** has n-type material on one side and p-type on the other (made by diffusing dopant through a window in the oxide layer). At equilibrium the Fermi level is constant across the crystal, which forces the conduction band of the n-side to lie **lower** than that of the p-side by the contact potential $eV_0$ — a potential barrier at the junction.
> >
> > ![[EP2 - p-n junction band diagram at equilibrium.png|450]]
> >
> > *Figure — the p-n junction at equilibrium: a single Fermi level runs across both sides, the bands are offset by $eV_0$, and the junction region contains the resulting barrier.*
> >
> > At equilibrium the current from n to p equals that from p to n, both equal to $I_0$, so the net current is zero. (Electrons from the p-side slide *down* the hill with current $I_0$; the many n-side electrons must climb the barrier, and only a small Boltzmann fraction manages it.)
> >
> > - **Forward bias** — the p-side is made **positive** relative to the n-side. The barrier is **lowered by $eV_i$**, so many more n-side electrons cross; the p → n flow is unchanged (still downhill). The result is a **large net current** in the forward direction.
> >
> > ![[EP2 - Forward bias lowered barrier.png|440]]
> >
> > *Figure — forward bias: the barrier is lowered by $eV_i$, so the majority electrons can cross in large numbers and the current rises steeply.*
> >
> > - **Reverse bias** — the voltage is applied the other way. The barrier is **raised by $eV_i$**, drastically reducing the n → p flow, while the reverse flow stays at $I_0$. The net current is only the **small, constant $I_0$** (the reverse saturation current).
> >
> > ![[EP2 - Reverse bias raised barrier.png|440]]
> >
> > *Figure — reverse bias: the barrier is raised by $eV_i$, the n → p current is choked off, and only the small, barrier-independent $I_0$ survives.*
> >
> > $$ \boxed{\ I = I_0\left[\exp\!\left(\frac{eV_i}{kT}\right) - 1\right]\ } $$
> >
> > This is the **rectifying action** of the diode — large current in one direction, almost none in the other. *(The diode equation is added depth beyond the slides.)*

> [!tip] Exam pointer — Endsem 3, electrical (Q12–Q14)
> The same pointers as Endsem-1 Q8–Q10 apply: uniform potential, $E = h^2k^2/2m$, Fermi–Dirac, and the empty-states argument ending in $\sigma = ne^2\tau/m$; the $80\ \text{\AA}$ donor orbit and mass action; the three regions of $\log\sigma$ vs $1/T$ and the barrier $eV_0$ raised or lowered by the bias (§6.2–§6.6, §7.7–§7.14).

---

## E3-E. Magnetic and dielectric materials (Q15–Q16)

> [!question] Q15: (a) Explain ferromagnetism in Heusler alloys although Mn is not ferromagnetic in elemental form. (b) Explain what happens to the magnetization of NiFe₂O₄ upon addition of Zn. (c) What is ferrimagnetism? [2+2+1 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Ferromagnetism in Heusler alloys** [2 marks]
> >
> > In Fe, Co and Ni the unpaired $3d$ electrons of neighbouring atoms align their spins in parallel and lower their spin-dependent electrostatic energy. The **net energy gain** is the exchange interaction energy, $E_{\text{exchange}} = E_{\text{unmagnetized}} - E_{\text{magnetized}}$, a sensitive function of the ratio of the atomic diameter to the $3d$ orbital diameter. It is positive — parallel spins are favoured — only when
> >
> > $$ \boxed{\ 1.5 < \frac{d_{\text{atom}}}{d_{3d}} < 2.0 \ \Longrightarrow\ E_{\text{exchange}} > 0\ } $$
> >
> > In elemental **Mn** this ratio is outside the window, so the exchange energy is not positive and Mn is not ferromagnetic. On **alloying** the interatomic distance can be changed: in the **Heusler alloys** $\text{Cu}_2\text{MnSn}$ and $\text{Cu}_2\text{MnAl}$ the Mn atoms are separated by Cu and Sn (or Al), which **increases the Mn–Mn distance by the right amount**, so the ratio falls in the range $1.5$–$2.0$, the exchange energy becomes positive, and the Mn spins on neighbouring atoms align. The alloys are ferromagnetic even though none of the constituents is (Cu is diamagnetic; Mn and Sn are not ferromagnetic in elemental form). Ferromagnetism is thus a property of a *ratio* that can be engineered by alloying.
> >
> > **(b) Effect of Zn on the magnetization of NiFe₂O₄** [2 marks]
> >
> > NiFe₂O₄ is a **ferrite** with the **inverse spinel** structure: the $\text{Ni}^{2+}$ ions and half of the $\text{Fe}^{3+}$ ions occupy octahedral (B) sites, and the other half of the $\text{Fe}^{3+}$ ions occupy tetrahedral (A) sites. The two $\text{Fe}^{3+}$ sets ($5\,\mu_B$ each) are coupled **antiparallel**, so they cancel, and the net moment comes from $\text{Ni}^{2+}$ alone ($\approx 2\,\mu_B$ per formula unit) — the same logic as for $\text{Fe}^{2+}$ in magnetite, where the net moment is from the ferrous ions only.
> >
> > $\text{Zn}^{2+}$ ($3d^{10}$) has **no magnetic moment** and strongly prefers **tetrahedral** sites. On adding Zn it therefore **displaces $\text{Fe}^{3+}$ from tetrahedral sites** to octahedral sites. For $\text{Ni}_{1-x}\text{Zn}_x\text{Fe}_2\text{O}_4$:
> >
> > $$ \text{A (tetrahedral)}:\ \text{Zn}_x\text{Fe}_{1-x} \qquad \text{B (octahedral)}:\ \text{Ni}_{1-x}\text{Fe}_{1+x} $$
> >
> > $$ M = M_B - M_A = \left[2(1-x) + 5(1+x)\right] - 5(1-x) = 2 + 8x \ \ (\mu_B\ \text{per formula unit}) $$
> >
> > Each $\text{Zn}^{2+}$ added removes one antiparallel $\text{Fe}^{3+}$ ($5\,\mu_B$) from the A sublattice and puts one more on the B sublattice, so the **magnetization increases** with $x$. *(Added depth beyond the slides, which give only the ferrite formula and magnetite example:)* the linear rise holds only for small $x$; at high Zn content the A–B coupling that holds the lattice ordered is so weakened that the net magnetization and Curie temperature fall again, and for $\text{ZnFe}_2\text{O}_4$ the compound is not ferrimagnetic.
> >
> > **(c) Ferrimagnetism** [1 mark]
> >
> > **Ferrimagnetism** occurs in compounds whose constituent atoms are **antiferromagnetically coupled but have different magnetic moments**. The unequal antiparallel moments do not cancel, so each coupling leaves a **net moment**, and the sum over all the couplings can give a magnetization comparable in order of magnitude to ferromagnetism. Ferrites $\text{Me}^{2+}\text{Fe}_2^{3+}\text{O}_4^{2-}$ are the standard examples; in magnetite $\text{Fe}_3\text{O}_4$ the ferric ions ($5\,\mu_B$) cancel and the net $4\,\mu_B$ per formula unit comes from the ferrous ion.
> >
> > ![[MAG - Ferro antiferro ferrimagnetic coupling.png|460]]
> >
> > *Figure — (a) ferromagnetic, (b) antiferromagnetic and (c) ferrimagnetic coupling of electron spins in atoms, denoted by arrows; the length of an arrow is a measure of the magnetic moment of the atom. In (b) the antiparallel moments are equal and cancel exactly; in (c) they are unequal, so each pair leaves a net moment and the solid is magnetized.*
> >
> > | Coupling | Neighbouring moments | Net moment |
> > | --- | --- | --- |
> > | **Ferromagnetic** | Parallel | Full sum |
> > | **Antiferromagnetic** | Antiparallel, equal | Zero |
> > | **Ferrimagnetic** | Antiparallel, unequal | Difference of sublattice moments |

> [!warning] Part (b) goes beyond the slides
> The slides give the ferrite formula, the inverse-spinel site distribution and the magnetite moment count, but not the Zn substitution itself. The cation-site argument above is the standard textbook explanation — check it against your class notes ([[MO NOTES (1).pdf]]) before relying on the numbers.

> [!question] Q16: (a) Define the various polarization mechanisms. (b) Explain why BaTiO₃ shows ferroelectricity. [2+3 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Polarization mechanisms** [2 marks]
> >
> > When a dielectric is placed between capacitor plates it **binds charge** at its surfaces and the capacitance rises from $C = \varepsilon_0A/d$ to $C = \varepsilon_r\varepsilon_0A/d$. The **polarization** $P$ is the dipole moment per unit volume ($\text{C m}^{-2}$). The total polarization is the sum of four contributions:
> >
> > $$ \boxed{\ P = P_e + P_i + P_o + P_s\ } $$
> >
> > ![[DIE - Four polarization mechanisms.png|430]]
> >
> > *Figure — the four polarization processes in one figure: (a) electronic, (b) ionic, (c) orientation and (d) space charge; each panel shows the charge configuration before and after the field is applied.*
> >
> > 1. **Electronic polarization ($P_e$)** — displacement of the positively charged **nucleus and the negative electron cloud of an atom in opposite directions** under a field. The fastest mechanism, and **independent of temperature**.
> > 2. **Ionic polarization ($P_i$)** — in an ionic solid, **cations and anions are displaced in opposite directions**, each relative to its oppositely charged neighbours (not relative to its own nucleus, which is what distinguishes it from electronic polarization). **Independent of $T$**, but **slower** than electronic polarization because whole ions are heavier than an electron cloud.
> > 3. **Orientation polarization ($P_o$)** — molecules with a **permanent dipole moment** (e.g. CH₃Cl, where Cl pulls the bonding electrons more strongly than H; CH₄ has none) **align** with the applied field, like permanent magnetic moments in paramagnetism. It is **temperature dependent**, since thermal energy randomizes the alignment, and slower than ionic.
> > 4. **Space charge polarization ($P_s$)** — **accumulation of charge at electrodes or at interfaces** in a multiphase material, as ions diffuse over appreciable distances in the field and redistribute. It is the **slowest** mechanism, since ions diffuse over several interatomic distances.
> >
> > | Mechanism | What moves | $T$ dependence | Speed |
> > | --- | --- | --- | --- |
> > | **Electronic** | Electron cloud vs its own nucleus | Independent | Fastest |
> > | **Ionic** | Cations vs anions | Independent | Slower than electronic |
> > | **Orientation** | Permanent molecular dipoles align | Dependent | Slower than ionic |
> > | **Space charge** | Ions diffuse to interfaces | Dependent | Slowest |
> >
> > Because each mechanism can follow only a field that alternates slowly enough, the slowest ones drop out first as frequency rises — so $\varepsilon_r$ is a function of frequency.
> >
> > **(b) Ferroelectricity in BaTiO₃** [3 marks]
> >
> > A **ferroelectric** has its electric dipoles **aligned in the same direction even with no applied field** (spontaneous polarization), and its dielectric constant is about two orders of magnitude larger than that of ordinary dielectrics — over **2000** for BaTiO₃, against under 10 for ordinary dielectrics. It is the electric analogue of ferromagnetism.
> >
> > - **Above $120\ ^\circ\text{C}$** BaTiO₃ is **cubic**: the centres of positive and negative charge coincide, so there is no spontaneous dipole.
> > - **Cooling below the ferroelectric Curie temperature of $120\ ^\circ\text{C}$**, the **Ti⁴⁺ ion shifts to one side of the body centre**, with a displacement of the neighbouring oxygen anions. The cell becomes **tetragonal**, with
> >
> > $$ \frac{c}{a} = \frac{4.03\ \text{\AA}}{3.98\ \text{\AA}} = 1.012 $$
> >
> > - The positive and negative charge centres no longer coincide, so each cell carries a **dipole**. The dipoles of neighbouring cells **line up**, giving a large polarization in the solid even without a field — hence ferroelectricity and the very large $\varepsilon_r$.
> > - Ferroelectric crystals always show the **piezoelectric** effect (a charge in response to stress, a shape change in response to a field); BaTiO₃ is used in microphones, strain gauges and sonar, and its high dielectric constant makes it useful for small capacitors.
> >
> > ![[DIE - BaTiO3 cubic and tetragonal cells.png|400]]
> >
> > *Figure — the BaTiO₃ unit cell above and below the Curie temperature: the dashed circle in the front view marks the Ti ion, which shifts off the body centre on cooling, dragging the neighbouring oxygens with it.*

> [!tip] Exam pointer — Endsem 3, magnetic and dielectric (Q15–Q16)
> Quote $1.5 < d_{\text{atom}}/d_{3d} < 2.0$ for Q15(a); the sublattice count for Zn; "antiparallel + unequal = net moment". For Q16 give what moves, the $T$ dependence and the speed ranking, then cubic above 120 °C → Ti off-centre → tetragonal with $c/a = 1.012$ (§8.9, §8.11–§8.13, §9.3–§9.9).

---

## E3-F. Composites again (Q17–Q18)

> [!question] Q17: What are (a) cermets and (b) hybrid composites? (c) What is the importance of critical fiber length? [2+2+1 = 5]
>
> > [!success]- Solution (Click to expand)
> > **(a) Cermets** [2 marks]
> >
> > **Cermets** are **ceramic–metal** composites and the classic example of a *large-particle composite*. The most common cermet is **cemented carbide**: extremely hard particles of a refractory carbide ceramic — **tungsten carbide (WC)** or **titanium carbide (TiC)** — embedded in a matrix of a metal such as **cobalt or nickel**.
> >
> > - Used extensively as **cutting tools for hardened steels**.
> > - **Toughness is enhanced** by the ductile metal matrix, which isolates the carbide particles from one another and stops cracks running from particle to particle.
> > - Both matrix and particles are **refractory**, so the material withstands the high temperatures of cutting.
> > - Particle volume fractions are large — often **above 90 vol.%** — and no single material could give this combination of properties.
> >
> > **(b) Hybrid composites** [2 marks]
> >
> > A **hybrid composite** contains **two or more different kinds of fibres in a single matrix**, giving a better all-round combination of properties than a composite with only one fibre type.
> >
> > - The commonest system is **carbon + glass fibres in a polymeric resin**. Carbon fibres are strong, stiff and light but expensive; glass fibres are cheap but less stiff. The **glass–carbon hybrid** is stronger and tougher, has higher impact resistance, and can cost less than either the all-carbon or all-glass composite.
> > - The fibres may be aligned and intimately mixed, or laid up in alternating layers of one type; in virtually all hybrids the properties are **anisotropic**.
> > - Failure in tension is **non-catastrophic**: the carbon fibres fail first and load transfers to the glass fibres; when the glass fails the matrix carries the load; final failure coincides with failure of the matrix.
> > - Applications: lightweight land, water and air transport structures, sporting goods, lightweight orthopaedic components.
> >
> > **(c) Importance of the critical fibre length** [1 mark]
> >
> > The matrix loads a fibre by **shear along the interface**, so the fibre stress is zero at each end and rises towards the centre. The **critical fibre length $l_c$** is the shortest length for which the fibre can be loaded to its ultimate tensile strength $\sigma_f^*$:
> >
> > $$ \sigma_f^*\,\frac{\pi d^2}{4} = \tau_c\,\pi d\,\frac{l_c}{2} \quad\Longrightarrow\quad \boxed{\ l_c = \frac{\sigma_f^* d}{2\tau_c}\ } $$
> >
> > where $d$ is the fibre diameter and $\tau_c$ is the fibre–matrix bond strength or the matrix shear yield strength, whichever is smaller.
> >
> > ![[COMP - Fiber stress profiles at critical length.png|430]]
> >
> > *Figure — stress–position profiles for a fibre-reinforced composite loaded to the fibre tensile strength $\sigma_f^*$: (a) $l=l_c$, where the maximum fibre stress is reached only at the axial centre; (b) $l>l_c$, where the fibre is more effectively loaded; (c) $l<l_c$, where the fibre never reaches its strength and pulls out instead of fracturing.*
> >
> > | Fibre length | What happens |
> > | --- | --- |
> > | $l < l_c$ | Fibre never reaches $\sigma_f^*$ — it **pulls out**; little reinforcement |
> > | $l = l_c$ | Peak stress $\sigma_f^*$ reached only at the centre |
> > | $l > l_c$ | Fibre loaded to its full strength over most of its length — effective reinforcement |
> > | $l > 15\,l_c$ | Treated as **continuous** |
> >
> > For common glass and carbon fibres $l_c \approx 1\ \text{mm}$, i.e. 20–150 times the fibre diameter. $l_c$ therefore tells the designer how long the fibres must be to reinforce effectively.

> [!question] Q18: Explain the types of structural composites. [5]
>
> > [!success]- Solution (Click to expand)
> > **Types of structural composites**
> >
> > A **structural composite** is a multi-layered, normally low-density composite used where structural integrity — high tensile, compressive and torsional strength and stiffness — is needed. Its properties depend on the constituent materials *and* on the **geometrical design** of the structural elements. The two most common types are **laminar composites** and **sandwich panels**.
> >
> > *1. Laminar composites (laminates).* Two-dimensional sheets or **plies** (laminae), each with a preferred high-strength direction (as in continuous aligned fibre polymers), are bonded together. Properties depend on how the high-strength direction changes from ply to ply:
> >
> > | Class | Stacking pattern | Consequence |
> > | --- | --- | --- |
> > | **Unidirectional** | Same high-strength direction in every ply | Maximum axial stiffness and strength; highly anisotropic |
> > | **Cross-ply** | Alternating $0^\circ$ and $90^\circ$ layers | Stiffness in two perpendicular directions; more balanced |
> > | **Angle-ply** | Alternating $+\theta$ and $-\theta$ (e.g. $\pm45^\circ$) | Good shear and torsion resistance |
> > | **Multidirectional** | Several orientations | Most isotropic in-plane response |
> >
> > ![[COMP - Classes of laminar composites.png|360]]
> >
> > *Figure — the four classes of laminar composites: (a) unidirectional, (b) cross-ply, (c) angle-ply and (d) multidirectional. The arrows show the high-strength direction of each ply.*
> >
> > Layers are stacked **symmetrically about the midplane** to prevent out-of-plane twisting or bending. Applications: aircraft fuselage and stabilizers, automobile panels and drive shafts, ship hulls and decks, bridge components and roof structures, the modern ski.
> >
> > *2. Sandwich panels.* A lightweight beam or panel with high stiffness and strength: two outer sheets (**faces** or skins) separated by, and adhesively bonded to, a thicker **core**.
> >
> > - **Faces** are stiff and strong (aluminium alloys, steel, stainless steel, fibre-reinforced plastics, plywood) and carry the **bending loads** — one face in compression, the other in tension.
> > - The **core** is lightweight with a low modulus; it supports the faces continuously, holds them apart, and resists **transverse shear** (it needs adequate shear strength and enough thickness for shear stiffness, to resist buckling).
> > - Panel stiffness depends mainly on **core material and thickness**. Core materials are **rigid polymeric foams, wood, and honeycombs**. Strong face–core bonding is essential, and the panel is cost-effective because cores are cheaper than faces.
> >
> > ![[COMP - Sandwich panel cross section.png|380]]
> >
> > *Figure — cross-section of a sandwich panel: two stiff, strong faces separated by a thick, lightweight core. The faces carry bending stress; the core carries transverse shear and keeps the faces apart.*
> >
> > ![[COMP - Honeycomb core sandwich panel.png|460]]
> >
> > *Figure — construction of a honeycomb-core sandwich panel: face sheets are adhesively bonded to a honeycomb core, giving high bending stiffness at low weight.*

> [!tip] Exam pointer — Endsem 3, composites (Q17–Q18)
> Q17: $l_c = \sigma_f^*d/2\tau_c$ with its force-balance derivation, and the $l < l_c$ / $l > l_c$ / $l > 15l_c$ ladder. Q18: laminates (four classes) plus sandwich panels (faces, core, three core types) (§5.9, §5.16, §5.18).

---

## Formula Summary — Endsem 3

The new questions of this paper add the formulas below; the formulas of the carried-over questions are already in the Formula Summary of the Endsem-1 section above.

| Quantity | Expression | Notes |
| --- | --- | --- |
| Resolved shear stress | $\tau_R = \sigma\cos\phi_1\cos\phi_2 = \sigma m$ | $\phi_1$ to plane normal, $\phi_2$ to slip direction |
| Maximum Schmid factor | $m_{\max} = 0.5$ at $\phi_1 = \phi_2 = 45^\circ$ | From $\cos^2\phi_1 + \cos^2\phi_2 \le 1$ and AM–GM |
| Single-crystal yield | $\sigma_y = \tau_{CRSS}/m$ | Minimum $2\tau_{CRSS}$ at $m = 0.5$; polycrystal $\sigma_y \approx M\tau_{CRSS}$, $M \approx 3.06$ |
| Poisson's ratio | $\nu = -\varepsilon_x/\varepsilon_z$ | $\nu \approx 0.3$ elastic, $0.5$ plastic |
| Considère criterion | $d\sigma_T/d\varepsilon_T = \sigma_T$; $\varepsilon_{T,u} = n$ | Necking is a geometric instability |
| Modulus of resilience | $U_r = \sigma_y^2/2E$ | Area up to yield; J/m³ |
| Knoop hardness | $HK = 14.2\,P/l^2$ | $l$ = long diagonal |
| Longitudinal modulus | $E_{cl} = E_mV_m + E_fV_f$ | Isostrain; upper bound; $F_f/F_m = E_fV_f/E_mV_m$ |
| Transverse modulus | $E_{ct} = \dfrac{E_mE_f}{V_mE_f + V_fE_m}$ | Isostress; lower bound |
| Zone refining | $c_0 \to c_s' \to c_s''$ at rising $T_1 < T_2$ | First solid is purer in the solvent; ten passes $\to 10^{-6}$ |

> [!note] Source images
> The Excalidraw figures in this section are the existing `MP - ` and `COMP - ` drawings. The extracted figures are the original lecture figures stored in `Material Science/images/` with their topic prefix; the zone-refining phase diagram was extracted from [[Phase_Diagrams.pdf]] and stored as `PD - Zone Refining Phase Diagram.png`.
