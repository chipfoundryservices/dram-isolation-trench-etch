# Chapter 14: Advanced Schemes — Dual-Depth Isolation, EUV AA, 4F² & 3D DRAM

## Overview

The reference process is a single-step silicon etch of an SAQP-patterned 6F² array. It works because pulsing brings the ARDE coefficient low enough for one recipe to put the cell and the periphery inside their windows, and because low-surface-tension drying keeps the fins upright. Each new generation narrows the margins. The spaces shrink, the aspect ratio rises, the fins get thinner, and the window and the collapse margin both close.

This chapter covers the schemes that respond to that pressure: dual-depth etches that decouple the cell and the periphery, EUV patterning that changes the incoming pattern, the last shrinks of the 6F² cell, the 4F² vertical-channel cell that changes the isolation geometry, and 3D DRAM, where isolation becomes a high-aspect-ratio stack etch.

**Learning Objectives:**
- Design a cell pre-etch dual-depth scheme and compute its depths
- Compare dual-depth schemes by mask count, boundary effects, and recipe freedom
- Describe how EUV AA patterning changes pitch walk, roughness, and defect modes
- Compute the window and collapse margin for a further-shrunk 6F² array
- Describe isolation in 4F² vertical-channel DRAM and its etch challenges
- Describe isolation in 3D DRAM stacks and relate it to 3D NAND stack etch

---

## 14.1 Dual-Depth Isolation

### 14.1.1 Why Decouple

Chapter 12 showed that a single-step etch needs k below about 0.057, and below about 0.025 for a comfortable window. A dual-depth scheme removes this constraint by giving the cell and the periphery different amounts of etch time. It costs a lithography step and introduces a boundary between the two regions.

### 14.1.2 Cell Pre-Etch

The most direct scheme gives the cell a head start:

```
Step 1: Block mask covers the periphery (non-critical lithography)
Step 2: Pre-etch the cell to depth z₁ (periphery protected)
Step 3: Strip the block mask (ash; Book #20)
Step 4: Common etch: cell from z₁ to 250 nm, periphery from 0
```

```
Example with a fast continuous-wave recipe (ER₀ = 380 nm/min,
k = 0.058, h_m = 49 nm, S = 18 nm):

  t(z) = [z + (k/S)(z²/2 + h_m z)] / ER₀

  Cell time to 250 nm:      t(250) = 1.027 min
  Cell time to 55 nm:       t(55)  = (55 + 0.003222 × 4208) / 380
                                   = 68.6 / 380 = 0.180 min
  Common etch needed:       1.027 − 0.180 = 0.846 min = 50.8 s

  At the end of the common etch:
    Periphery open:     380 × 0.846 = 322 nm   ✓ (280–330)
    Periphery 100 nm:   289 nm
    Periphery 60 nm:    273 nm                 ✓ (≥ 270)

  Pre-etch window (all limits met):
    z₁ = 50 nm → open 328, 60 nm 278
    z₁ = 56 nm → open 320, 60 nm 271
    → z₁ = 50–56 nm
```

With a 55 nm pre-etch, the CW recipe that had no window as a single step (Chapter 12) puts every feature in specification at a higher rate. The pre-etch depth becomes a tuning knob for the cell-periphery offset.

The window on z₁ is narrow, though, and the reason is instructive. The pre-etch decouples the cell from the periphery, but **the periphery's own width range still feels ARDE**. At k = 0.058, the 60 nm periphery trenches end about 49 nm shallower than the open areas, which uses most of the room between "60 nm ≥ 270" and "open ≤ 330". A dual-depth scheme with a moderately pulsed recipe (k ≈ 0.04) gives a much wider window on both z₁ and time, and is the usual practical choice.

### 14.1.3 Other Dual-Depth Schemes

```
Scheme                    Sequence                                Notes
───────────────────────────────────────────────────────────────────────────────────────
Cell pre-etch             Block periphery; etch cell; strip;      Common etch gives
(above)                   common etch                             matched profiles at
                                                                  the end of the trench
Periphery post-etch       Common etch to cell depth; block the    Used when the
                          cell; etch periphery deeper             periphery must be
                                                                  much deeper than ARDE
                                                                  gives
Separate modules          Cell isolation and periphery            Full freedom; two
                          isolation patterned and etched          hard-mask schemes;
                          independently                           highest cost
```

### 14.1.4 The Boundary

```
Effects at the cell / periphery boundary (block-mask edge):
  - Block-mask overlay places the edge in the dummy region; a 20–50 nm
    overlay budget is easily accommodated by the dummy AA lines
  - A step forms in the trench floor where the pre-etched and
    non-pre-etched regions meet
  - The resist strip after the pre-etch exposes 55 nm fins to an ash
    and possibly a wet clean; at this height the fins are
    (250/55)⁴ ≈ 430 times stiffer against capillary loads than at full
    depth, so collapse is not a concern
  - Two etch steps on the cell: a profile mark at z₁ (keep z₁ above the
    word-line region, as in Chapter 7)
```

The pre-etch depth must therefore stay well above 140 nm. At 55 nm, the mark lies above the saddle fin but inside the depth band of the storage-node junction, where its effect on island width and on sidewall damage must be checked (Chapter 13).

---

## 14.2 EUV Active-Area Patterning

### 14.2.1 EUV Cuts and EUV Islands

```
Approach                        What changes for the etch
──────────────────────────────────────────────────────────────────────────────────
SAQP lines + EUV cut            Fewer cut exposures (one instead of two ArFi);
                                better cut-to-cut overlay; island ends more
                                uniform. Lines and pitch walk unchanged
EUV single-exposure islands     No SAQP: no α/β/γ pitch walk, no depth walk from
(direct 2D print)               it. Higher roughness and stochastic defects;
                                island shape set directly by the mask and resist
```

### 14.2.2 Roughness Instead of Pitch Walk

```
Comparison at 32 nm pitch (illustrative, 3σ):

                              SAQP + cut          EUV direct islands
  ────────────────────────────────────────────────────────────────────
  Space range (pitch walk)    ≤ 2 nm              ≈ 0 (no SAQP)
  LER per edge                2.4 nm              3.0–3.5 nm
  Edge correlation            High (ρ ≈ 0.8)      Low (ρ ≈ 0–0.3)
  LWR                         1.4 nm              4.0–4.5 nm
  Local space variation       ≈ 3.1 nm            ≈ 4.5 nm

Etch consequences of EUV direct:
  - No periodic depth walk, but more random local depth variation:
    ≈ 2.75 × 4.5/2 ≈ ±6 nm (3σ) from local space variation alone
  - More random fin-width variation → transistor variability
  - Random capillary asymmetry → lean in random locations rather than
    with the SAQP period
```

EUV direct patterning trades a systematic error that can be measured and corrected (pitch walk) for a random one that cannot. The isolation etch can reduce the random part only by smoothing roughness during transfer (Chapter 2) and by lowering k, which shrinks every width-to-depth conversion.

### 14.2.3 Stochastic Defects

EUV resists at these dimensions can fail locally: a missing opening (a space that does not print) or a bridge (two islands joined). In the etched array, a missing space is an AA bridge just like the particle bridges of Chapter 9. Because stochastic failures scale with the number of features, failure probabilities of 10⁻¹⁰ to 10⁻¹² per feature are needed for billions of islands. The etch can help slightly, for example by a descum or trim that clears partially printed spaces, but cannot fix a space that is fully closed in the resist.

### 14.2.4 Thinner Patterning Stacks

EUV resists are thin (20–40 nm), and underlayers are thinner too. The hard-mask open must transfer the pattern through a shorter, less forgiving stack. The silicon etch itself still uses the SiO₂/SiN/pad-oxide mask, so its selectivity budget is unchanged, but the incoming mask CD and edge quality depend more on the open.

---

## 14.3 Further 6F² Shrinks

```
Next-node 6F² array (illustrative):

  Parameter                      Reference      Next node
  ─────────────────────────────────────────────────────────
  AA pitch                       32 nm          28 nm
  W_t / S_t                      14 / 18 nm     12 / 16 nm
  Cell depth                     250 nm         240 nm
  A (with 49 nm mask)            16.6           18.1
  Fin H / W_t                    17.9           20.0
```

### 14.3.1 Window

```
k = 0.025, ER₀ = 300 nm/min, cell minimum 215 nm, periphery unchanged:

  Cell ≥ 215 nm (S = 16):    t ≥ [215 + (0.025/16)(215²/2 + 49 × 215)] / 300
                             = (215 + 52.6) / 300 = 0.892 min = 53.5 s
  Periphery 60 nm ≥ 270 nm:  58.1 s     (unchanged)
  Periphery open ≤ 330 nm:   66.0 s     (unchanged)

  Window: 58.1 – 66.0 s (still periphery-bound)
```

The cell's lower limit moves, but the window is still set by the periphery, so it does not shrink. What shrinks is the cell's own margin inside it: at 62 s the 16 nm spaces are about 245 nm deep, 30 nm above their minimum, and the narrowest pitch-walked spaces have less.

### 14.3.2 Collapse Margin

```
w_eff ≈ 1.49 × 12 = 17.9 nm (1.0°), H = 240 nm, s = 16 nm, IPA:
  M = 1.03 E w_eff³ / H⁴ ÷ 4 γ / s²
    ≈ 0.87

The next-node fin is unstable under IPA drying at the reference angle.
```

The next shrink needs at least one of: a lower-surface-tension or meniscus-free drying process (supercritical CO₂, vapour-phase cleans), a shallower isolation enabled by a shallower buried word line, more taper (with its fill cost), or a process order that fills the trenches before any liquid touches the fins. Each is in use or development. Their combined difficulty is one reason the industry is moving toward 4F² and 3D cells.

---

## 14.4 Isolation in 4F² Vertical-Channel DRAM

### 14.4.1 The Cell

A 4F² cell places the transistor vertically: a silicon (or oxide-semiconductor) pillar with the bit line below, the storage capacitor on top, and the word line wrapped around the pillar's sides. Each cell occupies 2F × 2F.

```
Vertical-channel cell (schematic cross-section along the word line):

      capacitor   capacitor   capacitor
          │           │           │
       ┌──┴──┐     ┌──┴──┐     ┌──┴──┐
  WL ══╡     ╞═════╡     ╞═════╡     ╞══   word line wraps the pillars
       │ Si  │     │ Si  │     │ Si  │     (gate on two or four sides)
       │pillar│    │pillar│    │pillar│
       └──┬──┘     └──┬──┘     └──┬──┘
  ════════╧═══════════╧═══════════╧══════  buried bit line
```

### 14.4.2 What Isolation Becomes

```
Function                         6F² BCAT                    4F² VCT
──────────────────────────────────────────────────────────────────────────────
Isolation trench                 Around tilted islands,      Two orthogonal sets:
                                 one etch                    between bit lines
                                                             (deep) and between
                                                             word lines
Channel                          Saddle fin along the WL     Vertical pillar; its
                                 trench                      width is the gate
                                                             control dimension
Depth requirement                Below WL saddle + margin    Through the pillar
                                                             height to separate
                                                             buried bit lines
Mechanical structure             Walls (islands 84 nm long)  Free-standing pillars
                                                             (square, ≈ 2F wide
                                                             pitch both ways)
```

### 14.4.3 Etch Challenges

```
1. Pillar mechanics. A pillar has no long dimension to stiffen it; it
   can bend in any direction, and capillary collapse in 2D arrays forms
   clusters of four. Pillars are usually supported or filled before any
   wet step.

2. Bit-line separation. The trench between bit lines must cut through
   the bit-line layer (doped Si, silicide, or metal) beneath the pillars,
   which requires a change of chemistry at depth and, for a metal bit
   line, an etch-stop and selectivity design closer to a contact etch.

3. Two directions of ARDE. Trenches along and across the array may have
   different widths and therefore different depths, which must both
   reach the bit-line level.

4. Gate-all-around control. The pillar width at the word-line height
   sets the gate control, as the saddle-fin width does in 6F². Taper
   in pillars changes width in both directions.
```

Oxide-semiconductor (IGZO) channel variants of 4F² DRAM move the channel to a deposited film and change the isolation problem again: the critical etch becomes a dielectric hole or trench etch rather than a silicon trench.

---

## 14.5 Isolation in 3D DRAM

### 14.5.1 Stacked Horizontal Cells

3D DRAM proposals stack horizontal 1T1C cells in many layers. A common approach grows a Si/SiGe superlattice epitaxially, etches deep trenches or slits through it to define strips, removes the SiGe laterally to separate the silicon layers, and builds the transistors and capacitors horizontally from the sides.

### 14.5.2 The Isolation Etch Becomes a Stack Etch

```
Stack (illustrative): 32 × (Si 30 nm / SiGe 20 nm) = 1.6 µm
Slit width: 60–100 nm → aspect ratio 16–27

Challenges:
  - Alternating materials: SiGe etches faster than Si in Cl/Br
    chemistries → scalloped sidewalls with a period of one pair;
    similar to the ON-stack striation of 3D NAND (Books #24, #25)
  - Depth and straightness through micrometres, with tilt and bow
    budgets like a 3D NAND slit
  - Mask budget: µm-scale silicon etch needs a thick carbon or oxide
    mask (Book #19)
  - Lateral recess control: the subsequent selective SiGe removal
    depends on uniform exposure of every layer along the slit
```

The physics of Chapter 3 still applies, but the problem moves toward the high-aspect-ratio stack etches of 3D NAND: transport over micrometres, mask budgets measured in microns, edge tilt over a deep trench, and striation from alternating layers. The lessons of this book on damage, passivation, and the conversion of geometry errors into device errors carry over directly.

---

## 14.6 Roadmap

```
Generation      Cell / isolation                   Key etch challenge
───────────────────────────────────────────────────────────────────────────────────
1a / 1b         6F² BCAT; SAQP + cut; single-step  Low k; pitch walk; IPA collapse
                isolation, pulsed                  margin; retention
1c / 1d         6F² BCAT; EUV cuts or islands;     Random roughness; collapse
                possibly dual-depth                margin < 1 without new drying
                                                   or shallower WL
4F²             Vertical channel (Si or IGZO);     Pillar etch and support; bit-
                buried bit line                    line separation; 2D collapse
3D DRAM         Stacked horizontal cells           Si/SiGe stack slit etch;
                (Si/SiGe superlattice)             striation; tilt; lateral
                                                   recess uniformity
```

---

## 14.7 Summary & Key Takeaways

1. **Dual depth removes the cell–periphery constraint.** A 50–56 nm cell pre-etch lets a fast CW recipe with k = 0.058, which has no single-step window, put the cell at 250 nm and every periphery width in specification. The periphery's own width range still needs moderate k for a robust window.

2. **The boundary is manageable.** It falls in the dummy region; the pre-etch mark should stay above the word-line region.

3. **EUV trades systematic for random.** Direct EUV islands remove pitch walk but bring higher, uncorrelated roughness and stochastic bridges.

4. **The next 6F² shrink is mechanically marginal.** A 12 nm AA at 240 nm depth has an IPA collapse margin below 1. New drying or process order is required.

5. **4F² changes the geometry.** Isolation runs in two directions and must separate buried bit lines; pillars are mechanically weaker than walls.

6. **3D DRAM turns isolation into a stack etch.** Si/SiGe slits of micrometre depth inherit the problems of 3D NAND high-aspect-ratio etch.

---

## Study Questions

1. Using the CW recipe of Section 14.1.2, compute the pre-etch depth z₁ that puts the open periphery at exactly 305 nm when the cell reaches 250 nm. What is the 60 nm periphery depth then, and is it in specification? What does this tell you about the k needed in the common etch?

2. For the next-node array of Section 14.3, compute the collapse margin for H = 220 nm. What buried word-line depth change would this require, if the oxide margin of 40 nm is kept?

3. An EUV direct-island process has LER = 3.2 nm per edge with zero edge correlation. Compute LWR and the local space variation (3σ) between two independent neighboring edges. Estimate the 3σ local depth variation with ∂D/∂S = 2.75 nm/nm.

4. Compare the cost of a dual-depth scheme (one extra non-critical lithography and an ash) with the cost of lowering k from 0.040 to 0.025 by pulsing (open-area rate −21%, same cell time). Which would you choose for a fab with idle conductor-etch capacity and a tight lithography budget?

5. Explain why pillars in a 4F² array are more prone to capillary collapse than the 84 nm-long islands of a 6F² array, even at the same width and height.

6. A 3D DRAM slit etch through a Si/SiGe stack shows a 2 nm lateral scallop at every SiGe layer. Using the concepts of Chapters 4 and 10, suggest two chemistry changes and one hardware change that would reduce it.

---

**Next Chapter:** [Chapter 15: Endpoint, Metrology & Advanced Process Control](./15-endpoint-metrology-apc.md)

---

**Chapter 14 Development Status:** Complete  
**Version:** 1.0
