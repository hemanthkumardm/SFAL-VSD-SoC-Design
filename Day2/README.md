# Day 2: Introduction to Verilog RTL Design and Synthesis

## Overview
On Day 2, the focus was on Verilog RTL design and synthesis using tools like Iverilog and Yosys within the SKY130 process design kit (PDK).

## Tasks Completed

<details>
    <summary>1. Introduction to Open-Source Simulator Iverilog</summary>

- **Key Concepts**:
  - **Simulator**: A tool used to check the design of RTL (Register Transfer Level). The tool used for this purpose is Iverilog.
  - **Design**: Verilog code or a set of Verilog codes that implement the intended functionality to meet required specifications.
  - **Testbench**: A setup used to apply test vectors to the design to verify its functionality.

- **How It Works**:
  - The simulator checks for changes in input signals.
  - If there is a change in input, the output is evaluated.
  - If no input changes, there is no change in output.

- **Design Structure**:
  - The design may have one or more primary inputs and one or more primary outputs.
  - The testbench does not have primary inputs or outputs.

- **Iverilog-Based Simulation Flow**:
  - Both the design and the testbench are given to Iverilog.
  - Iverilog generates a VCD (Value Change Dump) file, which is then provided to GTKWave for waveform visualization.
</details>

<details>
    <summary>2. Labs Using Iverilog and GTKWave</summary>

- **Steps**:
  1. Load the latch and its testbench into Iverilog, then execute the `a.out` file.
     
     ![Latch Testbench](https://github.com/user-attachments/assets/f5c09d2d-8663-42db-854b-53cda992bac6)

  2. Load the `.vcd` file into GTKWave for waveform visualization.
     
     ![GTKWave Visualization](https://github.com/user-attachments/assets/475d843e-b965-4af9-a84b-c81a4ed22ae8)
</details>

<details>
    <summary>3. Introduction to Yosys and Logic Synthesis</summary>

#### Introduction to Yosys
- **Yosys**: A tool used to convert RTL into a netlist.
  - **Netlist**: Represents the design in terms of cells from the `.lib` (library) file.

    ![Yosys Tool](https://github.com/user-attachments/assets/50f13129-e000-45fc-a638-e76b554b804e)

- **Verification of Synthesis**:
  - The primary inputs and outputs of the synthesized netlist remain the same as in the RTL design, meaning the same testbench can be used.

    ![Netlist Verification](https://github.com/user-attachments/assets/2d289936-912b-4a13-a402-af55b73aeeab)

#### Introduction to Logic Synthesis
1. **RTL Design**: Behavioral representation of the required specification.

   ![RTL Design](https://github.com/user-attachments/assets/8af7b724-9f76-45aa-a56b-21fbd58f2757)

2. **Synthesis**: Conversion of RTL to gate-level, where the design is transformed into gates with interconnections.

3. **Netlist**: The output of the synthesis process, consisting of gates and their interconnections.

   ![Netlist](https://github.com/user-attachments/assets/1d80cc79-2931-4b27-9eae-fd5b9301cdee)

4. **.lib**: A collection of logical modules, including basic logic gates (e.g., AND, OR, NOT). Different flavors of the same gate exist (e.g., slow, medium, fast versions).

5. **Why Different Flavors of Gates?**: Faster cells are used for performance, while slower cells meet hold time constraints.
   ![Fast cells](https://github.com/user-attachments/assets/44928f5d-7fd3-4ecd-9e95-cf905cde974b)
   ![Slow cells](https://github.com/user-attachments/assets/9141d461-acad-4b9b-9467-958ab1a6f605)
7. **Selection of cells.
<img width="1042" alt="Screenshot 2024-10-22 at 9 53 13 AM" src="https://github.com/user-attachments/assets/080568c9-13af-4340-8448-a80009099884">
8. **Synthesis.
<img width="1059" alt="Screenshot 2024-10-22 at 9 54 08 AM" src="https://github.com/user-attachments/assets/97a840ad-cc7b-49de-a7c3-81874f6f25fb">

   
</details>




<details>
    <summary>4. Labs Using Yosys and SKY130 PDKs</summary>

#### Part 1
- **Lab Steps**:
  - Use Iverilog to simulate RTL and generate netlists using Yosys.
  - Visualize waveforms and analyze synthesized designs.
  1. Invoke yosys to start the synthesis tool:  
     `yosys`  
     ![Lab Example 1](https://github.com/user-attachments/assets/00fe4aa1-6fcf-4bff-bfa9-8ae8fb95b36b)
  2. Read liberty files (library cells):  
     `read_liberty -lib ../mylib/lib/sky130_fd_sc_hd__mux__2_1.lib`  
     ![Lab Example 2](https://github.com/user-attachments/assets/a9a6fba4-2481-4b85-a2be-57fc6b63c236)
  3. Check for errors by reading Verilog design:  
     `read_verilog good_mux.v`  
     ![Lab Example 3](https://github.com/user-attachments/assets/16568d51-9d18-4975-9603-0a2e7806b85e)
  4. Run synthesis process on top-level module:  
     `synth -top good_mux`  
     ![Lab Example 4](https://github.com/user-attachments/assets/bb294d66-7aac-4157-9c0c-42fe84e4c5f2)
  5. Perform logic optimization using ABC algorithm:  
     `abc -liberty ../mylib/lib/sky130_fd_sc_hd__mux__2_1.lib`  
     ![Lab Example 5](https://github.com/user-attachments/assets/586268ee-de55-4265-b8ca-1390df63b3c3)
  6. Creating netlist:
     `write_verilog good_mux_netlist.v`
     ![netlist creation](https://github.com/user-attachments/assets/e8478c08-3186-4e17-89b5-73ce7c92eaca)
  7. For Precise netlist:
     `write_verilog -noattr good_mux_netlist.v`
     ![Precise nerlist](https://github.com/user-attachments/assets/26c0f7e3-2a13-4e24-9b85-76b5dbfaba7d)
  8. Explaination of .lib library:
     `!gvim ../mylib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
     ![Explanation](https://github.com/user-attachments/assets/fa116f8d-9874-4cf5-a1e0-465c88eb6dc3)
     tt = typical (Process)<br>
     025C = 77 °F (Temperature)<br>
     1v80 = Voltage<br>
     ![lib filename explaination](https://github.com/user-attachments/assets/8e2fac9d-6ef7-4dce-8e20-e829e6c7bbef)



     
</details>
