# VSDBabySoC Project

## Overview
The **VSDBabySoC** is a simple SoC (System-on-Chip) design incorporating a RISC-V processor (`rvmyth`), a PLL (Phase-Locked Loop) module (`pll`), and a DAC (Digital-to-Analog Converter) module (`dac`). This project demonstrates integration of these IP cores and aims to simulate and verify the design behavior using pre-synthesis and post-synthesis simulations.

## Project Structure
- `src/include/` - Contains header files (`*.vh`) with necessary macros or parameter definitions.
- `src/module/` - Contains Verilog files for each module in the SoC design.
- `output/` - Directory where compiled outputs and simulation files will be generated.

## Requirements
Ensure you have **Icarus Verilog** installed for compilation and **GTKWave** for viewing waveform files. This project assumes a Unix-like environment (macOS/Linux).

## Step-by-Step Guide

### 1. Setup and Prepare Project Directory
   Clone or set up the directory structure as follows:
   ```plaintext
   VSDBabySoC/
   ├── src/
   │   ├── include/
   │   │   ├── sandpiper.vh
   │   │   └── other header files...
   │   ├── module/
   │   │   ├── vsdbabysoc.v      # Top-level module integrating all components
   │   │   ├── rvmyth.v          # RISC-V core module
   │   │   ├── avsdpll.v         # PLL module
   │   │   ├── avsddac.v         # DAC module
   │   │   └── testbench.v       # Testbench for simulation
   └── output/
       └── compiled_tlv/         # Holds compiled intermediate files if needed
