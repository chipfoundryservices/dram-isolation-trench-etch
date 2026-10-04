# Appendix C: Standard Operating Procedures

Procedures for characterizing, qualifying, matching, and maintaining the DRAM isolation etch. Each procedure lists its purpose, the wafers and structures needed, the steps, and the acceptance criteria (illustrative). Adapt sample sizes and limits to the product and fab.

---

## C.1 Depth-Series Characterization (k and α(z))

**Purpose:** Extract the open-area rate ER₀, the ARDE coefficient k for each main-etch step, and the sidewall angle in each depth segment (Chapters 3, 7, 10).

**Wafers:** 7 patterned wafers with cell arrays, cut-gap targets, and periphery targets (60 nm, 100 nm, 1 µm, open), from one hard-mask lot.

```
Steps:
1. Run BT + ME-1 stopped at 10, 20, 30 s (3 wafers)
2. Run BT + ME-1 + ME-2 stopped at 10, 20, 32 s (3 wafers)
3. Run the full recipe including PS (1 wafer)
4. For each wafer: OCD on all targets (center, mid, edge);
   cross-section TEM at the center for the 30 s, 62 s, and full wafers
5. Fit, per step: D(t, S) = solution of t = [z + (k/S)(z²/2 + h_m z)]/ER₀
   (Appendix E.2) to all widths simultaneously → ER₀, k
6. From TEM: AA width at 0, 50, 100, 140, 180 nm and bottom → α per
   segment; locate the ME-1 / ME-2 step mark

Acceptance (reference):
  k (ME-2) = 0.025 ± 0.003; ER₀ = 300 ± 9 nm/min
  α (each segment) = 1.0 ± 0.15°; step mark above 135 nm
```

---

## C.2 Chamber Qualification After Wet Clean

**Purpose:** Return a chamber to production after a full wet clean or major part change (Chapter 9).

```
Steps:
1. Leak check and base pressure; RF and MFC calibration verification
2. ESC: He leak per zone with a bare wafer; zone temperature
   calibration (thermocouple or phosphor wafer)
3. Season: 25–50 dummy Si wafers through the production recipe with
   per-wafer WAC + season
4. Particles: bare Si wafer through the recipe; adders ≥ 26 nm
5. Metals: bare Si wafer; VPD-ICPMS for Fe, Ni, Cr, Cu, Y, Al, Na, K
6. Process: 2 patterned wafers; OCD at 13 sites: cell depth, periphery
   depths, W_t, W(140), SWA, remaining cap; CD-SEM top-down; TEM at
   center and edge (r = 145 mm)
7. Edge: tilt and edge depth at r = 145, 147 mm (C.4)

Acceptance (illustrative):
  Particle adders ≤ 10 (≥ 26 nm)
  Metals within Appendix A.7 limits
  Outputs within chamber-matching tolerances of Chapter 5.7.3
```

---

## C.3 Chamber Matching

**Purpose:** Keep every chamber in the fleet producing the same islands (Chapter 5).

```
Steps:
1. Inputs: delivered RF power (source and bias) at three set points
   with a calibrated load; MFC flow verification (rate-of-rise);
   pressure gauge cross-check; ESC zone temperature map; edge-ring
   height
2. Outputs: run a matching lot (3 wafers per chamber, same hard-mask
   lot) and measure the full output set
3. Compare each chamber to the fleet median:
     cell depth ± 3 nm, periphery open ± 4 nm, W_t ± 0.3 nm,
     W(140) ± 0.5 nm, SWA ± 0.1°, cap ± 1 nm, edge tilt ± 0.1°
4. For outliers: fix input deviations first; then set chamber-specific
   offsets (main-etch time, O₂ trim, zone temperatures, edge setting)
5. Record offsets in the APC system as chamber constants (Ch. 15)
```

---

## C.4 Edge Tilt and Ring Compensation Calibration

**Purpose:** Build the lift or tuning curve that holds edge tilt within ±0.3° at r = 147 mm over ring life (Chapter 9).

```
Steps:
1. With a new ring at the nominal setting, run 2 patterned wafers;
   cross-section TEM (or tilt-sensitive OCD) at r = 140, 145, 147 mm
   at 0°, 90°, 180°, 270°
2. Repeat at two other ring heights or tuning settings (±10 µm or
   equivalent) → dθ/d(setting)
3. Repeat at 100, 300, 600 RF hours → θ vs. RF hours at fixed setting
4. Fit: setting(RF h) = setting₀ + (dθ/dh) / (dθ/d setting) × RF h
5. Verify at the next interval; update the slope with each ring

Acceptance: tilt at r = 147 mm within ±0.3°; edge depth within −3% of
center; edge W(140) within +0.5 nm of center
```

---

## C.5 ESC Zone Transfer Matrix

**Purpose:** Map zone temperatures to the radial W(140) and depth profiles (Chapter 8).

```
Steps:
1. Baseline wafer at nominal zone setpoints; OCD at ≥ 25 radial sites
2. For each zone i: raise its setpoint by +3 °C, others nominal; run
   one wafer; measure the same sites
3. Response matrix: R_ji = ΔW(140)_j / ΔT_i (and the same for depth)
4. For a target correction ΔW, solve ΔT = R⁺ ΔW (pseudo-inverse,
   with limits on |ΔT_i| ≤ 6 °C and on depth side effects)
5. Verify with one wafer at the computed setpoints

Repeat after ESC replacement or major chamber change.
```

---

## C.6 Collapse-Margin Qualification

**Purpose:** Measure the capillary collapse margin of the fins with the production clean and dry (Chapter 11).

```
Structures: arrays of fins at the production pitch, with deliberately
varied width (W_t − 2 to + 2 nm in 0.5 nm steps) and, where possible,
varied depth (by etch time on separate wafers: 230–290 nm)

Steps:
1. Etch, clean, and dry with the production sequence
2. Top-down SEM or e-beam inspection on each array: fraction of
   collapsed or bridged pairs
3. Plot collapse fraction vs. w_eff and H; find the collapse onset
4. Compute the measured margin: M_meas = (H_onset / H_prod)⁴ for a
   depth split, or (w_prod / w_onset)³ for a width split
5. Calibrate the single-fin criterion of Chapter 11 against the onset
   (adjust the effective γ cos θ or eigenvalue coefficient)

Acceptance: collapse onset ≥ 1.1 × production depth (H) with the
production dry; zero collapsed pairs in production-dimension arrays
over ≥ 10⁸ inspected islands
```

---

## C.7 OCD Model Validation

**Purpose:** Ensure the scatterometry model reports depth, angle, and width correctly, including pitch-walk effects (Chapter 15).

```
Steps:
1. Build a design of experiments: 5–7 wafers spanning ±10% etch time,
   ±1 sccm O₂, and two mask-CD splits
2. Measure OCD at fixed sites; prepare TEM lamellae at the same sites
   (across the AA lines, covering ≥ 2 SAQP periods)
3. Compare OCD vs. TEM for depth (per space type), W_t, W(140), SWA
4. Check correlations: does a pure-angle split produce a reported depth
   change? A pure-time split an angle change?
5. Accept if slope 1.00 ± 0.05, offset within ±1 nm (depth) / ±0.3 nm
   (width), R² ≥ 0.9, cross-talk below 20% of the true change
```

---

## C.8 Retention-Impact Screening for Recipe Changes

**Purpose:** Screen any change to the etch (chemistry, energy, pulsing, chamber parts) for retention impact before product qualification (Chapter 13).

```
Steps:
1. Split lot: reference vs. change, same hard-mask lot, ≥ 3 wafers each
2. Run through the front end to the first electrical test point
3. Measure perimeter-to-area diode sets and array-like diodes at 85 °C;
   extract J_P and J_A per wafer (Appendix E.7)
4. Gated diodes / charge pumping for sidewall D_it (where available)
5. If J_P or D_it changes by more than 20%, stop or redesign; otherwise
   continue to product retention test at probe
6. Product: compare cumulative fail-bit curves vs. refresh time at
   85 °C; the change must not move the tail by more than the agreed
   factor at the screen condition

Acceptance: J_P within ±20% of reference; tail-bit count at the screen
condition within the noise of the reference (or improved)
```

---

**Appendix C Version:** 1.0
