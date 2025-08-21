# drone_2025
Drone Project 2025
Quadrotor Senior Project (EE Focus) — 2-Semester Plan
Baseline code: Joop Brokking’s quadcopter code (ported and extended on STM32F103)

Overview
Duration: 2 semesters, 15 weeks each (grouped into 2-week blocks)

Goals: Custom STM32F103 flight controller (PCB+assembly), sensor integration, stable flight with AltHold, PosHold, and waypoint navigation

Emphasis: Power/signal integrity, EMI/EMC, PCB DFM/DFA, real-time firmware, estimation/control, testing and safety

Semester 1 — Hardware, Interfaces, PCB, Assembly, Bring-Up
Weeks 1–2
Topics:

Project kickoff, safety (LiPo, props-off, ESD), requirements (AUW, thrust/weight, endurance)

STM32F103 architecture; toolchain bring-up; GPIO/SysTick timing markers

EE focus: Power budgets, repo hygiene, clock tree, decoupling basics

Deliverables: Project charter, initial BOM, risk register, minimal STM32 project and coding standards

Weeks 3–4
Topics:

Power electronics: battery model, voltage sag, LC filters, TVS, BOD

I2C/SPI interfaces, pull-ups, bus capacitance; IMU/baro dev-board readout

EE focus: Oscilloscope/logic analyzer measurements, SI on buses

Deliverables: Power tree schematic and component selections; WHO_AM_I + raw logs; SI notes with captures

Weeks 5–6
Topics:

Joop Brokking code walkthrough: complementary filter, PID, mixer, RC parsing

FC v1 schematic capture: MCU, SWD, regulators, IMU/baro, mag, GPS UART, RC input, ESC outputs

EE focus: Separate math from I/O; test points, programming headers, calibration storage

Deliverables: Porting plan; unit tests for filter/PID/mixer; completed schematic, ERC pass

Weeks 7–8
Topics:

PCB layout for EMI/EMC: planes/returns, decoupling placement, baro venting, crystal routing, IMU keepouts

Firmware timing model: deterministic scheduler; jitter budgeting; watchdog

EE focus: Return paths and stitching vias; timing verification with GPIO markers

Deliverables: Gerbers/BOM/pos submitted; timing/jitter CSV and report

Weeks 9–10
Topics:

SMD assembly training (stencil, reflow profile, inspection/rework)

FC v1 assembly; electrical validation (rails, current, clock start, SWD attach)

EE focus: IPC-lite inspection; controlled power-up; inrush/short checks

Deliverables: Practice board pass; FC v1 smoke test; rail/clock/SWD verified

Weeks 11–12
Topics:

Peripheral and sensor bring-up (I2C scan, SPI loopback, IMU/baro streaming, calibration)

ESC/motor interface, bench rig; PWM vs DShot signaling; failsafe output state

EE focus: Noise floor characterization; sag/EMI mitigation; timer channel mapping

Deliverables: Calibrated sensor logs and noise report; safe motor ramp tests; current/sag data

Weeks 13–14
Topics:

Integrate Joop’s estimator and rate loop on FC v1; complementary filter tuning

Safety/arming logic; RC/CLI; loss-of-signal and low-voltage failsafes

EE focus: Loop frequency/jitter plots; watchdog/reset handling

Deliverables: Ground integration pass (props off): sensor→estimator→rate loop→mixer; arming/failsafe validated

Week 15
Topics:

Design review, readiness for flight; contingency planning (FC v1.1/v2 if needed)

EE focus: DFM/DFA, PI/SI margins, risk mitigation

Deliverables: Review deck; action items; go/no-go decision

Semester 2 — Controls, Alt/Pos, GPS/Path, Tuning, Flight Test
Weeks 1–2
Topics:

Estimation refinement: complementary vs Mahony/Madgwick; mag options; Euler vs quaternions

Attitude/rate control design; anti-windup; derivative filtering; bench tuning

EE focus: Preserve deterministic timing; tuning interface (CLI)

Deliverables: Estimator validation plots; stable inner rate loop with step/sine testing

Weeks 3–4
Topics:

Vibration mitigation: prop/motor balance, soft-mounts; gyro LPF/notch filter design

First hover attempt with safety/tether; rate P/D tuning

EE focus: PSD analysis to place notches; mixer validation and motor directions

Deliverables: Vibration report and filter settings; stable hover in Attitude mode with logs

Weeks 5–6
Topics:

Altitude sensing and AltHold: baro filtering, vertical velocity (baro+accel), thrust linearization

GPS and compass: UART parsing (UBX/NMEA), fix/HDOP gating, mag calibration/alignment

EE focus: Sensor fusion practicalities; GPS quality gating before enabling modes

Deliverables: AltHold within target band; GPS/heading pipeline validated

Weeks 7–8
Topics:

Position estimation/hold: XY with GPS, Z with baro; anti-windup; rate limiting

Pathway/waypoint navigation: ENU conversion; L1/vector pursuit; RTL basics

EE focus: Safety limits (tilt/speed/altitude), mission abort conditions

Deliverables: PosHold within small radius; 3–5 waypoint mission at low speed/altitude

Weeks 9–10
Topics:

Robustness: failsafes for RC/GPS loss, low battery, geofence; RTL/land logic

Power/thermal reliability: regulator/ESC temps; brownout margin under load

EE focus: Test matrices; thermal measurement (IR/thermocouple)

Deliverables: Failsafe test results; reliability report and mitigations

Weeks 11–12
Topics:

Code quality/optimization: DMA for sensors, interrupt priorities, logging to SPI Flash/SD

Validation across modes and environments; KPI-based evaluation

EE focus: Deterministic loop timing under logging load; CPU/memory headroom

Deliverables: Optimized firmware; performance report (RMS pos/alt error, settling time)

Weeks 13–14
Topics:

Documentation/manufacturing package: schematics, BOM with alternates, Gerbers, assembly drawings

Final demo rehearsal; checklists/test cards; contingency plan

EE focus: Calibration/user guides; maintenance checklist

Deliverables: Release doc pack; demo-ready airframe

Week 15
Topics:

Final demonstration, evaluation, and post-mortem

EE focus: Flight metrics vs goals; repository archival

Deliverables: Public demo video; final report; retrospectives; archived repo

Joop Brokking Code Integration Notes
Early S1: Extract and unit-test math (complementary filter, PID, mixer) independent of hardware.

Mid S1: Port STM32 I/O layers (I2C/SPI/UART, timers, RC input), maintain loop timing; log jitter.

S2: Add AltHold (baro fusion), GPS gating, failsafes, CLI tuning, optional mag integration; move blocking I/O to DMA/interrupts; add blackbox logging.

Assessment (Suggested Weights)
Hardware design quality (schematic/layout, PI/SI/EMI, DFM/DFA): 25%

Firmware architecture and real-time/timing correctness: 20%

Estimation and control implementation/tuning: 20%

System reliability and safety (failsafes, testing discipline): 15%

Flight performance across modes: 10%

Documentation and professional practice: 10%
