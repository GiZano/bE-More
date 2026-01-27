# ⚡ bE-More: Company Energetic Efficiency System

![bE-More architecture](https://github.com/user-attachments/assets/7b5e7096-b4c3-451a-82bb-c95ca022e853)

> **Fullstack IoT solution utilizing Arduino, ThingsBoard, and Local AI (Mistral:7b) to optimize workspace energy consumption.**

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-Local_AI-333333?style=for-the-badge&logo=ollama&logoColor=white)
![ThingsBoard](https://img.shields.io/badge/ThingsBoard-IoT_Core-29B6F6?style=for-the-badge&logo=thingsboard&logoColor=white)

---

## 📖 Overview
**bE-More** is a semi-automatic system designed to increase energy efficiency in working environments. It combines **embedded hardware** for real-time sensing, a **Java Dashboard** for management, and **Local Generative AI** for data analysis.

### ✨ Key Features
* **IoT & MQTT:** Real-time communication between sensors and the cloud.
* **Smart Automation:** Automatic shutdown of lights when natural light is sufficient (`> 450` value).
* **Privacy-First AI:** Uses a local instance of **Mistral:7b** (via Ollama) to analyze consumption trends without sending data to external APIs.
* **Hybrid Interface:** A Java 23 application combining a WebView dashboard and a console-based AI assistant.

---

## 📐 Hardware & Wiring
The physical layer consists of an Arduino board communicating via MQTT Protocol.

![circuit](https://github.com/user-attachments/assets/bca92431-5202-4c54-b24f-d2595b3f0679)

### Logic Table
The system manages the environment based on sensor inputs and button states:

| Input / Condition | State | Action Triggered |
| :--- | :--- | :--- |
| **Button "AUTO" (Pin 2)** | Pressed | Toggles **Auto Mode**. Activates Buzzer & Status LED. |
| **Button "LED" (Pin 1)** | Pressed | Manually toggles Main LEDs (Pin 5). |
| **Light Sensor (A3)** | `> 450` & `Auto Mode ON` | **Auto-Shutdown:** Turns OFF Main LEDs to save energy. |

---

## 🧠 Software Architecture & AI
The project integrates multiple layers of technology:

### 1. Java Desktop App (Controller)
Built with **Java 23**, acting as the central hub:
* **WebViewer:** Embeds the ThingsBoard dashboard (port 8080) for visual data monitoring.
* **Console Bridge:** Connects to the Python backend to trigger AI analysis.

### 2. Python AI Analyzer (Intelligence)
A Python script that interfaces with a local LLM:
1.  **Fetches Data:** Retrieves historical telemetry from ThingsBoard.
2.  **Processes:** Sends formatted data prompts to **Ollama (Mistral:7b)**.
3.  **Predicts:** Returns efficiency trends and anomaly detection to the user console.

---

## 🚀 Setup & Installation

### Prerequisites
* [Java JDK 23](https://www.oracle.com/java/technologies/downloads/)
* [ThingsBoard CE](https://thingsboard.io/) (running on `localhost:8080`)
* [Ollama](https://ollama.com/) with Mistral model:
    ```bash
    ollama pull mistral
    ```

### Quick Start
1.  **Hardware:** Flash the provided sketch to your Arduino and wire components as per the diagram.
2.  **Backend:** Configure your MQTT Device in ThingsBoard.
3.  **AI Service:** Start the local model server:
    ```bash
    ollama serve
    ```
4.  **Run the App:** Compile and run the Java application.

---

## 📚 Documentation
For detailed step-by-step guides, please refer to the **[Project Wiki](../../wiki)**:
* [📄 Extended Hardware Guide](../../wiki/Hardware-Wiring)
* [📄 Full Software Architecture](../../wiki/Software-Architecture)
* [🇮🇹 Descrizione in Italiano](../../wiki/Italian-Description)

---
*Created by [GiZano](https://github.com/GiZano)*
