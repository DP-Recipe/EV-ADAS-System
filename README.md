\# EV ADAS System



A simulation-based Electric Vehicle (EV) control and Advanced Driver Assistance System (ADAS) developed using \*\*STM32F103C8T6 firmware\*\*, \*\*PICSimLab\*\*, \*\*VSPE\*\*, and a \*\*Python-based real-time dashboard\*\*.



The project simulates an EV control system and ADAS functionality in a virtual embedded environment. The STM32 firmware is executed within \*\*PICSimLab\*\*, while \*\*VSPE (Virtual Serial Ports Emulator)\*\* provides the virtual serial connection between the simulation and the Python dashboard.



\## System Overview



The project consists of three main components:



1\. \*\*STM32 Firmware\*\* – Embedded C code developed using STM32CubeIDE.

2\. \*\*PICSimLab Simulation\*\* – Used to simulate the STM32-based system and its inputs/sensors.

3\. \*\*Python Dashboard\*\* – Displays the simulated vehicle parameters and ADAS status in real time.



Communication between PICSimLab and the Python dashboard is established using \*\*VSPE\*\*, which creates a pair of interconnected virtual COM ports.



\## Features



\### EV Control



\* Accelerator and brake pedal monitoring through ADC

\* Multiple drive modes:



&#x20; \* ECO

&#x20; \* NORMAL

&#x20; \* SPORT

\* Motor torque calculation

\* Regenerative braking

\* Vehicle speed estimation

\* Battery State of Charge (SOC) estimation

\* Estimated driving range

\* Motor temperature monitoring

\* Vehicle state management



\### ADAS



\* Forward Collision Warning (FCW)

\* Time-to-Collision (TTC) estimation

\* Blind Spot Detection (BSD)

\* Distance-based warning levels

\* Critical collision warnings

\* Ultrasonic sensor-based distance measurement



\### Fault Management



\* Vehicle fault detection

\* Fault-state handling

\* Safe-state transitions

\* Monitoring of system operating conditions



\### Real-Time Dashboard



The Python dashboard receives data from the simulated STM32 system and displays:



\* Vehicle speed

\* Battery SOC

\* Motor temperature

\* Drive mode

\* Vehicle state

\* ADAS warnings

\* Sensor information

\* Vehicle status



\## System Architecture



```text

&#x20;                  ┌──────────────────────────┐

&#x20;                  │     PICSimLab Simulation  │

&#x20;                  │                          │

&#x20;                  │     STM32F103C8T6        │

&#x20;                  │                          │

&#x20;                  │  EV Control              │

&#x20;                  │  ADAS Logic              │

&#x20;                  │  Fault Management        │

&#x20;                  │  Sensor Processing       │

&#x20;                  └────────────┬─────────────┘

&#x20;                               │

&#x20;                        Virtual COM Port

&#x20;                               │

&#x20;                               ▼

&#x20;                  ┌──────────────────────────┐

&#x20;                  │           VSPE           │

&#x20;                  │ Virtual Serial Port      │

&#x20;                  │       Emulator           │

&#x20;                  └────────────┬─────────────┘

&#x20;                               │

&#x20;                        Virtual COM Port

&#x20;                               │

&#x20;                               ▼

&#x20;                  ┌──────────────────────────┐

&#x20;                  │     Python Dashboard     │

&#x20;                  │                          │

&#x20;                  │  Speed                   │

&#x20;                  │  SOC                     │

&#x20;                  │  Temperature             │

&#x20;                  │  Drive Mode              │

&#x20;                  │  ADAS Status             │

&#x20;                  │  Vehicle State           │

&#x20;                  └──────────────────────────┘

```



\## Simulation Environment



The complete system was developed and tested \*\*in simulation\*\*.



\### PICSimLab



\*\*PICSimLab\*\* is used as the embedded simulation environment. It provides the virtual hardware environment in which the STM32-based control system is tested.



The simulated inputs include parameters such as:



\* Accelerator pedal

\* Brake pedal

\* Battery SOC

\* Motor temperature

\* Ultrasonic sensor measurements



\### VSPE



\*\*Virtual Serial Ports Emulator (VSPE)\*\* is used to create virtual serial ports that allow the PICSimLab simulation to communicate with the Python dashboard.



The communication path is:



```text

PICSimLab

&#x20;   │

&#x20;   │ Virtual Serial Port

&#x20;   ▼

&#x20;  VSPE

&#x20;   │

&#x20;   │ Virtual Serial Port

&#x20;   ▼

Python Dashboard

```



\## Software Architecture



The STM32 firmware is divided into multiple functional modules.



\### EV Control



`ev\_control.c`



Responsible for:



\* Accelerator and brake processing

\* Drive-mode selection

\* Motor torque calculation

\* Regenerative braking

\* Speed modelling

\* Power calculation

\* SOC estimation

\* Range estimation

\* Motor thermal modelling



\### ADAS



`adas.c`



Implements:



\* Forward Collision Warning

\* Time-to-Collision estimation

\* Blind Spot Detection

\* Warning thresholds

\* Critical warning conditions



\### Ultrasonic Sensors



`ultrasonic.c`



Handles ultrasonic sensor timing and distance measurement used by the ADAS functions.



\### Fault Management



`fault.c`



Handles system fault detection and transitions into appropriate vehicle safety states.



\### UART Communication



`uart\_shell.c`



Handles serial communication between the simulated STM32 system and the Python dashboard.



\## Python Dashboard



The dashboard is located at:



```text

ev\_python/ev\_dash.py

```



The Python application receives the simulated vehicle data through the virtual serial connection created using VSPE and presents the information through a real-time dashboard.



\## Project Structure



```text

EV-ADAS-System/

│

├── ev\_dash/

│   ├── Core/

│   │   ├── Inc/

│   │   └── Src/

│   │       ├── adas.c

│   │       ├── ev\_control.c

│   │       ├── fault.c

│   │       ├── main.c

│   │       ├── uart\_shell.c

│   │       └── ultrasonic.c

│   │

│   ├── Drivers/

│   │   ├── CMSIS/

│   │   └── STM32F1xx\_HAL\_Driver/

│   │

│   ├── Startup/

│   ├── ev\_dash.ioc

│   └── STM32F103C8TX\_FLASH.ld

│

├── ev\_python/

│   └── ev\_dash.py

│

├── .gitignore

└── README.md

```



\## Tools \& Technologies



\### Embedded Development



\* STM32F103C8T6

\* STM32CubeIDE

\* STM32CubeMX

\* Embedded C

\* STM32 HAL

\* ADC

\* UART

\* Timers



\### Simulation \& Communication



\* PICSimLab

\* VSPE (Virtual Serial Ports Emulator)



\### Dashboard



\* Python

\* Serial communication

\* Real-time data visualization



\## Running the Simulation



\### 1. STM32 Firmware



Open the STM32 project using \*\*STM32CubeIDE\*\*.



Open:



```text

ev\_dash/ev\_dash.ioc

```



Build the project and generate the required firmware output for use with the simulation environment.



\### 2. PICSimLab



Open the corresponding simulation setup in \*\*PICSimLab\*\* and load the STM32 firmware into the simulated microcontroller environment.



Configure the required simulated inputs and sensors.



\### 3. VSPE



Create a pair of interconnected virtual COM ports using \*\*VSPE\*\*.



One virtual port is connected to the PICSimLab serial interface and the other is used by the Python dashboard.



\### 4. Python Dashboard



Navigate to:



```text

ev\_python/

```



and run:



```bash

python ev\_dash.py

```



Configure the Python dashboard to use the appropriate virtual COM port created by VSPE.



Once connected, the dashboard receives and displays the data generated by the simulated STM32 system.



\## Communication Flow



```text

Simulated Sensors

&#x20;      │

&#x20;      ▼

PICSimLab

&#x20;      │

&#x20;      ▼

STM32F103C8T6 Firmware

&#x20;      │

&#x20;      │ UART

&#x20;      ▼

&#x20;    VSPE

&#x20;      │

&#x20;      │ Virtual COM

&#x20;      ▼

Python Dashboard

```



\## Project Goals



The project was developed to explore the integration of:



\* Embedded systems

\* EV control algorithms

\* ADAS logic

\* Sensor interfacing

\* UART communication

\* Embedded simulation

\* Real-time monitoring

\* PC-based visualization



The simulation approach allows the complete control and ADAS system to be developed and tested without requiring physical automotive hardware.



\## Future Scope



Potential improvements include:



\* CAN bus simulation and integration

\* Real motor controller integration

\* Physical sensor integration

\* GPS integration

\* Camera-based ADAS

\* Advanced object detection

\* Data logging and trip analysis

\* Hardware-in-the-loop testing

\* Integration with a physical EV platform



\## Author



\*\*Pranav Dhamodharan\*\*



Electronics and Communication Engineering

SSN College of Engineering



