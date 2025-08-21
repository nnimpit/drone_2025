# drone_2025
Drone Project 2025
Semester 1: Hardware, Interfaces, PCB, Assembly, Bring-up
Weeks	Topics (Lecture & Lab)	EE Emphasis	Key Deliverables
1–2	Kickoff, requirements, safety; STM32F103 architecture, toolchain bring-up, GPIO/SysTick	System requirements, LiPo safety, code repo hygiene; clock tree, decoupling, NVIC	Project charter, BOM draft, risk register, minimal STM32 project and coding standards
3–4	Power electronics & distribution; I2C/SPI interfaces and signal integrity; IMU/baro reading on dev board	LC filters, TVS, brownout; pull-ups, bus capacitance, logic-analyzer measurements	Power tree schematic and component choices; WHO_AM_I + raw read logs; SI notes with scope captures
5–6	Joop Brokking code walkthrough and STM32 port plan; FC v1 schematic capture	Code modularization, separating math vs I/O; schematic ERC, test points, programming access	Porting plan and unit tests for filter/PID/mixer; completed schematic, libraries, ERC pass
7–8	PCB layout for EMI/EMC; deterministic scheduler and timing budget; send for fab	Ground planes/returns, decoupling placement, IMU/baro placement, baro vent; jitter measurement	Gerbers/BOM/pos files submitted; timing report with GPIO markers and jitter CSV
9–10	SMD assembly training and reflow; FC v1 assembly and electrical validation	Reflow profiles, inspection (IPC-lite), rework; rail verification, inrush, SWD	Assembled practice board; FC v1 smoke test pass, rail/clock/SWD verified
11–12	Sensor and peripheral bring-up on FC v1; ESC/motor interface and bench rig	I2C scan, SPI loopback, calibration storage; timer/PWM or DShot signaling and SI	Calibrated IMU/baro logs and noise report; safe motor ramp test, current/sag measurements
13–14	Integrate Joop’s estimator and rate loop on FC v1; safety/arming logic, failsafes	Complementary filter tuning; watchdog, low-voltage cutoff, RC loss behavior	Loop frequency/jitter plots; arming/failsafe implementation and ground test pass
15	Design review, readiness for flight testing; contingency for FC v2	DFM/DFA review, PI/SI margins, risk mitigation	Formal review slides, action items, go/no-go decision
