# Chapter 15: Endpoint, Metrology & Advanced Process Control

## Overview

The isolation etch has no layer to stop on, and the feature that matters most, an 18 nm trench in a dense array, is invisible to every practical endpoint signal. Depth is controlled by time. Time is right only if the rate is right, and the rate depends on the chamber, the walls, the product, and the incoming mask. Profile and AA width at depth cannot be seen during the etch at all. Control therefore rests on three things: a stable chamber, accurate measurement after the etch, and a control system that turns measurements into the next wafer's settings.

This chapter covers what can and cannot be sensed during the etch, the metrology used to measure depth, width, angle, and pitch-walk signatures after it, fault detection, and the feed-forward and feedback control that keeps the cell and the periphery inside their windows.

**Learning Objectives:**
- Explain why depth endpoint is not available and what in-situ signals are useful
- Choose OES lines for breakthrough and mask-open endpoints and for rate monitoring
- Describe OCD scatterometry, CD-SEM, CD-SAXS, and cross-section TEM for AA profiles and their limits
- Design a sampling plan for cell, cut gap, array edge, and periphery
- Set up fault detection on RF, gas, thermal, and OES signals
- Build feed-forward and EWMA feedback control on etch time and a second knob for the cell/periphery balance
- Explain virtual metrology and its role

---

## 15.1 What Can Be Sensed During the Etch

### 15.1.1 No Depth Endpoint

```
Signal                     Why it does not give cell depth
──────────────────────────────────────────────────────────────────────────────
OES (etch products)        Silicon is uniform with depth; product emission
                           stays nearly constant. ≈ 60% open area means the
                           signal is dominated by the periphery and open areas
Laser interferometry       Spot (≈ 1 mm) on an array averages a dense grating;
(single wavelength)        the fringe tracks an effective-medium depth, not the
                           cell trench, and periphery areas dominate if in the
                           spot
In-situ spectral           Can follow a dense grating with a real-time
reflectometry              optical model; emerging, needs a dedicated target
                           and a robust model through changing passivation
```

In-situ spectral reflectometry with a scatterometry model is the most promising route, and some tools offer it on dedicated test areas. For most production processes, depth is still controlled by time.

### 15.1.2 Endpoints That Work

```
Step                     Transition                   OES signal (nm)
──────────────────────────────────────────────────────────────────────────────
Hard-mask open (SiN)     SiN cleared → pad oxide      CN 387 nm falls; N₂ / N
                                                      lines fall
Hard-mask open (pad)     Pad oxide cleared → Si       SiF 440 nm / 777 nm O falls,
                                                      CO 483.5 nm falls
Breakthrough (native     ≈ 1 nm oxide, 8 s            Too short and too small for
oxide)                                                a reliable endpoint: timed
WAC (per wafer)          Wall deposits removed        SiF 440 nm decays to
                                                      baseline
```

The WAC endpoint is useful: if the clean takes longer than usual, the walls carried more deposit than usual, which is an early sign of a change in the main etch.

### 15.1.3 Rate Monitoring by OES

Even without an endpoint, the intensity of silicon-product emission during the main etch tracks the total silicon removal rate:

```
Signals (illustrative):
  Si I 288.2 nm             Etch products dissociated in the plasma
  SiCl 287 nm (ME-1)        Cl-containing products
  Br I 827 nm / Ar 750 nm   Actinometric Br density (with a small Ar flow)
  O I 777 nm / Ar 750 nm    Actinometric O: passivation supply

Use:
  - Integrated product signal ∝ silicon removed (mostly from open and
    periphery areas) → wafer-level rate indicator
  - O/Ar and Br/Ar ratios → wall state and gas delivery faults
  - Step-to-step consistency → fault detection and virtual metrology
```

---

## 15.2 Post-Etch Metrology

### 15.2.1 Methods

```
Method                Measures                                  Limits
──────────────────────────────────────────────────────────────────────────────────────
OCD (spectroscopic    Depth (per space type), top CD, CD at     Model-based; parameter
ellipsometry /        several heights, SWA, bottom shape,       correlation (depth vs.
reflectometry,        remaining mask; on dedicated array-like   angle); needs TEM
RCWA model)           targets or in-die arrays                  reference; 1–2 min/site
CD-SEM (top-down)     Top CD of AA and spaces, space-type       Top only; charging on
                      identification (pitch walk), island ends, the mask; no depth
                      LWR/LER, lean (top offset)
CD-SAXS (transmission Average profile of a periodic array at    Slow; needs a large
X-ray scattering)     every depth, including pitch walk         periodic target; not
                                                                inline at high volume
Cross-section TEM /   Full profile, bottom shape, damage        Destructive; few sites;
STEM                  layer (high resolution), island end       days of turnaround
                      profile along the AA
E-beam inspection     Bridges, collapse, missing spaces;        Slow for full wafers;
                      voltage contrast after liner or contact   sampled areas
Optical inspection    Particles, clusters, collapse clusters    Small defects below
(broadband)                                                     sensitivity
```

### 15.2.2 OCD Models for the AA Array

```
Model parameters (typical floating set):
  Mask remaining (SiO₂ cap, SiN)
  AA top CD (W_t)
  Space top CD per type (α, β, γ) — or a single space with a pitch-walk
    parameter
  Sidewall angle per segment (ME-1, ME-2) or AA CD at 50, 140, 180 nm
  Depth per space type
  Bottom rounding radius
  Cut-gap depth (if the target includes cuts)

Precision (3σ, illustrative):
  Depth             0.6–1.0 nm
  W_t               0.2–0.3 nm
  W(140)            0.4–0.6 nm
  SWA               0.05–0.1°
  Pitch-walk depth  1.0–1.5 nm
```

The main risk in OCD is correlation between parameters that produce similar spectral changes. Depth and sidewall angle are the classic pair. A model that lets both float can report a depth change when the angle has changed. Fixing correlated parameters from other data (TEM, CD-SEM top CD) and validating against TEM after every model change keeps the model honest.

A single-space model averages the three SAQP spaces. It reports the mean depth correctly but hides the depth walk (Chapter 12). The production model should resolve space types, at least on a qualification target.

### 15.2.3 Sampling Plan

```
Location                      Why                                  Per lot
──────────────────────────────────────────────────────────────────────────────────────
Cell array center (OCD)       Cell depth, W_t, W(140), SWA         2 wafers × 13 sites
Cut-gap target (OCD / SEM)    Cut depth, island end                2 wafers × 5 sites
Array edge (SEM)              Lean, edge-line profile              1 wafer × 5 sites
Periphery 60 nm, 100 nm, open Periphery depth window               2 wafers × 9 sites
(OCD on periphery targets)
Extreme edge (r ≥ 145 mm)     Edge depth, W(140), tilt             2 wafers × 4 sites
CD-SEM top-down               W_t, spaces α/β/γ, LWR, ends, lean   1 wafer × 9 sites
TEM (cross-section)           Full profile; model validation       Per chamber, weekly
E-beam inspection             Bridges, collapse                    Per chamber, per day
                                                                   (sampled areas)
```

---

## 15.3 Fault Detection

```
Signal                         Fault it reveals                     Effect on the islands
──────────────────────────────────────────────────────────────────────────────────────────────
Bias voltage (Vpp, Vdc)        Ion energy change; ion flux change   Depth, facet, damage
                               (Chapter 5: energy = power/current)
Match positions, reflected     RF delivery, coil or window state    Rate, uniformity
power
Pulse timing / duty readback   Pulsing fault (CW-like behavior)     k ↑ → periphery deep
                                                                    (Chapter 12)
Pressure, throttle position    Gas flow error, pump degradation,    Rate, ARDE, profile
                               leak
MFC flows (O₂, NF₃ especially) Passivation supply                   Angle, W(140)
ESC zone temps, heater power   Thermal drift; heater failure        Radial W(140)
He leak per zone               Wafer seating; backside particles    Local narrow AA
O/Ar, Br/Ar actinometry        Wall state; gas delivery             Angle; rate
Si 288 nm integrated signal    Total silicon removal                Depth (wafer level)
WAC endpoint time              Wall deposit load                    Drift precursor
```

Per-step statistics (mean, slope, standard deviation of each signal within each step) are compared with control limits built from a clean reference population. A pulse-timing fault deserves special mention: if pulsing fails silently and a step runs continuous-wave, k rises from 0.025 toward 0.058, and the periphery goes 80 nm deeper with nothing else visible.

---

## 15.4 Advanced Process Control

### 15.4.1 Feed-Forward

```
Incoming data                       Adjusted parameter            Model (illustrative)
──────────────────────────────────────────────────────────────────────────────────────────
Mask height h_m (± 2 nm)            Main-etch time (cell)         ∂t/∂h_m ≈ +0.07 s/nm
Space top CD (S_t)                  Main-etch time (cell)         ∂D/∂S ≈ 2.75 nm/nm
AA top CD (W_t)                     ME-2 O₂ (to hold W(140))      ∂W(140)/∂O₂ ≈ +1.2 nm/sccm
Product open-area fraction          Main-etch time                ER₀ ∝ (1 + κ f_ref)/(1 + κ f)
Chamber RF hours since clean, ring  Time offset, edge setting     Calibration curves
hours                                                             (Chapter 9)
```

### 15.4.2 Feedback by EWMA

```
Exponentially weighted moving average of the offset between the model
and the measurement:

  o_{n+1} = λ o_meas,n + (1 − λ) o_n       λ ≈ 0.3–0.5

Example: time control on the periphery open depth (the binding limit)
  Model: D_open = ER₀ × t + o
  Target 310 nm; ER₀ (model) = 300 nm/min

  Lot n:   t = 62.1 s, measured 316 nm → o_meas = +5.5 nm
  With λ = 0.4 and o_n = +1.0: o_{n+1} = 0.4 × 5.5 + 0.6 × 1.0 = 2.8 nm
  Next time: t = (310 − 2.8) / 300 min = 61.4 s
```

### 15.4.3 Two Outputs, Two Knobs

Time alone can put one depth on target. The cell and the periphery move together with time but differently with anything that changes k. A second knob that changes k (ME-2 pressure or duty cycle) allows both to be controlled:

```
Sensitivities near the reference (illustrative):
  ∂D_cell/∂t  = ER₀ × 0.707 = 3.5 nm/s      (rate at the cell bottom)
  ∂D_open/∂t  = ER₀          = 5.0 nm/s
  ∂D_cell/∂p  = +0.75 nm per mTorr (ME-2)
  ∂D_open/∂p  = −1.75 nm per mTorr (ME-2)

Measured: cell 244 nm, open 318 nm (targets 250, 310)
  Required: ΔD_cell = +6, ΔD_open = −8

  3.5 Δt + 0.75 Δp = +6
  5.0 Δt − 1.75 Δp = −8

  → Δp = +5.9 mTorr, Δt = +0.46 s
```

The solution asks for nearly 6 mTorr more ME-2 pressure, which would raise the sidewall angle by about 0.2–0.3° (Chapter 7). A controller must therefore limit the second knob and weigh the angle. In practice, a k shift this large is treated as a fault (pulsing, wall state, or gas delivery) rather than corrected by control. **APC should correct drift, not mask a broken chamber.**

### 15.4.4 Width Control

```
W(140) feedback (OCD), knob: ME-2 O₂ flow (or zone temperatures for radial)
  Sensitivity: +1.2 nm per sccm O₂ (Chapter 7)
  Measured W(140) = 19.4 nm (target 18.9): ΔO₂ = −0.5 / 1.2 = −0.4 sccm
  Side effects: angle −0.1°, S(250) +0.9 nm, cell depth +1 nm

Radial: zone temperatures by the transfer matrix (Chapter 8)
```

Width control uses a small O₂ trim within a narrow band, and the zone temperatures for radial shape. Larger corrections indicate a change in the chamber or in the incoming mask and are escalated.

### 15.4.5 Virtual Metrology

Only a few wafers per lot are measured. Virtual metrology predicts depth and width for every wafer from its FDC and OES data (integrated Si emission, bias voltage, actinometry, temperatures) using a regression model trained on measured wafers. It catches wafer-level excursions between measured wafers and, combined with the EWMA, can give per-wafer time adjustment. Its predictions must be validated continuously; a model trained before a chamber clean or part change can be wrong afterward.

---

## 15.5 Control Limits

```
Parameter                  Target     Control limits (±)    Spec (±)
──────────────────────────────────────────────────────────────────────
Cell depth                 250 nm     12 nm                 30 nm (220–280)
Periphery open depth       310 nm     12 nm                 20/25 (280–330)
Periphery 60 nm depth      287 nm     10 nm                 ≥ 270
W_t                        14.0 nm    0.6 nm                1.0 nm (3σ)
W(140)                     18.9 nm    1.0 nm                1.5 nm (3σ)
SWA (cell)                 1.0°       0.15°                 0.7–1.25°
Depth walk (α/β/γ range)   ≤ 5.5 nm   7 nm                  ± 6 nm
Remaining cap              10.7 nm    1.5 nm                ≥ 8 nm
```

Control limits are set inside the specification so that excursions are seen and corrected before product falls outside it.

---

## 15.6 Summary & Key Takeaways

1. **Depth is controlled by time.** OES and interferometry cannot see an 18 nm trench in a dense array; in-situ scatterometry is emerging but not yet general.

2. **OES still matters.** It gives the mask-open and WAC endpoints, wafer-level rate, and wall-state and gas-delivery faults.

3. **OCD needs a model that knows the array.** Space types, segment angles, and correlations must be in the model; TEM keeps it honest.

4. **Sample where the windows are.** Cell, cut gaps, array edge, periphery widths, and the extreme edge each have their own failure modes.

5. **Two depths need two knobs.** Time sets one depth; a k knob (pressure or duty) sets the cell/periphery ratio, within limits that protect the angle.

6. **Control drift, escalate faults.** A large k shift is usually a pulsing, wall, or gas fault. APC should not hide it.

---

## Study Questions

1. Explain why the integrated Si 288 nm signal is a better indicator of periphery depth than of cell depth. What would you expect it to show if pulsing failed and ME-2 ran continuous-wave?

2. An OCD model fit shows the cell depth up by 4 nm and the SWA down by 0.2° on one lot, with no change in CD-SEM top CD. What would you check before believing the depth change?

3. With λ = 0.3, an initial offset o = 0, and measured open depths of 314, 312, 317, and 309 nm on four consecutive lots at ER₀ = 300 nm/min, compute the offset and the time after each lot (target 310 nm).

4. Using the two-knob sensitivities of Section 15.4.3, compute the corrections for measured cell 253 nm and open 305 nm. Are they within a reasonable band (|Δp| ≤ 2 mTorr)?

5. W(140) reads 18.3 nm on center sites and 19.1 nm on edge sites (target 18.9 nm). Design a correction using O₂ for the mean and zone temperatures for the radial shape, and list the side effects you would check.

6. Propose a set of FDC signals and limits that would detect (a) a slow O₂ MFC drift, (b) a He leak on one zone, and (c) a pulsing failure, each before the next OCD measurement.

---

**Next Chapter:** [Chapter 16: Post-Etch Integration, Yield & Cost of Ownership](./16-integration-yield-coo.md)

---

**Chapter 15 Development Status:** Complete  
**Version:** 1.0
