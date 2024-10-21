# Day 2: Introduction to Verilog RTL Design and Synthesis

## Overview
we focused on Verilog RTL design and synthesis using tools like Iverilog and Yosys, within the SKY130 process design kit (PDK).

## Tasks Completed

### 1. Introduction to Open-Source Simulator Iverilog

- **Key Concepts**:
  - **Simulator**: A tool used to check the design of RTL (Register Transfer Level). The tool used for this purpose is Iverilog.
  - **Design**: It refers to the Verilog code or a set of Verilog codes that implement the intended functionality to meet the required specifications.
  - **Testbench**: A setup used to apply test vectors to the design to verify its functionality.

- **How It Works**:
  - The simulator looks for changes in the input signals.
  - If there is a change in the input, the output is evaluated.
  - If there is no change to the input, there is no change to the output.
  
- **Design Structure**:
  - The design may have one or more primary inputs and one or more primary outputs.
  - The testbench does not have primary inputs or outputs.

- **Iverilog Based Simulation Flow**:
  - Both the design and the testbench are given to Iverilog.
  - Iverilog generates a VCD file (Value Change Dump file), which is then provided to GTKWave for waveform visualization.
  
### 2. Labs Using Iverilog and GTKWave
Load latch & its testbench to Iverilog and a.out file is executed
<img width="1440" alt="Screenshot 2024-10-21 at 6 32 26 PM" src="https://github.com/user-attachments/assets/f5c09d2d-8663-42db-854b-53cda992bac6">

Loading the .vcd file into GTKWave generator.
<img width="1440" alt="Screenshot 2024-10-21 at 6 33 35 PM" src="https://github.com/user-attachments/assets/475d843e-b965-4af9-a84b-c81a4ed22ae8">


### 3. Introduction to Yosys and Logic Synthesis

  
### 4. Labs Using Yosys and Sky130 PDKs


## Challenges Faced


## Next Steps


## Resources

