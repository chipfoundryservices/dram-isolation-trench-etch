# Appendix E: Trench Geometry, Transport & Mechanical Calculations

The formulas used in this book, collected with their assumptions and worked reference values. Symbols follow the chapters. Lengths in nm unless noted.

---

## E.1 Geometry

### E.1.1 Cell Layout

```
6F² cell: WL pitch = 2F, BL pitch = 3F, cell area = 6F²
WL crossing spacing along an AA tilted φ from the BL direction:
  d = WL pitch / cos φ
AA period along the line (three crossings): 3d
Island area: P × 3d = 12F²   (two cells per island)

Reference: F = 17, φ = 20°, P = 32 → d = 36.2, period = 108.5,
           P × period = 3472 ≈ 12F² = 3468 nm²
```

### E.1.2 Profile

```
W(z) = W_t + 2 z tan α          AA width at depth z
S(z) = S_t − 2 z tan α          trench width at depth z
z_close = S_t / (2 tan α)       closure depth of a tapered trench
α_max(fill) = atan[(S_t − S_min) / (2D)]

Reference: W(140) = 18.9, W(180) = 20.3, W(250) = 22.7, S(250) = 9.3
```

### E.1.3 Aspect Ratios

```
A_Si = D / S_t                      silicon only (13.9)
A_tot = (D + h_m) / S_t             with mask (16.6)
Fin ratio = H / W_t                 (17.9 top; 11.0 at the base)
```

### E.1.4 Patterning

```
SAQP spaces:  α = t₁;  β = M − 2t₂;  γ = P₁ − M − 2t₁ − 2t₂
Cut window:   W_t + 2 OL ≤ w_c ≤ W_t + 2 S_min − 2 OL
Mask-open taper: S_Si = S_mask,top − 2 h_m tan β
LWR from LER with edge correlation ρ: LWR = LER √(2(1 − ρ))
```

---

## E.2 ARDE and Time to Depth

### E.2.1 Coburn–Winters

```
ER_bottom / ER_open = K / (K + β (1 − K))
K = neutral transmission, β = bottom reaction probability
```

### E.2.2 Linear Form

```
ER / ER₀ = 1 / (1 + k A),  A = (z + h_m) / S
k ≈ β / (ln A + 0.15) ≈ β / 3 for A ≈ 15
```

### E.2.3 Integration

```
dz/dt = ER₀ / (1 + k (z + h_m)/S)

  t(z) = [ z + (k/S)(z²/2 + h_m z) ] / ER₀

Inverse (depth at time t):
  a = k / (2S),  b = 1 + k h_m / S,  c = −ER₀ t
  z(t) = [ −b + √(b² − 4ac) ] / (2a)

Reference check (k = 0.025, S = 18, h_m = 49, ER₀ = 300 nm/min):
  t(250) = [250 + 0.001389 × (31,250 + 12,250)] / 300
         = (250 + 60.4) / 300 = 1.035 min = 62.1 s
```

### E.2.4 Fitting k From a Depth Series

```
For each measured (t, S, z):
  k = [ER₀ t − z] / [(z²/2 + h_m z) / S]

Determine ER₀ from open-area depth (k-independent), then k from the
narrow features; fit all points by least squares.

Example: z = 248 nm at S = 18 nm, t = 1.0 min, open depth 300 nm:
  ER₀ = 300 nm/min; k = (300 − 248) / [(30,752 + 12,152)/18] = 0.022
```

### E.2.5 Taper-Coupled ARDE

```
Use the mean width of the silicon part in the aspect ratio:
  S_mean(z) = S_t − z tan α
  dz/dt = ER₀ / (1 + k (z + h_m) / S_mean(z))
Integrate numerically; stop if S(z) = S_t − 2z tan α reaches ≈ 0
(self-limited V).

Refit k so the reference trench reaches 250 nm at 62.1 s:
  k = 0.021 (α = 1.0°) → ∂D/∂S ≈ 2.75 nm/nm
```

### E.2.6 Macroloading

```
ER₀(f) = ER₀,ref (1 + κ f_ref) / (1 + κ f)       κ ≈ 1.5, f_ref = 0.60
```

---

## E.3 Transport

```
Neutral transmission (diffuse walls):
  K_slot ≈ (ln A + 0.15) / A
  K_hole ≈ 1 / (1 + 0.75 A)

Ion direct transmission across a slot:
  K_i ≈ 1 − 0.80 A σ_θ   (σ_θ in rad)

Mean free path:  λ = kT / (√2 σ p)
Neutral flux:    Γ = n v̄ / 4,   v̄ = √(8kT / πm)
Collisional fraction of the sheath: 1 − exp(−s/λ_i)

Thermal angular spread:  σ_θ ≈ √(kT_i⊥ / (2 e V_sh))
Charging deflection:     θ_defl ≈ q E⊥ L / (2 E_i)
```

---

## E.4 Ion Energy and Pulsing

```
Mean sheath voltage:     ⟨V_sh⟩ ≈ η P_bias / I_i      (η ≈ 0.85)
Bohm speed:              u_B = √(kT_e / M)
Sheath-edge density:     n_s = J_i / (e u_B)
Child-law sheath:        s = (√2/3) λ_D (2V/T_e)^(3/4)
Ion transit time:        τ_i ≈ 3 s / √(2eV/M)
Low-frequency IED:       P(E < E_c) = ½ + arcsin(E_c/e⟨V⟩ − 1)/π
Yield:                   Y = A (√E − √E_th)

Coverage model:
  R = s Γ_n / (Y_d Γ_i)
  θ = R / (1 + R)
  β = s / (1 + R),  k ≈ β / 3

  CW:     R = 2 → β = 0.17 → k ≈ 0.058
  Pulsed: R = 6 → β = 0.071 → k ≈ 0.024
```

---

## E.5 Fin Mechanics

### E.5.1 Tapered-Beam Equivalent Width

```
Width w(x) = W_b − (W_b − W_t) x / H   (x from the root)
Uniform lateral load q per unit height, unit length:
  M(x) = q (H − x)² / 2
  δ_tip = ∫₀ᴴ (H − x) M(x) / (E I(x)) dx,  I(x) = w(x)³ / 12

Equivalent uniform width w_eff from δ_tip = q H⁴ / (8 E w_eff³ / 12):
  w_eff = [12 H⁴ q / (8 E δ_tip)]^(1/3)

Reference (W_t = 14, W_b = 22.7, H = 250): w_eff = 20.8 nm
```

### E.5.2 Capillary Stability

```
Laplace pressure in a slot:     Δp = 2 γ cos θ / s
Net on a fin with spaces s₁, s₂: Δp_net = 2 γ cos θ (1/s₁ − 1/s₂)
Destabilizing stiffness:        κ = 4 γ cos θ / s²   (neighbors fixed)
Clamped-free buckling on a negative foundation:
  κ_cr = 12.36 E I / H⁴ = 1.03 E w³ / H⁴   (per unit length)

Margin:          M = (1.03 E w_eff³ / H⁴) / (4 γ cos θ / s²)
Critical height: H_c = [1.03 E w_eff³ s² / (4 γ cos θ)]^(1/4)

Reference, IPA: M = 1.48, H_c = 276 nm; water: M = 0.45, H_c = 205 nm
```

### E.5.3 Deflection Under Asymmetric Load

```
Uniform load:     δ₀ = 1.5 Δp_net H⁴ / (E w_eff³)
Amplification:    δ = δ₀ / (1 − 1/M)
One-sided load:   Δp = 2 γ cos θ / s (last line, wide side dry)
```

### E.5.4 Surface-Stress Bending and Adhesion

```
Bimorph curvature:   κ ≈ 6 Δf / (E w²);  δ_tip ≈ κ H² / 2
Elastic energy (tip deflection δ):  U_el = ½ (3 E I' / H³) δ²
Adhesion energy:     U_ad = W_a h_c   (sticks if U_ad > U_el)
```

---

## E.6 Edge Tilt and Ring Life

```
θ_e ≈ Δ / (2 s)                     Δ = sheath-edge mismatch
θ(x) ≈ θ_e exp(−x / λ_e)            λ_e ≈ 3 mm
Fin bottom offset:  D tan θ
Ring life (no lift): 2 Δ_allow / wear rate

Reference: Δ = 17 µm → θ_e ≈ 1.0°; at x = 3 mm θ ≈ 0.37°
           Δ_allow = ±14 µm, wear 0.05 µm/RF h → 560 RF h
```

---

## E.7 Junction Leakage

```
SRH single mid-gap trap:   e = σ v_th n_i;  g ≈ e/2;  I = q g
  85 °C: e ≈ 5.3×10³ s⁻¹ → I ≈ 0.4 fA
Field enhancement:         ×10–100 at ≈ 1 MV/cm

Trap count near a junction: N = D_it × ΔE × A_sidewall
  1×10¹⁰ × 0.2 × 3.2×10⁻¹¹ ≈ 0.064

Metal atoms per junction:   N_M = C_surface × A_sidewall

Perimeter–area extraction:  I = J_A A + J_P P
  J_P = (I₂ − I₁) / (P₂ − P₁)  (equal-area diodes)

Retention budget:           I_max = ΔQ_allowed / t_REF
  0.4 × 8 fF × 0.55 V / 64 ms ≈ 28 fA
```

---

## E.8 Thermal

```
Wafer rise above chuck:     ΔT = q R
Wafer time constant:        τ_w = ρ c_p t_w R
  0.41 W/cm² × 1.5 K·cm²/W = 0.6 °C;  τ_w ≈ 0.19 s
```

---

## E.9 Throughput, Window, Control, and Cost

```
Residence time:             τ = p V / Q
Product flow (sccm):        Ṅ_Si / 4.48×10¹⁷
WPH:                        3600 / t_cycle
Chambers:                   (WSPM / 720) / (WPH × availability)

Window (single step):       t ∈ [max(t_cell,min, t_peri,min), min(t_cell,max, t_peri,max)]

EWMA:                       o_{n+1} = λ o_meas + (1 − λ) o_n

Two-knob control:
  [∂D_c/∂t  ∂D_c/∂p] [Δt]   [ΔD_c]
  [∂D_o/∂t  ∂D_o/∂p] [Δp] = [ΔD_o]

Cost per wafer (capital):   C_cap / (years × WPH × availability × 8760)
Killer-defect die loss:     1 − exp(−D₀ A)
```

---

**Appendix E Version:** 1.0
