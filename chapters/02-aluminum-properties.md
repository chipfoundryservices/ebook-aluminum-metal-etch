# Chapter 2: Aluminum Physical/Chemical Properties & Oxidation Kinetics

## Executive Summary

Aluminum is unique among semiconductor interconnect metals in the interplay of its exceptional thermal conductivity, chemical reactivity, and mechanical properties. Understanding aluminum etch requires first understanding aluminum itself: Why does it oxidize so readily? What does that oxide layer mean for etch selectivity and residue formation? How do thermal properties constrain chamber design? What role do alloying elements play? This chapter develops aluminum from first principles—electron configuration through oxidation kinetics—establishing the material science foundation for the plasma chemistry and etch mechanisms that follow. Special attention is paid to native Al₂O₃ formation, because this ~3-5nm layer is the first barrier that plasma must penetrate before etch can begin, and its reformation during post-etch residue removal complicates in-situ cleaning processes.

---

## Part 1: Aluminum Fundamentals

### 1.1 Electron Configuration and Valence Chemistry

**Aluminum (Al) in the periodic table:**
- Atomic number: 13
- Electron configuration: [Ne] 3s² 3p¹
- Valence: 3 (three valence electrons available for bonding)
- Group IIIA (boron group)
- Period 3

**Oxidation states:**
- Primary: Al³⁺ (aluminum stripped of all three valence electrons; +3 formal charge)
- Secondary: Al⁰ (metallic aluminum)
- Rare: Al⁺, Al²⁺ (intermediate oxidation states, only in specific coordination chemistry)

**Why Al³⁺ is thermodynamically favorable:**

The ionization energy to remove the third electron from aluminum is substantial:
- 1st ionization energy (Al → Al⁺): 5.985 eV
- 2nd ionization energy (Al⁺ → Al²⁺): 18.828 eV
- 3rd ionization energy (Al²⁺ → Al³⁺): 28.447 eV
- **Total: 53.26 eV**

Despite the high energy cost, Al³⁺ is the stable oxidation state in most compounds because the energy cost is recovered through:
1. **Lattice energy:** Formation of Al₂O₃ lattice releases 15,916 kJ/mol (massive energetic gain)
2. **Hydration energy:** In aqueous solution, Al³⁺ is hydrated by 6 water molecules, releasing additional energy

**Net thermodynamic result:** Formation of Al₂O₃ is highly favorable; once formed, the oxide is extremely stable.

### 1.2 Metallic Properties of Aluminum

#### Density and Crystallography

| Property | Value | Units | Significance for Interconnect |
|----------|-------|-------|------|
| **Density** | 2.70 | g/cm³ | ~1/3 density of Cu (8.96) or W (19.3); enables thinner films for same conductance |
| **Crystal structure** | FCC | — | Face-centered cubic; highly symmetric, favors equiaxed grain growth |
| **Lattice parameter** | 4.05 | Å | Slightly larger than Cu (3.61 Å); affects grain boundary properties |
| **Melting point** | 933 | K (660°C) | Sets upper thermal process limit; limits reflow during or post-etch |
| **Grain size (typical)** | 50-200 | nm | Interconnect layer thickness often 100-300nm; few grains thick |

**Consequence for interconnect design:** Aluminum films deposited by sputtering form columnar grains with {111} texture (111 planes parallel to film surface). This texture affects:
- Electromigration resistance (higher activation energy for Al cation transport in columnar structure)
- Mechanical stress distribution (grain boundaries act as stress concentrators)
- Oxidation rate (111 surfaces oxidize faster than 100 surfaces)

#### Thermal Transport Properties

| Property | Al | Cu | W | Units | Significance |
|----------|----|----|---|-------|---|
| **Thermal conductivity (300K)** | 237 | 385 | 173 | W/m·K | Al conducts heat 2-3× faster than typical dielectrics |
| **Temperature coefficient** | -0.31 | -0.38 | -0.007 | % / K | Al thermal conductivity decreases with T; chamber cooling design critical |
| **Specific heat** | 897 | 386 | 132 | J/kg·K | Al has higher heat capacity than Cu; more thermal inertia |
| **Thermal expansion** | 23.1 | 16.5 | 4.5 | ppm/K | Al expands significantly; CTE mismatch with SiO₂ (0.5 ppm/K) creates stress |

**Consequence for chamber design:** Aluminum's thermal conductivity means:
1. **Wafer temperature uniformity difficult:** Heat generated at electrode rapidly conducts to cool areas of wafer
2. **Thermal transients large:** When RF power switches on/off, wafer temperature changes quickly (timescale ~1-2 seconds)
3. **Temperature gradients inevitable:** Center of wafer (exposed to plasma) hotter than edges; thermal gradients ±10-20°C common without active cooling
4. **Chuck must be cooled:** Typical requirement 10-20°C below process temperature to maintain wafer at target

**Quantitative thermal load:**
- RF power dissipated in plasma: ~500-1500W
- Fraction reaching wafer: ~30-40% (balance to chamber walls)
- Power to 300mm wafer area (area ~70,650 mm²): ~50-200 W/cm²
- With Al wafer thermal conductivity 237 W/m·K, this creates temperature rise of:

$$\Delta T = \frac{P}{\kappa \cdot A} \approx \frac{100 \text{ W/cm}^2}{237 \text{ W/m·K} \times 10^{-4} \text{ m}^2/\text{cm}^2} \approx 4.2 \text{ K/cm}^2$$

Without cooling: wafer center reaches 120-150°C, edges 60-80°C → 50-70°C gradient unacceptable.

#### Electrical Properties

| Property | Al | Cu | Units | Notes |
|----------|----|----|-------|-------|
| **Resistivity (300K, bulk)** | 2.65 | 1.68 | µΩ·cm | Al 58% higher resistance than Cu |
| **Temperature coefficient** | 0.39 | 0.39 | % / K | Nearly identical |
| **Electron mean free path (bulk)** | ~60 | ~100 | nm | Size-effect scattering becomes important below ~100nm thickness |
| **Electron mean free path (interfaces)** | ~10-20 | ~20-40 | nm | Surface/grain boundary scattering dominates in thin films |

**Consequence for interconnect:** At M0-M1 (linewidth 20-40nm, thickness 30-50nm), resistance increases nonlinearly due to surface scattering:

$$R = \rho \frac{L}{W \cdot T} \cdot \frac{1}{1 - 3\lambda(W+T)/(8W \cdot T)}$$

where λ is electron mean free path. For narrow lines:
- Bulk resistivity 2.65 µΩ·cm becomes effective 4-6 µΩ·cm
- Resistance scales inversely with thickness; thinner films have higher resistance per unit length
- This drives designers toward copper for lowest-resistance layers

### 1.3 Aluminum Alloys in Semiconductor Interconnect

Pure aluminum (99.99%+) has limited use in interconnects due to:
1. **Electromigration susceptibility:** Al cations drift under high current density + temperature gradient
2. **Mechanical softness:** Pure Al deforms under stress, compromising line integrity
3. **Interface reactivity:** Pure Al reacts violently with oxygen and moisture

**Standard interconnect alloys:**

#### AlCu (Aluminum-Copper, 0.5-2 wt% Cu)

**Purpose:** Reduce electromigration

**Mechanism:** Cu atoms occupy Al lattice positions and grain boundaries, impeding Al cation transport. Copper also:
- Decreases Al grain size (Cu acts as grain refiner during crystallization)
- Increases mechanical hardness
- Forms Cu-rich phases at grain boundaries that act as diffusion barriers

**Industrial adoption:**
- Introduced 1990s when electromigration became limiting at 0.5µm pitch
- Remains standard for M1-M3 layers at all technology nodes
- Typical composition: AlCu(0.5%) or AlCu(1.0%)

**Impact on etch:**
- Etch rate of AlCu similar to pure Al in Cl₂ plasmas
- Cu atoms sputtered at same rate as Al (both removed as CuCl₂ or AlCuClₓ species)
- Residue composition changes: Cu-containing chlorides (CuCl₂, CuCl) less volatile than AlCl₃
- Selectivity to oxide slightly improved (Cu etch slower in oxide than Al)

#### AlSi (Aluminum-Silicon, 0.1-1.5 wt% Si)

**Purpose:** Reduce Si spike penetration from contacts into Al

**Mechanism:** When Al line overlaps tungsten or polysilicon contact, silicon can spike upward (solid-state diffusion during post-etch annealing). Si in Al reduces driving force for spike growth. AlSi also:
- Increases mechanical strength
- Lowers melting point (eutectic at Al-Si 12.6% Si, melting 577°C)
- Reduces grain size

**Industrial adoption:**
- Used in M0-M1 (local interconnect), where Al directly contacts Si contacts or polysilicon
- Not used in upper metal layers
- Typical composition: AlSi(0.5%) or AlSi(1.0%)

**Impact on etch:**
- Silicon forms thin SiO₂ interfacial layer on contact, affecting initial etch
- Si etch rate in Cl₂ plasma much lower than Al → etch stops on Si-containing interface
- Selectivity Al/Si or Al/SiO₂ slightly reduced compared to pure Al (Si etch competes)
- Residue composition: AlSiClₓ species expected (intermediate volatility between AlCl₃ and SiCl₄)

#### AlSiCu (Aluminum-Silicon-Copper, 0.5-1.5 wt% Si + 0.5-2 wt% Cu)

**Purpose:** Combine benefits of Si spike suppression and electromigration resistance

**Industrial adoption:**
- Modern standard for M0-M1 at all advanced nodes (2020+)
- Provides maximum flexibility for various interconnect schemes
- Composition: AlSi(1.0%)Cu(0.5%) or AlSi(0.5%)Cu(1.0%) typical

**Impact on etch:**
- Combined effects of AlCu and AlSi
- Three-component residue chemistry: Al, Si, Cu chlorides all present
- Etch rate somewhat reduced compared to pure Al (Si component etch-limited)
- Selectivity complex: depends on relative Si and Cu content

**Thermodynamic data for common alloys:**

| Alloy | Density (g/cm³) | Melting Point (°C) | Thermal Conductivity 300K (W/m·K) | Electrical Resistivity (µΩ·cm) |
|-------|---|---|---|---|
| Pure Al | 2.70 | 660 | 237 | 2.65 |
| AlCu(1%) | 2.71 | 658 | 233 | 2.80 |
| AlSi(1%) | 2.67 | 649 | 209 | 3.10 |
| AlSiCu(1/1) | 2.68 | 647 | 205 | 3.25 |

**Interpretation:** Alloying decreases thermal conductivity (~5-10% reduction) and increases electrical resistivity (~20-25% increase). These trade-offs are accepted because electromigration/reliability advantages outweigh the modest performance penalties.

---

## Part 2: Oxidation Kinetics and Native Al₂O₃ Formation

### 2.1 Thermodynamics of Aluminum Oxidation

**The oxidation reaction:**
$$4 \text{Al} + 3 \text{O}_2 \rightarrow 2 \text{Al}_2\text{O}_3$$

**Gibbs free energy of formation:**
$$\Delta G_f^\circ(\text{Al}_2\text{O}_3) = -1,576.4 \text{ kJ/mol (at 298K)}$$

**Comparison to other metal oxides:**

| Oxide | ΔGf (kJ/mol, 298K) | Oxide Type | Relevance |
|-------|---|---|---|
| **Al₂O₃** | -1576.4 | Ceramic, ionic | Extremely stable |
| **SiO₂** | -856.6 | Ceramic, covalent | Stable, used as etch stop |
| **CuO** | -129.7 | Ionic | Weakly stable; Cu preferentially metallic |
| **WO₃** | -764.8 | Transition metal oxide | Moderate stability |
| **TiO₂** | -944.8 | Transition metal oxide | Very stable, used as barrier coating |

**Key insight:** Al₂O₃ is *thermodynamically among the most stable oxides*. This is why:
1. Aluminum cannot be stored in open air (oxidation is spontaneous)
2. Native Al₂O₃ films reform immediately after etch (re-oxidation is inevitable)
3. Post-etch cleaning to remove AlCl₃ must avoid excess oxygen (which forms Al₂O₃ instead of volatile products)

### 2.2 Native Al₂O₃ Formation Kinetics

**Aluminum oxidation occurs in stages:**

#### Stage 0: Bare Aluminum (No Oxide)
Time scale: <1 second in air

Pure Al surface is thermodynamically unstable in presence of O₂. Native oxide nucleates instantly on fresh surfaces created by physical sputtering, cleaving, or chemical processes.

#### Stage 1: Initial Oxide Growth (0-5 nm thickness, seconds to minutes)

**Mechanism:** Oxygen atoms chemically adsorb on Al surface, then dissociate and diffuse into oxide lattice.

**Growth rate (Wagner model):**
$$h(t) = \sqrt{2 \kappa t}$$

where h is oxide thickness, κ is the parabolic rate constant.

**Parabolic rate constant κ (experimental data):**

| Temperature (°C) | κ (nm²/s) | Reference |
|---|---|---|
| 20 | 0.008 | Typical room air |
| 50 | 0.020 | Mild heating |
| 100 | 0.065 | Interconnect process temp |
| 150 | 0.18 | Upper thermal limit |

**Interpretation:** Oxide growth rate increases dramatically with temperature. At 100°C, oxide grows 8× faster than at 20°C.

**At 100°C (typical etch temperature), typical kinetics:**
- Native oxide after 10 seconds: h = √(2 × 0.065 × 10) ≈ 1.1 nm
- Native oxide after 60 seconds: h = √(2 × 0.065 × 60) ≈ 2.8 nm
- Native oxide after 300 seconds: h = √(2 × 0.065 × 300) ≈ 6.2 nm

**Consequence:** In a 45-minute etch cycle with process temperature ~100°C, if metal is exposed at any point, native oxide grows to ~5nm within minutes. This oxide layer must be penetrated during etch initiation, consuming ion dose.

#### Stage 2: Breakaway Oxidation (>5 nm, minutes to hours)

At thicknesses >3-5 nm, oxide growth transitions from diffusion-limited to reaction-rate-limited. The Tammann temperature (where bulk Al atoms gain sufficient mobility to participate) is ~280°C (well above interconnect process temperature), so Stage 2 behavior is less relevant for sub-150°C processes.

At room temperature, Al₂O₃ on Al reaches equilibrium thickness ~2-4 nm (Cabrera-Mott oxide).

### 2.3 Al₂O₃ Properties Critical for Etch

**Crystal structure:**
- **Corundum structure:** Al₂O₃ adopts the α-Al₂O₃ (corundum) structure, trigonal crystal system
- **Lattice parameters:** a = 4.758 Å, c = 12.991 Å
- **Density:** 3.97 g/cm³
- **Hardness:** 1900 HV (second only to diamond; extremely hard)

**Optical properties:**
- **Bandgap:** 8.8 eV (transparent to visible light, opaque to UV below ~140 nm)
- **Refractive index:** 1.76 at 633 nm (relevant for OES endpoint detection)
- **Opacity:** Non-transparent at UV/VUV wavelengths used in some plasma diagnostics

**Electrical properties:**
- **Dielectric constant:** κ = 9.3 (relatively high for a ceramic)
- **Breakdown field:** ~10 MV/cm (high dielectric strength)
- **Resistivity:** >10¹⁴ Ω·cm at room temperature (insulating)

**Mechanical properties:**
- **Young's modulus:** 345 GPa (very stiff; comparable to steel ~200 GPa)
- **CTE:** 5.3 ppm/K (roughly 10× higher than SiO₂ at 0.5 ppm/K)
- **Fracture toughness:** ~3-4 MPa·m^{1/2} (brittle; low impact resistance)

**Chemical properties:**
- **Acid solubility:** Dissolves slowly in strong acids (HCl, H₂SO₄, H₃PO₄)
- **Base solubility:** Dissolves readily in strong bases (NaOH, KOH) — amphoteric
- **Chlorine reactivity:** Partially reacts with Cl₂ gas at elevated temperature (>400°C), but kinetics negligible at 100-150°C
- **Hydrogen reactivity:** No reaction with H₂ at typical etch temperatures

### 2.4 Al₂O₃ in Interconnect Etch Context

**During etch process:**

1. **At t=0 (fresh aluminum surface after deposition):**
   - Native oxide thickness: 2-4 nm
   - Oxide composition: Mix of Al₂O₃ and amorphous aluminum oxihydroxide (from air exposure during wafer handling)
   - Oxide interface: Rough at atomic scale due to Mott-Cabrera oxide growth mechanism

2. **Etch initiation (first 10-20 seconds of plasma):**
   - Ions (Cl⁺, Ar⁺) bombard surface with 50-200 eV kinetic energy
   - Ion sputtering removes native oxide, exposing underlying Al metal
   - Sputtering yield for Al₂O₃: ~0.5-1.5 atoms/ion at 100 eV (lower than metal due to oxide binding energy)
   - Process consumes ~500-2000 ion/nm² to fully clear 3nm oxide
   - This ion dose is "wasted" on oxide removal, not available for metal etch

3. **Metal etch phase (main etch, 20-3000 seconds):**
   - Bare Al exposed; etch proceeds via ion-sputtering and ion-assisted chemical reaction
   - Etch rate: 200-500 nm/min typical
   - Native oxide does not reform significantly (low O₂ partial pressure in Cl₂/HCl plasma)

4. **Etch completion (after metal cleared):**
   - Underlying SiO₂ or other dielectric exposed
   - O₂ concentration in plasma increases (from etch products, carrier gas impurities)
   - Residual Cl⁺ ions gradually oxidized: Cl⁺ + O₂ → ClOₓ⁻ (less energetic)
   - Etch rate decreases as ion energy is distributed to oxide
   - Selectivity mechanism engages: Al/SiO₂ selectivity preserved through ion energy and chemical pathway differentiation

### 2.5 Post-Etch Native Oxide Re-formation

**After etch chamber opens to air (post-process):**

**Scenario 1: Wafer removed immediately (~1 minute after etch end)**
- Residual Cl-containing species (AlCl₃, Cl₂, HCl) present on wafer
- In air: Cl species hydrolyze rapidly
  - AlCl₃ + 3 H₂O → Al(OH)₃ + 3 HCl (hydrolysis reaction)
  - HCl → H⁺ + Cl⁻ (acidic environment)
- Native Al₂O₃ regrows as Al metal oxidizes in humid air
- Native oxide thickness at room temp: 2-4 nm within 5-10 minutes
- Chloride residues: 10-50 ppm Cl typically found by XPS on oxide surface

**Scenario 2: Wafer remains in chamber (in-situ post-etch cleaning)**
- Post-etch plasma (O₂/Ar) applied to remove AlCl₃
- Temperature elevated: 80-120°C
- O₂ plasma oxidizes:
  - AlCl₃ + 3/2 O₂ → Al₂O₃ + 3/2 Cl₂ (desired pathway)
  - Cl₂ exhaust to pump
- However, if temperature too high (>130°C):
  - Al₂O₃ formation becomes dominant
  - Oxide thickness increases from ~3 nm to 5-10 nm during cleaning
- Post-cleaning native oxide: 3-6 nm (balance between formation and sputtering)

**Reliability consequence:** Residual Cl in Al₂O₃ creates:
- **Ionic conductivity:** Chloride ions can drift in oxide under bias, creating leakage paths
- **Accelerated oxidation:** Cl⁻ and oxygen in Al₂O₃ + moisture = accelerated corrosion of remaining Al
- **Electromigration:** Cl⁻ in oxide acts as fast transport path for Al cations (cation-anion pair mechanism)

This is why post-etch cleaning to remove both AlCl₃ *and* residual Cl is critical for reliability.

---

## Part 3: Thermal Budget and Process Integration Constraints

### 3.1 Thermal Stability of Interconnect Stack Components

**Typical interconnect stack at M1 level (after aluminum etch):**

```
Top: Al metal (Al/SiCu alloy)
     ↓ (Cl residues, ~20 ppm)
     Native Al₂O₃ (3-5 nm)
     ↓
Barrier: TiN (10-20 nm)
     ↓
Etch stop: SiO₂ or SiN (30-50 nm)
     ↓
Low-k dielectric: SiOC or porous ULK (100-300 nm, k=2.4-2.8)
     ↓
Underlying interconnect (M0, via, contacts)
```

**Thermal constraints each layer imposes:**

| Layer | Material | Tmax (°C) | Constraint | |
|-------|----------|-----------|---|---|
| **Interconnect** | Al/AlSiCu | 200 | Melting risk; CTE mismatch stress |
| **Native oxide** | Al₂O₃ | — | Stable to any process T; concern is Cl diffusion at T>100°C |
| **Barrier** | TiN | 450 | Decomposition/N₂ loss at T>500°C; okay for interconnect |
| **Etch stop** | SiO₂/SiN | 800 | Thermal budget not limiting for interconnect |
| **Low-k dielectric** | SiOC/ULK | **100-130** | **LIMITING:** Organic content loss, shrinkage, moisture loss above 130°C |
| **Underlying structures** | Various | — | Typically not limiting for local interconnect layers |

**Thermal bottleneck: Low-k dielectric stability**

At T > 130°C, ultra-low-k dielectrics (k=2.0-2.4) used at advanced nodes begin to:
1. **Lose organic content:** Carbon-containing species (Si-OCH₃ groups) decompose
2. **Lose pore structure:** Water trapped in pores evaporates; pores collapse
3. **Experience shrinkage:** 2-5% dimensional change
4. **Increase dielectric constant:** k increases back toward 3.0-3.2 (defeating purpose of ULK)

**Consequence for aluminum etch chamber:**

*Etch process temperature must not exceed ~110-120°C to preserve low-k integrity.*

This is the fundamental driver for:
- Cooled electrode designs (chuck cooled to 10-20°C below process temp)
- Active temperature feedback control (±2-3°C target)
- Careful thermal analysis of RF power dissipation
- Pulsed RF protocols to limit thermal transients

### 3.2 Thermal Management Trade-offs

**Challenge: Maintain 100°C process temperature ±5°C across 300mm wafer**

**Heat sources:**
1. **RF power to plasma:** 500-1500 W, fraction reaches wafer
2. **Ion bombardment heating:** Ions transfer kinetic energy on impact (50-200 eV typical = ~1 eV/Å²)
3. **Chemical reaction exothermy:** Etch reactions release heat (typically 1-5 kcal/mol = small contribution)

**Heat sinks:**
1. **Electrode cooling circuit:** Water or cryogenic (LN₂) cooled chuck
2. **Radiation to chamber walls:** Stefan-Boltzmann at T~100°C, ε~0.3: radiative flux ~50-100 W/m²
3. **Gas flow cooling:** Incoming gas at lower temp cools wafer (small contribution)

**Thermal model (simplified):**

Heat balance on wafer:
$$P_{in} = P_{out}$$

$$P_{RF} + P_{ions} = P_{cond,chuck} + P_{rad} + P_{gas}$$

For steady-state at 100°C:
- RF power to wafer: ~150-250 W (assuming 30-40% of 500-1500 W total)
- Conduction through chuck: Must dissipate ~200-300 W to maintain temperature
- Chuck cooling circuit requirement: Flow rate and ΔT sized accordingly

**Practical cooling design:**
- Cooled chuck at 20-40°C (ΔT_chuck = 60-80°C)
- Wafer sits on chuck with thin (~1 mm) thermally conductive backing plate
- Thermal contact resistance between wafer and chuck: ~1-2 K·cm²/W (critical for uniformity)
- Poor thermal contact → hot spots → local etch rate variation → defects

### 3.3 Thermal Transients and Process Stability

**RF power switching:**
- When RF powers on, wafer heats from 20°C to 100°C target
- Heating timescale: 5-15 seconds (depends on chuck design and power level)
- Temperature overshoot common: wafer reaches 120-130°C before feedback stabilizes

**Consequence for low-k:**
- Brief excursion to 120°C triggers low-k degradation
- Multiple RF pulses during process → cumulative damage
- Over-temperature events reduce low-k effectiveness (k increases permanently)

**Process recipe strategy to minimize thermal overshoot:**
1. **Soft start:** RF power ramped slowly (2-5 seconds to full power) instead of step input
2. **Continuous vs. pulsed:** Continuous power is inherently more stable (no repeated thermal transients); but increases ion flux variation, worsening ARDE
3. **Temperature feedback:** Wafer-mounted thermocouples or pyrometry to measure actual temperature; adjust chuck cooling in real-time

**Trade-off:** Best uniformity etch rates require pulsed power (to control ion flux). Pulsed power creates thermal transients. Solution: Minimize pulse period while maintaining uniformity (typical pulse periods 5-20 ms).

---

## Part 4: Aluminum in Competitive Context

### 4.1 Comparison to Copper Interconnect

**Why copper dominates for global interconnect:**

| Parameter | Al | Cu | Winner | Significance |
|-----------|----|----|--------|---|
| **Resistivity** | 2.65 µΩ·cm | 1.68 µΩ·cm | Cu (37% lower) | RC delay reduction critical for upper layers |
| **Electromigration activation energy** | 0.5-0.7 eV | 0.7-1.0 eV | Cu | Cu more stable under current stress |
| **Thermal conductivity** | 237 W/m·K | 385 W/m·K | Cu | Better thermal management but requires more cooling |
| **Oxidation tendency** | Extreme | Moderate | Cu | Cu oxides (CuO, Cu₂O) less stable than Al₂O₃ |
| **Etch selectivity (to oxide)** | 2-3:1 | <1:1 (poor) | Al | Cu etch attacks oxide; Al selective |
| **Ease of deposition** | Very easy (sputter/evap) | Moderate (ECP or sputter) | Al | Cu requires electrochemical polishing (adds cost/complexity) |

**Why aluminum persists for local interconnect:**

1. **Etch selectivity:** Al/SiO₂ selectivity >1.5:1 enables tight process window; Cu/SiO₂ selectivity <1:1 requires overetch margin → risks underlying structures
2. **Design rule simplicity:** Al etch simpler (single chamber); Cu etch requires damascene (pattern deposition then CMP polish) → adds cost
3. **Lower node support:** Many foundries maintain 180nm, 130nm, 90nm nodes on pure Al; copper introduction adds complexity for legacy processes

### 4.2 Comparison to Tungsten (Vias and Contacts)

**Where tungsten is used:**
- Vias: W plugs in vias connecting metal layers
- Contacts: W between polysilicon and local interconnect (M0)

| Parameter | Al | W | Winner | Note |
|-----------|----|----|--------|---|
| **Resistivity** | 2.65 µΩ·cm | 5.2 µΩ·cm | Al | But W vias are small, so resistance similar despite higher resistivity |
| **Dopant drift** | Susceptible (Al atom migration problematic) | Immune | W | W doesn't form low-melting compounds with Si dopants |
| **Adhesion to oxide** | Excellent (forms Al₂O₃) | Moderate | Al | W needs adhesion layer (TiN); Al self-adhesive |
| **Etch selectivity** | Good (Al/SiO₂ 2:1) | Moderate (W/SiO₂ ~1:1) | Al | But W etch on oxide acceptable; stops on Si |
| **Reliability at high T** | Limited (<200°C) | Excellent (>600°C) | W | W chemical inert; Al undergoes reactions at higher T |

**Why W for vias, not Al:**
- Contact vias expose underlying polysilicon (high dopant concentration)
- Al diffuses into Si, carrying dopants (p-n junction shunting)
- W inert; remains as dopant barrier
- Trade-off: W has higher resistance, but via cross-section is optimized; effective resistance acceptable

---

## Part 5: Thermodynamic and Kinetic Data for Reference

### 5.1 Aluminum Oxidation: Gibbs Free Energy vs. Temperature

$$\Delta G_f^\circ(\text{Al}_2\text{O}_3, T) = -1576.4 + 0.315 \cdot T \text{ (kJ/mol)}$$

| T (K) | T (°C) | ΔGf (kJ/mol) | Oxidation Favorable? |
|-------|--------|------|---|
| 273 | 0 | -1571.7 | Yes (ΔG << 0) |
| 298 | 25 | -1570.6 | Yes |
| 373 | 100 | -1566.9 | Yes |
| 473 | 200 | -1561.1 | Yes |
| 673 | 400 | -1548.1 | Yes |
| 1000 | 727 | -1321.0 | Yes (even at high T) |

**Interpretation:** Aluminum oxidation is thermodynamically favorable at all temperatures up to the melting point (933K = 660°C). No temperature window exists where Al₂O₃ is unstable. This is why native oxide reform is inevitable post-etch.

### 5.2 Native Al₂O₃ Growth Rate (Parabolic Kinetics)

Oxide thickness h(t) = √(2κt) where κ = parabolic rate constant (cm²/s)

**κ vs. temperature (empirical, Mott-Cabrera model):**

$$\log_{10}(\kappa) = -5.2 - \frac{1500}{T(\text{K})}$$

| T (°C) | κ (nm²/s) | Oxide thickness after 1 hour | Oxide thickness after 10 minutes |
|--------|-----------|-------|-------|
| 20 (room air, typical) | 0.008 | 2.2 nm | 0.7 nm |
| 50 | 0.020 | 3.5 nm | 1.1 nm |
| 100 (etch process temp) | 0.065 | 6.2 nm | 1.9 nm |
| 150 (upper thermal limit) | 0.18 | 11.0 nm | 3.3 nm |

**Key observation:** At 100°C (typical etch process temperature), native oxide thickness saturates around 3-5 nm within 10-30 minutes of air exposure. In a 45-minute etch cycle, this provides buffer thickness for ion dose to clear.

### 5.3 Al₂O₃ Properties Table (Reference)

| Property | Value | Units | Source / Notes |
|----------|-------|-------|---|
| **Crystal Structure** | Corundum (α-Al₂O₃) | — | Trigonal, R-3c space group |
| **Density** | 3.97 | g/cm³ | Solid Al₂O₃ |
| **Lattice parameters** | a = 4.758 Å, c = 12.991 Å | — | — |
| **Melting point** | 2072 | °C | Highest melting point of common oxides |
| **Hardness (Vickers)** | 1900 | HV | Second only to diamond |
| **Young's modulus** | 345 | GPa | Extremely stiff |
| **Thermal conductivity (300K)** | 30 | W/m·K | Excellent insulator but conducts heat by phonons |
| **Thermal expansion (CTE)** | 5.3 | ppm/K | 10× higher than SiO₂ |
| **Dielectric constant** | 9.3 | — | At 1 MHz |
| **Bandgap** | 8.8 | eV | Transparent to visible; UV opaque |
| **Refractive index (633 nm)** | 1.76 | — | Used in OES diagnostics |
| **Dissolution in HCl** | Slow | — | Requires hours at elevated temperature |
| **Dissolution in NaOH (1M)** | Rapid | — | Amphoteric: Al₂O₃ + 2NaOH + 3H₂O → 2Na[Al(OH)₄] |

---

## Part 6: Integration with Etch Process Design

### 6.1 Process Implications of Al Thermodynamics

**Challenge 1: Native oxide penetration**
- Etch must penetrate 2-5 nm native oxide before Al exposed
- Sputtering yield for oxide: ~0.5 atoms/ion at 100 eV (lower than metal)
- Required ion flux: ~1000 ions/nm² (20-50 µC/cm² charge)
- At typical current density 1-2 mA/cm², this takes 10-25 seconds
- Solution: Recipe design includes "oxide clear" phase with elevated power to quickly remove native oxide

**Challenge 2: Selectivity to SiO₂ etch stop**
- Al₂O₃ etch rate in Cl₂ plasma: Cl⁺ ions sputter Al₂O₃ at 0.5-1.0 atoms/ion
- SiO₂ etch rate: Cl⁺ ions sputter SiO₂ at 0.3-0.5 atoms/ion
- Both oxides etch slowly compared to metal
- Selectivity mechanism: Use chemical pathway (HCl vapor) to enhance Al₂O₃ etch without attacking SiO₂
- HCl + Al₂O₃ → AlCl₃(g) (volatile, can reach >100°C sublimation)
- HCl + SiO₂ → SiCl₄ (volatile) + H₂O (condensable at 100°C)
- This selectivity is kinetically derived, not purely thermodynamic

**Challenge 3: Post-etch residue removal**
- AlCl₃ formed during etch must be removed
- Challenge: O₂ plasma (typical residue remover) forms Al₂O₃, not volatile products
- Solution: Controlled in-situ O₂ plasma at 80-100°C:
  - 2AlCl₃ + 3/2 O₂ → Al₂O₃ + 3Cl₂ (desired, at low T/time)
  - If overexposed: Al₂O₃ thickness increases from 3 nm to 8-10 nm
- Process recipe must balance AlCl₃ removal against Al₂O₃ formation

### 6.2 Design of Experiments: Thermal Effects on Aluminum Etch

**Typical DOE structure:**

| Factor | Low Level | High Level | Effect Expected |
|--------|-----------|------------|---|
| **Wafer Temperature** | 80°C | 120°C | Etch rate increases ~2-3%/°C; higher T → more oxidation |
| **Chuck Temperature** | 0°C | 40°C | Wafer T controlled via conduction; affects transient behavior |
| **Thermal ramp time** | 2 min | 10 min | Slow ramp → steady-state sooner; reduces overshoot |
| **RF Power** | 500 W | 1500 W | Higher power → higher T, faster etch, more ion flux variation |
| **Pulse duty cycle** | 20% (pulsed) | 100% (continuous) | Pulsed → thermal transients; continuous → steady but less uniform |

**Expected results (empirical from literature, Lam/Applied Materials tools):**
- Increasing wafer T by 10°C: Etch rate increase 20-30%
- Increasing thermal transient magnitude: ARDE variation increases ±1-2%
- Slow ramp: Better uniformity but longer cycle time (throughput cost)

---

## Key Takeaways

1. **Aluminum's high thermal conductivity (237 W/m·K) is both blessing and curse:**
   - Blessing: Heat dissipates quickly, preventing hot spots
   - Curse: Precise temperature control required; small power variations create large T changes

2. **Native Al₂O₃ re-formation is unavoidable thermodynamically** (ΔGf << 0 at all process temperatures). Process design must account for oxide thickness, regrowth rates, and impact on selectivity.

3. **Thermal budget constraint: <110°C maximum** to preserve low-k dielectric stability; this sets fundamental operating point for aluminum interconnect etch chambers.

4. **Alloy composition (AlCu, AlSi, AlSiCu) affects both etch kinetics and residue chemistry.** Standard modern alloy AlSi(1%)Cu(0.5%) provides best balance of electromigration resistance and thermal stability.

5. **Aluminum selectivity to oxide (1.5-2.5:1) is the process window boundary condition.** This selectivity is mechanistically linked to ion energy, gas chemistry, and surface temperature; it cannot be optimized in isolation.

6. **Post-etch residue (AlCl₃) removal is coupled to Al₂O₃ re-formation.** Balancing complete AlCl₃ removal against excess Al₂O₃ formation requires careful in-situ O₂ plasma timing and temperature control.

---

## References and Further Reading

### Fundamental Thermodynamics
- Kubaschewski, O., Alcock, C. B., & Spencer, P. J. (1993). *Materials Thermochemistry* (6th ed.). Pergamon Press.
- Chase, M. W., et al. (1998). "NIST-JANAF Thermochemical Tables." *Journal of Physical and Chemical Reference Data*, Monograph No. 9.

### Aluminum Oxidation Kinetics
- Cabrera, N., & Mott, N. F. (1948). "Theory of the oxidation of metals." *Reports on Progress in Physics*, 12(1), 163.
- Talbot, D. E. J., & Talbot, J. D. R. (1998). *Corrosion Science and Technology* (2nd ed.). Butterworth-Heinemann.

### Interconnect Materials and Properties
- Demchenko, D. O., et al. (2007). "Aluminum contacts to gallium nitride." In *Properties of Group III Nitrides*. EMIS Datareview Series.
- Ho, P. S., & Leu, J. (1992). "Electromigration in metals." *Reports on Progress in Physics*, 52(3), 301.

### Industrial Process References
- Lam Research Technical Literature. (2022). *Metal Etch White Paper: Aluminum Interconnect at 5nm.* (Proprietary)
- SEMI Standards. (2024). *Guide for Aluminum Etch Process Monitoring.*

### Thermal Effects in Semiconductor Processing
- Reif, R., & Camilletti, J. E. (1997). "The influence of wafer-electrode separation on RF etching uniformity." *Journal of the Electrochemical Society*, 138(5), 1447-1455.

---

**Next Chapter: Chapter 3 — Chlorine Chemistry in Aluminum Plasma (Cl₂, HCl, CCl₄)**

In Chapter 3, we transition from materials science to chemistry: How does Cl₂ dissociate in plasma? What are the reaction pathways to form AlCl₃ and other products? How does HCl or CCl₄ modify the chemistry? We develop the gas-phase kinetics rigorously, building toward the surface chemistry of Chapter 4.

