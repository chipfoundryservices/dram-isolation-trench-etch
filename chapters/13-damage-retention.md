# Chapter 13: Etch Damage, Contamination & Data Retention

## Overview

Every surface the isolation etch creates will be part of a DRAM cell. The sidewalls of each island end, near the top, become the depletion region of the storage-node junction: the one junction on the chip that must leak no more than a few femtoamperes, in the worst cell out of billions, at 85 °C. A single defect in the wrong place can make a cell leak ten times its budget. The plasma that cuts the trench also bombards, implants, and coats those surfaces.

This chapter connects the etch to retention. It starts with the physics of junction leakage and shows how a single trap can create a tail cell. It then describes what the plasma leaves in and on the silicon, how the clean, the liner oxidation, and the anneals remove it, and what each removal step costs in AA width. It ends with the measurements that tie etch changes to retention and with the principles of damage-aware recipe design.

**Learning Objectives:**
- List the leakage paths of a DRAM storage node and identify those the isolation etch influences
- Compute the generation current from a single deep-level trap and its field enhancement
- Estimate the number of interface traps and metal atoms near one storage-node junction
- Describe the damage, implanted species, and residues the plasma leaves on the sidewall and bottom
- Compute silicon consumption and AA-width loss in liner oxidation
- Explain how test structures and retention-tail measurements connect etch changes to cell leakage
- Apply damage-aware principles to recipe design

---

## 13.1 How a Cell Loses Its Charge

### 13.1.1 Leakage Paths

```
Path                                   Physics                         Etch influence
───────────────────────────────────────────────────────────────────────────────────────────
SN junction: bulk generation           SRH generation in the           Defects, metals, H in
(depletion region)                     depletion volume                the silicon near the
                                                                       sidewall
SN junction: surface generation        Interface traps at the          Sidewall damage and
(where the depletion region meets      liner–Si interface              roughness; residues;
the trench sidewall)                                                   liner quality
Trap-assisted tunneling (TAT)          Field-enhanced emission from    Field concentration at
                                       traps in high-field regions     bow, corners, rough
                                                                       spots
GIDL (gate-induced drain leakage)      Band-to-band tunneling under    AA profile near the
                                       the WL / passing WL edge        top; passing-WL
                                                                       distance
Access transistor subthreshold         Off-state current               Fin width at WL depth
                                                                       (Chapter 10)
Capacitor dielectric                   Tunneling through the high-k    None
```

Most cells leak far below their budget. The tail cells that set the refresh interval nearly always owe their leakage to a localized defect in or next to the junction depletion region, often at the trench sidewall.

### 13.1.2 Generation From a Single Trap

```
Shockley–Read–Hall generation from one mid-gap trap in a depleted region:
  Emission rate for each carrier: e = σ v_th n_i
  Net generation rate: g = e_n e_p / (e_n + e_p)  (= e/2 for a symmetric
                                                  mid-gap trap)

At 85 °C (358 K):
  n_i ≈ 4.4×10¹¹ cm⁻³   (≈ 44× its 300 K value)
  v_th ≈ 1.2×10⁷ cm/s
  σ ≈ 1×10⁻¹⁵ cm²
  e = 1×10⁻¹⁵ × 1.2×10⁷ × 4.4×10¹¹ ≈ 5.3×10³ s⁻¹
  g ≈ 2.6×10³ s⁻¹

Current from one trap: I = q g = 1.6×10⁻¹⁹ × 2.6×10³ ≈ 4×10⁻¹⁶ A = 0.4 fA
```

One mid-gap trap in a low-field part of the depletion region adds about 0.4 fA. That alone does not make a tail cell.

### 13.1.3 Field Enhancement

In high fields (above about 0.5 MV/cm), emission from a trap is enhanced by the Poole–Frenkel effect and by phonon-assisted tunneling. Enhancement factors of 10–100 are typical at 1 MV/cm:

```
Single trap at 1 MV/cm, enhancement ×30 (illustrative):
  I ≈ 0.4 fA × 30 ≈ 12 fA
Two such traps, or enhancement ×70:  ≈ 25–30 fA

Retention budget per cell (Chapter 1): ≈ 28 fA
```

**One or two traps in the high-field part of the junction can create a tail cell.** The high-field region of the storage-node junction is small, but it often meets the trench sidewall, especially at the top of the island end, where the junction is shallowest and the passing word line is closest.

### 13.1.4 How Many Traps Are Near Each Junction?

```
Sidewall area in the SN junction depletion band (one island end):
  Two side walls: 2 × 20 nm (along the line) × 60 nm (depth band)
                = 2400 nm²
  End wall:       14 nm × 60 nm = 840 nm²
  Total:          ≈ 3200 nm² = 3.2×10⁻¹¹ cm²

Interface traps (after liner and anneal), D_it ≈ 1×10¹⁰ cm⁻² eV⁻¹,
within ±0.1 eV of mid-gap (the efficient generators):
  N = D_it × 0.2 eV × A = 1×10¹⁰ × 0.2 × 3.2×10⁻¹¹ ≈ 0.064 per junction

If ≈ 10% of that area is high-field:
  ≈ 0.006 per junction → ≈ 6×10⁻³ of all cells carry one efficient
  trap in a high-field spot
```

The interface-trap density of the trench sidewall therefore sets the size of the population from which tail cells come. A factor-of-two increase in mid-gap D_it doubles it. The tail itself, typically 10⁻⁵ to 10⁻⁴ of cells at long refresh times, is the extreme end of this population (the highest fields and the most efficient traps).

### 13.1.5 Metals

```
Surface metal contamination of 1×10¹⁰ atoms/cm² on the sidewall:
  Atoms per junction area: 1×10¹⁰ × 3.2×10⁻¹¹ ≈ 0.32

Roughly one metal atom for every three storage-node junctions.
```

If even a fraction of these atoms diffuse into the silicon during the liner oxidation and end up as mid-gap centres in the depletion region (Fe, Ni, Cr, and others), they add to the trap population at a rate comparable to the interface traps. This is why the metal limits of Chapter 9 are as low as they are, and why gettering by the substrate is an important part of the DRAM front end.

---

## 13.2 What the Plasma Leaves Behind

### 13.2.1 At the Trench Bottom

```
Modification                      Depth (150 eV ions)       Fate
─────────────────────────────────────────────────────────────────────────────
Displacement damage (amorphized   2–3 nm                    Partly consumed by
or heavily damaged layer)                                   liner; rest annealed
Br incorporation                  1–2 nm                    Consumed by liner
H incorporation (from HBr)        5–20 nm                   Out-diffuses at
                                                            ≥ 700–800 °C
Microtrench corners (periphery)   Local                     Stress concentrator
                                                            (Chapter 10)
```

The bottom takes the full ion dose, but it is covered by thick fill oxide and lies 150 nm or more below the storage-node junction. Bottom damage matters mainly for periphery isolation leakage and for dislocation nucleation at sharp corners.

### 13.2.2 On the Sidewalls

```
Modification                      Source                    Depth / amount
─────────────────────────────────────────────────────────────────────────────
Light displacement damage         Off-angle and collided     ≈ 0.5–1 nm
                                  ions (Chapter 6);
                                  reflected ions
SiOₓBrᵧ passivation film          Product redeposition       1–3 nm (removed by
                                                             clean)
Br at the Si / film interface     Film formation             Fraction of a
                                                             monolayer to ≈ 1 nm
H in silicon                      H⁺ and H atoms from HBr    Several nm; B–H
                                                             complexes deactivate
                                                             p-type dopant near
                                                             the surface
Roughness, striations             Mask LER transfer;         0.3–1 nm rms
                                  step transitions
Carbon, fluorine                  Breakthrough               Top 20–30 nm of the
                                                             wall
UV / VUV exposure                 Plasma emission            Charge and defects
                                                             in the pad oxide and
                                                             later in the liner
                                                             interface
```

The sidewalls receive far fewer and less energetic ions than the bottom, but they carry the junction. What matters for retention is the residual damage after the liner and anneals, at the top 100 nm of the island ends.

### 13.2.3 Hydrogen and the Well Doping

In many flows the wells are implanted after the isolation module, but in some they precede it, and the channel-stop doping near the sidewall can be introduced early. Hydrogen from HBr diffuses several nanometres into the silicon and forms neutral complexes with boron acceptors. Until it is driven out by an anneal, it reduces the effective p-type doping near the sidewall, which changes the junction field profile and the parasitic-channel threshold under the passing word line. Liner oxidation at 800–1000 °C removes most of it.

---

## 13.3 Removing the Damage

### 13.3.1 The Sequence

```
Step                            Removes                           Cost
──────────────────────────────────────────────────────────────────────────────────
Dilute HF                       SiOₓBrᵧ film; chemical oxide      Pad-oxide undercut;
                                                                  cap loss (Ch. 4)
SC1 / ozonated water            Particles, organics; thin         Si loss ≈ 0.2–0.5 nm
                                chemical oxide                    per side (SC1)
IPA dry                         —                                 Collapse risk
                                                                  (Chapter 11)
Liner oxidation (radical,       Consumes 0.44 t_ox of Si:         AA width
ISSG or plasma, 800–1000 °C)    damaged and Br-rich layer;
                                rounds corners; out-diffuses H
Fill anneal                     Further anneal of residual        Thermal budget
                                damage; H out-diffusion
```

### 13.3.2 Silicon Consumption

```
Thermal oxidation consumes 0.44 nm of Si per nm of oxide grown.

  Liner t_ox    Si consumed per side    AA width after liner (top)
  ────────────────────────────────────────────────────────────────────
  1.5 nm        0.66 nm                 14.0 − 1.3 = 12.7 nm
  2.5 nm (ref)  1.10 nm                 14.0 − 2.2 = 11.8 nm
  4.0 nm        1.76 nm                 14.0 − 3.5 = 10.5 nm

  (plus SC1 loss: −0.4 to −1.0 nm on the width)
```

The reference liner removes about 1.1 nm of silicon from each sidewall, which is more than the sidewall damage depth (≈ 0.5–1 nm) and about the depth of the bromine-rich layer. It does not reach the full depth of hydrogen, which is removed by diffusion during the oxidation and later anneals instead.

### 13.3.3 The Width Trade-Off

```
Liner thicker by 1 nm:
  + removes 0.44 nm more Si per side (more margin on residual damage)
  + more corner rounding
  − AA width −0.88 nm at every depth (contacts, saddle fin)
  − trench bottom narrower by the oxide growth (fill margin, Ch. 10)
  − more oxidation-induced stress in the narrow fin

Etch damage 0.5 nm shallower (lower ion energy at the sidewall):
  lets the liner be ≈ 1 nm thinner for the same residual damage
  → recovers ≈ 0.9 nm of AA width
```

This is the central trade-off of the module. **Every nanometre of damage the etch avoids is worth almost a nanometre of AA width**, because it allows a thinner liner. Damage-aware etch is therefore not only a retention measure but also a dimensional one.

### 13.3.4 Corners

Radical oxidation grows at nearly the same rate on all crystal planes and on convex corners, so it rounds the top corners of the island (Chapter 10) without the thinning at corners typical of conventional dry oxidation. Rounded, uniformly oxidized corners lower the local field at the top of the junction, which reduces both trap-assisted tunneling and GIDL. Sharp or microtrenched corners at the bottom are less important for retention but are stress concentrators where dislocations can nucleate during later anneals, and a dislocation that crosses a junction leaks heavily.

---

## 13.4 Measuring the Link

### 13.4.1 Test Structures

```
Structure                           What it isolates                     Etch sensitivity
─────────────────────────────────────────────────────────────────────────────────────────────
Large-area diodes with different    Area (bottom/bulk) vs. perimeter      Perimeter term
perimeter-to-area ratios            (trench sidewall) leakage:            reflects sidewall
(same total area)                   I = J_A A + J_P P                     damage and liner
                                                                          quality
Array-like diode (cell AA layout,   Sidewall leakage in the real          High
all islands in parallel)            geometry
Gated diodes                        Surface generation vs. bulk;          Interface traps
                                    interface trap density                (D_it)
Charge-pumping on array-like        D_it at the sidewall                  High
transistors
Retention test arrays               Retention tail directly               Highest; slowest
```

### 13.4.2 Extracting the Sidewall Term

```
Two diodes, same area A = 1×10⁴ µm², at 85 °C, reverse bias 1.5 V:
  Diode 1: perimeter P₁ = 400 µm     I₁ = 2.6 pA
  Diode 2: perimeter P₂ = 20,000 µm  I₂ = 12.4 pA (array-like islands)

  J_P = (I₂ − I₁) / (P₂ − P₁) = 9.8 pA / 19,600 µm = 0.50 fA/µm
  J_A A = I₁ − J_P P₁ = 2.6 − 0.2 = 2.4 pA

Per cell, sidewall perimeter of one junction ≈ 2 × 20 nm + 14 nm ≈ 0.054 µm:
  Average sidewall leakage per junction ≈ 0.50 × 0.054 ≈ 0.027 fA
  (far below the 28 fA budget; the tail is set by rare defects, not by
  the average)
```

The average perimeter leakage is a sensitive, fast indicator of sidewall quality. A recipe change that doubles J_P will usually raise the retention tail, even though the average leakage per cell is tiny. Test-structure data correlate with the tail but do not replace retention testing.

### 13.4.3 The Retention Tail

```
Cumulative fail-bit count vs. refresh time (85 °C), illustrative:

  Fail bits     │                                      ╱ new recipe
  per 16 Gb     │                                ╱   ╱
     10⁴        │                           ╱   ╱
     10³        │                      ╱   ╱ reference
     10²        │                 ╱   ╱
     10¹        │            ╱   ╱
                └──────────────────────────────────────
                     64 ms   128   256   512   1024 ms

A shift of the tail to the left by a factor of 2 in time at a fixed
fail count means the cells with the worst defects now leak twice as
fast, or there are many more of them.
```

The tail is measured at probe, on full dies, weeks after the etch. Etch changes are therefore screened first by test structures and qualified finally by retention testing on product.

---

## 13.5 Damage-Aware Recipe Design

```
Principle                                  Implementation
─────────────────────────────────────────────────────────────────────────────
Lowest ion energy that keeps the bottom    ≈ 140–150 eV main etch; 60 eV
clear                                      profile step at the end
Narrow IED, no high-energy tail            13.56 MHz or higher bias; tailored
                                           waveforms (Chapter 6)
Fewer off-angle ions on the sidewall       Low pressure in ME-1 (upper wall,
near the junction                          where the junction sits)
Pulsing                                    Lower average energy dose; charge
                                           relief; less sidewall bombardment
Limit hydrogen where possible              Cl₂-rich ME-1 (top of the trench);
                                           HBr where selectivity needs it
Clean breakthrough                         Short; low C and F residue
End with a low-damage step                 Profile step removes or does not add
                                           damage at the bottom
Metals and particles                       Chamber condition, gas-line moisture
                                           control (Chapter 9)
```

The most important principle is placement: the top 100 nm of the island ends carry the junction, so the upper part of the trench, etched in ME-1, deserves the most care. Damage near the bottom matters less for retention and can be traded for profile control there.

---

## 13.6 Summary & Key Takeaways

1. **Tail cells come from single defects.** One mid-gap trap gives about 0.4 fA at 85 °C; field enhancement at 1 MV/cm can raise it to tens of femtoamperes, comparable to the 28 fA budget.

2. **The sidewall is the junction.** About 3200 nm² of sidewall lies in each storage-node junction's depletion band. At D_it = 10¹⁰ cm⁻² eV⁻¹, roughly 6% of junctions carry an efficient interface trap.

3. **Metals at 10¹⁰ atoms/cm² mean one atom per three junctions.** Metal control is a retention requirement, not only a cleanliness requirement.

4. **The plasma leaves layers.** Displacement damage, Br, H, the SiOₓBrᵧ film, roughness, and breakthrough residue, deepest at the bottom and lightest, but most important, on the upper sidewalls.

5. **The liner removes damage by consuming width.** A 2.5 nm liner consumes 1.1 nm per side; each nanometre of damage the etch avoids saves almost a nanometre of AA width.

6. **Measure with perimeter structures, qualify with the tail.** Perimeter-to-area diode sets give fast sidewall leakage data. The retention tail at probe is the final judge.

---

## Study Questions

1. Compute the generation current from a single mid-gap trap at 95 °C (n_i ≈ 7.5×10¹¹ cm⁻³, v_th ≈ 1.2×10⁷ cm/s, σ = 2×10⁻¹⁵ cm²). With a field enhancement of 20, how does it compare with the 28 fA budget?

2. A new node shortens the junction depth band to 50 nm and the island-end segment to 18 nm on each side, with W_t = 12 nm. Compute the sidewall area per junction. At D_it = 1.5×10¹⁰ cm⁻² eV⁻¹ (±0.1 eV), how many efficient traps per junction are expected?

3. A process engineer proposes a 3.5 nm liner to reduce the retention tail. Compute the AA width after the liner (top, 140 nm, and bottom) for the reference profile, and the change in trench bottom width. Which specifications in Chapter 1 are at risk?

4. Perimeter-to-area diode data after an etch change give J_P = 0.85 fA/µm (reference 0.50). Estimate the change in average sidewall leakage per junction. Why might the retention tail change by more than this ratio?

5. A chamber shows Fe at 3×10¹⁰ atoms/cm² on monitor wafers after a gas-line repair. Estimate the Fe atoms per junction area. What actions would you take before releasing the chamber?

6. Explain why lowering hydrogen in ME-1 might improve retention more than lowering it in ME-2, using the depth position of the storage-node junction.

---

**Next Chapter:** [Chapter 14: Advanced Schemes — Dual-Depth Isolation, EUV AA, 4F² & 3D DRAM](./14-advanced-isolation-schemes.md)

---

**Chapter 13 Development Status:** Complete  
**Version:** 1.0
