# Day 2 - Timing Libraries, Hierarchical vs Flat Synthesis, and Efficient Flop Coding Styles

## Overview:
On Day 2, I focused on understanding timing libraries (`.libs`), the differences between hierarchical and flat synthesis, and efficient flip-flop coding styles. These concepts are crucial for improving the design and synthesis processes in RTL design. Below is the breakdown of the tasks and labs completed today.

<details>
  <summary>SKY130RTL D2SK1 - Introduction to Timing Libraries (.libs)</summary>

  ### Lab4 - Introduction to .lib Files (Parts 1-3)
  - Studied the structure and significance of `.lib` files, which are essential for timing analysis and cell characterization.
  - Analyzed timing arcs, cell delays, and power information contained in `.lib` files.
  -  Explaination of .lib library:
     `!gvim ../mylib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
     ![Explanation](https://github.com/user-attachments/assets/fa116f8d-9874-4cf5-a1e0-465c88eb6dc3)
     tt = typical (Process)<br>
     025C = 77 °F (Temperature)<br>
     1v80 = Voltage<br>
     ![lib filename explaination](https://github.com/user-attachments/assets/8e2fac9d-6ef7-4dce-8e20-e829e6c7bbef)
     <img width="594" alt="Screenshot 2024-10-23 at 10 48 57 AM" src="https://github.com/user-attachments/assets/b45fc544-f0ea-4148-ae2c-7318dc72fc6f">

  











</details>

<details>
  <summary>SKY130RTL D2SK2 - Hierarchical vs Flat Synthesis</summary>

  ### Lab05 - Hierarchical vs Flat Synthesis (Parts 1-2)
  - Explored the differences between hierarchical and flat synthesis.
  - Understood how hierarchical synthesis allows for modular design, while flat synthesis provides a single-level design view.
  - Conducted synthesis experiments to observe the impact on area, power, and performance.
  
  #### Key Learnings:
  - The trade-offs between hierarchical and flat synthesis.
  - Impact on the design's complexity, performance, and area.

</details>

<details>
  <summary>SKY130RTL D2SK3 - Various Flop Coding Styles and Optimization</summary>

  ### Why Flops and Flop Coding Styles (Parts 1-2)
  - Learned about the importance of flip-flops in digital design and explored different flop coding styles.

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


