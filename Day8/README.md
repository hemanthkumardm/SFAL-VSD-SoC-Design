# Day 8 - Optimizations

<details>
  <summary><b>DC_D4SK1 - Optimizations Combinational Opt</b></summary>

  **Optimization goals**
      - Cost function based optimizations.
        - Optimization till the cost is met.
        - Over optimization of one goal will harm other goals.
        - Goals for synthesis.
            - Meet timing
            - Meet Area
            - Meet Power
  - **Combinational Optimizations**
    - Squeezing the logic to get the most optimised design
      - Area and Power savings
    - Constant Propagation
      - Direct Optimisaton
    - Boolean Logic Optimisation
      - К-Мар
      - Quine McKluskey

    **Constant Propagation**
    <img width="1109" alt="Screenshot 2024-10-29 at 10 19 43 PM" src="https://github.com/user-attachments/assets/5956def8-a5e1-4fa2-9443-480d12e6caf1">

    **Boolean Logic Optimization**
    <img width="1272" alt="Screenshot 2024-10-29 at 10 20 32 PM" src="https://github.com/user-attachments/assets/d854f4c9-d245-4481-a322-1d71cf79adfd">

    **Resource Sharing**
    <img width="1237" alt="Screenshot 2024-10-29 at 10 21 00 PM" src="https://github.com/user-attachments/assets/b431cbcb-6de1-41dd-aceb-97b82b68b929">

    **Logic Sharing**
    <img width="1289" alt="Screenshot 2024-10-29 at 10 21 51 PM" src="https://github.com/user-attachments/assets/896c5612-e8f0-4bc0-8685-b6761c987e91">

    **Balanced Vs Preferential Implementation**
    <img width="1426" alt="Screenshot 2024-10-29 at 10 22 54 PM" src="https://github.com/user-attachments/assets/d56698b1-eccc-4743-8f3a-f0d5a2050b75">

  - **Sequential Optimizations**
    - Basic
      - Sequential Constant propagation
      - Retiming
      - Unused Flop removal
      - Clock Gating
    - Advanced [Not covered as part of Lab]
      - State optimisation
      - Sequential Logic Cloning (Floor Plan Aware Synthesis)

  **Example 1**
  <img width="1023" alt="Screenshot 2024-10-29 at 10 25 54 PM" src="https://github.com/user-attachments/assets/c4a04a7b-a396-493c-8759-c162c25d9192">

  **Example 2**
  <img width="1281" alt="Screenshot 2024-10-29 at 10 42 07 PM" src="https://github.com/user-attachments/assets/e40b25a5-fdd0-49e3-89b5-1aca04a4d8ef">

  **Example 3**
  <img width="1415" alt="Screenshot 2024-10-29 at 10 42 50 PM" src="https://github.com/user-attachments/assets/f2362ad9-f3df-4c78-b27b-bd74a0d06d7e">

  **Example 4**
  <img width="1229" alt="Screenshot 2024-10-29 at 11 06 09 PM" src="https://github.com/user-attachments/assets/aa6829d9-be61-46a1-902b-03e300258625">

  **Optimization of unloaded outputs**
  <img width="1440" alt="Screenshot 2024-10-29 at 11 07 42 PM" src="https://github.com/user-attachments/assets/9d85ddc8-fd96-489a-a2bd-516eac50ff48">

  **Controlling sequential optimizations in DC**
    ```tcl 
    compile_seqmap_propagate_constants
    compile_delete_unloaded_sequential_cells
    compile_register_replication
    ```verilog
    module opt_check (input a , input b, 
wire a 1; assign yl = a?b: 1'b0;|
assign y2 = ~( (a_l&b) | c) :
assign a_1 =


</details>

<details>
  <summary><b>DC_D4SK2 - Combinational Optimizations</b></summary>
  
  - Combinational Optimizations
    **opt_check.v**
    ```verilog
    module opt_ check (input a , input b , input c , output y1 , output y2; 
    wire a_1;
    assign yl =a?b:1'b0;
    assign y2 = ~( (a_l&b) | c);
    assign a_1 = 1'b0;
    endmodule
    ```
    **Expected output**
    <img width="501" alt="Screenshot 2024-10-30 at 12 04 16 AM" src="https://github.com/user-attachments/assets/358d5040-3095-4ad9-a0eb-a298dc25b85a">

      **Design Vision output**
    <img width="318" alt="Screenshot 2024-10-30 at 12 04 54 AM" src="https://github.com/user-attachments/assets/31d1fb30-0217-4be4-aa15-3d27d4fb01d2">


  - Resource Sharing Optimizations

    `resource_sharing_mult_check.v`
    ```verilog
    module resource sharing mult check (input [3:0] b, input [3:0] c, input [3:0] d, output [7:0] y , input sel);
      assign y = sel? (a*b) : (c*d) ;
    endmodule
    ```
    <img width="808" alt="Screenshot 2024-10-30 at 12 11 10 AM" src="https://github.com/user-attachments/assets/ec9ec35d-5d1f-45b8-88fa-462b369a7951">

    **Design Vision Output**
    <img width="617" alt="Screenshot 2024-10-30 at 12 11 25 AM" src="https://github.com/user-attachments/assets/1e9fb541-1e91-4355-8dda-4ce0e26040ca">

    **compile_ultra results**
    <img width="326" alt="Screenshot 2024-10-30 at 12 13 01 AM" src="https://github.com/user-attachments/assets/d91e81db-a305-47c5-8436-3c3c8115838b">
    
    <img width="842" alt="Screenshot 2024-10-30 at 12 13 38 AM" src="https://github.com/user-attachments/assets/b3a22317-b59e-4567-857b-0bf9e71ca330">

  - Sequential Optimizations

    **dff_const1.v**
    ```verilog
    module dff constl(input clk, input reset, output reg q);
    always @(posedge clk, posedge reset)
    begin
      if (reset)
        q <= 1'b0;
      else
        q = 1'b1;
      end
    endmodule
    ```

    **dff_const2.v**
    ```verilog
    module dff const2(input clk, input reset, output reg q) ;
    always @(posedge clk, posedge reset)
    begin
      if (reset)
        q <= 1'b1;
      else
        q < 1'b1;
      end
    endmodule
    ```
    <img width="578" alt="Screenshot 2024-10-30 at 12 29 51 AM" src="https://github.com/user-attachments/assets/5cd768b7-637e-487d-b77f-25c5749cbfcb">
    
    <img width="624" alt="Screenshot 2024-10-30 at 12 34 20 AM" src="https://github.com/user-attachments/assets/cc9c92ff-ce90-46db-a349-07ce5729bbfc">
    <img width="652" alt="Screenshot 2024-10-30 at 12 36 01 AM" src="https://github.com/user-attachments/assets/6d602328-2631-43a0-a827-f30294a692e6">

</details>

<details>
  <summary><b>DC_D4SK3 - Special Optimizations</b></summary>
  
  - Special Optimizations
    
  - How Paths are Timed (MCP - Multicycle Paths)
    
</details>

<details>
  <summary><b>DC_D4SK4 - Boundary Optimization</b></summary>
  
  - Boundary Optimization
  - Register Retiming
  - Isolating Output Ports
  - Multicycle Path Optimization
</details>
