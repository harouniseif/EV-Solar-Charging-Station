# ⚡ Autonomous Solar Charging Station for Electric Vehicles

> **Graduation Project — ENP Constantine, 2025**  
> Ingéniorat d'État en Electrotechnique / Automatique

---

## 📌 Overview

Design, sizing, and simulation of a **grid-independent DC microgrid** for fast-charging electric vehicles using photovoltaic energy.

The system integrates a PV generator with MPPT tracking, a Li-ion battery storage unit, and DC/DC converters managed by PI/PID controllers — modeled and validated under **MATLAB/Simulink**.

---

## 🏗️ System Architecture

```
[PV Field 9.8 kWp] → [Boost + MPPT] → [DC Bus 500V]
                                              │
                              ┌───────────────┤
                              ▼               ▼
                    [BDC Converter]     [Buck Converter]
                  [Battery 300V/400Ah]  [EV Battery 400V]
```

- ☀️ **Daytime:** PV charges EV directly + stores excess in battery  
- 🌙 **Night / Cloudy:** Battery discharges to continue EV charging  
- 🔋 **SoC > 80%:** System switches from CC to CV mode automatically  

---

## ⚙️ Key Specifications

| Component | Value |
|-----------|-------|
| PV Peak Power | 9.8 kWp |
| PV Module | Galix JW-G2100 (210W) — 10S × 46P |
| DC Bus Voltage | 500 V |
| Storage Battery | 300 V / 400 Ah (120 kWh) |
| EV Battery | 50 kWh — Tesla Model 3 / Y |
| Charge Protocol | CC–CV, Mode 4 DC Fast Charge |
| Charge Current | 125 A |
| Switching Frequency | 5 kHz |

---

## 🔬 Control Strategies

| Converter | Strategy |
|-----------|----------|
| Boost | MPPT — Perturb & Observe (P&O) |
| BDC (Buck/Boost) | Double-loop PI — voltage + current |
| Buck (EV charger) | CC/CV with PI regulators |

---

## 📊 Simulation Results

| Scenario | Result |
|----------|--------|
| PV peak output | ~9,800 W |
| DC bus stability | 500 V ± 1 V |
| EV charge time (10% → 80%) | ~42 minutes |
| Behavior at 0 W/m² | Auto-shutdown, bus held at 500 V |

---

## 🗂️ Repository Structure

```
EV-Solar-Charging-Station/
├── README.md
├── simulation/
│   └── main_system.slx
├── results/
│   └── (simulation screenshots)
└── docs/
    └── memoire_HAROUNI_2025.pdf
```

---

## 🛠️ Requirements

- MATLAB R2021a or later
- Simulink
- Simscape Electrical toolbox

---

## 📚 Context

Developed as a **State Engineering graduation thesis** at the **École Nationale Polytechnique de Constantine (ENP)**, defended June 2025.

**Supervisor:** Dr. Maria Larakeb — ENP Constantine  
**Jury President:** Prof. Boulakroune M'Hamed — ENP Constantine

---

## 👤 Author

**HAROUNI Seif Eddine**  
Electrical Engineer — ENP Constantine, 2025

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Seif%20Eddine%20Harouni-blue?logo=linkedin)](https://www.linkedin.com/in/seif-eddine-harouni-4991a1328)

