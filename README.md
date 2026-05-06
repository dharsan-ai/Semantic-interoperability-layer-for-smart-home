# 🏠 Smart Home Semantic Interoperability Layer

An IoT project that enables seamless communication between heterogeneous smart home devices by implementing a semantic interoperability layer.

## 🎯 Problem Statement

Modern smart homes consist of devices from multiple manufacturers, each using different APIs and communication standards. This leads to poor interoperability and forces users to rely on separate applications for each device.

## 💡 Solution

This project implements a **Semantic Interoperability Layer** that:
- Converts device-specific data into unified JSON format
- Enables cross-platform device communication
- Provides real-time monitoring and control
- Supports multiple device types through a single interface

## 🛠️ Hardware Components

| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino UNO R4 WiFi | 1 | Main controller |
| Ultrasonic Sensor (HC-SR04) | 1 | Distance measurement |
| IR Sensor | 1 | Object detection |
| Servo Motor (SG90) | 1 | Automated control |
| Buzzer | 1 | Alert notification |
| LED (Red/Green) | 2 | Status indication |
| Jumper Wires | Set | Connections |

## 📊 System Architecture
┌─────────────┐
│ A_GREEN │ (5 seconds)
│ A_Red=0 │
│ B_Red=1 │
└──────┬──────┘
│ timer_done
▼
┌─────────────┐
│ A_YELLOW │ (2 seconds)
│ A_Red=0 │
│ B_Red=1 │
└──────┬──────┘
│ timer_done
▼
┌─────────────┐
│ B_GREEN │ (5 seconds)
│ A_Red=1 │
│ B_Red=0 │
└──────┬──────┘
│ timer_done
▼
┌─────────────┐
│ B_YELLOW │ (2 seconds)
│ A_Red=1 │
│ B_Red=0 │
└──────┬──────┘
│ timer_done
└──────────► (back to A_GREEN)

text

## 📊 State Encoding

| State | Binary Code | Duration | A_Green | A_Yellow | A_Red | B_Green | B_Yellow | B_Red |
|-------|-------------|----------|---------|----------|-------|---------|----------|-------|
| A_GREEN | 00 | 5 sec | 1 | 0 | 0 | 0 | 0 | 1 |
| A_YELLOW | 01 | 2 sec | 0 | 1 | 0 | 0 | 0 | 1 |
| B_GREEN | 10 | 5 sec | 0 | 0 | 1 | 1 | 0 | 0 |
| B_YELLOW | 11 | 2 sec | 0 | 0 | 1 | 0 | 1 | 0 |

## ✨ Features

- ✅ Four clearly defined states with deterministic transitions
- ✅ Configurable timing intervals (5s Green, 2s Yellow)
- ✅ Safety-critical design - prevents conflicting green signals
- ✅ Synchronous design with clock-driven state transitions
- ✅ Synchronous reset for reliable initialization
- ✅ FPGA-ready Verilog implementation
- ✅ Complete testbench with waveform validation

## 🔧 Technologies Used

- **Language:** Verilog HDL
- **Simulation:** ModelSim / Vivado
- **Methodology:** ASM (Algorithmic State Machine)
- **State Encoding:** Binary (2 flip-flops)

## 📁 Files

| File | Description |
|------|-------------|
| `traffic_controller.v` | Main Verilog module |
| `testbench.v` | Simulation testbench |
| `waveforms/` | Simulation result images |

## 🚀 How to Run

### Using ModelSim
```bash
vlib work
vlog traffic_controller.v testbench.v
vsim -c testbench
run -all
