# Post-Midsem Syllabus — Phase Diagrams

---

## Master Topic & Reference Guide

| # | Topic / Syllabus Module | Recommended Book & Section | Pages & Figures |
|---|------------------------|---------------------------|-----------------|
| 1 | Iron-Carbon (Fe–Fe₃C) Diagram | Callister & Rethwisch, Ch. 9, Sec 9.18–9.20 | pp. 287–301 (Figs 9.24–9.32) |
| | | A. Prince, Ch. 6, Sec 6.2 | pp. 104–108 (Figs 89–92) |
| 2 | Concept of Coring | Callister & Rethwisch, Ch. 9, Sec 9.8 | p. 261 (Fig. 9.5) |
| | | Paul Gordon, Ch. 4, Sec 4.8 | pp. 65–70 (Figs 4.10–4.12) |
| | | A. Prince, Ch. 4, Sec 4.2.3 | p. 74 |
| 3 | Invariant Reactions | A. Prince, Ch. 3, Sec 3.1; Ch. 4; Ch. 6 | p. 43, pp. 66–88, pp. 104–108 |
| | | Paul Gordon, Ch. 6, Sec 6.1–6.9 | pp. 148–172 (Figs 6.19–6.23) |
| 4 | Flawed Diagram Rules / Errors | Paul Gordon, Ch. 6, Sec 6.14 / Ch. 4 & 6 | pp. 186–191 & pp. 86–90 |
| | | A. Prince, Ch. 4, Sec 4.2.4 & 4.2 | p. 74, p. 79 (Figs 58–60) |
| 5 | Gibbs Phase Rule Derivation | A. Prince, Ch. 2, Sec 2.2.1; Ch. 8, Sec 8.1 | pp. 25–27, p. 119 |
| | | Paul Gordon, Ch. 3, Sec 3.3 | pp. 21–22 (Eqn 3.13) |
| | | Callister & Rethwisch, Ch. 9, Sec 9.17 | pp. 284–285 (Eqn 9.16) |
| 6 | Phase Diagram Synthesis | Paul Gordon, Ch. 6 & Ch. 7 | pp. 148–185 |
| | | A. Prince, Ch. 4 & Ch. 7 | pp. 66–88, pp. 114–118 |
| 7 | All About Gibbs Triangle | A. Prince, Ch. 8, Sec 8.2 & 8.3 | pp. 120–125 (Figs 105–110) |
| | | Porter & Easterling, Ch. 1, Sec 1.7 | pp. 56–58 (Figs 1.40–1.42) |
| 8 | Ternary Systems & Sections | A. Prince, Ch. 8, Sec 8.4; Ch. 9, Sec 9.1, 9.3; Ch. 10, Sec 10.1 | pp. 128–142; pp. 139–168; pp. 173–179 |
| 9 | Experimental Determination | Porter & Easterling, Ch. 2, Sec 2.3 & Ch. 3 | pp. 60–63 |
| | | Callister & Rethwisch, Ch. 10, Sec 10.3 | pp. 315–320 |
| | | Paul Gordon, Ch. 4, Sec 4.9 | pp. 70–71 |

---

## 1. The Iron-Carbon (Fe–Fe₃C) Phase Diagram

### 1. Underlying Theory & Foundations

#### A. Thermodynamic & Kinetic Principles

- **Primary Source:** [[Materials Science and Engineering]] (Callister & Rethwisch), Sections 9.18–9.20, pp. 287–301.
- **Secondary Source:** [[A Prince2.pdf]], Chapter 6, Section 6.2, pp. 104–108.
- Equilibrium diagram between pure iron and iron carbide ($\text{Fe}_3\text{C}$, cementite).

#### B. Governing Formulations & Derivations

**Pure Iron Allotropes:**
- $\alpha$-ferrite: BCC, stable up to 912°C.
- $\gamma$-austenite: FCC, 912°C to 1394°C.
- $\delta$-ferrite: BCC, 1394°C to 1538°C.
- Cementite: $\text{Fe}_3\text{C}$ at 6.70 wt% C (25 at% C).

**The Three Invariant Reactions:**

1. **Peritectic** (1493°C, 0.17 wt% C):

$$L_{(0.53\%\,C)} + \delta_{(0.09\%\,C)} \rightleftharpoons \gamma_{(0.17\%\,C)}$$

2. **Eutectic** (1147°C, 4.30 wt% C) — forms Ledeburite:

$$L_{(4.3\%\,C)} \rightleftharpoons \gamma_{(2.14\%\,C)} + \text{Fe}_3\text{C}$$

3. **Eutectoid** (727°C, 0.76 wt% C) — forms Pearlite:

$$\gamma_{(0.76\%\,C)} \rightleftharpoons \alpha_{(0.022\%\,C)} + \text{Fe}_3\text{C}$$

#### C. Phase & Microstructural Evolution

- **Hypoeutectoid steels** ($< 0.76\%\,C$): proeutectoid ferrite precipitates first, then pearlite at 727°C.
- **Hypereutectoid steels** ($> 0.76\%\,C$): proeutectoid cementite precipitates first, then pearlite.
- Apply the **lever rule** to calculate weight fractions of microconstituents (Callister pp. 290–294, Figs 9.29–9.32).

#### D. Literature References

- [[Materials Science and Engineering]] — Sections 9.18–9.20, pp. 287–301, Figs 9.24–9.32.
- [[A Prince2.pdf]] — Ch. 6, Sec 6.2, pp. 104–108, Figs 89–92.

---

## 2. Concept of Coring (Non-Equilibrium Solidification)

### 1. Underlying Theory & Foundations

#### A. Thermodynamic & Kinetic Principles

- **Primary Source:** [[P Gordon.pdf]], Chapter 4, Section 4.8, pp. 65–70.
- **Secondary Sources:** [[Materials Science and Engineering]], Section 9.8, p. 261; [[A Prince2.pdf]], Section 4.2.3, p. 74.
- Occurs during fast cooling in isomorphous systems where liquid diffusion is rapid ($D_L \to \infty$) but solid-state diffusion is negligible ($D_S \approx 0$).

#### B. Governing Formulations & Derivations

- Partition coefficient: $k = C_S / C_L$ (ratio of solid to liquid composition at the interface).
- Under Scheil conditions ($D_S = 0$, complete liquid mixing): each increment of solid freezes at the local liquidus.
- Effective solidus is depressed below the equilibrium solidus due to compositional gradients.

#### C. Phase & Microstructural Evolution

- Dendrite cores are enriched in the high-melting component; interdendritic grain boundaries are enriched in the low-melting component (Gordon Fig. 4.10, p. 68).
- **Consequences:** Lowers effective solidus, causes incipient melting at grain boundaries upon reheating, degrades mechanical properties.
- **Remedy:** High-temperature homogenization heat treatment below the solidus.

#### D. Literature References

- [[P Gordon.pdf]] — Ch. 4, Sec 4.8, pp. 65–70, Figs 4.10–4.12.
- [[Materials Science and Engineering]] — Sec 9.8, p. 261, Fig. 9.5.
- [[A Prince2.pdf]] — Sec 4.2.3, p. 74.

---

## 3. Types of Invariant Reactions & Representative Diagrams

### 1. Underlying Theory & Foundations

#### A. Thermodynamic & Kinetic Principles

- **Primary Source:** [[A Prince2.pdf]], Ch. 3, Sec 3.1 (p. 43); Ch. 4 & 6 (pp. 66–88, 104–108).
- **Secondary Source:** [[P Gordon.pdf]], Ch. 6, Sec 6.1–6.9, pp. 148–172.
- At an invariant reaction, $F = 0$ (condensed rule), meaning temperature and all phase compositions are fixed.

#### B. Governing Formulations & Derivations

| Reaction | Equation | Example System | Reference |
|----------|----------|---------------|-----------|
| Eutectic | $L \rightleftharpoons \alpha + \beta$ | Pb–Sn, Ag–Cu | Prince Fig. 44, p. 66 |
| Eutectoid | $\gamma \rightleftharpoons \alpha + \beta$ | Fe–Fe₃C, Cu–Al | Prince Fig. 90, p. 105 |
| Peritectic | $L + \alpha \rightleftharpoons \beta$ | Pt–Re, Fe–C | Prince Fig. 65, p. 82 |
| Peritectoid | $\alpha + \beta \rightleftharpoons \gamma$ | Ni–Zn, Al–Cu | — |
| Monotectic | $L_1 \rightleftharpoons L_2 + \alpha$ | Cu–Pb, Al–In | Prince Fig. 82, p. 95 |
| Monotectoid | $\alpha_1 \rightleftharpoons \alpha_2 + \beta$ | — | — |
| Syntectic | $L_1 + L_2 \rightleftharpoons \alpha$ | K–Zn | — |
| Metatectic | $\beta \rightleftharpoons \alpha + L$ | Co–Os, Co–Ru | Prince p. 115 |

#### D. Literature References

- [[A Prince2.pdf]] — Ch. 3, Sec 3.1, p. 43; Ch. 4, pp. 66–88; Ch. 6, pp. 104–108.
- [[P Gordon.pdf]] — Ch. 6, Sec 6.1–6.9, pp. 148–172, Figs 6.19–6.23.

---

## 4. Rules for Constructing Complex Phase Diagrams & Spotting Errors

### 1. Underlying Theory & Foundations

#### A. Thermodynamic & Kinetic Principles

- **Primary Source:** [[P Gordon.pdf]], Ch. 6, Sec 6.14, pp. 186–191; Ch. 4, Sec 4.14, pp. 86–90.
- **Secondary Source:** [[A Prince2.pdf]], Ch. 4, Sec 4.2.4, p. 74; Sec 4.2, p. 79, Figs 58–60.

#### B. Governing Formulations & Derivations

**Core Rules for Spotting Flaws:**

1. **180° Boundary Extension Rule:** Extensions of phase boundaries bounding a single-phase region at an invariant horizontal must project into adjacent two-phase regions at an angle $< 180°$ (Prince Figs 58–60, p. 79).
2. **Phase Boundary Directionality:** Boundaries enclosing a two-phase region must extrapolate smoothly into neighboring two-phase fields — never crossing into single-phase fields (Gordon pp. 186–188).
3. **Tangency at Extrema:** Liquidus and solidus curves must meet tangentially with zero slope ($dT/dX = 0$) at congruent melting points or liquidus/solidus minima/maxima (Gordon Fig. 4.22, p. 86).
4. **Dilute-Solution Limit:** Terminal phase boundaries cannot be strictly vertical at 0% or 100% composition because $\mu_i \to -\infty$ as $X_i \to 0$ (Gordon p. 50).
5. **Adjacent Phase Field Rule:** Two single-phase regions must always be separated by a two-phase region containing both of those phases.

#### D. Literature References

- [[P Gordon.pdf]] — Ch. 6, Sec 6.14, pp. 186–191; Ch. 4, Sec 4.14, pp. 86–90.
- [[A Prince2.pdf]] — Ch. 4, Sec 4.2.4, p. 74; Sec 4.2, p. 79, Figs 58–60.

---

## 5. Gibbs Phase Rule: Derivation & Application

### 1. Underlying Theory & Foundations

#### A. Thermodynamic & Kinetic Principles

- **Primary Source:** [[A Prince2.pdf]], Ch. 2, Sec 2.2.1, pp. 25–27; Ch. 8, Sec 8.1, p. 119.
- **Secondary Sources:** [[P Gordon.pdf]], Sec 3.3, pp. 21–22; [[Materials Science and Engineering]], Sec 9.17, pp. 284–285.

#### B. Governing Formulations & Derivations

**General derivation** (variables vs. equations):

$$F = n - m = \bigl[P(C-1) + 2\bigr] - \bigl[C(P-1)\bigr] \implies \boxed{F = C - P + 2}$$

**Condensed rule** (isobaric, $P_{\text{ext}} = 1\,\text{atm}$):

$$\boxed{F = C - P + 1}$$

**Applying variance:**

| System | Phases $P$ | Degrees of Freedom $F$ | Character |
|--------|-----------|----------------------|-----------|
| Binary ($C=2$) | 1 | 2 | Bivariant |
| Binary ($C=2$) | 2 | 1 | Monovariant |
| Binary ($C=2$) | 3 | 0 | Invariant line |
| Ternary ($C=3$) | 1 | 3 | Trivariant |
| Ternary ($C=3$) | 2 | 2 | Bivariant |
| Ternary ($C=3$) | 3 | 1 | Monovariant curve |
| Ternary ($C=3$) | 4 | 0 | Invariant plane |

#### D. Literature References

- [[A Prince2.pdf]] — Ch. 2, Sec 2.2.1, pp. 25–27; Ch. 8, Sec 8.1, p. 119.
- [[P Gordon.pdf]] — Sec 3.3, pp. 21–22, Eqn 3.13.
- [[Materials Science and Engineering]] — Sec 9.17, pp. 284–285, Eqn 9.16.

---

## 6. Developing Phase Diagrams from Invariant Reactions

### 1. Underlying Theory & Foundations

#### A. Thermodynamic & Kinetic Principles

- **Primary Source:** [[P Gordon.pdf]], Ch. 6 & 7, pp. 148–185.
- **Secondary Source:** [[A Prince2.pdf]], Ch. 4 & 7, pp. 66–88, 114–118.

#### B. Governing Formulations & Derivations

**Key methodology:**
- Link given temperature levels of invariant reactions (e.g., a high-temperature peritectic feeding into a lower-temperature eutectic).
- Draw single-phase fields ($\alpha, \beta, \gamma$) extending from pure component axes or intermediate compound lines.
- Fill intervening spaces with appropriate two-phase fields ($\alpha + \beta$, $L + \alpha$, $L + \beta$) while obeying boundary extension rules (see Topic 4).

#### D. Literature References

- [[P Gordon.pdf]] — Ch. 6 & 7, pp. 148–185.
- [[A Prince2.pdf]] — Ch. 4 & 7, pp. 66–88, 114–118.

---

## 7. All About the Gibbs Triangle

### 1. Underlying Theory & Foundations

#### A. Thermodynamic & Kinetic Principles

- **Primary Source:** [[A Prince2.pdf]], Ch. 8, Sec 8.2 & 8.3, pp. 120–125.
- **Secondary Source:** [[Phase Transformations in met...pdf]] (Porter & Easterling), Ch. 1, Sec 1.7, pp. 56–58.

#### B. Governing Formulations & Derivations

**Plotting compositions — Viviani's distance theorem:**

$$X_A + X_B + X_C = 1$$

**Special lines:**
- Lines parallel to a side $\implies$ constant concentration of one component.
- Lines from a vertex to the opposite edge $\implies$ constant ratio of the remaining two components: $X_A / X_C = \text{const}$.

**Two-phase equilibrium** — tie-line mass balance:

$$\mathbf{c}^0 = f^\alpha\,\mathbf{c}^\alpha + f^\beta\,\mathbf{c}^\beta$$

Lever rule applies along the tie-line direction (Prince Fig. 108, p. 123).

**Three-phase equilibrium** — barycentric (area) rule:

$$f^\alpha = \frac{A_\alpha}{A_{\text{total}}}$$

where $A_\alpha$ is the sub-triangle area opposite vertex $\alpha$ (Prince Fig. 109, p. 123).

#### D. Literature References

- [[A Prince2.pdf]] — Ch. 8, Sec 8.2–8.3, pp. 120–125, Figs 105–110.
- [[Phase Transformations in met...pdf]] — Ch. 1, Sec 1.7, pp. 56–58, Figs 1.40–1.42.

---

## 8. Ternary Phase Diagrams: Space Models, Isothermal & Vertical Sections

### 1. Underlying Theory & Foundations

#### A. Thermodynamic & Kinetic Principles

- **Primary Source:** [[A Prince2.pdf]], Ch. 8, Sec 8.4 (pp. 128–142); Ch. 9, Sec 9.1 & 9.3 (pp. 139–168); Ch. 10, Sec 10.1 (pp. 173–179).
- **Secondary Source:** [[Phase Transformations in met...pdf]], Sec 1.7, pp. 56–59.

#### B. Governing Formulations & Derivations

- **3D Space Model Prisms:** $T$–$X_A$–$X_B$ right-triangular prisms for isomorphous and eutectic systems (Prince Fig. 111, p. 128; Fig. 179, p. 179).
- **Isothermal Sections:** Horizontal cuts at constant $T$; sequence from above $T_A$ down to below $T_C$ (Prince Fig. 116, p. 129; Fig. 176, p. 176).
- **Vertical (Isoplethic) Sections:** Vertical cuts along composition lines. Note: horizontal lines on vertical sections are **not** tie-lines because 3D tie-lines are skewed in space (Prince Figs 119–120, pp. 130–131).
- **Konovalov's Rule for Ternary Tie-lines:** Counter-clockwise rotation of tie-lines toward lower-melting components (Prince Fig. 117, p. 130).

#### D. Literature References

- [[A Prince2.pdf]] — Ch. 8, Sec 8.4, pp. 128–142; Ch. 9, pp. 139–168; Ch. 10, pp. 173–179.
- [[Phase Transformations in met...pdf]] — Sec 1.7, pp. 56–59.

---

## 9. Experimental Determination of Phase Diagrams

### 1. Underlying Theory & Foundations

#### A. Thermodynamic & Kinetic Principles

- **Primary Source:** [[Phase Transformations in met...pdf]], Ch. 2, Sec 2.3, pp. 60–63; Ch. 3, pp. 120–121.
- **Secondary Sources:** [[Materials Science and Engineering]], Ch. 10, Sec 10.3, pp. 315–320; [[P Gordon.pdf]], Sec 4.9, pp. 70–71.

#### B. Governing Formulations & Derivations

**Isothermal Methods (Point Nature):**
- **Optical Microscopy & SEM/TEM:** Microstructural phase identification.
- **X-Ray Diffraction (XRD):** Crystal structure and lattice parameters.
- **EDS (Energy Dispersive Spectroscopy):** Quantitative local elemental compositions of coexisting phases.

**Isothermal Methods (Diffusion Couples):**
- Welded pure metal blocks annealed at constant $T_1$ create diffusion layers displaying local equilibrium across interfaces ($a_\alpha = a_\beta$) (Porter & Easterling Fig. 2.29, p. 119).

**Non-Isothermal Methods:**
- **Cooling Curves:** Thermal arrests — inflections for liquidus/solidus, horizontal plateaus for invariant reactions.
- **Differential Thermal Analysis (DTA) & DSC:** Measuring latent heat absorption/evolution peaks during heating and cooling.

#### D. Literature References

- [[Phase Transformations in met...pdf]] — Ch. 2, Sec 2.3, pp. 60–63; Ch. 3, pp. 120–121.
- [[Materials Science and Engineering]] — Ch. 10, Sec 10.3, pp. 315–320.
- [[P Gordon.pdf]] — Sec 4.9, pp. 70–71.
