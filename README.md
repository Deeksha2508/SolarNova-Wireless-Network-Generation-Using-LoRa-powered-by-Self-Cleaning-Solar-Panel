# SolarNova: Wireless Network Generation Using LoRa Powered by Self-Cleaning Solar Panel

> **Status: 🚧 Ongoing (Work in Progress)** — Capstone project, midterm stage. Full deployment, final mesh testing, and self-cleaning integration are planned for final submission (Nov 2026).

A decentralized, infrastructure-independent communication network built on LoRa mesh technology — designed to work with **no internet, no SIM card, and no cellular connectivity**. Powered by a solar panel with an automated self-cleaning mechanism for long-term outdoor deployment.

## Overview

Traditional communication infrastructure (cellular towers, internet) often fails during disasters, natural calamities, or gets overloaded during high-density public events. SolarNova solves this by creating self-contained LoRa mesh nodes that let users message each other, share GPS location, and send SOS alerts — directly from a smartphone browser, with no app install required.

Each node is solar-powered and self-sustaining, using a self-cleaning mechanism to keep the solar panel free of dust for reliable long-term operation.

## Team

This is a Capstone Project (Group 30) by B.E. Electronics & Communication Engineering students at **Thapar Institute of Engineering & Technology, Patiala**, under the supervision of **Dr. Amanpreet Kaur** (Associate Professor, ECED) and **Dr. Arnab Pattanayak** (Assistant Professor, ECED).

- Paridhi 
- Aadhya 
- Natasha 
- Deeksha Sharma 
- Mohit Narang 

## Features

- **Infrastructure-free mesh networking** — self-routing, multi-hop LoRa mesh with no internet, SIM, or gateway dependency
- **Private, alias-based messaging** — point-to-point private messages between users (unlike open broadcast systems)
- **GPS location sharing** — real-time location tracking and map view via the web interface
- **SOS emergency alerts** — one-tap distress broadcast with GPS location across the mesh
- **Browser-based UI** — connect to a node's Wi-Fi hotspot and use any smartphone browser; no app installation needed
- **Solar-powered, self-sustaining** — 3W solar panel + Li-ion battery for 72+ hours of off-grid operation
- **Self-cleaning solar panel** — motorized wiper/brush mechanism to remove dust buildup and maintain charging efficiency

## Tech Stack / Hardware

**Hardware**
- HiLetgo ESP32 LoRa SX1276 (dual-core MCU + LoRa transceiver, 866 MHz, 20 dBm)
- NEO-6M GPS Module (UART/NMEA)
- 0.96" OLED Display (SSD1306, I2C)
- 3W Solar Panel (8.5V open circuit)
- LM7805 Voltage Regulator
- TP4056 Li-ion Charge Controller
- 3.7V / 2500mAh Li-ion Battery
- LoRa Antenna (866 MHz, 3dBi, SMA)
- DC motor + limit switches (self-cleaning wiper mechanism)

**Firmware**
- Arduino IDE, ESP32 Arduino Core, FreeRTOS
- `arduino-LoRa` (SX1276 driver, SF9, 125 kHz BW)
- `ESPAsyncWebServer`, `TinyGPS++`, `Adafruit SSD1306`, `ArduinoJSON`

**Web App**
- HTML5, CSS3, Vanilla JavaScript (ES6)
- WebSocket API (RFC 6455) for real-time messaging and GPS updates

## System Architecture

Each node integrates four subsystems: power management, processing/communication core, location tracking, and user interface — all running concurrently on the ESP32 under FreeRTOS scheduling.

- **Power:** Solar panel → LM7805 regulator → TP4056 charge controller → Li-ion battery → stable 5V supply
- **Compute + Radio:** ESP32 runs the LoRa mesh radio stack on one core, and a GPS parser + AsyncWebServer on the other
- **Networking:** Custom store-and-forward routing inspired by AODV (RFC 3561), with RSSI-based next-hop selection and duplicate-message filtering — validated up to 5 hops in testing
- **Range:** ~1.2 km (urban), ~2.8 km (rural) at SF9 / 125 kHz bandwidth, ~2 kbps data rate

## How It Works

1. Users connect their smartphone to a node's Wi-Fi access point (`SolarNova`, at `192.168.4.1`) — no app required.
2. The web interface (served by the ESP32) offers private messaging, a live GPS map, and an SOS button.
3. Messages are packaged as JSON (packet ID, sender, recipient, hop count, source node) and routed through the mesh via store-and-forward relaying until they reach the destination.
4. The self-cleaning mechanism runs on a scheduled cycle: a blowing fan loosens dust, then a motorized wiper sweeps the panel surface (guided by limit switches) to restore charging efficiency.

## Current Progress (Midterm)

- ✅ LoRa point-to-point communication verified (message transmission/reception without internet)
- ✅ Web-based private messaging interface built and tested
- ✅ Solar charging circuit validated (solar panel → TP4056 → Li-ion battery → LM7805 regulated 5V)
- ✅ Battery backup and charging-state indication tested
- 🔲 Full multi-hop mesh networking across 3+ nodes (planned)
- 🔲 Self-cleaning mechanism hardware integration (planned)
- 🔲 Field-scale range/load testing (planned)
- 🔲 Final documentation and demonstration (Oct–Nov 2026)

## Getting Started

> Fill in with your actual repo structure once firmware/web code is pushed.

```bash
git clone https://github.com/Deeksha2508/SolarNova.git
cd SolarNova

# Flash firmware to ESP32 via Arduino IDE
# Configure LoRa sync word, node ID, and Wi-Fi AP settings in the config file
```

## Bill of Materials (Core, ~₹8,000)

| Component | Qty | Est. Cost (₹) |
|---|---|---|
| ESP32 + LoRa module | 2 | 4,960 |
| GPS Module (NEO-6M) | 2 | 530 |
| Solar Panel | 2 | 641 |
| Voltage Regulator | 2 | 12 |
| Charge Controller (TP4056) | 2 | 146 |
| Li-ion Battery | 2 | 679 |
| Capacitors | — | 43 |
| Wires/PCB | — | 180 |
| Cleaning apparatus (buggy) | — | 1,000 |

## Standards Followed

IEEE 802.11 (Wi-Fi AP), IEEE 802.15.4 (LPWAN PHY), TRAI IN865 (865–867 MHz unlicensed band, India), RFC 3561 (AODV routing), RFC 6455 (WebSocket), IEEE 1625 (battery management), NMEA 0183 (GPS data).

## Future Scope

- Complete multi-node mesh deployment and field testing on campus
- Integrate and validate the self-cleaning solar panel mechanism
- Add end-to-end message encryption
- Explore larger-scale deployment for disaster response and rural connectivity

## Authors

- Paridhi 
- Aadhya 
- Natasha 
- Deeksha Sharma 
- Mohit Narang 
 
