
# SFAL-VSD-SoC-Design Program - Day 4

This repository contains my progress for Day 4 of the SFAL-VSD-SoC-Design program. The focus of today's tasks includes GLS, blocking vs non-blocking, and synthesis-simulation mismatch.

## Table of Contents
- [Day 4 Overview](#day-4-overview)
- [Tasks](#tasks)
  - [SKY130RTL D4SK1: GLS, Synthesis-Simulation Mismatch, and Blocking/Non-blocking Statements](#sky130rtl-d4sk1-gls-synthesis-simulation-mismatch-and-blockingnon-blocking-statements)
  - [SKY130RTL D4SK2: Labs on GLS and Synthesis-Simulation Mismatch](#sky130rtl-d4sk2-labs-on-gls-and-synthesis-simulation-mismatch)
  - [SKY130RTL D4SK3: Labs on Synth-Sim Mismatch for Blocking Statement](#sky130rtl-d4sk3-labs-on-synth-sim-mismatch-for-blocking-statement)

---

## Day 4 Overview

On Day 4, I explored the following concepts:
- Gate Level Simulation (GLS)
- Synthesis-Simulation mismatch
- Blocking and non-blocking statements in Verilog
- Associated labs and practical tasks

## Tasks

### SKY130RTL D4SK1: GLS, Synthesis-Simulation Mismatch, and Blocking/Non-blocking Statements

<details>
  <summary>SKY130RTL D4SK1 L1: GLS Concepts and Flow Using Iverilog</summary>

  - **Task**: Understand the basic concepts of Gate Level Simulation (GLS) and how it fits into the overall digital design flow.
  - **Objective**: Learn how to use Iverilog to simulate designs at the gate level and understand the purpose of GLS.
  - **Progress**: Documented steps to run GLS using Iverilog and verified outputs.
  
</details>

<details>
  <summary>SKY130RTL D4SK1 L2: Synthesis-Simulation Mismatch</summary>

  - **Task**: Identify common synthesis-simulation mismatches that can occur during the RTL to netlist conversion process.
  - **Objective**: Learn how mismatches happen and how to detect and resolve them.
  - **Progress**: Simulated RTL and synthesized netlist to observe mismatches and documented findings.
  
</details>

<details>
  <summary>SKY130RTL D4SK1 L3: Blocking and Non-blocking Statements in Verilog</summary>

  - **Task**: Explore the differences between blocking and non-blocking assignments in Verilog.
  - **Objective**: Understand when and how to use each type of assignment to avoid synthesis-simulation mismatches.
  - **Progress**: Completed code examples and simulations to demonstrate the use of both types of assignments.
  
</details>

<details>
  <summary>SKY130RTL D4SK1 L4: Caveats with Blocking Statements</summary>

  - **Task**: Learn the pitfalls of using blocking assignments and how they can lead to timing issues in synthesized designs.
  - **Objective**: Become familiar with best practices for avoiding issues caused by blocking statements.
  - **Progress**: Documented scenarios where blocking assignments can cause issues and analyzed example code.
  
</details>

---

### SKY130RTL D4SK2: Labs on GLS and Synthesis-Simulation Mismatch

<details>
  <summary>SKY130RTL D4SK2 L1: Lab GLS Synth Sim Mismatch part 1</summary>

  - **Task**: Run a lab exercise to identify synthesis-simulation mismatches.
  - **Objective**: Execute gate level simulations and analyze mismatches between RTL and netlist simulations.
  - **Progress**: Completed part 1 of the lab and documented the steps and results.
  
</details>

<details>
  <summary>SKY130RTL D4SK2 L2: Lab GLS Synth Sim Mismatch part 2</summary>

  - **Task**: Continue with the second part of the synthesis-simulation mismatch lab.
  - **Objective**: Further explore and resolve mismatches by adjusting RTL code and re-synthesizing.
  - **Progress**: Completed part 2 of the lab, corrected mismatches, and documented the fixes.
  
</details>

---

### SKY130RTL D4SK3: Labs on Synth-Sim Mismatch for Blocking Statement

<details>
  <summary>SKY130RTL D4SK3 L1: Lab Synth Sim Mismatch Blocking Statement part 1</summary>

  - **Task**: Investigate synthesis-simulation mismatches caused by blocking assignments.
  - **Objective**: Identify how incorrect use of blocking statements can lead to mismatches in simulation vs synthesis.
  - **Progress**: Completed the first part of the lab, demonstrating mismatch scenarios with blocking assignments.
  
</details>

<details>
  <summary>SKY130RTL D4SK3 L2: Lab Synth Sim Mismatch Blocking Statement part 2</summary>

  - **Task**: Continue investigating blocking statement mismatches and how to resolve them.
  - **Objective**: Apply fixes to RTL code and re-run simulations to ensure no mismatches occur.
  - **Progress**: Successfully fixed issues and documented results in part 2 of the lab.
  
</details>

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
