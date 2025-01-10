

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

---

`cd Desktop/hemanth/VLSI/VSDBabySOC/src/lib/`

<img width="739" alt="Screenshot 2024-11-08 at 12 12 58 PM" src="https://github.com/user-attachments/assets/6257df5a-5775-45dc-adc9-9d49a949f917">

---

Launch `lc_shell`

<img width="736" alt="Screenshot 2024-11-08 at 12 13 45 PM" src="https://github.com/user-attachments/assets/1ded9195-26bc-46f6-bab3-b68618b7fde3">

---

Reading avsddac library `read_lib avsddac.lib`
<img width="879" alt="Screenshot 2024-11-08 at 12 27 30 PM" src="https://github.com/user-attachments/assets/27e09272-de9b-47d7-b4c0-bfec5344352b">

---

writing  .db file `write_lib avsddac -format db -output avsddac.db`

<img width="881" alt="Screenshot 2024-11-08 at 12 24 58 PM" src="https://github.com/user-attachments/assets/3a41681b-6dc7-4764-a3f1-ceedd29608a1">

---

### Converting `avsdpll.lib` to `avsdpll.db`

---

`cd Desktop/hemanth/VLSI/VSDBabySOC/src/lib/`

<img width="739" alt="Screenshot 2024-11-08 at 12 12 58 PM" src="https://github.com/user-attachments/assets/6257df5a-5775-45dc-adc9-9d49a949f917">

---

Launch `lc_shell`

<img width="736" alt="Screenshot 2024-11-08 at 12 13 45 PM" src="https://github.com/user-attachments/assets/1ded9195-26bc-46f6-bab3-b68618b7fde3">

---

Reading avsdpll library `read_lib avsdpll.lib`

<img width="849" alt="Screenshot 2024-11-08 at 12 30 25 PM" src="https://github.com/user-attachments/assets/460d4dd9-9a34-4709-92d1-b96f8f0fd1cc">

---

Writing .db file `write_lib avsdpll -format db -output avsdpll.db`

<img width="845" alt="Screenshot 2024-11-08 at 12 31 36 PM" src="https://github.com/user-attachments/assets/0d554a72-714f-463a-b72c-8c987dee1b12">

---

### Converting sky130_fd_sc_hd__tt_025C_1v80.lib to sky130_fd_sc_hd__tt_025C_1v80.db

---

First, download the .lib file

`wget https://raw.githubusercontent.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/master/timing/sky130_fd_sc_hd__tt_025C_1v80.lib`

---

`cd Desktop/hemanth/VLSI/VSDBabySOC/src/lib/`

<img width="739" alt="Screenshot 2024-11-08 at 12 12 58 PM" src="https://github.com/user-attachments/assets/6257df5a-5775-45dc-adc9-9d49a949f917">

---

Launch `lc_shell`

<img width="736" alt="Screenshot 2024-11-08 at 12 13 45 PM" src="https://github.com/user-attachments/assets/1ded9195-26bc-46f6-bab3-b68618b7fde3">

---

Reading sky130_fd_sc_hd__tt_025C_1v80 library `read_lib sky130_fd_sc_hd__tt_025C_1v80.lib`

<img width="740" alt="Screenshot 2024-11-08 at 12 35 50 PM" src="https://github.com/user-attachments/assets/784655f2-6ecd-462c-922a-db7da234e2f1">

---

Writing .db file `write_lib sky130_fd_sc_hd__tt_025C_1v80 -format db -output sky130_fd_sc_hd__tt_025C_1v80.db`

<img width="1366" alt="Screenshot 2024-11-08 at 12 37 59 PM" src="https://github.com/user-attachments/assets/3493c817-12e6-4ba7-9cc4-29a9a504c38c">

---

## Running Synthesis and GLS

After setting up the libraries, proceed with synthesis and GLS.

### Synthesis

---

`cd Desktop/hemanth/VLSI/VSDBabySOC/src/lib/`

<img width="739" alt="Screenshot 2024-11-08 at 12 12 58 PM" src="https://github.com/user-attachments/assets/6257df5a-5775-45dc-adc9-9d49a949f917">

---

Launch `dc_shell`

<img width="1371" alt="Screenshot 2024-11-08 at 12 40 06 PM" src="https://github.com/user-attachments/assets/bc412639-c9e2-44d8-94e5-9fd0ae185eae">

---

`set target_library /home/bhaskar/vsd/VSDBabySOC/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db`

<img width="1002" alt="Screenshot 2024-11-08 at 12 30 49 AM" src="https://github.com/user-attachments/assets/f78b96ac-823b-496c-b1c3-3a9317fba1a3">

---

`set link_library {* /home/bhaskar/vsd/VSDBabySOC/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db /home/bhaskar/vsd/VSDBabySOC/VSDBabySoC/src/lib/avsdpll.db /home/bhaskar/vsd/VSDBabySOC/VSDBabySoC/src/lib/avsddac.db}`

<img width="1440" alt="Screenshot 2024-11-08 at 12 31 29 AM" src="https://github.com/user-attachments/assets/8fb0f3e5-369b-4d58-a050-5df452e1bb87">

---

`set search_path {/home/bhaskar/vsd/VSDBabySOC/VSDBabySoC/src/include /home/bhaskar/vsd/VSDBabySOC/VSDBabySoC/src/module}`

<img width="1440" alt="Screenshot 2024-11-08 at 12 31 41 AM" src="https://github.com/user-attachments/assets/a8bea31f-f957-4e8c-8f7e-ee751f2d575b">

---

`read_file {sandpiper_gen.vh  sandpiper.vh  sp_default.vh  sp_verilog.vh clk_gate.v rvmyth.v rvmyth_gen.v vsdbabysoc.v} -autoread -top vsdbabysoc`

<img width="1440" alt="Screenshot 2024-11-08 at 12 40 01 AM" src="https://github.com/user-attachments/assets/8d2512d6-200d-4053-88a1-0cef7f25fb95">

Statistics for MUX_OPs

<img width="718" alt="Screenshot 2024-11-08 at 12 43 37 AM" src="https://github.com/user-attachments/assets/2bdd1d49-96b2-4902-a77c-c1af4bd03b0f">

---

`link`

<img width="1123" alt="Screenshot 2024-11-08 at 12 43 44 AM" src="https://github.com/user-attachments/assets/ad81ef9d-9a39-4deb-a057-524f94ac781a">

---

`compile_ultra`

<img width="1157" alt="Screenshot 2024-11-08 at 12 44 06 AM" src="https://github.com/user-attachments/assets/fa786166-2502-4ef8-958a-39373eb15b83">

<img width="928" alt="Screenshot 2024-11-08 at 12 44 44 AM" src="https://github.com/user-attachments/assets/bfaff94f-a8a8-41c3-b134-6b279fa16339">

<img width="966" alt="Screenshot 2024-11-08 at 12 46 58 AM" src="https://github.com/user-attachments/assets/f1259856-decb-4364-8a4b-7e9c4210d46b">

---

`write_file -format verilog -hierarchy -output /home/bhaskar/vsd/VSDBabySOC/VSDBabySoC/output/vsdbabysoc_net.v`

<img width="1112" alt="Screenshot 2024-11-08 at 12 47 38 AM" src="https://github.com/user-attachments/assets/b2de7330-208f-456f-9025-161f6b77e253">

---

`report_qor > report_qor.txt`

<img width="337" alt="Screenshot 2024-11-08 at 12 53 03 AM" src="https://github.com/user-attachments/assets/65dc9f04-35d3-43b3-aabb-69e45a1a2cf2">

<img width="573" alt="Screenshot 2024-11-08 at 12 53 23 AM" src="https://github.com/user-attachments/assets/27ca650d-1379-490e-b37a-65f0ceaf14d4">

---

## Post-Synthesis Simulation

---

`iverilog -DFUNCTIONAL -DUNIT_DELAY=#1 -o ./output/post_synth_sim.out ./src/gls_model/primitives.v ./src/gls_model/sky130_fd_sc_hd.v ./output/vsdbabysoc_net.v ./src/module/avsdpll.v ./src/module/avsddac.v ./src/module/testbench.v`

<img width="1440" alt="Screenshot 2024-11-08 at 12 50 03 AM" src="https://github.com/user-attachments/assets/3c752e3c-578a-4f0f-89ec-d0e6cc5eaa4e">

---
Debug the errors
---

`./post_synth_sim.out`

<img width="437" alt="Screenshot 2024-11-08 at 12 50 24 AM" src="https://github.com/user-attachments/assets/da6b1b6f-fc58-4aea-909f-0e44d2dc1870">

----

gtkwave dump.vcd

<img width="1003" alt="Screenshot 2024-11-08 at 12 23 24 AM" src="https://github.com/user-attachments/assets/05bf53de-860d-49c0-ae15-eb4f15cfb384">

---

Verify Pre-Synthesis vs Post-Synthesis

<img width="544" alt="Screenshot 2024-11-08 at 12 56 27 PM" src="https://github.com/user-attachments/assets/40470752-b8ed-4381-9c6a-60682739ef38">

---

### Common Errors and Debugging Tips

  - Error: Port Not Defined (GND, VDD, VSSA, VDDA)
    - Ensure all necessary power and ground ports are defined in each module.
    - Add GND/VDD in avsdpll and VSSA/VDDA in avsddac, or set them as global nets if supported.
  - Syntax Errors in Library Files
    - Errors in .lib files (e.g., avsdpll.lib) can prevent .db conversion. Open the file and fix any issues (e.g., mismatched braces, missing parameters).
  - Warnings About Unresolved References
    - This often indicates missing or incorrectly linked files. Double-check file paths in dc_shell commands and the link_library and search_path settings.
  - Mismatched Waveforms Post-Synthesis
    - If waveform outputs differ between pre- and post-synthesis simulations, check for latch inferences or unintentional asynchronous behavior caused by synthesis.

---


















