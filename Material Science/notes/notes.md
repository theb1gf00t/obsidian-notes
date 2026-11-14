---
title: Material Science — MO-201 Notes
tags:
  - materials-science
  - MO-201
---

# Syllabus Map

Compiled from the lecture slides ([[Mechanical Properties part 1_Odd_2026-27.pdf]], [[Mechanical Properties part 2_Odd_2026-27.pdf]], [[Mechanical Properties part 3_Odd_2026-27.pdf]], [[Composites_Odd_2026-27.pdf]], [[Electrical and Electronic Properties - Part 1_Odd_2026-27.pdf]], [[Electrical and Electronic Properties - Part 2_Odd_2026-27.pdf]], [[Magnetic Properties_Odd_2026-27.pdf]], [[Dielectric materials_Polarization_Optical properties_Odd_2026-27.pdf]]) and the handwritten class notes in [[MO NOTES (1).pdf]] (pp. 100–131 and 132–152). Slides follow **Raghavan, *Materials Science and Engineering*** and **Callister, *Fundamentals of Materials Science and Engineering***.

## Post-Midsem Topics (from [[syllabus]])

| # | Topic | Status |
| --- | --- | --- |
| 1 | Mechanical Properties — I | ✅ noted below |
| 2 | Mechanical Properties — II | ✅ noted below |
| 3 | Mechanical Properties — III | ✅ noted below |
| 4 | Shockley and Frankel Partial Dislocations | — |
| 5 | Composites | ✅ noted below |
| 6 | Electrical and Electronic Properties — Part 1 | ✅ noted below |
| 7 | Electrical and Electronic Properties — Part 2 | ✅ noted below |
| 8 | Magnetic Properties | ✅ noted below |
| 9 | Dielectric Materials, Polarization, Optical Properties | ✅ noted below |

> [!info] How the three parts fit together
> **Part I** builds the vocabulary — deformation, stress, strain, types of loading, the catalogue of mechanical tests, and the five design properties. **Part II** explains *why* materials respond that way — the atomic model of elasticity, slip/twinning, CRSS and the Schmid factor, dislocation reactions — and then dissects the tensile test in full detail. **Part III** deals with materials that cannot be tested in simple tension (ceramics → three-point bending) and with the cheapest, most widely used test of all (hardness).

---

# 1. Mechanical Properties — I

Materials in service are always subjected to forces or loads. Their response — **deformation**, and eventually **fracture or failure** — decides whether a design works. Mechanical testing exists to quantify that response so that materials can be selected, compared and designed with.

---

## 1.1 Why study mechanical properties?

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

### What a "mechanical property" actually is

A **mechanical property** is the *response of a material to an applied load*, expressed as a quantity that can be measured in a reproducible test and inserted into a design calculation. It is therefore not an intrinsic constant like density: it is a *behaviour*, defined only relative to a specified test (specimen geometry, loading mode, temperature, strain rate). This is why "strength" is meaningless without saying *strength in what loading mode, at what temperature, at what speed*.

Every engineering component is loaded in a particular way, and a *different* property governs each case:

| Component | Dominant loading | Property that decides the design |
| --- | --- | --- |
| Bridge girder, building column | Bending / compression | Stiffness (deflection limit), yield strength |
| Car body panel | Bending + impact | Formability (ductility), toughness |
| Turbine blade | Centrifugal tension + creep | Creep strength at temperature, fatigue life |
| Pressure vessel | Biaxial tension | Yield strength, fracture toughness, DBTT |
| Cutting tool, drill bit | Compression + wear | Hardness, wear resistance, hot hardness |
| Spring | Bending/torsion, cyclic | Resilience, fatigue limit |
| Hip implant | Bending + corrosion | Fatigue strength, modulus match to bone |
| Optical fibre, silicon wafer | Bending, thermal stress | Fracture strength (flaw-controlled) |

### Where the numbers come from — and why they matter

The chain of reasoning in materials engineering is *processing → structure → properties → performance*. Mechanical testing is the step that closes the loop: it converts microstructural reality (grain size, dislocation density, porosity, phase fractions) into the design numbers an engineer can use, and it lets a metallurgist work backwards from a failed part to the microstructural cause.

Three distinct uses of mechanical testing:

1. **Design** — provide *allowable stresses* (yield strength divided by a factor of safety) so a component can be sized.
2. **Quality control / acceptance** — check that a delivered batch meets specification (a hardness check on a forged shaft, a Charpy test on a pressure-vessel plate).
3. **Failure analysis and alloy development** — explain *why* a part broke, and rank candidate compositions/processes.

### Failures that shaped the subject

Mechanical properties are studied because getting them wrong kills people. Three canonical cases, all of which recur in this topic:

- **Titanic (1912)** — hull steel with a high DBTT, in ice-cold water, under impact loading (see §2.7). The Charpy tests on recovered plate showed a transition temperature near the water temperature.
- **Liberty ships (1942–45)** — all-welded hulls of a steel with inadequate notch toughness; several broke in two at low temperature, some while at dock. The direct ancestor of modern fracture-toughness specifications.
- **Comet airliner (1954)** — fatigue cracks from square window corners, initiated by stress concentration and driven by repeated pressurisation cycles far below the yield stress (§1.5). The ancestor of damage-tolerance design.

> [!note] The design mindset
> A material is never chosen for a single number. Design asks: *is it stiff enough? strong enough? does it give warning before failing? does it stay tough at the service temperature? can it be made into the required shape?* Those five questions map exactly onto the five key design properties in §1.6.

## 1.2 Deformation: elastic, plastic, fracture

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

### The three responses compared

| | **Elastic** | **Plastic** | **Fracture** |
| --- | --- | --- | --- |
| Recoverable? | Fully, on unloading | No — permanent set remains | No — the body is separated |
| Atomic mechanism | Bond stretching/compression, bond angles bending; atoms displaced by a small fraction of $r_0$ | Dislocation glide (shear of atomic planes), twinning; bonds are *broken and re-made* | Cohesive bonds broken across a plane; crack nucleation + propagation |
| Strain magnitude (metals) | $\lesssim 0.005$ (0.5 %) | 0.01 – 1.0 (1 %–100 %+) | total strain at breaking |
| Stress measure | $E$ (slope) | yield strength, flow stress | fracture strength, toughness |
| Depends strongly on | bond stiffness, temperature (weakly) | temperature, strain rate, grain size, prior deformation | flaws, temperature, strain rate, constraint |
| Reversible in time? | Instantaneous (except anelasticity, §2.9) | No | No |

A useful way to remember the physics: **elasticity is a property of the bonds; plasticity is a property of the defects (dislocations); fracture is a property of the flaws (cracks, pores, inclusions).** Almost every confusing observation in this topic — why a strong material is brittle, why a small crystal is stronger than a big one, why a scratch can halve the strength of glass — follows from that one sentence.

> [!important] Elastic limit, proportional limit, yield point
> These are three *different* landmarks that are often the same number for metals and different for polymers and grey cast iron.
> **Proportional limit** — stress up to which stress $\propto$ strain (Hooke's law holds).
> **Elastic limit** — stress up to which all deformation is recoverable (may exceed the proportional limit slightly).
> **Yield point** — stress at which a measurable *permanent* strain appears (in practice, 0.2 % offset; §2.11).

> [!warning] "Failure" is broader than "fracture"
> A component has failed when it can no longer do its job. That includes:
> - **fracture** (separation) — the obvious case;
> - **excessive elastic deflection** (a shaft that whips, a mirror that distorts) — the material is perfectly intact;
> - **excessive plastic deformation** (a bolt that stretches, a roof that sags);
> - **loss of function by surface damage** — wear, corrosion, fretting.
> Design therefore uses *stiffness* limits as often as *strength* limits.

## 1.3 Types of loading

![[MP - Types of Loading.excalidraw]]

- **Tension** — forces pull the body apart along its axis; the specimen elongates and its cross-section contracts.
- **Compression** — forces push the body together; the specimen shortens and bulges.
- **Shear** — two parallel forces act on opposite faces in opposite directions; layers of material slide over one another.
- **Torsion** — a twisting moment about the long axis; this is really shear varying linearly from zero at the axis to a maximum at the surface.
- **Bending** — not a separate fundamental mode: it is *tension on one face and compression on the other*, with a neutral axis in between.

Two kinds of strain follow from these loadings:

1. **Change in dimension** — elongation, shortening (normal strain).
2. **Angular distortion** — the change of angle between two initially perpendicular lines (shear strain).

### Each loading mode in mechanics terms

| Mode | Stress produced | How it varies across the section | Typical failure mode |
| --- | --- | --- | --- |
| **Tension** | $\sigma = P/A_0$ (uniform) | Constant along the gauge length | Necking → ductile rupture, or cleavage |
| **Compression** | $\sigma = -P/A_0$ | Uniform (away from ends) | Barrelling/shear bands (ductile) or splitting (brittle) |
| **Shear** | $\tau = V/A$ (average) | Parabolic for a rectangular section, max at the neutral axis | Shear fracture at $45^\circ$ to the axis in tension |
| **Torsion** | $\tau = Tr/J$, max at $r = R$ | Linear from zero on the axis to max at the surface | Helical shear fracture at $45^\circ$ |
| **Bending** | $\sigma = My/I$ | Linear from zero at the neutral axis to max at the surfaces | Fracture on the tensile face (brittle) or yield of the tensile face first (ductile) |

Two results worth carrying forward, because they explain why torsion and bending tests exist at all:

- **Torsion** is a pure-shear test. For a circular shaft of radius $R$ and polar moment $J = \pi R^4/2$,
  $$ \tau_{\max} = \frac{T R}{J}, \qquad \theta = \frac{T L}{G J} $$
  so a single torsion test gives the **shear modulus** $G$ and the **shear yield strength** $\tau_y$ directly — quantities that a tensile test only gives indirectly (through $G = E/2(1+\nu)$). Torsion also avoids the necking instability, so it can reach much larger strains than tension.
- **Bending** is not a fundamental mode. The top fibres are in compression and the bottom fibres in tension, with a **neutral axis** in between that is stress-free. For an elastic beam, $\sigma = M y / I$ with $I = bd^3/12$ for a rectangle, so the maximum surface stress is $\sigma = 6M/(bd^2)$. This is exploited in §3.1 to test brittle materials, which are far stronger in compression than in tension.

### Hydrostatic stress — the loading that produces no yielding

If equal normal stresses act on all faces ($\sigma_{11}=\sigma_{22}=\sigma_{33}=-p$) with zero shear, the state is **hydrostatic compression**. Because plastic flow is driven by *shear*, and a hydrostatic state has no shear on any plane, it produces **no plastic deformation and no fracture** — it only changes volume elastically:

$$ \frac{\Delta V}{V} = -3(1-2\nu)\frac{p}{E} = -\frac{p}{K} $$

with $K$ the bulk modulus. This is why:
- a submarine hull, a deep-sea sphere or a specimen under a 10 kbar pressure cell does not "crush" plastically;
- the **triaxial tension** that builds up inside a neck or ahead of a notch *does* promote fracture, because it adds hydrostatic tension that opens cracks (this is the physical content of the Bridgman correction in §2.18 and of notch brittleness in §2.7);
- **superplastic forming** and **hydrostatic extrusion** can reach enormous strains — the superimposed pressure suppresses void growth and fracture.

### Combined loading is the normal case

Real components see several modes at once: a rotating shaft carries bending + torsion + axial load; a tooth of a gear carries contact pressure + bending + sliding shear. Because the equations of elasticity are linear, the stresses from each load case **superpose**: add the tensors component by component, then compare the resulting multiaxial state with a yield criterion (von Mises or Tresca, §1.4) rather than with the uniaxial yield strength.

## 1.4 Concepts of stress and strain

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

![[MP1 - Stress tensor at a point.png|420]]

*Figure — the nine stress components acting on an elemental cube; the three visible faces carry one normal stress each and two shear stresses each.*

### Why nine components, and how they reduce

The stress at a point is a **second-rank tensor** because it is a linear map from a surface normal $\mathbf{n}$ to a traction vector $\mathbf{t}$: $t_i = \sigma_{ij}n_j$. It is a *tensor*, not a scalar, because a bar loaded in tension along $z$ also has shear stresses on planes inclined to $z$ — the number observed depends on the orientation of the plane you cut.

1. **Symmetry** ($\sigma_{ij}=\sigma_{ji}$, from moment equilibrium of an infinitesimal element) reduces 9 → **6** independent components.
2. **Principal axes** — for any stress state there is one orientation in which all shear stresses vanish. The three normal stresses on those planes are the **principal stresses** $\sigma_1 \ge \sigma_2 \ge \sigma_3$, and they are the eigenvalues of $\sigma_{ij}$. Design codes are usually written in terms of them.
3. **Invariants** — the combinations
   $$ I_1 = \sigma_1+\sigma_2+\sigma_3, \qquad I_2 = \sigma_1\sigma_2+\sigma_2\sigma_3+\sigma_3\sigma_1, \qquad I_3 = \sigma_1\sigma_2\sigma_3 $$
   are independent of the coordinate system, so *any* physically meaningful failure criterion must be expressible in them.
4. **Mohr's circle** is the graphical version: for a given $\sigma_{ij}$ it gives the normal and shear stress on every possible plane, and the largest circle's radius is the maximum shear stress $\tau_{\max}=(\sigma_1-\sigma_3)/2$.

**Yield criteria for multiaxial stress.** A uniaxial yield strength $\sigma_y$ is not directly applicable to a multiaxial state; two criteria replace it:

$$ \sigma_{\text{vM}} = \sqrt{\tfrac12\left[(\sigma_1-\sigma_2)^2+(\sigma_2-\sigma_3)^2+(\sigma_3-\sigma_1)^2\right]} = \sigma_y \quad\text{(von Mises, distortion energy)} $$

$$ \tau_{\max} = \frac{\sigma_1-\sigma_3}{2} = \frac{\sigma_y}{2} \quad\text{(Tresca, maximum shear)} $$

Both depend only on *differences* of principal stresses — confirming that a hydrostatic stress cannot cause yielding. They differ by at most 15.5 %, and they let a tensile-test yield strength be applied to any complex load case.

### Strain as a tensor, and the two strain measures

The **strain tensor** is the symmetric part of the displacement gradient:

$$ \varepsilon_{ij} = \frac12\left(\frac{\partial u_i}{\partial x_j}+\frac{\partial u_j}{\partial x_i}\right) $$

Its diagonal terms are **normal strains** ($\Delta L/L_0$); the off-diagonal terms are the *tensor* shear strains, which are **half** the engineering shear strain: $\gamma_{xy} = 2\varepsilon_{xy}$. The factor of 2 is a constant source of error — the physical distortion of a square element is $\gamma = \Delta x/y_0 = \tan\theta \approx \theta$, and it is $\gamma$ that appears in $G$ and in the strain-energy expressions.

### Counting the elastic constants

The fourth-rank stiffness tensor $C_{ijkl}$ maps strain to stress, $\sigma_{ij}=C_{ijkl}\varepsilon_{kl}$. Because both stress and strain are symmetric, $C_{ijkl}=C_{jikl}=C_{ijlk}$, the $81$ components collapse as:

| Symmetry | Independent elastic constants | Examples |
| --- | --- | --- |
| Triclinic (no symmetry) | **21** | — |
| Monoclinic | 13 | gypsum |
| Orthorhombic | 9 | polyethylene crystals, wood |
| Hexagonal / transversely isotropic | 5 | Mg, Zn, Ti, graphite, drawn fibres |
| Cubic | 3 ($C_{11}, C_{12}, C_{44}$) | Al, Cu, Fe, Ni, diamond, Si |
| Isotropic (polycrystal average) | **2** | any random polycrystal, glass |

For a **cubic** crystal the *direction* of loading changes the measured modulus — the elastic anisotropy ratio is

$$ A = \frac{2C_{44}}{C_{11}-C_{12}} \qquad (A=1\ \text{isotropic}) $$

with $A_{\text{Al}}\approx1.2$, $A_{\text{Fe}}\approx2.5$, $A_{\text{Cu}}\approx3.2$, $A_{\text{W}}\approx1.0$. In aluminium the $\langle111\rangle$ direction is stiffer ($\sim76$ GPa) than $\langle100\rangle$ ($\sim63$ GPa); in a random polycrystal these average to $\sim70$ GPa.

### Units and magnitudes

$$ 1\ \text{MPa} = 10^6\ \text{Pa} = 10^6\ \text{N/m}^2, \quad 1\ \text{GPa} = 10^3\ \text{MPa}, \quad 1\ \text{ksi} = 6.895\ \text{MPa}, \quad 1\ \text{MPa} = 145\ \text{psi} $$

Strain is dimensionless (m/m or %). Typical room-temperature moduli, for order-of-magnitude intuition:

| Class | Material | $E$ (GPa) |
| --- | --- | --- |
| Covalent ceramic | diamond | 1000–1050 |
| | SiC / $\text{Si}_3\text{N}_4$ | 400–450 / 300 |
| Ionic ceramic | $\text{Al}_2\text{O}_3$ | 380–400 |
| | glass (soda-lime) | 70–80 |
| Metal | steel | 200–215 |
| | nickel, tungsten | 200, 400 |
| | cast iron | 100–170 |
| | titanium alloy (Ti-6Al-4V) | 110–120 |
| | copper, aluminium | 110–128, 69–72 |
| | magnesium | 45 |
| Composite | CFRP (fibre direction) | 70–200 |
| Polymer | PMMA, PS | 2.4–3.4 |
| | HDPE | 0.7–1.4 |
| Elastomer | natural rubber | 0.001–0.01 |

> [!note] Why $E$ is the least structure-sensitive property
> $E$ depends almost entirely on **bonding** and only weakly on microstructure. Alloying, cold work, grain size, phase changes and heat treatment move the yield strength by factors of 2–5 but move $E$ by only a few percent. Only porosity and cracks (which reduce the load-bearing section) change $E$ appreciably. This is why "$E$ = property of the bond, $\sigma_y$ = property of the defects" is such a useful summary.

## 1.5 Examples of mechanical tests

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

### What each test really delivers

| Test | Standard | Raw output | Derived properties | Main limitation |
| --- | --- | --- | --- | --- |
| Tension | ASTM E8 / ISO 6892 | Load–elongation | $E$, YS, UTS, %EL, %RA, $n$, $K$ | Requires a machinable, grip-able specimen; unstable after necking |
| Compression | ASTM E9 | Load–deformation | Compressive YS, compressive strength, $E$ | Buckling of slender specimens; friction/barrelling at platens |
| Torsion | ASTM E143 | Torque–twist | $G$, shear YS, shear strength | Non-uniform stress if section is not circular |
| Bend (3/4-point) | ASTM C1161, C674 | Load–deflection | Flexural strength (MOR) | Only the surface fibre sees the maximum stress |
| Hardness | ASTM E10/E18/E92/E384 | Indent size or depth | HB, HV, HK, HRx; estimate of UTS | Empirical; indenter/size effects; not a fundamental property |
| Fatigue | ASTM E466, E606 | Cycles to failure at a stress amplitude | S–N curve, endurance limit, fatigue strength | Long test times; scatter; specimen-sensitive |
| Impact (Charpy/Izod) | ASTM E23 / ISO 148 | Absorbed energy | Notch toughness vs temperature, DBTT | Comparative, not a design stress; geometry-dependent |
| Creep / stress rupture | ASTM E139 | Strain vs time, time to rupture | Secondary creep rate, rupture life, activation energy | Months-long tests; extrapolation needed |

**Fatigue, in more detail.** Failure occurs by the initiation and growth of a crack under *cyclic* stress whose peak is below the yield strength. The fatigue life is divided into initiation (most of the life at low stress) and propagation. Results are plotted as an **S–N curve** (stress amplitude vs number of cycles on a log scale). Ferrous alloys and titanium show a true **endurance limit** — a stress below which the life is effectively infinite ($>10^7$ cycles); aluminium, copper and most polymers do not, and must be designed for a finite life. Fatigue is the single most common cause of service failure in rotating and vibrating machinery, precisely because the part shows no visible deformation beforehand.

**Impact testing, in more detail.** A heavy pendulum strikes a **notched** specimen and the energy absorbed is read from the height of the swing. The notch is essential: it produces a triaxial stress state and a high strain rate, which is what makes the test sensitive to the ductile–brittle transition. Results are reported in joules (or ft·lb) and are *not* a material constant — they depend on notch geometry and specimen size. The **27 J (20 ft·lb) at −20 °C** type criteria in ship and pressure-vessel codes come directly from this test (§2.7).

**Creep, in more detail.** Under a constant load at high temperature the strain–time curve has three stages: **primary** (decreasing rate — work hardening dominates), **secondary/steady-state** (constant minimum rate — hardening balanced by recovery, the stage used for design), and **tertiary** (accelerating — necking and void growth, ending in rupture). The steady-state rate is described by
$$ \dot{\varepsilon}_s = A\sigma^n\exp\!\left(-\frac{Q}{RT}\right) $$
with a stress exponent $n\approx3$–$5$ for dislocation creep and $Q$ the activation energy for self-diffusion; at low stress and fine grain size, diffusional creep takes over with $n\approx1$.

## 1.6 Key mechanical design properties

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

### The five properties, in engineering language

- **Stiffness** ($E$, or $G$) sets the *deflection* for a given load. It is a **design limit in its own right** — a bridge that sags 1 m has failed its serviceability requirement even if no metal has yielded. It cannot be changed by heat treatment; only by changing the material (or the section shape, which is a *geometry* fix, not a materials fix).
- **Strength** sets the *load* a part can carry. Design is normally based on **yield**, not fracture, because yield is a well-defined, reproducible, structure-insensitive-in-the-small quantity, and because a part that yields visibly gives warning.
- **Hardness** is a *localised* strength: resistance of the surface to being pushed in. It is the cheapest surrogate for strength and wear resistance.
- **Ductility** is the *warning system*: the amount of plastic strain before fracture. It is what allows a part to redistribute stress at a stress concentration, and it is what allows a material to be *formed* (rolled, drawn, bent, deep-drawn).
- **Toughness** is *energy absorbed before fracture*, i.e. strength **and** ductility together. A tough material resists the propagation of a crack. It is the property that decides whether a small manufacturing flaw becomes a catastrophic failure.

$$\text{Strength} \neq \text{Toughness} \neq \text{Hardness}$$

### Typical values, for scale

| Material | $E$ (GPa) | Yield strength (MPa) | UTS (MPa) | Elongation (%) | Hardness |
| --- | --- | --- | --- | --- | --- |
| Mild steel (A36) | 200 | 250 | 400–500 | 20–25 | 120 HB |
| High-strength low-alloy steel | 205 | 550 | 620 | 18 | 180 HB |
| Quenched & tempered 4340 | 205 | 1500 | 1800 | 8–12 | 50 HRC |
| Austenitic stainless 304 | 193 | 205 | 515 | 40 | 80 HRB |
| Aluminium 6061-T6 | 69 | 275 | 310 | 12 | 95 HB |
| Titanium Ti-6Al-4V | 114 | 830 | 900 | 10–15 | 35 HRC |
| Copper (annealed) | 110 | 70 | 220 | 45 | 40 HB |
| Alumina (99.5 %) | 380 | — (brittle) | 300 (flexural) | $\sim0$ | 1500 HV |
| Soda-lime glass | 70 | — | 70 (flexural) | $\sim0$ | 550 HV |
| PMMA | 3.0 | 70 | 70 | 2–5 | — |
| Nylon 6,6 | 3.0 | 80 | 85 | 60 | — |
| Natural rubber | 0.005 | — | 20–30 | 500–800 | — |

### Factor of safety

Design does not use the measured strength directly:

$$ \sigma_{\text{allowable}} = \frac{\sigma_y}{n}, \qquad n = 1.5\text{–}2 \text{ (normal service)},\ 2\text{–}4 \text{ (shock/fatigue)},\ 4\text{+ (pressure vessels, uncertain loads)} $$

The safety factor covers scatter in the material data, uncertainty in the load, stress concentrations not captured by the simple formula, and consequences of failure. It is a *legal and economic* choice as much as a technical one.

### Stiffness vs strength trade-off, and specific properties

A material can be stiff but weak (glass), strong but compliant (some polymers), or both (steel). For **moving parts** the relevant quantities are the *specific* ones — property divided by density:

| Specific property | Expression | Winner |
| --- | --- | --- |
| Specific stiffness | $E/\rho$ | CFRP, ceramics, Al, Ti |
| Specific strength | $\sigma_y/\rho$ | CFRP, Ti alloys, Al-Li |
| Specific toughness | $K_{Ic}/\rho$ | Al alloys, steel |

This is the basis of **Ashby material-selection charts** (modulus–density, strength–density bubble charts): the material classes form clusters, and the selection lines are iso-performance lines of the form $E = C\rho$. Polymers lie bottom-left, metals in the middle, ceramics top-right (stiff, strong, but brittle), composites occupy the gap. The charts make the trade-offs in this table visible at a glance.

## 1.7 Mechanical testing ↔ deformation mechanisms

Mechanical tests are only the *symptom*; the *cause* is what happens to atoms and dislocations. The lecture maps the bridge explicitly:

- **Plastic deformation mechanisms:** slip, twinning, dislocation climb, grain-boundary sliding, …
- **Schmid factor / CRSS** — which slip system operates, and at what stress.
- **Glissile vs sessile dislocations** — mobile dislocations vs locked ones.
- **Theoretical shear strength of a perfect crystal** — why real crystals are $10^3$–$10^4$ times weaker.
- **Peierls stress / Peierls–Nabarro force** — the lattice friction that a dislocation must overcome to move.
- **Creep test** — time-dependent deformation at elevated temperature under constant stress.
- **Fatigue test** — cyclic loading below yield.

All of these are developed in §2.

### The length-scale ladder

| Scale | What exists there | What it controls |
| --- | --- | --- |
| Atomic ($10^{-10}$ m) | Bonds, potential well $U(r)$ | $E$, theoretical strength, melting point |
| Dislocation core ($10^{-9}$ m) | Peierls–Nabarro friction, core width | Yield stress, temperature dependence of strength |
| Dislocation substructure ($10^{-7}$–$10^{-6}$ m) | Pile-ups, cells, locks | Work hardening, $n$ |
| Grain ($10^{-5}$–$10^{-4}$ m) | Grain boundaries, orientation | Yield strength (Hall–Petch), ductility |
| Specimen ($10^{-3}$–$10^{-1}$ m) | Flaws, surface finish, constraint | Strength of brittle materials, DBTT |
| Component | Stress concentrations, residual stress | Fatigue life, fracture |

Each row explains a distinct part of a mechanical test. The atomic scale fixes the *slope* of the curve, the dislocation scale fixes *where the curve bends*, and the specimen scale fixes *where it ends*.

### Mechanism → measurable signature

| Observation in a test | Underlying mechanism |
| --- | --- |
| Straight elastic line, slope = $E$ | Bond stretching; no defects involved |
| Yield at $\sim10^{-3}$–$10^{-4}G$ instead of $G/10$ | Dislocation glide, not rigid plane shear |
| Upper/lower yield point, Lüders plateau | Unpinning of dislocations from interstitial (C, N) atmospheres |
| Rising plastic branch (work hardening) | Dislocation multiplication, $\tau \propto b\sqrt{\rho}$, jog/lock formation |
| Strong temperature dependence of $\sigma_y$ in BCC | Peierls–Nabarro lattice friction, kink-pair nucleation |
| Weak temperature dependence in FCC | Obstacle-controlled glide, forest hardening |
| Yield stress $\propto d^{-1/2}$ | Grain-boundary barrier to slip (Hall–Petch) |
| Ductility limited in HCP | Only 3 basal slip systems $<5$ required by von Mises |
| Time-dependent strain at high $T$ | Dislocation climb + diffusional flow (creep) |
| No warning before failure | Crack propagation with negligible plastic zone (fatigue, cleavage) |

The key relationships that connect these scales (developed in §2):

$$ \tau_y \approx \tau_0 + \alpha G b\sqrt{\rho} \quad\text{(forest hardening)}, \qquad \sigma_y = \sigma_0 + k_y d^{-1/2}\ \text{(Hall–Petch)}, \qquad \tau \approx \frac{Gb}{2\pi L}\ \text{(Orowan, obstacle spacing } L\text{)} $$

So a single tensile test is really a *probe of defect populations*: two specimens of the same composition and different grain size give different yield stresses, different work-hardening rates and different ductilities, all from the same atoms and bonds.

## 1.8 Tensile test: first look

The tensile test pulls a specimen along its axis at a constant rate and records **load** and **elongation**, which are converted to **stress** and **strain**.

- A **ductile** material shows a long plastic region, work hardening, necking and a cup-and-cone (or shear) fracture.
- A **brittle** material shows an almost perfectly linear elastic line up to sudden fracture, with negligible plastic strain.

The same test on the *same* material can produce either curve depending on temperature — this is the subject of §2.7.

![[MP - Brittle vs ductile tensile curves.png|480]]

*Figure — engineering stress–strain curves for a ductile metal (steel, with upper and lower yield points and a long work-hardening regime) and a brittle material (grey cast iron or a ceramic), which is linear-elastic to fracture.*

**Reading the ductile curve feature by feature:**

1. **Linear elastic rise** — slope $E$; at this point the strain is entirely bond stretching and is fully recoverable.
2. **Upper yield point $\to$ lower yield point** — a sudden drop. It is caused by the *unpinning* of dislocations from solute atmospheres: once a few dislocations break free they multiply and the stress needed falls. The associated plastic band (**Lüders band**) propagates along the gauge length at constant stress, producing the flat plateau.
3. **Work hardening** — the curve rises again as the dislocation density climbs; the specimen deforms uniformly.
4. **UTS (maximum) and necking** — the load reaches a maximum when the *increase* in strength from work hardening is exactly offset by the *decrease* in cross-section.
5. **Fracture** — in a ductile round bar the neck develops a **cup-and-cone** appearance: a central fibrous zone of micro-void coalescence, surrounded by a $45^\circ$ **shear lip**. In a brittle fracture, the surface shows flat **cleavage facets** and no neck.

The brittle curve, by contrast, has **no yielding at all**: fracture happens on the linear elastic line, at a stress that is strongly dependent on the largest flaw in the specimen (hence the enormous scatter, and hence the statistical treatment in §3.1–§3.2).

**What the machine actually records** is load and crosshead displacement; the stress–strain curve is computed afterwards using the *initial* area and gauge length. Two corrections are needed to get physically meaningful data: the machine's own elastic compliance must be subtracted from the displacement, and the specimen must be loaded through a *reduced-section* gauge so that it yields away from the grips (§2.6).

> [!tip] Exam pointer
> Part I is mostly *vocabulary*. Be able to state, in one line each: elastic vs plastic vs fracture vs failure; the four loading modes; the difference between engineering and true stress/strain; and the property ↔ test mapping in §1.6.

---

# 2. Mechanical Properties — II

## 2.1 Atomic model of elastic behaviour

![[MP2 - Interatomic force-distance curve.png|420]]

*Figure — the interatomic force–distance curve: zero force at $r_0$; a tensile force $F'$ at $r'>r_0$, a compressive force $F''$ at $r''<r_0$. The curve is steeper for compression than for tension, which is the origin of thermal expansion.*

Elastic deformation is nothing but a small change in the **interatomic spacing**. The interaction between two atoms is described by a potential energy $U(r)$ with a minimum at the equilibrium separation $r_0$:

$$ F(r) = \frac{dU}{dr}, \qquad \left.\frac{dU}{dr}\right|_{r_0} = 0 $$

- At $r = r_0$ the net force is **zero** — the equilibrium state.
- Stretching the bond to $r'>r_0$ or compressing it to $r''<r_0$ requires an external force $F'$ or $F''$, obtained from the slope of the $U$–$r$ (or $F$–$r$) curve.
- The **stiffness** is the curvature of the well at the minimum:

$$ E \propto \left.\frac{dF}{dr}\right|_{r_0} = \left.\frac{d^2U}{dr^2}\right|_{r_0} $$

Hence a **deep, steep, narrow potential well → high modulus** (covalent ceramics such as diamond, SiC), while a **shallow, wide well → low modulus** (soft metals, polymers). This is also why the force–distance curve is asymmetric: it is much harder to compress a bond than to stretch it (repulsion rises steeply), which is the origin of **thermal expansion** and of the fact that elastic behaviour is only linear for *small* displacements.

> [!note] Why Hooke's law works
> Near $r_0$ the $F$–$r$ curve is essentially a straight line, so force $\propto$ displacement → **linear elasticity**. At large strains the curve bends and Hooke's law fails. Anelasticity and nonlinear elasticity are the corrections.

### Theoretical shear strength of a perfect crystal

If a perfect crystal were sheared, the shear stress would vary roughly sinusoidally with displacement, giving

$$ \tau_{\text{theoretical}} \approx \frac{Gb}{2\pi d} \approx \frac{G}{2\pi}\ \ (\text{for } b \approx d) \approx \frac{G}{6} $$

where $b$ is the repeat distance along the slip direction and $d$ the interplanar spacing; depending on the $b/d$ ratio of the crystal, the estimate ranges from about $G/6$ down to $G/30$. Measured yield stresses are typically $10^{-3}$–$10^{-4}\,G$ — three to four orders of magnitude lower. **This discrepancy is the classic proof that plastic deformation occurs by the motion of dislocations, not by the simultaneous sliding of whole planes.**

The stress needed to move a dislocation through the lattice is the **Peierls–Nabarro stress**:

$$ \tau_{PN} = \frac{2G}{1-\nu}\,\exp\!\left(-\frac{2\pi w}{b}\right), \qquad w = \frac{d}{1-\nu} $$

where $b$ is the Burgers vector, $d$ the interplanar spacing and $w$ the width of the dislocation core.

- **Wide core** (metals — metallic bonding, non-directional) → exponential term small → **low Peierls stress** → easy glide, ductile.
- **Narrow core** (covalent/ionic ceramics) → **high Peierls stress** → hard, brittle.

### The potential well, quantitatively

The two standard model potentials are the **Morse** potential (bonding, three parameters) and the **Lennard-Jones** potential:

$$ U(r) = 4\epsilon\left[\left(\frac{\sigma}{r}\right)^{12}-\left(\frac{\sigma}{r}\right)^{6}\right] $$

the $r^{-12}$ term being the Pauli/ion-core repulsion and the $r^{-6}$ term the van der Waals attraction. Expanding any such $U(r)$ about its minimum in a Taylor series gives

$$ U(r) \approx U(r_0) + \underbrace{\frac{dU}{dr}\Big|_{r_0}}_{=\,0}(r-r_0) + \frac12\frac{d^2U}{dr^2}\Big|_{r_0}(r-r_0)^2 + \cdots $$

The first non-zero term is **parabolic**, i.e. the force is *linear* in displacement:

$$ F = \frac{dU}{dr} \approx \left.\frac{d^2U}{dr^2}\right|_{r_0}(r-r_0) = k\,(r-r_0) $$

That is Hooke's law, derived from the shape of the potential well. The modulus of a solid is this bond stiffness multiplied by the number of bonds per unit area:

$$ E = \frac{k}{r_0}\ \propto\ \frac{1}{r_0}\left.\frac{d^2U}{dr^2}\right|_{r_0} $$

Three consequences, all directly examinable:

1. **$E$ scales with the depth and steepness of the well.** Deep wells (high melting point, high cohesive energy) → high $E$. A useful correlation is that the ratio $E\,\Omega/(k_BT_m)$ (with $\Omega$ the atomic volume) is roughly constant within a class of solids of the same bond type, so $E$ tracks the melting point: diamond, the deepest well, has the highest modulus; lead, with a low melting point and a shallow well, has one of the lowest among metals.
2. **$E$ decreases with temperature**, roughly linearly, by typically **2–5 % per 100 K**, because thermal expansion increases $r_0$ and the potential well becomes effectively shallower (anharmonicity). This is why the "room-temperature modulus" must be quoted with a temperature for high-temperature design.
3. **Elastic strain is small** because the parabola is only a good approximation for $|r-r_0| \ll r_0$. Real elastic strains are $\approx 0.1$–$1$ % — only a small fraction of an interatomic spacing. Beyond that, the higher-order (anharmonic) terms dominate and the stress–strain relation becomes **non-linear**; rubber is the extreme case, where the "bonds" are chain conformations and enormous non-linear recoverable strains are the norm.

### Theoretical cohesive (fracture) strength

The same force–displacement curve gives the *maximum tensile force a bond can sustain*, obtained by setting $dF/dr = 0$ on the tensile side. Equating the work done in separating two planes to the surface energy $2\gamma_s$ gives the **theoretical cohesive strength**:

$$ \sigma_{\text{th}} \approx \sqrt{\frac{E\gamma_s}{a_0}} \approx \frac{E}{10} \ \ (10\text{–}15\,\%\ \text{of } E) $$

Compare with the **theoretical shear strength** $\tau_{\text{th}} \approx G/2\pi$ derived above. Both are one to two orders of magnitude *above* what is measured (real strengths are $E/100$ to $E/1000$). But the *reasons* are different, and the distinction matters:

| Quantity | Theoretical | Measured | Ratio | Why the gap? |
| --- | --- | --- | --- | --- |
| Shear (yield) strength | $G/2\pi \approx G/6$ | $10^{-3}$–$10^{-4}G$ | $10^3$–$10^4$ | **Dislocations** — plasticity is not rigid-plane sliding |
| Cohesive (fracture) strength | $\sqrt{E\gamma_s/a_0}\approx E/10$ | $E/100$–$E/1000$ | $10$–$100$ | **Flaws** — a crack concentrates stress at its tip |

So the two great weaknesses of real materials have separate explanations: **dislocations explain why metals are soft; cracks explain why brittle solids are weak.** Both are "defects", but they are different defects with different consequences — and that is the organising idea of the whole of §2 and §3.

> [!important] The Frenkel derivation, step by step
> 1. Assume the sheared planes slide as rigid blocks and the resisting shear stress is a periodic function of displacement $x$ with period $b$ (the repeat distance in the slip direction):
> $$ \tau = \tau_{\max}\sin\frac{2\pi x}{b} $$
> 2. For small $x$ this must reduce to Hooke's law in shear, $\tau = G\gamma = Gx/d$, where $d$ is the interplanar spacing.
> 3. Therefore $\tau_{\max}\dfrac{2\pi x}{b} = G\dfrac{x}{d}$, giving
> $$ \tau_{\max} = \frac{Gb}{2\pi d} $$
> 4. Taking $b \approx d$ (close-packed plane and direction) gives $\tau_{\max}\approx G/2\pi \approx G/6$.
> The measured CRSS of a soft FCC metal is $\sim10^{-5}G$ — a factor of $10^4$ discrepancy. A dislocation does not shear the whole plane at once; it shears one line of bonds at a time, so the *applied* stress only has to supply the (small) Peierls friction.

### The Peierls–Nabarro stress in physical terms

$$ \tau_{PN} = \frac{2G}{1-\nu}\exp\!\left(-\frac{2\pi w}{b}\right), \qquad w = \frac{d}{1-\nu} $$

The exponential is the whole story: the resistance falls off **exponentially with the width of the dislocation core** $w$, measured in units of $b$. A dislocation whose core is spread over many atomic spacings is "smeared out" and barely notices the discrete lattice; a dislocation squeezed into one atomic spacing feels every atom it passes.

- **Metals**: non-directional metallic bonding spreads the core over $w\sim2$–$5b$ → $\tau_{PN}$ is a small fraction of $G$ → easy glide even at low temperature. This is why FCC metals stay ductile to cryogenic temperatures.
- **Covalent/ionic solids**: directional, stiff bonds keep the core narrow → $\tau_{PN}$ is a large fraction of $G$ (approaching the theoretical shear strength) → the crystal prefers to *fracture* rather than to deform plastically. Diamond, SiC, sapphire and silicon are hard and brittle for exactly this reason, and they become *ductile* only above $\sim0.5T_m$ (silicon is brittle at room temperature despite being a semiconductor; silicon is used as a "brittle" material in MEMS for the same reason).
- **BCC metals sit in between**: their screw dislocation cores are *non-planar*, spread over three intersecting $\{110\}$ planes, which gives a high and strongly **temperature-dependent** Peierls stress. This is the origin of the sharp yield drop, the strong temperature dependence of $\sigma_y$ in iron, and the **DBTT** (§2.7). It also explains why BCC metals are strong at low temperature (high $\tau_{PN}$) but why that strength is useless — they fracture before yielding.
- **Motion of a dislocation past the Peierls barrier requires kink-pair nucleation**: the dislocation advances by forming a pair of kinks on its line, each kink being a short segment that has already crossed the barrier. The activation energy for kink-pair formation sets the temperature dependence of the yield stress, giving the characteristic $\ln(1/T)$ behaviour seen in BCC metals.

![[MP1 - Slipped and unslipped regions of a crystal.png|460]]

*Figure — a dislocation as the boundary between a slipped and an unslipped region of the crystal: the "interfacial region" is the dislocation core, of width $w$, and the lattice above and below it is perfect except for the elastic distortion around the core.*

## 2.2 Deformation by slip and twinning

![[MP - Slip and Twinning.excalidraw]]

| | **Slip** | **Twinning** |
| --- | --- | --- |
| Displacement | Whole block above the plane shifts by a **discrete, integral number of lattice spacings** | Each successive plane shifts by a **fraction** of a lattice spacing, increasing with distance from the twin plane |
| Result at surface | A visible **step** (slip line/steps) | A reoriented region; surface tilts |
| Lattice orientation | **Unchanged** after slip | **Changed** — the twinned region is a mirror image of the parent |
| When it dominates | Normal case for metals with many slip systems (FCC, BCC) | When slip is difficult: HCP metals, low temperature, high strain rate, shock loading |
| Magnitude of strain | Large (slip can repeat indefinitely) | Small (a twin can accommodate only a limited strain) |

Both are **shear** processes: the resolved shear stress on the plane, in the direction, does the work. Twinning is also important because the reoriented twin lamellae can *re-activate* otherwise hard slip systems, and twin boundaries act as barriers to dislocation motion.

![[MP2 - Slip and twinning sequence.png|420]]

*Figure — (a) before deformation; (b) after slip, the upper block is displaced by a whole number of lattice spacings and the surface shows a step; (c) after twinning, each plane is displaced by a fraction of a spacing, producing a mirror-image (twinned) region.*

### Slip in more detail

- Slip is **quantised**: the offset at the surface is a whole number of Burgers vectors, $n b$, because every dislocation that emerges leaves a step of height $b$. A visible **slip line** on an electropolished surface is not one dislocation but a **slip band** containing hundreds of dislocations.
- Slip is *not* a simultaneous rigid sliding of two half-crystals. It proceeds by the nucleation, glide and escape of dislocations; the surfaces of the slipped region remain perfect, and the crystal orientation on both sides of the slip plane is unchanged.
- Slip is **conservative** (no atoms added or removed) and **athermal in principle** for FCC metals — it needs only the Peierls stress to be exceeded, plus the stress to bypass obstacles. It is therefore possible at absolute zero (given enough stress).
- Because slip repeats indefinitely on the same system, it can produce **arbitrarily large strains**; this is why metals can be rolled to 99 % reduction in thickness.

### Twinning in more detail

- In **deformation (mechanical) twinning** every successive plane is displaced by a *fraction* of a lattice vector, so the sheared volume is uniformly reoriented. For FCC the twin system is $\{111\}\langle112\rangle$ with a **twinning shear** of $1/\sqrt2 = 0.707$; for HCP it is $\{10\bar12\}\langle10\bar11\rangle$ (the common "tension twin") or $\{10\bar11\}\langle10\bar12\rangle$ (compression twin). BCC twins on $\{112\}\langle111\rangle$.
- The twin is a **mirror image** of the parent lattice. It is *not* a phase; the crystal structure is identical, only its orientation differs.
- Twinning accommodates only a **small, fixed** strain: once the twin has grown across the grain, no further deformation is possible on that system. It is therefore a *supplementary* mechanism, used when slip is restricted.
- **When twinning dominates:** HCP metals (Mg, Zn, Cd, Ti) with few slip systems; BCC metals at low temperature or high strain rate (shock loading, explosive forming); FCC metals of **low stacking-fault energy** (brass, austenitic stainless steel — the "TWIP" steels exploit twinning-induced plasticity for exceptional ductility); and any metal at very large strains or during recrystallisation.
- **Twin boundaries are effective barriers to slip** — they are coherent, low-energy boundaries that dislocations cannot cross easily, so a fine twin lamellar structure strengthens the material exactly as grain boundaries do (Hall–Petch-like). Twinning therefore both *enables* deformation (new orientations) and *hardens* (new barriers).
- **Annealing twins** (seen as straight parallel bands in FCC metals such as copper, brass and austenitic stainless steel) form during heat treatment/grain growth, not by deformation — they do not contribute to shape change, but they do affect properties and are a microstructural fingerprint.

| Feature | Slip | Twinning |
| --- | --- | --- |
| Stress required | Low (reaches CRSS early) | High (often $\sim$2–3× CRSS; or when slip is geometrically impossible) |
| Temperature dependence | Weak in FCC, strong in BCC | Increases as temperature falls (twinning stress rises more slowly than slip stress) |
| Strain produced | Unbounded | Bounded (a few %) |
| Orientation change | None | Reorientation of the twinned volume |
| Surface evidence | Slip steps/lines | Tilts/offsets, straight-sided lamellae |

## 2.3 Slip systems

A **slip system** = one **slip plane** (the close-packed plane — highest atomic density, widest interplanar spacing, hence lowest shear resistance) + one **slip direction** (the close-packed direction within that plane) + the Burgers vector of the dislocation that glides.

| Crystal | Slip plane(s) | Slip direction(s) | Independent systems | Remarks |
| --- | --- | --- | --- | --- |
| **FCC** | $\{111\}$ (4 octahedral planes) | $\langle 110\rangle$ | $4\times3 = 12$ | Most ductile; e.g. Cu, Al, Ni, austenitic stainless steel |
| **BCC** | $\{110\}$ **more common**; $\{112\}$, $\{123\}$ **less common** | $\langle 111\rangle$ | $6\times2 = 12$ (from $\{110\}$) | Slip is *not* on the closest-packed plane; temperature-sensitive (low-T brittleness) |
| **HCP** | Basal $(0001)$ **more common**; prismatic and pyramidal planes **less common** | Close-packed $\langle 11\bar{2}0\rangle$ | 3 from basal ($1\times3$) | Only 3 basal systems → limited ductility; Ti, Mg, Zn, Cd |
| **NaCl (ionic)** | $\{110\}$ | $\langle 110\rangle$ | 6 | Slip on $\{110\}$ avoids bringing like-charged ions together |

The **number of independent slip systems** controls ductility (von Mises criterion: at least 5 independent systems are needed for an arbitrary shape change of a polycrystal). This is why FCC metals are ductile and HCP metals are not.

![[MP2 - Slip planes and directions table.png|440]]

*Figure — the lecture table of slip planes and directions for FCC, BCC, NaCl and HCP, with the "less common" alternatives marked.*

### Why the close-packed plane and the close-packed direction win

Slip requires the *smallest possible disturbance of the lattice*, and both choices reduce it:

- **Close-packed direction**: the shortest lattice translation, i.e. the shortest Burgers vector $b$. Since the elastic energy of a dislocation is $\propto b^2$, this is the lowest-energy dislocation, and the offset produced per dislocation is smallest.
- **Close-packed plane**: the largest interplanar spacing $d$. The shear stress needed to slide the planes is roughly $\propto 1/d$ (fewer bonds per unit area to break), the Peierls stress falls exponentially with $d$ (through $w = d/(1-\nu)$), and the atomic "corrugation" felt by the moving dislocation is smallest.
- A **slip system** must combine both: $\{111\}$ with $\langle110\rangle$ in FCC, for instance, because the $\langle110\rangle$ direction lies *in* the $\{111\}$ plane.

### Stacking faults, partials and the width of the core

In FCC, the perfect dislocation $\tfrac{a}{2}\langle110\rangle$ can lower its energy by dissociating into two **Shockley partials** joined by a strip of **stacking fault**:

$$ \frac{a}{2}[\bar110] \longrightarrow \frac{a}{6}[\bar211] + \frac{a}{6}[\bar12\bar1] $$

The balance between the repulsion of the partials and the fault energy $\gamma_{SF}$ sets the **separation** of the partials, and hence the *effective width* of the dislocation core. This single quantity controls a surprising amount of behaviour:

| Stacking-fault energy | Fault ribbon | Glide style | Behaviour | Examples |
| --- | --- | --- | --- | --- |
| **High** ($\gamma_{SF}\gtrsim100$ mJ/m²) | Narrow, partials close | Wavy, easy **cross-slip** | Low work-hardening rate, high ductility, good for forming | Al, Cu-Zn with low Zn, Ni |
| **Low** ($\gamma_{SF}\lesssim25$ mJ/m²) | Wide | **Planar** glide, cross-slip difficult | High work-hardening rate, high strength, more twinning, "springy" | 70/30 brass, 304 stainless steel, Cu-Al |

This is why **brass work-hardens so much faster than aluminium** even though both are FCC, and why austenitic stainless steels are both strong and highly ductile (they work-harden and twin). It also explains why cross-slip (needed for dislocations to bypass obstacles and for dynamic recovery) is temperature-dependent: at high temperature the partials recombine thermally and cross-slip becomes easy, which is the basis of Stage III hardening and of recovery.

### Special cases

- **BCC** slip is on $\{110\}$, $\{112\}$ and $\{123\}$ depending on temperature and stress state, always in $\langle111\rangle$. This "pencil glide" gives many *geometrically* possible systems, but the highly stressed non-planar screw core makes the CRSS strongly temperature-dependent. Result: BCC metals are strong but brittle at low $T$, ductile at high $T$.
- **HCP** metals have only 3 basal systems (one plane $\times$ three directions), which by itself cannot satisfy von Mises. Ductility is rescued by (i) prismatic $\{10\bar10\}\langle11\bar20\rangle$ slip, (ii) pyramidal $\langle c+a\rangle$ slip with $b$ out of the basal plane (5 independent systems), and (iii) twinning, which reorients grains so that new systems become favourable. When these are all hard — as in Mg at room temperature, or Zn and Cd — the metal is brittle in polycrystalline form. Adding lithium to magnesium, or raising the temperature, activates $\langle c+a\rangle$ slip and restores ductility.
- **Ionic crystals (NaCl, MgO, LiF)**: slip on $\{110\}\langle110\rangle$ keeps like-charged ions from approaching each other across the slip plane; $\{111\}$ slip would put $\text{Na}^+$ next to $\text{Na}^+$ and is electrostatically forbidden. Cubic ionic crystals are therefore *less* ductile than their 6 independent systems suggest.
- **Covalently bonded crystals** (Si, Ge, diamond, SiC): $\{111\}\langle110\rangle$ slip is *geometrically* available, but the enormous Peierls stress means slip needs $T\gtrsim0.5T_m$. At room temperature they are brittle despite having 12 slip systems — a sharp reminder that **the number of slip systems is necessary but not sufficient for ductility; the CRSS must also be low enough.**
- **Ordered alloys/intermetallics** (Ni$_3$Al, TiAl, FeAl): slip of a single dislocation destroys the ordered arrangement and creates an antiphase boundary, so dislocations must move as **superdislocations** with $b = a\langle110\rangle$ (twice as long, four times the energy), or in coupled pairs. This, plus the limited number of independent systems, is why intermetallics are strong at high temperature but brittle at room temperature.

> [!note] Von Mises criterion — why exactly five?
> A general deformation of a polycrystal requires an arbitrary *shape change at constant volume*. The strain tensor has 6 independent components; the constant-volume constraint removes 1, leaving **5 independent strain components**. Each independent slip system can supply only one, so at least 5 are needed for the *grain* to conform to its neighbours. With fewer, grain boundaries must crack or slide → low ductility. (Grain-boundary sliding and diffusional flow can relax this requirement, which is why fine-grained HCP metals at high temperature are more ductile.)

## 2.4 CRSS and the Schmid factor

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

![[MP2 - Schmid factor geometry.png|420]]

*Figure — the tensile axis at angles $\phi_1$ (to the slip-plane normal) and $\phi_2$ (to the slip direction); the resolved shear stress is $\tau = \sigma\cos\phi_1\cos\phi_2$.*

### The same result in tensor form

The resolved shear stress is the projection of the stress tensor onto the slip plane and the slip direction:

$$ \tau_R = \sigma_{ij}\,b_i\,n_j \quad\text{(per unit } b\text{)} \qquad\text{so}\qquad m = b_i n_j / b $$

where $\mathbf{n}$ is the slip-plane normal and $\mathbf{b}$ the unit slip direction. This **Schmid tensor** form is what finite-element crystal-plasticity codes use, and it makes two facts obvious:

- The Schmid factor depends only on the **relative orientation** of the stress axis, plane normal and slip direction — not on the material.
- For a *general* stress state, each of the 12 systems of an FCC crystal has its own $m$; the active one is whichever maximises $\tau_R$ for that stress state.

### Worked example (typical exam question)

> A copper single crystal is loaded in tension along $[123]$. The primary slip system is $(111)[01\bar1]$. Find the Schmid factor and the yield stress if $\tau_{CRSS} = 0.8$ MPa.

1. Normalise the axis: $\mathbf{t} = [123]/\sqrt{14} = (0.267,\,0.535,\,0.802)$.
2. Plane normal: $\mathbf{n} = [111]/\sqrt3 = (0.577,\,0.577,\,0.577)$.
3. Slip direction: $\mathbf{b} = [01\bar1]/\sqrt2 = (0,\,0.707,\,-0.707)$.
4. $\cos\phi_1 = \mathbf{t}\cdot\mathbf{n} = (0.267+0.535+0.802)(0.577) = 0.926$.
5. $\cos\phi_2 = \mathbf{t}\cdot\mathbf{b} = (0.535-0.802)(0.707) = -0.189$ (sign irrelevant for a shear component; take $+0.189$).
6. $m = 0.926 \times 0.189 = 0.175$.
7. $\sigma_y = \tau_{CRSS}/m = 0.8/0.175 \approx 4.6$ MPa.

Note how *small* the yield stress is: a nearly-perfect copper crystal yields at a few MPa, whereas polycrystalline copper yields at $\sim70$ MPa. That factor of $\sim15$ is the combined effect of orientation averaging (Taylor factor $\sim$3), grain boundaries, and the initial dislocation density.

### Orientation dependence: the "soft" and "hard" orientations

Because $\sigma_y = \tau_{CRSS}/m$, a single crystal's yield stress varies with orientation by a factor of $\infty$ in principle and by roughly $2$–$3$ in practice over the orientations that can actually be tested. Two features of the classic single-crystal data:

- **Multiple slip near $m=0.5$**: when the axis is at $45^\circ$ to both plane and direction, *several* systems simultaneously reach $m\approx0.5$ (there are 8 systems with $m=0.5$ for the $\langle100\rangle$ axis, 6 for $\langle110\rangle$, 6 for $\langle111\rangle$... in fact the number depends on the axis). The crystal then deforms by multiple slip, work-hardens very rapidly, and the load–extension curve shows a sharp "corner". This is why the Schmid law holds well in the "single-slip" orientations and breaks down near high-symmetry axes.
- **Latent hardening**: slip on the primary system hardens the *latent* (inactive) systems even more than itself. This violates the assumption that CRSS is a constant, and it is the reason real crystals show a higher flow stress than the simple Schmid prediction after a few percent strain.

### From single crystal to polycrystal: the Taylor factor

In a polycrystal, grains are randomly oriented and each must accommodate the shape change of its neighbours (von Mises: 5 systems). Averaging the Schmid factors over all orientations and all active systems gives the **Taylor factor**

$$ M = \frac{\sigma_y}{\tau_{CRSS}} \approx 3.06\ \text{(FCC, random texture)}, \qquad M\approx2.75\ \text{(BCC)} $$

- $M$ is a *geometric* factor (it is the reciprocal of the average Schmid factor), so it changes with **texture**: a strong $\langle111\rangle$ fibre texture (drawn wire, rolled sheet) raises $M$ and therefore the strength.
- The same idea explains why **polycrystals are stronger than single crystals**: not only orientation averaging but also grain-boundary constraint (each grain is prevented from deforming freely by its neighbours), which adds the Hall–Petch term.
- Conversely, a **single crystal of a superalloy** (turbine blade) is *weaker* per unit CRSS but has no grain boundaries to slide or crack, so it has far better creep and fatigue resistance — which is why blades are directionally solidified or single-crystal.

## 2.5 Dislocation reactions and sessile (Lomer) locks

![[MP - Dislocation Reaction Sessile Lock.excalidraw]]

Dislocations gliding on **non-parallel** slip planes meet along the line of intersection of those planes and can **react** to form a third dislocation. Whether the reaction happens is decided by the **strain energy**, which for a dislocation is proportional to $b^2$ per unit length:

$$ \Delta E \propto b_3^2 - (b_1^2 + b_2^2) < 0 \quad\text{(reaction is favourable)} $$

**Example (FCC).** Take $b_1 = \tfrac{a}{2}[011]$ gliding on $(1\bar{1}1)$ and $b_2 = \tfrac{a}{2}[10\bar{1}]$ gliding on $(11\bar{1})$. They meet along the intersection line of the two planes and react:

$$ \frac{a}{2}[011] + \frac{a}{2}[10\bar{1}] \longrightarrow \frac{a}{2}[110] $$

$$ b_1^2 + b_2^2 = \frac{a^2}{2} + \frac{a^2}{2} = a^2 \qquad\longrightarrow\qquad b_3^2 = \frac{a^2}{2} $$

The strain energy therefore **decreases by 50 %**, so the reaction is energetically favourable. The product $\tfrac{a}{2}[110]$ lies **along the line of intersection**, i.e. in a $\{100\}$-type plane, which is *not* a close-packed slip plane of the FCC lattice. It is therefore **immobile — sessile** (a *Lomer lock*).

**Consequence.** Dislocations gliding on the two planes **pile up** behind the lock. The pile-up produces a long-range back stress that opposes the applied stress, so a higher applied stress is needed for further deformation — this is one of the fundamental mechanisms of **work hardening** (§2.17).

![[MP2 - Lomer sessile lock formation.png|440]]

*Figure — two mobile dislocations on non-parallel $\{111\}$ planes meet along the line of intersection and react to form a sessile dislocation; further glide on either plane is blocked and dislocations pile up behind the lock.*

> [!warning] Correct indices for the classic example
> b$_1 = \tfrac{a}{2}[011]$ glides on $(1\bar11)$ and b$_2=\tfrac{a}{2}[10\bar1]$ glides on $(11\bar1)$; the intersection line of those two planes is $[110]$, and the sum $[011]+[10\bar1]=[110]$. (Both Burgers vectors must lie **in** their own plane — check with a dot product against the plane normal.) The product $\tfrac{a}{2}[110]$ is a $\langle110\rangle$ dislocation whose line lies in a $\{001\}$ plane, which is not a glide plane of the FCC lattice.

### Frank's rule — the general criterion

A reaction $\mathbf{b}_1+\mathbf{b}_2 \to \mathbf{b}_3$ is energetically favourable if the elastic energy per unit length falls. Since $E_{el}\approx\alpha G b^2$ (with $\alpha\approx0.5$–$1$),

$$ \boxed{\ b_3^2 < b_1^2 + b_2^2\ } \qquad\text{and}\qquad \mathbf{b}_3 = \mathbf{b}_1+\mathbf{b}_2\ \text{(Burgers vector conservation)} $$

Both conditions must hold: **conservation of the Burgers vector** (it is a topological charge — the closure failure of a Burgers circuit — and cannot be created or destroyed at a node) and **reduction of energy**. The reaction above reduces $b^2$ from $a^2$ to $a^2/2$: a **50 %** drop. (If the product had $b_3^2 > b_1^2+b_2^2$ the dislocations would *repel*; if equal, the reaction is neutral.)

Two useful corollaries:

- **Two dislocations with the same $\mathbf{b}$ repel** each other (a reaction to $2\mathbf{b}$ would quadruple the energy) — hence dislocations arrange themselves into low-energy arrays (tilt and twist boundaries, cells).
- **A dislocation can dissociate** (as in the Shockley partial reaction of §2.3) if the partials' energy sum is lower than the perfect dislocation's — this is why stacking faults exist at all.

### Types of sessile obstacle

| Obstacle | What it is | How it is overcome |
| --- | --- | --- |
| **Lomer (Lomer–Cottrell) lock** | Product of a reaction between dislocations on intersecting planes; $\mathbf{b}$ not in a slip plane | Cannot glide at all; requires climb (high $T$) or very high stress to recombine |
| **Cottrell atmosphere** | Solute/interstitial cloud pinning a dislocation (C, N in Fe) | Thermally activated unpinning → sharp yield point (§2.11) |
| **Precipitate particle** | Second-phase particle in the glide plane | **Shearing** (if coherent and small) or **Orowan looping** (if hard) |
| **Grain boundary / twin boundary** | Change of orientation | Slip transfer to the next grain; pile-up stress concentration |
| **Jog / forest dislocation** | Dislocation threading the glide plane | Thermal activation; jog dragging (also generates point defects) |
| **Surface oxide / coating** | Hard film | Cracking of the film; nucleation site for fatigue cracks |

### Pile-ups, stress concentration and the Hall–Petch relation

A pile-up of $n$ dislocations blocked at an obstacle multiplies the applied stress at the head of the pile-up by roughly $n$:

$$ \tau_{\text{head}} \approx n\,\tau_{\text{applied}}, \qquad n \approx \frac{\pi\,\tau_{\text{applied}}\,L}{Gb} $$

where $L$ is the pile-up length (≈ the grain radius). Yielding of the *next* grain begins when $\tau_{\text{head}}$ reaches its CRSS, $\tau^{*}$. Setting $\tau_{\text{head}}=\tau^{*}$ and $L = d/2$ gives

$$ \tau_{\text{applied}} \approx \sqrt{\frac{2Gb\,\tau^{*}}{\pi d}} \quad\Longrightarrow\quad \sigma_y = \sigma_0 + k_y d^{-1/2} $$

which is precisely the **Hall–Petch equation**. The same pile-up stress concentration, applied to a *crack* instead of a grain boundary, is the mechanism by which a slip band nucleates a cleavage crack — the link between plasticity and brittle fracture in §2.7.

> [!note] Why work hardening has three stages
> - **Stage I (easy glide)** — single slip on the primary system, long free path, low hardening rate. Dominant in single crystals oriented for single slip.
> - **Stage II (linear hardening)** — multiple slip begins; Lomer locks and forest dislocations form; hardening rate is high and nearly constant ($\theta\approx G/200$).
> - **Stage III (parabolic/dynamic recovery)** — cross-slip lets dislocations bypass obstacles, so the hardening rate falls; in polycrystals, Stage II–III behaviour is what appears as the "rising plastic branch" of the tensile curve.

## 2.6 The tensile test: specimen, machine, curve

![[MP - Engineering Stress Strain Curve.excalidraw]]

**Specimen** (standard proportions): a cylindrical or flat bar with a **reduced section** — a central **gauge length** (typically 50 mm / 2 in.) and a smaller diameter (e.g. 12.8 mm / 0.505 in.), with fillets of radius into the enlarged grip ends. The reduced section ensures that yielding and fracture occur away from the grips, in the region where strain is measured.

**Machine — Universal Testing Machine (UTM):** a **load cell** measures the applied load, an **extensometer** clipped to the gauge length measures elongation, and a **moving crosshead** applies the displacement at a controlled rate. Output: load–elongation → stress–strain.

**The engineering stress–strain curve** has four regimes:

1. **Elastic (linear) region** — slope $= E$; unloading returns the specimen to its original length.
2. **Yielding** — the onset of plastic deformation at the yield strength $\sigma_y$ (in some low-carbon steels, an upper and a lower yield point appear by the yield-point phenomenon).
3. **Strain hardening** — stress rises with strain up to the **UTS**, the maximum of the curve.
4. **Necking and fracture** — after the UTS the deformation localises in a neck; the engineering stress falls (because it is computed on the original area) until fracture.

![[MP2 - Tensile specimen geometry.png|460]]

*Figure — the standard tensile specimen: enlarged grip ends, fillet radii, a reduced-section gauge length with the smaller diameter, and the dimensions marked.*

![[MP2 - Universal testing machine.png|340]]

*Figure — the load train of a universal testing machine: fixed crosshead with load cell, specimen, extensometer clipped to the gauge, and the moving crosshead.*

### Specimen geometry and why it is standardised

- The standard round specimen has gauge diameter $d_0 = 12.8$ mm (0.505 in.) and gauge length $L_0 = 50$ mm (2 in.), i.e. $L_0 = 4d_0$; the **proportional** designation is $L_0 = 5.65\sqrt{S_0}$ (ISO), where $S_0$ is the original cross-sectional area. Flat specimens are used for sheet, with the same proportional relation.
- The **reduced section** guarantees that the stress is highest in the gauge, so the specimen yields and breaks where the extensometer is attached, not in the grips. The **fillet radius** between gauge and grip reduces the stress concentration there; too small a fillet causes grip-end failures (a classic bad-data signature).
- Because **% elongation depends on gauge length** (the neck contributes a fixed extra length, so a shorter gauge gives a larger %EL), $L_0$ must always be quoted with the ductility value. % reduction in area, measured at the neck, does not have this problem.

### The machine and the measurement chain

| Element | Function | Practical point |
| --- | --- | --- |
| **Load cell** | Converts force to an electrical signal | Must be calibrated; range chosen so the test is in the top 10–90 % of capacity for accuracy |
| **Extensometer** | Measures strain directly on the gauge (clip gauge, strain-gauge or optical) | Should be removed before fracture to avoid damage; machine crosshead displacement includes machine compliance and is *not* the specimen strain |
| **Crosshead** | Applies displacement at controlled rate | Quoted as **strain rate** ($10^{-5}$–$10^{-1}\ \text{s}^{-1}$ for quasi-static tests); faster rates raise the measured strength, especially in polymers and BCC metals |
| **Grips** | Transmit load without slipping or bending | Wedge, collet or shoulder grips; misalignment produces bending and premature failure |
| **Data acquisition** | Records load–displacement pairs | The raw curve is corrected for machine compliance and for the extensometer's own stiffness before $E$ is computed |

### Lüders bands and the yield-point phenomenon

The upper and lower yield points are not a curiosity — they are the visible signature of **solute pinning**:

1. In annealed low-carbon steel, carbon and nitrogen atoms segregate to dislocations (**Cottrell atmospheres**) because the solute is smaller/larger than the host atom and relieves elastic strain by sitting in the dislocation's stress field.
2. To move such a dislocation, it must be **torn away** from its atmosphere — this requires a stress peak (the upper yield point).
3. Once free, dislocations multiply rapidly and glide at a lower stress (the lower yield point). The plastic zone spreads as a **Lüders band** — a visible band of roughened surface that sweeps along the gauge, giving the flat plateau.
4. The band's propagation ends when the whole gauge has yielded; work hardening then takes over.

Consequences: the sharp yield point causes **stretcher strains** (flamboyant markings) in deep-drawn sheet, which is why sheet is **temper-rolled** (skin-passed) to remove it. It also means the yield stress of such a steel depends on the specimen's history, not only on composition.

> [!warning] Common exam trap
> The slope of the *engineering* stress–strain curve in the elastic region equals $E$ only if the displacement used is the *specimen's* elongation. Many textbook problems give load–extension data from a machine; you must convert using the gauge length and area, not the full specimen length.

## 2.7 Brittle and ductile behaviour: temperature, and the Yoffee diagram

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

![[MP2 - Iron curves at three temperatures.png|440]]

*Figure — the same material (iron) tested at $-200$, $-100$ and $25\ ^\circ\text{C}$: the low-temperature curve is almost linear to fracture; the room-temperature curve shows a long plastic region and a neck.*

![[MP2 - Yoffee diagram.png|380]]

*Figure — the Yoffee diagram: yield stress falls with temperature, cleavage fracture stress is nearly temperature-independent, and the intersection defines the DBTT.*

![[MP2 - Materials for low temperature service.png|520]]

*Figure — service limits of engineering alloys at low temperature: BCC carbon and low-alloy steels stop at moderate $T$, nickel steels extend lower, and FCC aluminium, nickel, titanium and austenitic stainless alloys reach liquid-helium temperature.*

### The physics behind the two curves

Why does the yield stress fall with temperature while the fracture stress does not?

- **Yield stress is thermally activated.** Dislocation motion past obstacles (Peierls barriers, solute atoms, forest dislocations) needs a *combination* of applied stress and thermal energy. At low temperature there is little thermal energy, so a higher applied stress is needed; as $T$ rises, the thermal contribution grows and $\sigma_y$ falls. The effect is strongest in BCC metals because their non-planar screw cores give a large Peierls barrier (§2.1), and weak in FCC metals where the Peierls barrier is small.
- **Cleavage fracture stress is essentially athermal.** Breaking bonds across a plane does not need diffusion or thermal activation; the stress at which a pre-existing microcrack propagates depends on the crack size and on the surface energy, both nearly independent of temperature. It is a *stress-controlled* event, so it plots as a nearly horizontal line.
- **Where they cross** is the DBTT. Below it, the material reaches the cleavage stress *before* it can generate the plastic flow needed to blunt the crack → brittle. Above it, it yields first, the plastic zone blunts the crack tip, and the material is ductile.

### Why a notch and a high strain rate shift the transition up

- A **notch** creates a triaxial stress state: the axial stress is raised by a factor $\sim$2–3 relative to the von Mises equivalent stress, while the *shear* stress that drives slip is unchanged. So the local tensile stress reaches the cleavage stress while the shear stress is still below the CRSS — fracture wins. This is why brittle behaviour is always associated with **constraint** (thick sections, notches, welds, sharp corners).
- A **high strain rate** (impact) leaves less time for thermal activation, so $\sigma_y$ rises, while the fracture stress does not — the yield curve is effectively shifted up, moving the intersection to a higher temperature.
- **Grain size** affects the two curves differently: Hall–Petch raises $\sigma_y$ (strengthening, raising DBTT) but a finer grain size also reduces the size of the *microcrack* formed by a slip-band pile-up, and the cleavage stress scales as $d^{-1/2}$ — a finer grain size improves both strength and toughness. That is why grain refinement is the only strengthening mechanism that *lowers* the DBTT.
- **Chemistry**: C, P, S, Sn, Sb, As raise the DBTT (segregation to grain boundaries weakens them, and P/Sn cause **temper embrittlement**); Ni lowers it. **Hydrogen** causes severe embrittlement at room temperature; **neutron irradiation** raises the DBTT by producing hardening and Cu-rich precipitates (a life-limiting issue for reactor pressure vessels).
- **Thickness**: a thick section cannot relax the through-thickness stress by yielding at the free surfaces, so constraint is high — large sections are more brittle than thin ones, an uncomfortable fact for scaling.

### The Charpy transition curve

Plotting absorbed energy against test temperature gives an S-shaped curve with three regions: **lower shelf** (low energy, pure cleavage, brittle), **transition** (steeply rising, mixed cleavage + ductile tearing), and **upper shelf** (high energy, fully ductile, fibrous). The DBTT is conventionally defined by a fixed energy level (**27 J** for ship steels), a fixed lateral expansion, or 50 % shear appearance. Because the transition region is very steep, a small temperature error causes a large energy error — hence the emphasis on temperature control and on reporting the *criterion* alongside the number.

Historical note: the **Liberty ship** fractures occurred at hatch corners (stress concentration) in welded (no crack-arresting riveted seams) hulls at low temperature, and are the reason impact-testing requirements entered ship-classification rules.

> [!note] Practical consequence for design codes
> Pressure-vessel and ship codes require the steel's DBTT (measured by Charpy) to lie below the minimum service temperature by a margin. Where that cannot be guaranteed — very low temperature, very thick section, or hydrogen service — the material is changed to an FCC alloy (austenitic stainless, aluminium, nickel alloy), which has no such transition.

## 2.8 Properties obtained from the tensile test

1. **Elastic modulus** and **resilience**
2. **Yield stress** (YS)
3. **Tensile strength** (TS / UTS)
4. **Elongation to failure** / **reduction in area** at fracture
5. **Toughness**

| Property | Symbol / definition | Units | Typical values | Design use |
| --- | --- | --- | --- | --- |
| Elastic modulus | $E = \sigma/\varepsilon$ (slope) | GPa | 200 (steel), 70 (Al), 380 (Al$_2$O$_3$) | Deflection, stiffness-critical parts |
| Resilience | $U_r=\sigma_y^2/2E$ | J/m³ = Pa | 0.5–2 (steels), 0.6 (Al) | Springs, snap-fits, elastic energy storage |
| Yield strength | $\sigma_y$ (0.2 % offset) | MPa | 250 (mild steel), 1500 (4340 QT) | The primary design allowable |
| Tensile strength | $\sigma_{UTS}$ (max of curve) | MPa | 400–500 (mild steel), 1800 (4340) | Specification, QC, ranking, forming loads |
| Elongation to failure | $\%EL = (l_f-l_0)/l_0\times100$ | % | 2 (PMMA), 25 (mild steel), 45 (Cu) | Ductility/warning, formability |
| Reduction in area | $\%RA = (A_0-A_f)/A_0\times100$ | % | 50–60 (steels) | Ductility, cleanliness indicator |
| Toughness (modulus) | $U_t=\int_0^{\varepsilon_f}\sigma\,d\varepsilon$ | J/m³ | $\sim10^8$ (ductile steel) | Energy absorption, crash structures |

Two practical remarks:

- **$E$ is measured from the steepest part of the curve**, which is why an extensometer (not crosshead displacement) is required — the elastic strain is only a few thousandths and machine compliance would dominate.
- **Resilience and toughness are energies per unit volume**, so they are *not* the same as the impact energy in joules measured in a Charpy test (which is energy for a whole specimen, and includes notch effects). Keep the units straight.

## 2.9 Anelasticity and viscoelasticity

- In real materials, part of the elastic strain is **time-dependent**: deformation continues slowly *after* the stress is applied, and on unloading some finite time is needed for complete recovery. This is **anelasticity**.
- Its origin is time-dependent microscopic/atomistic processes accompanying the deformation (e.g. stress-induced ordering of solute atoms, grain-boundary relaxation).
- In **metals** the anelastic component is small and usually neglected. In **polymers** it is large; the behaviour is then called **viscoelastic** (rubber-like).
- Idealised responses: **elastic** (instant strain, instant recovery), **viscous** (strain grows linearly with time under constant load, permanent), and **viscoelastic** (intermediate — retarded elastic strain plus permanent flow).

![[MP2 - Anelasticity elastic viscous viscoelastic.png|420]]

*Figure — the standard four-panel comparison: load–time cycle (top) against strain–time response (bottom) for (a) elastic, (b) anelastic/viscoelastic, (c) viscous and (d) elastomeric behaviour.*

### Anelasticity in metals: small but not always negligible

- The anelastic strain is typically $\sim0.1$ % of the elastic strain at room temperature, so it is ignored for stiffness calculations. But it is the basis of **internal-friction (damping) measurements**, which are exquisitely sensitive to point defects:
  - the **Snoek effect** — interstitial C/N pairs in BCC iron reorient under stress, giving a damping peak whose height measures the interstitial content (a non-destructive chemical analysis);
  - the **Zener (thermoelastic) peak** — heat flow between differently strained regions of a polycrystal;
  - **grain-boundary relaxation** — sliding of boundaries accommodated by diffusion, appearing at high temperature and low frequency.
- Anelasticity is why a *precisely* sized part (a quartz oscillator, a tuning fork, a precision spring) is chosen for low damping, and why high-damping alloys (Mn-Cu, cast iron) are chosen to suppress vibration and noise.

### Viscoelasticity in polymers: the same physics writ large

Because polymer deformation involves the *uncoiling and sliding of long chains* rather than the stretching of strong bonds, the "elastic" response itself is time-dependent. Three consequences, all seen in service:

1. **Creep** — under constant stress the strain continues to grow with time (chain uncoiling + chain sliding). A plastic pipe under internal pressure slowly bulges; a shelf sags.
2. **Stress relaxation** — under constant *strain* (a bolt holding a gasket, a stretched seal) the stress decays with time. Bolted plastic joints loosen.
3. **Hysteresis and damping** — on cyclic loading the unloading curve lies *below* the loading curve, so energy is dissipated per cycle (the area of the loop). This is why elastomers are good vibration isolators and why tyre rubber heats up.

The simplest models:

| Model | Configuration | Captures |
| --- | --- | --- |
| **Maxwell** (spring + dashpot in series) | $\dot{\varepsilon} = \dot{\sigma}/E + \sigma/\eta$ | Stress relaxation; steady flow under constant stress |
| **Kelvin–Voigt** (spring + dashpot in parallel) | $\sigma = E\varepsilon + \eta\dot{\varepsilon}$ | Retarded (delayed) elastic strain; no permanent flow |
| **Standard linear solid** | Both combined | Real polymer: instantaneous elastic + retarded elastic + viscous flow |

The characteristic time is the **relaxation time** $\tau = \eta/E$. The ratio of the test time to this relaxation time (the *Deborah number*) decides what you observe: fast loading → glassy, stiff, brittle response; slow loading → rubbery, compliant, flowing response. This is why a silicone rubber ball bounces (fast) but sags under its own weight overnight (slow), and why the same polymer can be a "plastic" in a car bumper and a "rubber" in a seal.

## 2.10 Poisson's ratio

When a tensile stress is applied along $z$, the specimen elongates in $z$ ($\varepsilon_z>0$) and **contracts laterally** in $x$ and $y$ ($\varepsilon_x,\varepsilon_y<0$):

$$ \nu = -\frac{\varepsilon_x}{\varepsilon_z} = -\frac{\varepsilon_y}{\varepsilon_z} \qquad (\varepsilon_x = \varepsilon_y \text{ for an isotropic material}) $$

- $\nu \approx 0.25$–$0.35$ for metals and alloys
- $\nu \approx 0.33$–$0.46$ for polymers
- $\nu = 0.5$ for a perfectly incompressible material (no volume change — rubber, and the theoretical limit); $\nu \approx 0$ for cork
- For an **isotropic** material the elastic constants are linked:

$$ E = 2G(1+\nu) $$

so a high Poisson's ratio (or a low shear modulus) means a low modulus relative to $G$. Structural materials with high $E$ usually have low $\nu$; polymers have low $E$ and high $\nu$.

![[MP2 - Poisson lateral contraction.png|420]]

*Figure — axial extension $\varepsilon_z$ accompanied by lateral contractions $\varepsilon_x=\varepsilon_y$; the ratio defines $\nu$.*

### Deriving the relations between the four elastic constants

For an isotropic solid only **two** constants are independent; the other two follow from them. Starting from the definition of $\nu$ and requiring that a hydrostatic pressure produce only a volume change:

$$ G = \frac{E}{2(1+\nu)}, \qquad K = \frac{E}{3(1-2\nu)}, \qquad \lambda = \frac{E\nu}{(1+\nu)(1-2\nu)} $$

The bulk modulus expression shows the meaning of the $0.5$ limit: as $\nu\to0.5$, $K\to\infty$ — the material becomes **incompressible**, which is exactly what a rubber is (its bulk modulus is $\sim$2 GPa while its shear modulus is $\sim$1 MPa, a ratio of $10^3$).

### Volume change under uniaxial tension

$$ \frac{\Delta V}{V} = \varepsilon_z(1-2\nu) = \frac{\sigma}{E}(1-2\nu) $$

So for $\nu = 0.3$ a tensile strain of 0.3 % produces a volume increase of only $0.12$ %, and for $\nu=0.5$ the volume is unchanged. This is the basis of the **constant-volume assumption** used in plasticity (§2.16): plastic deformation proceeds by shear, which does not change volume, so $A_0l_0=A_il_i$.

### Values, limits and the exotic cases

| Material | $\nu$ |
| --- | --- |
| Cork | $\approx 0$ |
| Ceramics, glasses | 0.2–0.3 |
| Steels | 0.27–0.30 |
| Aluminium alloys | 0.33 |
| Titanium alloys | 0.31–0.34 |
| Copper, brass | 0.33–0.35 |
| Polymers (bulk) | 0.33–0.40 |
| Elastomers | 0.49–0.499 |
| **Theoretical limits** | $-1 < \nu < 0.5$ |

- **$\nu\approx0$ (cork)** — the material does not expand sideways when compressed, which is exactly why cork is used in wine bottles: it must be compressed to seal without swelling against the glass.
- **$\nu<0$ (auxetic materials)** — engineered foams and some crystals expand laterally when stretched. They are of interest because a negative $\nu$ gives enhanced shear modulus, indentation resistance and energy absorption.
- **$\nu = 0.5$** — rubber and soft tissue; also the reason that a rubber band stretched 300 % hardly changes volume, and why rubber is a poor material for a pressure-tight seal designed to swell.

> [!note] Why $\nu$ is a *bond* property, like $E$
> $\nu$ is the ratio of lateral to axial strain, which for an isotropic solid is fixed by the geometry of bond stretching vs bond-angle bending. It is insensitive to microstructure, so alloying and cold work barely move it. It *does* vary with temperature and, in polymers, with time (viscoelastic Poisson effect) — a rubber's effective $\nu$ drifts towards 0.5 as the test becomes slower.

## 2.11 Yield stress and tensile strength

- **Yield strength** is the stress at which plastic deformation begins. Because the elastic-to-plastic transition is gradual for most metals, it is defined by the **0.2 % offset** construction: draw a line parallel to the elastic portion, starting at $\varepsilon = 0.002$; its intersection with the curve is $\sigma_y$.
- **Tensile strength (UTS)** is the maximum stress on the engineering curve; it marks the **onset of necking** and the end of uniform deformation.
- Above the UTS, deformation is **localised** — the curve descends, but this does not mean the material is softening (see true stress, §2.16).

![[MP2 - 0.2 percent offset yield strength.png|440]]

*Figure — the 0.2 % offset construction (left) and the upper/lower yield points of a low-carbon steel with the 0.2 % offset yield strength marked on the same curve (right).*

### The offset construction, precisely

1. Draw the elastic line through the origin with slope $E$.
2. Draw a line parallel to it, offset by $\varepsilon = 0.002$ (0.2 %) on the strain axis.
3. The intersection of this line with the stress–strain curve is $\sigma_y$ — the stress at which the material has accumulated 0.2 % **plastic** strain.

The offset is 0.2 % because it is just at the resolution of a good extensometer and small enough to be a sensible "engineering yield"; for polymers 2 % or 1 % offsets are used because their transitions are much broader; for materials with a sharp yield point, the upper or lower yield point is used directly (with the convention stated).

**Why an offset at all?** Most metals do not show a sharp break in slope: the transition from elastic to plastic is gradual as individual grains with favourable orientations yield one by one. A convention is therefore needed, and 0.2 % is internationally agreed.

### Factors that move the yield strength

| Factor | Effect on $\sigma_y$ | Reason |
| --- | --- | --- |
| Lower temperature | Increases (strongly in BCC, weakly in FCC) | Thermal activation assists obstacle bypass |
| Higher strain rate | Increases | Less time for thermal activation |
| Finer grain size | Increases ($d^{-1/2}$) | Hall–Petch (§2.5) |
| More alloying / solutes | Increases | Solid-solution hardening, atmospheres |
| Cold work | Increases | Dislocation density $\rho$, forest hardening |
| Precipitates | Increases (peak aged) | Orowan looping / particle shearing |
| Porosity, cracks | Decreases | Reduced load-bearing section, stress concentration |
| Hydrostatic pressure | Slight increase in tension tests | Suppresses void growth |

### Tensile strength: what it does and does not mean

- $\sigma_{UTS}$ is the **maximum engineering stress**, and its significance is *geometric*: it marks the point where the rate of work hardening exactly balances the rate of area reduction (Considère condition, §2.15). It is not a "breaking stress" — the stress at fracture is *lower* on the engineering curve.
- It is nevertheless the most-quoted strength number because it is easy to measure, reproducible, and it correlates with hardness and with fatigue strength. It is used for **specifications and quality control** and for estimating working loads in forming operations.
- **Design is based on yield, not UTS**, because at the UTS the material has already deformed by many percent; a component at UTS is already unserviceable. The ratio $\sigma_{UTS}/\sigma_y$ is the **strain-hardening capacity**, a measure of the safety margin between first yield and final failure.
- For **brittle materials** there is no yield, so the "strength" quoted is the fracture stress (flexural strength for ceramics, §3.1). For **polymers**, the "yield point" may be a maximum followed by **strain softening** (necking and cold drawing), so the curve shape needs care in interpretation.

> [!note] Tension–compression asymmetry
> Some materials yield at different stresses in tension and compression — cast iron, many polymers, glasses and geological materials. For polymers and foams this is a real effect (chain tension vs buckling of struts); for metals it is usually small. It matters because a "yield strength" measured in tension may not apply in a compressive design, and because bending, which has both, produces a shifted neutral axis.

## 2.12 Resilience and toughness

| | **Resilience** | **Toughness** |
| --- | --- | --- |
| Area | Under the curve **up to yield** | Under the **whole curve to fracture** |
| Meaning | Energy absorbed per unit volume in the elastic range; ability to store energy and spring back | Energy absorbed per unit volume before fracture; resistance to fracture |
| Formula | $U_r = \int_0^{\varepsilon_y}\sigma\,d\varepsilon = \frac12\sigma_y\varepsilon_y = \dfrac{\sigma_y^2}{2E}$ | $U_t = \int_0^{\varepsilon_f}\sigma\,d\varepsilon$ (no simple closed form) |
| Units | J/m³ | J/m³ |
| Favoured by | **High yield strength, low modulus** | **High strength *and* high ductility** |

A tough material needs both: a ceramic may have huge strength but negligible ductility → *low* toughness. This is why "toughness" and "strength" are not the same design property.

![[MP2 - Resilience and toughness areas.png|400]]

*Figure — the modulus of resilience is the small triangular area up to yield; the modulus of toughness is the whole area under the curve to fracture.*

### Resilience in detail

The area of the elastic triangle is

$$ U_r = \frac12\sigma_y\varepsilon_y = \frac{\sigma_y^2}{2E} \qquad [\text{J/m}^3] $$

This is the **modulus of resilience**; the *proof resilience* is the same quantity multiplied by the volume of the part (total energy stored, in J). Design implications:

- **Springs** should be made of high-yield, low-modulus material — hence spring steels (high $\sigma_y$) or, for non-metallic springs, polymers/composites (low $E$).
- Because $U_r\propto\sigma_y^2$, doubling the yield strength *quadruples* the energy stored — a far stronger lever than any change in modulus.
- Resilience is the relevant property for anything that must "bounce back" without permanent set: leaf springs, snap-fits, diaphragms, buffer springs, and the elastic range of a golf ball.

### Toughness in detail — three different quantities share the name

| "Toughness" | Symbol / units | Definition | When used |
| --- | --- | --- | --- |
| **Modulus of toughness** | $U_t$, J/m³ | Area under the *whole* $\sigma$–$\varepsilon$ curve to fracture | Comparing materials, crash energy absorption per volume |
| **Impact (notch) toughness** | J (or J/cm²) | Energy absorbed by a standard notched specimen in Charpy/Izod | Specification and DBTT determination (§2.7) |
| **Fracture toughness** | $K_{Ic}$, MPa·m$^{1/2}$ (or $G_{Ic}$, J/m²) | Resistance to propagation of a pre-existing sharp crack | Damage-tolerant design, fitness-for-service assessment |

The last of these is the one used in modern design codes, because the first two do not account for the *size* of the flaw. The relationship between them is

$$ K_{Ic} = Y\sigma\sqrt{\pi a} $$

where $a$ is the crack length and $Y$ a geometry factor of order 1. It says the *stress* a cracked body can carry falls as $1/\sqrt{a}$: doubling the crack length halves the allowable stress. This is the single most important equation behind "damage tolerance" design in aircraft and pressure vessels, and it explains why the same steel can be tough in a small specimen and brittle in a large structure.

Typical magnitudes:

| Material | $U_r$ (kJ/m³) | Modulus of toughness (MJ/m³) | $K_{Ic}$ (MPa·m$^{1/2}$) | Charpy energy (J) |
| --- | --- | --- | --- | --- |
| Mild steel | 150 | 80–100 | 100–150 | $>200$ (upper shelf) |
| 4340 quenched & tempered | 5500 | 120–180 | 40–60 | 20–40 |
| Aluminium 2024-T3 | 600 | 20–30 | 30–40 | — |
| Alumina | 100 | 0.1 | 3–4 | $\sim$0.02 |
| Glass | 35 | 0.03 | 0.7–1 | $\sim$0.01 |
| PMMA | 800 | 0.5–1 | 1–1.5 | — |
| HDPE | 450 | 10–30 | 2–4 | — |

> [!warning] The three "toughnesses" do not agree with each other
> Note that 4340 has a *higher* modulus of toughness than mild steel (its strength more than compensates for its lower ductility), yet it has a **lower** fracture toughness and a **much lower** Charpy energy. The modulus of toughness integrates the whole curve, so it rewards strength; $K_{Ic}$ and impact energy are dominated by the *local* fracture process, so they reward ductility and purity. A high-strength steel can therefore absorb a lot of energy in uniform tension and still fail catastrophically from a small crack. **When a specification says "tough", it is almost always referring to $K_{Ic}$ or impact energy, not to the area under the tensile curve.**

The genuine trade-off is between **strength and $K_{Ic}$**: within one alloy family, every increment of strength (by alloying, cold work or ageing) reduces the fracture toughness, because the plastic zone that blunts a crack shrinks. That is the central compromise of high-strength alloy design.

## 2.13 Tensile curves for polymers

Three characteristic shapes:

- **Brittle** — linear elastic to a sudden break, very small strain (PMMA, PS at room temperature).
- **Plastic** — yield, then cold drawing with a long plateau, then strain hardening and fracture (many thermoplastics).
- **Elastomeric** — highly elastic: enormous recoverable strain (several hundred %), low modulus, no permanent set (rubbers/vulcanised elastomers).

![[MP2 - Polymer tensile curves.png|440]]

*Figure — the three characteristic polymer curves: brittle (PMMA/PS), plastic with cold drawing (many thermoplastics) and elastomeric (rubber).*

![[MP2 - Polymer tensile curve annotated.png|400]]

*Figure — the annotated plastic-type polymer curve: Young's modulus from the initial slope, the yield point (upper yield), the drop into cold drawing, the draw ratio, and the tensile strength at break.*

### What each shape means physically

- **Brittle** (PMMA, PS, epoxy at room temperature) — below the glass transition temperature $T_g$ the chains are frozen; the material behaves like a stiff glass. Failure is by **crazing** (micro-cavitation ahead of the crack) followed by crack growth; the fracture surface is mirror-smooth near the origin with **hackle** markings further out. Strain to failure is a few percent.
- **Plastic** (HDPE, PP, PET, nylon, PC) — above $T_g$ but below $T_m$ (or in a semicrystalline polymer), chains can slide past one another. The curve shows a **yield maximum**, then a drop (strain softening) as a neck forms, then a long **cold-drawing plateau** at nearly constant stress while the neck propagates, and finally **strain hardening** as the chains become aligned, followed by fracture.
- **Elastomeric** (natural rubber, silicone, vulcanised EPDM) — lightly cross-linked chains above $T_g$. Deformation uncoils the chains, which is an **entropy** effect: the chain wants to return to a random coil, so the restoring force *increases* with extension (the curve rises steeply at high strain). Modulus is very low (1–10 MPa), failure strain huge (300–800 %), and recovery essentially complete. The energy lost per cycle (hysteresis) makes rubber a good damper.

### The strong dependence on temperature and rate

For a polymer the same specimen can show all three types of curve:

$$ T \ll T_g:\ \text{brittle} \qquad T \approx T_g:\ \text{leathery/plastic} \qquad T \gg T_g\ (\text{cross-linked}):\ \text{rubbery} $$

Raising the test **rate** is equivalent to lowering the temperature (time–temperature superposition): a plastic bag that stretches slowly and gracefully will shatter if hit sharply. This is why polymer design data must always be quoted at a specified temperature *and* rate, and why "the same" PVC can be a rigid pipe or a flexible hose depending on plasticiser content.

| Typical values (room temperature) | $E$ (GPa) | Yield stress (MPa) | Elongation (%) |
| --- | --- | --- | --- |
| PS (brittle) | 3.0 | — | 2–3 |
| PMMA | 3.0 | 70 | 3–5 |
| Nylon 6,6 | 3.0 | 80 | 60 |
| HDPE | 1.0 | 30 | 300–800 |
| PC | 2.4 | 65 | 100 |
| Natural rubber | 0.005 | — | 500–800 |

## 2.14 Measures of strength and ductility

$$ \sigma = \frac{F}{A_0} \qquad\qquad \varepsilon = \frac{l_i - l_0}{l_0} $$

$$ \%EL = \frac{l_f - l_0}{l_0}\times 100 \qquad\qquad \%RA = \frac{A_0 - A_f}{A_0}\times 100 $$

- **Yield strength and tensile strength** are measures of **strength**.
- **Fracture strength is not used as a design criterion** — it is highly scattered, depends on flaws, and a design that allows stresses to approach fracture is already unsafe. Design is based on yield (with a factor of safety).
- **% elongation to failure** and **% reduction in area** are measures of **ductility**. Reduction in area is often the more sensitive indicator, because it is measured at the neck where deformation is concentrated.

### The gauge-length dependence of %EL

The total elongation is the sum of a *uniform* strain over the gauge and a *localised* strain concentrated in the neck. The neck contributes an approximately fixed length ($\sim\beta\sqrt{A_0}$), so its *relative* contribution grows as the gauge length shrinks. Empirically (Barba's law):

$$ \Delta L = \beta\sqrt{A_0} + \varepsilon_u L_0 \qquad\Longrightarrow\qquad \%EL \text{ increases as } L_0 \text{ decreases} $$

Hence a "20 % elongation" for a 25 mm gauge is not the same material property as "20 %" for a 50 mm gauge. The **Russell–Bailey** and **Oliver** relations are variants of the same idea. %RA has no such ambiguity, which is why it is preferred for comparing materials and why specifications quote both.

### Ductility in design

- **Ductility is the warning system.** A ductile material at a stress concentration yields locally, redistributes load, and deforms visibly before breaking. A brittle one cracks. Codes therefore specify minimum elongation (e.g. $\ge$ 20 % for structural steel, $\ge$ 5 % for many pressure-vessel alloys).
- **Ductility is a processing requirement.** Rolling, forging, drawing and deep-drawing all need large uniform elongation; formability is a separate (but related) property, measured by the forming-limit diagram, and it is controlled by $n$ (§2.18) and by the strain-rate sensitivity $m$.
- **Ductility is not monotonic in temperature or purity.** Increasing strength by cold work or by ageing consumes ductility. Impurities (S, P) and inclusions reduce it sharply — a "clean steel" is a ductile steel.
- **Brittleness** is often quantified as $\%RA < 5$ or as the absence of a yield point; for ceramics the Weibull modulus (§3.2) plays the same role by describing the scatter in strength.

| Material class | $\%EL$ at 50 mm gauge | Character |
| --- | --- | --- |
| Ceramics, glasses | $\sim0$ (elastic only) | perfectly brittle |
| Cast iron (grey) | $<1$ | brittle (flakes) |
| Tool steel (hardened) | 1–3 | low ductility |
| High-strength Al alloy | 10–12 | moderate |
| Structural steel | 20–30 | ductile |
| Austenitic stainless | 40–60 | very ductile |
| Copper, gold (annealed) | 45–60 | very ductile |
| Superplastic alloy | 300–1000 | exceptional ($m>0.3$) |

> [!note] Why fracture strength is not used as a design criterion
> The stress at fracture is (i) measured after the specimen has already failed to be useful, (ii) strongly dependent on the largest flaw, so it scatters by a factor of 2–10 between nominally identical brittle specimens, and (iii) reduced by any stress concentration or by the size of the component. Designing to fracture strength would mean designing to the point of no return. Design therefore uses **yield strength with a safety factor** (for ductile materials) or **fracture toughness with a flaw-size inspection limit** (for brittle/high-strength materials).

## 2.15 Necking

After the UTS the cross-section decreases locally — a **neck** forms, and further deformation is confined to it. Because engineering stress uses $A_0$, the curve falls even though the *true* stress in the neck continues to rise. In **semicrystalline polymers** the neck is *stable*: it draws down and then propagates along the gauge length (cold drawing), giving a long plateau rather than a fall.

![[MP2 - Necking in tension.png|420]]

*Figure — the onset of necking at the tensile strength: the load maximum coincides with the point where the area reduction outruns the work hardening.*

![[MP2 - Neck propagation semicrystalline polymer.png|400]]

*Figure — in a semicrystalline polymer the neck stabilises and propagates along the gauge length (cold drawing), producing a long plateau instead of a descending branch.*

### The Considère criterion — why necking starts exactly at the UTS

Necking begins when the *load* stops increasing, i.e. $dP=0$. With $P = \sigma_T A_i$ and constant volume ($A_i l_i$ = const, so $dA/A = -d\varepsilon_T$):

$$ dP = \sigma_T\,dA + A\,d\sigma_T = 0 \quad\Longrightarrow\quad \frac{d\sigma_T}{d\varepsilon_T} = \sigma_T $$

$$ \boxed{\ \text{Necking begins when}\ \ \dfrac{d\sigma_T}{d\varepsilon_T} = \sigma_T\ } $$

**Graphical form (the Considère construction):** on a plot of true stress against true strain, necking begins where the straight line drawn from the origin is tangent to the curve — that is, where the *slope* of the curve equals the *secant* from the origin, $\sigma_T/\varepsilon_T$. Two important consequences:

1. **Necking is a geometric instability, not a material failure.** A material with no work hardening would neck immediately at yield; a strongly work-hardening material resists localisation. Ductility in tension is therefore *set by the work-hardening rate*.
2. **Combining with Hollomon**, $\sigma_T = K\varepsilon_T^n$, gives $d\sigma_T/d\varepsilon_T = nK\varepsilon_T^{n-1} = n\sigma_T/\varepsilon_T$, so the criterion becomes
$$ n = \varepsilon_{T,u} $$
i.e. **the strain-hardening exponent equals the true uniform strain at the UTS.** This is one of the most examinable results in the whole topic, and it means that a tensile test gives $n$ directly as the true strain at maximum load.

### Strain-rate sensitivity and neck stability

A neck is stable if the material in the neck becomes *stronger in strain rate* as it thins — positive strain-rate sensitivity,

$$ \sigma = C\dot{\varepsilon}^{m} $$

With $m>0$ the rapidly deforming neck region hardens and resists further localisation. This is why:

- **Superplastic materials** ($m\approx0.3$–$0.5$, fine grain size, $T>0.5T_m$) can stretch to 300–1000 % without necking — they are used to form complex sheet shapes by blow forming;
- **cold-drawn polymers** show a stable neck, because drawing is a rate-sensitive orientation process;
- raising the test temperature or slowing the rate (both raising the *effective* $m$) delays necking and increases elongation.

### The triaxial stress state in the neck

Once a neck forms, the necked region is constrained by the (still cylindrical) shoulders. This builds up **radial and hoop stresses** in addition to the axial one — a **triaxial tension** state. The axial stress computed as $F/A_{\text{neck}}$ therefore *overestimates* the true flow stress. Bridgman's correction is

$$ \sigma_{\text{corr}} = \frac{\sigma_T}{\left(1+\dfrac{2R}{a}\right)\ln\!\left(1+\dfrac{a}{2R}\right)} $$

where $a$ is the neck radius and $R$ the radius of curvature of the neck profile. The correction is small (a few %) at the start of necking and grows as the neck sharpens — this is exactly the gap between the "true" and "corrected" curves in §2.18. The same triaxiality is what makes notched bars brittle (§2.7): constraint raises the maximum principal stress without raising the shear stress that would relieve it by yielding.

## 2.16 True stress and true strain

![[MP - True vs Engineering Stress Strain.excalidraw]]

Engineering quantities are referred to the *original* area and length. **True** quantities are referred to the *instantaneous* values:

$$ \sigma_T = \frac{F}{A_i} \qquad\qquad \varepsilon_T = \int_{l_0}^{l_i}\frac{dl}{l} = \ln\frac{l_i}{l_0} $$

Assuming **constancy of volume** during plastic deformation ($A_0 l_0 = A_i l_i$):

$$ \sigma_T = \sigma(1+\varepsilon) \qquad\qquad \varepsilon_T = \ln(1+\varepsilon) $$

- The volume-constancy assumption is valid **only up to the onset of necking** — beyond that the deformation is no longer uniform.
- True strain in compression is negative, and $\varepsilon_T$ is **additive** whereas engineering strain is not: two successive true strains of $0.5$ simply add to $1.0$, but the engineering strains of the same two steps ($0.5$ each, i.e. $l_0\to1.5l_0\to2.25l_0$) combine to a total engineering strain of $1.25$, not $1.0$.
- Also useful: $\varepsilon_T = \ln(A_0/A_i)$.
- **After necking the two curves diverge completely**: the engineering curve falls while the true curve keeps rising. The fall of the engineering curve is a *geometric* artefact, not softening.

![[MP2 - True corrected engineering curves.png|440]]

*Figure — engineering, true and corrected true stress–strain curves for a ductile metal: the engineering curve peaks and falls after the UTS, the true curve rises monotonically, and the corrected curve lies slightly below the true one in the necked region.*

### Where the conversions come from

Starting from constancy of volume during plastic flow, $A_0l_0=A_il_i \Rightarrow A_i = A_0l_0/l_i$:

$$ \sigma_T = \frac{F}{A_i} = \frac{F}{A_0}\cdot\frac{A_0}{A_i} = \sigma\cdot\frac{l_i}{l_0} = \sigma(1+\varepsilon) $$

$$ \varepsilon_T = \int_{l_0}^{l_i}\frac{dl}{l} = \ln\frac{l_i}{l_0} = \ln(1+\varepsilon) = \ln\frac{A_0}{A_i} $$

Both follow from the same assumption and are therefore valid only while deformation is **uniform** (before necking).

### Why true strain is the "right" measure

- **Additivity**: strain increments multiply lengths, so logarithms add. Drawing a wire from $l_0\to l_1\to l_2$ gives $\varepsilon_T = \ln(l_1/l_0)+\ln(l_2/l_1)=\ln(l_2/l_0)$. Engineering strains do not add: the two steps $l_0\to1.5l_0\to2.25l_0$ are *each* an engineering strain of $0.5$, yet the total engineering strain is $1.25$, whereas the true strains add exactly, $\ln 1.5+\ln 1.5=\ln 2.25=0.811$.
- **Symmetry in tension/compression**: reversing a true strain gives $-\varepsilon_T$ exactly; reversing an engineering strain of $+0.5$ gives $-0.33$, not $-0.5$. True strain treats the two directions consistently.
- **Thickness reduction in rolling** is $\varepsilon_T = \ln(t_0/t_f)$, the standard formula in metal-forming analysis; a 50 % reduction in thickness is $\varepsilon_T = 0.693$, not 0.5.
- **Large-strain equivalence**: for a general 3D deformation one uses the **effective (von Mises) strain** $\bar\varepsilon = \sqrt{\tfrac23(\varepsilon_1^2+\varepsilon_2^2+\varepsilon_3^2)}$ in the same way as the von Mises stress, so that a multiaxial forming operation can be compared with a uniaxial flow curve.

### True fracture stress

At fracture, the true stress is

$$ \sigma_{T,f} = \frac{F_f}{A_f} $$

where $A_f$ is the *measured* fracture area. This is much larger than the engineering fracture stress (for a ductile steel, $\sigma_f\approx0.7\sigma_{UTS}$ while $\sigma_{T,f}\approx1.5$–$2\sigma_{UTS}$), and the true fracture strain is

$$ \varepsilon_{T,f} = \ln\frac{A_0}{A_f} = \ln\frac{100}{100-\%RA} $$

which is a gauge-length-independent measure of ductility — the natural companion to %RA.

> [!warning] Do not use these conversions after necking
> Once the neck forms, the strain is no longer uniform across the gauge, so "the" true stress and "the" true strain of the specimen are ill-defined; $F/A_{\text{neck}}$ gives a *local* stress that overestimates the flow stress because of triaxiality. That is precisely why the "corrected" curve exists.

## 2.17 Work hardening / strain hardening

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

### The quantitative link to dislocation density

The flow stress is related to the *total* dislocation density by the Taylor relation

$$ \tau = \tau_0 + \alpha G b\sqrt{\rho}, \qquad \alpha \approx 0.3\text{–}0.5 $$

Since $\rho$ increases roughly linearly with plastic strain in Stage II, $\tau\propto\sqrt{\varepsilon}$ — which is close to the observed parabolic hardening. This is the cleanest statement of the microscopic origin: **work hardening is the resistance of a dislocation population to its own motion.**

| Process | Effect on $\rho$ (m$^{-2}$) |
| --- | --- |
| Well-annealed single crystal | $10^{8}$–$10^{10}$ |
| Annealed polycrystal | $10^{10}$–$10^{12}$ |
| Cold worked 10 % | $10^{13}$–$10^{14}$ |
| Heavily deformed (90 %) | $10^{15}$–$10^{16}$ |
| Theoretical maximum (cell walls) | $\sim10^{17}$ |

### Why dislocations obstruct each other

1. **Forest hardening** — a dislocation gliding on its plane must cut through the dislocations threading that plane ("forest"). Each intersection creates a jog, costing energy.
2. **Junction formation** — two dislocations on intersecting planes can react to form a segment that is not glissile (**Lomer locks**, §2.5). Junctions are strong obstacles.
3. **Pile-ups at obstacles** — grain boundaries, twin boundaries, particles, and previously formed locks. The back stress from a pile-up reduces the effective stress on the source.
4. **Cell/subgrain structure** — at large strains dislocations arrange into dense walls surrounding nearly dislocation-free cells, and the cell size sets the mean free path.
5. **Twin boundaries** — in low-SFE metals (brass, TWIP steels) deformation twins subdivide the grains and add barriers, giving exceptionally high hardening rates.

### Consequences and practical aspects

- **Uniform elongation is controlled by the hardening rate**: high hardening delays the Considère instability, so high-$n$ materials stretch further. This is why annealed copper and 304 stainless steel can be deep-drawn and why tempered 4340 cannot.
- **The Bauschinger effect**: after tensile pre-strain, the compressive yield stress is *lower* than the tensile flow stress — the internal back stresses from pile-ups assist reverse flow. This matters in cyclic loading, in spring making, and in any forming operation with reversed strain.
- **Recovery and recrystallisation**: annealing removes work hardening in two stages — *recovery* (dislocation rearrangement and annihilation, small property change) then *recrystallisation* (new strain-free grains nucleate and grow, hardness drops to the annealed value, ductility is restored). The temperature at which this happens in one hour is the **recrystallisation temperature**, roughly $0.3$–$0.4T_m$.
- **Hot working vs cold working**: above the recrystallisation temperature, hardening is continuously removed by dynamic recovery/recrystallisation, so enormous strains are possible with low forces (rolling, forging, extrusion). Below it, the work hardening accumulates (cold rolling, wire drawing) and is used deliberately to strengthen the product.
- **Work hardening is limited**: it cannot exceed the fracture strength, so a heavily drawn wire eventually fails; and it consumes all the ductility, so a cold-rolled sheet may be too brittle to bend.

## 2.18 The plastic flow curve and the Hollomon equation

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

![[MP2 - Hollomon n and K values.png|460]]

*Figure — the table of $n$ and $K$ values for various alloys (Callister, Table 7.4); note that $n$ varies by almost a factor of four between annealed copper and tempered 4340 steel.*

### Why the log–log plot is a straight line

Taking logarithms of $\sigma_T=K\varepsilon_T^{\,n}$:

$$ \log\sigma_T = \log K + n\log\varepsilon_T $$

so a plot of $\log\sigma_T$ vs $\log\varepsilon_T$ has slope $n$ and intercept $\log K$ at $\varepsilon_T=1$ — which is why $K$ is called the *strength coefficient* and is quoted in MPa (or psi). $K$ is *not* a strength in the design sense; it is the extrapolated stress at unit true strain, and it is usually much larger than the UTS.

### The link to the UTS and to Considère

Combining the Hollomon law with the Considère condition (§2.15) gives three useful results:

$$ \varepsilon_{T,u} = n \qquad\text{(true strain at the UTS)} $$

$$ \sigma_{UTS} = K\left(\frac{n}{e}\right)^{n}, \qquad e = 2.718 $$

$$ \sigma_{T,u} = K n^{n} $$

The first is the most useful in practice: **read $n$ straight off the tensile curve** as the true strain at maximum load. The second lets a specification be checked from $K$ and $n$ without a full curve, and it shows why a high-$n$ material has a UTS that is a large fraction of $K$, while a low-$n$ material's UTS is much lower than $K$.

### Worked example

> A steel has $K=600$ MPa and $n=0.21$. Estimate the UTS, the true stress at the UTS, and the flow stress at a true strain of 0.10.

- UTS: $\sigma_{UTS} = 600\,(0.21/e)^{0.21} = 600 \times (0.0773)^{0.21}$.
  $\ln(0.0773) = -2.560$, times $0.21 = -0.5376$, so $(0.0773)^{0.21}=e^{-0.5376}=0.584$. Hence $\sigma_{UTS}\approx 350$ MPa.
- True stress at UTS: $\sigma_{T,u} = 600\,(0.21)^{0.21}$. $\ln 0.21=-1.561$, times 0.21 = $-0.3278$, so $e^{-0.3278}=0.720$ → $\sigma_{T,u}\approx432$ MPa. (Check: $\sigma_T=\sigma(1+\varepsilon)$ at necking → $350\times1.21 = 424$ MPa ✓.)
- Flow stress at $\varepsilon_T=0.10$: $\sigma_T = 600(0.10)^{0.21} = 600\times e^{0.21\ln0.1} = 600 e^{-0.4835}=600\times0.6166\approx370$ MPa.

Note how flat the flow curve is: ten-fold strain increases the flow stress by only a factor of $\sim$1.6. That is what $n\approx0.2$ means.

### Where Hollomon fails, and what is used instead

- **Below the yield point** the equation is not valid (it predicts zero stress at zero strain); it applies only from the onset of plastic flow.
- **Double-$n$ behaviour**: many metals (particularly austenitic stainless and some aluminium alloys) show two slopes on the log–log plot — a low $n$ at small strains (easy glide, planar slip) and a higher $n$ at large strains (twinning, multiple slip). A single $n$ then underestimates large-strain formability.
- **Other empirical laws**:
  $$ \text{Ludwik: } \sigma_T=\sigma_0+K\varepsilon_T^{\,n}, \qquad \text{Swift: } \sigma_T=K(\varepsilon_0+\varepsilon_T)^{n}, \qquad \text{Voce: } \sigma_T=\sigma_{sat}-(\sigma_{sat}-\sigma_0)e^{-\varepsilon_T/\varepsilon_c} $$
  The Voce form describes **saturation** of work hardening (dynamic recovery), which Hollomon never does.
- **Strain-rate sensitivity** is added as $\sigma_T = K\varepsilon_T^{\,n}\dot{\varepsilon}^{\,m}$, with $m\approx0.01$–0.05 for metals at room temperature and $m\approx0.3$–0.5 for superplastic alloys.

### Why $n$ matters commercially

$n$ is the single best predictor of **stretch formability**: a high-$n$ sheet resists local thinning (the Considère criterion is pushed to larger strain), so it can be deep-drawn and stretch-formed without splitting. That is why automotive sheet is specified by $n$ (and by the normal plastic-strain ratio $r$, the Lankford coefficient, which measures resistance to through-thickness thinning). It also explains why **annealed** sheet is used for forming and then **painted/baked or work-hardened** in service.

## 2.19 Elastic recovery after plastic deformation

- When the load is released during a test, the specimen unloads **parallel to the elastic line**; the recovered strain is $\sigma/E$.
- This **elastic strain recovery** is why a formed sheet springs back after the tool is removed — the practical reason for over-bending in press forming.
- On **reloading**, the material yields at approximately the *previous* maximum stress — direct evidence of work hardening.
- An elastic recovery also occurs at fracture, so the measured elongation contains a small elastic contribution.

![[MP2 - Elastic recovery on unloading.png|420]]

*Figure — unloading from a point on the plastic branch runs parallel to the elastic line; the horizontal distance between the loading and unloading curves is the elastic strain recovery. Reapplying load retraces the same line and yields again near the previous maximum stress.*

### Springback, quantitatively

If a sheet is bent to a radius $R_0$ and the load is released, the elastic recovery is

$$ \frac{1}{R_f} = \frac{1}{R_0} - \frac{3\sigma_y}{E\,t}\quad\text{(approximate, thin sheet of thickness } t\text{)} $$

so the final radius is larger than the tool radius and the part "opens up". Practical consequences and remedies:

- **Over-bending** — the die is machined with a smaller radius than the target, so that springback lands the part on dimension.
- **Bottoming / coining** — pressing the sheet against the die so that the through-thickness stress state becomes compressive everywhere, suppressing the recovery.
- **Stretch forming** — deforming in tension so that the whole section is yielded in one direction; the residual stress gradient is smaller.
- **Compensation in high-strength steels and aluminium** — springback scales as $\sigma_y/E$, so it is far worse for high-strength steel ($\sigma_y/E\approx0.008$) than for mild steel ($\approx0.0012$). This is a real manufacturing problem for automotive AHSS and a reason hydroforming and hot forming are used.

### Residual stresses

Because unloading is elastic and non-uniform (the outer fibres of a bent sheet have yielded more than the neutral axis), the final part retains a **residual stress** pattern: tension on one surface, compression on the other. Consequences — both useful and dangerous:

- **Distortion** on machining: removing material unbalances the residual stress and the part warps.
- **Fatigue and stress-corrosion cracking**: tensile residual stresses at a surface add to service stress and accelerate crack growth.
- **Beneficial residual stress**: **shot peening**, **surface rolling** and **autofrettage** (pre-pressurising a cylinder so the bore is left in compression) deliberately introduce compressive surface stress, which dramatically improves fatigue life. **Tempered glass** works the same way — the surface is in compression, so a crack will not propagate until the compression is overcome.

> [!note] Reloading, and why it matters
> On reloading, the curve follows the unloading line and yields again near the previous maximum stress. This is *proof* of work hardening with no microscopy needed, and it is the basis of **proof testing**: a pressure vessel is pressurised above its service pressure (but below yield) so that any part that survives has been proven, and the yield strength has been raised slightly by the pre-strain. The same effect is the **Bauschinger effect** in reverse — after tensile pre-strain, the compressive yield strength is reduced.

> [!tip] Exam pointer — Part II
> The most examined items are: the Schmid factor derivation and $\sigma_y = \tau_{CRSS}/m$ with $m_{\max}=0.5$; the true vs engineering conversion $\sigma_T=\sigma(1+\varepsilon)$, $\varepsilon_T=\ln(1+\varepsilon)$; $U_r = \sigma_y^2/2E$; the Hollomon equation and $n$; and the $b^2$ energy criterion for a dislocation reaction. The newer additions worth being able to state in one line each: the Frenkel estimate $\tau\approx G/2\pi$ vs the measured $10^{-4}G$; the Peierls stress falling exponentially with core width; the Considère condition and $n=\varepsilon_{T,u}$; the Taylor factor $M\approx3.06$; and the Hall–Petch pile-up derivation.

---

# 3. Mechanical Properties — III

## 3.1 Testing brittle materials: the three-point bend test

![[MP - Three Point Bending.excalidraw]]

**Why not a tensile test?** Ceramics are hard and brittle: they cannot easily be machined into a waisted tensile specimen, gripping introduces stress concentrations that cause premature fracture, and the tensile strength is only about **one-tenth** of the compressive strength. In bending, only a small specimen is needed and no gripping is involved.

**Setup.** A rectangular (or circular) bar rests on **two support pins** a distance $L$ apart and is loaded at the **mid-span** — three contact points. The **top surface is in compression** and the **bottom surface in tension**. Because ceramics are far weaker in tension, **fracture always initiates on the tensile (bottom) face**; the test therefore measures a *tensile* strength, but in a convenient geometry.

Bending stress from simple beam theory:

$$ \sigma = \frac{Mc}{I} $$

with $M_{\max} = \dfrac{F L}{4}$ at mid-span. Hence, for the two standard cross-sections:

$$ \sigma_{fs} = \frac{3F_f L}{2bd^2} \quad\text{(rectangular, width } b,\ \text{depth } d) \qquad\qquad \sigma_{fs} = \frac{F_f L}{\pi r^3} \quad\text{(circular, radius } r) $$

where $F_f$ is the fracture load.

**Names.** The stress at fracture in this test is variously called the **flexural strength**, **modulus of rupture**, **fracture strength** or **bend strength** — all the same quantity.

![[MP3 - Three point bending test.png|420]]

*Figure — the three-point bend arrangement: a bar on two support pins, loaded at mid-span, with the top surface in compression and the bottom surface in tension; the two standard cross-sections (rectangular and circular) are also shown.*

### Where the formula comes from

For a beam of rectangular section, width $b$ and depth $d$, the second moment of area about the neutral axis is

$$ I = \frac{bd^3}{12}, \qquad c = \frac{d}{2}, \qquad M_{\max} = \frac{FL}{4} $$

so

$$ \sigma = \frac{Mc}{I} = \frac{(FL/4)(d/2)}{bd^3/12} = \frac{3FL}{2bd^2} $$

For a circular section of radius $r$: $I = \pi r^4/4$, $c=r$, giving

$$ \sigma = \frac{(FL/4)r}{\pi r^4/4} = \frac{FL}{\pi r^3} $$

Both assume: (i) the beam is elastic, (ii) deflections are small, (iii) shear stresses are negligible (span-to-depth ratio $L/d\ge8$–$10$; for ceramics $L/d\approx4$–$8$ is usual, and a shear correction can be applied), and (iv) the material is homogeneous and isotropic.

### Why bending instead of tension for ceramics

1. **Specimen preparation** — a simple rectangular bar can be cut and ground; a waisted tensile specimen of a hard, brittle ceramic is difficult and expensive to machine without introducing flaws.
2. **Gripping** — a tensile specimen must be gripped, and every grip contact introduces a stress concentration that will fracture a brittle material at the grip rather than in the gauge. Bending needs only support pins.
3. **Strength asymmetry** — ceramics are much stronger in compression than in tension (typically $\sigma_{comp}\approx10\,\sigma_{tens}$ for glasses and porosities), so a tensile test wastes the material's capability; the bend test puts only the bottom fibre in tension, which is where failure occurs anyway.
4. **Small specimens** — components are often small; bend bars can be made from available material.

**The cost**: only a small volume of the specimen is at the maximum stress, so the test samples a small population of flaws. Because ceramic strength is **flaw-controlled and highly scattered** (a Weibull distribution, §3.2), the flexural strength of a small bend bar is systematically *higher* than the tensile strength of a large component. This is a size effect, not a materials effect, and it must be allowed for in design.

### Four-point bending

In four-point bending the load is applied through two inner rollers, so the central span experiences a **constant bending moment** and a uniform maximum stress over a region of length $L-2a$. Advantages over three-point bending:

- a *larger volume* of material is tested at the maximum stress, so the strength is more representative and less optimistic;
- the region of maximum stress is free of contact stresses from the loading rollers;
- it is the preferred geometry in standards for advanced ceramics (ASTM C1161).

The trade-off is a more complex rig and a larger specimen.

> [!note] What "flexural strength" is not
> It is not the true uniaxial tensile strength. It is the *modulus of rupture* — the stress computed from the elastic beam formula at the fracture load. If the material yields (metals) or has a non-linear stress–strain response (some ceramics, all polymers), this computed stress differs from the true surface stress. It is nonetheless the standard engineering number, and it is comparable between materials only when measured with the same specimen geometry and loading rate.

## 3.2 Stress–strain behaviour of ceramics and the influence of porosity

- The stress–strain curve of a ceramic is **linear elastic up to fracture** — there is essentially **no plastic deformation**. The fracture strain is tiny ($\sim10^{-4}$–$10^{-3}$), so $E$ is large and the area under the curve (toughness) is small.
- **Porosity** degrades both stiffness and strength, because pores act as stress concentrators and reduce the load-bearing cross-section:

$$ E = E_0\left(1 - 1.9P + 0.9P^2\right) \qquad\qquad \sigma_{fs} = \sigma_0 \exp(-nP) $$

where $P$ is the **volume fraction porosity** and $E_0,\sigma_0$ are the values at zero porosity. The exponential drop in strength ($n\approx4$–$7$) is far steeper than the drop in modulus — a few percent porosity can halve the strength. This is why ceramic processing is obsessed with densification (sintering, hot pressing, HIPing).

![[MP3 - Stress-strain curve for ceramics.png|400]]

*Figure — stress–strain curves for alumina and glass: linear elastic to fracture, with fracture strains of a few parts in $10^4$ — there is no plastic region at all.*

![[MP3 - Modulus vs porosity.png|380]]

*Figure — Young's modulus against volume fraction porosity: a shallow, almost parabolic decrease described by $E=E_0(1-1.9P+0.9P^2)$.*

![[MP3 - Flexural strength vs porosity.png|380]]

*Figure — flexural strength against porosity: a much steeper, exponential fall, $\sigma_{fs}=\sigma_0e^{-nP}$ with $n\approx4$–$7$.*

### Interpreting the two porosity equations

- **The modulus equation** $E=E_0(1-1.9P+0.9P^2)$ is essentially a *rule of mixtures* correction: a pore carries no load, so the load-bearing area is reduced, and the pore also perturbs the local stress field. The effect is gentle and *reversible* — a porous ceramic is still stiff, just less so, and the relation is nearly the same whether the pores are spherical or irregular.
- **The strength equation** $\sigma_{fs}=\sigma_0e^{-nP}$ is far more severe because a pore is a **stress concentrator**, not merely missing area. A spherical pore of radius $r$ in a field $\sigma$ raises the local stress at its equator to $\sim3\sigma$ (for a spherical cavity, $K_t=3$ in the elastic solution; sharper pores and pore clusters give much higher values). A pore that touches a grain boundary or a surface flaw can *be* the critical crack. Since brittle fracture is governed by the *largest* flaw, the strength is exponentially sensitive to the *number* of pores — hence the exponential law and the $n\approx4$–$7$ values.
- **Practical numbers**: a 10 % porosity alumina retains about 82 % of its modulus but only 50–60 % of its strength; a 99.5 % dense alumina and a 96 % dense one can differ by a factor of 2 in strength while both look "solid".
- **Processing implications**: **sintering** (diffusional densification at $T\approx0.7T_m$) removes porosity; **hot pressing / HIPing** (pressure-assisted sintering) removes the last few percent, which is where most of the strength is; **additives** (MgO in alumina) inhibit grain growth so that pores are not trapped inside grains. Porosity also degrades **optical transparency** (pores scatter light), **thermal conductivity** and **dielectric breakdown strength**, so the same processing discipline is needed for functional ceramics.

### The statistics of brittle strength: Weibull

Because failure initiates at the *weakest* flaw, the strength of nominally identical ceramic specimens scatters widely (coefficient of variation 10–30 %, versus 1–3 % for metals). The standard description is the **Weibull distribution**:

$$ P_f = 1-\exp\!\left[-\left(\frac{\sigma}{\sigma_0}\right)^{m}\right] $$

where $m$ is the **Weibull modulus** — a measure of the *uniformity* of the flaw population. Metals and ductile materials effectively have $m>50$; engineering ceramics have $m\approx5$–15; a very well-processed fine-grained ceramic can reach $m\approx20$. A low $m$ means the strength data are broad, so a large safety factor is needed.

Two consequences that follow directly:

- **Size effect** — a larger component has a higher probability of containing a large flaw, so its strength is lower. The strength therefore depends on the tested volume, which is why bend-bar data cannot be applied naively to a big part.
- **Proof testing** — loading every part to a proof stress removes the weak ones and *certifies a minimum strength*, which is how brittle components (spark plugs, ceramic insulators, optical fibres) are qualified.

| Ceramic | $E$ (GPa) | Flexural strength (MPa) | Fracture strain |
| --- | --- | --- | --- |
| Soda-lime glass | 70 | 70 | $10^{-3}$ |
| Alumina (99.5 %) | 380 | 300–400 | $10^{-3}$ |
| Silicon carbide | 410 | 400–600 | $10^{-3}$ |
| Silicon nitride | 300 | 600–900 | $10^{-3}$ |
| Zirconia (TZP) | 200 | 900–1200 | $5\times10^{-3}$ |
| Concrete | 30 | 3–5 (tension) | $10^{-4}$ |

## 3.3 Hardness: definition and advantages

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

![[MP3 - Hardness vs tensile strength.png|380]]

*Figure — tensile strength plotted against Brinell hardness for steels, brass and nodular cast iron: each class follows its own approximately straight line, with steels offset from the non-ferrous metals.*

### Why hardness correlates with strength at all

Both quantities measure the **same physical event**: the onset of plastic flow. Under a spherical or pyramidal indenter the material beneath the tip is in a complex, constrained, triaxial compression state, and it yields when the local shear stress reaches the shear yield strength. The mean pressure under the indenter (the hardness) is therefore a fixed multiple of the uniaxial flow stress — **Tabor's relation**:

$$ H \approx 3\,\sigma_y \qquad (H \text{ in MPa, } \sigma_y \text{ in MPa}) $$

The factor 3 comes from the geometry of the plastic zone: a hydrostatically constrained region yields at a mean pressure about three times the uniaxial yield stress (for a perfectly plastic material, the slip-line field gives $p\approx2.57\sigma_y$ for a wedge and $\approx3\sigma_y$ for a sphere; strain hardening raises it further). Applying this to the steel correlation above:

$$ \sigma_{UTS}\approx 3.45\,HB \quad\Longleftrightarrow\quad HB \approx \frac{\sigma_{UTS}}{3.45} $$

so a structural steel of 400 MPa UTS reads about 116 HB — which is consistent with the Tabor factor, because 116 kgf/mm² $\approx 1140$ MPa of indentation pressure, and the *flow stress at the large strain under the indenter* is much higher than the yield strength. The numerical coefficient 3.45 is therefore not a fundamental constant: it folds together the constraint factor (≈3), the work hardening under the indenter, and the ratio $\sigma_{UTS}/\sigma_y$ for steels. This is exactly why the correlation is material-specific.

### What hardness is *not*

- **Not a fundamental property.** It has no unique definition independent of the test: it depends on indenter shape, load, loading rate, dwell time, and the material's work-hardening behaviour. A Brinell number and a Vickers number for the same steel are numerically similar but conceptually different measurements.
- **Not a strength for design.** It cannot be inserted into a stress calculation; it is a *ranking* and *QC* parameter, and only through an empirical correlation does it estimate a strength.
- **Not toughness.** See the warning callout above: a hard surface resists penetration but a crack can run through it with little energy. Hardness and fracture toughness are often inversely related, which is why tool steels are hard but brittle, and why tough grades are softer.
- **Not uniform.** Surface hardness after machining, grinding, decarburisation, shot peening, nitriding or induction hardening differs from the core. Hardness *gradients* are used deliberately (case-hardened gears: hard case for wear, tough core for shock) and are measured by traverses across a section.

### Advantages, in design and production terms

| Advantage | Consequence |
| --- | --- |
| Fast | One measurement in seconds; thousands of parts per shift |
| Cheap | Simple, robust machines; no specimen preparation for Rockwell/Brinell |
| Essentially non-destructive | The part can still be used (one small indent) |
| Local | Measures the surface, a weld, a heat-affected zone, an individual phase (microindentation) |
| Estimative | Gives a first estimate of tensile strength, wear resistance, machinability, cold formability |
| Portable | Portable hardness testers (Leeb, UCI, rebound) for field inspection of large structures |

Typical industrial uses: incoming inspection of bar stock; verification of heat treatment (a quench-and-temper cycle is checked by HRC); case-depth measurement; weld qualification; monitoring of cold-work level; sorting mixed materials (a hardness traverse distinguishes a 1045 from a 4140).

## 3.4 Hardness-testing techniques — summary

| Test | Indenter | Load | Hardness number |
| --- | --- | --- | --- |
| **Brinell** | 10 mm sphere of steel or tungsten carbide | 500–3000 kg | $HB = \dfrac{2P}{\pi D\left[D-\sqrt{D^2-d^2}\right]}$ |
| **Vickers** (microindentation) | Diamond pyramid, 136° | 1–1000 g | $HV = 1.854\,P/d^2$ |
| **Knoop** (microindentation) | Diamond pyramid, elongated ($l/b = 7.11$) | 1–1000 g | $HK = 14.2\,P/l^2$ |
| **Rockwell / superficial Rockwell** | Diamond cone (120°) or steel/WC ball ($\tfrac{1}{16}$ in., $\tfrac{1}{8}$ in., $\tfrac{1}{4}$ in.) | 15, 30, 45, 60, 100, 150 kg | From depth of penetration $h$ |

($P$ in kg; $D, d, l$ in mm.)

![[MP3 - Hardness testing techniques table.png|480]]

*Figure — the lecture table (Callister, Table 7.5) of hardness-testing techniques with indenter shapes, side/top views, formulas and the standard designation of each number.*

### Choosing between them

| | **Brinell** | **Vickers** | **Knoop** | **Rockwell** |
| --- | --- | --- | --- | --- |
| Indent size | Largest ($\sim1$–5 mm) | Small ($\sim50$–500 µm) | Small, elongated | Medium |
| Load range | 500–3000 kg | 1 g – 1000 g (micro), up to 50 kg (macro) | 1 g – 1000 g | 15–150 kg (superficial 15–45 kg) |
| Measurement | Diameter by microscope | Diagonals by microscope | Long diagonal by microscope | Depth, read directly |
| Speed | Slow (measurement) | Slow | Slow | Fast |
| Best for | Coarse/inhomogeneous microstructures (cast iron), large parts | General purpose, hard materials, case depth, phase hardness | Very brittle ceramics, thin coatings, oriented features | Routine QC of metals, production lines |
| Weakness | Large indent; unsuitable for thin parts | Needs polished surface, optical measurement | Same | Several scales; not for very hard/thin without care |

Two practical distinctions matter:

- **Macro vs micro indentation**: Brinell and Rockwell are macro tests where the indent samples many grains, so they give a *bulk average*. Vickers and Knoop are micro tests where the indent can be placed inside a single grain or a thin coating, so they give a *local* value. The same material often shows different numbers at the two scales (the **indentation size effect**, §3.9).
- **Strength-based vs depth-based**: Brinell and Vickers report a *stress-like* quantity (load divided by indent area), so HB and HV are close to each other and roughly proportional to strength. Rockwell reports a *depth*, and its number is arbitrary and scale-dependent — hence the many letter scales and the restricted ranges.

## 3.5 The Rockwell test

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

![[MP3 - Rockwell scales table.png|480]]

*Figure — the standard Rockwell (7.6a) and superficial Rockwell (7.6b) scale tables: scale symbol, indenter and major load.*

![[MP3 - Rockwell scale applications.png|480]]

*Figure — the Rockwell scale-selection table with typical applications for each scale.*

### The test sequence, step by step

1. The specimen is placed on a flat, rigid anvil and the indenter is brought into contact.
2. The **minor load** (10 kg) is applied. This seats the indenter, breaks through surface contamination and eliminates the effect of surface roughness — the depth reached under the minor load becomes the *reference zero*.
3. The dial is zeroed.
4. The **major load** is applied and held for a specified dwell (typically 10–15 s, allowing plastic flow to finish).
5. The major load is removed, the minor load remains, and the **permanent increase in depth** $h$ is read on the dial. Each division corresponds to $0.002$ mm.

$$ HR = 100 - \frac{h}{0.002}\ \text{(diamond spheroconical)} \qquad\qquad HR = 130 - \frac{h}{0.002}\ \text{(ball)} $$

**Why 100 and 130?** The scales are defined so that numbers increase with hardness. For the diamond cone, a depth increase of 0.2 mm corresponds to the full dial travel of 100 divisions, so $h=0$ gives 100 (the hardest reading). For ball indenters the geometry allows a deeper penetration before the dial runs out, so the zero point is set at 130. This is why the two families are not interchangeable and why the maximum meaningful reading differs.

**Why the minor load improves accuracy.** Without it, the measured depth would include the elastic/plastic seating of a rough surface — typically tens of micrometres, i.e. tens of hardness points. The minor load removes this by making the reference a *loaded* state. The major load's depth is then purely the response of the material.

### Scale selection

- Use the **hardest scale whose reading stays in the valid range**. Valid readings are roughly 20–100 (or up to 130 on some scales): below 20 the divisions are compressed and resolution is poor, above 100 the indenter may be penetrating the anvil or the material may be at the limit of the indenter.
- **A**: cemented carbides, thin hardened steel, shallow case. **B**: soft steels, copper and aluminium alloys. **C**: steels, hard cast irons, titanium (the workhorse scale). **D**: thin steel, medium case. **E/F/G/H/K**: progressively softer non-ferrous metals and bearing metals.
- For **thin** specimens or thin cases, use a **superficial** scale (15N/30N/45N, 15T/30T/45T) with low load so the indent depth stays under 1/10 of the thickness.
- A useful rule: if the reading is above HRB 100, switch to HRC (the ball is flattening and the reading is no longer reliable); if below HRC 20, switch to HRB or a lower-load scale.

### Typical values worth remembering

| Condition of steel | HRC |
| --- | --- |
| Annealed low-carbon steel | $\sim$10 (or HRB 80) |
| Normalised medium-carbon steel | 20–25 |
| Quenched and tempered (structural) | 30–40 |
| Quenched and tempered (tool) | 45–55 |
| As-quenched tool steel | 60–65 |
| Cemented carbide | 70–75 (HRA) |

**Corrections for cylindrical specimens.** On a curved surface the indent is shallower than on a flat, so the reading is high; tables give corrections for each diameter and scale. This is a standard source of error when testing shafts and pins.

## 3.6 The Brinell test

- A hardened steel or **tungsten carbide ball of 10 mm diameter** is pressed into the surface.
- Standard loads: **500–3000 kg in 500 kg increments**; harder materials need larger loads (to keep the indent size in the measurable range).
- The load is held constant for a specified time, typically **10–30 s**.
- The **diameter of the circular indent** $d$ is measured with a **microscope/measuring scale**, and

$$ HB = \frac{2P}{\pi D\left[D - \sqrt{D^2 - d^2}\right]} $$

- $HB$ therefore depends on **both** the load and the indent diameter — this is why the load must always be quoted with the number.
- There is **only one Brinell scale** (in contrast to Rockwell's many letter scales).
- Specimen thickness, edge distance, spacing and surface-finish requirements are the same as for Rockwell. The indentation is large, so Brinell averages over a coarse microstructure (useful for cast irons and inhomogeneous alloys) but is unsuitable for thin specimens.

### Deriving the Brinell formula

Brinell hardness is the **load divided by the curved surface area of the spherical cap** — not by the projected circular area. From the geometry of a sphere of diameter $D$ indented to a chordal diameter $d$:

$$ \text{depth of cap } h = \frac{D-\sqrt{D^2-d^2}}{2}, \qquad A_{\text{cap}} = \pi D h = \frac{\pi D\left[D-\sqrt{D^2-d^2}\right]}{2} $$

$$ HB = \frac{P}{A_{\text{cap}}} = \frac{2P}{\pi D\left[D-\sqrt{D^2-d^2}\right]} $$

This is the origin of the formula — and it explains why $HB$ is a *stress* (kgf/mm²) with a genuine physical meaning, unlike the Rockwell number.

### Load selection and the "constant $P/D^2$" rule

Two specimens of the same material tested with different loads must give the same $HB$ — otherwise the test would be useless. Empirically, the indent geometry scales with $D$ only if the ratio $P/D^2$ is held constant. The standard values are:

| Material | $P/D^2$ | Load with 10 mm ball |
| --- | --- | --- |
| Ferrous metals | 30 | 3000 kgf |
| Copper alloys | 10 | 1000 kgf |
| Aluminium, softer metals | 5 | 500 kgf |
| Lead, tin, bearing metals | 2.5 | 250 kgf |

Keeping $P/D^2$ constant keeps the *strain* under the ball constant; too low a load gives a shallow indent with large measurement error, too high a load may deform the anvil or over-strain the material. This is the **Meyer law**: $P = kd^n$, with $n\approx2.0$–2.5.

### Practical points

- **The ball material**: hardened steel for $HB<350$; **tungsten carbide** for harder materials, to avoid ball flattening that would corrupt the result. Above $\sim$600 HB the method is not reliable.
- **Dwell time 10–30 s** allows plastic flow to complete; for soft metals a longer dwell increases the indent, so the time must be standardised (15 s is common).
- **Measurement**: the diameter is read in two perpendicular directions under a low-power microscope, and the mean is used. This is the slow step that makes Brinell unsuitable for high production rates.
- **The large indent** ($\sim$2–5 mm) is both an advantage (averages inhomogeneity — good for cast iron, coarse forgings) and a limitation (damages finished surfaces, unusable on thin or small parts, and the minimum thickness is $\sim8$–10 × indent depth).
- Because the indent is large, the result includes grain boundaries, porosity and inclusions — it reports the *engineering* hardness of the material rather than that of a single phase.

## 3.7 The Knoop and Vickers microindentation tests

- A **very small diamond indenter of pyramidal geometry** is forced into the surface. **Vickers**: a square-based pyramid with a **136°** included angle. **Knoop**: an elongated pyramid with diagonal ratio $l/b = 7.11$ and face angles chosen so that the long diagonal is about seven times the short one.
- Applied loads are much smaller than for Rockwell/Brinell — **1 to 1000 g** (hence *microindentation*).
- The impression is observed under a **microscope** and its diagonals measured; the measurement is converted into a hardness number.
- Because the indent is tiny, **careful surface preparation (grinding and polishing)** is essential for a well-defined, measurable impression — and the test can be used to measure the hardness of individual phases, thin foils, coatings and case depths.

$$ HV = 1.854\,\frac{P}{d^2} \qquad\qquad HK = 14.2\,\frac{P}{l^2} $$

where $d$ is the mean Vickers diagonal and $l$ the long Knoop diagonal.

### Where the constants come from

**Vickers.** The indenter is a square-based pyramid with a **face angle of 136°** (chosen so that the ratio of indent area to depth matches that of an ideal conical indenter producing the same strain as a Brinell ball — the 136° is not arbitrary). Hardness is load divided by the *contact surface area* of the four faces:

$$ A = \frac{d^2}{2\sin(\theta/2)}, \quad \theta = 136^\circ \ \Longrightarrow\ A = \frac{d^2}{2\sin68^\circ} = 0.5393\,d^2 $$

$$ HV = \frac{P}{A} = \frac{2P\sin68^\circ}{d^2} = 1.854\,\frac{P}{d^2} $$

The constant $1.854 = 2\sin 68^\circ$. Because the indent is *self-similar* (a pyramid produces geometrically similar indents at all loads), HV is in principle **independent of load** — a major advantage over the ball tests, and the reason Vickers is the standard for research and for hard materials.

**Knoop.** The indenter is a rhombic-based pyramid with diagonal ratio $l/b = 7.11$ and face angles of 172.5° and 130°, giving $HK = 14.2\,P/l^2$. The elongated shape produces a shallow indent (depth $\approx l/30$), which is why Knoop is preferred for **thin coatings, brittle ceramics and case-depth traverses**: the plastic zone is shallow and does not extend through the layer being measured.

### Why microindentation matters

- **Individual phases**: an indent of 10–50 µm can be placed inside a single grain, so the hardness of ferrite, pearlite, cementite, austenite, a precipitate or a weld-zone constituent can be measured separately. This is the basis of microstructural QC.
- **Case depth and coatings**: a traverse of indentations from surface to core gives the hardness profile — the definition of effective case depth (typically the depth where hardness falls to a specified value, e.g. 550 HV for carburised steel).
- **Thin foils and small features**: MEMS, thin films, additively manufactured lattices.
- **Brittle materials**: Vickers is the workhorse; Knoop is used where cracking must be minimised (§3.9).

### Limitations and refinements

- **Surface preparation is critical**: the diagonal is measured optically, and a poorly polished surface gives a ragged indent and a large error. Grinding and polishing (down to 1 µm diamond) is mandatory, and care must be taken not to introduce a deformed layer.
- **Indentation size effect (ISE)**: at small loads the measured hardness is higher — the plastic zone is small, geometrically necessary dislocations are dense, and surface effects dominate. The value falls to a load-independent plateau at larger loads. This is why a hardness value must be quoted with its load.
- **Cracking**: for hard/brittle materials a crack system forms around the indent. Its length can be used to estimate fracture toughness:
  $$ K_{Ic} = \xi\left(\frac{E}{H}\right)^{1/2}\frac{P}{c^{3/2}} \qquad\text{(Anstis equation)} $$
  with $c$ the crack length and $\xi\approx0.016$ — a way to measure toughness from a single indent.
- **Instrumented (nano)indentation**: modern instruments record load vs depth continuously (Oliver–Pharr analysis) and give hardness *and* modulus from the unloading slope, at scales of nanometres — used for thin films and individual phases. This is a direct descendant of the Vickers/Knoop idea.

## 3.8 Hardness conversion

- **Hardness is not a well-defined physical property** — it is a response to a particular indenter geometry, load and material behaviour. Because the experimental conditions differ so much between techniques, **no comprehensive conversion scheme exists**.
- Conversion tables/charts have been determined **empirically** and depend on the **material type and characteristics**.
- The most reliable conversion data exist for **steels** (that is why "TS = 3.45 HB" works well for steels and poorly for everything else).
- A useful anchor: the **Mohs** scratch scale (talc = 1 … diamond = 10) is a completely different, ordinal hardness scale and cannot be converted to HB/HV/HK by formula.

![[MP3 - Hardness conversion chart.png|420]]

*Figure — the standard conversion chart relating Brinell, Vickers, Rockwell and Mohs hardness to tensile strength, with the material classes (tool steels, alloy steels, brasses, plastics) marked on the same axes.*

### Why conversion is possible at all — and why it is not exact

Hardness numbers from different tests are different *functions* of the same underlying plastic response, so they are monotonically related. But the relationship is not unique because each test probes a different combination of:

- **strain level** (a Brinell ball at $P/D^2=30$ reaches an effective strain of $\sim$8 %, while a Vickers pyramid reaches $\sim$8 % too but over a much smaller volume);
- **volume sampled** (macro vs micro — see the indentation size effect);
- **work-hardening behaviour** (a strongly work-hardening material gives a higher macro hardness relative to its yield strength than a non-hardening one);
- **anisotropy and texture** (rolled sheet is harder in the through-thickness direction);
- **elastic recovery** (diamond pyramid indents recover elastically on unloading, so the measured diagonal is smaller than the true contact size — a bigger effect in hard materials).

Hence conversion tables are **empirical**, are material-specific, and are only reliable within the class for which they were established. **ASTM E140** gives standard tables for metals, but explicitly states that they are approximate and that the material must be "in the same condition" as the reference.

| Approximate conversions for steels | | | |
| --- | --- | --- | --- |
| HRC | HV | HB (10 mm/3000 kg) | UTS (MPa) |
| 20 | 238 | 226 | 780 |
| 30 | 302 | 286 | 1000 |
| 40 | 392 | 371 | 1290 |
| 50 | 513 | 484 | 1690 |
| 60 | 697 | 654 | 2290 |

The spread in such tables is typically ±3–5 % of the hardness value, and much larger for cast irons, duplex stainless steels and cold-worked non-ferrous alloys.

### The Mohs scale — a different kind of hardness

Mohs hardness is **ordinal and qualitative**: it ranks minerals by whether one scratches another (talc 1, gypsum 2, calcite 3, fluorite 4, apatite 5, orthoclase 6, quartz 7, topaz 8, corundum 9, diamond 10). Its steps are wildly non-uniform — the jump from 9 to 10 is a factor of about 4 in indentation hardness, while 1 to 2 is a small increment. It measures *scratch resistance* (a form of wear), not indentation resistance, so:

- it cannot be converted to HB/HV/HK by formula;
- it is still used in mineralogy and in the abrasives/ceramics industry because it maps directly onto the practical question "what will scratch what";
- the modern instrumented equivalent is the **scratch test** (a stylus under a ramped load), which gives a quantitative scratch hardness.

> [!warning] Don't mix scales in a specification
> A drawing that specifies "hardness 45" is meaningless. Always quote the scale, the load and the indenter: "45 HRC", "600 HV1" (Vickers, 1 kg), "200 HBW 10/3000" (tungsten ball, 10 mm, 3000 kg). Conversion between scales should be treated as an estimate, not a measurement.

## 3.9 Hardness of ceramics

- **Spherical indenters** (Rockwell, Brinell) are **not used** for ceramics — the concentrated load produces severe **cracking** around the indent instead of a clean impression.
- **Vickers** is the workhorse for ceramics; for **very brittle** ceramics the **Knoop** test is often preferred because the elongated indent is less prone to cracking.
- For both, the measured hardness **decreases with increasing load (indentation size effect)** and then reaches a **constant plateau** that is independent of load. The plateau value varies from ceramic to ceramic.
- An **ideal** test uses a load large enough to be on the plateau, but not so large as to introduce excessive cracking.

### Why spherical indenters fail on ceramics

A sphere produces a **Hertzian** stress field: high shear stresses at a depth of about half the contact radius, beneath a region of high hydrostatic compression. In a ductile metal that shear zone yields and forms a normal indent. In a ceramic there is no plastic flow to relieve it, so the tensile hoop stress at the contact periphery exceeds the (very low) tensile strength and a **ring/cone crack** forms — often before any measurable indent. The result is a damaged surface, not a hardness number.

Pyramidal (Vickers) and rhombic (Knoop) indenters are used instead because they produce **localised shear** rather than a large tensile field; a small plastic zone does form under a sharp indenter even in a hard ceramic (the high hydrostatic pressure suppresses cracking), and the hardness is obtained from the indent size.

### The indentation size effect (ISE) in ceramics

Plotted against load, hardness typically **decreases** with increasing load and then flattens:

- **Low loads** — the indent is small relative to the surface damage layer, the plastic zone is constrained by the surrounding elastic material, and there are few defects within the sampled volume → **higher** apparent hardness.
- **High loads** — the measured value approaches the true bulk hardness; but at very high loads the indent is surrounded by an extensive crack system, the measurement becomes unreliable, and the material may chip.

The standard practice is therefore to report a **plateau value** measured with a load chosen so that the indent is large enough to be measured accurately (diagonal $\gtrsim$ 20 µm) but small enough that cracking is limited. Reporting "hardness" without the load is meaningless for ceramics.

### Typical values (Vickers, plateau)

| Ceramic | HV (GPa) | Comment |
| --- | --- | --- |
| Talc (Mohs 1) | $\sim$0.02 | softest reference |
| Soda-lime glass | 5.5–6 | cracks readily |
| Quartz | 11–12 | Mohs 7 |
| Alumina (99.5 %) | 15–18 | workhorse technical ceramic |
| Zirconia (TZP) | 12–14 | transformation toughening gives toughness, lower hardness |
| Silicon nitride | 15–20 | |
| Silicon carbide | 22–30 | |
| Boron carbide | 30–35 | armour ceramics |
| Cubic boron nitride | 45–50 | |
| Diamond | 70–100 | the practical limit of indentation |

Note the pattern: **hardness and toughness are usually inversely related** — zirconia is comparatively soft but the toughest engineering ceramic, while diamond and B4C are the hardest and among the most brittle. This is the same trade-off as in hardened tool steels (§3.3), and it is why "hard coating on a tough substrate" is the standard design for cutting tools and wear parts.

## 3.10 Tear strength and hardness of polymers

- **Tear strength** — the ability to resist tearing — is important for **thin films** (packaging). It is defined as the **energy required to tear apart a cut specimen of standard geometry**; the crack must be propagated through the specimen, so tear strength depends on both the **tensile strength** and the **thickness** of the film. Magnitudes of tensile and tear strength are related (both reflect chain alignment and intermolecular bonding).
- Polymers are much softer than metals and ceramics, so **Rockwell** tests (with ball indenters and low loads) are frequently used; other techniques are the **Durometer** and **Barcol** tests, both designed for soft materials.

### Tear strength in more detail

- **What it measures.** The energy (or force) needed to propagate a tear through a standard notched specimen. It is a *fracture* property, not a strength: it depends on the energy dissipated in the plastic/viscoelastic zone ahead of the tear tip.
- **Standard tests.** The **Elmendorf** (pendulum) test for films and the **trouser-tear** and **Graves** tests for sheet; units are N/mm (force per thickness) or g/µm for thin films, sometimes mJ/mm² for energy per area.
- **Thickness dependence.** Tear resistance rises with thickness but not linearly (the plastic zone is constrained differently), and for very thin films the value approaches a constant "intrinsic" tear resistance. This is why tear data are always quoted with the thickness.
- **Relation to tensile strength.** Both reflect the same underlying chain alignment and intermolecular bonding, so a tougher, more oriented film tears less easily. Biaxially oriented films (BOPP, PET) have high tear resistance *along* the machine direction and low *across* it — a serious issue for packaging where the tear must run predictably.
- **Why it matters.** A packaging film that tears at 1 N is a convenience; a cable insulation that tears is a failure; a balloon that tears is burst. Tear strength is also a routine QC measure for polymer processing consistency.

### Hardness of polymers

Because polymers are soft and viscoelastic, the standard metals tests are unsuitable (a diamond cone would simply disappear into the material). The dedicated tests are:

| Test | Indenter | Load | Scale | Typical use |
| --- | --- | --- | --- | --- |
| **Durometer (Shore A)** | Truncated cone | $\sim$0.8 kg (spring) | 0–100 | Soft rubbers, elastomers |
| **Durometer (Shore D)** | Sharp cone | $\sim$4.5 kg (spring) | 0–100 | Rigid plastics |
| **Rockwell R/L/M** | $\tfrac12$ in. or $\tfrac14$ in. ball | 60/100 kg | R, L, M | Rigid thermoplastics, similar to metals procedure |
| **Barcol** | Spring-loaded steel point | Small | 0–100 | Field testing of composites, GRP, plastics |
| **Ball indentation (ISO 2039)** | Steel ball | 36 kg | N/mm² | Standard for rigid plastics |

Two points that make polymer hardness tricky:

1. **Time dependence.** Because the material is viscoelastic, the reading drifts with the dwell time and with the loading rate. Standards specify a dwell (often 15 s) and the reading is meaningless without it.
2. **Temperature dependence.** Hardness falls sharply as the temperature approaches $T_g$; a polymer that reads Shore D 80 at 20 °C may be Shore A 70 at 60 °C. Indentation hardness of polymers is really a *viscoelastic* measurement, and it is one of the most sensitive ways to detect a glass transition.

Typical values: Shore A 30–60 for soft rubber, Shore A 70–90 for shoe soles and tyre treads, Shore D 60–80 for rigid PVC, polycarbonate and nylon, Barcol 30–50 for glass-fibre composites.

> [!tip] Exam pointer — Part III
> Expect: why three-point bending is used for ceramics and the two $\sigma_{fs}$ formulae; the porosity equations $E = E_0(1-1.9P+0.9P^2)$ and $\sigma_{fs}=\sigma_0 e^{-nP}$; the definition of hardness and why it is not a fundamental property; the Rockwell depth formulae ($100 - h/0.002$ vs $130 - h/0.002$); and the Brinell/Vickers/Knoop expressions with their load ranges. The added depth to be ready with: the derivation of each hardness formula from the indenter geometry (spherical cap area, square pyramid at 136°); Tabor's $H\approx3\sigma_y$ as the reason hardness tracks strength; why four-point bending is preferred for ceramics; Weibull statistics and the size effect; and the indentation size effect that makes a hardness number meaningless without its load.

---

## Formula Summary — Mechanical Properties (Parts I–III)

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
| Tabor relation | $H \approx 3\sigma_y$ | Hardness vs flow stress |
| von Mises equivalent stress | $\sigma_{\text{vM}}=\sqrt{\tfrac12[(\sigma_1-\sigma_2)^2+(\sigma_2-\sigma_3)^2+(\sigma_3-\sigma_1)^2]}$ | Yields when $=\sigma_y$ |
| Isotropic elastic constants | $G=\dfrac{E}{2(1+\nu)}$, $K=\dfrac{E}{3(1-2\nu)}$ | Two constants define the rest |
| Volume change, uniaxial | $\Delta V/V=\varepsilon_z(1-2\nu)$ | Zero at $\nu=0.5$ |
| Considère criterion | $d\sigma_T/d\varepsilon_T=\sigma_T$ | Onset of necking |
| Uniform strain at UTS | $\varepsilon_{T,u}=n$ | With Hollomon law |
| UTS from Hollomon | $\sigma_{UTS}=K(n/e)^n$ | $e=2.718$ |
| True fracture strain | $\varepsilon_{T,f}=\ln\!\left(\dfrac{100}{100-\%RA}\right)$ | Gauge-independent ductility |
| Bridgman correction | $\sigma_{\text{corr}}=\dfrac{\sigma_T}{(1+2R/a)\ln(1+a/2R)}$ | Triaxiality in the neck |
| Taylor relation | $\tau=\tau_0+\alpha Gb\sqrt{\rho}$ | Forest hardening |
| Hall–Petch | $\sigma_y=\sigma_0+k_y d^{-1/2}$ | Grain-size strengthening |
| Taylor factor | $\sigma_y=M\tau_{CRSS}$, $M\approx3.06$ (FCC) | Polycrystal vs single crystal |
| Creep rate | $\dot\varepsilon_s=A\sigma^n e^{-Q/RT}$ | $n\approx3$–5 (dislocation creep) |
| Springback | $\dfrac{1}{R_f}=\dfrac{1}{R_0}-\dfrac{3\sigma_y}{Et}$ | Thin sheet, approximate |
| Fracture toughness | $K_{Ic}=Y\sigma\sqrt{\pi a}$ | Flaw-tolerant design |
| Weibull failure probability | $P_f=1-\exp[-(\sigma/\sigma_0)^m]$ | Brittle strength scatter |
| Toughness from indent | $K_{Ic}=\xi(E/H)^{1/2}P/c^{3/2}$ | Anstis relation |

> [!note] Source images
> All Excalidraw figures in this note are original reconstructions of the diagrams in the three lecture PDFs and the handwritten notes; the vault copies live in the `Excalidraw/` folder with the `MP - ` prefix. The photographs, plots and tables embedded above are the original figures extracted from the three lecture PDFs and stored in `Material Science/images/` with the `MP`/`MP2`/`MP3` prefix.

---

# Shockley and Frankel Partial Dislocations

A perfect dislocation is *not* the lowest-energy line defect a crystal can build. In the close-packed metals the lattice pays itself to **split** the perfect dislocation into two **partial** dislocations separated by a narrow strip of **stacking fault** — an **extended dislocation**. This short block works through the two families of partial that exist in the face-centred cubic lattice: the **Shockley** partials, which are *glissile* and whose glide creates and destroys the fault, and the **Frank** partials, which are *sessile* edge dislocations bounding a single fault plane and can move only by climb. Nearly everything that later looks like a materials property — the ease of cross-slip, the rate of work hardening, the tendency to deform by twinning, the hardening left behind by a quench or by neutron irradiation — is decided by which of these two is present and how wide the fault ribbon is.

Compiled from the lecture slides ([[Shockley and Frank partial dislocations_Odd_2026-27.pdf]] — a three-slide deck: a title slide and one figure slide per partial type) and the handwritten class notes in [[MO NOTES (1).pdf]] (pp. 132–152). The slides are completed against **Raghavan, *Materials Science and Engineering*** and **Callister, *Fundamentals of Materials Science and Engineering*** (ch. 7, *Dislocations and strengthening mechanisms*); the force expressions of §4.4 follow *Hull & Bacon, Introduction to Dislocations*.

> [!info] How the two halves fit together
> **§4.1–§4.5** are the Shockley half: why the perfect dislocation dissociates at all (§4.1), what the stacking fault it leaves behind actually is (§4.2), the geometry of the $\mathbf{b} = \tfrac{a}{6}\langle112\rangle$ partials (§4.3), the force balance that fixes the **width** of the ribbon (§4.4), and Thompson's tetrahedron — the bookkeeping device that makes every vector in the block readable at a glance (§4.5). **§4.6–§4.7** are the Frank half: the sessile $\mathbf{b} = \tfrac{a}{3}\langle111\rangle$ partial (§4.6), how it is created by the collapse of a vacancy disc and removed again by unfaulting (§4.7). **§4.8** is the comparison table examiners ask for; **§4.9** is the payoff — what the stacking-fault energy controls.

> [!warning] "Frankel" or "Frank"?
> The syllabus writes *Shockley and **Frankel** partial dislocations*; the lecture slide and every textbook write **Frank** — after **F. C. Frank**, who introduced the sessile partial bounding a fault. There is no separate "Frankel" dislocation here: *Frankel* (Frenkel) belongs to the **Frenkel pair** of point defects, an unrelated idea. Write **Frank partial** in the exam.

---

## 4. Shockley and Frankel Partial Dislocations

### 4.1 Why a perfect dislocation dissociates

![[SD - Dissociation into Shockley partials.excalidraw]]

A dislocation line stores elastic energy in proportion to the square of its Burgers vector, $E_{el} \approx \alpha G b^2$ per unit length. That quadratic dependence is what makes dissociation possible: replacing one long vector by two short ones whose vector sum is unchanged lowers the energy, exactly as in the dislocation reactions of §2.5. In the fcc lattice the saving is large — $a^2/2$ becomes $a^2/3$, a **33 % reduction** — and it is available on every $\{111\}$ plane at once, which is why dissociation is the *normal* state of a dislocation in a close-packed metal rather than an exotic exception.

$$ \boxed{\ \frac{a}{2}[1\bar{1}0] \;\longrightarrow\; \frac{a}{6}[2\bar{1}1] + \frac{a}{6}[1\bar{2}\bar{1}], \qquad b^2:\ \frac{a^2}{2} \;\to\; \frac{a^2}{3}\ } $$

The price of the split is the strip of **stacking fault** between the two partials: it costs $\gamma_{SF}$ per unit area, so the partials do not fly apart to infinity — they settle at the separation where elastic repulsion just balances fault energy (§4.4). The object that results — two partials joined by a fault ribbon, gliding as one unit — is an **extended dislocation**.

> [!important] Definitions
> **Perfect (unit) dislocation** — a dislocation whose Burgers vector is a *lattice translation vector*, so that its passage takes every atom to an equivalent lattice site and leaves a perfect crystal behind it. In fcc, $\mathbf{b} = \tfrac{a}{2}\langle110\rangle$.
> **Partial dislocation** — a dislocation whose Burgers vector is *not* a lattice translation; its passage leaves a planar defect — a stacking fault — in its wake. In fcc, $\mathbf{b} = \tfrac{a}{6}\langle112\rangle$ (Shockley) or $\tfrac{a}{3}\langle111\rangle$ (Frank).
> **Stacking fault** — a planar defect on a close-packed plane in which the layer sequence $\ldots ABCABC\ldots$ is interrupted. No bonds are broken and no atoms are added; only the *stacking* is wrong, which is why the energy is small (tens of mJ/m², not J/m²).
> **Stacking-fault energy $\gamma_{SF}$** — the excess energy per unit area of the fault plane. It is the single number that decides how wide the partials separate and therefore how the metal deforms.
> **Extended dislocation** — the composite object: leading partial + fault ribbon + trailing partial, moving together as one dislocation of total Burgers vector $\tfrac{a}{2}\langle110\rangle$.
> **Glissile / sessile** — a dislocation is *glissile* if it can glide conservatively on a slip plane (its $\mathbf{b}$ lies in that plane); *sessile* if it cannot, and must move by climb or not at all.

| Feature | Perfect dislocation | Shockley partial | Frank partial |
| --- | --- | --- | --- |
| Burgers vector (fcc) | $\tfrac{a}{2}\langle110\rangle$ | $\tfrac{a}{6}\langle112\rangle$ | $\tfrac{a}{3}\langle111\rangle$ |
| $b^2$ | $a^2/2 = 0.50\,a^2$ | $a^2/6 = 0.17\,a^2$ | $a^2/3 = 0.33\,a^2$ |
| $\mathbf{b}$ relative to the fault plane | lies in the glide plane | lies **in** the fault plane | **normal** to the fault plane |
| Passage leaves behind | perfect crystal | a stacking fault | the fault it bounds (no new fault created) |
| Mobility | glissile | **glissile** (moves with its fault) | **sessile** (climb only) |
| Character | edge, screw or mixed | mixed, $30^\circ$ to the parent $\mathbf{b}$ | pure edge |

> [!note] Why the splitting stops at two partials
> There is nothing shorter to split into. The $\tfrac{a}{6}\langle112\rangle$ vector is the shortest *lattice-irrational* vector of the fcc lattice that lies in a $\{111\}$ plane; a further split would demand a vector of the $\tfrac{a}{12}\langle110\rangle$ type, which is not a lattice vector combination at all, and would leave a second, higher-energy fault type behind. The two partials also repel each other (same sign), so the pair is stable against collapse; the fault tension makes it stable against infinite separation. A minimum energy therefore exists at a finite width.

### 4.2 The close-packed stacking of $\{111\}$ and the stacking fault

![[SD - Stacking sequence and stacking fault.excalidraw]]

Along the $\langle111\rangle$ direction the fcc lattice stacks *close-packed planes* in the sequence $\ldots ABCABC\ldots$; the hcp lattice stacks the same planes as $\ldots ABAB\ldots$. There is no difference in the *number* of nearest neighbours (12 in both) — the difference lies entirely in the **third** neighbour shell. That is the whole reason a stacking fault is cheap: a fault converts a slab of the crystal into hcp-like stacking, breaking no bonds and changing no coordination number, and costing only the small third-neighbour misfit.

![[SD - Shockley partials slide.png|500]]

*Figure — the lecture slide on Shockley partials: the close-packed stacking of the $\{111\}$ planes together with the $\tfrac{a}{6}\langle112\rangle$ partial vectors by which one perfect dislocation splits, and the stacking-fault ribbon lying between the two partials.*

A shear of one layer of the stack by one Shockley vector $\tfrac{a}{6}\langle112\rangle$ — one-third of a close-packed translation — moves the layer above from a $B$ site onto a $C$ site, so

$$ \ldots A\,B\,C\,A\,B\,C\,A\,B\,C \ldots \;\xrightarrow{\ \text{one Shockley partial}\ }\; \ldots A\,B\,C\,A\,|\,C\,A\,B\,C \ldots $$

which is a single "wrong" pair — an **intrinsic** stacking fault. The faulted plane is sandwiched by a thin layer of hcp-like $\ldots C\,A\,C\ldots$ stacking, two atomic planes thick. Two varieties exist:

> [!important] Definitions
> **Intrinsic stacking fault** — one violation of the $\ldots ABC\ldots$ sequence, produced by the glide of a *single* Shockley partial over one plane, or by the removal of one close-packed plane (a collapsed disc of vacancies). The standard fault of §4.3–§4.4.
> **Extrinsic stacking fault** — *two* violations, produced by inserting an extra plane (a collapsed disc of interstitials) or by the passage of two Shockley partials on *adjacent* planes. Higher energy, and it must be bounded by a Frank partial.
> **Coherent twin boundary** — the limiting case of a stack of intrinsic faults on every successive plane; it is a mirror plane, not a single fault, and its energy is roughly half the intrinsic fault energy per plane.

| Metal (annealed, room temperature) | $\gamma_{SF}$ (mJ/m²) | Ribbon width (edge, computed) | Behaviour |
| --- | --- | --- | --- |
| **Ag** | $\sim$22 | $\sim$5.8 nm | wide ribbon, planar glide, heavy twinning |
| **Cu** | $\sim$45 | $\sim$3.3 nm | wide enough to hinder cross-slip |
| **Ni** | $\sim$125 | $\sim$1.7 nm | narrow, cross-slip fairly easy |
| **Al** | $\sim$166 | $\sim$0.6 nm | effectively constricted, wavy glide |
| **Cu–30Zn (brass)** | $\sim$20 | wide | planar glide, very high work hardening |
| **304 stainless steel** | $\sim$18 | wide | planar glide, twinning (TWIP), $\varepsilon$-martensite |
| **Co (fcc)** | $\sim$15 | wide | fcc Co transforms/twins readily |

The absolute values vary between sources by tens of per cent and depend on temperature, alloying and solute segregation to the fault (Suzuki segregation); the **ranking** is what matters, and it is the ranking that propagates into every property listed in §4.9.

> [!warning] The fault is not a second phase
> A stacking fault is a *planar defect inside one phase*: same composition, same coordination, same lattice parameter, no interface in the thermodynamic sense. It therefore has no thickness, no separate diffraction pattern and no equilibrium tie-line — it appears in TEM only as a fringe pattern, in the diffraction pattern as streaks, and in the energy balance as a surface tension $\gamma_{SF}$ acting on the partials that bound it.

### 4.3 The Shockley partial: $\mathbf{b} = \tfrac{a}{6}\langle112\rangle$

The **Shockley partial** is the glissile half of a dissociated dislocation. Its Burgers vector is one-third of a close-packed translation, its magnitude is $b_p = a\sqrt{6}/6 = 0.408\,a = b/\sqrt{3}$, and — critically — it lies **in** the $\{111\}$ plane of the fault, so the partial can glide conservatively in that plane, converting perfect stacking into faulted stacking as it sweeps.

> [!important] Definitions
> **Shockley partial** — a partial dislocation with $\mathbf{b} = \tfrac{a}{6}\langle112\rangle$, lying in the $\{111\}$ fault plane it bounds. It is **glissile**: glide of the leading partial *creates* the fault, glide of the trailing partial *removes* it, and glide of the pair together translates the fault without changing its width.
> **Leading and trailing partial** — the two members of the pair. The one that moves first (into perfect crystal) leaves the fault behind it: the *leading* partial. The second one follows through the faulted strip and restores perfect stacking: the *trailing* partial. Which is which depends on the sense of the applied stress; reversal of the stress reverses their roles and the pair glides back.
> **Constriction** — the local recombination of the two partials into a single perfect dislocation, needed before the dislocation can cross-slip onto another plane. Requires the ribbon to be squeezed to zero width over some length, which costs energy $\propto \gamma_{SF}$.

> [!important] The dissociation, checked three ways
> 1. **Burgers-vector conservation.** The partial vectors must add to the parent vector:
>
> $$ \frac{a}{6}[2\bar{1}1] + \frac{a}{6}[1\bar{2}\bar{1}] = \frac{a}{6}[3\bar{3}0] = \frac{a}{2}[1\bar{1}0] \quad\checkmark $$
>
> 2. **Frank's rule (§2.5).** Dissociation is favourable only if the energy falls:
>
> $$ b_1^2 + b_2^2 = \frac{a^2}{6} + \frac{a^2}{6} = \frac{a^2}{3} \;<\; \frac{a^2}{2} = b^2 \quad\checkmark $$
>
> 3. **Geometry.** Both partials must lie *in the plane of the fault*, otherwise the pair cannot glide together: $[2\bar{1}1]\cdot[111] = 0$ and $[1\bar{2}\bar{1}]\cdot[111] = 0\ \checkmark$. Each partial is $30^\circ$ from the parent vector ($\cos\theta = \tfrac{3}{6} = 0.5$) and the two are $60^\circ$ apart, so their sum recovers the full $\tfrac{a}{2}\langle110\rangle$ magnitude: $2 b_p\cos30^\circ = 2(0.408a)(0.866) = 0.707a = b\ \checkmark$.

The $30^\circ$ angle is not an accident of the example — it is forced. See the H4 below.

Each $\{111\}$ plane contains three $\langle112\rangle$ axes, so six Shockley partial vectors when both senses are counted; over the four planes this gives **12 Shockley partial vectors** in the crystal, the same count as the 12 perfect $\tfrac{a}{2}\langle110\rangle$ vectors.

| Plane | The three $\langle112\rangle$ axes lying in it | Perfect vectors reproduced by a $60^\circ$ pair |
| --- | --- | --- |
| $(111)$ | $[2\bar{1}\bar{1}]$, $[\bar{1}2\bar{1}]$, $[\bar{1}\bar{1}2]$ | $\tfrac{a}{2}[\bar{1}10]$, $\tfrac{a}{2}[\bar{1}01]$, $\tfrac{a}{2}[0\bar{1}1]$ |
| $(\bar{1}11)$ | $[211]$, $[1\bar{2}1]$, $[1\bar{1}2]$ | $\tfrac{a}{2}[101]$, $\tfrac{a}{2}[\bar{1}01]$, $\tfrac{a}{2}[01\bar{1}]$ |
| $(1\bar{1}1)$ | $[2\bar{1}1]$, $[121]$, $[\bar{1}12]$ | $\tfrac{a}{2}[011]$, $\tfrac{a}{2}[\bar{1}10]$, $\tfrac{a}{2}[10\bar{1}]$ |
| $(11\bar{1})$ | $[21\bar{1}]$, $[112]$, $[\bar{1}\bar{1}\bar{2}]$ | $\tfrac{a}{2}[\bar{1}10]$, $\tfrac{a}{2}[101]$, $\tfrac{a}{2}[011]$ |

#### Why the partials sit at exactly $30^\circ$ to the parent

The angle is fixed by the requirement that the two partials be **equal in length and both in the fault plane**. Choose the parent vector in the fault plane and express it in the close-packed basis: because the $\langle112\rangle$ directions are the *shortest* lattice-irrational vectors in a $\{111\}$ plane and are spaced $60^\circ$ apart within it, the parent vector — which spans $60^\circ$ between two of them — can only be resolved as the sum of two equal vectors inclined $30^\circ$ to it. Any other pair would either be unequal (one partial would have a larger $b$ than the other, which Frank's rule rejects) or would leave the plane (which the ribbon forbids). Formally, in the orthonormal frame of the plane the three axes are $\pm(\hat{e}_1)$, $\pm(\tfrac12\hat{e}_1+\tfrac{\sqrt3}{2}\hat{e}_2)$, $\pm(\tfrac12\hat{e}_1-\tfrac{\sqrt3}{2}\hat{e}_2)$, and adding the first two successive axes returns a vector of length $\sqrt3 b_p = 0.707a$ inclined $30^\circ$ to each — precisely $\tfrac{a}{2}\langle110\rangle$.

### 4.4 The extended dislocation: width of the fault ribbon

Once split, the two partials are pushed apart by their elastic repulsion and pulled together by the fault they create. Writing the repulsion per unit length between two parallel dislocations separated by $d$ as

$$ F_{rep} = \frac{G}{2\pi d}\left[ b_s^{(1)} b_s^{(2)} + \frac{b_e^{(1)} b_e^{(2)}}{1-\nu} \right] $$

with $b_s$, $b_e$ the screw and edge components of each partial, and setting $F_{rep} = \gamma_{SF}$ (the fault tension, which acts like a surface tension per unit length) gives the equilibrium separation. With $b_p = b/\sqrt3$ and a partial at $30^\circ$ to the parent line:

| Parent dislocation | Character of the two partials | Equilibrium separation $d$ |
| --- | --- | --- |
| **Edge** | opposite screw components, same-sign edge components | $d = \dfrac{G\,b_p^{\,2}}{8\pi\,\gamma_{SF}}\cdot\dfrac{2+\nu}{1-\nu}$ |
| **Screw** | same-sign screw components, opposite edge components | $d = \dfrac{G\,b_p^{\,2}}{8\pi\,\gamma_{SF}}\cdot\dfrac{2-3\nu}{1-\nu}$ |

$$ \boxed{\ d \;\propto\; \frac{G\,b_p^{\,2}}{\gamma_{SF}} \qquad\Longleftrightarrow\qquad \gamma_{SF} = \frac{G\,b_p^{\,2}}{8\pi d}\cdot\frac{2+\nu}{1-\nu}\ \ (\text{edge})\ } $$

The scaling is the whole physics: a **high** $\gamma_{SF}$ pinches the ribbon shut, a **low** $\gamma_{SF}$ lets it spread. Because the prefactor is larger for the edge orientation, an edge dislocation is always dissociated *more widely* than a screw of the same material — which is why cross-slip (a screw process) is possible at all while climb and edge–obstacle interactions behave as if the core were wide.

| Metal | $G$ (GPa) | $\nu$ | $b$ (nm) | $\gamma_{SF}$ (mJ/m²) | $d$ edge (nm) | $d$ screw (nm) |
| --- | --- | --- | --- | --- | --- | --- |
| **Ag** | 30 | 0.38 | 0.289 | 22 | 5.8 | 2.4 |
| **Cu** | 48 | 0.34 | 0.256 | 45 | 3.3 | 1.4 |
| **Ni** | 76 | 0.31 | 0.249 | 125 | 1.7 | 0.7 |
| **Al** | 26 | 0.345 | 0.286 | 166 | 0.6 | 0.3 |

The widths above are computed from the boxed relation with typical handbook constants and are **illustrative** — they reproduce the magnitudes measured by weak-beam TEM (a few nm in Cu, sub-nm in Al) and, more importantly, the ordering.

> [!note] Constriction — why a low fault energy means planar glide
> To cross-slip, a screw dislocation must first **constrict**: the two partials have to be forced back into a single perfect line over some length $L$, which costs an energy of order $\gamma_{SF}\cdot L d$ per unit length released elsewhere — and the probability of that fluctuation is exponentially small in $\gamma_{SF} d^2/kT$.
> - **Narrow ribbon** (Al, Ni): cheap constriction $\Rightarrow$ cross-slip easy $\Rightarrow$ dislocations bypass obstacles and cluster into cells $\Rightarrow$ **wavy glide**, low work-hardening rate, Stage III starts early (§2.17).
> - **Wide ribbon** (brass, 304 stainless, Ag): expensive constriction $\Rightarrow$ cross-slip nearly forbidden $\Rightarrow$ **planar glide**, dislocations pile up on single planes $\Rightarrow$ very high work-hardening rate, strong tendency to twin (§2.2), and in austenitic steels the formation of $\varepsilon$-martensite.
> This single chain is why two FCC metals with identical crystal structure — aluminium and 70/30 brass — behave like different classes of material.

#### How the width is actually measured

- **Weak-beam dark-field TEM** resolves the two partials directly and the separation is read off the image once the foil thickness and the projection are corrected.
- **Triple-node geometry.** Where three extended dislocations meet, the equilibrium node radius $R$ is set by the balance of the three line tensions and the three fault tensions; measuring $R$ by conventional TEM gives $\gamma_{SF}$ through the Brown–Thölén relation $\gamma_{SF} = \dfrac{G b_p^2}{8\pi R}\left(\dfrac{2-\nu}{1-\nu}\right)\ln\!\left(\dfrac{R}{r_0}\right)$ — the standard route when the partials themselves are not resolvable.
- **Indirectly, from behaviour:** the onset temperature of cross-slip, the Stage II hardening rate ($\theta_{II}$ scales roughly as $1/\gamma_{SF}$), and the stress at which twinning starts.

### 4.5 Thompson's tetrahedron: the vector bookkeeping

![[SD - Thompson tetrahedron.excalidraw]]

The **Thompson tetrahedron** is a notation, not a new theory: a tetrahedron whose four faces are the four $\{111\}$ planes of the fcc crystal, whose six edges are the six $\langle110\rangle$ axes, and whose vertices $A$, $B$, $C$, $D$ name the faces *opposite* them. Every Burgers vector in this block is then a segment of the figure, and every reaction is a path along it. $\delta$ is the centroid of the face $ABC$; $\alpha$ the centroid of the face $BCD$.

| Segment | Vector | What it represents | Character |
| --- | --- | --- | --- |
| $AB$, $BC$, $CA$, $DA$, $DB$, $DC$ | $\tfrac{a}{2}\langle110\rangle$ | perfect dislocation, edge length $a/\sqrt2$ | glissile on the two faces containing the edge |
| $A\delta$, $B\delta$, $C\delta$ | $\tfrac{a}{6}\langle112\rangle$ | **Shockley partial** lying in the face $ABC$ | glissile in $ABC$ |
| $D\delta$ | $\tfrac{a}{3}\langle111\rangle$ | **Frank partial**, normal to $ABC$, length $a/\sqrt3$ | sessile |
| $\delta\alpha$ | $\tfrac{a}{6}\langle110\rangle$ | **stair-rod** where partials from two faces meet | sessile |

Two identities do most of the work:

$$ AB = A\delta + \delta B \quad\text{(the dissociation of a perfect dislocation)} $$

$$ D\delta + \delta B = DB \quad\text{(a Frank partial + a Shockley partial} \to \text{a perfect dislocation)} $$

The first is §4.1; the second is the **unfaulting** reaction of §4.7 — the fault is erased when a Shockley partial sweeps the faulted plane and merges with the Frank partial that bounded it. Thompson notation also shows at once why the **Lomer–Cottrell lock** (§2.5) is sessile: the stair-rod $\delta\alpha$ lies along the intersection of two faces and its $\mathbf{b}$ is *not* in any one of them.

> [!tip] Reading a reaction off the tetrahedron
> A reaction is allowed only if the two vectors can be drawn head-to-tail on the figure and the sum is again a segment. This instantly rules out the classic exam mistakes — e.g. pairing two Shockleys from *different* faces and expecting a perfect dislocation: their sum is a stair-rod of length $a/\sqrt{6}$... which is *shorter*, so the reaction is allowed energetically but the product is **sessile**, not glissile.

### 4.6 Frank partials: $\mathbf{b} = \tfrac{a}{3}\langle111\rangle$

![[SD - Frank partials slide.png|470]]

*Figure — the lecture slide on Frank partials: the faulted plane closed by an edge partial whose Burgers vector $\tfrac{a}{3}\langle111\rangle$ is normal to the fault, the geometry that makes the Frank partial sessile.*

The **Frank partial** is the second way a fault can terminate. Here the fault is a *single* close-packed plane — created, for instance, by removing one layer — and the dislocation that closes the gap does **not** lie in the plane; it is perpendicular to it, a pure edge dislocation with $\mathbf{b} = \tfrac{a}{3}\langle111\rangle$.

The magnitude is worth noticing: $|\tfrac{a}{3}[111]| = a\sqrt3/3 = a/\sqrt3$, which is **exactly the $\{111\}$ interplanar spacing** $d_{111}$.

$$ \boxed{\ \mathbf{b}_F = \frac{a}{3}\langle111\rangle,\qquad |\mathbf{b}_F| = \frac{a}{\sqrt3} = d_{111},\qquad b_F^2 = \frac{a^2}{3}\ } $$

Because $|\mathbf{b}|$ equals the spacing between the planes, the loop can close the gap with **no shear at all**: the two halves of the crystal are simply brought together by one plane spacing. That is the geometric statement of "the Frank partial is the fault vector of the collapsed layer".

> [!important] Definitions
> **Frank partial** — an edge partial dislocation with $\mathbf{b} = \tfrac{a}{3}\langle111\rangle$, perpendicular to the stacking fault it bounds. It terminates a fault that is confined to one plane and cannot glide, because its Burgers vector is normal to that plane.
> **Faulted loop** — a closed Frank partial loop enclosing a disc of stacking fault (a collapsed vacancy or interstitial plate). Vacancy type when the missing plane is inside the loop (intrinsic fault), interstitial type when an extra plane has been inserted (extrinsic fault).
> **Prismatic loop** — more generally, any loop whose $\mathbf{b}$ is normal to its plane; the Frank loop is the faulted, $\{111\}$-plane member of that family.

Why *sessile* is the defining property: a dislocation glides when its Burgers vector lies **in** the glide plane. Here $\mathbf{b} \perp$ fault plane, so any glide of the loop out of its plane would have to drag the fault disc with it — the fault would have to move through the crystal without growing, which is not a conservative process. The only conservative motion available is **climb**: the loop shrinks or grows by absorbing or emitting vacancies and interstitials, one plane at a time. This is why a Frank partial is a *strong, immovable barrier* to other dislocations, and why faulted loops persist in quenched and irradiated metals instead of annealing out at low temperature.

> [!warning] Two different "Frank rules" — do not merge them
> **Frank's rule (reactions)**, §2.5: $\mathbf{b}_1+\mathbf{b}_2\to\mathbf{b}_3$ is favourable if $b_3^2 < b_1^2 + b_2^2$. This decides whether a dissociation happens.
> **Frank's rule (faulted loops)**: a loop bounding a stacking fault must have its Burgers vector *normal to the fault plane and equal to the fault displacement vector*, otherwise it drags a second, higher-energy fault around the loop. For a $\{111\}$ fault the fault displacement is exactly $\tfrac{a}{3}\langle111\rangle$ — which is why there is only **one** species of Frank partial and not a family of them.
> Both are due to F. C. Frank, and exam questions often invoke the second while writing the first.

#### Why the faulted loop wins at small size and loses at large

A faulted loop carries two energies: the line energy $\alpha G b_F^2$ per unit length around its perimeter $\propto r$, and the fault energy $\gamma_{SF}$ times the enclosed area $\propto r^2$. A *perfect* loop avoids the fault entirely but must carry the larger vector $\tfrac{a}{2}\langle110\rangle$:

$$ E_{\text{frank}} = \alpha G\,\frac{a^2}{3}\,2\pi r + \gamma_{SF}\,\pi r^2 \qquad\text{versus}\qquad E_{\text{perfect}} = \alpha G\,\frac{a^2}{2}\,2\pi r $$

Subtracting, the faulted loop is stable while

$$ \gamma_{SF}\,\pi r^2 < \alpha G\,2\pi r\left(\frac{a^2}{2}-\frac{a^2}{3}\right) = \alpha G\,2\pi r\,\frac{a^2}{6} \quad\Longrightarrow\quad r < \frac{a^2 \alpha G}{3\,\gamma_{SF}} $$

so **small loops stay faulted, large loops unfault** — a result with direct consequences in §4.7 (irradiation damage) and in the annealing of quenched metals.

### 4.7 How Frank partials are made — and how they are removed

![[SD - Frank partial from a vacancy plate.excalidraw]]

1. **Supersaturate the metal with vacancies.** Quenching from near the melting point, or irradiating it, freezes in far more vacancies than equilibrium allows.
2. **The vacancies condense on a $\{111\}$ plane** — the close-packed plane, where the surface energy of the disc is lowest — forming a flat plate of missing atoms.
3. **The plate collapses.** The two half-crystals are pulled together by one interplanar spacing and the surrounding lattice relaxes into an **intrinsic stacking fault** on the plane of the plate.
4. **The rim of the faulted disc is a Frank partial loop** with $\mathbf{b} = \tfrac{a}{3}[111]$, a pure edge dislocation of vacancy type. When instead interstitials condense, the extra plane produces an **extrinsic** fault bounded by an interstitial-type Frank loop.

The loop is then locked in place: it cannot glide (§4.6), so it acts as an obstacle, contributes to hardening, and can disappear only by two routes.

> [!important] The two ways out for a faulted loop
> **Climb (needs diffusion).** The loop absorbs or emits point defects and shrinks plane by plane. This is a high-temperature process, and it is the annihilation route during annealing; below roughly $0.3T_m$ it is frozen out and the loops survive indefinitely.
> **Unfaulting by a Shockley sweep.** A Shockley partial is nucleated at the loop and sweeps the faulted plane; where it meets the far side of the loop it reacts with the Frank partial,
>
> $$ \underbrace{\frac{a}{3}[111]}_{\text{Frank}} + \underbrace{\frac{a}{6}[2\bar{1}1]}_{\text{Shockley}} \longrightarrow \frac{a}{6}[0\,3\,3] = \underbrace{\frac{a}{2}[011]}_{\text{perfect}} $$
>
> and the loop becomes a **perfect prismatic loop** — no fault, and now glissile along its prism. In Thompson's notation this is the identity $D\delta + \delta B = DB$ of §4.5.

Where this matters in practice:

| Situation | What forms | Consequence |
| --- | --- | --- |
| **Quenched Al, Cu, Au** | faulted vacancy loops on $\{111\}$, a few nm to tens of nm | hardening; loops visible as fringe contrast in TEM; a classic demonstration of vacancy supersaturation |
| **Neutron- or ion-irradiated metals** | vacancy Frank loops *and* interstitial loops; in fcc, **stacking-fault tetrahedra** at high dose | radiation hardening and embrittlement; the loops pin glide dislocations |
| **Austenitic stainless steels (reactor internals)** | dense Frank-loop populations | the dominant contribution to irradiation hardening; also solute segregation to the loops |
| **Ion-implanted silicon** | $\{311\}$ defects and Frank loops in the damaged layer | residual damage after anneal, leakage in devices |
| **Fatigue and cyclic loading** | partials and faults in planar-slip alloys | the persistent slip bands of low-SFE metals are built from dissociated dislocations |
| **Annealing / recovery** | unfaulting then climb | loop density falls; hardness returns towards the annealed value |

> [!note] Why faulted loops are such effective hardeners
> A gliding dislocation cannot cut a faulted loop — the loop's $\mathbf{b}$ is out of every glide plane, so there is no reaction that removes it, and the fault must be dragged or sheared at high energy cost. The Orowan-type bypass stress therefore stays high even for loops only a few nanometres across, and the hardening per unit volume is far larger than for the same volume fraction of coherent precipitates. This is the microscopic origin of the "radiation hardening" that raises the yield stress and drops the ductility of reactor structural steels.

#### The stacking-fault tetrahedron

If a small triangular Frank loop on $\{111\}$ becomes unstable at its corners, it can dissociate into a tetrahedron bounded by **four** intrinsic faults on the four faces and six stair-rod dislocations along the edges — the **stacking-fault tetrahedron** (Silcox–Hirsch). It contains *no* Frank partial at all, is completely sessile, and is the characteristic defect of quenched gold and of heavily irradiated fcc metals. It is the one defect in this block that is stable, invisible to glide dislocations in every orientation, and removed only by vacancy emission at high temperature — a useful exam cameo of the fact that a faulted defect will always find the configuration of lowest total energy, even at the cost of inventing new partials.

### 4.8 Shockley versus Frank — the comparison to write out

| | **Shockley partial** | **Frank partial** |
| --- | --- | --- |
| Burgers vector | $\tfrac{a}{6}\langle112\rangle$ | $\tfrac{a}{3}\langle111\rangle$ |
| Magnitude | $a/\sqrt6 = 0.408a$ | $a/\sqrt3 = 0.577a = d_{111}$ |
| $b^2$ | $a^2/6$ | $a^2/3$ |
| $\mathbf{b}$ vs fault plane | **lies in** the fault plane | **perpendicular** to the fault plane |
| Character | mixed, $30^\circ$ to the parent $\mathbf{b}$ | pure edge |
| Mobility | **glissile** — glides conservatively in the $\{111\}$ plane | **sessile** — climb only |
| Effect of its glide | creates (leading) or erases (trailing) the fault; the pair translates the fault | cannot glide at all; its loop bounds a fixed fault disc |
| Fault it is associated with | intrinsic fault ribbon (dynamic, width $d$) | the single fault plane of a collapsed disc (static) |
| How it is created | dissociation of a perfect $\tfrac{a}{2}\langle110\rangle$ | collapse of a vacancy (or interstitial) plate; climb from a Shockley partial |
| How it is removed | recombination into the perfect dislocation (constriction) | climb, or unfaulting by a Shockley sweep |
| Found in | every fcc metal and alloy, always | quenched, irradiated, implanted and fatigued metals |
| Effect on properties | sets cross-slip, work-hardening rate, twinning tendency | hardening, radiation embrittlement, loop pinning |
| Thompson symbol | $A\delta$, $B\delta$, $C\delta$ | $D\delta$ |

### 4.9 What the stacking-fault energy controls

Because $\gamma_{SF}$ fixes the ribbon width $d$ (§4.4), and $d$ fixes how easily a dislocation can constrict, $\gamma_{SF}$ is a master variable. The chain of consequences, all of them already met in earlier blocks:

| $\gamma_{SF}$ | Ribbon | Cross-slip | Work hardening | Twinning | Microstructure in TEM | Example |
| --- | --- | --- | --- | --- | --- | --- |
| **High** ($\gtrsim$100 mJ/m²) | narrow | easy | low rate, long Stage III | rare | dislocation cells, wavy slip lines | Al, Ni |
| **Medium** (40–100) | moderate | possible at high $T$ | moderate | occasional | cells + planar arrays | Cu |
| **Low** ($\lesssim$25) | wide | very difficult | high rate, extended Stage II | easy | planar arrays, faulted dipoles, twins | Ag, brass, 304 SS, fcc Co |

- **Work hardening (§2.17).** $\theta_{II}$ rises as $\gamma_{SF}$ falls, because dislocations cannot cross-slip past each other and pile up instead. This is the whole difference between deep-drawing aluminium and deep-drawing brass.
- **Twinning (§2.2).** A deformation twin in fcc is built by the passage of $\tfrac{a}{6}\langle112\rangle$ partials on successive $\{111\}$ planes — the same partials as §4.3, one plane apart, *not* recombining. Low $\gamma_{SF}$ lowers the stress for this, hence the TWIP steels and the twinning of 70/30 brass.
- **Martensite.** The $\varepsilon$ (hcp) martensite of austenitic steels is nothing but an intrinsic fault on every second plane, i.e. the stacking sequence converted from $ABC$ to $AB$; low $\gamma_{SF}$ makes it form spontaneously on cooling or straining.
- **Recovery and creep.** Climb of extended dislocations requires constriction first, so a wide ribbon slows recovery; in the same way the climb of Frank loops sets the annealing kinetics of irradiated material.
- **Fatigue.** Planar-slip (low $\gamma_{SF}$) metals form sharp persistent slip bands and extrude intrusions easily — they fatigue-crack from the surface; wavy-slip metals distribute strain and form cells.

---

> [!tip] Exam pointer — Shockley and Frank partials
> Have ready: (i) the dissociation equation with its **three checks** — vector sum, Frank's rule $a^2/2 \to a^2/3$ (33 %), and the geometric requirement that both partials lie in the fault plane at $30^\circ$ to the parent; (ii) $b_p = a/\sqrt6$, $b_F = a/\sqrt3 = d_{111}$, and $b_F^2 = a^2/3$; (iii) the boxed scaling $d \propto G b_p^2/\gamma_{SF}$ with the edge result $\tfrac{2+\nu}{1-\nu}$, and the sentence that **constriction is what cross-slip costs**, so a wide ribbon means planar glide; (iv) the Thompson construction — edge $=$ perfect, vertex-to-centroid $=$ Shockley, apex-to-centroid $=$ Frank, centroid-to-centroid $=$ stair-rod; (v) the **unfaulting** reaction Frank $+$ Shockley $=$ perfect; and (vi) the one trap: the Frank partial is sessile **because $\mathbf{b}$ is normal to the fault plane**, not because it is an edge dislocation.

## Formula Summary — Partial Dislocations

| Quantity | Expression | Notes |
| --- | --- | --- |
| Perfect dislocation (fcc) | $b = \tfrac{a}{2}\langle110\rangle$, $b^2 = a^2/2$ | Lattice translation; leaves no fault |
| Shockley partial | $b_p = \tfrac{a}{6}\langle112\rangle$, $b_p^2 = a^2/6 = b^2/3$ | Lies **in** the $\{111\}$ fault plane; glissile |
| Frank partial | $b_F = \tfrac{a}{3}\langle111\rangle$, $b_F^2 = a^2/3$, $\lvert b_F\rvert = a/\sqrt3 = d_{111}$ | Normal to the fault plane; sessile |
| Stair-rod partial | $b = \tfrac{a}{6}\langle110\rangle$ | At the intersection of two faults; sessile |
| Dissociation criterion (Frank's rule) | $b_1^2 + b_2^2 < b^2$ | $\Rightarrow a^2/3 < a^2/2$: 33 % saving, always favourable in fcc |
| Standard dissociation | $\tfrac{a}{2}[\bar{1}10] \to \tfrac{a}{6}[2\bar{1}1] + \tfrac{a}{6}[1\bar{2}\bar{1}]$ | Both partials in $(111)$; $60^\circ$ apart, $30^\circ$ from $b$ |
| Partial/perfect magnitude ratio | $b_p = b/\sqrt3$ | Fixed by the $30^\circ$ geometry |
| Repulsion between partials | $F = \dfrac{G}{2\pi d}\left[b_s^{(1)}b_s^{(2)} + \dfrac{b_e^{(1)}b_e^{(2)}}{1-\nu}\right]$ | Per unit length; balance with $\gamma_{SF}$ |
| Ribbon width, edge parent | $d = \dfrac{G b_p^2}{8\pi\gamma_{SF}}\cdot\dfrac{2+\nu}{1-\nu}$ | Widest ribbons; sets the core width |
| Ribbon width, screw parent | $d = \dfrac{G b_p^2}{8\pi\gamma_{SF}}\cdot\dfrac{2-3\nu}{1-\nu}$ | Narrower; governs cross-slip (§2.17) |
| Fault tension balance | $\gamma_{SF} = F_{rep}(d)$ | Equilibrium width, no external stress |
| Node method for $\gamma_{SF}$ | $\gamma_{SF} = \dfrac{G b_p^2}{8\pi R}\cdot\dfrac{2-\nu}{1-\nu}\ln\!\left(\dfrac{R}{r_0}\right)$ | Brown–Thölén; $R$ = node radius |
| Faulted vs perfect loop | faulted (Frank) stable while $r < \dfrac{a^2\alpha G}{3\gamma_{SF}}$ | Small loops faulted, large loops unfault |
| Unfaulting reaction | $\tfrac{a}{3}[111] + \tfrac{a}{6}[2\bar{1}1] \to \tfrac{a}{2}[011]$ | Frank $+$ Shockley $=$ perfect; $D\delta + \delta B = DB$ |
| Thompson identities | $AB = A\delta + \delta B$; $D\delta + \delta B = DB$ | Edges $=$ perfect; $D\delta$ $=$ Frank |
| Fault energy from stacking | $\gamma_{SF}\sim 20$–$170\ \text{mJ/m}^2$ | Ranking, not the absolute value, drives behaviour |

> [!note] Source images
> The lecture deck [[Shockley and Frank partial dislocations_Odd_2026-27.pdf]] contains only three slides — a title slide and one figure slide for each partial type; both figure slides are extracted above and stored in `Material Science/images/` as `SD - Shockley partials slide.png` and `SD - Frank partials slide.png`. All four Excalidraw diagrams in this block (vector triangle, stacking sequence, Thompson tetrahedron, vacancy-disc collapse) are original reconstructions, stored in `Excalidraw/` with the `SD - ` prefix.

---

# Composites

A composite is what you get when two materials that would not naturally form one phase are forced to work together: one continuous **matrix** holds and protects a **dispersed** phase that carries load, adds stiffness, or supplies some other function. The engineering interest is not the average of the two properties but the *combination* — stiffness without density, strength without brittleness, toughness without weight. This block builds that idea from the definition (§5.1) through the classification (§5.4), the two strengthening strategies for particles (§5.6–§5.8), the shear-lag and rule-of-mixtures mechanics of fibres (§5.9–§5.11), the three matrix families (§5.13–§5.15), processing (§5.17), structural laminates and sandwich panels (§5.18), and nanocomposites (§5.19). It closes with the applications that make the subject recognisable — skis, the Boeing 787, and automotive body panels (§5.20).

Compiled from the lecture slides ([[Composites_Odd_2026-27.pdf]], 66 slides) and the handwritten class notes in [[MO NOTES (1).pdf]] (pp. 132–152). The slides follow **Callister, *Fundamentals of Materials Science and Engineering*** (Ch. 16).

> [!info] How the block fits together
> **§5.1–§5.5** establish the vocabulary — what a composite is, the matrix/dispersed-phase pair, and the five geometric variables (size, shape, concentration, orientation, distribution) that decide the properties. **§5.6–§5.8** treat particle-reinforced systems: large-particle (continuum load sharing, rule of mixtures, cermets, concrete) and dispersion-strengthened (dislocation pinning that survives high temperature). **§5.9–§5.12** treat fibre-reinforced systems: critical fibre length, load transfer, the isostrain/isostress extremes, and what the fibre and matrix must each do. **§5.13–§5.16** compare polymer-, metal- and ceramic-matrix composites and hybrids. **§5.17–§5.19** cover processing, structural laminates/sandwich panels and nanocomposites. **§5.20** puts the whole block into service.

---

## 5. Composites

### 5.1 What is a composite?

The lecture opens with the definition that carries the whole topic: a composite is not a new compound but a *mixture of phases*, deliberately arranged so that the strengths of each constituent cover the weaknesses of the other. The constituents come from the three familiar families — metals, ceramics and polymers — and they remain distinguishable in the finished material.

> [!important] Definitions
> **Composite** — a material composed of two (or more) individual materials that come from the well-known categories of materials — metals, ceramics and polymers — combined to achieve a combination of properties not displayed by any single material.
> **Matrix** — the continuous phase. It surrounds the dispersed phase, binds the reinforcement together, protects it, and transmits the applied stress to it.
> **Dispersed phase (reinforcement)** — the discontinuous phase. It may be particulate, fibrous or lamellar; it is the phase that usually carries the load, raises the stiffness, or resists deformation.
> **Interface** — the boundary between matrix and dispersed phase. It is not a passive surface: stress transfer, debonding, crack deflection and fibre pullout all happen there.

The objective is stated as two clauses, and both matter:

1. **Achieve a combination of properties that is not displayed by any single material.** A single material cannot be simultaneously stiff, strong, tough and light; a composite can be *tailored* towards that combination.
2. **Incorporate the best characteristics of each component.** The matrix contributes toughness, ductility, processing ease and environmental protection; the reinforcement contributes stiffness and strength.

Nature got there first. Two examples are worth remembering because they show the two archetypal geometries — fibre in a matrix, and brittle particles in a soft matrix:

| Natural composite | Matrix | Dispersed phase | What the combination achieves |
| --- | --- | --- | --- |
| **Wood** | Lignin | Cellulose fibres | Stiff, strong cellulose fibres held in a softer lignin matrix; the fibre direction gives wood its grain and anisotropy |
| **Bone** | Collagen (a protein) | Hydroxyapatite (predominantly calcium phosphate) | A hard but brittle mineral supplies stiffness and compressive strength; the soft, flexible collagen supplies toughness |

The first engineered example in the lecture is the one everybody knows:

- **Fibreglass** — small glass fibres embedded in a polymeric material (epoxy or polyester).
- Glass fibres are relatively **strong and stiff**, but also **brittle**.
- The polymer matrix is **more flexible** and binds the fibres together.
- The result is relatively **stiff, strong and flexible**, and it has a **low density** — a combination that neither bulk glass nor bulk polymer offers.

#### Why not just an alloy?

*Added depth beyond the slides.* An alloy is a single-phase solid solution (or a set of phases grown from the melt) in which the atoms are mixed on the atomic scale; there is no deliberate, separately shaped second component. A composite keeps its constituents as distinct phases with a *designed* interface between them. That interface is the extra degree of freedom: it can be made strong enough to transfer stress, weak enough to debond and absorb energy, or chemically chosen to protect the reinforcement. The price is that the interface is also the weak link — the place where water, oxygen or a crack first attacks.

### 5.2 A catalogue of engineering composites

The lecture then walks through four composites that between them cover the design space: a high-performance polymer-matrix composite, a metal-matrix composite, a dispersion-strengthened metal, and a large-particle ceramic composite.

- **Carbon-fibre-reinforced polymer (CFRP).** Carbon fibres replace glass fibres in a polymer matrix. CFRP is **stiffer and stronger than glass-fibre-reinforced materials but more expensive**. It is used in aircraft and aerospace structures, high-tech sporting equipment (bicycles, golf clubs, tennis rackets, skis and snowboards) and, more recently, automobile bumpers.
- **Aluminium–boron (Al–B) composite.** Boron has **low density and a high elastic modulus ($E = 440\ \text{GN m}^{-2}$)**, but it is **brittle**. Boron is therefore used as a reinforcing fibre in a **ductile aluminium matrix**. The elastic modulus of the composite is increased by the boron fibres, and — the key point — **the ductile matrix stops a propagating crack if a fibre embedded in it breaks accidentally**. If the entire material were boron only, a propagating crack would run through the whole cross-section and cause catastrophic fracture.
- **Thoria-dispersed nickel.** The high-temperature strength of nickel alloys is enhanced significantly by adding about **3 vol.% thoria ($\text{ThO}_2$)** as finely dispersed particles.
- **Concrete.** A common **large-particle composite**: an aggregate of sand/gravel particles bound together in a solid body by a binding medium, cement.

The boron example is the cleanest statement of the matrix's fracture-mechanical job. The fibre is the stiff, strong phase; the matrix is the tough, ductile phase that *blunts* a crack when a fibre breaks, so failure of one fibre does not become failure of the component.

The lecture also notes that composites are not confined to structural materials. **Semiconductor-based composites** exist too, and their nomenclature is fixed: the composite is designated by the **matrix first, followed by the dispersed semiconductor phase** — for example Ni/TiO$_2$, Ni/CdS, Pt/TiO$_2$, Zn/TiO$_2$, polypyrrole/TiO$_2$, phthalocyanine/ZnO and Nafion/CdS (K. Rajeshwar *et al.*, *Chem. Mater.* **2001**, *13*, 2765–2782). The same matrix-first convention is used throughout this block.

| Composite | Matrix | Dispersed phase | Property combination sought |
| --- | --- | --- | --- |
| **CFRP** | Polymer (epoxy) | Carbon fibres | High specific stiffness and strength; fatigue resistance; low density |
| **GFRP (fibreglass)** | Polyester/epoxy | Glass fibres | Stiffness and strength at low cost; electrical insulation; corrosion resistance |
| **Al–B** | Aluminium | Boron fibres | High modulus with a ductile, crack-arresting matrix |
| **TD nickel** | Nickel alloy | 3 vol.% $\text{ThO}_2$ particles | High-temperature strength retained by inert particles |
| **Cermet** | Cobalt or nickel | WC or TiC particles | Hardness plus toughness; cutting-tool life |
| **Concrete** | Cement paste | Sand and gravel aggregate | Compressive strength and rigidity at low cost |

#### The interface is the third phase

*Added depth beyond the slides.* It is tempting to treat a composite as "fibre plus matrix", but every property that makes the composite useful is transmitted through the interface. A strong bond transfers stress efficiently and lets the fibre reach its strength; a weak bond debonds early, which lowers strength but can raise toughness by allowing pullout and crack bridging. The interface also decides environmental durability: water ingress along a fibre–matrix interface is the classic failure path in marine GFRP. This is why the later sections keep returning to **bond strength** and **fibre pullout** rather than treating adhesion as a detail.

### 5.3 Where composites stand among materials

The lecture places composites on the same room-temperature property charts used for metals, ceramics and polymers. The point is not that composites beat every material on every axis — they do not — but that they occupy a *region* of the chart that no single family reaches.

![[COMP - Room temperature density of material families.png|440]]
*Figure — room-temperature density on a logarithmic scale: the composite band (carbon-fibre and glass-fibre reinforced polymers, CFRP/GFRP) lies at the low-density end, alongside polymers and wood and well below steels and most ceramics.*

![[COMP - Room temperature stiffness of material families.png|440]]
*Figure — room-temperature elastic (Young's) modulus: composites span a wide range because the fibre type and volume fraction can be changed; CFRP reaches the high-stiffness region, while GFRP sits at intermediate stiffness.*

![[COMP - Room temperature tensile strength of material families.png|440]]
*Figure — room-temperature tensile strength: the composite band overlaps the upper end of the light alloys and reaches towards the high-strength steels, but the important quantity for design is strength per unit density (see below).*

![[COMP - Room temperature fracture toughness of material families.png|440]]
*Figure — room-temperature fracture toughness: composites lie between the low-toughness ceramics and the tough metals; the matrix and the fibre–matrix interface control how much energy is absorbed.*

![[COMP - Room temperature electrical conductivity of material families.png|440]]
*Figure — room-temperature electrical conductivity, spanning many orders of magnitude: carbon fibres are conductive, glass fibres and polymers are insulating, so a composite's conductivity can be tailored from the fibre type and content.*

| Property | Where composites sit | Consequence for design |
| --- | --- | --- |
| **Density** | Low, comparable with polymers and light alloys | Specific properties are high even when absolute values are not |
| **Stiffness** | Wide range, from GFRP to CFRP | Fibre type and volume fraction are the design knobs |
| **Tensile strength** | Moderate to high; not automatically above steels | Strength-to-weight, not strength alone, is the selection criterion |
| **Fracture toughness** | Intermediate; below tough metals, above ceramics | Damage tolerance depends on matrix plasticity and interface debonding |
| **Electrical conductivity** | Tailorable from insulating to conductive | Carbon-filled polymers can dissipate static; glass-filled polymers remain insulators |

#### Specific strength and specific modulus

*Added depth beyond the slides.* The charts explain why aerospace, sports equipment and transport use composites: the selection indices are not $E$ and $\sigma$ but $E/\rho$ and $\sigma/\rho$.

$$ \text{specific strength}=\frac{\sigma}{\rho}, \qquad \text{specific modulus}=\frac{E}{\rho} $$

A steel may have a higher absolute modulus than a GFRP, but its density is roughly four times larger, so the *specific* modulus can favour the composite. This is the same logic that makes a hollow tube better in bending than a solid rod: what matters is how much stiffness or strength each kilogram buys.

### 5.4 Classification of composites

Composites are classified first by the **geometry of the dispersed phase**, and then by the **strengthening mechanism** inside each class.

![[COMP - Classification of Composites.excalidraw]]

> [!important] The four classes
> **Particle-reinforced** — the dispersed phase is **equiaxed**, i.e. its dimensions are approximately the same in all directions. Subdivided into **large-particle** and **dispersion-strengthened** composites according to the size of the particles and the mechanism.
> **Fibre-reinforced** — the dispersed phase has the geometry of a **fibre**, i.e. a large length-to-diameter ratio. Subdivided by fibre length and orientation: continuous and aligned, discontinuous and aligned, discontinuous and random.
> **Structural** — **multi-layered** composites designed to have low densities and high degrees of structural integrity; the common forms are laminates and sandwich panels.
> **Nanocomposites** — the dimensions of the dispersed-phase particles are on the order of **nanometres**.

| Class | Dispersed-phase geometry | Dominant strengthening mechanism | Examples |
| --- | --- | --- | --- |
| **Large-particle** | Equiaxed, particle size above the atomic scale | Continuum load sharing: particles restrain matrix flow | Cermets, concrete, filled polymers |
| **Dispersion-strengthened** | Equiaxed, 10–100 nm | Dislocation pinning by fine inert particles | TD nickel, SAP (Al–Al$_2$O$_3$) |
| **Fibre-reinforced** | Large $l/d$ | Load transfer from matrix to fibre along the interface | CFRP, GFRP, aramid composites |
| **Structural** | Layered or sandwich | Geometry of the layers carries bending and shear | Laminates, honeycomb panels |
| **Nanocomposite** | Nanometre-scale | Surface/quantum effects; huge interfacial area | Nanoclay–polymer, CNT–epoxy |

The broad differences stated in the lecture are worth keeping as a checklist:

- **Particle-reinforced:** equiaxed particles; the matrix transfers some of the applied stress to the particles, which bear a fraction of the load.
- **Fibre-reinforced:** the dispersed phase is a fibre with a large length-to-diameter ratio; the fibre carries load along its axis.
- **Structural:** multi-layered, low density, high structural integrity; the *geometric design* of the layers is as important as the constituent materials.
- **Nanocomposites:** dispersed-phase dimensions on the order of nanometres; the surface-to-volume ratio and quantum effects become important.

#### Length scale decides the mechanism

*Added depth beyond the slides.* Two composites with the same volume fraction of the same second phase can behave completely differently if the phase is a 50 nm particle, a 50 µm particle, or a 5 mm fibre. The nanoparticle pins dislocations; the large particle forces the matrix to flow around it; the fibre carries load along its length. This is why the classification is by *geometry* first and *chemistry* second — the mechanism, and therefore the design equation, follows the geometry.

### 5.5 The matrix and the dispersed phase

Many composites contain just two phases. One is the **matrix**, which is continuous and surrounds the other; the other is the **dispersed phase**, which is often called the reinforcement.

> [!important] What controls the properties
> The properties of a composite are a function of three things:
> 1. the properties of the constituent phases;
> 2. their **relative amounts** (volume fractions);
> 3. the **geometry** of the dispersed phase — its size, shape, concentration, orientation and distribution.

The geometry is not a single number. The lecture lists five descriptors, and each one changes a different part of the behaviour:

| Geometric variable | What it controls | Example of the effect |
| --- | --- | --- |
| **Size** | Whether the mechanism is continuum or atomic; the critical length for fibres | 10–100 nm particles pin dislocations; coarse particles share load by continuum mechanics |
| **Shape** | Stress concentration and load path | Equiaxed particle → isotropic reinforcement; fibre → directional reinforcement |
| **Concentration** | The magnitude of the rule-of-mixtures contribution | More fibre → higher modulus, until processing or bonding limits intervene |
| **Orientation** | Anisotropy | Aligned fibres give high axial stiffness and low transverse stiffness; random fibres give more isotropy |
| **Distribution** | Uniformity of stress transfer | Uniform dispersion gives uniform properties; agglomerates create stress concentrations and weak paths |

This is exactly why the same fibre and the same resin can produce a stiff unidirectional laminate or a more isotropic chopped-fibre panel: the chemistry is unchanged, the geometry is not.

#### Volume fraction versus weight fraction

*Added depth beyond the slides.* The rule-of-mixtures equations are written in **volume fractions** because stress is carried by area, and area fractions equal volume fractions when the phases run the same length. Manufacturers often quote **weight fractions**, so the conversion is worth having. For a two-phase composite with weight fractions $w_f$ and $w_m$ and densities $\rho_f$ and $\rho_m$:

$$ V_f=\frac{w_f/\rho_f}{w_f/\rho_f+w_m/\rho_m}, \qquad V_m=1-V_f $$

A 50 wt.% carbon-fibre composite is therefore *more* than 50 vol.% fibre, because carbon is lighter than the resin. Mixing the two conventions is one of the commonest numerical errors in composite problems.

#### Why uniform distribution matters

*Added depth beyond the slides.* A composite with the correct average volume fraction can still be poor if the reinforcement is clumped. An agglomerate behaves like one large particle with a weak interface; the surrounding matrix is unreinforced, so the applied strain concentrates in the matrix and the composite fails before the fibres reach their strength. The lecture's statement that "better overall composite properties are realized when the fibre distribution is uniform" is therefore a processing requirement, not an aesthetic one.

### 5.6 Particle-reinforced composites

Particle-reinforced composites are divided into two classes by the **size of the particles** and the **strengthening mechanism** that operates.

> [!important] Two particle mechanisms
> **Large-particle composite** — the particles are large enough that particle–matrix interactions cannot be treated on the atomic or molecular level; **continuum mechanics** is used. The particles are harder and stiffer than the matrix, restrain the matrix in their vicinity, and bear a fraction of the load. The degree of reinforcement depends on **strong bonding at the matrix–particle interface**.
> **Dispersion-strengthened composite** — the particles are much smaller, with diameters between **0.01 and 0.1 µm (10 and 100 nm)**. Particle–matrix interactions occur on the atomic or molecular level; the matrix bears the major portion of the load, while the small particles **hinder or impede the motion of dislocations**. Plastic deformation is restricted, so yield strength, tensile strength and hardness all increase.

The distinction is mechanical, not semantic. In a large-particle composite the particle is a *phase* that the matrix must flow around; in a dispersion-strengthened composite the particle is an *obstacle* to dislocation motion.

#### The rule of mixtures for a two-phase composite

For a two-phase composite loaded in parallel (both phases experience the same strain — the **isostrain** or **Voigt** bound), the stiffness is the volume-fraction-weighted arithmetic mean:

$$ \boxed{\ E_{c(u)}=E_mV_m+E_pV_p\ } $$

For loading in series (both phases experience the same stress — the **isostress** or **Reuss** bound), the compliance is the weighted mean and the modulus is the harmonic mean:

$$ \boxed{\ E_{c(l)}=\frac{E_mE_p}{V_mE_p+V_pE_m}\ } $$

Here $E$ and $V$ denote elastic modulus and volume fraction; the subscripts $c$, $m$ and $p$ represent composite, matrix and particulate phases. The upper bound is the **stiffest possible** two-phase arrangement; the lower bound is the **most compliant**.

![[COMP - Rule of mixtures copper tungsten.png|380]]
*Figure — upper and lower bounds for a copper–tungsten composite with tungsten as the particle phase. Experimental points lie between the bounds and closer to the lower bound at intermediate compositions, because an equiaxed particulate composite is neither a perfect parallel nor a perfect series arrangement.*

> [!note] Why the bounds bracket the data
> The upper bound assumes the two phases strain together, so the stiff phase is fully mobilised. The lower bound assumes they carry the same stress, so the soft phase is fully compliant. A real equiaxed particle composite lies in between: the stress state around each particle is neither uniform strain nor uniform stress. Elongated or interconnected particles push the response towards the upper bound; isolated equiaxed particles sit closer to the lower bound.

#### Cermets

**Cermets** are ceramic–metal composites and the classic example of a large-particle composite used with all three material classes. The most common cermet is **cemented carbide**: extremely hard particles of a refractory carbide ceramic such as **tungsten carbide (WC)** or **titanium carbide (TiC)** embedded in a matrix of a metal such as **cobalt or nickel**.

- Used extensively as **cutting tools for hardened steels**.
- **Toughness is enhanced** by the ductile metal matrix, which isolates the carbide particles from one another and prevents particle-to-particle crack propagation.
- Both matrix and particulate phases are **refractory** to the high temperatures generated by the cutting action on extremely hard materials.
- No single material could provide the combination of properties of a cermet; relatively large volume fractions of the particulate phase may be used, often **exceeding 90 vol.%**.

#### Carbon black–reinforced rubber

Both elastomers and plastics are frequently reinforced with particulate materials. Many modern rubbers would be severely restricted without **carbon black** — very small, essentially spherical carbon particles produced by the combustion of natural gas or oil in an atmosphere with a limited air supply.

- Added to vulcanised rubber, this extremely inexpensive material enhances **tensile strength, toughness, and tear and abrasion resistance**.
- Automobile tyres contain on the order of **15 to 30 vol.% carbon black**.
- For significant reinforcement the particle size must be extremely small, with diameters between **20 and 50 nm**; the particles must be **evenly distributed** through the rubber and must form a **strong adhesive bond** with the rubber matrix.
- Particle reinforcement with other materials (e.g. silica) is much less effective because the special interaction between the rubber molecules and the particle surfaces does not exist.

### 5.7 Concrete — a large-particle ceramic composite

Concrete is the most widely used composite in the world, and it is unusual because **both** the matrix and the dispersed phase are ceramics. The distinction between **cement** and **concrete** is worth stating explicitly: cement is the binding medium (a powder that reacts with water), while concrete is the composite of cement paste plus aggregate.

- The two most familiar concretes are made with **Portland** and **asphaltic** cements, in which the aggregate is gravel and sand.
- **Asphaltic concrete** is used primarily as a paving material; **Portland cement concrete** is used extensively as a structural building material.
- Portland cement concrete is a major construction material primarily because it can be **poured in place** and **hardens at room temperature**, even when submerged in water.

Portland cement concrete also has limitations as a structural material:

- Like most ceramics, it is **relatively weak and extremely brittle**; its **tensile strength is approximately 1/15 to 1/10 of its compressive strength**.
- Large concrete structures experience considerable **thermal expansion and contraction** with temperature fluctuations.
- **Water penetrates external pores**, which can cause severe cracking in cold weather as a consequence of **freeze–thaw cycles**.

#### The ingredients and the mixing problem

The ingredients of Portland cement concrete are Portland cement, a **fine aggregate (sand)**, a **coarse aggregate (gravel)**, and water.

- The aggregate particles act as a **filler** to reduce the overall cost, because aggregate is cheap while cement is relatively expensive.
- To achieve optimum strength and workability, the ingredients must be added in the correct proportions.
- **Dense packing** and good interfacial contact are achieved by having particles of two different sizes: fine sand particles fill the void spaces between the gravel particles.
- Typically, the aggregates constitute between **60% and 80% of the total volume**.

The cement–water paste must be sufficient to coat all the sand and gravel particles; otherwise the cementitious bond is incomplete. All constituents must be thoroughly mixed, and the water quantity is critical:

- **Too little water** → incomplete bonding.
- **Too much water** → excessive porosity.
- In either case the final strength is less than the optimum.
- The **size distribution** of the aggregate influences the amount of cement–water paste required.
- Surfaces must be **clean and free from clay and silt**, which prevent a sound bond at the particle surface.

#### Reinforced concrete

The strength of Portland cement concrete can be increased by additional reinforcement — usually **steel rods, wires, bars (rebar) or mesh** embedded into the fresh, uncured concrete.

Steel is a suitable reinforcement because:

1. its **coefficient of thermal expansion is nearly the same as that of concrete**;
2. steel is **not rapidly corroded** in the cement environment;
3. a relatively **strong adhesive bond** forms between steel and cured concrete.

Concrete can also be reinforced by mixing **fibres** of a high-modulus material such as glass, steel, nylon or polyethylene into the fresh concrete. Care is needed because some fibre materials deteriorate rapidly in the cement environment.

#### Prestressed concrete

Another technique introduces **residual compressive stresses** into the structural member; the result is **prestressed concrete**.

- High-strength steel wires are positioned inside empty moulds and stretched with a high tensile force, which is maintained constant.
- After the concrete is placed and allowed to harden, the tension is released.
- As the wires contract, they put the structure into **compression** because the stress is transmitted to the concrete through the concrete–wire bond.
- A variant in which the stress is applied **after** the concrete hardens is called **posttensioning**.

#### Why concrete is strong in compression and weak in tension

*Added depth beyond the slides.* Concrete is a particulate composite held together by a cementitious matrix. Under compression, the aggregate particles are pushed together and the matrix is confined; under tension, the matrix cracks open, the crack runs around the aggregate, and there is little resistance once the cementitious bridges fail. Prestressing works by pre-loading the concrete in compression so that the tensile stress from service loads must first cancel that compression before any crack can open. This is the same principle as a pre-tensioned bolt in a joint, applied at the scale of a beam.

### 5.8 Dispersion-strengthened composites

Dispersion-strengthened composites contain a **uniform dispersion of several volume per cent of fine particles of a very hard and inert material**. The particles may be metallic or non-metallic; oxide materials are often used.

The strengthening mechanism is the same one that operates in precipitation hardening: the particles interact with **dislocations** in the matrix and make it harder for them to move. The difference is the *stability* of the particles:

- In a **dispersion-strengthened** composite the particles are chosen to be **unreactive with the matrix**, so the strengthening is **retained at elevated temperatures and for extended time periods**.
- In a **precipitation-hardened** alloy the increase in strength may **disappear on heat treatment** because the precipitates grow (coarsen) or dissolve.

That single distinction is the whole reason dispersion strengthening exists: it is a way to keep a fine obstacle population at a temperature where normal precipitates would coarsen away.

| Feature | Precipitation hardening | Dispersion strengthening |
| --- | --- | --- |
| Particle source | Nucleated from the matrix by heat treatment | Added as a separate powder/phase |
| Particle size | Typically nanometres, but coarsens with time | 10–100 nm, stable |
| Matrix–particle reaction | The particle is a phase in local equilibrium | Particle chosen to be inert |
| High-temperature stability | Strength falls on over-ageing or solution treatment | Strength retained to high temperature |
| Typical example | Al–Cu alloys (GP zones, $\theta''$) | TD nickel, SAP (Al–Al$_2$O$_3$) |

Examples named in the lecture:

- **Thoria-dispersed nickel (TD nickel)** — fine $\text{ThO}_2$ particles in a nickel matrix; the high-temperature strength is retained because the oxide does not react with the matrix.
- **Aluminium–aluminium oxide (SAP, sintered aluminium powder)** — a thin, adherent alumina coating on the surface of extremely small aluminium flakes (**0.1 to 0.2 µm thick**), dispersed within an aluminium metal matrix.

> [!note] Why the particles must be inert
> A dispersion-strengthened composite is designed for the temperature range where the matrix would normally soften. If the particle dissolved or coarsened, the obstacle spacing would increase and the strengthening would vanish — exactly what happens when a precipitation-hardened alloy is over-aged. The oxide particles work because they are thermodynamically stable and essentially insoluble in the matrix.

### 5.9 Fibre-reinforced composites

Fibre-reinforced composites contain the dispersed phase in the form of a **fibre**. The design goals are stated in terms of weight:

- **High strength and/or stiffness on a weight basis**, i.e. high **specific strength** and **specific modulus**.
- **Low-density fibre and matrix materials** are used to reach very high specific strength and specific modulus.
- Further classification is based on **fibre length**: continuous (long) or discontinuous (short), and on orientation: aligned or randomly oriented.

![[COMP - Fiber orientation and concentration.png|420]]
*Figure — the three fibre architectures: continuous and aligned, discontinuous and aligned, and discontinuous and randomly oriented. Better overall composite properties are realized when the fibre distribution is uniform.*

#### Fibre length and load transfer

The mechanical characteristics of a fibre-reinforced composite depend on two things:

1. **the properties of the fibre**, and
2. **the degree of transmittance of the applied load from the matrix to the fibres**.

The extent of load transmittance depends on the magnitude of the **interfacial bond** between fibre and matrix. At each fibre extremity there is no load transmittance from the matrix, so the tensile stress in the fibre must build up from zero at the end to its maximum somewhere along the length.

![[COMP - Matrix deformation around fiber ends.png|380]]
*Figure — matrix deformation around a fibre: the matrix shears near the fibre ends, and there is no load transfer at the very extremities. The fibre stress therefore rises from zero at each end towards the centre.*

The **critical fibre length** $l_c$ is the shortest length for which the fibre can be loaded to its ultimate tensile strength by the matrix:

$$ \boxed{\ l_c=\frac{\sigma_f^*d}{2\tau_c}\ } $$

where $d$ is the fibre diameter, $\sigma_f^*$ is the ultimate tensile strength of the fibre, and $\tau_c$ is the **fibre–matrix bond strength** or the **shear yield strength of the matrix**, whichever is smaller. For a number of glass- and carbon-fibre–matrix combinations this critical length is on the order of **1 mm**, which is between **20 and 150 times the fibre diameter**.

![[COMP - Fiber stress profiles at critical length.png|430]]
*Figure — stress–position profiles for a fibre-reinforced composite loaded to the fibre tensile strength $\sigma_f^*$: (a) $l=l_c$, where the maximum fibre stress is reached only at the axial centre; (b) $l>l_c$, where the fibre is more effectively loaded; (c) $l<l_c$, where the fibre never reaches its strength and pulls out instead of fracturing.*

Fibres for which $l\gg l_c$ — usually $l>15l_c$ — are termed **continuous**; **discontinuous** or **short** fibres have lengths shorter than this.

#### Derivation of the critical length

> [!important] The critical-length derivation, step by step
> 1. Consider a fibre of diameter $d$ carrying a tensile stress $\sigma_f$. The tensile force on a cross-section is
>    $$F_f=\sigma_f\frac{\pi d^2}{4}$$
> 2. The matrix feeds load into the fibre by **shear along the interface**. Over the half-length $l/2$ from one end to the centre, the interfacial area is $\pi d(l/2)$, so the maximum shear force the interface can supply is
>    $$F_\tau=\tau_c\,\pi d\,\frac{l}{2}$$
> 3. At the critical length the fibre just reaches its strength at the centre, so the two forces balance:
>    $$\sigma_f^*\frac{\pi d^2}{4}=\tau_c\,\pi d\,\frac{l_c}{2}$$
> 4. Cancelling $\pi d$ and solving for $l_c$:
>    $$l_c=\frac{\sigma_f^*d}{2\tau_c}$$
> 5. The correct $\tau_c$ is the **smaller** of the interfacial bond strength and the matrix shear yield strength, because the weaker of the two mechanisms limits load transfer.

#### Why $l>15l_c$ is called "continuous"

*Added depth beyond the slides.* The average stress carried by a fibre of length $l$ is reduced from the peak by the unloaded regions at its two ends. The factor is approximately $(1-l_c/2l)$: at $l=l_c$ the average is only half the fibre strength, at $l=5l_c$ it is 90%, and at $l=15l_c$ it is about 97%. Beyond that point, making the fibre longer buys almost nothing, so $l>15l_c$ is treated as "continuous" for design purposes.

### 5.10 Continuous and aligned fibre composites

When the fibres are continuous and aligned, the mechanical response depends on:

- the **stress–strain behaviour of the fibre and matrix phases**,
- the **volume fractions** of the two phases, and
- the **direction in which the stress or load is applied**.

Because the fibres are aligned, the properties are **highly anisotropic**: they depend on the direction in which they are measured. The composite is stiff and strong along the fibre direction and much more compliant and weaker across it.

![[COMP - Stress strain stages of aligned composite.png|460]]
*Figure — tensile loading along the fibre direction. Stage I: both fibres and matrix deform elastically. Stage II: the matrix yields and deforms plastically at $\varepsilon_{ym}$ while the fibres continue to stretch elastically. The onset of composite failure begins as the fibres start to fracture, at a strain of approximately $\varepsilon_f^*$.*

The two stages are the key to reading the curve:

- **Stage I** — the fibre–matrix bond is intact and both phases strain together; the slope is the composite modulus $E_{cl}$.
- **Stage II** — the matrix has yielded, so it contributes little additional stiffness; the fibres continue to carry the increasing load elastically.
- **Failure** — the fibres begin to fracture at about $\varepsilon_f^*$. Because the fibres are brittle, this strain is usually much smaller than the matrix failure strain $\varepsilon_m^*$.

#### Why composite failure is not catastrophic

Composite failure is not catastrophic for two reasons:

1. **Not all fibres fracture at the same time** — there is always considerable variation in the fracture strength of brittle fibre materials.
2. **Even after fibre failure the matrix is still intact**, because $\varepsilon_f^*<\varepsilon_m^*$.

The fractured fibres, now shorter than the original ones, are still embedded in the intact matrix and can sustain a diminished load as the matrix continues to deform plastically. The composite therefore retains load-carrying capacity after the first fibre breaks; it does not separate instantly.

#### Elastic behaviour in longitudinal loading — the isostrain state

The assumption is that the fibre–matrix interfacial bond is very good, so the matrix and fibres deform by the same amount. This is the **isostrain** state.

> [!important] Longitudinal modulus, step by step
> 1. The total load on the composite is the sum of the loads on the two phases:
>    $$F_c=F_m+F_f$$
> 2. Using $F=\sigma A$:
>    $$\sigma_cA_c=\sigma_mA_m+\sigma_fA_f$$
> 3. Divide by $A_c$:
>    $$\sigma_c=\sigma_m\frac{A_m}{A_c}+\sigma_f\frac{A_f}{A_c}$$
> 4. If the matrix and fibre run the same length, the area fractions equal the volume fractions, so
>    $$\sigma_c=\sigma_mV_m+\sigma_fV_f$$
> 5. The isostrain condition is $\varepsilon_c=\varepsilon_m=\varepsilon_f$. Substituting $\sigma=E\varepsilon$ and cancelling the common strain:
>    $$E_{cl}=E_mV_m+E_fV_f$$
> 6. Since $V_m+V_f=1$, this is equivalently
>    $$E_{cl}=E_m(1-V_f)+E_fV_f$$

![[COMP - Isostrain vs Isostress.excalidraw]]

$$ \boxed{\ E_{cl}=E_mV_m+E_fV_f=E_m(1-V_f)+E_fV_f\ } $$

The same volume-fraction rule applies to **density**:

$$ \rho_c=\rho_mV_m+\rho_fV_f $$

and the ratio of the load carried by the fibres to the load carried by the matrix is

$$ \boxed{\ \frac{F_f}{F_m}=\frac{E_fV_f}{E_mV_m}\ } $$

#### Elastic behaviour in transverse loading — the isostress state

When the load is applied perpendicular to the fibres, the two phases are in series: they carry the **same stress**, and the total strain is the volume-fraction-weighted sum of the phase strains. This is the **isostress** state.

> [!important] Transverse modulus, step by step
> 1. Isostress: $\sigma_c=\sigma_m=\sigma_f=\sigma$.
> 2. The composite strain is the weighted sum:
>    $$\varepsilon_c=\varepsilon_mV_m+\varepsilon_fV_f$$
> 3. Substitute $\varepsilon=\sigma/E$ and cancel the common stress:
>    $$\frac{1}{E_{ct}}=\frac{V_m}{E_m}+\frac{V_f}{E_f}$$
> 4. Invert:
>    $$E_{ct}=\frac{E_mE_f}{V_mE_f+V_fE_m}$$

$$ \boxed{\ E_{ct}=\frac{E_mE_f}{V_mE_f+V_fE_m}\ } $$

This is analogous to the **lower bound** for a particle-reinforced composite, while the longitudinal case is analogous to the **upper bound**.

#### Tensile strength

The **longitudinal tensile strength** is dominated by the fibre strength:

$$ \boxed{\ \sigma_{cl}^*=\sigma_m'(1-V_f)+\sigma_f^*V_f\ } $$

where $\sigma_f^*$ is the fibre fracture strength and $\sigma_m'$ is the **stress in the matrix when the composite fails** — i.e. the matrix stress at the fibre failure strain $\varepsilon_f^*$, not the matrix tensile strength.

The **transverse tensile strength** is a different problem. Whereas longitudinal strength is dominated by fibre strength, a variety of factors significantly influence the transverse strength:

- the properties of **both** the fibre and the matrix,
- the **fibre–matrix bond strength**,
- the presence of **voids**.

Measures used to improve transverse strength usually involve **modifying the properties of the matrix**, because in transverse loading the matrix is the continuous load path.

#### Why the longitudinal modulus is an arithmetic mean

*Added depth beyond the slides.* In isostrain loading the stiff phase is forced to strain by the same amount as the soft phase, so its stress is proportional to its modulus and it dominates the load. The composite modulus is therefore a **stiffness-weighted average**. In isostress loading the soft phase is free to strain more, so it dominates the *compliance*; the modulus is a **compliance-weighted average**, which is always lower than the arithmetic mean. This is the same parallel/series distinction as resistors or springs, and it explains why $E_{cl}>E_{ct}$ for every real composite.

#### Load sharing in a real composite

*Added depth beyond the slides.* The ratio $F_f/F_m=E_fV_f/E_mV_m$ is the reason a small volume fraction of carbon fibre can transform a polymer. For a typical carbon–epoxy system $E_f/E_m$ is of order 50–100; at $V_f=0.6$ the fibres carry the great majority of the axial load. The matrix's job is not to carry load but to **transfer** it and to protect the fibres. This is also why matrix-dominated properties (transverse strength, shear, compression) are the weak directions of a unidirectional laminate.

#### Anisotropy is the design variable

*Added depth beyond the slides.* A unidirectional composite has $E_{cl}$ along the fibres and $E_{ct}$ across them, with $E_{cl}\gg E_{ct}$. That is not a defect; it is a licence to put stiffness only where the load path needs it. A beam that is bent in one plane can be made with fibres along its length; a pressure vessel needs fibres in more than one direction; a laminate can be built from plies at 0°, ±45° and 90° to approximate an isotropic in-plane response (§5.18).

### 5.11 Discontinuous and randomly oriented fibre composites

Discontinuous fibres are shorter than the continuous case, so the reinforcement efficiency is lower — but they are increasingly important commercially because they can be processed by ordinary polymer methods. **Chopped-glass fibres** are used most extensively; carbon and aramid discontinuous fibres are also used. These short-fibre composites can be produced with moduli of elasticity and tensile strengths that approach **90% and 50%**, respectively, of their continuous-fibre counterparts.

#### Discontinuous and aligned fibres

For a discontinuous and aligned-fibre composite with a uniform fibre distribution and $l>l_c$, the longitudinal strength is

$$ \boxed{\ \sigma_{cd}^*=\sigma_f^*V_f\left(1-\frac{l_c}{2l}\right)+\sigma_m'(1-V_f)\ } $$

where $\sigma_f^*$ and $\sigma_m'$ are the fibre fracture strength and the matrix stress at composite failure, respectively. The factor $(1-l_c/2l)$ is the same end-effect correction that appeared in §5.9: the shorter the fibre relative to $l_c$, the smaller the average stress it carries.

If the fibre length is **less than critical** ($l<l_c$), the fibre never reaches its fracture strength; it pulls out or yields at the interface instead. The longitudinal strength is then controlled by the interfacial shear strength:

$$ \boxed{\ \sigma_{cd}^*=\frac{\tau_cl}{d}V_f+\sigma_m'(1-V_f)\ } $$

where $d$ is the fibre diameter and $\tau_c$ is the smaller of the fibre–matrix bond strength and the matrix shear yield strength.

#### Discontinuous and randomly oriented fibres

When the fibre orientation is random, short and discontinuous fibres are normally used. A similar rule-of-mixtures equation gives the elastic modulus:

$$ \boxed{\ E_{cd}=KE_fV_f+E_mV_m\ } $$

Here $K$ is a **fibre efficiency parameter** that depends on $V_f$ and the $E_f/E_m$ ratio. Its magnitude is less than unity, usually in the range **0.1 to 0.6**. For random-fibre reinforcement, as for oriented-fibre reinforcement, the modulus increases with increasing volume fraction of fibre.

The price of randomness is anisotropy's opposite: the composite is more isotropic in-plane, but it is much less stiff than an aligned composite at the same $V_f$. The following table from the lecture makes the point with polycarbonate reinforced by randomly oriented glass fibres.

| Property | Unreinforced | 20 vol% glass | 30 vol% glass | 40 vol% glass |
| --- | --- | --- | --- | --- |
| **Specific gravity** | 1.19–1.22 | 1.35 | 1.43 | 1.52 |
| **Tensile strength**, MPa (ksi) | 59–62 (8.5–9.0) | 110 (16) | 131 (19) | 159 (23) |
| **Modulus of elasticity**, GPa ($10^6$ psi) | 2.24–2.345 (0.325–0.340) | 5.93 (0.86) | 8.62 (1.25) | 11.6 (1.68) |
| **Elongation**, % | 90–115 | 4–6 | 3–5 | 3–5 |
| **Impact strength, notched Izod**, ft·lb/in | 12–16 | 2.0 | 2.0 | 2.5 |

The table is a compact lesson in composite trade-offs: stiffness and strength rise steeply with fibre content, while **ductility collapses** — elongation falls from 90–115% to a few per cent — and impact strength drops by an order of magnitude. A composite is not a free lunch; it is a different balance.

#### Fibre orientation and reinforcement efficiency

The efficiency of reinforcement depends on the angle between the fibre axis and the stress axis:

| Fibre orientation | Stress direction | Reinforcement efficiency |
| --- | --- | --- |
| **All fibres parallel** | Parallel to fibres | 1 |
| **All fibres parallel** | Perpendicular to fibres | 0 |
| **Random, uniform in a plane** | Any direction in that plane | $3/8$ |
| **Random, uniform in three dimensions** | Any direction in space | $1/5$ |

![[COMP - Reinforcement efficiency of fiber orientations.png|420]]
*Figure — the four fibre-orientation cases and their reinforcement efficiency: aligned fibres loaded along their axis ($1$), aligned fibres loaded across their axis ($0$), random in-plane ($3/8$) and random in three dimensions ($1/5$).*

> [!warning] Efficiency is not a property of the fibre
> The efficiency factor is a *geometric* multiplier, not a materials constant. The same fibre can be fully effective (parallel), useless (perpendicular), or intermediate (random) depending only on how it is laid down relative to the load. This is why the laminate stacking sequence in §5.18 is a design decision, not a manufacturing afterthought.

#### Why $K$ is smaller than one

*Added depth beyond the slides.* In a random short-fibre composite, only the component of fibre length along the load axis contributes stiffness, and the end regions of every fibre are poorly loaded. $K$ lumps both losses together: the orientation average and the finite-length end effect. It rises towards the upper end of the 0.1–0.6 range when the fibres are longer, better bonded, and more nearly aligned with the load.

### 5.12 Fibres and the matrix — what each must do

Fibres are grouped into three classifications on the basis of **diameter and character**: whiskers, fibres and wires.

| Type | Diameter / character | Strengths and limitations | Typical materials |
| --- | --- | --- | --- |
| **Whiskers** | Very thin single crystals; extremely large length-to-diameter ratio | High crystalline perfection and virtually flaw-free → exceptionally high strength; among the strongest known materials. Extremely expensive and difficult to incorporate into a matrix | Graphite, SiC, $\text{Si}_3\text{N}_4$, $\text{Al}_2\text{O}_3$ |
| **Fibres** | Polycrystalline or amorphous; small diameters | Good strength and stiffness; available in continuous or chopped form; the workhorse reinforcement | Aramid polymers, glass, carbon, boron, $\text{Al}_2\text{O}_3$, SiC |
| **Wires** | Relatively large diameters | High strength and stiffness; used where a robust, large-diameter reinforcement is acceptable | Steel, molybdenum, tungsten; radial tyre reinforcement, filament-wound rocket casings, wire-wound high-pressure hoses |

The matrix has several distinct functions in a fibre-reinforced composite:

1. **Bind the fibres together** and act as the medium by which an externally applied stress is transmitted and distributed to the fibres.
2. **Protect the individual fibres from surface damage** caused by mechanical abrasion or chemical reactions with the environment. Such interactions may introduce surface flaws capable of forming cracks, which can lead to failure at low tensile stress levels.
3. **Separate the fibres** and, by virtue of its relative softness and plasticity, **prevent the propagation of brittle cracks from fibre to fibre**, which could otherwise cause catastrophic failure.

In addition, it is essential that **adhesive bonding forces between fibre and matrix be high** to minimise fibre pullout, and that bonding be adequate to maximise stress transmittance from the weak matrix to the strong fibres.

> [!important] The matrix's job in one sentence
> The matrix is not the strong phase; it is the **load-transfer medium, the protector and the crack stopper**. A composite with strong fibres and a poor matrix fails by debonding or by fibre-to-fibre crack propagation before the fibres reach their strength.

#### Fibre pullout versus fibre fracture

*Added depth beyond the slides.* A fibre that is shorter than $l_c$ cannot be loaded to its fracture strength, so it pulls out; a fibre longer than $l_c$ fractures. Both behaviours can be useful. Fracture gives high strength; pullout absorbs energy and raises toughness, because friction along the debonded interface does work. This is the same trade-off that appears in ceramic-matrix composites (§5.15), where whisker pullout is deliberately encouraged.

### 5.13 Polymer-matrix composites

**Polymer-matrix composites (PMCs)** consist of a polymer resin as the matrix and fibres as the reinforcement medium. They are used in the greatest diversity of composite applications, and in the largest quantities, because of their room-temperature properties, ease of fabrication and cost. In this context the term **resin** denotes a high-molecular-weight reinforcing plastic.

PMCs are classified according to the reinforcement type: **glass**, **carbon** and **aramid**.

#### Glass fibre-reinforced polymer composites

**Fibreglass** is a composite consisting of glass fibres, either continuous or discontinuous, contained within a polymer matrix. It is produced in the largest quantities. The glass most commonly drawn into fibres is **E-glass**; fibre diameters normally range between **3 and 20 µm**.

Advantages of glass as a fibre reinforcement:

1. Easily drawn into high-strength fibres from the molten state.
2. Readily available and may be fabricated into a glass-reinforced plastic economically.
3. Relatively strong fibre that can produce very high specific strength composites.
4. Chemical inertness, making the composite useful in corrosive environments.

Limitations:

1. **Not very stiff** — it does not display the rigidity necessary for some applications (e.g. structural members for airplanes and bridges).
2. Limited to service temperatures **below 200°C**; at higher temperatures most polymers begin to flow or deteriorate. High-purity fused silica fibres and high-temperature polymers such as polyimide resins extend the range to about **300°C**.

Applications: automotive and marine bodies, plastic pipes, storage containers and industrial floorings. The transportation industry is using increasing amounts of glass-fibre-reinforced plastics to decrease vehicle weight and boost fuel efficiency.

#### Carbon fibre-reinforced polymer composites

Carbon is a high-performance fibre material and the most commonly used reinforcement in advanced (non-fibreglass) polymer-matrix composites.

Advantages of carbon as a reinforcement:

1. High **specific moduli and specific strengths**.
2. Retains high tensile modulus and high strength at elevated temperatures; high-temperature **oxidation** can be a problem.
3. At room temperature, not affected by moisture or a wide variety of solvents, acids and bases.
4. Exhibits a diversity of physical and mechanical characteristics, allowing composites to be engineered for specific properties.
5. Relatively inexpensive and cost-effective fibre- and composite-manufacturing processes.

Carbon fibres are classified by tensile modulus as **standard, intermediate, high and ultrahigh modulus**. Fibre diameters normally range between **4 and 10 µm**; both continuous and chopped forms are available. They are normally coated with a protective **epoxy size** that also improves adhesion to the polymer matrix.

Applications: sports and recreational equipment (fishing rods, golf clubs), filament-wound rocket motor cases, pressure vessels, and aircraft structural components — military and commercial, fixed-wing and helicopters (wing, body, stabilizer and rudder components).

#### Aramid fibre-reinforced polymer composites

Aramid fibres are high-strength, high-modulus materials introduced in the early 1970s. They have outstanding strength-to-weight ratios, superior to metals. Chemically the group is **poly(paraphenylene terephthalamide)**; the common trade names are **Kevlar** and **Nomex**, with several grades (Kevlar 29, 49 and 149) having different mechanical behaviour.

During synthesis the rigid molecules are aligned along the fibre axis as **liquid-crystal domains**; the repeat unit and chain alignment are shown in the lecture. Mechanically, aramid fibres have longitudinal tensile strengths and moduli higher than other polymeric fibres, but they are **relatively weak in compression**. They are known for **toughness, impact resistance, and resistance to creep and fatigue**. Despite being thermoplastics, they are resistant to combustion and stable over a wide temperature range, retaining high mechanical properties between **−200°C and 200°C**. Chemically they are susceptible to degradation by strong acids and bases, but relatively inert in other solvents and chemicals.

Aramid fibres are most often used in polymer matrices, commonly epoxies and polyesters. Applications: ballistic products (bulletproof vests and armour), sporting goods, tyres, ropes, missile cases, pressure vessels, and as a replacement for asbestos in automotive brake and clutch linings and gaskets.

| Fibre | Absolute stiffness | Absolute strength | Weakness | Best-fit applications |
| --- | --- | --- | --- | --- |
| **E-glass** | Moderate | Moderate | Not stiff; service limit $\sim$200°C | Marine, automotive, pipes, tanks, insulation |
| **Carbon** | High | High | Cost; oxidation at high temperature | Aerospace, pressure vessels, sports equipment |
| **Aramid** | High along fibre | High along fibre | Weak in compression; acid/base attack | Ballistics, ropes, tyres, impact-resistant panels |

> [!note] Why aramid is strong in tension but weak in compression
> *Added depth beyond the slides.* Aramid fibres are built from rigid rod-like chains aligned along the fibre axis, held by strong inter-chain hydrogen bonds. That structure is excellent in tension, because the load is carried along the aligned chains. In compression the same fibrillar structure buckles and splits, so the compressive strength is much lower. Design with aramid where the load is tensile or impact-driven, not where the component is compression-critical.

### 5.14 Metal-matrix composites

**Metal-matrix composites (MMCs)** have a ductile metal matrix. The reinforcement is added to allow the composite to be used at **higher service temperatures** than the base metal, or to improve specific stiffness, specific strength, abrasion resistance, creep resistance, thermal conductivity and dimensional stability.

The advantages of MMCs over polymer-matrix composites are:

- **higher operating temperatures**,
- **nonflammability**,
- **greater resistance to degradation by organic fluids**.

The disadvantage is that **MMCs are more expensive than PMCs**.

| Feature | Polymer-matrix composite (PMC) | Metal-matrix composite (MMC) |
| --- | --- | --- |
| Matrix | Epoxy, polyester, thermoplastic | Al, Mg, Ti, Cu alloys; superalloys |
| Service temperature | Room temperature to $\sim$200–300°C | Higher; limited by matrix |
| Flammability | Polymer-dependent | Nonflammable |
| Organic-fluid resistance | Degrades in some solvents | Generally good |
| Cost | Lower | Higher |
| Typical reinforcement | Glass, carbon, aramid fibres | SiC particles/whiskers, Al$_2$O$_3$, carbon, boron, refractory metals |

Usual matrix materials are alloys of **Al, Mg, Ti, Cu** or superalloys. Reinforcement may be in the form of **particulates, continuous and discontinuous fibres, and whiskers**, with concentrations normally between **10 and 60 vol%**. Continuous-fibre reinforcements include carbon, silicon carbide, boron, aluminium oxide and refractory metals. Discontinuous reinforcements consist primarily of **SiC whiskers**, chopped fibres of **Al$_2$O$_3$ and carbon**, and particulates of **SiC and Al$_2$O$_3$**.

Sometimes a **protective surface coating** on the reinforcement, or tuning of the matrix alloy composition, is necessary to prevent high-temperature degradation.

Processing of MMCs has two steps:

1. **Consolidation/synthesis** — introduction of the reinforcement into the matrix.
2. **Shaping operation** — for discontinuous-fibre MMCs this can be done by standard metal-forming operations such as rolling, forging or extrusion.

Applications named in the lecture:

- Automobile engine components made of Al-alloy matrix reinforced with Al-oxide and carbon fibres (light weight, wear resistance and thermal-distortion resistance).
- Driveshafts, extruded stabilizer bars, forged suspension and transmission components.
- Advanced Al-alloy MMCs in aerospace, because of low density and control over thermal and mechanical properties.
- Continuous graphite fibres as reinforcement for an antenna boom on the **Hubble Space Telescope**.
- **GPS satellites** use SiC–Al and graphite–Al MMCs for electronic packaging and thermal-management systems.
- The high-temperature creep and rupture properties of some Ni- and Co-based superalloys are enhanced by fibre reinforcement with refractory metals such as tungsten (turbine-engine applications).

> [!note] Why MMCs exist at all
> *Added depth beyond the slides.* A polymer matrix is limited by the softening or decomposition of the polymer, and a ceramic matrix is limited by brittleness. A metal matrix occupies the middle ground: it keeps a useful fraction of its strength at temperatures where polymers are unusable, it conducts heat, and it can be shaped by metalworking. The reinforcement then adds the stiffness or wear resistance that the monolithic alloy lacks. The price is density and cost — which is why MMCs are used in aerospace, automotive and satellite hardware rather than in disposable consumer goods.

### 5.15 Ceramic-matrix composites

The fracture toughness of ceramics can be improved significantly by **ceramic-matrix composites (CMCs)**, which consist of particles, fibres or whiskers of one ceramic material embedded in a matrix of another ceramic. The improvement comes from **interactions between an advancing crack and the dispersed phase**: cracks initiate in the matrix, but crack propagation is hindered by the particles, fibres or whiskers.

Crack propagation may be retarded by several toughening mechanisms:

- **Transformation toughening** (described in detail below).
- **Ceramic whiskers** (e.g. SiC/Si$_3$N$_4$), which may inhibit crack propagation by:
  1. **deflecting crack tips**,
  2. **forming bridges across crack faces**,
  3. **absorbing energy during pullout** as the whiskers debond from the matrix, and/or
  4. **causing a redistribution of stresses** in regions adjacent to the crack tips.

In general, increasing fibre content improves strength and fracture toughness. CMCs also exhibit improved **high-temperature creep behaviour** and **resistance to thermal shock**. They may be fabricated by **hot pressing, hot isostatic pressing, and liquid-phase sintering**.

Applications: **SiC whisker-reinforced alumina** is used as cutting-tool inserts for machining hard metal alloys; tool lives for these materials are greater than for cemented carbides.

#### Transformation toughening

Transformation toughening uses a **phase transformation** to arrest the propagation of cracks.

- Small particles of **partially stabilised zirconia** are dispersed within a matrix material, often $\text{Al}_2\text{O}_3$ or $\text{ZrO}_2$ itself.
- Typically **CaO, MgO, Y$_2$O$_3$ and CeO$_2$** are used as stabilisers.
- Partial stabilisation leaves the zirconia in a **metastable tetragonal phase** rather than the stable monoclinic phase.
- The stress field in front of a propagating crack causes these metastably retained tetragonal particles to transform to the stable **monoclinic** phase.
- Accompanying the transformation is a slight **particle volume increase**. The net result is that **compressive stresses are established on the crack surfaces near the crack tip**, which tend to pinch the crack shut and arrest its growth.

![[COMP - Transformation toughening in zirconia.png|440]]
*Figure — the transformation-toughening mechanism: (a) a crack approaching tetragonal $\text{ZrO}_2$ particles; (b) crack arrestment after the stress-induced tetragonal-to-monoclinic transformation has generated compressive stresses on the crack faces.*

> [!important] Transformation toughening, step by step
> 1. Stabilisers (CaO, MgO, Y$_2$O$_3$, CeO$_2$) are added so that $\text{ZrO}_2$ retains the **tetragonal** phase at room temperature instead of transforming to monoclinic.
> 2. A crack tip generates a **stress concentration** in the surrounding matrix.
> 3. The tetragonal particles inside that stress field transform to **monoclinic**.
> 4. The transformation involves a **volume increase**, so the surrounding matrix is put into compression.
> 5. The compressive stress acts on the crack faces near the tip, **pinching the crack shut** and reducing the driving force for further growth.

#### Carbon–carbon composites

**Carbon–carbon composites** are carbon-fibre-reinforced carbon-matrix composites. They are relatively new and expensive because of the complex processing.

- High tensile moduli and tensile strengths, retained to **$T>2000$°C**.
- Creep resistance and relatively large fracture-toughness values.
- Low coefficients of thermal expansion and relatively high thermal conductivities → relatively low susceptibility to **thermal shock**.
- The major drawback is a **propensity to high-temperature oxidation**.

Applications: rocket motors, friction materials in aircraft and high-performance automobiles, hot-pressing moulds, components for advanced turbine engines, and ablative shields for re-entry vehicles.

| CMC | Matrix | Reinforcement | Attraction |
| --- | --- | --- | --- |
| **SiC whisker-reinforced alumina** | $\text{Al}_2\text{O}_3$ | SiC whiskers | Cutting-tool inserts; longer tool life than cemented carbides |
| **Transformation-toughened zirconia** | $\text{Al}_2\text{O}_3$ or $\text{ZrO}_2$ | Metastable tetragonal $\text{ZrO}_2$ | Crack arrest by stress-induced transformation |
| **Carbon–carbon** | Carbon | Carbon fibres | Strength and creep resistance above 2000°C; thermal shock resistance |

### 5.16 Hybrid composites

A **hybrid composite** contains two or more different kinds of fibres in a single matrix, giving a better all-round combination of properties than a composite with only one fibre type.

The most common system incorporates both **carbon and glass fibres** into a polymeric resin:

- **Carbon fibres** are strong and relatively stiff, and provide low-density reinforcement, but they are expensive.
- **Glass fibres** are inexpensive but lack the stiffness of carbon.
- The **glass–carbon hybrid** is stronger and tougher, has higher impact resistance, and may be produced at a lower cost than either the comparable all-carbon or all-glass reinforced plastic.

The two fibre types may be combined in several ways, and the arrangement affects the overall properties: the fibres may all be aligned and intimately mixed, or laminations may be constructed with layers of a single fibre type alternating with one another. In virtually all hybrids the properties are **anisotropic**.

When hybrid composites are stressed in tension, failure is usually **non-catastrophic**:

1. The **carbon fibres fail first**, and the load is transferred to the glass fibres.
2. On failure of the glass fibres, the **matrix** must sustain the applied load.
3. Eventual composite failure coincides with failure of the matrix phase.

Principal applications are lightweight land, water and air transport structural components, sporting goods, and lightweight orthopaedic components.

> [!tip] The hybrid design idea
> A hybrid is the composite equivalent of alloying: instead of accepting one fibre's property profile, you mix two profiles to buy toughness from one and stiffness from the other. The failure sequence above is the mechanical signature — the brittle, stiff carbon fails first, the ductile glass and matrix pick up the load, and the component gives warning instead of separating.

### 5.17 Processing of fibre-reinforced composites

The three processes described in the lecture are all ways of putting continuous fibres into a resin and then shaping and curing the result.

#### Pultrusion

**Pultrusion** is used for components with **continuous lengths and a constant cross-sectional shape** — rods, tubes, beams and similar profiles.

1. Continuous-fibre **rovings or tows** are impregnated with a thermosetting resin.
2. The wet stock is pulled through a **steel die** that preforms it to the desired shape and establishes the resin/fibre ratio.
3. The stock then passes through a **curing die**, precision-machined to the final shape and heated to initiate curing of the resin matrix.
4. A **pulling device** draws the stock through the dies and determines the production speed.
5. Tubes and hollow sections are made by using **centre mandrels or inserted hollow cores**.

Typical reinforcement content is **40–70 vol%** glass, carbon or aramid fibres; matrices are polyesters, vinyl esters or epoxy resins.

#### Prepreg

**Prepreg** is the composite industry's term for continuous-fibre reinforcement preimpregnated with a polymer resin that is only **partially cured**.

1. A series of spool-wound continuous-fibre tows is collimated.
2. The tows are sandwiched and pressed between sheets of **release and carrier paper** using heated rollers — a process called **calendering**.
3. The release paper has been coated with a thin film of heated resin solution of relatively low viscosity, so that the resin thoroughly impregnates the fibres.
4. A **doctor blade** spreads the resin into a film of uniform thickness and width.
5. The final prepreg — a thin tape of continuous, aligned fibres in partially cured resin — is wound onto a cardboard core for packaging.

Typical tape thickness is **0.08–0.25 mm**; tape width is **25–1525 mm** (1–60 in.); resin content is **35–45 vol%**. Both thermoplastic and thermosetting resins are used, with carbon, glass and aramid fibres as the common reinforcements.

#### Filament winding

**Filament winding** positions continuous reinforcing fibres accurately in a predetermined pattern to form a hollow, usually cylindrical, shape.

1. The fibres, as individual strands or tows, are fed through a **resin bath**.
2. They are continuously wound onto a **mandrel**, usually with automated winding equipment.
3. After the appropriate number of layers, curing is carried out in an oven or at room temperature.
4. The mandrel is then removed.

Various winding patterns are possible — **circumferential, helical and polar** — to give the desired mechanical characteristics. Filament-wound parts have very high strength-to-weight ratios, a high degree of control over winding uniformity and orientation, and are most economically attractive when automated. Common structures include rocket motor casings, storage tanks and pipes, and pressure vessels.

| Process | Product shape | Key feature | Typical reinforcement |
| --- | --- | --- | --- |
| **Pultrusion** | Continuous constant cross-section (rods, tubes, beams) | Fibres pulled through impregnation, preforming and curing dies | Glass, carbon, aramid (40–70 vol%) |
| **Prepreg** | Thin tape or sheet for subsequent lay-up | Fibres preimpregnated with partially cured resin | Carbon, glass, aramid |
| **Filament winding** | Hollow cylinders, pressure vessels, rocket cases | Resin-wet tow wound on a mandrel in a controlled pattern | Continuous carbon, glass, aramid |

> [!note] Why prepreg is kept cold
> *Added depth beyond the slides.* Prepreg is only *partially* cured so that it remains drapeable and can be laid up into a laminate. The curing reaction is deliberately slowed by storage at low temperature; at room temperature the resin gradually advances and the prepreg loses its tack and formability. This is why prepreg has a shelf life and why lay-up shops store it in a freezer.

### 5.18 Structural composites

A **structural composite** is a multi-layered, normally low-density composite used in applications requiring structural integrity — ordinarily high tensile, compressive and torsional strengths and stiffnesses. Its properties depend not only on the constituent materials but also on the **geometrical design** of the structural elements. The two most common structural composites are **laminar composites** and **sandwich panels**.

#### Laminates

A **laminar composite** is composed of two-dimensional sheets or panels (**plies** or **laminae**) bonded to one another. Each ply has a preferred high-strength direction, as found in continuous and aligned fibre-reinforced polymers. A multi-layered structure of this kind is a **laminate**.

Laminate properties depend on how the high-strength direction varies from layer to layer. There are four classes:

| Class | Stacking pattern | Consequence |
| --- | --- | --- |
| **Unidirectional** | High-strength direction the same in every ply | Maximum axial stiffness and strength; highly anisotropic |
| **Cross-ply** | Alternating 0° and 90° layers | Stiffness in two perpendicular directions; more balanced |
| **Angle-ply** | Alternating $+\theta$ and $-\theta$ (e.g. $\pm45^\circ$) | Good shear/torsion resistance; tailored off-axis properties |
| **Multidirectional** | Several high-strength orientations | Most isotropic in-plane response of the four |

![[COMP - Classes of laminar composites.png|360]]
*Figure — the four classes of laminar composites: (a) unidirectional, (b) cross-ply, (c) angle-ply and (d) multidirectional. The arrows show the high-strength direction of each ply.*

For virtually all laminates the layers are stacked so that fibre orientations are **symmetric relative to the laminate midplane**; this arrangement prevents out-of-plane twisting or bending. In-plane properties of unidirectional laminates are highly anisotropic. Cross-, angle- and multidirectional laminates are designed to increase the degree of in-plane isotropy: multidirectional can be made most isotropic, and the degree of isotropy decreases through angle-ply and cross-ply.

Applications are primarily in aircraft, automotive, marine and building/civil-infrastructure sectors:

- **Aircraft** — fuselage, vertical and horizontal stabilizers, landing-gear hatch, floors, fairings, helicopter rotor blades.
- **Automotive** — automobile panels, sports-car bodies, drive shafts.
- **Marine** — ship hulls, hatch covers, deckhouses, bulkheads, propellers.
- **Building/civil** — bridge components, long-span roof structures, beams, structural panels, roof panels, tanks.
- **Sports and recreation** — the modern ski.

#### Sandwich panels

A **sandwich panel** is a lightweight beam or panel with relatively high stiffness and strength. It consists of two outer sheets (**faces** or **skins**) separated by, and adhesively bonded to, a thicker **core**.

- The **faces** are made of a relatively stiff and strong material — typically aluminium alloys, steel and stainless steel, fibre-reinforced plastics, or plywood. They carry the bending loads. When the panel bends, one face is in compression and the other in tension.
- The **core** is lightweight and normally has a low modulus of elasticity. It provides continuous support for the faces and holds them together. It must have sufficient **shear strength** to withstand transverse shear stresses and be thick enough to provide high **shear stiffness** (to resist buckling of the panel).
- Tensile and compressive stresses in the core are much lower than in the faces. Panel stiffness depends primarily on the **core material and core thickness**; bending stiffness increases significantly with increasing core thickness. Strong bonding between faces and core is essential.
- A sandwich panel is cost-effective because core materials are less expensive than face materials.
- Core materials typically fall into three categories: **rigid polymeric foams, wood, and honeycombs**.

![[COMP - Sandwich panel cross section.png|380]]
*Figure — cross-section of a sandwich panel: two stiff, strong faces separated by a thick, lightweight core. The faces carry bending stress; the core carries transverse shear and keeps the faces apart.*

![[COMP - Honeycomb core sandwich panel.png|460]]
*Figure — construction of a honeycomb-core sandwich panel: face sheets are adhesively bonded to a honeycomb core, giving high bending stiffness at low weight.*

> [!note] Why a sandwich panel is so stiff
> *Added depth beyond the slides.* Bending stiffness depends on how far the load-bearing material sits from the neutral axis. Separating two thin faces by a thick, light core moves the faces far from the neutral plane, so their contribution to the second moment of area rises approximately with the **square of the separation**. The core itself carries very little bending stress; its job is to keep the faces apart and to carry shear. This is the same principle as an I-beam, with the core acting as the web and the faces as the flanges.

### 5.19 Nanocomposites

**Nanocomposites** are composed of nanosized particles embedded in a matrix material. Their physical and chemical properties change dramatically as the particle size decreases, and the degree of change depends on the particle size (i.e. the number of atoms).

Two factors account for the size-induced properties:

1. The increase in the ratio of **particle surface area to volume**.
2. The **particle size** itself.

Surface atoms behave differently from atoms in the interior. As the particle size decreases, the relative ratio of surface atoms to bulk atoms increases, so **surface phenomena begin to dominate**. For extremely small particles, **quantum effects** begin to appear.

- Matrix materials may be metals or ceramics, but the most common matrices are **polymers**.
- The properties of a nanocomposite depend not only on the matrix and nanoparticle properties but also on **nanoparticle shape and content** and on **matrix–nanoparticle interfacial characteristics**.
- Most commercial nanocomposites use three general nanoparticle types: **nanocarbons, nanoclays and particulate nanocrystals**.

Nanoparticle loadings vary with the application:

- Carbon-nanotube concentrations on the order of **5 wt.%** can lead to significant increases in strength and stiffness.
- Between **15 and 20 wt.%** of carbon nanotubes are required to produce the electrical conductivity needed for some applications, such as protecting a structure from electrostatic discharge.

One of the main challenges in nanocomposite production is **processing**: for most applications the nanosize particles must be dispersed uniformly and homogeneously within the matrix.

| Application | Nanocomposite | Function |
| --- | --- | --- |
| Food/beverage packaging | Nanocomposite thin-film bags/containers | Barrier and mechanical improvement |
| Automobile tyres | Nanocomposite coatings | Increased air-pressure retention |
| Lithium-ion batteries | Graphene nanocomposite anodes | Charge storage |
| Flame barriers | Multi-walled carbon nanotubes in silicone | Flame retardancy |
| Dental restoration | Polymer nanocomposite filling materials | Wear and aesthetics |
| Wind-turbine blades / sports equipment | Multi-walled carbon nanotubes in epoxy | Stiffness and fatigue resistance |
| Automotive/aircraft fuel lines | Multi-walled carbon nanotubes in polymer | Electrostatic dissipation |

> [!note] Why a few per cent of nanotubes can matter
> *Added depth beyond the slides.* Nanotubes have an enormous aspect ratio, so they percolate — form a connected network — at a much lower volume fraction than spherical particles. The same network that raises stiffness can also conduct electricity, which is why the loading for mechanical reinforcement (about 5 wt.%) is lower than the loading for electrical conductivity (15–20 wt.%). The property you want determines the loading you need.

### 5.20 Composites in service — skis, aircraft and cars

The final slides are a reminder that the design equations in this block end up in objects people use.

#### The modern ski

A ski is a layered structural composite. The lecture's cut-away shows a **top sheet** (a polyamide polymer with a relatively low glass-transition temperature that resists chipping), a **torsion-box wrap** of fibre-reinforced composite using glass, aramid or carbon fibres in a variety of weaves and weights to tune the flexural characteristics, and a **core** of foam, vertical wood laminates, wood–foam laminates, honeycomb or other materials (commonly poplar and other woods). The ski is a laminate in which each layer is chosen for a different function — abrasion resistance on top, torsional stiffness in the wrap, low weight and damping in the core.

![[COMP - Composite construction of a modern ski.png|420]]
*Figure — cut-away of a modern composite ski: top sheet, fibre-reinforced torsion-box wrap and a lightweight core. Each layer is a different composite with a different job.*

#### The Boeing 787 Dreamliner

The 787 is the aircraft that made composites a mainstream airframe material:

- **Carbon laminates** in the wing and tail structures.
- **Continuous carbon-fibre–epoxy laminates** in the fuselage.
- **Glass-fibre-reinforced epoxy and hybrid composites** (glass + carbon fibres) in the tail and trailing wing structures.
- **Sandwich panels** in the nacelles (the housings around the engines) and trailing tail components; the faces are carbon-fibre–epoxy laminates and the cores are honeycomb structures of aluminium-alloy sheet.

![[COMP - Materials used in the Boeing 787.png|480]]
*Figure — materials used in the Boeing 787 body by weight: composites dominate at about 50%, compared with about 12% in the 777; aluminium falls from about 50% in the 777 to about 20% in the 787, with titanium, steel and other materials making up the balance.*

The comparison with the 777 is the point: the 787 uses roughly **50% composites by weight** against **12%** for the 777, while aluminium drops from about **50% to 20%**. That shift is what makes the weight saving — and the corresponding fuel efficiency — possible.

#### Automotive applications

The lecture closes with a map of composite parts in modern cars: CFRP engine covers, doors, cockpits, steering wheels/roofs, lift gates, bodies, wheels, fenders, seats, brake discs and transmission shafts, together with glass-fibre/polyamide bumper beams and polypropylene-honeycomb floor panels. The reasons are the same as in aerospace — mass reduction, stiffness, and the ability to mould a complex shape in one piece — but the cost constraint is much tighter, so automotive composites tend to use faster processes (SMC, RTM, short-fibre moulding) and cheaper fibres.

![[COMP - Composite parts in automobiles.png|480]]
*Figure — composite parts in modern automobiles, with the material identified for each part: CFRP for body, door, roof and transmission components; GF/PA6 for bumper beams; PP-honeycomb for floor panels.*

| Application | Composite | Why it is used |
| --- | --- | --- |
| Aircraft fuselage/wing | Carbon-fibre–epoxy laminate | High specific stiffness and strength; fatigue resistance |
| Engine nacelle | Carbon-face / Al-honeycomb sandwich | Stiff, light, damage-tolerant shell |
| Ski | Glass/aramid/carbon laminate + wood/foam core | Tunable flex, damping, low weight |
| Car body panel | CFRP or GFRP | Mass reduction and complex shape |
| Bumper beam | Glass-fibre/polyamide | Impact energy absorption at lower cost |
| Floor panel | PP–honeycomb | Bending stiffness with low mass |
| Cutting tool | Cemented carbide (WC–Co) | Hardness plus toughness at temperature |

> [!tip] Exam pointer — Composites
> Expect: the definition and objective of a composite; the matrix/dispersed-phase definitions; the five geometric variables; the classification tree and the difference between large-particle and dispersion-strengthened; the rule-of-mixtures upper and lower bounds and why experimental data lie between them; cermets, carbon-black rubber and concrete; the critical fibre length $l_c=\sigma_f^*d/2\tau_c$ and its derivation; the isostrain and isostress derivations, $E_{cl}$ and $E_{ct}$; longitudinal and transverse tensile strength; the discontinuous aligned formulae for $l>l_c$ and $l<l_c$; the random-fibre $K$ factor; whiskers/fibres/wires and the functions of the matrix; glass, carbon and aramid PMCs; MMC advantages and applications; CMC toughening and transformation toughening; pultrusion, prepreg and filament winding; laminate classes and sandwich panels; and the size effects in nanocomposites. The added depth to be ready with: the load-ratio $F_f/F_m$, the weight-to-volume fraction conversion, why $K<1$, why aramid is weak in compression, the step-by-step transformation-toughening sequence, and why sandwich stiffness scales with the square of the core separation.

---

## Formula Summary — Composites

| Quantity | Expression | Notes |
| --- | --- | --- |
| Specific strength | $\sigma/\rho$ | Selection index for weight-limited strength |
| Specific modulus | $E/\rho$ | Selection index for weight-limited stiffness |
| Volume fraction from weight fraction | $V_f=\dfrac{w_f/\rho_f}{w_f/\rho_f+w_m/\rho_m}$ | Two-phase composite; $V_m=1-V_f$ |
| Rule of mixtures — upper bound | $E_{c(u)}=E_mV_m+E_pV_p$ | Isostrain (Voigt); stiffest arrangement |
| Rule of mixtures — lower bound | $E_{c(l)}=\dfrac{E_mE_p}{V_mE_p+V_pE_m}$ | Isostress (Reuss); most compliant arrangement |
| Density of a composite | $\rho_c=\rho_mV_m+\rho_fV_f$ | Volume-fraction weighted |
| Critical fibre length | $l_c=\dfrac{\sigma_f^*d}{2\tau_c}$ | $\tau_c$ = smaller of bond strength and matrix shear yield strength |
| Longitudinal modulus | $E_{cl}=E_mV_m+E_fV_f=E_m(1-V_f)+E_fV_f$ | Continuous aligned fibres; isostrain |
| Transverse modulus | $E_{ct}=\dfrac{E_mE_f}{V_mE_f+V_fE_m}$ | Continuous aligned fibres; isostress |
| Fibre-to-matrix load ratio | $\dfrac{F_f}{F_m}=\dfrac{E_fV_f}{E_mV_m}$ | Longitudinal loading |
| Longitudinal tensile strength | $\sigma_{cl}^*=\sigma_m'(1-V_f)+\sigma_f^*V_f$ | $\sigma_m'$ = matrix stress at fibre failure strain |
| Discontinuous aligned strength, $l>l_c$ | $\sigma_{cd}^*=\sigma_f^*V_f\left(1-\dfrac{l_c}{2l}\right)+\sigma_m'(1-V_f)$ | End-effect correction |
| Discontinuous aligned strength, $l<l_c$ | $\sigma_{cd}^*=\dfrac{\tau_cl}{d}V_f+\sigma_m'(1-V_f)$ | Fibre pulls out rather than fracturing |
| Random-fibre modulus | $E_{cd}=KE_fV_f+E_mV_m$ | $K=0.1$–$0.6$; fibre efficiency parameter |
| Reinforcement efficiency | Parallel 1; perpendicular 0; random in plane $3/8$; random in 3D $1/5$ | Geometric multiplier on fibre contribution |

> [!note] Source images
> All Excalidraw figures in this block are original reconstructions of the classification tree and the isostrain/isostress loading states; the vault copies live in the `Excalidraw/` folder with the `COMP - ` prefix. The photographs, property charts, schematics and application figures embedded above are the original figures extracted from [[Composites_Odd_2026-27.pdf]] and stored in `Material Science/images/` with the `COMP - ` prefix.

---

# Electrical & Electronic Properties

The electrical response of a solid spans a wider range than any other property in this course — twenty-five orders of magnitude in resistivity, from a superconductor below $10^{-20}\ \Omega\,\text{m}$ to polyethylene beyond $10^{17}\ \Omega\,\text{m}$. Two models carry the whole block. The **free electron gas** explains why a metal conducts at all, and how impurities, other electrons and lattice vibrations limit it. The **band model** then explains why a solid built from the same outermost electrons can instead be a semiconductor or an insulator. The same band picture reappears at the end of the course, where it decides whether a material is transparent, coloured or opaque.

Compiled from the lecture slides ([[Electrical and Electronic Properties - Part 1_Odd_2026-27.pdf]], [[Electrical and Electronic Properties - Part 2_Odd_2026-27.pdf]]) and the handwritten class notes in [[MO NOTES (1).pdf]]. Slides follow **Raghavan, *Materials Science and Engineering*** and **Callister, *Fundamentals of Materials Science and Engineering***.

> [!info] How the two parts fit together
> **Part 1** builds the free electron gas from the de Broglie relation upwards: the parabolic $E$–$k$ curve (§6.3), its quantization into states up to the Fermi level (§6.4), the Fermi–Dirac occupation of those states (§6.5), and conduction as a field-induced bias of the velocity distribution (§6.6). It then breaks the model twice: once to describe the two kinds of superconductor (§6.7–§6.10), and once to derive the **energy gap** from Bragg reflection and standing waves (§6.11–§6.12). **Part 2** starts from that gap, classifies solids by their band structure (§7.1–§7.6), then works through intrinsic and extrinsic conduction (§7.7–§7.11), doping practice (§7.12) and the p-n junction (§7.13–§7.14).

---

## 6. Electrical and Electronic Properties — Part 1

### 6.1 The resistivity range: twenty-five orders of magnitude

The electrons in the outermost orbitals of the atoms of a solid determine its electrical properties. What makes the topic remarkable is not that statement but its consequence: because those electrons can be bound, shared, donated or completely free, the electrical resistivity $\rho$ (or its reciprocal, the conductivity $\sigma$) varies over **25 orders of magnitude** across materials that are otherwise ordinary solids.

| Class | Resistivity $\rho$ ($\Omega\,\text{m}$) | Conductivity $\sigma$ ($\Omega^{-1}\text{m}^{-1}$) | Examples |
| --- | --- | --- | --- |
| **Conductors** (metals and alloys) | $10^{-9}$–$10^{-3}$ | $10^{9}$–$10^{3}$ | Au, Ag, Cu (the best three), then Al |
| **Semiconductors** | $10^{-3}$–$10^{3}$ | $10^{3}$–$10^{-3}$ | Si, Ge, doped Ge |
| **Insulators** | $10^{4}$ to beyond $10^{17}$ | below $10^{-4}$ | Polyethylene, bakelite, lucite, mica, PVC, rubber, porcelain |

![[EP1 - Resistivity ranges of materials.png|460]]

*Figure — the resistivity spectrum: the same plot that spans conductors, semiconductors and insulators is the reason the free electron model has to be repaired rather than replaced.*

The semiconductor row is the one that behaves unlike a metal. A metal's resistivity is fixed by composition and microstructure; a semiconductor's resistivity is a **strong function of small concentrations of impurities**. Doped Ge with an impurity content of only a few tens per million can have a resistivity about two orders of magnitude lower than that of pure Ge. That sensitivity is the whole basis of solid-state electronics, and it is why §7.9–§7.12 are about doping rather than about the host crystal.

> [!warning] Resistivity is a range, not a fingerprint
> Do not quote a single resistivity for a semiconductor. The same crystal can be $10^{3}\ \Omega\,\text{m}$ undoped and two orders of magnitude lower when doped at the tens-of-ppm level; the number is meaningless without the doping level and the temperature.

### 6.2 The free electron model

The conducting properties of a solid are **not** a function of the total number of electrons in the solid, because only the outermost electrons of the atoms can take part in conduction. In the free electron model those outermost electrons are not bound to any particular atom but are free to move through the whole solid. They have been variously called the **free electron cloud**, the **free electron gas** or the **Fermi gas**.

The basic assumption of the theory is that the potential field due to the ion cores is **uniform** throughout the solid — the free electrons have the same potential energy everywhere in the solid. That potential energy is a finite, negative value, because of the electrostatic attraction between a free electron and the ion cores. Since only energy *differences* matter, the constant can be set to zero, and the only energy left to consider is the kinetic energy.

$$ E_{\text{kin}} = \tfrac12 mv^2 $$

That kinetic energy is **substantially lower** than the kinetic energy of a bound electron in an isolated atom. The reason is geometric: the field of motion for the free electron is considerably enlarged in the solid compared with the field around an isolated atom, and a larger box means longer permitted wavelengths and hence lower kinetic energies (§6.3).

> [!important] Definitions
> **Free electron model** — the outermost electrons of the atoms of a solid are treated as unbound particles moving in a constant (zero) potential, subject only to the Pauli exclusion principle.
> **Free electron gas / Fermi gas** — the collection of these electrons, named by analogy with a gas of classical particles.
> **Fermi energy $E_F$** — the energy of the highest filled level at $0\ \text{K}$ (§6.4).

### 6.3 The electron as a wave: de Broglie, wave number and the $E$–$k$ parabola

Electrons have both particle-like and wave-like characteristics. The de Broglie wavelength $\lambda$ of an electron is related to its momentum $mv$ by

$$ \lambda = \frac{h}{mv} \tag{1} $$

where $h$ is Planck's constant, $m$ the mass of the free electron and $v$ its velocity. The wavelength is inversely related to the magnitude of the wave number vector $k$:

$$ k = \frac{2\pi}{\lambda} \tag{2} $$

As the velocity of free electrons is much smaller than that of light, relativistic effects can be ignored and the classical kinetic energy used:

$$ E = \tfrac12 mv^2 \tag{3} $$

Substituting the first two relations into the third gives the free electron dispersion relation

$$ \boxed{\ E = \frac{h^2k^2}{2m}\ } \tag{4} $$

The kinetic energy therefore increases as the **square** of the wave number — a parabolic relation. Since $\lambda$ is inversely related to $k$, the electron with the largest de Broglie wavelength has the lowest kinetic energy, and with the enlarged field of motion in the solid, the electrons can have larger wavelengths and hence lower kinetic energies than in an isolated atom.

![[EP1 - Parabolic E-k free electron.png|380]]

*Figure — the parabolic $E$–$k$ relation of a free electron: energy rises as the square of the wave number, so long waves (small $k$) sit at the bottom of the curve.*

#### Why the parabola is the whole free electron model

The entire content of the free electron gas is in that one curve: the density of available states, the Fermi energy, the response to a field and the heat capacity all follow from the fact that $E \propto k^2$ and that states are filled from the bottom up. The model's failure later in the topic is equally visible on it — the parabola is *smooth everywhere*, and the next thing the slides do is show that a periodic lattice puts a **break** in it at particular values of $k$ (§6.12).

### 6.4 Quantization: states in a box and the Fermi energy

Although the variation of $E$ with $k$ in the figure is drawn as continuous, the levels are in fact very closely spaced **discrete** levels, because the quantum restrictions arising from the Pauli exclusion principle apply to the free electrons as well.

Consider a solid in which electron motion is unidirectional, along an axis of length $L$. The longest wavelength permissible for the free electron is twice this length, because the amplitude of the wave must be zero at both ends. The next smaller permissible wavelength is $L$, the third is $\tfrac23 L$, and so on. The corresponding wave numbers are $\pi/L$, $2\pi/L$, … from Eq. (2).

In an electrically neutral solid, a free electron having a certain speed in one direction is always associated with another electron having the same speed but moving in the opposite direction; that is, $k$ takes both positive and negative values. For the first two states $k = \pm\pi/L$ and $\pm 2\pi/L$, and in general

$$ k = \pm\frac{n\pi}{L} $$

where the quantum number $n$ takes successively increasing integer values. Substituting into Eq. (4):

$$ E = \frac{n^2h^2}{8mL^2} \tag{5} $$

For three-dimensional motion, with box dimensions $L_x$, $L_y$, $L_z$ and quantum numbers $n_x$, $n_y$, $n_z$:

$$ \boxed{\ E = \frac{h^2}{8m}\left(\frac{n_x^2}{L_x^2} + \frac{n_y^2}{L_y^2} + \frac{n_z^2}{L_z^2}\right)\ } \tag{6} $$

Each distinct combination of $n_x$, $n_y$, $n_z$ corresponds to a **quantum state**, in which two electrons of opposite spin can reside. Several combinations can give the same value of $E$; quantum states with the same energy are said to be **degenerate**. The successive levels are so close that $E$ can be treated as continuous, and the levels fill from the bottom.

![[EP1 - de Broglie wavelengths along x.png|440]]

*Figure — the first few permissible de Broglie wavelengths for unidirectional motion: the fundamental $\lambda = 2L$ has nodes at both ends of the solid, and each higher state fits one more half-wavelength.*

The waveforms of Fig. 2 raise a difficulty. The probability of finding an electron at any point is proportional to the square of the amplitude of the wave at that point, so for the state $\lambda = 2L$ the probability would be a maximum at the midpoint and would *not* be uniform — an unacceptable result, since the probability of finding a free electron must be the same anywhere in the solid. The difficulty is removed by treating the waves as **travelling waves with constant velocity**, so that the time-averaged probability is constant throughout the solid.

In keeping with the minimum-energy criterion and the Pauli exclusion principle, the free electrons occupy successive quantum states of increasing kinetic energy. The energy corresponding to the highest filled level at $0\ \text{K}$ is the **Fermi energy $E_F$**: at $0\ \text{K}$ the electrons occupy all levels up to the Fermi level and leave all those above it empty. At $T > 0\ \text{K}$, thermal excitation gives a finite probability that some electrons from below $E_F$ move to levels above it.

> [!important] Definitions
> **Fermi energy $E_F$** — the energy of the highest occupied level at absolute zero.
> **Fermi level** — that level which has a **50 % probability of occupation by an electron at any temperature**.
> **Degenerate states** — distinct quantum states having the same energy.

### 6.5 Fermi–Dirac statistics

The probability of occupation $P(E)$ of an energy level $E$ by an electron is given by the **Fermi–Dirac distribution**, which takes into account the quantum restrictions due to the Pauli exclusion principle:

$$ \boxed{\ P(E) = \frac{1}{1 + \exp\!\left(\dfrac{E - E_F}{kT}\right)}\ } $$

where $k$ is Boltzmann's constant and $T$ the absolute temperature.

At $0\ \text{K}$, $P(E)$ is constant at unity up to $E_F$, where it falls abruptly to zero. At $T_1 > 0\ \text{K}$, some electrons just below $E_F$ are thermally excited to levels just above $E_F$; at a still higher temperature, more electrons leave the lower levels and occupy higher ones. The cross-over point, where $P(E) = 0.5$, occurs at *the same* value of energy for every temperature — and that energy is $E_F$.

![[EP1 - Fermi-Dirac distribution at three temperatures.png|440]]

*Figure — the Fermi–Dirac distribution at three temperatures: the step at $0\ \text{K}$ broadens with temperature but every curve pivots about $P = 0.5$ at $E = E_F$.*

> [!note] Why the Fermi level is the 50 % level
> The distribution is symmetric about $E = E_F$: an electron promoted from a level $E_F - \delta$ to a level $E_F + \delta$ leaves one empty state below and fills one above, so the two levels must have equal and opposite occupation probabilities. That is exactly $P(E_F - \delta) + P(E_F + \delta) = 1$, which at $\delta = 0$ forces $P(E_F) = \tfrac12$.

### 6.6 Conduction by free electrons: drift velocity and conductivity

In an electrically neutral solid, for every electron moving with a certain speed in a given direction there is another moving with the same speed in the opposite direction. This equal and opposite velocity distribution can be **biased** by an externally applied electric field to yield a net velocity in one direction — and with that biasing, the solid conducts electricity. Under an applied field the $E$–$k$ relationship of §6.3 is modified into the distribution shown below: electrons moving towards the positive end of the field acquire extra velocity, while those moving in the opposite direction lose some.

![[EP1 - Electron redistribution under field.png|360]]

*Figure — the field-induced shift of the occupied states: the whole Fermi sphere is displaced in $k$-space, so the electron gas acquires a net drift velocity.*

Such redistribution is possible **only when empty electron states are available immediately above $E_F$**. That availability is the basic characteristic of conductors, as opposed to semiconductors and insulators — it is the single structural difference that §7.3 will formalise.

The electrons accelerated towards the positive end do not continue to increase their velocity indefinitely. They collide with obstacles on the way, and depending on the time interval between two successive collisions they acquire an average increment of velocity called the **drift velocity**, all of which they lose during a collision.

![[EP1 - Extra velocity lost on collision.png|440]]

*Figure — the drift velocity: each electron accelerates between collisions and loses the whole increment at the next one, so the steady state is a sawtooth in velocity.*

With $n$ the number of free electrons per unit volume, $e$ the electronic charge, $\tau$ the average collision time and $m$ the electron mass, the conductivity is

$$ \boxed{\ \sigma = \frac{ne^2\tau}{m}\ } $$

> [!important] Definitions
> **Drift velocity** — the average extra velocity an electron acquires between two collisions under an applied field; it is lost at each collision.
> **Mean free path $l$** — the mean distance an electron travels between successive collisions.
> **Collision time $\tau$** — the mean time between successive collisions; $\tau = l/v$.

#### The mean free path and the scattering hierarchy

For an ideal crystal with no impurities and no imperfections, the mean free path at $0\ \text{K}$ is **infinite** — there are no collisions and the electrical conductivity is ideally infinite. Every real crystal falls short of that limit, and the slides rank the culprits:

| Scattering centre | Effect on $l$ | Effect on $\sigma$ | Note |
| --- | --- | --- | --- |
| **Solute atoms** (dissolved in the lattice) | Decrease | Decrease | The *most effective* of all the centres listed |
| Other point imperfections (vacancies, interstitials) | Decrease | Decrease | — |
| Dislocations | Decrease | Decrease | — |
| Grain boundaries | Decrease | Decrease | Inversely proportional to grain size |

Solute atoms provide effective scattering centres because their introduction into the crystal results in collisions, decreasing the mean free path and the conductivity; among all these centres, impurities dissolved in the crystal lattice as solutes are **more effective than the others**. This is the physical basis of the alloying rule that pure annealed copper conducts better than brass, and it is the same hierarchy that later explains why a superconducting wire is deliberately made *dirty* in a controlled way (§6.10), where the same defects become useful.

### 6.7 Superconductors: the abrupt disappearance of resistance

The resistivity of pure Ag decreases gradually to a low but measurable value of about $10^{-11}\ \Omega\,\text{m}$ at $0\ \text{K}$: silver is a very good conductor but **not** a superconductor. The resistivity of Sn, by contrast, falls *abruptly* at about $4\ \text{K}$ to a value below the measurable limit of $10^{-20}\ \Omega\,\text{m}$. The temperature at which this abrupt fall occurs is the **superconducting transition temperature $T_c$**.

![[EP1 - Resistivity of silver and tin near 0 K.png|470]]

*Figure — resistivity near $0\ \text{K}$: silver approaches a residual value, tin drops discontinuously to immeasurably small resistance at $T_c$.*

> [!important] Definition
> **Superconductor** — a material whose electrical resistivity falls abruptly to below the measurable limit ($\sim10^{-20}\ \Omega\,\text{m}$) at a critical temperature $T_c$, and which expels magnetic flux from its interior.

The first application conceived for the effect was to produce a large permanent magnetic field by inducing a **perpetual current** in a superconductor. That idea runs into a limit: at temperatures below $T_c$, as the magnetic field strength reaches a critical value $H_c$, superconductivity disappears. At $T = T_c$, $H_c = 0$; $H_c$ increases as the temperature decreases below $T_c$. The critical current density $J_c$ increases in the same way. In other words, the maximum current a superconductor carries at a given temperature below $T_c$ is limited by the magnetic field that current produces at the surface of the superconductor.

![[EP1 - Critical field versus temperature.png|420]]

*Figure — the critical field as a function of temperature: the superconducting state survives only below the curve, and the curve closes at $H_c = 0$ for $T = T_c$.*

### 6.8 The Meissner effect

In the superconducting state the flux lines of a magnetic field are **ejected** from the superconductor. This is the **Meissner effect**, and it makes the superconductor a **perfect diamagnet**, with magnetic susceptibility $\chi = -1$ — the value already quoted in §8.2 for the ideal diamagnetic limit.

![[EP1 - Meissner effect flux expulsion.png|440]]

*Figure — the Meissner effect: on crossing into the superconducting state the flux lines are pushed out of the solid rather than merely excluded from a surface layer.*

> [!note] Why $\chi = -1$ is not merely "very diamagnetic"
> From $B = \mu_0(H + M)$ (§8.1), a susceptibility of exactly $-1$ means $M = -H$, hence $B = 0$ *everywhere inside*. A normal diamagnet only reduces $B$; a superconductor annihilates it. This is why the Meissner effect is a thermodynamic state property and not a consequence of zero resistance: a hypothetical perfect conductor would trap whatever flux it had at the transition.

### 6.9 Type I and Type II superconductors

**Type I** (the ideal superconductor), placed in a magnetic field, repels the flux lines totally until the field attains the critical value $H_c$; the magnetization is $M = -H$ up to $H_c$, where it drops to zero. **Type II** (hard) superconductors show the ideal behaviour only up to a *lower* critical field $H_{c1}$; beyond it the magnetization changes gradually and attains zero at an *upper* critical field $H_{c2}$. The Meissner effect is incomplete between $H_{c1}$ and $H_{c2}$ — that region is the **vortex region**.

![[EP1 - Magnetization of type I and type II superconductors.png|470]]

*Figure — magnetization against applied field for (a) type I and (b) type II: the type I curve is a single vertical drop at $H_c$, the type II curve has a gradual tail between $H_{c1}$ and $H_{c2}$.*

| Feature                  | Type I (ideal)                  | Type II (hard)                                           |
| ------------------------ | ------------------------------- | -------------------------------------------------------- |
| Flux expulsion           | Complete up to $H_c$            | Complete only up to $H_{c1}$                             |
| Magnetization            | $M = -H$ up to $H_c$, then zero | Gradual fall from $H_{c1}$ to zero at $H_{c2}$           |
| Meissner effect          | Complete                        | Incomplete between $H_{c1}$ and $H_{c2}$ (vortex region) |
| Critical current density | Low                             | High — hence of practical importance                     |
|                          |                                 |                                                          |

Type II superconductors can carry high current densities and are therefore the ones of practical importance. Their current-carrying capacity is limited by how well the flux lines in the vortex region can be **pinned**, and the slides give the microstructural recipe for pinning:

- **Heavily cold-worked and recovery-annealed material** has cell walls of high dislocation density; this microstructure effectively pins the magnetic flux lines and makes their penetration difficult.
- **Grain boundaries** also exert a pinning action; an extremely fine grain size is effective in increasing $H_{c2}$.
- **Very fine precipitates** dispersed in the matrix, with an interparticle spacing of about $300\ \text{\AA}$, give optimum flux pinning.

The critical current density $J_c$ also increases as $H_{c2}$ increases.

> [!warning] The slide's "up to $T_c$" is a typo
> The type I magnetization is $M = -H$ up to $H_c$ (the critical *field*), not up to $T_c$. The transition at $T_c$ happens in zero applied field, where $H_c = 0$; the whole $M$–$H$ curve of the figure exists *below* $T_c$ and is traversed by changing the field.

### 6.10 Why the free electron model must fail

Everything so far has assumed that the potential in which the electrons move inside the crystal is **constant**. In reality this is a gross approximation. The potential energy of an electron is undoubtedly a function of its position with respect to the ion cores and the other electrons: it will be **less** when the electron is close to a (positive) ion core, and **more than the average** when it is farthest away from neighbouring ion cores.

This fact, combined with the **diffracting properties of electrons**, has an important effect on the electron energy calculations — especially at certain critical values of the de Broglie wavelength of the electrons. The failure is therefore not a small correction: it is a *periodicity* effect that appears only at particular wavelengths, and it is the origin of the energy gap that makes semiconductors and insulators possible.

### 6.11 The energy gap: Bragg reflection and standing waves

Consider motion of electrons along one axis, as before. Electrons moving to the right or to the left are scattered by the atoms in their path. This scattering is largely **coherent** and is reinforced in the direction of motion of the electrons. If, however, the spacing $d$ between neighbouring atoms along the axis is such that the **Bragg equation** is exactly satisfied, the electrons are **totally reflected**.

For unidirectional motion the atoms along the axis can be visualised as successive "planes" perpendicular to the direction of electron motion, so that $\sin\theta = 1$. The Bragg equation then gives critical wavelengths

$$ \lambda = 2d,\ d,\ \tfrac{2d}{3},\ \dots $$

for successively increasing order of reflection $n$. Expressed as wave numbers, the critical conditions are

$$ k = \pm\frac{\pi}{d},\ \pm\frac{2\pi}{d},\ \pm\frac{3\pi}{d},\ \dots $$

At these values the electrons are reflected back and forth repeatedly, so that the **net velocity of the electrons in the given direction is zero**.

The waveform of the electrons under such critical conditions comes out as **two standing waves** rather than the travelling wave used for the free electron. The travelling wave gives a constant, time-averaged density of electrons throughout the solid; the standing wave gives a **periodic variation** in amplitude and in electron probability density. The two possible combinations — the sum and the difference of the travelling waves — are respectively a **cosine wave** and a **sine wave**, each with maximum amplitude at fixed points in space.

![[EP1 - Standing waves at Bragg condition.png|470]]

*Figure — at the Bragg condition the electron is described by two standing waves; their probability densities $\rho$ peak either on the ion cores or between them, and the potential-energy variation along the row is sketched underneath.*

Since the probability of finding an electron at a point is proportional to the square of the amplitude, the electron is most likely to be found at the crest of the probability-density curve — it is **localised**, in contrast to the free electron, which can be found anywhere in the crystal.

Once the electrons are localised, the potential-energy variation due to location must be included:

- When there is **no** critical condition and the electrons are not reflected, they have the average potential energy, taken as zero.
- At a critical condition the electron is a standing wave and is localised. As a **cosine** wave it sits close to an ion core and has a potential energy **lower** than the average. As a **sine** wave it sits farthest from the ion cores and has a potential energy **higher** than the average.

These deviations from the average potential energy appear as a **break in the $E$–$k$ curve**. The break at a critical value of $k$ gives rise to an **energy gap**: two groups of very closely spaced levels — **energy bands** — separated by a gap at the critical value of $k$. The magnitude of the gap is the difference in potential energy of the two electron locations.

![[EP1 - E-k break at critical wave number.png|380]]

*Figure — the $E$–$k$ curve broken at the critical wave number: the two branches that meet there are separated by the gap whose width is the potential-energy difference between the cosine and sine standing waves.*

$$ \boxed{\ \Delta E_{\text{gap}} = E_{\text{sine}} - E_{\text{cosine}}\ } $$

#### The derivation in one line

The gap is not imposed on the model; it is the *difference between two expectation values of the same periodic potential*, evaluated for the two standing waves that the Bragg condition forces. The cosine wave piles probability density on the cores (favourable, lower energy), the sine wave piles it in the interstitial regions (unfavourable, higher energy), and the splitting between the two is the forbidden band. This is why the gap opens exactly at $k = \pm n\pi/d$ and nowhere else, and why its size measures how strongly the potential varies with position — the point that §7.5 uses to explain the diamond → Si → Ge → Sn → Pb trend.

### 6.12 The forbidden gap in three dimensions

In a 3-D crystal the electrons can move in any direction, not necessarily normal to the reflecting planes, so the Bragg angle $\theta$ can take any value from $0$ to $90^\circ$. The critical values of $k$ then correspond to

$$ k = \pm\frac{n\pi}{d\sin\theta} $$

rather than the $\pm n\pi/d$ used for the 1-D case. Depending on the value of $\theta$, reflection occurs at different values of $k$, even for the same set of reflecting planes: the $E$–$k$ curves for motion along $[100]$ and $[110]$ are different, and for first-order reflection from $(100)$ planes the gap occurs at $k = \pi/d$ for $[100]$ motion and at $k = \sqrt{2}\pi/d$ for $[110]$ motion.

The **effective gap** is the interval between the *bottom* line of the gap in the $[110]$ direction and the *top* line of the gap in the $[100]$ direction. This effective gap is the **forbidden gap**, because electrons cannot take those values of energy that lie in it, whatever their direction of motion.

![[EP1 - Forbidden gap and Brillouin zones.png|470]]

*Figure — the effective forbidden gap: the two directional $E$–$k$ curves have their breaks at different $k$, and the overlap of the two gap intervals defines the range of energies no electron can occupy in any direction.*

> [!note] Why a "forbidden" gap needs all directions
> A single direction only forbids a *line* of energies at one $k$. A solid is isotropic in the sense that electrons move in all directions at once, so an energy is truly forbidden only if it falls inside the gap for *every* direction. That is why the three-dimensional argument is an *overlap* argument, and why the gap can close altogether when the directional intervals stop overlapping (§7.1).

> [!tip] Exam pointer — Part 1
> Expect: the resistivity ranges and the definition of the three classes; the free electron assumptions (constant potential, only KE, enlarged box lowers $E$); Eqs. (1)–(4) and the parabolic $E$–$k$; the box quantisation with $\lambda = 2L$ and $E = n^2h^2/8mL^2$, extended to Eq. (6) in 3-D; degeneracy and the two-spins-per-state rule; the Fermi–Dirac form and the 50 % definition of $E_F$; conduction as a biased velocity distribution requiring empty states just above $E_F$; $\sigma = ne^2\tau/m$ and the mean free path, with solutes the most effective scatterers; the $T_c$, $H_c$ and $J_c$ definitions and their interrelation; the Meissner effect and $\chi = -1$; type I versus type II with $H_{c1}$, $H_{c2}$ and the vortex region; the pinning recipe (cold work cell walls, fine grains, $\sim300\ \text{\AA}$ precipitate spacing); the Bragg condition at $\sin\theta = 1$ giving $k = \pm n\pi/d$; the two standing waves, their localisation and the potential-energy difference that *is* the gap; and $k = \pm n\pi/(d\sin\theta)$ with the effective forbidden gap. The added depth to be ready with: why the 50 % level is $E_F$ by symmetry, and why the forbidden gap requires an overlap over all directions.

---

## 7. Electrical and Electronic Properties — Part 2

### 7.1 Overlapping bands and the disappearance of the gap

The forbidden gap **disappears** if the bottom line of the gap for the $[110]$ direction lies *above* the top line of the gap in the $[100]$ direction. Such a situation arises when the potential energy of an electron is **not a strong function of location** in the crystal. The energy bands on either side of a critical value of $k$ are then said to **overlap**, and there is no forbidden energy at all.

This is the single criterion that decides whether a solid is a metal: not the number of valence electrons, but whether the periodic potential is strong enough to open a gap that survives in all directions.

### 7.2 Brillouin zones

The $E$–$k$ plot used so far is for unidirectional motion of the electrons. When all directions of electron motion and all possible reflections are considered together, the ranges of $k$ that lie between the forbidden gaps are called **Brillouin zones**. The first Brillouin zone contains all the energy levels up to the first $E$–$k$ discontinuity; the second zone contains all levels between the first and second discontinuities, and so on.

For example, the first zone for an FCC crystal is a polyhedron bounded by planar surfaces of the $\{111\}$ and $\{200\}$ types, these two corresponding to the first and the second allowed reflections for the FCC lattice.

> [!important] Definition
> **Brillouin zone** — a range of wave numbers (and hence of energies) lying between two successive $E$–$k$ discontinuities, for electron motion in all directions and all possible reflections.

### 7.3 The valence band, the conduction band, and the classification of solids

The outermost energy band that is full or partially filled is the **valence band**. The band above the valence band, empty at $0\ \text{K}$, is the **conduction band**. Solids are classified on the basis of their band structure as metals, semiconductors and insulators.

> [!important] Definitions
> **Valence band** — the outermost band that is full or partially filled at $0\ \text{K}$.
> **Conduction band** — the band above the valence band, empty at $0\ \text{K}$.
> **Band gap $E_g$** — the forbidden energy interval separating them.

### 7.4 Metals: two ways to be a conductor

Metals are those solids that have **vacant electron energy states immediately above the highest filled level of the valence band**. This can happen in two ways: either the valence band is only **half-filled**, or a **full valence band overlaps the conduction band** so that there is no forbidden gap.

![[EP2 - Metals partially filled and overlapping bands.png|460]]

*Figure — the two metallic band structures: a partially filled band (left) and a full valence band overlapping an empty conduction band (right); both leave empty states immediately above the occupied levels.*

The periodic table follows the rule closely:

| Element group | Outermost electrons | Band situation | Consequence |
| --- | --- | --- | --- |
| **Monovalent** — Cu, Ag, Au | One | Outermost band only **half full** | Conduct |
| **Divalent** — Mg, Be | Two (even) | Valence band full but **overlaps** the conduction band | Conduct |
| **Trivalent** — Al | Three | Outermost band **half full** | Conducts, band structure similar to the monovalent metals |
| **Fourth column** — C, Si, Ge, Sn, Pb | Four (even) | Valence band full, **no overlap** | Do *not* conduct as metals — the band gap decides (§7.5) |

### 7.5 The fourth column: from diamond to lead

In elements of the fourth column the electrons in the outermost orbital are even in number, as in the divalent metals: the valence band is full, but here there is **no overlap** of the valence band with the conduction band. Whether the solid is an insulator or a semiconductor is then fixed by the *size* of the resulting gap.

Taking covalent diamond, the potential energy of the electrons is a strong function of their location in the crystal; correspondingly a forbidden gap exists, and it is relatively large — $5.4\ \text{eV}$.

As we move down the fourth column to the elements below diamond, the electrons of the outermost orbital are farther away from the nucleus. The effect of this increasing separation is **dominant over** the effect of the increasing charge on the nucleus, so the electrons are less tightly bound to the nucleus as we go down the column. The potential energy of the electron is no longer a strong function of its location, and this reduces the gap:

| Element | $E_g$ (eV) | Character |
| --- | --- | --- |
| **Diamond (C)** | 5.4 | Insulator |
| **Si** | 1.1 | Semiconductor |
| **Ge** | 0.7 | Semiconductor |
| **Gray Sn** | 0.08 | Semiconductor, nearly metallic |
| **Pb** | 0 | Metal — the forbidden gap has closed |

> [!note] Why the trend is monotonic down a column
> Two competing effects act on the outermost electron: it moves farther from the nucleus (which *weakens* binding) and the nuclear charge rises (which *strengthens* binding). The slides state explicitly that the separation effect dominates, so binding weakens downwards, the potential becomes flatter, and the gap shrinks from 5.4 eV to zero. The same logic explains why the gap of a *compound* semiconductor can be tuned by changing the average atomic size rather than the electron count.

### 7.6 The semiconductor–insulator divide

Those materials with an energy gap of about $2$–$3\ \text{eV}$ or less are called **semiconductors**, and those with a gap of more than $3\ \text{eV}$ are **insulators**. In contrast to metals, both have a finite forbidden gap; the only difference between them is the **magnitude** of that gap.

![[EP2 - Insulator versus semiconductor energy gap.png|450]]

*Figure — the only difference between an insulator and a semiconductor: the same band diagram with a wide gap ($>3\ \text{eV}$) and a narrow one ($\lesssim3\ \text{eV}$).*

> [!warning] The dividing line is a convention, not a physical boundary
> The $3\ \text{eV}$ cut is a rule of thumb. Diamond ($5.4\ \text{eV}$) and Si ($1.1\ \text{eV}$) behave very differently at room temperature only because the *fraction* of electrons thermally excited across the gap is exponential in $E_g/kT$ — not because the two materials differ in kind. A "semiconductor" at $4\ \text{K}$ is an insulator.

![[EP - Band structure classification.excalidraw]]

The decision sequence of §7.3–§7.6 in one figure: half-filled band → metal; full band → test for overlap; no overlap → the gap across all directions decides semiconductor or insulator, with the column-IV sequence providing the calibration from $5.4\ \text{eV}$ down to zero.

### 7.7 Intrinsic semiconductors: carrier statistics

In **intrinsic** semiconductors the conduction is due to the intrinsic processes characteristic of the crystal in question, without the influence of impurities. A pure Si or Ge crystal is an intrinsic semiconductor: the electrons excited from the top of the valence band to the bottom of the conduction band by thermal energy are responsible for conduction.

The number of electrons excited across the gap is calculated from the Fermi–Dirac probability distribution. For an intrinsic semiconductor the Fermi level lies in the **middle of the energy gap**, so that $E - E_F = E_g/2$. For Si this is $0.55\ \text{eV}$, which is more than twenty times larger than the thermal energy $kT$ at room temperature ($0.026\ \text{eV}$).

![[EP2 - Fermi level midgap in intrinsic semiconductor.png|380]]

*Figure — the Fermi level of an intrinsic semiconductor sits midgap, so that the energy measured from $E_F$ to either band edge is exactly $E_g/2$.*

Because $E - E_F \gg kT$, the factor of unity in the denominator of the Fermi–Dirac expression can be ignored in comparison with the exponential term, and the occupation probability becomes

$$ P(E) \approx \exp\!\left(-\frac{E - E_F}{kT}\right) $$

The fraction of electrons at energy $E$ equals this probability, so the number $n$ of electrons promoted across the gap is

$$ \boxed{\ n = N\exp\!\left(-\frac{E_g}{2kT}\right)\ } $$

where $N$ is the number of electrons available for excitation from the top of the valence band.

> [!warning] The Boltzmann approximation is the whole point
> Dropping the "1" is not a mathematical convenience — it is the statement that the electron gas is **non-degenerate**, i.e. the states above $E_F$ are almost empty. The approximation is valid precisely because $E_g/2 \gg kT$; it would fail for a zero-gap or heavily doped semiconductor, and it is why the intrinsic carrier concentration is so violently temperature-dependent.

The promotion of some electrons across the gap leaves vacant electron sites in the valence band — **holes**. As each excited electron leaves back one hole, an intrinsic semiconductor contains an equal number of holes in the valence band and electrons in the conduction band:

$$ n_e = n_h = N\exp\!\left(-\frac{E_g}{2kT}\right) $$

### 7.8 Conductivity of an intrinsic semiconductor

Under an externally applied field, the electrons excited into the conduction band by thermal means accelerate using the vacant states available in the conduction band. At the same time the holes in the valence band also move, but in a direction **opposite** to that of the electrons.

The conductivity depends on the concentration of these charge carriers, $n_e$ and $n_h$. In the case of metals we referred to the drift velocity acquired by the free electrons in an applied field; similarly, the **mobility** of conduction electrons and holes, $\mu_e$ and $\mu_h$, is defined as the drift velocity acquired under unit field gradient. The conductivity of a semiconductor is then

$$ \boxed{\ \sigma = e\left(n_e\mu_e + n_h\mu_h\right)\ } $$

where $e$ is the electronic charge and $n_e$, $n_h$ are concentrations per unit volume. For Si the mobilities are $\mu_e = 0.14$ and $\mu_h = 0.05\ \text{m}^2\text{V}^{-1}\text{s}^{-1}$; for Ge, $0.39$ and $0.19$.

> [!important] Definition
> **Mobility $\mu$** — the drift velocity acquired by a charge carrier under unit field gradient, in $\text{m}^2\text{V}^{-1}\text{s}^{-1}$.

For an intrinsic semiconductor the number of charge carriers is dependent on temperature **exponentially**, and therefore increases very rapidly with increasing temperature; the conductivity increases in the same fashion. The small temperature dependence of the mobilities can be neglected compared with the effect of temperature on the number of carriers. Consequently a plot of $\log\sigma$ against $1/T$ (in kelvin) is a straight line, and the energy gap is computed from its slope.

$$ \ln\sigma = \ln\sigma_0 - \frac{E_g}{2k}\cdot\frac{1}{T} \qquad\Longrightarrow\qquad \text{slope} = -\frac{E_g}{2k} $$

### 7.9 Extrinsic semiconductors: donors and n-type conduction

In **extrinsic** semiconductors the conduction is due to the presence of extraneous impurities. The process of deliberate addition of controlled quantities of impurities to a pure semiconductor is called **doping**, and doping markedly increases the conductivity.

Consider a Si crystal doped with a fifth-column element such as P, As or Sb. The fifth-column element substitutes for a Si atom in the diamond cubic structure. Four of the five electrons in the outermost orbital of the phosphorus atom take part in the tetrahedral bonding with the four Si neighbours.

![[EP2 - Silicon doped with phosphorus n-type.png|450]]

*Figure — silicon doped with phosphorus: four of the five outer electrons enter the tetrahedral bonds, and the fifth occupies a shallow donor level just below the conduction band.*

The fifth electron cannot take part in the discrete covalent bonding — it is **loosely bound** to the parent atom. It is possible to calculate an orbit for the fifth electron by assuming that it revolves around the positively charged phosphorus ion in the same way as the $1s$ electron revolves around the hydrogen nucleus. There is, however, one important difference: the electron of the phosphorus atom is moving in the **electric field of the silicon crystal** and not in free space, as in the hydrogen atom. This brings the **dielectric constant of the crystal** into the orbital calculation, and the radius of the electron orbit turns out to be very large — about $80\ \text{\AA}$ against $0.5\ \text{\AA}$ for the hydrogen orbit.

Such a large orbit evidently means that the fifth electron is almost free and is at an energy level close to the conduction band. Excitation of the fifth electron into the conduction band therefore takes place much more readily than excitation from the valence band of the silicon crystal. The phosphorus atom is said to **donate** its electron to the semiconductor; the energy level of the fifth electron is the **donor level**; and the energy required to excite it into the conduction band is the **ionization energy**.

As the elements to the right of the fourth column donate negative charges (electrons), semiconductors doped with them are called **n-type**.

> [!important] Definitions
> **Doping** — deliberate addition of controlled quantities of impurity to a pure semiconductor.
> **Donor level** — the shallow energy level just below the conduction band at which the loosely bound fifth electron sits.
> **Ionization energy** — the energy required to excite a donor electron into the conduction band; small compared with $E_g$.
> **n-type semiconductor** — one in which electrons donated by a fifth-column impurity are the majority carriers.

As compared to the energy gap, the ionization energy of an impurity atom is very small; at room temperature, therefore, a large fraction of the donor-level electrons are excited into the conduction band, much larger than the fraction excited by the intrinsic process from the valence band. According to the **law of mass action**, the product of the number of electrons in the conduction band and the number of holes in the valence band must be constant:

$$ n_e\,n_h = \text{constant} = n_i^2 $$

This condition drastically reduces the number of holes in the n-type semiconductor, and the electrons in the conduction band become the **majority charge carriers**.

### 7.10 Acceptors and p-type conduction

Consider the alternative process of doping a Si crystal with a third-column element such as Al, Ga or In. Al has three electrons in the outer orbital; substituting for Si in the crystal, it needs an **extra electron** to complete the tetrahedral arrangement of bonds around it.

The extra electron can come only from one of the neighbouring Si atoms, thereby creating a vacant electron site (**hole**) on that Si. The Al atom with the extra electron becomes a negative charge, and the hole with a positive charge can be considered to revolve around the Al atom, leading to the same orbital calculations as before.

![[EP2 - Silicon doped with aluminium p-type.png|470]]

*Figure — silicon doped with aluminium: the trivalent atom completes its four bonds by taking an electron from a neighbour, leaving a mobile hole bound to a shallow acceptor level.*

At $0\ \text{K}$ the holes remain bound to the impurity atoms; as the temperature is raised, the holes break away from the impurity atoms by thermal excitation and become available for conduction. The ionization energy to free a hole bound to the impurity is approximately the same as the ionization energy of donor electrons in the same crystal. The bound-hole levels are called **acceptor levels** (Al accepts an electron) and lie just **above the valence band**.

The fraction of holes created by thermal excitation in doped Si is much larger than the fraction of electrons created by excitation into the conduction band. The law of mass action holds here as well, and the positive holes become the **majority charge carriers**. Such an extrinsic semiconductor is a **p-type** semiconductor.

> [!note] The symmetry is exact
> Donor electron and acceptor hole are the same problem viewed from opposite bands: a hydrogen-like centre in a dielectric medium, with a large Bohr radius and a correspondingly small binding energy. That is why the ionization energies are nearly equal, and why the same orbital calculation serves both.

The conductivity equation of §7.8 describes extrinsic semiconductors as well. The only difference is that the number of electrons in the conduction band and the number of holes in the valence band are **not equal** in an extrinsic semiconductor; one of the two dominates, depending on the type of the extrinsic process.

| | **n-type** | **p-type** |
| --- | --- | --- |
| Dopant | Fifth column — P, As, Sb | Third column — Al, Ga, In |
| Mechanism | Donates a loosely bound electron | Accepts an electron, leaving a hole |
| Impurity level | Donor, just below conduction band | Acceptor, just above valence band |
| Majority carrier | Electrons | Holes |
| Minority carrier | Holes (suppressed by mass action) | Electrons (suppressed by mass action) |

### 7.11 The three regions of the conductivity–temperature plot

A typical plot of the logarithm of conductivity against temperature for an extrinsic semiconductor divides into **three distinct regions**.

![[EP2 - log conductivity versus reciprocal temperature.png|450]]

*Figure — $\log\sigma$ against $1/T$: a steep extrinsic (ionization) branch at low temperature, a flat exhaustion plateau near room temperature, and a steeper intrinsic branch above it.*

1. **Extrinsic (ionization) region — low temperature, large $1/T$.** The conductivity is an exponential function of temperature, because electrons excited from the donor level to the conduction band (or holes created by excitation to the acceptor level) become available in increasing numbers as temperature rises. From the slope of the straight line in this region, the **ionization energy of the impurity** can be calculated.
2. **Exhaustion region — higher temperature.** Excitation of charge carriers from the impurities is nearing completion, because the unexcited impurities are exhausted. The region is flat, with almost zero slope. The slope can even become **positive**, because of the dominance of the temperature-dependent mobility term: increasing $T$ decreases the mean free path of the conduction electrons/holes, so the mobility falls as $T$ rises.
3. **Intrinsic region — above room temperature.** Another linear region, with a negative slope of large magnitude, corresponding to intrinsic conduction. The difference in slope between the extrinsic and intrinsic regions reflects the difference in magnitude between the impurity ionization energy and the energy gap $E_g$.

> [!tip] Design consequence of the plateau
> For **stability** of operation of a semiconductor device, a relatively flat region — where conductivity does not vary appreciably with ambient temperature — is often desirable. For a **thermistor**, on the other hand, maximum sensitivity to temperature is desirable, so the device is deliberately operated on the steep extrinsic or intrinsic branch. The same curve is therefore either a nuisance or the product, depending on which region the device is biased into.

### 7.12 Doping in practice: diffusion, predeposition and drive-in

Impurity doping can be carried out by solid-state diffusion under two conditions:

- **Constant surface concentration.** A constant surface concentration of the dopant is maintained at a high enough temperature for the dopant to diffuse in and create a characteristic concentration profile.
- **Constant total quantity (predeposition + drive-in).** A constant total quantity of the dopant is first deposited on the surface by **predeposition** — either by short-time annealing or by another technique such as **ion implantation** at low temperature. The concentration profile is then altered by a high-temperature anneal in a non-doping atmosphere, the **drive-in**.

A **p-n junction** is created by diffusing an impurity, say a p-type one, into the bulk semiconductor through a **window in the oxide layer**, where the bulk crystal has already been doped to be n-type.

> [!note] The oxide is the mask
> The window-in-oxide method is the reason doping can be *patterned*: SiO₂ is impermeable to the common dopants, so the junction is defined lithographically rather than by a mechanical mask. Everything that follows about the diode assumes this geometry.

### 7.13 The p-n junction at equilibrium

When a pure semiconductor is doped to become n-type, the **Fermi level shifts up** from the middle of the energy gap towards the donor level. This happens because the position corresponding to 50 % probability of occupation moves up, owing to the relatively high concentration of donor electrons in the conduction band. If the crystal is p-type, the Fermi level shifts **down** towards the acceptor level.

When the same crystal is doped to become n-type on one side and p-type on the other, the Fermi level must be **constant throughout the crystal in thermal equilibrium**. This forces the electron energy levels at the bottom of the conduction band in the n-part to be **lower** than those in the p-part by an amount equal to the contact potential $eV_0$.

![[EP2 - p-n junction band diagram at equilibrium.png|450]]

*Figure — the p-n junction at equilibrium: a single Fermi level runs across both sides, the bands are offset by $eV_0$, and the junction region contains the resulting barrier.*

At equilibrium there is no net current across the junction:

- The concentration of electrons in the conduction band on the p-side is small; these electrons can accelerate **down the potential hill** across the junction to the n-side, giving a current $I_0$ proportional to their number.
- The concentration on the n-side is large, because of the donor contribution; but only a small number of these electrons can flow to the p-side, because they face the **potential barrier**. That small number is computed with the Boltzmann probability equation.
- At equilibrium the current from n-side to p-side and the current in the opposite direction are the same, both equal to $I_0$. An equal additional contribution to $I_0$ comes from the flow of holes across the junction — the hole concentration is large in the p-region compared with the n-region.

### 7.14 Forward and reverse bias

If an external voltage $V_i$ is applied such that the **p-side becomes positive** with respect to the n-side, the electron energy levels change. Note that the potential for electrons is **opposite in sense** to the conventional method of representing the sign of an electric potential. The barrier at the junction is now **lowered by $eV_i$**, resulting in a greatly enhanced current flow in the forward direction, from n-side to p-side.

![[EP2 - Forward bias lowered barrier.png|440]]

*Figure — forward bias: the barrier is lowered by $eV_i$, so the majority electrons can cross in large numbers and the current rises steeply.*

This change in barrier does **not** affect the flow of electrons in the reverse direction, from p-side to n-side, because that flow is still down the potential hill. The applied voltage therefore causes a large **net** current in the forward direction.

If the voltage is applied in the **reverse** direction, the potential barrier for electrons at the junction is **increased by $eV_i$**. This drastically reduces the current flow from the n-side to the p-side; in the reverse direction, the flow remains unchanged at $I_0$.

![[EP2 - Reverse bias raised barrier.png|440]]

*Figure — reverse bias: the barrier is raised by $eV_i$, the n → p current is choked off, and only the small, barrier-independent $I_0$ survives.*

> [!note] The asymmetry in one sentence
> Forward bias lowers a barrier that was *already* being crossed by the majority carriers, so the current grows exponentially; reverse bias raises the same barrier, but the reverse current never had to climb it, so it stays at $I_0$. That is the rectifying action of the diode, and it follows from the band diagram alone.

#### The diode equation behind the curve

*Added depth beyond the slides.* The qualitative picture above is summarised by the Shockley diode equation

$$ I = I_0\left[\exp\!\left(\frac{eV_i}{kT}\right) - 1\right] $$

which gives $I \to -I_0$ for large negative $V_i$ (the barrier-independent reverse current) and exponential growth for positive $V_i$. The prefactor $I_0$ is exactly the equilibrium exchange current of §7.13, which is why the two bias cases are mirror images of the same number.

> [!tip] Exam pointer — Part 2
> Expect: the overlap criterion for the disappearance of the gap; the definition of a Brillouin zone and the FCC first zone bounded by $\{111\}$/$\{200\}$; valence band versus conduction band; the two metallic band structures (half-filled, overlapping) and the group-by-group table (Cu/Ag/Au half full, Mg/Be overlapping, Al half full, column IV full with no overlap); the gap sequence 5.4 → 1.1 → 0.7 → 0.08 → 0 eV with the separation-dominates-over-charge argument; the 3 eV semiconductor/insulator convention; $E_F$ midgap, $E - E_F = E_g/2$, and $n = N\exp(-E_g/2kT)$ with the Boltzmann approximation justified by $E_g/2 \gg kT$; $n_e = n_h$ intrinsic and $\sigma = e(n_e\mu_e + n_h\mu_h)$ with the Si and Ge mobilities; the donor/acceptor mechanisms, the $80\ \text{\AA}$ versus $0.5\ \text{\AA}$ orbit and the role of the dielectric constant; mass action $n_en_h$ = constant and majority/minority carriers; the three regions of $\log\sigma$ versus $1/T$ and what each slope measures; the two diffusion conditions (constant surface concentration; predeposition + drive-in) and the oxide-window junction; the constant-$E_F$ construction with the $eV_0$ offset; and the forward/reverse barrier argument. The added depth to be ready with: why the slope of the exhaustion region can turn positive, and why the reverse current is independent of the barrier.

---

## Formula Summary — Electrical & Electronic Properties

| Quantity | Expression | Notes |
| --- | --- | --- |
| Resistivity and conductivity | $\rho = 1/\sigma$ | Ranges: conductor $10^{-9}$–$10^{-3}$, semiconductor $10^{-3}$–$10^{3}$, insulator $>10^{4}\ \Omega\,\text{m}$ |
| de Broglie wavelength | $\lambda = h/mv$ | Electron as a wave |
| Wave number | $k = 2\pi/\lambda$ | Inversely related to $\lambda$ |
| Free electron energy | $E = \dfrac{h^2k^2}{2m}$ | Parabolic $E$–$k$; non-relativistic |
| 1-D box quantisation | $E = \dfrac{n^2h^2}{8mL^2}$ | $\lambda_{\max} = 2L$ |
| 3-D box quantisation | $E = \dfrac{h^2}{8m}\left(\dfrac{n_x^2}{L_x^2}+\dfrac{n_y^2}{L_y^2}+\dfrac{n_z^2}{L_z^2}\right)$ | Two electrons (opposite spin) per state |
| Fermi–Dirac occupation | $P(E) = \dfrac{1}{1+\exp[(E-E_F)/kT]}$ | $P(E_F) = 0.5$ at every $T$ |
| Conductivity of a metal | $\sigma = \dfrac{ne^2\tau}{m}$ | $\tau$ = mean collision time; $l = v\tau$ |
| Critical field | $H_c = 0$ at $T = T_c$ | $H_c$ and $J_c$ rise as $T$ falls below $T_c$ |
| Superconductor susceptibility | $\chi = -1$, $M = -H$, $B = 0$ | Perfect diamagnetism (Meissner) |
| Type II critical fields | $H_{c1} < H < H_{c2}$ | Vortex region; Meissner incomplete |
| Bragg condition (1-D motion) | $k = \pm n\pi/d$ | $\sin\theta = 1$; electrons totally reflected |
| Bragg condition (3-D) | $k = \pm n\pi/(d\sin\theta)$ | $\theta$ between 0 and 90° |
| Energy gap | $\Delta E_{\text{gap}} = E_{\text{sine}} - E_{\text{cosine}}$ | Potential-energy difference of the two standing waves |
| Intrinsic carrier concentration | $n = N\exp\!\left(-\dfrac{E_g}{2kT}\right)$ | Valid for $E_g/2 \gg kT$ |
| Intrinsic equality | $n_e = n_h$ | Every excited electron leaves one hole |
| Semiconductor conductivity | $\sigma = e\left(n_e\mu_e + n_h\mu_h\right)$ | $\mu_e,\mu_h$: Si 0.14/0.05, Ge 0.39/0.19 $\text{m}^2\text{V}^{-1}\text{s}^{-1}$ |
| Slope of $\ln\sigma$ vs $1/T$ | $-E_g/2k$ (intrinsic); $-E_i/2k$ (extrinsic) | $E_i$ = impurity ionization energy |
| Mass action | $n_e n_h = n_i^2$ | Constant at a given $T$; holds for extrinsic too |
| Contact potential | $eV_0$ | Band offset across the junction at equilibrium |
| Diode equation | $I = I_0\left[\exp(eV_i/kT)-1\right]$ | *Added depth*; $I_0$ = equilibrium exchange current |

> [!note] Source images
> The diagrams and plots embedded in this block — the resistivity-range chart (Part 1, slide 2), the parabolic $E$–$k$ (Fig. 1), the de Broglie wavelengths (Fig. 2), the Fermi–Dirac curves (Fig. 3), the field-biased distribution (Fig. 4), the collision sawtooth (Fig. 5), the Ag/Sn resistivity (Fig. 6), $H_c$ versus $T$ (Fig. 7), the Meissner effect (Fig. 8), type I/II magnetization (Fig. 9), the standing waves (Fig. 10), the $E$–$k$ break (Fig. 11) and the forbidden gap (Fig. 12); and in Part 2, the overlapping bands (Fig. 13), the insulator/semiconductor gap (Fig. 14), the midgap Fermi level (Fig. 15), the P-doped and Al-doped cells (Figs. 16–17), the $\log\sigma$ versus $1/T$ plot (Fig. 18) and the three junction band diagrams (Fig. 19) — are the original figures extracted from [[Electrical and Electronic Properties - Part 1_Odd_2026-27.pdf]] and [[Electrical and Electronic Properties - Part 2_Odd_2026-27.pdf]] and stored in `Material Science/images/` with the `EP1`/`EP2` prefix. The band-structure classification flowchart in §7.6 is an original reconstruction of the decision sequence in the slides and lives in the vault as `Excalidraw/EP - Band structure classification.excalidraw.md`.

---

# Magnetic Properties

Every material is magnetic to some degree, but the *strength* of the response spans more than ten orders of magnitude — a diamagnetic solid barely pushes the lines of force out of its interior, a soft ferromagnet multiplies them thousands of times for the same applied field. This block builds that response from one microscopic quantity, the **Bohr magneton**, then shows how exchange coupling between neighbouring spins turns a collection of tiny atomic moments into domains, and how the domain behaviour turns into the hysteresis loop, the transformer core and the permanent magnet.

Compiled from the lecture slides ([[Magnetic Properties_Odd_2026-27.pdf]]) and the handwritten class notes in [[MO NOTES (1).pdf]]. Slides follow **Raghavan, *Materials Science and Engineering*** and **Callister, *Fundamentals of Materials Science and Engineering***.

> [!info] How the block fits together
> The first third is *field bookkeeping*: $B$, $H$, $\mu$, $\mu_r$, and the three classes of magnetic response ranked by susceptibility (§8.1–§8.2). The middle third is *atomic origin*: where a permanent moment comes from (electron spin, Hund's rule, the Bohr magneton), why the moment of a free atom shrinks when the atom enters a crystal, and why only Fe, Co and Ni — and the heavy rare earths — keep their moments aligned at all (§8.3–§8.14). The last third is *engineering*: domains, the hysteresis loop, wall motion versus rotation, and the split between soft and hard magnetic materials that follows from the loop's shape (§8.15–§8.17).

---

## 8. Magnetic Properties

### 8.1 Magnetic induction, field strength and permeability

A magnetic field applied to vacuum produces a magnetic induction that is strictly proportional to the applied field strength; the constant of proportionality is the permeability of free space. In a solid the same relation holds with the permeability of the *material*, and the ratio of the two permeabilities is the single number that ranks how strongly a material responds. Everything later in this block — susceptibility, domains, hysteresis — sits on top of this distinction between the applied field $H$ and the resulting flux density $B$.

$$ B = \mu_0 H $$

In SI units the permeability of free space is $\mu_0 = 4\pi \times 10^{-7}\ \text{H m}^{-1}$ (henry per metre). It was *originally defined to have a value of unity* in the cgs system, which is why cgs susceptibilities and permeabilities are quoted as bare dimensionless numbers.

If the field is applied to a solid medium, the magnetic induction in the solid is given by the same relationship with the permeability of the solid:

$$ B = \mu H $$

where $\mu$ is the permeability of the solid material through which the magnetic lines of force pass. In general $\mu \ne \mu_0$; the ratio of the two is the **relative permeability**:

$$ \mu_r = \frac{\mu}{\mu_0} $$

	The magnetic induction in a solid is also defined in a second way, which separates the applied field from the material's own contribution:

$$ \boxed{\ B = \mu_0 (H + M)\ } $$

> [!important] Definitions
> **Magnetic induction (magnetic flux density) $B$** — the flux per unit area inside the medium, in tesla ($\text{T}$) or weber per square metre ($\text{Wb m}^{-2}$).
> **Field strength $H$** — the applied magnetic driving field, in ampere per metre ($\text{A m}^{-1}$).
> **Permeability $\mu$** — the property of the medium through which the lines of force pass, in $\text{H m}^{-1}$; in general $\mu \ne \mu_0$.
> **Relative permeability $\mu_r$** — the dimensionless ratio $\mu/\mu_0$.
> **Magnetization $M$** — the magnetic moment per unit volume of the solid, in $\text{A m}^{-1}$ (see §8.6).

Comparing the two definitions of $B$ gives $B=\mu_0(H+M)=\mu_0\mu_r H$, so $\mu_r = 1 + M/H$. The ratio $M/H$ is the **magnetic susceptibility** $\chi$ — the quantity by which the three classes of magnetic behaviour are actually ranked in §8.2.

| Symbol | Quantity | SI unit |
| --- | --- | --- |
| $B$ | Magnetic induction / flux density | $\text{T} = \text{Wb m}^{-2}$ |
| $H$ | Magnetic field strength | $\text{A m}^{-1}$ |
| $M$ | Magnetization (moment per volume) | $\text{A m}^{-1}$ |
| $\mu_0$ | Permeability of free space | $4\pi\times10^{-7}\ \text{H m}^{-1}$ |
| $\mu$ | Permeability of the medium | $\text{H m}^{-1}$ |
| $\mu_r$ | Relative permeability, $\mu/\mu_0$ | — |
| $\chi$ | Susceptibility, $M/H$ | — |

> [!warning] The two classical traps in this section
> **$B$ and $H$ are not interchangeable.** $H$ is what the coil produces and is set by the current and geometry alone; $B$ is what the material does with it. A ferromagnet leaves $H$ unchanged but raises $B$ by a factor $\mu_r$ of $10^2$–$10^5$.
> **$\mu_0$ is not 1.** In cgs it was defined as unity, so a cgs susceptibility of $10^{-5}$ and an SI susceptibility of $10^{-5}$ are the same number *only because* $\chi$ is dimensionless in both systems — but $\mu_r$ and $\mu$ are not. Always state the system when quoting $\mu$.

### 8.2 Diamagnetism, paramagnetism and ferromagnetism

The mechanical picture of magnetism in an atom is a current loop. The **orbital motion of the charge-carrying electrons** in an atom is analogous to a current-carrying coil; when a magnetic field is applied to an atom, the motion of the orbital electrons is modified in such a way that a *weak magnetic moment opposing the field* is induced. This interaction is diamagnetism.

In a **diamagnetic** solid the lines of force due to an applied field are therefore repelled. The diamagnetic susceptibility is negative and very small in magnitude, typically of the order of $-10^{-5}$.

An important exception is a **superconductor**, which is perfectly diamagnetic with a susceptibility value of $-1$: all the lines of force are repelled by a superconductor, which makes superconductors useful for shielding out magnetic fields.

**Paramagnetic** solids have a small positive susceptibility, of the order of $10^{-3}$; it *decreases* with increasing temperature, because thermal energy tends to randomize the alignment. **Ferromagnetic** solids have a very large positive susceptibility, in the range $10^2$–$10^5$, and strongly attract the magnetic lines of force.

| Class | Susceptibility $\chi$ | Response of the lines of force | Origin |
| --- | --- | --- | --- |
| **Diamagnetic** | $-10^{-5}$ (negative, very small) | Slightly repelled | Induced orbital moment *opposing* the field |
| **Superconductor** | $-1$ (perfect diamagnet) | Completely expelled | Perfect shielding of the interior |
| **Paramagnetic** | $+10^{-3}$, falls as $T$ rises | Weakly attracted | Alignment of permanent moments, fought by thermal energy |
| **Ferromagnetic** | $+10^2$ to $10^5$ | Strongly attracted | Permanent moments already aligned by bonding forces |

![[MAG - Diamagnetic paramagnetic ferromagnetic.png|440]]

*Figure — the three responses side by side: (a) a diamagnetic solid repels the lines of force slightly, (b) a paramagnetic solid attracts them weakly, (c) a ferromagnetic solid attracts them very strongly, concentrating the flux inside itself.*

> [!note] Why the superconductor is the exception that proves the rule
> Diamagnetism is a *universal* consequence of orbital electrons, so every material is diamagnetic to the extent of $\sim10^{-5}$ — it is simply swamped whenever permanent moments exist. In a superconductor the induced screening currents are lossless, so the expulsion is complete rather than partial: $\chi=-1$ is the largest diamagnetic response physically possible, and it is why a magnet can be levitated over a superconducting cup.

### 8.3 Paramagnetism: alignment of permanent moments

Some atoms and molecules possess **intrinsic permanent magnetic moments**. In the absence of an externally applied field the moments of the atoms in a solid are randomly oriented with respect to one another, and the solid as a whole has no net magnetic moment. If an external field is applied, the moments tend to align themselves parallel to the applied field so as to lower their potential energy.

Just as a suspended magnetic needle aligns itself spontaneously with the earth's magnetic field, there is a spontaneous tendency for the permanent moments of the atoms of the solid to align in the direction of the field, thereby *intensifying* the lines of force in the field direction — this phenomenon is **paramagnetism**.

The aligning force on the permanent moments of the atoms in ordinary magnetic fields is rather small, so the paramagnetic effect is weak — this is exactly why $\chi_{\text{para}}\sim10^{-3}$ and why it falls with temperature: the alignment competes with thermal randomization and loses ground as $T$ rises.

**Ferromagnetic solids** are those in which the permanent magnetic moments (due to electron spins) are *already aligned* by bonding forces, without any applied field. That is the whole structural difference between the two: paramagnetism is field-induced alignment of independent moments; ferromagnetism is spontaneous alignment produced by the chemical bond.

> [!note] What "already aligned by bonding forces" is doing
> The phrase is the entire content of §8.8–§8.9. There is no external field and no thermal assistance — the parallel arrangement of neighbouring spins must lower the *electronic* energy of the solid, by an amount (the exchange energy) that beats the entropy of randomization up to the Curie temperature. Ferromagnetism is therefore a bonding phenomenon, and like any bonding phenomenon it depends on interatomic distance.

### 8.4 Magnetic moments due to electron spin

Permanent magnetic moments can arise from three sources: the **orbital magnetic moment** of electrons, corresponding to the quantum number $m_l$; the **spin magnetic moment** of electrons, corresponding to the spin quantum number $m_s$; and the **spin magnetic moment of the nucleus**. Of these, the spin magnetic moments of the electrons are the only ones that are important from our point of view — the nuclear moment is some three orders of magnitude smaller, and the orbital contribution is largely quenched in the solids of interest.

An electron can be crudely approximated as a charge-carrying particle spinning about its axis and thereby creating its own magnetic field. The magnetic moment of one electron spin is taken as one unit, called the **Bohr magneton** $\mu_B$:

$$ \mu_B = 9.273 \times 10^{-24}\ \text{A m}^2 $$

The net magnetic moment of two electrons of opposite spin is zero. Atoms or molecules whose quantum states have *all* electrons paired therefore have zero net magnetic moment; atoms with unpaired electrons do not. For instance, the alkali metal atoms have only one electron in the outermost $s$ orbital; that electron is unpaired and can align itself in an applied field, giving rise to paramagnetism.

> [!important] Hund's rule — the order of filling
> **All orbitals will be singly occupied before any is doubly occupied.**
> **All of the unpaired electrons must have the same spin.**

Hund's rule converts an electron count into a magnetic moment in units of $\mu_B$, because the moment is simply the excess of one spin direction over the other:

| Orbital filling | Unpaired electrons | Net moment |
| --- | --- | --- |
| $p^3$ | 3 (all parallel) | $3\,\mu_B$ |
| $p^4$ | 2 (fourth opposes) | $2\,\mu_B$ |
| $d^5$ | 5 (all parallel) | $5\,\mu_B$ |
| $d^9$ | 1 | $1\,\mu_B$ |
| $f^7$ | 7 (all parallel) | $7\,\mu_B$ |

An atom with 3 electrons in a $p$ orbital has all 3 spins aligned, giving a net magnetic moment of $3\,\mu_B$; an atom with 4 electrons in the $p$ orbital has a net moment of only $2\,\mu_B$, because the spin of the fourth electron is opposite to that of the first three. Similarly an atom with 5 electrons in a $d$ orbital has a net moment of five units, but an atom with 9 electrons in the $d$ orbital has a net moment of only one; 7 electrons in an $f$ orbital give 7 units.

### 8.5 The solid state correction: 4s–3d overlap

The simple deduction of the net moment from Hund's rule has to be modified in the solid state, where the electron energy levels of the outermost orbitals interact and form **energy bands**.

In the transition metals the energy bands due to the $4s$ and the $3d$ orbitals may overlap to some extent; the $4s$ electrons spend some time in the $3d$ band. If the $3d$ electrons are five or more in number, the spins of the overlapping $4s$ electrons must be opposite to that of the unpaired $3d$ electrons — such an overlap therefore *reduces* the net magnetic moment.

| Atom | Outer configuration | Moment as free atom ($\mu_B$) | Moment in the crystal ($\mu_B$) |
| --- | --- | --- | --- |
| Fe | $3d^6 4s^2$ | 4 | 2.2 |
| Co | $3d^7 4s^2$ | 3 | 1.7 |
| Ni | $3d^8 4s^2$ | 2 | 0.6 |
| Gd | $4f^7$ (no $4f$ overlap) | 7 | 7 |

The Fe atom with an outer electronic configuration $3d^6 4s^2$ has a moment of 4 units as a free atom but only 2.2 as part of the crystal; Co with $3d^7 4s^2$ has 1.7, and Ni with $3d^8 4s^2$ has only 0.6 unit in the crystal. In the case of Gd the net magnetic moment of seven in the free atom remains *unchanged* in the solid state, because there is no overlap of the $4f$ orbitals with the other energy bands — the $4f$ states stay atomic.

> [!warning] Hund's rule gives an upper bound, not the crystal value
> An exam answer that quotes $4\,\mu_B$ for iron is quoting the *free atom*. The engineering number is $2.2\,\mu_B$ per atom, and the difference is not a rounding correction but a band effect: $4s$ electrons leak into the $3d$ band and pair off part of the moment. This is also why Gd is the outlier, with its full 7 units retained.

### 8.6 Magnetization

The magnetization of a solid is the sum of the magnetic moments in unit volume of the solid:

$$ M = \frac{\sum \mu}{V} $$

$$ \left[\text{A m}^2/\text{m}^3\right] = \left[\text{A m}^{-1}\right] $$

The unit works out to ampere per metre, the same as $H$ — which is why $M$ can be added directly to $H$ in $B=\mu_0(H+M)$.

### 8.7 Hund's rule as spin-dependent electrostatic energy

Hund's rule is a manifestation of the **spin-dependent electrostatic energy** of the electrons in an orbital. When the electrons have the same momentum and the same spin, a certain distance must separate them from one another in order to be consistent with the **Pauli exclusion principle**. This physical separation tends to *increase* their kinetic energy, but it *reduces* the electrostatic repulsive energy between them.

Whether the electrons will align their spins or not therefore depends on the sign of the net change in energy. The stable, energetically favoured order of filling of electronic orbitals in atoms is what we call Hund's rule — it is not an arbitrary convention but the outcome of that energy balance.

> [!note] Why the same balance reappears in the solid
> This is the same competition that decides ferromagnetism in §8.8: parallel spins cost kinetic energy (the electrons are forced apart, raising the Fermi level) and gain electrostatic energy. In the free atom Hund's rule fixes the filling; in the crystal the same trade decides whether *neighbouring atoms* align their moments.

### 8.8 Band overlap in the first transition series

In the solid state the outer electronic orbitals of neighbouring atoms overlap and produce energy bands. Consider the overlapping and the formation of energy bands in the first transition metals.

At the **left end** of the series the radius of the $3d$ orbitals in the atoms is large enough to give good overlap between neighbours in the crystalline state. The $3d$ band then contains all electrons paired up and there is no net magnetic moment in the crystal. We can say that the atoms are **antiferromagnetically coupled**, because the magnetic moments of a pair of atoms exactly cancel out.

As we go to the **right** in the transition series the $3d$ orbitals shrink, because of greater attraction from the increasing charge on the nucleus, and consequently the overlap of the $3d$ orbitals decreases. The elements Fe, Co and Ni sit in the special situation where this decrease has gone far enough for the exchange interaction to become favourable (next section).

### 8.9 The exchange interaction energy and the 1.5–2.0 criterion

In Fe, Co and Ni the unpaired electrons in the $3d$ orbitals of neighbouring atoms align their spins in a parallel fashion and thereby lower their spin-dependent electrostatic energy. This lowering is partly offset by the rise in the Fermi level and the consequent increase in the average kinetic energy of the electrons; the increase in the Fermi level is directly attributable to the greater physical separation between electrons.

The **net gain in energy** is called the exchange interaction energy:

$$ E_{\text{exchange}} = E_{\text{unmagnetized}} - E_{\text{magnetized}} $$

and it is a *sensitive function of the ratio of the atomic diameter to the 3d orbital diameter*. It turns out that only when this ratio lies between 1.5 and 2.0 is the exchange energy positive and parallel spins energetically favoured:

$$ \boxed{\ 1.5 < \frac{d_{\text{atom}}}{d_{3d}} < 2.0 \ \Longrightarrow\ E_{\text{exchange}} > 0\ } $$

Among the common metals only Fe, Co and Ni have positive exchange energy and are in the spontaneously magnetized state; these metals, or their ions, form the basis of the majority of magnetic materials.

No overlap of the $d$ orbitals occurs in the higher transition series, because the $d$ electrons are strongly attracted to their respective nuclei, which have larger positive charges. The only other elemental crystals in which the exchange energy is appreciable belong to the first rare-earth series, such as **gadolinium, terbium and dysprosium** — there the $4f$ electrons align themselves in a parallel fashion.

#### Why the criterion is a ratio and not a distance

The exchange energy cannot be a function of the interatomic distance alone, because the same distance means different things in different atoms. What matters physically is how much the $3d$ wavefunctions of neighbouring atoms overlap: overlap needs both a large enough orbital ($d_{3d}$ small relative to the spacing) and a small enough separation ($d_{\text{atom}}$). The ratio $d_{\text{atom}}/d_{3d}$ carries both.

The ratio also explains the shape of the transition series. Moving right, $d_{3d}$ shrinks faster than $d_{\text{atom}}$, so the ratio climbs *into* the window at Fe, Co and Ni and back *out* of it beyond them, where the $3d$ orbitals no longer overlap at all. Below the window (left end, large orbitals, strong overlap) the $3d$ band is full and the coupling is antiferromagnetic; above it (higher series, negligible overlap) no coupling at all survives. The window is the narrow band of the periodic table where the two effects are balanced — which is why only three elements out of the whole table are ferromagnetic.

### 8.10 The Curie temperature

Thermal energy tends to randomize the aligned spins, so all ferromagnetic materials become paramagnetic at a sufficiently high temperature. The transition temperature at which all the spin alignment is lost is the **Curie temperature** $T_C$.

Just below the Curie temperature the susceptibility can be $10^2$ to $10^3$, *increasing* as the temperature decreases, because the alignment becomes more complete.

The Curie temperature is a function of the magnitude of the exchange energy — the stronger the coupling, the more thermal energy is needed to destroy it:

| Material | Exchange energy | Curie temperature |
| --- | --- | --- |
| **Co** | Highest | 1400 K |
| **Fe** | Large | 1041 K ($768\,^\circ$C) |
| **Gd** | Small | Below room temperature |

Co, which has the highest exchange energy, has the highest Curie temperature, 1400 K; Gd, with a small exchange energy, has a Curie temperature below room temperature.

### 8.11 Changing the ratio by alloying: the Heusler alloys

The interatomic distance can be changed within limits by **alloying**. Mn in the elemental form is not ferromagnetic; on alloying, the exchange energy can become positive and the spins on neighbouring atoms can become aligned if the Mn–Mn distance is increased by the right amount, so that the ratio of the atomic diameter to the $3d$ orbital diameter falls in the range 1.5–2.0.

This happens in the **Heusler alloys** $\text{Cu}_2\text{MnSn}$ and $\text{Cu}_2\text{MnAl}$, which are ferromagnetic even though none of their constituent elements is ferromagnetic on its own (Cu is diamagnetic, Mn and Sn are not ferromagnetic in the elemental state).

> [!tip] The design lever this opens
> Ferromagnetism is not a property of an element but of a *ratio* — and a ratio can be engineered by alloying. Heusler alloys are the proof of principle: diluting Mn in a Cu–Sn or Cu–Al matrix stretches the Mn–Mn spacing into the 1.5–2.0 window and switches the coupling on. The same logic, read backwards, explains why most alloying of a ferromagnet *weakens* it: the wrong spacing pushes the ratio out of the window.

### 8.12 Ferrimagnetism

In some compounds the constituent atoms may be **antiferromagnetically coupled but have different magnetic moments**. This gives rise to a net magnetic moment in each coupling, and the sum of the moments over all the couplings can result in a magnetization comparable in order of magnitude to ferromagnetism. This phenomenon is **ferrimagnetism**.

![[MAG - Ferro antiferro ferrimagnetic coupling.png|460]]

*Figure — (a) ferromagnetic, (b) antiferromagnetic and (c) ferrimagnetic coupling of electron spins in atoms, denoted by arrows; the length of an arrow is a measure of the magnetic moment of the atom. In (b) the antiparallel moments are equal and cancel exactly; in (c) they are unequal, so each pair leaves a net moment and the solid is magnetized.*

| Coupling | Arrangement of neighbouring moments | Net moment |
| --- | --- | --- |
| **Ferromagnetic** | Parallel | Full sum of the moments |
| **Antiferromagnetic** | Antiparallel, equal moments | Zero — exact cancellation |
| **Ferrimagnetic** | Antiparallel, *unequal* moments | Difference of the sublattice moments |

### 8.13 Ferrites, the inverse spinel, and magnetite

Ferrites of the general formula $\text{Me}^{2+}\text{Fe}_2^{3+}\text{O}_4^{2-}$ can be ferrimagnetic. The divalent metal cation $\text{Me}^{2+}$ is usually $\text{Fe}^{2+}$, $\text{Ni}^{2+}$, $\text{Zn}^{2+}$, $\text{Mg}^{2+}$, $\text{Co}^{2+}$, $\text{Ba}^{2+}$, $\text{Mn}^{2+}$ or some combination of these ions.

These compounds crystallize mostly as the **inverse spinel** structure — a different cation distribution from the normal spinel, in that all of the $A$ cations *and half of the $B$ cations* occupy octahedral sites, while the other half of the $B$ cations occupy tetrahedral sites, for the general formula $AB_2O_4$.

As an example of the incomplete cancellation of magnetic moments, consider the crystal of magnetite, $\text{Fe}_3\text{O}_4$. The ferric ion, with two $4s$ electrons and one $3d$ electron removed from the neutral iron atom, has a magnetic moment of 5 units, and the ferrous ion has 4 units. All the ferric ions in magnetite are antiferromagnetically coupled, so the net magnetic moment of the compound arises from the ferrous ions only. The magnetization $M$ calculated on the basis of **4 net magnetic moments per $\text{Fe}_3\text{O}_4$** is in good agreement with the experimental value for magnetite, which is ferrimagnetic.

#### Counting the moments in magnetite

$\text{Fe}_3\text{O}_4$ contains one $\text{Fe}^{2+}$ and two $\text{Fe}^{3+}$ per formula unit:

- $\text{Fe}^{3+} = 3d^5$: five unpaired spins, $5\,\mu_B$ each — but the two ferric ions are coupled antiparallel, so they contribute $5-5=0$.
- $\text{Fe}^{2+} = 3d^6$: six $d$ electrons, i.e. five parallel plus one opposed, $4\,\mu_B$ — and it has no partner to cancel against.

The surviving moment is therefore $4\,\mu_B$ per formula unit, on the octahedral ferrous site. This is the ferrimagnetic signature: the *sum* is not zero because the two sublattices carry different moments, and the measured magnetization agrees with the 4-unit count rather than with the 14 units that a naive sum of all three ions would give.

### 8.14 The domain structure

Iron has a high Curie temperature of 1041 K ($768\,^\circ$C) and, consequently, almost all the spins remain aligned at room temperature. Yet at room temperature an ordinary piece of iron is *not* magnetic in the absence of an applied field. To explain this discrepancy Weiss conceived the idea of **magnetic domains**.

	The unmagnetized iron crystal consists of a number of domains; within each domain the spins of all the atoms are aligned, but the spins of adjacent domains are not parallel. Because the domains are randomly oriented with respect to one another, their magnetic moments cancel out and the crystal as a whole is not magnetic. In the presence of an external field the domains tend to align with the field, resulting in a large net magnetization of the solid.

> [!important] Definition
> **Magnetic domain** — a region of a ferromagnetic crystal within which the electron spins of all atoms are aligned parallel; the crystal is the assembly of such regions, whose orientations differ.

> [!note] Magnetization is domain alignment, not spin alignment
> The process of magnetization of the iron crystal is *not* the aligning of the electron spins of the different atoms — those are already aligned inside every domain — but the alignment of the various domains, each of which is already ferromagnetic. The energy needed to turn a domain is therefore the energy of a boundary, not the exchange energy of §8.9, and this is why a ferromagnet responds to a field at all at room temperature.

The **magnetostatic energy** of a ferromagnetic solid can be reduced if a number of domains are arranged such that no poles exist at the surface and no lines of force go out of the material. Hence a single domain tends to break up into several domains, even if this means an increase in the domain boundary energy; the domain size does not decrease indefinitely, because at some stage the increasing domain boundary energy would oppose the further splitting.

![[MAG - Domain structure flux closure.png|400]]

*Figure — (a) with one domain the magnetic lines of force go out of the material, storing magnetostatic energy in the surrounding space; (b) with several domains arranged head-to-tail the lines close inside the material and the magnetostatic energy is minimised: no surface poles, no external field.*

### 8.15 The hysteresis loop

The $B$–$H$ curve for a typical ferromagnetic material traces a **hysteresis loop**. As the applied field $H$ is increased, the magnetic induction $B$ increases slowly at first and then more rapidly; the rate of increase slows down again, eventually attaining a saturation value $B_s$. With further increase in the magnetic field there is no increase in the induction.

If the field is reversed, the induction decreases, slowly at first, and reaches a residual value $B_r$ at zero field. $B_r$ represents the amount of residual induction left in the specimen after the removal of the field. If the application of the field is continued in the opposite direction, the domains tend to reverse their alignment, so that the remaining induction is lost at a certain value of the reverse field called the **coercive field** $H_c$. The process of reversal of domains continues to give a net magnetization in the opposite direction; after saturation occurs in this direction, restoring the original field direction completes the loop.

![[MAG - Hysteresis loop.png|420]]

*Figure — magnetic induction $B$ as a function of the applied field $H$ for a ferromagnetic material, tracing a hysteresis loop: the initial curve rises to saturation $B_s$, and on reversal the loop closes through the residual induction $B_r$ and the coercive field $H_c$.*

> [!important] Definitions — the three numbers that describe a loop
> **Saturation induction $B_s$** — the largest induction the material can reach; further increase of $H$ produces no increase in $B$.
> **Residual induction (remanence) $B_r$** — the induction left in the specimen when the applied field is returned to zero.
> **Coercive field (coercivity) $H_c$** — the reverse field required to bring the induction back to zero, i.e. to reverse the remaining domains.

| Feature of the loop | Physical event | Where on the curve |
| --- | --- | --- |
| Slow initial rise | Reversible wall bowing; few domains favourably oriented | Just above the origin |
| Steep middle section | Rapid growth of favourably oriented domains at the expense of others | Below saturation |
| Approach to $B_s$ | Growth complete; rotation of the last domains begins | Near saturation |
| $B_r$ at $H=0$ | Domains stay in their field-set orientation | On the $B$ axis |
| $H_c$ at $B=0$ | Reverse field has undone the alignment | On the $H$ axis |

### 8.16 The magnetization process: wall motion first, rotation last

There are two possible ways to align a random domain structure by applying an external field: one is to **rotate a domain** in the direction of the field, and the other is to allow the **growth of the more favourably oriented domains** at the expense of the less favourably oriented ones.

If the domain structure is compared with the grain structure of a polycrystalline material, the boundaries separating the domains — the **domain walls** — are the analogue of grain boundaries. The domain boundary energy is about $0.002\ \text{J m}^{-2}$. The domain walls, however, are some two orders of magnitude *thicker* than the grain boundaries, because there is a gradual transition from one domain orientation to the next across the wall. Also, unlike grain boundaries, domain boundaries can exist *within* a grain.

Analogous to grain growth, the domain walls can move such that the more favourably oriented domains grow at the expense of the others:

1. **Wall motion dominates below saturation.** In the earlier stages of magnetization, below the saturation region of the hysteresis curve, domain growth is dominant.
2. **Growth is complete near saturation.** The growth is more or less complete as the saturation region is approached.
3. **Rotation takes over.** Thereafter the most favourably oriented, fully grown domain tends to rotate so as to be in complete alignment with the field direction.
4. **The slope falls because rotation costs more.** The energy required to rotate an entire domain is more than that required to move the domain walls during growth; consequently the slope of the $B$–$H$ curve decreases on approaching saturation.

> [!note] The loop area is energy, and the area is paid every cycle
> Each time the hysteresis loop is traversed, energy equal to the area of the loop is dissipated as heat. The power loss due to hysteresis in a transformer core therefore depends on the number of times the full loop is traversed per second — which is why the loss is quoted per cycle and why a transformer on 50 Hz heats less than the same core on 400 Hz.

| Comparison | Grain boundary | Domain wall |
| --- | --- | --- |
| Energy per unit area | — | $\sim0.002\ \text{J m}^{-2}$ |
| Thickness | Thin (a few atomic spacings) | $\sim$2 orders of magnitude thicker |
| Transition across it | Abrupt | Gradual rotation of spins |
| Confined to grains? | Separates grains | Can lie *inside* a grain |
| Motion | Grain growth | Domain growth (magnetization) |

### 8.17 Soft and hard magnetic materials

**Soft magnetic materials** are used in applications requiring frequent reversals of the direction of magnetization. In soft magnetic materials the hysteresis losses must be kept to a minimum. When the induction is large for a small applied field the loop area is small and the hysteresis loss is reduced; the key factor in the design of a soft magnet is therefore to have **easily moving domain walls**.

**Hard magnetic materials** are used to produce permanent magnets. Hysteresis losses are of no significance here, because no repeated reversal of the magnetization is involved in a permanent magnet; what matters is that they must have a **high residual induction $B_r$ and a large coercive force $H_c$**.

The area of the hysteresis loop between $B_r$ and $H_c$ represents the energy required to demagnetize a permanent magnet. The maximum value of this area, $B_rH_c$, is called the **energy product**, and it must be as large as possible for permanent magnets. High-carbon steels and other low-alloy tungsten and chromium steels are used in the martensitic condition as permanent magnets.

| | **Soft magnetic** | **Hard magnetic** |
| --- | --- | --- |
| Application | Transformers, motors, inductors — frequent reversals | Permanent magnets — no reversal |
| Hysteresis loss | Must be minimised | Irrelevant |
| Loop shape | Narrow, steep; large $B$ for small $H$ | Wide; large $B_r$ and large $H_c$ |
| Figure of merit | Small loop area, high $\mu_r$ | Energy product $B_rH_c$ maximised |
| Microstructural requirement | Easily moving domain walls | Pinned walls, high anisotropy |
| Examples | Soft iron, Si–Fe, ferrites | High-C steels; low-alloy W and Cr steels, martensitic |

![[MAG - Soft vs Hard Hysteresis.excalidraw]]

#### The energy product

The demagnetizing energy of a permanent magnet is the area of the second-quadrant rectangle bounded by $B_r$ on the $B$ axis and $H_c$ on the $H$ axis; its largest value is the energy product $B_rH_c$. The two requirements pull in opposite directions microstructurally: $B_r$ wants a large spontaneous moment (a Fe- or Co-rich phase), while $H_c$ wants that moment to be *hard to rotate*, i.e. strong magnetocrystalline anisotropy and pinned domain walls. Alloying for one usually costs the other, which is why permanent-magnet development is a search for the best product rather than the best of either number — and why the martensitic high-carbon and W/Cr steels of the slides, with their heavily pinned walls, were the historical route to a large $H_c$.

> [!tip] Exam pointer — Magnetic Properties
> Expect: the definitions and units of $B$, $H$, $\mu$, $\mu_r$, $M$ and $\chi$; $B=\mu_0H$, $B=\mu H$, $B=\mu_0(H+M)$; the susceptibility ranking (diamagnet $-10^{-5}$, superconductor $-1$, paramagnet $10^{-3}$ falling with $T$, ferromagnet $10^2$–$10^5$); the three sources of moment and why only electron spin matters; Hund's rule with the $p^3/p^4/d^5/d^9/f^7$ moments; the free-atom versus crystal moments of Fe (4 → 2.2), Co (3 → 1.7), Ni (2 → 0.6) and Gd (7 → 7); the exchange-energy criterion $1.5<d_{\text{atom}}/d_{3d}<2.0$; the Curie temperatures (Co 1400 K, Fe 1041 K, Gd below room temperature); ferrimagnetism versus antiferromagnetism versus ferromagnetism and the magnetite 4-$\mu_B$ count; Weiss domains and flux closure; the loop definitions $B_s$, $B_r$, $H_c$; wall motion before rotation and the falling slope near saturation; and the soft/hard split with the energy product $B_rH_c$. The added depth to be ready with: *why* Hund's rule is an electrostatic-energy rule, *why* the criterion is a ratio and how alloying (Heusler alloys) moves it, why domain walls are two orders of magnitude thicker than grain boundaries, and why the loop area is the per-cycle heat in a transformer core.

---

## Formula Summary — Magnetic Properties

| Quantity | Expression | Notes |
| --- | --- | --- |
| Induction in vacuum | $B=\mu_0 H$ | $\mu_0 = 4\pi\times10^{-7}\ \text{H m}^{-1}$ |
| Induction in a solid | $B=\mu H$ | $\mu \ne \mu_0$ in general |
| Relative permeability | $\mu_r=\mu/\mu_0$ | Dimensionless |
| Induction and magnetization | $B=\mu_0(H+M)$ | $M$ in $\text{A m}^{-1}$ |
| Susceptibility | $\chi=M/H$, $\mu_r=1+\chi$ | Negative for diamagnets, $-1$ for a superconductor |
| Magnetization | $M=\sum\mu/V$ | $\text{A m}^2/\text{m}^3=\text{A m}^{-1}$ |
| Bohr magneton | $\mu_B=9.273\times10^{-24}\ \text{A m}^2$ | Moment of one electron spin |
| Moment from Hund's rule | $\mu = (n_\uparrow - n_\downarrow)\,\mu_B$ | e.g. $p^3\to3$, $d^9\to1$, $f^7\to7$ |
| Exchange energy | $E_{\text{exchange}}=E_{\text{unmag}}-E_{\text{magnetized}}$ | Positive $\Rightarrow$ parallel spins favoured |
| Ferromagnetism criterion | $1.5<\dfrac{d_{\text{atom}}}{d_{3d}}<2.0$ | Only Fe, Co, Ni among common metals |
| Curie temperature | $T_C = f(E_{\text{exchange}})$ | Co 1400 K, Fe 1041 K, Gd below room temperature |
| Hysteresis loss per cycle | $W=\oint B\,\mathrm{d}H$ | Equal to the loop area, dissipated as heat |
| Energy product | $(BH)_{\max}\approx B_rH_c$ | Figure of merit for a permanent magnet |

> [!note] Source images
> All Excalidraw figures in this block are original reconstructions; the comparison of soft and hard hysteresis loops lives in the vault as `Excalidraw/MAG - Soft vs Hard Hysteresis.excalidraw.md`. The plots and schematics embedded above — the three magnetic responses (Fig. 1), the ferro/antiferro/ferrimagnetic coupling (Fig. 2), the domain flux closure (Fig. 3) and the hysteresis loop (Fig. 4) — are the original figures extracted from [[Magnetic Properties_Odd_2026-27.pdf]] and stored in `Material Science/images/` with the `MAG` prefix.

---

# Dielectric Materials, Polarization & Optical Properties

The previous block ended by deriving a forbidden energy gap and then using it to build a diode. This block takes the same gap and asks two different questions of it. First: if the gap is so large that no electron can cross it, what *does* an applied electric field do to an insulator? The answer is that it displaces charge without freeing it — the material **polarizes**, and that polarization is the entire basis of the capacitor, the piezoelectric transducer and the ferroelectric memory. Second: what does the gap do to light? The answer decides whether a solid is transparent, coloured or opaque, and the same band diagram that made a diode also explains why diamond is clear and copper is not.

Compiled from the lecture slides ([[Dielectric materials_Polarization_Optical properties_Odd_2026-27.pdf]]) and the handwritten class notes in [[MO NOTES (1).pdf]]. Slides follow **Raghavan, *Materials Science and Engineering*** and **Callister, *Fundamentals of Materials Science and Engineering***.

> [!info] How the block fits together
> §9.1–§9.7 build **polarization**: why an insulator is a dielectric, what a dipole moment per unit volume means, the four mechanisms and the ranking of their speeds. §9.8–§9.9 carry one of those mechanisms to its collective limit in the **ferroelectric**, where BaTiO₃ supplies both the largest dielectric constant in the syllabus and a piezoelectric response. §9.10–§9.12 turn to **light**: metals absorb because empty states are continuous; nonmetals refract because of electronic polarization, and absorb only when a photon can bridge the gap — which is what puts the colour of a material in the window between $1.8$ and $3.1\ \text{eV}$.

---

## 9. Dielectric Materials, Polarization, Optical Properties

### 9.1 Why an insulator is a dielectric

The large magnitude of the energy gap in an ideal insulator precludes the possibility of electrons being excited from the valence band to the conduction band by thermal means — much less by an externally applied electric field. Insulators are therefore very poor conductors of electricity, and are known as **dielectrics**. They find extensive use in the electrical industry for insulation and as **capacitors**.

The charge stored in a capacitor **increases** if a dielectric material is inserted between the plates, and this is due to the **polarization** in the dielectric.

> [!important] Definition
> **Dielectric** — an insulating material in which an applied electric field produces a displacement of bound charge (polarization) rather than a flow of free charge.

When an electric field is applied to a solid containing positive and negative charges, the positive charges are displaced in the direction of the field, towards the negative end, while the negative charges are displaced in the opposite direction. This displacement produces local **dipoles** throughout the solid. The dipole moment per unit volume of the solid — the sum of all the individual dipole moments within that volume — is the **polarization $P$** of the solid.

### 9.2 Polarization and capacitance

When a voltage $V$ is applied to a capacitor whose plates are separated by vacuum, a charge develops on the plates; the capacitance $C$ is a measure of that charge and is defined by

$$ C = \frac{\varepsilon_0 A}{d} $$

where $\varepsilon_0$ is the dielectric constant (permittivity) of free space (vacuum), $A$ the area of the parallel plates and $d$ the distance of separation between them.

If a dielectric material is inserted between the plates, the charge on the plates increases because of the polarization in the material, and the capacitance becomes

$$ \boxed{\ C = \frac{\varepsilon_r \varepsilon_0 A}{d}\ } $$

where $\varepsilon_r$ is the **relative dielectric constant** (relative permittivity) of the material. $\varepsilon_r$, and hence $P$, is determined by measuring the capacitance with and without the dielectric.

> [!important] Definitions
> **Permittivity of free space $\varepsilon_0$** — $8.85\times10^{-12}\ \text{F m}^{-1}$.
> **Relative permittivity $\varepsilon_r$** — the factor by which a dielectric multiplies the capacitance of a vacuum capacitor of the same geometry; dimensionless, and equal to at least 1.
> **Polarization $P$** — the dipole moment per unit volume, in $\text{C m}^{-2}$.

> [!note] Where the extra charge comes from
> The dielectric does not create charge; it *binds* charge at its surfaces. The field displaces positive charge towards the negative plate and negative charge towards the positive one, and the bound surface charge partially cancels the field inside — so the same applied voltage holds more charge on the plates. The measured capacitance therefore rises by exactly $\varepsilon_r$, which is why the effect is a direct, quantitative probe of $P$.

### 9.3 Electronic polarization

**Electronic polarization** is the result of the displacement of the positively charged nucleus and the negative electrons of an atom in opposite directions on application of an electric field.

![[DIE - Four polarization mechanisms.png|430]]

*Figure — the four polarization processes in one figure: (a) electronic, (b) ionic, (c) orientation and (d) space charge; each panel shows the charge configuration before and after the field is applied.*

It is the fastest of the mechanisms, because only the electron cloud has to move, and it is **independent of temperature**: the stiffness of the electron cloud against displacement is an electronic property, not a thermal one.

### 9.4 Ionic polarization

When an electric field is applied to an ionic solid, cations and anions get displaced in opposite directions. The **ionic polarizability** is due to this shift of the ions relative to other oppositely charged neighbours. It must be distinguished from electronic polarization, where the electron cloud of *an atom* shifts with reference to its own nucleus.

Both are independent of $T$; however, ionic polarization is **slower** than electronic polarization, because the displacement of a much heavier ion takes place compared with the electron cloud in the latter.

> [!warning] The two "displacements" are not the same
> Electronic polarization moves an electron cloud *within* an atom (its nucleus stays put); ionic polarization moves whole ions *relative to each other*. A single ionic crystal shows both at once, and they add — which is why the total polarization of an ionic solid is larger than that of a covalent solid of similar size, and why the two mechanisms are often resolved only by their different relaxation frequencies.

### 9.5 Orientation polarization

In the CH₄ molecule the centres of the negative and positive charges coincide, so there is **no permanent dipole moment**. In CH₃Cl, on the other hand, the positive and negative charges do not coincide: since the electronegativity of Cl is greater than that of H, the Cl atom pulls the bonding electrons to itself more strongly than H, so the molecule carries a dipole moment **even without an electric field**.

If an electric field is applied to such molecules, they tend to **align themselves** in the applied field — just like atoms with permanent magnetic moments tend to align with an applied magnetic field, causing paramagnetism. The polarization due to this alignment is **orientation polarization**, and it is **temperature dependent**: with increasing temperature, the thermal energy tends to randomize the alignment.

> [!note] The direct magnetic analogy
> Orientation polarization is to a polar dielectric what paramagnetism is to a collection of permanent moments (§8.3), and it fails for the same reason at the same place: thermal energy. This is why the dielectric constant of a polar liquid falls as it is heated, whereas that of a purely electronic or ionic dielectric barely moves.

### 9.6 Space charge polarization

**Space charge polarization** occurs because of the accumulation of charges at the electrodes or at the interfaces in a multiphase material. The ions diffuse over appreciable distances in response to the applied field, giving rise to a redistribution of charges in the dielectric medium.

The total polarization of a material is the sum of the contributions from the various sources:

$$ \boxed{\ P = P_e + P_i + P_o + P_s\ } $$

> [!important] Definition
> **Space charge polarization** — polarization produced by the drift and accumulation of mobile ionic charge over macroscopic distances, at electrodes or internal interfaces.

### 9.7 The ranking of the mechanisms

The four mechanisms differ not only in origin but in **speed**, and the ranking is strict:

| Mechanism | What moves | $T$ dependence | Relative speed |
| --- | --- | --- | --- |
| **Electronic** | Electron cloud relative to its own nucleus | Independent of $T$ | Fastest |
| **Ionic** | Cations and anions relative to each other | Independent of $T$ | Slower than electronic (heavier ions) |
| **Orientation** | Alignment of permanent molecular dipoles | **Dependent** — thermal randomization | Slower than ionic |
| **Space charge** | Diffusion of ions over several interatomic distances | Dependent (diffusion) | Slowest |

Orientation polarization is even slower than ionic polarization, and space charge polarization is the slowest process of all, because it involves the diffusion of ions over several interatomic distances.

> [!tip] Why the ranking matters for a capacitor
> Each mechanism can only follow a field that alternates slowly enough for it to keep up; above its relaxation frequency it drops out and stops contributing to $\varepsilon_r$. So $\varepsilon_r$ is not a constant of the material but a function of frequency, and a dielectric chosen for a 50 Hz capacitor may be useless at microwave frequency even though nothing about its chemistry changed.

#### Why "slowest" means "first to drop out"

A polarization mechanism is a mass on a spring: the field applies a force, the charge takes a finite time to reach its displaced position. If the field reverses before the displacement completes, the mechanism contributes nothing to the stored charge and instead dissipates energy as heat. Ordering electronic < ionic < orientation < space-charge by response time is therefore identical to ordering them by the frequency at which each stops working — the highest-frequency mechanism survives to the highest frequency, which is why the optical (visible-light) dielectric constant of a transparent solid contains only the electronic contribution.

### 9.8 Ferroelectric materials

In ferroelectrics the dielectric constants are some **two orders of magnitude larger** than those of ordinary dielectrics. Barium titanate is a ferroelectric with a relative dielectric constant of over **2000**, compared with less than 10 for ordinary dielectrics. The difference in magnetic susceptibility between ferromagnetic and paramagnetic materials bears a direct analogy to this difference in the values of the dielectric constants.

As in the ferromagnetic phenomenon, the electric dipoles in a ferroelectric solid are all **aligned in the same direction, even in the absence of an electric field**.

Ferroelectric crystals always exhibit the **piezoelectric** property, which is the mechanical response of a crystal to an electric field, or the electrical response to a mechanical stress.

> [!important] Definitions
> **Ferroelectric** — a material with a spontaneous electric polarization that can be reversed by an applied field; characterized by a very large $\varepsilon_r$.
> **Piezoelectric** — a crystal that develops a charge when stressed, and changes shape when a field is applied; always true of ferroelectrics.

The most important use of BaTiO₃ is as a piezoelectric crystal, in applications such as microphones, phonograph pickups, strain gauges and sonar devices. The high dielectric constant of ferroelectric crystals is also useful for storing energy in small-sized capacitors in electrical circuits.

### 9.9 BaTiO₃ and the ferroelectric Curie temperature

Above $120\,^\circ\text{C}$, barium titanate is a **cubic** crystal in which the centres of the negative and positive charges coincide and there is no spontaneous dipole moment. If the crystal is cooled below the (ferroelectric) **Curie temperature** of $120\,^\circ\text{C}$, the Ti ion shifts to one side of the body centre, and there is also a displacement of the neighbouring oxygen anions. The crystal transforms from cubic to **tetragonal** on cooling through $120\,^\circ\text{C}$; the $c/a$ ratio of the tetragonal cell is

$$ \frac{c}{a} = \frac{4.03\ \text{\AA}}{3.98\ \text{\AA}} = 1.012 $$

![[DIE - BaTiO3 cubic and tetragonal cells.png|400]]

*Figure — the BaTiO₃ unit cell above and below the Curie temperature: the dashed circle in the front view marks the Ti ion, which shifts off the body centre on cooling, dragging the neighbouring oxygens with it.*

The centres of the positive and negative charges no longer coincide, and local dipoles are created throughout the crystal; the aligned dipoles of neighbouring unit cells result in a large polarization in the solid.

> [!note] A 1.2 % distortion doing all the work
> The $c/a$ ratio is only $1.012$ — a distortion of about one part in eighty — yet it is the whole origin of a dielectric constant above 2000 and of the piezoelectric response. The lesson is the same one the magnetic block taught with the $1.5$–$2.0$ exchange criterion: in a cooperative phenomenon, a tiny local distortion is amplified by the alignment of every neighbouring cell, so the macroscopic property is not proportional to the microscopic cause.

> [!warning] Ferroelectric is not ferromagnetic
> The name is borrowed, not shared. "Ferro" in both cases refers to a spontaneous, switchable, aligned state below a Curie temperature — but the order parameter is electric dipole in one case and magnetic spin in the other, and the two materials are otherwise unrelated. A ferroelectric need not be magnetic, and BaTiO₃ is not.

### 9.10 Optical properties of metals

In both cases of metals shown in the figure — Cu and Mg — a high-energy band is only **partially filled** with electrons. Metals are opaque because incident radiation with frequencies in the visible range excites electrons into unoccupied energy states above the Fermi energy; as a consequence, the incident radiation is absorbed.

![[DIE - Band structure of copper and magnesium.png|420]]

*Figure — the band structures of (a) Cu and (b) Mg: both have a partially filled high-energy band, so empty states are continuously available immediately above the occupied levels.*

Total absorption occurs within a very thin outer layer, usually **less than $0.1\ \mu\text{m}$**; thus only metallic films thinner than $0.1\ \mu\text{m}$ are capable of transmitting visible light. All frequencies of visible light are absorbed by metals, because of the continuously available empty electron states that permit the transitions.

![[DIE - Photon absorption and reemission in metals.png|450]]

*Figure — (a) a photon excites an electron above $E_F$ and is absorbed; (b) the electron drops back and re-emits a photon of the same wavelength, which is the reflected beam.*

Metals are in fact opaque to all electromagnetic radiation on the low end of the frequency spectrum — from radio waves, through infrared and the visible, and into about the middle of the ultraviolet. Metals are **transparent to high-frequency (X- and $\gamma$-ray) radiation**.

Most of the absorbed radiation is re-emitted from the surface as visible light of the same wavelength, which appears as **reflected** light; the reflectivity for most metals is between $0.90$ and $0.95$. Some small fraction of the energy from electron-decay processes is dissipated as heat. Because metals are opaque and highly reflective, the perceived **colour** is determined by the wavelength distribution of the radiation that is reflected and *not* absorbed:

- A bright silvery appearance under white light indicates that the metal is highly reflective over the entire visible spectrum — the frequency and number of re-emitted photons in the reflected beam are approximately the same as in the incident beam, as for **Al** and **Ag**.
- **Cu** and **Au** appear red-orange and yellow respectively, because some of the energy associated with light photons having short wavelengths is not re-emitted as visible light.

> [!note] Why a metal cannot be coloured by transmission
> The empty states above $E_F$ form a continuum, so there is no threshold to select wavelengths: every visible photon is absorbed and most are re-emitted. A metal's colour is therefore a *deficit* in the reflected spectrum, never a transmitted one — which is exactly why thin films below $0.1\ \mu\text{m}$ are the only metallic objects that transmit at all.

### 9.11 Optical properties of nonmetals: refraction

By virtue of their electron energy band structures, nonmetallic materials may be **transparent** to visible light. Therefore, in addition to reflection and absorption, **refraction** and **transmission** must also be considered.

Light transmitted into the interior of a transparent material experiences a **decrease in velocity** and, as a result, is bent at the interface; this is **refraction**. The phenomenon is related to **electronic polarization** at the relatively high frequencies of visible light. Because the retardation of electromagnetic radiation in a medium results from electronic polarization, the size of the constituent atoms or ions has considerable influence on the magnitude of the effect: generally, the larger an atom or ion, the greater the electronic polarization, the slower the velocity, and the greater the index of refraction.

$$ n = \frac{c}{v} $$

where $c$ is the velocity in vacuum and $v$ the velocity in the medium.

| Glass | Index of refraction $n$ | Reason |
| --- | --- | --- |
| **Soda–lime glass** | $\approx 1.5$ | Typical silicate network |
| **Highly leaded glass** (90 wt.% PbO) | $\approx 2.1$ | Large Ba and Pb ions raise the electronic polarization |

Additions of large Ba and Pb ions (as BaO and PbO) to a glass increase $n$ significantly — the highly leaded glass containing 90 wt.% PbO reaches approximately $2.1$.

For crystalline ceramics with **cubic** crystal structures, and for glasses, the index of refraction is independent of crystallographic direction, i.e. it is **isotropic**. **Noncubic** crystals have an **anisotropic** $n$: the refractive index is greatest along the directions that have the highest density of ions.

### 9.12 Reflection, absorption and the band gap

Higher index of refraction means greater **reflectivity**; for typical silicate glasses the reflectivity is approximately $0.05$. Just as $n$ depends on the wavelength of the incident light, so the reflectivity varies with wavelength. Reflection losses for lenses and other optical instruments are minimized significantly by coating the reflecting surface with very thin layers of dielectric materials such as **magnesium fluoride (MgF₂)**.

![[DIE - Transmission reflection and absorption.png|460]]

*Figure — transmission through a plate: part of the beam is reflected at the front face, part at the back face, and the remainder is attenuated by absorption over the thickness $l$.*

For an incident beam of intensity $I_0$ impinging on the front surface of a specimen of thickness $l$ and absorption coefficient $\beta$, the transmitted intensity at the back face is

$$ \boxed{\ I_T = I_0(1-R)^2\exp(-\beta l)\ } $$

where $R$ is the reflectance; the expression assumes the same medium exists outside both front and back faces.

Nonmetallic materials may be opaque or transparent to visible light; if transparent, they often appear **coloured**. In principle, light radiation is absorbed in this group of materials by **two basic mechanisms**, which also influence their transmission characteristics:

1. **Electronic polarization** — important only at light frequencies in the vicinity of the **relaxation frequency** of the constituent atoms, that is, the frequency at which the dielectric loss factor $\varepsilon''$ reaches a maximum, for a dielectric material that has no static (d.c.) conductivity and is subjected to an alternating electromagnetic field.
2. **Valence band → conduction band electron transitions** — dependent on the electron energy band structure of the material. Absorption of a photon may occur by the promotion of an electron from the nearly filled valence band, across the band gap, into an empty state within the conduction band.

![[DIE - Photon absorption across the band gap.png|400]]

*Figure — band-gap absorption: a photon of energy at least $E_g$ promotes an electron across the gap and leaves a hole behind; a lower-energy photon passes through.*

These excitations with the accompanying absorption can take place only if the photon energy is greater than that of the band gap, $E_g$:

$$ h\nu \ge E_g \qquad\Longleftrightarrow\qquad \lambda \le \frac{hc}{E_g} $$

In other words, **no visible light is absorbed** by nonmetallic materials having band gap energies greater than about $3.1\ \text{eV}$; these materials, if of high purity, appear **transparent and colourless**. Conversely, **all visible light is absorbed** by valence-band-to-conduction-band transitions for semiconducting materials with band gap energies less than about $1.8\ \text{eV}$; these materials are **opaque**. Only a **portion** of the visible spectrum is absorbed by materials with band gaps between $1.8$ and $3.1\ \text{eV}$; consequently, these materials appear **coloured**.

Every nonmetallic material becomes opaque at some wavelength, which depends on the magnitude of its $E_g$: diamond, with a band gap of $5.6\ \text{eV}$, is opaque to radiation having wavelengths less than about $0.22\ \mu\text{m}$.

| Band gap $E_g$ | Visible light absorbed | Appearance | Example |
| --- | --- | --- | --- |
| $E_g$ above $3.1\ \text{eV}$ | None | Transparent, colourless (if pure) | Diamond ($5.6\ \text{eV}$) |
| $1.8$–$3.1\ \text{eV}$ | Part of the spectrum | Coloured | — |
| $E_g$ below $1.8\ \text{eV}$ | All of it | Opaque | Narrow-gap semiconductors |

> [!warning] The $3.1\ \text{eV}$ and $1.8\ \text{eV}$ thresholds are the visible-spectrum edges
> Both numbers come from the same equation, $\lambda = hc/E_g$, evaluated at the ends of the visible range: $3.1\ \text{eV}$ corresponds to about $0.40\ \mu\text{m}$ (violet) and $1.8\ \text{eV}$ to about $0.70\ \mu\text{m}$ (red). A material with $E_g$ just inside the window absorbs the violet end and transmits the rest, which is why it looks yellow or red — the *complement* of what it absorbs. Colour in a transparent dielectric is therefore an absorption-edge position, not a pigment.

> [!note] The transmission budget
> The fraction of incident light transmitted through a transparent material depends on the losses incurred by **absorption and reflection**, and the respective fractions depend on wavelength. For example, at $0.4\ \mu\text{m}$ a specimen may show $0.90T + 0.05A + 0.05R$, while at $0.55\ \mu\text{m}$ the same specimen shows $0.50T + 0.48A + 0.02R$. The reflected share is fixed by $n$ through $(1-R)^2$, the absorbed share by $\beta l$; only the second is a strong function of wavelength, so a colour change with thickness is an absorption effect.

> [!tip] Exam pointer — Dielectrics & Optical Properties
> Expect: why an insulator is a dielectric and the definition of $P$ as dipole moment per unit volume; $C = \varepsilon_0A/d$ and $C = \varepsilon_r\varepsilon_0A/d$ with the capacitance-measurement method for $\varepsilon_r$; the four mechanisms (electronic, ionic, orientation, space charge) with their origins, $T$ dependence and the strict speed ranking — electronic fastest, then ionic (heavier ions), then orientation (thermal randomization), then space charge (diffusion over interatomic distances) — and $P = P_e + P_i + P_o + P_s$; the CH₄/CH₃Cl comparison as the definition of a permanent dipole; ferroelectrics with BaTiO₃ above 2000 versus $<10$ for ordinary dielectrics, the ferro/paramagnetic analogy, spontaneous alignment and the mandatory piezoelectricity with its applications; the $120\,^\circ\text{C}$ Curie temperature, cubic → tetragonal, Ti off-centre with oxygen displacement, $c/a = 4.03/3.98 = 1.012$; metals opaque because of continuous empty states above $E_F$, absorption within $0.1\ \mu\text{m}$, opaqueness from radio to mid-UV, transparency to X- and $\gamma$-rays, reflectivity $0.90$–$0.95$, and colour as a reflected-spectrum deficit (Al/Ag silvery, Cu red-orange, Au yellow); refraction from electronic polarization with $n = c/v$, larger ions → larger $n$ → slower light (soda–lime 1.5, 90 wt.% PbO 2.1), isotropic for cubic/glass and anisotropic otherwise; the two absorption mechanisms, $h\nu \ge E_g$ and $\lambda \le hc/E_g$; the $3.1 / 1.8\ \text{eV}$ window and the transparent/coloured/opaque classification with diamond opaque below $0.22\ \mu\text{m}$; and $I_T = I_0(1-R)^2e^{-\beta l}$ with the $0.4\ \mu\text{m}$ and $0.55\ \mu\text{m}$ transmission budgets. The added depth to be ready with: why $\varepsilon_r$ is a function of frequency (relaxation of each mechanism), why colour is the complement of the absorbed band, and why the $c/a$ distortion of $1.012$ can control a dielectric constant of 2000.

---

## Formula Summary — Dielectrics & Optical Properties

| Quantity | Expression | Notes |
| --- | --- | --- |
| Capacitance, vacuum | $C = \varepsilon_0 A/d$ | $\varepsilon_0 = 8.85\times10^{-12}\ \text{F m}^{-1}$ |
| Capacitance, with dielectric | $C = \varepsilon_r \varepsilon_0 A/d$ | $\varepsilon_r \ge 1$; measured by comparing the two |
| Total polarization | $P = P_e + P_i + P_o + P_s$ | Sum of the four mechanisms |
| Electronic / ionic polarization | $P_e$, $P_i$ | Independent of $T$; ionic slower |
| Orientation polarization | $P_o$ | Falls as $T$ rises (thermal randomization) |
| Space charge polarization | $P_s$ | Slowest; interfacial/electrode charge |
| Index of refraction | $n = c/v$ | Larger ions → larger $n$ |
| Reflectance (normal incidence) | $R = \left(\dfrac{n-1}{n+1}\right)^2$ | Fresnel result read from $n$; silicate glass $\approx 0.05$ |
| Photon energy condition | $h\nu \ge E_g$ | Otherwise the photon passes |
| Absorption edge wavelength | $\lambda \le hc/E_g$ | $hc = 1.24\ \mu\text{m eV}$ |
| Visible window | $1.8\ \text{eV} < E_g < 3.1\ \text{eV}$ | Below → opaque; above → colourless |
| Transmitted intensity | $I_T = I_0(1-R)^2e^{-\beta l}$ | Same medium outside both faces |
| Ferroelectric Curie temperature | $T_C = 120\,^\circ\text{C}$ (BaTiO₃) | Cubic above, tetragonal below |
| Tetragonal distortion | $c/a = 4.03/3.98 = 1.012$ | Origin of the spontaneous dipole |

> [!note] Source images
> The schematic figures embedded in this block — the four polarization mechanisms (Fig. 1), the BaTiO₃ cubic and tetragonal cells (Fig. 2), the band structures of Cu and Mg and the photon absorption/re-emission mechanism (Figs. 3–4), the band-gap absorption event (Fig. 5) and the reflection/absorption/transmission schematic (Fig. 6) — are the original figures extracted from [[Dielectric materials_Polarization_Optical properties_Odd_2026-27.pdf]] and stored in `Material Science/images/` with the `DIE` prefix. The frequency ordering of the four mechanisms is discussed in §9.7 rather than drawn, because the slides give only the relative speeds.
