---
layout: post
title: "EC2 §6.1: Rectangular Beam Bending Design — Complete Worked Example (Free Download)"
date: 2026-11-23
description: "Step-by-step EC2 §6.1 bending design of a 300×600 rectangular beam: stress block, neutral axis from equilibrium, lever arm, A_s,min/A_s,max, bar spacing and the balanced-section yield check. Free workbook."
tags: [EC2, bending, flexure, beam, worked example]
---

## The Problem

The same 6 m office beam as the shear worked example: 300 × 600 mm, C30/37, B500B, carrying g_k = 35 kN/m and q_k = 20 kN/m. The design moment is 347.6 kNm at midspan, and the shear post took 4H25 as the main steel from a "bending pre-step" it did not show. This post is that step. The task is to design the longitudinal steel for bending at the ultimate limit state: solve the neutral axis from the rectangular stress block, size the bars, verify the provided section against the design moment, and check whether the steel yields before the concrete crushes — every intermediate value shown. No iteration is needed: the equilibrium equation is a quadratic, and both roots should be examined.

## The Relevant Clauses

- §6.1(2): plane sections remain plane; tensile strength of the concrete is ignored; concrete stresses from §3.1.7 and steel stresses from §3.2
- §3.1.6(1)P, Eq (3.15): f_cd = α_cc · f_ck / γ_C — α_cc = 1.0 is the recommended value (0.8–1.0; check your National Annex)
- §3.1.7(3), Eq (3.19) and (3.20): rectangular stress block with λ = 0.8 and η = 1.0 for f_ck ≤ 50 MPa
- Table 3.1: C30/37 — f_ctm = 2.9 MPa, ε_cu3 = 3.5 ‰ (bilinear diagram, Figure 3.4)
- §3.2.7(2) and (4): f_yd = f_yk / γ_S, E_s = 200 GPa
- §9.2.1.1(1), Eq (9.1N) and §9.2.1.1(3): minimum and maximum longitudinal steel
- §8.2(2): minimum clear spacing between bars
- EN 1990 Eq (6.10): persistent design situation, γ_G = 1.35, γ_Q = 1.5
- §5.5(4), Eq (5.10a): neutral-axis limit for linear analysis with limited redistribution — δ ≥ k₁ + k₂·x_u/d, with recommended k₁ = 0.44 and k₂ = 1.25(0.6 + 0.0014/ε_cu2); at δ = 1 this gives x_u/d ≤ 0.45 for C50/60

All values below are the EN 1992-1-1 recommended (CEN) values. Check your National Annex before relying on any of them.

## Input Data

| Parameter | Value | Unit | Notes |
|-----------|-------|------|-------|
| Span L | 6,000 | mm | Simply supported |
| b | 300 | mm | Beam width |
| h | 600 | mm | Overall depth |
| g_k | 35 | kN/m | Permanent, incl. self-weight |
| q_k | 20 | kN/m | Office + movable partitions |
| f_ck | 30 | MPa | C30/37 |
| f_yk | 500 | MPa | B500B |
| c_nom | 35 | mm | XC1, structural class S4 (as post #1) |
| Links | H8 | mm | Two legs |
| Main bars | 4H25 | — | To be confirmed in Step 6 |
| Max aggregate d_g | 20 | mm | For the spacing check |

## Step-by-Step Calculation

### Step 1: Material Properties

Concrete design strength, §3.1.6(1)P Eq (3.15):

f_cd = α_cc × f_ck / γ_C = 1.0 × 30 / 1.5 = **20.0 MPa**

Steel design strength, §3.2.7(2):

f_yd = f_yk / γ_S = 500 / 1.15 = **434.8 MPa**

Design yield strain, §3.2.7(4) with E_s = 200 GPa:

ε_yd = f_yd / E_s = 434.8 / 200,000 = **0.002174** (2.174 ‰)

From §3.1.7(3) for f_ck ≤ 50 MPa: λ = 0.8, η = 1.0. From Table 3.1, C30/37: ε_cu3 = 3.5 ‰, f_ctm = 2.9 MPa. The ε_cu3 = 3.5 ‰ limit belongs to the bilinear diagram of Figure 3.4; combined with the rectangular block of §3.1.7(3) (Figure 3.5) it is the standard ULS idealisation used in this post.

### Step 2: Design Moment

Load combination, EN 1990 Eq (6.10):

w_d = 1.35 × 35 + 1.5 × 20 = 47.25 + 30.0 = **77.25 kN/m**

M_Ed = w_d × L² / 8 = 77.25 × 6.0² / 8 = **347.6 kNm**

### Step 3: Effective Depth

d = h − c_nom − φ_link − φ_main/2 = 600 − 35 − 8 − 25/2 = **544.5 mm**

The cover is inherited from the shear post: exposure class XC1 with structural class S4 gives c_nom = 35 mm under §4.4.1 and the National Annex. If your cover step gives a different value, d moves and every number below changes.

### Step 4: Neutral Axis from Equilibrium

The rectangular block (§3.1.7(3), Figure 3.5) gives the concrete force:

C = η × f_cd × b × λx = 1.0 × 20 × 300 × 0.8x = 4,800x (N, x in mm)

The lever arm between C and the steel is:

z = d − λx/2 = 544.5 − 0.4x

The resistance is M = C × z:

M(x) = 4,800x × (544.5 − 0.4x)

Setting M(x) = M_Ed = 347.6 × 10⁶ N·mm gives a quadratic:

0.4x² − 544.5x + 72,421.9 = 0

x = [544.5 ± √(544.5² − 4 × 0.4 × 72,421.9)] / (2 × 0.4)

x = [544.5 ± √(296,480 − 115,875)] / 0.8 = [544.5 ± 425.0] / 0.8

The two roots are x = **149.4 mm** and x = 1,211.8 mm. The second root is not a section: 0.8x would be 969 mm, deeper than the 600 mm beam. Only the first root is valid. This is worth doing explicitly — the invalid root is how a negative or nonsense lever arm slips into a spreadsheet.

At x = 149.4 mm:

x/d = 149.4 / 544.5 = **0.274**

z = 544.5 − 0.4 × 149.4 = **484.7 mm**

### Step 5: Required Reinforcement

Equilibrium of forces, C = T:

C = 4,800 × 149.4 = 717,139 N = **717.1 kN**

A_s,req = C / f_yd = 717,139 / 434.8 = **1,649 mm²**

### Step 6: Bar Selection

| Option | A_s (mm²) | M_Rd (kNm) | Utilisation | Verdict |
|--------|-----------|------------|-------------|---------|
| 3H25 | 1,473 | 314.5 | 1.11 | ✗ |
| 4H20 | 1,257 | 272.6 | 1.28 | ✗ |
| 4H25 | 1,963.5 | 404.1 | 0.86 | ✓ |
| 3H32 | 2,413 | 479.5 | 0.72 | ✓ |

3H25 lands at a utilisation of 1.11 — 11 % short, the most common result of sizing off A_s,req alone and rounding to a familiar pattern. I keep **4H25**, the same steel as the shear post, so the series works one beam rather than four. 3H32 also passes on area; it fails nothing here, but larger bars make anchorage and crack control harder in a 300 mm web, so the redundant option buys nothing.

### Step 7: Verify the Provided Section

For 4H25, A_s = 4 × 490.9 = **1,963.5 mm²**. The steel force at yield:

T = A_s × f_yd = 1,963.5 × 434.8 = **853.7 kN**

The neutral axis follows from C = T:

x = T / (η × f_cd × b × λ) = 853,693 / (1.0 × 20 × 300 × 0.8) = **177.9 mm**

z = 544.5 − 0.4 × 177.9 = **473.4 mm**

M_Rd = T × z = 853.7 × 473.4 / 1,000 = **404.1 kNm**

Utilisation: M_Ed / M_Rd = 347.6 / 404.1 = **0.86**.

The steel strain at the design section, from strain compatibility (§6.1(2)):

ε_s = ε_cu3 × (d − x) / x = 3.5 × (544.5 − 177.9) / 177.9 = **7.22 ‰**

That is more than three times ε_yd = 2.174 ‰, so the steel yields well before the concrete crushes. Good — but "the steel yields" is a conclusion, and Step 8 shows how to prove it before choosing bars rather than after.

### Step 8: The Balanced Section — When Does the Steel Yield?

The balanced section is the one where the concrete reaches ε_cu3 and the steel reaches ε_yd at the same instant. Strain compatibility gives:

x_bal / d = ε_cu3 / (ε_cu3 + ε_yd) = 3.5 / (3.5 + 2.174) = **0.617**

For this section:

x_bal = 0.617 × 544.5 = **335.9 mm**

z_bal = 544.5 − 0.4 × 335.9 = **410.1 mm**

M_bal = η × f_cd × b × λx_bal × z_bal = 20 × 300 × 0.8 × 335.9 × 410.1 / 10⁶ = **661.2 kNm**

A_s,bal = M_bal / (f_yd × z_bal) = 661.2 × 10⁶ / (434.8 × 410.1) = **3,708 mm²** (ρ = 2.06 % of A_c)

The demand is M_Ed / M_bal = 347.6 / 661.2 = **0.53**. Below 1 means the required steel is less than A_s,bal, so the steel yields before the concrete crushes — the section is under-reinforced. If M_Ed had exceeded M_bal, any steel quantity that satisfied moment would leave the steel below yield, and the section would need compression reinforcement or a larger depth.

The balanced point is a property of the section, not a code limit: it tells you when the steel yields, not whether the section is admissible. The limit on a singly reinforced section comes from §5.5(4), Eq (5.10a), which ties the neutral-axis depth to the redistribution δ used in the analysis:

δ ≥ k₁ + k₂ · x_u/d

with k₁ = 0.44 and k₂ = 1.25(0.6 + 0.0014/ε_cu2) at the recommended values. For no redistribution (δ = 1) and ε_cu2 = 3.5 ‰, k₂ = 1.25 and the expression gives x_u/d ≤ 0.448 — the familiar 0.45 limit is this equation evaluated at δ = 1, not a separate ductility rule. The Designer's Guide to EN 1992-1-1 (§5.2.1) reads clause 5.5 the same way and sets the singly reinforced limit from it: when the moment exceeds the limiting value for the δ used, the section needs compression reinforcement (§5.2.2, Eqs D5.7/D5.8), not more tension steel.

For this beam, x/d = 0.327 at the provided steel, below 0.448, so a singly reinforced section is admissible and 4H25 is the whole solution. The balanced ratio of 0.617 sits well above both — that margin is what makes the yielding conclusion comfortable.

### Step 9: Detailing Checks

Minimum steel, §9.2.1.1(1) Eq (9.1N):

A_s,min = max(0.26 × f_ctm / f_yk, 0.0013) × b × d = max(0.26 × 2.9 / 500, 0.0013) × 300 × 544.5

= max(0.001508, 0.0013) × 163,350 = **246 mm²** ✓

Maximum steel, §9.2.1.1(3): A_s,max = 0.04 × A_c = 0.04 × 180,000 = **7,200 mm²** ✓

Reinforcement ratio: ρ = 1,963.5 / 180,000 = **1.09 %**.

Clear spacing, §8.2(2):

s_clear = (300 − 2 × 35 − 2 × 8 − 4 × 25) / 3 = **38 mm**

The minimum is max(k₁φ, d_g + 5, 20) = max(25, 25, 20) = **25 mm** with 20 mm aggregate, so 38 mm passes. With 32 mm aggregate the limit becomes 37 mm and the check still passes, barely.

## Result Summary

| Check | Value | Reference | Ratio | Result |
|-------|-------|-----------|-------|--------|
| M_Rd | 404.1 kNm | M_Ed = 347.6 kNm | 0.86 | ✅ |
| A_s required | 1,649 mm² | 1,963.5 mm² (4H25) | 0.84 | ✅ |
| A_s,min (§9.2.1.1(1)) | 1,963.5 mm² | 246 mm² | 0.13 | ✅ |
| A_s,max (§9.2.1.1(3)) | 1,963.5 mm² | 7,200 mm² | 0.27 | ✅ |
| x/d provided | 0.327 | balanced 0.617 | 0.53 | ✅ |
| ε_s at M_Ed | 7.22 ‰ | ε_yd = 2.174 ‰ | 3.3 | ✅ |
| Clear bar spacing (§8.2(2)) | 38 mm | 25 mm | 0.66 | ✅ |

The provided x/d in the table is 177.9 / 544.5 = 0.327; the required one is 0.274. Both sit well below the balanced ratio of 0.617, which is the point of Step 8.

## What This Post Does Not Cover

Shear design and crack width have their own worked examples in this series; deflection, anchorage and curtailment, flanged (T-) sections, doubly reinforced sections, and continuous beams with redistribution are outside this example. The design is for a persistent load case on a simply supported beam; seismic detailing and accidental combinations are not addressed.

## The Download

📥 [Download the full calculation spreadsheet](/assets/ec2-bending-rectangular-beam.xlsx)

The workbook carries every value in this post — inputs, the quadratic, the balanced-section check, the bar options and the detailing checks — as values only. It is free, no email gate. If something in it does not reconcile with your own calculation, email me at hugo@civion.cloud and I will look at it.

## What I'm Building

Bending design is where most spreadsheet errors enter a project: a wrong lever arm or an unchecked second root is invisible in the output and decisive in the design. I'm building Civion's EC2 RC Column Section Designer to run this equilibrium — and the strain-compatibility check behind it — across load cases at once, with every intermediate value kept visible. If that sounds useful, write to me at <hugo@civion.cloud> and I'll tell you when it's ready.