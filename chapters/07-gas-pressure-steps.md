# Chapter 7: Gas Delivery, Pressure & Multi-Step Recipe Design

## Overview

The isolation etch takes about a minute of plasma time, yet it is rarely a single step. The trench at 30 nm depth and the trench at 230 nm depth have different aspect ratios, different passivation demands, and different sensitivities to every knob. A recipe that is right for the top is wrong for the bottom. Production recipes therefore divide the etch into steps and sometimes ramp parameters continuously within a step.

This chapter treats pressure, flow, and gas ratios as separate knobs, explains the architecture of the reference recipe and the reasoning behind each step, describes step transitions and gas-arrival delays, introduces cyclic and quasi-atomic-layer variants, and closes with radial gas tuning and the depth-series method used to develop and maintain the recipe.

**Learning Objectives:**
- Separate the effects of pressure, total flow, and gas ratios on rate, ARDE, and profile
- Explain the purpose of each step in the reference recipe and where each step boundary belongs
- Compute gas-line and chamber exchange times at step transitions
- Evaluate cyclic and quasi-ALE variants against throughput
- Use center/edge gas injection and coil ratio to tune radial uniformity
- Plan and interpret a depth series to extract k and α(z)

---

## 7.1 Pressure

### 7.1.1 What Pressure Changes

```
Raising pressure from 5 to 20 mTorr at fixed powers and flow ratios:

Quantity                     Direction        Mechanism
──────────────────────────────────────────────────────────────────────────────
Radical density              ↑ (≈ linear)     More gas to dissociate
Ion flux                     ≈ flat to ↓      Higher collisional losses;
                                              lower T_e
Neutral-to-ion ratio R       ↑                Both of the above
Bottom reaction prob. β      ↓                Higher coverage (Chapter 6)
ARDE coefficient k           ↓ (often)        Lower β
Ion angular spread           ↑                More sheath collisions
Sheath ion energy            ↓ slightly       Collisional energy loss
Residence time (fixed flow)  ↑                τ = pV/Q
Product redeposition         ↑                Longer τ, higher product density
Sidewall passivation         ↑                More products and O
```

Pressure is therefore not a single knob. Raising it lowers ARDE through coverage, but broadens the ion angles and thickens the passivation, which can cost taper and bow. The reference recipe uses 8 mTorr in ME-1, where profile matters and ARDE is still small, and 12 mTorr in ME-2, where ARDE matters most.

### 7.1.2 Pressure and the Cell/Periphery Balance

```
Illustrative response at 62 s (reference otherwise):

  ME-2 pressure    k        Cell depth    Peri (open)   Cell α
  ──────────────────────────────────────────────────────────────
  8 mTorr          0.032    244 nm        317 nm        0.9°
  12 mTorr (ref)   0.025    250 nm        310 nm        1.0°
  16 mTorr         0.020    253 nm        303 nm        1.2°
  20 mTorr         0.017    255 nm        298 nm        1.4°
```

Each step up in pressure brings the periphery closer to the cell, but the sidewall angle grows. At 20 mTorr the angle would close the trench bottom to 5–6 nm, below the fill limit (Chapter 10).

---

## 7.2 Flow and Ratios as Separate Knobs

### 7.2.1 Total Flow at Fixed Pressure

```
Total flow changes the residence time and the etch-product fraction
(Chapter 5), without changing pressure:

  ME-2 total flow      τ (ms)    Product fraction    Effect
  ────────────────────────────────────────────────────────────────────
  250 sccm             160       ≈ 8%                More passivation; taper;
                                                     loading sensitivity
  351 sccm (ref)       115       ≈ 6%
  600 sccm             67        ≈ 3.5%              Thinner film; risk of bow;
                                                     more gas, pump at limit
```

Flow is the cleanest way to move product redeposition without moving the plasma. It is limited by the pump: doubling flow at fixed pressure needs double the pumping speed.

### 7.2.2 Ratios

```
Ratio                    Main effect                         Sensitivity (illustrative)
───────────────────────────────────────────────────────────────────────────────────────────────
O₂ / HBr                 Passivation thickness → angle,      +1 sccm O₂ (of 220 HBr):
                         AA width at depth                   α +0.25°, W(140) +1.2 nm
Cl₂ / (HBr + Cl₂)        Rate, smoothness; lateral etch      +10% Cl₂: ER₀ +8%;
                                                             top CD −0.2 nm/side
NF₃ / HBr                Thins passivation; clears bottom    +1 sccm NF₃: α −0.15°,
                                                             W(140) −0.7 nm; S_ox −3
He dilution              Lower radical density; shorter τ;   +50 sccm He: ER₀ −4%,
                         smoother plasma                     k −0.002
```

Because the cell is far more sensitive to passivation than the periphery (Chapter 4), the O₂ and NF₃ flows are the most tightly controlled flows in the recipe. Mass-flow controllers for these gases are low-range (10–20 sccm full scale) units, calibrated more often than the main-gas MFCs.

---

## 7.3 Recipe Architecture

### 7.3.1 The Reference Steps

```
Depth profile of the reference recipe (cell line space):

  Si surface ─┬─  0 nm      BT     (8 s)   native oxide; ≈ 3 nm Si recess
              │
              │             ME-1   (30 s)  Cl₂-assisted, 8 mTorr, 50% duty
              │                            vertical walls below the mask;
              │                            rate while A is low
              ├─ ≈ 120 nm   ─── step boundary ───
              │
              │             ME-2   (32 s)  no Cl₂, +O₂, small NF₃, 12 mTorr,
              │                            40% duty; low ARDE; angle hold
              │
              ├─ ≈ 245 nm   PS     (6 s)   low-bias HBr/He; bottom rounding;
              │                            ≈ 5 nm more depth
  Bottom    ──┴─ 250 nm
```

### 7.3.2 Why the Boundary Is Near 120 nm

```
Criteria for the ME-1 → ME-2 switch:

1. Above the switch, the profile must be vertical just below the mask,
   where bow forms (Chapter 10). Cl₂ and higher energy keep this region
   straight without excess film.

2. Below the switch, the aspect ratio exceeds ≈ 9 (with mask:
   (120 + 49) / 18 = 9.4). Here the CW-like ME-1 chemistry would starve
   the bottom, and ARDE begins to dominate the cell/periphery balance.

3. The switch must sit above the word-line depth (140–180 nm), so that
   any profile kink at the transition does not fall in the saddle-fin
   region where AA width is a transistor parameter.
```

The third criterion is specific to DRAM. **Step transitions leave marks on the sidewall**: a small change in angle or a slight notch where the passivation balance changes. A mark at 160 nm would put a width step inside the saddle fin. A mark at 120 nm is above it and is later partly covered by the word-line recess.

### 7.3.3 The Profile Step

The final step uses low bias, no oxygen, and high helium dilution. With little energy and no new film, it removes a few nanometres from the bottom corners where passivation has accumulated, rounding the V-shaped bottom of the narrow cell trenches and the square corners of the periphery trenches. Rounded bottom corners reduce stress concentration and field enhancement after fill and make the liner oxidation more uniform (Chapter 10). The step adds only about 5 nm of depth and is included in the main-etch calibration.

---

## 7.4 Step Transitions

### 7.4.1 Gas-Arrival Delay

When a step changes gases, the new mixture must travel from the MFCs to the chamber and replace the old gas:

```
Gas line from the final valve to the chamber:
  Volume V_line ≈ 50 cm³ at the line pressure (≈ 10–30 Torr)
  Flow of a minor gas: NF₃ 3 sccm

  Delay to fill the line with the new composition:
    t_line ≈ V_line × p_line / (Q × 760 Torr) 
           = 50 cm³ × 20 Torr / (3 cm³/min × 760 Torr)
           = 0.44 min ≈ 26 s   (for a dedicated low-flow line)

  With a carrier (minor gas merged into the 220 sccm HBr line):
    t_line ≈ 50 × 20 / (223 × 760) min ≈ 0.35 s
```

A minor gas delivered alone through a long line arrives tens of seconds late. That is half the length of ME-2. Recipes avoid this by merging minor gases into a high-flow carrier, by pre-flowing to a divert line before the step, or by keeping the gas flowing (at a low level) through the preceding step.

### 7.4.2 Chamber Exchange

```
Chamber gas exchange: three residence times for ≈ 95% replacement
  ME-2: τ ≈ 0.11 s → ≈ 0.35 s

Throttle-valve settling for a pressure change (8 → 12 mTorr): 1–3 s
```

Pressure changes take longer than gas changes. A plasma-on transition between steps of different pressure gives a second or two of intermediate conditions. The reference recipe keeps the plasma on across the ME-1 → ME-2 transition to avoid re-ignition transients and absorbs the settling time into the step calibration.

### 7.4.3 Ramps

Instead of a single step boundary, some recipes ramp O₂, bias, or pressure linearly through the main etch. Ramps avoid sidewall marks and let the passivation follow the aspect ratio continuously. Their disadvantages are that every intermediate condition must be robust, and that a drift in one endpoint of the ramp changes the whole profile.

---

## 7.5 Cyclic and Quasi-Atomic-Layer Variants

### 7.5.1 Silicon ALE

In atomic layer etching, the surface is first chlorinated (Cl₂ adsorption, no ions), then the chlorinated layer is removed by low-energy ions (Ar⁺, ≈ 50 eV) that cannot etch bare silicon. Each cycle removes about 0.5 nm, independent of aspect ratio, with very little damage.

```
Throughput for the whole trench by ALE:
  250 nm / 0.5 nm per cycle = 500 cycles
  Cycle time (adsorb, purge, remove, purge): ≈ 2 s
  Total ≈ 1000 s ≈ 17 min per wafer

Fleet impact: chamber cycle rises from 166 s to ≈ 1100 s → ≈ 6.6×
the chambers
```

True ALE is far too slow for the full trench. It is used, if at all, for the last few nanometres (bottom shaping) or for the breakthrough.

### 7.5.2 Quasi-ALE by Gas or Power Pulsing

Faster cyclic schemes alternate a passivation phase (O₂-rich, low bias, or a deposition gas) with an etch phase (halogen, higher bias) on a timescale of 0.2–2 s:

```
Phase              Duration     Purpose
─────────────────────────────────────────────────────────────────
Passivation        0.3 s        Build film on sidewalls; saturate bottom
Etch               0.7 s        Remove bottom film; etch ≈ 3 nm of Si
Cycle              1.0 s        ≈ 3 nm per cycle (illustrative)
```

Separating the phases decouples the sidewall film from the bottom etch and can lower ARDE below what continuous pulsing achieves. It costs time (transitions are limited by the gas exchange of Section 7.4) and leaves a scalloped sidewall with a period equal to the etch per cycle. In an 18 nm trench, a scallop amplitude of even 0.5 nm per side is noticeable. RF multi-level pulsing (Chapter 6) achieves part of the same effect without gas switching.

---

## 7.6 Radial Tuning

### 7.6.1 Knobs and Signatures

```
Knob                          Radial signature it moves
──────────────────────────────────────────────────────────────────────────────
Coil current ratio            Ion flux: center vs. middle → depth, rate
(inner / outer)
Gas injection split           Radical and O₂ profile → angle, AA width
(center / edge)
ESC zone temperatures         Passivation → AA width, angle (Chapter 8)
Edge ring height / tuning     Extreme edge (last 5–10 mm): tilt, edge CD
                              (Chapter 9)
```

### 7.6.2 An Example

```
Measured (center → edge, at r = 0, 75, 120, 145 mm):
  Cell depth:       250, 252, 255, 247 nm
  AA W(140):        18.9, 18.8, 18.5, 19.4 nm

Interpretation:
  Middle-high depth (255 at 120 mm): ion flux peaks under the outer
    coil → shift coil ratio toward inner (raises center, lowers middle)
  Extreme-edge depth low and AA wide at 145 mm: excess passivation at
    the edge (edge-injected O₂ or cooler edge) → reduce edge O₂ split
    or raise edge ESC zone by 2–3 °C
```

Depth and width signatures usually need different knobs. Depth follows ion flux. Width follows passivation. Radial tuning is most efficient when each signature is assigned to the knob that moves it with the least side effect.

---

## 7.7 Depth-Series Development

### 7.7.1 The Method

A depth series runs the recipe on test wafers stopped at several times and measures every feature at each stop:

```
Plan (reference recipe):
  Stops: BT + ME-1 at 10, 20, 30 s; + ME-2 at 10, 20, 32 s; + PS
  Features: cell line space, cut gap, periphery 60 nm, 100 nm, 1 µm, open
  Measurements: depth (OCD or cross-section), AA width at 0, 50, 100,
                140, 180 nm, bottom width; angle by segment
```

### 7.7.2 What It Gives

```
Output                          Use
──────────────────────────────────────────────────────────────────────
Depth vs. time per width        Fit k and ER₀ per step (Appendix E.2)
Width vs. depth per feature     Angle per depth segment; step marks
Mask remaining vs. time         Selectivity and facet rate
Cell vs. periphery at each      Where the depth gap opens; which step
stop                            to retune
```

A depth series is the only reliable way to see which step causes a profile feature. A final-profile cross-section shows the result. The series shows when and why it happened.

---

## 7.8 Summary & Key Takeaways

1. **Pressure is several knobs at once.** It lowers ARDE through coverage but widens ion angles and thickens passivation. ME-1 and ME-2 use different pressures for this reason.

2. **Flow and ratios are separate from pressure.** Total flow moves product redeposition; O₂ and NF₃ ratios move the passivation the cell is most sensitive to.

3. **Step boundaries leave marks.** The ME-1 → ME-2 boundary sits near 120 nm, above the 140–180 nm saddle-fin region where AA width matters most.

4. **Minor gases arrive late.** A 3 sccm gas in its own line can take tens of seconds to arrive. Carrier merging or pre-flow is required.

5. **ALE is too slow for the trench.** Full silicon ALE would take about 17 minutes. Quasi-ALE cycles of about a second are a middle ground with scalloping costs.

6. **Depth and width need different radial knobs.** Ion flux (coil ratio) moves depth. Passivation (gas split, zone temperature) moves width.

---

## Study Questions

1. Using the pressure table in Section 7.1.2, choose an ME-2 pressure that keeps the periphery (open) at or below 305 nm and the sidewall angle at or below 1.2°. What cell depth results?

2. NF₃ at 3 sccm is delivered through a dedicated line of 80 cm³ at 25 Torr. Compute the arrival delay. Propose two ways to reduce it below 1 s.

3. A process engineer moves the ME-1 → ME-2 switch from 30 s to 40 s to gain rate. Estimate the new boundary depth. Which device parameter could be affected, and how would you check it?

4. A quasi-ALE variant etches 3.5 nm per 1.1 s cycle. Compute the cycle count and plasma time for 250 nm, and the change in chamber cycle time compared with the 62 s main etch. What scallop period would you expect on the sidewall?

5. A radial map shows cell depth center-low (244 nm at center, 252 nm at 120 mm) with uniform AA width. Which knob would you adjust first and in which direction? What side effect would you check?

6. Design a depth series to determine whether a 0.3° increase in sidewall angle comes from ME-1 or ME-2. List stops, features, and the decisive measurement.

---

**Next Chapter:** [Chapter 8: Wafer Temperature, Electrostatic Chucks & Radial Control](./08-temperature-esc-radial.md)

---

**Chapter 7 Development Status:** Complete  
**Version:** 1.0
