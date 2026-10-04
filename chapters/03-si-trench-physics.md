# Chapter 3: Silicon Trench Etch Physics at Sub-20 nm Widths

## Overview

The isolation etch removes silicon from the bottom of an 18 nm-wide trench for about a minute, while the trench grows to fourteen times its width. At the same time, a few microns away, the same plasma etches periphery trenches 60 nm to 20 µm wide. Why the narrow trench etches more slowly, how much more slowly, and what can be done about it are questions of transport: how many reactive neutrals and energetic ions reach the bottom of each trench, and what happens to them on the way.

This chapter builds the physical model used throughout the book. It starts from the ion-neutral synergy that makes silicon etch anisotropic, establishes that transport in these trenches is free-molecular, computes neutral and ion transmission in line spaces and cut gaps, and assembles them into an ARDE model that gives time-to-depth curves for every feature type. It closes with charging and the symmetry-breaking effects that lean fins and tilt profiles.

**Learning Objectives:**
- Explain ion-neutral synergy in halogen silicon etch and estimate the fluxes involved
- Show that transport in sub-20 nm trenches is free-molecular and compute neutral transmission
- Use the Coburn–Winters model to relate bottom reaction probability to ARDE
- Compute ion direct transmission from the angular spread
- Apply the ARDE model ER/ER₀ = 1/(1 + kA) to line spaces, cut gaps, and periphery trenches
- Compute time-to-depth for the reference process and the cell/periphery depth difference
- Estimate ion deflection by charging and identify where symmetry breaks

---

## 3.1 Ion-Neutral Synergy in Silicon Etch

### 3.1.1 Three Regimes

Silicon etches in halogen plasmas by forming volatile halides (SiCl₄, SiBr₄, and lower halides that desorb under ion impact). Without ions, chlorine and bromine atoms etch undoped silicon very slowly at room temperature, because the halogenated surface layer does not desorb readily. Without halogens, ions sputter silicon with a yield of about 0.1–0.3 atoms per ion at 100–300 eV. Together, they etch at rates far above the sum of the two:

```
Regime                     Si removal          Character
─────────────────────────────────────────────────────────────────────────
Br or Cl atoms only        Very slow           Isotropic (heavily doped
(room temperature)         (< 5 nm/min)        n⁺ Si faster)
Ar⁺ ions only (150 eV)     Y ≈ 0.2 Si/ion      Physical sputtering
Br/Cl + ions               Y_eff ≈ 1–3 Si/ion  Ion-enhanced; anisotropic
```

The ion-enhanced reaction is what makes the trench vertical. Ions arrive nearly normal to the wafer, so the trench bottom is bombarded and etches fast. The sidewalls see almost no ions and are protected by a passivation film (Chapter 4), so they barely etch.

### 3.1.2 Flux Estimates at the Open Surface

```
Reference open-area etch rate: ER₀ = 300 nm/min = 5.0 nm/s
Silicon atom density:          n_Si = 5.0×10²² cm⁻³

Si removal flux:  Γ_Si = ER₀ × n_Si = 5.0×10⁻⁷ cm/s × 5.0×10²² cm⁻³
                       = 2.5×10¹⁶ atoms cm⁻² s⁻¹

Ion flux (time-averaged, pulsed ICP, illustrative):
  J_i = 2.5 mA/cm² → Γ_i = 2.5×10⁻³ / 1.602×10⁻¹⁹ = 1.56×10¹⁶ cm⁻² s⁻¹

Effective yield: Y_eff = Γ_Si / Γ_i = 2.5 / 1.56 = 1.6 Si per ion

Bromine atom flux (n_Br ≈ 5×10¹³ cm⁻³, T_g ≈ 350 K):
  v̄ = √(8kT/πm) = √(8 × 1.38×10⁻²³ × 350 / (π × 80 × 1.66×10⁻²⁷)) ≈ 304 m/s
  Γ_Br = n v̄ / 4 = 5×10¹³ × 3.04×10⁴ / 4 = 3.8×10¹⁷ cm⁻² s⁻¹

Halogen needed: ≈ 4 per Si (as SiX₄; less for SiX₂ products)
  ≈ 1.0×10¹⁷ cm⁻² s⁻¹ → supply-to-demand ratio ≈ 4 at the open surface
```

At the open surface, both species are in reasonable supply. The question is how much of each reaches the bottom of a deep trench.

### 3.1.3 A Simple Rate Law

The bottom etch rate can be written as two resistances in series, one for neutral supply and one for ion supply:

```
1/ER = 1/ER_n + 1/ER_i

ER_n = neutral-limited rate (∝ halogen flux reaching the bottom)
ER_i = ion-limited rate (∝ ion flux × yield at the bottom)
```

When neutrals are plentiful, the rate follows the ion flux (ion-limited). When ions are plentiful, it follows the neutral flux (neutral-limited). ARDE depends on which of these falls off faster with depth, and the recipe can choose which regime it operates in.

---

## 3.2 Transport Regime

```
Mean free path at 8 mTorr (1.07 Pa), T_g ≈ 350 K, σ ≈ 4×10⁻¹⁹ m²:

  λ = kT / (√2 σ p) = 1.38×10⁻²³ × 350 / (1.414 × 4×10⁻¹⁹ × 1.07)
    ≈ 8 mm

Knudsen number in an 18 nm trench: Kn = λ / S = 8×10⁻³ / 18×10⁻⁹ ≈ 4×10⁵
```

Inside the trench, molecules never collide with each other. They fly in straight lines from wall to wall. This is **free-molecular (Knudsen) flow**, and transport is set entirely by geometry and by what happens when a molecule hits a wall: whether it sticks, reacts, or bounces off in a random direction. The same is true of ions, which also travel ballistically once they leave the sheath.

The sheath itself is far larger than the trench. At these conditions the sheath is hundreds of microns thick. Ions enter the trench with the energy and angle they gained crossing the sheath, and the trench does not perturb the sheath except through the charging of its surfaces (Section 3.6).

---

## 3.3 Neutral Transport

### 3.3.1 Transmission Through a Slot

A molecule entering a long slot of aspect ratio A (depth over width) reaches the bottom only after a random walk of wall collisions. With diffusely reflecting walls that do not consume it, the probability of reaching the bottom before escaping back out of the top is the Clausing transmission. For a long slot, a good approximation is:

```
K_slot(A) ≈ (ln A + 0.15) / A

For comparison, a round hole of the same depth-to-diameter ratio:
K_hole(A) ≈ 1 / (1 + 0.75 A)       (Clausing, approximate)

  A        K_slot     K_hole
  ─────────────────────────────
  5        0.35       0.21
  10       0.25       0.12
  14       0.20       0.087
  16.6     0.18       0.074
  20       0.16       0.063
```

The cell line spaces are slots. They transmit two to three times more neutral flux than holes of the same aspect ratio. The cut gaps are short openings that join the line spaces on both sides, and their transport is closer to a slot than to a hole because they open laterally into the neighboring spaces.

### 3.3.2 The Coburn–Winters Model

Transmission alone does not set the bottom flux. Molecules that reach the bottom react with probability β (the bottom reaction probability). Those that do not react bounce back into the trench and may return. Coburn and Winters showed that, for walls that do not consume the species, the ratio of bottom etch rate to open-area etch rate is:

```
ER_bottom / ER_open = K / (K + β (1 − K))

Reference line space with mask, A = 16.6 (K = 0.178):

  β        ER_bottom / ER_open
  ──────────────────────────────
  0.05     0.81
  0.10     0.68
  0.20     0.52
```

**The bottom reaction probability is the lever.** A trench whose bottom consumes every fifth halogen atom it sees starves at depth. A trench whose bottom consumes one in twenty is still fed at 80% of the open-area rate. The recipe sets β through the balance of ions (which activate the surface and raise β) and the passivating species (oxygen, which lowers it), and through pulsing (Chapter 6).

### 3.3.3 The Linear ARDE Form

For A ≫ 1, (1 − K)/K ≈ A/(ln A + 0.15), and the Coburn–Winters ratio takes the form used throughout this book:

```
ER / ER₀ = 1 / (1 + k A)          with k ≈ β / (ln A + 0.15) ≈ β / 3

  k = 0.058  ↔  β ≈ 0.17   (uncompensated HBr/O₂, continuous wave)
  k = 0.025  ↔  β ≈ 0.07   (reference recipe: pulsed, tuned passivation)
```

The coefficient k is measured directly from depth versus width at a fixed time and is the single most useful number for describing a recipe's ARDE (Appendix E.2).

### 3.3.4 Sidewall Consumption

If the walls consume the species (for example, by depositing passivation), the transmission falls further. Oxygen, which builds the SiOₓBrᵧ film on the sidewalls, is partly consumed on the way down. This is one reason the bottom of a deep trench can be less passivated than the top, and why the profile can change with depth (Chapter 10).

---

## 3.4 Ion Transport

### 3.4.1 Angular Spread and Direct Transmission

Ions leave the sheath with a small angular spread, set mainly by the ratio of ion temperature to sheath voltage. In a line space, only the spread across the slot matters. For a Gaussian spread of standard deviation σ_θ, the fraction of ions that reach the bottom without striking a sidewall is approximately:

```
K_i ≈ 1 − 0.80 A σ_θ          (σ_θ in radians; 0.80 ≈ √(2/π))

  σ_θ      A = 10     A = 16.6
  ────────────────────────────────
  1.0°     0.86       0.77
  1.5°     0.79       0.65
  2.0°     0.72       0.54
  3.0°     0.58       0.30
```

A spread of 1.5° (typical of a low-pressure ICP with a few hundred volts of bias) delivers about two thirds of the ions directly to the bottom of the finished reference trench. At 3°, less than a third arrive directly.

### 3.4.2 Grazing Reflection

Ions that hit a sidewall do so at grazing incidence, typically 85–89° from the wall normal. At such angles, most heavy ions reflect forward with a large fraction of their energy. Many of these reflected ions still reach the bottom, and they arrive near the bottom corners. This has two effects:

```
Effect                              Consequence
───────────────────────────────────────────────────────────────────
Reflected ions add to bottom flux   Ion transmission higher than K_i;
                                    weaker ion-driven ARDE
Reflected ions concentrate near     Faster etching at bottom corners
the bottom corners                  → microtrenching (Chapter 10)
Energy lost in reflection           Corner flux is lower-energy;
                                    may not clear passivation
```

### 3.4.3 Why Ion Transport Matters Less Than Neutral Transport Here

At A = 16.6 with σ_θ = 1.5°, the direct ion transmission is 0.65, and grazing reflection brings the effective value to roughly 0.75–0.85. The neutral ratio at the same aspect ratio with β = 0.17 is about 0.52. In the uncompensated recipe, the bottom is starved of neutrals before it is starved of ions. This is the basis of the main ARDE remedy: lower the bottom reaction probability so neutrals reach the bottom at a rate closer to the ions (Chapters 6, 7, and 12).

---

## 3.5 ARDE in the Reference Process

### 3.5.1 Time to Depth

The etch front in a trench of width S, with mask height h_m, advances at:

```
dz/dt = ER₀ / (1 + k (z + h_m) / S)

Integrating from z = 0:

t(z) = [ z + (k/S)(z²/2 + h_m z) ] / ER₀
```

```
Reference: ER₀ = 300 nm/min, h_m = 49 nm

Uncompensated chemistry, k = 0.058:

  Depth z    Rate ratio     t (S = 18)    t (S = 24)    t (S = 60)    t (open)
  (nm)       at S = 18      (s)           (s)           (s)           (s)
  ──────────────────────────────────────────────────────────────────────────────
  0          0.86           0             0             0             0
  100        0.68           26.4          24.8          21.9          20.0
  200        0.56           59.2          54.4          45.8          40.0
  250        0.51           78.0          71.0          58.4          50.0
  300        0.47           98.5          88.9          71.5          60.0

Reference recipe, k = 0.025:

  0          0.94           0             0             0             0
  100        0.83           22.8          22.1          20.8          20.0
  200        0.74           48.3          46.2          42.5          40.0
  250        0.71           62.1          59.1          53.6          50.0
  300        0.67           76.6          72.4          65.0          60.0
```

The rate ratio at z = 0 is below 1 because the mask already forms a short trench (A = 49/18 = 2.7) when the silicon etch begins.

### 3.5.2 Depths at the Cell End Time

Both recipes are timed to put the cell line spaces at 250 nm. The depths of the other features at that moment are:

```
                         Uncompensated       Reference
                         (k = 0.058,         (k = 0.025,
                         t = 78 s)           t = 62 s)
──────────────────────────────────────────────────────────────
Cell line space, 18 nm   250 nm              250 nm
Cut gap, 24 nm           270 nm              262 nm
Periphery, 60 nm         324 nm              287 nm
Periphery, 100 nm        346 nm              296 nm
Periphery, open (> 1 µm) 390 nm              310 nm

Periphery spec: 280–330 nm
```

With the uncompensated chemistry, the periphery is 60–140 nm too deep and the 100 nm trenches are out of specification by 16 nm. With the reference recipe, every periphery width lands inside the 280–330 nm window. **Reducing k from 0.058 to 0.025 is what makes a single-step isolation etch possible.** Chapter 12 develops this into a full depth-loading analysis and shows what to do when k cannot be lowered enough.

### 3.5.3 Sensitivity to Space Width

ARDE also turns small width differences into depth differences:

```
Reference recipe, t = 62.1 s:
  S = 16 nm → 244.8 nm
  S = 18 nm → 250.0 nm
  S = 20 nm → 254.4 nm
  ∂D/∂S ≈ 2.4 nm depth per nm of width

Uncompensated, t = 78.0 s:
  S = 16 nm → 241.5 nm
  S = 20 nm → 257.5 nm
  ∂D/∂S ≈ 4.0 nm per nm
```

This is the link between SAQP pitch walk (Chapter 2) and depth walk (Chapter 12).

### 3.5.4 Macroloading

The open-area rate ER₀ is itself not fixed. With about 60% of the wafer surface etching silicon (Chapter 2), halogen atoms are consumed faster than they are supplied, and ER₀ falls as the open fraction rises:

```
ER₀(f) = ER₀,ref × (1 + κ f_ref) / (1 + κ f)

Illustrative κ = 1.5, f_ref = 0.60:
  f = 0.55 → ER₀ rises by (1 + 0.90)/(1 + 0.825) − 1 = +4.1%
  f = 0.65 → ER₀ falls by 1 − (1.90/1.975) = −3.8%
```

A new product with 5% more open area etches about 4% slower, which at a fixed time costs about 10 nm of cell depth. Product-specific times, or feed-forward from the open fraction, handle this (Chapter 15).

---

## 3.6 Charging and Ion Deflection

### 3.6.1 Why Charging Is Weaker Than in Dielectric Etch

In dielectric etch, the trench bottom is an insulator and charges positive, slowing and deflecting the ions. In silicon trench etch, the bottom and the sidewalls of the trench are silicon, connected to the substrate and through it to the chuck. Charge does not accumulate on them. Only the hard mask (49 nm of oxide and nitride) can charge.

### 3.6.2 Electron Shading at the Mask

Electrons arrive with a nearly isotropic distribution and are blocked by the top of the mask. Ions arrive nearly vertically and pass between the mask lines. The mask sidewalls therefore charge negative near the top, and any difference between the two walls of a space creates a lateral field:

```
Deflection of an ion crossing a lateral field E⊥ over a length L,
with energy E_i:

  θ_defl ≈ q E⊥ L / (2 E_i)

Illustrative: 2 V difference across an 18 nm space, over the 49 nm
mask height, 150 eV ions:

  E⊥ = 2 V / 18 nm = 1.1×10⁸ V/m
  θ_defl ≈ (1.1×10⁸ × 49×10⁻⁹) / (2 × 150) = 5.4 / 300 = 0.018 rad ≈ 1.0°
```

A one-degree deflection is comparable to the whole sidewall-angle budget (Chapter 1). In a perfectly periodic array, the two walls of every space charge identically and the field cancels. It does not cancel where the symmetry breaks.

### 3.6.3 Where Symmetry Breaks

```
Location                           Asymmetry                  Effect
──────────────────────────────────────────────────────────────────────────────
Pitch-walked spaces (α/β/γ)        Different neighbor         Unequal sidewall
                                   spacing                    flux; fins lean
                                                              toward the wider
                                                              space during etch
Array edge (last active lines)     Dense on one side,         Tilted profile;
                                   open on the other          lean (Ch. 11)
Island ends and cut gaps           Local geometry changes     Rounded ends;
                                   in plan view               end pull-back
Wafer edge                         Sheath tilt (Chapter 9)    Whole-trench tilt
```

Pulsing helps: in the off phase of a pulsed plasma, electrons cool and the sheath collapses, and low-energy electrons and negative ions can reach the mask surfaces and neutralize them (Chapter 6).

---

## 3.7 Summary & Key Takeaways

1. **Silicon etch is ion-enhanced.** Halogen atoms and ions together etch at yields of about 1.6 Si per ion. The bottom etches; the sidewall, with few ions and a passivation film, does not.

2. **Transport is free-molecular.** The mean free path is about 8 mm, half a million times the trench width. Geometry and surface reaction probabilities decide what reaches the bottom.

3. **Slots feed better than holes.** At A = 16.6, a line space transmits 0.18 of incoming neutrals to the bottom by diffuse flight, against 0.074 for a hole.

4. **Bottom reaction probability sets ARDE.** In the Coburn–Winters model, lowering β from 0.17 to 0.07 lowers the ARDE coefficient k from 0.058 to 0.025.

5. **Lower k makes one-step isolation work.** At k = 0.025 the cell reaches 250 nm in 62 s while every periphery width stays within 280–330 nm. At k = 0.058 the wide periphery reaches 390 nm.

6. **Width differences become depth differences.** At k = 0.025, each nanometre of space width is worth 2.4 nm of depth.

7. **Charging is small but not zero.** Only the mask charges, but a 2 V asymmetry can deflect ions by a degree where the array's symmetry breaks.

---

## Study Questions

1. A recipe has J_i = 3.0 mA/cm² and an open-area silicon rate of 360 nm/min. Compute the effective yield. If the bromine density is 8×10¹³ cm⁻³, what is the halogen supply-to-demand ratio at the open surface?

2. Compute the neutral transmission of a slot at A = 12 and of a hole at A = 12. For β = 0.1, what is the Coburn–Winters bottom rate ratio for each?

3. A depth-versus-width test at a fixed time of 60 s gives 248 nm in 18 nm spaces and 300 nm in a wide open area. Assuming h_m = 49 nm and ER₀ = 300 nm/min, compute k. Is this recipe closer to the uncompensated or the reference chemistry?

4. For the reference recipe (k = 0.025), compute the time to 250 nm in an 18 nm space if the mask were 39 nm instead of 49 nm. What is the periphery open-area depth at that time?

5. For σ_θ = 2.0°, compute the direct ion transmission at the bottom of the reference trench. Using the series-resistance rate law of Section 3.1.3, explain qualitatively whether the trench would become more ion-limited or more neutral-limited as σ_θ grows.

6. A pitch-walked array has spaces of 15, 18.5, 20, and 18.5 nm. Using the reference recipe and t = 62.1 s, estimate the depth of each space with ∂D/∂S ≈ 2.4 nm/nm. What is the depth range?

---

**Next Chapter:** [Chapter 4: Silicon Etch Chemistries & Sidewall Passivation](./04-chemistry-passivation.md)

---

**Chapter 3 Development Status:** Complete  
**Version:** 1.0
