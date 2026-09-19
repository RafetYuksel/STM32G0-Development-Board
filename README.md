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
