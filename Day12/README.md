# Post-Synthesis Simulation (Gate Level Simulation) of BabySoC

## Table of Contents
- [Introduction](#introduction)
- [Why Pre-Synthesis and Post-Synthesis?](#why-pre-synthesis-and-post-synthesis)
- [Setting Up the Environment](#setting-up-the-environment)
- [Steps for Conversion of .lib to .db Files](#steps-for-conversion-of-lib-to-db-files)
  - [Converting `avsddac.lib` to `avsddac.db`](#converting-avsddaclib-to-avsddacdb)
  - [Converting `avsdpll.lib` to `avsdpll.db`](#converting-avsdplllib-to-avsdplldb)
  - [Converting `sky130_fd_sc_hd__tt_025C_1v80.lib` to `.db`](#converting-sky130_fd_sc_hd__tt_025c_1v80lib-to-db)
- [Running Synthesis and GLS](#running-synthesis-and-gls)
- [Common Errors and Debugging Tips](#common-errors-and-debugging-tips)

## Introduction

Gate-level simulation (GLS) checks both functionality and timing of the design after synthesis. Unlike pre-synthesis simulation (which only verifies logic without delay), GLS includes gate delays, helping catch timing violations and misuses of operators.

## Why Pre-Synthesis and Post-Synthesis?

1. **Pre-Synthesis Simulation**: 
   - Focuses only on verifying functionality based on the RTL code.
   - Zero-delay environment, with events occurring on the active clock edge.

2. **Post-Synthesis Simulation (GLS)**:
   - Uses the synthesized netlist (gate-level) to simulate both functionality and timing.
   - Identifies timing violations and potential mismatches (e.g., unintended latches).
   - Helps verify dynamic circuit behavior that static methods may miss.

## Setting Up the Environment

1. **Ensure Synopsys Library Compiler (lc_shell) is installed**: Needed for .lib to .db conversions.
2. **Download Required Libraries**: 
   - Use `wget` to download `sky130_fd_sc_hd__tt_025C_1v80.lib` from the [Skywater GitHub repository](https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/tree/master/timing).

## Steps for Conversion of .lib to .db Files

We need `.db` files for `avsddac`, `avsdpll`, and `sky130_fd_sc_hd__tt_025C_1v80` libraries. Follow these steps:

### Converting `avsddac.lib` to `avsddac.db`
`cd Desktop/hemanth/VLSI/VSDBabySOC/src/lib/`
<img width="739" alt="Screenshot 2024-11-08 at 12 12 58 PM" src="https://github.com/user-attachments/assets/6257df5a-5775-45dc-adc9-9d49a949f917">

Launch `lc_shell`
<img width="736" alt="Screenshot 2024-11-08 at 12 13 45 PM" src="https://github.com/user-attachments/assets/1ded9195-26bc-46f6-bab3-b68618b7fde3">

Reading avsddac library `read_lib avsddac.lib`


write_lib avsddac -format db -output avsddac.db
<img width="881" alt="Screenshot 2024-11-08 at 12 24 58 PM" src="https://github.com/user-attachments/assets/3a41681b-6dc7-4764-a3f1-ceedd29608a1">



