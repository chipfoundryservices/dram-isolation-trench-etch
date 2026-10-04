# Chapter 10: Profile Control — Taper, Bottom Shape, Corner Rounding & AA Width

## Overview

The isolation profile is the shape of the silicon fin, read from the top of the island to the bottom of the trench. Every depth has a customer. The top sets the contact landing area. Just below the top, a bow narrows the island where the storage-node junction sits. The word-line depth sets the saddle-fin width. The bottom sets whether the trench can be filled and how stiff the fin is. A recipe that improves one depth usually changes the others.

This chapter treats the profile depth by depth. It develops the sidewall-angle budget and the closure of narrow trenches, explains bottom shapes and how to control them, covers the top corner and the bow beneath it, and assembles the AA width at every depth into a single picture. It ends with a lever-response matrix and a strategy for fixing each feature at the right step of the recipe.

**Learning Objectives:**
- Compute the AA width and trench width at any depth from the top width and sidewall angle
- Derive the maximum sidewall angle from the fill limit, including pitch walk
- Explain how taper and ARDE interact to produce V-shaped, self-limited bottoms
- Describe microtrenching, bottom rounding, and the profile step that controls them
- Compute bow depth from mask facet angle and estimate its effect on the island top
- Use a lever-response matrix to choose recipe changes
- Explain why bow is fixed early and bottom width is fixed late

---

## 10.1 The Profile, Depth by Depth

```
Reference AA profile (S_t = 18 nm, W_t = 14 nm, α = 1.0°):

  Depth (nm)   AA width (nm)   Trench width (nm)   Customer
  ────────────────────────────────────────────────────────────────────────
  0            14.0            18.0                BC/DC contacts
  20–40        14.0–14.5       —                   SN junction (bow zone)
  140          18.9            13.1                WL bottom on AA
  180          20.3            11.7                WL bottom in isolation
                                                   (saddle-fin base)
  250          22.7            9.3                 Fill; fin stiffness

W(z) = W_t + 2 z tan α          S(z) = S_t − 2 z tan α
```

A real profile is not a single straight line. It has a slightly different angle in each recipe step, a small bow just under the mask, and a rounded bottom. The straight-line model is still the right starting point, because the deviations are a few tenths of a nanometre per side and the angle term is several nanometres.

---

## 10.2 The Sidewall-Angle Budget

### 10.2.1 Closure Depth

A tapered trench closes at the depth where its two walls meet:

```
z_close = S_t / (2 tan α)

  α        z_close (S_t = 18)    Bottom width at 250 nm
  ────────────────────────────────────────────────────────
  0.5°     1031 nm               13.6 nm
  1.0°     516 nm                9.3 nm
  1.25°    413 nm                7.1 nm
  1.5°     344 nm                4.9 nm
  2.0°     258 nm                0.5 nm
```

### 10.2.2 The Fill Limit

The cell trench is filled by ALD oxide (sometimes with a nitride liner first) that grows conformally from both walls. A bottom narrower than about 7 nm, after the liner oxidation has consumed silicon from each wall, leaves too little room for the liner stack and risks a seam or void at the bottom.

```
Fill limit: S(250) ≥ 7 nm

  For the nominal space (S_t = 18):  tan α ≤ (18 − 7) / 500 → α ≤ 1.26°

With pitch walk, the narrowest space sets the limit:
  γ = 16 nm (2 nm range):  tan α ≤ (16 − 7) / 500 → α ≤ 1.03°
  γ = 15 nm (Ch. 2 example): tan α ≤ 8 / 500     → α ≤ 0.92°
```

**Pitch walk spends angle budget.** With a 2 nm space range, the reference angle of 1.0° is already at the limit for the narrowest space. This is one reason the pitch-walk specification (Chapter 2) is as tight as it is.

### 10.2.3 The Word-Line Limit

From below, the angle is limited by the saddle-fin width:

```
W(140) tolerance: ± 1.5 nm (3σ) around 18.9 nm
  ∂W(140)/∂α = 2 × 140 × (π/180) ≈ 4.9 nm per degree
  → angle window from W(140) alone: 1.0° ± 0.31°

Combined window (fill above, word line below): 0.7° – 1.25°
  (narrower if pitch walk or W_t variation use part of the budget)
```

### 10.2.4 Taper and ARDE Together

Taper narrows the trench as it deepens, which raises the aspect ratio faster than the depth alone and slows the etch further. With the narrowing included in the ARDE model (Appendix E.2, k refitted to 0.021 so that the reference trench still reaches 250 nm in 62.1 s):

```
Depth at 62.1 s and bottom width (taper-coupled ARDE):

  Angle   S_t = 15 nm          S_t = 16 nm          S_t = 18 nm          S_t = 20 nm
  ────────────────────────────────────────────────────────────────────────────────────────
  0.7°    243 nm / 9.1 nm      247 / 10.0           252 / 11.8           257 / 13.7
  1.0°    241 / 6.6            244 / 7.5            250 / 9.3            255 / 11.1
  1.25°   238 / 4.6            242 / 5.5            248 / 7.2            253 / 8.9
  1.5°    235 / 2.7            239 / 3.5            246 / 5.1            251 / 6.8
  2.0°    211 / closed         225 / closed         241 / 1.2            247 / 2.7
```

Two effects stand out. First, a narrower space is both shallower (ARDE) and narrower at its bottom (taper), so pitch walk hurts twice. Second, at 2° the narrowest spaces close before the end of the etch, and their depth becomes **self-limited**: once the passivated walls meet, the etch stops, no matter how long the recipe runs. A self-limited trench is a V with a depth set by its top width and angle, not by time.

---

## 10.3 Bottom Shape

### 10.3.1 Three Shapes

```
          V-bottom                Rounded               Flat + microtrench
          (narrow, tapered)       (target, cell)        (wide, periphery)

           │       │              │       │             │               │
            \     /               │       │             │               │
             \   /                 \     /              │╲             ╱│
              \ /                   ╲___╱               │ ╲___________╱ │
               V                                         ↑ microtrenches ↑
```

### 10.3.2 Microtrenching

In wide trenches, ions that strike the lower sidewalls at grazing angles reflect toward the bottom corners (Chapter 3). The corners receive extra ion flux and etch faster than the center, leaving narrow grooves:

```
Microtrench depth (illustrative): 5–15 nm in a 100 nm periphery trench
  More with: higher ion energy, wider angular spread, steeper walls,
             less passivation at the bottom corners
  Less with: some taper (reflected ions land on the wall, not the
             corner), more bottom passivation, lower energy at the end

Why it matters:
  - Sharp corners concentrate stress after fill and oxidation → defects
    (dislocations) that leak
  - Thin liner oxide at the sharp corner → field enhancement
  - Fill voids in the groove
```

The cell trenches rarely microtrench, because their bottoms are narrow and tapered. Microtrenching is mainly a periphery concern.

### 10.3.3 The Profile Step

The reference profile step (Chapter 7) runs for 6 s at low bias (≈ 60 eV), no oxygen, and high helium dilution:

```
Effect on the cell trench:   rounds the V; ≈ 5 nm more depth;
                             no change in W(140) (above the bottom)
Effect on the periphery:     softens microtrench corners (corner radius
                             from ≈ 2 nm to ≈ 8–10 nm); ≈ 5 nm more depth
Damage:                      low (60 eV), confined to the bottom
```

A longer or more energetic profile step would round more but would also start to etch the lower sidewalls and change the bottom width. The profile step is tuned on the periphery, where the corners are sharpest, and checked on the cell, where the bottom width is critical.

---

## 10.4 The Top of the Island

### 10.4.1 Etch Bias at the Surface

```
Etch bias at the top:  ΔW_t = W_Si,top − W_mask,bottom

Contributions (illustrative, per side):
  Sidewall film forming at the mask edge          +0.2 nm  (wider AA)
  Lateral etch in the Cl₂-rich ME-1 early seconds −0.1 nm
  Fluorine from the breakthrough (first seconds)  −0.1 nm
  Net                                             ≈ 0 nm per side

Target: W_t = W_mask,bottom ± 0.2 nm per side
```

The reference recipe is tuned for zero net bias at the top. A positive bias would widen the island and narrow the space, raising ARDE. A negative bias would narrow the island and its contact landing.

### 10.4.2 Mask Facets and Bow

As the 14 nm mask lines facet (Chapter 4), ions reflect from the facets into the trench. A vertical ion striking a facet inclined at φ_f to the horizontal leaves at 2φ_f from vertical and crosses the trench to strike the opposite wall:

```
Depth below the facet where reflected ions strike the opposite wall:
  z_hit ≈ S / tan(2 φ_f)

  φ_f      2φ_f     z_hit (S = 18 nm)
  ─────────────────────────────────────
  10°      20°      49 nm
  15°      30°      31 nm
  25°      50°      15 nm
  45°      90°      0 (horizontal; hits at the facet level)
```

With the facet bottom at the top of the 49 nm mask, the reflected ions land on the silicon within roughly 0–50 nm of the silicon surface. That is where a small **bow** forms: a local widening of the trench, and so a local narrowing of the island, just under the surface.

```
Reference bow (illustrative): 0.3–0.6 nm per side at 20–40 nm depth
  AA width at 30 nm: 15.0 − 2 × 0.45 ≈ 14.1 nm (vs. 15.0 nm without bow)

Why it matters in DRAM:
  The storage-node junction sits in the top 30–80 nm of the island end.
  A narrowed island there concentrates the junction field (GIDL) and
  reduces the silicon volume under the storage-node contact.
```

Bow is controlled by keeping facets small (low ion energy, pulsing, enough cap), by adequate passivation in ME-1 just below the mask, and by low pressure in ME-1 to reduce off-angle ions.

### 10.4.3 Top-Corner Rounding

The top corner of the island (where the trench wall meets the silicon surface under the pad oxide) should be slightly rounded after the liner oxidation. A sharp corner gives a thin liner oxide at the corner, a stress concentration, and later a divot in the fill oxide where the pad oxide and nitride are stripped. Rounding comes from three sources:

```
Source                                 Typical contribution
──────────────────────────────────────────────────────────────────
Breakthrough / early ME-1 (slight      0.5–1 nm radius
lateral attack under the pad oxide)
Post-etch HF clean (pad-oxide          Sets the corner exposed to
pull-back)                             oxidation; ≤ 1–2 nm pull-back
Liner oxidation (convex-corner         Rounds to 2–3 nm radius
oxidation rounding)
```

Too much rounding costs the top AA width that the contacts need. The reference target is a 2–3 nm radius after the liner.

---

## 10.5 AA Width at Every Depth

### 10.5.1 Sensitivities

```
Sensitivity of AA width to profile parameters:

  ∂W(z) / ∂W_t   = 1
  ∂W(z) / ∂α     = 2 z (π/180) nm per degree
                   z = 140: 4.9 nm/°;  z = 180: 6.3 nm/°;  z = 250: 8.7 nm/°

Example: W_t +0.4 nm (mask CD), α −0.1° (warmer chuck):
  W(0)   = +0.40 nm
  W(140) = +0.40 − 0.49 = −0.09 nm
  W(250) = +0.40 − 0.87 = −0.47 nm
```

Errors in top width and angle can cancel at one depth and add at another. A recipe adjustment that restores W(140) after a mask CD change will change W(0) and W(250) in opposite directions. **The width must be measured at more than one depth** (Chapter 15).

### 10.5.2 The Saddle Fin

```
Saddle fin under the word line (reference):
  Height h_sf = 40 nm (from 140 to 180 nm)
  Width at its top W(140) = 18.9 nm, at its base W(180) = 20.3 nm
  Gate perimeter around the fin ≈ W(140) + 2 √(h_sf² + (ΔW/2)²)
                                  ≈ 18.9 + 2 × 40.0 ≈ 99 nm
```

The fin width does not change the gate perimeter much (most of it is the two sidewalls), but it changes how well the gate controls the fin body. A thinner fin is controlled more completely, with a lower subthreshold slope and lower off-state leakage; a thicker fin has a higher threshold-voltage variability and leaks more when off. Since the access transistor's off-state leakage contributes directly to the retention budget (Chapter 1), W(140–180) is a retention parameter as well as a drive parameter.

### 10.5.3 Step Marks

The ME-1 → ME-2 boundary at about 120 nm can leave a small angle change or notch. Section 7.3 explained why it is placed above the word-line region. If the boundary drifts deeper (longer ME-1, faster rate), the mark can move into the saddle-fin region. Depth-series and cross-section checks after any recipe change confirm where the mark sits.

---

## 10.6 Lever-Response Matrix

```
Lever (increase)       W_t    Bow    α      W(140)   S(250)   Cell D   Peri D   Microtr.
─────────────────────────────────────────────────────────────────────────────────────────────
O₂ in ME-2             0      0      ↑↑     ↑↑       ↓↓       ↓        ↓        ↓
NF₃ in ME-2            0      0      ↓      ↓        ↑        ↑        ↑        ↑
Cl₂ in ME-1            ↓      ↑      ↓      ↓        ↑        ↑        ↑        ↑
Bias power (ME-1)      ↓      ↑      ↓      ↓        ↑        ↑        ↑        ↑↑
Bias power (ME-2)      0      0      ↓      ↓        ↑        ↑        ↑        ↑↑
Duty cycle             0      ↑      ↓      ↓        ↑        ↑        ↑↑       ↑
ME-2 pressure          0      0      ↑      ↑        ↓        ↑ (k↓)   ↓        ↓
Wafer temperature      ↓      ↑      ↓      ↓        ↑        ↑        ↑        —
Total flow             0      ↑      ↓      ↓        ↑        ↑        ↑        —
Profile-step time      0      0      0      0        ↑ (round) ↑       ↑        ↓↓
ME-1 time (fixed ME-2) ↓      ↑      ↓      ↓ (if    ↑        ↑        ↑        ↑
                                            mark at
                                            depth)

↑ / ↓ : increase / decrease; double arrows: strong; 0: negligible
(illustrative; signs typical of HBr/O₂-based trench etch)
```

### 10.6.1 Fix Bow Early, Bottom Late

The matrix shows why the reference recipe is split. Bow and top width are set in the first 30–50 nm, by ME-1 and the facet state of the mask. Bottom width and microtrenching are set in the last 50 nm, by ME-2 and the profile step. Levers applied to the whole recipe move both ends at once. Levers applied to one step move mainly its own depth range. **Fix the top in ME-1, the word-line region in ME-2's first half, and the bottom in ME-2's end and the profile step.**

---

## 10.7 Summary & Key Takeaways

1. **The profile is the transistor.** AA width at the top, at 140–180 nm, and at the bottom serve contacts, the saddle-fin word line, and fill and stiffness.

2. **The angle window is narrow.** Fill requires S(250) ≥ 7 nm; the word line requires W(140) within ±1.5 nm. Together: 0.7–1.25°, narrower with pitch walk.

3. **Narrow spaces suffer twice.** They etch shallower (ARDE) and close faster (taper). At 2°, the narrowest spaces self-limit before the target depth.

4. **Bottom shape is a periphery problem and a cell problem.** Periphery trenches microtrench; cell trenches V. The low-energy profile step rounds both.

5. **Facets make a bow where the junction sits.** Reflected ions strike within about 50 nm of the silicon surface, narrowing the island under the storage-node contact.

6. **Measure width at several depths.** Top width and angle errors can cancel at one depth and add at another.

7. **Fix each depth in its own step.** Top in ME-1, word-line region in early ME-2, bottom at the end.

---

## Study Questions

1. Compute W(140), W(180), and S(250) for W_t = 13.5 nm, S_t = 18.5 nm, and α = 1.15°. Is the profile inside the specification of Chapter 1?

2. A pitch-walked array has spaces of 16.5, 18, 19.5, and 18 nm. Using the fill limit S(250) ≥ 7 nm, compute the maximum angle. Using the taper-coupled ARDE table, estimate the depth of the narrowest space at 1.0°.

3. Mask facets in a new recipe reach φ_f = 12°. Compute where reflected ions strike the opposite wall in an 18 nm space. What would you change in ME-1 to reduce the resulting bow, and what would that change do to W_t?

4. A mask CD change widens W_t by 0.6 nm. What angle change would hold W(140) constant? What would that angle change do to W(250) and S(250)?

5. Periphery trenches show 12 nm microtrenches, and the cell bottoms are within specification. Using the lever-response matrix, choose two changes that reduce microtrenching with the least effect on cell W(140). Explain your choice.

6. Explain why a self-limited V-bottom makes the narrowest spaces insensitive to etch time, and why that is not a good way to control depth.

---

**Next Chapter:** [Chapter 11: Fin Bending, Leaning & Pattern Collapse](./11-fin-bending-collapse.md)

---

**Chapter 10 Development Status:** Complete  
**Version:** 1.0
