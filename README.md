# Quadrotor Senior Project (Electrical Engineering Focus)
Baseline code: Joop Brokking’s quadcopter code (ported and extended on STM32F103)

## Overview
- Duration: 2 semesters, 15 weeks each (grouped into 2-week blocks)
- Goals: Build a custom STM32F103 flight controller (PCB + assembly), integrate sensors, and achieve stable flight with Attitude (Angle), Altitude Hold, Position Hold, and Waypoint Navigation
- Emphasis: Power/signal integrity, EMI/EMC, PCB DFM/DFA, real-time firmware, estimation/control, testing discipline, and safety

---

## Semester 1 — Hardware, Interfaces, PCB, Assembly, Bring-Up

### Weeks 1–2
- Topics
  - Project kickoff, safety (LiPo, props-off, ESD, spotter), mission requirements (AUW, thrust/weight, endurance, geofence)
  - STM32F103 architecture; toolchain bring-up; GPIO/SysTick timing markers
- Electrical Engineering Focus
  - Power budgets and derating; repo hygiene; clock tree, decoupling
- Deliverables
  - Project charter, initial BOM, risk register, minimal STM32 project and coding standards

### Weeks 3–4
- Topics
  - Power electronics: battery model, voltage sag, LC filters, TVS, brownout detection
  - I2C/SPI interfaces: pull-ups, bus capacitance, signal integrity; IMU/baro dev-board readout
- Electrical Engineering Focus
  - Oscilloscope/logic analyzer measurements; SI on digital buses; grounding strategies
- Deliverables
  - Power tree schematic and component selections; WHO_AM_I + raw logs; SI notes with captures

### Weeks 5–6
- Topics
  - Joop Brokking code walkthrough: complementary filter, PID, mixer, RC parsing
  - FC v1 schematic: MCU, SWD, regulators, IMU/baro, magnetometer, GPS UART, RC input, ESC outputs, test points
- Electrical Engineering Focus
  - Separate math/control from I/O; calibration storage; DFM/DFA in schematic design
- Deliverables
  - Porting plan; unit tests for filter/PID/mixer; completed schematic, ERC pass

### Weeks 7–8
- Topics
  - PCB layout (EMI/EMC): planes/returns, decoupling placement, baro venting, crystal routing, IMU keepouts, stitching vias
  - Firmware timing: deterministic scheduler; jitter budgeting; watchdog and fault handling
- Electrical Engineering Focus
  - Return path analysis and via stitching; timing verification with GPIO markers
- Deliverables
  - Gerbers/BOM/pos submitted; timing/jitter CSV and report

### Weeks 9–10
- Topics
  - SMD assembly training (stencil, reflow profile, inspection/rework)
  - FC v1 assembly and electrical validation (rails, current draw, clock start, SWD attach)
- Electrical Engineering Focus
  - IPC-lite inspection criteria; controlled power-up; inrush/short checks
- Deliverables
  - Practice board pass; FC v1 smoke test; rail/clock/SWD verified

### Weeks 11–12
- Topics
  - Peripheral and sensor bring-up (I2C scan, SPI loopback, IMU/baro streaming, calibration)
  - ESC/motor interface and bench rig; PWM vs DShot; failsafe output state
- Electrical Engineering Focus
  - Noise floor characterization; sag/EMI mitigation; timer channel mapping and isolation
- Deliverables
  - Calibrated IMU/baro logs and noise report; safe motor ramp tests; current/sag data

### Weeks 13–14
- Topics
  - Integrate Joop’s estimator and rate loop on FC v1; complementary filter tuning
  - Safety/arming logic; RC/CLI; loss-of-signal and low-voltage failsafes; watchdog behavior
- Electrical Engineering Focus
  - Loop frequency/jitter plots; robust state machine for arming/failsafe
- Deliverables
  - Ground integration pass (props off): sensor → estimator → rate loop → mixer; arming/failsafe validated

### Week 15
- Topics
  - Design review, readiness for flight; contingency (FC v1.1/v2 if needed)
- Electrical Engineering Focus
  - DFM/DFA, PI/SI margins, risk mitigation, test readiness
- Deliverables
  - Review deck; action items; go/no-go decision

---

## Semester 2 — Controls, Alt/Pos, GPS/Path, Tuning, Flight Test

### Weeks 1–2
- Topics
  - Estimation refinement: complementary vs Mahony/Madgwick; magnetometer options; Euler vs quaternion
  - Attitude/rate control: discrete PID, anti-windup, derivative filtering; bench tuning
- Electrical Engineering Focus
  - Deterministic timing and latency control; CLI-based tuning workflow
- Deliverables
  - Estimator validation plots; stable inner rate loop (bench step/sine tests)

### Weeks 3–4
- Topics
  - Vibration mitigation: prop/motor balance, soft-mounts; gyro LPF/notch design and deployment
  - First hover attempt with tether/safety; rate P/D tuning; mixer validation
- Electrical Engineering Focus
  - PSD analysis to locate blade-passing frequency; motor direction/order checks
- Deliverables
  - Vibration report and filter settings; stable hover in Attitude mode with logs

### Weeks 5–6
- Topics
  - Altitude sensing and AltHold: baro filtering (median+IIR), vertical velocity (baro+accel), thrust linearization
  - GPS/compass: UART parsing (UBX/NMEA), fix type and HDOP gating, mag calibration/alignment
- Electrical Engineering Focus
  - Fusion/gating practicalities; sensor health checks before enabling modes
- Deliverables
  - AltHold within target band; GPS/heading pipeline validated with quality metrics

### Weeks 7–8
- Topics
  - Position estimation/hold: GPS XY + baro Z; anti-windup; rate limiting and deadband
  - Pathway/waypoint navigation: ENU conversion; L1/vector pursuit; RTL basics
- Electrical Engineering Focus
  - Safety limits (tilt/speed/altitude), mission abort conditions
