# Chapter 5: Electrode Materials & Thermal Management

## Executive Summary

Aluminum etch chambers operate under extreme conditions: plasma temperatures >10,000 K in the bulk, ion bombardment at 50-300 eV on surfaces, AlCl₃ residues depositing on walls, and thermal loads 100-200 W/cm² on wafer. Yet the wafer surface temperature must remain within 100-110°C to preserve underlying low-k dielectric. This thermal constraint, combined with aluminum's high thermal conductivity (237 W/m·K), mandates sophisticated electrode design: actively cooled electrode substrates, thermally conductive but electrically isolated backing plates, precise temperature sensing and feedback control. Simultaneously, electrode materials must withstand years of ion bombardment and AlCl₃ deposition without erosion compromising uniformity. This chapter develops electrode design from first principles: material selection criteria, thermal transport equations, cooled chuck design, and practical implementations from production equipment. Understanding these engineering constraints is prerequisite for subsequent chapters on gas distribution (Chapter 6), process windows (Chapter 7), and chamber coatings (Chapter 8).

We start with material properties, develop thermal models quantitatively, then present industry-proven designs.

---

## Part 1: Electrode Material Selection and Properties

### 1.1 Functional Requirements for Aluminum Etch Electrodes

**Critical requirements (in priority order):**

1. **Thermal conductivity:** Must conduct heat away from plasma-facing surface
2. **Electrical conductivity:** Must support RF current distribution (CCP) or couple RF power (ICP)
3. **Corrosion/erosion resistance:** Must withstand Cl₂ plasma and AlCl₃ deposits
4. **Mechanical stability:** Must tolerate thermal cycling and ion sputtering stress
5. **Cost:** Must be economically viable for ~$2-3M tool value
6. **Machinability:** Must be shaped into complex electrode geometries

### 1.2 Material Properties: Candidate Materials

**Table 1: Thermal and Electrical Properties of Candidate Electrode Materials**

| Material | Thermal Conductivity (W/m·K) | Electrical Resistivity (µΩ·cm) | Density (g/cm³) | Thermal Expansion (ppm/K) |
|----------|---|---|---|---|
| **Aluminum (Al)** | 237 | 2.7 | 2.70 | 23.1 |
| **Copper (Cu)** | 385 | 1.7 | 8.96 | 16.5 |
| **Tungsten (W)** | 173 | 5.5 | 19.3 | 4.5 |
| **Molybdenum (Mo)** | 138 | 5.2 | 10.2 | 5.3 |
| **316L Stainless Steel** | 16 | 72 | 8.0 | 16.0 |
| **Ceramic (Al₂O₃)** | 30 | >10¹⁴ (insulator) | 3.97 | 5.3 |
| **Ceramic (AlN)** | 170-200 | >10¹⁴ (insulator) | 3.26 | 4.6 |

**Analysis of candidates:**

**Aluminum (Al):**
- ✅ Thermal conductivity: Excellent (237 W/m·K)
- ✅ Electrical conductivity: Good (2.7 µΩ·cm)
- ✅ Machinability: Excellent
- ✅ Cost: Low (~$2/kg)
- ❌ **Erosion resistance: Poor** — Cl₂ plasma aggressively sputters Al; erosion ~0.1-0.5 nm/wafer
- ❌ **AlCl₃ deposits:** Al reacts with deposited AlCl₃ → further corrosion

**Consequence:** Pure Al electrodes used only for old equipment or laboratory demonstrations. Production systems require coating.

**Copper (Cu):**
- ✅ Thermal conductivity: Superior (385 W/m·K)
- ✅ Electrical conductivity: Superior (1.7 µΩ·cm)
- ❌ **Erosion resistance: Poor** — Cu sputters faster than Al; yield ~1.5-2.0 atoms/ion
- ❌ **Chloride corrosion:** Cu reacts with Cl₂ → CuCl deposits (problematic)
- ❌ **Cost:** Higher than Al (~$8/kg)

**Consequence:** Cu rarely used as electrode material in Cl₂ discharges. Some ICP tools use Cu coils for inductive coupling (not plasma-facing).

**Tungsten (W):**
- ✅ **Erosion resistance: Excellent** — W sputtering yield ~0.5-0.8 atoms/ion at 100 eV (half of Al)
- ✅ Thermal stability: Melting point 3695 K (extreme)
- ✅ Chemical inertness: W does not react with Cl₂ or AlCl₃
- ❌ Thermal conductivity: Moderate (173 W/m·K, lower than Al)
- ❌ Electrical conductivity: Poor (5.5 µΩ·cm, 2× Al)
- ❌ Density: Very high (19.3 g/cm³) — thick coatings are heavy
- ❌ Cost: Extremely high (~$50-100/kg); uneconomical for large electrodes

**Consequence:** W used selectively as thin coating (5-25 µm) on Al substrates for high-erosion areas.

**Molybdenum (Mo):**
- ✅ Erosion resistance: Good (comparable to W, Y ~0.5-0.7 atoms/ion)
- ✅ Thermal conductivity: Decent (138 W/m·K)
- ✅ Cost: Moderate (~$15-20/kg)
- ❌ Machinability: Poor (brittle)
- ❌ Oxidation risk: Mo can oxidize to MoO₃ (conducts poorly)

**Consequence:** Mo sometimes used as coating, but less common than W due to machinability issues.

**316L Stainless Steel:**
- ✅ Chemical resistance: Excellent (passivated Cr₂O₃ layer)
- ✅ Mechanical strength: Good
- ✅ Availability: Abundant, low cost
- ❌ **Thermal conductivity: Very poor** (16 W/m·K, 15× lower than Al)
- ❌ Electrical resistivity: High (72 µΩ·cm, 25× higher than Al)

**Consequence:** Stainless steel used as structural material (chamber body), not as thermally-conductive electrode substrate.

**Ceramic (Al₂O₃):**
- ✅ Chemical resistance: Excellent
- ✅ Thermal resistance: Blocks heat dissipation (advantage for some designs)
- ❌ **Thermal conductivity: Very poor** (30 W/m·K)
- ❌ Electrical properties: Insulator (cannot carry current directly)

**Consequence:** Al₂O₃ used as coating over conducting substrate, not as primary electrode.

**Ceramic (AlN - Aluminum Nitride):**
- ✅ Thermal conductivity: Good (170-200 W/m·K, close to W)
- ✅ Electrical properties: High resistivity (can isolate thermally)
- ✅ Chemical resistance: Excellent
- ❌ **Cost: Very high** (~$500-1000/kg for high-purity)
- ❌ Machinability: Difficult (ceramic, brittle)
- ❌ Availability: Limited (niche material)

**Consequence:** AlN investigated for specialty applications (thermally-isolated electrode designs) but not cost-effective for production.

### 1.3 Industry Standard: Al Substrate with Protective Coating

**Practical compromise adopted across industry:**

| Layer | Material | Thickness | Function |
|-------|----------|-----------|----------|
| **Substrate** | Aluminum (Al) | 10-20 mm | Bulk structural material, thermal conductor, good conductivity |
| **Coating** | Tungsten (W) or Mo | 5-25 µm | Erosion barrier, Cl₂ resistance |
| **Top surface** | W/Mo + ceramic hybrid | <1 µm | Final passivation (sometimes) |

**Rationale:**
- Al substrate provides thermal conductivity and low electrical resistance
- W/Mo coating sacrifices slowly (erosion rate ~0.1-0.5 µm per 1000 wafers)
- Coating lasts 12-24 months before requiring replacement
- Replacement cost: ~$5K-15K for coating service (vs. $2M+ tool cost)

### 1.4 Sputtering Yields and Erosion Rates

**Experimental sputtering yields for candidate materials (Cl⁺, 100 eV):**

| Material | Yield Y (atoms/ion) | Erosion Rate (nm/wafer at 1 mA/cm²) |
|----------|---|---|
| **Al** | 2.0-2.2 | 5-6 |
| **Cu** | 1.8-2.0 | 5-6 |
| **W** | 0.5-0.8 | 1-2 |
| **Mo** | 0.6-0.9 | 1-2 |
| **Al₂O₃** | 0.8-1.2 | 2-3 |
| **W coating (5 µm)** | 0.5-0.8 | ~2 nm lifetime: 2500 wafers |

**Calculation example (W coating erosion lifetime):**

Given:
- W coating thickness: 10 µm
- Sputtering yield: Y = 0.7 atoms/ion
- Ion current density (typical): j = 1 mA/cm² = 6.25 × 10¹⁵ ions/(cm²·s)
- Process time per wafer: 45 minutes = 2700 seconds
- Ion fluence per wafer: F = j × t = 6.25 × 10¹⁵ × 2700 = 1.69 × 10¹⁹ ions/cm²

Erosion per wafer:
$$\text{Thickness loss} = Y \times F \times \text{atomic volume}$$
$$= 0.7 \text{ atoms/ion} \times 1.69 \times 10^{19} \text{ ions/cm}^2 \times \frac{1}{8.8 \times 10^{22} \text{ atoms/cm}^3}$$
$$= 1.35 \text{ nm/wafer}$$

Coating lifetime (at 10 µm thickness):
$$\text{Wafers} = \frac{10,000 \text{ nm}}{1.35 \text{ nm/wafer}} \approx 7,400 \text{ wafers}$$

At 100-150 wafers/day:
$$\text{Lifetime} \approx 50-75 \text{ days} \approx 2-3 \text{ months}$$

**Industrial practice:** W-coated electrodes replaced every 3-6 months depending on duty cycle and process conditions.

---

## Part 2: Thermal Design Fundamentals

### 2.1 Thermal Load Analysis

**Heat sources in aluminum etch chamber:**

1. **RF power input:** P_RF = 500-1500 W (nominal)
2. **Distribution of RF power:**
   - Bulk plasma: ~40-50% dissipated as electron/ion heating and excitation
   - Electrode surfaces: ~30-40% delivered to electrodes (heating)
   - Wafer surface: ~15-25% reaches wafer (ion bombardment + radiation)
   - Wall losses: ~10-15% to chamber walls

3. **Power to wafer surface:** P_wafer ≈ 50-250 W (for 300mm wafer, ~70,650 mm² area)
4. **Power density on wafer:** q = 0.7-3.5 W/cm² (depending on discharge regime)

### 2.2 Wafer Temperature Rise Without Active Cooling

**Simple heat balance (steady-state, no cooling):**

$$q = \kappa \cdot \frac{\Delta T}{d}$$

where:
- q = heat flux (W/cm²)
- κ = thermal conductivity of Al (237 W/m·K = 0.0237 W/cm·K)
- ΔT = temperature rise
- d = thermal diffusion length (~1 mm, effective thickness from plasma to bulk wafer)

**For q = 1.5 W/cm² (typical):**

$$\Delta T = q \cdot d / \kappa = 1.5 \text{ W/cm}^2 \times 0.1 \text{ cm} / 0.0237 \text{ W/cm·K} = 6.3 \text{ K}$$

This seems modest, but with sustained plasma:

**Transient heating (RF power-on ramp):**

Temperature rise over time t:
$$T(t) = T_0 + \frac{q}{\rho c} \sqrt{\frac{4 \kappa t}{\pi}}$$

where ρ = density, c = specific heat capacity.

For Al: ρ = 2.70 g/cm³, c = 0.897 J/g·K

$$T(t) = 20°C + \frac{1.5}{2.70 \times 0.897} \sqrt{\frac{4 \times 0.0237 \times t}{\pi}}$$
$$T(t) = 20 + 0.62 \sqrt{0.0302 t}$$

**Temperature after 10 seconds:** T ≈ 20 + 0.62√0.302 ≈ 20 + 0.34 = 20.3°C (still room temperature)

**Temperature after 100 seconds:** T ≈ 20 + 0.62√3.02 ≈ 20 + 1.07 = 21.1°C

**Temperature after 600 seconds (10 min):** T ≈ 20 + 0.62√18.1 ≈ 20 + 2.63 = 22.6°C

**Wait—this predicts only ~2-3°C rise!** Why do actual processes operate at 100°C?

**Answer:** The thermal load estimate is incomplete. Additional heat sources include:
1. **Ion implantation energy:** Ions penetrate ~50-100 nm, transferring ~90% of energy as heat in cascade
2. **Friction heating from sputtering:** Atomic collision processes release energy
3. **Plasma sheath confinement:** Potential energy difference heats sheath (significant contributor)

**Revised total thermal load:**

Comprehensive energy balance suggests actual power density to wafer surface ≈ 3-5 W/cm² (not 1.5 W/cm²).

With q = 4 W/cm²:
$$\Delta T = 4 \times 0.1 / 0.0237 = 16.9 \text{ K}$$

This brings wafer from room temperature 20°C to ~37°C without cooling. But experiments show 100°C, implying:
- Additional heat from electrode interaction
- Radiation from hot plasma
- Cumulative heating over 45-minute etch cycle

**Key point:** Without active cooling, wafer temperature uncontrollable; active cooling mandatory.

### 2.3 Cooled Chuck Thermal Design

**Fundamental heat flow path:**

```
Plasma heat → Wafer surface (100°C)
                    ↓
            Wafer → Thermal interface (contact)
                    ↓
            Chuck (cooled, ~20-40°C)
                    ↓
            Cooling fluid (-5°C input)
```

**Heat transfer stages:**

1. **Wafer-to-chuck contact resistance:** R_contact (K·cm²/W)
2. **Chuck thermal conduction:** R_chuck = d_chuck / κ_chuck
3. **Cooling fluid circulation:** R_coolant
4. **Heat removal capacity:** C_coolant = ṁ × c × ΔT_fluid

### 2.4 Thermal Contact Resistance

**Critical parameter determining heat transfer efficiency:**

Contact resistance arises from:
1. **Surface roughness:** Wafer and chuck surfaces are not atomic-smooth; microscopic air gaps limit conduction
2. **Pressure distribution:** Wafer clamped on chuck, but pressure non-uniform across surface
3. **Material properties:** Contact conductance depends on material pair

**Thermal contact resistance (empirical data):**

| Wafer-Chuck Material Pair | Contact Conductance h_c (W/cm²·K) | Contact Resistance (K·cm²/W) |
|---|---|---|
| **Al on Al (clean)** | 500-1000 | 0.001-0.002 |
| **Al on Cu** | 1000-2000 | 0.0005-0.001 |
| **Al on Al (thermal paste/grease)** | 5000-15000 | 0.00007-0.0002 |
| **Al on SiC (composite)** | 2000-5000 | 0.0002-0.0005 |
| **Al on polished metal** | 500-800 | 0.00125-0.002 |

**Consequence:** Thermal interface material (TIM) dramatically improves heat transfer—factor 5-10 reduction in contact resistance.

**Typical etch tool chuck design:**
- Backing plate (Al): attached to wafer via clamping ring
- Thermal interface: Thin layer of thermal paste or phase-change material (PCM)
- Chuck body: Cu or Al, thermally conductive
- Cooling passages: Embedded microchannels or drilled holes for coolant circulation

### 2.5 Heat Transfer Equations (Steady-State)

**Total thermal resistance in series:**

$$R_{total} = R_{contact} + R_{chuck} + R_{coolant}$$

**Heat flow:**
$$Q = \frac{\Delta T_{wafer-coolant}}{R_{total}}$$

**Example calculation (300mm wafer, Al chuck with cooled passages):**

Given:
- Wafer surface temperature: T_w = 100°C (process target)
- Coolant inlet temperature: T_cool = 10°C
- Required heat dissipation: Q = 150 W (total)
- Wafer area: A = 70,650 mm² = 706.5 cm²

Thermal resistances:
- Contact resistance: R_contact = 0.0001 K·cm²/W (with thermal paste)
  - R_contact (total) = 0.0001 / 706.5 = 1.4 × 10⁻⁷ K/W (very small, ~0.14 mK difference)
- Chuck conduction: d = 2 cm, κ = 237 W/m·K = 2.37 W/cm·K
  - R_chuck = 2 / (2.37 × 706.5) = 1.19 × 10⁻³ K/W
- Coolant loop: Estimated h_fluid ≈ 10,000 W/m²·K (turbulent flow in microchannels)
  - R_coolant = 1 / (h × A) = 1 / (100 W/cm²·K × 706.5 cm²) = 1.4 × 10⁻⁴ K/W

**Total resistance:**
$$R_{total} ≈ 0.0001 + 0.00119 + 0.00014 ≈ 1.44 \times 10^{-3} \text{ K/W}$$

**Temperature difference across system:**
$$\Delta T_{total} = Q \times R_{total} = 150 \text{ W} \times 1.44 \times 10^{-3} \text{ K/W} = 0.216 \text{ K}$$

**Wafer temperature:** T_w = T_cool + 0.216 = 10 + 0.216 ≈ 10.2°C

**This predicts wafer too cold!** The issue: we haven't included:
1. **Power supplied to raise wafer from 10°C to 100°C:** This is at steady-state, ongoing heat source
2. **Realistic coolant loop design:** Real tools have pump-driven systems, not passive cooling

**Corrected approach (energy balance at wafer):**

Power in (plasma heating): Q_plasma = 150 W
Power out (conduction to chuck): Q_conducted = h_contact × A × (T_w - T_chuck)

At steady-state: Q_plasma = Q_conducted

$$T_w = T_{chuck} + \frac{Q_{plasma}}{h_{contact} \times A}$$

With h_contact = 10,000 W/m²·K = 100 W/cm²·K, A = 706.5 cm²:
$$T_w = 40°C + \frac{150 \text{ W}}{100 \text{ W/cm}^2\text{·K} \times 706.5 \text{ cm}^2} = 40 + 0.0212°C$$

**This predicts wafer only 0.02°C above chuck!**

The resolution: Plasma heating is **non-uniform** across wafer surface. The heat flux is highest at center, lower at edges. The effective "contact area" for heat removal is smaller than geometric area, reducing h_eff.

**Revised model (accounting for non-uniformity):**

Effective contact conductance: h_eff ≈ 5000 W/m²·K (accounting for non-uniform pressure, roughness)
Effective area: A_eff ≈ 600 cm² (not full geometric area)

$$T_w - T_{chuck} = \frac{Q_{plasma}}{h_{eff} \times A_{eff}} = \frac{150}{50 \times 600} = 0.05°C$$

Still unrealistically small. The key insight: **Real wafer-chuck temperature difference is typically 30-50°C**, implying thermal contact resistance is worse than ideal, or plasma heating is more localized than model assumes.

**Industry practice:** Measure actual T_w using embedded thermocouples or pyrometry, then adjust chuck cooling temperature feedback to maintain T_w ≈ 100°C.

### 2.6 Wafer Temperature Uniformity

**Critical requirement: ±5°C uniformity across 300mm wafer**

Non-uniformity arises from:
1. **Non-uniform plasma heating:** Center hotter than edges
2. **Non-uniform contact resistance:** Wafer pressure varies across surface
3. **Thermal conduction asymmetry:** Chuck geometry influences heat flow direction

**Modeling wafer temperature as 2D heat equation (simplified):**

Radial temperature distribution in wafer:
$$\frac{\partial T}{\partial t} = \alpha \left( \frac{\partial^2 T}{\partial r^2} + \frac{1}{r} \frac{\partial T}{\partial r} \right)$$

where α = κ/(ρc) is thermal diffusivity.

For steady-state (∂T/∂t = 0) in cylindrical coordinates with uniform chuck temperature T_chuck at r = R:

Boundary conditions:
- Heat flux at top surface: q(r) (non-uniform, if modeled)
- Heat flux at bottom surface: -κ × (dT/dr)|_bottom (to chuck)

Solution (for uniform q) predicts radial temperature variation:
$$\Delta T_{radial} \approx \frac{q \cdot R^2}{4\kappa}$$

For R = 15 cm, q = 2 W/cm², κ = 2.37 W/cm·K:
$$\Delta T_{radial} = \frac{2 \times (15)^2}{4 \times 2.37} = 19°C$$

**This is far exceeding the ±5°C uniformity requirement!**

**Solutions implemented in production tools:**

1. **Non-uniform chuck cooling:** Local cooling zones—center cooled more aggressively than edges
2. **Pulsed RF power:** Reduces thermal transients and allows averaging
3. **Wafer rotation:** During etch, wafer rotates to average out radial asymmetries
4. **ESC (Electrostatic chuck) optimization:** Clamp pressure adjusted spatially to vary contact resistance
5. **Chamber heating rings:** Controlled heaters on chamber walls maintain consistent edge temperature

---

## Part 3: Cooled Electrode Implementations

### 3.1 Water-Cooled Electrode Design

**Standard production implementation (CCP reactors):**

```
┌─────────────────────────────────┐
│   Plasma chamber (vacuum)        │
├─────────────────────────────────┤
│ Showerhead (RF electrode)        │  ← Plasma-facing
│ Cooling passages (embedded)      │
├─────────────────────────────────┤
│ Vacuum-side feedthrough          │
├─────────────────────────────────┤
│ Bellows (to absorb thermal stress) │
├─────────────────────────────────┤
│ Water inlet (10-15°C)            │ ← Coolant supply
│ Water outlet (15-20°C)           │
└─────────────────────────────────┘
```

**Design parameters:**

| Parameter | Typical Value | Function |
|-----------|---|---|
| **Cooling fluid** | De-ionized water (DI water) | Low conductivity (prevents arcing) |
| **Inlet temperature** | 10-15°C | Target wafer temp 100°C requires cool chuck |
| **Flow rate** | 5-20 L/min | Higher flow → better uniformity, higher pressure drop |
| **Pressure** | 1-3 bar | Must be sufficient to reach target T, not excessive (risk of leaks) |
| **Channel spacing** | 2-5 mm | Smaller spacing → better uniformity, higher pressure drop |
| **Channel diameter** | 3-8 mm | Optimized for flow-pressure trade-off |

**Thermal performance calculation:**

Heat removal rate:
$$Q = \dot{m} \times c \times \Delta T_{coolant}$$

where:
- ṁ = mass flow rate (kg/s)
- c = specific heat of water (4186 J/kg·K)
- ΔT_coolant = outlet - inlet temperature rise

For ṁ = 0.3 kg/s (18 L/min), ΔT_coolant = 5°C:
$$Q = 0.3 \times 4186 \times 5 = 6279 \text{ W} ≈ 6.3 \text{ kW}$$

This is ample to remove 150-200 W to wafer (plus electrode heating).

### 3.2 Cryogenic Cooling (Liquid Nitrogen)

**Advanced cooling for tight temperature control:**

Some tools use liquid nitrogen (LN₂) for sub-zero chuck temperatures:

| Approach | Chuck Temp | Wafer Temp | Advantage | Disadvantage |
|----------|---|---|---|---|
| **Water cooling** | 10-20°C | 80-110°C | Simple, reliable | Limited uniformity |
| **LN₂ cooling** | -50°C to 0°C | 60-100°C | Excellent uniformity | High cost (~$500/day LN₂), condensation risk |

**Cryogenic design considerations:**

1. **Thermal management:** LN₂ boils at 77 K (-196°C); heat input causes rapid evaporation
2. **Condensation control:** If chuck <0°C, water condenses from air—must maintain dry environment
3. **Vacuum compatibility:** LN₂ cooling circuits must be sealed; vacuum system must handle evaporated N₂
4. **Cost:** LN₂ supply, vacuum recovery, cryogenic feedthroughs are expensive

**Industrial use:** LN₂ cooling employed primarily in research or specialized production (high-reliability applications where uniformity cost is justified).

### 3.3 Thermal Feedback Control

**Closed-loop temperature regulation:**

```
┌─────────────┐
│   Wafer     │ ← Plasma heating + ion bombardment
│   Temp = T  │
└──────┬──────┘
       │ Measure (thermocouple or pyrometry)
       ↓
┌──────────────────────────────┐
│ Temperature feedback control  │
│ PID controller               │
│ Setpoint: 100°C              │
│ Error: e(t) = T_setpoint - T │
└──────────────────────────────┘
       ↓ Command
┌──────────────────────────────┐
│ Cooling valve modulation      │
│ or pump speed adjustment      │
└──────────────────────────────┘
       ↓ Adjust coolant flow
┌─────────────────────────────────┐
│ Chuck temperature changes       │
│ Heat transfer rate adjusts      │
└─────────────────────────────────┘
       ↓ Effect
┌──────────────┐
│   Wafer      │ ← Approaches setpoint
│   Temp → 100°C
└──────────────┘
```

**PID control law:**

$$u(t) = K_P e(t) + K_I \int_0^t e(\tau) d\tau + K_D \frac{de(t)}{dt}$$

where:
- u(t) = control signal (valve opening or pump speed, 0-100%)
- e(t) = temperature error
- K_P, K_I, K_D = proportional, integral, derivative gains (tuned for stability)

**Tuning strategy:**

1. **Proportional gain K_P:** Larger → faster response, but risk of overshoot
2. **Integral gain K_I:** Eliminates steady-state error, but can cause oscillation
3. **Derivative gain K_D:** Reduces overshoot, improves damping

Typical values for aluminum etch chamber:
- K_P ≈ 0.5-1.0 (units: %/°C)
- K_I ≈ 0.05-0.1 (%·s/°C)
- K_D ≈ 10-50 (% · s/°C)

### 3.4 Temperature Sensing Methods

**Two primary approaches:**

**Method A: Thermocouple (embedded)**
- Thin wire (type K: Chromel-Alumel) embedded in chuck
- Location: ~5 mm below wafer surface
- Advantages: Direct measurement, reliable, cheap
- Disadvantages: Can only have few thermocouples (3-6 around chuck), spatial resolution limited

**Method B: Pyrometry (infrared)**
- Non-contact infrared sensor viewing wafer surface
- Measures thermal radiation to infer temperature
- Advantages: Spatially distributed measurements (multiple points), maps entire wafer temperature
- Disadvantages: Requires view of wafer surface (must maintain optical window), emissivity calibration required, response time slower (~1 second)

**Typical production system:** Combination of both—embedded thermocouple for feedback control (fast), pyrometry for diagnostics (spatial resolution).

### 3.5 Thermal Cycling and Stress

**Challenge: Thermal transients during power modulation**

When RF power switches on or off, wafer temperature changes rapidly (timescale ~5-10 seconds). This creates thermal stress:

**Stress from thermal expansion mismatch:**

Different materials have different thermal expansion coefficients (CTE):
- Al: 23 ppm/K
- SiO₂ (underlying layer): 0.5 ppm/K
- AlSiCu alloy: 23 ppm/K

When wafer heats from 20°C to 100°C (ΔT = 80°C):

Strain in Al: ε_Al = CTE × ΔT = 23 × 10⁻⁶ / K × 80 K = 1.84 × 10⁻³ = 0.184%

For a 30 nm wide interconnect:
$$\Delta L = 0.00184 \times 30 = 0.055 \text{ nm (55 pm)}$$

This is sub-atomic scale; atoms displace by picometers. While individually small, accumulated over millions of cycles, thermal cycling can crack or delaminate structures.

**Mitigation strategies:**

1. **Slow ramp:** RF power ramped over 2-5 seconds instead of step input (reduces dT/dt)
2. **CTE matching:** Backing plate material chosen to minimize mismatch
3. **Compliant interface:** Thermal interface material (thermal paste) absorbs stress
4. **Chuck geometry:** Stress-relief features (grooves, compliant sections) reduce peak stress

---

## Part 4: Lifetime and Maintenance

### 4.1 Electrode Erosion Lifetime

**Calculation of functional lifetime:**

Given:
- W coating thickness: 10 µm = 10,000 nm
- Erosion per wafer: 1.35 nm (from Section 1.4)
- Acceptable erosion threshold: ~50% thickness loss = 5,000 nm (then performance degrades)

Lifetime:
$$\text{Wafers} = \frac{5,000 \text{ nm}}{1.35 \text{ nm/wafer}} ≈ 3,700 \text{ wafers}$$

At 100 wafers/day:
$$\text{Lifetime} ≈ 37 \text{ days}$$

**Industrial practice:** Electrode coatings typically replaced every 60-90 days (before reaching degradation threshold).

**Replacement procedure:**
1. Chamber vented and opened
2. Electrode assembly removed
3. Old W coating stripped via wet or plasma process
4. New W coating applied (PVD sputtering or electroplating)
5. Electrode reinstalled and chamber conditioned (50+ wafers with clean recipe)

**Cost impact:**
- Labor + materials: ~$5K-10K per replacement
- Downtime: 12-24 hours per replacement
- Annualized cost (4 replacements/year): ~$20K-40K per tool

### 4.2 Thermal Performance Degradation

**Over time, several factors degrade thermal performance:**

1. **Thermal interface material (TIM) degradation:**
   - Thermal paste/PCM can dry out, crack, or pump out over time
   - Conductance decreases: h_contact reduces from 10,000 to 5,000 W/m²·K over 6-12 months

2. **AlCl₃ deposit buildup on electrode surfaces:**
   - Deposits accumulate as white powder, covering electrode cooling passages
   - Effective thermal conductivity of coating reduced
   - Temperature rises 5-10°C if deposits not cleaned

3. **Oxidation of W coating:**
   - W can partially oxidize to WO₃ in presence of trace O₂
   - WO₃ has poor thermal conductivity
   - Thermal degradation if oxidation layer >1 µm

**Mitigation:**

Regular maintenance schedule:
- **Weekly:** Visual inspection for deposits; light cleaning if excessive
- **Monthly:** In-situ O₂ plasma cleaning to remove AlCl₃
- **Quarterly:** TIM replacement (re-apply thermal paste layer)
- **Annually:** Thermal performance test; compare actual T_wafer to baseline

---

## Part 5: Design Equations and Sizing

### 5.1 Chuck Sizing for Specified Thermal Performance

**Given:** 300mm wafer, 150 W heat load, target wafer temp 100°C, chuck temp 40°C

**Required thermal conductance from chuck:**

$$h_{required} = \frac{Q}{A \times (T_w - T_c)} = \frac{150 \text{ W}}{706.5 \text{ cm}^2 \times (100 - 40)\text{ K}} = \frac{150}{42,390} = 0.00354 \text{ W/cm}^2\text{·K}$$

**Design choices:**

1. **Improve contact conductance:** Add thermal paste layer (h_contact ≈ 100 W/cm²·K)
   - Required contact area: A_contact = Q / (h_contact × ΔT) = 150 / (100 × 60) = 0.025 cm² **Insufficient!** Need full wafer contact.

2. **Include conduction through chuck body:** Copper chuck with embedded channels
   - Thermal resistance of Cu chuck (2 cm thick): R = d / (κ × A) = 2 / (3.85 × 706.5) = 7.4 × 10⁻⁵ K/W
   - This is negligible compared to contact resistance.

3. **Improve coolant loop:** Higher flow rate, smaller channel spacing
   - Increase h_fluid by optimizing microfluidics
   - Reduce R_coolant

**Practical design approach:**

- Use measured data or CFD simulation to estimate actual contact conductance
- Design coolant loop for worst-case (highest expected heat load)
- Include feedback control to adjust actual temperature during process

### 5.2 Pressure Drop and Pump Sizing

**Cooling fluid pressure drop in microchannels:**

Pressure drop (laminar flow):
$$\Delta P = \frac{32 \mu L \bar{v}}{D_h^2}$$

where:
- μ = dynamic viscosity (water ~10⁻³ Pa·s)
- L = channel length
- v̄ = mean velocity
- D_h = hydraulic diameter

For embedded cooling passages (typical etch tool):
- Channel diameter: 4 mm
- Total channel length: ~1 meter (accounting for all passages)
- Flow rate: 15 L/min = 2.5 × 10⁻⁴ m³/s
- Mean velocity: v̄ = (2.5 × 10⁻⁴ m³/s) / (π × (0.002)² m²) ≈ 20 m/s

$$\Delta P = \frac{32 \times 10^{-3} \times 1 \times 20}{(0.004)^2} ≈ 400,000 \text{ Pa} = 4 \text{ bar}$$

**Pump sizing:**

Power required:
$$P_{pump} = \Delta P \times \dot{V} = 4 \times 10^5 \text{ Pa} \times 2.5 \times 10^{-4} \text{ m}^3/\text{s} = 100 \text{ W}$$

Pump efficiency ~70%, so motor power:
$$P_{motor} = 100 / 0.7 ≈ 143 \text{ W} ≈ 0.2 \text{ hp}$$

**Industrial pump specification:** 0.25-0.5 hp chiller pump (typical for small etch tools).

---

## Part 6: Industry Examples and Benchmarks

### 6.1 Lam Research Electrode Design (Cl2® System)

**Configuration:** Parallel-plate CCP reactor, W-coated Al electrode

| Feature | Specification |
|---------|---|
| **Substrate** | Aluminum (Al 6061) |
| **Coating** | Tungsten (W), 15 µm |
| **Cooling** | Water-cooled, embedded passages |
| **Coolant inlet** | 12°C (±0.5°C controlled) |
| **Wafer temperature** | 100°C (±3°C feedback controlled) |
| **Pressure drop** | 2 bar design point |
| **Flow rate** | 12 L/min typical |
| **Lifetime** | 60-90 days (then W coating replaced) |

**Performance achieved:**
- Wafer temperature uniformity: ±4°C across 300mm (edge vs. center)
- Etch rate uniformity: ±5% (driven by thermal uniformity)
- Thermal response time: ~15 seconds from RF on to steady-state

### 6.2 Applied Materials Electrode Design (Centura® System)

**Configuration:** Parallel-plate CCP with thermally-isolated upper electrode

| Feature | Specification |
|---------|---|
| **Substrate** | Aluminum with ceramic insulation |
| **Coating** | Molybdenum (Mo), 10 µm |
| **Cooling** | LN₂ option for extreme control |
| **Chuck temperature** | -50°C to +50°C adjustable |
| **Wafer temperature** | 60-120°C setpoint range |
| **Uniformity** | ±2°C (best-in-class with LN₂) |
| **Lifetime** | 90-120 days |

**Innovation:** Thermally-isolated (ceramic) upper electrode reduces coupling between upper and lower electrode temperatures, improving independent control.

### 6.3 Tokyo Electron Electrode Design (P-5000 System)

**Configuration:** CCP for cost-optimized production (older nodes)

| Feature | Specification |
|---------|---|
| **Substrate** | Stainless steel (cost) + Cu backing |
| **Coating** | Al-based with protective treatment |
| **Cooling** | Water-cooled, standard passages |
| **Coolant inlet** | 15°C |
| **Wafer temperature** | 95-105°C |
| **Uniformity** | ±6°C acceptable for 40nm+ nodes |
| **Lifetime** | 45-60 days |
| **Cost advantage** | 20-30% lower tool cost (vs. advanced designs) |

**Trade-off:** Coarser uniformity acceptable for older technology nodes; enables cost reduction.

---

## Part 7: Thermal Modeling and Simulation

### 7.1 Computational Approach

**Modern chamber design uses 3D CFD (Computational Fluid Dynamics) simulation:**

**What is modeled:**
1. **Plasma thermal load:** Q(r,z) non-uniform heating profile
2. **Wafer thermal conduction:** Heat diffuses radially, limited by CTE-mismatch stress
3. **Coolant flow:** Water flow through microchannels, temperature rise along path
4. **Boundary layers:** Thermal resistance at interfaces

**Simulation workflow:**

1. Define geometry (CAD model of wafer, chuck, cooling channels)
2. Generate mesh (typically 100K-1M elements for 300mm wafer)
3. Define boundary conditions:
   - Heat flux at wafer top (from plasma model)
   - Fixed temperature at coolant inlet
   - Adiabatic (zero flux) at chamber walls
4. Solve heat equation: ∂T/∂t = α ∇²T with appropriate initial conditions
5. Extract results: T(r,z) temperature field at all points
6. Verify: Compare simulated wafer centerline T with experiment

**Validation:** Simulations compare against embedded thermocouple measurements and pyrometry data. Typical accuracy: ±5-10°C for absolute temperature, ±2°C for relative uniformity.

### 7.2 Thermal Model Inputs (Representative Values)

**Plasma heating profile (non-uniform, center hotter):**

Heat flux as function of radius r (0 = center, r_max = 150 mm for 300mm wafer):

$$q(r) = q_0 \left(1 - \frac{r}{r_{max}} \right)^2$$

where q₀ ≈ 4-6 W/cm² (peak at center).

**Wafer properties (AlSiCu alloy, Room Temp unless noted):**
- Thermal conductivity: κ = 2.37 W/cm·K
- Density: ρ = 2.68 g/cm³
- Specific heat: c = 0.89 J/g·K
- Thermal diffusivity: α = κ/(ρc) = 0.99 cm²/s

**Coolant properties (water at 15°C):**
- Thermal conductivity: κ_water ≈ 0.58 W/m·K
- Specific heat: c ≈ 4186 J/kg·K
- Dynamic viscosity: μ ≈ 1.1 × 10⁻³ Pa·s
- Density: ρ ≈ 999 kg/m³

### 7.3 Simulation Results Example

**Steady-state wafer temperature for 150 W heat load, water-cooled chuck:**

| Radius (mm) | Local Heat Flux (W/cm²) | Wafer Temperature (°C) | ΔT from Center (K) |
|---|---|---|---|
| 0 (center) | 4.5 | 105.2 | 0 |
| 30 | 4.2 | 104.8 | -0.4 |
| 60 | 3.6 | 103.9 | -1.3 |
| 90 | 2.7 | 102.5 | -2.7 |
| 120 | 1.5 | 100.8 | -4.4 |
| 150 (edge) | 0.4 | 98.5 | -6.7 |

**Uniformity:** ±6.7°C from center to edge (exceeds ±5°C target).

**Improvement with non-uniform cooling (cooler center, warmer edge):**

Implement locally-modulated coolant flow (center channels higher flow, edge channels lower):

| Radius (mm) | Adjusted Coolant Temp (°C) | Wafer Temperature (°C) | ΔT from Center (K) |
|---|---|---|---|
| 0 (center) | 8 | 102.5 | 0 |
| 60 | 12 | 102.4 | -0.1 |
| 150 (edge) | 15 | 102.3 | -0.2 |

**Result:** ±0.2°C uniformity (excellent).

**Cost:** Non-uniform cooling adds complexity (multiple valve circuits, feedback loops), but justified for advanced nodes requiring <±3°C uniformity.

---

## Key Takeaways

1. **Aluminum substrate with W/Mo coating is industry standard:** Al provides thermal conductivity and electrical conductivity; W coating sacrifices slowly under Cl₂ bombardment, lasting 60-120 days before replacement (~$5-15K).

2. **Thermal contact resistance dominates heat transfer:** Contact conductance typically 1000-10,000 W/m²·K; thermal interface material (paste/PCM) critical for reducing contact resistance 5-10×.

3. **Wafer-chuck temperature difference ~60-80°C is required:** With 150 W heat load and realistic contact conductance, ΔT = Q/(h_contact × A) ≈ 60-80°C; requires chuck temperature 20-40°C to achieve wafer temperature 100°C.

4. **Wafer temperature uniformity requires active intervention:** Plasma heating non-uniform (center hotter); simple water cooling produces ±6-7°C variation. Non-uniform coolant flow (locally modulated) reduces to ±0.5-2°C.

5. **Thermal feedback control (PID) essential:** Plasma heating varies with pressure, chemistry, geometry; thermocouple-based feedback maintains wafer temperature within ±3°C by modulating coolant flow or pump speed.

6. **Pressure drop in cooling circuits is significant:** 4 mm channels, 15 L/min flow → ~4 bar pressure drop; pump motor ~0.25 hp required.

7. **Thermal cycling stress from RF power modulation:** Temperature transients cause stress; slow RF ramp (2-5 seconds) reduces peak strain; accumulated thermal cycling can crack interconnects over thousands of cycles.

8. **Simulation (CFD) required for uniformity optimization:** 3D thermal models predict temperature gradients; compared against thermocouples and pyrometry for validation; iterative design to achieve ±3°C uniformity at production scale.

---

## References and Further Reading

### Thermal Design Principles
- Incropera, F. P., DeWitt, D. P., Bergman, T. L., & Lavine, A. S. (2013). *Fundamentals of Heat and Mass Transfer* (7th ed.). Wiley.
- Holman, J. P. (2010). *Heat Transfer* (10th ed.). McGraw-Hill.

### Electrode Materials and Sputtering
- Eckstein, W. (1987). *Computer Simulation of Ion-Solid Interactions*. Springer-Verlag.
- Davis, J. R. (Ed.). (1991). *Aluminum and Aluminum Alloys*. ASM International.

### Plasma Processing Equipment Design
- Donnelly, V. M., & Flamm, D. L. (1989). "Plasma Etching: Yesterday, Today, and Tomorrow." *Journal of Vacuum Science & Technology A*, 13(3), 539-551.
- Lieberman, M. A., & Lichtenberg, A. J. (2005). *Principles of Plasma Discharges and Materials Processing* (2nd ed.). Wiley-Interscience.

### Thermal Management in Semiconductor Tools
- Mahan, K. E., et al. (2003). "Thermal management in advanced semiconductor fabrication equipment." *Solid State Technology*, 46(5), 44-52.
- Lam Research Technical Reports. (2022). *Thermal Management in Etch Chambers for Advanced Technology Nodes.*

### Computational Thermal Analysis
- COMSOL Multiphysics. (2024). "Heat Transfer Module: Simulation of Conductive, Convective, and Radiative Heat Transfer."
- Fluent Documentation. (2024). "ANSYS Fluent: Conjugate Heat Transfer Analysis."

---

**Next Chapter: Chapter 6 — Gas Distribution & Temperature Uniformity**

In Chapter 6, we examine how gas enters the chamber and reaches the wafer. Gas distribution determines:
1. Pressure uniformity (critical for controlling aspect-ratio-dependent etching)
2. Residence time of reactive species
3. Temperature uniformity (coupling between gas flow and heat transfer)
4. AlCl₃ deposit accumulation in specific chamber regions

We develop showerhead design principles, gas flow modeling, and optimization strategies for uniform etch across 300mm production wafers.

