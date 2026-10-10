# XiangShan Verification Kit

**A reproducible and extensible verification toolkit for the OpenXiangShan RISC-V processor.**

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](LICENSE)
![Project Status: Early Development](https://img.shields.io/badge/status-early%20development-orange)

## Overview

`xiangshan-verification-kit` is an independent engineering project that aims to build a reproducible and extensible verification workflow around [OpenXiangShan](https://github.com/OpenXiangShan/XiangShan), an open-source, high-performance RISC-V processor.

The project focuses on the infrastructure and workflows needed to configure, execute, reproduce, and analyze CPU verification experiments. It is intended to evolve from basic development-environment setup into a broader CPU verification portfolio covering test automation, randomized testing, multicore scenarios, and power-management-related verification.

Where practical, the project will keep its verification infrastructure separate from the upstream XiangShan RTL, using external scripts, test programs, configuration files, and analysis tools.

**Current stage:** Early development. The initial priority is to establish a maintainable repository structure and a reproducible development workflow.

## Goals

The long-term goals of this project are to:

- Establish a reproducible development and verification environment for XiangShan.
- Automate test configuration, execution, logging, and result collection.
- Explore integration with RISC-V test-generation tools, including Force-RISCV.
- Develop directed and randomized verification scenarios.
- Investigate multicore concurrency, atomic operations, and memory-system behavior.
- Explore low-power state transitions and related stress-testing scenarios where the platform supports them.
- Build a reusable workflow that makes verification experiments easier to reproduce and debug.

These are development goals, not claims that all capabilities are already implemented.

## Verification Scope

The project will expand incrementally across the following areas.

### 1. Environment Setup and Reproducibility

**Status: In Progress**

Planned work includes:

- Documenting required tools, dependencies, and supported environments.
- Automating environment checks and setup where practical.
- Recording tool versions and relevant configuration parameters.
- Providing repeatable commands for development and verification tasks.
- Supporting resource-conscious workflows in local and cloud development environments.

The initial development environment uses Linux and the official [XiangShan environment scripts](https://github.com/OpenXiangShan/xs-env) as a reference.

### 2. Test Execution and Automation

**Status: Planned**

Planned work includes:

- Creating a consistent interface for launching verification jobs.
- Organizing test inputs, configurations, logs, and results.
- Recording execution status and failure information.
- Supporting reproducible test runs through explicit configuration and random seeds.
- Establishing a foundation for automated regression testing.

### 3. RISC-V Test Generation

**Status: Planned**

The project intends to explore integration with [Force-RISCV](https://github.com), subject to confirming the appropriate upstream repository, supported interfaces, and integration requirements.

Potential tasks include:

- Automating test generation and execution.
- Managing generated test programs and associated metadata.
- Connecting generated tests to the selected execution or simulation flow.
- Collecting results and preserving information needed to reproduce failures.

Force-RISCV-5 integration is a future milestone, not an existing capability of this repository.

### 4. CPU Functional and System-Level Verification

**Status: Planned**

This area will explore verification workflows for processor functionality and system-level behavior.

Potential topics include:

- Directed tests for selected processor behaviors.
- Randomized instruction and workload testing.
- Test execution across different configurations.
- Failure classification and reproducibility.
- Automated result checking and regression tracking.

The supported test types and execution methods will be documented as they are implemented and validated.

### 5. Multicore and Memory-System Verification

**Status: Planned**

Potential areas of investigation include:

- Concurrent memory accesses from multiple cores.
- Atomic operations and synchronization primitives.
- Cache-coherence behavior and memory consistency.
- Randomized concurrent workloads.
- Stress testing and reproducible failure analysis.

The initial focus will be on constructing small, understandable experiments before expanding to more complex multicore scenarios.

### 6. Low-Power and State-Transition Verification

**Status: Planned**

A longer-term direction is to explore verification scenarios involving power-management behavior.

Potential topics include:

- Repeated power-state transitions and recovery.
- Interactions between state transitions and concurrent workloads.
- Randomized transition sequences.
- Detection and reproduction of failures around transitions.

The implementation will depend on the capabilities exposed by the selected XiangShan configuration and its simulation, emulation, or hardware environment. The project will distinguish simulated state transitions from actual hardware power cycling.

## Development Roadmap

| Phase | Milestone | Status |
|---|---|---|
| 1 | Establish repository structure and development environment | In Progress |
| 2 | Add environment checks and reproducible setup instructions | In Progress |
| 3 | Implement basic test execution and result collection | Planned |
| 4 | Explore Force-RISCV-5 integration | Planned |
| 5 | Add directed and randomized verification experiments | Planned |
| 6 | Explore multicore and memory-system scenarios | Planned |
| 7 | Investigate low-power and state-transition verification | Planned |

The roadmap is iterative. Each milestone should produce a concrete artifact, such as a script, test case, configuration, document, or reproducible experiment.

## Repository Structure

The repository is expected to evolve toward the following structure:

```text
xiangshan-verification-kit/
├── docs/          # Design notes and verification documentation
├── scripts/       # Environment checks and automation scripts
├── tests/         # Test programs and verification cases
├── configs/       # Test and experiment configurations
├── results/       # Local execution results (not committed by default)
├── README.md
└── LICENSE
```

This is a proposed structure. Directories and components will be added as the corresponding functionality is implemented.

## Getting Started

**Status: Initial environment setup**

The development workflow is being established incrementally. A fully validated, end-to-end verification flow is not yet available.

### Prerequisites

The initial development environment is based on Linux. Exact tool requirements will be documented alongside the scripts and workflows that depend on them.

Depending on the selected XiangShan workflow, development may require tools such as:

- Git
- A supported JDK
- GCC and C++ build tools
- RISC-V cross-compilation tools
- Verilator or other simulation-related tools
- Python and required packages

Refer to the official XiangShan resources for upstream setup details:

- [XiangShan repository](https://github.com/OpenXiangShan/XiangShan)
- [XiangShan environment scripts](https://github.com/OpenXiangShan/xs-env)
- [XiangShan documentation](https://docs.xiangshan.cc/)

Installation commands and example verification runs will be added after they have been tested in the target environment.

## Design Principles

- **Reproducibility:** Record inputs, configurations, tool versions, and execution commands.
- **Automation:** Reduce repetitive manual work in test execution and result analysis.
- **Modularity:** Keep verification infrastructure separate from upstream RTL where practical.
- **Incremental development:** Validate small workflows before scaling to resource-intensive tasks.
- **Debuggability:** Preserve useful logs and metadata to support failure investigation.
- **Resource awareness:** Design workflows that can be developed on modest machines and scaled to more capable environments when needed.
- **Transparent status reporting:** Clearly distinguish implemented features, ongoing work, and future plans.

## Relationship with Upstream XiangShan

This project builds on the open-source XiangShan ecosystem but is developed independently.

The preferred approach is to use external verification infrastructure, test programs, scripts, and configuration files wherever practical, minimizing changes to upstream RTL.

RTL modifications may be considered when a specific verification experiment requires them. Any such modifications should be documented separately, including their purpose and relationship to the upstream project.

This repository is not an official XiangShan project unless explicitly stated otherwise.

## Contributing

Suggestions, issues, and contributions are welcome.

For proposed changes, please include relevant context, configuration details, execution steps, and validation results where available. Reproducible examples and clearly documented limitations are especially useful.

## License

This repository is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.

OpenXiangShan and other third-party components remain subject to their respective licenses and terms. Their inclusion or use does not imply endorsement of this independent project.