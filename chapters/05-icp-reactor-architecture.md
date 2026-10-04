# Chapter 5: Inductively Coupled Reactor Architecture for DRAM Isolation Etch

## Overview

The isolation etch is run in a **conductor-etch chamber**: an inductively coupled plasma (ICP) reactor, often called a transformer-coupled plasma (TCP) reactor, with a planar or dome-shaped coil above a dielectric window and a separate RF bias on the wafer chuck. This architecture has dominated silicon gate and trench etch since the 1990s, and every major DRAM maker runs its active-area etch on it.

This chapter explains why, describes the main subsystems, and puts numbers on the quantities that matter for the isolation etch: ion flux and energy, residence time, product load in the gas phase, heat load, and throughput. Later chapters in Part II go deeper into each subsystem.

**Learning Objectives:**
- Explain why ICP reactors suit low-energy, high-flux silicon trench etch better than capacitively coupled reactors
- Describe the coil, window, chamber body, chuck, and pumping subsystems and their roles
- Estimate mean ion energy from bias power and ion current
- Compute residence time, pumping speed, and the etch-product fraction of the gas
- Compute chamber cycle time, wafers per hour, and fleet size for a DRAM fab
- List the parameters used to match chambers in a fleet

---

## 5.1 Why ICP

### 5.1.1 Requirements From the Etch

```
Requirement (from Chapters 3–4)                    Reactor property needed
──────────────────────────────────────────────────────────────────────────────
High ion flux at modest energy (100–200 eV):       Plasma density set independently
  rate with low damage and good selectivity        of ion energy
Narrow ion angular spread (σ_θ ≈ 1–1.5°):          Low pressure (5–20 mTorr),
  verticality in a 14:1 trench                     thin, nearly collisionless sheath
High halogen radical density:                      Efficient dissociation at low
  supply to 60% open area                          pressure
Radial uniformity of ion flux and radicals:        Tunable source distribution
  ±1% depth across 300 mm                          (coil zones, gas zones)
Pulsing of source and bias:                        Fast-switching generators with
  ARDE, charging, damage control (Chapter 6)       synchronized phase control
```

### 5.1.2 ICP Versus CCP

```
Property                       ICP (conductor etch)        CCP (dielectric etch)
────────────────────────────────────────────────────────────────────────────────────
Plasma density (ions/cm³)      10¹¹–10¹²                   10¹⁰–10¹¹
Operating pressure             3–30 mTorr                  15–80 mTorr
Ion energy at the wafer        20–400 eV (bias)            200 eV – several keV
Independent flux / energy      Yes (coil vs. bias)         Partly (VHF source + LF bias)
Typical use                    Si, poly-Si, metals,        Oxide, nitride, HAR
                               hard-mask trim              dielectric stacks
```

A silicon trench needs ion energies well above the ion-enhanced etch threshold (about 15–20 eV) but well below the energies that sputter the oxide mask and drive damage deep into the silicon. The ICP gives high flux at 100–200 eV and low pressure, which is exactly that window. A CCP could reach the same energies, but at lower density and higher pressure, with a wider angular spread and a lower rate.

---

## 5.2 The Source

### 5.2.1 Coil and Window

```
Schematic (cross-section):

        ┌──────── coil (inner + outer zones) ────────┐
        │   ○ ○ ○        ○ ○ ○         ○ ○ ○          │  13.56 MHz
        └──────────────────────────────────────────────┘
        ═════════════ dielectric window ═══════════════   Al₂O₃ / quartz,
           (Faraday shield optional, between)             Y₂O₃-coated
        ┌────────────────────────────────────────────┐
        │                 plasma                      │  gap 8–12 cm
        │                                             │
        │         ┌─────── wafer ───────┐             │
        └─────────┤  ESC (bias 13.56)   ├─────────────┘
                  └─────────────────────┘
                     edge ring ↑   pump ↓ (annular)
```

The coil's RF current induces an azimuthal electric field in the plasma just below the window, which heats electrons. Power is absorbed in a skin layer a few centimetres thick. Ions and radicals diffuse from there to the wafer.

### 5.2.2 Radial Control

A single coil tends to produce a plasma that peaks at a ring under the coil and diffuses inward. Two or more coil zones, with an adjustable current ratio between them, let the radial ion-flux profile be tuned from center-high to edge-high. In the isolation etch, this ratio is one of the main knobs for radial depth uniformity (Chapter 7).

### 5.2.3 Capacitive Coupling and Window Sputtering

The coil also couples capacitively through the window. The RF voltage on the coil drives ions into the window, sputtering it and adding window material (Al, Y, O) to the plasma. A Faraday shield (a slotted conductor between the coil and the window) suppresses this and can be partly opened during cleans to sputter deposits off the window. Window temperature control (heaters or air cooling) keeps deposition on the window stable from wafer to wafer.

---

## 5.3 The Bias

### 5.3.1 Ion Energy From Bias Power

The wafer chuck carries a separate RF bias, typically 13.56 MHz in silicon trench etch. Almost all the bias power goes into accelerating ions across the sheath, so the mean sheath voltage can be estimated from power and ion current:

```
⟨V_sh⟩ ≈ η P_bias / I_i      (η ≈ 0.85: fraction of bias power delivered
                             to ions; the rest heats electrons and losses)

ME-1 during the pulse-on phase:
  P_bias = 450 W (peak)
  J_i,on ≈ 4.0 mA/cm² over 707 cm² → I_i = 2.83 A
  ⟨V_sh⟩ ≈ 0.85 × 450 / 2.83 = 135 V

Mean ion energy ≈ e(⟨V_sh⟩ + V_p) ≈ 135 + 15 ≈ 150 eV

ME-2 (800 W source at 12 mTorr, J_i,on ≈ 3.6 mA/cm² → I_i = 2.55 A):
  ⟨V_sh⟩ ≈ 0.85 × 380 / 2.55 = 127 V → ≈ 140 eV
```

The relationship has a practical consequence: **at fixed bias power, anything that raises ion flux lowers ion energy.** More source power, a lower-ionization-potential gas, or a cleaner chamber that loses fewer ions to the walls all raise I_i and reduce the energy per ion. Some tools control bias voltage rather than power for this reason. Others monitor the bias voltage and use it in fault detection (Chapter 15).

### 5.3.2 Bias Frequency

At 13.56 MHz, heavy ions such as Br⁺ and HBr⁺ take several RF cycles to cross the sheath and respond mainly to the average sheath voltage, giving a relatively narrow energy distribution. Lower bias frequencies (400 kHz – 2 MHz) give broad, bimodal distributions with high-energy tails that increase mask faceting and damage. Chapter 6 develops this.

---

## 5.4 Gas Flow, Pumping, and Residence Time

### 5.4.1 Residence Time

```
Chamber volume (plasma region + pumping plenum): V ≈ 40 L = 0.040 m³
ME-1 total flow: HBr 200 + Cl₂ 40 + O₂ 6 + He 100 = 346 sccm
  1 sccm = 1.69×10⁻³ Pa·m³/s → Q = 0.585 Pa·m³/s
Pressure: 8 mTorr = 1.07 Pa

Residence time: τ = pV / Q = 1.07 × 0.040 / 0.585 = 0.073 s ≈ 73 ms
Effective pumping speed at the chamber: S = Q / p = 0.585 / 1.07
                                          = 0.55 m³/s = 550 L/s
```

A turbomolecular pump of 2000–3500 L/s behind a throttle valve and an annular baffle delivers this with enough reserve to reach lower pressures at full flow. The throttle valve sets the pressure. The flow and the pressure together set the residence time.

### 5.4.2 How Much of the Gas Is Etch Product?

```
Si removal rate over the wafer:
  Γ_Si (open-area) = 2.5×10¹⁶ cm⁻² s⁻¹ (Chapter 3), open fraction 0.60,
  area 707 cm² (and narrow trenches slower; take 85% on average)

  Ṅ_Si ≈ 2.5×10¹⁶ × 0.60 × 707 × 0.85 = 9.0×10¹⁸ Si atoms/s

  1 sccm = 4.48×10¹⁷ molecules/s → 9.0×10¹⁸ / 4.48×10¹⁷ ≈ 20 sccm of
  SiXₙ product

Feed: 346 sccm → products ≈ 6% of the gas leaving the chamber
```

Six percent is a large fraction. These products redeposit on the wafer, the walls, and the window, and they are the silicon source for the sidewall passivation (Chapter 4). This is why the product fraction, and with it the passivation, depends on open area (macroloading), on total flow, and on the chamber wall state.

```
Effect of total flow at fixed pressure (product fraction ∝ 1/Q):
  346 sccm → 6%
  700 sccm → 3% (τ ≈ 36 ms; needs ≈ 1100 L/s)
  Lower product fraction → thinner passivation, less taper, less
  loading sensitivity; more gas cost and pump load
```

### 5.4.3 Gas Injection

Gas enters through a center nozzle in the window and, on most modern tools, through additional side or edge injectors. The split between center and edge injection changes the radial radical profile and is a radial-uniformity knob (Chapter 7).

---

## 5.5 Chamber Body and Materials

```
Component                    Material (typical)             Concern
──────────────────────────────────────────────────────────────────────────────
Chamber walls and liner      Anodized Al with Y₂O₃ or       Erosion; particle
                             YOF coating; heated liner      release; Y and Al
                             (60–120 °C)                    contamination
Window                       Al₂O₃ or quartz, Y₂O₃-coated   Sputter (capacitive
                                                            coupling); deposits
Gas nozzle                   Y₂O₃ or Al₂O₃ ceramic          Erosion; flow change
Edge ring                    Si, SiC, or quartz            Wear → edge tilt and
                                                            edge CD (Chapter 9)
ESC surface                  Al₂O₃ or AlN ceramic           Chucking force; He
                                                            leak; particles
```

Bromine and chlorine attack bare aluminium and stainless steel, so every plasma-facing surface is a ceramic or a coating. The liner is heated to keep etch products from condensing on it as thick, flaky deposits and to make the wall a reproducible surface (Chapter 9).

---

## 5.6 The Chuck

The electrostatic chuck (ESC) holds the wafer, carries the bias, and controls wafer temperature through backside helium and a temperature-controlled base with embedded heaters in several radial zones. Chapter 8 covers it in detail. Two numbers matter here:

```
Heat load during ME-1 (illustrative):
  Bias power to ions:      450 W × 0.5 duty × 0.85 ≈ 190 W
  Ion neutralization,
  recombination, radiation ≈ 100 W
  Total                    ≈ 290 W over 707 cm² ≈ 0.41 W/cm²

Wafer-to-chuck temperature rise through the He gap
  (R ≈ 1.5 K·cm²/W):       ΔT ≈ 0.41 × 1.5 ≈ 0.6 °C
```

The wafer runs less than a degree above the chuck surface, and its temperature follows the chuck setpoint closely. This is why chuck zone temperatures are such effective radial knobs.

---

## 5.7 Throughput and Fleet Size

### 5.7.1 Chamber Cycle Time

```
Activity                                       Time (s, illustrative)
─────────────────────────────────────────────────────────────────────
Wafer transfer in, chuck, He fill, stabilize   25
Breakthrough                                   8
Gas stabilization                              5
Main etch (ME-1 + ME-2)                        62
Profile step                                   6
Dechuck, pump-out, transfer out                20
Waferless autoclean + season (every wafer)     40
─────────────────────────────────────────────────────────────────────
Total                                          166 s ≈ 2.8 min
Wafers per hour per chamber:                   3600 / 166 ≈ 21.7
```

The plasma etch itself is less than half of the cycle. Transfer, stabilization, and the per-wafer clean and season take the rest. Shortening the clean is often worth more throughput than speeding up the etch, but the clean protects wafer-to-wafer stability (Chapter 9).

### 5.7.2 Fleet Size

```
DRAM fab output: 100,000 wafer starts per month (WSPM)
  Isolation etch passes per wafer: 1
  Required rate: 100,000 / (30 × 24) = 139 wafers/hour

Chamber availability (after PM, qualification, idle): 85%
Effective WPH per chamber: 21.7 × 0.85 = 18.4

Chambers needed: 139 / 18.4 = 7.5 → 8 production chambers
  plus engineering and redundancy → ≈ 10 chambers
  (≈ 2–3 mainframes with 4 chambers each)
```

### 5.7.3 Chamber Matching

Every chamber in the fleet must produce the same islands. Matching is done on the outputs, not only on the inputs:

```
Matched output (illustrative tolerance between chambers)
───────────────────────────────────────────────────────────
Cell depth (line space)               ± 3 nm
Periphery depth (open)                ± 4 nm
AA top width                          ± 0.3 nm
AA width at 140 nm                    ± 0.5 nm
Sidewall angle                        ± 0.1°
Remaining cap                         ± 1 nm
Edge tilt at 147 mm                   ± 0.1°
Defect density                        Within fleet control limits
```

Input matching (delivered RF power, gas flow calibration, pressure gauge calibration, chuck temperature calibration, edge-ring height) removes most differences. The rest is removed by chamber-specific offsets on time and on a few radial knobs, maintained by APC (Chapter 15).

---

## 5.8 Summary & Key Takeaways

1. **ICP fits the window.** Silicon trench etch needs high ion flux at 100–200 eV and low pressure. Independent source and bias give exactly that.

2. **Ion energy comes from bias power divided by ion current.** At 450 W and 2.83 A, the mean ion energy is about 150 eV. Raising flux at fixed power lowers energy.

3. **Etch products are a large part of the gas.** About 20 sccm of silicon halide leaves a 60%-open wafer, around 6% of the gas. It feeds passivation and loading.

4. **Residence time is short.** About 73 ms at 8 mTorr and 346 sccm, set by flow and pressure together.

5. **The cycle is mostly not etching.** Of a 166 s cycle, 62 s is main etch. A 100k WSPM fab needs about 10 chambers.

6. **Chambers are matched on outputs.** Depth, AA width, angle, cap, and edge tilt are matched to tight tolerances using calibrated inputs plus chamber-specific offsets.

---

## Study Questions

1. A recipe uses 300 W of bias power with an ion current density of 3.0 mA/cm² across a 300 mm wafer. Estimate the mean sheath voltage and the mean ion energy (V_p = 15 V). If source power is raised so that ion current density becomes 3.6 mA/cm² at the same bias power, what happens to the mean ion energy?

2. Compute the residence time for ME-2 (HBr 220, O₂ 8, NF₃ 3, He 120 sccm) at 12 mTorr in a 40 L chamber. What effective pumping speed is required?

3. A new product has an open silicon fraction of 0.66 instead of 0.60. Estimate the change in etch-product flow and in product fraction in ME-1. What do you expect for the sidewall angle and why?

4. A fab wants to drop the per-wafer clean and season to every fifth wafer, saving 32 s on average per wafer. Compute the new WPH and the number of production chambers needed for 100k WSPM. What risks should be weighed against the saving?

5. Two chambers differ by 0.4 nm in AA width at 140 nm depth and by 4 nm in cell depth. List the input checks you would make first, and the outputs you would compare to separate a temperature difference from an RF difference.

---

**Next Chapter:** [Chapter 6: Ion Energy, Bias Pulsing & Angular Control](./06-ion-energy-pulsing.md)

---

**Chapter 5 Development Status:** Complete  
**Version:** 1.0
