# Day 6 - Basics of STA (Static Timing Analysis)

## DC_D2SK1 - Introduction to STA

<details>
  <summary>Intro to STA</summary>
  
  - Overview of Static Timing Analysis (STA).
  - Key concepts related to timing verification and analysis.
    Introduction to STA
    <img width="1381" alt="Screenshot 2024-10-27 at 8 06 12 AM" src="https://github.com/user-attachments/assets/30d0859a-7472-461b-bc78-3c227d368771">
    <img width="1397" alt="Screenshot 2024-10-27 at 8 08 45 AM" src="https://github.com/user-attachments/assets/14f987eb-246d-4f8a-971b-121c8111e148">
    **Is delay a cell constant?**
    <img width="1289" alt="Screenshot 2024-10-27 at 8 09 16 AM" src="https://github.com/user-attachments/assets/1c704357-cbbd-484b-a4ce-a0fe1d4d1b04">

    ### Timing Arcs

    **Combinational Cell**
    Delay information from every input pin to every output pin which it can control
    <img width="897" alt="Screenshot 2024-10-27 at 8 11 19 AM" src="https://github.com/user-attachments/assets/427de53e-0cab-4812-bafa-ec4a480750e5">
    <img width="1279" alt="Screenshot 2024-10-27 at 8 11 56 AM" src="https://github.com/user-attachments/assets/3de62217-7aef-4d1d-84d1-066a91f62545">
    <img width="1407" alt="Screenshot 2024-10-27 at 8 12 34 AM" src="https://github.com/user-attachments/assets/667de41b-b1ac-4dba-a45c-b21adb5d712e">

</details>

-----

<details>
  <summary>What are constraints?</summary>
  
  - Explanation of design constraints in STA.
  - Importance of specifying constraints for accurate timing analysis.

    **Timing Paths**
    <img width="1404" alt="Screenshot 2024-10-27 at 8 18 28 AM" src="https://github.com/user-attachments/assets/52802610-ffe5-40a1-8d16-fc10656b0294">

    **Why Constraints**
    <img width="1437" alt="Screenshot 2024-10-27 at 8 19 26 AM" src="https://github.com/user-attachments/assets/e6640fcc-25ee-49dd-8394-ed5e16d17253">

    **Timing Paths**
    - Start Points
        - Input Ports
        - Clk Pins of Register
    - End Points
        - Output Ports
        - D pin of DFF / DLAT
    - Always the timing paths start at one of the start points and ends at one of the end points.
        - Clk to D
        - Clk to Output
        - Input to D
        - Input to Output

    **Why Constraints**
    <img width="1394" alt="Screenshot 2024-10-27 at 8 23 32 AM" src="https://github.com/user-attachments/assets/338eecc5-0bb6-4bdb-b81e-c2fbf2f5e0b0">
    <img width="1426" alt="Screenshot 2024-10-27 at 8 24 13 AM" src="https://github.com/user-attachments/assets/1c312b17-ea26-4974-ab34-016dc41e8605">
    <img width="1428" alt="Screenshot 2024-10-27 at 8 24 31 AM" src="https://github.com/user-attachments/assets/1245c33d-49f1-4437-896f-1bcd262455f7">

    - Timing Paths :
      - REG 2 REG : Constrained by Clock
      - REG 2 OUT : Constrained by Output External Delay and Clock Period
      - IN 2 REG: Constrained by Input External Delay and Clock Period
      - Collectively the REG2OUT and IN2REG are called IO Paths and the delay modelling referred above is called Delay Modelling.
    <img width="1415" alt="Screenshot 2024-10-27 at 8 25 54 AM" src="https://github.com/user-attachments/assets/469485f9-3abc-405d-a7f1-4bf5f39f0860">
    
</details>

<details>
  <summary>Input Transition & Output Load</summary>
  
  - Detailed understanding of input transition and output load in timing analysis.
  - Impact on the performance and timing of the design.

  ### IO Contraints
  <img width="1391" alt="Screenshot 2024-10-27 at 8 37 39 AM" src="https://github.com/user-attachments/assets/a82efb7b-1c4f-41dd-bb9e-dee27372c9ea">
  <img width="1419" alt="Screenshot 2024-10-27 at 8 39 25 AM" src="https://github.com/user-attachments/assets/823cc4e8-c7ba-436e-bf1a-8486c46022fe">
  <img width="1436" alt="Screenshot 2024-10-27 at 8 40 20 AM" src="https://github.com/user-attachments/assets/bee5fac0-ac17-4996-b638-ea70953c6862">


</details>

---

## Timing .Libs and Exploration

<details>
  <summary>Timing .Libs</summary>
  
  - Introduction to timing libraries (`.lib`) and their role in STA.
  - Understanding the structure of `.lib` files and the key parameters.

  **Reading .lib file**
  `gvim ~/DC WORKSHOP/lib/sky130_fd_schd tt_ 025C_1v80.lib`
  <img width="1004" alt="Screenshot 2024-10-27 at 9 34 39 PM" src="https://github.com/user-attachments/assets/1a08b8ef-ae33-4e93-a219-2378f2427402">

  **Delay model lookup table**
  <img width="1418" alt="Screenshot 2024-10-27 at 9 38 18 PM" src="https://github.com/user-attachments/assets/8a3c355e-ff24-41a0-b426-6b6e5c9f757e">

  **Comparing two flavours of AND gates**
  <img width="1018" alt="Screenshot 2024-10-27 at 9 39 52 PM" src="https://github.com/user-attachments/assets/8b2637ea-89b1-4ab9-80ce-4a29f613e6ee">

  **Unateness**
  <img width="1434" alt="Screenshot 2024-10-27 at 9 41 05 PM" src="https://github.com/user-attachments/assets/cc4c637d-9056-414e-8c51-e39098812d27">

  **Looking for library cells**
  `get_lib_cells */* -filter "is_sequential==true"`
  <img width="1125" alt="Screenshot 2024-10-27 at 9 44 48 PM" src="https://github.com/user-attachments/assets/062f46eb-e38c-41af-936f-279ef5fb4053">

  **Timing type for negetive latch and positive latch**
  <img width="1018" alt="Screenshot 2024-10-27 at 9 48 12 PM" src="https://github.com/user-attachments/assets/296a36e5-d8ae-4dda-8663-0f83af3cf68b">

</details>

<details>
  <summary>Lab6 - Exploring dotLib</summary>
  
  - Hands-on exploration of `.lib` files.
  - Analyzing timing, power, and delay information from `.lib` files.

    `get_lib_cells */*and*`
    <img width="1128" alt="Screenshot 2024-10-27 at 9 50 42 PM" src="https://github.com/user-attachments/assets/52f6b937-8215-4d8b-9624-e2685d7dbd3a">

    **Looping into each cell in collection**
    ```tcl
    foreach in collection my lib cell [get lib cells */*and*] {
      set my_lib_cell_name [get_object_name $my_lib_cell];
      echo $my_lib_cell;
    }
    ```
    <img width="1124" alt="Screenshot 2024-10-27 at 9 52 36 PM" src="https://github.com/user-attachments/assets/884ba6ab-43a5-4322-95c6-07d965ab7b99">

    `get_lib_attribute sky130_fd schd tt_025C_1v80/sky130_fd schd and2_0/A input`
    <img width="708" alt="Screenshot 2024-10-27 at 9 53 27 PM" src="https://github.com/user-attachments/assets/229809e3-174e-4222-ac11-a64ebb74fe23">

    **To get functionality of the attribute**
    `get_lib_attribute sky130_fd_sc_hd_tt_025C_1v80/sky130_fd_sc_hd_nand4_1/Y function`
    <img width="755" alt="Screenshot 2024-10-27 at 9 55 23 PM" src="https://github.com/user-attachments/assets/657bedc0-8182-4305-b42c-e96345935ee8">
    <img width="1185" alt="Screenshot 2024-10-27 at 9 56 53 PM" src="https://github.com/user-attachments/assets/bd2a26a2-d1f9-465f-ae24-39f6c080b457">

    `get_lib_attribute sky130_fd_sc_ha_tt_025C_1v80/sky130_fd_sc_hd__and4bb_1/X function`
    <img width="764" alt="Screenshot 2024-10-27 at 10 18 56 PM" src="https://github.com/user-attachments/assets/b2cd4aba-29fe-4274-b61f-ddb2e5df466a">

    ```tcl
    set my_list [list sky130_fd_sc_hd_tt_025C_1v80/sky130_fd_sc_hd__nand3b_1 \
    sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd_nand3b_2 \
    sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd_nand3b 4\
    sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__nand4_1\
    sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__nand4_2\
    sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__nand4_4\
    sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd_nand4b_1 \
    sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd_nand4b_2 ]
    
    #For each cell in the list, find the output pin name and its functionality
    
    foreach my_cell $my_list {
      foreach_in_collection my_lib_pin [get_lib_pins ${mycell}/*] {
        set my_lib pin name [get_object_name $my_lib_ pin];
        set a [get_lib_attribute $my_lib_pin_name direction];
        if{ $a > 1 } {
          set fn [get_lib_attribute $my_lib_pin_name function];
          echo smy_lib_pin_name $a $fn;
        }
      }
    }
    ```
    <img width="1127" alt="Screenshot 2024-10-27 at 10 30 59 PM" src="https://github.com/user-attachments/assets/428a1396-775a-49ce-96bd-387926270918">

    `get lib attribute sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd nand4b_2/B capacitance`
    `get_lib_attribute sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd_nand4b_2 area`
    `get_lib_attribute sky130_fd_sc_hd__tt_025C_Iv80/sky130_fd_sc_hd_nand4b_2/B clock`
    <img width="737" alt="Screenshot 2024-10-27 at 10 34 33 PM" src="https://github.com/user-attachments/assets/56919dae-59fa-41e9-863c-4fb2f29a4681">

    `list_attributes -app`
    <img width="1123" alt="Screenshot 2024-10-27 at 10 36 03 PM" src="https://github.com/user-attachments/assets/637c738d-af06-4636-9165-616119bfd783">





    


  
</details>
