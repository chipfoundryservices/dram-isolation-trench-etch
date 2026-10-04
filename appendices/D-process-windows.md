# Appendix D: Process Windows & Lookup Tables

Starting recipes, sensitivities, and lookup tables for the reference DRAM isolation etch. All values are illustrative and consistent with the models of Chapters 3, 10, 11, and 12. Use them as starting points for a design of experiments, not as qualified conditions.

---

## D.1 Reference Recipe

```
Step   Time   p        Source /     Pulsing          Gases (sccm)               ESC
              (mTorr)  bias (W)                                                 (°C, C/E)
─────────────────────────────────────────────────────────────────────────────────────────────
BT     8 s    5        500 / 150    CW               CF₄ 80, He 50              50 / 52
STAB   5 s    8        0 / 0        —                HBr 200, Cl₂ 40, O₂ 6,     50 / 52
                                                     He 100
ME-1   30 s   8        900 / 450    Sync, 1 kHz,     HBr 200, Cl₂ 40, O₂ 6,     50 / 52
                       (peak)       50%              He 100
ME-2   32 s   12       800 / 380    Sync, 1 kHz,     HBr 220, O₂ 8, NF₃ 3,      50 / 52
                       (peak)       40%              He 120
PS     6 s    20       600 / 60     CW               HBr 150, He 150            50 / 52
─────────────────────────────────────────────────────────────────────────────────────────────
After each wafer: WAC (NF₃/O₂, ≈ 20 s, SiF endpoint) + SEASON (SiCl₄/O₂, ≈ 20 s)

Outputs: cell 250 nm, periphery 60 nm / 100 nm / open = 287 / 296 / 310 nm,
W_t 14.0 nm, W(140) 18.9 nm, α 1.0°, S(250) 9.3 nm, cap remaining 10.7 nm
```

---

## D.2 Sensitivities (Around the Reference)

```
Lever                           Cell D    Peri open D   W_t      W(140)    α         S(250)
                                (nm)      (nm)          (nm)     (nm)      (°)       (nm)
──────────────────────────────────────────────────────────────────────────────────────────────
Main-etch time +1 s             +3.5      +5.0          0        0         0         −0.1
O₂ (ME-2) +1 sccm               −1.5      −1.0          0        +1.2      +0.25     −2.2
NF₃ (ME-2) +1 sccm              +1.0      +1.5          0        −0.7      −0.15     +1.3
Cl₂ (ME-1) +10 sccm             +2.0      +3.0          −0.4     −0.5      −0.02     +0.6
Bias (ME-2) +40 W               +2.5      +4.0          0        −0.5      −0.10     +0.9
Duty (ME-2) +10% (abs.)         +2.0      +7.0          0        −0.3      −0.06     +0.5
ME-2 pressure +1 mTorr          +0.75     −1.75         0        +0.25     +0.05     −0.45
Wafer temperature +1 °C         +0.3      +0.3          −0.04    −0.09     −0.010    +0.1
Total flow (ME-2) +100 sccm     +1.0      +1.5          0        −0.4      −0.08     +0.7
PS time +2 s                    +1.7      +1.7          0        0         0         +0.3
                                                                                     (rounding)
```

---

## D.3 Time-to-Depth Tables

ER₀ = 300 nm/min, h_m = 49 nm, straight walls (Chapter 3 model). Depths in nm.

### D.3.1 Reference Recipe, k = 0.025

```
  t (s)   S=15   S=16   S=18   S=20   S=24   60 nm   100 nm   open
  ─────────────────────────────────────────────────────────────────────
  50      200    202    206    210    215    234     240      250
  55      218    220    225    228    234    256     263      275
  58      228    231    235    239    246    269     277      290
  62.1    242    245    250    254    262    287     296      310
  66      255    258    264    268    276    304     314      330
  70      268    272    278    283    291    322     332      350
```

### D.3.2 Reduced Pulsing, k = 0.040

```
  t (s)   S=15   S=16   S=18   S=20   S=24   60 nm   100 nm   open
  ─────────────────────────────────────────────────────────────────────
  50      182    185    189    194    200    226     234      250
  55      197    200    206    210    218    247     257      275
  58      206    209    215    220    228    259     270      290
  62.1    218    222    228    233    242    276     288      310
  66      230    233    240    246    255    292     305      330
  70      241    245    252    258    268    308     323      350
```

At k = 0.040 the cell reaches 220 nm only after about 59.5 s, and the window (Chapter 12) narrows to 60.6–66.0 s.

---

## D.4 Cell / Periphery Window vs. k

```
  k        Window (s)        Width     Binding limits
  ─────────────────────────────────────────────────────────────────
  0.020    57.3 – 66.0       8.7 s     peri 60 nm / peri open
  0.025    58.1 – 66.0       7.9 s     peri 60 nm / peri open
  0.032    59.3 – 66.0       6.7 s     peri 60 nm / peri open
  0.040    60.6 – 66.0       5.4 s     peri 60 nm / peri open
  0.050    63.4 – 66.0       2.6 s     cell 220 nm / peri open
  0.057    none (k_max ≈ 0.0566)    —   cell 220 nm vs. peri open
  0.058    none              —         —
```

---

## D.5 Profile Lookup (S_t = 18 nm, W_t = 14 nm)

```
  α (°)    W(140)    W(180)    W(250)    S(250)    z_close    w_eff
  ──────────────────────────────────────────────────────────────────────
  0.5      16.4      17.1      18.4      13.6      1031       ≈ 16.8
  0.7      17.4      18.4      20.1      11.9      737        18.8
  0.9      18.4      19.7      21.9      10.1      573        ≈ 20.1
  1.0      18.9      20.3      22.7      9.3       516        20.8
  1.1      19.4      20.9      23.6      8.4       469        ≈ 21.5
  1.25     20.1      21.9      24.9      7.1       413        22.4
  1.5      21.3      23.4      27.1      4.9       344        —
  2.0      23.8      26.6      31.5      0.5       258        —
```

---

## D.6 Collapse Margin Lookup (IPA, s = 18 nm)

```
M = 1.03 E w_eff³ / H⁴ ÷ (4 γ cos θ / s²),  γ = 0.022 N/m, cos θ = 1

  w_eff \ H   200 nm   220 nm   240 nm   250 nm   260 nm   280 nm
  ──────────────────────────────────────────────────────────────────
  18 nm       2.34     1.60     1.13     0.96     0.82     0.61
  19 nm       2.75     1.88     1.32     1.13     0.96     0.72
  20 nm       3.20     2.19     1.55     1.31     1.12     0.83
  20.8 nm     3.60     2.46     1.74     1.48     1.26     0.94
  22 nm       4.27     2.91     2.06     1.75     1.49     1.11
  23 nm       4.87     3.33     2.35     2.00     1.71     1.27

For water (γ = 0.072), divide by 3.27.
```

---

## D.7 Liner Thickness vs. AA Width and Fill Gap

```
  Liner t_ox   Si per side   W_t after   W(140) after   Bottom gap (α = 1.0°)
  ──────────────────────────────────────────────────────────────────────────
  1.5 nm       0.66 nm       12.7 nm     17.6 nm        7.6 nm
  2.0 nm       0.88 nm       12.2 nm     17.1 nm        7.1 nm
  2.5 nm       1.10 nm       11.8 nm     16.7 nm        6.5 nm
  3.0 nm       1.32 nm       11.4 nm     16.3 nm        5.9 nm
  4.0 nm       1.76 nm       10.5 nm     15.4 nm        4.8 nm

Bottom gap = S(250) − 2 × (t_ox − Si consumed) = 9.3 − 2 × 0.56 t_ox
```

---

## D.8 Remaining Mask

```
Cap loss = BT loss (≈ 1.5 nm) + (ER₀ / S_ox) × t_ME + facet allowance

  t_ME (s)    S_ox = 40     S_ox = 34     S_ox = 28
  ───────────────────────────────────────────────────
  55          ≈ 11.6 nm     ≈ 10.4 nm     ≈ 8.7 nm
  62.1        ≈ 10.7 nm     ≈ 9.4 nm      ≈ 7.4 nm
  70          ≈ 9.8 nm      ≈ 8.2 nm      ≈ 6.0 nm

Remaining SiO₂ cap from 20 nm (planar; facets on 14 nm lines remove
the flat top earlier). Spec ≥ 8 nm.
```

---

**Appendix D Version:** 1.0
