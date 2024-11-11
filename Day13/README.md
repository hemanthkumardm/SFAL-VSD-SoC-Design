# VSDBabySoC: PVT Corner Timing Analysis and Synthesis with Constraints

## Overview

This project involves performing synthesis and timing analysis on the VSDBabySoC design with Synopsys DC using SDC constraints across multiple PVT (Process, Voltage, Temperature) corners. The goal is to validate the design across various operating conditions to ensure it meets timing requirements for robust operation.

### Key Terms
- **PVT Corners**: Different conditions under which a semiconductor device is tested to ensure it performs reliably. PVT stands for:
  - **Process**: Accounts for variations in manufacturing.
  - **Voltage**: Represents the different voltage levels the design might encounter.
  - **Temperature**: Represents the range of temperatures the design might experience.

By analyzing PVT corners, we can simulate the behavior of the SoC under various real-world conditions.

---

## Steps for Synthesis with SDC Constraints

### 1. Setting Up SDC Constraints
The constraints file, `vsdbabysoc_synthesis.sdc`, defines the design requirements for synthesis. Key constraints included:
- **Timing and Area**: Constraints to manage maximum area usage and ensure signal timings within a 10ns clock period.
- **Clock Specifications**: Configurations for clock latency, uncertainty, and input delays.
- **Input/Output Loads**: Defines acceptable input/output transition and load values.

### 2. Synthesis Commands
Run the following commands for synthesis with SDC constraints:

```bash
dc_shell
set target_library /path/to/sky130_fd_sc_hd__tt_025C_1v80.db
set link_library {* /path/to/sky130_fd_sc_hd__tt_025C_1v80.db /path/to/avsdpll.db /path/to/avsddac.db}
read_file {sandpiper_gen.vh sandpiper.vh sp_default.vh sp_verilog.vh clk_gate.v rvmyth.v rvmyth_gen.v vsdbabysoc.v} -autoread -top vsdbabysoc
link
read_sdc /path/to/vsdbabysoc_synthesis.sdc
compile_ultra
write_file -format verilog -hierarchy -output /output/vsdbabysoc_net_sdc.v
report_qor > report_qor_sdc.txt
report_timing -nets -attributes -input_pins -transition_time -delay_type max > report_setup_sdc.txt
report_timing -nets -attributes -input_pins -transition_time -delay_type min > report_hold_sdc.txt
