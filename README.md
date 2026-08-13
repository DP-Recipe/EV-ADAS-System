# 🚗 EV ADAS System

### Simulation-Based Electric Vehicle Control & Advanced Driver Assistance System

A **simulation-based EV control and ADAS project** developed using **STM32F103C8T6 firmware**, **PICSimLab**, **VSPE**, and a **Python real-time dashboard**.

The system simulates core EV control functions and ADAS features while communicating vehicle data from the simulated STM32 environment to a PC-based dashboard through a virtual serial connection.

---

## 📌 Project Overview

The project combines **embedded C firmware, automotive control logic, ADAS algorithms, sensor simulation, UART communication, and real-time data visualization** into a single simulation environment.

The STM32 firmware is executed within **PICSimLab**, while **VSPE (Virtual Serial Ports Emulator)** provides the virtual serial communication link between the simulation and the Python dashboard.

```text
┌─────────────────────┐
│      PICSimLab      │
│                     │
│  STM32F103C8T6      │
│  EV Control         │
│  ADAS Logic         │
│  Sensor Processing  │
│  Fault Management   │
└──────────┬──────────┘
           │
       Virtual UART
           │
           ▼
┌─────────────────────┐
│        VSPE         │
│ Virtual COM Ports   │
└──────────┬──────────┘
           │
       Virtual UART
           │
           ▼
┌─────────────────────┐
│  Python Dashboard   │
│                     │
│ Speed               │
│ SOC                 │
│ Temperature         │
│ Drive Mode          │
│ ADAS Status         │
│ Vehicle State       │
└─────────────────────┘
```

---

## ⚙️ Key Features

### 🔋 EV Control

* Accelerator and brake pedal monitoring
* ECO, NORMAL and SPORT drive modes
* Motor torque calculation
* Regenerative braking
* Vehicle speed estimation
* Battery State of Charge (SOC) estimation
* Driving range estimation
* Motor temperature modelling
* Vehicle state management

### 🛡️ ADAS

* **Forward Collision Warning (FCW)**
* **Time-to-Collision (TTC) estimation**
* **Blind Spot Detection (BSD)**
* Distance-based warning levels
* Critical collision warnings
* Ultrasonic sensor-based distance measurement

### ⚠️ Fault Management

* Fault detection
* Vehicle fault-state handling
* Safe-state transitions
* System operating-condition monitoring

### 📊 Real-Time Dashboard

The Python dashboard provides real-time visualization of the simulated vehicle:

* 🚗 Vehicle speed
* 🔋 Battery SOC
* 🌡️ Motor temperature
* ⚙️ Drive mode
* 🚦 Vehicle state
* ⚠️ ADAS warnings
* 📡 Sensor information
* 🔧 System status

---

## 🧠 Embedded System

The STM32 firmware was developed using **STM32CubeIDE** and follows a modular architecture.

### EV Control — `ev_control.c`

Responsible for:

* Pedal input processing
* Drive-mode selection
* Motor torque calculation
* Regenerative braking
* Speed modelling
* Power calculation
* SOC estimation
* Range estimation
* Motor thermal modelling

### ADAS — `adas.c`

Implements:

* Forward Collision Warning
* Time-to-Collision calculation
* Blind Spot Detection
* Warning thresholds
* Critical warning conditions

### Ultrasonic Sensors — `ultrasonic.c`

Handles ultrasonic sensor timing and distance measurement used by the ADAS algorithms.

### Fault Management — `fault.c`

Handles fault detection and transitions into appropriate vehicle safety states.

### UART Communication — `uart_shell.c`

Provides the serial communication interface used to transfer vehicle information between the simulated STM32 system and the Python dashboard.

---

## 🖥️ Simulation Environment

This project was developed and tested **completely in simulation** rather than on physical automotive hardware.

### PICSimLab

PICSimLab is used to provide the simulated embedded environment in which the STM32-based firmware and system inputs are tested.

### VSPE

**Virtual Serial Ports Emulator (VSPE)** creates interconnected virtual COM ports, allowing the PICSimLab simulation to communicate with the Python dashboard.

### Python Dashboard

The Python application receives the simulated vehicle data through the virtual serial connection and presents it through a real-time dashboard.

---

## 🔄 Data Flow

```text
Simulated Inputs
      │
      ▼
  PICSimLab
      │
      ▼
STM32 Firmware
      │
      ├── EV Control
      ├── ADAS
      ├── Fault Management
      └── Sensor Processing
      │
      │ UART
      ▼
     VSPE
      │
      │ Virtual COM
      ▼
Python Dashboard
      │
      ▼
Real-Time Vehicle Monitoring
```

---

## 🛠️ Technologies Used

| Category                 | Technologies      |
| ------------------------ | ----------------- |
| Microcontroller          | STM32F103C8T6     |
| Firmware                 | Embedded C        |
| IDE                      | STM32CubeIDE      |
| Configuration            | STM32CubeMX       |
| Simulation               | PICSimLab         |
| Serial Communication     | UART              |
| Virtual Serial Interface | VSPE              |
| Dashboard                | Python            |
| Embedded Libraries       | STM32 HAL         |
| Peripherals              | ADC, UART, Timers |

---

## 📁 Project Structure

```text
EV-ADAS-System/
│
├── ev_dash/
│   ├── Core/
│   │   ├── Inc/
│   │   └── Src/
│   │       ├── adas.c
│   │       ├── ev_control.c
│   │       ├── fault.c
│   │       ├── main.c
│   │       ├── uart_shell.c
│   │       └── ultrasonic.c
│   │
│   ├── Drivers/
│   │   ├── CMSIS/
│   │   └── STM32F1xx_HAL_Driver/
│   │
│   ├── Startup/
│   ├── ev_dash.ioc
│   └── STM32F103C8TX_FLASH.ld
│
├── ev_python/
│   └── ev_dash.py
│
├── .gitignore
└── README.md
```

---

## ▶️ Running the Project

### 1. STM32 Firmware

Open the project in **STM32CubeIDE** and load:

```text
ev_dash/ev_dash.ioc
```

Build the project and generate the firmware required for the simulation.

### 2. PICSimLab

Open the corresponding PICSimLab simulation and load the generated STM32 firmware.

Configure the required simulated inputs and sensors.

### 3. VSPE

Create a pair of interconnected virtual COM ports using VSPE.

Connect one virtual port to PICSimLab and use the other port for the Python dashboard.

### 4. Python Dashboard

Navigate to:

```text
ev_python/
```

Run:

```bash
python ev_dash.py
```

Configure the dashboard to use the appropriate virtual COM port created by VSPE.

---

## 🎯 Project Objectives

The project was developed to explore the integration of:

* Embedded systems
* Electric vehicle control
* ADAS algorithms
* Sensor interfacing
* UART communication
* Embedded system simulation
* Real-time monitoring
* PC-based visualization

The simulation-based approach enables development and testing of the complete system without requiring physical automotive hardware.

---

## 🚀 Future Scope

* CAN bus integration and simulation
* Real motor controller integration
* Physical sensor integration
* GPS integration
* Camera-based ADAS
* Advanced object detection
* Vehicle data logging
* Hardware-in-the-loop testing
* Integration with a physical EV platform

---


---

⭐ **If you find this project interesting, feel free to explore the implementation and simulation setup in the repository.**
