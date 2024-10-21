# Day 2: Introduction to Verilog RTL Design and Synthesis

## Overview
On Day 2, we focused on Verilog RTL design and synthesis using tools like Iverilog and Yosys, within the SKY130 process design kit (PDK).

## Tasks Completed

<details>
    <summary>1. Introduction to Open-Source Simulator Iverilog</summary>

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
</details>

<details>
    <summary>2. Labs Using Iverilog and GTKWave</summary>

   - **Steps**:
     - Load the latch and its testbench to Iverilog, and execute the `a.out` file.
       <br><img width="1440" alt="Screenshot 2024-10-21 at 6 32 26 PM" src="https://github.com/user-attachments/assets/f5c09d2d-8663-42db-854b-53cda992bac6">
     - Load the `.vcd` file into GTKWave for waveform visualization.
       <br><img width="1440" alt="Screenshot 2024-10-21 at 6 33 35 PM" src="https://github.com/user-attachments/assets/475d843e-b965-4af9-a84b-c81a4ed22ae8">
</details>


<details>
    <summary>3. Introduction to Yosys and Logic Synthesis</summary>
    <details>
        <summary>Introduction to yosys</summary>
        it is a tool used to convert RTL to netlist
        used tool is yosys
        
        
        <p> 
            ## yosys setup
            netlist is representing a design in the form of cell present in the .lib
            netlist is the representation of the design in the form of cell present in .lib
            ![Screenshot 2024-10-22 at 12 45 01 AM](https://github.com/user-attachments/assets/50f13129-e000-45fc-a638-e76b554b804e)
            ## verify the synthesis
            Note: the set of primary input / primary output will be remain same between the RTl design and synthesized netlist same test bench can be used
<img width="1440" alt="Screenshot 2024-10-22 at 12 45 20 AM" src="https://github.com/user-attachments/assets/2d289936-912b-4a13-a402-af55b73aeeab">
        </p>
    </details>
    <details>
        <summary>Introduction to Logic Synthesis</summary>
        1. RTK design :- Behavioural representation of the required specification
<img width="402" alt="Screenshot 2024-10-22 at 1 03 31 AM" src="https://github.com/user-attachments/assets/8af7b724-9f76-45aa-a56b-21fbd58f2757">
        2. Synthesis :- RTL tp gate level translation
        the design is converted into gates and the connections are mode between the gates
        3. the output of this is called netlist
        <img width="446" alt="Screenshot 2024-10-22 at 1 07 11 AM" src="https://github.com/user-attachments/assets/1d80cc79-2931-4b27-9eae-fd5b9301cdee">
        4. .lib :- collection of logical modules
        includes basic logic gates like AND, OR, NOT etc.
        different flavours of same gate
        * 2-input AND gates
         . slow
         . medium 
         . fast
        it contains standard cells to implement any boolean logic functionality
        

<img width="1440" alt="Screenshot 2024-10-22 at 1 04 02 AM" src="https://github.com/user-attachments/assets/98351880-36b9-42e4-9a8e-a177be9e8626">

        
        
        <p> 
            ## yosys setup
            netlist is representing a design in the form of cell present in the .lib
            netlist is the representation of the design in the form of cell present in .lib
            ![Screenshot 2024-10-22 at 12 45 01 AM](https://github.com/user-attachments/assets/50f13129-e000-45fc-a638-e76b554b804e)
            ## verify the synthesis
            Note: the set of primary input / primary output will be remain same between the RTl design and synthesized netlist same test bench can be used
<img width="1440" alt="Screenshot 2024-10-22 at 12 45 20 AM" src="https://github.com/user-attachments/assets/2d289936-912b-4a13-a402-af55b73aeeab">
        </p>
    </details>
</details>

<details>
    <summary>4. Labs Using Yosys and Sky130 PDKs</summary>
    <details>
        <summary>Part 1</summary>
        <p> 
            <img width="628" alt="Screenshot 2024-10-22 at 12 32 45 AM" src="https://github.com/user-attachments/assets/00fe4aa1-6fcf-4bff-bfa9-8ae8fb95b36b">
            <img width="608" alt="Screenshot 2024-10-22 at 12 33 55 AM" src="https://github.com/user-attachments/assets/a9a6fba4-2481-4b85-a2be-57fc6b63c236">
            <img width="641" alt="Screenshot 2024-10-22 at 12 34 25 AM" src="https://github.com/user-attachments/assets/16568d51-9d18-4975-9603-0a2e7806b85e">
            <img width="467" alt="Screenshot 2024-10-22 at 12 35 34 AM" src="https://github.com/user-attachments/assets/bb294d66-7aac-4157-9c0c-42fe84e4c5f2">
            <img width="446" alt="Screenshot 2024-10-22 at 12 36 13 AM" src="https://github.com/user-attachments/assets/e663c118-8f44-4813-b07a-6a218f56f347">
            <img width="1440" alt="Screenshot 2024-10-22 at 12 27 59 AM" src="https://github.com/user-attachments/assets/a28ab7f6-ab37-4f74-a1ee-e433352410e7">
        </p>
    </details>

</details>

## Challenges Faced
- List any challenges you encountered here.

## Next Steps
- Outline your next steps and goals for upcoming tasks.

## Resources
- List any references or resources that were useful.
