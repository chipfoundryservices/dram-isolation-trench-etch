# Chapter 1: The DRAM Cell Array & the Role of the Isolation Trench

## Overview

A DRAM stores each bit as charge on a capacitor, reached through a single access transistor. The cell array packs these one-transistor, one-capacitor (1T1C) cells as tightly as lithography and physics allow. In every DRAM made since the 6F² buried-channel generation, the transistors sit in short silicon islands called **active areas** (AAs), and every island is surrounded by an isolation trench filled with dielectric. The plasma etch that forms those trenches is the subject of this book.

This chapter explains why the cell array is built from islands, what the isolation trench has to do for the transistor, the contacts, and the stored charge, and how those jobs set the trench's depth, width, and profile. It ends with the specification sheet that the rest of the book works to.

**Learning Objectives:**
- Describe the 1T1C cell, the 6F² layout, and the geometry of tilted AA islands
- Explain the four jobs of the isolation trench: isolation, transistor definition, passing-gate spacing, and junction surface
- Compute stored charge and the leakage budget that retention imposes
- Derive the minimum cell trench depth from the buried word-line saddle fin
- Compute aspect ratios, fin height-to-width ratios, and AA width at depth for the reference process
- Place the isolation etch in the DRAM front-end flow and read its specification sheet

---

## 1.1 The 1T1C Cell

### 1.1.1 Storing a Bit

```
One DRAM cell:

        Bit line (BL)
            │
            │ bit-line contact (DC)
          ┌─┴─┐
   WL ────┤ T ├──── access transistor (buried-channel, n-type)
          └─┬─┘
            │ storage-node contact (BC)
          ══╪══ storage capacitor C_s (≈ 8 fF), plate at V_PL = V_DD/2
            │
           ───

Write:  WL high, BL driven to V_DD ("1") or 0 ("0")
Hold:   WL low (negative), transistor off; charge must stay on C_s
Read:   BL precharged to V_DD/2; WL high; charge sharing moves BL by
        ΔV_BL = (V_DD/2) · C_s / (C_s + C_BL); sense amplifier restores
```

The stored signal is small:

```
Reference values (illustrative):
  C_s = 8 fF, V_DD (array) = 1.1 V, plate at V_DD/2

  Charge relative to the plate:  Q = C_s · V_DD/2 = 8 fF × 0.55 V = 4.4 fC
                                  = 4.4×10⁻¹⁵ / 1.602×10⁻¹⁹ ≈ 27,500 electrons

  BL signal with C_BL = 40 fF:   ΔV_BL = 0.55 × 8/48 = 92 mV
```

### 1.1.2 The Retention Budget

The access transistor is never perfectly off, and the storage-node junction is never perfectly tight. The cell must be refreshed before it loses enough charge that the sense amplifier misreads it. The standard refresh interval is 64 ms (32 ms above 85 °C in many specifications).

```
Allowed signal loss before misread: ≈ 40% (illustrative; sense margin,
noise, and coupling take the rest)

  ΔQ_allowed = 0.4 × 4.4 fC = 1.76 fC

  Maximum average leakage over 64 ms:
  I_max = ΔQ / t_REF = 1.76×10⁻¹⁵ C / 0.064 s = 2.8×10⁻¹⁴ A = 28 fA
```

Most cells leak far less than this, often well below 1 fA at 85 °C, and hold their data for seconds. The chip's refresh interval is set by the few thousand **tail cells** out of eight billion that leak tens of femtoamperes. These tail cells almost always have a defect at or near the storage-node junction: a trap in the depletion region, a damaged interface, or a local high field. Much of that junction is the sidewall of the isolation trench. **The retention tail is partly written by the isolation etch** (Chapter 13).

---

## 1.2 The 6F² Array and Its Active Areas

### 1.2.1 Cell Area

DRAM layouts are described in units of F, the minimum half-pitch. A 6F² cell is 2F along the bit line (one word-line pitch) and 3F along the word line (one bit-line pitch):

```
Reference array (illustrative 1b-class):
  F = 17 nm
  Word-line pitch     = 2F = 34 nm
  Bit-line pitch      = 3F = 51 nm
  Cell area           = 6F² = 34 × 51 = 1734 nm²

  16 Gb die: 2³⁴ ≈ 1.72×10¹⁰ cells (plus redundancy)
  Array area = 1.72×10¹⁰ × 1734 nm² = 2.98×10¹⁰ nm² ≈ 29.8 mm²
  At ≈ 55% array efficiency → die ≈ 54 mm²
```

"1b" and similar node names are marketing labels and do not equal F. What matters for the etch is the active-area geometry derived from the cell.

### 1.2.2 Tilted Islands

Each active area is shared by two cells. The bit-line contact (DC) lands in the middle of the island, the two word lines cross it on either side, and a storage-node contact (BC) lands at each end:

```
One AA island (along its length):

   BC        WL₁         DC         WL₂        BC
  ┌────┬───────────┬──────────┬───────────┬────┐
  │ SN │  channel  │  shared  │  channel  │ SN │
  │    │  (cell 1) │  BL node │  (cell 2) │    │
  └────┴───────────┴──────────┴───────────┴────┘
  ◄──────────────── L_AA ≈ 84 nm ─────────────►
```

The islands are laid out along lines that are **tilted** away from the bit-line direction, by about 20° in the reference layout. The tilt lets the bit-line contact at the island center sit under a bit line while both storage-node contacts land between bit lines. Every word line crosses each AA line at the same angle, so the spacing of word-line crossings along an AA line is:

```
Spacing of WL crossings along the AA direction:
  d = WL pitch / cos φ = 34 / cos 20° = 36.2 nm

AA line period along the line (one island + one cut gap) spans three
word-line crossings in the reference layout:
  Period = 3 × 36.2 = 108.5 nm

Island area check: each island serves 2 cells → 12F² per island
  AA pitch normal to the line:  P = 32 nm
  Area per island = P × period = 32 × 108.5 = 3472 nm²
  12F² = 12 × 17² = 3468 nm²   ✓
```

Two of the three word-line crossings in each period fall on the island and gate its two transistors. The third falls in the cut gap between islands. That word line is a **passing word line** for this AA line: it runs through isolation and gates transistors in the neighboring AA lines.

```
Reference AA geometry (all at the silicon surface):
  AA pitch normal to the line       P    = 32 nm
  AA width                          W_t  = 14 nm
  Line space (trench width)         S_t  = 18 nm
  Island length                     L_AA = 84 nm
  Cut gap (end-to-end space)        G    = 24 nm
  Period along the line                  = 108 nm
```

### 1.2.3 Plan View of the Array

```
Plan view (schematic, not to scale):

    ╱████████╱   ╱████████╱   ╱████████╱
   ╱        ╱   ╱        ╱   ╱        ╱       ████ AA islands (silicon)
     ╱████████╱   ╱████████╱   ╱████████╱      spaces between them:
    ╱        ╱   ╱        ╱   ╱        ╱       isolation trench
       ╱████████╱   ╱████████╱   ╱████████╱
   ←── line spaces (18 nm) between AA lines
   ←── cut gaps (24 nm) between island ends, staggered line to line

Word lines run horizontally (buried), bit lines vertically (above).
```

The isolation trench is one continuous region that surrounds every island. It has two kinds of opening, the long **line spaces** between neighboring AA lines and the short **cut gaps** between island ends. Where a cut gap meets the line spaces on either side, the opening is locally wider, which matters for transport and depth (Chapter 12).

---

## 1.3 The Buried-Channel Array Transistor

### 1.3.1 Why the Word Line Is Buried

A planar access transistor would need a gate length of about F = 17 nm, far too short to keep subthreshold leakage at the femtoampere level. The buried-channel array transistor (BCAT) solves this by burying the word line in a trench etched across the AA and the isolation. Current flows down one side of the word-line trench, under its bottom, and up the other side. The effective channel length becomes several times the word-line width.

```
Cross-section ALONG an AA island (through two word lines):

  BC          DC          BC
  ▼           ▼           ▼
 ─┬──┐     ┌──┴──┐     ┌──┬─  ← silicon surface
  │n⁺│ WL₁ │ n⁺  │ WL₂ │n⁺│
  │  │ ▓▓▓ │     │ ▓▓▓ │  │
  │  │ ▓▓▓ │     │ ▓▓▓ │  │    WL bottom 140 nm below the Si surface
  │  └─┬─┬─┘     └─┬─┬─┘  │
  │    channel       channel
  │    (wraps under the WL)
  └── p-well ─────────────┘
```

### 1.3.2 The Saddle Fin

The word-line trench cuts through the AA and the isolation at the same time, but the two materials etch differently. The process recesses the isolation oxide deeper than the silicon, so under the word line the silicon stands up as a short fin. The gate wraps over its top and down its sides. This **saddle fin** adds the fin's sidewalls to the channel width and gives the gate much better control.

```
Cross-section ACROSS an AA, under a word line:

           WL metal (TiN/W)
   ┌──────────────────────────────┐
   │   ┌──────────┐               │
   │   │  Si fin  │  gate wraps   │ ← WL bottom in isolation: 180 nm
   │   │  (AA)    │  three sides  │
   │   │          │               │ ← WL bottom on the AA top: 140 nm
 ──┴───┘          └───────────────┴──
  isolation oxide     isolation oxide
       │◄── W(z) ──►│

Saddle-fin height h_sf = 180 − 140 = 40 nm
Channel width ≈ W(140 nm) + 2 h_sf (top plus two sides)
```

The fin's width at 140–180 nm depth is set by the isolation trench profile. This is the first place where the isolation etch draws the transistor (Section 1.4.2).

---

## 1.4 The Four Jobs of the Isolation Trench

### 1.4.1 Job 1: Isolation

The trench must keep each island electrically separate from its neighbors. Three leakage paths matter:

```
Path                              Where                    What prevents it
─────────────────────────────────────────────────────────────────────────────────
SN junction to neighbor SN        Under the cut gap        Trench depth below the
  (end to end)                    between island ends      junctions; p-well doping
SN junction to neighbor AA        Under the line space     Trench depth; oxide
  (side to side)                                           thickness under the WL
Parasitic channel under the       Below the passing WL     Oxide under the WL in
  trench, gated by a WL           in the isolation         the isolation (depth
                                                           margin below 180 nm)
```

The last path sets the depth requirement. Wherever a word line passes through the isolation, its bottom sits 180 nm deep. Below it is fill oxide and then the trench bottom. If the oxide under the word line is thin, the word line can invert the silicon below the trench bottom and connect the two neighboring islands. A margin of about 40 nm of oxide between the word-line bottom and the trench bottom is a typical minimum:

```
Minimum cell trench depth:
  D_min = WL bottom in isolation + oxide margin
        = 180 nm + 40 nm = 220 nm

Target with depth variation of ±15 nm (3σ, Chapter 12):
  D_target ≈ 220 + 15 + 15 (guard) = 250 nm
```

An upper limit comes from the other side. A deeper trench costs fin stability (Chapter 11), a narrower bottom for fill (Chapter 10), and more mask (Chapter 4). In the reference process the upper limit is 280 nm.

### 1.4.2 Job 2: Transistor Definition

The silicon left between trenches is the transistor body. Its width at three depths matters:

```
Depth         What it sets                               Reference value
────────────────────────────────────────────────────────────────────────────
0 nm (top)    BC and DC contact landing area; contact    W_t = 14 nm
              resistance; overlay margin
140–180 nm    Saddle-fin channel width; drive current    W(140) ≈ 18.9 nm
              (write speed, tWR); subthreshold control   W(180) ≈ 20.3 nm
Bottom        Fin stiffness (collapse margin); body      W(250) ≈ 22.7 nm
              connection to the p-well
```

With a straight sidewall at an angle α from vertical, the AA width at depth z is:

```
W(z) = W_t + 2 z tan α

Reference α = 1.0° (tan α = 0.01746):
  W(140) = 14 + 2 × 140 × 0.01746 = 18.9 nm
  W(180) = 14 + 2 × 180 × 0.01746 = 20.3 nm
  W(250) = 14 + 2 × 250 × 0.01746 = 22.7 nm

Trench width at depth: S(z) = P − W(z) = S_t − 2 z tan α
  S(250) = 18 − 8.7 = 9.3 nm
```

A 0.5° change in sidewall angle changes W(140) by 2.4 nm. That is a 13% change in the fin width, enough to move the gate's control of the fin body, and with it the threshold voltage and the off-state leakage that retention depends on. **The sidewall angle is a transistor parameter.**

### 1.4.3 Job 3: Passing-Gate Spacing

A passing word line runs through the isolation beside an island it does not control. In the cut gap, it passes the end of an island, close to that island's storage-node junction. When the passing word line is repeatedly switched on and off, it disturbs the stored charge in the neighboring cell. This is one of the mechanisms of **row hammer**. Its strength depends on how close the passing word line comes to the storage-node junction and on the oxide between them, both of which depend on the shape of the island end and the trench profile in the cut gap (Chapter 12).

### 1.4.4 Job 4: Junction Surface

The storage-node junction sits at the island end, just below the surface. Its depletion region meets the trench sidewall. Whatever the plasma did to that sidewall (displaced silicon atoms, implanted hydrogen and bromine, residual carbon or metal, a rough surface) is inside or next to the depletion region of the one junction in the chip that must leak no more than femtoamperes. The liner oxidation after the etch consumes a few nanometres of sidewall and anneals much of the damage, but only within the width budget of Job 2 (Chapter 13).

---

## 1.5 Geometry and Aspect Ratios

### 1.5.1 Trench Aspect Ratio

```
Reference cell trench:
  Line space at the top:        S_t = 18 nm
  Silicon depth:                D_c = 250 nm
  Hard mask at the start:       h_m = 49 nm (20 nm SiO₂ / 25 nm SiN / 4 nm pad)

  Aspect ratio, silicon only:   A_Si  = 250 / 18 = 13.9
  Aspect ratio with the mask:   A_tot = (250 + 49) / 18 = 16.6

Cut gap:                        G = 24 nm → A_tot = 299 / 24 = 12.5
Periphery trench (narrowest):   60 nm, D_p = 300 nm → A_tot = 349/60 = 5.8
Wide periphery (> 1 µm):        A < 0.4, effectively open area
```

Transport sees the total height, including the mask, because radicals and ions enter at the top of the mask. The aspect ratio falls slightly during the etch as the mask erodes.

### 1.5.2 Fin Height-to-Width Ratio

```
Fin height H = 250 nm
  At the top:   H / W_t   = 250 / 14   = 17.9
  At the base:  H / W(250) = 250 / 22.7 = 11.0
```

No other high-volume structure combines this height-to-width ratio with this density. The fin is stiff enough to stand in vacuum but only marginally stable when a liquid meniscus forms between neighbors (Chapter 11).

### 1.5.3 Generational Trend

```
Generation    AA pitch    AA width    Cell trench    A_Si     Fin H/W
(class)       (nm)        top (nm)    depth (nm)              (top)
──────────────────────────────────────────────────────────────────────────
2x            ~50         ~22         ~280           ~10      ~13
1x            ~42         ~18         ~270           ~11      ~15
1y/1z         ~36         ~16         ~260           ~13      ~16
1a/1b         ~32         ~14         ~250           ~14      ~18
1c/1d         ~28         ~12         ~240           ~15      ~20
(illustrative; values vary by manufacturer)
```

Pitch shrinks faster than depth, because the depth is tied to the buried word line, which cannot shrink as fast without losing channel length. Aspect ratio and fin height-to-width ratio therefore rise every generation. This is why the 4F² vertical-channel cell and 3D DRAM (Chapter 14) change the isolation problem rather than continuing the trend.

---

## 1.6 The Isolation Etch in the Process Flow

### 1.6.1 Before the Etch

```
Step                                   Result
──────────────────────────────────────────────────────────────────────────
1. Pad oxidation                       4 nm SiO₂ on bare Si
2. SiN deposition (LPCVD)              25 nm; later the CMP stop
3. SiO₂ cap deposition                 20 nm; the top hard mask
4. Patterning stack (a-C, SiON)        For SAQP mandrels (Book #19)
5. SAQP of AA lines                    32 nm pitch lines in the cap (Ch. 2)
6. AA cut patterning                   Lines cut into islands (Ch. 2)
7. Periphery AA patterning             Peri active areas merged into the
                                       same mask
8. Hard-mask open                      SiO₂ / SiN / pad oxide opened down to
                                       Si (dielectric etch, Books #6–10)
```

### 1.6.2 The Isolation Etch

```
9. ISOLATION TRENCH ETCH               Breakthrough + silicon main etch
   (this book)                         (+ profile steps) to 250 nm (cell)
                                       and ≈ 300 nm (periphery)
```

### 1.6.3 After the Etch

```
Step                                   What it needs from the etch
──────────────────────────────────────────────────────────────────────────
10. Post-etch clean + drying           Fins that survive capillary forces;
                                       removable residue (Ch. 11, 13)
11. Liner oxidation (radical, ~2.5 nm) A clean, low-damage sidewall; enough
                                       AA width to spend ~1.1 nm/side
12. Nitride liner (optional)           Smooth sidewalls, rounded bottom
13. Gap fill (ALD oxide in the cell,   Trench bottom ≥ ~8 nm wide; no
    flowable/SOD oxide in periphery)   re-entrant profile; uniform depth
14. Anneal, CMP to SiN, SiN strip      Mask left with ≥ 8 nm SiO₂ so the SiN
                                       is intact for CMP
15. Buried word-line trench etch       Uniform cell depth and AA width at
    (Si and oxide recess)              140–180 nm (saddle fin)
16. BC and DC contacts                 AA top width and island-end shape
```

Every one of these customers sees a different part of the trench. The fill sees the bottom, the word line sees the middle, the contacts see the top, and retention sees the sidewall.

---

## 1.7 The Specification Sheet

```
Parameter                           Target         Limit (illustrative)      Customer
──────────────────────────────────────────────────────────────────────────────────────────
Cell trench depth (line space)      250 nm         220–280 nm                Isolation, WL,
                                                                             fin stability
Periphery depth (≥ 1 µm wide)       300 nm         280–330 nm                Peri isolation
Periphery depth (60 nm wide)        ≈ 290 nm       ≥ 270 nm                  Peri isolation
AA top width (post-etch)            14.0 nm        ± 1.0 nm (3σ)             Contacts
AA width at 140 nm                  18.9 nm        ± 1.5 nm (3σ)             WL saddle fin
Sidewall angle (from vertical)      1.0°           0.7–1.25°                 WL, fill
Trench bottom width (cell)          9.3 nm         ≥ 7 nm                    Fill
Bottom shape                        Rounded        No microtrench, no V      Fill, isolation
Top-corner radius (after liner)     2–3 nm         ≥ 1.5 nm                  Gate oxide at WL
Depth walk (α/β/γ spaces)           —              ≤ ± 6 nm                  WL saddle fin
Island-end retreat (per end)        ≤ 5 nm         ≤ 8 nm                    BC contact
Fin lean (top offset)               < 1 nm         ≤ 2 nm; no contact        Contacts, fill
Remaining SiO₂ cap                  ≥ 10 nm        ≥ 8 nm                    CMP stop
Sidewall damage (post-liner)        —              No retention-tail shift   Retention
Defects (residue, micromask)        —              Within module budget      Yield
```

**No item on this sheet is about the trench alone.** Each one is a requirement passed back from a step that uses the silicon or the trench later in the flow.

---

## 1.8 Summary & Key Takeaways

1. **The isolation trench surrounds every AA island.** In a 6F² array, each island carries two cells, and the islands are tilted lines cut into 84 nm segments at a 32 nm pitch.

2. **The trench has four jobs.** It isolates islands, defines the transistor width, sets the spacing to the passing word line, and forms the sidewall of the storage-node junction.

3. **Depth is set by the buried word line.** The cell trench must reach below the word line's saddle-fin bottom in the isolation (180 nm) with oxide margin: at least 220 nm, 250 nm target.

4. **The sidewall angle is a transistor parameter.** W(z) = W_t + 2z tan α. At 1°, the fin is 18.9 nm wide at word-line depth and the trench bottom is 9.3 nm wide.

5. **The structure is extreme.** A 13.9:1 trench (16.6:1 with the mask) between fins with a height-to-width ratio near 18, and these ratios rise every generation.

6. **Retention depends on the sidewall.** A tail cell may leak only about 28 fA, and the defects that cause tail leakage often sit on the surfaces the etch creates.

---

## Study Questions

1. A cell has C_s = 7 fF and V_DD = 1.05 V, with the plate at V_DD/2. The sense margin allows a 35% loss of signal. Compute the stored charge in electrons and the maximum average leakage for a 32 ms refresh interval.

2. A 6F² layout has F = 15 nm and AA lines tilted 22° from the bit-line direction, with three word-line crossings per AA period. Compute the word-line pitch, the crossing spacing along the AA, the AA period, and the AA pitch normal to the line that gives 12F² per island.

3. The buried word line in a new node has its bottom at 130 nm in the AA and 175 nm in the isolation, and the required oxide margin is 35 nm. The 3σ depth variation is ±18 nm. Compute the minimum depth and a reasonable target.

4. For the reference AA (W_t = 14 nm, S_t = 18 nm), compute W(140), W(180), and the trench bottom width at 250 nm for sidewall angles of 0.6°, 1.0°, and 1.4°. At what angle does the trench close at 250 nm?

5. A process change narrows the AA top width from 14 nm to 13 nm with no change in angle. By what percentage does the fin height-to-width ratio at the top change? Which customers in Section 1.6.3 are affected, and how?

---

**Next Chapter:** [Chapter 2: Active-Area Patterning — SAQP Lines, Cuts & the Hard-Mask Stack](./02-aa-patterning-hardmask.md)

---

**Chapter 1 Development Status:** Complete  
**Version:** 1.0
