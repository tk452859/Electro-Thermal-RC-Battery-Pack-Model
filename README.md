# 🔋 Electro-Thermal RC Battery Pack Model with EKF SOC Estimation (MATLAB)

This project implements a physics-inspired Li-ion battery pack simulation using an equivalent circuit model (ECM) with:

- SOC dynamics
- 1-RC Thevenin electrical model
- Multi-cell series pack
- Weakest-cell protection logic
- Pulse-current (HPPC-style) testing
- Parameter identification (R0 and RC time constant)
- Electro-thermal coupling
- Temperature-dependent resistances
- Extended Kalman Filter (EKF) for SOC estimation

The goal is to replicate **core Battery Management System (BMS) algorithms** used in EVs.

---

## 📌 Features Implemented

### Electrical Model
- Coulomb counting SOC update
- OCV(SOC) function
- Ohmic resistance R0
- Polarization branch R1–C1
- Discrete-time state equations

### Pack-Level Modeling
- Series-connected cells
- Cell-to-cell voltage variation
- Pack voltage aggregation
- Undervoltage protection based on weakest cell

### Thermal Model
- I²R heat generation
- Ambient cooling
- Lumped thermal RC
- Temperature-dependent R0 and R1

### Parameter Identification
- R0 extraction from voltage step
- RC time constant identification from Vrc relaxation

### State Estimation
- EKF estimating:
  - SOC
  - Polarization voltage
- Voltage-based correction
- Noisy measurement scenario

---

## 🧠 Mathematical Model

### SOC Dynamics

SOC update:

SOC(k+1) = SOC(k) − (I·Δt)/(Q·3600)

---

### RC Polarization State

Vrc(k+1) = a·Vrc(k) + R1·(1 − a)·I

where:

a = exp(−Δt / (R1·C1))

---

### Terminal Voltage

V = OCV(SOC) − I·R0 − Vrc

---

### Thermal Dynamics

Cth·dT/dt = I²·R0 − h·(T − Tamb)

---

### EKF State Vector

x = [ SOC ; Vrc ]

Measurement:

Vmeas = OCV(SOC) − I·R0 − Vrc

---

## ▶️ How to Run

1. Open MATLAB.
2. Run:


3. Observe plots:
   - Current pulses
   - Pack voltage
   - Cell voltages
   - Temperature rise
   - EKF SOC convergence

---

## 📊 Example Outputs

- RC relaxation after pulses
- Estimated time constant τ ≈ R1·C1
- EKF SOC converging from wrong initial guess
- Temperature rise during discharge pulses

<img width="1740" height="749" alt="pack_voltage and pulse" src="https://github.com/user-attachments/assets/a8e70cd0-39de-4e26-9ac0-107e86486282" />
<img width="1817" height="785" alt="ekf_soc" src="https://github.com/user-attachments/assets/9f5e37e4-4789-4b3b-af9e-263683493c09" />


---

## 💡 Key Engineering Insights

- Terminal voltage relaxation is contaminated by SOC drift → RC states must be isolated.
- Temperature affects resistance and RC dynamics.
- Parameter dispersion across cells biases pack-level identification.
- EKF improves SOC accuracy compared to coulomb counting alone.
- Weakest-cell logic dominates pack-level protection.

---

## 🧪 Applications

- EV battery algorithm development
- BMS software prototyping
- SOC/SOH research
- Thermal derating studies
- Charging strategy development
- Fault injection experiments

---

## 🚀 Future Extensions

Optional upgrades:

- SOC-dependent lookup tables
- Aging model (capacity fade, resistance growth)
- SOH estimator
- Active cell balancing
- Multi-RC branches
- CAN interface simulation
- Drive cycle profiles (WLTP)
- Fast-charging derating logic

---

## 👤 Author

Tarun Singh  
Electrical Engineering | EV & BMS Modeling  
