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

  <img width="1440" alt="Screenshot 2024-12-10 at 11 31 14 AM" src="https://github.com/user-attachments/assets/6d26edae-1904-40a6-a42a-00ed5b774e8b">

  run `dc_shell` and `source sythesis.tcl`

  <img width="898" alt="Screenshot 2024-12-10 at 11 32 38 AM" src="https://github.com/user-attachments/assets/2bdf6140-7a32-4e20-9210-eeb982b1aec8">

  <img width="879" alt="Screenshot 2024-12-10 at 11 33 09 AM" src="https://github.com/user-attachments/assets/f4715559-a683-41e6-a305-558a8868ad6c">

  <img width="861" alt="Screenshot 2024-12-10 at 11 33 45 AM" src="https://github.com/user-attachments/assets/e3fe7bd3-46ff-4070-bfad-7ed420cdf105">

## Reports

**1.	QoR Report:**

 ```txt
 Information: Updating design information... (UID-85)
 
****************************************
Report : qor
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Tue Dec 10 17:12:13 2024
****************************************


  Timing Path Group 'clk'
  -----------------------------------
  Levels of Logic:              46.00
  Critical Path Length:          9.92
  Critical Path Slack:           0.01
  Critical Path Clk Period:     10.00
  Total Negative Slack:          0.00
  No. of Violating Paths:        0.00
  Worst Hold Violation:          0.00
  Total Hold Violation:          0.00
  No. of Hold Violations:        0.00
  -----------------------------------

  Timing Path Group 'default'
  -----------------------------------
  Levels of Logic:               1.00
  Critical Path Length:          0.87
  Critical Path Slack:           9.13
  Critical Path Clk Period:       n/a
  Total Negative Slack:          0.00
  No. of Violating Paths:        0.00
  Worst Hold Violation:          0.00
  Total Hold Violation:          0.00
  No. of Hold Violations:        0.00
  -----------------------------------


  Cell Count
  -----------------------------------
  Hierarchical Cell Count:          1
  Hierarchical Port Count:         12
  Leaf Cell Count:               3273
  Buf/Inv Cell Count:            1120
  Buf Cell Count:                 368
  Inv Cell Count:                 752
  CT Buf/Inv Cell Count:            0
  Combinational Cell Count:      2597
  Sequential Cell Count:          676
  Macro Count:                      0
  -----------------------------------


  Area
  -----------------------------------
  Combinational Area:    13486.684574
  Noncombinational Area: 13532.978775
  Buf/Inv Area:           4204.031868
  Total Buffer Area:          1381.32
  Total Inverter Area:        2822.71
  Macro/Black Box Area:      0.000000
  Net Area:                  0.000000
  -----------------------------------
  Cell Area:             27019.663349
  Design Area:           27019.663349


  Design Rules
  -----------------------------------
  Total Number of Nets:          3295
  Nets With Violations:             0
  Max Trans Violations:             0
  Max Cap Violations:               0
  -----------------------------------


  Hostname: sfalvsd

  Compile CPU Statistics
  -----------------------------------------
  Resource Sharing:                    6.75
  Logic Optimization:                  3.28
  Mapping Optimization:                5.08
  -----------------------------------------
  Overall Compile Time:               39.46
  Overall Compile Wall Clock Time:    40.16

  --------------------------------------------------------------------

  Design  WNS: 0.00  TNS: 0.00  Number of Violating Paths: 0


  Design (Hold)  WNS: 0.00  TNS: 0.00  Number of Violating Paths: 0

  --------------------------------------------------------------------
 ```

**2.	Area Report**

```txt
****************************************
Report : area
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Tue Dec 10 17:12:13 2024
****************************************

Library(s) Used:

    sky130_fd_sc_hd__tt_025C_1v80 (File: /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db)
    avsddac (File: /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsddac.db)
    avsdpll (File: /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsdpll.db)

Number of ports:                           19
Number of nets:                          3307
Number of cells:                         3274
Number of combinational cells:           2595
Number of sequential cells:               676
Number of macros/black boxes:               2
Number of buf/inv:                       1120
Number of references:                       4

Combinational area:              13486.684574
Buf/Inv area:                     4204.031868
Noncombinational area:           13532.978775
Macro/Black Box area:                0.000000
Net Interconnect area:      undefined  (Wire load has zero net area)

Total cell area:                 27019.663349
Total area:                 undefined
```

**3.	Power Report**

```txt
****************************************
Report : power
        -analysis_effort low
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Tue Dec 10 17:12:13 2024
****************************************


Library(s) Used:

    sky130_fd_sc_hd__tt_025C_1v80 (File: /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db)
    avsddac (File: /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsddac.db)
    avsdpll (File: /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsdpll.db)


Operating Conditions: tt_025C_1v80   Library: sky130_fd_sc_hd__tt_025C_1v80
Wire Load Model Mode: top

Design        Wire Load Model            Library
------------------------------------------------
vsdbabysoc             Small             sky130_fd_sc_hd__tt_025C_1v80


Global Operating Voltage = 1.8  
Power-specific unit information :
    Voltage Units = 1V
    Capacitance Units = 1.000000pf
    Time Units = 1ns
    Dynamic Power Units = 1mW    (derived from V,C,T units)
    Leakage Power Units = 1nW


Attributes
----------
i - Including register clock pin internal power


  Cell Internal Power  =   2.8782 mW   (82%)
  Net Switching Power  = 615.5834 uW   (18%)
                         ---------
Total Dynamic Power    =   3.4938 mW  (100%)

Cell Leakage Power     =   8.7213 nW


                 Internal         Switching           Leakage            Total
Power Group      Power            Power               Power              Power   (   %    )  Attrs
--------------------------------------------------------------------------------------------------
io_pad             0.0000            0.0000            0.0000            0.0000  (   0.00%)
memory             0.0000            0.0000            0.0000            0.0000  (   0.00%)
black_box          0.0000            0.4454            0.0000            0.4454  (  12.75%)
clock_network      2.7524            0.0000            0.0000            2.7524  (  78.78%)  i
register       4.6189e-02        1.6094e-02            5.4668        6.2288e-02  (   1.78%)
sequential         0.0000            0.0000            0.0000            0.0000  (   0.00%)
combinational  7.9652e-02            0.1541            3.2545            0.2338  (   6.69%)
--------------------------------------------------------------------------------------------------
Total              2.8782 mW         0.6156 mW         8.7213 nW         3.4938 mW
--------------------------------------------------------------------------------------------------
```

### Schematics

**1.	VSDBabySoC Schematic**

<image here>

**2.	RVMYTH Core Schematic**

<image here>

**Script Setup for Collaterals**

Collateral setup scripts can be found at the following path:

`/home/hemanth/Desktop/VLSI/VSDBabySoc/standaloneFlow`

**Key Files:**

  . compile_pg_example.tcl
  . init_design.mcmm_example.auto_expanded.tcl
  . init_design.read_parasitic_tech_example.tcl
  . init_design.tech_setup.tcl
  . pns_example.tcl
  . top.tcl
  . write_block_data.tcl

**compile_pg_example.tcl**

```tcl
compile_pg -strategies core_ring
#compile_pg -strategies s_pad
compile_pg -strategies s_mesh1
#compile_pg -strategies macro_con 
compile_pg -strategies rail_strat
```
**init_design.mcmm_example.auto_expanded.tcl**

<img width="1440" alt="Screenshot 2024-12-10 at 10 54 31 PM" src="https://github.com/user-attachments/assets/ba857b56-0f9a-4a03-ac14-bf30ca431832">

**init_design.read_parasitic_tech_example.tcl**

<img width="1440" alt="Screenshot 2024-12-10 at 10 58 23 PM" src="https://github.com/user-attachments/assets/c4fd6ef9-f8d9-4ade-8a63-1fa720becbc6">

**init_design.tech_setup.tcl**

<img width="1440" alt="Screenshot 2024-12-10 at 10 59 28 PM" src="https://github.com/user-attachments/assets/713d084e-3309-4b45-92de-e0fb8b1586d2">

**pns_example.tcl**

<img width="1440" alt="Screenshot 2024-12-10 at 11 00 16 PM" src="https://github.com/user-attachments/assets/8b22bac7-4e57-4fd1-a60d-ee02cf04b41c">

**top.tcl**

<img width="1440" alt="Screenshot 2024-12-10 at 11 01 02 PM" src="https://github.com/user-attachments/assets/73475867-b1c2-4512-b4f8-60d61c8fc5a1">

<img width="1440" alt="Screenshot 2024-12-10 at 11 01 17 PM" src="https://github.com/user-attachments/assets/392a023c-6bcc-41fd-b9c4-3a8ed9762dbc">

<img width="1440" alt="Screenshot 2024-12-10 at 11 01 30 PM" src="https://github.com/user-attachments/assets/407cfede-34fd-46c7-91a1-66a52405dbd9">

<img width="1440" alt="Screenshot 2024-12-10 at 11 01 55 PM" src="https://github.com/user-attachments/assets/3f93cddf-2a35-4198-afe9-98dfccc1a792">

<img width="1440" alt="Screenshot 2024-12-10 at 11 02 08 PM" src="https://github.com/user-attachments/assets/e74c2f4d-6b7f-4a1a-9ce3-ee8906722839">

**write_block_data.tcl**

<img width="1440" alt="Screenshot 2024-12-10 at 11 03 00 PM" src="https://github.com/user-attachments/assets/31bbbbcb-711c-4c66-b88a-3949ffce2163">

---

**Run `icc2_shell`**

<img width="776" alt="Screenshot 2024-12-10 at 11 04 19 PM" src="https://github.com/user-attachments/assets/79abccc6-fe74-440d-9da6-4d5e6d9e0a2d">

`source top.tcl`

<img width="768" alt="Screenshot 2024-12-10 at 11 18 14 PM" src="https://github.com/user-attachments/assets/c5f1729a-eb66-4590-83d7-b10edaed7b47">

---

**Output**

`start_gui`

<image here>
  
extract parasitics information in .SPEF format and post_route netlist by using following command :

```bash
file mkdir ./output_after_placement
write_verilog ./output_after_placement/design_after_place_opt.v
file mkdir ./output_spef_after_placement
write_parasitics -corner func1 -output ./output_spef_after_placement/design_after_place_opt.spef
write_verilog /home/subhasis/VSDBabySoC/output/vsdbabysoc_post_route_net.v
```

<img width="974" alt="Screenshot 2024-12-10 at 11 21 06 PM" src="https://github.com/user-attachments/assets/93a4f4f3-a16e-426e-9524-474639d4d1c0">

**design_after_place_opt.spef.temp1_25.spef**

<img width="1440" alt="Screenshot 2024-12-10 at 11 22 34 PM" src="https://github.com/user-attachments/assets/b903d421-c81a-49a0-bb44-3cc05dda067c">

**vsdbabysoc_post_route_net.v**

<img width="1440" alt="Screenshot 2024-12-10 at 11 25 29 PM" src="https://github.com/user-attachments/assets/0eb9be22-113b-4479-abe1-8d0cbc839487">

---

## Prime Time STA analysis for all available PVT Corners

Script to run STA analysis for all PVT Corners:

```tcl
set m1 ""
set pvt ""
set wns ""
set whs ""
set FH [open report_timing_prime_time.rpt w]
puts $FH "PVT_Corner\tWNS\tWHS"
set lib_files [glob -directory /home/hemanth/Desktop/VLSI/VSDBabySoc/src/Timing/timing/ -type f *.db]
foreach lib_file_paths $lib_files {
regexp {.*\/sky130_fd_sc_hd__(.*)\.db$} $lib_file_paths m1 pvt

set link_path "* /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsdpll.db /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsddac.db"
lappend link_path $lib_file_paths

read_verilog "/home/hemanth/Desktop/VLSI/VSDBabySoc/standaloneFlow/output_after_placement/design_after_place_opt.v"
current_design vsdbabysoc

link_design
read_sdc "/home/hemanth/Desktop/VLSI/VSDBabySoc/vsdbabysoc_icc2.sdc"
read_parasitics "/home/hemanth/Desktop/VLSI/VSDBabySoc/standaloneFlow/output_spef_after_placement/design_after_place_opt.spef.temp1_25.spef"


set wns [get_attribute [get_timing_paths -delay_type max -max_paths 1] slack]
set whs [get_attribute [get_timing_paths -delay_type min -max_paths 1] slack]

puts $FH "$pvt\t$wns\t$whs"

remove_annotated_parasitics -all
reset_design
remove_design -all
remove_lib -all
}
close $FH
```

run `pt_shell`

<img width="965" alt="Screenshot 2024-12-10 at 11 37 15 PM" src="https://github.com/user-attachments/assets/397a5db5-7d5b-4a6d-8f99-f96756f5d01d">

`source prime_time_sta.tcl`

---

<img width="1440" alt="Screenshot 2024-12-10 at 11 51 08 PM" src="https://github.com/user-attachments/assets/35785883-e22c-40a7-9090-7f3d77304e3d">

---







