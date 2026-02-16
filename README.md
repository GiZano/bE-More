<div align="center">

# ⚡ bE-More: Company Energetic Efficiency System

### Fullstack IoT & Local AI Architecture for Workspace Optimization

<img src="https://github.com/user-attachments/assets/7b5e7096-b4c3-451a-82bb-c95ca022e853" alt="bE-More architecture" width="80%" />
<br><br>

![Java](https://img.shields.io/badge/Java_23-Controller-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Arduino](https://img.shields.io/badge/Arduino-Edge_Hardware-00979D?style=for-the-badge&logo=Arduino&logoColor=white)
![Python](https://img.shields.io/badge/Python-AI_Bridge-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-Local_LLM-333333?style=for-the-badge&logo=ollama&logoColor=white)
![ThingsBoard](https://img.shields.io/badge/ThingsBoard-IoT_Platform-29B6F6?style=for-the-badge&logo=thingsboard&logoColor=white)

</div>

---

## 📖 Overview

**bE-More** is an advanced, semi-autonomous IoT system engineered to optimize energy consumption within enterprise working environments. The architecture integrates **embedded hardware** for real-time telemetry, a **Java-based Dashboard** for centralized management, and **Local Generative AI** for predictive data analysis.

### ✨ Key Features
* **📡 IoT & MQTT Telemetry:** Real-time, low-latency communication between edge sensors and the centralized ThingsBoard cloud instance.
* **⚙️ Smart Automation:** Rule-based environmental control (e.g., automatic lighting shutdown when ambient natural light exceeds a `> 450` threshold).
* **🔒 Privacy-First AI Analytics:** Utilizes a locally hosted instance of **Mistral:7b** (via Ollama) to analyze consumption trends and detect anomalies, ensuring sensitive corporate data never leaves the internal network.
* **🖥️ Hybrid Interface:** A robust Java 23 application that seamlessly embeds a visual web dashboard alongside a console-based AI assistant.

---

## 📐 Hardware Architecture

The physical layer relies on an Arduino microcontroller handling sensor data acquisition and MQTT transmission.

<div align="center">
  <img src="https://github.com/user-attachments/assets/bca92431-5202-4c54-b24f-d2595b3f0679" alt="Circuit Wiring Diagram" width="70%" />
</div>

### Edge Logic & Actuation
The embedded system manages the environment based on the following deterministic rules:

| Input Sensor / Actuator | State | System Action |
| :--- | :--- | :--- |
| **"AUTO" Button (Pin 2)** | Pressed | Toggles **Autonomous Mode**. Engages status LED and confirmation Buzzer. |
| **"LED" Button (Pin 1)** | Pressed | Manual override to toggle Main Workspace LEDs (Pin 5). |
| **Photoresistor (A3)** | `> 450` + `Auto Mode ON` | **Energy Saver:** Automatically powers down Main LEDs to reduce consumption. |

---

## 🧠 Software Stack & AI Integration

The project features a decoupled, multi-tier software architecture:

### 1. The Controller (Java Desktop App)
Developed in **Java 23**, this application acts as the central operations hub:
* **WebView Integration:** Natively embeds the local ThingsBoard dashboard (port 8080) for real-time data visualization.
* **Process Bridging:** Manages the lifecycle and communication with the Python-based AI backend via console streams.

### 2. The Intelligence (Python + Local LLM)
A Python service acting as the middleware between the IoT data and the Generative AI:
1.  **Data Ingestion:** Fetches historical telemetry and state changes from the ThingsBoard API.
2.  **Prompt Engineering:** Formats the raw time-series data into contextual prompts optimized for **Ollama (Mistral:7b)**.
3.  **Inference:** The LLM processes the data locally to identify inefficiencies, predict trends, and return actionable energy-saving insights directly to the Java console.

---

## 🚀 Setup & Deployment

### Prerequisites
* [Java JDK 23](https://www.oracle.com/java/technologies/downloads/)
* [ThingsBoard CE](https://thingsboard.io/) (configured on `localhost:8080`)
* [Ollama](https://ollama.com/) with the Mistral model installed:
    ```bash
    ollama pull mistral
    ```

### Quick Start Guide
1.  **Hardware Provisioning:** Wire the components according to the schematic and flash the provided C++ sketch to the Arduino.
2.  **IoT Platform:** Configure the MQTT Device profile and dashboards within your ThingsBoard instance.
3.  **Initialize AI Service:** Start the local Ollama inference server:
    ```bash
    ollama serve
    ```
4.  **Launch the Hub:** Compile and execute the Java application to monitor and optimize your environment.

---

## 📚 Documentation & Deep Dive

For detailed wiring schematics, full architectural diagrams, and step-by-step guides, please refer to the **[Project Wiki](../../wiki)**:

* [📄 Extended Hardware & Wiring Guide](../../wiki/Hardware-Wiring)
* [📄 Full Software Architecture & API Spec](../../wiki/Software-Architecture)
* [🇮🇹 Documentazione in Italiano](../../wiki/Italian-Description)

---
<div align="center">

**Architected and Developed by [GiZano](https://giovanni-zanotti.is-a.dev)**

</div>
