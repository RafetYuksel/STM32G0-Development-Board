# STM32G0-Development-Board

A custom 4-layer development board based on the **STM32G0B1RET6** microcontroller, designed from schematic through PCB layout with a focus on practical hardware design, power management, USB, industrial communication interfaces, debugging, and PCB design practices.

---

## Overview

This project is a custom STM32G0 development board designed and developed from the ground up.

The board provides a general-purpose hardware platform for embedded development and includes USB connectivity, CAN, RS485, SWD debugging, UART, I2C and SPI interfaces.

The design process includes:

- System architecture
- Schematic design
- Component selection
- Power architecture
- PCB layout
- 4-layer PCB stack-up
- Ground-plane design
- USB differential-pair routing
- Communication interfaces
- Design Rule Check (DRC) 
- PCB manufacturing
- Hardware bring-up

---

## Key Features

| Feature | Description |
|---|---|
| MCU | STM32G0B1RET6 |
| PCB | 4-layer |
| USB | USB Type-C |
| Debug | SWD |
| CAN | FDCAN1 |
| RS485 | MAX3485 |
| UART | USART2 |
| I2C | Header |
| SPI | Header |
| Logic Supply | 3.3 V |
| USB Supply | 5 V |
| External Input | Supported |
| Protection | Input protection and USB ESD protection |
| Status | LEDs and user button |

---

## System Architecture

```text
                         ┌─────────────────────┐
                         │      USB Type-C     │
                         │    Power + USB      │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   Power Management  │
                         │ Protection + DC/DC  │
                         └──────────┬──────────┘
                                    │      
                              5 V / 3.3 V
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    STM32G0B1RET6    │
                         │        MCU          │
                         └──────┬──┬──┬──┬────┘
                                │  │  │  │
                    ┌───────────┘  │  │  └───────────┐
                    │              │  │              │
                    ▼              ▼  ▼              ▼
                  USB             CAN RS485       SWD
                    │              │  │              │
                    ▼              ▼  ▼              ▼
                USB ESD         Transceivers     Debugger
                Protection

```
---

## Hardware Design

### MCU
* **Main Controller:** STM32G0B1RET6
* Provides processing, communication, and peripheral interfaces required by the board.
* Includes local decoupling capacitors and dedicated filtering for the MCU supply.
* MCU analog supply is additionally filtered from the main 3.3 V rail.

### Power Management
Supports USB and external power input.

**Power Architecture:**
USB-C / External Input
          │
          ▼
   Input Protection
          │
          ▼
       SYS_5V
          │
          ▼
        3.3 V
          │
          ▼
    STM32G0 + Logic

### USB
USB connectivity is provided through a USB Type-C connector with data lines routed as a differential pair on the PCB.
* USB Type-C connector
* USB VBUS & CC resistors
* USB ESD protection
* USB differential data lines

### CAN
Connected to the STM32G0 FDCAN peripheral. The termination network allows configuration based on its position in the CAN bus.
* CANH / CANL lines
* CAN transceiver & connector
* Selectable termination (Jumper-selectable)

### RS485
Uses an MAX3485 transceiver for RS485 communication.
* MCU UART connection
* Driver Enable control
* RS485 A/B lines
* RS485 termination (Jumper-selectable)
* External connector

### Debug Interface
Provides Serial Wire Debug (SWD) interface for programming and debugging via an external ST-LINK debugger. Access provided to:
* SWDIO & SWCLK
* 3.3 V & GND
* MCU reset

### Peripheral Interfaces
Exposes several MCU peripherals through external headers to act as a general-purpose embedded development platform:
* UART, I2C, SPI
* CAN, RS485
* GPIO

---

## PCB Design

### Stack-up (4-Layer)
| Layer | Name | Description |
| :--- | :--- | :--- |
| **Layer 1** | TOP | Components and signal routing |
| **Layer 2** | GND | Ground plane |
| **Layer 3** | INNER SIGNAL | Signal routing |
| **Layer 4** | BOTTOM | Signal routing |

* A dedicated internal ground layer (Layer 2) provides continuous ground coverage, low-impedance return paths, and improved return-current dynamics.
* Ground stitching vias are placed throughout to enhance connections between ground regions.

### PCB Layout Considerations
* MCU decoupling capacitor placement & short USB signal paths
* Power-rail routing & ground-plane continuity
* USB differential-pair routing
* Communication-interface routing
* Ground stitching & signal/power routing
* **DRC:** Completed using CircuitMaker Design Rule Check.

---

## Design Decisions

* **4-Layer PCB:** Selected to provide additional routing space, low-impedance return paths, and a dedicated internal ground plane.
* **Ground Plane:** Dedicated GND plane on Layer 2 with stitching vias added where appropriate to improve continuity between PCB regions.
* **USB Differential Pair:** D+ and D− signals routed as a differential pair in a compact layout around the connector, ESD protection, and MCU.
* **Selectable CAN Termination:** Jumper-selectable termination resistor allows use at either end of a CAN bus or without local termination.
* **Selectable RS485 Termination:** Jumper-selectable termination network to enable or disable based on position in the network.

---

## Manufacturing & Status

### Manufacturing Workflow
Schematic -> PCB Layout -> DRC -> PCB Manufacturing -> Bare PCB Received -> Component Assembly -> Hardware Bring-up -> Firmware Validation

### Project Status
* **Hardware Design:** Complete
* **PCB Manufacturing:** Complete
* **Bare PCB:** Received
* **Component Assembly:** Pending
* **Hardware Bring-up:** Pending
* **Firmware Validation:** Pending

---

## Firmware & Bring-up Plan

Firmware development will be performed using **STM32CubeIDE**.

Planned firmware validation includes:
* GPIO, UART, USB, CAN, RS485
* ADC, Timers, PWM
* SWD debugging

### Hardware Bring-up Sequence
1. Visual inspection
2. Power-input verification
3. 5 V rail verification
4. 3.3 V rail verification
5. MCU supply verification
6. SWD connection
7. MCU programming
8. Peripheral tests (GPIO -> UART -> USB -> CAN -> RS485)

### Validation Matrix
| Function / Test | Status |
| :--- | :--- |
| Visual inspection | Pending |
| Power input | Pending |
| SYS_5V | Pending |
| 3.3 V | Pending |
| MCU power | Pending |
| SWD | Pending |
| GPIO | Pending |
| UART | Pending |
| USB | Pending |
| CAN | Pending |
| RS485 | Pending |

---

## Repository Structure

```text
STM32G0-Development-Board/
├── Hardware/
│   ├── Schematic/
│   ├── PCB/
│   ├── BOM/
│   └── 3D/
├── Firmware/
├── Documentation/
├── Images/
└── README.md
