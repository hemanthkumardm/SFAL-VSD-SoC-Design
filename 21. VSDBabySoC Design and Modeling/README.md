# VSDBabySoC Design and Modeling

VSDBabySoC is a small yet powerful RISC-V-based SoC designed to integrate three open-source IP cores. This project showcases the modeling, synthesis, and physical design flow of the SoC, leveraging open-source tools and Nangate45nm PDKs.

---

## Table of Contents

- <details>
  <summary>Introduction</summary>

  ### What is VSDBabySoC?
  VSDBabySoC is a compact SoC featuring:
  - **RVMYTH**: A simple RISC-V-based CPU core.
  - **PLL**: An 8x Phase-Locked Loop for stable clock generation.
  - **DAC**: A 10-bit Digital-to-Analog Converter for interfacing with analog devices.

  Its primary purpose is to integrate and test these IPs collaboratively and calibrate the analog part of the SoC.

<img width="624" alt="Screenshot 2024-12-01 at 7 38 02 AM" src="https://github.com/user-attachments/assets/51998ac2-e3af-4965-83d2-82a1e5d71db9">


  ---
  
  ### What is an SoC?
  An SoC (System on Chip) is a single-die chip that combines multiple IP cores, ranging from digital microprocessors to analog broadband modems.

  ### Key Components
  - **RVMYTH**: A RISC-V-based CPU core created by students during a workshop by RedwoodEDA and VSD.
  - **PLL**: Synchronizes clock signals using phase relationships.
  - **DAC**: Converts digital signals to analog for communication with analog systems.

  </details>

- <details>
  <summary>VSDBabySoC Modeling</summary>

  ### Overview
  - **Design Flow**: Physical Design performed using IC Compiler II (ICC2).
  - **PDKs**: Initially planned with SAED32_28nm, switched to Nangate45nm due to compatibility issues.
  - **Workflow**: Integration of digital (RVMYTH) and analog (DAC, PLL) blocks.

  ### Workflow Breakdown
  1. Input signals initialize the SoC.
  2. PLL generates a stable clock for RVMYTH.
  3. RVMYTH processes instructions and sends values to the DAC.
  4. DAC outputs the final signal.

  ---
  
  **Note**: Currently, the modeling focuses on RVMYTH due to DAC and PLL compatibility challenges.

  </details>

- <details>
  <summary>Modeling Details</summary>

  ### RVMYTH Modeling
  - Created in **TL-Verilog** and converted to Verilog using SandPiper SaaS.
  - Reference repository: [RVMYTH GitHub](#)

  ### DAC Modeling
  - Synthesized with **Design Compiler** and verified with **PrimeWave**.
  - Reference repository: [DAC GitHub](#)

  ### PLL Modeling
  - Simulated using real datatype for analog design verification.
  - Reference repository: [PLL GitHub](#)

  </details>

- <details>
  <summary>Lab Instructions</summary>

  ### Getting Started with VSDBabySoC

  #### Exporting LEF Files
  - For DAC and PLL (Analog Blocks):
    1. Navigate to **Custom Compiler (CC)**.
    2. Go to `Export > LEF` and `Export > Stream`.
  - For RVMYTH (Digital Block):
    1. Use the `rvmyth.v` file.
    2. Write the `vsdbabysoc.v` code integrating `rvmyth`, `PLL`, and `DAC`.

  ---
  
  #### Gate-Level Synthesis
  - Run **Design Compiler**:
    ```bash
    dc_shell> source vsdbabysoc.tcl
    ```
    - Output: `vsdbabysoc_gtlvl.v` (Synthesis file)
  
  ---
  
  #### Physical Design
  - Run **IC Compiler II**:
    ```bash
    icc2_shell> source top.tcl
    ```
    - Executes the complete Physical Design Flow.

  ---

  </details>

---

# IC Compiler II (ICC2) Overview

IC Compiler II is Synopsys' industry-leading physical design tool for place and route, delivering optimized **Performance, Power, and Area (PPA)** for next-generation designs. It supports a wide range of designs across market verticals and process technologies, enabling efficient design closure and faster time-to-market.

<img width="494" alt="Screenshot 2024-12-01 at 7 38 57 AM" src="https://github.com/user-attachments/assets/4d4bfa64-efae-449b-8516-7ee54dd614d6">

<img width="579" alt="Screenshot 2024-12-01 at 7 39 27 AM" src="https://github.com/user-attachments/assets/5977870a-c24b-45ea-b456-24ba8a57e9f1">

<img width="327" alt="Screenshot 2024-12-01 at 7 39 43 AM" src="https://github.com/user-attachments/assets/fcad6b4c-6018-4e08-837b-f8237b1c1d1c">

---

## Key Features

### 1. **Hierarchical and Flat Design Support**
- **Hierarchical Design Flow**: 
  - Multi-level physical hierarchy support for large, complex designs.
  - Efficient design partitioning with **Hierarchy Browser**.
- **Flat Design Flow**: Streamlined for smaller designs with minimal hierarchy.

### 2. **Floorplanning**
- Logical-to-physical block mapping and layout generation.
- Iterative process to ensure:
  - **Timing Closure**
  - **Minimal Routing Congestion**
  - **Optimized Area Utilization**
- Includes features like:
  - Macro placement.
  - Power plan creation.
  - Pin placement and timing budgeting.

### 3. **Power Planning**
- Pattern-based methodology for creating robust power and ground meshes.
- Supports **multi-voltage designs** with strategies for different voltage areas.

### 4. **Clock Tree Synthesis (CTS)**
- Concurrent clock and data optimization.
- Advanced algorithms for reduced clock skew and better performance.

### 5. **Routing**
- Modern routing solutions for advanced nodes (e.g., **FinFET**, **multi-patterning**).
- Congestion-aware routing for optimal layout.

### 6. **Timing and ECO Closure**
- Real-time **signoff timing analysis** with **path-based analysis (PBA)**.
- Supports **Engineering Change Orders (ECOs)** for quick iterations.

### 7. **Machine Learning Integration**
- Predictive optimization for faster design convergence and improved QoR.

---


## Technology and Libraries

### Technology File
Defines process-specific parameters such as:
- Metal layer and via characteristics.
- Design rules for width, spacing, and routing.
- Electrical properties like dielectric constants.

### Milkyway Reference Libraries
Stores design views, including:
- **CEL**: Full layout view.
- **FRAM**: Abstract view for P&R.
- **LM**: Logical Model with timing and power data.

```
Technology {
dielectric = 3.7
unitTimeName = "ns"
timePrecision = 1000
unitLengthName = "micron"
lengthPrecision = 1000
gridResolution = 5
unitVoltageName = "v"
}
...
Layer "m1" {
layerNumber = 16
maskName = "metal1"
pitch = 0.56
defaultWidth = 0.23
minWidth = 0.23
minSpacing = 0.23
```

---

## Design Flow

<img width="516" alt="Screenshot 2024-12-01 at 7 40 30 AM" src="https://github.com/user-attachments/assets/389e5594-a297-427b-ac4c-cd436f458ad6">


### 1. **Design Planning**
- **Partitioning**: Divide designs into manageable blocks for parallel processing.
- **Timing Budgeting**: Allocate timing constraints to each block.
- **Power Planning**: Define strategies for power/ground connections.

### 2. **Placement**
- Macro and standard cell placement optimized for:
  - Congestion.
  - Timing.
  - Area utilization.

### 3. **Routing**
- High-performance routing for signal and power integrity.
- Ensures compliance with DRC and advanced manufacturing rules.

### 4. **Validation**
- Use the `check_design` command to validate the design at each stage:
  - Pre-floorplan.
  - Pre-macro placement.
  - Pre-power insertion.



---

## Commands and Tools

- **Hierarchy Browser**: Navigate design hierarchy for partitioning and analysis.
- **check_design**: Validate design readiness for the next stage.
- **set_editability**: Control block-level hierarchy for planning and editing.

---

## Advantages

- **Improved QoR**: Enhanced PPA and reduced congestion.
- **Scalability**: Efficient use of multi-core systems for faster runtimes.
- **Flexibility**: Supports flat and hierarchical designs.
- **Future-Ready**: Machine learning integration for predictive optimizations.

---

# RVMYTH Core in VSDBabySoC

This repository includes scripts and instructions for generating a Gate-Level Netlist, performing synthesis, and completing physical design using Synopsys tools like **dc_shell** and **icc2_shell**.

<img width="455" alt="Screenshot 2024-12-01 at 7 40 47 AM" src="https://github.com/user-attachments/assets/f8060832-f67e-4083-9afe-bd60da5c2a68">

<img width="426" alt="Screenshot 2024-12-01 at 7 41 03 AM" src="https://github.com/user-attachments/assets/f0eab5ef-480d-46da-97c5-82fda413b2a2">

---

## Synthesis

### Script for Gate-Level Netlist Generation

Below is the `vsdbabysoc.tcl` (or your preferred filename, e.g., `[filename].tcl`) script to generate the Gate-Level Netlist (`vsdbabysoc_gtlvl.v`):

```tcl
set target_library [list /path/to/target_lib1.db /path/to/target_lib2.db /path/to/target_lib3.db]
set link_library [list /path/to/link_lib1.db /path/to/link_lib2.db /path/to/link_lib3.db]
set symbol_library ""

read_file -format verilog {/path/to/vsdbabysoc.v}
read_verilog /path/to/rvmyth.v
read_verilog /path/to/clk_gate.v

analyze -library WORK -format verilog {/path/to/vsdbabysoc.v}
elaborate vsdbabysoc -architecture verilog -library WORK

set_units -time ns
create_clock [get_pins {pll/CLK}] -name clk -period 10

set_max_area 8000
set_max_fanout 5 vsdbabysoc
set_max_transition 10 vsdbabysoc

set_input_delay -max 4 -clock [get_clocks MYCLK] [get_ports ENb_CP]
set_input_transition -max 0.4 [get_ports ENb_CP]
set_load -max 0.5 [get_ports OUT]

check_design

compile_ultra

file mkdir report
write -hierarchy -format verilog -output /path/to/vsdbabysoc_gtlvl.v
write_sdc -nosplit -version 2.0 /path/to/vsdbabysoc.sdc
report_area -hierarchy > /path/to/report/vsdbabysoc.area
report_timing > /path/to/report/vsdbabysoc.timing
report_power -hierarchy > /path/to/report/vsdbabysoc.power

gui_start
```
 
# RVMYTH Core in VSDBabySoC

This repository includes scripts and instructions for generating a Gate-Level Netlist, performing synthesis, and completing physical design using Synopsys tools like **dc_shell** and **icc2_shell**.

---

## Synthesis

### Script for Gate-Level Netlist Generation

Below is the `vsdbabysoc.tcl` (or your preferred filename, e.g., `[filename].tcl`) script to generate the Gate-Level Netlist (`vsdbabysoc_gtlvl.v`):

```tcl
set target_library [list /path/to/target_lib1.db /path/to/target_lib2.db /path/to/target_lib3.db]
set link_library [list /path/to/link_lib1.db /path/to/link_lib2.db /path/to/link_lib3.db]
set symbol_library ""

read_file -format verilog {/path/to/vsdbabysoc.v}
read_verilog /path/to/rvmyth.v
read_verilog /path/to/clk_gate.v

analyze -library WORK -format verilog {/path/to/vsdbabysoc.v}
elaborate vsdbabysoc -architecture verilog -library WORK

set_units -time ns
create_clock [get_pins {pll/CLK}] -name clk -period 10

set_max_area 8000
set_max_fanout 5 vsdbabysoc
set_max_transition 10 vsdbabysoc

set_input_delay -max 4 -clock [get_clocks MYCLK] [get_ports ENb_CP]
set_input_transition -max 0.4 [get_ports ENb_CP]
set_load -max 0.5 [get_ports OUT]

check_design

compile_ultra

file mkdir report
write -hierarchy -format verilog -output /path/to/vsdbabysoc_gtlvl.v
write_sdc -nosplit -version 2.0 /path/to/vsdbabysoc.sdc
report_area -hierarchy > /path/to/report/vsdbabysoc.area
report_timing > /path/to/report/vsdbabysoc.timing
report_power -hierarchy > /path/to/report/vsdbabysoc.power

gui_start
```

Running this script in dc_shell generates the Gate-Level Netlist (vsdbabysoc_gtlvl.v).

### Schematic

Once the synthesis flow completes successfully, the following blocks are generated:

<img width="769" alt="Screenshot 2024-12-01 at 7 45 06 AM" src="https://github.com/user-attachments/assets/7a700caf-6d2f-4e04-9cac-a501ef19efcb">


# Physical Design

The top.tcl script provided in this repository is used for the physical design flow. It can be executed in the icc2_shell to generate the final layout. The steps in the flow include:

**Key Steps**

```txt

###---NDM Library creation---###

###---Read Synthesized Verilog---###

## Technology setup for routing layer direction, offset, site default, and site symmetry.

###---Routing settings---###

####################################
# Check Design: Pre-Floorplanning
####################################

####################################
# Floorplanning
####################################

####################################
## PG Pin connections
#####################################

####################################
### Place IO
######################################

####################################
### Memory Placement
######################################

####################################
# Configure placement
####################################

########################################
## Read parasitic files
########################################

########################################
## Read constraints
########################################

####################################
# Fix all shaped blocks and macros
####################################

####################################
# Create Power
####################################

####################################
# Pin Placement
####################################

####################################
# Timing estimation
####################################

####################################
# Place, CTS, Route
####################################

## Start gui
```

After running the script, type start_gui in icc2_shell to visualize the layout:

<img width="1440" alt="Screenshot 2024-12-05 at 8 49 31 PM" src="https://github.com/user-attachments/assets/e9606ac5-6a3a-4c88-b0a4-23e8b7496042">

## FINCELLs

Standard cells and their placements are shown below:

<img width="1279" alt="Screenshot 2024-12-05 at 8 54 21 PM" src="https://github.com/user-attachments/assets/11c55424-3f75-4717-87ae-34185f725def">


## Outputs Generated

1.	Set Clock Propagation:
 
`set_propagated_clock [all_clocks]`  

<img width="624" alt="Screenshot 2024-12-01 at 7 46 04 AM" src="https://github.com/user-attachments/assets/c03cecb7-5e1b-45fc-9056-39148a8d120b">

## Violations

To check for violations, type the following command in icc2_shell after generating the layout:

`report_constraints -all_violators -nosplit -verbose -significant_digits 4 > violators.rpt`

<img width="819" alt="Screenshot 2024-12-01 at 7 48 04 AM" src="https://github.com/user-attachments/assets/a2ea38a9-3399-4ca6-8b85-a6ace1cacecc">

View the report using:

`vim violators.rpt`

**Example output:**

<img width="659" alt="Screenshot 2024-12-01 at 7 47 28 AM" src="https://github.com/user-attachments/assets/91b044f0-3b5a-4dfc-a26b-16fb51e85b82">

<images>

### File Structure

  . vsdbabysoc.tcl: Script for Gate-Level Netlist generation.
  . top.tcl: Script for physical design flow.
  . report/: Directory containing synthesis and design reports.


---

