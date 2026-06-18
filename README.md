

---

# Smart IoT-Based Weather Monitoring System

An industrial-grade, self-sustaining weather station built on the ESP32 platform. This project implements advanced **Low-Power Optimization** techniques alongside a hybrid communication stack to achieve indefinite energy autonomy via solar harvesting.

---

## 👥 Group Information

* **Group Number:**
* **Team Members:**
* Sarathi Jayasekara
* Ravindu Weerakoon
* Yuvindu Dassanayaka
* Dhupika Bandara



---

## 🚀 Core Features

* **Energy Autonomy:** Operates using ultra-low power deep sleep cycles ($<10\mu A$) optimized by hardware-level power-gating and solar charging circuits.
* **Hybrid Connectivity:** Automatically adapts its communication stack between Wi-Fi and GSM/GPRS based on signal availability and power constraints.
* **Data Integrity:** Employs a "Sample, Buffer, Burst" strategy using ESP32 RTC memory to minimize radio transmissions, alongside idempotent API ingestion to prevent data duplication.
* **Scalable Time-Series Backend:** High-performance data ingestion powered by FastAPI and TimescaleDB, built for efficient storage and complex environmental data analysis.

---

## 📐 System Architecture

### 1. Hardware Layer

The hardware utilizes a modular bus system designed for flexible sensor deployments:

* **Processing Core:** Dual-core ESP32 (separating sensing tasks from transmission tasks).
* **Environmental Sensing:** I2C-based sensors including **BME280** (Temperature, Humidity, Pressure) and **BH1750** (Lux/Optical).
* **Power Subsystem:** Triple solar panel array (~3W peak), 18650 lithium cells, custom charging circuitry, and Low Dropout Regulators (LDOs) for high efficiency.

### 2. Software & Power Strategy

Instead of continuous polling, the firmware executes an optimized cycle:

1. **Sample:** Sensors are powered on via a P-channel MOSFET switch, sampled, and immediately de-energized.
2. **Buffer:** Readings are securely written to the ESP32's **RTC memory**, preserving data through deep sleep.
3. **Burst:** Upon reaching a set buffer threshold, the system wakes the network stack (Wi-Fi or GPRS) for a high-speed data burst to the backend.

### 3. Industrial Backend Design

* **API Framework:** Asynchronous FastAPI for high-concurrency ingestion.
* **Database:** TimescaleDB (PostgreSQL) optimized for time-series datasets.
* **Security & Reliability:** Device-level API key authentication, rate-limiting, schema validation, and idempotent ingestion pipelines.
* **Observability:** Health checks and threshold-based automated alerts.

---

## 🗺️ Project Roadmap & Build Order

* [ ] **Phase I: Core Logic** – Establish stable I2C sensor communication and implement deep sleep logic.
* [ ] **Phase II: Power Gating** – Integrate P-channel MOSFETs to completely de-energize sensors during sleep cycles.
* [ ] **Phase III: Networking Failover** – Develop software logic to seamlessly switch between Wi-Fi (primary) and GSM (backup).
* [ ] **Phase IV: Data Visualization** – Deploy the FastAPI backend and connect a dashboard (e.g., Grafana) for real-time monitoring.

---

## 🛠️ Repository Structure

```text
├── firmware/              # ESP32 Source Code (C++/Arduino/ESP-IDF)
│   ├── src/               # Core logic (Sensors, Power Management, Network)
│   └── lib/               # Hardware and sensor libraries
├── backend/               # FastAPI Application
│   ├── app/               # Main application logic & API routes
│   ├── database/          # TimescaleDB migrations and schemas
│   └── requirements.txt   # Python dependencies
├── hardware/              # Schematic and PCB layout files
└── README.md              # Project documentation

```

---

## ⚡ Quick Start (Development)

### Prerequisites

* **Hardware:** ESP32 Development Board, BME280, BH1750, 18650 Battery, Solar Panel.
* **Software:** VS Code + PlatformIO (or Arduino IDE), Python 3.10+, Docker (for TimescaleDB).

### Backend Setup

1. Clone the repository and navigate to the backend directory:
```bash
git clone https://github.com/[your-repository].git
cd backend

```



```
2. Install dependencies:
   ```bash
pip install -r requirements.txt

```

3. Run the development server:
```bash

```



uvicorn app.main:app --reload

```

### Firmware Setup
1. Open the `firmware/` folder in **PlatformIO**.
2. Configure your WiFi credentials and backend API URL in `config.h`.
3. Build and upload the code to your ESP32.

***

Would you like me to add specific configuration scripts, license templates, or expand the hardware schematics section for this README?

```
