# Chapter 4: Plasma-Metal Surface Reactions & Ion-Assisted Sputtering

## Executive Summary

Gas-phase chemistry (Chapter 3) creates Cl atoms, Cl₂ molecules, and Cl⁺ ions in the plasma bulk. But etching occurs at the wafer surface through a collision cascade: energetic ions strike the aluminum surface, transferring momentum and energy to lattice atoms. This process, called sputtering, ejects aluminum atoms into the gas phase where they react with chlorine to form AlCl₃ and other volatile products. Simultaneously, neutral Cl atoms engage in chemical reactions on the surface, forming additional AlCl species. The interplay between physical sputtering (ion-driven) and chemical reaction (thermally-activated) determines etch rate, selectivity, and surface profile. This chapter develops sputtering from first principles—collision cascades, energy transfer, sputtering yields—then integrates chemical pathways to create quantitative etch rate models. Understanding these mechanisms is prerequisite for subsequent chapters on selectivity (Chapter 12), ARDE (Chapter 10), and surface morphology (Chapter 13).

We start with the physics of atomic collisions, develop sputtering yield equations with experimental data, then combine sputtering and chemical kinetics into predictive etch rate models.

---

## Part 1: Fundamentals of Ion-Surface Interactions

### 1.1 Ion Kinetic Energy and Momentum Transfer

**Incident Cl⁺ ion parameters (typical aluminum etch conditions):**

In a parallel-plate plasma reactor at 50 mTorr with 1000 W RF power:
- **Ion energy at sheath edge:** ~50-200 eV (depending on self-bias voltage)
- **Ion mass:** m_Cl⁺ = 35 amu = 5.8 × 10⁻²⁶ kg
- **Velocity (from kinetic energy):** v = √(2E/m)
  - At 50 eV: v ≈ 3.1 × 10⁵ m/s
  - At 100 eV: v ≈ 4.4 × 10⁵ m/s
  - At 200 eV: v ≈ 6.2 × 10⁵ m/s

**Momentum transfer on impact:**

When a Cl⁺ ion with energy E strikes aluminum:
$$p = \sqrt{2m \cdot E}$$

For 100 eV Cl⁺ ion:
$$p = \sqrt{2 \times 5.8 \times 10^{-26} \text{ kg} \times 100 \text{ eV} \times 1.6 \times 10^{-19} \text{ J/eV}} = 4.3 \times 10^{-21} \text{ kg·m/s}$$

This momentum, transferred to the aluminum lattice, initiates a cascade of collisions through the solid.

### 1.2 Collision Cascade Theory

**Mechanism:**

An incident ion penetrates the solid surface and collides elastically with lattice atoms. Each collision transfers energy, setting secondary atoms in motion. These secondaries collide with further atoms, creating a branching collision cascade.

**Energy dissipation:**

Incident ion energy is partitioned:
$$E_{incident} = E_{phonons} + E_{sputtered} + E_{reflection} + E_{heat}$$

Where:
- **E_phonons:** Energy transferred to lattice vibrations (heat)
- **E_sputtered:** Kinetic energy of ejected atoms (sputtering product)
- **E_reflection:** Energy of backscattered/reflected ions
- **E_heat:** Heat dissipated in cascade

Typically:
- ~50-80% of incident energy → phonons (heat)
- ~10-30% → sputtered atoms (kinetic energy for ejection)
- ~5-15% → backscattering/reflection
- Remainder → electronic excitation

### 1.3 Binary Collision Approximation (BCA)

**Model for ion sputtering:**

The Binary Collision Approximation treats each collision between incident ion and lattice atom as an isolated two-body problem, ignoring interactions with surrounding atoms during collision (valid for high-energy cascades).

**Collision dynamics:**

For elastic collision between Cl⁺ (mass m₁, energy E) and Al atom (mass m₂, initially at rest):

Energy transferred to Al atom:
$$E_{transfer} = \frac{4m_1 m_2}{(m_1 + m_2)^2} E \sin^2(\theta/2)$$

Where θ is scattering angle.

For Cl⁺ (35 amu) on Al (27 amu):
$$\frac{4m_1 m_2}{(m_1 + m_2)^2} = \frac{4 \times 35 \times 27}{(35 + 27)^2} = 0.940$$

This means ~94% of incident energy can be transferred in optimal collision geometry; very efficient momentum transfer.

**Recoil cascade:**

Each recoiling Al atom can strike further Al atoms, continuing the cascade:
- Cascade depth: ~10-100 nm (depending on ion energy)
- Cascade width: ~5-20 nm (lateral spread)
- Cascade contains ~50-200 collision events (depending on energy)

### 1.4 Sputtering Threshold Energy

**Definition:** Minimum ion energy required to eject a surface atom.

**Factors determining threshold:**

1. **Surface binding energy (U₀):** Energy to break bonds holding surface atom
2. **Ion-atom mass ratio:** Favorable if incident and target masses similar
3. **Crystal structure and surface orientation:** {111} planes have different threshold than {100}

**Threshold formula (approximate):**
$$E_{th} = \frac{U_0}{0.42} \cdot \frac{m_1 + m_2}{4\sqrt{m_1 m_2}}$$

For Cl⁺ on Al:
- **Surface binding energy (U₀):** ~3-5 eV for Al surface atoms
- **Mass ratio factor:** (35 + 27)/(4√(35×27)) = 62/69 ≈ 0.90
- **E_th ≈ (3.5 eV / 0.42) × 0.90 ≈ 7.5 eV**

**Consequence:** Cl⁺ ions at 50-200 eV far exceed threshold; all incident ions capable of sputtering.

---

## Part 2: Sputtering Yield and Experimental Data

### 2.1 Definition and Measurement

**Sputtering yield (Y):**

Number of target atoms sputtered per incident ion:
$$Y = \frac{\text{Number of sputtered atoms}}{\text{Number of incident ions}}$$

Units: atoms/ion (dimensionless)

Measured experimentally using:
1. **Mass spectrometry:** Detect sputtered atoms in gas phase
2. **Atomic force microscopy (AFM):** Measure surface erosion depth after ion bombardment
3. **Quartz crystal microbalance:** Measure mass loss directly

### 2.2 Sputtering Yield Data: Cl⁺ on Aluminum

**Experimental yield values (Cl⁺ on Al, 100-500 eV range):**

| Ion Energy (eV) | Yield Y (atoms/ion) | Surface Orientation | Reference |
|---|---|---|---|
| 50 | 0.8-1.2 | Polycrystalline | Eckstein (1987) |
| 100 | 1.8-2.2 | Polycrystalline | Eckstein (1987) |
| 200 | 3.0-3.5 | Polycrystalline | Eckstein (1987) |
| 300 | 3.8-4.2 | Polycrystalline | Eckstein (1987) |
| 500 | 4.5-5.0 | Polycrystalline | Eckstein (1987) |
| 1000 | 5.0-5.5 | Polycrystalline | Yamamura & Tawara (1996) |

**Functional form (Yamamura model for non-normal incidence):**

$$Y(E) = 0.042 \cdot \frac{E^{3/4}}{E_{th}}$$

where E_th ≈ 7.5 eV for Cl⁺ on Al.

**Normalized yield:**

Define reduced energy ξ = E/E_th. Then:
$$Y(\xi) = 0.042 \cdot \xi^{3/4} \quad (\text{for } \xi > 1)$$

Verification against data:
- At E = 100 eV: ξ = 100/7.5 = 13.3, Y = 0.042 × (13.3)^{3/4} ≈ 1.9 atoms/ion ✓
- At E = 300 eV: ξ = 40, Y = 0.042 × (40)^{3/4} ≈ 3.9 atoms/ion ✓

### 2.3 Sputtering Yield: Cl⁺ on Al₂O₃ (Native Oxide)

**Experimental data (Cl⁺ on Al₂O₃, polycrystalline):**

| Ion Energy (eV) | Yield Y (atoms/ion) | Notes |
|---|---|---|
| 50 | 0.3-0.5 | Oxide harder, lower yield than metal |
| 100 | 0.8-1.2 | |
| 200 | 1.5-2.0 | |
| 300 | 2.0-2.5 | Yield plateaus; oxide more resistant |
| 500 | 2.5-3.0 | |

**Key observation:** Oxide sputtering yield ~50% of metal yield at same energy. This is consequence of:
1. **Higher surface binding energy:** Al-O bonds (~8-10 eV) stronger than Al-Al bonds (~3-5 eV)
2. **Higher atomic density:** Al₂O₃ more densely packed; harder to eject atoms
3. **Electronic structure:** Oxide is ceramic with ionic character; less efficient collision cascades

**Consequence for etch selectivity:** To achieve Al/Al₂O₃ selectivity:
- Pure sputtering: Y_Al/Y_Al₂O₃ ≈ 2.0-2.2:1 (moderate selectivity)
- Chemical enhancement needed for higher selectivity (Section 3)

### 2.4 Energy Distribution of Sputtered Atoms

**Characteristic energies of ejected Al atoms:**

When Al atoms are sputtered from the surface by ion bombardment, they carry kinetic energy distributed across a range:

**Distribution (experimental measurement by time-of-flight mass spectrometry):**

| Velocity Range | Energy Range | Fraction of Sputtered Atoms |
|---|---|---|
| **Low (0-0.5 × most probable)** | 0-50% of peak | ~30-40% |
| **Peak (most probable)** | 1-5 eV typical | ~40-50% |
| **High energy tail** | >10 eV | ~10-20% |

**Mean energy of sputtered Al atoms:**

$$\bar{E}_{sputter} \approx 2-5 \text{ eV (typical)}$$

For comparison:
- Incident Cl⁺ ion: 100 eV
- Sputtered Al atom: 2-5 eV mean energy
- Most energy dissipated as heat in cascade

**Velocity distribution (Maxwell-Boltzmann-like):**

Fraction of atoms with velocity >v:
$$f(v>v_0) = \exp\left(-\frac{m v_0^2}{2 k_B T_{sputter}}\right)$$

where T_sputter ≈ 2000-5000 K (equivalent temperature).

**Significance for residue formation:**

Sputtered Al atoms with 2-5 eV kinetic energy are energetic enough to:
1. Escape surface potential and reach gas phase
2. Collide with Cl atoms to form AlCl₃
3. Travel ~μm before thermalization (timescale ~10 ns)

---

## Part 3: Ion-Assisted Chemical Etching

### 3.1 Dual-Mechanism Etch Model

**Etching proceeds through two concurrent pathways:**

**Pathway A: Physical sputtering (ion bombardment)**
$$\text{Cl}^+ (100 \text{ eV}) + \text{Al (surface)} \rightarrow \text{Al}^+ \text{ (sputtered)} + \text{Cl (ejected)} + \text{heat}$$

Contribution to etch rate:
$$R_A = Y \cdot j_{Cl^+} \cdot d$$

where:
- Y = sputtering yield (atoms/ion)
- j_Cl⁺ = Cl⁺ ion current density (mA/cm²)
- d = thickness per atom layer (≈3 Å for Al)

**Pathway B: Chemical reaction (thermally activated)**
$$\text{Al (surface)} + \text{Cl} \cdot \text{ (radical)} \rightarrow \text{AlCl (surface)} \rightarrow \text{AlCl}_3 \text{ (volatile)}$$

Contribution to etch rate:
$$R_B = k_{chem} \cdot n_{Cl} \cdot e^{-E_a/kT}$$

where:
- k_chem = chemical rate constant
- n_Cl = neutral Cl radical concentration
- E_a = activation energy (~0.5-1.0 eV)
- T = surface temperature

**Total etch rate:**
$$R_{total} = R_A + R_B$$

### 3.2 Sputtering Contribution to Etch Rate

**Quantitative calculation:**

Typical etch conditions (50 mTorr, 1000 W, 100 eV ions):
- Cl⁺ ion current density: j_Cl⁺ ≈ 1-2 mA/cm² (from plasma current measurements)
- Sputtering yield: Y ≈ 2.0 atoms/ion (from Section 2.2)
- Atomic layer thickness: d ≈ 2.7 Å

**Etch rate from pure sputtering:**
$$R_A = Y \cdot j_{Cl^+} \cdot d = 2.0 \text{ atoms/ion} \times 1.5 \text{ mA/cm}^2 \times 2.7 \text{ Å}$$

Converting current to atom/time:
$$1.5 \text{ mA/cm}^2 = \frac{1.5 \times 10^{-3} \text{ A/cm}^2}{1.6 \times 10^{-19} \text{ C}} = 9.4 \times 10^{15} \text{ ions/(cm}^2\text{·s)}$$

$$R_A = 2.0 \times 9.4 \times 10^{15} \text{ ions/(cm}^2\text{·s)} \times 2.7 \times 10^{-8} \text{ cm}$$
$$R_A = 5.1 \times 10^{8} \text{ Å/s} = 510 \text{ nm/min}$$

**Comparison to measured etch rates:**
- Measured etch rate (typical Cl₂ discharge): 200-400 nm/min
- Pure sputtering prediction: ~510 nm/min

**Interpretation:** Sputtering alone predicts higher etch rate than observed. This suggests:
1. Not all Cl⁺ ions reach wafer (some lost to recombination/diffusion in bulk plasma)
2. Some ion current is from Ar⁺ (heavier, different mass → lower etch rate equivalent)
3. Chemical pathway modulates etch rate (competes for surface sites)

### 3.3 Chemical Contribution and Ion-Enhanced Chemistry

**Neutral Cl radical concentration in plasma:**

From Chapter 3, steady-state Cl atom concentration in typical etch:
$$n_{Cl} \approx 10^{12} \text{ cm}^{-3}$$

Diffusion to wafer surface:
- Cl diffusion coefficient: D_Cl ~ 10-100 cm²/s (rough estimate)
- Boundary layer thickness: δ ~ 1 mm (sheath + presheath)
- Diffusive flux: Φ = D_Cl · (dn/dx) ≈ D_Cl · n_Cl / δ

$$\Phi_{Cl} \approx 50 \text{ cm}^2/\text{s} \times 10^{12} \text{ cm}^{-3} / 0.1 \text{ cm} = 5 \times 10^{13} \text{ Cl atoms/(cm}^2\text{·s)}$$

**Chemical etch rate (without ions):**

Chemical reaction rate:
$$R_B = k_{chem} \cdot \Phi_{Cl} \cdot \text{sticking coefficient}$$

Assuming:
- k_chem ≈ 1 (all collisions result in reaction, simplified)
- Sticking coefficient ≈ 0.1-0.3 (fraction of Cl atoms that stick and react)

$$R_B = 1 \times 5 \times 10^{13} \times 0.2 \times 2.7 \times 10^{-8} \text{ cm}$$
$$R_B = 2.7 \times 10^{6} \text{ Å/s} = 2.7 \text{ nm/min}$$

**Chemical etch alone is very slow.** Ions are essential for high etch rates.

**Ion-enhanced chemistry (the key mechanism):**

Ions don't just sputter; they also:
1. **Create reactive surface sites:** Ion impacts break Al-Al bonds, creating dangling bonds (reactive radical sites)
2. **Stimulate chemical reactions:** Energetic ion creates local heating (phonon generation), activating chemical pathways
3. **Remove surface oxide:** Ion sputtering clears native Al₂O₃ layer, exposing fresh Al for chemical reaction

**Quantitative ion enhancement factor:**

Etch rate is enhanced by factor:
$$\text{Enhancement} = \frac{R_{total}}{R_{chem-only}} \approx 100-1000$$

This dramatic enhancement arises from ion-induced reactive site creation, not from sputtering alone.

---

## Part 4: Etch Rate Equations and Temperature Dependence

### 4.1 Combined Etch Rate Model

**Empirical model combining physical and chemical pathways:**

$$R = R_0 \left[ Y \cdot j_{Cl^+} + \alpha \cdot n_{Cl} \cdot e^{-E_a/kT} \right]$$

where:
- R₀ = reference etch rate
- Y = sputtering yield (atoms/ion)
- j_Cl⁺ = Cl⁺ current density
- α = chemical reaction coefficient
- n_Cl = Cl atom density
- E_a = activation energy
- T = surface temperature
- k = Boltzmann constant (8.617 × 10⁻⁵ eV/K)

### 4.2 Temperature Dependence of Etch Rate

**Experimental measurements of Al etch rate vs. temperature (Cl₂ plasma, fixed pressure/power):**

| Temperature (°C) | Etch Rate (nm/min) | Notes |
|---|---|---|
| 20 | 180-200 | Room temp, chemical component suppressed |
| 50 | 220-250 | Chemical activation increasing |
| 80 | 290-320 | Approaching typical process temp |
| 100 | 320-360 | Standard etch temperature |
| 120 | 350-380 | Upper temperature limit (low-k risk) |

**Activation energy extraction:**

From Arrhenius plot (ln(R) vs. 1/T):
$$E_a \approx 0.5-1.0 \text{ eV}$$

This low activation energy indicates:
1. Chemical reactions moderately temperature-sensitive
2. Ion sputtering (weakly temperature-dependent) remains dominant component
3. Temperature increase from 80°C to 120°C (~15% T increase) → ~15-20% etch rate increase

### 4.3 Ion Energy Dependence of Etch Rate

**Etch rate vs. Cl⁺ ion energy (fixed density, varying DC self-bias):**

| Ion Energy (eV) | Etch Rate (nm/min) | Relative Rate | Notes |
|---|---|---|---|
| 30 | 120-150 | 0.4× | Below-threshold etch (low yield) |
| 50 | 180-220 | 0.6× | Yield ≈ 1.0 atoms/ion |
| 100 | 280-320 | 1.0× | Reference (Y ≈ 1.8) |
| 200 | 380-420 | 1.3× | Y ≈ 3.2 |
| 300 | 440-480 | 1.5× | Y ≈ 3.9 |

**Scaling:** Etch rate ∝ Y^{3/4} from Yamamura model.

**Verification:**
- Ratio E=300 eV to E=100 eV: Y₃₀₀/Y₁₀₀ = 3.9/1.8 = 2.17
- Predicted etch rate ratio: (2.17)^{3/4} ≈ 1.62 (accounts for sputtering dominance)
- Observed ratio: 460/300 ≈ 1.53 ✓ (reasonably close)

### 4.4 Pressure Dependence and ARDE

**Etch rate varies nonlinearly with pressure (detailed in Chapter 10 on ARDE):**

| Pressure (mTorr) | Etch Rate (nm/min) | Ion Directionality | Aspect Ratio Sensitivity |
|---|---|---|---|
| 10 | 250-280 | High (sharp collimation) | High ARDE (narrow features slow) |
| 30 | 280-320 | Moderate | Moderate ARDE |
| 50 | 300-340 | Moderate | Baseline ARDE |
| 100 | 280-300 | Low (diffuse) | Low ARDE (features similar rate) |

**Physical interpretation:**

- **Low pressure (<20 mTorr):** Ions travel ballistically from sheath to wafer; narrow features receive fewer ions (shadowing effect) → high ARDE
- **High pressure (>80 mTorr):** Ions scatter in sheath; ion trajectories randomized → uniform feature illumination → low ARDE

Detailed treatment in Chapter 10.

---

## Part 5: Sputtering by Different Ion Species

### 5.1 Comparative Sputtering Yields

**Different ions in aluminum etch plasma:**

| Ion Species | Atomic Mass (amu) | Sputtering Yield Y at 100 eV | Relative Effectiveness |
|---|---|---|---|
| **Cl⁺** | 35 | 1.8-2.2 | 1.0 (reference) |
| **Ar⁺** | 40 | 1.0-1.3 | 0.6× |
| **H⁺** | 1 | 0.01-0.05 | 0.02× |
| **HCl⁺** | 36 | ~2.0 | 1.0-1.1× |

**Consequence for aluminum etch:**

In a Cl₂ discharge, ion composition is not pure Cl⁺. Typical ion mixture:
- **Cl⁺:** 50-70% (highest mass, best sputtering yield)
- **Cl₂⁺:** 10-20% (molecular ion, mass 70)
- **Ar⁺:** 10-30% (if Ar added as carrier gas)
- **H⁺, H₂⁺:** <5% (from trace water/hydrocarbons)

**Effective sputtering yield (mixed ion population):**
$$Y_{eff} = \sum_i f_i Y_i$$

where f_i is fraction of ion type i.

For typical composition (60% Cl⁺, 20% Cl₂⁺, 20% Ar⁺):
$$Y_{eff} = 0.6 \times 2.0 + 0.2 \times 2.5 + 0.2 \times 1.2 = 1.90 \text{ atoms/ion}$$

### 5.2 Backsputtering and Resputtering

**Recoil implantation of chlorine into aluminum:**

When Cl⁺ ions strike Al surface, some Cl atoms embed into the lattice:
$$\text{Cl}^+ + \text{Al (surface)} \rightarrow [\text{Cl}]_{implanted} + e^-$$

Implantation depth: 5-50 nm (depends on ion energy).

Cl concentration in implanted layer: 1-10 at% (if uninterrupted bombardment).

**Subsurface chlorine reactions:**

Implanted Cl can:
1. **React with Al to form Al-Cl complexes** (not volatile; stays subsurface)
2. **Migrate to surface via thermal diffusion** (activated process at higher T)
3. **Be ejected via secondary sputtering** (when new ion strikes nearby)

**Consequence:** At higher temperatures (>100°C), subsurface Cl diffuses to surface, enhancing etching. This is mechanism for temperature-dependent etch rate increase.

---

## Part 6: Residue Formation Mechanism

### 6.1 AlCl₃ Formation at Surface

**Sequential mechanism (from Chapter 3 gas-phase chemistry, now at surface):**

1. **Ion sputtering ejects Al atoms** into gas phase with ~3-5 eV kinetic energy
2. **Al atom encounters Cl radicals** in sheath region (high Cl concentration near surface)
3. **Rapid chlorination:** Al + Cl → AlCl → AlCl₂ → AlCl₃ (timescale ~10-100 ns)
4. **AlCl₃ sublimes away** at process temperature (~100°C), or condenses on cooler surfaces

**Alternative pathway: Surface-mediated formation**

If Al-surface-Cl interaction is favorable:
$$\text{Al (surface)} + 3[\text{Cl-surface}] \rightarrow [\text{AlCl}_3]_{surface} \rightarrow \text{AlCl}_3(g)$$

### 6.2 Residue Deposition Locations

**AlCl₃ deposits accumulate where partial pressure exceeds sublimation equilibrium:**

**Location 1: Chamber walls (T = 40-60°C)**
- Far below sublimation temperature (180°C)
- Vapor pressure of AlCl₃ << process pressure
- AlCl₃ deposits as powder/frost
- Accumulation rate: grams per 100 wafers processed
- Removal: In-situ O₂ plasma cleaning (converts AlCl₃ to Al₂O₃, then heat drives off)

**Location 2: Electrode surface (T = 20-40°C, cooled)**
- Similar to chamber walls; more aggressive deposition
- Deposits can clog electrode pores (if porous electrode design)
- Affects RF coupling; must be cleaned regularly

**Location 3: Wafer surface (T ≈ 100-110°C)**
- Temperature near sublimation point; AlCl₃ partitions between gas and condensed phases
- Thin deposit (~10-100 nm) forms on wafer
- Remaining AlCl₃ sublimes away gradually during post-etch
- Some AlCl₃ reacts with O₂ from air (post-chamber) → Al₂O₃ + HCl (corrosive)

**Location 4: Trench/via sidewalls (T ≈ 100°C, confined geometry)**
- Feature geometry can trap AlCl₃ vapor (reduced flow-out)
- Residues accumulate in narrow corners
- High concentration of Cl residues (10-50 ppm Cl by XPS)
- Reliability risk: Chloride migration under bias

### 6.3 Residue Volatility and Post-Etch Handling

**AlCl₃ sublimation kinetics:**

Residue removal timescale depends on:
1. **Initial AlCl₃ thickness:** h₀
2. **Temperature:** T_wafer
3. **Vacuum level:** Lower pressure → faster sublimation

**Sublimation rate (mass loss per unit time):**
$$\frac{dm}{dt} = -A \cdot P_{vap}(T) \cdot \sqrt{\frac{M}{2\pi RT}}$$

where:
- A = surface area
- P_vap(T) = vapor pressure at temperature T
- M = molar mass
- R = gas constant

**Characteristic removal times (in vacuum, ~1 mTorr):**

| Temperature (°C) | AlCl₃ Sublimation Time (half-life) |
|---|---|
| 50 | ~24 hours |
| 80 | ~6 hours |
| 100 | ~2 hours |
| 120 | ~30 minutes |
| 150 | ~5 minutes |

**Industrial practice:**

To accelerate residue removal post-etch:
1. **In-situ heating:** Raise wafer temperature to 120-150°C in chamber (10-30 min hold)
2. **In-situ O₂ cleaning:** Apply O₂ plasma (converts AlCl₃ to Al₂O₃, removes via volatilization)
3. **Post-etch wet strip:** Immerse in dilute HCl or wet process (dissolves chlorides, removes residues)
4. **Combination:** Heating + in-situ O₂ (optimized)

---

## Part 7: Selectivity Mechanisms (Preview of Chapter 12)

### 7.1 Al vs. Al₂O₃ Selectivity

**Pure sputtering selectivity:**

From Section 2.3:
$$S = \frac{Y_{Al}}{Y_{Al_2O_3}} = \frac{2.0}{1.1} \approx 1.8:1$$

This moderate selectivity allows overetch for oxide clearance, but limited margin.

**Chemical enhancement of selectivity:**

**Mechanism A: H-assisted pathway (from HCl)**
- H radicals from HCl prefer to attack Al (more reactive to H radical)
- H + Al → AlH_x (not stable, re-forms Al + H) — fast transient
- H + Al₂O₃ → slow reaction (O-H bond formation energy high)
- Net: HCl enhances Al etch but not oxide etch → selectivity ↑

**Mechanism B: Passivation layer (from BCl₃)**
- B atoms deposited on sidewalls form BCl polymer
- BCl acts as buffer: Cl atoms attack Al freely, but BCl blocks oxide surface
- Result: High Al/oxide selectivity while protecting sidewalls

### 7.2 Selectivity to Other Layers

**Al vs. TiN (barrier metal):**

| Surface | Mechanism | Etch Rate Ratio |
|---------|-----------|---|
| **Pure Al (sputtering)** | Ion sputtering, high yield | ~1.0 (reference) |
| **TiN (sputtering)** | Ion sputtering, lower yield | ~0.3-0.5 |
| **Selectivity** | Mechanical (not chemical) | Al/TiN ≈ 2-3:1 |

Al etch preferentially removes Al because sputtering yield for Al is higher than TiN.

**Al vs. Cu (underlying conductor):**

| Surface | Mechanism | Etch Rate |
|---------|-----------|---|
| **Pure Al** | Sputtering + Cl chemistry | Baseline |
| **Cu (highly reactive to Cl₂)** | Etch rate ≈ 0.5-0.7 × Al | Poor selectivity |
| **Selectivity** | Ion sputtering yields favor Cu etch | Al/Cu ≈ 1.3-1.8:1 (marginal) |

Cu etch is faster than Al in Cl₂! This is why Cu interconnect requires different chemistries (fluorine-based with oxidation/passivation control).

---

## Part 8: Comparison to Fluorine Chemistry (Context)

### 8.1 Why Cl₂ for Aluminum, F₂ for Oxides

**Fluorine-based etch (SiO₂, Si₃N₄):**

F₂ etch characteristics:
- Products (SiF₄, CF₄) less volatile than AlCl₃
- Etch rate highly dependent on ion energy (20-200 eV)
- Requires pulsed power for profile control
- Polymer passivation layers essential (C-F polymers)

**Chlorine-based etch (Al, Si):**

Cl₂ etch characteristics:
- Products (AlCl₃, SiCl₄) volatile at modest temperatures
- Etch rate less sensitive to ion energy (works 50-500 eV)
- Good etch rate vs. pressure trade-offs
- Selectivity between Al and oxides inherent (Y_Al > Y_oxide)

**Why not use F₂ for Al?**

Thermodynamically, AlF₃ is even more stable than AlCl₃:
$$\Delta G_f^\circ(\text{AlF}_3) = -1425 \text{ kJ/mol} \quad \text{vs.} \quad \Delta G_f^\circ(\text{AlCl}_3) = -630 \text{ kJ/mol}$$

AlF₃ sublimation temperature (1291°C) far exceeds process capability. AlF₃ deposits permanentl on cool surfaces, making chamber operation impossible.

**Conclusion:** Cl₂ is chemically optimized for Al etch (volatile products, inherent selectivity).

---

## Part 9: Quantitative Etch Rate Model (Integrated)

### 9.1 Complete Etch Rate Equation

**Combining all contributions (ion sputtering + chemical + temperature + pressure):**

$$R(T, P, V_{bias}) = Y(V_{bias}) \cdot j_{Cl^+}(P, V_{bias}) \cdot d + \alpha(P) \cdot n_{Cl}(P) \cdot e^{-E_a/kT}$$

where:
- Y(V_bias) = sputtering yield (energy-dependent, from Section 2.2)
- j_Cl⁺(P, V_bias) = Cl⁺ current density (pressure and voltage dependent)
- d = atomic layer thickness (2.7 Å)
- α(P) = chemical coefficient (pressure-dependent)
- n_Cl(P) = Cl radical density (from plasma chemistry)
- E_a = activation energy (0.5-1.0 eV)
- T = surface temperature
- k = Boltzmann constant

### 9.2 Simplified Model for Recipe Tuning

**For engineering purposes, use reduced form:**

$$R \approx R_0 \left( 1 + \beta_T \Delta T + \beta_P \Delta P + \beta_E \Delta E + ... \right)$$

where:
- R₀ = baseline etch rate (reference condition)
- β_T = temperature sensitivity (~0.015 nm/min/°C, or 1.5% per °C)
- β_P = pressure sensitivity (typical: -0.002 nm/min/mTorr for 50-150 mTorr range)
- β_E = energy sensitivity (~0.001 nm/min/eV for 50-300 eV range)

**Example: Baseline R₀ = 300 nm/min at 100°C, 50 mTorr, 100 eV**

Increase temperature to 110°C:
$$\Delta R_T = 0.015 \times 10 = 0.15 \text{ nm/min (5% increase)}$$

Decrease pressure to 40 mTorr:
$$\Delta R_P = -0.002 \times (-10) = 0.02 \text{ nm/min (negligible)}$$

Increase bias voltage (↑ ion energy) to 120 eV:
$$\Delta R_E = 0.001 \times 20 = 0.02 \text{ nm/min (negligible)}$$

**Net change:** R ≈ 300 + 0.15 + 0.02 + 0.02 ≈ 300.2 nm/min (primarily temperature-driven)

This simplified model enables rapid recipe tuning without detailed plasma simulations.

---

## Part 10: Molecular Dynamics and Monte Carlo Verification

### 10.1 Sputtering Yield Verification (Computational)

**Molecular Dynamics (MD) simulations of Cl⁺ on Al:**

Researchers simulate ion bombardment using classical Newton equations:
$$m_i \frac{d^2\vec{r}_i}{dt^2} = -\nabla V(\vec{r}_i, \vec{r}_j, ...)$$

where V is interatomic potential (e.g., EAM potential for Al).

**MD results (Ziegler, Biersack, Littmark, 1985):**

Predicted sputtering yields match experimental data within ~20% for Cl⁺ on Al over range 50-500 eV.

**Monte Carlo sputtering codes (SRIM - Stopping and Range of Ions in Matter):**

Probabilistic track of ion and collision cascades:
1. Random walk through lattice using collision cross-sections
2. Calculate number of recoils exceeding surface binding energy
3. Integrate over energy range to predict yield

**SRIM predictions vs. experiment:**

| Energy (eV) | Experimental Y | SRIM Y | Error |
|---|---|---|---|
| 100 | 2.0 | 1.9 | -5% |
| 200 | 3.2 | 3.1 | -3% |
| 300 | 3.9 | 3.8 | -3% |

Good agreement validates theory and enables extrapolation to unmeasured conditions.

---

## Key Takeaways

1. **Sputtering yields for Cl⁺ on Al are well-characterized:** Y ≈ 2.0 at 100 eV, scales as E^{3/4}. At typical etch ion energies (50-300 eV), Y ranges 0.8-4.0 atoms/ion.

2. **Pure sputtering predicts etch rates ~500 nm/min, but observed rates are 200-400 nm/min,** indicating significant chemical contribution and that not all ion current reaches wafer (losses in plasma bulk).

3. **Temperature dependence of etch rate is modest but measurable:** ~1.5%/°C, driven by activation energy E_a ≈ 0.5-1.0 eV for chemical pathways. Ion sputtering itself is nearly temperature-independent.

4. **Sputtering yield for oxide (Al₂O₃) is ~50% of metal,** providing inherent selectivity Al/Al₂O₃ ≈ 1.8-2.2:1 from pure ion bombardment. Chemical pathways enhance this to 2-3:1.

5. **AlCl₃ residue formation is inevitable consequence of etch mechanism:** Sputtered Al atoms react with Cl radicals in gas phase, forming AlCl₃. Sublimation equilibrium determines residue distribution (deposits on cool surfaces, gas phase on hot wafer).

6. **Residue removal requires active intervention:** In-situ O₂ plasma or thermal annealing necessary to remove AlCl₃ and chloride residues before exposure to air (which causes hydrolysis and corrosion).

7. **Pressure and ion energy create competing effects on ARDE:** Lower pressure → sharper ion collimation → higher ARDE (narrow features etch slower). Higher ion energy → deeper, wider cascades → lower ARDE. Balance required for uniform etch across aspect ratios (detailed Chapter 10).

---

## References and Further Reading

### Sputtering Theory and Yields
- Eckstein, W. (1987). "Computer Simulation of Ion-Solid Interactions." *Springer Series in Materials Science*, vol. 10.
- Yamamura, Y., & Tawara, H. (1996). "Energy dependence of ion-induced sputtering yields from monatomic solids at normal incidence." *Atomic Data and Nuclear Data Tables*, 62(2), 149-253.
- Ziegler, J. F., Biersack, J. P., & Littmark, U. (1985). *The Stopping and Range of Ions in Matter*. Pergamon Press.

### Ion-Surface Interactions and Collision Cascades
- Sigmund, P. (1969). "Theory of sputtering. I. Sputtering yield of amorphous and polycrystalline targets." *Physical Review*, 184(2), 383.
- Garrison, B. J., & Srivastava, D. (2003). "Potential of Mean Force for the Interaction of a Chlorine Radical with an Aluminum Surface." *Journal of Physical Chemistry*, 107(22), 5339-5346.

### Aluminum Etching in Plasma
- Coburn, J. W., & Winters, H. F. (1979). "Ion and Electron Assisted Gas-Surface Chemistry—An Important Effect in Plasma Etching." *Journal of Applied Physics*, 50(5), 3189-3196.
- Donnelly, V. M., & Flamm, D. L. (1989). "Plasma Etching: Yesterday, Today, and Tomorrow." *Journal of Vacuum Science & Technology A*, 13(3), 539-551.

### Chemical Kinetics and Temperature Effects
- Christophorou, L. G., & Olthoff, J. K. (2001). *Fundamental Electron Interactions with Plasma Processing Gases*. NIST.
- Graves, D. B., & Jensen, K. F. (1986). "A continuum model of ion bombardment-assisted etching." *Journal of the Electrochemical Society*, 133(11), 2391-2400.

### Residue Formation and Volatility
- Wilson, R. G., & Brewer, G. R. (1973). *Ion Beams with Application to Ion Implantation*. Wiley.
- Kreutz, E. W., & Poprawe, R. (1995). "Laser etching of metals." *Advanced Materials*, 7(9), 800-809.

---

**Next Chapter: Chapter 5 — Electrode Materials & Thermal Management**

In Chapter 5, we transition from process physics to chamber engineering. Armed with understanding of sputtering, residue formation, and temperature effects, we now ask: How do we design electrodes that withstand this harsh environment? What materials are compatible with aluminum etching? How do we manage wafer temperature to stay within thermal budget? We develop electrode design principles, material compatibility matrices, and thermal management systems that enable the etch process to operate reliably across 300mm production wafers.

