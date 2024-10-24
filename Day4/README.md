# Day 4 - GLS, Blocking vs Non-blocking, and Synthesis-Simulation Mismatch

## Overview:
On Day 4, I focused on Gate-Level Simulation (GLS), the differences between blocking and non-blocking statements, and understanding synthesis-simulation mismatches. These concepts are crucial for debugging and improving the accuracy of RTL designs during the synthesis process. Below is the breakdown of the tasks and labs completed today.

<details>
  <summary>GLS, Synthesis-Simulation Mismatch, and Blocking/Non-blocking Statements</summary>

  ### GLS Concepts and Flow Using Iverilog
  - Studied the purpose and process of Gate-Level Simulation using the Iverilog simulator.
  - Understood the flow of GLS and how it helps in verifying the design after synthesis.
    #### What is GLS?
    
    Running the test bench with netlist as Design under test.

    #### Why GLS?

    - verifying the logical correctness of design after synthesis
    - Ensuring the timing of the design
    - GLS needs to be run with delay annotation
   
    #### GLS using iverilog
    <img width="926" alt="Screenshot 2024-10-24 at 3 30 20 PM" src="https://github.com/user-attachments/assets/5cf4687d-89c8-4202-abca-c7952388d4df">
    
    > **Note:** If the gate level models are delay annoted, then we can use for timing validation.

  

  ### Synthesis-Simulation Mismatch
  - Investigated the causes of synthesis-simulation mismatches.
  - Explored strategies to identify and fix common mismatches that occur during synthesis.



  ### Blocking and Non-blocking Statements in Verilog
  - Analyzed the difference between blocking (`=`) and non-blocking (`<=`) statements in Verilog.
  - Learned how improper use of these statements can lead to simulation vs synthesis issues.


  ### Caveats with Blocking Statements
  - Explored issues caused by incorrect use of blocking statements in sequential logic.
  - Understood scenarios where blocking statements can cause unwanted behavior in simulation and synthesis.


</details>

-----------------------------------------------------------------------------------------------------------------------------------

<details>
  <summary>SKY130RTL D4SK2 - Labs on GLS and Synthesis-Simulation Mismatch</summary>

  ### Lab GLS Synth Sim Mismatch Part 1
  - Performed Gate-Level Simulation to identify synthesis-simulation mismatches.
  - Debugged and resolved mismatches using simulation output.

</details>

------------------------------------------------------------------------------------------------------------------------------------

<details>
  <summary>SKY130RTL D4SK3 - Labs on Synth-Sim Mismatch for Blocking Statement</summary>

  ### Lab Synth Sim Mismatch Blocking Statement 
  - Focused on identifying issues caused by blocking statements in synthesized designs.
  - Ran simulations to observe incorrect behavior due to blocking statements.

</details>

