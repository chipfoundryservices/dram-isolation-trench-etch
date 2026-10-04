# Preface: The Etch That Draws the Transistor

## Why This Book Exists

Most isolation etches are judged by the trench. A logic STI trench has to be deep enough, have the right slope, and fill without voids, and the silicon between trenches is usually wide enough that nobody worries about it. The DRAM cell array turns this around. The silicon left between the trenches is an island 14 nm wide and 250 nm tall, and it is the most valuable structure on the chip. It holds two access transistors. Its top surface takes one bit-line contact and two storage-node contacts. Its sidewalls form the junctions that must hold a few femtocoulombs of charge for 64 ms at 85 °C, and for much longer in most cells. There are more than eight billion of these islands on a 16 Gb die, and the chip is only as good as its worst few thousand.

DRAM isolation etch became a defining process when the industry moved to the **buried-channel array transistor** and the **6F² cell**. The word line is no longer a planar gate on top of the silicon. It is buried in a trench that cuts across the active areas and the isolation between them. Where it crosses an island, the gate wraps over the top and down the sides of a short silicon fin, and the depth of that fin is set by how much deeper the word line goes in the isolation than in the silicon. Where it passes beside an island it does not control, it is a **passing gate**, only one trench width away from the storage-node junction. Both relationships depend on the depth, slope, and shape of the isolation trench.

The method, a timed silicon etch through an oxide/nitride hard mask, looks routine. It asks a great deal of the plasma etch:

1. **Depth in the narrowest spaces.** The cell trenches must be deeper than the saddle-fin bottom of the buried word line, with margin. They are 18 nm wide, so ARDE makes them etch at about 70% of the open-area rate by the time they reach depth, while the periphery etches at full rate beside them.

2. **Verticality to a fraction of a degree.** At 250 nm depth, a sidewall 1° off vertical moves each wall 4.4 nm inward. Two walls take 8.7 nm from an 18 nm trench. At 2° the trench closes completely before it reaches its target depth.

3. **The right silicon width at every depth.** The AA width at the surface sets the contact area. The width at 140–180 nm depth sets the saddle-fin channel width and the drive current. The width at the bottom sets the fin's stiffness. All three come from one profile.

4. **Uniform depth across alternating spaces.** Self-aligned quadruple patterning leaves three kinds of trench in a repeating sequence, each 1–3 nm different in width. ARDE turns those width differences into depth differences, and the buried word line sees them as different saddle fins.

5. **Fins that stay upright.** A silicon fin with a height-to-width ratio near 18 is close to the limit where the surface tension of the rinse water pulls neighbors together. Any asymmetry in the etch, the clean, or the fill can tip it.

6. **Silicon that stays clean.** Every sidewall the plasma touches becomes part of a storage-node junction. Ion damage, implanted hydrogen and bromine, and residue that survive the liner oxidation become leakage paths that set the data-retention tail.

This book treats DRAM isolation as a **precision silicon patterning process in its own right**, not as a logic STI recipe applied to a denser layout.

---

## Unique Aspects of DRAM Isolation Etch

### 1. The Silicon Is the Feature

In most etch steps, the critical dimension is the opening. In DRAM isolation, the critical dimensions are the islands. Engineers talk about the AA width at the top, at the word-line depth, and at the bottom, and about the AA length and the shape of the AA ends. The trench is what is left over. A recipe that widens the trench by 1 nm per side narrows the transistor by 2 nm, which can be 15% of its width.

### 2. Two Patterns, One Etch

The cell array and the periphery share one hard mask and one etch. The array is a dense, nearly uniform field of 18 nm spaces. The periphery has trenches from 60 nm to tens of microns wide, beside large open active regions for sense amplifiers, word-line drivers, and I/O transistors. The same plasma must produce 250 nm in the array and about 300 nm in the periphery, and both depths have windows of a few tens of nanometres.

### 3. Lines and Cuts

The active areas are made as long lines and then cut into islands. The etch sees two different openings: the long, narrow line spaces, which behave like slots, and the cut gaps between island ends, which are short openings joined to the line spaces on both sides. They etch at different rates and leave different shapes. The island ends, where the storage-node contacts land, are shaped by the cut and by the etch together.

### 4. No Etch Stop

The trench ends in bulk silicon. There is no layer to stop on and no reliable optical signal from the bottom of a 250 nm trench 18 nm wide. Depth is controlled by time, by the stability of the chamber, and by feed-forward and feedback from metrology.

### 5. The Fin Is Mechanical

The isolation etch makes the tallest, thinnest free-standing silicon structures in high-volume manufacturing. They are stable while they stand in vacuum, but every later step that puts liquid or stressed film between them pushes them sideways. The etch decides how much margin they have, through their height, their width at the base, and how evenly spaced they are.

---

## Why This Book Is Organized This Way

Book #26 follows the same four-part structure as Books #19–25:

**Part I: Fundamentals (Chapters 1–4)**
- Why the cell array needs isolation trenches and what sets their geometry, how the active areas are patterned, the physics of silicon etch in sub-20 nm trenches, and the chemistry of the etch and its passivation

**Part II: Hardware (Chapters 5–9)**
- The reactors, bias and pulsing systems, gas and recipe structure, temperature and chuck control, and wall, edge, and contamination management that let one chamber etch a dense array and a sparse periphery together

**Part III: Phenomena (Chapters 10–14)**
- Profile and AA width, fin bending and collapse, depth loading, damage and retention, and advanced isolation schemes

**Part IV: Production (Chapters 15–16)**
- Endpoint, metrology, APC, the integration steps that use the trench, yield, and cost

### Reading Paths

**Process Engineers:** Chapters 3, 4, 7, 10, 12, 13  
→ Recipe design, profile and AA width, depth loading, damage control

**Equipment Engineers:** Chapters 5–9, 15  
→ Reactor selection, pulsing, gas and temperature control, chamber walls, endpoint hardware

**Integration Engineers:** Chapters 1, 2, 10, 11, 12, 16  
→ AA layout and patterning, profile budget, fin stability, cell/periphery depth, downstream steps

**Device Engineers:** Chapters 1, 10, 13, 16  
→ How isolation errors become retention tails, leakage, row-hammer sensitivity, and variability

**Researchers:** Chapters 3, 4, 6, 11, 13, 14  
→ Nanoscale transport, passivation, collapse mechanics, damage, next-generation DRAM

---

## Key Questions This Book Answers

1. **Why does the depth of the isolation trench depend on the buried word line, and how deep must the cell trench be?**
2. **Why do the cell trenches etch more slowly than the periphery, and how is the depth difference brought inside both windows?**
3. **How much sidewall angle can an 18 nm trench afford before its bottom closes, and what does angle do to the transistor?**
4. **How does SAQP pitch walk turn into depth walk, and how large is it?**
5. **Why do tall silicon fins lean or collapse, and how much margin does the reference fin have?**
6. **What does the plasma do to the silicon that becomes the storage-node junction, and how is that damage removed?**
7. **How is depth controlled without an etch stop or a usable endpoint at the trench bottom?**
8. **How does isolation change for EUV-patterned active areas, 4F² vertical-channel cells, and 3D DRAM?**
9. **What does the isolation etch cost per wafer, and how does that compare with what it costs when it goes wrong?**

---

## How to Read This Book

**Complete study (2–3 weeks):** Read Part I closely, then work through Parts II and III in order. Finish with Part IV.

**Focused study (3–5 days):** Read Chapters 1 and 3, then follow the reading path for your role.

**Reference mode:** Go straight to the chapter you need. Use the INDEX, GLOSSARY, and the Appendix G troubleshooting guide.

**Every chapter includes:**
- Learning objectives
- Quantitative models with worked numerical examples
- Representative production values, labelled as illustrative where appropriate
- Summary and key takeaways
- Study questions

**Appendices provide:**
- A: Silicon, mask, liner, and chamber material properties
- B: Etch chemistry and reaction data
- C: Standard operating procedures
- D: Process windows and lookup tables
- E: Trench geometry, transport, and mechanical calculations
- F: Endpoint and metrology reference
- G: Troubleshooting guide

---

## A Note on Data and Depth

The relationships in this book (ion-enhanced silicon etching, halogen and oxybromide surface chemistry, free-molecular transport, sheath physics, beam mechanics, capillary forces, defect-assisted junction leakage) are well established in the literature. The specific numbers in recipes, tables, and worked examples are **representative**. They are chosen to be physically consistent and close to typical practice, but they are not qualified conditions for any particular tool, layout, or node. Where a value is illustrative, the text says so and shows the arithmetic, so readers can repeat the analysis with their own measurements.

Throughout the book, a **reference process** ties the examples together:

```
Reference device:      1b-class DRAM, 6F² cell, buried-channel array transistor
                       (BCAT); word-line pitch 34 nm, bit-line pitch 51 nm
                       (F = 17 nm, cell area 6F² = 1734 nm²)
Reference AA:          SAQP lines at pitch P = 32 nm (normal to the line),
                       tilted ≈ 20° from the bit-line direction (illustrative)
                       top width W_t = 14 nm, line space S_t = 18 nm
                       islands L_AA = 84 nm long, cut gap G = 24 nm
                       (period 108 nm along the line)
Reference cell trench: depth D_c = 250 nm (spec 220–280 nm)
                       sidewall angle 1.0° from vertical
                       → fin base 22.7 nm, trench bottom 9.3 nm
                       aspect ratio 13.9 (Si only), 16.6 with the mask
Reference periphery:   STI widths 60 nm – 20 µm; depth D_p = 300 nm
                       (spec 280–330 nm)
Reference mask:        20 nm SiO₂ cap / 25 nm SiN / 4 nm pad SiO₂
                       (h_m = 49 nm at the start of the silicon etch)
Reference word line:   buried WL bottom 140 nm deep in the AA, 180 nm in the
                       isolation → 40 nm saddle fin
Reference etch:        ICP, 13.56 MHz source + 13.56 MHz bias, synchronized
                       pulsing; HBr/Cl₂/O₂/He; open-area Si rate 300 nm/min;
                       ARDE coefficient k = 0.025 → cell main etch ≈ 62 s
```

We assume you know basic plasma physics and the general logic STI process from earlier books. We do **not** assume you know DRAM cell architecture, buried word-line integration, SAQP pitch walk, nanoscale pattern collapse, or the link between etch damage and data retention.

---

## Organization of This Repository

1. **README.md**: overview, scope, file structure, cross-references
2. **PREFACE.md**: this document
3. **INDEX.md**: detailed chapter outline, reading paths, estimated times
4. **chapters/**: Chapters 1–16
5. **appendices/**: Appendices A–G
6. **GLOSSARY.md**: technical terminology

---

## Acknowledgments & Scope

Book #26 is part of the **ChipFoundryServices Technical Series**. It draws on:

- The published plasma etch literature on silicon trench etch, halogen chemistry, sidewall passivation, ARDE, and pulsed plasmas
- Classical results on free-molecular flow through channels (Knudsen, Clausing) and on beam mechanics and capillary collapse
- Published descriptions of DRAM cell architecture, buried word lines, and retention physics
- Representative industrial practice for DRAM active-area modules
- The earlier books in this series, especially Books #21 and #22

It is a **technical reference for professionals**. Background in plasma processing is assumed.

---

## Final Thought

An active area is one small rectangle repeated sixteen billion times. It is also a silicon fin a quarter of a micron tall that must be the right width at every depth, stand straight through a wet clean, and carry a junction that holds its charge for longer than almost anyone will ever ask it to.

Mastering DRAM isolation etch means seeing that **the silicon left behind is the product, the narrowest trench sets the depth, and the sidewall the plasma touches becomes the junction that sets retention**. This book is meant to build that understanding.

---

**Welcome to Book #26: DRAM Isolation Trench Etch — Active-Area Patterning and Cell-Array Isolation for Buried-Channel DRAM.**

---

**Preface Version:** 1.0  
**Last Updated:** 2026-10-04
