# Water Quality Monitoring (WQM) Autonomous Vessel

## 1. Project Links
- Repository: `WQM-Project/Power_ele`
- Schematic: [`Schematic.pdf`](./Schematic.pdf)

## 2. Problem Statement
Manual water quality testing in lakes and reservoirs is slow, labor-intensive, and limits spatial coverage. Fixed sensor buoys only measure water at a single location, missing localized pollution events or gradient changes across large water bodies.

## 3. Problem Solution
An autonomous surface vessel (ASV) navigates water bodies to collect real-time water quality metrics across multiple locations. The vessel uses GPS and LiDAR for navigation, environmental sensors to measure water conditions, and LoRa to transmit data to a base station.

## 4. System Representation

### System Overview
An STM32 Nucleo-F722ZE microcontroller aggregates sensor data, handles navigation, and controls propulsion. It communicates over LoRa for long-range telemetry. Two underwater thrusters provide differential thrust for steering.

### Block Diagram Description
1. **Sensing Layer:** Analog and digital sensors capture environmental data (pH, DO, TDS, temperature, humidity, pressure) and navigational data (GPS, IMU, LiDAR).
2. **Processing Layer:** The STM32 Nucleo-F722ZE reads sensor inputs via I2C, UART, SPI, and Analog pins.
3. **Communication Layer:** A Waveshare Core1262 LoRa module transmits telemetry via SPI. A FlySky receiver takes manual override commands.
4. **Propulsion Layer:** The STM32 outputs PWM signals to two SimonK 30A ESCs, which drive the underwater thrusters.
5. **Power System:** A LiFePO4 battery routes through an emergency kill switch to the ESCs and a buck converter. The converter steps the voltage down to 5V to power the MCU and sensors.

## 5. Tools, Sensors, and Equipment

- **Microcontroller:** STMicroelectronics NUCLEO-F722ZE (ARM Cortex-M7)
- **Water Quality Sensors:**
  - Dissolved Oxygen (DO) Sensor Kit (Galvanic, Analog out)
  - Analog TDS Sensor Module (Analog out)
  - Industrial Grade Analog pH Sensor Kit (Analog out)
- **Environmental Sensor:** BME280 (Temperature, Humidity, Pressure via I2C)
- **Navigation & Telemetry:**
  - 9-Axis IMU MPU-9250 (I2C/SPI)
  - LiDAR Sensor 4-Wire (Obstacle avoidance via UART)
  - Radiolink SE100 GPS (UART)
  - Waveshare Core1262 LoRa Module (Telemetry via SPI)
  - FlySky 6-Channel Receiver FS-iA6B (RC override)

## 6. Reported Specifications

### Communication Protocols
- **I2C:** BME280, MPU-9250 (SDA/SCL)
- **UART:** LiDAR (TX/RX), GPS (TX/RX)
- **SPI:** Waveshare Core1262 LoRa (MISO, MOSI, SCK, NSS)
- **Analog:** DO, TDS, pH sensors
- **PWM:** FlySky Receiver, ESC control

### Power Specifications
- **Main Source:** LiFePO4 Battery
- **Logic Power:** DC-DC Buck Converter (Steps battery voltage down to 5V)
- **Safety:** Manual Kill Switch (Instant power cut)

## 7. Bill of Materials (Power & Propulsion)

| Component | Description | Qty | Unit Cost (INR) | Source | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ESC** | SimonK 30A BLDC Electronic Speed Controller | 2 | 700.00 | [Robu](https://robu.in/product/simonk-30a-bldc-esc-electronic-speed-controller-without-connectors/) | Direct install; no CAD needed. |
| **Thruster** | Furbabies Boat Underwater Propeller (CW/CCW) | 2 | 8,000 | [Amazon](https://amzn.in/d/00W6ubMV) | Direct install; no CAD needed. |
| **Battery** | LiFePO4 Battery | 1 | TBD | TBD | Main power source (BOM pending) |
| **Kill Switch** | Instant Power Cut Emergency Switch | 1 | TBD | TBD | Safety disconnect (BOM pending) |
| **Buck Converter** | DC-DC Converter | 1 | TBD | TBD | Steps down to 5V for logic (BOM pending) |
