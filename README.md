# ⚡ Autonomous Solar Charging Station for Electric Vehicles

> **Graduation Project — ENP Constantine, 2025**  
> Ingéniorat d'État en Automatique / Electrotechnique

---

## 📌 Overview

Design, sizing, and simulation of a **grid-independent DC microgrid** for fast-charging electric vehicles using photovoltaic energy.

The system integrates a PV generator with MPPT tracking, a Li-ion battery storage unit, and a cascade of DC/DC converters managed by PI/PID controllers — all modeled and validated under **MATLAB/Simulink**.

---

## 🏗️ System Architecture

```
[PV Field (9.8 kWp)]
        │
        ▼
  [Boost Converter]  ←→  [MPPT Control (P&O)]
        │
        ▼
   [DC Bus 500V]
        │
   ┌────┴────┐
   ▼         ▼
[BDC Converter]    [Buck Converter]
[Battery 300V/400Ah]   [EV Battery 400V/50kWh]
```

**Energy flow logic:**
- ☀️ **Daytime:** PV charges EV directly + stores excess in battery
- 🌙 **Night / Low irradiation:** Battery discharges to maintain EV charging
- 🔋 **SoC > 80%:** System switches from CC to CV mode automatically

---

## ⚙️ Technical Specifications

| Component | Parameter | Value |
|-----------|-----------|-------|
| PV Field | Peak Power | 9.8 kWp |
| PV Module | Model | Galix JW-G2100 (210W) |
| PV Configuration | Series × Parallel | 10S × 46P |
| DC Bus | Nominal Voltage | 500 V |
| Storage Battery | Voltage / Capacity | 300 V / 400 Ah (120 kWh) |
| EV Battery | Capacity | 50 kWh (Tesla Model 3/Y) |
| Boost Converter | L / C | 1.5 mH / 100–130 µF |
| BDC Converter | L / C | 2.5 mH / 3000 µF |
| Buck Converter | L / C | 2.13 mH / 47 µF |
| Switching Frequency | All converters | 5 kHz |
| Charge Protocol | Mode | CC–CV (Mode 4 DC fast charge) |
| Charge Current | EV | 125 A (1C rate) |

---

## 🔬 Control Strategies

### MPPT — Boost Converter
- Algorithm: **Perturb & Observe (P&O)**
- Dynamically adjusts duty cycle to track maximum power point under variable irradiation

### BDC — Bidirectional Buck/Boost
- **Double-loop PI control** (outer voltage loop + inner current loop)
- Maintains DC bus at 500 V ± 1%

| Loop | Kp | Ki | Kd | N |
|------|----|----|----|---|
| Voltage | 0.05 | 300 | 0.05 | 150 |
| Current | 0.06 | 180 | 0.10 | 120 |

### Buck — EV Charger
- **CC/CV strategy**: constant current (125 A) until SoC = 80%, then constant voltage (400 V)

| Loop | Kp | Ki |
|------|----|----|
| Voltage | 8 | 5000 |
| Current | 1.1 | 220 |

---

## 📊 Key Simulation Results

| Scenario | Result |
|----------|--------|
| PV peak power (1000 W/m²) | ~9,800 W |
| DC bus stability | 500 V ± 1 V |
| EV charge time (10% → 80%) | ~42 minutes |
| Battery SoC response | Smooth CC→CV transition at 80% |
| System behavior at 0 W/m² | Auto-shutdown, bus maintained at 500 V |

> 📁 See `/results/` folder for Simulink simulation screenshots.

---

## 🗂️ Repository Structure

```
EV-Solar-Charging-Station/
│
├── README.md
├── simulation/
│   └── main_system.slx          # Full Simulink model
├── results/
│   ├── pv_power_curve.png
│   ├── dc_bus_voltage.png
│   ├── battery_soc.png
│   ├── ev_charging_curve.png
│   └── bdc_current_response.png
├── docs/
│   └── memoire_HAROUNI_2025.pdf
└── LICENSE
```

---

## 🛠️ Requirements

- MATLAB R2021a or later
- Simulink
- Simscape Electrical toolbox

---

## 🚀 Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/EV-Solar-Charging-Station.git

# 2. Open MATLAB and navigate to the project folder

# 3. Open the Simulink model
open('simulation/main_system.slx')

# 4. Run the simulation
```

---

## 📚 Context

This project was developed as part of the **State Engineering graduation thesis** at the **École Nationale Polytechnique de Constantine (ENP)**, defended in June 2025.

**Supervisor:** Dr. Maria Larakeb — ENP Constantine  
**Jury President:** Prof. Boulakroune M'Hamed — ENP Constantine

---

## 👤 Author

**HAROUNI Seif Eddine**  
State Engineer — Automation / Electrical Engineering  
École Nationale Polytechnique de Constantine, 2025  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com/in/YOUR_PROFILE)

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
