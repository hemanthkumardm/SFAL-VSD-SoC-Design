# OpenLANE EDA Tool: Simplified Overview

Welcome to the OpenLANE EDA Tool repository. This guide provides a basic understanding of the open-source EDA, the RTL to GDSII flow, and the key components used in digital ASIC design with the Sky130 PDK.

---

<details>
<summary>### Day 13 - Inception of Open-Source EDA, OpenLANE, and Sky130 PDK</summary>

#### How to Talk to Computers
- **QFN-48 Package**: Outer part of a chip for connecting to the outside world.
- **Chip**: Contains pads and the core (where digital logic resides).
- **IP (Intellectual Property)**: Pre-designed, reusable circuit blocks.
  - **Soft IP**: Synthesizable HDL code.
  - **Hard IP**: Fixed, pre-verified layout designs.
  - **Firm IP**: A mix of soft and hard IP.

#### Introduction to RISC-V
- A processor architecture implemented using HDLs like Verilog.
- Programs are compiled from C to assembly, then to binary for execution.

#### From Software Applications to Hardware
- Applications (e.g., Microsoft Excel) run through system software:
  - **Compiler**: Converts high-level code to hardware instructions.
  - **Assembler**: Converts instructions to machine-readable binary.

</details>

<details>
<summary>### SoC Design and OpenLANE</summary>

#### Components of Digital ASIC Design
- **EDA Tools**: Open-source tools like OpenLANE.
- **PDK (Process Design Kit)**: Provides rules and resources for designing chips.

#### PDK Key Components
- **Technology Files**: Define process parameters.
- **Design Rules**: Guidelines for manufacturability.
- **Device Models**: SPICE models for simulation.
- **Standard Cell Libraries**: Basic building blocks.
- **IO Libraries**: For communication with the external world.
- **Memory Compilers**: Tools for creating memory blocks.

#### Simplified RTL to GDSII Flow
1. **Synthesis**: Converts RTL code to a gate-level netlist.
2. **Floorplanning**: Organizes the chip layout.
3. **Placement**: Positions standard cells and macros.
   - **Global Placement**: Approximate locations.
   - **Detailed Placement**: Final legal positions.
4. **Clock Tree Synthesis (CTS)**: Designs the clock distribution network.
5. **Routing**: Connects components with metal interconnections.
6. **Sign-Off**: Final verification before fabrication.

</details>

<details>
<summary>### Get Familiar with Open-Source EDA</summary>

#### OpenLANE Directory Structure
- Explore and understand the folder structure.

#### Design Preparation
- Prepare the design files for synthesis.

#### Synthesis
- Analyze the synthesis results and characterize the output.

#### Tools in OpenLANE
- **Yosys**: Converts RTL to a gate-level netlist.
- **OpenROAD**: Physical design tools (placement, CTS, routing).
- **Magic**: Layout and physical verification.
- **OpenSTA**: Timing analysis.

</details>

---
