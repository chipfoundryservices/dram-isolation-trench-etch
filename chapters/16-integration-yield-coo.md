# Chapter 16: Post-Etch Integration, Yield & Cost of Ownership

## Overview

The isolation etch is finished when the plasma turns off, but its results are judged much later: after the trenches are lined, filled, and polished, after the buried word line is recessed through them, after the contacts land on the islands, and finally at probe, when billions of cells are tested for retention and disturb. Each of those steps is a customer with specific needs, and each turns certain etch errors into specific failure signatures.

This chapter follows the wafer through the steps that use the isolation trench, lists what each needs from the etch, maps etch errors to the yield signatures they produce, and closes with the cost of ownership of the etch compared with the value of the yield it protects.

**Learning Objectives:**
- Describe the clean, liner, fill, CMP, word-line recess, and contact steps that follow the isolation etch and what each requires from it
- Compute the remaining gap after the liner and the fill margin in the cell trench
- Explain how bow, seams, and depth walk affect fill and the word-line recess
- Map etch errors to bit-fail signatures at probe
- Estimate yield loss from killer defects and from retention-tail shifts
- Build a cost-of-ownership model for the etch and compare it with the value of yield

---

## 16.1 Clean, Dry, and Queue Time

The post-etch clean removes the SiOₓBrᵧ film and residues and dries the fins without collapse (Chapters 4, 11, and 13). Between the dry and the liner oxidation, the wafer waits:

```
Queue-time effects after the dry (illustrative):
  Native oxide regrowth on bare Si sidewalls: ≈ 0.5 nm in a few hours
  Moisture and organic adsorption: changes the early liner growth
  Residual bromine reacting with moisture: HBr formation, slight Si
    pitting if the clean left Br behind

Typical limit: dry-to-liner queue time ≤ 4–6 h
```

---

## 16.2 Liner Oxidation and Nitride Liner

### 16.2.1 What the Liner Does

```
Function                                  Requirement on the etch
──────────────────────────────────────────────────────────────────────
Consumes the damaged, Br-rich surface     Damage depth ≤ the Si consumed
(Chapter 13)                              (≈ 1.1 nm per side)
Rounds top and bottom corners             No sharp microtrench corners
Forms the Si/SiO₂ interface of the        Smooth sidewall; no residue
storage-node junction sidewall            (interface traps)
Narrows the trench                        Enough bottom width for the fill
```

### 16.2.2 The Gap Left for Fill

```
Liner t_ox = 2.5 nm: consumes 1.1 nm Si per wall, grows 1.4 nm outward
  Trench narrows by 2 × 1.4 = 2.8 nm

  Location        Etched width    After liner    Free gap for fill
  ───────────────────────────────────────────────────────────────────
  Top (S_t)       18.0 nm         15.2 nm        15.2 nm
  140 nm depth    13.1 nm         10.3 nm        10.3 nm
  Bottom (250)    9.3 nm          6.5 nm         6.5 nm
  Bottom, α = 1.25°   7.1 nm      4.3 nm         4.3 nm
```

### 16.2.3 Nitride Liner

Some flows add a thin SiN liner (2–4 nm) to block oxidation of the silicon during later anneals, to tune stress, or to protect the fill from later wet etches. In the cell trench, a 2 nm nitride liner on each wall would reduce the 6.5 nm bottom gap to 2.5 nm and the 4.3 nm gap at 1.25° to almost nothing. **A nitride liner in the cell trench is only possible with a vertical profile or a shallower trench.** In most DRAM flows, the cell uses an oxide-only liner, and the nitride liner, if any, is used in the periphery.

---

## 16.3 Gap Fill

### 16.3.1 Fill Materials

```
Region                  Fill                         Concern
──────────────────────────────────────────────────────────────────────────────
Cell line spaces and    ALD SiO₂ (conformal), or     Seam at the center line; seam
cut gaps                ALD + flowable cap           opening in later wet steps
Periphery (wide)        Flowable / spin-on oxide     Shrinkage on cure (10–15%),
                        (FCVD / SOD) + steam anneal; stress, densification;
                        HDP-CVD in some flows        voids in microtrench grooves
```

### 16.3.2 What the Profile Does to Fill

```
Profile feature (Chapter 10)        Effect on conformal ALD fill
──────────────────────────────────────────────────────────────────────────────
Positive taper (V-shaped trench)    Fill closes from the bottom up; seam
                                    shallow and short → good
Vertical walls                      Seam along the full depth; acceptable if
                                    the seam stays closed
Bow just below the surface          Re-entrant: the top closes before the
(re-entrant)                        region below → keyhole void under the
                                    surface
Microtrench grooves (periphery)     Voids in the groove
Rough or striated walls             Seam irregular; local voids
```

A bow of 0.45 nm per side at 20–40 nm depth (Chapter 10) makes the trench slightly wider below the surface than at it. With conformal ALD, that can leave a small keyhole just under the island top, exactly where the storage-node junction and the contacts sit. Bow control is therefore a fill requirement as well as a junction-field requirement.

### 16.3.3 Seams Later in the Flow

The seam left by conformal fill is a line of weaker oxide. Later wet etches (pad SiN strip in hot phosphoric acid, pad oxide strip in HF, pre-clean before the word-line etch) can open it. An opened seam in a cell trench can fill with word-line metal or contact polysilicon and short two islands or a word line to a contact. Taper helps: a V-shaped fill seam is shorter and closes higher than a vertical one.

---

## 16.4 CMP and Hard-Mask Removal

```
Sequence:
  1. Oxide CMP stops on the SiN (25 nm, intact because the SiO₂ cap
     protected it: Chapter 4)
  2. SiN strip (hot H₃PO₄), pad oxide strip (dilute HF)
  3. Result: fill oxide stands slightly above or level with the Si
     surface (step height); a small divot can form at the island edge

Etch dependencies:
  - Cap consumed locally → SiN thinned → local CMP over-polish → step
    height error and dishing
  - Top-corner shape → divot depth at the island edge; deep divots
    can trap contact material and raise GIDL
  - Periphery depth → wide-trench dishing; the deeper and wider, the
    more the flowable oxide shrinks and dishes
```

---

## 16.5 The Buried Word-Line Recess

The word-line trench is etched across the array after CMP. It must recess silicon (in the islands) and oxide (in the isolation) to different depths in one step or a short sequence:

```
Word-line recess targets (reference):
  Silicon (AA):         140 nm
  Isolation oxide:      180 nm → saddle fin h_sf = 40 nm

What the isolation etch decides:
  - Fin width at 140–180 nm: W(140) = 18.9, W(180) = 20.3 nm
  - Oxide margin under the word line: cell trench depth − 180 nm
    (70 nm nominal; ≥ 40 nm required)
  - Uniformity of the oxide being recessed: the same ALD fill in
    every line space, but the cut gaps are wider and deeper (Chapter
    12) and recess faster through ARDE in the oxide etch
  - Seams: an oxide recess etch opens seams faster than solid oxide,
    so the saddle fin can be locally deeper along a seam
```

```
Depth walk and the oxide margin:
  Shallowest space type (taper-coupled, 2 nm space range): 247 nm
  Oxide under the WL there: 247 − 180 = 67 nm   (≥ 40 ✓)
  With a 4 nm space range: ≈ 244 nm → 64 nm      (✓)
  A shallow excursion to 220 nm leaves exactly 40 nm, with no margin
  for word-line recess variation
```

---

## 16.6 Contacts

```
Contact              Lands on                   Isolation-etch dependencies
──────────────────────────────────────────────────────────────────────────────────────
Bit-line contact     Island center              W_t (contact area and overlay
(DC)                                            margin); top-corner shape; divot
Storage-node         Island ends                Island-end pull-back (Ch. 12);
contact (BC)                                    end shape; W_t; bow just below
                                                the surface; top-corner damage
                                                (junction leakage)
```

The BC contact is the most demanding. Its landing area is the island end, which the cut shapes, the etch pulls back, and the liner consumes. A 1 nm narrower W_t and 3 nm of pull-back per end together reduce the silicon under the contact by roughly 15%, raising contact resistance and tightening its overlay margin.

---

## 16.7 Yield Signatures

```
Bit-fail signature at probe                 Likely isolation-etch cause              Chapter
──────────────────────────────────────────────────────────────────────────────────────────────────
Paired bits in adjacent AAs (same           AA bridge: fin collapse, particle,       9, 11
position, neighboring lines)                missing space (EUV stochastic)
Small clusters of failing bits              Particle during etch; collapse cluster   9, 11
Failures in the first rows/columns          Lean of edge lines; insufficient          11, 12
next to array edges                         dummies; edge-line profile
Retention tail worse in a ring at the       Edge AA width / depth; edge tilt;        8, 9
wafer edge                                  ring wear
Retention tail worse wafer-wide,            Damage, metals, residue; liner change;   9, 13
one chamber                                 gas-line contamination
Retention or disturb fails periodic         Shallow narrow (γ) space from pitch      2, 12
every fourth AA line (SAQP period)          walk; lean toward narrow space
Row-hammer sensitivity increased            Cut-gap profile / island-end shape;      1, 12
                                            shallow cut gap; passing-WL spacing
Column failures from sense-amplifier        Depth / width gradient across matched    12
offset                                      pairs near the array
Periphery leakage, shorts between           Periphery depth shallow (60 nm),         9, 10, 12
periphery transistors                       grass, microtrench voids
Word line to contact shorts                 Opened fill seams (re-entrant bow,       10, 16
                                            vertical seams)
```

The most valuable diagnostic is often the spatial and logical pattern of the fails. A periodic signature at the SAQP period points to the patterning-etch interaction. A ring at the wafer edge points to the edge hardware. A chamber-specific wafer-wide shift points to the chamber's condition.

---

## 16.8 Yield Models

### 16.8.1 Killer Defects

```
Isolation-etch killer defect density D₀ = 0.02 /cm² (Chapter 9)
Die area A = 0.54 cm²

  Die with at least one killer defect: 1 − exp(−D₀ A) = 1 − exp(−0.0108)
                                     ≈ 1.1%

If 80% of defects fall in the array and are repairable by redundancy:
  Effective die loss ≈ 0.2 × 1.1% ≈ 0.2%
```

### 16.8.2 Retention Tail and Repair

A die passes if the number of retention-failing bits at the test condition is within the repair capacity of its redundant rows and columns. The yield therefore depends on the whole distribution of tail bits per die, and it falls off steeply once the mean approaches the capacity:

```
Illustrative: repair capacity 600 bits per die at the screen condition

  Mean tail bits per die    Spread (die to die)      Die yield (retention,
                                                     normal approximation)
  ─────────────────────────────────────────────────────────────────────────
  300                       ±25% (1σ, spatial)       ≈ 100%
  450                       ±25%                     ≈ 91%
  600                       ±25%                     ≈ 50%
  900                       ±25%                     ≈ 9%
```

An etch change that raises the tail by 50% can take a product from fully yielding to losing a large fraction of die, with no visible change in the trench. This nonlinearity is why retention testing is the final qualification of any change to the isolation etch.

---

## 16.9 Cost of Ownership

### 16.9.1 Cost per Wafer

```
Inputs (illustrative):
  Chamber capital (with share of mainframe): $4.5M, 5-year depreciation
  Throughput: 21.7 WPH (Chapter 5), availability 85%
  Wafers per chamber per year: 21.7 × 0.85 × 8760 ≈ 161,600
  RF time per wafer (BT + ME + PS + WAC/season): 116 s ≈ 0.032 h

Item                                       Basis                          $/wafer
──────────────────────────────────────────────────────────────────────────────────────
Capital depreciation                       $0.9M/yr ÷ 161,600             5.57
Edge ring                                  $6k per 1500 RF h              0.13
                                           (≈ 46,500 wafers)
Wet-clean parts kit                        $25k per 2500 RF h             0.32
                                           (≈ 77,600 wafers)
ESC                                        $120k per 4 years              0.19
Gases (HBr ≈ 0.8 g, NF₃, SiCl₄, others)                                  0.25
Electricity (≈ 25 kW × 166 s)                                             0.12
Maintenance labor and other spares                                        1.00
Cleanroom space and facilities                                            0.80
Metrology allocation (OCD, SEM, TEM,                                      1.50
inspection)
──────────────────────────────────────────────────────────────────────────────────────
Total                                                                    ≈ 9.90
```

Capital dominates, followed by metrology and labor. Consumables and gases are small.

### 16.9.2 Alternatives

```
Scheme                            Change                                 $/wafer
────────────────────────────────────────────────────────────────────────────────────
Reference (pulsed single step)    —                                      ≈ 9.9
Quasi-ALE main etch               Cycle +30 s → 18.4 WPH                 ≈ 11.5
Dual-depth (cell pre-etch)        + non-critical litho (≈ $3), ash       ≈ 14.7
                                  (≈ $0.8), extra etch step (≈ $1)
Full silicon ALE                  Cycle ≈ 1100 s; 6.6× chambers          ≈ 45
Per-5-wafer clean instead of      WPH 26.9 (Chapter 5 Q4)                ≈ 8.3
per-wafer                         (with drift risk, Chapter 9)
```

### 16.9.3 Yield Dominates

```
Value of a DRAM wafer (illustrative):
  Gross die ≈ 1150 per wafer (54 mm²), ≈ $5–6 per die
  → ≈ $6,000 per wafer

  0.1% die yield ≈ $6 per wafer
  The entire etch step costs ≈ $10 per wafer ≈ 0.17% of die yield
```

A yield difference of 0.2% between two isolation-etch schemes outweighs the whole cost of the step. Saving $1.60 per wafer by cleaning every fifth wafer is worth it only if it does not cost more than about 0.03% of yield, which the drift data of Chapter 9 suggest it would. **Cost-of-ownership decisions on this step are yield decisions.**

---

## 16.10 Summary & Key Takeaways

1. **Every later step uses a different part of the trench.** The liner and fill use the bottom, the word line uses the middle, the contacts use the top, and retention uses the sidewall.

2. **The cell fill has little room.** After a 2.5 nm liner, the reference bottom gap is 6.5 nm, leaving no room for a nitride liner in the cell.

3. **Bow and seams cause later shorts.** A re-entrant bow below the surface can leave a keyhole; opened seams can fill with metal.

4. **The word line spends depth margin.** The oxide under the passing word line is cell depth minus 180 nm: 70 nm nominal, 40 nm minimum.

5. **Fail patterns point to causes.** Paired bits, edge rings, SAQP-period signatures, and chamber-specific shifts each identify a different isolation-etch mechanism.

6. **Yield dominates cost.** The step costs about $10 per wafer, roughly 0.17% of die yield. Retention tails make yield highly nonlinear in etch quality.

---

## Study Questions

1. Compute the free gap for fill at the top, at 140 nm, and at the bottom of the reference cell trench for a 3.0 nm liner. Could a 1.5 nm nitride liner be added?

2. A new recipe reduces the sidewall angle to 0.8° to recover fill margin. Compute the new etched bottom width, the gap after a 2.5 nm liner, and the change in W(140). What happens to the collapse margin (Chapter 11)?

3. A probe map shows retention fails concentrated every fourth AA line in one quadrant of the wafer. Using Section 16.7, list the most likely causes in order and the inline measurement that would confirm each.

4. Using the repair-capacity table, estimate the yield change if a damage reduction lowers the mean tail bits per die from 450 to 360. What is that worth per wafer at $6,000 per wafer?

5. A fab considers replacing the per-wafer clean with a per-five-wafer clean. Using the cost model and the drift of Chapter 9, compute the cost saving per wafer and the maximum yield loss that would make the change worthwhile.

6. Compare the cost per wafer of the dual-depth scheme and the reference process. Under what conditions (node, k achievable, lithography capacity) would the dual-depth scheme be the better choice?

---

**Book #26 Complete.** Continue to the appendices for reference data, procedures, and calculations: [Appendix A](../appendices/A-material-properties.md)

---

**Chapter 16 Development Status:** Complete  
**Version:** 1.0
