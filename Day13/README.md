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

---

`dc_shell`

<img width="1440" alt="Screenshot 2024-11-10 at 9 01 51 PM" src="https://github.com/user-attachments/assets/0925c0a4-f6f9-471c-a953-56b619a2afb6">

---

`set target_library /home/hemanth/Desktop/VLSI/VSDBbySoc/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db`

<img width="768" alt="Screenshot 2024-11-10 at 9 02 17 PM" src="https://github.com/user-attachments/assets/5fbe41fd-0ae3-41ba-bb3d-a6495567f337">

---

`set link_library {* /home/hemanth/Desktop/VLSI/VSDBbySoc/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db /home/hemanth/Desktop/VLSI/VSDBbySoc/src/lib/avsdpll.db /home/hemanth/Desktop/VLSI/VSDBbySoc/src/lib/avsddac.db}`

<img width="776" alt="Screenshot 2024-11-10 at 9 02 28 PM" src="https://github.com/user-attachments/assets/f3fdd206-8afe-44fc-8e51-c5cd1fdeb2f1">

---

`set search_path {/home/hemanth/Desktop/VLSI/VSDBabySoc/src/include /home/hemanth/Desktop/VLSI/VSDBabySoc/src/module}

<img width="902" alt="Screenshot 2024-11-10 at 9 03 27 PM" src="https://github.com/user-attachments/assets/d37ecd94-16e9-4511-a898-7b6741af997d">

---

`read_file {sandpiper_gen.vh sandpiper.vh sp_default.vh sp_verilog.vh clk_gate.v avsdpll.v avsddac.v vsdbabysoc.v} -autoread -top vsdbabysoc`

<img width="1061" alt="Screenshot 2024-11-11 at 10 33 28 AM" src="https://github.com/user-attachments/assets/8a420fc8-9a7f-4cd7-9b4a-eaaf9113a05e">

---

`link`

<img width="877" alt="Screenshot 2024-11-11 at 10 33 48 AM" src="https://github.com/user-attachments/assets/fd86ed4e-4cb7-4651-b65f-1c6a315bc1c7">

---

`read_sdc /home/hemanth/Desktop/VLSI/VSDBabySoc/src/sdc/vsdbabysoc_synthesis.sdc`

<img width="681" alt="Screenshot 2024-11-10 at 10 04 58 PM" src="https://github.com/user-attachments/assets/408844e6-decb-4bf1-b15d-4bd6ae6b113c">

---

`compile_ultra`

<img width="859" alt="Screenshot 2024-11-11 at 10 40 18 AM" src="https://github.com/user-attachments/assets/1eeb292c-7be7-4406-a13b-a1bb0f2a7dd6">

<img width="771" alt="Screenshot 2024-11-11 at 10 40 30 AM" src="https://github.com/user-attachments/assets/5eb04803-901f-4769-ac72-db0ed93d20b7">
---

`write_file -format verilog -hierarchy -output /output/vsdbabysoc_net_sdc.v`

<img width="646" alt="Screenshot 2024-11-11 at 10 42 50 AM" src="https://github.com/user-attachments/assets/d4cf071a-d39b-4936-afc5-90d527476195">m

---

`report_qor > report_qor_sdc.txt`

```txt
Information: Updating design information... (UID-85)
Information: Timing loop detected. (OPT-150)
        pll/U3/A pll/U3/Y
Warning: Disabling timing arc between pins 'A' and 'Y' on cell 'pll/U3'
         to break a timing loop. (OPT-314)

****************************************
Report : qor
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Mon Nov 11 05:13:38 2024
****************************************


  Timing Path Group 'clk'
  -----------------------------------
  Levels of Logic:              40.00
  Critical Path Length:          9.40
  Critical Path Slack:           0.01
  Critical Path Clk Period:     10.00
  Total Negative Slack:          0.00
  No. of Violating Paths:        0.00
  Worst Hold Violation:         -0.18
  Total Hold Violation:        -28.24
  No. of Hold Violations:      588.00
  -----------------------------------

  Timing Path Group 'default'
  -----------------------------------
  Levels of Logic:               0.00
  Critical Path Length:          0.87
  Critical Path Slack:           9.13
  Critical Path Clk Period:	  n/a
  Total Negative Slack:          0.00
  No. of Violating Paths:        0.00
  Worst Hold Violation:          0.00
  Total Hold Violation:          0.00
  No. of Hold Violations:        0.00
  -----------------------------------


  Cell Count
  -----------------------------------
  Hierarchical Cell Count:          2
  Hierarchical Port Count:        115
  Leaf Cell Count:               4050
  Buf/Inv Cell Count:             763
  Buf Cell Count:                  32
  Inv Cell Count:                 731
  CT Buf/Inv Cell Count:            0
  Combinational Cell Count:	 3374
  Sequential Cell Count:          676
  Macro Count:                      0
  -----------------------------------

  Area
  -----------------------------------
  Combinational Area:    21077.714814
  Noncombinational Area: 13534.229975
  Buf/Inv Area:           2981.609507
  Total Buffer Area:           232.72
  Total Inverter Area:        2748.89
  Macro/Black Box Area:      0.000000
  Net Area:                  0.000000
  -----------------------------------
  Cell Area:             34611.944788
  Design Area:           34611.944788


  Design Rules
  -----------------------------------
  Total Number of Nets:          4280
  Nets With Violations:             0
  Max Trans Violations:             0
  Max Cap Violations:               0
  -----------------------------------

  Hostname: sfalvsd

  Compile CPU Statistics
  -----------------------------------------
  Resource Sharing:                    7.19
  Logic Optimization:                  5.03
  Mapping Optimization:                5.62
  -----------------------------------------
  Overall Compile Time:               45.13
  Overall Compile Wall Clock Time:    45.95

  --------------------------------------------------------------------

  Design  WNS: 0.00  TNS: 0.00  Number of Violating Paths: 0


  Design (Hold)  WNS: 0.18  TNS: 28.24  Number of Violating Paths: 588

  --------------------------------------------------------------------

```

---

`report_timing -nets -attributes -input_pins -transition_time -delay_type max > report_setup_sdc.txt`

```txt

****************************************
Report : timing
        -path full
        -delay max
        -input_pins
        -nets
	-max_paths 1
        -transition_time
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Mon Nov 11 05:16:55 2024
****************************************

Operating Conditions: tt_025C_1v80   Library: sky130_fd_sc_hd__tt_025C_1v80
Wire Load Model Mode: top

  Startpoint: core/CPU_is_addi_a3_reg
              (rising edge-triggered flip-flop clocked by clk)
  Endpoint: core/CPU_Xreg_value_a4_reg[27][31]
            (rising edge-triggered flip-flop clocked by clk)
  Path Group: clk
  Path Type: max

  Des/Clust/Port     Wire Load Model	   Library
  ------------------------------------------------
  vsdbabysoc         Small                 sky130_fd_sc_hd__tt_025C_1v80

Attributes:
    d - dont_touch
    u - dont_use
   mo - map_only
   so - size_only
    i - ideal_net or ideal_network
  inf - infeasible path

  Point                                                    Fanout     Trans	 Incr       Path      Attributes
  ----------------------------------------------------------------------------------------------------------------------
  clock clk (rise edge)                                                          0.00       0.00
  clock network delay (ideal)                                                    3.00       3.00
  core/CPU_is_addi_a3_reg/CLK (sky130_fd_sc_hd__dfxtp_2)               0.00	 0.00       3.00 r
  core/CPU_is_addi_a3_reg/Q (sky130_fd_sc_hd__dfxtp_2)                 0.45	 0.59       3.59 r
  core/CPU_is_addi_a3 (net)                                 33                   0.00       3.59 r
  U496/A (sky130_fd_sc_hd__nor2_1)                                     0.45	 0.00       3.59 r
  U496/Y (sky130_fd_sc_hd__nor2_1)                                     0.09	 0.11       3.70 f
  n82 (net)                                                  2                   0.00       3.70 f
  U497/A (sky130_fd_sc_hd__nand2_1)                                    0.09	 0.00       3.71 f
  U497/Y (sky130_fd_sc_hd__nand2_1)                                    0.10	 0.12       3.82 r
  n79 (net)                                                  2                   0.00       3.82 r
  U53/A (sky130_fd_sc_hd__nand2_2)                                     0.10	 0.01       3.83 r
  U53/Y (sky130_fd_sc_hd__nand2_2)                                     0.29	 0.26       4.09 f
  n217 (net)                                                32                   0.00       4.09 f
  U499/B1 (sky130_fd_sc_hd__a22o_1)                                    0.29	 0.00       4.09 f
  U499/X (sky130_fd_sc_hd__a22o_1)                                     0.05	 0.28       4.37 f
  n80 (net)                                                  1                   0.00       4.37 f
  U500/A (sky130_fd_sc_hd__xor2_1)                                     0.05	 0.01       4.38 f
  U500/X (sky130_fd_sc_hd__xor2_1)                                     0.17	 0.17       4.55 f
  n152 (net)                                                 2                   0.00       4.55 f
  U610/A2 (sky130_fd_sc_hd__a21oi_1)                                   0.17	 0.00       4.56 f
  U610/Y (sky130_fd_sc_hd__a21oi_1)                                    0.20	 0.25       4.81 r
  n797 (net)                                                 2                   0.00       4.81 r
  U612/A2 (sky130_fd_sc_hd__o21ai_1)                                   0.20	 0.00       4.81 r
  U612/Y (sky130_fd_sc_hd__o21ai_1)                                    0.08	 0.11       4.93 f
  n779 (net)                                                 2                   0.00       4.93 f
  U616/A1 (sky130_fd_sc_hd__a21oi_1)                                   0.08	 0.00       4.93 f
  U616/Y (sky130_fd_sc_hd__a21oi_1)                                    0.20	 0.20       5.13 r
  n761 (net)                                                 2                   0.00       5.13 r
  U618/A2 (sky130_fd_sc_hd__o21ai_1)                                   0.20	 0.00       5.13 r
  U618/Y (sky130_fd_sc_hd__o21ai_1)                                    0.08	 0.11       5.25 f
  n743 (net)                                                 2                   0.00       5.25 f
  U623/A1 (sky130_fd_sc_hd__a21oi_1)                                   0.08	 0.00       5.25 f
  U623/Y (sky130_fd_sc_hd__a21oi_1)                                    0.20	 0.20       5.45 r
  n728 (net)                                                 2                   0.00       5.45 r
  U625/A2 (sky130_fd_sc_hd__o21ai_1)                                   0.20	 0.00       5.45 r
  U625/Y (sky130_fd_sc_hd__o21ai_1)                                    0.08	 0.11       5.57 f
  n707 (net)                                                 2                   0.00       5.57 f
  U630/A1 (sky130_fd_sc_hd__a21oi_1)                                   0.08	 0.00       5.57 f
  U630/Y (sky130_fd_sc_hd__a21oi_1)                                    0.20	 0.20       5.77 r
  n692 (net)                                                 2                   0.00       5.77 r
  U632/A2 (sky130_fd_sc_hd__o21ai_1)                                   0.20	 0.00       5.77 r
  U632/Y (sky130_fd_sc_hd__o21ai_1)                                    0.08	 0.11       5.89 f
  n674 (net)                                                 2                   0.00       5.89 f
  U637/A1 (sky130_fd_sc_hd__a21oi_1)                                   0.08	 0.00       5.89 f
  U637/Y (sky130_fd_sc_hd__a21oi_1)                                    0.20	 0.20       6.09 r
  n659 (net)                                                 2                   0.00       6.09 r
  U639/A2 (sky130_fd_sc_hd__o21ai_1)                                   0.20	 0.00       6.09 r
  U639/Y (sky130_fd_sc_hd__o21ai_1)                                    0.08	 0.11       6.21 f
  n641 (net)                                                 2                   0.00       6.21 f
  U360/A1 (sky130_fd_sc_hd__a21oi_1)                                   0.08	 0.00       6.21 f
  U360/Y (sky130_fd_sc_hd__a21oi_1)                                    0.20	 0.20       6.41 r
  n626 (net)                                                 2                   0.00       6.41 r
  U361/A2 (sky130_fd_sc_hd__o21ai_1)                                   0.20	 0.00       6.41 r
  U361/Y (sky130_fd_sc_hd__o21ai_1)                                    0.08	 0.11       6.53 f
  n608 (net)                                                 2                   0.00       6.53 f
  U38/A1 (sky130_fd_sc_hd__a21oi_1)                                    0.08	 0.00       6.53 f
  U38/Y (sky130_fd_sc_hd__a21oi_1)                                     0.20	 0.20       6.73 r
  n593 (net)                                                 2                   0.00       6.73 r
  U362/A2 (sky130_fd_sc_hd__o21ai_1)                                   0.20	 0.00       6.73 r
  U362/Y (sky130_fd_sc_hd__o21ai_1)                                    0.08	 0.11       6.85 f
  n575 (net)                                                 2                   0.00       6.85 f
  U37/A1 (sky130_fd_sc_hd__a21oi_1)                                    0.08	 0.00       6.85 f
  U37/Y (sky130_fd_sc_hd__a21oi_1)                                     0.20	 0.20       7.05 r
  n560 (net)                                                 2                   0.00       7.05 r
  U357/A2 (sky130_fd_sc_hd__o21ai_1)                                   0.20	 0.00       7.05 r
  U357/Y (sky130_fd_sc_hd__o21ai_1)                                    0.08	 0.11       7.17 f
  n542 (net)                                                 2                   0.00       7.17 f
  U95/A1 (sky130_fd_sc_hd__a21o_1)                                     0.08	 0.00       7.17 f
  U95/X (sky130_fd_sc_hd__a21o_1)                                      0.04	 0.17       7.35 f
  n525 (net)                                                 1                   0.00       7.35 f
  U1008/CIN (sky130_fd_sc_hd__fa_1)                                    0.04	 0.01       7.35 f
  U1008/COUT (sky130_fd_sc_hd__fa_1)                                   0.10	 0.39       7.74 f
  n511 (net)                                                 2                   0.00       7.74 f
  U93/A1 (sky130_fd_sc_hd__a21o_1)                                     0.10	 0.00       7.75 f
  U93/X (sky130_fd_sc_hd__a21o_1)                                      0.04	 0.18       7.93 f
  n494 (net)                                                 1                   0.00       7.93 f
  U971/CIN (sky130_fd_sc_hd__fa_1)                                     0.04	 0.01       7.94 f
  U971/COUT (sky130_fd_sc_hd__fa_1)                                    0.08	 0.37       8.31 f
  n479 (net)                                                 1                   0.00       8.31 f
  U367/CIN (sky130_fd_sc_hd__fa_1)                                     0.08	 0.01       8.31 f
  U367/COUT (sky130_fd_sc_hd__fa_1)                                    0.08	 0.38       8.70 f
  n464 (net)                                                 1                   0.00       8.70 f
  U4/CIN (sky130_fd_sc_hd__fa_1)                                       0.08	 0.01       8.71 f
  U4/COUT (sky130_fd_sc_hd__fa_1)                                      0.09	 0.39       9.09 f
  n449 (net)                                                 1                   0.00       9.09 f
  U36/CIN (sky130_fd_sc_hd__fa_2)                                      0.09	 0.01       9.10 f
  U36/COUT (sky130_fd_sc_hd__fa_2)                                     0.08	 0.36       9.46 f
  n435 (net)                                                 2                   0.00       9.46 f
  U88/A (sky130_fd_sc_hd__clkinv_1)                                    0.08	 0.00       9.47 f
  U88/Y (sky130_fd_sc_hd__clkinv_1)                                    0.03	 0.05       9.52 r
  n215 (net)                                                 1                   0.00       9.52 r
  U664/A2 (sky130_fd_sc_hd__o21ai_1)                                   0.03	 0.01       9.52 r
  U664/Y (sky130_fd_sc_hd__o21ai_1)                                    0.05	 0.05       9.57 f
  n417 (net)                                                 1                   0.00       9.57 f
  U889/CI (sky130_fd_sc_hd__fah_1)                                     0.05	 0.00       9.58 f
  U889/COUT (sky130_fd_sc_hd__fah_1)                                   0.06	 0.23       9.81 f
  n402 (net)                                                 1                   0.00       9.81 f
  U873/CI (sky130_fd_sc_hd__fah_1)                                     0.06	 0.00       9.81 f
  U873/COUT (sky130_fd_sc_hd__fah_1)                                   0.07	 0.26	   10.07 f
  n370 (net)                                                 1                   0.00	   10.07 f
  U3/CIN (sky130_fd_sc_hd__fa_1)                                       0.07	 0.01	   10.08 f
  U3/COUT (sky130_fd_sc_hd__fa_1)                                      0.08	 0.38	   10.46 f
  n344 (net)                                                 1                   0.00	   10.46 f
  U15/CIN (sky130_fd_sc_hd__fa_1)                                      0.08	 0.01	   10.47 f
  U15/COUT (sky130_fd_sc_hd__fa_1)                                     0.10	 0.40	   10.87 f
  n319 (net)                                                 2                   0.00	   10.87 f
  U670/A1 (sky130_fd_sc_hd__a21o_1)                                    0.10	 0.00	   10.87 f
  U670/X (sky130_fd_sc_hd__a21o_1)                                     0.04	 0.18	   11.05 f
  n291 (net)                                                 1                   0.00	   11.05 f
  U368/CIN (sky130_fd_sc_hd__fa_1)                                     0.04	 0.01	   11.06 f
  U368/COUT (sky130_fd_sc_hd__fa_1)                                    0.08	 0.37	   11.43 f
  n265 (net)                                                 1                   0.00	   11.43 f
  U366/CIN (sky130_fd_sc_hd__fa_1)                                     0.08	 0.01	   11.44 f
  U366/COUT (sky130_fd_sc_hd__fa_1)                                    0.08	 0.38	   11.82 f
  n222 (net)                                                 1                   0.00	   11.82 f
  U671/B (sky130_fd_sc_hd__xor2_1)                                     0.08	 0.01	   11.83 f
  U671/X (sky130_fd_sc_hd__xor2_1)                                     0.22	 0.21	   12.04 r
  n246 (net)                                                 2                   0.00	   12.04 r
  U672/A (sky130_fd_sc_hd__nand2_2)                                    0.22	 0.01	   12.04 r
  U672/Y (sky130_fd_sc_hd__nand2_2)                                    0.22	 0.19	   12.23 f
  n244 (net)                                                15                   0.00	   12.23 f
  U673/B2 (sky130_fd_sc_hd__o22ai_1)                                   0.22	 0.00	   12.23 f
  U673/Y (sky130_fd_sc_hd__o22ai_1)                                    0.18	 0.16	   12.39 r
  core/n3166 (net)                                           1                   0.00	   12.39 r
  core/CPU_Xreg_value_a4_reg[27][31]/D (sky130_fd_sc_hd__dfxtp_1)      0.18	 0.00	   12.40 r
  data arrival time                                                                        12.40

  clock clk (rise edge)                                                         10.00	   10.00
  clock network delay (ideal)                                                    3.00	   13.00
  clock uncertainty                                                             -0.50	   12.50
  core/CPU_Xreg_value_a4_reg[27][31]/CLK (sky130_fd_sc_hd__dfxtp_1)              0.00	   12.50 r
  library setup time                                                            -0.09	   12.41
  data required time                                                                       12.41
  ----------------------------------------------------------------------------------------------------------------------
  data required time                                                                       12.41
  data arrival time                                                                       -12.40
  ----------------------------------------------------------------------------------------------------------------------
  slack (MET)                                                                               0.01


  Startpoint: dac/OUT[0] (internal path startpoint)
  Endpoint: OUT[0] (output port)
  Path Group: default
  Path Type: max

  Des/Clust/Port     Wire Load Model	   Library
  ------------------------------------------------
  vsdbabysoc         Small                 sky130_fd_sc_hd__tt_025C_1v80

Attributes:
    d - dont_touch
    u - dont_use
   mo - map_only
   so - size_only
    i - ideal_net or ideal_network
  inf - infeasible path

  Point                        Fanout     Trans      Incr	Path	  Attributes
  ------------------------------------------------------------------------------------------
  input external delay                               0.00	0.00 r
  dac/OUT[0] (avsddac)                               0.00	0.00 r
  OUT[0] (net)                                       0.00	0.00 r
  OUT[0] (out)                             1.34      0.87	0.87 r
  data arrival time                                             0.87

  max_delay                                         10.00      10.00
  output external delay                              0.00      10.00
  data required time                                           10.00
  ------------------------------------------------------------------------------------------
  data required time                                           10.00
  data arrival time                                            -0.87
  ------------------------------------------------------------------------------------------
  slack (MET)                                                   9.13
```

---

`report_timing -nets -attributes -input_pins -transition_time -delay_type min > report_hold_sdc.txt`

```txt

****************************************
Report : timing
        -path full
        -delay min
        -input_pins
        -nets
	-max_paths 1
        -transition_time
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Mon Nov 11 05:16:47 2024
****************************************

Operating Conditions: tt_025C_1v80   Library: sky130_fd_sc_hd__tt_025C_1v80
Wire Load Model Mode: top

  Startpoint: core/CPU_is_addi_a2_reg
              (rising edge-triggered flip-flop clocked by clk)
  Endpoint: core/CPU_is_addi_a3_reg
            (rising edge-triggered flip-flop clocked by clk)
  Path Group: clk
  Path Type: min

  Des/Clust/Port     Wire Load Model	   Library
  ------------------------------------------------
  vsdbabysoc         Small                 sky130_fd_sc_hd__tt_025C_1v80

Attributes:
    d - dont_touch
    u - dont_use
   mo - map_only
   so - size_only
    i - ideal_net or ideal_network
  inf - infeasible path

  Point                                           Fanout     Trans	Incr	   Path      Attributes
  -------------------------------------------------------------------------------------------------------------
  clock clk (rise edge)                                                 0.00	   0.00
  clock network delay (ideal)                                           3.00	   3.00
  core/CPU_is_addi_a2_reg/CLK (sky130_fd_sc_hd__dfxtp_1)      0.00	0.00	   3.00 r
  core/CPU_is_addi_a2_reg/Q (sky130_fd_sc_hd__dfxtp_1)        0.04	0.28	   3.28 r
  core/CPU_is_addi_a2 (net)                         1                   0.00	   3.28 r
  core/CPU_is_addi_a3_reg/D (sky130_fd_sc_hd__dfxtp_2)        0.04	0.00	   3.28 r
  data arrival time                                                                3.28

  clock clk (rise edge)                                                 0.00	   0.00
  clock network delay (ideal)                                           3.00	   3.00
  clock uncertainty                                                     0.50	   3.50
  core/CPU_is_addi_a3_reg/CLK (sky130_fd_sc_hd__dfxtp_2)                0.00	   3.50 r
  library hold time                                                    -0.04	   3.46
  data required time                                                               3.46
  -------------------------------------------------------------------------------------------------------------
  data required time                                                               3.46
  data arrival time                                                               -3.28
  -------------------------------------------------------------------------------------------------------------
  slack (VIOLATED)                                                                -0.18
```

---

### 3. Post-Synthesis Simulation on Constraints data

```tcl
iverilog -DFUNCTIONAL -DUNIT_DELAY=#1 -o ./output/post_synth_sdc_sim.out ./src/gls_model/primitives.v ./src/gls_model/sky130_fd_sc_hd.v ./output/vsdbabysoc_net_sdc.v ./src/module/avsdpll.v ./src/module/avsddac.v ./src/module/testbench.v
./post_synth_sim.out
gtkwave dump.vcd
```

<img width="1440" alt="Screenshot 2024-11-10 at 10 23 01 PM" src="https://github.com/user-attachments/assets/067f1a6e-112a-4d7d-ae24-891e21df4db8">

---

# PVT Corners and Timing Analysis

---

## What are PVT Corners?

PVT Corners represent the extremes of Process, Voltage, and Temperature conditions:

  - Process Corners: Variations in manufacturing can lead to Fast (F), Typical (T), or Slow (S) transistor speeds.
  - Voltage Corners: The design’s voltage can vary, with nominal (N), high (H), and low (L) values.
  - Temperature Corners: Temperature affects semiconductor performance, with testing at low, typical, and high extremes.

By analyzing these corners, we ensure the design is robust under diverse conditions.

## Generating PVT Timing Libraries

  - **Download Libraries:** Obtain .lib files for different corners from [Skywater PDK timing libraries](https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/tree/master/timing).
  - **Convert .lib to .db:** Using Synopsys LC Shell, convert the .lib files to .db format for use in synthesis.

---

## Script to convert .lib files to .db

Create a bash file `nano conversion.sh`.

```bash
#!/bin/sh

LC_SHELL_PATH="/usr/synopsys/lc/T-2022.03-SP5/bin/lc_shell"
TCL_SCRIPT="lib2db.tcl"

#Execute the lc_shell with the specified TCL script
$LC_SHELL_PATH -f $TCL_SCRIPT
```

<img width="737" alt="Screenshot 2024-11-11 at 5 28 29 PM" src="https://github.com/user-attachments/assets/80664bb4-aa98-4991-9a11-74701176c76f">

---

Make diretory `mkdir db_files`
Create TCL file `nano lib2db.tcl`.

```tcl
# convert_lib_to_db.tcl
set lib_files_dir "/home/hemanth/Desktop/VLSI/VSDBabySoc/src/Timing/timing";
set db_output_dir "/home/hemanth/Desktop/VLSI/VSDBabySoc/src/db_files";
foreach lib_file [glob -nocomplain $lib_files_dir/*.lib] {
set base_name [file rootname [file tail $lib_file]]
set db_file "$db_output_dir/${base_name}.db"

if {[llength [list_libs]] > 0} {
    remove_lib [lindex [list_libs] 0]
}

read_lib $lib_file

write_lib $base_name -format db -output $db_file

if {[llength [list_libs]] > 0} {
    remove_lib [lindex [list_libs] 0]
}
}
exit
```

<img width="650" alt="Screenshot 2024-11-11 at 5 30 02 PM" src="https://github.com/user-attachments/assets/09ee4d59-e7c1-456c-9657-d61d2ea2e842">

---

run `./conversion.sh

--- 

## Output in db_files

<img width="1440" alt="Screenshot 2024-11-11 at 5 31 47 PM" src="https://github.com/user-attachments/assets/e7dce70d-b3ee-4899-a905-926a8ad526a2">

---

## Multi-PVT Corner Synthesis Script

---

Create bash file `nano pvt_corners.sh`

```bash
#!/bin/bash
TCL_SCRIPT_PATH="/home/hemanth/Desktop/VLSI/VSDBabySoc/src/script/pvt_corners.tcl"
LOG_FILE="/home/hemanth/Desktop/VLSI/VSDBabySoc/src/dc_shell.log"

# Run the TCL script within dc_shell
dc_shell -f $TCL_SCRIPT_PATH | tee $LOG_FILE
```

<img width="659" alt="Screenshot 2024-11-11 at 5 33 20 PM" src="https://github.com/user-attachments/assets/ac9ffe7f-9e05-4fde-a6c4-2db541e49879">

---

To perform synthesis across multiple PVT corners.

`cd script`
Create TCL file `pvt_corners.tcl`

```tcl
# timing_multi_pvt_corners.tcl
set file_handle [open report_timing.rpt w]
puts $file_handle "PVT_Corner\tWNS\tWHS"

set lib_files [glob -directory /home/hemanth/Desktop/VLSI/VSDBabySoc/src/db_files/ -type f *.db]

foreach lib_file_paths $lib_files {

regexp {.*\/sky130_fd_sc_hd__(.*)\.db$} $lib_file_paths full_match pvt_corners

set timing_report_fast_mode true

set target_library $lib_file_paths
set link_library {* /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsdpll.db /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsddac.db}
lappend link_library $target_library
set search_path {/home/hemanth/Desktop/VLSI/VSDBabySoc/src/include /home/hemanth/Desktop/VLSI/VSDBabySoc/src/module}
read_file {sandpiper_gen.vh  sandpiper.vh  sp_default.vh  sp_verilog.vh clk_gate.v rvmyth.v rvmyth_gen.v vsdbabysoc.v} -autoread -top vsdbabysoc
read_sdc /home/hemanth/Desktop/VLSI/VSDBabySoc/src/sdc/vsdbabysoc_synthesis.sdc
link
compile_ultra

set wns [get_attribute [get_timing_paths -delay_type max -max_paths 1] slack]
set whs [get_attribute [get_timing_paths -delay_type min -max_paths 1] slack]

puts $file_handle "$pvt_corners\t$wns\t$whs"

reset_design
}

close $file_handle
exit
```

<img width="1103" alt="Screenshot 2024-11-11 at 5 35 54 PM" src="https://github.com/user-attachments/assets/fb98f8a6-0e53-43e7-ab22-907bf73baed8">

---

run `pvt_corners.sh`

---

`nano report_timing.rpt`

<img width="708" alt="Screenshot 2024-11-11 at 5 42 18 PM" src="https://github.com/user-attachments/assets/c941623c-634d-41dd-96ff-907d2fb9264a">

---

# Timing Analysis Report for VSDBabySoC

This report provides an analysis of timing slack values across various Process, Voltage, and Temperature (PVT) corners for the VSDBabySoC. 

## PVT Timing Report Table

| PVT Corner       | Worst Negative Slack (WNS) | Worst Hold Slack (WHS) |
|------------------|----------------------------|-------------------------|
| ff_100C_1v65     | 0.0046                     | -0.2449                |
| ff_100C_1v95     | 0.2279                     | -0.2986                |
| ff_n40C_1v56     | 0.0493                     | -0.2017                |
| ff_n40C_1v65     | 0.0183                     | -0.2386                |
| ff_n40C_1v76     | 0.0322                     | -0.2698                |
| ff_n40C_1v95     | 0.0913                     | -0.3071                |
| ss_100C_1v40     | 0.0060                     | 0.4140                 |
| ss_100C_1v60     | 1.7014                     | 0.1493                 |
| ss_n40C_1v28     | -2.1464                    | 1.2782                 |
| ss_n40C_1v35     | 0.0016                     | 0.8259                 |
| ss_n40C_1v40     | 0.0035                     | 0.6072                 |
| ss_n40C_1v44     | 0.0013                     | 0.4990                 |
| ss_n40C_1v60     | 0.0063                     | 0.1696                 |
| ss_n40C_1v76     | 0.0054                     | -0.0056                |
| tt_025C_1v80     | 0.1988                     | -0.1840                |
| tt_100C_1v80     | 0.0027                     | -0.1792                |

--- 

## Analysis of the Timing Report

Each row in the report lists:

  - PVT Corner: Indicates the specific process, voltage, and temperature condition tested.
  - Worst Negative Slack (WNS): The most negative slack value for setup timing (data arriving late).
    - Goal: Keep WNS close to zero or positive, meaning data arrives on time.
  - Worst Hold Slack (WHS): The worst slack for hold timing (data held too long).
    - Goal: Ensure WHS is positive or minimal, indicating stability of data until the next clock edge.

---

### Key Observations

- **Fast-Fast Corners (`ff`)**:
  - The **WNS** values are positive, indicating that setup timing is generally met in fast process conditions.
  - The **WHS** values are negative in most cases, particularly at higher voltages (e.g., `ff_n40C_1v95`), suggesting potential hold timing violations. Negative WHS means data may not be stable long enough before the next clock edge.

- **Slow-Slow Corners (`ss`)**:
  - **WNS** is positive for most corners, except for `ss_n40C_1v28` (-2.1464), indicating a setup timing issue at very low voltage.
  - **WHS** is generally positive or near zero, implying that hold timing is likely met at slower conditions.

### Interpretation for Design Robustness

- **Negative WHS** indicates a need for hold-time buffers in cases like the fast-fast (ff) corners.
- **Negative WNS** points to setup timing issues that may benefit from optimizing the logic path or pipeline stages.

### Selected PVT Corners for Detailed Analysis

To verify robustness, the following corners were chosen:
1. **ss_n40C_1v28 with WNS of -2.14636**: Extreme slow process at low temperature and voltage for worst-case setup timing analysis.
2. **ff_100C_1v95 with WHS of -0.307088**: Fast process at high temperature and voltage for hold timing stability during peak performance.

---

### Graphs

---

**WNS vs PVT_corners**

![WNS vs  PVT_Corner](https://github.com/user-attachments/assets/0a69b123-6a39-4ef9-9af4-d29f1e4e150c)

---

**WHS vs PVT_corners**

![   WHS vs  PVT_Corner](https://github.com/user-attachments/assets/f313be48-ddbd-4fb3-92a7-9bc5d75480bb)

---

**WHS and WNS**

![   WHS and WNS](https://github.com/user-attachments/assets/169494cf-a5c9-4e76-97a0-b3a99db2a041)

---

### 










