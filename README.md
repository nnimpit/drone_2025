# 📌 Senior Project 1
# 📌 บรรยายรายวิชา
รายวิชานี้มุ่งเน้นการพัฒนาทักษะทางวิศวกรรมไฟฟ้าและระบบควบคุม ผ่านการออกแบบและพัฒนาโดรน นักศึกษาจะได้เรียนรู้ตั้งแต่ การออกแบบ PCB, การประกอบอุปกรณ์, การเขียนโปรแกรมควบคุมด้วย STM32F103C8 และ Arduino IDE, การสื่อสารระหว่างอุปกรณ์, ไปจนถึงการทดสอบการบิน

โดยเนื้อหาของรายวิชาจะช่วยให้นักศึกษาสามารถ อธิบายความรู้เกี่ยวข้องกับการจัดการพลังงานของอุปกรณ์ (CLO1) เลือกใช้เทคโนโลยีที่เหมาะสม (CLO2), แก้ไขปัญหาที่เกิดขึ้นระหว่างพัฒนา (CLO3) และสร้างโครงการต้นแบบที่สามารถทำงานได้จริง

# 📌 เกณฑ์การให้คะแนน
- การเข้าเรียน (20%)
- การออกแบบ PCB (30%)
- ผลการประกอบและทดสอบบิน (30%)
- การนำเสนอ (20%)

# Flight Controller Development Plan (Semester 1)

| Weeks | Objectives | Topics | Labs | Deliverables |
|-------|------------|--------|------|--------------|
| **1–2**: Kickoff, Requirements, and Safety | - Define mission profile<br>- Establish development environment<br>- Safety practices | **Mission profile**: Frame size, prop/motor/ESC selection; flight time & payload; Max. Take off Weight (MTOW) <br>**EE focus**: Power/energy constraints<br>**Safety**: LiPo handling, Prop-off bench, Test stand, Range discipline<br>**Tooling setup**: Arduino–STM32, ST-LINK, HAL-lite mindset (timers, I2C/SPI, interrupts) | - LED blink<br>- SysTick timing markers<br>- UART printf over USB/serial | - Project charter<br>- System block diagram<br>- Risk register |
| **3–4**: Energy Budgeting and Power Tree | - Build quantitative energy model<br>- Draft power distribution design<br>- Start sensor I/O | **Energy modeling**: Battery Wh, hover vs maneuver draw, Flight-time<br>**Power tree**: Battery→ESCs, 5V→3.3V conversion, LC/TVS/EMI, grounding<br>**Measurement**: Current/voltage sensors (INA219/226, shunt/Hall)<br>**Sensor I/O**: IMU & baro basics, pull-ups, bus integrity, shielding | - Minimal Arduino drivers<br>- WHO_AM_I and burst reads<br>- Log raw gyro/accel/baro | - Energy budget spreadsheet<br>- Preliminary power schematic<br>- Sensor read demo + raw data |
| **5–6**: PCB Design — Power & MCU Core | - Capture schematics<br>- Validate ESC/motor interfacing | **Schematic**: STM32F103, clocking, SWD, decoupling, reset<br>**Power**: DC-DC rules, rails, thermal, returns<br>**EMI/surge**: LC input, TVS, analog/digital isolation<br>**Actuation**: ESC bench, throttle ramps, failsafe | - Motor/ESC tests (props off)<br>- PWM/timer timing | - Draft schematics (MCU+power)<br>- Library footprints<br>- ESC test firmware + timing report |
| **7–8**: Sensing + PCB Layout/Fab | - Implement electrical sensing for V/I telemetry<br>- Complete PCB layout | **Energy sensing**: Divider/ADC scaling, shunt vs Hall, calibration, filtering, Coulomb counting<br>**PCB layout**: Stack-up, decoupling, IMU/baro placement, return paths, via stitching, ground segregation | - Live V/I telemetry vs DMM<br>- ERC/DRC cleanup, generate Gerbers/BOM/CPL | - Verified telemetry + calibration<br>- ERC/DRC clean layout<br>- Gerbers/BOM/CPL submitted |
| **9–10**: Software Architecture + SMD Assembly | - Establish firmware architecture<br>- Train for SMD assembly | **Architecture**: Loop, sensor read, PID/mixer, arming; STM32 refactor; drivers; unit tests; CSV logging<br>**SMD process**: Solder paste, reflow, hot air, inspection | - Compile baseline firmware (STM32 dev board)<br>- Assemble practice board | - Compilable baseline<br>- IPC-style inspection checklist |
| **11–12**: Assemble FC v1 + Bring-Up | - Assemble FC v1<br>- Electrical bring-up & verification | **Assembly**: Power, MCU, IMU, baro, connectors, SWD<br>**Bring-up**: Programming, current checks, rail verification, UART/GPIO<br>- I2C/SPI scans, IMU/baro reads | - Follow bring-up checklist<br>- Log issues & fixes | - FC v1 passes smoke test<br>- Bring-up logbook + patch list |
| **13**: Sensor Calibration & Filtering | - Calibrate sensors<br>- Implement first-pass filtering | **Calibration**: Gyro bias, accel scale, baro offset, temp drift<br>**Filtering**: LPF/notch placeholders; store calibration constants | - Collect & validate datasets<br>- Persist + reload constants | - Calibration routine + constants<br>- Initial filter config |
| **14–15**: Semester 1 Checkpoint Demo | - Demonstrate system integration with safety logic & telemetry | **Integration rehearsal**: Arming FSM (dry-run), ESC spin (no props), Live sensor streaming with VI monitoring | - Full ground test plan<br>- Record logs<br>- Verify timing/jitter | - Checkpoint demo completed<br>- Ground test report |
