# Index: Book #26 Navigation Guide

## Quick Navigation

**Total Content:** 16 chapters + 7 appendices + glossary  
**Estimated Read Time:** 22–30 hours for the complete book; 5–10 hours for a focused reading path

| Part | Chapters | Theme |
|------|----------|-------|
| I | 1–4 | Fundamentals: cell architecture, AA patterning and hard mask, sub-20 nm trench physics, chemistry and passivation |
| II | 5–9 | Hardware: ICP reactor, ion energy and pulsing, gas and recipe steps, temperature and ESC, walls, edge and contamination |
| III | 10–14 | Phenomena: profile and AA width, fin bending and collapse, depth loading, damage and retention, advanced schemes |
| IV | 15–16 | Production: endpoint, metrology, APC, integration, yield, cost |

---

## Part I: Fundamentals (Chapters 1–4)

### Chapter 1: [The DRAM Cell Array & the Role of the Isolation Trench](./chapters/01-dram-cell-isolation-architecture.md)
**Estimated Time:** 60 min | **Difficulty:** Foundation | **Reading Level:** All roles  
**Focus:** Why does the array need isolation trenches, and what must they deliver?

**Key Topics:**
- The 1T1C cell, stored charge, and the 28 fA retention budget
- The 6F² layout, tilted AA islands, line spaces and cut gaps
- The buried-channel array transistor and the saddle fin
- The four jobs: isolation, transistor definition, passing-gate spacing, junction surface
- Aspect ratios, fin height-to-width ratio, generational trend, specification sheet

**Prerequisites:** None (foundational)  
**Cross-References:** Book #21 (logic STI)  
**Critical Equations:** Q = C_s V_DD/2; I_max = ΔQ/t_REF; D_min = WL bottom + margin; W(z) = W_t + 2z tan α  
**Study Questions:** 5 calculations on charge, layout, depth, and profile

---

### Chapter 2: [Active-Area Patterning — SAQP Lines, Cuts & the Hard-Mask Stack](./chapters/02-aa-patterning-hardmask.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Process/Integration roles  
**Focus:** What pattern does the etch inherit, and with what errors?

**Key Topics:**
- SAQP sequence; α, β, γ spaces and their error sensitivities
- Spacer-is-line versus spacer-is-space
- Edge roughness and correlation
- Cut schemes, cut window, island-end shape
- SiO₂/SiN/pad-oxide mask; mask-open taper; queue time; pattern density

**Prerequisites:** Chapter 1  
**Cross-References:** Books #19, #22; Appendix E.1.4  
**Critical Equations:** α = t₁, β = M − 2t₂, γ = P₁ − M − 2t₁ − 2t₂; W_t + 2OL ≤ w_c ≤ W_t + 2S − 2OL; S_Si = S_top − 2h_m tan β  
**Study Questions:** 5 calculations on SAQP, cuts, and masks

---

### Chapter 3: [Silicon Trench Etch Physics at Sub-20 nm Widths](./chapters/03-si-trench-physics.md)
**Estimated Time:** 90 min | **Difficulty:** Advanced | **Reading Level:** Process/Research roles  
**Focus:** Why do narrow trenches etch slowly, and by how much?

**Key Topics:**
- Ion-neutral synergy; flux estimates; series rate law
- Free-molecular transport; slot versus hole transmission
- Coburn–Winters model; the linear ARDE form and k
- Time-to-depth curves for cell, cut gap, and periphery
- Space-width sensitivity; macroloading; charging and deflection

**Prerequisites:** Chapters 1–2; Books #1–5  
**Cross-References:** Appendix B.7, Appendix E.2–E.3  
**Critical Equations:** K/(K + β(1 − K)); ER/ER₀ = 1/(1 + kA); t(z) = [z + (k/S)(z²/2 + h_m z)]/ER₀; θ_defl ≈ qE⊥L/(2E_i)  
**Study Questions:** 6 calculations on flux, transport, and ARDE

---

### Chapter 4: [Silicon Etch Chemistries & Sidewall Passivation](./chapters/04-chemistry-passivation.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Process/Research roles  
**Focus:** Which gases do what, and how does passivation set the angle?

**Key Topics:**
- HBr, Cl₂, O₂, He, and fluorine additives
- SiOₓBrᵧ formation, self-passivation of narrow trenches
- tan α ≈ r_p/ER_b; the oxygen window
- Mask consumption and facets on 14 nm lines
- Breakthrough options; residues and clean constraints; reference recipe

**Prerequisites:** Chapter 3  
**Cross-References:** *Polysilicon Etch* companion; Appendix B  
**Critical Equations:** tan α ≈ r_p/ER_b; cap loss = ER₀ t/S_ox + BT loss  
**Study Questions:** 5 calculations on passivation and mask

---

## Part II: Hardware Design (Chapters 5–9)

### Chapter 5: [Inductively Coupled Reactor Architecture for DRAM Isolation Etch](./chapters/05-icp-reactor-architecture.md)
**Estimated Time:** 65 min | **Difficulty:** Intermediate | **Reading Level:** Equipment/Process roles  
**Focus:** What chamber etches a dense array and a sparse periphery together?

**Key Topics:**
- ICP versus CCP for silicon trench etch
- Coil zones, window, Faraday shield
- Ion energy from bias power and ion current
- Residence time; etch products as 6% of the gas
- Cycle time, fleet size, chamber matching

**Prerequisites:** Chapters 1–4  
**Cross-References:** Books #11–15  
**Critical Equations:** ⟨V_sh⟩ ≈ ηP_bias/I_i; τ = pV/Q; WPH = 3600/t_cycle  
**Study Questions:** 5 calculations on energy, flow, and throughput

---

### Chapter 6: [Ion Energy, Bias Pulsing & Angular Control](./chapters/06-ion-energy-pulsing.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Equipment/Research roles  
**Focus:** How much energy, in what distribution, and why does pulsing lower ARDE?

**Key Topics:**
- Yield and selectivity versus energy; damage depth
- Sheath, transit time, IED at 2 and 13.56 MHz; light ions
- Synchronized pulsing and the coverage model: k from 0.058 to 0.025
- CW versus pulsed: same cell time, periphery 390 versus 310 nm
- Angular spread and sheath collisions

**Prerequisites:** Chapters 3, 5  
**Cross-References:** Books #11–15; Appendix E.4  
**Critical Equations:** Y = A(√E − √E_th); θ = R/(1 + R), β = s/(1 + R); σ_θ ≈ √(kT_i/2eV)  
**Study Questions:** 6 calculations on IED, pulsing, and angles

---

### Chapter 7: [Gas Delivery, Pressure & Multi-Step Recipe Design](./chapters/07-gas-pressure-steps.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Process/Equipment roles  
**Focus:** How is the recipe structured, and why is the step boundary at 120 nm?

**Key Topics:**
- Pressure as several knobs; flow and ratios
- BT / ME-1 / ME-2 / PS architecture; step marks and the word-line region
- Gas-arrival delay for minor gases
- ALE and quasi-ALE variants
- Radial tuning; depth-series development

**Prerequisites:** Chapters 4–6  
**Cross-References:** Appendix C.1, Appendix D  
**Critical Equations:** t_line ≈ V_line p_line/(Q × 760 Torr); exchange ≈ 3τ  
**Study Questions:** 6 calculations and planning exercises

---

### Chapter 8: [Wafer Temperature, Electrostatic Chucks & Radial Control](./chapters/08-temperature-esc-radial.md)
**Estimated Time:** 60 min | **Difficulty:** Intermediate | **Reading Level:** Equipment/Process roles  
**Focus:** How does temperature move the profile, and how is it used radially?

**Key Topics:**
- Temperature as a passivation knob; sensitivities
- Heat balance, time constants, ignition transient
- Multi-zone chucks and the transfer matrix
- Chucking, He leak, dechuck; the wafer edge; low-temperature etch

**Prerequisites:** Chapters 4–5  
**Cross-References:** Appendix C.5  
**Critical Equations:** ΔT = qR; τ_w = ρc_p t R; ∂W(140)/∂T ≈ −0.09 nm/°C  
**Study Questions:** 5 calculations on thermal control

---

### Chapter 9: [Chamber Walls, Edge Control & Contamination](./chapters/09-walls-edge-contamination.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Equipment/Process roles  
**Focus:** How do walls, edge ring, and contamination change the islands?

**Key Topics:**
- Wall deposits and drift; per-wafer WAC and season
- Edge sheath, tilt, edge depth and width; ring wear and compensation
- Metal contamination sources and limits
- Particles, AA bridges, micromasking; maintenance and recovery

**Prerequisites:** Chapters 5, 8  
**Cross-References:** Chapter 13 (retention); Appendix C.2, C.4  
**Critical Equations:** θ_e ≈ Δ/(2s); θ(x) = θ_e e^(−x/λ_e); ring life = 2Δ_allow/wear  
**Study Questions:** 5 calculations and diagnosis exercises

---

## Part III: Process Phenomena (Chapters 10–14)

### Chapter 10: [Profile Control — Taper, Bottom Shape, Corner Rounding & AA Width](./chapters/10-profile-aa-width.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration roles  
**Focus:** What shapes the AA at each depth, and how is each feature fixed?

**Key Topics:**
- Closure depth; fill limit; word-line limit; window 0.7–1.25°
- Taper-coupled ARDE and self-limited V-bottoms
- Microtrenching and the profile step
- Top etch bias, facet-driven bow, corner rounding
- AA width sensitivities; saddle fin; lever-response matrix

**Prerequisites:** Chapters 3, 4, 7  
**Cross-References:** Appendix D.2, D.5  
**Critical Equations:** z_close = S_t/(2 tan α); z_hit ≈ S/tan 2φ_f; ∂W(z)/∂α = 2z(π/180)  
**Study Questions:** 6 calculations on profile

---

### Chapter 11: [Fin Bending, Leaning & Pattern Collapse](./chapters/11-fin-bending-collapse.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Integration/Process/Research roles  
**Focus:** Will the fins stay upright through clean, dry, and fill?

**Key Topics:**
- Tapered cantilever and w_eff
- Capillary stability criterion; margins for water and IPA
- Why contact is permanent (adhesion vs. elastic energy)
- Pitch-walk amplification; array-edge one-sided load; surface-stress bending; fill
- Design, etch, and clean remedies; detection

**Prerequisites:** Chapters 2, 10  
**Cross-References:** Appendix C.6, D.6, E.5  
**Critical Equations:** M = (1.03Ew³/H⁴)/(4γcosθ/s²); δ = δ₀/(1 − 1/M); κ ≈ 6Δf/(Ew²)  
**Study Questions:** 6 calculations on mechanics

---

### Chapter 12: [Depth Loading — Cell Versus Periphery, Pitch Walk & Island Ends](./chapters/12-depth-loading-cell-peri.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration roles  
**Focus:** Can one etch time put every trench in its window?

**Key Topics:**
- Time window 58.1–66.0 s; periphery-bound
- k_max ≈ 0.057; rate tolerance ±6%
- Depth walk from pitch walk; cut gaps deeper; island-end pull-back
- Array edges, iso-dense periphery, sense amplifiers
- Depth budget; ARDE-reduction strategies; failure modes

**Prerequisites:** Chapters 3, 6, 10  
**Cross-References:** Chapter 14 (dual depth); Appendix D.3–D.4  
**Critical Equations:** window = [max lower limits, min upper limits]; ∂D/∂S ≈ 2.75 nm/nm  
**Study Questions:** 6 calculations on windows and budgets

---

### Chapter 13: [Etch Damage, Contamination & Data Retention](./chapters/13-damage-retention.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Device/Process/Research roles  
**Focus:** How does the plasma reach the retention tail?

**Key Topics:**
- Leakage paths; single-trap SRH current and field enhancement
- Trap and metal counts per junction
- Damage, Br, H, residue on bottom and sidewalls
- Liner consumption and the width trade-off
- Perimeter–area extraction; retention tail; damage-aware design

**Prerequisites:** Chapters 1, 6, 9  
**Cross-References:** Appendix C.8, E.7, F.6  
**Critical Equations:** I = q σ v_th n_i/2; N = D_it ΔE A; I = J_A A + J_P P; Si consumed = 0.44 t_ox  
**Study Questions:** 6 calculations on leakage and liner

---

### Chapter 14: [Advanced Schemes — Dual-Depth Isolation, EUV AA, 4F² & 3D DRAM](./chapters/14-advanced-isolation-schemes.md)
**Estimated Time:** 70 min | **Difficulty:** Advanced | **Reading Level:** Integration/Research roles  
**Focus:** What changes as 6F² shrinks and new cells arrive?

**Key Topics:**
- Cell pre-etch dual depth; boundary effects
- EUV cuts and direct islands; roughness versus pitch walk; stochastic bridges
- Next-node 6F² window and collapse margin
- 4F² vertical-channel isolation; 3D DRAM Si/SiGe stack slits

**Prerequisites:** Chapters 10–12  
**Cross-References:** Books #19, #24, #25  
**Critical Equations:** common-etch time = t(D) − t(z₁); M scaling w³/H⁴  
**Study Questions:** 6 calculations and comparisons

---

## Part IV: Production Scale (Chapters 15–16)

### Chapter 15: [Endpoint, Metrology & Advanced Process Control](./chapters/15-endpoint-metrology-apc.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Process/Equipment roles  
**Focus:** How do we see the islands, and how do we steer the etch?

**Key Topics:**
- Why no depth endpoint; endpoints that work; OES rate monitoring
- OCD, CD-SEM, CD-SAXS, TEM; OCD model pitfalls; sampling
- Fault detection, including silent pulsing failure
- Feed-forward; EWMA; two-knob control; width control; virtual metrology

**Prerequisites:** Chapters 9, 12  
**Cross-References:** Appendix F  
**Critical Equations:** o_{n+1} = λo_meas + (1 − λ)o_n; 2×2 sensitivity solve  
**Study Questions:** 6 calculations and design exercises

---

### Chapter 16: [Post-Etch Integration, Yield & Cost of Ownership](./chapters/16-integration-yield-coo.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** All roles  
**Focus:** What do later steps need from the etch, and what is it worth?

**Key Topics:**
- Queue time, liner, nitride-liner limits, fill gap
- Fill, bow keyholes, seams; CMP; word-line recess and oxide margin; contacts
- Yield signatures and their causes
- Killer-defect and retention-tail yield models
- Cost of ownership; alternatives; yield dominates

**Prerequisites:** Chapters 1, 10–13  
**Cross-References:** Book #21; *Silicon Nitride Etch* companion  
**Critical Equations:** gap = S(250) − 2 × 0.56 t_ox; 1 − exp(−D₀A); cost per wafer model  
**Study Questions:** 6 calculations on integration and cost

---

## Appendices

| Appendix | Title | Use |
|----------|-------|-----|
| [A](./appendices/A-material-properties.md) | Silicon, Mask, Liner & Chamber Material Properties | Film data, rates, geometry, liquids, chamber materials, metal limits |
| [B](./appendices/B-chemistry-reaction-data.md) | Chemistry & Reaction Data | Gases, bond energies, volatility, reactions, OES lines, transport tables |
| [C](./appendices/C-standard-procedures.md) | Standard Operating Procedures | Depth series, qualification, matching, edge calibration, zone matrix, collapse, OCD validation, retention screening |
| [D](./appendices/D-process-windows.md) | Process Windows & Lookup Tables | Reference recipe, sensitivities, time-to-depth, windows vs. k, profile, collapse, liner, mask |
| [E](./appendices/E-trench-geometry-transport-calculations.md) | Trench Geometry, Transport & Mechanical Calculations | All formulas with reference values |
| [F](./appendices/F-endpoint-metrology-reference.md) | Endpoint & Metrology Reference | Signals, FDC limits, methods, OCD checklist, sampling, electrical monitors, control limits |
| [G](./appendices/G-troubleshooting-guide.md) | Troubleshooting Guide | Symptom → cause → check → action |

Also: [GLOSSARY.md](./GLOSSARY.md)

---

## Reading Paths by Role

### Process Engineer (≈10 hours)
1 → 3 → 4 → 7 → 10 → 12 → 13 → Appendix D, E, G

### Equipment Engineer (≈9 hours)
1 → 5 → 6 → 7 → 8 → 9 → 15 → Appendix A, C, F

### Integration Engineer (≈8 hours)
1 → 2 → 10 → 11 → 12 → 16 → Appendix D, E, G

### Device Engineer (≈5 hours)
1 → 10 → 13 → 16

### Researcher (≈10 hours)
3 → 4 → 6 → 11 → 13 → 14 → Appendix B, E

---

## Cross-Reference Map to Other Books

| Book | Topic | Relevant Chapters |
|------|-------|-------------------|
| Books #1–5 | Plasma Physics Fundamentals | Ch. 3, 5, 6 |
| Books #6–10 | Dielectric & Fluorocarbon Etch | Ch. 2 (mask open), 4 (breakthrough) |
| Books #11–15 | Advanced Plasma Engineering | Ch. 5, 6, 7, 15 |
| Book #19 | Carbon Hard Mask Etch | Ch. 2, 11 (wiggle), 14 |
| Book #20 | Photoresist Ashing | Ch. 2, 14 (block-mask strip) |
| Book #21 | Shallow Trench Isolation Etch | Ch. 1, 13, 16 |
| Book #22 | Spacer Etchback | Ch. 2 (SAQP spacers) |
| Books #24, #25 | 3D NAND HAR Etch | Ch. 14 (3D DRAM) |
| Companion | Polysilicon Etch | Ch. 4 |
| Companion | Silicon Nitride Etch | Ch. 4, 16 |

---

## Study Questions Summary

**Total Study Questions:** 90 (5–6 per chapter × 16 chapters)  
**Nature:** Mostly calculation-based  
**Topics:** Cell layout and retention budget, SAQP and cut windows, transport and ARDE, passivation and angle, ion energy and pulsing, thermal and edge control, profile and AA width, collapse mechanics, depth windows and budgets, junction leakage and liner trade-offs, dual-depth and next-node scaling, APC, integration, cost

Examples:
- Derive the minimum cell depth from the buried word line and its oxide margin
- Compute α, β, γ spaces from SAQP mandrel and spacer dimensions
- Extract the ARDE coefficient from a depth-versus-width test
- Show why pulsing gives the same cell time but an 80 nm shallower periphery
- Find the time window for cell and periphery and the maximum k
- Compute the collapse margin of a tapered fin dried from IPA
- Estimate the leakage from a single trap and the traps per junction
- Size a cell pre-etch for a dual-depth scheme
- Solve a two-knob APC correction for cell and periphery depth
- Compare cost per wafer with the value of 0.1% yield

---

## How to Use This Index

1. **First time?** Read PREFACE.md, then this INDEX, then Chapter 1.
2. **Focused reading?** Pick your role from the reading paths above.
3. **Reference mode?** Jump to the chapter. Use Appendix G for symptoms and Appendix E for formulas.
4. **Deep dive?** Read Chapters 1–16 in order and work the study questions.

---

**Index Version:** 1.0  
**Last Updated:** 2026-10-04  
**Next:** Begin [Chapter 1: The DRAM Cell Array & the Role of the Isolation Trench](./chapters/01-dram-cell-isolation-architecture.md)
