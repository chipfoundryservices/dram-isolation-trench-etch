# Book #26: DRAM Isolation Trench Etch — Active-Area Patterning and Cell-Array Isolation for Buried-Channel DRAM

## Overview

**Book #26** is a technical reference on **DRAM isolation trench etch**: the silicon plasma etch that cuts the dense array of isolation trenches around every active area (AA) in a DRAM cell array, together with the wider and deeper shallow-trench isolation (STI) of the periphery, in a single step. In a modern 6F² DRAM, the active areas are short silicon islands, about 14 nm wide and 85 nm long, packed at a pitch of about 32 nm and tilted at an angle to the word lines. The etch turns a patterned hard mask into a forest of these islands, each standing about 250 nm tall, separated by trenches only 18 nm wide at the top. The trench aspect ratio is about 14:1. The silicon fin that remains between two trenches has a height-to-width ratio near 18:1.

Each island is the body of two access transistors and the landing for one bit-line contact and two storage-node contacts. The isolation trench around it has several jobs at once. It is the **isolation** that stops charge stored on one capacitor from leaking to a neighbor. It **defines the transistor**: the width of the silicon left between trenches is the channel width of the buried-channel array transistor (BCAT), and the depth and profile of the trench set the shape of the saddle fin that the buried word line wraps around. It sets the **spacing to the passing word line**, the gate of a neighboring cell that runs through the isolation beside the island and drives row-hammer disturbance. And because every surface the etch touches becomes the sidewall of a storage-node junction, it sets the **data-retention tail** of the whole chip.

The basic method is easy to state. Pattern a thin oxide/nitride hard mask with self-aligned quadruple-patterned lines and a cut mask. Break through the native oxide. Etch the silicon anisotropically in an HBr/Cl₂/O₂ plasma in an inductively coupled reactor, relying on a thin silicon-oxybromide film on the sidewalls for direction. Stop on time, because there is no etch-stop layer in bulk silicon. **The trench must be deep enough between the islands, the islands must stay the width they were drawn, and nothing may lean, touch, or be damaged.**

Doing it in production is hard. The cell array and the periphery are etched at the same time but have trench widths that differ by three orders of magnitude, so aspect-ratio-dependent etching (ARDE) makes the periphery 25–55% deeper than the array. Self-aligned quadruple patterning leaves three different trench widths that alternate across the array, and ARDE turns that pitch walk into a depth walk. A sidewall angle 1° off vertical widens each fin by 9 nm over its height and closes the trench bottom to 9 nm. The tall, thin fins bend under capillary forces in the wet clean that follows, under the stress of the fill, and under asymmetric ion and charging forces during the etch itself. The ions that make the trench vertical also damage and implant the silicon that will form the junctions. This book covers the physics, chemistry, equipment, and production engineering that make DRAM isolation etch work.

---

## Intended Audience

This book is written for **semiconductor industry professionals** with working knowledge of plasma processing:

- **Process Engineers**: developing silicon trench recipes for dense DRAM arrays; controlling depth, sidewall angle, AA width, bottom shape, and cell/periphery depth loading
- **Equipment Engineers**: specifying inductively coupled conductor-etch chambers with pulsed source and bias, multi-zone temperature control, and edge tuning; managing chamber walls, seasoning, and contamination in bromine chemistries
- **Integration Engineers**: setting AA width, trench depth, and profile against buried word-line, bit-line contact, storage-node contact, and fill requirements; managing pattern collapse through clean and fill
- **Device Engineers**: understanding how isolation etch errors become retention tails, gate-induced drain leakage, row-hammer sensitivity, AA-to-AA leakage, and transistor variability
- **Researchers**: studying sub-20 nm trench transport, sidewall passivation, nanoscale pattern collapse, plasma-induced damage in silicon, and isolation for 4F² vertical-channel and 3D DRAM

The material assumes a working knowledge of plasma physics (Books #1–5) and advanced plasma engineering (Books #11–15). Book #21 (Shallow Trench Isolation Etch) covers the general logic STI process this book builds on. Book #22 (Spacer Etchback) describes the spacer etches inside self-aligned multiple patterning, and the companion volume *Polysilicon Etch* covers the HBr/Cl₂/O₂ silicon chemistry in a gate context.

---

## Technical Scope

### Core Concepts Covered

**Architecture & Geometry:**
- The 6F² buried-channel DRAM cell: active-area islands, buried word lines, bit-line and storage-node contacts
- Isolation trench geometry: AA pitch and width, line spaces and cut gaps, depth, aspect ratio, fin height-to-width ratio
- The depth requirement from saddle-fin word lines and junction-to-junction leakage
- The sidewall-angle budget: fin widening with depth and trench-bottom closure

**Patterning & Masks:**
- Self-aligned quadruple patterning (SAQP) of AA lines and the three-space pitch walk
- AA cut (chop) masks, cut-first and cut-last schemes, EUV single-patterned cuts
- The SiO₂/SiN/pad-oxide hard mask, mask open, and remaining-mask requirements
- Periphery STI patterning merged into the same hard mask

**Etch Physics & Chemistry:**
- Ion-neutral synergy in silicon etch; free-molecular transport in sub-20 nm trenches
- ARDE in line spaces, cut gaps, and periphery trenches; reverse-ARDE strategies
- HBr/Cl₂/O₂ chemistry, SiOₓBrᵧ sidewall passivation, selectivity to oxide and nitride
- Breakthrough of native oxide and pad oxide; fluorine additives and their risks

**Equipment Design:**
- Inductively coupled (TCP-type) reactors with independent source and bias
- Synchronized source and bias pulsing, low ion energy, and narrow angular distributions
- Gas delivery, multi-step recipes, and cyclic (quasi-atomic-layer) variants
- Wafer temperature and multi-zone electrostatic chucks for radial profile control
- Wall deposits, seasoning, edge rings, and metal and particle contamination

**Process Phenomena:**
- Taper, bottom rounding, top-corner rounding, and AA width at every depth
- Fin bending, leaning, and pattern collapse during etch, clean, and fill
- Cell/periphery depth loading, pitch-walk depth walk, and island-end effects
- Plasma-induced damage, bromine and hydrogen in silicon, and the retention tail
- Advanced schemes: dual-depth isolation, EUV AA patterning, 4F² vertical-channel and 3D DRAM isolation

**Production Integration:**
- Timed etch without a stop layer: endpoint for breakthrough, depth control by APC
- OCD scatterometry, CD-SEM, cross-section TEM, and electrical monitors
- Liner oxidation, nitride liner, gap fill, CMP, and the buried word-line recess as customers of the etch
- Yield signatures, throughput, and cost of ownership

### Technology Context

- **Device architectures:** 6F² buried-channel array transistor (BCAT) DRAM from the 1x to the 1c generation (DDR5, LPDDR5X, HBM core dies); 4F² vertical-channel transistor (VCT) DRAM and 3D DRAM as emerging forms
- **Isolation structures:** dense cell-array trenches between AA islands (primary focus) and periphery STI etched in the same step. Separate periphery isolation flows are covered where they differ
- **Process sequence:** Isolation etch follows AA line patterning (SAQP), AA cut, periphery patterning, and hard-mask open. It comes before liner oxidation, nitride liner, gap fill, CMP, and the buried word-line trench etch
- **Manufacturing scale:** 300 mm wafers, one isolation etch per wafer, 60–90 s of silicon etch inside a 2.5–3.5 min chamber cycle, a large fleet of conductor-etch chambers per DRAM fab

---

## Book Organization

### Part I: Fundamentals (4 Chapters)

**Chapter 1: The DRAM Cell Array & the Role of the Isolation Trench**
- The 1T1C cell, the 6F² layout, and tilted active-area islands
- The four jobs of the isolation trench: isolation, transistor definition, passing-gate spacing, junction surface
- Geometry, aspect ratio, and the depth requirement from the buried word line
- Where isolation etch sits in the flow and the specification sheet

**Chapter 2: Active-Area Patterning — SAQP Lines, Cuts & the Hard-Mask Stack**
- SAQP of AA lines and the origin of three trench widths
- AA cut masks and island-end shapes
- The hard-mask stack and the mask-open etch
- Periphery patterning and the merged mask

**Chapter 3: Silicon Trench Etch Physics at Sub-20 nm Widths**
- Ion-neutral synergy in silicon etch
- Free-molecular transport in line spaces, cut gaps, and wide trenches
- ARDE models and the time-to-depth curve for the reference array
- Charging, ion deflection, and where symmetry breaks

**Chapter 4: Silicon Etch Chemistries & Sidewall Passivation**
- HBr, Cl₂, O₂, and additives: what each does
- The SiOₓBrᵧ passivation film: formation, thickness, and transport
- Selectivity to oxide and nitride masks
- Breakthrough chemistry and post-etch residue

### Part II: Hardware Design (5 Chapters)

**Chapter 5: Inductively Coupled Reactor Architecture for DRAM Isolation Etch**
- Why ICP conductor chambers dominate silicon trench etch
- Source and bias decoupling, ion flux and energy
- Pumping, residence time, and wall area
- Throughput, fleet size, and chamber matching

**Chapter 6: Ion Energy, Bias Pulsing & Angular Control**
- Ion energy for anisotropy versus damage
- Bias frequency and the ion energy distribution
- Synchronized source and bias pulsing
- Ion angular distribution and its effect on a 14:1 trench

**Chapter 7: Gas Delivery, Pressure & Multi-Step Recipe Design**
- Pressure, flow, and residence time as separate knobs
- Breakthrough, main-etch, and profile steps; depth-dependent ramps
- Cyclic and quasi-atomic-layer etch variants
- Center/edge gas tuning

**Chapter 8: Wafer Temperature, Electrostatic Chucks & Radial Control**
- Temperature dependence of passivation and profile
- Heat balance and multi-zone chucks
- Radial tuning of CD, angle, and depth
- Thermal transients in short recipes

**Chapter 9: Chamber Walls, Edge Control & Contamination**
- Wall deposits in bromine chemistries and the first-wafer effect
- Waferless autoclean and seasoning
- Edge rings, edge tilt, and edge CD
- Metal, particle, and micromasking defects

### Part III: Process Phenomena (5 Chapters)

**Chapter 10: Profile Control — Taper, Bottom Shape, Corner Rounding & AA Width**
- The sidewall-angle budget and trench-bottom closure
- Bottom rounding, microtrenching, and V-shaped bottoms
- Top-corner rounding and mask facets
- AA width at the surface, at word-line depth, and at the bottom

**Chapter 11: Fin Bending, Leaning & Pattern Collapse**
- Stiffness of tall, thin silicon fins
- Capillary collapse in the post-etch clean
- Bending from etch asymmetry, charging, and fill stress
- Design and process remedies

**Chapter 12: Depth Loading — Cell Versus Periphery, Pitch Walk & Island Ends**
- Cell/periphery depth difference and its window
- Pitch-walk depth walk across the array
- Cut gaps, island ends, and array-edge effects
- Reverse-ARDE and ARDE-reduction strategies

**Chapter 13: Etch Damage, Contamination & Data Retention**
- Ion damage, hydrogen and bromine incorporation, and carbon residue
- How damage becomes junction leakage and the retention tail
- Liner oxidation as damage removal and the width it costs
- Damage-aware recipe design

**Chapter 14: Advanced Schemes — Dual-Depth Isolation, EUV AA, 4F² & 3D DRAM**
- Dual-depth and two-step isolation etch
- EUV single-patterned AA and direct cut patterning
- Isolation for 4F² vertical-channel DRAM
- Isolation in 3D DRAM stacks

### Part IV: Production Scale (2 Chapters)

**Chapter 15: Endpoint, Metrology & Advanced Process Control**
- Endpoint for breakthrough; depth by time
- OCD scatterometry, CD-SEM, and cross-section TEM
- Electrical and inline monitors of isolation quality
- Feed-forward and feedback APC

**Chapter 16: Post-Etch Integration, Yield & Cost of Ownership**
- Clean, liner oxidation, nitride liner, and gap fill
- CMP and the buried word-line recess
- Defect modes and yield signatures
- Throughput, consumables, and cost-of-ownership modeling

---

## Key Technical Themes

1. **The islands are the product.** The isolation etch is judged by the silicon it leaves, not the trench it makes. AA width at the surface, at word-line depth, and at the trench bottom is transistor width, contact area, and fin stiffness.
2. **Depth is needed where it is hardest to get.** The narrow cell trenches need depth for isolation below the buried word line, yet ARDE makes them the slowest-etching features on the wafer.
3. **Angle is the hidden budget.** In an 18 nm trench, every 0.5° of sidewall angle takes 4.4 nm from the trench bottom and adds 4.4 nm to the fin base. The trench closes before 260 nm at 2°.
4. **Pitch walk becomes depth walk.** SAQP leaves alternating trench widths, and ARDE turns each nanometre of width difference into 2–4 nm of depth difference.
5. **Tall fins move.** A 250 nm silicon fin 14–23 nm wide is near the limit of capillary stability. Etch asymmetry, cleans, and fill stress must all be designed to keep it upright.
6. **Every sidewall is a junction.** Damage, implanted hydrogen and bromine, and residue on the trench wall become leakage paths at the storage-node junction. The isolation etch writes the retention tail.

---

## Cross-References to Prior Books

**Related Books in the Series:**

- **Books #1–5** (Plasma Physics & Chemistry Fundamentals): sheath physics, ion energy and angular distributions, radical generation and transport
- **Books #6–10** (Dielectric Etch & Fluorocarbon Chemistry): the oxide and nitride hard-mask open that precedes the silicon etch
- **Books #11–15** (Advanced Plasma Engineering): ICP sources, RF delivery, pulsing, gas delivery, endpoint detection
- **Book #19** (Carbon Hard Mask Etch): carbon underlayers used in the SAQP and cut patterning stacks
- **Book #20** (Photoresist Ashing): removal of carbon and resist layers before the silicon etch
- **Book #21** (Shallow Trench Isolation Etch): general STI etch, liners, and isolation physics for logic
- **Book #22** (Spacer Etchback): spacer deposition and etchback inside self-aligned multiple patterning
- **Companion volumes:** *Polysilicon Etch*, which covers HBr/Cl₂/O₂ silicon chemistry and selectivity to thin oxide in a gate context, and *Silicon Nitride Etch: Chemistry, Selectivity and Integration*, which covers the nitride hard mask and liner removal

DRAM isolation etch takes the logic STI etch of Book #21 and applies it to the densest, narrowest silicon pattern in high-volume manufacturing, where the silicon left behind is as important as the trench removed.

---

## File Organization

```
dram-isolation-trench-etch/
├── README.md            ← You are here
├── PREFACE.md
├── INDEX.md
├── GLOSSARY.md
│
├── chapters/
│   ├── 01-dram-cell-isolation-architecture.md
│   ├── 02-aa-patterning-hardmask.md
│   ├── 03-si-trench-physics.md
│   ├── 04-chemistry-passivation.md
│   ├── 05-icp-reactor-architecture.md
│   ├── 06-ion-energy-pulsing.md
│   ├── 07-gas-pressure-steps.md
│   ├── 08-temperature-esc-radial.md
│   ├── 09-walls-edge-contamination.md
│   ├── 10-profile-aa-width.md
│   ├── 11-fin-bending-collapse.md
│   ├── 12-depth-loading-cell-peri.md
│   ├── 13-damage-retention.md
│   ├── 14-advanced-isolation-schemes.md
│   ├── 15-endpoint-metrology-apc.md
│   └── 16-integration-yield-coo.md
│
└── appendices/
    ├── A-material-properties.md
    ├── B-chemistry-reaction-data.md
    ├── C-standard-procedures.md
    ├── D-process-windows.md
    ├── E-trench-geometry-transport-calculations.md
    ├── F-endpoint-metrology-reference.md
    └── G-troubleshooting-guide.md
```

---

## Constraints & Scope

### What This Book Covers
✅ Silicon isolation trench etch for 6F² buried-channel DRAM cell arrays (primary focus)  
✅ Periphery STI etched in the same step, and dual-depth alternatives  
✅ AA patterning (SAQP, cuts, hard mask) as the input to the etch  
✅ Equipment design, chamber control, and production integration  
✅ The processes that use the trench (liner, fill, CMP, buried word line, contacts) as customers of the etch  
✅ Retention, leakage, and yield impact; cost of ownership  

### What This Book Does NOT Cover
❌ Logic STI in general, beyond what DRAM shares with it (see Book #21)  
❌ Lithography and SAQP deposition in detail, beyond what the etch inherits  
❌ The buried word-line etch and metal recess, beyond what the isolation must provide  
❌ Capacitor (storage-node) etch and detailed DRAM circuit design  
❌ Vendor-specific recipes or proprietary tool parameters  

### A Note on Numbers
Numbers in this book come from established plasma physics, published literature trends, and representative production practice. Worked examples use **illustrative values** chosen to show the method, and the arithmetic is written out so readers can substitute their own data. A single **reference process** (a 1b-class 6F² array with 32 nm AA pitch, 14 nm AA width, 250 nm cell trench depth, 300 nm periphery depth, and a 49 nm SiO₂/SiN/pad-oxide hard mask) is used across chapters so that examples connect. The ARDE, sidewall-angle, and pattern-collapse numbers in Chapters 3, 10, 11, and 12 come from closed-form models written out in Appendix E. Treat recipe values as starting points for a design of experiments, never as qualified process conditions.

---

## Development Status

**Book #26 Foundation:** Complete  
**Part I (Chapters 1–4):** Complete  
**Part II (Chapters 5–9):** In progress  
**Part III (Chapters 10–14):** Planned  
**Part IV (Chapters 15–16):** Planned  
**Back Matter (Appendices A–G, Glossary):** Planned  

---

## Next Steps

1. **Read [PREFACE.md](./PREFACE.md)** for the motivation and reading guidance
2. **Read [INDEX.md](./INDEX.md)** for the detailed chapter outline and reading paths by role
3. **Begin [Chapter 1](./chapters/01-dram-cell-isolation-architecture.md)**: The DRAM Cell Array & the Role of the Isolation Trench

---

**Book #26 Version:** 1.0  
**Last Updated:** 2026-10-04  
**Series:** ChipFoundryServices Technical Series
