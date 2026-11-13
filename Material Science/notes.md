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
