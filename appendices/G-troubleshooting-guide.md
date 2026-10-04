# Appendix G: Troubleshooting Guide

Symptom-driven guide for DRAM isolation-etch excursions. For each symptom: likely causes ranked from most to least common, checks to separate them, and corrective actions. Chapter references point to the underlying physics.

---

## G.1 Cell Trenches Too Shallow (Periphery Normal)

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. ARDE increased (k up): pressure or      Peri/cell depth ratio vs.           Restore ME-2 pressure /
   duty changed, passivation up            reference; depth series             O₂; check pulsing
   (Ch. 3, 6, 12)
2. Incoming spaces narrow (litho, mask     CD-SEM S_t and mask-open bias;      Feed-forward on S_t;
   open taper) (Ch. 2)                     OCD top CD                          mask-open correction
3. Excess O₂ (MFC drift) → V-bottom        O/Ar trend; MFC check; SWA up;      Recalibrate MFC;
   self-limiting (Ch. 10)                  S(250) down                         O₂ trim via APC
4. Mask taller than usual (cap thick)      Incoming film thickness             Feed-forward time
5. Wafer cooler (more passivation)         ESC temps; He pressure              Restore setpoints
```

## G.2 Periphery Too Deep (Cell Normal or Shallow)

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Pulsing fault: step running CW          Pulse readback; bias Vpp pattern;   Repair generator /
   (k jumps toward 0.058) (Ch. 6, 15)      FDC history                         sync cable; re-qualify
2. Main-etch time too long for the         APC log; product open-area          Correct product
   product (wrong product constant)        fraction                            constants
3. Open-area rate up (clean walls,         First-wafer pattern; WAC endpoint   Season check;
   fluorine release) (Ch. 9)                                                   per-wafer season
4. Lower open-area fraction product        Layout data                         Feed-forward (Ch. 3.5.4)
```

## G.3 W(140) Too Wide / Sidewall Angle Too High

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. O₂ high (MFC, gas-line delay at step    MFC; O/Ar actinometry in ME-2;      Recalibrate; pre-flow /
   boundary) (Ch. 7)                       depth series                        carrier merge
2. Wall state: thicker deposits, more O    Drift within lot; WAC endpoint      Verify WAC + season;
   release (Ch. 9)                         time                                extend WAC
3. Wafer colder (zone or He fault)         Zone temps; He leak map             Restore; check ESC
   (Ch. 8)
4. NF₃ low / missing                       MFC; F 703.7 nm in ME-2             Restore
5. Bias low (delivered power)              RF calibration; Vpp                 Calibrate generator
```

## G.4 Trench Bottom Too Narrow / Closed (V-Bottom)

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Angle above limit (see G.3)             SWA by segment                      Fix angle source
2. Narrow space type from pitch walk       CD-SEM space types; OCD depth by    Patterning correction;
   (γ space) (Ch. 2, 10)                   type                                tighten pitch-walk spec
3. Profile step missing or too short       Recipe audit; bottom radius         Restore PS
4. Etch too deep for the angle             Depth                               Time correction
```

## G.5 Bow Below the Mask / Top AA Narrowed

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Mask facets grown (cap thin, energy     Remaining cap; facet in TEM;        Restore bias / duty;
   high) (Ch. 4, 10)                       Vpp                                 cap thickness check
2. ME-1 passivation thin (O₂ low, warm)    O/Ar in ME-1; zone temps            Restore O₂; temps
3. ME-1 pressure high (off-angle ions)     Pressure gauge, throttle            Calibrate gauge
   (Ch. 6.4)
4. Fluorine carry-over from breakthrough   STAB step present; F 703.7 at       Restore STAB; pump-out
   (Ch. 4.4.3)                             ME-1 start
```

## G.6 Island-End Pull-Back Excessive

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Lower passivation (O₂, temperature,     Same checks as G.3 in reverse;      Restore passivation
   wall state) (Ch. 12.4)                  side-wall W(140) also narrow?
2. Cut CD or placement change (litho)      Post-cut CD-SEM                     Litho / cut-OPC
3. Cut-OPC tuned for an older etch         Compare pull-back vs. qualified     Update OPC model
                                           baseline
```

## G.7 Fin Lean or Collapse

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Drying: IPA displacement incomplete,    Clean-tool logs; pattern of         Fix dryer; IPA purity
   water in IPA (Ch. 11)                   collapse (wafer-wide, random)       and replacement time
2. Pitch walk out of spec → asymmetric     Lean toward narrow space with SAQP  Patterning correction
   load (Ch. 11.3)                         period
3. Depth too deep (H⁴) or fins narrow      Depth, W_t, angle                   Restore; APC
   (w³) (Ch. 11.2)
4. Array-edge lines only                   Location; dummies in layout         Layout: more dummies
5. Wafer-edge only                         Edge tilt; surface stress           Edge ring compensation
                                           asymmetry                           (Ch. 9)
```

## G.8 Depth Walk Too Large

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Pitch walk increased (mandrel CD,       Post-SAQP CD-SEM by space type      SAQP APC (Ch. 2.2.3)
   spacer-1 thickness)
2. ARDE increased (k up)                   Cell/peri ratio                     See G.1 cause 1
3. Angle increased (taper coupling)        SWA                                 See G.3
```

## G.9 Retention Tail Degraded

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Metal contamination (gas line, part     VPD-ICPMS monitors; lifetime / SPV; Isolate chamber; fix
   erosion) (Ch. 9, 13)                    chamber correlation                 source; re-qualify
2. Sidewall damage up (energy, pulsing,    J_P on perimeter diodes; Vpp;       Restore; damage-aware
   pressure change)                        recipe audit                        recipe (Ch. 13.5)
3. Liner thinner or changed                Liner thickness; anneal logs        Restore liner
4. Profile: bow / sharp top corners →      TEM at island ends                  See G.5
   field
5. Shallow cell (parasitic channel under   Depth; parasitic field transistor   See G.1
   passing WL) (Ch. 12.8)
6. Residue (incomplete clean, Br left)     XPS / TOF-SIMS on test wafers;      Clean recipe; queue
                                           queue time                          time
```

## G.10 Edge-Ring Signature (Outer 3–10 mm)

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Ring wear beyond compensation curve     RF hours; tilt and depth at         Update lift / tuning;
   (Ch. 9.3)                               r = 145–147 mm                      replace ring
2. Edge zone temperature off (Ch. 8.5)     Zone temps; W(140) edge             Adjust edge zone
3. Wrong ring part or seating after PM     Part number; height gauge           Reinstall
4. Edge gas split changed                  Flow split log                      Restore
```

## G.11 Silicon Grass / Micromasking in the Periphery

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Residual pad oxide after mask open      Mask-open OES endpoint margin;      Mask-open overetch;
                                           location (pattern-dependent?)       BT time
2. O₂ above the window (Ch. 4.2.5)         MFC; O/Ar                           Recalibrate
3. Season film flakes (Ch. 9.2.2)          Random location; particle trend;    Season thickness;
                                           time since PM                       full WAC
4. Sputtered Y / Al from parts             EDX on cones; part condition        Replace parts
```

## G.12 AA Bridges / Particle Clusters

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Particles during etch (wall flakes,     Particle monitor trend; defect      Clean / PM; dechuck
   dechuck events) (Ch. 9.5)               review (EDX)                        sequence
2. Collapse (see G.7)                      Pairs vs. clusters; SAQP period     See G.7
3. Missing spaces (EUV stochastic or       Pre-etch inspection; pattern        Litho / resist
   litho defects) (Ch. 14.2.3)             repeat
```

## G.13 First-Wafer Effect or Drift Within a Lot

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Per-wafer WAC / season skipped or       Recipe sequence; WAC endpoint       Restore per-wafer
   shortened (Ch. 9.1.3)                   time
2. Season too thin (F leak-through on      F 703.7 nm in early ME-1;           Increase season
   wafer 1)                                narrow W_t on first wafer
3. Edge ring and puck warming through      Edge-only drift; ring temperature   Warm-up wafers;
   the lot (Ch. 8.5)                                                           feed-forward offsets
4. Idle-time wall changes                  Drift after idle                    Idle season recipe
```

## G.14 Oxide Cap Consumed Locally

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Incoming cap thin (deposition           Incoming thickness map              Deposition fix;
   non-uniformity)                                                             feed-forward time
2. Selectivity down (energy up, O₂ down)   Vpp; O/Ar; Si:SiO₂ on monitors      Restore
3. Etch too long (product constant)        APC log                             Correct
4. Facets merged on 14 nm lines            TEM of mask top                     Lower energy / duty
   (Ch. 4.3.2)
```

---

**Appendix G Version:** 1.0
