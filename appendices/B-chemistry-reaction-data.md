# Appendix B: Chemistry & Reaction Data

Gas properties, bond energies, product volatility, key reactions, emission lines, and transport tables for silicon isolation etch in HBr/Cl₂/O₂ chemistry. Values are representative and intended for estimates.

---

## B.1 Process Gases

```
Gas      MW (g/mol)   Role in the isolation etch           Handling notes
──────────────────────────────────────────────────────────────────────────────────────
HBr      80.9         Main etchant; H scavenges O and F    Corrosive with moisture;
                                                           low-moisture supply; purged
                                                           lines (Ch. 9)
Cl₂      70.9         Rate, smoothness (ME-1)              Corrosive; toxic
O₂       32.0         Passivation (SiOₓBrᵧ)                Low-range MFC (Ch. 7)
NF₃      71.0         Thins passivation (ME-2); WAC        Low-range MFC; oxidizer
CF₄      88.0         Breakthrough                         Carbon and F residue
He       4.0          Diluent; plasma stability            —
Ar       39.9         Actinometry (small flow); diluent    —
SiCl₄    169.9        Season coating (with O₂)             Moisture-sensitive liquid
                                                           source
```

---

## B.2 Bond Energies (Approximate)

```
Bond                         Energy (eV)    kJ/mol    Relevance
──────────────────────────────────────────────────────────────────────────────
Si–Si (crystal)              2.3            ≈ 226     Bulk Si
Si–O (in SiO₂, per bond)     4.6            ≈ 450     Mask; passivation stability
Si–O (SiO molecule)          8.3            ≈ 800
Si–F                         5.7–6.0        ≈ 560–580 Spontaneous Si etch by F
Si–Cl                        4.0            ≈ 400
Si–Br                        3.4            ≈ 330     Lower than Si–O → oxide
                                                      not etched by Br
Si–H                         3.1            ≈ 300
H–Br                         3.8            366
H–Cl                         4.4            431
Br–Br                        2.0            193       Easy dissociation of Br₂
Cl–Cl                        2.5            243
```

---

## B.3 Etch Product Volatility

```
Product     Boiling point (°C)     Comment
──────────────────────────────────────────────────────────────────
SiF₄        −86 (sublimes −95)     Very volatile; F-based etch isotropic
SiCl₄       57.6                   Volatile; Cl-based etch smooth
SiBr₄       153                    Less volatile; redeposits readily →
                                   self-passivation (Ch. 4)
SiBr₂, SiCl₂ (radicals)            Reactive; stick on walls; oxidized to
                                   SiOₓXᵧ
```

---

## B.4 Key Reactions

```
At the trench bottom (ion-assisted):
  Si(s) + x Br(ads) → SiBrₓ(ads) → SiBrₓ(g)       (ion-induced desorption)
  Si(s) + x Cl(ads) → SiClₓ(g)

In the gas phase:
  HBr + e → H + Br + e                              (dissociation)
  Br₂ + e → 2 Br + e
  O₂ + e → 2 O + e
  H + O → OH ; H + F → HF                           (scavenging)

Passivation (sidewalls, chamber walls):
  SiBrₓ(ads) + O → SiOₓBrᵧ(s) + Br
  SiOₓBrᵧ is etched at the bottom by ions + Br, but not on sidewalls

Breakthrough:
  SiO₂ + CFₓ⁺ / F → SiF₄ + CO / CO₂                (ion-assisted)

WAC and season:
  SiOₓBrᵧ(wall) + NF₃ plasma → SiF₄ + Br + N₂ + O
  SiCl₄ + O₂ plasma → SiO₂(wall) + Cl₂               (season coating)
```

---

## B.5 Optical Emission Lines

```
Species     Wavelength (nm)      Use
──────────────────────────────────────────────────────────────────────────────
Ar I        750.4, 811.5         Actinometry reference
Br I        827.2, 863.9         Br density (Br/Ar actinometry)
Cl I        837.6                Cl density (ME-1)
O I         777.2, 844.6         O density; passivation supply; mask-open
F I         703.7                F after BT / during WAC
H α         656.3                H from HBr; moisture or leak indicator
Si I        288.2                Si-containing products: wafer-level rate
SiCl        ≈ 281–287 (band)     Products in Cl-containing steps
SiF         ≈ 436–443 (band)     WAC endpoint; mask-open (Si exposure)
CO          483.5, 519.8         Oxide etch (mask open, breakthrough)
CN          387.1                SiN clearing in the mask open
N₂          337.1                Leak / SiN etching
He I        587.6, 706.5         Diluent; plasma stability check
```

### B.5.1 Actinometry

```
n_X / n_Ar ≈ C × (I_X / I_Ar)

Valid when both emitting states are excited mainly by direct electron
impact from the ground state with similar threshold energies.
Example: O 777.2 / Ar 750.4 tracks relative O density; a slow drift
during a lot points to wall-state change (Ch. 9) or an O₂ MFC drift.
```

---

## B.6 Ion-Enhanced Yield Parameters (Illustrative)

```
Y(E) = A (√E − √E_th)

  Material / chemistry               E_th (eV)    A (atoms/ion/√eV)
  ───────────────────────────────────────────────────────────────────
  Si in HBr/Cl₂ (halogenated)        15           ≈ 0.19
  SiO₂ in HBr/O₂ (mask)              50           ≈ 0.0035*
  Ar⁺ physical sputter of Si         ≈ 30         ≈ 0.03

  * SiO₂ units per ion; scaled so that the thickness-rate ratio
    Si:SiO₂ ≈ 40 at 150 eV (Ch. 6.1), using 2.27×10²² SiO₂ units/cm³
    against 5.0×10²² Si atoms/cm³

Si yield at 150 eV: 0.19 × (12.25 − 3.87) ≈ 1.6 Si/ion   (Ch. 3.1.2)
```

---

## B.7 Neutral Transport Tables

### B.7.1 Transmission (Diffuse Walls, No Wall Loss)

```
  A       K_slot = (ln A + 0.15)/A      K_hole ≈ 1/(1 + 0.75A)
  ──────────────────────────────────────────────────────────────
  2.7     0.42                          0.33
  5       0.35                          0.21
  10      0.25                          0.12
  14      0.20                          0.087
  16.6    0.18                          0.074
  20      0.16                          0.063
```

### B.7.2 Coburn–Winters Bottom Rate Ratio (Slot)

```
ER_bottom / ER_open = K / (K + β(1 − K))

  A       β = 0.05    β = 0.10    β = 0.20
  ──────────────────────────────────────────
  2.7     0.94        0.88        0.79
  5       0.92        0.84        0.73
  10      0.87        0.77        0.62
  14      0.83        0.71        0.55
  16.6    0.81        0.68        0.52
```

### B.7.3 Ion Direct Transmission (Slot)

```
K_i ≈ 1 − 0.80 A σ_θ  (σ_θ in rad)

  σ_θ      A = 10     A = 16.6
  ──────────────────────────────
  1.0°     0.86       0.77
  1.5°     0.79       0.65
  2.0°     0.72       0.54
  3.0°     0.58       0.30
```

---

## B.8 Gas-Phase Reference Values (8 mTorr, 350 K)

```
Gas density                         2.2×10²⁰ m⁻³
Neutral mean free path              ≈ 8 mm
Ion mean free path (charge exch.)   ≈ 9 mm
Br mean speed                       ≈ 304 m/s
Br flux at n = 5×10¹³ cm⁻³          ≈ 3.8×10¹⁷ cm⁻² s⁻¹
Bohm speed (M = 80, T_e = 3 eV)     ≈ 1.9 km/s
Sheath (J_i = 4 mA/cm², 135 V)      ≈ 0.49 mm
Br⁺ transit time across sheath      ≈ 81 ns (vs. 74 ns RF period at 13.56 MHz)
```

---

**Appendix B Version:** 1.0
