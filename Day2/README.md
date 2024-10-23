# Day 2 - Timing Libraries, Hierarchical vs Flat Synthesis, and Efficient Flop Coding Styles

## Overview:
On Day 2, I focused on understanding timing libraries (`.libs`), the differences between hierarchical and flat synthesis, and efficient flip-flop coding styles. These concepts are crucial for improving the design and synthesis processes in RTL design. Below is the breakdown of the tasks and labs completed today.

<details>
  <summary>SKY130RTL D2SK1 - Introduction to Timing Libraries (.libs)</summary>

  ### Lab4 - Introduction to .lib Files (Parts 1-3)
  - Studied the structure and significance of `.lib` files, which are essential for timing analysis and cell characterization.
  - Analyzed timing arcs, cell delays, and power information contained in `.lib` files.
  - Explanation of .lib library:
     - File path: `!gvim ../mylib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
     - Key breakdown:
       - `tt`: typical (Process)
       - `025C`: 77 °F (Temperature)
       - `1v80`: Voltage
     - ![lib filename explanation](https://github.com/user-attachments/assets/8e2fac9d-6ef7-4dce-8e20-e829e6c7bbef)
       <img width="594" alt="Screenshot 2024-10-23 at 10 48 57 AM" src="https://github.com/user-attachments/assets/b45fc544-f0ea-4148-ae2c-7318dc72fc6f">
  - The logic gate `sky130_fd_sc_hd__a2111o_1`:
     - Has 5 inputs (A1, A2, B1, C1, D1), resulting in 2^5 = 32 possible input combinations.
     - Gate function explained:
       - `a2111o`:
         - `a`: represents the AND gate.
         - `o`: represents the OR gate.
         - `2111`: indicates the structure:
           - Two inputs (A1, A2) go into an AND gate.
           - The result of the AND gate feeds into the first input of a 4-input OR gate (A1, A2, B1, C1, D1).
     - ![Gate explanation](https://github.com/user-attachments/assets/65f2c6bb-37e8-4b5a-9481-8261973ef198)
     - As the number of gates increases area also increasing, i.e it larger cell is employing wider transistors.
     - Wider cells are faster but requires larger area and consume more power.
     - Smaller cell delay will be more but area will be less and consume less power.
     - <img width="1392" alt="Screenshot 2024-10-23 at 11 32 28 AM" src="https://github.com/user-attachments/assets/487a0c75-c2db-4eae-9e8a-a0f992110ac2">

</details>


---------------------------------------------------------------------------------------------------------------------------------------


<details>
  <summary>SKY130RTL D2SK2 - Hierarchical vs Flat Synthesis</summary>

  ### Lab05 - Hierarchical vs Flat Synthesis (Parts 1-2)
  - Understood how hierarchical synthesis allows for modular design, while flat synthesis provides a single-level design view.
  - Conducted synthesis experiments to observe the impact on area, power, and performance.
    For Example:-
    ```verilog
    module sub_module2 (input a, input b, output y);
	    assign y = a | b;
    endmodule
  
    module sub_module1 (input a, input b, output y);
	    assign y = a&b;
    endmodule

    module multiple_modules (input a, input b, input c , output y);
	    wire net1;
	    sub_module1 u1(.a(a),.b(b),.y(net1));  //net1 = a&b
	    sub_module2 u2(.a(net1),.b(c),.y(y));  //y = net1|c ,ie y = a&b + c;
    endmodule
    ```
    <img width="628" alt="Screenshot 2024-10-23 at 12 29 24 PM" src="https://github.com/user-attachments/assets/6927187b-04af-44e8-ba60-48db3aefbd9e">
    
    #### After synthesis<br>
    **multiple_modules**<br>
    <img width="263" alt="Screenshot 2024-10-23 at 12 34 11 PM" src="https://github.com/user-attachments/assets/3431a5ca-2378-4106-ae19-3233d59fbff2">
    **sub_module1**<br>
    <img width="262" alt="Screenshot 2024-10-23 at 12 34 35 PM" src="https://github.com/user-attachments/assets/1a840c8c-9809-4337-bd3d-c0eb55fcb740">
    **sub_module2**<br>
    <img width="260" alt="Screenshot 2024-10-23 at 12 35 04 PM" src="https://github.com/user-attachments/assets/daf0dcde-46e2-43f7-9d1a-7cd56d40ed23">
    **design hierarchy**<br>
    <img width="254" alt="Screenshot 2024-10-23 at 12 35 32 PM" src="https://github.com/user-attachments/assets/60bc031d-7865-411f-836d-017b0657f710"><br>

</details>

<details>
  <summary>SKY130RTL D2SK3 - Various Flop Coding Styles and Optimization</summary>

  ### Why Flops and Flop Coding Styles (Parts 1-2)
  - Learned about the importance of flip-flops in digital design and explored different flop coding styles.
  - Flops are used to minimize the glitches.
  - <img width="720" alt="Screenshot 2024-10-23 at 7 27 47 PM" src="https://github.com/user-attachments/assets/c0488023-1a2c-46ae-955d-955815aab11c">
  #### Flop Coding Styles
  **dff_asyncres.v**
  ```verilog
    module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
    always @ (posedge clk , posedge async_reset)
    begin
	if(async_reset)
	    q <= 1'b0;
	else	
	    q <= d;
    end
    endmodule
  ```
   **Waveforms**
![WhatsApp Image 2024-10-23 at 19 01 24](https://github.com/user-attachments/assets/82f4bc94-4b1e-418b-bb9f-6f1e52d45df2)
**dff_syncres.**
```verilog
module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk )
begin
	if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```
**Waveforms**
![WhatsApp Image 2024-10-23 at 19 37 15](https://github.com/user-attachments/assets/8d5e39c9-977b-4801-bfd5-9397bdf07d3d)





  ### Lab Flop Synthesis Simulations (Parts 1-2)
  - Simulated different flop designs to compare their synthesis results.
  
  ### Interesting Optimizations (Parts 1-2)
  - Applied optimizations to the flop designs to reduce area and improve performance.

  #### Key Learnings:
  - Efficient flop coding styles that optimize the design's performance and resource utilization.
  - Techniques for optimizing the synthesis results of flop designs.

</details>

## Snapshots:
- Added tool output snapshots for each lab section to document the progress and results.


