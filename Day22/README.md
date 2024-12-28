# Understanding ECO in VLSI Design

## What is ECO?

ECO stands for **Engineering Change Order**, a process used to make changes to the design of a chip even after it has gone through important stages like synthesis, placement, and routing. The goal of an ECO is to fix problems, improve performance, or meet new design requirements without starting the design process from scratch. This helps save time and ensures the chip can be released to the market faster.

---

## Types of ECO

There are two main types of ECOs based on the level of changes made to the chip:

1. **All Layers ECO**:
   - Involves changes across all parts of the chip, including the base and metal layers.
   - Used for big changes, such as replacing large components (hard macros) or making major updates.

2. **Metal-Only ECO**:
   - Focuses on changes only to the metal layers of the chip.
   - Preferred when smaller updates are needed, as it is cheaper and faster than changing the base layers.

---

## Steps in the ECO Process

The ECO process has a few important steps:

1. **Define the Changes**:
   - First, decide what needs to be fixed or updated in the design.

2. **Compare Netlists**:
   - Compare the updated design (new netlist) with the original design (golden netlist) to find the differences.

3. **Placement and Routing**:
   - Adjust the placement of new components and update the routing (connections) to fit the changes.

4. **Verification**:
   - Check if the design works as expected after the changes and ensure no new issues are introduced.

---

## Why is ECO Important?

ECO helps save time and costs because it avoids restarting the entire design process. This is especially important in the competitive semiconductor industry, where launching products quickly is essential.

---

## Challenges in ECO

Even though ECO is helpful, it can be tricky to implement because:
- Designs are very complex and have tight physical space constraints.
- Manual changes take a lot of time and are error-prone.

To address these issues, companies are working on better ECO tools that can automate the process and handle modern, complicated designs efficiently.

---

## LABS

Script to setup Prime Time for ECO run `nano prime.tcl`

```tcl
set link_path "* /home/hemanth/Desktop/VLSI/VSDBabySoc/src/Timing/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.db /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsdpll.db /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsddac.db"

read_verilog /home/hemanth/Desktop/VLSI/VSDBabySoc/output/vsdbabysoc_post_route_net_max_cap.v
current_design vsdbabysoc
link_design
set_min_library -min_version /home/hemanth/Desktop/VLSI/VSDBabySoc/src/Timing/timing_libs/sky130_fd_sc_hd__ff_n40C_1v95.db /home/hemanth/Desktop/VLSI/VSDBabySoc/src/Timing/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.db

read_sdc /home/hemanth/Desktop/VLSI/VSDBabySoc/output/vsdbabysoc_post_route.sdc
#read_parasitics /home/hemanth/Desktop/VLSI/VSDBabySoc/output/vsdbabysoc_parasitics.temp1_25.spef
read_parasitics /home/hemanth/Desktop/VLSI/VSDBabySoc/output/vsdbabysoc_parasitics_max_cap.temp1_25.spef

update_timing -full

report_analysis_coverage > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/prime_time_analysis_coverage.rpt
report_constraint -all_violators > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/prime_time_constraint.rpt
report_timing -delay_type max -capacitance -input_pins -nets -transition_time -nosplit -significant_digits 4 > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/prime_time_setup_timing.rpt
report_timing -delay_type min -capacitance -input_pins -nets -transition_time -nosplit -significant_digits 4 > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/prime_time_hold_timing.rpt
```

Open `less /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/prime_time_analysis_coverage.rpt`

<img width="579" alt="before 1st iteration" src="https://github.com/user-attachments/assets/fbc54d33-aa60-4d29-bc33-0fae94bc0320" />

# **Fixing Timing Violations Using ECO in PrimeTime**

This document explains how to **fix timing violations** using the **`fix_eco_timing`** command in **PrimeTime**. It also describes how to generate and apply an **Engineering Change Order (ECO)** script to update your design in another tool, such as **Design Compiler (DC)**, **IC Compiler (ICC)**, or **IC Compiler II (ICC2)**.

---

## **1. What is Timing Violation?**

Timing violations occur when signals in a circuit fail to meet **setup time** or **hold time** requirements during data transfers.

- **Setup Time Violation:**  
  The data signal arrives **too late** at the destination register and cannot be captured in the current clock cycle.

- **Hold Time Violation:**  
  The data signal arrives **too early** and might overwrite the previously captured value, leading to **data corruption**.

---

## **2. Fixing Timing Violations with `fix_eco_timing`**

The **`fix_eco_timing`** command helps **fix or reduce** these violations by:  
1. **Resizing cells** (changing drive strength).  
2. **Inserting buffers** to delay the signal path.  
3. **Inserting inverter pairs** to control signal transitions.

The tool minimizes the impact on **area** and **power** while focusing on **timing improvement**.

---

## **3. Engineering Change Order (ECO)**

- An **ECO** is a **list of design modifications** needed to fix timing issues.  
- After fixing violations, the changes are exported as a **script** using the **`write_changes`** command.  
- This script can be reused to **apply the changes** in:  
  - **PrimeTime**  
  - **Design Compiler**  
  - **IC Compiler**  
  - **IC Compiler II**  

---

## **4. Options in `fix_eco_timing` Command**

The **`fix_eco_timing`** command has multiple options to control how violations are fixed. Key options include:

### **4.1 Fix Types**
- **`-type setup`** - Fix **setup violations** (reduce delays).  
- **`-type hold`** - Fix **hold violations** (increase delays).

### **4.2 Scope of Fixing**
- **Entire Design:** Fix violations across the **whole design**.  
- **Specific Paths:** Focus on **critical paths** between specific start and endpoints.  

### **4.3 Methods of Fixing**
- **Cell Sizing:** Changes the **drive strength** of cells.  
- **Buffer Insertion:** Adds **buffers** to **delay signals**.  
- **Inverter Pair Insertion:** Adds **inverter pairs** to **adjust signal transitions**.

### **4.4 Buffer Library**
- Specify the **buffer types** to use, for example:
- buffer_list {sky130_fd_sc_hd__buf_1 sky130_fd_sc_hd__buf_2}

### **4.5 Types of Cells Modified**
- **Data Paths Only (default):** Focuses only on data signal paths.  
- **Sequential Cells:** Allows changes to **flip-flops** or **registers**.  
- **Clock Networks:** Enables modifications to **clock trees**.

### **4.6 Slack Target**
- Set a **target slack value** to achieve, such as:
- target_slack 0.1

### **4.7 Analysis Modes**
- **Graph-Based Analysis:** Faster and approximates results.  
- **Path-Based Analysis:** Slower but provides **accurate results**.  
- **Exhaustive Path Analysis:** Checks all paths thoroughly.

---

## **5. Fixing Violations - Step-by-Step Example**

### **Step 1: Fix Setup Violations**
```tcl
fix_eco_timing -type setup \
-methods cell_sizing \
-target_slack 0.1
```

<img width="1231" alt="fix-eco -setup 1" src="https://github.com/user-attachments/assets/a8143e21-6649-454f-b73b-3da870eb6d6c" />

<img width="464" alt="fix-setup 1" src="https://github.com/user-attachments/assets/78c9b4e2-b060-48c2-bc28-a2ae0300b5f6" />

## Step 2: Fix Hold Violations

`fix_eco_timing -type hold -methods insert_buffer -buffer_list {sky130_fd_sc_hd__buf_1 sky130_fd_sc_hd__buf_2 sky130_fd_sc_hd__buf_4 sky130_fd_sc_hd__buf_8}`

<img width="1185" alt="fix-eco -hold 1" src="https://github.com/user-attachments/assets/baaf76ab-e6cf-480b-8f1b-0940d44adb1c" />

<img width="442" alt="fix-hold 1" src="https://github.com/user-attachments/assets/5401a23f-4904-493e-ac98-4c78b2f03926" />

## Step 3: Export Changes as ECO Script

`write_changes -format icc2tcl -output output/vsdbabysoc_eco.tcl`

## Step 4: Apply Changes in ICC2

`icc2_shell> source output/vsdbabysoc_eco.tcl`

# **Post-ECO Timing Verification Using PrimeTime**

This guide explains how to verify timing after applying **Engineering Change Order (ECO)** fixes using **PrimeTime (PT)**. It includes steps to **legalize placement**, **route ECO changes**, and re-run **Static Timing Analysis (STA)** to confirm that timing violations are resolved.

---

## **1. Applying ECO Changes in ICC2**

### **Step 1: Source the ECO Script**

Load the generated ECO script into the **ICC2 tool**:
```tcl
source vsdbabysoc_eco.tcl
```

### Step 2: Legalize Placement

After sourcing the ECO script, placement might become illegal due to overlapping cells or misalignment.
Use the following command to legalize placement:

`check_legality`

![check_legality](https://github.com/user-attachments/assets/5ededc8b-d9e9-4cc3-bc16-8ee85f9663b8)

`legalize_placement`

<img width="1440" alt="legalize_placement" src="https://github.com/user-attachments/assets/454dc267-1885-4598-9861-4705f589d999" />

   - If placement is still illegal, review the errors using:

`report_legality`

### Step 3: Perform ECO Routing

**1: Route Newly Added Nets**

After legalizing placement, we must route the new nets created during ECO:

`route_eco`

### Step 4: Extract Updated Database

`write_verilog -output post_route_netlist.v`
`write_parasitics -output post_route.spef`

modify the prime_time_sta.tcl with new generated parasitics and netlist files as follows:

```tcl
set link_path "* /home/hemanth/Desktop/VLSI/VSDBabySoc/src/Timing/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.db /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsdpll.db /home/hemanth/Desktop/VLSI/VSDBabySoc/src/lib/avsddac.db"

read_verilog /home/hemanth/Desktop/VLSI/VSDBabySoc/output/vsdbabysoc__post_eco_net.v
current_design vsdbabysoc
link_design
set_min_library -min_version /home/hemanth/Desktop/VLSI/VSDBabySoc/src/Timing/timing_libs/sky130_fd_sc_hd__ff_n40C_1v95.db /home/hemanth/Desktop/VLSI/VSDBabySoc/src/Timing/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.db

read_sdc /home/hemanth/Desktop/VLSI/VSDBabySoc/output/vsdbabysoc_post_route.sdc
#read_parasitics /home/hemanth/Desktop/VLSI/VSDBabySoc/output/vsdbabysoc_parasitics.temp1_25.spef
read_parasitics /home/hemanth/Desktop/VLSI/VSDBabySoc/output/vsdbabysoc_parasitics_post_eco.temp1_25.spef

update_timing -full

report_analysis_coverage > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/prime_time_analysis_coverage.rpt
report_constraint -all_violators > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/prime_time_constraint.rpt
report_timing -delay_type max -capacitance -input_pins -nets -transition_time -nosplit -significant_digits 4 > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/prime_time_setup_timing.rpt
report_timing -delay_type min -capacitance -input_pins -nets -transition_time -nosplit -significant_digits 4 > /home/hemanth/Desktop/VLSI/VSDBabySoc/reports/prime_time_hold_timing.rpt
```

# First Iteration

<img width="585" alt="Screenshot 2024-12-21 at 10 20 25 AM" src="https://github.com/user-attachments/assets/b62cae47-c609-4f7a-947a-6f6ea3a4dbcd" />

<img width="453" alt="Screenshot 2024-12-21 at 4 26 43 PM" src="https://github.com/user-attachments/assets/664d4159-74cd-43e8-8f95-21d9f59ea2a0" />

# Second Iteration

<img width="652" alt="Screenshot 2024-12-21 at 2 14 59 PM" src="https://github.com/user-attachments/assets/c7899aac-43a2-4d01-9cdc-f1fbc7f9e90e" />

<img width="454" alt="Screenshot 2024-12-21 at 4 27 02 PM" src="https://github.com/user-attachments/assets/0b9b2410-bfa1-451a-838f-70390cee72e9" />

# Third Iteration

<img width="637" alt="Screenshot 2024-12-21 at 2 24 36 PM" src="https://github.com/user-attachments/assets/7dd3acb9-ec91-47fa-8f2c-81bd042f8953" />

<img width="453" alt="Screenshot 2024-12-21 at 4 27 20 PM" src="https://github.com/user-attachments/assets/c3061c80-7675-4f2c-be75-07900476baaa" />

# Graphical Outputs

<img width="910" alt="Screenshot 2024-12-21 at 4 26 16 PM" src="https://github.com/user-attachments/assets/76156728-85d3-4f0a-8e66-d8ef624d96f9" />


# Fourth Iteration [modified `set_min_library -min_version /home/hemanth/Desktop/VLSI/VSDBabySoc/src/Timing/timing_libs/sky130_fd_sc_hd__ss_n40C_1v28.db` and /home/hemanth/Desktop/VLSI/VSDBabySoc/src/Timing/timing_libs/sky130_fd_sc_hd__ss_n40C_1v28.db]

<img width="637" alt="Screenshot 2024-12-21 at 2 24 36 PM" src="https://github.com/user-attachments/assets/7dd3acb9-ec91-47fa-8f2c-81bd042f8953" />

<img width="453" alt="Screenshot 2024-12-21 at 4 27 20 PM" src="https://github.com/user-attachments/assets/c3061c80-7675-4f2c-be75-07900476baaa" />

# Graphical Outputs

<img width="910" alt="Screenshot 2024-12-21 at 4 26 16 PM" src="https://github.com/user-attachments/assets/76156728-85d3-4f0a-8e66-d8ef624d96f9" />















