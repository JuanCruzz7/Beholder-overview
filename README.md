# Beholder — Skydiving Trajectory Visualizer

**Full-Stack Telemetry System for High-Fidelity Jump Analysis**

> ⚠️ This repository contains documentation and interface only. Hardware schematics and source code are private — this is an active commercial project under development.

---

## Overview

Beholder is a hardware + software system designed for the precise capture and 3D spatial analysis of skydiving trajectories. It consists of two tightly integrated components: a custom-built wearable data logger and a browser-based 3D analysis engine.

The system is built around a core principle: **data integrity over aesthetics**. Rather than smoothing or interpolating sensor data, Beholder uses a *Nearest Neighbor* approach — every cursor position on the visualizer snaps to a real recorded data point, ensuring that analysis reflects what actually happened in the air.

---

## System Architecture

```
[Wearable Hardware Logger]
        |
        | .csv file (via microSD)
        v
[Beholder Analyser - Browser SPA]
        |
        |---> 3D Path Rendering (Three.js)
        |---> Heatmap Analysis (Speed / Pitch / Roll)
        |---> Geospatial Overlay (Google Maps Static API)
        |---> Multi-Track Comparison
```

---

## Components

### 1. Hardware — High-Precision Data Logger

A compact, wearable device recording 9-axis motion and environmental data at high frequency to a microSD card.

| Component | Function | Protocol |
|---|---|---|
| ESP32 (Dual-core) | Main MCU — Wi-Fi/BT ready for future live telemetry | — |
| BNO085 (9-axis IMU) | Sensor fusion — stabilized Heading, Pitch, Roll | I2C |
| BMP390 | High-precision barometric altimeter (sub-meter accuracy) | I2C |
| M100 Mini GPS (drone-grade) | High-speed positioning, rapid satellite lock | UART |
| MicroSD Module | Logs data in `.csv` format | SPI |
| LiPo 3.7V + USB-C | Battery with DC-DC step-up for stable 5V / 3.3V rails | — |

---

### 2. Software — Beholder Analyser

A high-performance, browser-based 3D visualization tool built with Three.js. No installation required — delivered as a single monolithic HTML file.

**Key capabilities:**

- **3D Path Rendering** — Visualizes jump trajectories as adaptive tube geometries in a full 3D coordinate system
- **Heatmap Analysis** — Dynamically colors the path based on Speed, Pitch, or Roll to identify aerodynamic efficiency and deployment points
- **Data Snap (Integrity Mode)** — Cursor locks to exact raw sensor data points — no interpolation, no mathematical guessing
- **Geospatial Context** — Optional Google Maps Static API integration to project real satellite imagery beneath the flight path
- **Multi-Track Comparison** — Load multiple `.csv` files simultaneously to compare flight lines, wingsuit glides, or jumper-to-jumper performance

---

## Data Format

The analyser auto-maps headers from standard CSV files.

| Column | Description | Required |
|---|---|---|
| `lat`, `lon` | Global positioning | ✅ |
| `alt` | Barometric or GPS altitude | ✅ |
| `vel` / `speed` | Groundspeed or 3D velocity | For heatmaps |
| `pitch`, `roll` | Orientation from BNO085 | For heatmaps |

---

## Availability

> The Beholder Analyser and hardware firmware are not publicly available at this stage — this is an active commercial project under development.
>
> A browser-based interactive demo is planned for a future release.

## Technical Stack

| Layer | Technology |
|---|---|
| Hardware firmware | C++ (Arduino / ESP-IDF) |
| 3D visualization | Three.js v0.166.1 |
| Frontend | Vanilla JavaScript (ES6+) |
| UI | Custom dark-mode technical interface |
| Hardware protocols | I2C · SPI · UART |

---

## Status

🔧 **Active development** — hardware logger functional, analyser core complete, live telemetry (Wi-Fi) planned for next phase.

---

## Author

**Juan Cruz Armando** — Electronic Engineer & Embedded Software Developer

[cruzjuanarmando@gmail.com](mailto:cruzjuanarmando@gmail.com) · [github.com/JuanCruzz7](https://github.com/JuanCruzz7)
