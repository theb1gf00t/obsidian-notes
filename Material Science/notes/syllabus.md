---
title: MO-201 — Material Science Syllabus Tracker
aliases:
  - MO-201 Syllabus
course: Material Science
code: MO-201
tags:
  - materials-science
  - MO-201
  - syllabus
---

# MO-201 — Material Science Syllabus

This file is the **authority** for the topic list, the topic order and the midsem / post-midsem split; [[notes]] is written against it section for section. Every topic below links to its lecture PDF and straight to the matching heading(s) in [[notes]].

> [!warning] Scope of the examination
> **The end-semester examination includes all of the syllabus** — both the pre-midsem block (topics 1–8) and the post-midsem block (topics 1–9). Nothing drops out.

> [!info] How to use this tracker
> - Tick the box on a topic line when the topic is **revised and recallable**, not merely read once. Untick it if a revision pass exposes a hole.
> - **PDF** opens the lecture slides; **Notes** jumps to the topic's heading in [[notes]]; the section index at the bottom gives a one-click jump to every written section.
> - The counter below is live (Dataview) — it reads the checkboxes in this file, so nothing needs counting by hand.
> - `§` numbers are the H3 section numbers used inside [[notes]] (e.g. §2.4 is a real heading there).

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

- [ ] **1 · Crystal Defects** — [[Crystal Defects.pdf|PDF]] · *notes not yet written*
- [ ] **2 · Introduction and Structures of Materials — I** — [[Introduction and Structures of Materials - I.pdf|PDF]] · *notes not yet written*
- [ ] **3 · Introduction and Structures of Materials — II** — [[Introduction and Structures of Materials - II.pdf|PDF]] · *notes not yet written*
- [ ] **4 · Introduction and Structures of Materials — IIIa** — [[Introduction and Structures of Materials - IIIa.pdf|PDF]] · *notes not yet written*
- [ ] **5 · Introduction and Structures of Materials — IIIb** — [[Introduction and Structures of Materials - IIIb.pdf|PDF]] · *notes not yet written*
- [ ] **6 · Introduction and Structures of Materials — IV** — [[Introduction and Structures of Materials - IV.pdf|PDF]] · *notes not yet written*
- [ ] **7 · Phase Diagrams** — [[Phase_Diagrams.pdf|PDF]] · *notes not yet written* · depth: [[Phase Diagrams/Syllabus|Phase Diagrams syllabus]] + [[Post Midsem Notes]]
- [ ] **8 · Quasi Crystals** — [[Quasicrystals.pdf|PDF]] · *notes not yet written* · papers: [[A journey through the history of quasicrystals » MIT Physics.pdf|MIT Physics]], [[A journey through the history of quasicrystals – The Varsity.pdf|The Varsity]], [[Paul_Steinhardt_The_Second_Kind_of_Impossible.pdf|Steinhardt]], [[quasicrystals_nobelprize_dot_org.pdf|NobelPrize.org]]

---

## Post-Midsem — 9 topics

- [x] **1 · Mechanical Properties — I** — [[Mechanical Properties part 1_Odd_2026-27.pdf|PDF]] · [[notes#1. Mechanical Properties — I|Notes → §1]] (8 sections)
- [x] **2 · Mechanical Properties — II** — [[Mechanical Properties part 2_Odd_2026-27.pdf|PDF]] · [[notes#2. Mechanical Properties — II|Notes → §2]] (19 sections)
- [x] **3 · Mechanical Properties — III** — [[Mechanical Properties part 3_Odd_2026-27.pdf|PDF]] · [[notes#3. Mechanical Properties — III|Notes → §3]] (10 sections)
- [ ] **4 · Shockley and Frankel Partial Dislocations** — [[Shockley and Frank partial dislocations_Odd_2026-27.pdf|PDF]] · [[notes#4. Shockley and Frankel Partial Dislocations|Notes → §4]] (9 sections)
- [ ] **5 · Composites** — [[Composites_Odd_2026-27.pdf|PDF]] · [[notes#5. Composites|Notes → §5]] (20 sections)
- [x] **6 · Electrical and Electronic Properties — Part 1** — [[Electrical and Electronic Properties - Part 1_Odd_2026-27.pdf|PDF]] · [[notes#6. Electrical and Electronic Properties — Part 1|Notes → §6]] (12 sections)
- [ ] **7 · Electrical and Electronic Properties — Part 2** — [[Electrical and Electronic Properties - Part 2_Odd_2026-27.pdf|PDF]] · [[notes#7. Electrical and Electronic Properties — Part 2|Notes → §7]] (14 sections)
- [x] **8 · Magnetic Properties** — [[Magnetic Properties_Odd_2026-27.pdf|PDF]] · [[notes#8. Magnetic Properties|Notes → §8]] (17 sections)
- [ ] **9 · Dielectric Materials, Polarization, Optical Properties** — [[Dielectric materials_Polarization_Optical properties_Odd_2026-27.pdf|PDF]] · [[notes#9. Dielectric Materials, Polarization, Optical Properties|Notes → §9]] (12 sections)

> [!note] Slug-to-slide map
> The PDF file names carry the `_Odd_2026-27` suffix and spell the titles slightly differently from the syllabus (e.g. syllabus *Mechanical Properties - I* → file *Mechanical Properties part 1*). The topic number is the anchor: **topic N in the syllabus = `## N` in [[notes]] = the Nth lecture PDF**.

> [!tip] Exam pointer
> The marks in this course sit on the **comparisons and the derivations**, not on definitions: mechanical-property trade-offs (§1.6, §1.7), Schmid/CRSS (§2.4), Considère and Hollomon (§2.15, §2.18), hardness-test selection (§3.4), rule of mixtures and critical fibre length (§5.6, §5.9), band structure → conductivity class (§7.3), the exchange criterion (§8.9), and the four polarization mechanisms (§9.3–§9.7).

---

## Section index of the notes

Every written section of [[notes]], grouped by topic, so a topic can be opened at the exact sub-heading.

### §1 · Mechanical Properties — I

| § | Section |
| --- | --- |
| 1.1 | [[notes#1.1 Why study mechanical properties?\|Why study mechanical properties?]] |
| 1.2 | [[notes#1.2 Deformation: elastic, plastic, fracture\|Deformation: elastic, plastic, fracture]] |
| 1.3 | [[notes#1.3 Types of loading\|Types of loading]] |
| 1.4 | [[notes#1.4 Concepts of stress and strain\|Concepts of stress and strain]] |
| 1.5 | [[notes#1.5 Examples of mechanical tests\|Examples of mechanical tests]] |
| 1.6 | [[notes#1.6 Key mechanical design properties\|Key mechanical design properties]] |
| 1.7 | [[notes#1.7 Mechanical testing ↔ deformation mechanisms\|Mechanical testing ↔ deformation mechanisms]] |
| 1.8 | [[notes#1.8 Tensile test: first look\|Tensile test: first look]] |

### §2 · Mechanical Properties — II

| § | Section |
| --- | --- |
| 2.1 | [[notes#2.1 Atomic model of elastic behaviour\|Atomic model of elastic behaviour]] |
| 2.2 | [[notes#2.2 Deformation by slip and twinning\|Deformation by slip and twinning]] |
| 2.3 | [[notes#2.3 Slip systems\|Slip systems]] |
| 2.4 | [[notes#2.4 CRSS and the Schmid factor\|CRSS and the Schmid factor]] |
| 2.5 | [[notes#2.5 Dislocation reactions and sessile (Lomer) locks\|Dislocation reactions and sessile (Lomer) locks]] |
| 2.6 | [[notes#2.6 The tensile test: specimen, machine, curve\|The tensile test: specimen, machine, curve]] |
| 2.7 | [[notes#2.7 Brittle and ductile behaviour: temperature, and the Yoffee diagram\|Brittle and ductile behaviour: temperature, and the Yoffee diagram]] |
| 2.8 | [[notes#2.8 Properties obtained from the tensile test\|Properties obtained from the tensile test]] |
| 2.9 | [[notes#2.9 Anelasticity and viscoelasticity\|Anelasticity and viscoelasticity]] |
| 2.10 | [[notes#2.10 Poisson's ratio\|Poisson's ratio]] |
| 2.11 | [[notes#2.11 Yield stress and tensile strength\|Yield stress and tensile strength]] |
| 2.12 | [[notes#2.12 Resilience and toughness\|Resilience and toughness]] |
| 2.13 | [[notes#2.13 Tensile curves for polymers\|Tensile curves for polymers]] |
| 2.14 | [[notes#2.14 Measures of strength and ductility\|Measures of strength and ductility]] |
| 2.15 | [[notes#2.15 Necking\|Necking]] |
| 2.16 | [[notes#2.16 True stress and true strain\|True stress and true strain]] |
| 2.17 | [[notes#2.17 Work hardening / strain hardening\|Work hardening / strain hardening]] |
| 2.18 | [[notes#2.18 The plastic flow curve and the Hollomon equation\|The plastic flow curve and the Hollomon equation]] |
| 2.19 | [[notes#2.19 Elastic recovery after plastic deformation\|Elastic recovery after plastic deformation]] |

### §3 · Mechanical Properties — III

| § | Section |
| --- | --- |
| 3.1 | [[notes#3.1 Testing brittle materials: the three-point bend test\|Testing brittle materials: the three-point bend test]] |
| 3.2 | [[notes#3.2 Stress–strain behaviour of ceramics and the influence of porosity\|Stress–strain behaviour of ceramics and the influence of porosity]] |
| 3.3 | [[notes#3.3 Hardness: definition and advantages\|Hardness: definition and advantages]] |
| 3.4 | [[notes#3.4 Hardness-testing techniques — summary\|Hardness-testing techniques — summary]] |
| 3.5 | [[notes#3.5 The Rockwell test\|The Rockwell test]] |
| 3.6 | [[notes#3.6 The Brinell test\|The Brinell test]] |
| 3.7 | [[notes#3.7 The Knoop and Vickers microindentation tests\|The Knoop and Vickers microindentation tests]] |
| 3.8 | [[notes#3.8 Hardness conversion\|Hardness conversion]] |
| 3.9 | [[notes#3.9 Hardness of ceramics\|Hardness of ceramics]] |
| 3.10 | [[notes#3.10 Tear strength and hardness of polymers\|Tear strength and hardness of polymers]] |

### §4 · Shockley and Frankel Partial Dislocations

| § | Section |
| --- | --- |
| 4.1 | [[notes#4.1 Why a perfect dislocation dissociates\|Why a perfect dislocation dissociates]] |
| 4.2 | [[notes#4.2 The close-packed stacking of $\{111\}$ and the stacking fault\|The close-packed stacking of {111} and the stacking fault]] |
| 4.3 | [[notes#4.3 The Shockley partial: $\mathbf{b} = \tfrac{a}{6}\langle112\rangle$\|The Shockley partial]] |
| 4.4 | [[notes#4.4 The extended dislocation: width of the fault ribbon\|The extended dislocation: width of the fault ribbon]] |
| 4.5 | [[notes#4.5 Thompson's tetrahedron: the vector bookkeeping\|Thompson's tetrahedron: the vector bookkeeping]] |
| 4.6 | [[notes#4.6 Frank partials: $\mathbf{b} = \tfrac{a}{3}\langle111\rangle$\|Frank partials]] |
| 4.7 | [[notes#4.7 How Frank partials are made — and how they are removed\|How Frank partials are made — and how they are removed]] |
| 4.8 | [[notes#4.8 Shockley versus Frank — the comparison to write out\|Shockley versus Frank — the comparison to write out]] |
| 4.9 | [[notes#4.9 What the stacking-fault energy controls\|What the stacking-fault energy controls]] |

### §5 · Composites

| § | Section |
| --- | --- |
| 5.1 | [[notes#5.1 What is a composite?\|What is a composite?]] |
| 5.2 | [[notes#5.2 A catalogue of engineering composites\|A catalogue of engineering composites]] |
| 5.3 | [[notes#5.3 Where composites stand among materials\|Where composites stand among materials]] |
| 5.4 | [[notes#5.4 Classification of composites\|Classification of composites]] |
| 5.5 | [[notes#5.5 The matrix and the dispersed phase\|The matrix and the dispersed phase]] |
| 5.6 | [[notes#5.6 Particle-reinforced composites\|Particle-reinforced composites]] |
| 5.7 | [[notes#5.7 Concrete — a large-particle ceramic composite\|Concrete — a large-particle ceramic composite]] |
| 5.8 | [[notes#5.8 Dispersion-strengthened composites\|Dispersion-strengthened composites]] |
| 5.9 | [[notes#5.9 Fibre-reinforced composites\|Fibre-reinforced composites]] |
| 5.10 | [[notes#5.10 Continuous and aligned fibre composites\|Continuous and aligned fibre composites]] |
| 5.11 | [[notes#5.11 Discontinuous and randomly oriented fibre composites\|Discontinuous and randomly oriented fibre composites]] |
| 5.12 | [[notes#5.12 Fibres and the matrix — what each must do\|Fibres and the matrix — what each must do]] |
| 5.13 | [[notes#5.13 Polymer-matrix composites\|Polymer-matrix composites]] |
| 5.14 | [[notes#5.14 Metal-matrix composites\|Metal-matrix composites]] |
| 5.15 | [[notes#5.15 Ceramic-matrix composites\|Ceramic-matrix composites]] |
| 5.16 | [[notes#5.16 Hybrid composites\|Hybrid composites]] |
| 5.17 | [[notes#5.17 Processing of fibre-reinforced composites\|Processing of fibre-reinforced composites]] |
| 5.18 | [[notes#5.18 Structural composites\|Structural composites]] |
| 5.19 | [[notes#5.19 Nanocomposites\|Nanocomposites]] |
| 5.20 | [[notes#5.20 Composites in service — skis, aircraft and cars\|Composites in service — skis, aircraft and cars]] |

### §6 · Electrical and Electronic Properties — Part 1

| § | Section |
| --- | --- |
| 6.1 | [[notes#6.1 The resistivity range: twenty-five orders of magnitude\|The resistivity range: twenty-five orders of magnitude]] |
| 6.2 | [[notes#6.2 The free electron model\|The free electron model]] |
| 6.3 | [[notes#6.3 The electron as a wave: de Broglie, wave number and the $E$–$k$ parabola\|The electron as a wave: de Broglie, wave number and the E–k parabola]] |
| 6.4 | [[notes#6.4 Quantization: states in a box and the Fermi energy\|Quantization: states in a box and the Fermi energy]] |
| 6.5 | [[notes#6.5 Fermi–Dirac statistics\|Fermi–Dirac statistics]] |
| 6.6 | [[notes#6.6 Conduction by free electrons: drift velocity and conductivity\|Conduction by free electrons: drift velocity and conductivity]] |
| 6.7 | [[notes#6.7 Superconductors: the abrupt disappearance of resistance\|Superconductors: the abrupt disappearance of resistance]] |
| 6.8 | [[notes#6.8 The Meissner effect\|The Meissner effect]] |
| 6.9 | [[notes#6.9 Type I and Type II superconductors\|Type I and Type II superconductors]] |
| 6.10 | [[notes#6.10 Why the free electron model must fail\|Why the free electron model must fail]] |
| 6.11 | [[notes#6.11 The energy gap: Bragg reflection and standing waves\|The energy gap: Bragg reflection and standing waves]] |
| 6.12 | [[notes#6.12 The forbidden gap in three dimensions\|The forbidden gap in three dimensions]] |

### §7 · Electrical and Electronic Properties — Part 2

| § | Section |
| --- | --- |
| 7.1 | [[notes#7.1 Overlapping bands and the disappearance of the gap\|Overlapping bands and the disappearance of the gap]] |
| 7.2 | [[notes#7.2 Brillouin zones\|Brillouin zones]] |
| 7.3 | [[notes#7.3 The valence band, the conduction band, and the classification of solids\|The valence band, the conduction band, and the classification of solids]] |
| 7.4 | [[notes#7.4 Metals: two ways to be a conductor\|Metals: two ways to be a conductor]] |
| 7.5 | [[notes#7.5 The fourth column: from diamond to lead\|The fourth column: from diamond to lead]] |
| 7.6 | [[notes#7.6 The semiconductor–insulator divide\|The semiconductor–insulator divide]] |
| 7.7 | [[notes#7.7 Intrinsic semiconductors: carrier statistics\|Intrinsic semiconductors: carrier statistics]] |
| 7.8 | [[notes#7.8 Conductivity of an intrinsic semiconductor\|Conductivity of an intrinsic semiconductor]] |
| 7.9 | [[notes#7.9 Extrinsic semiconductors: donors and n-type conduction\|Extrinsic semiconductors: donors and n-type conduction]] |
| 7.10 | [[notes#7.10 Acceptors and p-type conduction\|Acceptors and p-type conduction]] |
| 7.11 | [[notes#7.11 The three regions of the conductivity–temperature plot\|The three regions of the conductivity–temperature plot]] |
| 7.12 | [[notes#7.12 Doping in practice: diffusion, predeposition and drive-in\|Doping in practice: diffusion, predeposition and drive-in]] |
| 7.13 | [[notes#7.13 The p-n junction at equilibrium\|The p-n junction at equilibrium]] |
| 7.14 | [[notes#7.14 Forward and reverse bias\|Forward and reverse bias]] |

### §8 · Magnetic Properties

| § | Section |
| --- | --- |
| 8.1 | [[notes#8.1 Magnetic induction, field strength and permeability\|Magnetic induction, field strength and permeability]] |
| 8.2 | [[notes#8.2 Diamagnetism, paramagnetism and ferromagnetism\|Diamagnetism, paramagnetism and ferromagnetism]] |
| 8.3 | [[notes#8.3 Paramagnetism: alignment of permanent moments\|Paramagnetism: alignment of permanent moments]] |
| 8.4 | [[notes#8.4 Magnetic moments due to electron spin\|Magnetic moments due to electron spin]] |
| 8.5 | [[notes#8.5 The solid state correction: 4s–3d overlap\|The solid state correction: 4s–3d overlap]] |
| 8.6 | [[notes#8.6 Magnetization\|Magnetization]] |
| 8.7 | [[notes#8.7 Hund's rule as spin-dependent electrostatic energy\|Hund's rule as spin-dependent electrostatic energy]] |
| 8.8 | [[notes#8.8 Band overlap in the first transition series\|Band overlap in the first transition series]] |
| 8.9 | [[notes#8.9 The exchange interaction energy and the 1.5–2.0 criterion\|The exchange interaction energy and the 1.5–2.0 criterion]] |
| 8.10 | [[notes#8.10 The Curie temperature\|The Curie temperature]] |
| 8.11 | [[notes#8.11 Changing the ratio by alloying: the Heusler alloys\|Changing the ratio by alloying: the Heusler alloys]] |
| 8.12 | [[notes#8.12 Ferrimagnetism\|Ferrimagnetism]] |
| 8.13 | [[notes#8.13 Ferrites, the inverse spinel, and magnetite\|Ferrites, the inverse spinel, and magnetite]] |
| 8.14 | [[notes#8.14 The domain structure\|The domain structure]] |
| 8.15 | [[notes#8.15 The hysteresis loop\|The hysteresis loop]] |
| 8.16 | [[notes#8.16 The magnetization process: wall motion first, rotation last\|The magnetization process: wall motion first, rotation last]] |
| 8.17 | [[notes#8.17 Soft and hard magnetic materials\|Soft and hard magnetic materials]] |

### §9 · Dielectric Materials, Polarization, Optical Properties

| § | Section |
| --- | --- |
| 9.1 | [[notes#9.1 Why an insulator is a dielectric\|Why an insulator is a dielectric]] |
| 9.2 | [[notes#9.2 Polarization and capacitance\|Polarization and capacitance]] |
| 9.3 | [[notes#9.3 Electronic polarization\|Electronic polarization]] |
| 9.4 | [[notes#9.4 Ionic polarization\|Ionic polarization]] |
| 9.5 | [[notes#9.5 Orientation polarization\|Orientation polarization]] |
| 9.6 | [[notes#9.6 Space charge polarization\|Space charge polarization]] |
| 9.7 | [[notes#9.7 The ranking of the mechanisms\|The ranking of the mechanisms]] |
| 9.8 | [[notes#9.8 Ferroelectric materials\|Ferroelectric materials]] |
| 9.9 | [[notes#9.9 BaTiO₃ and the ferroelectric Curie temperature\|BaTiO₃ and the ferroelectric Curie temperature]] |
| 9.10 | [[notes#9.10 Optical properties of metals\|Optical properties of metals]] |
| 9.11 | [[notes#9.11 Optical properties of nonmetals: refraction\|Optical properties of nonmetals: refraction]] |
| 9.12 | [[notes#9.12 Reflection, absorption and the band gap\|Reflection, absorption and the band gap]] |

---

## Supplementary sources

| Source | What it is for |
| --- | --- |
| [[MO NOTES (1).pdf]] | Handwritten class notes — the lecturer's own emphasis and worked examples (pp. 100–131, 132–152 for the post-midsem block) |
| [[Materials Science and Engineering An Introduction by William D. Callister, Jr., David G. Rethwish (z-lib.org).pdf]] | Prescribed textbook — *Fundamentals of Materials Science and Engineering* (Callister & Rethwisch) |
| [[MO NOTES (1).pdf#page=100\|MO NOTES — post-midsem range]] | Direct page jump into the handwritten block |
| [[Tutorial_1.pdf]] · [[Tutorial_2.pdf]] · [[MO-201_Tutorial 3_SS.pdf]] | Tutorial sheets — [[MO-201_Tutorial 3_stress-strain_curve.xlsx]] holds the Tutorial 3 data |
| [[Youtube Links for videos on composites.pdf]] | Curated videos for the composites block |
| [[BCC octahedral void position visualization.mp4]] | Void-position animation (structures block) |
| [[Phase_Diagrams.pdf]] | Phase diagrams deck (pre-midsem topic 7) |

---

## Open gaps

> [!warning] What is still missing
> - **All eight pre-midsem topics** have slides but no written notes yet.
> - Pre-midsem topic 7 (phase diagrams) already has a separate, much deeper treatment in the [[Phase Diagrams/Syllabus|Phase Diagrams]] folder — use [[Post Midsem Notes]] there rather than duplicating it here.

> [!question] Self-check before you tick a topic
> - Can you state the topic's **key formula** from memory and give its validity limit?
> - Can you draw the **figure** that carries the topic (Yoffee diagram, hysteresis loop, isostrain/isostress, band-gap classification)?
> - Can you name the **one trap** the lecturer flagged for it?
