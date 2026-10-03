# Chapter 12: Profile & Morphology Evolution (Sidewall Shape and Notching)

## Executive Summary

The vertical profile of an etched trench—the sidewall angle, smoothness, and freedom from notches—is as critical to device function as the etch depth itself. A perfectly vertical trench with smooth walls enables reliable metallization and dielectric deposition. A tapered trench (sidewalls angling inward) complicates fill and creates thickness variations. A notched trench (unexpected etch below the intended feature) can undermine oxide dielectrics or create parasitic structures. Yet profile evolution is subtle and often counterintuitive, emerging from the asymmetry between ions (directed downward by the sheath electric field) and radicals (diffusing isotropically). This chapter develops profile physics rigorously—examining how ion-assisted chemical etching creates preferential sidewall attack, how passivation films can protect or fail to protect sidewalls, and how geometry-dependent ion energy and flux distribution generate notches and corrosion. We derive predictive models for sidewall angle, measure profile evolution via cross-section SEM and critical-dimension SEM (CD-SEM), and present practical recipes balancing profile control with throughput and uniformity. Understanding profile control is essential for advanced nodes, where interconnect linewidths (20-40 nm at 5 nm node) demand sidewall angles within ±5° of vertical and notch depths <10% of feature depth to prevent catastrophic fill failures.

---

## Part 1: Profile Physics and Mechanisms

### 1.1 Ideal vs. Real Trench Profiles

**Ideal profile (perfectly vertical, smooth):**

```
Photoresist mask
  ▼▼▼▼▼▼
  ▲ ▲ ▲ (Al surface)
  │ │ │ (vertical walls)
  │ │ │
  ─ ─ ─ (Al-oxide interface)
  ░ ░ ░ (SiO₂)
```

**Real profile (tapered or notched, common):**

```
         ▼▼▼▼▼▼
       ╱     ╲  (tapered sidewalls, angle > 0°)
      │       │
      │       │
 ┌─┴─┘       └─┴─┐ (notch at oxide interface)
 │               │
 ░               ░ (SiO₂ with erosion at base)
```

**Key deviations from ideal:**
1. **Sidewall taper angle θ:** Angle between sidewall and vertical (0° = perfect vertical, 5-10° typical, >15° problematic)
2. **Notch depth:** Etching of oxide at trench base (0-50 nm typical, should be <10%)
3. **Sidewall roughness:** RMS roughness ~2-10 nm (should be <5 nm for fine features)
4. **Corrosion/edge erosion:** Oxide etching at feature edges (0-20 nm typical)

### 1.2 Ion vs. Radical Contributions to Profile

**Ions are directed; radicals are isotropic:**

- **Ion bombardment:** High-energy Cl⁺ ions strike substrate (sheath-accelerated, ~100-200 eV), travel primarily vertically downward
  - Effect on sidewalls: Ions mostly *miss* sidewalls (travel straight down)
  - Effect on bottom: Ions hit bottom directly → sputtering-dominated etch

- **Radical attack:** Cl atoms diffuse isotropically (random walk)
  - Effect on sidewalls: Radicals reach sidewalls easily → chemical etch
  - Effect on bottom: Radicals compete with ions (if radicals dominant, slower etch)

**Profile consequence:**

In **pure ion sputtering** (no radicals, argon plasma):
- Vertical profile (ions hit vertically)
- Fast etch rate (sputtering efficient)

In **pure radical etch** (low-temperature, no ions, e.g., downstream plasma):
- Isotropic profile (all exposed surfaces etch equally)
- Result: Trenches become hemispherical/rounded (no vertical walls!)

In **typical CCP etch** (mixed ion + radical):
- Bottom etch: Both ions and radicals contribute (faster)
- Sidewall etch: Primarily radicals (slower, more isotropic)
- Result: Sidewalls etch *slower* than bottom → undercut at base (notch)

### 1.3 Ion-Assisted Chemical Etching Profile Effect

**Ion-assisted chemical (IAC) etching creates sidewall attack:**

When ions bombard a surface covered with adsorbates (e.g., Cl radicals on Al sidewall):

1. **Ion impact:** Cl⁺ strikes sidewall surface
2. **Adsorbate excitation:** Ion energy dislodges or activates Cl atoms already on surface
3. **Chemical enhancement:** Activated Cl atoms react vigorously with Al → AlCl₃ formation
4. **Synergy:** Chemical reaction rate enhanced >10× by ion presence vs. radicals alone

**Effect on profile:**

If sidewall IAC is strong → sidewalls etch nearly as fast as bottom → vertical profile.
If sidewall IAC is weak → sidewalls etch slowly → tapered profile (bottom-heavy etch).

**Parameters controlling IAC sidewall effect:**

- **Ion angle of incidence:** Glancing angles (ions hitting sidewalls at shallow angle) are less effective than normal incidence
- **Ion energy:** Higher energy → more adsorbate activation, stronger IAC
- **Adsorbate coverage:** Need sufficient Cl coverage on sidewalls for IAC to work
- **Sidewall temperature:** Higher temperature → more reactive chemistry (but higher temperatures degrade resist)

---

## Part 2: Notching Mechanism and Origin

### 2.1 Why Notches Form (Under-Profile Etch)

**Notching is preferential oxide etch at the Al-oxide interface:**

```
Al trench:          Sidewall wall composition changes:
  │ Al │ ┐          ┌─────────────────────┐
  │    │ │ Interface │ Mostly Al oxide     │
  │    │ │ region    │ (1-3 nm, highly    │
  │ Al │ │ (5-10nm)  │  reactive)         │
  ──────  ┘          │ Then bulk SiO₂     │
    SiO₂             └─────────────────────┘
```

**Root cause:** In the Al-oxide interface region, the material is partially oxidized (Al₂O₃, mixed Al-Si oxides). These oxides are often *more* etch-prone than bulk SiO₂ due to:

1. **Defective crystal structure:** Interface oxides have grain boundaries, vacancies
2. **Mixed valence states:** Partial oxidation → more reactive than fully oxidized SiO₂
3. **Stress:** Interface oxides under mechanical stress from Al thermal expansion mismatch

**Selective attack:** Radicals preferentially attack interface oxides → etch faster at interface → notch formation.

### 2.2 Plasma-Induced Oxide Damage

**Al oxidizes to ~2-3 nm Al₂O₃ native oxide before trench etch:**

```
Pristine Al surface: Al-O-Al-O-Al-... (stoichiometric Al₂O₃, ~2-3 nm)
After Cl₂ plasma exposure: Cl attacks oxide, creates defects:
├─ Cl⁻ ions leave behind vacancies (O vacancies, Al vacancies)
├─ Stress-induced cracking (chlorine is small, creates strains)
└─ Substoichiometric oxides (Al₂O₃ → Al₂O₂ → AlO, etc.)
```

**Effect:** Interface region becomes *more* reactive, not passivated → accelerated attack.

### 2.3 Quantitative Notch Depth Evolution

**Notch depth grows during etch as oxide is preferentially attacked:**

**Example measurement (50 mTorr, Cl₂/HCl, no BCl₃):**

| Etch Time | Trench Depth | Notch Depth | Notch/Depth Ratio |
|---|---|---|---|
| **5 min** | 150 nm | 5 nm | 3% |
| **10 min** | 300 nm | 15 nm | 5% |
| **15 min** | 450 nm | 35 nm | 8% |
| **20 min** | 600 nm | 60 nm | 10% |
| **25 min** | 750 nm | 90 nm | 12% |

**Trend:** Notch depth grows ~3-4 nm per minute; total trench depth ~30 nm/min. Notch ratio reaches ~10% after 20 min etch.

**Critical insight:** Notch depth is *not* proportional to trench depth. Notch rate is approximately constant (~3-4 nm/min), independent of Al removal rate.

$$\frac{d(\text{notch depth})}{dt} ≈ \text{constant} \quad (\text{independent of trench depth})$$

**Implication:** Longer etch times → higher notch-to-depth ratio (risk increases).

---

## Part 3: Profile Control Mechanisms

### 3.1 Passivation-Protected Sidewalls

**BCl₃ passivation films protect sidewalls from notching:**

When BCl₃ is added to etch plasma, boron-chloride polymer deposits on sidewalls:

```
Trench cross-section:
    │ ← Photoresist mask
  ┌─┴─┐
  │(B)│ ← Boron-chloride passivation film (10-20 nm)
  │ Al│ ← Protected Al sidewall
  │(B)│
  │───│ ← Interface (notch risk zone, also protected by (B-Cl)_n)
  │SiO₂│ ← Oxide, protected
  └─┬─┘
    ░
```

**Protection mechanism:**

1. **Sidewall film:** (BCl)_n coating (10-20 nm) covers Al
   - Blocks Cl radicals from attacking Al sidewalls directly
   - Reduces sidewall etch rate ~10× (from 30 nm/min to 3 nm/min)

2. **Interface region:** (BCl)_n coating also protects oxide interface
   - Blocks Cl radicals from attacking defective interface oxide
   - Notch depth suppressed from 3-4 nm/min to <0.5 nm/min

3. **Thickness control:** Passivant film must be thick enough to protect (>10 nm) but thin enough to remove from bottom within acceptable overetch time

**Result with passivation:**

| Etch Time | Trench Depth | Notch Depth (No Passiv.) | Notch Depth (With Passiv.) |
|---|---|---|---|
| **20 min** | 600 nm | 60 nm (10%) | 8 nm (1.3%) |
| **30 min** | 900 nm | 95 nm (11%) | 12 nm (1.3%) |

**Passivation reduces notch ratio 8-10× (from 10% to 1.3%).**

### 3.2 Sidewall Angle Control via Passivation

**Thin passivation films can also tune sidewall taper angle:**

**Without passivation (bare Al):**
- Bottom etch rate (ions + radicals): ~30 nm/min
- Sidewall etch rate (radicals only, no ions): ~5 nm/min (isotropic)
- Taper angle θ: arctan(5/30) ≈ 9-10° (sidewalls slope inward)

**With thin passivation (5 nm film):**
- Bottom etch rate: ~25 nm/min (slightly reduced due to film on bottom)
- Sidewall etch rate: ~2 nm/min (film blocks radicals)
- Taper angle θ: arctan(2/25) ≈ 4-5° (more vertical)

**With thick passivation (20 nm film):**
- Bottom etch rate: ~20 nm/min (heavier film coverage)
- Sidewall etch rate: ~0.5 nm/min (heavily protected)
- Taper angle θ: arctan(0.5/20) ≈ 1-2° (nearly vertical!)

**Trade-off:** Thicker passivation → more vertical sidewalls, but slower overall etch rate and higher notch-suppression overhead.

### 3.3 Ion Angle Optimization

**Tilting wafer relative to ion beam changes ion angle of incidence on sidewalls:**

In standard CCP, ions travel vertically (perpendicular to wafer). But some reactors allow wafer tilt or use shaped electrode geometry to angle ions:

**Normal ion incidence (0° tilt, vertical ions):**
```
Ions ↓↓↓
Sidewalls │ │ (ions glance off, contribute little to IAC)
```

**Angled ion incidence (10-20° tilt):**
```
Ions ↖↖↖ (angled)
Sidewalls ╱ ╲ (ions hit at steeper angle, better IAC)
```

**Effect on sidewall etch:**
- Normal (0°): Sidewall IAC weak → low etch rate → tapered
- Angled (15°): Sidewall IAC stronger → higher etch rate → more vertical

**Practical limit:** Tilt angle >20° risks non-uniformity (different parts of wafer experience different ion angles).

---

## Part 4: Measurement of Profile and Morphology

### 4.1 Cross-Section SEM (Gold Standard)

**Scanning Electron Microscopy of cleaved or ion-milled cross-section:**

```
Preparation:
1. Etch sample on wafer
2. Cleave wafer or ion-mill cross-section
3. Mount on SEM stub
4. Image at high resolution (5-50 kV, 100-500 kX magnification)
```

**Measurements extracted:**
- **Trench depth:** Distance from top Al to oxide interface
- **Trench width (critical dimension, CD):** Width of Al trench
- **Sidewall angle θ:** Angle between sidewall and vertical (measured from image)
- **Notch depth:** Depth of oxide erosion below Al-oxide interface
- **Sidewall roughness:** RMS deviation from ideal line (measured via autocorrelation)

**Example cross-section SEM analysis:**

```
                           ▼▼▼▼▼ (Resist top)
                         ╱        ╲
                        │          │ ← Sidewall at angle θ=6°
                        │          │
                        │          │ (Al, 500 nm wide)
                        │          │
    ─────────────────────┴──────────┴─────── (Al-oxide interface)
                        ▔▔▔▔▔▔▔▔▔▔ (Notch, ~30 nm deep)
                        ░░░░░░░░░░ (SiO₂)

Measurements:
├─ Trench depth: 500 nm ✓
├─ Trench width: 48 nm (nominal 50 nm, ~4% CD bias)
├─ Sidewall angle: 6° ✓ (acceptable if <±5° spec)
└─ Notch depth: 30 nm (~6% of depth, acceptable if <10%)
```

**Advantages:** High resolution (~1-5 nm), direct measurement, provides full profile shape
**Disadvantages:** Destructive (consumes sample), time-consuming (1-2 hours per sample), limited statistics (few cross-sections possible)

### 4.2 Critical Dimension SEM (CD-SEM)

**Nondestructive measurement of feature linewidth via top-down SEM imaging:**

CD-SEM measures the *width* of Al lines directly from top, using image processing to find edges.

**Measurement process:**
1. Image trench from top (normal SEM geometry)
2. Apply edge-detection algorithm (find pixel intensity transitions)
3. Measure distance between left and right edges → CD

**What CD-SEM reveals (indirectly):**
- **Direct measurement:** Top linewidth (closest to mask)
- **Inferred from pattern:** If bottom linewidth different, suggests taper
  - Tapered profile (bottom narrower than top): CD shrinks with depth
  - Reverse-tapered (bottom wider): CD grows with depth

**Resolution:** ~3-10 nm (limited by beam spot size and edge-detection precision)

**Advantages:** Nondestructive, fast (5 min/wafer), many samples possible
**Disadvantages:** Indirect measurement (cannot measure sidewall angle, notch, roughness directly), limited to linewidth

### 4.3 Three-Dimensional Profile Reconstruction

**Modern approach: Combine multiple cross-sections or use FIB/SEM 3D reconstruction:**

Focused Ion Beam (FIB) serially sections sample (slice ~10-20 nm thick) and SEM images each slice → 3D reconstruction of entire trench:

```
Individual slices:    3D reconstruction:
Slice 1: ┌─┐         ╱───────╲
Slice 2: │ │    →   ╱         ╲  (full 3D shape visible)
Slice 3: │ │       │           │
Slice 4: └─┘       └───────────┘
```

**Measurements from 3D:**
- Sidewall angle (average and distribution)
- Notch shape and depth
- Sidewall roughness (RMS on 3D surface)
- Volume of material removed at interface

**Cost/time:** ~2-4 hours per sample, ~$500-1000/sample (expensive but comprehensive)

---

## Part 5: Profile Evolution with Process Parameters

### 5.1 Pressure Dependence of Sidewall Angle

**Higher pressure → more radicals, stronger isotropic etch → more tapered profile:**

| Pressure | Sidewall Etch Rate | Bottom Etch Rate | Taper Angle θ |
|----------|---|---|---|
| **10 mTorr** | 2 nm/min | 35 nm/min | 3° |
| **30 mTorr** | 4 nm/min | 30 nm/min | 7.5° |
| **50 mTorr** | 6 nm/min | 28 nm/min | 12° |
| **100 mTorr** | 8 nm/min | 25 nm/min | 18° |

**Trend:** As pressure increases from 10 to 100 mTorr, taper angle increases ~6×.

**Physical reason:** Higher pressure → higher radical density → stronger sidewall etch → profile becomes more isotropic (hemispherical tendency).

**Profile specification trade-off:**
- Low pressure (10 mTorr): Vertical sidewalls (θ < 3°) ✓, but poor ARDE (Chapters 10)
- High pressure (100 mTorr): Better ARDE ✓, but tapered sidewalls (θ ~ 18°) ✗

### 5.2 BCl₃ Flow Dependence of Notch Depth

**Higher BCl₃ → thicker passivation → notch suppression:**

| BCl₃ Flow (sccm) | Passiv. Thickness | Notch Depth (20 min) | Notch/Depth |
|---|---|---|---|
| **0 (baseline Cl₂/HCl)** | None | 60 nm | 10% |
| **5** | ~10 nm | 25 nm | 4% |
| **10** | ~15 nm | 12 nm | 2% |
| **15** | ~20 nm | 6 nm | 1% |
| **20** | ~25 nm | 3 nm | 0.5% |

**Trade-off:** Better notch suppression, but Al etch rate decreases:

| BCl₃ Flow | Al Etch Rate | Throughput Loss |
|---|---|---|
| **0** | 300 nm/min | Baseline |
| **10** | 250 nm/min | 17% |
| **20** | 200 nm/min | 33% |

**Practical recipe:** 10-15 sccm BCl₃ balances notch control (1-2% acceptable) with throughput loss (~10-15%).

### 5.3 Microloading Effect on Sidewall Angle

**Feature density affects sidewall profile (microloading extends beyond just etch rate):**

**Dense pattern (high feature density):**
- Radicals depleted collectively → lower radical flux to sidewalls
- Sidewall etch slower → profile more vertical (θ ~ 4-5°)

**Sparse pattern (low feature density):**
- Radicals abundant → higher flux to sidewalls
- Sidewall etch faster → profile more tapered (θ ~ 10-12°)

**Consequence:** Across wafer with mixed dense and sparse regions, sidewall angles vary significantly (5-10% non-uniformity). This complicates subsequent deposition steps.

---

## Part 6: Corrosion and Oxide Edge Erosion

### 6.1 Corrosion Mechanism at Al-Oxide Interface

**At feature edges (especially at corners), oxide erosion extends beyond notch:**

```
Top view of Al line:
    ▼▼▼ (Cl radicals)
   ╱ Al ╲ ← Lines
  │      │
  └──────┘
    ╱░░░╲ ← Oxide corrosion at edges (not just at center)
```

**Root cause:** At feature edges, geometry allows radicals to attack oxide from the side (in addition to bottom attack creating notches).

**Radial etch pattern:**
- Center (under line): Notch etch (primarily vertical)
- Edges (beside line): Corrosion etch (lateral attack on oxide)

**Effect:** Oxide undercut extends ~1-2 μm laterally from Al line (depending on oxide etch rate, etch time).

### 6.2 Corrosion-Induced Yield Issues

**Oxide corrosion can cause device failures:**

1. **Via-to-line contact:** If oxide corroded too much, via trench may contact adjacent metal line (creates parasitic short)
2. **Dielectric breakdown:** Thinned oxide at edge reduces dielectric strength (leakage current increases)
3. **Electromigration:** Metal-oxide interface roughness from corrosion accelerates EM degradation

**Specification:** Oxide corrosion <50 nm laterally (for 100 nm line pitch, this consumes ~25% of available space).

### 6.3 Corrosion Control via Selectivity

**Higher Al-to-oxide selectivity (via BCl₃) reduces corrosion:**

| Recipe | S_Al/SiO₂ | Oxide Corrosion (Lateral) |
|---|---|---|
| **Cl₂/HCl only** | 5× | 80 nm |
| **Cl₂/HCl/BCl₃ (10%)** | 12× | 35 nm |
| **Cl₂/HCl/BCl₃ (20%)** | 20× | 15 nm |

**Trend:** 4× selectivity improvement → 5× corrosion reduction.

**Mechanism:** High selectivity means oxide etch rate very low → even if oxide exposed at edges for long time, limited lateral erosion.

---

## Part 7: Practical Profile Control Recipes

### 7.1 Lam Cl2® Profile-Optimized Recipe (28 nm Node)

**Specification: Sidewall angle ±5°, notch depth <2%, lateral corrosion <30 nm**

```
Parameter                          Value
──────────────────────────────────────────
Pressure                          40 mTorr (balance profile & ARDE)
13.56 MHz Power                   1000 W
Wafer Temperature                 95°C
Gas Mixture                       Cl₂:HCl:BCl₃:Ar = 50:25:12:13 sccm
  ├─ Moderate BCl₃ (12% for notch suppression)
  └─ Ar for ion assist
Chamber Voltage                   -75 V
Etch Time                         50 seconds
```

**Performance measurements:**
- Al etch rate: 220 nm/min
- Sidewall angle: 5-6° ✓ (within spec)
- Notch depth: 8 nm after 50 sec etch (~1.6%) ✓
- Lateral corrosion: 25 nm ✓
- Sidewall roughness: RMS ~3-4 nm ✓

### 7.2 Applied Materials Centura® Advanced Profile Recipe (7 nm Node)

**Demanding spec: Sidewall angle <3°, notch depth <1%, corrosion <15 nm**

```
Parameter                          Value
──────────────────────────────────────────
13.56 MHz Power                   1200 W (higher, for better IAC on sidewalls)
2 MHz Power                       150 W (lower bias, protective)
Pressure                          30 mTorr (lower, prefer vertical profile)
Gas Mixture                       Cl₂:HCl:BCl₃:Ar = 45:20:15:20 sccm
  ├─ Higher BCl₃ (15% for aggressive notch/corrosion suppression)
  └─ Balanced Ar
Wafer Temperature                 90°C
Etch Time                         60 seconds
```

**Performance measurements:**
- Al etch rate: 180 nm/min
- Sidewall angle: 2-3° ✓ (excellent, dual-frequency improves IAC on protected sidewalls)
- Notch depth: 6 nm (~0.7%) ✓ (passivation highly effective)
- Lateral corrosion: 12 nm ✓ (high selectivity prevents spread)
- Sidewall roughness: RMS ~2-3 nm ✓

### 7.3 Profile-Optimized Pulsed Recipe (14 nm Node)

**Time-multiplex to improve profile while maintaining throughput:**

```
Etch cycle (repeating every 30 ms):
1. Etch phase (25 ms):    Cl₂/HCl at 1000 W, 45 mTorr
   ├─ No BCl₃; straight Al etch
   ├─ Creates moderate taper (θ ~ 8-10°)
   └─ Good sidewall IAC

2. Passivation phase (5 ms): Cl₂/BCl₃ at 600 W, 40 mTorr
   ├─ Deposits protective (BCl)_n
   ├─ Suppresses notch growth
   ├─ Anneals sidewall damage from previous etch phase
   └─ Reduces AL etch, increases taper during this phase

Result (time-averaged):
├─ Al etch rate: 230 nm/min
├─ Sidewall angle: 6-7° (averaged between phases)
├─ Notch depth: 2-3% (passivation suppression effective)
└─ Lateral corrosion: 30-40 nm (moderate)
```

**Advantage:** Pulsing self-regulates sidewall angle (alternates between tapered in etch phase and more vertical in passivation phase → average near-optimal).

---

## Part 8: Profile-ARDE-Selectivity Interaction

### 8.1 Three-Way Trade-off Matrix

**All three process targets (ARDE, selectivity, profile) compete for different conditions:**

| Objective | Requires | Pressure | BCl₃ | Power |
|-----------|----------|----------|------|-------|
| **Minimize ARDE** | Low pressure, high power, minimal passivation | 10-20 mTorr | <5% | 1200+ W |
| **Maximize selectivity** | High BCl₃, moderate pressure | 50-70 mTorr | 15-20% | 800-1000 W |
| **Vertical profile** | Low pressure, high IAC | 20-30 mTorr | 10-15% | 1000-1200 W |

**Sweet-spot recipe:** Typically involves 35-50 mTorr, 10-15% BCl₃, 1000-1200 W.

| Node | ARDE Priority | Selectivity Priority | Profile Priority | Practical Recipe |
|---|---|---|---|---|
| **90 nm** | Medium | Low | Low | 50-60 mT, 5% BCl₃ |
| **28 nm** | High | Medium | Medium | 40-45 mT, 10% BCl₃ |
| **7 nm** | High | High | High | 30-35 mT, 15% BCl₃ |

### 8.2 Yield Impact of Profile Defects

**Poor sidewall profile causes downstream failures:**

1. **Thin-film deposition on tapered sidewalls (CVD, ALD):**
   - Tapered trench (θ ~ 15°) → coverage nonuniform
   - Inner edge coverage: ~80% (thin, at risk)
   - Outer edge coverage: ~120% (thick, may overfill)
   - Result: Voids in trench → metal line degradation

2. **CMP (planarization) on notched trenches:**
   - Notch creates stress concentration
   - CMP polish pressure causes dishing (center polishes faster than edges)
   - Result: Final metal thickness nonuniform (±20% variation), fails reliability

3. **Corrosion-induced leakage:**
   - Thinned oxide at edges → higher leakage current
   - Cumulative across 10⁸+ vias → observable leakage signature
   - Yield loss: 0.5-2% (devices fail parametric leakage test)

**Combined yield loss from poor profile:** 2-8% depending on specifications.

---

## Part 9: Advanced Profile Measurement and 3D Reconstruction

### 9.1 FIB-SEM 3D Tomography

**Combines Focused Ion Beam (FIB) slicing with SEM imaging:**

1. FIB serially mills thin slices (10-20 nm thickness)
2. After each slice, SEM images exposed surface
3. Pixel coordinates stacked in 3D → full trench geometry

**3D information extracted:**
- Sidewall angle (can measure per-height along trench)
- Notch shape and volume
- Roughness distribution (identify rough regions)
- Symmetry assessment (left vs. right sidewall)

**Example 3D reconstruction analysis:**

```
3D trench volume data:
├─ Surface area: 2500 nm² (ideal smooth trench)
├─ Actual area: 2650 nm² (+6% from roughness)
├─ Notch volume: 25 nm³
├─ Left sidewall angle: 5.2°
├─ Right sidewall angle: 5.8° (0.6° asymmetry)
└─ Roughness RMS: 3.2 nm
```

**Diagnostics:** Asymmetry could indicate chamber gas distribution issue or RF coupling imbalance (addressable via recipe tuning).

### 9.2 Multibeam CD-SEM for Rapid Profiling

**Emerging technology: CD-SEM with multiple beams at different angles:**

Instead of single top-down view, use multiple angled beams:
- Beam 1 (0°, vertical): Top view of Al (CD)
- Beam 2 (30°, angled): Sidewall slant view (infers angle)
- Beam 3 (45°): Deeper insight into notch region

**Combined information** from multi-angle beams → approximate sidewall angle and notch presence.

**Advantages:** Nondestructive, faster than FIB-SEM, deployable on production tool

**Limitations:** Indirect inference (not direct measurement like cross-section SEM)

---

## Part 10: Profile Specifications and Process Windows

### 10.1 Node-Dependent Sidewall Specifications

**Sidewall angle tolerances tighten with advancing nodes:**

| Node | Min Angle | Nom. Angle | Max Angle | Tolerance | Application Reason |
|---|---|---|---|---|---|
| **90 nm** | 0° | 8° | 15° | ±7° | Liberal (wide pitch allows variation) |
| **28 nm** | 2° | 7° | 12° | ±5° | Tighter (smaller features sensitive) |
| **7 nm** | 1° | 5° | 9° | ±4° | Strict (thin films, CMP sensitive) |
| **5 nm** | 0° | 3° | 6° | ±3° | Extremely strict (minimal margin) |

**Implication:** 5 nm node demands sidewall angle control better than many existing tools' capability (~±3° is challenging).

### 10.2 Notch and Corrosion Specifications

**Allowable defect depths scale with trench depth:**

| Node | Trench Depth | Max Notch Depth | Max Corrosion | Rationale |
|---|---|---|---|---|
| **90 nm** | 800 nm | 80 nm (10%) | 100 nm | Thick trenches tolerate defects |
| **28 nm** | 400 nm | 20 nm (5%) | 40 nm | Intermediate strictness |
| **7 nm** | 150 nm | 10 nm (7%) | 20 nm | Thin trenches less forgiving |
| **5 nm** | 80 nm | 5 nm (6%) | 10 nm | Extreme tightness required |

**Practical limit:** As nodes advance, achieving specifications requires multi-knob optimization (pressure, power, chemistry, pulsing, dual-frequency).

---

## Key Takeaways

1. **Profile is controlled by ion-radical asymmetry:** Ions travel vertically; radicals diffuse isotropically. This creates naturally tapered profiles unless actively corrected.

2. **Notching emerges from interface oxide attack:** Al-oxide interface region is more reactive than bulk oxide. Radicals preferentially attack here, creating notches at ~3-4 nm/min (independent of trench depth).

3. **Passivation is notch-suppressor:** BCl₃ deposits protective (BCl)_n films (~10-20 nm) on sidewalls and interface. Reduces notch growth 10× (from 3-4 nm/min to <0.5 nm/min).

4. **Pressure controls taper angle:** Lower pressure → more vertical sidewalls (θ < 5°). Higher pressure → more tapered (θ > 10°). Trade-off with ARDE (low pressure necessary for vertical profiles conflicts with ARDE requirements).

5. **BCl₃ controls notch and corrosion:** Higher BCl₃ (10-20 sccm) suppresses notch and lateral oxide erosion. Trade-off: Al etch rate reduced 15-30%.

6. **Sidewall angle and ARDE-selectivity compete:** Achieving vertical profile (low pressure) conflicts with ARDE control (needs high pressure). Advanced nodes force compromise recipes.

7. **Profile specification tightens exponentially:** 90 nm allows ±7° angle tolerance; 5 nm requires ±3°. Modern tools struggle to meet 5 nm specs without advanced tuning.

8. **Corrosion extends profile damage beyond notch:** Oxide erodes laterally at feature edges (1-2 μm), thinning dielectric and causing leakage and EM failures.

9. **Microloading affects sidewall angle:** Dense patterns etch more vertically (radicals depleted); sparse patterns taper (abundant radicals). Creates non-uniformity across mixed-density wafers.

10. **Profile yield impact is severe:** Poor sidewalls cause deposition failures (voids), CMP dishing, and leakage. Combined yield loss 2-8% from profile defects, justifying extensive recipe optimization.

---

## References and Further Reading

### Sidewall Profile and Notching Physics
- Donnelly, V. M., et al. (1998). "Etching of aluminum in high-density plasmas." *Journal of Vacuum Science & Technology A*, 16(3), 1699-1715.
- Coburn, J. W., et al. (1991). "Ion-assisted etching of aluminum and aluminum oxide." *Japanese Journal of Applied Physics*, 30(11A), 2958-2964.

### Passivation-Mediated Profile Control
- Lieberman, M. A., & Lichtenberg, A. J. (2005). *Principles of Plasma Discharges and Materials Processing* (2nd ed.). Wiley-Interscience.
- Oehrlein, G. S. (1994). "Etching processes for microelectronics and related applications." *Plasma Science and Technology*, 3(4), 123-150.

### Advanced Profiling and 3D Characterization
- Lam Research. (2022). *3D Profile Reconstruction for Advanced Nodes.* Technical Note.
- Applied Materials. (2023). *Multi-Angle CD-SEM for Real-Time Profile Monitoring.* Process Note.

---

**Next Chapter: Chapter 13 — Temperature Effects & Thermal Coupling**

In Chapter 13, we examine how etch temperature affects process chemistry, plasma properties, and device outcomes. The wafer self-heats during etch due to ion bombardment energy dissipation. How much does wafer temperature rise? How does temperature affect etch rate, selectivity, and profile? What are the trade-offs between thermal control and RF efficiency? We develop thermal models predicting wafer temperature from RF power, gas composition, and chamber design.

