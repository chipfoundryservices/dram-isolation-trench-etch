# Appendix A: Silicon, Mask, Liner & Chamber Material Properties

Reference data for the materials in and around the DRAM isolation trench. Values are representative room-temperature values unless noted, and are intended for estimates. Chapter references point to where each value is used.

---

## A.1 Silicon

```
Property                                 Value                         Used in
──────────────────────────────────────────────────────────────────────────────────
Density                                  2.33 g/cm³
Atom density                             5.0×10²² cm⁻³                 Ch. 3.1
Lattice constant                         0.543 nm
Young's modulus  ⟨100⟩                   130 GPa
                 ⟨110⟩ (in-plane, fin    169 GPa                       Ch. 11
                 bending, typical)
Poisson ratio (⟨110⟩ in-plane)           ≈ 0.06–0.28 (direction-
                                         dependent)
Thermal conductivity (bulk)              150 W/(m·K)                   Ch. 8
  (thin fins, < 30 nm: reduced by
  boundary scattering, ≈ 20–50)
Specific heat                            700 J/(kg·K)                  Ch. 8.2
Band gap (300 K)                         1.12 eV
Intrinsic carrier density  300 K         1.0×10¹⁰ cm⁻³                 Ch. 13
                           358 K (85 °C) ≈ 4.4×10¹¹ cm⁻³
                           368 K (95 °C) ≈ 7.5×10¹¹ cm⁻³
Electron thermal velocity (358 K)        ≈ 1.2×10⁷ cm/s                Ch. 13
Si consumed per nm of thermal oxide      0.44 nm                       Ch. 13.3
Wafer thickness (300 mm)                 775 µm                        Ch. 8.2
```

---

## A.2 Hard-Mask and Liner Films

```
Film                    Density     Modulus    Stress            Notes
                        (g/cm³)     (GPa)      (typical)
──────────────────────────────────────────────────────────────────────────────────────
Thermal SiO₂ (pad)      2.27        70–75      −300 MPa (comp.)  4 nm reference
PECVD / ALD SiO₂ (cap)  2.1–2.2     60–70      −100 to −200 MPa  20 nm reference
LPCVD Si₃N₄             3.0–3.1     220–280    +1.0–1.2 GPa      25 nm reference;
                                               (tensile)         CMP stop
Radical (ISSG) liner    2.25        70         compressive       2.5 nm reference
oxide
ALD SiO₂ (cell fill)    2.0–2.2     50–70      low               Seam at center
Flowable / SOD oxide    1.9–2.2     30–60      tensile after     Shrinks 10–15% on
(periphery fill)        (after cure)            cure              cure / anneal
ALD SiN liner           2.8–3.0     200–250    tensile           Periphery only
                                                                 (Ch. 16)
```

### A.2.1 Etch Rates in Post-Etch Wet Chemistry (Illustrative, Room Temperature)

```
Film                     Dilute HF (100:1)     SC1 (1:1:50, 50 °C)   Hot H₃PO₄ (160 °C)
───────────────────────────────────────────────────────────────────────────────────────
Thermal SiO₂             ≈ 4–5 nm/min          < 0.1 nm/min          ≈ 0.1 nm/min
PECVD / ALD SiO₂         ≈ 8–20 nm/min         ≈ 0.1–0.3 nm/min      ≈ 0.2–0.5 nm/min
LPCVD Si₃N₄              ≈ 0.1–0.2 nm/min      < 0.05 nm/min         ≈ 4–6 nm/min
Si (undoped)             ≈ 0                   ≈ 0.2–0.5 nm/min      ≈ 0
SiOₓBrᵧ passivation      Fast (seconds)        —                     —
```

---

## A.3 Plasma Etch Rates and Selectivities (Reference Recipe, Illustrative)

```
Step     Si open-area rate    SiO₂ rate     SiN rate      Si:SiO₂    Si:SiN
──────────────────────────────────────────────────────────────────────────────
BT       ≈ 60 nm/min          ≈ 11 nm/min   ≈ 15 nm/min   ≈ 5        ≈ 4
ME-1     ≈ 330 nm/min         ≈ 8.5 nm/min  ≈ 22 nm/min   ≈ 39       ≈ 15
ME-2     ≈ 270 nm/min         ≈ 6.5 nm/min  ≈ 18 nm/min   ≈ 42       ≈ 15
PS       ≈ 90 nm/min          ≈ 1 nm/min    ≈ 3 nm/min    ≈ 90       ≈ 30
Average  300 nm/min (ME)      7.5 nm/min    —             40         —
```

---

## A.4 Reference Geometry

```
Quantity                                Value
─────────────────────────────────────────────────────────────
F / WL pitch / BL pitch                 17 / 34 / 51 nm
Cell area 6F²                           1734 nm²
AA pitch (normal to line)               32 nm
AA top width W_t / line space S_t       14 / 18 nm
Island length L_AA / cut gap G          84 / 24 nm
AA period along the line                108 nm
AA tilt from bit-line direction         ≈ 20°
Cell depth / periphery depth            250 / 300 nm (targets)
Hard mask (SiO₂ / SiN / pad)            20 / 25 / 4 nm (h_m = 49 nm)
Sidewall angle                          1.0°
AA width at 140 / 180 / 250 nm          18.9 / 20.3 / 22.7 nm
Trench bottom width (cell)              9.3 nm
Equivalent fin width w_eff              20.8 nm
Buried WL bottom (AA / isolation)       140 / 180 nm
Liner oxide                             2.5 nm (1.1 nm Si per side)
Open Si fraction (wafer)                ≈ 0.60
```

---

## A.5 Liquids for Clean and Dry

```
Liquid                      Surface tension γ     Notes (Ch. 11)
                            at 25 °C (N/m)
────────────────────────────────────────────────────────────────────────
Water                       0.072                 Reference fin unstable
                                                  (M = 0.45)
Isopropyl alcohol (IPA)     0.022                 M ≈ 1.5
Acetone                     0.023
Hydrofluoroether (HFE)      0.013–0.016           Lower load; chemistry
                                                  compatibility
Supercritical CO₂           0 (no meniscus)       No capillary load
Contact angle, water on:
  hydroxylated oxide        < 10° (cos θ ≈ 1)
  H-terminated Si (HF-last) 70–80° (cos θ ≈ 0.2–0.35)
```

---

## A.6 Chamber Materials

```
Component              Material                   Erosion / concern               Ch.
───────────────────────────────────────────────────────────────────────────────────────
Wall liner             Anodized Al + Y₂O₃ or YOF  Coating erosion; Y and Al       5, 9
                       coating; heated            particles
Window                 Al₂O₃ or quartz; Y₂O₃      Capacitive sputter; deposits    5, 9
                       coated
Gas nozzle             Y₂O₃ / Al₂O₃               Erosion changes flow pattern    5
Edge ring              Si / SiC / quartz          ≈ 0.05 µm per RF hour (Si,      9
                                                  illustrative); tilt drift
ESC surface            Al₂O₃ or AlN (JR type)     Wear; He leak; particles        8
Gas lines              Electropolished 316L SS    Corrosion by wet HBr → Fe, Ni,  9
                                                  Cr contamination
```

---

## A.7 Metal Contamination Limits (On-Wafer, Illustrative)

```
Element             Limit (atoms/cm²)      Concern
──────────────────────────────────────────────────────────────────
Fe, Ni, Cr          < 5×10⁹                Mid-gap traps; retention tail
Cu                  < 1×10⁹                Fast diffuser; precipitates
Y, Al               < 1×10¹⁰               Chamber coatings; particles
Na, K               < 1×10¹⁰               Mobile ions
Atoms per SN junction sidewall area (3.2×10⁻¹¹ cm²) at 1×10¹⁰ cm⁻²:
≈ 0.32 (Ch. 13.1.5)
```

---

**Appendix A Version:** 1.0
