# Chapter 6: Ion Energy, Bias Pulsing & Angular Control

## Overview

Ions do three things in the isolation etch. They drive the reaction at the trench bottom, which makes the etch fast and vertical. They erode the mask and its corners, which costs selectivity and bends the top of the profile. And they penetrate the silicon they strike, which leaves damage and implanted hydrogen and bromine in the surfaces that become storage-node junctions. The first job needs enough energy, aimed straight down. The other two get worse with every extra electronvolt and every degree of spread.

This chapter treats the ion energy, its distribution, its angular spread, and the pulsing schemes that shape them in time. It shows that pulsing is the main tool that brings the ARDE coefficient from 0.058 to 0.025 in the reference process, and why.

**Learning Objectives:**
- Compute etch yield and mask selectivity as functions of ion energy
- Estimate sheath thickness, ion transit time, and the shape of the ion energy distribution at different bias frequencies
- Explain how synchronized pulsing changes the neutral-to-ion flux ratio and lowers the bottom reaction probability
- Compute the change in ARDE coefficient from a surface-coverage model
- Estimate the ion angular spread from sheath voltage and collisions
- Choose duty cycle and pulse frequency for rate, ARDE, charging, and damage

---

## 6.1 How Much Energy?

### 6.1.1 Yield Versus Energy

Ion-enhanced etch yields rise as the square root of ion energy above a threshold:

```
Y(E) = A (√E − √E_th)

Illustrative thresholds in HBr/O₂:
  Si (ion-enhanced, halogenated surface):  E_th,Si ≈ 15 eV
  SiO₂ mask (Br does not etch it readily): E_th,ox ≈ 50 eV

  E (eV)    √E − √15    √E − √50    Ratio (Si/ox)
  ──────────────────────────────────────────────────
  100       6.13        2.93        2.09
  150       8.38        5.18        1.62
  200       10.27       7.07        1.45
  250       11.94       8.74        1.37
```

The selectivity to oxide scales with this ratio (times the chemical factor that makes bromine poor at etching oxide). Normalizing to the reference S_ox = 40 at 150 eV:

```
  E (eV)    Si yield (rel. 150 eV)    S_ox (Si:SiO₂)
  ────────────────────────────────────────────────────
  100       0.73                      52
  150       1.00                      40
  200       1.23                      36
  250       1.42                      34
```

Raising the energy from 150 to 250 eV buys 42% more yield and costs 15% of the selectivity. It also raises facet growth on the 14 nm mask lines faster than the planar loss, because the angle-dependent sputter yield of the oxide peaks at the facet angle. Below about 100 eV, the yield falls quickly and the passivation at the bottom is not cleared reliably, so narrow spaces begin to stop.

### 6.1.2 Energy and Depth of Damage

```
Projected range in Si (approximate):
  Br⁺ at 150 eV       ≈ 1.0–1.5 nm (heavy; damage stays shallow)
  HBr⁺ / H⁺ fragments  H travels 3–5 nm and diffuses deeper
  Ar⁺ at 150 eV       ≈ 1.5–2 nm

Damaged layer at the trench bottom: ≈ 2–3 nm at 150 eV
On the sidewalls: far less (grazing incidence), mostly from
  scattered and off-angle ions
```

The trench bottom takes the full dose, but it is later covered by thick fill oxide, well away from the storage-node junction. The sidewalls receive a much smaller dose, but they are the junction surface. Chapter 13 develops this.

---

## 6.2 The Ion Energy Distribution

### 6.2.1 Sheath Thickness and Transit Time

```
ME-1 sheath at the wafer (pulse-on):
  Ion current density J_i = 4.0 mA/cm² = 40 A/m²
  T_e ≈ 3 eV; dominant ion Br⁺/HBr⁺ (M ≈ 80 amu)
  Bohm velocity: u_B = √(kT_e/M) = √(3 × 1.6×10⁻¹⁹ / 1.33×10⁻²⁵) ≈ 1.9 km/s
  Sheath-edge density: n_s = J_i / (e u_B) = 40 / (1.6×10⁻¹⁹ × 1900)
                       ≈ 1.3×10¹⁷ m⁻³ = 1.3×10¹¹ cm⁻³
  Debye length: λ_D = √(ε₀ T_e / (n_s e)) ≈ 36 µm

Child-law sheath for ⟨V_sh⟩ = 135 V:
  s = (√2 / 3) λ_D (2 V / T_e)^(3/4) = 0.471 × 36 µm × (90)^0.75
    ≈ 0.49 mm

Ion transit time (Child-law sheath):
  τ_i ≈ 3 s / √(2 e V / M) = 3 × 0.49 mm / 18 km/s ≈ 81 ns
```

### 6.2.2 Bias Frequency

```
Bias       RF period τ_rf    τ_i / τ_rf (Br⁺)     IED character
──────────────────────────────────────────────────────────────────────────────
2 MHz      500 ns            0.16                 Ions follow the RF: broad,
                                                  bimodal, ≈ 0 to 2⟨V⟩
13.56 MHz  74 ns             1.1                  Intermediate: bimodal, peaks
                                                  closer, width ≈ 50–80% of ⟨V⟩
27–60 MHz  37–17 ns          2–5                  Ions see the average: narrow
                                                  peak; width ∝ τ_rf / τ_i
```

For a low-frequency bias where ions follow the instantaneous sheath voltage, the fraction of ions below an energy E_c is:

```
P(E < E_c) = ½ + arcsin(E_c / e⟨V⟩ − 1) / π      (sinusoidal sheath,
                                                  amplitude = ⟨V⟩)

At 2 MHz with ⟨V⟩ = 150 V:
  Fraction above 225 eV (1.5⟨V⟩):  ½ − arcsin(0.5)/π   = 0.33
  Fraction below 50 eV (0.33⟨V⟩):  ½ + arcsin(−0.67)/π = 0.27
```

A third of the ions arrive above 225 eV, where they facet the mask and damage the silicon, and a quarter arrive below 50 eV, where they barely etch. **The same mean energy at 13.56 MHz delivers most ions between about 100 and 200 eV.** This is why silicon trench etch in DRAM uses 13.56 MHz or higher bias frequencies, and why some tools offer tailored bias waveforms that flatten the sheath voltage to produce a single narrow peak.

### 6.2.3 Light Ions

Hydrogen-containing ions (H⁺, H₂⁺, H₃⁺) from HBr have one-fortieth to one-eightieth the mass of Br⁺. Their transit time is short, and they follow the RF even at 13.56 MHz, arriving with a broad energy distribution reaching about twice the mean sheath voltage. They are a small fraction of the ion flux, but they penetrate deeply and contribute most of the hydrogen found in the silicon after the etch (Chapter 13).

---

## 6.3 Synchronized Pulsing

### 6.3.1 What Happens in a Pulse

```
One period (1 kHz, 50% duty):

  Source RF   ████████████████████░░░░░░░░░░░░░░░░░░░░
  Bias RF     ████████████████████░░░░░░░░░░░░░░░░░░░░
              0                  500 µs               1000 µs

  On phase:   T_e ≈ 3 eV, high ion flux, ions accelerated by bias
  Off phase:  T_e collapses in ≈ 10 µs; positive ion density decays in
              ≈ 50–100 µs; in electronegative HBr/Cl₂ the afterglow becomes
              an ion–ion plasma (Br⁻, Cl⁻ and positive ions)
              Radicals (Br, Cl, O) persist: lifetime ≈ 1–10 ms
```

Because radicals outlive ions by one to two orders of magnitude, the time-averaged radical flux to the wafer barely notices the off phase, while the time-averaged ion flux falls roughly in proportion to the duty cycle. Peak source power is usually raised to keep the average dissociation similar. **Pulsing raises the neutral-to-ion flux ratio.**

### 6.3.2 A Surface-Coverage Model for ARDE

Chapter 3 showed that ARDE is set by the bottom reaction probability β. A simple Langmuir picture links β to the flux ratio. Halogen atoms adsorb on free bottom sites with sticking probability s. Ions remove adsorbed halogen (as etch products). At steady state the halogen coverage θ is:

```
θ = s Γ_n / (s Γ_n + Y_d Γ_i)  =  R / (1 + R)

  R = s Γ_n / (Y_d Γ_i)   (supply ratio: halogen adsorbed per halogen
                           removed by ions on a bare surface)

An arriving halogen atom reacts only if it finds a free site:
  β = s (1 − θ) = s / (1 + R)
```

```
Illustrative, s = 0.5:

  Condition                       R      θ       β       k ≈ β/3
  ─────────────────────────────────────────────────────────────────
  Continuous wave (CW)            2      0.67    0.17    0.058
  Synchronized pulsing            6      0.86    0.071   0.024
  (≈ 3× higher Γ_n/Γ_i)
```

When the bottom is nearly saturated with halogen, an extra atom arriving at the bottom of a deep trench adds little, and a shortfall of atoms costs little. The rate becomes **ion-limited**, and since ions are transmitted much better than neutrals at A ≈ 16 (Chapter 3), ARDE falls. Tripling the supply ratio takes the coefficient from 0.058 to the reference 0.025.

### 6.3.3 The Cost: Rate

The bottom is now limited by ions, and pulsing has reduced the time-averaged ion flux. The open-area rate falls:

```
                          CW               Pulsed (reference)
──────────────────────────────────────────────────────────────────
Open-area rate ER₀        380 nm/min       300 nm/min
ARDE coefficient k        0.058            0.025

Time for the cell (S = 18 nm) to reach 250 nm:
  t = [z + (k/S)(z²/2 + h_m z)] / ER₀,  z = 250, h_m = 49
  CW:     (250 + 0.003222 × 43,500) / 380 = 390.2 / 380 = 1.027 min = 61.6 s
  Pulsed: (250 + 0.001389 × 43,500) / 300 = 310.4 / 300 = 1.035 min = 62.1 s

Periphery (open) depth at that time:
  CW:     380 × 1.027 = 390 nm
  Pulsed: 300 × 1.035 = 310 nm
```

**For the cell, the two recipes take the same time.** The CW recipe is faster everywhere, but it spends its speed overshooting the periphery. The pulsed recipe gives up open-area rate that the cell could not use anyway, and brings the periphery inside its window.

### 6.3.4 Charge Relief

During the on phase, the oxide mask charges as described in Chapter 3. In the off phase, the sheath collapses, and slow electrons and, in electronegative plasmas, negative ions can reach the mask surfaces and discharge them. A few tens of microseconds of afterglow are enough. At 1 kHz and 50% duty, the off phase is 500 µs, so the mask starts every pulse close to neutral. This removes most of the asymmetric deflection at array edges and pitch-walked spaces (Chapter 11).

### 6.3.5 Choosing Duty and Frequency

```
Duty cycle (synchronized, 1 kHz, peak powers adjusted):

  Duty     ER₀ (rel.)    k        Profile                 Notes
  ───────────────────────────────────────────────────────────────────────
  100%     1.00 (CW)     0.058    Vertical upper part;    Fast; periphery
                                  bow risk                overshoot
  70%      0.90          0.040
  50%      0.79          0.025    Reference ME-1
  40%      0.74          0.021    Reference ME-2          Lower facet rate
  25%      0.60          0.016    Taper grows (more       Slow; passivation
                                  film per ion)           dominates
  (illustrative)

Frequency:
  < 200 Hz    Off phase long enough for wall-state and gas changes;
              plasma re-ignition transients become a larger fraction
  0.5–5 kHz   Typical; off phase ≫ ion decay, ≪ radical lifetime
  > 10 kHz    Off phase too short for full afterglow; benefits shrink
```

Lower duty keeps reducing k, but the passivation grows relative to the ion dose, and the profile begins to taper (Chapter 4). In the reference process, ME-1 runs at 50% for rate in the shallow part of the trench, and ME-2 runs at 40% where ARDE matters most.

### 6.3.6 Variants

```
Scheme                         What is pulsed           Typical use
──────────────────────────────────────────────────────────────────────────────
Bias-only pulsing              Bias; source CW          Lower ion energy dose;
                                                        selectivity; damage
Source-only pulsing            Source; bias CW          Lower T_e, less
                                                        dissociation; bias in
                                                        afterglow extracts
                                                        negative ions
Synchronized pulsing           Both, in phase           ARDE, charging (reference)
Phase-shifted / asynchronous   Both, with delay         Bias on in early
                                                        afterglow: low-energy,
                                                        narrow IED; tuning knob
Multi-level pulsing            Two or more power        Passivation and etch
                               levels per period        phases in one period
                                                        (quasi-ALE, Chapter 7)
```

---

## 6.4 Ion Angular Distribution

### 6.4.1 Collisionless Spread

Ions enter the sheath with a small transverse thermal velocity and are accelerated normal to the wafer. The resulting angular spread is:

```
σ_θ ≈ √( kT_i⊥ / (2 e V_sh) )

T_i⊥ ≈ 0.05 eV, V_sh = 135 V:
  σ_θ ≈ √(0.05 / 270) = 0.0136 rad ≈ 0.8°
```

### 6.4.2 Collisions in the Sheath

```
Gas density at 8 mTorr, 350 K: n_g = p / kT ≈ 2.2×10²⁰ m⁻³
Charge-exchange cross section (Br⁺ on HBr, illustrative): ≈ 5×10⁻¹⁹ m²
  λ_i = 1 / (n_g σ) ≈ 9 mm

Fraction of ions colliding in a 0.49 mm sheath:
  1 − exp(−s/λ_i) = 1 − exp(−0.054) ≈ 5%   (8 mTorr)
  At 20 mTorr (λ_i ≈ 3.6 mm, s ≈ 0.45 mm): ≈ 12%
```

Ions that collide in the sheath restart from low energy partway across it and arrive with lower energy and wide angles. They form a tail of the angular distribution that does not etch the bottom effectively but does strike the sidewalls. The effective spread, including this tail, is about 1–1.5° at the reference conditions.

### 6.4.3 What the Spread Does to the Trench

```
Effect of σ_θ at the reference trench (A = 16.6):
  Direct ion transmission K_i ≈ 1 − 0.80 A σ_θ (Chapter 3)
    σ_θ = 0.8° → 0.81
    σ_θ = 1.5° → 0.65

Ions striking the upper sidewall:
  thin the passivation there → bow just below the mask (Chapter 10)
Ions striking the lower sidewall at grazing angles:
  reflect to the bottom corners → microtrenching (Chapter 10)
```

Higher pressure lowers k in some recipes (more radicals per ion), but it broadens the angular spread and can cost profile. The reference ME-2 at 12 mTorr is a compromise: its 7% collisional fraction is acceptable deep in the trench, where the passivation is thicker.

---

## 6.5 Ion Energy Through the Etch

```
Recipe stage        Ion energy (mean)     Reason
────────────────────────────────────────────────────────────────────
Breakthrough        ≈ 120–150 eV, CW      Clear native oxide uniformly
ME-1                ≈ 150 eV, 50% duty    Rate; clear bottom polymer at low A
ME-2                ≈ 140 eV, 40% duty    ARDE, selectivity, facet control
Profile step        ≈ 50–70 eV, CW        Round the bottom with little damage
```

A ramp of bias through ME-2 is sometimes used to keep the bottom clear as the aspect ratio rises, at the cost of more facet growth late in the etch, when the mask is thinnest. The reference recipe holds energy constant in ME-2 and relies on pulsing and NF₃ to keep the bottom clean.

---

## 6.6 Summary & Key Takeaways

1. **Energy trades yield against selectivity.** From 150 to 250 eV, silicon yield rises 42% and oxide selectivity falls from 40 to 34. Facet growth on 14 nm lines rises faster still.

2. **Bias frequency shapes the distribution.** At 2 MHz, a third of the ions arrive above 1.5× the mean energy. At 13.56 MHz, most Br⁺ ions arrive within about ±40% of it. Light hydrogen ions follow the RF at any common bias frequency.

3. **Pulsing raises the neutral-to-ion ratio.** Radicals outlive ions by one to two orders of magnitude, so pulsing removes ions from the time average but keeps the radicals.

4. **Higher coverage means lower ARDE.** In the coverage model, tripling the supply ratio lowers β from 0.17 to 0.07 and k from 0.058 to 0.025, making the bottom ion-limited.

5. **The cell does not lose time.** CW and pulsed recipes reach 250 nm in the cell in about 62 s. The pulsed recipe puts the periphery at 310 nm instead of 390 nm.

6. **Angle spread is mostly collisions.** Thermal spread is about 0.8°. Sheath collisions add a wide tail that grows with pressure and drives bow and microtrenching.

---

## Study Questions

1. Using the yield model with E_th,Si = 15 eV and E_th,ox = 50 eV and S_ox = 40 at 150 eV, compute the selectivity at 120 eV and 180 eV. How much open-area rate (relative) does each give?

2. Compute the sheath thickness and Br⁺ transit time for J_i = 3.0 mA/cm², T_e = 2.5 eV, and ⟨V_sh⟩ = 110 V. What is τ_i/τ_rf at 13.56 MHz? Would you expect a narrower or broader IED than the reference?

3. For a 2 MHz bias with ⟨V⟩ = 140 V, compute the fraction of ions above 200 eV and below 40 eV using the sinusoidal-sheath formula.

4. In the coverage model with s = 0.5, a recipe has R = 4. Compute θ, β, and k. Using the reference ARDE equations with ER₀ = 330 nm/min, compute the time for the cell to reach 250 nm and the open periphery depth at that time.

5. A process engineer moves ME-2 from 12 mTorr to 20 mTorr to lower k further. Estimate the change in the collisional fraction of the sheath. Which profile defects would you check first, and where in the trench?

6. Explain why reducing the duty cycle below about 25% begins to increase taper even though it lowers ARDE. Which other lever could keep the angle constant while k falls?

---

**Next Chapter:** [Chapter 7: Gas Delivery, Pressure & Multi-Step Recipe Design](./07-gas-pressure-steps.md)

---

**Chapter 6 Development Status:** Complete  
**Version:** 1.0
