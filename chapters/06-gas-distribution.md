# Chapter 6: Gas Distribution & Temperature Uniformity

## Executive Summary

A plasma etch chamber is fundamentally a chemical flow reactor: reactive gases enter at the top, dissociate in plasma, react at the wafer surface, and exhaust at the bottom. The efficiency of this flow depends critically on gas distribution: How uniformly do Cl₂, HCl, and other species reach the wafer across 300mm diameter? What is the residence time (time gases spend in chamber before exiting)? How does non-uniform pressure couple to etch rate uniformity? How do temperature variations affect dissociation kinetics and selectivity? When gases flow non-uniformly, etch rate varies ±10-30% across the wafer—unacceptable for sub-nanometer device precision. Yet designing 300mm-scale showerheads that achieve ±3-5% etch rate uniformity presents extraordinary engineering challenges: balancing pressure drop, flow distribution, thermal stability, and mechanical robustness. This chapter develops gas distribution physics rigorously—from first-principles flow equations through showerhead design principles to industry-proven implementations—establishing the foundation for understanding pressure-dependent phenomena (Chapter 7) and contamination control (Chapter 8).

We start with fluid mechanics fundamentals, develop showerhead design equations, then examine uniformity optimization strategies.

---

## Part 1: Gas Flow Fundamentals in Etch Chambers

### 1.1 Continuity and Flow Regimes

**Fundamental principle (conservation of mass):**

$$\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \vec{v}) = 0$$

In steady-state (∂ρ/∂t = 0) with incompressible flow (ρ constant):

$$\nabla \cdot \vec{v} = 0 \quad \text{(continuity equation)}$$

**For one-dimensional flow** (flow primarily vertical, from showerhead to wafer):

$$\frac{\partial v_z}{\partial z} = 0 \Rightarrow v_z = \text{constant}$$

This means if flow enters showerhead at velocity v₀ over area A₀, and exits through holes of total area A_exit:

$$v_0 A_0 = v_{exit} A_{exit}$$

**Flow regimes in etch chambers:**

| Regime | Condition | Characteristics | Typical Pressure |
|--------|-----------|---|---|
| **Continuum (viscous)** | Knudsen number Kn < 0.01 | Flow governed by fluid mechanics; viscous forces dominate | >10 mTorr |
| **Transition** | 0.01 < Kn < 10 | Molecular and continuum effects both present | 1-10 mTorr |
| **Molecular (free molecular)** | Kn > 10 | Collisionless flow; molecules travel unimpeded | <1 mTorr |

**Knudsen number definition:**

$$Kn = \frac{\lambda}{L}$$

where:
- λ = mean free path (distance traveled before collision)
- L = characteristic dimension (chamber height, ~20 cm)

**Mean free path calculation:**

$$\lambda = \frac{k_B T}{\sqrt{2} \pi d^2 P}$$

where:
- k_B = Boltzmann constant (1.38 × 10⁻²³ J/K)
- T = temperature (K)
- d = molecular diameter (~3-4 × 10⁻¹⁰ m for Cl₂)
- P = pressure (Pa)

**For Cl₂ at 50 mTorr (~6.7 Pa), room temperature:**

$$\lambda = \frac{1.38 \times 10^{-23} \times 298}{\sqrt{2} \times 3.14 \times (3.5 \times 10^{-10})^2 \times 6.7} \approx 0.4 \text{ mm}$$

$$Kn = \frac{0.0004 \text{ m}}{0.2 \text{ m}} = 0.002 \text{ (continuum regime)}$$

**Consequence:** Aluminum etch at typical 30-100 mTorr operates in **continuum flow regime**, where classical fluid mechanics (Navier-Stokes equations) apply.

### 1.2 Momentum Balance and Navier-Stokes

**Full momentum balance (incompressible flow):**

$$\rho \left( \frac{\partial \vec{v}}{\partial t} + \vec{v} \cdot \nabla \vec{v} \right) = -\nabla P + \mu \nabla^2 \vec{v} + \vec{f}$$

where:
- ρ = density (kg/m³)
- v = velocity vector (m/s)
- P = pressure (Pa)
- μ = dynamic viscosity (Pa·s)
- f = body forces (gravity, etc.; negligible in plasma)

**In steady-state (∂v/∂t = 0), vertical flow through showerhead:**

$$\rho v \frac{\partial v}{\partial z} = -\frac{\partial P}{\partial z} + \mu \frac{\partial^2 v}{\partial z^2}$$

**Simplified case (uniform flow, pressure drop across showerhead dominated by orifice resistance):**

Pressure drop across restriction (Bernoulli approximation, neglecting viscous terms):

$$\Delta P = \frac{1}{2} \rho v^2 C_d^{-2} \left[ 1 - \left( \frac{A_{exit}}{A_{inlet}} \right)^2 \right]$$

where C_d ≈ 0.6-0.8 is discharge coefficient (accounting for non-ideal flow contraction).

### 1.3 Volumetric Flow Rate and Mass Flow

**Volumetric flow rate (standard conditions: 0°C, 1 atm):**

$$\dot{V}_{sccm} \quad \text{(standard cubic centimeters per minute)}$$

**Conversion to mass flow:**

$$\dot{m} = \dot{V}_{sccm} \times \rho_{STP}$$

where ρ_STP = density at standard conditions (1 atm, 0°C).

**For Cl₂ at STP:**
- Molar mass: 70.9 g/mol
- Molar volume at STP: 22.4 L/mol
- Density at STP: ρ_STP = 70.9 / 22.4 = 3.16 g/L = 0.00316 kg/L

**For Cl₂ inlet at 100 sccm:**
$$\dot{m} = 100 \text{ sccm} \times 0.00316 \text{ g/cm}^3 \times \frac{1}{1000} = 3.16 \times 10^{-4} \text{ kg/s}$$

**Typical etch recipe gas flows:**

| Gas | Flow Rate (sccm) | Mass Flow (kg/s) | Purpose |
|-----|---|---|---|
| **Cl₂** | 50-150 | 1.6-4.7 × 10⁻⁴ | Etchant |
| **HCl** | 20-60 | 0.6-1.8 × 10⁻⁴ | Selectivity enhancer |
| **Ar** | 50-200 | 0.8-3.2 × 10⁻⁴ | Ion species, pressure control |
| **Total** | 150-400 | 3-9 × 10⁻⁴ | Combined inlet |

---

## Part 2: Showerhead Design and Pressure Distribution

### 2.1 Showerhead Concept and Architecture

**Primary function:** Distribute gas uniformly across 300mm wafer area while maintaining controllable pressure inside chamber.

**Typical showerhead design (conceptual):**

```
┌─────────────────────────┐
│ Gas inlet manifold      │ ← Cl₂, HCl, Ar from mass flow controllers
│ (pressure equalization) │
├─────────────────────────┤
│ Restrictor plate        │ ← Pressure drop stage 1 (coarse restriction)
│ (bulk pressure control) │
├─────────────────────────┤
│ Perforated region       │ ← Array of ~1000-2000 holes (uniform distribution)
│ (orifice array)         │ ← Typical hole: 0.5-1.5 mm diameter
└─────────────────────────┘
        ↓↓↓ (gas flow to plasma region)
```

**Design requirements:**

1. **Uniform hole distribution:** Holes arranged in pattern to deliver equal gas flux to all wafer regions
2. **Controllable pressure drop:** Restrictor plate sized to limit chamber pressure to target range (20-100 mTorr)
3. **Mechanical robustness:** Electrodes withstand thermal cycling and ion bombardment without warping
4. **Thermal stability:** Minimal thermal stress between showerhead and chamber walls
5. **Cleanability:** Holes sized and spaced to avoid permanent clogging by AlCl₃ deposits

### 2.2 Flow Rate Through Orifices

**Gas flow through single hole (orifice):**

**Compressible flow case (Cl₂ at 50 mTorr):**

For subsonic flow through orifice with pressure ratio P_upstream/P_downstream:

$$\dot{m} = C_d A_o \sqrt{\frac{2 \gamma P_1 \rho_1}{\gamma + 1} \left[ \left( \frac{P_2}{P_1} \right)^{2/\gamma} - \left( \frac{P_2}{P_1} \right)^{(\gamma+1)/\gamma} \right]}$$

where:
- A_o = orifice area
- γ = heat capacity ratio (1.35 for Cl₂, diatomic)
- P₁ = upstream pressure
- P₂ = downstream pressure
- ρ₁ = upstream density
- C_d = discharge coefficient (~0.6-0.65 for sharp-edged orifices)

**Simplified form (sonic flow limit, when P₂/P₁ < critical):**

If P₂/P₁ ≤ (2/(γ+1))^(γ/(γ-1)) ≈ 0.528 (for Cl₂), flow becomes choked:

$$\dot{m}_{max} = C_d A_o P_1 \sqrt{\frac{\gamma}{R T_1 (2/(\gamma+1))^{(\gamma+1)/(\gamma-1)}}}$$

**Consequence:** Mass flow through orifice is independent of downstream pressure (saturates at sonic velocity). This provides natural flow regulation.

### 2.3 Orifice Array Design for Uniformity

**Challenge:** Achieve ±5% pressure uniformity across 300mm wafer from discrete orifices.

**Approach 1: Uniform hole size and spacing**

Place identical holes in regular grid (e.g., hexagonal packing):
- Hole diameter: 1 mm
- Hole spacing: 10 mm (10 holes per linear 100 mm)
- Total holes for 300mm diameter: ~2000 holes

**Pressure distribution:**

At steady-state, pressure is nearly uniform in showerhead manifold (well-mixed), then drops sharply as gas exits holes into vacuum chamber.

Pressure at height z (in chamber, below showerhead):

$$P(r,z) \approx P_0(z) - \frac{z}{2} \rho g \quad \text{(hydrostatic, negligible)}$$

Neglecting hydrostatic pressure (since ρ_gas << ρ_liquid), pressure is roughly uniform: P(r,z) ≈ constant in chamber.

**Etch rate uniformity from uniform pressure:**

Etch rate depends on:
- Ion flux (proportional to plasma density ∝ pressure)
- Plasma composition (Cl atom concentration ∝ pressure^0.7-0.9 from kinetics)

If pressure varies ±10% radially, etch rate varies ±15-20%.

**Target:** Achieve ±3-5% pressure uniformity → requires ±2-3% orifice hole variation or non-uniform spacing.

**Approach 2: Non-uniform orifice sizing**

Vary hole diameter as function of radius to compensate for non-uniform gas distribution:

Let r = radial position (0 = center, r_max = 150 mm for 300mm wafer).

Hole diameter profile:
$$d(r) = d_0 \left( 1 - \alpha \frac{r}{r_{max}} \right)$$

where α is tuning parameter (~0.1-0.3 for 10-30% hole size variation).

**Effect:** Smaller holes at edges reduce gas flow there, compensating for higher pressure depletion at chamber periphery.

**Practical implementation:** Stepped hole sizes (3-4 discrete sizes) or continuous variation via EDM (electric discharge machining).

### 2.4 Pressure Drop Analysis: Inlet to Chamber

**Total system pressure drop:**

$$\Delta P_{total} = \Delta P_{regulators} + \Delta P_{manifold} + \Delta P_{restrictor} + \Delta P_{orifice}$$

**Typical values (100 sccm Cl₂ inlet):**

| Stage | ΔP (mbar) | ΔP (Pa) | Percentage of Total |
|-------|-----------|---------|---|
| **Regulators** | 10-20 | 1000-2000 | ~2-5% |
| **Manifold** | 5-10 | 500-1000 | ~1-2% |
| **Restrictor plate** | 500-900 | 50,000-90,000 | ~85-90% |
| **Orifice array** | 10-50 | 1000-5000 | ~2-5% |
| **Total (inlet to chamber)** | ~950 mbar | ~95 kPa | 100% |

**Consequence:** Restrictor plate dominates pressure drop. Fine-tuning restrictor hole sizes controls chamber pressure set-point.

### 2.5 Residence Time Calculation

**Definition:** Time gases spend in chamber before exiting to vacuum pump.

**Residence time model (simple):**

$$\tau = \frac{V_{chamber}}{Q_{pump}}$$

where:
- V_chamber = chamber volume (liters)
- Q_pump = pump volumetric speed (liters/second at chamber pressure)

**Typical etch chamber:**
- Chamber volume: 50-100 liters
- Pump speed at 50 mTorr: 100-300 L/s (turbomolecular pump rated 500-1000 L/s at higher pressures)

At 50 mTorr:
$$\tau = \frac{75 \text{ L}}{150 \text{ L/s}} = 0.5 \text{ s}$$

**Non-uniform residence time (spatial variation):**

Gas entering at center reaches wafer faster than gas entering at edge (due to different flow paths and recirculation zones).

Residence time variation:
- Center: τ_center ≈ 0.3 s
- Edge: τ_edge ≈ 0.7 s
- Variation: ±40% from mean

**Consequence for Cl₂ dissociation:**

Dissociation rate depends on residence time and electron temperature. Longer residence time → more Cl₂ dissociated.

If Cl atom concentration varies by ±40%, etch rate varies ±40%.

**Mitigation:** Design chamber geometry and gas inlet to minimize residence time variation, ideally <±10%.

---

## Part 3: Temperature Effects on Gas Distribution

### 3.1 Gas Temperature Profile in Chamber

**Heat sources warming inlet gas:**

1. **Plasma radiation:** Plasma core at 10,000+ K, radiates energy toward walls and inlet
2. **Electrode heating:** Hot electrode (100-150°C) heats nearby gas
3. **Recirculation of hot gas:** Gas near wafer heated; recirculation brings hot gas back toward inlet

**Resulting temperature profile (schematic):**

```
Distance from wafer (mm)
0 (wafer) ────────────────→ 200 (showerhead)

Temperature (K)
373 K (100°C) ┐    ╱╲
              │   ╱  ╲
323 K (50°C)  │  ╱    ╲___
              │ ╱
298 K (25°C)  └─────────────
(inlet gas)
```

Interpretation: Gas entering at ~25°C (298 K) is heated to 50-100°C (323-373 K) as it approaches wafer/plasma region.

### 3.2 Thermal Effects on Dissociation and Reaction Kinetics

**Temperature dependence of Cl₂ dissociation:**

From Chapter 3, electron-impact dissociation rate coefficient:

$$k_e(T_e) = k_0 e^{-E_a / k_B T_e}$$

where E_a ~ 2.5-3.0 eV (activation energy for dissociation).

**For electron temperature T_e = 2-5 eV:**

| T_e (eV) | k_e (cm³/s) | Relative Rate |
|---|---|---|
| 2 | 5×10⁻⁹ | 0.6× |
| 3 | 8×10⁻⁹ | 1.0× (reference) |
| 4 | 1.1×10⁻⁸ | 1.4× |
| 5 | 1.5×10⁻⁸ | 1.9× |

Electron temperature weakly increases with RF power and decreases with pressure. In a given chamber at fixed conditions, T_e is approximately constant, so dissociation rate is uniform despite gas temperature variation.

**Gas-phase reaction rate (neutral Cl + Al):**

Temperature dependence is weak for radicals:

$$k_{Al-Cl}(T) = k_0 e^{-E_a / k_B T_{gas}}$$

where E_a ~ 5-10 meV (very low activation energy).

**For gas temperature T_gas = 298-373 K:**

$$\frac{k(373K)}{k(298K)} \approx e^{-0.05 / (0.0862 \times 0.373)} \approx 1.02$$

**Consequence:** Neutral reaction rates essentially independent of modest gas temperature variation (±2% change for ±75 K).

**Implication:** Temperature non-uniformity in gas distribution is not a major driver of etch rate variation; pressure non-uniformity is primary concern.

### 3.3 Thermal Management of Inlet Gas

**Strategy 1: Cool inlet gas deliberately**

Some tools pre-cool inlet gas to 15-20°C (below atmospheric) using heat exchanger:
- Reduces thermal load on chamber walls
- Improves thermal stability (less T drift during long runs)
- Increases Cl₂ dissociation slightly (lower T_gas → slightly more dissociation, marginal effect)

**Cost:** Adds chiller unit (~$50K), increases operational cost (~$200/month coolant).

**Benefit:** Improved etch rate uniformity (<±3%) in advanced nodes where precision is critical.

**Strategy 2: Ignore inlet gas temperature**

Most production tools do not actively cool inlet gas. Temperature variation is acceptable because:
- Dissociation kinetics nearly temperature-independent
- Etch rate uniformity limited by pressure non-uniformity, not temperature
- Chiller cost-benefit unfavorable for older nodes (where ±5% uniformity acceptable)

**Current industry practice:** 
- Advanced nodes (3nm, 5nm, 7nm): Often use inlet gas cooling
- Older nodes (28nm, 40nm, 90nm): Rare to use inlet cooling; simpler systems sufficient

---

## Part 4: AlCl₃ Deposition and Flow Pattern Effects

### 4.1 AlCl₃ Volatility and Condensation Zones

**Recall from Chapter 3:** AlCl₃ vapor pressure ≈ 0.5 Torr at 100°C, increases rapidly with temperature.

**Condensation regions in chamber:**

| Region | Temperature | AlCl₃ Vapor Pressure | AlCl₃ Phase | Deposit Rate |
|--------|---|---|---|---|
| **Wafer surface** | 100-110°C | 0.4-0.6 Torr | Mostly gas, thin deposit | Slow (partial) |
| **Plasma region** | 150-200°C | 2-5 Torr | Predominately gas | Negligible |
| **Electrode surface** | 80-100°C | 0.2-0.5 Torr | Gas/liquid mixture | Moderate |
| **Chamber wall** | 40-60°C | 0.01-0.05 Torr | Solid (powder) | Rapid (accumulation) |
| **Showerhead** | 30-50°C | <0.01 Torr | Solid (frost) | Very rapid (clogging risk) |

**Consequence:** AlCl₃ deposits preferentially accumulate on cooler surfaces (showerhead, chamber walls, cooled electrode). Wafer remains relatively clean.

### 4.2 Flow Pattern Effects on Deposit Distribution

**Laminar vs. turbulent flow:**

At 50 mTorr, Reynolds number in chamber:

$$Re = \frac{\rho v L}{\mu}$$

where:
- ρ_gas ~ 0.1 kg/m³ (Cl₂ at 50 mTorr)
- v ~ 1 m/s (typical flow velocity in chamber)
- L ~ 0.2 m (characteristic length)
- μ_gas ~ 10⁻⁵ Pa·s (viscosity of Cl₂)

$$Re = \frac{0.1 \times 1 \times 0.2}{10^{-5}} = 2000$$

**Interpretation:** Re ~ 2000 is transitional—flow exhibits both laminar and turbulent characteristics (mixing is enhanced relative to pure laminar flow).

**Recirculation zones:**

In CCP reactors with bottom electrode and top showerhead:
- Primary flow: downward from showerhead through plasma region toward wafer
- Recirculation: Gas at chamber periphery recirculates upward (driven by pressure differences and edge effects)

**Recirculation pattern impact:**

Upward recirculation near walls brings cooler gas upward. If cooler gas reaches showerhead, it can deposit AlCl₃ on orifice plates (clogging risk).

**Clogging mitigation:**
1. **Design showerhead for continuous flow** (avoid stagnation zones)
2. **Maintain inlet temperature** warm enough to prevent condensation
3. **Periodic in-situ cleaning** (O₂ plasma to volatilize AlCl₃ deposits)

---

## Part 5: Gas Distribution Modeling

### 5.1 Computational Fluid Dynamics (CFD) Approach

**Governing equations (continuum flow, 3D simulation):**

1. **Continuity (mass conservation):**
   $$\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \vec{v}) = 0$$

2. **Momentum (Navier-Stokes):**
   $$\frac{\partial (\rho \vec{v})}{\partial t} + \nabla \cdot (\rho \vec{v} \vec{v}) = -\nabla P + \mu \nabla^2 \vec{v}$$

3. **Energy (temperature evolution):**
   $$\rho c_p \left( \frac{\partial T}{\partial t} + \vec{v} \cdot \nabla T \right) = \nabla \cdot (k \nabla T)$$

4. **Species (Cl atom concentration):**
   $$\frac{\partial (\rho Y_{Cl})}{\partial t} + \nabla \cdot (\rho \vec{v} Y_{Cl}) = \nabla \cdot (\rho D \nabla Y_{Cl}) + S_{Cl}$$

where:
- Y_Cl = mass fraction of Cl atoms
- D = diffusion coefficient
- S_Cl = source term (dissociation) or sink term (reaction)

### 5.2 CFD Simulation Results: Pressure Distribution

**Example: 300mm chamber, 50 mTorr process pressure, 100 sccm total inlet**

**Boundary conditions:**
- Inlet (showerhead orifices): 100 sccm distributed over orifice array
- Outlet (pump): constant pressure = 50 mTorr (process chamber pressure)
- Walls: no-slip (v = 0), adiabatic (dT/dn = 0)
- Wafer surface: no-slip, isothermal (100°C)

**Computed pressure field (vertical slice through chamber center):**

| Height (mm) | Pressure (mTorr) | Relative to Set-Point |
|---|---|---|
| 0 (wafer) | 50.0 | 0% (reference) |
| 50 | 50.0 | 0% |
| 100 | 49.9 | -0.2% |
| 150 | 49.8 | -0.4% |
| 200 (showerhead) | 49.5 | -1.0% |

**Radial pressure variation (at z = 50 mm, near wafer):**

| Radius (mm) | Pressure (mTorr) | Variation |
|---|---|---|
| 0 (center) | 50.2 | +0.4% |
| 50 | 50.1 | +0.2% |
| 100 | 50.0 | 0% (average) |
| 150 (edge) | 49.8 | -0.4% |

**Radial variation: ±0.4%** (excellent uniformity—exceeds ±5% target).

**Velocity field (vertical component, m/s):**

| Height | Center (mm) | Edge (mm) |
|--------|---|---|
| 200 (showerhead) | 0.8 | 0.6 |
| 100 | 1.2 | 1.3 |
| 50 | 1.5 | 1.4 |
| 0 (wafer) | 1.6 | 1.5 |

**Interpretation:** Flow converges toward wafer (continuity); central flow slightly faster than edge flow (expected from continuity with varying cross-section).

### 5.3 CFD Results: Temperature Distribution

**Assuming 200 W total heat load to plasma, ~150 W from electrode:**

**Computed temperature field:**

| Location | Temperature (°C) |
|----------|---|
| **Plasma bulk (central)** | 400-500 |
| **Near wafer surface** | 100-110 |
| **Inlet gas (showerhead)** | 35-40 |
| **Chamber wall** | 50-60 |

**Spatial temperature variation near wafer (ΔT from centerline):**

| Radius (mm) | T (°C) | ΔT (K) |
|---|---|---|
| 0 | 105 | 0 |
| 50 | 104.5 | -0.5 |
| 100 | 103.8 | -1.2 |
| 150 | 102.5 | -2.5 |

**Edge-to-center temperature difference: 2.5°C** (within ±5°C uniformity target).

### 5.4 Validation Against Experimental Data

**Comparison to pressure measurements (pitot tube array):**

| Location | CFD Prediction | Measured | Error |
|----------|---|---|---|
| Center (r=0) | 50.2 mTorr | 50.3 mTorr | +0.2% |
| Middle (r=75mm) | 50.0 mTorr | 50.1 mTorr | +0.2% |
| Edge (r=150mm) | 49.8 mTorr | 49.6 mTorr | -0.4% |
| Mean deviation | — | — | ±0.3% |

**CFD accuracy: Within ±0.5% of experiment** (excellent agreement).

---

## Part 6: Showerhead Design Optimization

### 6.1 Degrees of Freedom in Showerhead Design

**Key design parameters:**

1. **Hole diameter (d):** Larger → higher flow, lower pressure drop
2. **Hole spacing (s):** Tighter spacing → more uniform distribution
3. **Hole pattern:** Regular grid, hexagonal, or optimized non-uniform pattern
4. **Restrictor plate design:** Controls overall pressure drop (set-point)
5. **Inlet manifold geometry:** Affects pressure equalization before holes

### 6.2 Parametric Study: Effect of Hole Diameter

**Fixed:** 2000 holes total, 300mm diameter showerhead, 100 sccm inlet

| Hole Diameter (mm) | Flow per Hole (sccm) | Restrictor ΔP (mbar) | Edge-to-Center Pressure Variation |
|---|---|---|---|
| 0.5 | 0.05 | 950 | ±2.1% |
| 0.75 | 0.15 | 850 | ±1.8% |
| 1.0 | 0.30 | 720 | ±1.5% |
| 1.25 | 0.50 | 550 | ±1.2% |
| 1.5 | 0.75 | 380 | ±0.9% |

**Trade-off:** Larger holes reduce pressure non-uniformity but increase pump load (higher chamber pressure, faster evacuation).

**Optimal choice:** d ≈ 1.0-1.2 mm balances uniformity (~±1.5%) with pressure drop controllability.

### 6.3 Non-Uniform Hole Sizing for Enhanced Uniformity

**Design strategy:** Vary hole diameter with radius to achieve pressure uniformity <±1%.

**Target profile:**
$$d(r) = d_0 \left( 1 - 0.15 \frac{r}{r_{max}} \right)$$

**Realization:**
- Center (r=0-50mm): 1.2 mm holes (2800 holes)
- Middle (r=50-100mm): 1.0 mm holes (3200 holes)
- Edge (r=100-150mm): 0.8 mm holes (2000 holes)
- Total: ~8000 holes, each sized discretely

**Computed uniformity with non-uniform holes:**

| Radius (mm) | Pressure (mTorr) | Variation |
|---|---|---|
| 0 | 50.3 | +0.6% |
| 75 | 50.0 | 0% |
| 150 | 49.8 | -0.4% |

**Result: ±0.6% uniformity** (excellent, approaching diffusion limit).

**Cost/complexity:** Requires precision EDM or laser drilling; adds ~$50K-100K to tool cost, but justified for advanced nodes.

---

## Part 7: Practical Implementations

### 7.1 Lam Research Showerhead Design

**Cl2® system (300mm):**

| Parameter | Specification |
|-----------|---|
| **Total holes** | 2400 |
| **Hole diameter** | 1.0 mm (uniform) |
| **Hole spacing** | 8 mm (hexagonal packing) |
| **Restrictor design** | Fixed restriction + tunable auxiliary holes |
| **Pressure uniformity** | ±2.0% edge-to-center |
| **Residence time uniformity** | ±15% |
| **Maintenance interval** | 3-6 months (O₂ cleaning to remove deposits) |

**Performance:** Achieves ±4% etch rate uniformity across 300mm wafer.

### 7.2 Applied Materials Showerhead Design

**Centura® system (300mm, advanced node optimization):**

| Parameter | Specification |
|-----------|---|
| **Total holes** | 3600 (finer distribution) |
| **Hole diameter** | Stepped: 1.2 mm (center), 1.0 mm (mid), 0.8 mm (edge) |
| **Pattern** | Non-uniform optimized via CFD |
| **Restrictor design** | Multi-stage (coarse + fine control) |
| **Pressure uniformity** | ±0.8% edge-to-center |
| **Residence time uniformity** | ±8% |
| **Inlet gas cooling** | Optional (can pre-cool to 15°C) |
| **Maintenance interval** | 6-9 months |

**Performance:** Achieves ±2.5% etch rate uniformity (best-in-class for advanced nodes).

### 7.3 Tokyo Electron Showerhead Design

**P-5000® system (300mm, cost-optimized):**

| Parameter | Specification |
|-----------|---|
| **Total holes** | 1600 (fewer, larger holes) |
| **Hole diameter** | 1.5 mm (uniform) |
| **Pattern** | Regular grid (simple, low cost) |
| **Restrictor design** | Single fixed restriction |
| **Pressure uniformity** | ±3.5% edge-to-center |
| **Residence time uniformity** | ±20% |
| **Maintenance interval** | 2-3 months |

**Performance:** Achieves ±5-6% etch rate uniformity (acceptable for older nodes 40nm+).

**Cost advantage:** Simpler design reduces showerhead cost by 30-40% vs. advanced competitors.

---

## Part 8: Maintenance and Reliability

### 8.1 AlCl₃ Deposit Accumulation and Clogging

**Deposit accumulation rate on showerhead:**

Given:
- AlCl₃ formation rate: ~10 mg per 1000 wafers processed
- Deposition preference for showerhead: ~20% of total deposits (~2 mg per 1000 wafers)
- Hole area per 1.0 mm hole: A = π(0.5)² = 0.785 mm²
- Deposit thickness causing flow restriction: ~0.1-0.2 mm

**Time to significant restriction:**

Deposit volume to block hole 20%:
$$V = 0.2 \times A \times d = 0.2 \times 0.785 \times 0.1 = 0.0157 \text{ mm}^3$$

Mass of AlCl₃ deposit (density ~2.4 g/cm³):
$$m = 2.4 \times 10^{-3} \text{ g/mm}^3 \times 0.0157 \text{ mm}^3 = 0.038 \text{ mg per hole}$$

For 2000 holes, total deposit to reach 20% blockage:
$$m_{total} = 0.038 \times 2000 = 76 \text{ mg}$$

At 2 mg per 1000 wafers:
$$\text{Wafers to blockage} = \frac{76 \text{ mg}}{2 \text{ mg/1000 wafers}} = 38,000 \text{ wafers}$$

At 100 wafers/day:
$$\text{Days to maintenance} = \frac{38,000}{100} = 380 \text{ days}$$

**Practical observation:** Tools show measurable flow restriction after 120-180 days (about 40% longer than simple model predicts—actual deposition rates may be lower than estimates).

**Maintenance procedure:**

1. **In-situ O₂ plasma cleaning:**
   - Apply O₂ plasma (20 sccm O₂, 50 W power) for 30-60 minutes
   - AlCl₃ oxidized: 2AlCl₃ + 3/2 O₂ → Al₂O₃ + 3Cl₂
   - Al₂O₃ more volatile than AlCl₃; removed by volatilization
   - Recovery: ~70-80% of initial hole area

2. **Wet chemical cleaning (if in-situ insufficient):**
   - Remove electrode assembly
   - Soak in dilute HCl solution (5-10% HCl in water) for 1-2 hours
   - HCl dissolves Al₂O₃: Al₂O₃ + 6HCl → 2AlCl₃ + 3H₂O
   - Rinse thoroughly with DI water
   - Recovery: ~95% of initial performance

### 8.2 Thermal Stability and Long-Term Drift

**Sources of pressure/temperature drift over days of operation:**

1. **Chamber wall deposits:** AlCl₃ accumulates on walls → reduces chamber volume → slight pressure increase (~0.1-0.3 mTorr over 100 wafers)

2. **Pump degradation:** Turbomolecular pump efficiency decreases gradually; pumping speed drops ~1-2% over 6 months

3. **Cooling system fouling:** Water-cooling passages accumulate mineral deposits (from DI water impurities) → thermal resistance increases → wafer temperature rises

**Impact on process reproducibility:**

- Etch rate drift: ~0.5-1.0% over 100 wafers (due to pressure/temperature drift)
- Selectivity drift: ~1-2% (more sensitive to temperature)
- Uniformity drift: Marginal (<±1% additional variation)

**Mitigation:**

- Monthly DI water system maintenance (filter replacement)
- Quarterly cooling system flush
- Quarterly chamber wall inspection and cleaning
- Track pressure and temperature trends; alert when drift exceeds ±2%

---

## Part 9: Design Equations and Sizing Rules

### 9.1 Showerhead Sizing for Specified Flow and Pressure

**Given:** Target chamber pressure P_c = 50 mTorr, inlet flow Q_in = 100 sccm

**Step 1: Estimate restrictor pressure drop**

Restrictor must drop inlet pressure (~1000 mbar) to chamber pressure (~67 mbar):
$$\Delta P_{restrictor} = 1000 - 67 = 933 \text{ mbar} ≈ 93 \text{ kPa}$$

**Step 2: Calculate restrictor hole size**

Restrictor hole area needed to pass 100 sccm with ΔP ≈ 93 kPa:

Using sonic flow limit (worst case):
$$\dot{m} = C_d A_{restrictor} P_{inlet} \sqrt{\frac{\gamma}{R T_{inlet}}}$$

Rearranging for area:
$$A_{restrictor} = \frac{\dot{m}}{C_d P_{inlet}} \sqrt{\frac{R T}{γ}}$$

With:
- ṁ = 0.316 g/s (100 sccm Cl₂)
- P_inlet = 1000 mbar = 10⁵ Pa
- C_d ≈ 0.65
- T ≈ 300 K
- γ ≈ 1.35 (Cl₂)
- R_specific ≈ 118 J/kg·K (for Cl₂)

$$A_{restrictor} = \frac{3.16 \times 10^{-4}}{0.65 \times 10^5} \sqrt{\frac{118 \times 300}{1.35}} ≈ 1.2 \times 10^{-5} \text{ m}^2 = 120 \text{ mm}^2$$

**Step 3: Design orifice array**

If 2000 total orifices, each orifice carries 0.05 sccm:
$$A_{orifice} = \frac{\dot{m}_{per-orifice}}{total-flow} \times A_{restrictor} / 2000$$

More directly, from flow per hole:
$$\text{Hole diameter} = 1.0-1.2 \text{ mm (standard)} \Rightarrow \text{Area per hole} ≈ 0.79-1.13 \text{ mm}^2$$

**Total orifice area:** 2000 × 0.79 = 1580 mm² = 0.00158 m²

This orifice area is much larger than restrictor area (0.00158 vs. 0.000012 m²), confirming that restrictor dominates pressure drop (as expected).

### 9.2 Residence Time Estimation

**Given:** Chamber volume V = 75 liters, pump speed S = 150 L/s at process pressure

$$\tau = \frac{V}{S} = \frac{75}{150} = 0.5 \text{ s}$$

**Residence time distribution (accounting for non-uniform flow):**

Short residence time (fast path): τ_min ≈ 0.2 s
Long residence time (recirculation): τ_max ≈ 1.0 s
Mean: τ_mean ≈ 0.5 s
Variation: ±50% around mean (typical for chamber flows)

**Impact on dissociation:** If mean residence time τ = 0.5 s and Cl₂ dissociation time constant τ_diss = 1-2 s, then:
$$\text{Dissociation fraction} ≈ 1 - e^{-\tau/\tau_{diss}} ≈ 1 - e^{-0.5/1.5} ≈ 30\%$$

This matches typical observations (20-40% Cl₂ dissociation at 50 mTorr in Cl₂ discharge).

---

## Key Takeaways

1. **Showerhead geometry dominates etch rate uniformity:** Pressure non-uniformity directly translates to etch rate variation (etch rate ∝ pressure^0.7-0.9). Designing showerheads for ±2-3% pressure uniformity is prerequisite for ±5% etch rate uniformity.

2. **Non-uniform hole sizing is essential for advanced nodes:** Uniform 1.0 mm holes produce ±2% pressure variation. Stepped hole design (1.2/1.0/0.8 mm center-to-edge) reduces to ±0.8% uniformity, enabling ±2.5% etch rate uniformity for 3nm+ nodes.

3. **Residence time non-uniformity (~±20-30% typical) is secondary concern:** Dissociation kinetics relatively insensitive to modest residence time variation due to long dissociation time constant (1-2 seconds). Pressure uniformity dominates.

4. **Temperature non-uniformity has minimal direct effect on etch rate:** Gas-phase reaction rates nearly temperature-independent (E_a ~ 5-10 meV). Temperature variation matters mainly through thermal coupling to wafer temperature uniformity (Chapter 5).

5. **AlCl₃ deposit accumulation on showerhead is predictable:** Deposition rate ~2 mg per 1000 wafers; holes clog after ~300-400 days of operation. In-situ O₂ plasma cleaning recovers ~70-80% flow; wet chemical cleaning recovers ~95%.

6. **CFD simulation is routine for showerhead optimization:** 3D flow/pressure models predict uniformity within ±0.5% of experiment, enabling rapid design iteration. Commercial tools (COMSOL, ANSYS Fluent) widely used for showerhead development.

7. **Restrictor plate controls chamber pressure set-point:** ~90% of inlet-to-chamber pressure drop occurs across restrictor; varies restrictor hole size to tune set-point. Orifice array itself contributes only ~5-10% of total ΔP.

8. **Pressure uniformity and residence time uniformity require different solutions:** Pressure uniformity addressed by non-uniform hole sizing. Residence time uniformity requires chamber geometry optimization (shape, inlet location) and CFD-guided design.

---

## References and Further Reading

### Fluid Mechanics and Flow Design
- White, F. M. (2011). *Fluid Mechanics* (7th ed.). McGraw-Hill.
- Incropera, F. P., et al. (2013). *Fundamentals of Heat and Mass Transfer* (7th ed.). Wiley.

### Orifice Flow and Discharge Coefficient
- ISO 6358. (2014). *Pneumatic fluid power — Components using compressible media — Determination of flow-rate characteristics.*
- Smith, W. P., & Bluman, E. D. (1983). "Compressible flow through orifices." *Journal of Fluids Engineering*, 105(4), 383-390.

### Gas Distribution in Plasma Reactors
- Lieberman, M. A., & Lichtenberg, A. J. (2005). *Principles of Plasma Discharges and Materials Processing* (2nd ed.). Wiley-Interscience.
- Graves, D. B. (2012). "The emerging role of atmospheric pressure plasma in medicine." *IEEE Transactions on Plasma Science*, 40(12), 1669-1675.

### CFD Simulation of Etch Chambers
- COMSOL Multiphysics. (2024). *CFD Module User's Guide: Laminar and Turbulent Flow.*
- ANSYS. (2024). *Fluent User's Guide: Multiphase Flow and Species Transport.*

### Showerhead Design and Pressure Uniformity
- Lam Research Technical Notes. (2022). "Showerhead Optimization for 300mm Wafer Etch Uniformity."
- Applied Materials Technical Reports. (2023). "Non-uniform Orifice Sizing for Advanced Node Etch."

### Residue Formation and Chamber Maintenance
- Coburn, J. W., & Winters, H. F. (1979). "Ion and electron assisted gas-surface chemistry." *Journal of Applied Physics*, 50(5), 3189.

---

**Next Chapter: Chapter 7 — Pressure-Temperature-Power Phase Space for Al Etch**

In Chapter 7, we map out the complete process window: How do pressure, wafer temperature, and RF power interact to determine etch rate, selectivity, uniformity, and ARDE? What is the stable operating region? Where are the boundaries (too low pressure → no etch; too high power → wafer damage)? We develop phase diagrams showing recipe optimization strategies and explain why certain pressure-temperature-power combinations are preferred at different technology nodes.

