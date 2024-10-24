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
    
    **For Example**
    <img width="362" alt="Screenshot 2024-10-24 at 3 35 09 PM" src="https://github.com/user-attachments/assets/68d464e3-1706-4f40-b9c2-fad52879157f">
    **Equivalant verilog**
    ```verilog
    assign y = (a&b)|c;
    ```

    **Netlist**
    ```verilog
    and u_and(.a(a), .b(b), .y(i0);
    or u_or(.a(i0), .b(c), .y(y);
    ```

    Gate level models are two types:
      - Timing aware: uses both timing and functional
      - Functional

  ### Synthesis-Simulation Mismatch
  - Investigated the causes of synthesis-simulation mismatches.
  - Explored strategies to identify and fix common mismatches that occur during synthesis.
    
    #### Reasons for Synthesis-Simulation Mismatch
      - Missing Sensitivity list
      - Blocking and Non-Blocking Assignments
      - Non standard Verilog coding
   
    #### Missing Sensitivity list
      - Simulator works based on sensitivit match [i.e Output change is based on change in Input]
        
    **For Example**
    ```verilog
    module mux (
      input io, input i1,
      input sel,
      output reg y
      );
      always @(sel)
      begin
        if(sel)
          y = i1;
        else
          y = 10;
      end
    endmodule
    ```
    Here, the changes in (`sel`) is assigned to (`y`) but the changes in (`i0`) and (`i1`) is not reflected in (`y`)

    **Correct method**
    ```verilog
    module mux (
      input io, input i1,
      input sel,
      output reg y
      );
      always @(*)
      begin
        if(sel)
          y = i1;
        else
          y = 10;
      end
    endmodule
    ```
    Here, (`*`) indicates that the changes in any  signal it is reflected in (`y`).

  ### Blocking and Non-blocking Statements in Verilog
  - Analyzed the difference between blocking (`=`) and non-blocking (`<=`) statements in Verilog.
  - Learned how improper use of these statements can lead to simulation vs synthesis issues.
    * Occurs inside the always block
        - (`=`) Blocking:
            - Executes the statements in the order it is written
            - First statement is Evaluated before the 2nd statement
        - (`<=) Non-Blocking:
            - Executes all the RHS where always block is Executed and assigns to LHS
            - Parallel Evaluation

    **Example 1**
    ```verilog
    module code (input clk,
    input reset,
    input d,
    output reg q);
    reg q0;
    always @(posedge clk, posedge reset)
    begin
    if (reset)
    begin
        q0 = 1'b0;
        q = 1'b0;
    end
    else
    begin
        q = q0;
        q0 = d;
    end
    endmodule
    ```

    **Example 2**
    ```verilog
    module code (input clk,
    input reset,
    input d,
    output reg q);
    reg q0;
    always @(posedge clk, posedge reset)
    begin
    if (reset)
    begin
        q0 = 1'b0;
        q = 1'b0;
    end
    else
    begin
        q = q0;
        q0 = d;
    end
    endmodule
    ```

    **Expected Output**
<img width="422" alt="Screenshot 2024-10-24 at 4 04 53 PM" src="https://github.com/user-attachments/assets/10fdc124-4be5-4679-b160-e02cb3a3a557">

    **Original Output**
    <img width="286" alt="Screenshot 2024-10-24 at 4 06 24 PM" src="https://github.com/user-attachments/assets/006d7e8d-ed58-480f-bd79-40cdc029bfff">

    > **Note:** Use Non-blocking assignments while writing sequential circuits.


  ### Caveats with Blocking Statements
  - Explored issues caused by incorrect use of blocking statements in sequential logic.
  - Understood scenarios where blocking statements can cause unwanted behavior in simulation and synthesis.

    **Synthesis simulation mismatch**

    **Example 1**
    ```verilog
    module code (input a, b,c
    output reg y);
    reg q0;
    always @(*)
    begin
        y = q0 & c;
        q0 = a|b;
    end
    endmodule
    ```
    Here, due to (`y = q0 & c`) before (`q0 = a|b`) introduces and delay/flop

    **Correct method**
    ```verilog
    module code (input a, b,c
    output reg y);
    reg q0;
    always @(*)
    begin
        q0 = a|b;
        y = q0 & c;
    end
    endmodule
    ```
    
</details>

-----------------------------------------------------------------------------------------------------------------------------------

<details>
  <summary>Labs on GLS and Synthesis-Simulation Mismatch</summary>

  ### Lab GLS Synth Sim Mismatch
  - Performed Gate-Level Simulation to identify synthesis-simulation mismatches.
  - Debugged and resolved mismatches using simulation output.
    **Example 1: ternary_operator_mux.v**<br>
    ```verilog
    module ternary_operator_mux (input i0 , input i1 , input sel , output y);
	      assign y = sel?i1:i0;
	  endmodule
    ```
    **Explaination**<br>
    `condition(`?`)true(`:`)false`

    **RTL Simulation**<br>
    <img width="1287" alt="Screenshot 2024-10-24 at 5 12 14 PM" src="https://github.com/user-attachments/assets/d03011c5-02ba-4ca0-ba47-1d59efb43a97">

    **Synthesis**<br>
    <img width="297" alt="Screenshot 2024-10-24 at 5 13 58 PM" src="https://github.com/user-attachments/assets/978035db-e148-4d13-9591-a7bd623be3af">

    **Output**<br>
    <img width="781" alt="Screenshot 2024-10-24 at 5 24 11 PM" src="https://github.com/user-attachments/assets/fe42792e-ba6f-4599-b2fe-5ba94c59e830">

    **GLS Output**<br>
    <img width="1287" alt="Screenshot 2024-10-24 at 5 29 28 PM" src="https://github.com/user-attachments/assets/86ada8d9-1644-406e-9eef-f7a579f1b0ff">

    **Example 2: bad_mux.v**<br>
    ```verilog
    module bad_mux (input i0 , input i1 , input sel , output reg y);
	always @ (sel)
	begin
		if(sel)
			y <= i1;
		else 
			y <= i0;
	end
	endmodule
    ```
    **Explaination**<br>
    Here, the changes in (`sel`) is assigned to (`y`) but the changes in (`i0`) and (`i1`) is not reflected in (`y`)

    **RTL Simulation**<br>
	<img width="1287" alt="Screenshot 2024-10-24 at 5 51 10 PM" src="https://github.com/user-attachments/assets/0eeb0fe7-707f-405b-a652-ddffff6216ae">

    **Synthesis**<br>
    <img width="307" alt="Screenshot 2024-10-24 at 5 51 57 PM" src="https://github.com/user-attachments/assets/fdb4763d-d9e2-4140-aa92-72df47291182">

    **Output**<br>
    <img width="832" alt="Screenshot 2024-10-24 at 5 53 10 PM" src="https://github.com/user-attachments/assets/05994e96-18d1-40f2-b8ca-27a629c1f73d">

    **GLS Output**<br>
    <img width="1287" alt="Screenshot 2024-10-24 at 5 55 26 PM" src="https://github.com/user-attachments/assets/edebea18-a033-4811-8c2e-b24f40f543b7">

</details>

------------------------------------------------------------------------------------------------------------------------------------

<details>
  <summary>Labs on Synth-Sim Mismatch for Blocking Statement</summary>

  ### Lab Synth Sim Mismatch Blocking Statement 
  - Focused on identifying issues caused by blocking statements in synthesized designs.
  - Ran simulations to observe incorrect behavior due to blocking statements.
    
    **Example 1: blocking_caveat**<br>
    ```verilog
    module blocking_caveat (input a , input b , input  c, output reg d); 
	reg x;
	always @ (*)
	begin
		d = x & c;
		x = a | b;
	end
	endmodule
	```
    **Explaination**<br>
	Here, result of `x & c` is stored in `d` but the register x it hold the previous data, later the result of `a | b` is stored in x.

    **RTL Simulation**<br>
	<img width="1286" alt="Screenshot 2024-10-24 at 6 06 20 PM" src="https://github.com/user-attachments/assets/a490069e-c155-484b-97a9-2bbf11c46642">

    **Synthesis**<br>
	<img width="306" alt="Screenshot 2024-10-24 at 6 07 21 PM" src="https://github.com/user-attachments/assets/0d019deb-466e-4a55-9ed3-18980106c924">

    **Output**<br>
	<img width="820" alt="Screenshot 2024-10-24 at 6 09 07 PM" src="https://github.com/user-attachments/assets/8d2ff7fa-d1ee-46de-b3ef-a596e4ca383e">

    **GLS Output**<br>
	<img width="1286" alt="Screenshot 2024-10-24 at 6 11 00 PM" src="https://github.com/user-attachments/assets/40fd4db0-2768-4256-972e-ce4f8857fed7">



</details>

