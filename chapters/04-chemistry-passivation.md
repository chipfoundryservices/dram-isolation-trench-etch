# Chapter 4: Silicon Etch Chemistries & Sidewall Passivation

## Overview

The physics of Chapter 3 decides how many ions and radicals reach the trench bottom. The chemistry decides what they do there and on the way down. In the isolation etch, the same gas mixture must etch silicon quickly at the bottom, leave the sidewalls almost untouched, erode the 20 nm oxide cap as little as possible, and leave behind a surface that a short clean can return to bare, undamaged silicon.

This chapter describes the HBr/Cl₂/O₂ chemistry that does this, the silicon-oxybromide passivation film that makes it anisotropic, the selectivity to the oxide and nitride mask, the breakthrough step that opens the native oxide, and the residues the etch leaves. It ends with the reference recipe that later chapters refine.

**Learning Objectives:**
- Explain the role of HBr, Cl₂, O₂, He, and fluorine additives in silicon trench etch
- Describe how the SiOₓBrᵧ passivation film forms, where it grows, and how it sets the sidewall angle
- Compute the sidewall deposition rate that gives a target taper
- Estimate the width the passivation film occupies in an 18 nm trench
- Compute mask consumption and remaining cap for the reference process
- Choose a breakthrough chemistry and explain its trade-offs
- Describe post-etch residues and the constraints on their removal

---

## 4.1 The Gas Palette

### 4.1.1 What Each Gas Does

```
Gas      Role                                  Effect of more             Risk of too much
──────────────────────────────────────────────────────────────────────────────────────────────
HBr      Main etchant (Br); hydrogen           Higher selectivity to      Slower rate; more
         scavenges O and F; Br products are   oxide; more passivation    H in Si; residue
         less volatile than Cl products
Cl₂      Faster etchant; more volatile         Higher rate; less          Lateral etch; bowing;
         products                              micromasking               lower oxide
                                                                          selectivity
O₂       Converts SiBrₓ products into          Thicker sidewall film;     Taper; "grass" from
         non-volatile SiOₓBrᵧ                  more taper; higher         oxide micromasks;
                                               selectivity                trench closure
He, Ar   Diluent; stabilizes plasma; shortens  Lower radical density;     Lower rate; Ar
         residence time; He aids heat          higher ion fraction        sputters the mask
         transfer
NF₃,     Fluorine to thin passivation and      Less taper; cleaner        Lateral etch;
SF₆,     clear bottom deposits                 bottom; faster rate        undercut; selectivity
CF₄                                                                       loss to oxide mask
```

### 4.1.2 Why Bromine Dominates

HBr-based chemistry has been the standard for silicon trench and gate etch for decades for three reasons:

```
1. Selectivity to oxide. Br atoms do not etch SiO₂ appreciably, and
   the Si–O bond (≈ 8 eV) is far stronger than Si–Br. Si:SiO₂
   selectivity in HBr/O₂ exceeds 100 at low bias and 30–50 at the
   bias needed for a vertical trench.

2. Low spontaneous etch. Br atoms etch undoped Si very slowly without
   ions, so the sidewalls do not etch laterally even where the
   passivation is thin.

3. Self-passivation. SiBrₓ products are heavy and less volatile than
   SiClₓ. They redeposit on sidewalls and, with a little oxygen, form
   a robust protective film.
```

Chlorine is added for rate, for smoother bottoms, and because its more volatile products reduce micromasking. A typical silicon trench recipe uses HBr as the majority etchant, with Cl₂ at 10–30% of the halogen flow in the upper part of the trench and less or none deeper.

---

## 4.2 The Passivation Film

### 4.2.1 Formation

```
At the trench bottom (ion-assisted):
  Si + x Br → SiBrₓ (x = 1–4), desorbing under ion impact

In the trench and on the sidewalls:
  SiBrₓ (product, sticking probability s_p ≈ 0.05–0.2) lands on a wall
  O (from O₂ dissociation) oxidizes it:
    SiBrₓ(ads) + O → SiOₓBrᵧ (non-volatile) + Br

On the sidewall (few ions):
  SiOₓBrᵧ accumulates → 1–3 nm film
On the bottom (many ions):
  SiOₓBrᵧ is sputtered and etched as fast as it forms → bottom stays clean
```

The film is a silicon oxide with incorporated bromine, closer to SiO₂ the more oxygen is present. It is not etched by Br atoms, so once formed it protects the silicon beneath it.

### 4.2.2 Where the Passivation Comes From

The silicon in the passivation film comes mostly from the etch products. In a trench, the main source of etch products is the trench's own bottom. Products leaving the bottom must travel up the trench, and in a narrow trench they hit the sidewalls many times on the way out. **Narrow trenches passivate themselves more heavily than wide ones**, especially near the bottom, where the product flux is highest.

```
Consequences:
  - Passivation is local: each trench is largely fed by its own products
  - The film thickens with depth as the aspect ratio rises
  - Wide (periphery) trenches see fewer wall hits per product and
    passivate less → less taper than the cell
  - Global loading changes product density in the gas phase, which
    feeds passivation everywhere (Chapter 3, macroloading)
```

### 4.2.3 Passivation and Sidewall Angle

The sidewall angle is set at the bottom corner. As the bottom advances, the wall just above it receives passivation. Any film deposited on the wall acts as a mask for the next increment of etch, so the trench narrows by twice the lateral growth for every increment of depth:

```
tan α ≈ r_p / ER_b

r_p   = lateral growth rate of passivation at the bottom corner (nm/s)
ER_b  = vertical etch rate at the bottom (nm/s)

Reference: α = 1.0° → tan α = 0.0175
  ER_b at mid-depth (k = 0.025, z ≈ 150 nm): 0.78 × 5.0 = 3.9 nm/s
  Required r_p ≈ 0.0175 × 3.9 = 0.068 nm/s

  Over the whole 62 s etch, the cumulative lateral growth at the
  bottom corner is ≈ 0.068 × 62 ≈ 4.2 nm per side, close to the
  250 nm × tan 1.0° = 4.4 nm the trench loses per wall
```

The relationship explains the main recipe levers for angle:

```
To make the trench more vertical (smaller α):
  - Less O₂ (less film)                       → risk: undercut, bow
  - More F (NF₃) to thin the film             → risk: lateral etch
  - Higher bias (faster ER_b, film sputtered  → risk: mask facet,
    at the corner)                              damage, selectivity
  - Warmer wafer (lower sticking of products) → risk: bow (Chapter 8)

To add taper (larger α):
  - The opposite of each
```

At the reference angle, about 4 nm of the original trench width per side is replaced by a sloped wall. In an 18 nm trench, that is half the width at the bottom. **No other common etch spends so much of its trench width on passivation.**

### 4.2.4 The Film as Occupied Width

During the etch, the film also physically occupies trench width:

```
Film thickness on the upper sidewall (illustrative): 1.5 nm per side
  Trench width occupied: 3 nm of 18 nm → 17%
  Effective opening during the etch: 15 nm instead of 18 nm
  Effective aspect ratio at 250 nm: (250 + 49) / 15 = 19.9 vs. 16.6
```

Because the film narrows the opening, the transport of Chapter 3 sees a narrower trench than the one measured after the clean. The k values in this book are fitted to post-clean dimensions and include this effect implicitly. When a recipe change thickens the film, ARDE gets worse even if nothing else changes.

### 4.2.5 Oxygen Window

```
O₂ fraction of total halogen-bearing flow (illustrative, ME-2):

  O₂ / HBr        Film          Profile                Defects
  ────────────────────────────────────────────────────────────────────
  < 1%            Too thin      Bow, undercut below    —
                                the mask
  2–4%            Correct       Near-vertical,         —
                                α ≈ 0.8–1.2°
  5–7%            Thick         Taper α > 1.5°;        —
                                bottom closing
  > 8%            Very thick    V-bottom, etch stop    Grass (micromasks)
                                in narrow spaces       in the periphery
```

The oxygen window is narrow and depends on the open area, the wall state, and the wafer temperature. A drift of 1 sccm of O₂ in a 200 sccm HBr flow can move the cell angle by 0.2–0.3° (Appendix D).

---

## 4.3 Selectivity to the Mask

### 4.3.1 Oxide Cap Consumption

```
Si:SiO₂ selectivity in the main etch (open area): S_ox ≈ 40 (illustrative)
Oxide etch rate on the mask top: ER₀ / S_ox = 300 / 40 = 7.5 nm/min

Main etch 62 s:            7.5 × 1.035 = 7.8 nm
Breakthrough 8 s (CF₄):    ≈ 1.5 nm (non-selective)
Total planar cap loss:     ≈ 9.3 nm

Remaining cap: 20 − 9.3 = 10.7 nm   (spec ≥ 8 nm) ✓
```

The mask top is effectively an open area, so it erodes at the open-area rate even though the cell trenches etch more slowly. This is why ARDE costs mask: every second spent waiting for the narrow trenches erodes the cap at full speed.

### 4.3.2 Facets on 14 nm Lines

Ion sputtering erodes the mask top corners faster than the flat top, forming facets at 45–55° from horizontal. On a 14 nm line, the facets from both sides can meet:

```
Facet geometry on a mask line of width W_m:
  Each facet grows inward by f (horizontal) as the corner erodes
  The flat top disappears when 2f ≥ W_m

  W_m = 14 nm → flat top lost at f = 7 nm per side

Once the flat top is gone:
  - The mask line is a ridge; its height falls faster
  - Ions reflect from the facets into the trench near the top of the Si
    → local bow just below the mask (Chapter 10)
  - The effective mask CD at the Si surface starts to shrink
```

The facet rate depends strongly on ion energy and on the angle-dependent sputter yield of the oxide, which peaks at 50–70° incidence. Low-energy, pulsed bias keeps facet growth small (Chapter 6).

### 4.3.3 The SiN Backup

If the oxide cap is consumed locally (thin cap from deposition non-uniformity, or excessive facet), the SiN becomes the mask:

```
Si:SiN selectivity in HBr/O₂: ≈ 10–20 (illustrative)
  → SiN erodes 2–4× faster than SiO₂
  → each nm of SiN lost before CMP reduces the CMP stop thickness
    and changes the final STI step height
```

A cap that is consumed anywhere before the end of the etch is an excursion: it will show up after CMP as a local step-height error and, at the extreme, as dishing into the active area.

---

## 4.4 Breakthrough

### 4.4.1 Why a Separate Step

Native oxide (0.5–1.0 nm) on the exposed silicon etches very slowly in HBr/O₂. If it is not removed uniformly, the silicon etch starts at different times in different places, and small islands of residual oxide act as micromasks.

### 4.4.2 Options

```
Option                         Chemistry          Pros                      Cons
──────────────────────────────────────────────────────────────────────────────────────────
Fluorocarbon BT                CF₄/He or          Fast, uniform; reliable   Removes ≈ 1–2 nm of
                               CF₄/CHF₃,          native-oxide removal      cap; leaves C/F on
                               5–10 s                                       Si; some Si recess
NF₃ or SF₆ BT                  NF₃/He, short      No carbon                 Isotropic Si attack
                                                                            under the mask edge;
                                                                            selectivity to
                                                                            oxide lower
High-bias Cl₂ or HBr BT        Cl₂ or HBr/Ar,     No F, no C; same          Sputter of mask
                               high bias,         chemistry family          corners; Si damage;
                               5–10 s                                       needs more bias
```

The reference process uses a CF₄/He breakthrough of 8 s. Its cost is about 1.5 nm of cap and a few nanometres of silicon recess, which is included in the depth target.

### 4.4.3 The Breakthrough-to-Main-Etch Transition

Fluorine and carbon left in the chamber and on the wafer after a fluorocarbon breakthrough change the first seconds of the main etch. Fluorine speeds up silicon etching and attacks the passivation; carbon adds polymer. Recipes include a short pump-out or a gas-stabilization step between breakthrough and main etch, and the main-etch time is calibrated with the breakthrough in place (Chapter 7).

---

## 4.5 Doping and Material Effects

In most DRAM flows, the isolation etch comes before the well implants, so the silicon is uniformly lightly doped p-type, and doping has little effect on rate. Where implants or epitaxial layers precede the etch, two effects matter:

```
Effect                                  Magnitude              Consequence
─────────────────────────────────────────────────────────────────────────────
Heavily doped n⁺ Si etches faster in    Up to several ×        Lateral notching at
Cl-based plasmas (spontaneous etch)     spontaneous rate       n⁺ layers
p⁺ (boron) Si etches more slowly        10–30% slower at       Depth loss; profile
                                        high concentration     kink
SiGe layers (3D DRAM stacks, Ch. 14)    Faster in Cl/Br        Lateral recess of
                                                               SiGe
```

---

## 4.6 Residues and Post-Etch Cleaning

### 4.6.1 What Remains After the Etch

```
Residue                          Where                     Removal
───────────────────────────────────────────────────────────────────────────────
SiOₓBrᵧ sidewall film            All trench walls,         Dilute HF
(1–3 nm)                         thickest near the bottom
Bromine adsorbed / implanted     Surface and first          Liner oxidation
                                 1–2 nm of Si              consumes it
Hydrogen in Si                   Up to ≈ 10 nm deep        Anneal / liner oxidation
                                                           (partly)
Carbon and fluorine (from BT)    Top surface, early wall   Clean; liner oxidation
Mask fragments, polymer flakes   Random                    Clean; inspection
```

### 4.6.2 Constraints on the Clean

The obvious remedy, a longer dilute-HF clean, runs into three limits:

```
1. Pad-oxide undercut. HF attacks the 4 nm pad oxide laterally under
   the SiN. An undercut of more than a few nm leaves a SiN overhang
   and a void path at the top corner of the AA.

2. Cap loss. HF also removes the oxide cap (already down to ≈ 11 nm).

3. Pattern collapse. Every wet step ends with drying; longer and more
   aggressive cleans give more chances for capillary collapse
   (Chapter 11).
```

A typical sequence is a short dilute HF (removing the passivation film and about 1 nm of oxide), followed by a mild SC1 or ozonated-water step to remove particles and organics and form a thin chemical oxide, then a low-surface-tension (IPA) dry. Chapter 13 discusses how the liner oxidation completes the work.

---

## 4.7 The Reference Recipe

```
Step   Time    p        Source /       Gases (sccm)                Purpose
               (mTorr)  bias (W)
──────────────────────────────────────────────────────────────────────────────────────────
BT     8 s     5        500 / 150 CW   CF₄ 80, He 50               Native oxide removal
STAB   5 s     8        0 / 0          HBr 200, Cl₂ 40, O₂ 6,      Gas exchange; no plasma
                                       He 100
ME-1   30 s    8        900 / 450      HBr 200, Cl₂ 40, O₂ 6,      Upper trench: rate,
               (sync. pulsed,          He 100                      verticality below mask
               1 kHz, 50%; peak W)
ME-2   32 s    12       800 / 380      HBr 220, O₂ 8, NF₃ 3,       Lower trench: low ARDE,
               (sync. pulsed,          He 120                      angle control at depth
               1 kHz, 40%; peak W)
PS     6 s     20       600 / 60       HBr 150, He 150             Bottom rounding;
                                                                   optional, low damage
──────────────────────────────────────────────────────────────────────────────────────────
Main etch (ME-1 + ME-2): 62 s → cell 250 nm, periphery 287–310 nm
Wafer (ESC) setpoint: 50 °C center / 52 °C edge (illustrative)
All values illustrative; see Chapters 6–8 for the pulsing, gas, and
temperature design behind them.
```

The two main-etch steps divide the trench at about 120 nm. ME-1 uses chlorine for rate and smoothness while the trench is shallow and the passivation demand is low. ME-2 removes chlorine, adds a little more oxygen to hold the angle as the trench deepens, and adds a small amount of NF₃ to keep the bottom clean and the passivation from closing the narrow spaces. Its higher pressure and lower bias reduce the bottom reaction probability and with it the ARDE coefficient.

---

## 4.8 Summary & Key Takeaways

1. **HBr is the base.** It gives high selectivity to oxide, almost no spontaneous lateral etch, and self-passivation. Cl₂ adds rate and smoothness; O₂ builds the film; fluorine thins it.

2. **The passivation comes from the trench itself.** SiBrₓ products from the bottom, oxidized on the walls, form a 1–3 nm SiOₓBrᵧ film. Narrow trenches passivate more, especially near the bottom.

3. **Angle is a ratio.** tan α ≈ r_p/ER_b. A 1.0° wall needs about 0.07 nm/s of lateral growth at the bottom corner while the bottom etches at about 4 nm/s.

4. **Passivation takes width.** At 1.0°, each wall moves 4.4 nm inward over 250 nm, half the trench width at the bottom. During the etch, the film itself narrows the opening further.

5. **The mask erodes at the open-area rate.** About 9 nm of the 20 nm cap is consumed, leaving 10.7 nm. Facets on 14 nm lines meet after about 7 nm of corner erosion.

6. **Breakthrough and clean are part of the chemistry.** The breakthrough must remove native oxide uniformly without leaving residue that disturbs the main etch. The post-etch clean is limited by pad-oxide undercut, cap loss, and collapse.

---

## Study Questions

1. A recipe gives a bottom etch rate of 3.5 nm/s at mid-depth and a sidewall angle of 1.3°. Compute the lateral passivation growth rate at the bottom corner. By how much must it fall to reach 0.9°?

2. The sidewall film during etch is 2.0 nm thick per side in an 18 nm space. Compute the effective aspect ratio at 250 nm depth with the 49 nm mask. Using k = 0.025 applied to the effective width, by how much does the bottom rate ratio change compared with the post-clean width?

3. Si:SiO₂ selectivity falls from 40 to 28 after a bias increase that shortens the main etch from 62 s to 55 s. Compute the planar cap loss in each case (include 1.5 nm from the breakthrough). Which condition leaves more cap?

4. Explain why an O₂ flow error affects the 18 nm cell spaces more than the 1 µm periphery trenches. What does this do to the cell AA width at 140 nm depth?

5. A fab replaces a CF₄ breakthrough with a high-bias HBr breakthrough to eliminate carbon. List two benefits and two risks, and the measurements you would use to qualify the change.

---

**Next Chapter:** [Chapter 5: Inductively Coupled Reactor Architecture for DRAM Isolation Etch](./05-icp-reactor-architecture.md)

---

**Chapter 4 Development Status:** Complete  
**Version:** 1.0
