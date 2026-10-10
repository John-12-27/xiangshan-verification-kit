# xiangshan-verification-kit

An industrial-grade verification platform focusing on microarchitectural corner cases, cluster-level features, and advanced constraint-random stimulus generation for the open-source **XiangShan Out-of-Order RISC-V Processor**.

[![Development Environment: Codespaces](https://shields.io)](https://github.com)
[![Stimulus: FORCE-RISCV](https://shields.io)](https://github.com)
[![Framework: UnityChip Python](https://shields.io)](https://github.com)

---

## 🎯 Project Overview & Objective

The goal of this project is to build a robust, scalable, and automated functional verification environment for high-performance Out-of-Order (OoO) processor cores. It maps complex, industrial-scale validation methodologies onto the open-source **XiangShan (Kunminghu Architecture)** ecosystem using modern software-driven verification patterns.

This kit acts as an engineering showcase focusing on:
1. **Cluster-level Interconnect & Interrupt Protocols**: Bridging AMBA CHI / TileLink memory consistency and advanced nested interrupt routing (PLIC/AIA).
2. **Low-Power Control Plane Verification**: Stressing microarchitectural state transitions during dynamic clock gating and power down modes.
3. **Agile Co-Simulation Infrastructure**: Orchestrating instruction stream generators with C++ Verilator models and Python-based unit testing engines.

---

## 🏗️ System Architecture & Verification Flow

The execution workflow bypasses hardware prototyping bottlenecks by relying entirely on a high-throughput, software-driven co-simulation and differential testing (Difftest) loop:

```text
       +---------------------------------------------+

       |   FORCE-RISCV Constraint-Random Templates   |
       +---------------------------------------------+
                              |
                              v  (Generates .elf/.bin)
         +--------------------+--------------------+

         |                                         |
         v                                         v
+-----------------------+               +-----------------------+

|  XiangShan RTL Core   |               |   NEMU / QEMU ISA     |
| (Verilator Emulation) |               |     Golden Model      |
+-----------------------+               +-----------------------+

         |                                         |
         v (Commit State Trace)                    v (Architectural State)
         +--------------------+--------------------+
                              |
                              v
                +---------------------------+

                |  Difftest Monitor Engine  | ---> [Pass / Fail Assertions]
                +---------------------------+
```

---

## 📋 Verification Plan & Test Matrix

| Feature Under Test | Verification Level | Strategy | Stimulus Mechanism | Key Exit Criteria / Metrics |
| :--- | :--- | :--- | :--- | :--- |
| **AIA / PLIC Interrupts** | TOP / Cluster | Validate interrupt prioritization, nesting, and Core-to-Core Inter-Processor Interrupts (IPI) under intensive back-to-back hazard conditions. | `FORCE-RISCV` Python multi-privileged templates with asynchronous interrupt injection. | Zero-lost interrupts, precise alignment with ISA reference state transitions. |
| **Dynamic Clock Gating** | UT / Sub-module | Verify power-state machine transitions when the core enters/exits `WFI` (Wait For Interrupt) sleep modes under multi-level pipeline stalls. | `UnityChip` Python testbenches forcing sudden execution pauses and flushes. | Structural state-coverage convergence; no hang/deadlock on wakeup bounds. |
| **Memory Consistency** | INTEGRATION | Stress the Load/Store unit, Store Buffers, and TileLink cache eviction pipelines against out-of-order memory dependency violations. | Multi-threaded litmus memory-ordering test sequences. | TSO/Weak Memory Model memory sequence assertion compliance. |

---

## 📁 Repository Directory Structure

*   `config/` — Configuration sheets for `FORCE-RISCV` and execution knobs for the XiangShan `emu` target.
*   `env/` — Sub-module unit testbenches (`UnityChip` integrations) and customized Verification IPs (VIPs).
*   `generators/force-templates/` — **Core Asset**. Highly constrained Python generation files dictating instruction stream variables for complex microarchitectural corner cases.
*   `scripts/` — Automated execution infrastructure, log parsers, and regression triage engines.
*   `tests/` — Self-contained binary registry for specific deterministic architectural regression test cases.

---

## 🚀 Quick Start in GitHub Codespaces

This repository includes a native `.devcontainer` configuration that fully automates dependency resolution upon launching a Codespace instance.

### 1. Launch Environment
Simply click the green **Code** button on this repository, select the **Codespaces** tab, and click **Create codespace on main**. 

The system automatically initializes an Ubuntu workspace preconfigured with:
*   `Verilator` (High-performance C++ RTL Simulator)
*   `RISC-V 64-bit GNU Toolchain` (Cross-compilers)
*   `Device Tree Compiler (DTC)` & `Python3/Pip` testing packages

### 2. Run a Constraint-Random Verification Scenario
To generate a complex nested interrupt instruction sequence using FORCE-RISCV and simulate it on top of the XiangShan execution target, run:

```bash
# Execute the automated verification runner
python3 ./scripts/run_single.py --template interrupt_nested --trace
```

### 3. Debugging Failures
When an architectural state mismatch is captured by the Difftest engine, the execution script logs the violation context. You can export and review microarchitectural signals using GTKWave:

```bash
# Open generated trace file to track pipeline state changes
gtkwave output/waves/interrupt_nested_fail.vcd
```

---

## 💡 Code Agent & Automation Integration

This platform is deliberately designed to seamlessly integrate with modern AI Software Agents (e.g., Cline, Continue, Copilot). Testbenches follow standardized modular definitions, allowing Agents to safely execute regression matrices, perform automatic log parsing on simulation drops, and dynamically write focused constraint overrides within the `generators/` directory to maximize microarchitectural state toggle coverage.
