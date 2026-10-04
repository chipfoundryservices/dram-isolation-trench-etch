# Chapter 9: Chamber Walls, Edge Control & Contamination

## Overview

A silicon etch chamber is not a fixed piece of hardware. Its walls are coated with etch products, cleaned, and coated again with every wafer. Its edge ring erodes by micrometres over hundreds of RF hours. Its ceramic surfaces slowly release yttrium, aluminium, and particles. Each of these changes the plasma or the wafer, and in the isolation etch each one shows up in the silicon left behind: in depth, in AA width, in the profile at the wafer edge, and in the defects and metals that reach the storage-node junction.

This chapter covers the chamber wall and its conditioning, the edge ring and the edge region of the wafer, and the metal, particle, and micromasking defects that the chamber can introduce. It ends with the maintenance cycle that keeps all of them under control.

**Learning Objectives:**
- Explain how wall deposits change radical densities and oxygen supply, and why they cause drift
- Describe waferless autoclean and seasoning and justify a per-wafer clean
- Estimate edge tilt from sheath-edge mismatch and ring wear, and its consequence for DRAM AAs
- Describe edge-ring compensation by lift or tuning
- Identify metal contaminants, their sources, and their limits
- Describe particle and micromasking defects and their electrical signatures
- Plan a maintenance and recovery cycle

---

## 9.1 Walls and Their Deposits

### 9.1.1 What Coats the Walls

```
Source                           Deposit on walls, window, and liner
──────────────────────────────────────────────────────────────────────────
SiBrₓ / SiClₓ etch products      SiOₓBrᵧ / SiOₓClᵧ (with O₂ in the plasma)
(≈ 20 sccm equivalent, Ch. 5)
Breakthrough (CF₄)               Fluorocarbon film; fluorinated surfaces
NF₃ in ME-2                      Fluorine on wall surfaces; thins deposits
Sputtered mask and window        SiO₂, Al, Y (traces)
```

### 9.1.2 How the Wall State Changes the Plasma

```
Wall property                     Effect on the plasma                Effect on the trench
──────────────────────────────────────────────────────────────────────────────────────────────
Br/Cl recombination coefficient   Halogen atom density (lower         Rate; ARDE
(SiO₂-like wall: low;             recombination → more atoms)
metal-fluoride wall: higher)
Oxygen release (SiOₓ film         Extra O in the gas → more           Angle; AA width
sputtered by ions at the wall)    passivation                         at depth
Fluorine release (after NF₃       Extra F early in the next etch      Less passivation;
clean)                                                                narrower AA; deeper
Ion loss to walls                 Ion flux at the wafer → ion energy  Depth; facet
                                  at fixed bias power (Chapter 5)
```

### 9.1.3 Drift Without a Per-Wafer Clean

```
Illustrative lot of 25 wafers with no clean between wafers:

  Wafer       Cell depth     W(140)       Angle
  ───────────────────────────────────────────────
  1           254 nm         18.4 nm      0.90°
  5           252 nm         18.7 nm      0.96°
  10          250 nm         18.9 nm      1.00°
  25          247 nm         19.6 nm      1.13°

Trend: wall deposits thicken → more O released, lower F → passivation
grows → angle up, AA wider at depth, depth down

Range over the lot: depth 7 nm; W(140) 1.2 nm (80% of the ±1.5 nm
tolerance)
```

The first wafer after a clean is etched in a chamber with fresh, fluorinated walls, and every later wafer sees a thicker deposit. The drift consumes most of the AA width tolerance by itself.

---

## 9.2 Waferless Autoclean and Seasoning

### 9.2.1 Clean-and-Season Every Wafer

The standard remedy is to return the walls to the same state before every wafer:

```
After each wafer (no wafer on the chuck, or a cover wafer):

  WAC  (≈ 20 s)  NF₃/O₂ plasma: removes SiOₓBrᵧ (as SiF₄) and
                 organics; leaves fluorinated walls
  SEASON (≈ 20 s) SiCl₄/O₂ plasma: deposits a thin, reproducible
                 SiO₂-like film over all surfaces; seals in fluorine
  ─────────────────────────────────────────────────────────────────
  Total ≈ 40 s (Chapter 5 cycle)
```

The season coat makes the wall look the same to every wafer: SiO₂-like, with low halogen recombination, and covering the fluorinated surface from the clean. Each wafer then deposits its own products on top, and the next clean removes them. The drift of Section 9.1.3 collapses to within the measurement noise.

### 9.2.2 Season Thickness

```
Too thin: fluorine from the clean leaks through early in the next
          etch → first seconds of ME-1 are fluorine-rich → narrow top
          AA, slight undercut below the mask
Too thick: season film accumulates if not fully removed by the next
          WAC → slow drift returns; flakes → particles
Typical:  a few tens of nanometres per cycle, fully removed each WAC
          (verified by OES endpoint of the WAC: SiF emission decay)
```

### 9.2.3 Window and Coil

Deposits on the window change its RF transparency and, through capacitive coupling, its sputtering. Window temperature control and the Faraday shield (Chapter 5) keep window deposition stable. Some cleans briefly increase capacitive coupling to sputter the window clean.

---

## 9.3 Edge Control

### 9.3.1 The Sheath at the Wafer Edge

At the wafer edge, the sheath must pass from the wafer surface to the edge ring. If the two surfaces sit at different heights, or at different RF potentials, the sheath edge bends, and ions arriving there strike the wafer at an angle:

```
Sheath-edge height mismatch Δ (sheath over ring higher or lower than
sheath over wafer), sheath thickness s ≈ 0.49 mm:

  Tilt at the wafer edge:  θ_e ≈ Δ / (2 s)        (radians)
  Decay inward:            θ(x) ≈ θ_e exp(−x / λ_e),  λ_e ≈ 3 mm
                           (x = distance in from the wafer edge)

Example: Δ = 17 µm
  θ_e = 0.017 / 0.98 = 0.017 rad ≈ 1.0°
  At x = 3 mm (r = 147 mm): θ ≈ 1.0° × e⁻¹ ≈ 0.37°
  At x = 6 mm (r = 144 mm): θ ≈ 0.14°
```

### 9.3.2 What Tilt Does to DRAM AAs

A tilted trench in a periodic array tilts every fin by the same angle. Unlike a slit or a contact hole, the fins still stand between their neighbors, and the top of the island is not displaced. The effects are subtler:

```
Tilt θ at r = 147 mm, depth 250 nm:
  Bottom offset of each fin relative to its top: 250 × tan θ
    θ = 0.37° → 1.6 nm

Consequences:
  - One sidewall more vertical, the other more tapered (relative to
    the wafer normal) → asymmetric saddle fin under the word line
  - Depth slightly asymmetric across each fin
  - Fin stiffness unchanged, but any residual asymmetric stress
    (fill, clean) now acts on a leaning starting shape (Chapter 11)
```

DRAM tolerates a little more edge tilt than 3D NAND slits, because no deep feature has to clear a neighbor by a fixed margin. The specification at r = 147 mm is typically about ±0.3°, set by saddle-fin symmetry and by collapse margin at the edge.

### 9.3.3 Edge Depth and Edge CD

More important than tilt in most DRAM isolation processes are the depth and AA-width roll-off in the outer few millimetres:

```
Typical uncompensated edge signature (r = 140 → 148 mm):
  Depth:    −2% to −5% (lower ion flux, product-rich gas over the ring)
  W(140):   +0.5 to +1.0 nm (more passivation)

Knobs: extreme-edge ESC zone (+2–4 °C), edge gas, ring height or
ring RF potential
```

### 9.3.4 Ring Wear and Compensation

```
Edge ring (Si or SiC): top surface erodes under ion bombardment
  Illustrative wear: 0.05 µm per RF hour
  Effect: sheath over the ring drops relative to the wafer
  Tilt sensitivity: dθ_e/dΔ = 1/(2s) ≈ 1.0 rad/mm ≈ 0.058° per µm

Tilt at r = 147 mm (factor 0.37 of θ_e) must stay within ±0.3°
  → θ_e within ±0.8° → Δ within ±14 µm
  → wear window 28 µm → 28 / 0.05 = 560 RF hours (with the ring
    installed at +14 µm)

Compensation:
  Ring lift: motorized pins raise the ring as it wears; each 1 µm of
    lift cancels 1 µm of wear. Life then set by total erosion budget
  Ring RF tuning: a variable impedance between the ring and the chuck
    sets the ring's RF potential and hence the sheath over it; tilt is
    adjusted electrically, step by step if needed
```

With lift or tuning, ring life extends to the erosion limit of the part, often more than 1500 RF hours. The compensation curve (lift or tuning versus RF hours) is calibrated by measuring edge tilt and edge depth on monitor wafers (Appendix C).

---

## 9.4 Metal Contamination

### 9.4.1 Why Metals Matter Here

Metals that reach the trench sidewall can diffuse into the silicon during the liner oxidation and later anneals. Several transition metals (Fe, Ni, Cu, Cr) form deep levels in the silicon band gap that act as generation centres in the depletion region of the storage-node junction. A single deep-level centre in the right place can raise a cell's leakage from below 1 fA to tens of femtoamperes and make it a tail cell (Chapter 13).

### 9.4.2 Sources and Limits

```
Metal       Source in the etch chamber                  Typical limit on wafer
                                                        (atoms/cm², VPD-ICPMS)
──────────────────────────────────────────────────────────────────────────────────
Y           Y₂O₃ / YOF coatings (erosion, particles)    < 1×10¹⁰
Al          Al₂O₃ parts, anodized surfaces              < 1×10¹⁰
Fe, Cr, Ni  Stainless gas lines and fittings corroded   < 5×10⁹
            by wet HBr; valve seats; chamber hardware
Cu          Rare in front-end chambers; cross-          < 1×10⁹
            contamination from handling
Na, K       Handling, O-rings, cleaning residues        < 1×10¹⁰
```

HBr is strongly corrosive to stainless steel in the presence of moisture. Gas-line moisture control (purged installation, low-moisture HBr, heated or purged lines) is the first defence against iron and nickel contamination. Chamber parts with high-purity coatings are the defence against yttrium and aluminium.

### 9.4.3 Monitoring

Metal contamination is monitored on bare silicon monitor wafers run through the recipe (or a standard test recipe) after PM and periodically during production, by vapour-phase decomposition with ICP-MS (VPD-ICPMS) or total-reflection X-ray fluorescence (TXRF). Electrical monitors (surface photovoltage for iron, minority-carrier lifetime) give faster, cheaper trend data (Chapter 15).

---

## 9.5 Particles and Micromasking

### 9.5.1 Particles During the Etch

A particle that lands on the hard mask before or during the etch blocks the etch beneath it:

```
Particle on a cell array region (size d):
  d < 18 nm       Shadows part of one space; local shallow spot
  d ≈ 20–100 nm   Bridges one or more spaces → two or more AAs joined
                  by unetched silicon ("AA bridge")
  d > 100 nm      Blocks a patch of array → cluster of bridged islands

Electrical effect of an AA bridge:
  The two (or more) islands share silicon → their storage nodes are
  connected through the bridge → bit failures in a small cluster
  Repairable by row/column redundancy if isolated and few
```

### 9.5.2 Micromasking and Silicon Grass

In the periphery, wide open silicon areas are prone to **micromasking**: small islands of oxide (residual pad oxide, redeposited SiOₓBrᵧ, sputtered mask material, or particles of season film) that block the etch locally and leave thin silicon spikes or "grass" standing in the trench.

```
Causes                                      Remedies
─────────────────────────────────────────────────────────────────────
Residual pad oxide after the mask open      Robust mask-open overetch;
                                            breakthrough
O₂ too high in the main etch (oxide         Stay inside the O₂ window
nuclei grow on the bottom)                  (Chapter 4)
Season film flakes                          Correct season thickness;
                                            full WAC removal
Sputtered Y/Al from parts                   Part condition; coatings
```

Silicon spikes in a periphery trench obstruct the fill (voids) and, if they reach the surface after CMP, become leakage paths between periphery transistors.

### 9.5.3 Defect Budget

```
Isolation-etch defect budget (illustrative):
  Killer defects (bridges, blocked patches, grass in critical areas):
    < 0.02 per cm² → on a 54 mm² die: 0.02 × 0.54 ≈ 0.011 per die
  Most of these are repairable by redundancy if they fall in the
  array; periphery defects are usually not repairable
```

---

## 9.6 Maintenance and Recovery

```
Event                           Interval (illustrative)   Recovery
───────────────────────────────────────────────────────────────────────────────
Per-wafer WAC + season          Every wafer               Built into cycle
Edge-ring lift / tuning update  Continuous (by RF hours)  Monitor every 50–100 h
Edge-ring replacement           Erosion limit             Seasoning; edge tilt
                                (≈ 1500 RF h with lift)   and edge depth check
Full wet clean (liner, window,  ≈ 1500–3000 RF h          Season with dummy
nozzle, ring set)                                         wafers (≈ 25–50);
                                                          particles, metals,
                                                          depth/CD/angle quals
ESC replacement                 Wear, He leak, or arcing  Thermal calibration;
                                                          zone transfer matrix
```

After a wet clean, the chamber walls are bare ceramic. Seasoning with dummy wafers rebuilds a stable wall state before production wafers return. The qualification after recovery measures the same outputs used for chamber matching (Chapter 5): cell and periphery depth, AA width at the surface and at 140 nm, angle, remaining cap, edge tilt, particles, and metals.

---

## 9.7 Summary & Key Takeaways

1. **The walls are part of the recipe.** Wall deposits change halogen recombination and release oxygen or fluorine, moving depth, angle, and AA width.

2. **Clean and season every wafer.** Without it, a lot drifts by about 7 nm in depth and 1.2 nm in W(140). A 40 s WAC plus season removes the drift.

3. **Edge tilt is set by the sheath.** θ_e ≈ Δ/(2s): 17 µm of mismatch tilts the extreme edge by about 1°. Ring wear moves Δ; lift or RF tuning compensates.

4. **In DRAM, edge depth and width matter as much as tilt.** The outer few millimetres etch shallower with wider AAs unless tuned with the edge zone, gas, and ring.

5. **Metals become tail cells.** Fe, Ni, Cr, Y, and Al from corroded lines and eroded coatings can reach the junction surface. Gas-line moisture control and part condition are the defences.

6. **Particles bridge islands; oxide nuclei grow grass.** Bridges cost bits, often repairable. Grass in the periphery blocks fill and is usually not repairable.

---

## Study Questions

1. A chamber without per-wafer cleaning shows the drift of Section 9.1.3. If a lot is split into the first 12 and last 13 wafers, by how much does the mean W(140) differ between the halves? Would a per-lot time offset fix the problem? Why or why not?

2. Compute the edge tilt at r = 147 mm and r = 145 mm for a sheath mismatch of 25 µm, with s = 0.49 mm and λ_e = 3 mm. What fin bottom offset results at 250 nm depth at each radius?

3. An edge ring wears at 0.08 µm per RF hour. Without lift, how many RF hours keep the tilt at r = 147 mm within ±0.3°? With lift that compensates 90% of the wear, how long?

4. A tail-bit analysis shows a retention-tail degradation on wafers from one chamber only, beginning after a gas-line maintenance. List the contaminants you would suspect, how they could have been introduced, and the monitor measurements you would run.

5. Periphery trenches in a new product show silicon grass, but only in the center of the wafer. List three possible causes and the check that separates them.

---

**Next Chapter:** [Chapter 10: Profile Control — Taper, Bottom Shape, Corner Rounding & AA Width](./10-profile-aa-width.md)

---

**Chapter 9 Development Status:** Complete  
**Version:** 1.0
