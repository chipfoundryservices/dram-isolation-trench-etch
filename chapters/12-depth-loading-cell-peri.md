# Chapter 12: Depth Loading — Cell Versus Periphery, Pitch Walk & Island Ends

## Overview

The isolation etch has no stop layer. Every trench on the wafer is etched for the same time, and each reaches whatever depth its width, its neighbors, and its position on the wafer allow. The cell line spaces, the cut gaps, the periphery trenches from 60 nm to tens of microns, the spaces at the array edge, and the three pitch-walked space types all end at different depths. Each has its own window.

This chapter assembles the depth picture. It finds the time window in which the cell and every periphery width are in specification at once, and shows how that window disappears as the ARDE coefficient rises. It quantifies the depth walk from pitch walk, the extra depth at cut gaps, the pull-back of island ends, and the effects at array edges and in the periphery. It closes with the depth budget and the strategies for reducing loading when the window is too narrow.

**Learning Objectives:**
- Compute the time window in which cell and periphery depths are both in specification
- Find the maximum ARDE coefficient for which a single-step etch has a window
- Compute depth walk from pitch walk with and without taper coupling
- Explain extra depth at cut gaps and pull-back of island ends
- Describe array-edge, iso-dense, and periphery loading effects
- Build a depth budget from radial, wafer-to-wafer, pattern, and local terms
- Choose an ARDE-reduction or dual-depth strategy for a given window

---

## 12.1 Windows and Spreads

```
Depth specifications (Chapter 1):

  Feature                        Window             Binding requirement
  ──────────────────────────────────────────────────────────────────────────
  Cell line space (18 nm)        220–280 nm         ≥ 220: oxide under WL
                                                    ≤ 280: collapse, fill
  Periphery, open (≥ 1 µm)       280–330 nm         ≥ 280: HV isolation
                                                    ≤ 330: fill, stress
  Periphery, narrowest (60 nm)   ≥ 270 nm           Isolation between dense
                                                    periphery transistors
```

The cell window is 60 nm wide. The periphery window is 50 nm wide. Because the periphery etches faster than the cell (ARDE), the two windows must be met at the same time from the same recipe.

---

## 12.2 Cell Versus Periphery

### 12.2.1 The Time Window

Using the time-to-depth model of Chapter 3 (ER₀ = 300 nm/min, h_m = 49 nm), each requirement becomes a time limit:

```
Reference recipe, k = 0.025:

  Requirement                      Time limit
  ──────────────────────────────────────────────
  Cell ≥ 220 nm                    t ≥ 53.7 s
  Periphery 60 nm ≥ 270 nm         t ≥ 58.1 s
  Periphery open ≥ 280 nm          t ≥ 56.0 s
  Periphery open ≤ 330 nm          t ≤ 66.0 s
  Cell ≤ 280 nm                    t ≤ 70.7 s
  ──────────────────────────────────────────────
  Window:                          58.1 – 66.0 s
  Reference time:                  62.1 s (center)
```

The window is ±4 s around the reference, or about ±6.4% of the etch time. **Both ends of the window are set by the periphery.** The cell's own window is wide; what makes the process hard is that the periphery must be inside its window at the same moment.

### 12.2.2 The Window Closes as k Rises

```
  k        Lower limit (s)          Upper limit (s)      Window
  ───────────────────────────────────────────────────────────────────
  0.025    58.1 (peri 60 nm)        66.0 (peri open)     7.9 s
  0.040    60.6 (peri 60 nm)        66.0                 5.4 s
  0.058    66.5 (cell ≥ 220)        66.0                 none

Maximum k for any window (cell = 220 nm when open = 330 nm):
  k_max ≈ 0.057
```

The uncompensated chemistry of Chapter 3 (k = 0.058) has no window at all: by the time the cell reaches 220 nm, the open periphery is already past 330 nm. **Lowering k is not a refinement; it is what makes a single-step isolation etch possible.** At k = 0.040, the window exists but is only ±2.7 s (±4.3%), which is tight against the run-to-run variation of a production chamber.

### 12.2.3 Rate Tolerance

At the reference time, how far can the rate move?

```
Reference recipe, t = 62.1 s, all rates scaled by a factor f:

  f        Cell     Peri 60 nm    Peri open    Status
  ───────────────────────────────────────────────────────
  0.92     232      266           286          60 nm periphery fails
  0.95     239      274           295          OK
  1.00     250      287           310          OK
  1.05     261      301           326          OK
  1.08     267      309           335          Open periphery fails
```

The process tolerates a rate error of about ±6%, but all sources of rate variation share it: radial non-uniformity, chamber-to-chamber matching, drift between cleans, product open-area differences, and incoming mask height. This sets the precision required of APC (Chapter 15).

---

## 12.3 Pitch Walk Becomes Depth Walk

### 12.3.1 Sensitivity

```
Depth at 62.1 s for different space widths:

                           S = 16    S = 18    S = 20    ∂D/∂S
  ────────────────────────────────────────────────────────────────
  k = 0.025, straight      244.8     250.0     254.4     2.4 nm/nm
  k = 0.058, straight      241.5     250.0     257.5     4.0 nm/nm
  k = 0.021, α = 1.0°      244.0     250.0     255.0     2.75 nm/nm
  (taper-coupled, Ch. 10)
```

Taper raises the sensitivity because a narrower space also narrows faster with depth. The taper-coupled value of 2.75 nm per nm is the one to use for budgets.

### 12.3.2 What Depth Walk Does

```
Space range 2 nm (17 / 18 / 19 nm):  depth range ≈ 5.5 nm
Space range 4 nm (16 / 18 / 20 nm):  depth range ≈ 11 nm

Consequences:
  - Oxide under the passing word line differs by the depth walk
    from one space type to the next (≥ 220 nm must hold for the
    shallowest)
  - Fill of three slightly different trench shapes; the narrowest
    and shallowest also has the narrowest bottom (Chapter 10)
  - Lean from capillary asymmetry (Chapter 11), which in practice
    limits pitch walk more strictly than depth walk does
```

### 12.3.3 Measuring It

Depth walk is a periodic signature with the 128 nm SAQP period (four spaces). Scatterometry with a model that allows three space types, or cross-section TEM through several periods, resolves it. A single-space OCD model averages it away and reports the mean depth correctly while hiding the walk (Chapter 15).

---

## 12.4 Cut Gaps and Island Ends

### 12.4.1 Cut Gaps Etch Deeper

```
Plan view near a cut gap:

    ═══════════════╗     ╔═══════════════   AA line n
                   ║ cut ║
  ─ line space ────╢ gap ╟──── line space ─
                   ║24 nm║
    ═══════╗       ╚═════╝       ╔═══════   AA line n+1 (staggered)
```

A cut gap is 24 nm long along the line, but it opens on both sides into the 18 nm line spaces. Its transport is closer to that of a wider opening. Treating it as an effective width of 24–30 nm:

```
Depth at 62.1 s (k = 0.025):
  S_eff = 24 nm → 262 nm
  S_eff = 30 nm → 269 nm
  vs. line space 250 nm → cut-gap bottoms 12–19 nm deeper
```

The extra depth under the cut gap is harmless for isolation (it adds margin between the storage-node junctions at the two island ends) and is generally accepted. It does affect the fill, which sees a locally deeper and wider pocket, and the word-line recess, which passes through the cut gap as the passing word line.

### 12.4.2 Island-End Pull-Back

The island end is a short wall facing a wider opening. It receives less redeposited passivation than the long sidewalls, which face narrow spaces full of their own products. It therefore etches back laterally:

```
End pull-back at the top (illustrative):
  From the mask: 2–4 nm per end
  Deeper, the end wall tapers less than the side walls → the island
  is shorter at depth than a simple taper would predict

Effect of 3 nm pull-back per end on an 84 nm island:
  Island length at the top: 84 − 6 = 78 nm (−7%)
  BC contact landing length: reduced by 3 nm on each end
  Passing word line to SN junction: the end moves away from the
    passing WL by 3 nm (helps row hammer slightly) but the BC
    contact overlay margin shrinks
```

End pull-back is compensated in the cut layout (a cut slightly shorter than the target gap), much as line-end shortening is compensated by optical proximity correction in lithography. The compensation is valid only for a fixed etch; any change in passivation (oxygen, temperature, wall state) changes the pull-back and must be re-checked at the island ends.

### 12.4.3 End Shape

The cut gives a rounded or slightly pointed end in plan view (Chapter 2). The etch smooths and further rounds it. The storage-node contact lands partly on the end, and the shape decides how much silicon lies under the contact. Island-end shape is measured by top-down CD-SEM with contour extraction and, for the profile of the end wall, by cross-section along the AA line.

---

## 12.5 Array Edges and the Periphery

### 12.5.1 Array Edge

```
Location                          Depth effect                 Other effects
────────────────────────────────────────────────────────────────────────────────
Space between last active line    Wider → deeper (ARDE)        One-sided passivation;
and first dummy (if wider)                                     lean (Ch. 11)
Dummy lines / outer spaces        Progressively deeper         Not electrically
                                  toward the open area         active
Transition to periphery           Large open area: full rate   Product depletion
                                                               lowers the rate of
                                                               nearby cell spaces
                                                               slightly
```

Because the first two to six lines are dummies, the depth and profile changes at the array edge fall mostly on structures that do not carry data.

### 12.5.2 Iso-Dense Effects in the Periphery

Periphery transistors include dense groups (sense-amplifier arrays, sub-word-line drivers) and isolated devices. Narrow trenches between dense active areas etch more slowly and passivate more than isolated wide trenches:

```
Periphery trench widths and depth at 62.1 s (k = 0.025):
  60 nm   → 287 nm
  100 nm  → 296 nm
  ≥ 1 µm  → 310 nm

AA width bias (illustrative): dense periphery AA +0.5 nm per side
relative to isolated (more passivation in narrow trenches)
```

These differences are absorbed by the periphery design rules and by optical proximity correction of the periphery mask. They must be re-characterized whenever the etch changes.

### 12.5.3 Sense-Amplifier Regions Next to the Array

The sense amplifiers sit immediately beside the array, in the bit-line direction. Their transistors are matched pairs, and a depth or width gradient across a pair produces an offset in the sense amplifier. The transition from the dense array to the sense-amplifier region is a gradient in product density and passivation. Layouts keep matched pairs parallel to the array edge, so that both members see the same distance from the array.

---

## 12.6 The Depth Budget

```
Cell line-space depth, 3σ contributions (illustrative):

  Term                                         3σ (nm)    Notes
  ─────────────────────────────────────────────────────────────────────────
  Radial non-uniformity (±1.5% after tuning)   3.8
  Wafer-to-wafer / chamber-to-chamber          3.8        After APC
  (±1.5% after APC)
  Pitch walk (2 nm range → ±2.75 nm)           2.8
  Local space variation from LWR/placement     3.0        Chapter 2
  (≈ ±1.1 nm × 2.75)
  Mask height (±2 nm)                          0.5        Small through ARDE
  Breakthrough / native-oxide variation        1.5
  ─────────────────────────────────────────────────────────────────────────
  RSS                                          ≈ 7.0
  Allocation (Chapter 1: target 250, min 220)  ±15 for margin
```

The budget is met with margin for the cell. The periphery budget is tighter, because its window is narrower and the same rate variation moves the open periphery further in absolute terms (310 nm × 1.5% = 4.7 nm per term).

---

## 12.7 Reducing Depth Loading

### 12.7.1 Strategies

```
Strategy                         How it works                      Cost / limit
──────────────────────────────────────────────────────────────────────────────────────────
Synchronized pulsing, lower      Raises neutral-to-ion ratio;      Open-area rate;
duty (Chapter 6)                 bottom ion-limited; lower k       taper at low duty
Higher ME-2 pressure             More radicals per ion; lower k    Angular spread;
(Chapter 7)                                                        taper; bow
Passivation loading ("inverse    More film in wide trenches        Hard to control;
RIE lag" chemistries: deposition (where line-of-sight flux is      profile in the
from the gas phase favors open   higher) slows them               periphery
areas)
Quasi-ALE cycling (Chapter 7)    Self-limiting steps reduce        Throughput;
                                 aspect-ratio dependence           scalloping
Separate periphery depth         Two etches, or a block mask on    Extra mask and
(dual-depth, Chapter 14)         one region for part of the etch   etch; overlay
                                                                   at the boundary
Accept a shallower periphery     Relax the periphery window by     Design changes
                                 design (lower HV isolation need)  (well doping,
                                                                   spacing)
```

### 12.7.2 Choosing a Strategy

```
Required window (±%)    Achievable with                      k needed
──────────────────────────────────────────────────────────────────────────
≥ ±6%                   Single step, pulsed (reference)      ≤ 0.025
±4–6%                   Single step + tight APC              ≤ 0.035
< ±4%                   Pulsing + quasi-ALE, or dual-depth   ≤ 0.040 with
                                                             cycling; ≤ ≈ 0.05
                                                             with dual depth
                                                             (periphery widths
                                                             still need it,
                                                             Chapter 14)
```

For each new node, the cell window shrinks (narrower spaces, higher aspect ratio) while the periphery window stays similar. The ARDE coefficient must fall with each node just to keep the same window. When it cannot, a dual-depth scheme becomes necessary.

---

## 12.8 Failure Modes

```
Failure                          Cause                             Consequence
───────────────────────────────────────────────────────────────────────────────────────────
Shallow cell (< 220 nm)          Low rate; high k; narrow spaces   Thin oxide under the
                                 (pitch walk); self-limited V       passing WL → parasitic
                                                                   channel → AA-to-AA
                                                                   leakage; retention and
                                                                   row-hammer degradation
Deep cell (> 280 nm)             High rate; overlong etch          Collapse margin −15%
                                                                   per 10 nm (Ch. 11);
                                                                   bottom closure; fill
Deep periphery (> 330 nm)        High rate; low k recipe drift     Fill voids in wide
                                 toward CW behavior                trenches; stress;
                                                                   dishing at CMP
Shallow periphery 60 nm          Low rate; high periphery          Leakage between dense
(< 270 nm)                       passivation                       periphery transistors
                                                                   (sense amplifiers)
Depth walk excess                Pitch walk out of spec            Variation in oxide under
                                                                   passing WL; lean
```

Shallow cell trenches are the most dangerous because they are the hardest to see: the trenches look normal from above and in most OCD models. They show up electrically as an increase in retention-tail bits and in row-hammer sensitivity, often weeks later at probe.

---

## 12.9 Summary & Key Takeaways

1. **The periphery sets the window.** For the reference recipe, the window is 58.1–66.0 s, bounded at both ends by periphery requirements.

2. **There is a maximum ARDE coefficient.** Above k ≈ 0.057, no etch time satisfies both cell and periphery. The uncompensated k = 0.058 has no window.

3. **The rate tolerance is about ±6%.** Radial, chamber, drift, product, and mask variations all share it.

4. **Pitch walk is worth 2.75 nm of depth per nm.** A 2 nm space range gives about 5.5 nm of depth walk, smaller in impact than the lean it causes.

5. **Cut gaps etch deeper and island ends pull back.** Cut gaps sit 12–19 nm deeper than line spaces; island ends lose 2–4 nm each, compensated in the cut layout.

6. **Dual depth is the fallback.** When k cannot be lowered enough for the node, separate cell and periphery depths remove the constraint at the cost of a mask.

---

## Study Questions

1. A recipe has k = 0.032 and ER₀ = 300 nm/min. Compute the time limits for each requirement in Section 12.2.1 and the resulting window. How does it compare with the reference?

2. A new node changes the cell space to 16 nm and the cell minimum depth to 210 nm, with the periphery windows unchanged. With k = 0.025, compute the window. What k is needed to restore a ±4 s window?

3. Using ∂D/∂S = 2.75 nm/nm, compute the depth of each space type for α/β/γ = 18.5/20/15 nm (Chapter 2). Is the shallowest space above 220 nm at the reference time? How much margin remains?

4. A design change shortens the cut gap from 24 nm to 20 nm while keeping its effective transport width at 26 nm. Estimate the cut-gap depth and the change in island length if pull-back is 3 nm per end. What must the cut layout do?

5. A product's open-area fraction rises from 0.60 to 0.66, lowering ER₀ by 3.8% (Chapter 3). Without APC, compute the cell, 60 nm periphery, and open periphery depths at 62.1 s. Which requirement fails first?

6. Construct a 3σ depth budget for the open periphery using the same terms as Section 12.6 (scale percentages to 310 nm). What fraction of the ±25 nm window does it consume?

---

**Next Chapter:** [Chapter 13: Etch Damage, Contamination & Data Retention](./13-damage-retention.md)

---

**Chapter 12 Development Status:** Complete  
**Version:** 1.0
