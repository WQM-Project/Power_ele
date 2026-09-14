# Power Electronics & Propulsion (WQM-Project)

This repository contains the power and propulsion subsystem designs for the Water Quality Monitoring (WQM) remote-controlled vessel.

## Schematic Overview

The design is split across two main pages in [`Schematic.pdf`](./Schematic.pdf):

### 1. Sensing & Logic (Brief Overview)

The first page of the schematic covers the main STM32 Nucleo-F722ZE microcontroller, water quality sensors (DO, TDS, pH), environmental sensors (BME280), location tracking (GPS, IMU), and telemetry (Waveshare LoRa). These components run on 5V/3.3V logic and handle the vessel's data collection and transmission. It also includes the FlySky receiver for capturing manual RC steering commands.

### 2. Power Delivery & Propulsion (Detailed Description)

The second page focuses on the high-power routing that drives the vessel.

- **Power Source & Distribution:** A LiFePO4 battery supplies the main system voltage. The battery's positive terminal routes through an instant-cut emergency kill switch, ensuring the vessel can be mechanically powered down immediately if needed.
- **Logic Power Step-down:** Post-kill-switch, the raw battery voltage feeds into a DC-DC buck converter. This converter drops the voltage down to a stable 5V, which is then routed back to power the microcontroller and the sensor suite described on page 1.
- **Propulsion Drive:** Two SimonK 30A Brushless DC (BLDC) Electronic Speed Controllers (ESCs) draw power directly from the battery line. They receive PWM control signals from the STM32 and drive two underwater thrusters (CW and CCW) to provide the vessel's movement and differential steering.

## Bill of Materials (Power, Propulsion & Control)

| Component | Description | Qty | Unit Cost (INR) | Source | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ESC** | SimonK 30A BLDC Electronic Speed Controller | 2 | 700.00 | [Robu](https://robu.in/product/simonk-30a-bldc-esc-electronic-speed-controller-without-connectors/) | Direct install in electronics box. |
| **Thruster** | Furbabies Boat Underwater Propeller (CW/CCW) | 2 | 8,000 | [Amazon](https://amzn.in/d/00W6ubMV) | Direct install; no CAD needed. |
| **RC Transmitter/Receiver** | FlySky FS-i6 2.4G 6CH PPM RC Transmitter With FS-iA6B Receiver | 1 | 5,729 | Robu | Receiver goes in electronics box. |
| **Battery** | LiFePO4 Battery | 1 | TBD | TBD | Main power source (BOM pending) |
| **Kill Switch** | Instant Power Cut Emergency Switch | 1 | TBD | TBD | Safety disconnect (BOM pending) |
| **Buck Converter** | DC-DC Converter | 1 | TBD | TBD | Steps down to 5V for logic (BOM pending) |
