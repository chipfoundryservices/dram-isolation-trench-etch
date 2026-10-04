# Chapter 11: Fin Bending, Leaning & Pattern Collapse

## Overview

When the isolation etch ends, the wafer carries billions of free-standing silicon walls 250 nm tall and 14–23 nm wide, separated by 18 nm gaps. In vacuum they stand straight. Within minutes they will be immersed in cleaning chemistry, rinsed in water, and dried, and within hours they will be oxidized and buried in fill oxide. Each of these steps pushes them sideways. If two neighbors touch, they usually stay stuck together, and the two islands become one electrical node: a bridge that fails both cells.

Collapse and leaning are not etch defects in the narrow sense, but the etch decides how much margin the fins have. Their height, their width at the root, the uniformity of the spaces between them, and the symmetry of their surfaces all come from the isolation etch. This chapter treats the fin as a mechanical structure, computes its stability against capillary collapse, examines the other forces that bend it, and lays out the design and process remedies.

**Learning Objectives:**
- Compute the bending stiffness of a tapered silicon fin and its equivalent uniform width
- Derive the capillary-collapse stability criterion and the critical fin height
- Compute collapse margins for water and low-surface-tension drying
- Estimate deflection from pitch-walk asymmetry and its amplification near instability
- Explain bending from asymmetric surface stress, array-edge drying, and fill
- Choose design, etch, and clean remedies and quantify their effect

---

## 11.1 The Fin as a Cantilever

### 11.1.1 Geometry

```
One island in cross-section across the AA line (the bending direction):

         W_t = 14 nm
         ┌──┐           top: free (mask still on it)
         │  │
         │  │  H = 250 nm
        ╱    ╲
       ╱      ╲
      └────────┘        root: W_b = 22.7 nm, fixed in the substrate
      ← s = 18 nm →      neighbor on each side at s (top)

Island length L_AA = 84 nm (bending stiffness and loads both scale
with length, so L cancels in the stability criterion)
```

The fin bends most easily across its narrow dimension, toward one of its neighbors. Its stiffness in that direction scales with the cube of the width, so the wide root dominates.

### 11.1.2 Equivalent Uniform Width

For a cantilever whose width tapers linearly from W_b at the root to W_t at the tip, the tip deflection under a uniform lateral load can be matched by a uniform beam of width w_eff:

```
Numerical integration of the tapered beam (Appendix E.5):

  Angle    W_b (nm)    w_eff (nm)
  ─────────────────────────────────
  0.7°     20.1        18.8
  1.0°     22.7        20.8     (reference)
  1.25°    24.9        22.4

Uniform-beam stiffness against a uniform load q (per unit height):
  tip deflection δ = q H⁴ / (8 E I),  I = L w_eff³ / 12

  E (Si, in-plane, ⟨110⟩) ≈ 169 GPa
```

The reference fin behaves like a uniform 20.8 nm wall. **Taper is stiffness**: each 0.25° of angle adds about 1.6–2 nm of equivalent width and roughly 25% of stiffness. This puts the profile in direct tension with the fill limit of Chapter 10, which wants less taper.

---

## 11.2 Capillary Collapse

### 11.2.1 The Load

When a liquid partly fills the spaces during drying, the meniscus in each space has a curvature set by the gap and the contact angle. The pressure inside the liquid is below the vapour pressure by the Laplace pressure:

```
Δp = 2 γ cos θ / s          (cylindrical meniscus in a long slot of
                             width s; acts on both walls of the slot)

Water (γ = 0.072 N/m), hydrophilic surface (cos θ ≈ 1), s = 18 nm:
  Δp = 2 × 0.072 / 18×10⁻⁹ = 8.0×10⁶ Pa = 8 MPa
```

In a perfectly periodic array, every fin has the same pressure on both sides, and the net force is zero. The danger is that the balance is **unstable**: if a fin deflects slightly toward one neighbor, that space narrows, its Laplace pressure rises, and the fin is pulled further.

### 11.2.2 The Stability Criterion

```
A fin with spaces s₁ and s₂ on its two sides feels a net pressure
  Δp_net = 2 γ cos θ (1/s₁ − 1/s₂)
Linearizing about the undeflected state (s₁ = s − δ, s₂ = s + δ, with
the neighbors held in place), the destabilizing load per unit deflection
is:

  d(Δp_net)/dδ ≈ 4 γ cos θ / s²

The deflection-dependent load acts like a negative elastic foundation
on a clamped-free beam. Its first buckling eigenvalue gives the
stability condition:

  1.03 E w_eff³ / H⁴  >  4 γ cos θ / s²

  Margin M = (1.03 E w_eff³ / H⁴) / (4 γ cos θ / s²)
  Stable if M > 1

Critical height: H_c = [ 1.03 E w_eff³ s² / (4 γ cos θ) ]^(1/4)

If neighboring fins move in opposite directions at the same time (the
alternating "pairing" mode of an infinite array), the load per unit
deflection doubles again. In practice the drying front passes through
neighboring spaces at slightly different times, and the single-fin
criterion above is the usual working estimate, calibrated against
collapse-test structures (Appendix C).
```

### 11.2.3 Margins for the Reference Fin

```
Reference: H = 250 nm, s = 18 nm, E = 169 GPa

  w_eff     Liquid / surface               Margin M     H_c
  ──────────────────────────────────────────────────────────────
  18.8 nm   Water, hydrophilic             0.33         190 nm
  (0.7°)    IPA (γ = 0.022), wetting       1.09         255 nm
  20.8 nm   Water, hydrophilic             0.45         205 nm
  (1.0°)    IPA, wetting                   1.48         276 nm
            Water, hydrophobic (cos θ≈0.3) 1.50         277 nm
  22.4 nm   Water, hydrophilic             0.56         217 nm
  (1.25°)   IPA, wetting                   1.84         291 nm
```

Three conclusions follow:

```
1. The reference fin cannot be dried from water on a hydrophilic
   surface: M = 0.45. It would collapse.

2. Replacing the final rinse liquid with IPA (or another low-surface-
   tension liquid) before drying gives a margin of about 1.5: stable,
   but thin, so any asymmetry is strongly amplified (Section 11.3).

3. A hydrophobic surface (for example, hydrogen-terminated silicon
   after an HF-last clean) lowers the capillary force as much as IPA
   does, but the oxide mask on top stays hydrophilic, and hydrophobic
   surfaces are prone to watermarks and particle deposition.
```

The critical height for water drying, 205 nm, is well below the 250 nm trench, and even with IPA the critical height (276 nm) is only 10% above it. **The DRAM isolation fin is beyond the capillary limit of water and close to the limit of IPA.** This is why every DRAM maker uses low-surface-tension drying (IPA vapour, Marangoni drying, or similar) after the post-etch clean, why asymmetries are controlled so tightly, and why the trench depth cannot simply be increased.

### 11.2.4 Why Touching Is Permanent

Once two fins touch, adhesion between their surfaces (van der Waals forces, and hydrogen bonding between hydroxylated oxide surfaces) usually exceeds the elastic energy that would spring them apart:

```
Elastic energy per unit length of a fin bent by s/2 = 9 nm at its tip
(each fin of a collapsed pair moves halfway):
  Tip stiffness per unit length: k' = 3 E I' / H³,  I' = w_eff³ / 12
    = 3 × 169×10⁹ × 7.5×10⁻²⁵ / (250×10⁻⁹)³ ≈ 2.4×10⁷ N/m per m
  U_el = ½ k' δ² = ½ × 2.4×10⁷ × (9×10⁻⁹)² ≈ 1.0×10⁻⁹ J/m

Adhesion energy per unit length over a contact band of height h_c,
with work of adhesion W_a ≈ 0.05–0.1 J/m²:
  U_ad = W_a h_c
  U_ad > U_el when h_c > 1.0×10⁻⁹ / W_a ≈ 10–20 nm

A contact band only 10–20 nm tall, out of 250 nm, holds the pair
together; as the last liquid leaves, the band grows
```

Collapsed pairs rarely recover. They become **AA bridges** in the oxidation that follows, and the two islands share a body and leakage path.

---

## 11.3 Deflection From Asymmetry

### 11.3.1 Pitch Walk

With pitch walk (Chapter 2), a fin has different spaces on its two sides, and the capillary pressures do not cancel even when the fin is straight:

```
Spaces 16 nm and 20 nm on either side (4 nm space range):
  Δp_net = 2 γ cos θ (1/16 nm − 1/20 nm) = 2 γ cos θ × 1.25×10⁷ m⁻¹

  Water: Δp_net = 1.80 MPa
  IPA:   Δp_net = 0.55 MPa

Initial (linear) deflection of the reference fin (w_eff = 20.8 nm),
uniform load over the height:
  δ₀ = 1.5 Δp_net H⁴ / (E w_eff³)
  Water: δ₀ ≈ 6.9 nm (and M < 1: collapses anyway)
  IPA:   δ₀ ≈ 2.1 nm

Amplification near instability: δ = δ₀ / (1 − 1/M)
  IPA, M = 1.48: δ ≈ 2.1 / (1 − 0.68) ≈ 6.6 nm, toward the narrow space

Spaces 17 nm and 19 nm (2 nm range, the patterning specification):
  IPA: δ₀ ≈ 1.0 nm → δ ≈ 3.3 nm
```

With a 4 nm space range, the fin leans 6.6 nm into a 16 nm space and leaves less than 10 nm at the top. With the 2 nm range of the patterning specification (Chapter 2), the lean is about 3.3 nm. **Near the stability limit, pitch walk is amplified threefold into lean.** This, more than depth walk, is often what sets the pitch-walk specification.

### 11.3.2 The Array Edge

The last active line in an array has the dense array on one side and a wide space or open area on the other. During drying, the wide side drains first, and the meniscus remains only in the narrow space:

```
One-sided Laplace pressure on the last line:
  Δp = 2 γ cos θ / s
  Water: 2 × 0.072 / 18×10⁻⁹ = 8.0 MPa → δ₀ ≈ 31 nm (collapse)
  IPA:   2 × 0.022 / 18×10⁻⁹ = 2.4 MPa → δ₀ ≈ 9.4 nm (over half of an
                                          18 nm space, before
                                          amplification: collapse)
```

Even with IPA, the last line is pulled into its neighbor. **This is the main reason the array ends in dummy lines**: two to six lines that are allowed to lean, and that shield the first active line from the one-sided load (Chapter 2).

### 11.3.3 Asymmetric Surface Stress

The plasma modifies a thin surface layer of the sidewall (bromine and hydrogen incorporation, damage, the SiOₓBrᵧ film). If the two sidewalls of a fin are modified differently, their surface stresses differ, and the fin bends like a bimorph:

```
Curvature from a surface-stress difference Δf (N/m):
  κ ≈ 6 Δf / (E w²)
Tip deflection: δ ≈ κ H² / 2

  Δf = 0.2 N/m:  δ ≈ 0.5 nm
  Δf = 0.5 N/m:  δ ≈ 1.3 nm
  (w = 20.8 nm, H = 250 nm)
```

Differences of this size arise where the two sidewalls see different ion flux or passivation: at array edges, next to pitch-walked spaces (Chapter 3), and at the wafer edge where the trench is tilted (Chapter 9). The resulting lean is small, but it is present before drying and adds to the capillary deflection.

### 11.3.4 Fill and Anneal

After liner oxidation, the trenches are filled. Flowable and spin-on oxides shrink as they cure and densify. In the dense array, the fill is usually ALD oxide, which shrinks little. In wide spaces at the array edge and in the periphery, flowable oxide shrinks more. A fin with ALD-filled narrow space on one side and flowable-filled wide space on the other is pulled toward the wide side as the flowable oxide densifies.

```
Observed lean of edge lines after fill and anneal: 1–5 nm (illustrative),
toward the wide space. Once the fill is rigid, the fin cannot collapse,
but the lean moves the top of the island relative to the contacts that
land on it later.
```

---

## 11.4 Wiggling

Long lines patterned under a stressed hard mask can buckle in plane into a wavy shape. In DRAM AA patterning, the risk is in the patterning stack above the hard mask (thick carbon layers with high stress; Book #19), where 14 nm lines stand tall during the SAQP transfer. Once the lines are cut into 84 nm islands, in-plane buckling of the silicon is no longer possible: the islands are too short. Wiggle from the patterning stack, however, is transferred into the islands as placement error and space-width variation, which then feeds ARDE and capillary asymmetry.

---

## 11.5 Remedies

### 11.5.1 Design

```
Remedy                           Effect                                   Cost
───────────────────────────────────────────────────────────────────────────────────────
Dummy AA lines at array edges    Shield active lines from one-sided       Area (2–6 lines
(2–6)                            drying and fill loads                    per edge)
Wider AA (W_t +1 nm)             w_eff +1 nm → stiffness +15%             Pitch, or narrower
                                                                          spaces (ARDE, fill)
Shallower isolation              H⁴ scaling: −20 nm → stiffness +40%      Isolation margin
                                                                          under the WL
Shorter islands or supports      Little effect on the bending criterion   —
                                 (L cancels)
```

### 11.5.2 Etch

```
Remedy                           Effect                                   Cost
───────────────────────────────────────────────────────────────────────────────────────
More taper (1.0° → 1.25°)        w_eff 20.8 → 22.4 nm: margin ×1.25       Bottom width 9.3 →
                                                                          7.1 nm (fill limit)
Pitch-walk-insensitive etch      Less depth walk; less fill asymmetry     Requires low k
(low k, Chapter 12)
Symmetric sidewall treatment     Less surface-stress bending              Pulsing; dummy
(pulsing for charge relief)                                               symmetry
Depth control (no overshoot)     Each 10 nm extra depth: −15% margin      APC (Chapter 15)
```

### 11.5.3 Clean and Dry

```
Remedy                           Effect (relative to water, hydrophilic)
─────────────────────────────────────────────────────────────────────────
IPA replacement before drying    Capillary load × 0.31 → margin × 3.3
Marangoni / IPA-vapour drying    Similar; meniscus moves slowly and evenly
Hydrophobic final surface        Capillary load × cos θ (≈ 0.2–0.4); risk
(HF-last)                        of watermarks, particles
Surfactant rinse                 Lowers γ and modifies cos θ
Supercritical CO₂ drying         No meniscus → no capillary load; cost,
                                 throughput, chemistry compatibility
Avoid wet clean before liner     Plasma or vapour-phase removal of the
(dry-only post-etch treatment)   passivation film; no liquid at all
```

### 11.5.4 Process Order

The fins are most vulnerable between the end of the etch and the moment the fill makes them rigid. Every wet step in that window carries collapse risk. Flows that minimize the number of wet steps, or that place the first liner deposition before any wet clean, reduce exposure. The trade-off is that the passivation film and etch residue must then be removed without liquid, which shifts the burden to the liner oxidation and dry cleans (Chapter 13).

---

## 11.6 Detection

```
Method                              What it sees                         When
──────────────────────────────────────────────────────────────────────────────────────
Top-down CD-SEM, pattern-matched    Lean (top offset), collapsed pairs,  After clean / dry;
                                    space asymmetry                      after fill
E-beam inspection (voltage          Bridged AAs (shared node) in large   After liner or fill
contrast)                           areas; ppm-level collapse density
Optical broadband inspection        Collapse clusters; array-edge lean   After clean / dry
Electrical (bit-fail maps)          Paired-bit failures in adjacent      Probe
                                    AAs; cluster signatures
```

Collapse density is usually specified in parts per million of islands or as clusters per wafer. Because each collapsed pair kills two or four cells, and because collapse clusters can exceed what redundancy can repair, the specification is far tighter than the raw bit count suggests.

---

## 11.7 Summary & Key Takeaways

1. **The fin is a tapered cantilever.** The reference fin behaves like a uniform 20.8 nm wall 250 nm tall. Stiffness scales as w_eff³/H⁴.

2. **Water drying collapses the reference fin.** The margin is 0.45, and the critical height (205 nm) is well below the trench depth. IPA drying gives a margin of about 1.5, with a critical height only 10% above the trench.

3. **Collapse is permanent.** Adhesion between touching surfaces exceeds the restoring force, and collapsed pairs become AA bridges.

4. **Asymmetry is amplified into lean.** Near the stability limit, a 2 nm space range leans the fin about 3.3 nm under IPA, and a 4 nm range about 6.6 nm. The last array line sees a one-sided load of 2.4 MPa even with IPA and collapses without dummies.

5. **Dummy lines are mechanical, not just optical.** They absorb the one-sided drying and fill loads at the array edge.

6. **Taper buys stiffness and costs fill.** Going from 1.0° to 1.25° raises the margin by 25% but narrows the bottom from 9.3 to 7.1 nm. Depth costs 15% of margin per 10 nm.

---

## Study Questions

1. Compute the collapse margin and critical height for a fin with w_eff = 19.5 nm, H = 260 nm, s = 17 nm, dried from IPA (γ = 0.022 N/m, cos θ = 1).

2. A new node shrinks the pitch to 28 nm with W_t = 12 nm and S_t = 16 nm, and the trench depth stays at 250 nm. Assuming w_eff scales with W_t (w_eff ≈ 1.49 W_t at 1.0°), compute the IPA margin. What depth would restore the reference margin of 1.48?

3. For the reference fin dried with IPA, compute the deflection caused by spaces of 17 nm and 19 nm on either side, including amplification. Repeat for 15 nm and 21 nm.

4. A wafer shows lean of 2–3 nm only in the outermost 3 mm, toward the wafer center. Using Chapters 9 and 11, propose two mechanisms and a measurement that distinguishes them.

5. Compare the effect on collapse margin of (a) increasing the angle from 1.0° to 1.25°, (b) reducing the depth from 250 nm to 235 nm, and (c) switching from IPA to a hydrophobic HF-last water rinse (cos θ = 0.3). Which has the fewest side effects, and why?

6. Explain why island length cancels from the capillary stability criterion. Under what conditions would island ends (the 84 nm length) matter for collapse?

---

**Next Chapter:** [Chapter 12: Depth Loading — Cell Versus Periphery, Pitch Walk & Island Ends](./12-depth-loading-cell-peri.md)

---

**Chapter 11 Development Status:** Complete  
**Version:** 1.0
