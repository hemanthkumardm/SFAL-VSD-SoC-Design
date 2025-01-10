
# Pre-layout Timing Analysis and Importance of Good Clock Tree

This section outlines the process of performing pre-layout timing analysis and emphasizing the importance of a good clock tree in VLSI design. It covers the necessary steps to ensure that the design is ready for further stages in the OpenLane flow, including the integration of custom-designed cells and timing optimization.


### Fix Small DRC Errors and Verify the Design

Before proceeding with the custom-designed cell layout, we verify that the design meets specific DRC (Design Rule Check) conditions:

1. The input and output ports of the standard cell should lie at the intersection of the vertical and horizontal tracks.
2. The width of the standard cell should be an odd multiple of the horizontal track pitch.
3. The height of the standard cell should be an even multiple of the vertical track pitch.

#### Commands to Open the Custom Inverter Layout

```bash
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

**Screenshot Verification:**

  - Condition 1: Verified with the ports on the intersection of the tracks.
    <img width="792" alt="Screenshot 2024-11-27 at 3 15 37 AM" src="https://github.com/user-attachments/assets/e1190ab0-0f30-4cb6-aeaa-fcac1d08e74c">

  - Condition 2: Verified with a cell width of 1.38µm (0.46 * 3).
    <img width="761" alt="Screenshot 2024-11-27 at 3 15 51 AM" src="https://github.com/user-attachments/assets/a93e9597-a9b8-4041-bd36-0e33e54e2c4d">

  - Condition 3: Verified with a cell height of 2.72µm (0.34 * 8).
    <img width="753" alt="Screenshot 2024-11-27 at 3 16 07 AM" src="https://github.com/user-attachments/assets/0258e8a5-f6ef-4bc2-9e52-f624793fb171">
    
#### Save Finalized Layout

After verifying the design, save the layout with a custom name.
```
# Command to save the layout with a custom name
save sky130_vsdinv.mag
# Command to open the newly saved layout
magic -T sky130A.tech sky130_vsdinv.mag &
```

Screenshot of Saved Layout:

  - The layout has been saved as sky130_vsdinv.mag for further steps.

#### Generate LEF from Layout

Generate a LEF (Library Exchange Format) file from the layout for integration into the OpenLane flow.

![Screenshot from 2024-11-25 18-51-06](https://github.com/user-attachments/assets/d55cf418-2c37-44af-9f69-aad09a89011d)
![Screenshot from 2024-11-25 18-49-03](https://github.com/user-attachments/assets/79c07942-5be7-4af1-9989-1c62a2e257ea)
![Screenshot from 2024-11-25 18-37-25](https://github.com/user-attachments/assets/04d2e011-c7d9-423e-90f6-2020d46eedad)
![Screenshot from 2024-11-25 18-37-00](https://github.com/user-attachments/assets/c98497b0-d68a-4bc8-9151-8acfc36db269)
![Screenshot from 2024-11-25 18-51-42](https://github.com/user-attachments/assets/bc5a5bf2-df63-4227-b931-fbb6e82c84b3)

---

#### Copy LEF and Library Files to the picorv32a Design

Copy the generated LEF and associated library files to the picorv32a design’s src directory.

```
# Copy LEF file to src directory
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Check if the files were copied successfully
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy library files to src directory
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Check if the library files were copied successfully
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

<img width="760" alt="Screenshot 2024-11-27 at 3 18 26 AM" src="https://github.com/user-attachments/assets/5b491344-62be-43ec-9aee-3107b8299dbc">

---

#### Edit config.tcl to Include Custom Cells

Modify the config.tcl file to include the custom LEF file and change the libraries to the ones we have added.

![Screenshot from 2024-11-25 20-04-13](https://github.com/user-attachments/assets/aed52c27-7629-4974-b87f-673d7ae7ad82)

---

#### Run OpenLane Flow Synthesis

Run the OpenLane flow to perform synthesis with the newly inserted custom inverter cell.

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```

<img width="765" alt="Screenshot 2024-11-27 at 3 25 52 AM" src="https://github.com/user-attachments/assets/64412f29-0df9-43b7-aa6e-2f44e56999b1">
<img width="585" alt="Screenshot 2024-11-27 at 3 26 11 AM" src="https://github.com/user-attachments/assets/9abb6c6c-5465-4f30-8815-51fcea072094">
<img width="517" alt="Screenshot 2024-11-27 at 3 26 34 AM" src="https://github.com/user-attachments/assets/ab1d9bfa-267f-48ba-a20d-1003d9236871">

---

#### Handle Violations Introduced by Custom Cell

After inserting the custom inverter, there may be violations introduced. Modify design parameters to fix these violations.

<img width="759" alt="Screenshot 2024-11-27 at 3 30 16 AM" src="https://github.com/user-attachments/assets/feb5deaa-32fe-459b-ac11-c9bda9c28e59">

---

# VLSI Design with OpenLane: Custom Inverter and Timing Analysis

This repository demonstrates the process of creating and integrating a custom inverter into a VLSI design using OpenLane. It covers the steps of design preparation, synthesis, floorplanning, placement, timing analysis, and fixing timing violations.


## Prerequisites

- **OpenLane** toolchain for physical design and synthesis.
- **Magic** tool for viewing placement and routing.
- **OpenSTA** for static timing analysis.
- **Docker** for running the OpenLane flow.
- **Custom LEF file** containing the custom inverter.

## Design Setup

1. **Prepare the design** by running the following command to set up the necessary files and directories:

    ```tcl
    prep -design picorv32a -tag 26-11_04-28 -overwrite
    ```

<img width="1056" alt="Screenshot 2024-11-27 at 8 43 54 AM" src="https://github.com/user-attachments/assets/0a23dcc8-adca-4c34-a9c0-504fbf9ff182">

--

2. **Add the custom LEF** file to the design flow:
    ```tcl
    set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
    add_lefs -src $lefs
    ```

<img width="420" alt="Screenshot 2024-11-27 at 8 46 02 AM" src="https://github.com/user-attachments/assets/33c2b158-97a5-486d-ab37-9de7e41ebda2">
 
---

3. **Set synthesis parameters** to optimize the design:
    ```tcl
    set ::env(SYNTH_STRATEGY) "DELAY 3"
    set ::env(SYNTH_SIZING) 1
    ```

<img width="354" alt="Screenshot 2024-11-27 at 8 47 19 AM" src="https://github.com/user-attachments/assets/fdfd57be-0df6-4abb-8e2e-3e75b51a57be">

---

## Custom Inverter Integration

1. **Create a custom inverter** and merge it into the design by updating the LEF file:
    - Use the `merged.lef` file for the integration of the custom inverter.
    - Update the OpenLane flow to include the newly added LEF file.

2. **Run synthesis** to ensure that the custom inverter is accepted by the flow:
    ```tcl
    run_synthesis
    ```
![Screenshot from 2024-11-26 13-23-02](https://github.com/user-attachments/assets/571669e6-4fcb-443c-bb81-801a53b4beec)

---


3. **Check the results** by observing the slack and area improvements. The slack should become 0, and area might increase due to the custom inverter.

## Synthesis and Timing Optimization

1. **Modify synthesis parameters** to optimize timing:
    ```tcl
    set ::env(SYNTH_MAX_FANOUT) 4
    ```

2. **Run synthesis again** to observe the improvements:
    ```tcl
    run_synthesis
    ```

3. **Perform timing analysis** with OpenSTA to verify improvements:
    ```bash
    sta pre_sta.conf
    ```


## Post-Synthesis Timing Analysis

1. **OpenSTA** is used to analyze the timing of the design post-synthesis. Ensure the design is prepped and run the synthesis before performing STA.

2. **Generate a timing report**:
    ```bash
    report_checks -fields {net cap slew input_pins} -digits 4
    ```

3. **Fix violations** by replacing cells (e.g., OR gates with higher drive strength):
    ```tcl
    replace_cell _14510_ sky130_fd_sc_hd__or3_4
    ```

## Floorplanning and Placement

1. **Run floorplan** and place IOs:
    ```tcl
    run_floorplan
    ```
    
![Screenshot from 2024-11-26 13-24-33](https://github.com/user-attachments/assets/1fa84394-a7cd-497a-9eeb-d8b2f40687ed)


2. **Use alternative commands** for floorplan if errors occur:
    ```tcl
    init_floorplan
    place_io
    tap_decap_or
    ```

![Screenshot from 2024-11-26 13-25-35](https://github.com/user-attachments/assets/6ff94de5-0ae4-47b2-b38c-e82b31a6f790)
 ![Screenshot from 2024-11-26 13-25-46](https://github.com/user-attachments/assets/25b05d28-bd41-4de4-bdf9-231f398c7712)
![Screenshot from 2024-11-26 13-25-39](https://github.com/user-attachments/assets/85d2880a-b654-4246-9ff7-999a589449e5)


3. **Run placement**:
    ```tcl
    run_placement
    ```

![Screenshot from 2024-11-26 13-35-02](https://github.com/user-attachments/assets/a17d7a04-39d6-4c0a-9897-8fcfa574b719)

4. **View placement in Magic**:
    - Load the placement definition into Magic for visualization:
    ```bash
    magic -T $PDK_ROOT/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
    ```

![Screenshot from 2024-11-26 13-43-51](https://github.com/user-attachments/assets/659cae33-244b-4cdd-8f1f-05e6665821bb)
![Screenshot from 2024-11-26 13-43-26](https://github.com/user-attachments/assets/c1ea06c1-0b16-4052-9bd9-7c1bbfac55dd)
![Screenshot from 2024-11-26 13-35-12](https://github.com/user-attachments/assets/924c1a33-8e70-4cd7-a6cf-e3e504cac7cf)

---

# Post-Synthesis Timing Analysis and ECO Fixes with OpenSTA

This documentation outlines the process of performing post-synthesis timing analysis, ECO (Engineering Change Order) fixes, and updating the netlist in OpenLANE. The primary focus is on analyzing timing violations, optimizing timing through ECO fixes, and incorporating the updated netlist into the physical design flow.

---

## 9. Post-Synthesis Timing Analysis with OpenSTA

### Initial Timing Analysis
Since the initial synthesis run contains timing violations, we analyze it before any optimization.

#### Steps to Invoke OpenLANE and Perform Synthesis
```bash
# Navigate to OpenLANE directory
cd Desktop/work/tools/openlane_working_dir/openlane

# Invoke the Docker environment
docker

# Open OpenLANE in interactive mode
./flow.tcl -interactive

# Load OpenLANE packages
package require openlane 0.9

# Prepare the design
prep -design picorv32a

# Include additional LEFs
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Set SYNTH_SIZING variable
set ::env(SYNTH_SIZING) 1

# Run synthesis
run_synthesis
```

Create pre_sta.conf

```
# Navigate to OpenLANE directory
cd Desktop/work/tools/openlane_working_dir/openlane

# Run OpenSTA with the configuration script
sta pre_sta.conf
```

**pre_sta.conf**

```
set_cmd_units -time ns -capacitance pF -current mA -voltage V - resistance kOhm -distance um

read_liberty -max /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib
read_liberty -min /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib

read_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/run s/25-03_18-52/results/synthesis/picorv32a.synthesis.v
link design picorv32a
read_sdc /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/my_base.sdc
report tns report wns
report_checks-path_delay min_max -fields {slew trans net cap input_pin}
```

<img width="752" alt="Screenshot 2024-11-27 at 9 15 37 AM" src="https://github.com/user-attachments/assets/f2bb6096-3752-457a-8b10-41747dcf4317">

Newly created `my_base.sdc` for STA analysis in `openlane/designs/picorv32a/src` directory based on the file `openlane/scripts/base.sdc`

**my_base.sdc**

```
set ::env(CLOCK_PORT) clk
set :: env(CLOCK PERIOD) 24.73
#set ::env(SYNTH_DRIVING_CELL) sky130_vsdinv
set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
set :: env(SYNTH_DRIVING CELL_PIN) Y
set :: env(SYNTH CAP LOAD) 17.653
set :: env(IO_PCT) 0.2
set :: env(SYNTH_MAX FANOUT) 6

create_clock [get_ports $:: env(CLOCK_PORT)] -name $::env(CLOCK_PORT) -period $:: env(CLOCK_PERIOD)
set input_delay_value [expr $::env(CLOCK_PERIOD) * $: :env(IO_PCT)]
set output_delay_value [expr $::env(CLOCK_PERIOD) * $:: :env(I0_PCT) ]
puts "\[INFO\]: Setting output delay to: $output_delay_value"
puts "\[INFO\]: Setting input delay to: $input_delay_value"

set_max_fanout $:: env (SYNTH_MAX_FANOUT) [current_design]

set clk_indx Ilsearch [all_ inputs] lget_port $::env(CLOCK_PORT)]]
#set rst_indx [lsearch [all_inputs] [get_port resetn]]
set all inputs_wo_clk [replace [all_inputs] $clk_indx $clk_indx]
#set all_inputs_wo_clk_rst Ilreplace Sall_inputs_wo _clk $rst_indx $rst_indx]
set all_inputs_wo_clk_rst $all_inputs_wo_clk

# correct resetn

set input delav $input_delay_value -clock [get_clocks $::env(CLOCK_PORT)] $all_inputs_wo_clk_rst
#set_rst_input_delay 0.0-clock [get_clocks §::env(CLOCK_PORT)] {resetn}
set_output_delay $output_delay_value -clock lget_clocks $::env(CLOCK_PORT)] [all_outputs]
# TODO set this as parameter
set_driving_cell - lib_cell $:: env(SYNTH_DRIVING_CELL) -pin $:: env(SYNTH_DRIVING_CELL_PIN) lall_in puts]
set cap_load [expr $::env(SYNTH_CAP_LOAD) / 1000.0]
puts "\[INFO\]: Setting load to: $cap_load"
set_load $cap_load [all_outputs]
```

**Run these commands**

```
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

<img width="756" alt="Screenshot 2024-11-27 at 9 46 58 AM" src="https://github.com/user-attachments/assets/5ac38b08-42f9-4a21-aaef-9f3f6a00725c">

---

### ECO Fixes to Remove Timing Violations

Identifying and Fixing Timing Violations

```
# Report all connections to a net
report_net -connections _11672_

# Replace a cell to improve timing
replace_cell _14510_ sky130_fd_sc_hd__or3_4

# Generate a custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

**Results**

  - Initial Worst Negative Slack (WNS): -23.9000
  - Reduced WNS: -22.6173 (Improvement: 1.2827 ns)

<img width="749" alt="Screenshot 2024-11-27 at 9 49 07 AM" src="https://github.com/user-attachments/assets/0bd2dd2e-cf60-4b0f-9528-75a6c9c12d0f">

---

# Run CTS

`run_cts`

![Screenshot from 2024-11-26 21-28-36](https://github.com/user-attachments/assets/9ec602b6-b8d1-4f83-8011-13c292bb97a5)

 # RTL to GDSII Flow with OpenLANE

This repository documents the RTL-to-GDSII implementation flow using OpenLANE, including post-CTS timing analysis, power distribution network (PDN) generation, detailed routing, and parasitic extraction with SPEF.

---

### Post-CTS Timing Analysis

Commands to perform timing analysis with OpenROAD after CTS:

```tcl
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
help report_checks
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
```

![Screenshot from 2024-11-26 21-48-00](https://github.com/user-attachments/assets/2551fc10-ab87-4882-ac8f-256bab25d99d)

**Modified Timing Analysis**

Steps to modify CTS_CLK_BUFFER_LIST and perform analysis:

```
# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Removing 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Checking current value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Setting def as placement def
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/placement/picorv32a.placement.def

# Run CTS again
run_cts

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts1.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Report hold skew
report_clock_skew -hold

# Report setup skew
report_clock_skew -setup

# Exit to OpenLANE flow
exit

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Inserting 'sky130_fd_sc_hd__clkbuf_1' to first index of list
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)
```

<img width="252" alt="Screenshot 2024-11-27 at 10 10 59 AM" src="https://github.com/user-attachments/assets/925a75bd-4d4f-4110-8c38-dafd5b471939">
<img width="757" alt="Screenshot 2024-11-27 at 10 11 12 AM" src="https://github.com/user-attachments/assets/7c73d404-9288-4932-a15e-816b51c9a3fe">

**Power Distribution Network Generation**

**Commands to generate the PDN and load the DEF in Magic**

```
gen_pdn
magic -T path-to-techfile lef read merged.lef def read pdn.def &
```

![Screenshot from 2024-11-26 22-19-39](https://github.com/user-attachments/assets/434a2cce-2abf-40ae-8213-7a67b82664b9)
![Screenshot from 2024-11-26 22-19-19](https://github.com/user-attachments/assets/cd687017-b676-480f-a026-976ba175cb6b)
![Screenshot from 2024-11-26 22-17-23](https://github.com/user-attachments/assets/9ff2a5ba-7f28-424e-968e-b0be77d4bdca)
![Screenshot from 2024-11-26 22-13-10](https://github.com/user-attachments/assets/8302edb4-eb3e-4949-b219-4ef8b10d9998)
![Screenshot from 2024-11-26 22-12-44](https://github.com/user-attachments/assets/68c14ff6-8a65-4811-b92b-7f1fe800d143)

**Detailed Routing with TritonRoute**

Steps to perform detailed routing:

`run_routing`

![Screenshot from 2024-11-26 22-34-42](https://github.com/user-attachments/assets/eae650ae-67bc-4d21-9282-474737b10f2b)
![Screenshot from 2024-11-26 22-28-03](https://github.com/user-attachments/assets/a33fce8d-4aa2-4dad-be50-132c2b15b961)
![Screenshot from 2024-11-26 22-36-55](https://github.com/user-attachments/assets/6a8f98f4-d032-4551-bb2a-a27c9da11919)
![Screenshot from 2024-11-26 22-37-10](https://github.com/user-attachments/assets/65f8e390-375a-49bf-b1ab-0ff2c46f7dcd)

**Post-Route Timing Analysis**

Commands for post-route timing analysis with SPEF:

```
read_spef /path/to/spef
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
```
![Screenshot from 2024-11-26 22-38-30](https://github.com/user-attachments/assets/aacbe871-3dbe-4d16-9b01-6900becb7bfe)

![Screenshot from 2024-11-26 22-38-34](https://github.com/user-attachments/assets/6a4bc617-77b6-4498-8cfc-49a51ec6deca)





