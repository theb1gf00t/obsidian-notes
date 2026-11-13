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

#### What a "mechanical property" actually is

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

#### Where the numbers come from — and why they matter

The chain of reasoning in materials engineering is *processing → structure → properties → performance*. Mechanical testing is the step that closes the loop: it converts microstructural reality (grain size, dislocation density, porosity, phase fractions) into the design numbers an engineer can use, and it lets a metallurgist work backwards from a failed part to the microstructural cause.

Three distinct uses of mechanical testing:

1. **Design** — provide *allowable stresses* (yield strength divided by a factor of safety) so a component can be sized.
2. **Quality control / acceptance** — check that a delivered batch meets specification (a hardness check on a forged shaft, a Charpy test on a pressure-vessel plate).
3. **Failure analysis and alloy development** — explain *why* a part broke, and rank candidate compositions/processes.

#### Failures that shaped the subject

Mechanical properties are studied because getting them wrong kills people. Three canonical cases, all of which recur in this topic:

- **Titanic (1912)** — hull steel with a high DBTT, in ice-cold water, under impact loading (see §2.7). The Charpy tests on recovered plate showed a transition temperature near the water temperature.
- **Liberty ships (1942–45)** — all-welded hulls of a steel with inadequate notch toughness; several broke in two at low temperature, some while at dock. The direct ancestor of modern fracture-toughness specifications.
- **Comet airliner (1954)** — fatigue cracks from square window corners, initiated by stress concentration and driven by repeated pressurisation cycles far below the yield stress (§1.5). The ancestor of damage-tolerance design.

> [!note] The design mindset
> A material is never chosen for a single number. Design asks: *is it stiff enough? strong enough? does it give warning before failing? does it stay tough at the service temperature? can it be made into the required shape?* Those five questions map exactly onto the five key design properties in §1.6.

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

#### The three responses compared

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

#### Each loading mode in mechanics terms

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

#### Hydrostatic stress — the loading that produces no yielding

If equal normal stresses act on all faces ($\sigma_{11}=\sigma_{22}=\sigma_{33}=-p$) with zero shear, the state is **hydrostatic compression**. Because plastic flow is driven by *shear*, and a hydrostatic state has no shear on any plane, it produces **no plastic deformation and no fracture** — it only changes volume elastically:

$$ \frac{\Delta V}{V} = -3(1-2\nu)\frac{p}{E} = -\frac{p}{K} $$

with $K$ the bulk modulus. This is why:
- a submarine hull, a deep-sea sphere or a specimen under a 10 kbar pressure cell does not "crush" plastically;
- the **triaxial tension** that builds up inside a neck or ahead of a notch *does* promote fracture, because it adds hydrostatic tension that opens cracks (this is the physical content of the Bridgman correction in §2.18 and of notch brittleness in §2.7);
- **superplastic forming** and **hydrostatic extrusion** can reach enormous strains — the superimposed pressure suppresses void growth and fracture.

#### Combined loading is the normal case

Real components see several modes at once: a rotating shaft carries bending + torsion + axial load; a tooth of a gear carries contact pressure + bending + sliding shear. Because the equations of elasticity are linear, the stresses from each load case **superpose**: add the tensors component by component, then compare the resulting multiaxial state with a yield criterion (von Mises or Tresca, §1.4) rather than with the uniaxial yield strength.

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

![[MP1 - Stress tensor at a point.png|420]]

*Figure — the nine stress components acting on an elemental cube; the three visible faces carry one normal stress each and two shear stresses each.*

#### Why nine components, and how they reduce

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

#### Strain as a tensor, and the two strain measures

The **strain tensor** is the symmetric part of the displacement gradient:

$$ \varepsilon_{ij} = \frac12\left(\frac{\partial u_i}{\partial x_j}+\frac{\partial u_j}{\partial x_i}\right) $$

Its diagonal terms are **normal strains** ($\Delta L/L_0$); the off-diagonal terms are the *tensor* shear strains, which are **half** the engineering shear strain: $\gamma_{xy} = 2\varepsilon_{xy}$. The factor of 2 is a constant source of error — the physical distortion of a square element is $\gamma = \Delta x/y_0 = \tan\theta \approx \theta$, and it is $\gamma$ that appears in $G$ and in the strain-energy expressions.

#### Counting the elastic constants

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

#### Units and magnitudes

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

#### What each test really delivers

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

#### The five properties, in engineering language

- **Stiffness** ($E$, or $G$) sets the *deflection* for a given load. It is a **design limit in its own right** — a bridge that sags 1 m has failed its serviceability requirement even if no metal has yielded. It cannot be changed by heat treatment; only by changing the material (or the section shape, which is a *geometry* fix, not a materials fix).
- **Strength** sets the *load* a part can carry. Design is normally based on **yield**, not fracture, because yield is a well-defined, reproducible, structure-insensitive-in-the-small quantity, and because a part that yields visibly gives warning.
- **Hardness** is a *localised* strength: resistance of the surface to being pushed in. It is the cheapest surrogate for strength and wear resistance.
- **Ductility** is the *warning system*: the amount of plastic strain before fracture. It is what allows a part to redistribute stress at a stress concentration, and it is what allows a material to be *formed* (rolled, drawn, bent, deep-drawn).
- **Toughness** is *energy absorbed before fracture*, i.e. strength **and** ductility together. A tough material resists the propagation of a crack. It is the property that decides whether a small manufacturing flaw becomes a catastrophic failure.

$$\text{Strength} \neq \text{Toughness} \neq \text{Hardness}$$

#### Typical values, for scale

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

#### Factor of safety

Design does not use the measured strength directly:

$$ \sigma_{\text{allowable}} = \frac{\sigma_y}{n}, \qquad n = 1.5\text{–}2 \text{ (normal service)},\ 2\text{–}4 \text{ (shock/fatigue)},\ 4\text{+ (pressure vessels, uncertain loads)} $$

The safety factor covers scatter in the material data, uncertainty in the load, stress concentrations not captured by the simple formula, and consequences of failure. It is a *legal and economic* choice as much as a technical one.

#### Stiffness vs strength trade-off, and specific properties

A material can be stiff but weak (glass), strong but compliant (some polymers), or both (steel). For **moving parts** the relevant quantities are the *specific* ones — property divided by density:

| Specific property | Expression | Winner |
| --- | --- | --- |
| Specific stiffness | $E/\rho$ | CFRP, ceramics, Al, Ti |
| Specific strength | $\sigma_y/\rho$ | CFRP, Ti alloys, Al-Li |
| Specific toughness | $K_{Ic}/\rho$ | Al alloys, steel |

This is the basis of **Ashby material-selection charts** (modulus–density, strength–density bubble charts): the material classes form clusters, and the selection lines are iso-performance lines of the form $E = C\rho$. Polymers lie bottom-left, metals in the middle, ceramics top-right (stiff, strong, but brittle), composites occupy the gap. The charts make the trade-offs in this table visible at a glance.

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

#### The length-scale ladder

| Scale | What exists there | What it controls |
| --- | --- | --- |
| Atomic ($10^{-10}$ m) | Bonds, potential well $U(r)$ | $E$, theoretical strength, melting point |
| Dislocation core ($10^{-9}$ m) | Peierls–Nabarro friction, core width | Yield stress, temperature dependence of strength |
| Dislocation substructure ($10^{-7}$–$10^{-6}$ m) | Pile-ups, cells, locks | Work hardening, $n$ |
| Grain ($10^{-5}$–$10^{-4}$ m) | Grain boundaries, orientation | Yield strength (Hall–Petch), ductility |
| Specimen ($10^{-3}$–$10^{-1}$ m) | Flaws, surface finish, constraint | Strength of brittle materials, DBTT |
| Component | Stress concentrations, residual stress | Fatigue life, fracture |

Each row explains a distinct part of a mechanical test. The atomic scale fixes the *slope* of the curve, the dislocation scale fixes *where the curve bends*, and the specimen scale fixes *where it ends*.

#### Mechanism → measurable signature

| Observation in a test | Underlying mechanism |
| --- | --- |
| Straight elastic line, slope = $E$ | Bond stretching; no defects involved |
| Yield at $\sim10^{-3}$–$10^{-4}G$ instead of $G/10$ | Dislocation glide, not rigid plane shear |
| Upper/lower yield point, Lüders plateau | Unpinning of dislocations from interstitial (C, N) atmospheres |
| Rising plastic branch (work hardening) | Dislocation multiplication, $t \propto b\sqrt{\rho}$, jog/lock formation |
| Strong temperature dependence of $\sigma_y$ in BCC | Peierls–Nabarro lattice friction, kink-pair nucleation |
| Weak temperature dependence in FCC | Obstacle-controlled glide, forest hardening |
| Yield stress $\propto d^{-1/2}$ | Grain-boundary barrier to slip (Hall–Petch) |
| Ductility limited in HCP | Only 3 basal slip systems $<5$ required by von Mises |
| Time-dependent strain at high $T$ | Dislocation climb + diffusional flow (creep) |
| No warning before failure | Crack propagation with negligible plastic zone (fatigue, cleavage) |

The key relationships that connect these scales (developed in §2):

$$ \tau_y \approx \tau_0 + \alpha G b\sqrt{\rho} \quad\text{(forest hardening)}, \qquad \sigma_y = \sigma_0 + k_y d^{-1/2}\ \text{(Hall–Petch)}, \qquad \tau \approx \frac{Gb}{2\pi L}\ \text{(Orowan, obstacle spacing } L\text{)} $$

So a single tensile test is really a *probe of defect populations*: two specimens of the same composition and different grain size give different yield stresses, different work-hardening rates and different ductilities, all from the same atoms and bonds.

### 1.8 Tensile test: first look

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

## 2. Mechanical Properties — II

### 2.1 Atomic model of elastic behaviour

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

#### Theoretical shear strength of a perfect crystal

If a perfect crystal were sheared, the shear stress would vary roughly sinusoidally with displacement, giving

$$ \tau_{\text{theoretical}} \approx \frac{G}{2\pi} \approx \frac{G}{6}\ \text{to}\ \frac{G}{30} $$

where $G$ is the shear modulus. Measured yield stresses are typically $10^{-3}$–$10^{-4}\,G$ — three to four orders of magnitude lower. **This discrepancy is the classic proof that plastic deformation occurs by the motion of dislocations, not by the simultaneous sliding of whole planes.**

The stress needed to move a dislocation through the lattice is the **Peierls–Nabarro stress**:

$$ \tau_{PN} = \frac{2G}{1-\nu}\,\exp\!\left(-\frac{2\pi w}{b}\right), \qquad w = \frac{d}{1-\nu} $$

where $b$ is the Burgers vector, $d$ the interplanar spacing and $w$ the width of the dislocation core.

- **Wide core** (metals — metallic bonding, non-directional) → exponential term small → **low Peierls stress** → easy glide, ductile.
- **Narrow core** (covalent/ionic ceramics) → **high Peierls stress** → hard, brittle.

#### The potential well, quantitatively

The two standard model potentials are the **Morse** potential (bonding, three parameters) and the **Lennard-Jones** potential:

$$ U(r) = 4\epsilon\left[\left(\frac{\sigma}{r}\right)^{12}-\left(\frac{\sigma}{r}\right)^{6}\right] $$

the $r^{-12}$ term being the Pauli/ion-core repulsion and the $r^{-6}$ term the van der Waals attraction. Expanding any such $U(r)$ about its minimum in a Taylor series gives

$$ U(r) \approx U(r_0) + \underbrace{\frac{dU}{dr}\Big|_{r_0}}_{=\,0}(r-r_0) + \frac12\frac{d^2U}{dr^2}\Big|_{r_0}(r-r_0)^2 + \cdots $$

The first non-zero term is **parabolic**, i.e. the force is *linear* in displacement:

$$ F = \frac{dU}{dr} \approx \left.\frac{d^2U}{dr^2}\right|_{r_0}(r-r_0) = k\,(r-r_0) $$

That is Hooke's law, derived from the shape of the potential well. The modulus of a solid is this bond stiffness multiplied by the number of bonds per unit area:

$$ E = \frac{k}{r_0}\ \propto\ \frac{1}{r_0}\left.\frac{d^2U}{dr^2}\right|_{r_0} $$

Three consequences, all directly examinable:

1. **$E$ scales with the depth and steepness of the well.** Deep wells (high melting point, high cohesive energy) → high $E$. A useful empirical correlation is $E \approx$ few hundred $\times$ melting temperature in K divided by molar volume, and in practice $\alpha = E/(k_BT_m)$ per atomic volume is roughly constant for crystals of a given bond type. Diamond has the deepest well of all and the highest modulus.
2. **$E$ decreases with temperature**, roughly linearly, by typically **2–5 % per 100 K**, because thermal expansion increases $r_0$ and the potential well becomes effectively shallower (anharmonicity). This is why the "room-temperature modulus" must be quoted with a temperature for high-temperature design.
3. **Elastic strain is small** because the parabola is only a good approximation for $|r-r_0| \ll r_0$. Real elastic strains are $\approx 0.1$–$1\,$% — only a small fraction of an interatomic spacing. Beyond that, the higher-order (anharmonic) terms dominate and the stress–strain relation becomes **non-linear**; rubber is the extreme case, where the "bonds" are chain conformations and enormous non-linear recoverable strains are the norm.

#### Theoretical cohesive (fracture) strength

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

#### The Peierls–Nabarro stress in physical terms

$$ \tau_{PN} = \frac{2G}{1-\nu}\exp\!\left(-\frac{2\pi w}{b}\right), \qquad w = \frac{d}{1-\nu} $$

The exponential is the whole story: the resistance falls off **exponentially with the width of the dislocation core** $w$, measured in units of $b$. A dislocation whose core is spread over many atomic spacings is "smeared out" and barely notices the discrete lattice; a dislocation squeezed into one atomic spacing feels every atom it passes.

- **Metals**: non-directional metallic bonding spreads the core over $w\sim2$–$5b$ → $\tau_{PN}$ is a small fraction of $G$ → easy glide even at low temperature. This is why FCC metals stay ductile to cryogenic temperatures.
- **Covalent/ionic solids**: directional, stiff bonds keep the core narrow → $\tau_{PN}$ is a large fraction of $G$ (approaching the theoretical shear strength) → the crystal prefers to *fracture* rather than to deform plastically. Diamond, SiC, sapphire and silicon are hard and brittle for exactly this reason, and they become *ductile* only above $\sim0.5T_m$ (silicon is brittle at room temperature despite being a semiconductor; silicon is used as a "brittle" material in MEMS for the same reason).
- **BCC metals sit in between**: their screw dislocation cores are *non-planar*, spread over three intersecting $\{110\}$ planes, which gives a high and strongly **temperature-dependent** Peierls stress. This is the origin of the sharp yield drop, the strong temperature dependence of $\sigma_y$ in iron, and the **DBTT** (§2.7). It also explains why BCC metals are strong at low temperature (high $\tau_{PN}$) but why that strength is useless — they fracture before yielding.
- **Motion of a dislocation past the Peierls barrier requires kink-pair nucleation**: the dislocation advances by forming a pair of kinks on its line, each kink being a short segment that has already crossed the barrier. The activation energy for kink-pair formation sets the temperature dependence of the yield stress, giving the characteristic $\ln(1/T)$ behaviour seen in BCC metals.

![[MP1 - Slipped and unslipped regions of a crystal.png|460]]

*Figure — a dislocation as the boundary between a slipped and an unslipped region of the crystal: the "interfacial region" is the dislocation core, of width $w$, and the lattice above and below it is perfect except for the elastic distortion around the core.*

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

![[MP2 - Slip and twinning sequence.png|420]]

*Figure — (a) before deformation; (b) after slip, the upper block is displaced by a whole number of lattice spacings and the surface shows a step; (c) after twinning, each plane is displaced by a fraction of a spacing, producing a mirror-image (twinned) region.*

#### Slip in more detail

- Slip is **quantised**: the offset at the surface is a whole number of Burgers vectors, $n b$, because every dislocation that emerges leaves a step of height $b$. A visible **slip line** on an electropolished surface is not one dislocation but a **slip band** containing hundreds of dislocations.
- Slip is *not* a simultaneous rigid sliding of two half-crystals. It proceeds by the nucleation, glide and escape of dislocations; the surfaces of the slipped region remain perfect, and the crystal orientation on both sides of the slip plane is unchanged.
- Slip is **conservative** (no atoms added or removed) and **athermal in principle** for FCC metals — it needs only the Peierls stress to be exceeded, plus the stress to bypass obstacles. It is therefore possible at absolute zero (given enough stress).
- Because slip repeats indefinitely on the same system, it can produce **arbitrarily large strains**; this is why metals can be rolled to 99 % reduction in thickness.

#### Twinning in more detail

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

### 2.3 Slip systems

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

#### Why the close-packed plane and the close-packed direction win

Slip requires the *smallest possible disturbance of the lattice*, and both choices reduce it:

- **Close-packed direction**: the shortest lattice translation, i.e. the shortest Burgers vector $b$. Since the elastic energy of a dislocation is $\propto b^2$, this is the lowest-energy dislocation, and the offset produced per dislocation is smallest.
- **Close-packed plane**: the largest interplanar spacing $d$. The shear stress needed to slide the planes is roughly $\propto 1/d$ (fewer bonds per unit area to break), the Peierls stress falls exponentially with $d$ (through $w = d/(1-\nu)$), and the atomic "corrugation" felt by the moving dislocation is smallest.
- A **slip system** must combine both: $\{111\}$ with $\langle110\rangle$ in FCC, for instance, because the $\langle110\rangle$ direction lies *in* the $\{111\}$ plane.

#### Stacking faults, partials and the width of the core

In FCC, the perfect dislocation $\tfrac{a}{2}\langle110\rangle$ can lower its energy by dissociating into two **Shockley partials** joined by a strip of **stacking fault**:

$$ \frac{a}{2}[10\bar1] \longrightarrow \frac{a}{6}[2\bar1\bar1] + \frac{a}{6}[\bar12\bar1] $$

The balance between the repulsion of the partials and the fault energy $\gamma_{SF}$ sets the **separation** of the partials, and hence the *effective width* of the dislocation core. This single quantity controls a surprising amount of behaviour:

| Stacking-fault energy | Fault ribbon | Glide style | Behaviour | Examples |
| --- | --- | --- | --- | --- |
| **High** ($\gamma_{SF}\gtrsim100$ mJ/m²) | Narrow, partials close | Wavy, easy **cross-slip** | Low work-hardening rate, high ductility, good for forming | Al, Cu-Zn with low Zn, Ni |
| **Low** ($\gamma_{SF}\lesssim25$ mJ/m²) | Wide | **Planar** glide, cross-slip difficult | High work-hardening rate, high strength, more twinning, "springy" | 70/30 brass, 304 stainless steel, Cu-Al |

This is why **brass work-hardens so much faster than aluminium** even though both are FCC, and why austenitic stainless steels are both strong and highly ductile (they work-harden and twin). It also explains why cross-slip (needed for dislocations to bypass obstacles and for dynamic recovery) is temperature-dependent: at high temperature the partials recombine thermally and cross-slip becomes easy, which is the basis of Stage III hardening and of recovery.

#### Special cases

- **BCC** slip is on $\{110\}$, $\{112\}$ and $\{123\}$ depending on temperature and stress state, always in $\langle111\rangle$. This "pencil glide" gives many *geometrically* possible systems, but the highly stressed non-planar screw core makes the CRSS strongly temperature-dependent. Result: BCC metals are strong but brittle at low $T$, ductile at high $T$.
- **HCP** metals have only 3 basal systems (one plane $\times$ three directions), which by itself cannot satisfy von Mises. Ductility is rescued by (i) prismatic $\{10\bar10\}\langle11\bar20\rangle$ slip, (ii) pyramidal $\langle c+a\rangle$ slip with $b$ out of the basal plane (5 independent systems), and (iii) twinning, which reorients grains so that new systems become favourable. When these are all hard — as in Mg at room temperature, or Zn and Cd — the metal is brittle in polycrystalline form. Adding lithium to magnesium, or raising the temperature, activates $\langle c+a\rangle$ slip and restores ductility.
- **Ionic crystals (NaCl, MgO, LiF)**: slip on $\{110\}\langle110\rangle$ keeps like-charged ions from approaching each other across the slip plane; $\{111\}$ slip would put $\text{Na}^+$ next to $\text{Na}^+$ and is electrostatically forbidden. Cubic ionic crystals are therefore *less* ductile than their 6 independent systems suggest.
- **Covalently bonded crystals** (Si, Ge, diamond, SiC): $\{111\}\langle110\rangle$ slip is *geometrically* available, but the enormous Peierls stress means slip needs $T\gtrsim0.5T_m$. At room temperature they are brittle despite having 12 slip systems — a sharp reminder that **the number of slip systems is necessary but not sufficient for ductility; the CRSS must also be low enough.**
- **Ordered alloys/intermetallics** (Ni$_3$Al, TiAl, FeAl): slip of a single dislocation destroys the ordered arrangement and creates an antiphase boundary, so dislocations must move as **superdislocations** with $b = a\langle110\rangle$ (twice as long, four times the energy), or in coupled pairs. This, plus the limited number of independent systems, is why intermetallics are strong at high temperature but brittle at room temperature.

> [!note] Von Mises criterion — why exactly five?
> A general deformation of a polycrystal requires an arbitrary *shape change at constant volume*. The strain tensor has 6 independent components; the constant-volume constraint removes 1, leaving **5 independent strain components**. Each independent slip system can supply only one, so at least 5 are needed for the *grain* to conform to its neighbours. With fewer, grain boundaries must crack or slide → low ductility. (Grain-boundary sliding and diffusional flow can relax this requirement, which is why fine-grained HCP metals at high temperature are more ductile.)

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

![[MP2 - Schmid factor geometry.png|420]]

*Figure — the tensile axis at angles $\phi_1$ (to the slip-plane normal) and $\phi_2$ (to the slip direction); the resolved shear stress is $\tau = \sigma\cos\phi_1\cos\phi_2$.*

#### The same result in tensor form

The resolved shear stress is the projection of the stress tensor onto the slip plane and the slip direction:

$$ \tau_R = \sigma_{ij}\,b_i\,n_j \quad\text{(per unit } b\text{)} \qquad\text{so}\qquad m = b_i n_j / b $$

where $\mathbf{n}$ is the slip-plane normal and $\mathbf{b}$ the unit slip direction. This **Schmid tensor** form is what finite-element crystal-plasticity codes use, and it makes two facts obvious:

- The Schmid factor depends only on the **relative orientation** of the stress axis, plane normal and slip direction — not on the material.
- For a *general* stress state, each of the 12 systems of an FCC crystal has its own $m$; the active one is whichever maximises $\tau_R$ for that stress state.

#### Worked example (typical exam question)

> A copper single crystal is loaded in tension along $[123]$. The primary slip system is $(111)[01\bar1]$. Find the Schmid factor and the yield stress if $\tau_{CRSS} = 0.8$ MPa.

1. Normalise the axis: $\mathbf{t} = [123]/\sqrt{14} = (0.267,\,0.535,\,0.802)$.
2. Plane normal: $\mathbf{n} = [111]/\sqrt3 = (0.577,\,0.577,\,0.577)$.
3. Slip direction: $\mathbf{b} = [01\bar1]/\sqrt2 = (0,\,0.707,\,-0.707)$.
4. $\cos\phi_1 = \mathbf{t}\cdot\mathbf{n} = (0.267+0.535+0.802)(0.577) = 0.926$.
5. $\cos\phi_2 = \mathbf{t}\cdot\mathbf{b} = (0.535-0.802)(0.707) = -0.189$ (sign irrelevant for a shear component; take $+0.189$).
6. $m = 0.926 \times 0.189 = 0.175$.
7. $\sigma_y = \tau_{CRSS}/m = 0.8/0.175 \approx 4.6$ MPa.

Note how *small* the yield stress is: a nearly-perfect copper crystal yields at a few MPa, whereas polycrystalline copper yields at $\sim70$ MPa. That factor of $\sim15$ is the combined effect of orientation averaging (Taylor factor $\sim$3), grain boundaries, and the initial dislocation density.

#### Orientation dependence: the "soft" and "hard" orientations

Because $\sigma_y = \tau_{CRSS}/m$, a single crystal's yield stress varies with orientation by a factor of $\infty$ in principle and by roughly $2$–$3$ in practice over the orientations that can actually be tested. Two features of the classic single-crystal data:

- **Multiple slip near $m=0.5$**: when the axis is at $45^\circ$ to both plane and direction, *several* systems simultaneously reach $m\approx0.5$ (there are 8 systems with $m=0.5$ for the $\langle100\rangle$ axis, 6 for $\langle110\rangle$, 6 for $\langle111\rangle$... in fact the number depends on the axis). The crystal then deforms by multiple slip, work-hardens very rapidly, and the load–extension curve shows a sharp "corner". This is why the Schmid law holds well in the "single-slip" orientations and breaks down near high-symmetry axes.
- **Latent hardening**: slip on the primary system hardens the *latent* (inactive) systems even more than itself. This violates the assumption that CRSS is a constant, and it is the reason real crystals show a higher flow stress than the simple Schmid prediction after a few percent strain.

#### From single crystal to polycrystal: the Taylor factor

In a polycrystal, grains are randomly oriented and each must accommodate the shape change of its neighbours (von Mises: 5 systems). Averaging the Schmid factors over all orientations and all active systems gives the **Taylor factor**

$$ M = \frac{\sigma_y}{\tau_{CRSS}} \approx 3.06\ \text{(FCC, random texture)}, \qquad M\approx2.75\ \text{(BCC)} $$

- $M$ is a *geometric* factor (it is the reciprocal of the average Schmid factor), so it changes with **texture**: a strong $\langle111\rangle$ fibre texture (drawn wire, rolled sheet) raises $M$ and therefore the strength.
- The same idea explains why **polycrystals are stronger than single crystals**: not only orientation averaging but also grain-boundary constraint (each grain is prevented from deforming freely by its neighbours), which adds the Hall–Petch term.
- Conversely, a **single crystal of a superalloy** (turbine blade) is *weaker* per unit CRSS but has no grain boundaries to slide or crack, so it has far better creep and fatigue resistance — which is why blades are directionally solidified or single-crystal.

### 2.5 Dislocation reactions and sessile (Lomer) locks

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

#### Frank's rule — the general criterion

A reaction $\mathbf{b}_1+\mathbf{b}_2 \to \mathbf{b}_3$ is energetically favourable if the elastic energy per unit length falls. Since $E_{el}\approx\alpha G b^2$ (with $\alpha\approx0.5$–$1$),

$$ \boxed{\ b_3^2 < b_1^2 + b_2^2\ } \qquad\text{and}\qquad \mathbf{b}_3 = \mathbf{b}_1+\mathbf{b}_2\ \text{(Burgers vector conservation)} $$

Both conditions must hold: **conservation of the Burgers vector** (it is a topological charge — the closure failure of a Burgers circuit — and cannot be created or destroyed at a node) and **reduction of energy**. The reaction above reduces $b^2$ from $a^2$ to $a^2/2$: a **50 %** drop. (If the product had $b_3^2 > b_1^2+b_2^2$ the dislocations would *repel*; if equal, the reaction is neutral.)

Two useful corollaries:

- **Two dislocations with the same $\mathbf{b}$ repel** each other (a reaction to $2\mathbf{b}$ would quadruple the energy) — hence dislocations arrange themselves into low-energy arrays (tilt and twist boundaries, cells).
- **A dislocation can dissociate** (as in the Shockley partial reaction of §2.3) if the partials' energy sum is lower than the perfect dislocation's — this is why stacking faults exist at all.

#### Types of sessile obstacle

| Obstacle | What it is | How it is overcome |
| --- | --- | --- |
| **Lomer (Lomer–Cottrell) lock** | Product of a reaction between dislocations on intersecting planes; $\mathbf{b}$ not in a slip plane | Cannot glide at all; requires climb (high $T$) or very high stress to recombine |
| **Cottrell atmosphere** | Solute/interstitial cloud pinning a dislocation (C, N in Fe) | Thermally activated unpinning → sharp yield point (§2.11) |
| **Precipitate particle** | Second-phase particle in the glide plane | **Shearing** (if coherent and small) or **Orowan looping** (if hard) |
| **Grain boundary / twin boundary** | Change of orientation | Slip transfer to the next grain; pile-up stress concentration |
| **Jog / forest dislocation** | Dislocation threading the glide plane | Thermal activation; jog dragging (also generates point defects) |
| **Surface oxide / coating** | Hard film | Cracking of the film; nucleation site for fatigue cracks |

#### Pile-ups, stress concentration and the Hall–Petch relation

A pile-up of $n$ dislocations blocked at an obstacle multiplies the applied stress at the head of the pile-up by roughly $n$:

$$ \tau_{\text{head}} \approx n\,\tau_{\text{applied}}, \qquad n \approx \frac{\pi\,\tau_{\text{applied}}\,L}{Gb} $$

where $L$ is the pile-up length (≈ the grain radius). Yielding of the *next* grain begins when $\tau_{\text{head}}$ reaches its CRSS, $\tau^{*}$. Setting $\tau_{\text{head}}=\tau^{*}$ and $L = d/2$ gives

$$ \tau_{\text{applied}} \approx \sqrt{\frac{2Gb\,\tau^{*}}{\pi d}} \quad\Longrightarrow\quad \sigma_y = \sigma_0 + k_y d^{-1/2} $$

which is precisely the **Hall–Petch equation**. The same pile-up stress concentration, applied to a *crack* instead of a grain boundary, is the mechanism by which a slip band nucleates a cleavage crack — the link between plasticity and brittle fracture in §2.7.

> [!note] Why work hardening has three stages
> - **Stage I (easy glide)** — single slip on the primary system, long free path, low hardening rate. Dominant in single crystals oriented for single slip.
> - **Stage II (linear hardening)** — multiple slip begins; Lomer locks and forest dislocations form; hardening rate is high and nearly constant ($\theta\approx G/200$).
> - **Stage III (parabolic/dynamic recovery)** — cross-slip lets dislocations bypass obstacles, so the hardening rate falls; in polycrystals, Stage II–III behaviour is what appears as the "rising plastic branch" of the tensile curve.

### 2.6 The tensile test: specimen, machine, curve

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

#### Specimen geometry and why it is standardised

- The standard round specimen has gauge diameter $d_0 = 12.8$ mm (0.505 in.) and gauge length $L_0 = 50$ mm (2 in.), i.e. $L_0 = 4d_0$; the **proportional** designation is $L_0 = 5.65\sqrt{S_0}$ (ISO), where $S_0$ is the original cross-sectional area. Flat specimens are used for sheet, with the same proportional relation.
- The **reduced section** guarantees that the stress is highest in the gauge, so the specimen yields and breaks where the extensometer is attached, not in the grips. The **fillet radius** between gauge and grip reduces the stress concentration there; too small a fillet causes grip-end failures (a classic bad-data signature).
- Because **% elongation depends on gauge length** (the neck contributes a fixed extra length, so a shorter gauge gives a larger %EL), $L_0$ must always be quoted with the ductility value. % reduction in area, measured at the neck, does not have this problem.

#### The machine and the measurement chain

| Element | Function | Practical point |
| --- | --- | --- |
| **Load cell** | Converts force to an electrical signal | Must be calibrated; range chosen so the test is in the top 10–90 % of capacity for accuracy |
| **Extensometer** | Measures strain directly on the gauge (clip gauge, strain-gauge or optical) | Should be removed before fracture to avoid damage; machine crosshead displacement includes machine compliance and is *not* the specimen strain |
| **Crosshead** | Applies displacement at controlled rate | Quoted as **strain rate** ($10^{-5}$–$10^{-1}\ \text{s}^{-1}$ for quasi-static tests); faster rates raise the measured strength, especially in polymers and BCC metals |
| **Grips** | Transmit load without slipping or bending | Wedge, collet or shoulder grips; misalignment produces bending and premature failure |
| **Data acquisition** | Records load–displacement pairs | The raw curve is corrected for machine compliance and for the extensometer's own stiffness before $E$ is computed |

#### Lüders bands and the yield-point phenomenon

The upper and lower yield points are not a curiosity — they are the visible signature of **solute pinning**:

1. In annealed low-carbon steel, carbon and nitrogen atoms segregate to dislocations (**Cottrell atmospheres**) because the solute is smaller/larger than the host atom and relieves elastic strain by sitting in the dislocation's stress field.
2. To move such a dislocation, it must be **torn away** from its atmosphere — this requires a stress peak (the upper yield point).
3. Once free, dislocations multiply rapidly and glide at a lower stress (the lower yield point). The plastic zone spreads as a **Lüders band** — a visible band of roughened surface that sweeps along the gauge, giving the flat plateau.
4. The band's propagation ends when the whole gauge has yielded; work hardening then takes over.

Consequences: the sharp yield point causes **stretcher strains** (flamboyant markings) in deep-drawn sheet, which is why sheet is **temper-rolled** (skin-passed) to remove it. It also means the yield stress of such a steel depends on the specimen's history, not only on composition.

> [!warning] Common exam trap
> The slope of the *engineering* stress–strain curve in the elastic region equals $E$ only if the displacement used is the *specimen's* elongation. Many textbook problems give load–extension data from a machine; you must convert using the gauge length and area, not the full specimen length.

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

![[MP2 - Iron curves at three temperatures.png|440]]

*Figure — the same material (iron) tested at $-200$, $-100$ and $25\ ^\circ\text{C}$: the low-temperature curve is almost linear to fracture; the room-temperature curve shows a long plastic region and a neck.*

![[MP2 - Yoffee diagram.png|380]]

*Figure — the Yoffee diagram: yield stress falls with temperature, cleavage fracture stress is nearly temperature-independent, and the intersection defines the DBTT.*

![[MP2 - Materials for low temperature service.png|520]]

*Figure — service limits of engineering alloys at low temperature: BCC carbon and low-alloy steels stop at moderate $T$, nickel steels extend lower, and FCC aluminium, nickel, titanium and austenitic stainless alloys reach liquid-helium temperature.*

#### The physics behind the two curves

Why does the yield stress fall with temperature while the fracture stress does not?

- **Yield stress is thermally activated.** Dislocation motion past obstacles (Peierls barriers, solute atoms, forest dislocations) needs a *combination* of applied stress and thermal energy. At low temperature there is little thermal energy, so a higher applied stress is needed; as $T$ rises, the thermal contribution grows and $\sigma_y$ falls. The effect is strongest in BCC metals because their non-planar screw cores give a large Peierls barrier (§2.1), and weak in FCC metals where the Peierls barrier is small.
- **Cleavage fracture stress is essentially athermal.** Breaking bonds across a plane does not need diffusion or thermal activation; the stress at which a pre-existing microcrack propagates depends on the crack size and on the surface energy, both nearly independent of temperature. It is a *stress-controlled* event, so it plots as a nearly horizontal line.
- **Where they cross** is the DBTT. Below it, the material reaches the cleavage stress *before* it can generate the plastic flow needed to blunt the crack → brittle. Above it, it yields first, the plastic zone blunts the crack tip, and the material is ductile.

#### Why a notch and a high strain rate shift the transition up

- A **notch** creates a triaxial stress state: the axial stress is raised by a factor $\sim$2–3 relative to the von Mises equivalent stress, while the *shear* stress that drives slip is unchanged. So the local tensile stress reaches the cleavage stress while the shear stress is still below the CRSS — fracture wins. This is why brittle behaviour is always associated with **constraint** (thick sections, notches, welds, sharp corners).
- A **high strain rate** (impact) leaves less time for thermal activation, so $\sigma_y$ rises, while the fracture stress does not — the yield curve is effectively shifted up, moving the intersection to a higher temperature.
- **Grain size** affects the two curves differently: Hall–Petch raises $\sigma_y$ (strengthening, raising DBTT) but a finer grain size also reduces the size of the *microcrack* formed by a slip-band pile-up, and the cleavage stress scales as $d^{-1/2}$ — a finer grain size improves both strength and toughness. That is why grain refinement is the only strengthening mechanism that *lowers* the DBTT.
- **Chemistry**: C, P, S, Sn, Sb, As raise the DBTT (segregation to grain boundaries weakens them, and P/Sn cause **temper embrittlement**); Ni lowers it. **Hydrogen** causes severe embrittlement at room temperature; **neutron irradiation** raises the DBTT by producing hardening and Cu-rich precipitates (a life-limiting issue for reactor pressure vessels).
- **Thickness**: a thick section cannot relax the through-thickness stress by yielding at the free surfaces, so constraint is high — large sections are more brittle than thin ones, an uncomfortable fact for scaling.

#### The Charpy transition curve

Plotting absorbed energy against test temperature gives an S-shaped curve with three regions: **lower shelf** (low energy, pure cleavage, brittle), **transition** (steeply rising, mixed cleavage + ductile tearing), and **upper shelf** (high energy, fully ductile, fibrous). The DBTT is conventionally defined by a fixed energy level (**27 J** for ship steels), a fixed lateral expansion, or 50 % shear appearance. Because the transition region is very steep, a small temperature error causes a large energy error — hence the emphasis on temperature control and on reporting the *criterion* alongside the number.

Historical note: the **Liberty ship** fractures occurred at hatch corners (stress concentration) in welded (no crack-arresting riveted seams) hulls at low temperature, and are the reason impact-testing requirements entered ship-classification rules.

> [!note] Practical consequence for design codes
> Pressure-vessel and ship codes require the steel's DBTT (measured by Charpy) to lie below the minimum service temperature by a margin. Where that cannot be guaranteed — very low temperature, very thick section, or hydrogen service — the material is changed to an FCC alloy (austenitic stainless, aluminium, nickel alloy), which has no such transition.

### 2.8 Properties obtained from the tensile test

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

### 2.9 Anelasticity and viscoelasticity

- In real materials, part of the elastic strain is **time-dependent**: deformation continues slowly *after* the stress is applied, and on unloading some finite time is needed for complete recovery. This is **anelasticity**.
- Its origin is time-dependent microscopic/atomistic processes accompanying the deformation (e.g. stress-induced ordering of solute atoms, grain-boundary relaxation).
- In **metals** the anelastic component is small and usually neglected. In **polymers** it is large; the behaviour is then called **viscoelastic** (rubber-like).
- Idealised responses: **elastic** (instant strain, instant recovery), **viscous** (strain grows linearly with time under constant load, permanent), and **viscoelastic** (intermediate — retarded elastic strain plus permanent flow).

![[MP2 - Anelasticity elastic viscous viscoelastic.png|420]]

*Figure — the standard four-panel comparison: load–time cycle (top) against strain–time response (bottom) for (a) elastic, (b) anelastic/viscoelastic, (c) viscous and (d) elastomeric behaviour.*

#### Anelasticity in metals: small but not always negligible

- The anelastic strain is typically $\sim0.1$ % of the elastic strain at room temperature, so it is ignored for stiffness calculations. But it is the basis of **internal-friction (damping) measurements**, which are exquisitely sensitive to point defects:
  - the **Snoek effect** — interstitial C/N pairs in BCC iron reorient under stress, giving a damping peak whose height measures the interstitial content (a non-destructive chemical analysis);
  - the **Zener (thermoelastic) peak** — heat flow between differently strained regions of a polycrystal;
  - **grain-boundary relaxation** — sliding of boundaries accommodated by diffusion, appearing at high temperature and low frequency.
- Anelasticity is why a *precisely* sized part (a quartz oscillator, a tuning fork, a precision spring) is chosen for low damping, and why high-damping alloys (Mn-Cu, cast iron) are chosen to suppress vibration and noise.

#### Viscoelasticity in polymers: the same physics writ large

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

### 2.10 Poisson's ratio

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

#### Deriving the relations between the four elastic constants

For an isotropic solid only **two** constants are independent; the other two follow from them. Starting from the definition of $\nu$ and requiring that a hydrostatic pressure produce only a volume change:

$$ G = \frac{E}{2(1+\nu)}, \qquad K = \frac{E}{3(1-2\nu)}, \qquad \lambda = \frac{E\nu}{(1+\nu)(1-2\nu)} $$

The bulk modulus expression shows the meaning of the $0.5$ limit: as $\nu\to0.5$, $K\to\infty$ — the material becomes **incompressible**, which is exactly what a rubber is (its bulk modulus is $\sim$2 GPa while its shear modulus is $\sim$1 MPa, a ratio of $10^3$).

#### Volume change under uniaxial tension

$$ \frac{\Delta V}{V} = \varepsilon_z(1-2\nu) = \frac{\sigma}{E}(1-2\nu) $$

So for $\nu = 0.3$ a tensile strain of 0.3 % produces a volume increase of only $0.12$ %, and for $\nu=0.5$ the volume is unchanged. This is the basis of the **constant-volume assumption** used in plasticity (§2.16): plastic deformation proceeds by shear, which does not change volume, so $A_0l_0=A_il_i$.

#### Values, limits and the exotic cases

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

### 2.11 Yield stress and tensile strength

- **Yield strength** is the stress at which plastic deformation begins. Because the elastic-to-plastic transition is gradual for most metals, it is defined by the **0.2 % offset** construction: draw a line parallel to the elastic portion, starting at $\varepsilon = 0.002$; its intersection with the curve is $\sigma_y$.
- **Tensile strength (UTS)** is the maximum stress on the engineering curve; it marks the **onset of necking** and the end of uniform deformation.
- Above the UTS, deformation is **localised** — the curve descends, but this does not mean the material is softening (see true stress, §2.16).

![[MP2 - 0.2 percent offset yield strength.png|440]]

*Figure — the 0.2 % offset construction (left) and the upper/lower yield points of a low-carbon steel with the 0.2 % offset yield strength marked on the same curve (right).*

#### The offset construction, precisely

1. Draw the elastic line through the origin with slope $E$.
2. Draw a line parallel to it, offset by $\varepsilon = 0.002$ (0.2 %) on the strain axis.
3. The intersection of this line with the stress–strain curve is $\sigma_y$ — the stress at which the material has accumulated 0.2 % **plastic** strain.

The offset is 0.2 % because it is just at the resolution of a good extensometer and small enough to be a sensible "engineering yield"; for polymers 2 % or 1 % offsets are used because their transitions are much broader; for materials with a sharp yield point, the upper or lower yield point is used directly (with the convention stated).

**Why an offset at all?** Most metals do not show a sharp break in slope: the transition from elastic to plastic is gradual as individual grains with favourable orientations yield one by one. A convention is therefore needed, and 0.2 % is internationally agreed.

#### Factors that move the yield strength

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

#### Tensile strength: what it does and does not mean

- $\sigma_{UTS}$ is the **maximum engineering stress**, and its significance is *geometric*: it marks the point where the rate of work hardening exactly balances the rate of area reduction (Considère condition, §2.15). It is not a "breaking stress" — the stress at fracture is *lower* on the engineering curve.
- It is nevertheless the most-quoted strength number because it is easy to measure, reproducible, and it correlates with hardness and with fatigue strength. It is used for **specifications and quality control** and for estimating working loads in forming operations.
- **Design is based on yield, not UTS**, because at the UTS the material has already deformed by many percent; a component at UTS is already unserviceable. The ratio $\sigma_{UTS}/\sigma_y$ is the **strain-hardening capacity**, a measure of the safety margin between first yield and final failure.
- For **brittle materials** there is no yield, so the "strength" quoted is the fracture stress (flexural strength for ceramics, §3.1). For **polymers**, the "yield point" may be a maximum followed by **strain softening** (necking and cold drawing), so the curve shape needs care in interpretation.

> [!note] Tension–compression asymmetry
> Some materials yield at different stresses in tension and compression — cast iron, many polymers, glasses and geological materials. For polymers and foams this is a real effect (chain tension vs buckling of struts); for metals it is usually small. It matters because a "yield strength" measured in tension may not apply in a compressive design, and because bending, which has both, produces a shifted neutral axis.

### 2.12 Resilience and toughness

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

#### Resilience in detail

The area of the elastic triangle is

$$ U_r = \frac12\sigma_y\varepsilon_y = \frac{\sigma_y^2}{2E} \qquad [\text{J/m}^3] $$

This is the **modulus of resilience**; the *proof resilience* is the same quantity multiplied by the volume of the part (total energy stored, in J). Design implications:

- **Springs** should be made of high-yield, low-modulus material — hence spring steels (high $\sigma_y$) or, for non-metallic springs, polymers/composites (low $E$).
- Because $U_r\propto\sigma_y^2$, doubling the yield strength *quadruples* the energy stored — a far stronger lever than any change in modulus.
- Resilience is the relevant property for anything that must "bounce back" without permanent set: leaf springs, snap-fits, diaphragms, buffer springs, and the elastic range of a golf ball.

#### Toughness in detail — three different quantities share the name

| "Toughness" | Symbol / units | Definition | When used |
| --- | --- | --- | --- |
| **Modulus of toughness** | $U_t$, J/m³ | Area under the *whole* $\sigma$–$\varepsilon$ curve to fracture | Comparing materials, crash energy absorption per volume |
| **Impact (notch) toughness** | J (or J/cm²) | Energy absorbed by a standard notched specimen in Charpy/Izod | Specification and DBTT determination (§2.7) |
| **Fracture toughness** | $K_{Ic}$, MPa·m$^{1/2}$ (or $G_{Ic}$, J/m²) | Resistance to propagation of a pre-existing sharp crack | Damage-tolerant design, fitness-for-service assessment |

The last of these is the one used in modern design codes, because the first two do not account for the *size* of the flaw. The relationship between them is

$$ K_{Ic} = Y\sigma\sqrt{\pi a} $$

where $a$ is the crack length and $Y$ a geometry factor of order 1. It says the *stress* a cracked body can carry falls as $1/\sqrt{a}$: doubling the crack length halves the allowable stress. This is the single most important equation behind "damage tolerance" design in aircraft and pressure vessels, and it explains why the same steel can be tough in a small specimen and brittle in a large structure.

Typical magnitudes:

| Material | $U_r$ (kJ/m³) | Modulus of toughness (MJ/m³) | $K_{Ic}$ (MPa·m$^{1/2}$) |
| --- | --- | --- | --- |
| Mild steel | 150 | 80–120 | 100–150 |
| 4340 QT (high strength) | 5000 | 5–10 | 40–60 |
| Aluminium 2024-T3 | 550 | 20–30 | 30–40 |
| Alumina | 20 | 0.02 | 3–4 |
| Glass | 1 | 0.005 | 0.7–1 |
| PMMA | 100 | 0.3 | 1–1.5 |
| HDPE | 20 | 10–30 | 2–4 |

Note the pattern: **high-strength materials have high resilience but low toughness**. Strength and toughness pull in opposite directions because both cannot be maximised by the same microstructure.

### 2.13 Tensile curves for polymers

Three characteristic shapes:

- **Brittle** — linear elastic to a sudden break, very small strain (PMMA, PS at room temperature).
- **Plastic** — yield, then cold drawing with a long plateau, then strain hardening and fracture (many thermoplastics).
- **Elastomeric** — highly elastic: enormous recoverable strain (several hundred %), low modulus, no permanent set (rubbers/vulcanised elastomers).

![[MP2 - Polymer tensile curves.png|440]]

*Figure — the three characteristic polymer curves: brittle (PMMA/PS), plastic with cold drawing (many thermoplastics) and elastomeric (rubber).*

![[MP2 - Polymer tensile curve annotated.png|400]]

*Figure — the annotated plastic-type polymer curve: Young's modulus from the initial slope, the yield point (upper yield), the drop into cold drawing, the draw ratio, and the tensile strength at break.*

#### What each shape means physically

- **Brittle** (PMMA, PS, epoxy at room temperature) — below the glass transition temperature $T_g$ the chains are frozen; the material behaves like a stiff glass. Failure is by **crazing** (micro-cavitation ahead of the crack) followed by crack growth; the fracture surface is mirror-smooth near the origin with **hackle** markings further out. Strain to failure is a few percent.
- **Plastic** (HDPE, PP, PET, nylon, PC) — above $T_g$ but below $T_m$ (or in a semicrystalline polymer), chains can slide past one another. The curve shows a **yield maximum**, then a drop (strain softening) as a neck forms, then a long **cold-drawing plateau** at nearly constant stress while the neck propagates, and finally **strain hardening** as the chains become aligned, followed by fracture.
- **Elastomeric** (natural rubber, silicone, vulcanised EPDM) — lightly cross-linked chains above $T_g$. Deformation uncoils the chains, which is an **entropy** effect: the chain wants to return to a random coil, so the restoring force *increases* with extension (the curve rises steeply at high strain). Modulus is very low (1–10 MPa), failure strain huge (300–800 %), and recovery essentially complete. The energy lost per cycle (hysteresis) makes rubber a good damper.

#### The strong dependence on temperature and rate

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

### 2.14 Measures of strength and ductility

$$ \sigma = \frac{F}{A_0} \qquad\qquad \varepsilon = \frac{l_i - l_0}{l_0} $$

$$ \%EL = \frac{l_f - l_0}{l_0}\times 100 \qquad\qquad \%RA = \frac{A_0 - A_f}{A_0}\times 100 $$

- **Yield strength and tensile strength** are measures of **strength**.
- **Fracture strength is not used as a design criterion** — it is highly scattered, depends on flaws, and a design that allows stresses to approach fracture is already unsafe. Design is based on yield (with a factor of safety).
- **% elongation to failure** and **% reduction in area** are measures of **ductility**. Reduction in area is often the more sensitive indicator, because it is measured at the neck where deformation is concentrated.

#### The gauge-length dependence of %EL

The total elongation is the sum of a *uniform* strain over the gauge and a *localised* strain concentrated in the neck. The neck contributes an approximately fixed length ($\sim\beta\sqrt{A_0}$), so its *relative* contribution grows as the gauge length shrinks. Empirically (Barba's law):

$$ \Delta L = \beta\sqrt{A_0} + \varepsilon_u L_0 \qquad\Longrightarrow\qquad \%EL \text{ increases as } L_0 \text{ decreases} $$

Hence a "20 % elongation" for a 25 mm gauge is not the same material property as "20 %" for a 50 mm gauge. The **Russell–Bailey** and **Oliver** relations are variants of the same idea. %RA has no such ambiguity, which is why it is preferred for comparing materials and why specifications quote both.

#### Ductility in design

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

### 2.15 Necking

After the UTS the cross-section decreases locally — a **neck** forms, and further deformation is confined to it. Because engineering stress uses $A_0$, the curve falls even though the *true* stress in the neck continues to rise. In **semicrystalline polymers** the neck is *stable*: it draws down and then propagates along the gauge length (cold drawing), giving a long plateau rather than a fall.

![[MP2 - Necking in tension.png|420]]

*Figure — the onset of necking at the tensile strength: the load maximum coincides with the point where the area reduction outruns the work hardening.*

![[MP2 - Neck propagation semicrystalline polymer.png|400]]

*Figure — in a semicrystalline polymer the neck stabilises and propagates along the gauge length (cold drawing), producing a long plateau instead of a descending branch.*

#### The Considère criterion — why necking starts exactly at the UTS

Necking begins when the *load* stops increasing, i.e. $dP=0$. With $P = \sigma_T A_i$ and constant volume ($A_i l_i$ = const, so $dA/A = -d\varepsilon_T$):

$$ dP = \sigma_T\,dA + A\,d\sigma_T = 0 \quad\Longrightarrow\quad \frac{d\sigma_T}{d\varepsilon_T} = \sigma_T $$

$$ \boxed{\ \text{Necking begins when}\ \ \dfrac{d\sigma_T}{d\varepsilon_T} = \sigma_T\ } $$

This is the **Considère construction**: plot the true stress and also the tangent from the origin... more usefully, plot $\sigma_T$ and its derivative; the point where the tangent to the $\sigma_T$–$\varepsilon_T$ curve passes through the origin is the instability point. Two important consequences:

1. **Necking is a geometric instability, not a material failure.** A material with no work hardening would neck immediately at yield; a strongly work-hardening material resists localisation. Ductility in tension is therefore *set by the work-hardening rate*.
2. **Combining with Hollomon**, $\sigma_T = K\varepsilon_T^n$, gives $d\sigma_T/d\varepsilon_T = nK\varepsilon_T^{n-1} = n\sigma_T/\varepsilon_T$, so the criterion becomes
$$ n = \varepsilon_{T,u} $$
i.e. **the strain-hardening exponent equals the true uniform strain at the UTS.** This is one of the most examinable results in the whole topic, and it means that a tensile test gives $n$ directly as the true strain at maximum load.

#### Strain-rate sensitivity and neck stability

A neck is stable if the material in the neck becomes *stronger in strain rate* as it thins — positive strain-rate sensitivity,

$$ \sigma = C\dot{\varepsilon}^{m} $$

With $m>0$ the rapidly deforming neck region hardens and resists further localisation. This is why:

- **Superplastic materials** ($m\approx0.3$–$0.5$, fine grain size, $T>0.5T_m$) can stretch to 300–1000 % without necking — they are used to form complex sheet shapes by blow forming;
- **cold-drawn polymers** show a stable neck, because drawing is a rate-sensitive orientation process;
- raising the test temperature or slowing the rate (both raising the *effective* $m$) delays necking and increases elongation.

#### The triaxial stress state in the neck

Once a neck forms, the necked region is constrained by the (still cylindrical) shoulders. This builds up **radial and hoop stresses** in addition to the axial one — a **triaxial tension** state. The axial stress computed as $F/A_{\text{neck}}$ therefore *overestimates* the true flow stress. Bridgman's correction is

$$ \sigma_{\text{corr}} = \frac{\sigma_T}{\left(1+\dfrac{2R}{a}\right)\ln\!\left(1+\dfrac{a}{2R}\right)} $$

where $a$ is the neck radius and $R$ the radius of curvature of the neck profile. The correction is small (a few %) at the start of necking and grows as the neck sharpens — this is exactly the gap between the "true" and "corrected" curves in §2.18. The same triaxiality is what makes notched bars brittle (§2.7): constraint raises the maximum principal stress without raising the shear stress that would relieve it by yielding.

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

![[MP2 - True corrected engineering curves.png|440]]

*Figure — engineering, true and corrected true stress–strain curves for a ductile metal: the engineering curve peaks and falls after the UTS, the true curve rises monotonically, and the corrected curve lies slightly below the true one in the necked region.*

#### Where the conversions come from

Starting from constancy of volume during plastic flow, $A_0l_0=A_il_i \Rightarrow A_i = A_0l_0/l_i$:

$$ \sigma_T = \frac{F}{A_i} = \frac{F}{A_0}\cdot\frac{A_0}{A_i} = \sigma\cdot\frac{l_i}{l_0} = \sigma(1+\varepsilon) $$

$$ \varepsilon_T = \int_{l_0}^{l_i}\frac{dl}{l} = \ln\frac{l_i}{l_0} = \ln(1+\varepsilon) = \ln\frac{A_0}{A_i} $$

Both follow from the same assumption and are therefore valid only while deformation is **uniform** (before necking).

#### Why true strain is the "right" measure

- **Additivity**: strain increments multiply lengths, so logarithms add. Drawing a wire from $l_0\to l_1\to l_2$ gives $\varepsilon_T = \ln(l_1/l_0)+\ln(l_2/l_1)=\ln(l_2/l_0)$. Engineering strains do not add: $0.5$ then $0.5$ gives $1.0$, whereas the true strain is $\ln 1.5+\ln 1.5 = 0.81$.
- **Symmetry in tension/compression**: reversing a true strain gives $-\varepsilon_T$ exactly; reversing an engineering strain of $+0.5$ gives $-0.33$, not $-0.5$. True strain treats the two directions consistently.
- **Thickness reduction in rolling** is $\varepsilon_T = \ln(t_0/t_f)$, the standard formula in metal-forming analysis; a 50 % reduction in thickness is $\varepsilon_T = 0.693$, not 0.5.
- **Large-strain equivalence**: for a general 3D deformation one uses the **effective (von Mises) strain** $\bar\varepsilon = \sqrt{\tfrac23(\varepsilon_1^2+\varepsilon_2^2+\varepsilon_3^2)}$ in the same way as the von Mises stress, so that a multiaxial forming operation can be compared with a uniaxial flow curve.

#### True fracture stress

At fracture, the true stress is

$$ \sigma_{T,f} = \frac{F_f}{A_f} $$

where $A_f$ is the *measured* fracture area. This is much larger than the engineering fracture stress (for a ductile steel, $\sigma_f\approx0.7\sigma_{UTS}$ while $\sigma_{T,f}\approx1.5$–$2\sigma_{UTS}$), and the true fracture strain is

$$ \varepsilon_{T,f} = \ln\frac{A_0}{A_f} = \ln\frac{100}{100-\%RA} $$

which is a gauge-length-independent measure of ductility — the natural companion to %RA.

> [!warning] Do not use these conversions after necking
> Once the neck forms, the strain is no longer uniform across the gauge, so "the" true stress and "the" true strain of the specimen are ill-defined; $F/A_{\text{neck}}$ gives a *local* stress that overestimates the flow stress because of triaxiality. That is precisely why the "corrected" curve exists.

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

#### The quantitative link to dislocation density

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

#### Why dislocations obstruct each other

1. **Forest hardening** — a dislocation gliding on its plane must cut through the dislocations threading that plane ("forest"). Each intersection creates a jog, costing energy.
2. **Junction formation** — two dislocations on intersecting planes can react to form a segment that is not glissile (**Lomer locks**, §2.5). Junctions are strong obstacles.
3. **Pile-ups at obstacles** — grain boundaries, twin boundaries, particles, and previously formed locks. The back stress from a pile-up reduces the effective stress on the source.
4. **Cell/subgrain structure** — at large strains dislocations arrange into dense walls surrounding nearly dislocation-free cells, and the cell size sets the mean free path.
5. **Twin boundaries** — in low-SFE metals (brass, TWIP steels) deformation twins subdivide the grains and add barriers, giving exceptionally high hardening rates.

#### Consequences and practical aspects

- **Uniform elongation is controlled by the hardening rate**: high hardening delays the Considère instability, so high-$n$ materials stretch further. This is why annealed copper and 304 stainless steel can be deep-drawn and why tempered 4340 cannot.
- **The Bauschinger effect**: after tensile pre-strain, the compressive yield stress is *lower* than the tensile flow stress — the internal back stresses from pile-ups assist reverse flow. This matters in cyclic loading, in spring making, and in any forming operation with reversed strain.
- **Recovery and recrystallisation**: annealing removes work hardening in two stages — *recovery* (dislocation rearrangement and annihilation, small property change) then *recrystallisation* (new strain-free grains nucleate and grow, hardness drops to the annealed value, ductility is restored). The temperature at which this happens in one hour is the **recrystallisation temperature**, roughly $0.3$–$0.4T_m$.
- **Hot working vs cold working**: above the recrystallisation temperature, hardening is continuously removed by dynamic recovery/recrystallisation, so enormous strains are possible with low forces (rolling, forging, extrusion). Below it, the work hardening accumulates (cold rolling, wire drawing) and is used deliberately to strengthen the product.
- **Work hardening is limited**: it cannot exceed the fracture strength, so a heavily drawn wire eventually fails; and it consumes all the ductility, so a cold-rolled sheet may be too brittle to bend.

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
