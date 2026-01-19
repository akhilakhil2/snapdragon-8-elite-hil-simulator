Snapdragon 8 Elite HIL Simulator & Validation Suite

📱 Project Overview

This project is a Hardware-in-the-Loop (HIL) Simulator for the Snapdragon 8 Elite (Gen 5) System-on-a-Chip (SoC). It simulates real-time hardware telemetry, including 8-core cluster dynamics, thermal throttling behaviors, and Power Management IC (PMIC) safety protocols.

The system is designed with a Dual-Layer Validation Architecture, ensuring that both the hardware logic (Backend API) and the monitoring interface (Frontend UI) operate within strict safety parameters.

🛠 Tech Stack

Backend/Simulator: FastAPI (Python) – Handles physics-based telemetry and state machine logic.

Frontend Dashboard: HTML5, CSS3 (Tailwind-inspired), JavaScript (ES6) – Real-time data visualization.

Automated Testing: * Pytest: API logic and hardware state validation.

Playwright: E2E UI testing and responsive layout verification.

🚀 Key Engineering Features

1. 8-Core Cluster Modeling

Simulates the advanced architecture of the Snapdragon 8 Elite:

2x Prime Cores (Oryon): Scaling up to 4.32 GHz for peak workloads.

6x Performance Cores: Efficiently handling multi-threaded background processes.

2. Thermal Throttling (Safety Governor)

Logic-driven clock speed capping designed to protect hardware integrity:

Triggers when SoC temperature exceeds 85°C.

Features recovery hysteresis to prevent "frequency oscillation" during cooling phases.

3. PMIC Battery Override

Automatic power state transitions based on critical thresholds:

Battery Saver: Triggered at 20% capacity.

Ultra Saver: Triggered at 5% capacity (Disables Prime cores, caps performance cores).

4. Real-time Telemetry

A constant 1Hz heartbeat synchronizes the hardware state machine with the dashboard, providing high-fidelity monitoring of voltage, clock speed, and thermals.

🧪 Automated Testing Suite (Regression Rig)

The project includes a robust regression suite to ensure system stability during software updates.

1. Backend Logic Tests (pytest)

Path: tests/test_backend.py

Telemetry Integrity: Ensures correct JSON structure and core counts.

Physics Accuracy: Verifies clock speed boosts in High-Performance mode.

Safety Rejection: Confirms the API rejects unsafe power requests when battery is low.

2. UI/UX Automation (playwright)

Path: tests/test_ui.py

Responsive Layout: Grid alignment verification on Mobile, Tablet, and Desktop breakpoints.

Visual Alerts: Verification of red "Throttling" alerts and CSS state animations.

E2E Safety Flow: Automated verification of the PMIC auto-override reflected in the browser DOM.

🚦 Getting Started

Prerequisites

Python 3.9+

Node.js (for Playwright browser binaries)

Installation

Clone the repo:

git clone https://github.com/akhilakhil2/snapdragon-8-elite-hil-simulator.git
cd snapdragon-8-elite-hil-simulator


Install dependencies:

pip install -r requirements.txt
playwright install chromium


Running the Simulator

uvicorn main:app --reload


Navigate to http://127.0.0.1:8000 to view the interactive dashboard.

Running the Test Rig

# Run all tests (Headless mode)
pytest -v

# Run UI tests with slow-mo for debugging/inspection
pytest --headed --slowmo 500 tests/test_ui.py
