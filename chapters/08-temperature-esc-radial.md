# Chapter 8: Wafer Temperature, Electrostatic Chucks & Radial Control

## Overview

In the isolation etch, wafer temperature is a passivation knob. The sticking of etch products on the sidewalls, the oxidation of those products into SiOₓBrᵧ, and the spontaneous reaction of bromine and chlorine with silicon all depend on temperature. A few degrees move the sidewall angle and the AA width at word-line depth measurably. Because the electrostatic chuck can hold different temperatures in different radial zones, temperature is also the most precise radial knob for AA width.

This chapter quantifies how temperature affects the profile, computes the heat balance and thermal time constants that decide how well the wafer follows the chuck, describes multi-zone chucks and their use for radial tuning, and covers chucking, dechucking, and the edge region.

**Learning Objectives:**
- Explain the temperature dependence of passivation, lateral etch, and selectivity
- Use sensitivity coefficients to predict angle and AA width changes from temperature
- Compute the wafer-to-chuck temperature rise and the thermal time constant
- Describe multi-zone ESC design and how zone temperatures map to radial profile
- Explain chucking, helium backside cooling, and dechuck failure modes
- Size temperature transients in a short recipe

---

## 8.1 Temperature as a Passivation Knob

### 8.1.1 Mechanisms

```
Process                              Effect of higher wafer temperature
──────────────────────────────────────────────────────────────────────────────
Sticking of SiBrₓ products on walls  Lower (desorption activated) → thinner film
Oxidation of adsorbed products       Faster, but less product to oxidize → film
                                     thinner overall in the 30–80 °C range
Spontaneous Br/Cl etch of Si         Faster (activated, E_a ≈ 0.1–0.4 eV for Cl
                                     on doped Si); small at 50 °C for Br
Mask selectivity                     Slightly lower (oxide etch less affected
                                     than Si; Si gains more)
```

The net effect in the 30–80 °C range is that **a warmer wafer passivates less**. The sidewall angle falls, the AA narrows at depth, and, at the limit, the upper sidewall bows.

### 8.1.2 Sensitivities

```
Reference ME-2, around 50 °C (illustrative):

  Output                          Sensitivity
  ────────────────────────────────────────────────────────
  Sidewall angle α                −0.010 ° per °C
  AA top width W_t                −0.04 nm per °C
  AA width at 140 nm, W(140)      −0.09 nm per °C
      (top CD: −0.04; angle: 2 × 140 × tan 0.010° = −0.05)
  Cell depth                      +0.3 nm per °C
  Bow (max width − top width)     +0.05 nm per °C
```

A 2 °C difference between two regions of the wafer moves W(140) by about 0.2 nm, which is 13% of the ±1.5 nm (3σ) tolerance in the specification sheet (Chapter 1). Temperature non-uniformity of ±1 °C is therefore a meaningful part of the AA width budget.

### 8.1.3 Why the Cell Is More Sensitive Than the Periphery

The film in an 18 nm trench comes mostly from the trench's own products, and these products hit the walls many times before escaping (Chapter 4). A small change in sticking probability changes the film many times over. In a wide periphery trench, products escape after few wall hits. The cell sidewall angle moves two to four times more per degree than the periphery angle.

---

## 8.2 Heat Balance

### 8.2.1 Wafer-to-Chuck Temperature Rise

```
Heat flux into the wafer during ME-1 (Chapter 5):  q ≈ 0.41 W/cm²

Thermal resistance between wafer and chuck surface (He backside,
10–15 Torr, contact plus gas conduction):          R ≈ 1.5 K·cm²/W

Wafer rise above the chuck surface:  ΔT = q R = 0.41 × 1.5 ≈ 0.6 °C

Ceramic puck (bonded to a cooled base), ΔT across the puck and bond:
  R_puck ≈ 3–5 K·cm²/W → 1.2–2.1 °C at the same flux, absorbed by the
  base temperature control and zone heaters
```

### 8.2.2 Time Constants

```
Wafer (775 µm Si):
  heat capacity per area C_w = ρ c_p t = 2330 × 700 × 775×10⁻⁶
                             = 1.26 kJ/(m²·K) = 0.126 J/(cm²·K)
  τ_w = C_w R = 0.126 × 1.5 ≈ 0.19 s

Puck surface (top few mm of ceramic): τ_p ≈ 2–10 s
Base / coolant loop: τ_b ≈ 30–120 s
```

The wafer follows the chuck surface within a fraction of a second. The chuck surface itself takes several seconds to respond to a change in heat load, and the zone heaters take longer still. In a recipe whose main etch lasts 62 s, the first 5–10 s after plasma ignition see the puck surface warming toward its steady state.

### 8.2.3 The Ignition Transient

```
At plasma on, heat flux jumps from 0 to 0.41 W/cm²:
  Steady rise of the puck surface above its pre-plasma value:
    ΔT_p ≈ q × R_puck ≈ 0.41 × 4 ≈ 1.6 °C (before heater compensation)
  Time to 63% of the rise: τ_p ≈ 5 s

Effect on the profile:
  For the first ≈ 5–10 s (top 20–40 nm of the trench), the wafer is
  1–1.5 °C cooler than during the rest of ME-1 → slightly more
  passivation, ≈ +0.01–0.015° of angle in that segment

  Small, but systematic: the top of the trench is always etched cold
```

Some tools pre-heat the puck surface with a feed-forward offset in the zone heaters before plasma ignition to cancel this transient. Others accept it, because the top 40 nm of the trench is above the region where AA width is most critical.

### 8.2.4 Step Changes in Heat Load

The ME-1 → ME-2 transition lowers the bias power from 450 W at 50% duty to 380 W at 40% duty, a 32% drop in average ion power. The wafer cools by about 0.2 °C over the following few seconds. Recipes with larger bias changes between steps see correspondingly larger temperature steps, and these appear as small angle changes at the step boundary, adding to the step mark discussed in Chapter 7.

---

## 8.3 Multi-Zone Chucks

### 8.3.1 Zone Layouts

```
Generation               Zones                      Use
─────────────────────────────────────────────────────────────────────────────
Dual-zone                Center, edge               Center-to-edge CD
Four-zone (radial)       Center, middle, outer,     Radial CD and angle
                         extreme edge               profiles; edge roll-off
Many-zone (radial and    Tens to 100+ heater        Azimuthal and local
azimuthal)               pixels                     correction; chamber
                                                    asymmetry
```

Each zone has a heater embedded in the ceramic, above a common cooled base. The heaters can only add heat. The base runs colder than the coldest zone setpoint, and each zone is held at its setpoint by its own heater power.

### 8.3.2 From Zone Temperature to Radial Profile

```
Reference: W(140) sensitivity −0.09 nm/°C (Section 8.1.2)

Measured W(140) radial profile (r = 0, 75, 120, 145 mm):
  18.9, 18.8, 18.5, 19.4 nm    (target 18.9 everywhere)

Required corrections:
  r = 75 mm:   +0.1 nm → zone −1.1 °C
  r = 120 mm:  +0.4 nm → zone −4.4 °C
  r = 145 mm:  −0.5 nm → zone +5.6 °C

Check side effects on depth (+0.3 nm/°C):
  r = 120 mm:  −1.3 nm;  r = 145 mm: +1.7 nm   → acceptable
```

Zones are coupled: each heater warms its neighbors, and the temperature profile between zones is smooth, not stepped. Production tuning uses a measured transfer matrix (the response of each radial position to each zone) rather than one-to-one assignment (Appendix C).

### 8.3.3 Azimuthal Non-Uniformity

Pumping ports, the wafer-transfer slot, gas injectors, and coil terminations can make the chamber slightly asymmetric. The result is an azimuthal variation in depth or AA width, typically ±0.5–1% of depth or ±0.2 nm of width. Chucks with azimuthal heater pixels can compensate the width part of this signature. Depth asymmetries are usually traced to hardware (coil, liner, or pumping) and fixed there.

---

## 8.4 Chucking and Backside Helium

### 8.4.1 Chucking Force

```
Coulombic ESC: P_e = ε₀ ε_r² V² / (2 d²)    (dielectric thickness d)

Johnsen–Rahbek (JR) ESC: higher force at lower voltage, through a
  slightly conductive dielectric; most conductor-etch chucks are JR type

Required: P_e > He backside pressure (10–15 Torr ≈ 1.3–2.0 kPa) with
          margin for wafer bow and edge lift
```

Front-end wafers at the isolation step are essentially flat (bow below 20 µm), so chucking is less critical than at later steps with thick films. The usual failure modes are particles on the backside, which locally lift the wafer and create a hot spot, and residual charge at dechuck.

### 8.4.2 Helium Leak as a Monitor

The backside helium flow needed to hold the setpoint pressure is a sensitive monitor of wafer seating. A rise in leak rate means the wafer is not fully seated somewhere, which means that region runs hotter, passivates less, and produces narrower AAs at depth. Helium leak rate is a standard fault-detection signal (Chapter 15).

### 8.4.3 Dechucking

After the plasma ends, residual charge in the dielectric holds the wafer. Lifting the wafer before the charge has dissipated can make it jump or slide, which breaks wafers and, more commonly, generates particles. Dechuck sequences use a short low-power plasma to provide a discharge path, reverse-polarity voltage, and monitored lift-pin force.

---

## 8.5 The Wafer Edge

The outermost 5–10 mm of the wafer sees a different thermal environment:

```
Factor                                      Effect at the edge
──────────────────────────────────────────────────────────────────────
Wafer overhangs the chuck by ≈ 1–2 mm       No backside contact → hotter
Edge ring absorbs ion power, heats up       Radiates to the wafer edge;
                                            ring temperature drifts with
                                            RF hours
Ring and wafer edge share gas-phase         Local product and O₂ balance
products                                    differs
```

The edge ring itself may be temperature-controlled or thermally coupled to the chuck, but its temperature rises during the recipe and from wafer to wafer in a lot until it reaches a steady state. A cold ring at the start of a lot is one cause of the first-wafer effect at the edge (Chapter 9).

---

## 8.6 Low-Temperature Silicon Etch

Cryogenic silicon etch (wafer below −80 °C, SF₆/O₂ chemistry) gives very high rates and smooth, vertical walls in deep silicon trenches, because a thin SiOₓF_y film forms on the sidewalls only at low temperature. It is used in MEMS and for some very deep silicon features. For the DRAM isolation etch it offers little: the trench is shallow, the rate is not limiting, and fluorine-based cryogenic etch gives worse selectivity to the thin oxide mask and a higher risk of lateral etch in 18 nm spaces. Moderately low wafer temperatures (0–20 °C) with HBr chemistry are used in some recipes to strengthen passivation without changing gases. Chapter 14 returns to temperature for the high-aspect-ratio isolation of 3D DRAM.

---

## 8.7 Summary & Key Takeaways

1. **Warmer means less passivation.** Around 50 °C, each degree reduces the angle by about 0.01° and narrows W(140) by about 0.09 nm.

2. **The cell is the sensitive feature.** Self-passivating narrow trenches respond two to four times more strongly to temperature than wide periphery trenches.

3. **The wafer follows the chuck.** The wafer runs about 0.6 °C above the chuck surface with a time constant of 0.2 s. The chuck surface has a time constant of several seconds, so the top of the trench is always etched slightly cold.

4. **Zones tune width radially.** A measured transfer matrix maps zone temperatures to the W(140) radial profile. Depth side effects (+0.3 nm/°C) are usually acceptable.

5. **Helium leak watches the seating.** A poorly seated region runs hot and produces narrow AAs. Leak rate is a key fault-detection signal.

6. **The edge is its own thermal region.** Overhang, ring heating, and ring drift make the outer 5–10 mm behave differently and change through a lot.

---

## Study Questions

1. A chamber's chuck is found to run 3 °C warmer than its setpoint in the middle zone. Predict the change in angle, W_t, W(140), and cell depth in that zone.

2. Compute the wafer temperature rise above the chuck surface during ME-2 if the heat flux is 0.30 W/cm² and the helium pressure is lowered so that R rises to 2.2 K·cm²/W. What does this do to the AA width at 140 nm?

3. A radial W(140) profile reads 19.2, 19.0, 18.8, 18.6 nm at r = 0, 75, 120, 145 mm. Assuming one-to-one zones with −0.09 nm/°C, compute the zone corrections to bring every point to 18.9 nm, and the resulting depth changes.

4. Explain why a backside particle under the wafer at r = 100 mm appears as a local spot of narrow AA width rather than a change in depth. What other signal would confirm it?

5. The edge ring temperature rises by 15 °C over the first five wafers of a lot. Describe the expected trend in edge AA width and edge angle across those wafers, and two ways to remove it.

---

**Next Chapter:** [Chapter 9: Chamber Walls, Edge Control & Contamination](./09-walls-edge-contamination.md)

---

**Chapter 8 Development Status:** Complete  
**Version:** 1.0
