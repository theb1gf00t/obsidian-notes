---
title: Material Science — MO-201 End-Sem Solutions (Odd Sem 2025–26)
tags:
  - materials-science
  - MO-201
  - end-sem
---

# End-Sem Solutions — MO 201 Materials Science

Worked solutions to the End-Sem paper [[endsem1.pdf]] (IIT (BHU) Varanasi, Odd Sem 2025–26, 3 hours, 50 marks; attempt any 10 of 12 questions, all of equal marks). Every answer is built from [[notes]] (cited by section, e.g. §4.3) and the lecture PDFs behind it — [[Shockley and Frank partial dislocations_Odd_2026-27.pdf]], [[Mechanical Properties part 2_Odd_2026-27.pdf]], [[Mechanical Properties part 3_Odd_2026-27.pdf]], [[Composites_Odd_2026-27.pdf]], [[Phase_Diagrams.pdf]], [[Electrical and Electronic Properties - Part 1_Odd_2026-27.pdf]], [[Electrical and Electronic Properties - Part 2_Odd_2026-27.pdf]], [[Magnetic Properties_Odd_2026-27.pdf]] and [[Dielectric materials_Polarization_Optical properties_Odd_2026-27.pdf]] — following the conventions of [[context]]. Where a point goes beyond the slides it is marked *added depth*.

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

## Formula Summary

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
