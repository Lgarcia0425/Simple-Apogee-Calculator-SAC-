# Simple Apogee Calculator (SAC)
A MATLAB based tool for estimating model rocket apogee and optimal ejection charge delay using algebra based kinematics.
 
 
## Overview
SAC takes a rocket's total mass and a user-selected motor, then uses the four kinematic equations to estimate:
- The rocket's maximum altitude (apogee) in feet
- The optimal time for the ejection charge to fire
No calculus or numerical integration is used — all calculations are direct algebraic substitution.
 

 
## Files
1. SimpleApogeeCalc.m Main script — run this to start the calculator
2. select_motor.m Displays the motor menu and returns the user's choice
3.  predict_apogee.m Calculates predicted apogee in feet
4.   optimal_delay.m Calculates optimal ejection delay in seconds 
 

 
## How to Run
1. Place all four .m files in the same folder.
2. Open SimpleApogeeCalc.m in MATLAB.
3. Press **Run** or type SimpleApogeeCalc in the Command Window
4. Enter your rocket's total mass in kilograms when prompted.
5. Select a motor from the menu by entering its number.
6. Results are printed in the Command Window.
---
 
## Inputs

 Rocket total dry mass  (kg)  Typed at prompt 
 and motor selection which is chosen from numbered menu 
 
---
 
## Outputs
Predicted apogee  (ft) Estimated maximum altitude
Optimal ejection delay (s) Ideal time from burnout to chute deployment 
 Motor ejection delay (s)  The selected motor's built-in delay for comparison 
 
---
 
## Available Motors

 1. H100-14 (38mm) | 97.7 N | 2.32 s | 14 s
 2.  J250-14 (54mm) | 250.0 N | 2.90 s | 14 s |
 3.   K1100-14 (54mm) | 1100.0 N | 1.61 s | 14 s |
 4.   65-P (54mm) | 65.0 N | 9.00 s | PLUGGED |
 
**Note:** The I65-P is a plugged motor — it has no built-in ejection charge. An electronic altimeter is required for parachute deployment. The calculator still outputs an optimal delay to help you program the altimeter.
 
Motor data sourced from ThrustCurve.org and Wildman Rocketry.
 
---
 
## Physics Model
The calculator uses two flight phases, each solved with the standard kinematic equations:
 
**Phase 1 — Powered ascent** (launch to burnout, starting from rest):
```
a_burn    = (F_thrust - m·g) / m
v_burnout = a_burn × t_burn          [v = vᵢ + a·t]
s_burnout = 0.5 × a_burn × t_burn²  [s = vᵢ·t + 0.5·a·t²]
```
 
**Phase 2 — Coast to apogee** (burnout to v = 0):
```
s_coast      = v_burnout² / (2·g)   [v² = vᵢ² + 2·a·s]
t_coast      = v_burnout / g        [t = (v - vᵢ) / a]
apogee       = s_burnout + s_coast
optimal_delay = t_coast
```
 
### Assumptions and Limitations
- Constant average thrust across the entire burn (no thrust curve)
- Aerodynamic drag is not modelled
- Sea-level launch (standard gravity, g = 9.81 m/s²)
- Rocket mass is treated as constant (motor propellant mass not subtracted)
These simplifications make the model straightforward and algebra-only, but mean the apogee estimate will generally read **higher** than actual flight — treat results as an upper-bound estimate.
 
---
 
## Requirements
- MATLAB R2025b or later
