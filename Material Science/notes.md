---
title: Material Science — MO-201 Notes
tags:
  - materials-science
  - MO-201
---

# Syllabus Map

Compiled from the lecture slides ([[Mechanical Properties part 1_Odd_2026-27.pdf]], [[Mechanical Properties part 2_Odd_2026-27.pdf]], [[Mechanical Properties part 3_Odd_2026-27.pdf]]) and the handwritten class notes in [[MO NOTES (1).pdf]] (pp. 100–131). Slides follow **Raghavan, *Materials Science and Engineering*** and **Callister, *Fundamentals of Materials Science and Engineering***.

## Post-Midsem Topics (from [[syllabus]])

| # | Topic | Status |
| --- | --- | --- |
| 1 | Mechanical Properties — I | ✅ noted below |
| 2 | Mechanical Properties — II | ✅ noted below |
| 3 | Mechanical Properties — III | ✅ noted below |
| 4 | Shockley and Frankel Partial Dislocations | — |
| 5 | Composites | — |
| 6 | Electrical and Electronic Properties — Part 1 | — |
| 7 | Electrical and Electronic Properties — Part 2 | — |
| 8 | Magnetic Properties | — |
| 9 | Dielectric Materials, Polarization, Optical Properties | — |

> [!info] How the three parts fit together
> **Part I** builds the vocabulary — deformation, stress, strain, types of loading, the catalogue of mechanical tests, and the five design properties. **Part II** explains *why* materials respond that way — the atomic model of elasticity, slip/twinning, CRSS and the Schmid factor, dislocation reactions — and then dissects the tensile test in full detail. **Part III** deals with materials that cannot be tested in simple tension (ceramics → three-point bending) and with the cheapest, most widely used test of all (hardness).

---

# Mechanical Properties

Materials in service are always subjected to forces or loads. Their response — **deformation**, and eventually **fracture or failure** — decides whether a design works. Mechanical testing exists to quantify that response so that materials can be selected, compared and designed with.

---

## 1. Mechanical Properties — I

### 1.1 Why study mechanical properties?

- Every material in service carries **loads** — a bridge girder, a turbine blade, a car panel, a silicon wafer in a holder.
- The response to load is **deformation**, and beyond a limit, **fracture/failure**.
- **Mechanical testing** converts this behaviour into numbers that can be used for *material selection, quality control and design*.

The car-accident thought experiment from the lecture makes the distinction concrete:

| Outcome of the accident | What happened mechanically |
| --- | --- |
| "Nothing at all happened" | Only **elastic** deformation — fully recovered |
| "Some scratches on the side" | Localised **plastic** deformation at the surface |
| "A dent on the side" | Large **plastic** deformation, but no separation |
| "The car broke into pieces" | **Fracture** — the material could no longer carry load |

### 1.2 Deformation: elastic, plastic, fracture

> [!important] Definitions
> **Elastic deformation** — reversible. The material returns to its original shape when the load is removed (e.g. a spring, a stretched rubber band). At the atomic level it is simply bond stretching: atoms move slightly from their equilibrium positions and spring back.
>
> **Plastic deformation** — permanent, **non-recoverable** change in size or shape. It occurs once the applied stress exceeds the elastic limit (e.g. bending a paper clip, a dent in a car door, clay being moulded).
>
> **Fracture** — after a point the material simply breaks apart; the material separates into pieces.
>
> **Failure** — the broader engineering term: the material/component can no longer perform its intended function. This includes *excessive deformation* and *wear*, not only fracture.

The central design question of this whole topic:

> *How much elastic and plastic deformation can a material accommodate before it fractures or fails?*

To answer it we need a language that is independent of the size of the specimen — hence **stress** and **strain**.

### 1.3 Types of loading

![[MP - Types of Loading.excalidraw]]

- **Tension** — forces pull the body apart along its axis; the specimen elongates and its cross-section contracts.
- **Compression** — forces push the body together; the specimen shortens and bulges.
- **Shear** — two parallel forces act on opposite faces in opposite directions; layers of material slide over one another.
- **Torsion** — a twisting moment about the long axis; this is really shear varying linearly from zero at the axis to a maximum at the surface.
- **Bending** — not a separate fundamental mode: it is *tension on one face and compression on the other*, with a neutral axis in between.

Two kinds of strain follow from these loadings:

1. **Change in dimension** — elongation, shortening (normal strain).
2. **Angular distortion** — the change of angle between two initially perpendicular lines (shear strain).

### 1.4 Concepts of stress and strain

$$\text{Stress} = \frac{\text{Load }(P)}{\text{Area of cross-section }(A_0)} \qquad \text{Strain} = \frac{\text{Displacement }(\Delta L)}{\text{Gauge length }(L_0)}$$

$$ \sigma = \frac{P}{A_0} \qquad\qquad \varepsilon = \frac{\Delta L}{L_0} $$

- **Units:** stress in $\text{N/m}^2 = \text{Pa}$ (practically MPa = $10^6$ Pa); strain is **dimensionless** (m/m).
- These "simple definitions" are *nominal/engineering* quantities — computed on the **original** area and the **original** length.

> [!warning] They are tensors, not scalars
> Stress and strain are in fact **second-rank tensors**; the elastic stiffness (and compliance) is a **fourth-rank tensor**. The scalar $\sigma = P/A_0$ is only the component along the loading axis.

The full stress state at a point needs nine components:

$$ \sigma_{ij} = \begin{bmatrix} \sigma_{11} & \sigma_{12} & \sigma_{13} \\ \sigma_{21} & \sigma_{22} & \sigma_{23} \\ \sigma_{31} & \sigma_{32} & \sigma_{33} \end{bmatrix} $$

- **Diagonal terms** $\sigma_{11}, \sigma_{22}, \sigma_{33}$ are **normal stresses** (perpendicular to the face).
- **Off-diagonal terms** are **shear stresses** (parallel to the face): $\sigma_{12} = \sigma_{21}$, $\sigma_{13} = \sigma_{31}$, $\sigma_{23} = \sigma_{32}$ — the tensor is symmetric (moment equilibrium), so only **six** components are independent.
- Likewise the fourth-rank stiffness tensor $C_{ijkl}$ has $3^4 = 81$ components, reducible to **21** independent constants for the most general crystal, and to just **2** ($E$ and $\nu$) for an isotropic material.

### 1.5 Examples of mechanical tests

| Test | What it measures | Typical use |
| --- | --- | --- |
| **Hardness** | Resistance to localised plastic deformation (dent/scratch) | Rapid QC, ranking, estimating tensile strength |
| **Tension** | Full stress–strain curve: $E$, YS, UTS, ductility, toughness | The reference test for ductile metals |
| **Compression** | Behaviour under compressive load; compressive strength | Brittle materials (concrete, ceramics), where tension is not representative |
| **Shear / torsion** | Shear modulus, shear strength, torsional stiffness | Shafts, springs, fasteners |
| **Three-point bend** | Flexural (bend) strength | Brittle materials, ceramics, glass, composites |
| **Fatigue** | Life under repeated/cyclic stress | Rotating parts, springs, aircraft structures |
| **Impact** | Energy absorbed under sudden (shock) loading; notch toughness | Quality control of steels, DBTT assessment |
| **Creep** | Time-dependent deformation at elevated temperature under constant stress | Turbine blades, boiler tubes, refractory parts |

Notes on the less obvious ones (from the class notes):

- **Fatigue:** the specimen is loaded and unloaded repeatedly, always **well below the yield stress**. It does not break for many cycles, then fails **suddenly** with no visible prior deformation. This makes fatigue the most dangerous failure mode in service.
- **Impact:** a sudden blow is delivered (pendulum hammer). The **energy absorbed** in breaking the specimen is measured — the *notch toughness*. Standard geometries are the **Izod** and **Charpy** tests. A ductile material deforms and absorbs much energy; a brittle material absorbs little and snaps.
- **Creep:** slow, continuous deformation under a **constant load** at high temperature — usually quoted as $T \gtrsim 0.4\,T_m$ (melting point in kelvin).

### 1.6 Key mechanical design properties

| Property | Meaning | Measured by |
| --- | --- | --- |
| **Stiffness** | Resistance to *elastic* deformation | Slope of the elastic line → Young's modulus $E$ |
| **Strength** | Stress at which plastic deformation or fracture begins | Yield strength (YS), Ultimate tensile strength (UTS) |
| **Hardness** | Resistance to localised plastic deformation | Indentation tests (Rockwell, Brinell, Vickers, Knoop) |
| **Ductility** | Amount of *plastic* deformation before fracture | % elongation, % reduction in area |
| **Toughness** | Energy absorbed up to fracture | Area under the stress–strain curve |

> [!question] What do "brittle" and "ductile" mean?
> **Ductile** — the material undergoes a *large amount of plastic deformation* before it fractures (mild steel, copper, aluminium, gold). It gives warning: it bends, stretches, necks.
> **Brittle** — the material fractures *suddenly, with little or no plastic deformation* (cast iron, glass, ceramics, and steels at low temperature). There is no warning.
> The same material can be ductile or brittle depending on **temperature, strain rate and the presence of a notch** — see the Yoffee diagram in §2.7.

### 1.7 Mechanical testing ↔ deformation mechanisms

Mechanical tests are only the *symptom*; the *cause* is what happens to atoms and dislocations. The lecture maps the bridge explicitly:

- **Plastic deformation mechanisms:** slip, twinning, dislocation climb, grain-boundary sliding, …
- **Schmid factor / CRSS** — which slip system operates, and at what stress.
- **Glissile vs sessile dislocations** — mobile dislocations vs locked ones.
- **Theoretical shear strength of a perfect crystal** — why real crystals are $10^3$–$10^4$ times weaker.
- **Peierls stress / Peierls–Nabarro force** — the lattice friction that a dislocation must overcome to move.
- **Creep test** — time-dependent deformation at elevated temperature under constant stress.
- **Fatigue test** — cyclic loading below yield.

All of these are developed in §2.

### 1.8 Tensile test: first look

The tensile test pulls a specimen along its axis at a constant rate and records **load** and **elongation**, which are converted to **stress** and **strain**.

- A **ductile** material shows a long plastic region, work hardening, necking and a cup-and-cone (or shear) fracture.
- A **brittle** material shows an almost perfectly linear elastic line up to sudden fracture, with negligible plastic strain.

The same test on the *same* material can produce either curve depending on temperature — this is the subject of §2.7.

> [!tip] Exam pointer
> Part I is mostly *vocabulary*. Be able to state, in one line each: elastic vs plastic vs fracture vs failure; the four loading modes; the difference between engineering and true stress/strain; and the property ↔ test mapping in §1.6.

---

## 2. Mechanical Properties — II

### 2.1 Atomic model of elastic behaviour

Elastic deformation is nothing but a small change in the **interatomic spacing**. The interaction between two atoms is described by a potential energy $U(r)$ with a minimum at the equilibrium separation $r_0$:

$$ F(r) = \frac{dU}{dr}, \qquad \left.\frac{dU}{dr}\right|_{r_0} = 0 $$

- At $r = r_0$ the net force is **zero** — the equilibrium state.
- Stretching the bond to $r'>r_0$ or compressing it to $r''<r_0$ requires an external force $F'$ or $F''$, obtained from the slope of the $U$–$r$ (or $F$–$r$) curve.
- The **stiffness** is the curvature of the well at the minimum:

$$ E \propto \left.\frac{dF}{dr}\right|_{r_0} = \left.\frac{d^2U}{dr^2}\right|_{r_0} $$

Hence a **deep, steep, narrow potential well → high modulus** (covalent ceramics such as diamond, SiC), while a **shallow, wide well → low modulus** (soft metals, polymers). This is also why the force–distance curve is asymmetric: it is much harder to compress a bond than to stretch it (repulsion rises steeply), which is the origin of **thermal expansion** and of the fact that elastic behaviour is only linear for *small* displacements.

> [!note] Why Hooke's law works
> Near $r_0$ the $F$–$r$ curve is essentially a straight line, so force $\propto$ displacement → **linear elasticity**. At large strains the curve bends and Hooke's law fails. Anelasticity and nonlinear elasticity are the corrections.

#### Theoretical shear strength of a perfect crystal

If a perfect crystal were sheared, the shear stress would vary roughly sinusoidally with displacement, giving

$$ \tau_{\text{theoretical}} \approx \frac{G}{2\pi} \approx \frac{G}{6}\ \text{to}\ \frac{G}{30} $$

where $G$ is the shear modulus. Measured yield stresses are typically $10^{-3}$–$10^{-4}\,G$ — three to four orders of magnitude lower. **This discrepancy is the classic proof that plastic deformation occurs by the motion of dislocations, not by the simultaneous sliding of whole planes.**

The stress needed to move a dislocation through the lattice is the **Peierls–Nabarro stress**:

$$ \tau_{PN} = \frac{2G}{1-\nu}\,\exp\!\left(-\frac{2\pi w}{b}\right), \qquad w = \frac{d}{1-\nu} $$

where $b$ is the Burgers vector, $d$ the interplanar spacing and $w$ the width of the dislocation core.

- **Wide core** (metals — metallic bonding, non-directional) → exponential term small → **low Peierls stress** → easy glide, ductile.
- **Narrow core** (covalent/ionic ceramics) → **high Peierls stress** → hard, brittle.

### 2.2 Deformation by slip and twinning

![[MP - Slip and Twinning.excalidraw]]

| | **Slip** | **Twinning** |
| --- | --- | --- |
| Displacement | Whole block above the plane shifts by a **discrete, integral number of lattice spacings** | Each successive plane shifts by a **fraction** of a lattice spacing, increasing with distance from the twin plane |
| Result at surface | A visible **step** (slip line/steps) | A reoriented region; surface tilts |
| Lattice orientation | **Unchanged** after slip | **Changed** — the twinned region is a mirror image of the parent |
| When it dominates | Normal case for metals with many slip systems (FCC, BCC) | When slip is difficult: HCP metals, low temperature, high strain rate, shock loading |
| Magnitude of strain | Large (slip can repeat indefinitely) | Small (a twin can accommodate only a limited strain) |

Both are **shear** processes: the resolved shear stress on the plane, in the direction, does the work. Twinning is also important because the reoriented twin lamellae can *re-activate* otherwise hard slip systems, and twin boundaries act as barriers to dislocation motion.

### 2.3 Slip systems

A **slip system** = one **slip plane** (the close-packed plane — highest atomic density, widest interplanar spacing, hence lowest shear resistance) + one **slip direction** (the close-packed direction within that plane) + the Burgers vector of the dislocation that glides.

| Crystal | Slip plane(s) | Slip direction(s) | Independent systems | Remarks |
| --- | --- | --- | --- | --- |
| **FCC** | $\{111\}$ (4 octahedral planes) | $\langle 110\rangle$ | $4\times3 = 12$ | Most ductile; e.g. Cu, Al, Ni, austenitic stainless steel |
| **BCC** | $\{110\}$ **more common**; $\{112\}$, $\{123\}$ **less common** | $\langle 111\rangle$ | $6\times2 = 12$ (from $\{110\}$) | Slip is *not* on the closest-packed plane; temperature-sensitive (low-T brittleness) |
| **HCP** | Basal $(0001)$ **more common**; prismatic and pyramidal planes **less common** | Close-packed $\langle 11\bar{2}0\rangle$ | 3 from basal ($1\times3$) | Only 3 basal systems → limited ductility; Ti, Mg, Zn, Cd |
| **NaCl (ionic)** | $\{110\}$ | $\langle 110\rangle$ | 6 | Slip on $\{110\}$ avoids bringing like-charged ions together |

The **number of independent slip systems** controls ductility (von Mises criterion: at least 5 independent systems are needed for an arbitrary shape change of a polycrystal). This is why FCC metals are ductile and HCP metals are not.

### 2.4 CRSS and the Schmid factor

![[MP - Schmid Factor Geometry.excalidraw]]

A tensile stress $\sigma$ applied along an arbitrary axis does **not** act as a shear stress on the slip plane. Only the component resolved onto the slip plane *and* along the slip direction drives glide.

**Derivation.** Let the tensile axis make an angle $\phi_1$ with the **slip-plane normal** $N$ and $\phi_2$ with the **slip direction** $D$.

1. The area of the slip plane, for a specimen of cross-section $A$, is enlarged by the obliquity: $A_s = A/\cos\phi_1$.
2. The component of the applied load $P$ along the slip direction is $P\cos\phi_2$.
3. Therefore the **resolved shear stress** (RSS) is

$$ \tau_R = \frac{P\cos\phi_2}{A/\cos\phi_1} = \frac{P}{A}\cos\phi_1\cos\phi_2 = \sigma\,\cos\phi_1\cos\phi_2 $$

$$ \boxed{\ \tau_R = \sigma\, m, \qquad m = \cos\phi_1\cos\phi_2\ } $$

$m$ is the **Schmid factor**. Its maximum value is $m_{\max} = 0.5$ (when $\phi_1 = \phi_2 = 45^\circ$); it is **zero** when the slip plane is perpendicular to the stress axis ($\phi_1 = 90^\circ$) or when the slip direction is perpendicular to the axis ($\phi_2 = 90^\circ$) — in those orientations the crystal cannot glide at all on that system.

**Critical resolved shear stress (CRSS).** Slip begins when $\tau_R$ on a given system reaches a critical value, $\tau_{CRSS}$, which is a **material property** (to first order independent of orientation, though it depends on temperature, impurities and dislocation density):

$$ \tau_R = \tau_{CRSS} \quad\Longrightarrow\quad \sigma_y = \frac{\tau_{CRSS}}{m} $$

Because different systems in the same crystal have different $m$ for the same applied $\sigma$, **the system with the largest Schmid factor yields first** as the load is raised from zero. Consequently:

- The **yield stress of a single crystal depends on the orientation of the stress axis** — it is minimum when $m = 0.5$ and theoretically infinite when $m = 0$.
- In a **polycrystal** grains are randomly oriented (and constrained by their neighbours), so an average factor — the **Taylor factor** $M \approx 3.06$ for FCC — relates macroscopic yield to CRSS: $\sigma_y \approx M\,\tau_{CRSS}$. This is one reason polycrystals are stronger than single crystals.

> [!tip] Geometric relations worth remembering
> For an axis lying in the plane containing $N$ and $D$: $\phi_1 + \phi_2 = 90^\circ$, so $m = \tfrac12\sin 2\phi_1$, maximum at $45^\circ$. Also $m = 0$ for both the "end-on" and "side-on" orientations — two of the classic single-crystal "hard orientations".

### 2.5 Dislocation reactions and sessile (Lomer) locks

![[MP - Dislocation Reaction Sessile Lock.excalidraw]]

Dislocations gliding on **non-parallel** slip planes meet along the line of intersection of those planes and can **react** to form a third dislocation. Whether the reaction happens is decided by the **strain energy**, which for a dislocation is proportional to $b^2$ per unit length:

$$ \Delta E \propto b_3^2 - (b_1^2 + b_2^2) < 0 \quad\text{(reaction is favourable)} $$

**Example (FCC).** Take $b_1 = \tfrac{a}{2}[101]$ gliding on $(1\bar{1}1)$ and $b_2 = \tfrac{a}{2}[0\,1\,\bar{1}]$ gliding on $(11\bar{1})$. They meet along the intersection line of the two planes and react:

$$ \frac{a}{2}[101] + \frac{a}{2}[0\,1\,\bar{1}] \longrightarrow \frac{a}{2}[110] $$

$$ b_1^2 + b_2^2 = \frac{a^2}{2} + \frac{a^2}{2} = a^2 \qquad\longrightarrow\qquad b_3^2 = \frac{a^2}{2} $$

The strain energy therefore **decreases by 50 %**, so the reaction is energetically favourable. The product $\tfrac{a}{2}[110]$ lies **along the line of intersection**, i.e. in a $\{100\}$-type plane, which is *not* a close-packed slip plane of the FCC lattice. It is therefore **immobile — sessile** (a *Lomer lock*).

**Consequence.** Dislocations gliding on the two planes **pile up** behind the lock. The pile-up produces a long-range back stress that opposes the applied stress, so a higher applied stress is needed for further deformation — this is one of the fundamental mechanisms of **work hardening** (§2.17).

### 2.6 The tensile test: specimen, machine, curve

![[MP - Engineering Stress Strain Curve.excalidraw]]

**Specimen** (standard proportions): a cylindrical or flat bar with a **reduced section** — a central **gauge length** (typically 50 mm / 2 in.) and a smaller diameter (e.g. 12.8 mm / 0.505 in.), with fillets of radius into the enlarged grip ends. The reduced section ensures that yielding and fracture occur away from the grips, in the region where strain is measured.

**Machine — Universal Testing Machine (UTM):** a **load cell** measures the applied load, an **extensometer** clipped to the gauge length measures elongation, and a **moving crosshead** applies the displacement at a controlled rate. Output: load–elongation → stress–strain.

**The engineering stress–strain curve** has four regimes:

1. **Elastic (linear) region** — slope $= E$; unloading returns the specimen to its original length.
2. **Yielding** — the onset of plastic deformation at the yield strength $\sigma_y$ (in some low-carbon steels, an upper and a lower yield point appear by the yield-point phenomenon).
3. **Strain hardening** — stress rises with strain up to the **UTS**, the maximum of the curve.
4. **Necking and fracture** — after the UTS the deformation localises in a neck; the engineering stress falls (because it is computed on the original area) until fracture.

### 2.7 Brittle and ductile behaviour: temperature, and the Yoffee diagram

The same material gives quite different curves at different temperatures. For **iron**:

| Temperature | Behaviour |
| --- | --- |
| $-200\ ^\circ\text{C}$ | Very high yield stress, almost no plasticity — **brittle** |
| $-100\ ^\circ\text{C}$ | Some ductility, but much less than at room temperature — **transition** |
| $25\ ^\circ\text{C}$ (room temperature) | Long plastic region, pronounced necking — **ductile** |

![[MP - Yoffee Diagram DBTT.excalidraw]]

**Yoffee diagram.** Plot, against temperature, (i) the **yield stress** — which *falls* as temperature rises (thermal activation helps dislocations overcome obstacles), and (ii) the **fracture stress** — which *rises* as temperature rises (yielding blunts cracks and relieves stress concentrations). The two curves cross at the **Ductile–Brittle Transition Temperature (DBTT)**:

- Below DBTT: fracture stress $<$ yield stress → the material **fractures before it yields → brittle**.
- Above DBTT: yield stress $<$ fracture stress → it **yields before it fractures → ductile**.

The **notch toughness** measured in a Charpy/Izod test plotted against temperature gives the same S-shaped transition curve, with a steep drop at the DBTT.

> [!warning] What shifts the DBTT upwards (makes a material brittle)
> - **Lower service temperature** — the most obvious factor.
> - **Higher strain rate / impact loading** — less time for thermal activation.
> - **A sharp notch or crack** — triaxial stress state suppresses shear yielding.
> - **Coarse grain size, impurities (S, P, Sn, Sb), high carbon** in steels.
> The Titanic's hull steel is the standard example: a low-temperature, high-strain-rate, notched impact.

**Materials for low-temperature service.** BCC carbon/alloy steels lose toughness quickly (hence the graded 3.5 % Ni, 5 % Ni, 9 % Ni steels for cryogenic tanks). **FCC** alloys — austenitic stainless steels (304, 310, 304 ELC), aluminium alloys (5083, 2219), nickel alloys (Inconel, Monel) and titanium alloys — retain toughness down to liquid-helium temperature because FCC has 12 slip systems and no DBTT of this kind.

### 2.8 Properties obtained from the tensile test

1. **Elastic modulus** and **resilience**
2. **Yield stress** (YS)
3. **Tensile strength** (TS / UTS)
4. **Elongation to failure** / **reduction in area** at fracture
5. **Toughness**

### 2.9 Anelasticity and viscoelasticity

- In real materials, part of the elastic strain is **time-dependent**: deformation continues slowly *after* the stress is applied, and on unloading some finite time is needed for complete recovery. This is **anelasticity**.
- Its origin is time-dependent microscopic/atomistic processes accompanying the deformation (e.g. stress-induced ordering of solute atoms, grain-boundary relaxation).
- In **metals** the anelastic component is small and usually neglected. In **polymers** it is large; the behaviour is then called **viscoelastic** (rubber-like).
- Idealised responses: **elastic** (instant strain, instant recovery), **viscous** (strain grows linearly with time under constant load, permanent), and **viscoelastic** (intermediate — retarded elastic strain plus permanent flow).

### 2.10 Poisson's ratio

When a tensile stress is applied along $z$, the specimen elongates in $z$ ($\varepsilon_z>0$) and **contracts laterally** in $x$ and $y$ ($\varepsilon_x,\varepsilon_y<0$):

$$ \nu = -\frac{\varepsilon_x}{\varepsilon_z} = -\frac{\varepsilon_y}{\varepsilon_z} \qquad (\varepsilon_x = \varepsilon_y \text{ for an isotropic material}) $$

- $\nu \approx 0.25$–$0.35$ for metals and alloys
- $\nu \approx 0.33$–$0.46$ for polymers
- $\nu = 0.5$ for a perfectly incompressible material (no volume change — rubber, and the theoretical limit); $\nu \approx 0$ for cork
- For an **isotropic** material the elastic constants are linked:

$$ E = 2G(1+\nu) $$

so a high Poisson's ratio (or a low shear modulus) means a low modulus relative to $G$. Structural materials with high $E$ usually have low $\nu$; polymers have low $E$ and high $\nu$.

### 2.11 Yield stress and tensile strength

- **Yield strength** is the stress at which plastic deformation begins. Because the elastic-to-plastic transition is gradual for most metals, it is defined by the **0.2 % offset** construction: draw a line parallel to the elastic portion, starting at $\varepsilon = 0.002$; its intersection with the curve is $\sigma_y$.
- **Tensile strength (UTS)** is the maximum stress on the engineering curve; it marks the **onset of necking** and the end of uniform deformation.
- Above the UTS, deformation is **localised** — the curve descends, but this does not mean the material is softening (see true stress, §2.16).

### 2.12 Resilience and toughness

| | **Resilience** | **Toughness** |
| --- | --- | --- |
| Area | Under the curve **up to yield** | Under the **whole curve to fracture** |
| Meaning | Energy absorbed per unit volume in the elastic range; ability to store energy and spring back | Energy absorbed per unit volume before fracture; resistance to fracture |
| Formula | $U_r = \int_0^{\varepsilon_y}\sigma\,d\varepsilon = \frac12\sigma_y\varepsilon_y = \dfrac{\sigma_y^2}{2E}$ | $U_t = \int_0^{\varepsilon_f}\sigma\,d\varepsilon$ (no simple closed form) |
| Units | J/m³ | J/m³ |
| Favoured by | **High yield strength, low modulus** | **High strength *and* high ductility** |

A tough material needs both: a ceramic may have huge strength but negligible ductility → *low* toughness. This is why "toughness" and "strength" are not the same design property.

### 2.13 Tensile curves for polymers

Three characteristic shapes:

- **Brittle** — linear elastic to a sudden break, very small strain (PMMA, PS at room temperature).
- **Plastic** — yield, then cold drawing with a long plateau, then strain hardening and fracture (many thermoplastics).
- **Elastomeric** — highly elastic: enormous recoverable strain (several hundred %), low modulus, no permanent set (rubbers/vulcanised elastomers).

### 2.14 Measures of strength and ductility

$$ \sigma = \frac{F}{A_0} \qquad\qquad \varepsilon = \frac{l_i - l_0}{l_0} $$

$$ \%EL = \frac{l_f - l_0}{l_0}\times 100 \qquad\qquad \%RA = \frac{A_0 - A_f}{A_0}\times 100 $$

- **Yield strength and tensile strength** are measures of **strength**.
- **Fracture strength is not used as a design criterion** — it is highly scattered, depends on flaws, and a design that allows stresses to approach fracture is already unsafe. Design is based on yield (with a factor of safety).
- **% elongation to failure** and **% reduction in area** are measures of **ductility**. Reduction in area is often the more sensitive indicator, because it is measured at the neck where deformation is concentrated.

### 2.15 Necking

After the UTS the cross-section decreases locally — a **neck** forms, and further deformation is confined to it. Because engineering stress uses $A_0$, the curve falls even though the *true* stress in the neck continues to rise. In **semicrystalline polymers** the neck is *stable*: it draws down and then propagates along the gauge length (cold drawing), giving a long plateau rather than a fall.

### 2.16 True stress and true strain

![[MP - True vs Engineering Stress Strain.excalidraw]]

Engineering quantities are referred to the *original* area and length. **True** quantities are referred to the *instantaneous* values:

$$ \sigma_T = \frac{F}{A_i} \qquad\qquad \varepsilon_T = \int_{l_0}^{l_i}\frac{dl}{l} = \ln\frac{l_i}{l_0} $$

Assuming **constancy of volume** during plastic deformation ($A_0 l_0 = A_i l_i$):

$$ \sigma_T = \sigma(1+\varepsilon) \qquad\qquad \varepsilon_T = \ln(1+\varepsilon) $$

- The volume-constancy assumption is valid **only up to the onset of necking** — beyond that the deformation is no longer uniform.
- True strain in compression is negative, and $\varepsilon_T$ is additive whereas engineering strain is not: two successive strains of 0.5 give $\varepsilon_T = \ln 1.5 + \ln 1.5 = \ln 2.25$, not 1.0.
- Also useful: $\varepsilon_T = \ln(A_0/A_i)$.
- **After necking the two curves diverge completely**: the engineering curve falls while the true curve keeps rising. The fall of the engineering curve is a *geometric* artefact, not softening.

### 2.17 Work hardening / strain hardening

In the plastic region the stress–strain curve has a **positive slope**: the stress required for further deformation increases with strain. This is **work hardening (strain hardening)**.

**Microscopic origin:** as deformation proceeds, dislocations multiply and interact —

- dislocation–dislocation interactions and **junctions**;
- **sessile locks** formed by reactions (§2.5);
- accumulation at **grain boundaries** and **twin boundaries**;
- hence a higher stress is continuously needed for further glide. The dislocation density rises from $\sim10^{10}$–$10^{12}\ \text{m}^{-2}$ (annealed) to $\sim10^{15}$–$10^{16}\ \text{m}^{-2}$ (heavily deformed).

**Idealised stress–strain models** (Dieter):

| Model | Description |
| --- | --- |
| **Rigid, ideal plastic** | No elastic region at all; the material deforms plastically at a constant stress once the yield stress is reached |
| **Ideal plastic with elastic region** | Linear elastic up to yield, then perfectly flat plastic flow at constant stress |
| **Piecewise linear (strain-hardening)** | Linear elastic up to yield, then a linear rising plastic branch — the simplest strain-hardening idealisation |

Work hardening is exploited industrially (cold rolling, drawing, forging) and is removed by **annealing** (recovery + recrystallisation).

### 2.18 The plastic flow curve and the Hollomon equation

$$ \sigma_T = K\,\varepsilon_T^{\,n} $$

- $K$ = **strength coefficient** (stress at $\varepsilon_T = 1$), MPa.
- $n$ = **strain-hardening exponent**, dimensionless, typically $0.1$–$0.5$.
- On a **log–log plot** of $\sigma_T$ vs $\varepsilon_T$ this is a straight line: slope $= n$, intercept $= \log K$.
- **Valid from the onset of plastic deformation to the onset of necking.** Beyond necking the stress state is no longer uniaxial.

**The "corrected" curve.** Inside the neck the stress state is **triaxial** (lateral stresses exist in addition to the axial one), so the axial stress computed as $F/A_{\text{neck}}$ is an *overestimate*. Correcting for this shifts the true curve *downwards* — the "corrected" curve lies slightly below the raw true curve after necking.

| Material | $n$ | $K$ (MPa) | $K$ (psi) |
| --- | --- | --- | --- |
| Low-carbon steel (annealed) | 0.21 | 600 | 87,000 |
| 4340 steel alloy (tempered at 315 °C) | 0.12 | 2650 | 385,000 |
| 304 stainless steel (annealed) | 0.44 | 1400 | 205,000 |
| Copper (annealed) | 0.44 | 530 | 76,500 |
| Naval brass (annealed) | 0.21 | 585 | 85,000 |
| 2024 aluminium alloy (T3) | 0.17 | 780 | 113,000 |
| AZ-31B magnesium alloy (annealed) | 0.16 | 450 | 66,000 |

A **high $n$** (0.44, annealed Cu and 304 SS) means a material that work-hardens strongly and therefore stretches a lot before necking — good formability. A **low $n$** (0.12, tempered 4340) means little uniform elongation.

### 2.19 Elastic recovery after plastic deformation

- When the load is released during a test, the specimen unloads **parallel to the elastic line**; the recovered strain is $\sigma/E$.
- This **elastic strain recovery** is why a formed sheet springs back after the tool is removed — the practical reason for over-bending in press forming.
- On **reloading**, the material yields at approximately the *previous* maximum stress — direct evidence of work hardening.
- An elastic recovery also occurs at fracture, so the measured elongation contains a small elastic contribution.

> [!tip] Exam pointer — Part II
> The most examined items are: the Schmid factor derivation and $\sigma_y = \tau_{CRSS}/m$ with $m_{\max}=0.5$; the true vs engineering conversion $\sigma_T=\sigma(1+\varepsilon)$, $\varepsilon_T=\ln(1+\varepsilon)$; $U_r = \sigma_y^2/2E$; the Hollomon equation and $n$; and the $b^2$ energy criterion for a dislocation reaction.

---

## 3. Mechanical Properties — III

### 3.1 Testing brittle materials: the three-point bend test

![[MP - Three Point Bending.excalidraw]]

**Why not a tensile test?** Ceramics are hard and brittle: they cannot easily be machined into a waisted tensile specimen, gripping introduces stress concentrations that cause premature fracture, and the tensile strength is only about **one-tenth** of the compressive strength. In bending, only a small specimen is needed and no gripping is involved.

**Setup.** A rectangular (or circular) bar rests on **two support pins** a distance $L$ apart and is loaded at the **mid-span** — three contact points. The **top surface is in compression** and the **bottom surface in tension**. Because ceramics are far weaker in tension, **fracture always initiates on the tensile (bottom) face**; the test therefore measures a *tensile* strength, but in a convenient geometry.

Bending stress from simple beam theory:

$$ \sigma = \frac{Mc}{I} $$

with $M_{\max} = \dfrac{F L}{4}$ at mid-span. Hence, for the two standard cross-sections:

$$ \sigma_{fs} = \frac{3F_f L}{2bd^2} \quad\text{(rectangular, width } b,\ \text{depth } d) \qquad\qquad \sigma_{fs} = \frac{F_f L}{\pi r^3} \quad\text{(circular, radius } r) $$

where $F_f$ is the fracture load.

**Names.** The stress at fracture in this test is variously called the **flexural strength**, **modulus of rupture**, **fracture strength** or **bend strength** — all the same quantity.

### 3.2 Stress–strain behaviour of ceramics and the influence of porosity

- The stress–strain curve of a ceramic is **linear elastic up to fracture** — there is essentially **no plastic deformation**. The fracture strain is tiny ($\sim10^{-4}$–$10^{-3}$), so $E$ is large and the area under the curve (toughness) is small.
- **Porosity** degrades both stiffness and strength, because pores act as stress concentrators and reduce the load-bearing cross-section:

$$ E = E_0\left(1 - 1.9P + 0.9P^2\right) \qquad\qquad \sigma_{fs} = \sigma_0 \exp(-nP) $$

where $P$ is the **volume fraction porosity** and $E_0,\sigma_0$ are the values at zero porosity. The exponential drop in strength ($n\approx4$–$7$) is far steeper than the drop in modulus — a few percent porosity can halve the strength. This is why ceramic processing is obsessed with densification (sintering, hot pressing, HIPing).

### 3.3 Hardness: definition and advantages

![[MP - Hardness Indenters.excalidraw]]

> [!important] Definition
> **Hardness** is a measure of a material's **resistance to localised plastic deformation** — a small dent or a scratch. A small **indenter** is forced into the surface under a specified **load and loading rate**; the **depth or size of the indent** is measured. The softer the material, the larger and deeper the indentation.

> [!warning] Hardness ⇏ toughness
> Higher hardness usually comes with **brittleness**. A hard surface resists scratching but a crack can run through it with little energy — this is the hardness–toughness trade-off behind case-hardening, tool steels and ceramic coatings.

**Advantages of hardness testing:**

- **Simple and inexpensive** — typically no special specimen is needed and the apparatus is relatively cheap.
- **Essentially non-destructive** — the specimen is neither fractured nor excessively deformed; a small indentation is the only damage.
- **Other properties can be estimated** from hardness, notably tensile strength. For steels:

$$ \text{TS (MPa)} \approx 3.45 \times \text{HB} $$

This empirical relation (and its counterparts for other alloys) is used for rapid QC where a full tensile test is impractical.

### 3.4 Hardness-testing techniques — summary

| Test | Indenter | Load | Hardness number |
| --- | --- | --- | --- |
| **Brinell** | 10 mm sphere of steel or tungsten carbide | 500–3000 kg | $HB = \dfrac{2P}{\pi D\left[D-\sqrt{D^2-d^2}\right]}$ |
| **Vickers** (microindentation) | Diamond pyramid, 136° | 1–1000 g | $HV = 1.854\,P/d^2$ |
| **Knoop** (microindentation) | Diamond pyramid, elongated ($l/b = 7.11$) | 1–1000 g | $HK = 14.2\,P/l^2$ |
| **Rockwell / superficial Rockwell** | Diamond cone (120°) or steel/WC ball ($\tfrac{1}{16}$ in., $\tfrac{1}{8}$ in., $\tfrac{1}{4}$ in.) | 15, 30, 45, 60, 100, 150 kg | From depth of penetration $h$ |

($P$ in kg; $D, d, l$ in mm.)

### 3.5 The Rockwell test

- The hardness number is determined by the **difference in depth of penetration** produced by an **initial minor load** (10 kg — improves accuracy by seating the indenter and removing surface roughness effects) followed by a **larger major load**.
- The depth is read directly on a dial/gauge; no microscope measurement is needed — hence the speed and popularity of the test.
- **Rockwell scales** (letter = indenter + load combination). Standard scales:

| Scale | Indenter | Major load (kg) | Typical applications |
| --- | --- | --- | --- |
| **A** | Diamond spheroconical | 60 | Cemented carbides, thin steel, shallow case-hardened steel |
| **B** | 1.588 mm ($\tfrac{1}{16}$ in.) ball | 100 | Copper alloys, soft steels, aluminium alloys, malleable iron |
| **C** | Diamond | 150 | Steels, hard cast irons, pearlitic malleable iron, titanium, deep case-hardened steel (harder than HRB 100) |
| **D** | Diamond | 100 | Thin steel, medium case-hardened steel, pearlitic malleable iron |
| **E** | 3.175 mm ($\tfrac18$ in.) ball | 100 | Cast iron, aluminium and magnesium alloys, bearing metals |
| **F** | 1.588 mm ball | 60 | Annealed copper alloys, thin soft sheet metals |
| **G** | 1.588 mm ball | 150 | Phosphor bronze, beryllium copper, malleable irons (upper limit HRG 92 to avoid flattening the ball) |
| **H** | 3.175 mm ball | 60 | Aluminium, zinc, lead |
| **K** | 3.175 mm ball | 150 | Bearing metals and other very soft or thin materials |

**Superficial Rockwell** scales use lower loads for thin specimens: **15N, 30N, 45N** (diamond) and **15T, 30T, 45T** ($\tfrac{1}{16}$ in. ball).

**Formulae** (with $h$ = permanent depth of penetration in mm):

$$ \text{HR} = 100 - \frac{h}{0.002} \ \text{(diamond spheroconical)} \qquad\qquad \text{HR} = 130 - \frac{h}{0.002}\ \text{(ball)} $$

Each $0.002$ mm of depth equals one hardness point. For each scale, values are meaningful only up to about **130**, and readings are unreliable **below 20 and above 100** (the scale becomes too compressed).

**Precautions (also apply to Brinell):**

- Inaccuracies arise if the specimen is **too thin**, if an indentation is made **too near an edge**, or if **two indentations are too close** to each other.
- Specimen thickness should be at least **10 × the indentation depth**; allow at least **three indentation diameters** between the centre of one indentation and the specimen edge or the centre of the next.
- **Stacking specimens** one on top of another is **not** recommended.
- The surface must be **smooth and flat**, and perpendicular to the indenter axis.

### 3.6 The Brinell test

- A hardened steel or **tungsten carbide ball of 10 mm diameter** is pressed into the surface.
- Standard loads: **500–3000 kg in 500 kg increments**; harder materials need larger loads (to keep the indent size in the measurable range).
- The load is held constant for a specified time, typically **10–30 s**.
- The **diameter of the circular indent** $d$ is measured with a **microscope/measuring scale**, and

$$ HB = \frac{2P}{\pi D\left[D - \sqrt{D^2 - d^2}\right]} $$

- $HB$ therefore depends on **both** the load and the indent diameter — this is why the load must always be quoted with the number.
- There is **only one Brinell scale** (in contrast to Rockwell's many letter scales).
- Specimen thickness, edge distance, spacing and surface-finish requirements are the same as for Rockwell. The indentation is large, so Brinell averages over a coarse microstructure (useful for cast irons and inhomogeneous alloys) but is unsuitable for thin specimens.

### 3.7 The Knoop and Vickers microindentation tests

- A **very small diamond indenter of pyramidal geometry** is forced into the surface. **Vickers**: a square-based pyramid with a **136°** included angle. **Knoop**: an elongated pyramid with diagonal ratio $l/b = 7.11$ and face angles chosen so that the long diagonal is about seven times the short one.
- Applied loads are much smaller than for Rockwell/Brinell — **1 to 1000 g** (hence *microindentation*).
- The impression is observed under a **microscope** and its diagonals measured; the measurement is converted into a hardness number.
- Because the indent is tiny, **careful surface preparation (grinding and polishing)** is essential for a well-defined, measurable impression — and the test can be used to measure the hardness of individual phases, thin foils, coatings and case depths.

$$ HV = 1.854\,\frac{P}{d^2} \qquad\qquad HK = 14.2\,\frac{P}{l^2} $$

where $d$ is the mean Vickers diagonal and $l$ the long Knoop diagonal.

### 3.8 Hardness conversion

- **Hardness is not a well-defined physical property** — it is a response to a particular indenter geometry, load and material behaviour. Because the experimental conditions differ so much between techniques, **no comprehensive conversion scheme exists**.
- Conversion tables/charts have been determined **empirically** and depend on the **material type and characteristics**.
- The most reliable conversion data exist for **steels** (that is why "TS = 3.45 HB" works well for steels and poorly for everything else).
- A useful anchor: the **Mohs** scratch scale (talc = 1 … diamond = 10) is a completely different, ordinal hardness scale and cannot be converted to HB/HV/HK by formula.

### 3.9 Hardness of ceramics

- **Spherical indenters** (Rockwell, Brinell) are **not used** for ceramics — the concentrated load produces severe **cracking** around the indent instead of a clean impression.
- **Vickers** is the workhorse for ceramics; for **very brittle** ceramics the **Knoop** test is often preferred because the elongated indent is less prone to cracking.
- For both, the measured hardness **decreases with increasing load (indentation size effect)** and then reaches a **constant plateau** that is independent of load. The plateau value varies from ceramic to ceramic.
- An **ideal** test uses a load large enough to be on the plateau, but not so large as to introduce excessive cracking.

### 3.10 Tear strength and hardness of polymers

- **Tear strength** — the ability to resist tearing — is important for **thin films** (packaging). It is defined as the **energy required to tear apart a cut specimen of standard geometry**; the crack must be propagated through the specimen, so tear strength depends on both the **tensile strength** and the **thickness** of the film. Magnitudes of tensile and tear strength are related (both reflect chain alignment and intermolecular bonding).
- Polymers are much softer than metals and ceramics, so **Rockwell** tests (with ball indenters and low loads) are frequently used; other techniques are the **Durometer** and **Barcol** tests, both designed for soft materials.

> [!tip] Exam pointer — Part III
> Expect: why three-point bending is used for ceramics and the two $\sigma_{fs}$ formulae; the porosity equations $E = E_0(1-1.9P+0.9P^2)$ and $\sigma_{fs}=\sigma_0 e^{-nP}$; the definition of hardness and why it is not a fundamental property; the Rockwell depth formulae ($100 - h/0.002$ vs $130 - h/0.002$); and the Brinell/Vickers/Knoop expressions with their load ranges.

---

## Formula Summary

| Quantity | Expression | Notes |
| --- | --- | --- |
| Engineering stress / strain | $\sigma = P/A_0$, $\varepsilon = \Delta L/L_0$ | Referred to original dimensions |
| True stress / strain | $\sigma_T = \sigma(1+\varepsilon)$, $\varepsilon_T = \ln(1+\varepsilon)$ | Valid to onset of necking only |
| Poisson's ratio | $\nu = -\varepsilon_x/\varepsilon_z$, $E = 2G(1+\nu)$ | Isotropic materials |
| Modulus of resilience | $U_r = \sigma_y^2/(2E)$ | Area under elastic region |
| Hollomon (plastic flow) | $\sigma_T = K\varepsilon_T^{\,n}$ | Up to onset of necking |
| Resolved shear stress | $\tau_R = \sigma\cos\phi_1\cos\phi_2$ | Schmid factor $m = \cos\phi_1\cos\phi_2 \le 0.5$ |
| Yield of a crystal | $\sigma_y = \tau_{CRSS}/m$ | Slip starts on the system with maximum $m$ |
| Dislocation reaction | favourable if $b_1^2 + b_2^2 > b_3^2$ | Energy $\propto b^2$ |
| Theoretical shear strength | $\tau \approx G/2\pi$ | Observed strength is $10^{-3}$–$10^{-4}G$ |
| Peierls–Nabarro stress | $\tau_{PN} = \dfrac{2G}{1-\nu}e^{-2\pi w/b}$, $w = \dfrac{d}{1-\nu}$ | Lattice friction on a dislocation |
| Flexural strength (rect.) | $\sigma_{fs} = 3F_fL/(2bd^2)$ | Three-point bending |
| Flexural strength (circ.) | $\sigma_{fs} = F_fL/(\pi r^3)$ | Three-point bending |
| Porosity — modulus | $E = E_0(1-1.9P+0.9P^2)$ | $P$ = volume fraction porosity |
| Porosity — strength | $\sigma_{fs} = \sigma_0 e^{-nP}$ | $n \approx 4$–$7$ |
| Brinell hardness | $HB = \dfrac{2P}{\pi D[D-\sqrt{D^2-d^2}]}$ | $P$ in kg, $D,d$ in mm |
| Vickers hardness | $HV = 1.854P/d^2$ | 136° diamond pyramid |
| Knoop hardness | $HK = 14.2P/l^2$ | $l/b = 7.11$ |
| Rockwell number | $HR = 100 - h/0.002$ (diamond); $130 - h/0.002$ (ball) | $h$ in mm |
| Strength from hardness | $TS\,(\text{MPa}) \approx 3.45\,HB$ | For steels |

> [!note] Source images
> All figures in this note are original Excalidraw reconstructions of the diagrams in the three lecture PDFs and the handwritten notes; the vault copies live in the `Excalidraw/` folder with the `MP - ` prefix.
