# fifo_verilog
# 🧠 Asynchronous FIFO Design in Verilog

A modular and synthesizable implementation of an **Asynchronous FIFO (First-In-First-Out)** in Verilog HDL. This design enables reliable data transfer between two independent clock domains using dual-port memory and proper synchronization mechanisms.

---

## 📌 Project Description

This project demonstrates the architecture and functionality of an asynchronous FIFO buffer with:

- Independent **write (`clkw`)** and **read (`clkr`)** clock domains
- Proper handling of **full** and **empty** conditions
- Use of **pointer synchronization** between domains using **2-flip-flop synchronizers**
- **Dual-port RAM** for non-blocking concurrent read/write operations

---

## 🧩 Module Breakdown

| Module            | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| `topmodule.v`     | Integrates RAM, controllers, and synchronizers to form a complete FIFO      |
| `RAM.v`           | Implements dual-port memory with independent read/write access              |
| `write_controller.v` | Maintains write pointer and generates `full` flag using synced read pointer |
| `read_controller.v`  | Maintains read pointer and generates `empty` flag using synced write pointer |
| `synchronizer.v`  | 2-stage flip-flop synchronizer for safe pointer transfer between domains     |

---

## 📐 Interface Specification

```verilog
module topmodule (
  input         clkw,        // Write domain clock
  input         clkr,        // Read domain clock
  input         resetw,      // Write domain reset
  input         resetr,      // Read domain reset
  input         write,       // Write enable
  input         read,        // Read enable
  input  [31:0] wd,          // Write data
  output [31:0] rd,          // Read data
  output        full,        // FIFO full flag (write side)
  output        empty        // FIFO empty flag (read side)
);
