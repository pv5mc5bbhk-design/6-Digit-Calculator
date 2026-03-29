# FSM-Based 6-Digit Calculator (Logisim)

## Overview
This project implements a 6-digit calculator in Logisim with support for sequential inputs, operator precedence, and overflow detection.

Unlike a simple calculator, this design models the problem as a **Finite State Machine (FSM) + datapath system**, similar to a basic processor architecture.

---

## Problem Definition
Design a calculator that:
- Accepts sequential button inputs
- Supports +, −, × operations
- Handles operator precedence (× before + / −)
- Displays results in real time
- Detects overflow conditions

### Constraints
- No built-in multiplier or subtractor
- No binary-to-BCD converter
- All arithmetic circuits implemented manually

---

## System Architecture

The system is divided into four main components:

### 1. Control Unit (FSM)
- 14 states
- 4-layer state hierarchy
- Handles:
  - Input sequencing
  - Operator switching
  - Precedence control

### 2. Datapath
- Custom adder / subtractor
- Multiplication logic (sequential or combinational)
- Registers for operand storage

### 3. Input Interface
- Buttons:
  - `number`, `+`, `-`, `×`, `=`, `reset`
- Converts user input into control signals

### 4. Display Unit
- 6-digit seven-segment display
- Manual binary-to-display conversion

---

## Key Design Insight

Operator precedence is implemented using **state hierarchy**, not immediate evaluation.

- Addition/Subtraction → computed immediately  
- Multiplication → deferred until next operand  

This requires additional FSM layers to correctly model expressions like:
3 + 2 × 5 = 13


---

## FSM Design

- Total states: 14  
- Structured into 4 layers:
  - Input state (A)
  - Operator state (A+, A-, Ax)
  - Operand state (A+N, A-N, AxN)
  - Precedence handling state (A+Nx, A-Nx, etc.)

state diagram :

![FSM Diagram](docs/state_diagram.png)

---

## Features

- Sequential operations (e.g., `2 + 3 + 5`)
- Operator switching during input
- Multiplication precedence handling
- Backspace support (B key)
- Clear/reset functionality
- Overflow detection with error signal
- Continuous calculation after `=`

---

## Example Test Cases

| Input          | Output      |
|----------------|-------------|
| 2 + 3          | 5           |
| 8 − 20         | -12 / Error |
| 2 × 3 × 5      | 30          |
| 3 + 2 × 5      | 13          |
| 3 × = × =      | 81          |      

---

## Implementation Details

- Each state is stored using D Flip-Flops
- One-hot encoding for FSM states
- Combinational logic determines next-state transitions
- Self-holding logic prevents unintended state changes

---

## Project Structure


.
├── README.md
├── docs/
│ ├── state_diagram.png
│ └── architecture.png
├── circuit/
│ └── calculator.circ


---

## Key Takeaways

- Modeled a calculator as a **control + datapath system**
- Implemented operator precedence using FSM abstraction
- Designed arithmetic circuits under hardware constraints
- Built a complete digital system from input to display

---
