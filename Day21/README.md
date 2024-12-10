# README.md

## Overview

**Physical Design** is the process of converting a gate-level netlist into a physical layout suitable for silicon manufacturing. It involves creating metal shapes and sizes that define the chip's structure. The process is iterative, focusing on optimizing performance, area, and power.

## Key Stages of Physical Design

### 1. Floorplanning

- Divides the design into smaller subsystems based on system architecture.
- Determines layout aspect ratio and area.
- Places standard cells, I/Os, and macros.
- Includes power planning for a robust power distribution network.

> *A good floorplan ensures design quality and simplifies subsequent steps.*

<img width="371" alt="Screenshot 2024-12-10 at 10 47 44 AM" src="https://github.com/user-attachments/assets/f5131db2-6dca-4979-88fb-ed5a4cdae0d7">


### 2. Logic Placement

- Places all standard cells in legal locations.
- Optimizes placement to reduce congestion and improve timing.
- Uses timing-driven placement algorithms for better performance.

### 3. Clock Tree Synthesis (CTS)

- Builds a clock network using buffers and inverters.
- Minimizes clock skew to meet timing requirements.
- Ensures a high-quality clock distribution for the design.

### 4. Routing

- Connects all components using metal layers.
- Optimizes routes to meet timing and signal integrity requirements.
- Finalizes connections between standard cells, macros, and I/Os.

### 5. Timing Analysis & Signoff

- Analyzes design timing paths using static timing analysis (STA).
- Identifies and resolves timing violations.
- Verifies design performance before final signoff.

### 6. Physical Verification & Signoff

- Ensures the layout meets fabrication rules and is manufacturable.
- Includes checks like:
  - Design Rule Check (DRC)
  - Layout vs. Schematic (LVS)
  - Electrical Rule Check (ERC)
  - Electromigration (EM) analysis
- Prepares layout for tapeout in GDSII/OASIS format.

## Floorplanning Details

### What is Floorplanning?

- Floorplanning arranges blocks and macros in the chip or core area.
- Objectives:
  - Minimize area, timing, and power consumption.
  - Ensure easy routing and reliability.

### Inputs for Floorplanning

- **Gate-level Netlist** (`.v`)
- **Libraries** (`.lefs`, `.libs`, etc.)
- **Constraints** (`.sdc`)
- **RC Tech File** (`TLU+`)
- **Technology File** (`.tf`)
- Design partitioning and parameters.

### Outputs of Floorplanning

- **Die/Core Area**: Physical dimensions of the design.
- **I/O Pad Information**: Placement of I/O pins.
- **Macro Placement**: Location of macros.
- **Standard Cell Areas**: Rows for standard cells.
- **Power Grid Design**: Power distribution plan.
- **Blockages**: Restricted areas for cell placement.

<img width="370" alt="Screenshot 2024-12-10 at 10 48 06 AM" src="https://github.com/user-attachments/assets/2ddb59e4-862d-4bc4-807c-79dadc153f92">


### Floorplan Techniques

<img width="617" alt="Screenshot 2024-12-10 at 10 49 47 AM" src="https://github.com/user-attachments/assets/64eb1248-192a-4d36-8935-bb33520c6b7f">


1. **Abutted**: Blocks placed without gaps (channel-less).
2. **Non-Abutted**: Gaps between blocks for routing.
3. **Mixed**: Combination of abutted and non-abutted techniques.

### Floorplan Control Parameters

- **Aspect Ratio**: Height-to-width ratio of the chip.
- **Core Utilization**: Percentage of the core area used.
- **Blockages**: Regions to prevent congestion.

### Steps in Floorplanning

1. Define chip width and height.
2. Place I/O pins around the boundary.
3. Plan power distribution.
4. Place macros based on logical connections.
5. Create standard cell rows.
6. Define blockages for better routing.

<img width="255" alt="Screenshot 2024-12-10 at 10 48 32 AM" src="https://github.com/user-attachments/assets/379a4a04-caad-474f-9933-c1b06cdc1279">

## Power Planning

### What is Power Planning?

- Power planning creates a network to supply stable power to all components.
- Objectives:
  - Maintain stable voltage across the chip.
  - Minimize IR drop and avoid electromigration.
  - Optimize power mesh for minimal area usage.

### Power Distribution Hierarchy

1. **Power Pads**: Bring power from outside the chip.
2. **Power Rings**: Surround the core area.
3. **Power Stripes**: Distribute power across the core.
4. **Power Rails**: Connect stripes to standard cells.

### Steps in Power Planning

1. Calculate the required number of power pins.
2. Create power rings, stripes, and rails.
3. Analyze and optimize for IR drop.
4. Use top metal layers for the power mesh to reduce resistance.

<img width="626" alt="Screenshot 2024-12-10 at 10 50 07 AM" src="https://github.com/user-attachments/assets/398adf96-1fef-44f7-89ec-eb6bc047c11e">

---

## Labs: Physical Design Collateral Setup

### Downloading Physical Design Collaterals

1. **Download Technology Files and Standard Cells**
   ```bash
   git clone https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd.git
   ```
    . Includes .techlef files for Skywater 130nm PDK.
    . Contains .lef files for standard cells.

   <img width="730" alt="Screenshot 2024-12-10 at 11 04 01 AM" src="https://github.com/user-attachments/assets/a0ad6faa-257b-4217-b42d-81807eb081a3">


3. **Download Technology and RC Tech Files**
   ```bash
   git clone https://github.com/bharath19-gs/synopsys_ICC2flow_130nm.git
   ```
    . Includes .tf files (Technology Files) for Skywater 130nm PDK.
    . Contains .itf files (Interconnect Technology Format) for parasitic extraction.

   <img width="674" alt="Screenshot 2024-12-10 at 11 05 03 AM" src="https://github.com/user-attachments/assets/b6ebeab8-754d-4481-8fb1-4f0d03ef5473">

3. **Download ICC2 Workshop Collaterals**
   ```bash
   git clone https://github.com/kunalg123/icc2_workshop_collaterals.git
   ```
    . Scripts for setting up and running the Physical Design flow in Synopsys ICC2.
   
   <img width="701" alt="Screenshot 2024-12-10 at 11 06 36 AM" src="https://github.com/user-attachments/assets/bcff4e42-d9f8-464d-a28f-9e112beeb55a">

### ITF Files: Overview and Usage

The Interconnect Technology Format (ITF) file describes process technology and interconnect attributes. Key details include:

  . Conductor Layers: Thickness, minimum width, minimum spacing, and sheet resistance (RPSQ).
  . Dielectric Layers: Thickness and dielectric constant (ER).
  . Via Layers: Resistivity (RHO) and area.

**Purpose:**

  . Enables parasitic resistance and capacitance (RC) modeling.
  . Input for parasitic extraction tools used for timing, signal integrity, power, and reliability analysis.
  . Generates TLU+ files for physical design tools.

**Conversion of ITF to TLUPLUS:**

  **1. Navigate to the directory:**

  `cd synopsys_ICC2flow_130nm/synopsys_skywater_flow_nominal/itf_files/`
  
  <img width="708" alt="Screenshot 2024-12-10 at 11 17 27 AM" src="https://github.com/user-attachments/assets/bae8174b-a8b3-4d30-b81a-aeb0276bae9c">

  **2.	Execute the following command:**

  `grdgenxo -itf2TLUPlus -i skywater130.nominal.itf -o skywater130.nominal.tluplus`

  <img width="868" alt="Screenshot 2024-12-10 at 11 20 34 AM" src="https://github.com/user-attachments/assets/6bc8d17f-1c22-4f5e-b596-123b98cab000">

  **SDC Constraints Used for Synthesis**

  ```tcl
  set target_library /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db
  set link_library {* /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsdpll.db    /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsddac.db}
  set search_path {/home/hemanth/Desktop/VLSI/VSDBabySoc/src/include /home/hemanth/Desktop/VLSI/VSDBabySoc/src/module}
  read_file {sandpiper_gen.vh  sandpiper.vh  sp_default.vh  sp_verilog.vh clk_gate.v rvmyth.v rvmyth_gen.v vsdbabysoc.v} -autoread -top vsdbabysoc
  link
  read_sdc /home/hemanth/Desktop/VLSI/VSDBabySoc/outputs/vsdbabysoc_net.sdc
  compile_ultra
  report_qor > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/qor_post_synth.rpt
  report_area > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/area_post_synth.rpt
  report_power > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/power_post_synth.rpt
  write_file -format verilog -hierarchy -output /home/hemanth/Desktop/VLSI/VSDBabySoc/output/vsdbabysoc_net.v
  write -f ddc -out /home/hemanth/Desktop/VLSI/VSDBabySoc/output/vsdbabysoc.ddc

  start_gui
  ```


  
