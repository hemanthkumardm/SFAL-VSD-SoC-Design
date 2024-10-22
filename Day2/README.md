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
</details>

<details>
    <summary>4. Labs Using Yosys and SKY130 PDKs</summary>

#### Part 1
- **Lab Steps**:
  - Use Iverilog to simulate RTL and generate netlists using Yosys.
  - Visualize waveforms and analyze synthesized designs.

   ![Lab Example 1](https://github.com/user-attachments/assets/00fe4aa1-6fcf-4bff-bfa9-8ae8fb95b36b)
   ![Lab Example 2](https://github.com/user-attachments/assets/a9a6fba4-2481-4b85-a2be-57fc6b63c236)
   ![Lab Example 3](https://github.com/user-attachments/assets/16568d51-9d18-4975-9603-0a2e7806b85e)
   ![Lab Example 4](https://github.com/user-attachments/assets/bb294d66-7aac-4157-9c0c-42fe84e4c5f2)
</details>

## Challenges Faced
<details>
    <summary>Expand to view challenges</summary>

</details>

## Resources
<details>

</details>
