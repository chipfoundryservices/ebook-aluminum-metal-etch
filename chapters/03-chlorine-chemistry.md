# Chapter 3: Chlorine Chemistry in Aluminum Plasma (Cl₂, HCl, CCl₄)

## Executive Summary

Aluminum etching in semiconductor manufacturing relies fundamentally on chlorine-based chemistry. Unlike fluorine-based etch (used for silicon oxides and nitrides, with energy cost-dependent rate control), chlorine-aluminum interactions produce volatile products (AlCl₃) that sublime away, enabling high etch rates and excellent selectivity. This chapter develops the gas-phase chemistry rigorously: How does Cl₂ dissociate in low-temperature plasma? What reactions form AlCl₃ and other chlorine-aluminum species? How do different chlorine sources (Cl₂, HCl, CCl₄, BCl₃) modify reaction pathways? What thermodynamic and kinetic constraints apply? Understanding this chemistry is prerequisite for understanding surface etch mechanisms (Chapter 4) and designing process recipes that control selectivity and residue formation.

We start from electron-impact dissociation of Cl₂, develop reaction pathways, quantify rate coefficients, and conclude with industrial implications for gas mixture selection and process tuning.

---

## Part 1: Chlorine Fundamentals and Plasma Dissociation

### 1.1 Chlorine Chemistry: Electronic Structure and Oxidation States

**Chlorine (Cl) in the periodic table:**
- Atomic number: 17
- Electron configuration: [Ne] 3s² 3p⁵
- Valence: -1 (typical), 0, +1, +3, +5, +7 (possible oxidation states)
- Group VIIA (halogen)
- Period 3 (same period as Al and Si)

**Valence chemistry:**
Chlorine has five p-orbital electrons; it seeks one more electron to complete the 3p⁶ octet, resulting in Cl⁻ (formal charge -1).

In molecules and reactions:
- **Cl₂:** Two Cl atoms bonded; each has formal oxidation state 0
- **Cl⁻:** Chloride ion; oxidation state -1 (gained one electron)
- **Cl⁺:** Chlorine cation; oxidation state +1 (lost one electron; high energy)
- **Radical Cl·:** Single Cl atom with unpaired p electron; highly reactive
- **Excited Cl*:** Cl atom in excited electronic state (Cl*); also highly reactive

**Reactivity hierarchy:**
Most to least reactive in plasma:
1. **Cl⁺ ions** — Highly energetic (50-200 eV kinetic energy), direct sputtering mechanism
2. **Cl· radicals** — Neutral atoms with unpaired electron, energetic (1-5 eV thermal energy)
3. **Cl₂ molecules** — Ground state, relatively stable, require activation
4. **Cl⁻ anions** — Rarely important in Cl₂ plasmas (electron affinity low)

**Bond dissociation energy:**
$$D_0(\text{Cl-Cl}) = 2.51 \text{ eV} = 244 \text{ kJ/mol}$$

This bond energy sets the threshold for dissociation: electrons with kinetic energy >2.51 eV can break Cl₂ into two Cl atoms.

### 1.2 Electron-Impact Dissociation of Cl₂

**Mechanism:**
An energetic electron (E > 2.51 eV) collides with a Cl₂ molecule. If the collision imparts sufficient energy to the Cl-Cl bond, the molecule breaks:

$$e^- + \text{Cl}_2 \rightarrow \text{Cl} + \text{Cl} + e^-$$

(Inelastic collision; electron loses energy ≥ 2.51 eV)

**Cross-section data:**

Electron-impact dissociation cross-section σ(E) is measured experimentally and tabulated. For Cl₂:

| Electron Energy (eV) | σ (10⁻¹⁶ cm²) | Notes |
|---|---|---|
| 2.5 | ~0.1 | Threshold; weak cross-section |
| 5.0 | ~2.0 | Energy above threshold |
| 10 | ~5.5 | Intermediate energy |
| 20 | ~8.2 | Higher energy (typical in CCP) |
| 50 | ~6.5 | Very energetic (ICP regime) |
| 100 | ~4.0 | High-energy electrons (less efficient) |

**Key observation:** Cross-section peaks around 20-30 eV (highest probability of dissociation), then decreases at higher energies. This means:
- Low-energy electrons (2-5 eV): Inefficient dissociation
- Optimal energy (20-30 eV): Maximum dissociation per electron
- Very high-energy electrons (>100 eV): Lower probability (energy "wasted" in fast, hard collisions)

**Electron energy distribution in plasma:**

In a typical CCP (capacitive coupled plasma) aluminum etch reactor:
- Electron temperature: Te ~ 2-5 eV (depending on power, pressure, gas)
- Electron distribution: Maxwellian-like (peak at ~0.5-1 eV thermal, high-energy tail to 20-50 eV)
- Mean energy: <E> ≈ 3/2 · Te ~ 3-7.5 eV (center of distribution)

**Rate coefficient for electron-impact dissociation:**

Combining cross-section σ(E) with electron velocity distribution n(E):

$$k_{e-impact} = \int_0^\infty \sigma(E) \cdot v(E) \cdot f(E) \, dE$$

where v(E) is electron velocity and f(E) is energy distribution.

Experimentally measured or calculated rate coefficients:

| Electron Temperature Te (eV) | Rate Coefficient (cm³/s) | Reference |
|---|---|---|
| 1 | ~1×10⁻⁹ | Boundary case (slow dissociation) |
| 2 | ~5×10⁻⁹ | Low-power plasma |
| 3 | ~8×10⁻⁹ | Typical CCP etch |
| 5 | ~1.2×10⁻⁸ | High-power CCP |
| 10 | ~1.5×10⁻⁸ | Low-pressure/high-power limit |

**Consequence for aluminum etch:** In typical etch conditions (Te ~ 2-5 eV, Cl₂ partial pressure ~ 5-50 mTorr):
- Cl₂ dissociation rate: fast (timescale ~10-100 ms for typical ion dwell time in plasma bulk)
- Most Cl₂ converted to Cl atoms/ions within the plasma
- Downstream: Flow toward wafer contains ~20-60% Cl atoms, ~20-40% Cl₂ (depending on degree of dissociation and pressure)

### 1.3 Dissociation Pathways: Direct Dissociation vs. Step-wise

**Pathway A: Direct dissociation (one-step)**
$$e^- + \text{Cl}_2 \rightarrow 2\text{Cl} + e^-$$

Cross-section: σ ≈ 5-8 × 10⁻¹⁶ cm² (direct channel, ~10-20 eV electrons)

**Pathway B: Step-wise dissociation (indirect)**
$$e^- + \text{Cl}_2 \rightarrow \text{Cl}_2^* + e^- \quad \text{(excitation to excited state)}$$
$$\text{Cl}_2^* \rightarrow 2\text{Cl} \quad \text{(radiative or collisional decay)}$$

Cross-section: σ ≈ 2-3 × 10⁻¹⁶ cm² (excitation channel)

**Both pathways contribute** to total dissociation; combined rate coefficients sum to values in table above.

**Excited-state dynamics:**
- Cl₂* (excited state) has lifetime ~10-100 ns
- Two decay mechanisms:
  1. **Radiative decay:** Cl₂* → Cl₂ + photon (low probability, ~1% branching)
  2. **Collisional decay:** Cl₂* + M → Cl₂ + M (high probability in plasma)

At 1-100 mTorr pressure, collisional decay dominates; Cl₂* does not dissociate but relaxes back to ground state.

**Consequence:** Most excited Cl₂ molecules are lost, and only direct dissociation (Pathway A) effectively produces Cl radicals. This sets practical limits on Cl atom fraction achievable in plasma.

---

## Part 2: Reaction Pathways to AlCl₃ and Other Aluminum Chlorides

### 2.1 Gas-Phase Reactions: Al → AlCl₃ Formation

**Primary pathway (direct aluminum-chlorine reaction):**

Once chlorine plasma is created (Cl atoms, Cl₂, Cl⁺ ions present), aluminum atoms/cations react to form aluminum chlorides:

**Reaction sequence (gas-phase):**

1. **Initiation (ion-surface sputtering):**
   $$\text{Cl}^+ + \text{Al (surface)} \rightarrow \text{Al}^{+*} + \text{Cl (neutral)}$$
   
   Kinetic sputtering ejects neutral Al atoms or Al⁺ ions from surface. These escape into gas phase.

2. **Gas-phase formation of AlCl₃:**
   $$\text{Al (gas)} + 3\text{Cl} \cdot \rightarrow \text{AlCl}_3 \quad \text{(radical pathway)}$$
   
   OR
   
   $$\text{Al}^+ + 3\text{Cl} \cdot \rightarrow \text{AlCl}_3^+ \rightarrow \text{AlCl}_3 + e^-$$
   
   OR
   
   $$\text{Al (gas)} + \text{Cl}_2 + \text{Cl} \cdot \rightarrow \text{AlCl}_3$$

3. **Intermediate species (AlCl, AlCl₂):**
   
   Full formation can proceed through intermediates:
   $$\text{Al} + \text{Cl} \cdot \rightarrow \text{AlCl} \quad \text{(reaction rate constant k1)}$$
   $$\text{AlCl} + \text{Cl} \cdot \rightarrow \text{AlCl}_2 \quad \text{(reaction rate constant k2)}$$
   $$\text{AlCl}_2 + \text{Cl} \cdot \rightarrow \text{AlCl}_3 \quad \text{(reaction rate constant k3)}$$

### 2.2 Thermodynamics of Aluminum Chloride Formation

**Gibbs free energy of formation (298 K):**

| Species | ΔGf° (kJ/mol) | State | Notes |
|---------|---|---|---|
| **AlCl** | -65 | Gas | Low stability; rarely stable |
| **AlCl₂** | -329 | Gas | Intermediate; can polymerize |
| **AlCl₃** | -630 | Gas | Highly stable, primary product |
| **AlCl₃·6H₂O** | -1598 | Aqueous | Fully solvated in water |

**Enthalpy of formation (298 K):**

| Species | ΔHf° (kJ/mol) | Significance |
|---------|---|---|
| **AlCl** | -40 | Weakly exothermic |
| **AlCl₂** | -284 | Moderately exothermic |
| **AlCl₃** | -581 | Highly exothermic; stable |

**Bond dissociation energies:**

| Bond | D₀ (eV) | Notes |
|------|---------|-------|
| **Al-Cl** | ~2.3 | Weaker than Al-F (~3.7 eV) |
| **Al-Cl (in AlCl₃)** | ~2.0-2.3 | Slightly weaker due to charge delocalization |

**Consequence:** AlCl₃ formation is thermodynamically favorable (ΔG << 0). Once formed, AlCl₃ is stable against decomposition back to AlCl or Al + Cl₃. The main loss mechanism for AlCl₃ is volatilization (sublimation to gas phase), not decomposition.

### 2.3 Reaction Rate Constants for Al-Cl Formation

**Experimental rate coefficients (gas-phase, 300-600 K):**

| Reaction | Rate Coefficient k (cm³/s) | Temperature (K) | Activation Energy Ea (kJ/mol) |
|----------|---|---|---|
| **Al + Cl· → AlCl + Cl·** | 1.5×10⁻¹¹ | 298 | ~5 |
| **AlCl + Cl· → AlCl₂ + Cl·** | 2.0×10⁻¹¹ | 298 | ~8 |
| **AlCl₂ + Cl· → AlCl₃ + Cl·** | 1.8×10⁻¹¹ | 298 | ~10 |
| **Al + Cl₂ → AlCl + Cl** | <1×10⁻¹⁴ | 298 | ~100 |
| **Al + Cl⁺ → AlCl⁺** | 2.0×10⁻⁹ | 298 | ~1 (fast, ion-molecule) |

**Key observations:**
1. **Radical pathway is dominant:** Al + Cl· reaction rates (~10⁻¹¹ cm³/s) are orders of magnitude faster than direct Cl₂ reaction
2. **Sequential chlorination is fast:** All three steps (AlCl → AlCl₂ → AlCl₃) have similar rate constants, implying rapid sequential reaction
3. **Ion-molecule reactions fastest:** Al + Cl⁺ is very fast (~10⁻⁹ cm³/s), but Cl⁺ concentration is low (~10⁶-10⁸ cm⁻³) compared to neutral Cl· (~10¹¹-10¹³ cm⁻³)

**Overall formation rate (in typical etch plasma):**

In a Cl₂ discharge at 50 mTorr, Te = 3 eV:
- Cl atom concentration: ~10¹² cm⁻³ (from dissociation)
- Al atom concentration (sputtered from surface): ~10⁷-10⁸ cm⁻³
- Collision rate: Al + Cl collision frequency ~10¹⁰ collisions/s
- With rate constant k ~ 1.5×10⁻¹¹ cm³/s:
  $$\text{Formation rate} = k \cdot n_{Cl} \cdot n_{Al} \approx 1.5×10⁻¹¹ \times 10^{12} \times 10^7 = 1.5×10^8 \text{ reactions/cm}^3\text{/s}$$

This implies AlCl formation timescale: τ ~ 1/(formation rate) ~ 10⁻⁸ seconds = 10 nanoseconds.

**Consequence:** Sequential chlorination (Al → AlCl → AlCl₂ → AlCl₃) occurs extremely rapidly; essentially all sputtered Al is converted to AlCl₃ before leaving the plasma.

### 2.4 AlCl₃ Stability and Sublimation

**Phase diagram of AlCl₃:**

| Temperature (°C) | Pressure (Torr) | Phase |
|---|---|---|
| -45 | 1 | Solid |
| 0 | 1 | Solid |
| 25 | 1 | Solid |
| 50 | 1 | Solid (beginning to sublime) |
| 100 | 1 | Solid (sublimation ongoing) |
| 180 | 1 | **Sublimation temperature (at 1 atm = 760 Torr)** |
| 200 | 1 | Mostly gas (sublimed) |

**Vapor pressure of AlCl₃ (solid → gas equilibrium):**

Clausius-Clapeyron equation:
$$\ln(P) = A - \frac{B}{T}$$

| Temperature (°C) | Vapor Pressure (Torr) | Interpretation |
|---|---|---|
| 25 | ~0.001 | Negligible sublimation at room temp |
| 50 | ~0.01 | Very slow sublimation |
| 100 | ~0.5 | Moderate sublimation |
| 150 | ~10 | Rapid sublimation (significant at this T) |
| 180 | ~760 | Boiling point (1 atm) |
| 200 | >1000 | Complete sublimation |

**Consequence for interconnect etch:**
- At typical etch temperature 100°C, AlCl₃ vapor pressure ~0.5 Torr
- In chamber at 50 mTorr total pressure, AlCl₃ partial pressure in gas phase is limited by sublimation equilibrium
- AlCl₃ can exist as mixture of solid (condensed) and gas (sublime) phases
- On cooler surfaces (walls, electrode): AlCl₃ condenses, forming powder deposit
- On wafer (warmer, ~100°C): AlCl₃ tends to remain gas or thin deposit

**Problem for production:** AlCl₃ deposits on chamber walls create:
1. Chamber conditioning necessity (periodic O₂ plasma to remove deposits)
2. Residue contamination of wafers (AlCl₃ particles dislodge and fall onto processed wafers)
3. Maintenance burden (deposits clog showerheads, electrodes)

---

## Part 3: Alternative Chlorine Sources and Gas Mixtures

### 3.1 Hydrogen Chloride (HCl) Chemistry

**Molecular properties:**
- Formula: HCl
- Molar mass: 36.5 g/mol
- Boiling point: -85°C (more volatile than Cl₂)
- Ionization energy: 12.7 eV (similar to Cl₂ at ~12.6 eV)

**Reaction with aluminum:**

HCl as etchant involves both atomic Cl and H radicals:

$$\text{HCl} + e^- \rightarrow \text{H} + \text{Cl} + e^- \quad \text{(dissociation)}$$

$$\text{Al (surface)} + 3\text{HCl} \rightarrow \text{AlCl}_3 + 3/2\text{H}_2 \quad \text{(chemical reaction)}$$

**Dissociation characteristics:**
- **Ionization energy:** ~12.7 eV (slightly higher than Cl₂)
- **Dissociation energy:** ~4.5 eV (Cl-H bond breaks easily)
- **Cross-section:** σ_dissoc ~ 2-4 × 10⁻¹⁶ cm² (comparable to Cl₂)

**Gas-phase reactions with HCl:**

| Reaction | Rate Coefficient (cm³/s) | Notes |
|----------|---|---|
| **e⁻ + HCl → H + Cl + e⁻** | ~8×10⁻⁹ (ionization) | Fast, produces H⁺ |
| **e⁻ + HCl → H + Cl + e⁻** | ~5×10⁻⁹ (dissociation) | Also produces neutral H, Cl |
| **H + Cl₂ → HCl + Cl** | ~1×10⁻¹¹ | Converts H to HCl reformation |
| **Al + Cl (from HCl)** | ~1.5×10⁻¹¹ | Same as Cl₂ pathway |

**Why HCl is used (benefits):**
1. **Selectivity enhancement:** H radicals preferentially etch Al over SiO₂ (H-assisted pathway selective)
2. **Smoother etch profile:** HCl produces smoother sidewalls compared to pure Cl₂
3. **Reduced ion energy requirement:** Chemical reaction component (H + Al) compensates for lower ion bombardment
4. **Residue chemistry:** HCl reactions produce HCl + Al₂O₃ complex (less volatile but less problematic than AlCl₃)

**Disadvantage:**
- **Lower etch rate:** Chemical pathway slower than pure ion sputtering
- **H₂ gas production:** Reaction produces H₂ gas (unreactive, just exhaust)
- **Selectivity trade-off:** If over-done, selectivity to oxide degrades

### 3.2 Carbon Tetrachloride (CCl₄) Chemistry

**Molecular properties:**
- Formula: CCl₄
- Molar mass: 153.8 g/mol
- Boiling point: 76.7°C (moderate volatility)
- Valence: Carbon is +4 oxidation state (4 Cl atoms bonded to central C)

**Dissociation in plasma:**

CCl₄ is more reactive than Cl₂ in plasma:

$$\text{CCl}_4 + e^- \rightarrow \text{CCl}_3 + \text{Cl} + e^- \quad \text{(loss of one Cl)}$$
$$\text{CCl}_3 + e^- \rightarrow \text{CCl}_2 + \text{Cl} + e^- \quad \text{(loss of second Cl)}$$
$$\text{CCl}_2 + e^- \rightarrow \text{CCl} + \text{Cl} + e^- \quad \text{(loss of third Cl)}$$

**Cross-sections:**
- CCl₄ dissociation: σ ~ 10-15 × 10⁻¹⁶ cm² (higher than Cl₂, more dissociable)
- Multiple dissociation channels produce Cl atoms efficiently
- Rate coefficient k_CCl₄_dissoc ~ 2-3×10⁻⁸ cm³/s (faster than Cl₂)

**Advantage: Higher Cl atom production**

Per molecule:
- Cl₂: Produces 2 Cl atoms per dissociation
- CCl₄: Produces up to 4 Cl atoms per dissociation (step-wise)

This makes CCl₄ efficient for generating high Cl atom concentration from lower pressure:
- Cl₂ at 30 mTorr: ~50% dissociation → ~15 mTorr Cl atoms
- CCl₄ at 15 mTorr: ~80% dissociation → ~12 mTorr Cl atoms equivalent (fewer molecules needed)

**Disadvantage: Carbon contamination**

Unreacted CCl₄ and intermediate species (CCl₃, CCl₂) contain carbon:
$$\text{CCl}_4, \text{CCl}_3, \text{CCl}_2 \rightarrow \text{carbon deposits on wafer/chamber}$$

Carbon deposits are problematic:
1. **Wafer contamination:** Carbon in interconnect → impurity scattering, reliability issues
2. **Chamber coating:** Carbon deposits on electrodes, reducing conductivity
3. **Etch uniformity:** Carbon deposits grow non-uniformly, creating source of wafer-to-wafer variation

**Modern practice:** CCl₄ used in limited applications (specialized selectivity needs) but largely replaced by Cl₂ + HCl mixtures.

### 3.3 Boron Trichloride (BCl₃) Chemistry

**Molecular properties:**
- Formula: BCl₃
- Boron oxidation state: +3
- Molar mass: 117.2 g/mol
- Boiling point: 12.5°C (volatile)

**Use in aluminum etch:**
BCl₃ is primarily used for **sidewall passivation** (to be detailed in Chapter 4), not as primary etchant.

**Gas-phase reaction (minor role):**
$$\text{Al} + 3\text{BCl}_3 \rightarrow \text{AlCl}_3 + 3\text{BCl} \quad \text{(not favorable; not main pathway)}$$

Instead, BCl₃ reacts with surface chlorine to form **B-containing passivation layer** (BCl polymer or B₂Cl).

---

## Part 4: Gas Mixture Effects and Industrial Recipes

### 4.1 Common Gas Mixtures for Aluminum Etch

**Recipe Type 1: Pure Cl₂ (legacy, 180nm and older nodes)**

Composition: 100% Cl₂
Conditions: 50-150 mTorr, 500-1000 W, 100°C

Characteristics:
- Highest etch rate (pure ion sputtering)
- Poor selectivity to oxide (~1.2-1.5:1)
- High residue (AlCl₃ deposition)
- Simple chemistry, easy to control

Current use: Legacy nodes only; obsolete for advanced nodes

---

**Recipe Type 2: Cl₂ + HCl (dominant at 90nm-28nm nodes)**

Composition: Cl₂ 70-90%, HCl 10-30%
Conditions: 30-100 mTorr, 600-1200 W, 95-110°C

Characteristics:
- Moderate etch rate (200-400 nm/min)
- Better selectivity (1.5-2.0:1 Al/SiO₂)
- Improved profile (smoother sidewalls due to H radical pathway)
- Reduced residue (HCl modifies AlCl₃ → intermediate products)

Mechanism:
- Cl₂ provides bulk etch rate via Cl⁺ ion sputtering
- HCl provides selectivity via H-assisted Al oxidation pathway (preferentially attacks Al over oxide)
- Chemical reaction rate determined by [HCl] and Cl concentration

Typical tuning:
- Increase HCl: Better selectivity but lower etch rate
- Decrease HCl: Higher etch rate but risk undercut

Current use: 90nm through 22nm nodes; established industrial standard

---

**Recipe Type 3: Cl₂ + HCl + BCl₃ (advanced nodes, 14nm-3nm)**

Composition: Cl₂ 60-75%, HCl 15-30%, BCl₃ 5-15%
Conditions: 20-50 mTorr, 800-1500 W, 100-110°C

Characteristics:
- Moderate etch rate (200-350 nm/min)
- Excellent selectivity (1.8-2.5:1 Al/SiO₂)
- Superior profile (BCl₃ passivates sidewalls, prevents undercut)
- Controlled ARDE (pressure tuning + pulsed power)
- Lower residue (complex product chemistry)

Mechanism:
- Cl₂: Primary etch rate
- HCl: Selectivity and profile control
- BCl₃: Sidewall passivation (forms B-Cl layer protecting sidewalls, Chapter 4 detail)

Why BCl₃ helps:
- B atoms deposited on sidewalls by ion sputtering
- Forms BCl polymer or boron subchloride layer
- This layer stops Al attack (passivation), but not SiO₂ etch (selectivity)
- Enables vertical profiles even at extreme aspect ratios

Current use: Leading edge (3nm, 5nm, 7nm nodes)

---

**Recipe Type 4: Cl₂ + CCl₄ (specialized use, M0-M1 layers)**

Composition: Cl₂ 80-95%, CCl₄ 5-20%
Conditions: 40-80 mTorr, 500-1000 W, 100-120°C

Characteristics:
- Moderate etch rate
- Excellent selectivity (due to carbon passivation)
- Carbon deposits → residue management critical
- High thermal load (many dissociation channels release energy)

Current use: Rare at production scale due to carbon contamination risk; used only in specialized applications or specific foundry processes

---

### 4.2 Plasma Chemistry Modeling: Rate Balance

**Simplified model for Cl atom production and consumption:**

Production:
$$\frac{d[Cl]}{dt} \bigg|_{prod} = k_{e-dissoc} \cdot n_e \cdot [Cl_2] + k_{HCl-dissoc} \cdot n_e \cdot [HCl] + k_{CCl_4-dissoc} \cdot n_e \cdot [CCl_4]$$

Consumption:
$$\frac{d[Cl]}{dt} \bigg|_{cons} = -k_{Al-Cl} \cdot [Al] \cdot [Cl] - k_{Cl-Cl} \cdot [Cl] \cdot [Cl] - k_{wall-loss} \cdot [Cl]$$

Where:
- $n_e$ = electron density (~10⁹-10¹¹ cm⁻³ in etch plasmas)
- $[Cl_2], [HCl], [CCl_4]$ = molecular concentrations
- $[Al]$ = sputtered Al atom concentration
- $k_{...}$ = rate constants
- $k_{wall-loss}$ = loss of Cl atoms to chamber walls (recombination)

**Steady-state assumption (plasma in quasi-equilibrium):**

$$\frac{d[Cl]}{dt} = 0 \Rightarrow \text{Production} = \text{Consumption}$$

This implies:
$$[Cl]_{ss} = \frac{k_{e-dissoc} \cdot n_e \cdot [Cl_2] + ...}{k_{Al-Cl} \cdot [Al] + k_{Cl-Cl} \cdot [Cl]_{ss} + k_{wall}}$$

**Consequence:** Cl atom concentration reaches steady-state in milliseconds to seconds, depending on pressure and gas mixture.

At 50 mTorr, Te = 3 eV, typical etch conditions:
- Cl₂ dissociation rate: ~10⁹ cm⁻³s⁻¹
- Cl atom concentration: ~10¹² cm⁻³ (steady-state)
- Mean free path of Cl between collisions: ~1 mm (in plasma, before hitting wafer)

---

## Part 5: Residue Product Chemistry

### 5.1 AlCl₃ as Primary Product

**Formation summarized:**
$$\text{Al (sputtered)} + 3\text{Cl (radicals/ions)} \rightarrow \text{AlCl}_3$$

**Volatility:**
AlCl₃ sublimes at temperature >~100°C; at etch temperature (100-110°C), significant fraction is gas, remainder is condensed (solid/liquid mixture depending on exact T and pressure).

**Residue behavior:**

On wafer surface (T ~ 100-110°C):
- Thin AlCl₃ film condenses (few monolayers to ~100 nm)
- Relatively volatile; heating to 150°C removes most
- Reacts with atmospheric moisture if exposed to air post-etch

On chamber walls (T ~ 40-60°C):
- AlCl₃ condenses more readily (lower T)
- Accumulates as powder deposit (white/tan color)
- Can reach grams per processing month on cooled surfaces
- Must be removed periodically (in-situ O₂ plasma cleaning)

### 5.2 Post-Etch Residue Composition

**Complex mixture after etch cycle:**

Primary species:
- AlCl₃ (volatile component)
- Al₂O₃ (from oxidation post-etch, or during etch on oxide etch stop)
- Cl⁻ residues (from incomplete volatilization)

Secondary species (if HCl used):
- AlOxClᵧ (aluminum oxychloride, intermediate between AlCl₃ and Al₂O₃)
- HCl·AlCl₃ (complex salt)

Tertiary species (if BCl₃ used):
- BCl polymer (B-Cl chain deposits)
- Boron-aluminum complex

**Typical residue analysis (XPS, post-etch):**

| Element | Atomic % (typical) | Chemical Form | Volatility |
|---------|---|---|---|
| Al | 30-40 | AlCl₃, Al₂O₃ | Medium (volatile as AlCl₃) |
| Cl | 35-45 | Cl⁻ in salts | Low (stays bound) |
| O | 15-25 | Oxide, oxychloride | Very low (stable) |
| C | <1-3 | Carbon contamination (if CCl₄) | Variable |
| B | <1 | BCl polymer (if BCl₃) | Low (sticky) |

---

## Part 6: Thermodynamic Data and Reference Tables

### 6.1 Thermodynamic Constants for Chlorine Species

**Standard formation enthalpies and free energies (298 K):**

| Species | State | ΔHf° (kJ/mol) | ΔGf° (kJ/mol) | S° (J/mol·K) |
|---------|-------|---|---|---|
| **Cl (atom)** | Gas | 121.3 | 105.3 | 165.2 |
| **Cl₂** | Gas | 0 | 0 | 223.1 |
| **HCl** | Gas | -92.3 | -95.3 | 186.9 |
| **CCl₄** | Gas | -102.9 | -60.6 | 309.7 |
| **AlCl** | Gas | -40 | -65 | ~210 (est.) |
| **AlCl₂** | Gas | -284 | -329 | ~260 (est.) |
| **AlCl₃** | Gas | -581 | -630 | ~307 |
| **AlCl₃·6H₂O** | Aqueous | -1598 | -1463 | ~217 |

**Interpretation:** 
- Negative ΔGf indicates thermodynamic stability
- AlCl₃ highly stable (ΔGf = -630 kJ/mol)
- Once formed, AlCl₃ requires significant activation energy to decompose
- Main loss mechanism: Sublimation to gas phase, not decomposition

### 6.2 Electron-Impact Cross-Sections (Reference Table)

**Dissociation cross-sections for chlorine molecules:**

| Molecule | Threshold Energy (eV) | Peak Cross-Section (10⁻¹⁶ cm²) | Peak Energy (eV) | Literature |
|----------|---|---|---|---|
| **Cl₂** | 2.5 | ~8 | 20-30 | Huxley & Crompton (1974) |
| **HCl** | 2.3 | ~4 | 25-35 | Kitajima et al. (2000) |
| **CCl₄** | 2.0 | ~12 | 15-25 | Christophorou et al. (1984) |
| **BCl₃** | 2.8 | ~6 | 25-30 | CRC Handbook (2005) |

---

## Part 7: Industrial Gas Mixture Selection Rationale

### 7.1 Process Window Tuning with Gas Mixture

**Challenge: Multi-objective optimization**

Given competing objectives:
1. High etch rate (throughput cost)
2. High selectivity (device margin)
3. Vertical profile (ARDE control)
4. Low residue (reliability)

**Gas mixture tuning strategy:**

| Objective | Lever | Mechanism |
|-----------|-------|-----------|
| **Increase etch rate** | ↑ Cl₂, ↓ HCl | More Cl atoms → ion sputtering dominates |
| **Increase selectivity** | ↑ HCl, ↓ Cl₂ | H-assisted pathway selective to Al over oxide |
| **Improve profile** | ↑ BCl₃ | Passivation layer on sidewalls prevents undercut |
| **Reduce residue** | ↑ HCl, ↓ Cl₂ | HCl chemistry produces less AlCl₃ buildup |
| **Reduce ARDE** | ↓ Pressure, ↑ BCl₃ | Lower pressure increases ion directionality; BCl₃ passivation compensates |

### 7.2 Equipment Capability and Gas System Design

**Typical etch tool gas supply:**

Modern tools can source:
- Cl₂ mass flow controller (0-500 sccm typical)
- HCl mass flow controller (0-200 sccm)
- BCl₃ mass flow controller (0-100 sccm)
- Ar or He carrier (0-1000 sccm)

Recipe flexibility:
- Change Cl₂:HCl ratio → adjust selectivity/etch rate trade-off
- Adjust absolute flow rate → pressure control
- Pulse on/off individual gases → recipe sophistication

---

## Part 8: Connection to Surface Chemistry and Etch Mechanisms

### 8.1 What Happens After Gas-Phase Reactions

**Cl atoms and ions generated in gas phase reach wafer surface where:**

1. **Cl⁺ ions:** Direct sputtering of Al
2. **Cl· radicals:** Engage in surface reactions (detailed in Chapter 4)
3. **Cl₂ molecules:** Assist in Al oxidation on surface

**Preview of Chapter 4:**

Gas-phase chemistry sets the conditions (Cl atom/ion flux, Cl₂ partial pressure, etc.) for surface reactions:
$$\text{Al (surface)} + \text{Cl⁺ (incident)} \rightarrow \text{Al⁺ (sputtered)} + \text{Cl (ejected)}$$
$$\text{Al (surface)} + \text{Cl} \cdot \text{(radical)} \rightarrow \text{AlCl (surface)} \rightarrow \text{AlCl}_3 \text{ (sublime)}$$

These surface mechanisms are the actual etch process; gas-phase chemistry is the enabler.

---

## Key Takeaways

1. **Cl₂ dissociation is efficient in plasma:** Electron-impact dissociation cross-section peaks at 20-30 eV, matching typical electron energies in CCP; dissociation rate coefficients ~10⁻⁹ cm³/s enable >50% conversion of Cl₂ to Cl atoms.

2. **AlCl₃ formation is rapid and thermodynamically favorable:** Gas-phase chlorination of Al atoms proceeds through AlCl → AlCl₂ → AlCl₃ with rate constants ~10⁻¹¹ cm³/s; timescale ~10 ns. ΔGf = -630 kJ/mol ensures stability.

3. **AlCl₃ volatility sets residue behavior:** At etch temperatures (100-110°C), AlCl₃ vapor pressure ~0.5 Torr enables gas-phase transport, but cooler surfaces (walls, electrodes) condense deposits requiring periodic cleaning.

4. **Gas mixture selection controls process trade-offs:** Pure Cl₂ maximizes etch rate but poor selectivity; Cl₂/HCl improves selectivity at cost of etch rate; Cl₂/HCl/BCl₃ provides best profile control for advanced nodes.

5. **HCl mechanism is selective:** H radicals generated from HCl dissociation preferentially attack Al over oxide, providing selectivity enhancement without sacrificing lateral control.

6. **BCl₃ enables sidewall passivation:** Boron deposits on sidewalls form low-permeability barrier to Cl atoms, protecting sidewalls while oxide remains exposed (Chapter 4 detail).

7. **Residue chemistry is complex:** Post-etch residue is mixture of AlCl₃, Al₂O₃, and halide/oxide intermediates; composition depends on gas mixture and post-etch conditions.

---

## References and Further Reading

### Plasma Chemistry and Electron-Impact Reactions
- Fridman, A., & Kennedy, L. A. (2011). *Plasma Discharges and Fundamentals of Their Modeling* (3rd ed.). Cambridge University Press.
- Kushner, M. J. (1992). "A three-dimensional model for the production of ground-state oxygen atoms in inductively coupled plasma discharge." *Journal of Applied Physics*, 63, 2532-2551.
- Graves, D. B., & Yan, B. (2018). "Plasma-surface interactions." In *Handbook of Materials Modeling* (pp. 1-26). Springer.

### Aluminum Chloride Chemistry and Thermodynamics
- Kubaschewski, O., & Alcock, C. B. (1979). *Metallurgical Thermochemistry* (5th ed.). Pergamon Press.
- NIST Chemistry WebBook. (2024). "Thermodynamic Data, Atomic Weights and Isotopic Composition." https://webbook.nist.gov/

### Gas-Phase Kinetics and Rate Coefficients
- Atkinson, R., et al. (2004). "Evaluated kinetic and photochemical data for atmospheric chemistry." *Atmospheric Chemistry and Physics*, 4, 1461-1738.
- Christophorou, L. G., & Olthoff, J. K. (2001). *Fundamental Electron Interactions with Plasma Processing Gases*. National Inst. of Standards & Technology.

### Aluminum Etching in Industry
- Lam Research. (2021). "Chlorine-Based Aluminum Etch Chemistry: From Plasma to Product." Technical Report.
- Applied Materials. (2022). "Gas Mixture Optimization for Advanced Interconnect Etch." Process Note.
- SEMI Standards. (2023). *Aluminum Plasma Etch Process Control.*

### Experimental Measurements of Cross-Sections
- Huxley, L. G. H., & Crompton, R. W. (1974). *The Diffusion and Drift of Electrons in Gases*. Wiley-Interscience.
- Kitajima, T., et al. (2000). "Dissociation cross sections for HCl by electron impact." *Journal of Applied Physics*, 88, 2455-2462.

---

**Next Chapter: Chapter 4 — Plasma-Metal Surface Reactions & Ion-Assisted Sputtering**

In Chapter 4, we translate gas-phase chemistry to surface chemistry. How do Cl⁺ ions sputter Al? What is ion-assisted chemical etching? How do ion energy and surface temperature determine etch rate? How does AlCl₃ form at the surface, and what causes residue deposition? We develop surface reaction mechanisms with quantitative etch rate models derived from sputtering yields and chemical rate constants.

