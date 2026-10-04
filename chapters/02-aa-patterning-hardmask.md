# Chapter 2: Active-Area Patterning — SAQP Lines, Cuts & the Hard-Mask Stack

## Overview

The isolation etch starts from a hard mask that already contains the full active-area pattern: 32 nm-pitch lines in the cell array, cut into islands, and the larger, irregular active areas of the periphery. Almost every geometric property of the finished islands is first decided here. The width of each AA line, the width of each space, the shape of every island end, and the roughness of every edge come from the patterning sequence. The silicon etch can only preserve them, or make them worse.

This chapter follows the pattern from lithography to the open hard mask. It explains how self-aligned quadruple patterning (SAQP) makes 32 nm-pitch lines, why it leaves three different space widths, how the lines are cut into islands, what the hard-mask stack must do, and how the periphery is merged into the same mask. It ends with the list of incoming properties the silicon etch inherits.

**Learning Objectives:**
- Describe the SAQP sequence and compute final line and space widths from mandrel and spacer dimensions
- Derive the three-space pitch walk and its sensitivity to each patterning error
- Compare spacer-is-line and spacer-is-space tone choices for DRAM AA
- Compute the cut-hole window from overlay and describe the island-end shape
- Explain the roles and thickness choices of the SiO₂/SiN/pad-oxide hard mask
- Size the effect of mask-open taper on the silicon opening
- List the incoming properties the isolation etch inherits and their tolerances

---

## 2.1 From Lithography to 32 nm Lines

### 2.1.1 Why Multiple Patterning

A 32 nm pitch is beyond single-exposure 193 nm immersion lithography (practical limit about 76–80 nm pitch for lines). DRAM makers reach it with **self-aligned quadruple patterning**: one lithography step at four times the final pitch, followed by two rounds of spacer deposition and etchback. EUV single exposure at 32 nm pitch is possible but has historically given worse roughness and stochastic defects than SAQP for long dense lines (Chapter 14).

### 2.1.2 The SAQP Sequence

```
Step                                        Result (reference, spacer-is-line)
───────────────────────────────────────────────────────────────────────────────────
1. Litho: core-1 (mandrel) lines            Pitch 128 nm, line CD M = 46 nm
2. Spacer-1 deposition (ALD oxide or        Thickness t₁ = 18 nm on every wall
   nitride) and etchback (Book #22)
3. Mandrel-1 removal                        Spacer-1 lines, width t₁ = 18 nm,
                                            pitch 64 nm (two per mandrel)
4. Spacer-2 deposition and etchback         Thickness t₂ = 14 nm on every wall
5. Spacer-1 removal                         Spacer-2 lines, width t₂ = 14 nm,
                                            pitch 32 nm (four per 128 nm)
6. Transfer into the hard mask              AA line pattern in SiO₂ cap / SiN
```

```
Cross-section through one 128 nm period (schematic):

Step 1:      ████████                                  mandrel M = 46
Step 3:    ▐█▌        ▐█▌                              spacer-1, t₁ = 18
Step 5:  ▐▌   ▐▌    ▐▌   ▐▌                            spacer-2, t₂ = 14
         │α │β  │α │  γ  │
         └──┴───┴──┴─────┘
         Four lines, four spaces per period:
         α appears twice (where spacer-1 stood)
         β once (inside the former mandrel)
         γ once (between former mandrels)
```

### 2.1.3 Line and Space Widths

In the spacer-is-line tone, the final lines are spacer-2, and their width is the spacer-2 deposition thickness. The three spaces are:

```
α = t₁                          (where a spacer-1 line stood)
β = M − 2 t₂                    (inside the original mandrel)
γ = P₁ − M − 2 t₁ − 2 t₂        (between original mandrels; P₁ = 128 nm)

Reference: t₁ = 18, t₂ = 14, M = 46
  α = 18
  β = 46 − 28 = 18
  γ = 128 − 46 − 36 − 28 = 18        ✓ all spaces 18 nm, lines 14 nm

Check: 4 × 14 + 2α + β + γ = 56 + 36 + 18 + 18 = 128 ✓
```

---

## 2.2 Pitch Walk: Three Spaces

### 2.2.1 Error Sensitivities

Each patterning error moves different spaces:

```
Error                  ∂α        ∂β        ∂γ        Line width
──────────────────────────────────────────────────────────────────────
δM (mandrel CD)        0         +δM       −δM       unchanged
δt₁ (spacer-1)         +δt₁      0         −2δt₁     unchanged
δt₂ (spacer-2)         0         −2δt₂     −2δt₂     +δt₂
```

The line width depends only on the spacer-2 thickness, which ALD controls to a few tenths of a nanometre across the wafer. The spaces carry all the other errors. **In spacer-is-line SAQP, AA width is well controlled and pitch walk appears in the trenches.**

### 2.2.2 A Worked Example

```
Mandrel CD 2 nm wide (M = 48), spacer-1 0.5 nm thick (t₁ = 18.5):

  α = 18.5
  β = 48 − 28 = 20.0
  γ = 128 − 48 − 37 − 28 = 15.0

Check: 56 + 2(18.5) + 20 + 15 = 128 ✓

Spaces now 18.5 / 20.0 / 18.5 / 15.0 nm in a repeating sequence.
Range: 5 nm (28% of nominal)
```

The silicon etch sees each space as a separate trench. Through ARDE, the narrow γ space etches shallower than the wide β space. Chapter 12 computes this **depth walk** and shows that it is the main source of saddle-fin variation along the word line.

### 2.2.3 Controlling Pitch Walk

```
Lever                            Removes                    Limit
──────────────────────────────────────────────────────────────────────────
Mandrel CD control (litho dose,  δM                         Litho and mandrel-
mandrel trim etch)                                          etch CD uniformity
Spacer-1 thickness (ALD)         δt₁                        Deposition uniformity
                                                            (±0.2–0.3 nm)
Spacer etchback footing/         Effective t₁, t₂ at the    Etchback profile
profile (Book #22)               base vs. top               (Book #22)
Feed-forward: mandrel CD →       β − γ imbalance            Metrology for each
spacer-1 thickness or mandrel                               lot; APC
trim
```

Pitch walk is measured after step 5 or after hard-mask transfer, usually by CD-SEM with space-type identification or by scatterometry with a three-space model (Chapter 15). A typical production specification is a range of ≤ 2 nm between the widest and narrowest space type.

### 2.2.4 Spacer-Is-Line Versus Spacer-Is-Space

The tone can be reversed: fill the spaces between spacer-2 lines, remove the spacers, and the spacers become the trenches. Then the trench width is the spacer-2 thickness, and the line widths carry the errors.

```
Tone               AA width              Trench width          Etch consequence
──────────────────────────────────────────────────────────────────────────────────────
Spacer-is-line     Uniform (t₂)          Three values          Depth walk;
                                                               uniform transistors
Spacer-is-space    Three values          Uniform (t₂)          Uniform depth;
                                                               three transistor
                                                               widths
```

DRAM makers have used both. The choice is a device question: whether the array tolerates three AA widths (drive-current and contact-area variation) better than three trench depths (saddle-fin variation). The reference process uses spacer-is-line. The isolation etch must then minimize the conversion of space-width differences into depth differences.

---

## 2.3 Edge Roughness

### 2.3.1 Sources

Spacer-defined lines inherit the roughness of the mandrel edge they were deposited on. Because both edges of a spacer-2 line are deposited on the same spacer-1 wall, they are highly correlated: the line moves sideways as a whole, but its width varies little.

```
Roughness of reference spacer-2 lines (illustrative, 3σ):
  Line-edge roughness (LER), each edge     ≈ 2.4 nm
  Line-width roughness (LWR)               ≈ 1.4 nm
  Placement (centerline) roughness         ≈ 2.2 nm

For uncorrelated edges: LWR = √2 × LER = 3.4 nm
Measured 1.4 nm → strong positive correlation between the two edges
  ρ = 1 − LWR²/(2 LER²) = 1 − 1.96/11.52 = 0.83
```

### 2.3.2 Transfer Into Silicon

The silicon etch partly smooths short-wavelength roughness (the passivation film averages out features a few nanometres long) and partly amplifies it (the mask erodes faster at protrusions). Line placement roughness in one line is space-width roughness for the trench beside it. A 2.2 nm placement wiggle in two neighboring lines, if uncorrelated between lines, gives local space-width variation of about √2 × 2.2 ≈ 3.1 nm (3σ). That variation, like pitch walk, turns into local depth and profile variation through ARDE.

---

## 2.4 Cutting Lines Into Islands

### 2.4.1 Cut Schemes

```
Scheme          Where the cut is made                     Notes
──────────────────────────────────────────────────────────────────────────────────
Cut-last        Cut holes opened over the finished line   Most common; cut shape
(hard-mask      pattern in the SiO₂ cap; exposed line     sets island end shape;
cut)            segments etched away                      line already at final CD
Cut-first       Cut applied to an intermediate layer      Cut edges follow spacer
(core cut)      (mandrel or spacer-1) before the final    processing; sharper ends
                spacer                                    but more complex
Direct EUV      Islands printed directly as a 2D pattern  Removes SAQP and cut;
                                                          stochastic defect risk
                                                          (Chapter 14)
```

The reference process uses cut-last: after the AA lines are transferred into the SiO₂ cap, a cut lithography step opens holes over the line where the cut gaps belong, and a short oxide etch removes the exposed line segments.

### 2.4.2 Cut Pitch and Lithography

The cuts are staggered from one AA line to the next. The nearest cut-to-cut distance in the reference layout is well below the single-exposure ArFi limit, so cuts are made either with two ArFi exposures (litho-etch-litho-etch) or with a single EUV exposure. Each additional exposure adds an overlay term between cut sets.

### 2.4.3 The Cut Window

A cut hole must sever the line completely but must not nick the neighboring lines:

```
Cut hole width across the line: w_c
Overlay error (3σ) of cut to lines: OL

Full cut:            w_c ≥ W_t + 2·OL
No nick of neighbor: w_c ≤ W_t + 2·S_t − 2·OL     (hole edge stays in the space)

Reference: W_t = 14, S_t = 18, OL = 4 nm
  Lower limit: 14 + 8  = 22 nm
  Upper limit: 14 + 36 − 8 = 42 nm
  Chosen:      w_c = 32 nm (centered, ±10 nm window)

The window shrinks with pitch: at P = 28, W_t = 12, S_t = 16, OL = 3.5:
  19 ≤ w_c ≤ 37 → still workable; OL is the dominant term
```

With pitch walk, the neighbor on one side may be closer than nominal. The upper limit uses the narrowest adjacent space (γ = 15 nm in the example of Section 2.2.2), which tightens it to 14 + 30 − 8 = 36 nm.

### 2.4.4 Island-End Shape

A cut hole is round or elliptical in plan view. Where it crosses the 14 nm line, its edge is curved, so the island end is rounded or slightly pointed rather than square. Along the line, the cut length sets the gap G.

```
Island-end features (plan view at the mask):

     ═══════════╮          ╭═══════════
                 )  cut   (                ← rounded ends
     ═══════════╯   gap   ╰═══════════
                ◄── G = 24 ──►

Cut placement error along the line, δ:
  one island gets longer by δ, its neighbor shorter by δ
  → the two storage-node contacts of an island see different
    landing areas
```

The island ends are where the storage-node contacts land and where the passing word line comes closest to the junction (Chapter 1). End shape and end position are therefore among the most closely watched dimensions after the etch. Section 12.3 shows how the silicon etch further rounds and pulls back the ends.

---

## 2.5 The Hard-Mask Stack

### 2.5.1 Layers and Roles

```
Reference hard mask (top to bottom, at the start of the silicon etch):

  Layer              Thickness   Role
  ─────────────────────────────────────────────────────────────────────────
  SiO₂ cap (PECVD    20 nm       Mask for the silicon etch (Si:SiO₂
  or ALD)                        selectivity 30–50 in HBr/O₂); protects SiN
  SiN (LPCVD)        25 nm       CMP stop after gap fill; second mask if
                                 the cap is consumed
  Pad SiO₂           4 nm        Stress buffer between SiN and Si; later
  (thermal)                      removed with the SiN
  ─────────────────────────────────────────────────────────────────────────
  Total h_m          49 nm       Adds to the aspect ratio (Chapter 1)
```

Above this stack, during patterning, sit the SAQP and cut layers (carbon underlayer, SiON or SiC hard masks, spacers). These are removed or consumed during transfer and hard-mask open (Books #19, #20).

### 2.5.2 Why Not a Thicker Mask?

A thicker mask adds margin against erosion but costs aspect ratio and makes the mask lines themselves tall and thin:

```
Mask line aspect ratio (height / width) at the start of the Si etch:
  49 / 14 = 3.5     (reference)
  80 / 14 = 5.7     (if the cap were 51 nm)

Each extra 10 nm of mask:
  - raises the total aspect ratio by 10/18 = 0.56
  - costs ≈ 1% of the cell etch rate at depth through ARDE in the
    reference recipe, ≈ 2% in an uncompensated chemistry (Chapter 3)
  - makes the mask lines more prone to wiggling during the open
```

The reference stack is sized so that roughly 10 nm of SiO₂ cap remains after the silicon etch (Chapter 4), which keeps the SiN intact for CMP.

### 2.5.3 The Hard-Mask Open

The hard-mask open is a dielectric etch (Books #6–10), often in a capacitively coupled chamber, sometimes in-situ in the silicon etch chamber:

```
Step               Chemistry (illustrative)       Key requirement
─────────────────────────────────────────────────────────────────────────────
SiO₂ cap           CF₄/CHF₃/Ar or C₄F₈/O₂/Ar      Vertical; no bowing of the
                                                  14 nm lines
SiN                CH₂F₂/CF₄/O₂ or CHF₃/O₂        Vertical; stop on pad oxide
Pad oxide          CF₄-based, short               Clear to Si everywhere;
                                                  minimal Si recess
```

### 2.5.4 Mask-Open Taper and the Silicon Opening

The silicon sees the width of the opening at the bottom of the mask. Any taper in the 49 nm mask open narrows it:

```
Opening at the Si surface:  S_Si = S_mask,top − 2 h_m tan β

h_m = 49 nm
  β = 0.5°:  2 × 49 × 0.00873 = 0.9 nm → S_Si = 17.1 nm (from 18.0)
  β = 1.5°:  2 × 49 × 0.0262  = 2.6 nm → S_Si = 15.4 nm
  β = 3.0°:  2 × 49 × 0.0524  = 5.1 nm → S_Si = 12.9 nm
```

Because the AA width at the silicon surface is the mask's bottom CD, mask-open taper also widens the AA. The reference process defines W_t = 14 nm and S_t = 18 nm **at the silicon surface**, after the mask open. Mask CD targets above the silicon are set by working back from these through the measured mask-open bias.

### 2.5.5 Queue Time and Native Oxide

Once the pad oxide is opened, bare silicon is exposed to air. A native oxide of 0.5–1.0 nm grows within hours. The silicon etch must begin with a breakthrough step to remove it (Chapter 4). Queue-time limits (typically a few hours) between hard-mask open and isolation etch keep the native oxide thin and predictable, and also limit moisture uptake by the mask.

---

## 2.6 Periphery and Array Boundaries

### 2.6.1 Merging the Periphery

The periphery contains sense amplifiers, sub-word-line drivers, row and column decoders, and I/O. Its active areas are larger and irregular, and its isolation trenches range from about 60 nm to tens of microns wide. They are patterned by a separate lithography step, usually with a block mask that protects the cell array during periphery patterning and vice versa, and merged into the same hard mask before the open.

### 2.6.2 The Array Edge

SAQP lines cannot simply stop at the array edge. The last few lines are dummies, and the transition region between the dense cell array and the periphery contains dummy AAs, wider spaces, and terminated lines. Two consequences follow for the etch:

```
At the array edge:
  - The last active AA line has a dense neighbor on one side and a wide
    space (or dummy) on the other → asymmetric etch, polymer, and later
    capillary forces → lean (Chapter 11)
  - Spaces next to the dummies are wider → deeper trenches (ARDE),
    different profile
Standard remedy: several dummy AA lines (2–6) outside the last active
line, so active cells see only array-like neighbors
```

---

## 2.7 Pattern Density

The silicon open area affects the etch rate through macroloading: the more silicon is exposed, the more etchant is consumed (Chapter 3).

```
Cell array:
  AA area fraction = (W_t / P) × (L_AA / period) = (14/32) × (84/108)
                   = 0.4375 × 0.778 = 0.34
  Trench (open Si) fraction = 0.66

Periphery: open fraction typically 0.4–0.6 (illustrative)

Wafer level (array ≈ 55% of die area, periphery ≈ 40%, scribe ≈ 5%):
  Open Si fraction ≈ 0.55 × 0.66 + 0.40 × 0.5 + 0.05 × 0.7 ≈ 0.60
```

About 60% of the wafer surface is etched silicon. This is high compared with a logic STI layer, and it makes the isolation etch strongly reactant-limited. Changes in die layout, scribe design, or edge die exclusion change the loading and therefore the rate (Chapter 7).

---

## 2.8 What the Silicon Etch Inherits

```
Incoming property                      Reference          Tolerance (illustr.)
──────────────────────────────────────────────────────────────────────────────────
AA width at Si surface                 14.0 nm            ± 0.8 nm (3σ)
Space widths α / β / γ at Si surface   18 / 18 / 18 nm    Range ≤ 2 nm
Line-width roughness (3σ)              1.4 nm             ≤ 1.8 nm
Cut gap G                              24 nm              ± 2 nm
Cut placement along line               0                  ± 4 nm (3σ)
Mask height h_m                        49 nm              ± 2 nm
SiO₂ cap                               20 nm              ± 1.5 nm
Mask-open sidewall angle               ≤ 0.5°             ≤ 1.0°
Pad-oxide residue on Si                None               None (blocks Si etch)
Native oxide                           ≤ 1 nm             Queue time ≤ 4 h
Periphery CD                           Per design         Per design
```

**The isolation etch can correct almost none of these.** It can shift all AA widths together by changing its etch bias, and it can reduce the depth consequences of space-width differences by reducing ARDE. It cannot remove pitch walk, roughness, or cut errors. These belong to the patterning module and must be controlled there.

---

## 2.9 Summary & Key Takeaways

1. **SAQP makes the 32 nm pitch.** One 128 nm-pitch lithography step and two spacers give four lines and four spaces per period, with three distinct space types.

2. **Pitch walk lives in the spaces.** In spacer-is-line SAQP, AA width equals the spacer-2 thickness and is well controlled. Mandrel and spacer-1 errors move the α, β, and γ spaces in different directions.

3. **Tone is a device choice.** Spacer-is-line gives uniform transistors and variable trenches. Spacer-is-space gives uniform trenches and variable transistors.

4. **Cuts shape the island ends.** The cut window is set by overlay and the narrowest neighboring space. Cut shape and placement set the end shape and the storage-node contact area.

5. **The hard mask is thin by design.** 49 nm of SiO₂/SiN/pad oxide balances erosion margin against aspect ratio and mask-line stability. Its open taper sets the silicon opening.

6. **The etch inherits nearly everything.** Pitch walk, roughness, and cut errors must be controlled upstream. The etch can only avoid amplifying them.

---

## Study Questions

1. An SAQP process has P₁ = 128 nm, M = 45 nm, t₁ = 17.5 nm, and t₂ = 14.5 nm. Compute the line width and the α, β, and γ spaces. Check that they sum to 128 nm.

2. The mandrel CD varies by ±1.5 nm (3σ) and the spacer-1 thickness by ±0.3 nm (3σ), independently. Compute the 3σ variation of β − γ. Which error dominates?

3. A cut process has OL = 5 nm (3σ). The AA width is 14 nm and the narrowest neighboring space is 16 nm. Compute the cut-width window. What overlay would close the window entirely?

4. The SiO₂ cap is increased from 20 nm to 30 nm to gain mask margin. Compute the new total aspect ratio for the reference cell trench and the change in mask-line height-to-width ratio. What does Chapter 3's ARDE model predict for the change in cell etch time (use k = 0.025)?

5. A mask open leaves a sidewall angle of 1.2° in a 49 nm mask. Compute the silicon opening and the AA width at the silicon surface if the mask top CDs are 14 nm lines and 18 nm spaces. What mask top CDs would restore the reference values?

---

**Next Chapter:** [Chapter 3: Silicon Trench Etch Physics at Sub-20 nm Widths](./03-si-trench-physics.md)

---

**Chapter 2 Development Status:** Complete  
**Version:** 1.0
