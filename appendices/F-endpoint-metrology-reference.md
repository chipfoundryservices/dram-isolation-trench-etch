# Appendix F: Endpoint & Metrology Reference

Signals, methods, sampling, and control limits for the DRAM isolation etch module. Values are illustrative.

---

## F.1 In-Situ Signals by Step

```
Step          Signal                          Use                        Typical behavior
───────────────────────────────────────────────────────────────────────────────────────────────
HM open       CN 387.1 nm                     SiN clear                  Falls at SiN clear
(SiN, pad)    CO 483.5 nm, O 777 nm           Pad oxide clear            Falls at Si exposure
              SiF 440 nm                      Si exposure                Rises at Si exposure
BT            CO 483.5 nm                     Monitor only (timed)       Small, short transient
STAB          Pressure, flows                 Gas exchange complete      Settle within 3 s
ME-1 / ME-2   Si I 288.2 nm                   Wafer-level Si removal     Flat; level ∝ rate ×
                                                                         open area
              Br 827 / Ar 750                 Br density                 Flat within ±2%
              O 777 / Ar 750                  O density (passivation)    Flat; drift = wall or
                                                                         MFC change
              H α 656.3 nm                    H; moisture; leak          Flat; rise = leak or
                                                                         wet gas
              Bias Vpp / Vdc                  Ion energy, flux           Within ±3%
              Pulse readback (duty, phase)    Pulsing health             Exact
PS            Bias Vpp                        Low-energy step            Within ±5%
WAC           SiF 440 nm                      Wall deposits removed      Decays to baseline;
                                                                         time-to-baseline is
                                                                         a drift monitor
```

---

## F.2 Fault Detection Summary Statistics

```
Signal                       Statistic per step          Limit (illustrative)
──────────────────────────────────────────────────────────────────────────────
Source / bias delivered      Mean                         ±2% of setpoint
power
Bias Vpp                     Mean, slope                  ±3% of reference; slope
                                                          within reference band
Match capacitor positions    Mean                         ±3% of reference
Reflected power              Max                          < 2% of forward
Pressure                     Mean, std                    ±2%; std < 1%
Throttle position            Mean                         ±5% of reference
                                                          (pump or leak)
MFC flows (O₂, NF₃)          Mean                         ±1% of setpoint
ESC zone temperatures        Mean                         ±0.5 °C
He leak per zone             Mean                         < 1.5× reference
Pulse duty / frequency       Readback                     Exact; any deviation =
                                                          fault
Si 288 integral (ME)         Integral                     ±3% of reference
O/Ar, Br/Ar                  Mean                         ±3% of reference
WAC endpoint time            Time                         ±15% of reference
```

---

## F.3 Post-Etch Metrology Methods

```
Method              Parameters                          Precision (3σ)      Throughput
───────────────────────────────────────────────────────────────────────────────────────────
OCD                 Depth (per space type), W_t,        0.6–1.0 nm depth;   1–2 min/site
                    W(50/140/180), SWA per segment,     0.2–0.3 nm W_t;
                    bottom radius, cap remaining        0.4–0.6 nm W(140);
                                                        0.05–0.1° SWA
CD-SEM              W_t, S_t per type, LWR/LER, island  0.3 nm CD;          < 1 min/site
                    ends, top-offset (lean)             0.5 nm LER
CD-SAXS             Average profile, pitch walk         0.3–0.5 nm          10–30 min/site
TEM / STEM          Full profile; damage layer; end     Reference (≈ 0.3    Days
                    profile along AA                    nm with care)
E-beam inspection   Bridges, collapse, missing spaces   Single defect       Sampled areas
Optical inspection  Particles, clusters                 ≥ 20–30 nm          Full wafer
VPD-ICPMS / TXRF    Metals on monitor wafers            10⁸–10⁹ cm⁻²        Hours
```

---

## F.4 OCD Model Checklist

```
□ Space types α / β / γ represented (or pitch-walk parameter)
□ Sidewall angle by segment (ME-1 above ≈ 120 nm, ME-2 below)
□ Bottom rounding radius
□ Cap and SiN thickness floating (mask erosion)
□ Material dispersion for Si (doping), SiO₂ cap (deposition type),
  SiN; SiOₓBrᵧ film if measuring before clean
□ Fixed parameters set from CD-SEM (W_t) where correlated
□ TEM validation after any model change (Appendix C.7)
□ Correlation matrix reviewed: |r(depth, SWA)| < 0.8
```

---

## F.5 Sampling Plan (Per Lot, Illustrative)

```
Location                      Method        Wafers × sites
─────────────────────────────────────────────────────────────
Cell array (radial)           OCD           2 × 13
Cut-gap target                OCD / SEM     2 × 5
Array edge                    SEM           1 × 5
Periphery 60 / 100 nm / open  OCD           2 × 9
Extreme edge (r ≥ 145 mm)     OCD           2 × 4
Top-down (W_t, spaces, LWR)   CD-SEM        1 × 9
Cross-section                 TEM           Per chamber, weekly
Bridges / collapse            E-beam        Per chamber, daily
Particles                     Optical       1 per lot
Metals                        VPD-ICPMS     Per chamber, weekly / post-PM
```

---

## F.6 Electrical Monitors

```
Structure                        Measured at             Indicates
──────────────────────────────────────────────────────────────────────────
Perimeter / area diode sets      FEOL test (85 °C)       Sidewall leakage J_P
Array-like diode (cell layout)   FEOL test               Leakage in real
                                                         geometry
Gated diode / charge pumping     FEOL test               Sidewall D_it
AA bridge chains (comb /         FEOL test               Bridging, collapse
serpentine on cell layout)
Parasitic field transistor       After WL                Oxide margin under the
(passing WL over isolation)                              WL; isolation depth
Retention test arrays            Probe                   Tail directly
Minority-carrier lifetime /      Monitor wafers          Fe and other metals
SPV (Fe-B pairing)
```

---

## F.7 Control Limits and Specifications

```
Parameter                  Target     Control limits (±)    Specification
───────────────────────────────────────────────────────────────────────────
Cell depth                 250 nm     12 nm                 220–280 nm
Periphery open depth       310 nm     12 nm                 280–330 nm
Periphery 60 nm depth      287 nm     10 nm                 ≥ 270 nm
W_t                        14.0 nm    0.6 nm                ±1.0 nm (3σ)
W(140)                     18.9 nm    1.0 nm                ±1.5 nm (3σ)
SWA (cell)                 1.0°       0.15°                 0.7–1.25°
S(250)                     9.3 nm     1.2 nm                ≥ 7 nm
Depth walk (range)         ≤ 5.5 nm   7 nm                  ≤ 12 nm (±6)
Island-end pull-back       ≤ 5 nm     2 nm                  ≤ 8 nm
Lean (top offset)          < 1 nm     1.5 nm                ≤ 2 nm
Remaining cap              10.7 nm    1.5 nm                ≥ 8 nm
Edge tilt (r = 147 mm)     0°         0.2°                  ±0.3°
```

---

**Appendix F Version:** 1.0
