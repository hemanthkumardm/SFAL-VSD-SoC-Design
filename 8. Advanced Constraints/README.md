<details>
  <summary>SDC Part 1 and Part 2</summary>

## SDC Part 1: Clock, Clock Tree Modelling, Uncertainty
    **What needs to be Constrained for Clocks**
    <img width="1421" alt="Screenshot 2024-10-29 at 4 40 33 PM" src="https://github.com/user-attachments/assets/f3972e48-4951-4a2c-822c-bcb93b2c8a86">

    **Implementation Flow of ASIC**
    <img width="891" alt="Screenshot 2024-10-29 at 4 41 08 PM" src="https://github.com/user-attachments/assets/68c10c96-7b0f-40ea-87ed-bf9d61607904">

    **Clock is built during Clock Tree Synthesis only. Till then Clock is an Ideal NW.**

    ### Clock Generation
      - Oscillator
      - PLL
      - External Clock Source
      - All of the above clock sources have inherent variations in the clock period due to stochastic effects.
    <img width="1253" alt="Screenshot 2024-10-29 at 4 43 46 PM" src="https://github.com/user-attachments/assets/bfbd8516-5546-4304-b565-f771c5e79f0f">


  ### Clock Distribution

  **Ideal Clock Network:** All flops sees the edge at same time.
  <img width="796" alt="Screenshot 2024-10-29 at 4 45 21 PM" src="https://github.com/user-attachments/assets/c07520ee-7b48-4c6c-9b0b-ddda1073ffce">
  
  **Practical Clock Network:** Practical Clock Network after CTS, All flops may not see the clock edge at same instance i.e Clock SKEW 
  <img width="794" alt="Screenshot 2024-10-29 at 4 46 16 PM" src="https://github.com/user-attachments/assets/75d4e97d-2e3f-4e49-8c9d-9ed4762eb2af">

  **Jitter:** Stocastic varition in clock generator.

  ### Clock Skew
    - Clock Tree built during CTS : **Practical Clock Tree**
    - Logic optimization happens in synthesis : **Ideal Clock Tree**
    - Timing Clean paths in Synthesis may fail after STA
  <img width="701" alt="Screenshot 2024-10-29 at 4 48 40 PM" src="https://github.com/user-attachments/assets/12be41be-aae2-493b-8e4b-da134ba44aea">

  **Ideal Scenario**
  <img width="516" alt="Screenshot 2024-10-29 at 4 48 50 PM" src="https://github.com/user-attachments/assets/e9bd566b-6dc5-496a-8d6c-ea6e4b551d73">
  `TCLK >= TCQ + TCOMBI + TSU`

  **Practical Scenario**
  <img width="553" alt="Screenshot 2024-10-29 at 4 50 10 PM" src="https://github.com/user-attachments/assets/f05f6022-9be9-447f-8b5b-ce4b10735c39">

  `(TCLK - TSKEW) >= TCQ + TCOMBI + TSU`
  Available timing window shrinks, Path is timing clean before CTS, but fails after CTS.

  ### Clock modelling

  - **Model the Clock for following**
    - **Period**
    - **Source Latency :** Time taken by the clock source to generate clock
    - **Clock Network Latency :** Time taken by Clock Distribution NW
    - **Clock Skew :** Clock path delay mismatches which causes difference in the arrival of clock.
      - CTS will balance the clocks, but still the skew cannot be reduced to 0 .
    - **Jitter :** Stochastic variations in the arrival of clock edge
        - Duty Cycle Jitter
        - Period
    - Collectively Clock Skew, Jitter is called Clock Uncertainty
  > **Note:** Post CTS, the clock network is real, and hence these modelled Clock Skew and Clock Network Latency MUST BE REMOVED !
    

## SDC Part 2: IO delays

  **How to Constraint the design in DC ?**
    
  - DC takes constraints in the form of SDC (Synopsys Design Constraints).
    <img width="1305" alt="Screenshot 2024-10-29 at 4 59 56 PM" src="https://github.com/user-attachments/assets/a3174eb0-a66d-4718-b77d-661530a17789">

   **Getting the Ports in DC**<br>
    - `get_ports clk;`<br>
    - `get_ports *clk*;` Wild card `*` supported<br>
    - `get_ports*;`<br>
    - `get_ports *-filter "direction == in";`  Filtering based on conditions.<br>
    - `get_ports *-filter "direction == out";`<br>
  > **Note:** Case Sensitive
  
  **Getting the clocks in DC**
    - `get_clocks *`
    - `get_clocks *clk*`: All clocks which has the name clk in it
    - `get_clocks *-filter "period > 10"`
    - `get_attribute [get_clocks my_clk] period`
    - `get_attribute [get_clocks my_clk] is_generated`

  **Querying the Cells in the Design**
  <img width="912" alt="Screenshot 2024-10-29 at 5 09 49 PM" src="https://github.com/user-attachments/assets/748dc934-b923-4ca0-a81b-82fd81a88796">

  ```verilog
  module combo_logic input in1, input in2, output out1);
    assign out1 = in1 | in2;
  endmodule
  ```
  <img width="553" alt="Screenshot 2024-10-29 at 5 10 41 PM" src="https://github.com/user-attachments/assets/36590aab-d769-4ad1-952f-ff09df36d000">

  Listing all the cells across all the hierarchies in the design .
  `get_cells * -hier`

  ```tcl
  get_attribute [get_cells _combo_logic] is_hierarchical
  get_attribute [get_cells _combo_logic/U1] is_hierarchical
  ```

  **Clock Distribution**
  <img width="1200" alt="Screenshot 2024-10-29 at 5 12 47 PM" src="https://github.com/user-attachments/assets/ab5fe9ff-2be6-403f-85d9-1ca95835e54a">

  `create_clock -name MY_CLK -per 5 [get_ports CLK]`

  > **Note:** Clocks must be created on the Clock Generators (PLL, OSCILLATORS) or Primary 10 Pins (For External Clocks) Clocks should not be created on hierarchical pins which are not Clock Generators.

  ```tcl
  create_clock -name MY_CLK -per 5 [get_ports CLK];
  set_clock_latency 3 MY_ _CLK; #This is the latency, modelling the clock delay in network
  set_clock_uncertainty 0.5 MY_CLK; # This is for setting the Clock network (skew + Jitter)
  ```

### Clock Waveforms
> **Note:** 50% DC clock starting phase is <br>

`create_clock —name MYCLK -per 10 [get_ports clk]`
<img width="434" alt="Screenshot 2024-10-29 at 5 17 11 PM" src="https://github.com/user-attachments/assets/350ee75f-40ea-4992-be2f-1b225b61de52">

> **Note:** 50% DC clock starting phase is low<br>

`create_clock -name MYCLK -per 10 [get_ports clk] -wave {5 10}`
<img width="526" alt="Screenshot 2024-10-29 at 5 17 54 PM" src="https://github.com/user-attachments/assets/d1c5ca2e-bb1b-4838-ad2d-af49d89338f6">

> **Note:** 50% DC clock starting phase is high, starting edge not at O.<br>

`create_clock —name MYCLK -per 10 [get_ports clk] -wave {2.5 7.5}`
<img width="594" alt="Screenshot 2024-10-29 at 5 21 13 PM" src="https://github.com/user-attachments/assets/adc59f98-c0cd-4f2d-abf9-01ba121b598a">

> **Note:** 25% DC clock.<br>

`create_clock -name MYCLK -per 10 [get_ports cik] -wave {0 2.5}`
<img width="519" alt="Screenshot 2024-10-29 at 5 22 46 PM" src="https://github.com/user-attachments/assets/fd2afbfc-586f-48b7-a9f2-90e6cbf781b2">

**Constraining the IO paths**
<img width="1238" alt="Screenshot 2024-10-29 at 5 23 18 PM" src="https://github.com/user-attachments/assets/691b6885-17ba-4d9f-bde5-678d6e7f49e4">

**Input Constraints**

```tcl
set_input_delay -max 3 -clock [get_clocks MY_CLK] [get_ports IN_*];
set_input_delay -min 0.5 -clock [get_clocks MY_CLK] [get_ports IN_*];
set_input_transition -max 1.5 [get_ports IN_*]; set _input_transition -min .75 [get_ports IN_*];
```
> **NOTE:** Both inputs IN_A, IN_B are coming w.r.t clock MY_CLK created on port CLK

**Output Constraints**

```tcl
set_output_delay -max 3 -clock Lget_clocks MY_CLK] [get_ports Out_y];
set _output_delay -min 0.5 -clock [get_clocks MY_CLK] [get_ports Out_y];
set_output_load -max 80 [get_ports Out_y]; set_output_load -min 20 [get_ports Out_yl;
```
> **NOTE:** Output Out_y is generated w.r.t clock MY_CLK created on port CLK.

</details>

----

<details>
  <summary>Design Loading and Clock Network Modelling</summary>

  - Loading design: `get_cells`, `get_ports`, `get_nets`
  - `get_pins`, `get_clocks`, `querying_clocks`
  - `create_clock` waveform
  - Clock Network Modelling: Uncertainty, `report_timing`
  - IO Delays

  **lab8_ciruit.v**
  ```verilog
  module labs circuit (input rst, input clk, input IN_A, input IN_B, output OUT_Y, output out_clk);
  reg REGA, REGB , REGC ;

  always @ (posedge clk, posedge rst)
  begin
    if(rst)
    begin
      REGA <= 1'b0;
      REGB <= 1'b0;
      REGC <= 1`b0;
    end
    else
    begin
      1'bo;
      REGA <= IN_A | IN_B;
      REGB <= IN_A ^ IN B;
      REGC <=! (REGA & REGB);
    end
  end
  assign OUT_Y = ~REGC;
  assign out_clk = clk;
  endmodule
  ```

  <img width="856" alt="Screenshot 2024-10-29 at 5 39 52 PM" src="https://github.com/user-attachments/assets/22c54628-f1f2-4a78-9382-cc521fc33471">

  <img width="1025" alt="Screenshot 2024-10-29 at 5 41 12 PM" src="https://github.com/user-attachments/assets/71c5832d-e3e3-4bce-a541-797c8bce28df">

  `read_verilog lab8_circuit.v`
  <img width="1129" alt="Screenshot 2024-10-29 at 5 45 05 PM" src="https://github.com/user-attachments/assets/d9bc0c0d-5196-437f-95bc-70308b4f4893">

  ```tcl
  link
  compile_ultra
  get_ports *
  ```
  <img width="629" alt="Screenshot 2024-10-29 at 6 35 11 PM" src="https://github.com/user-attachments/assets/10a5c8e3-f9ed-41aa-8c4e-b6caae4f13e5">

  ```tcl
  foreach_in_collections my_ports [get_ports *] {
    set port_name [get_object_name $my_ports]
    echo $port_name
  }
  ```

  <img width="658" alt="Screenshot 2024-10-29 at 6 47 02 PM" src="https://github.com/user-attachments/assets/abd1e35f-7a47-436b-b8b9-2d3b2b4d272f">

  `get_attribute lget_ports rst] direction`
  <img width="659" alt="Screenshot 2024-10-29 at 6 49 06 PM" src="https://github.com/user-attachments/assets/fc7e3c80-aa21-4100-ad8e-27cef54d37aa">

  ```tcl
  foreach_in_collections my_ports [get_ports *] {
  set port_names [get_object_name $my_ports];
  set dir [get_attributes [get_ports $port_names] direction];
  echo $port_names $dir
  }
  ```
  <img width="721" alt="Screenshot 2024-10-29 at 6 57 12 PM" src="https://github.com/user-attachments/assets/81afe923-053c-4b29-9f0c-a56b739a70c5">

  `get_cells *`
  <img width="804" alt="Screenshot 2024-10-29 at 6 58 30 PM" src="https://github.com/user-attachments/assets/35458bac-e91d-4d33-acdb-4034ef413667">
  
  `get_attribute [get_cells U9] is_hierarchical`
  <img width="811" alt="Screenshot 2024-10-29 at 7 00 47 PM" src="https://github.com/user-attachments/assets/920f7d3d-8126-4666-b577-b8b22d7e1a50">

  ```tcl
  get_cells * -hier -filter "is_hierarchical == false"
  get_cells * -hier -filter "is_hierarchical == true"
  ```
  <img width="520" alt="Screenshot 2024-10-29 at 7 04 10 PM" src="https://github.com/user-attachments/assets/f53da4db-5fb6-4b8d-aa61-1dd4951c3527">

  `get_attributes 0hier

  `get_attribute [get_cells REGA_reg] ref_name`
  <img width="488" alt="Screenshot 2024-10-29 at 7 05 29 PM" src="https://github.com/user-attachments/assets/9bb61d43-9764-41c2-8658-e9b887da097d">

  ```tcl
  foreach_in_collection my_cell [get_cells * -hier] {
  set my_cell_name [get_obiect_name $my_cell]:
  set rname [get_attribute [get_cells $my_cell_name] ref_namel;
  echo $my_cell_name $rname;
  }
  ```
  <img width="912" alt="Screenshot 2024-10-29 at 7 09 29 PM" src="https://github.com/user-attachments/assets/9d4dc95f-7209-4cde-9256-55e4c2e263e3">

  ## Design Vision
  <img width="794" alt="Screenshot 2024-10-29 at 7 15 07 PM" src="https://github.com/user-attachments/assets/a21c0f81-ba41-41e5-a884-279df9c87d5f">

  <img width="1296" alt="Screenshot 2024-10-29 at 7 16 30 PM" src="https://github.com/user-attachments/assets/3e9c08d8-e9e0-4951-81b0-4bfaa5aefd90">

  `get_nets *`
  <img width="732" alt="Screenshot 2024-10-29 at 7 17 19 PM" src="https://github.com/user-attachments/assets/0c5a5d7a-a864-496b-9994-3f30da603cfc">

  `all_connected N1`
  <img width="726" alt="Screenshot 2024-10-29 at 7 18 38 PM" src="https://github.com/user-attachments/assets/ab88aad5-78cd-4b40-94d7-3a20240bf40d">

  <img width="1433" alt="Screenshot 2024-10-29 at 7 19 39 PM" src="https://github.com/user-attachments/assets/4a55fe12-7c33-447c-9585-a8922a4d1c18">

  ```tcl
  foreach_in_collection my_pin [all_connected n5] {
  set pin_name [get_object_name $my_pin];
  set dir [get_attribute [get_pins $pin_name] direction];
  echo $pin_name $dir;
  }
  ```
  <img width="1242" alt="Screenshot 2024-10-29 at 7 21 12 PM" src="https://github.com/user-attachments/assets/6959270b-3e6e-4cdc-b69c-08fbeb91bd58">

  `get_pins *`
  <img width="1163" alt="Screenshot 2024-10-29 at 7 22 35 PM" src="https://github.com/user-attachments/assets/f2cc1811-5afc-4462-8f45-28744250f0e5">

  ```tcl
  foreach_in_collection my_pin [get_pins *] {
  set pin_name [get_object_name $my_pin];
  echo $pin_name;
  }
  ```
  <img width="234" alt="Screenshot 2024-10-29 at 7 23 29 PM" src="https://github.com/user-attachments/assets/27526287-e995-4b4c-bf88-6bc3ee32c2af">

  <img width="692" alt="Screenshot 2024-10-29 at 7 26 05 PM" src="https://github.com/user-attachments/assets/c33c21be-0f0b-4543-86a9-8e99b4926fe9">

  **Creating the clock**
    <img width="1110" alt="Screenshot 2024-10-29 at 7 27 49 PM" src="https://github.com/user-attachments/assets/5c3b497c-a6a4-4f50-9c48-26c4efd5c07b">

  `create_clock -name MYCLK -per 10 [get_ports clk]`
    <img width="451" alt="Screenshot 2024-10-29 at 7 29 20 PM" src="https://github.com/user-attachments/assets/efcf5a5a-d101-427c-868c-d9cc6ee98b89">

  `report_clocks *`
    <img width="716" alt="Screenshot 2024-10-29 at 7 33 23 PM" src="https://github.com/user-attachments/assets/fb3c8b49-0c64-41a4-a5eb-452ece1fe96d">

  ```tcl
    foreach_in_collection my_pin [get_pins *] {
      set my_pin_name [get_object_name $my_pin];
      set dir [get_attribute [get_pins $my_pin_name] direction];
      if { [regexp $dir in] } {
        if { [get_attribute [get_pins $my_pin_name] clock ] } {
          set clk [get_attribute [get_pins $my_pin_name] clocks];
          set clk_name [get_object_name $clk];
          echo $my_pin_name $clk_name;
        }
      }
    }
  ```
  <img width="502" alt="Screenshot 2024-10-29 at 7 39 18 PM" src="https://github.com/user-attachments/assets/b9b6944b-9924-4c3e-a1f5-8e133394e3cf">

  <img width="1141" alt="Screenshot 2024-10-29 at 7 41 01 PM" src="https://github.com/user-attachments/assets/77e52f11-89d2-464f-a356-eeabe6bb513a">

  ## Constraning

  **Removed all clocks**
    <img width="900" alt="Screenshot 2024-10-29 at 7 47 43 PM" src="https://github.com/user-attachments/assets/686d3849-9764-4bac-96a3-37aa44ea7f7b">

  `report_timing -to REGB_reg/D`
    <img width="839" alt="Screenshot 2024-10-29 at 8 15 49 PM" src="https://github.com/user-attachments/assets/3a079a85-b6c5-4255-97f8-d9efb1b5ec49">

  **After creating clock**
  <img width="793" alt="Screenshot 2024-10-29 at 8 21 55 PM" src="https://github.com/user-attachments/assets/abb9ef18-faf6-4f1d-bd76-82ae566b5188">

  <img width="1068" alt="Screenshot 2024-10-29 at 8 23 00 PM" src="https://github.com/user-attachments/assets/af922b86-3878-4e25-9815-d17ac5bfe01f">

  ```tcl
    set_clock_latency -source 2 [get_clocks MYCLK]
    set_clock_latency 1 [get_clocks MYCLK]
    set_clock_uncertainty -setup 0.5 [get_clocks MYCLK]
    set_clock_uncertainty -hold 0.1 [get_clocks MYCLK]
  ```
  <img width="686" alt="Screenshot 2024-10-29 at 8 30 45 PM" src="https://github.com/user-attachments/assets/a08553ed-2966-4512-9a4c-888142df479a">

  **Explaination**
    <img width="1204" alt="Screenshot 2024-10-29 at 8 32 20 PM" src="https://github.com/user-attachments/assets/f02105ac-5a67-4b49-b145-bad7d669e626">

  ### Modelling the inputs
  > Before modeling the inputs
  `report_port -verbose`
    <img width="728" alt="Screenshot 2024-10-29 at 8 38 52 PM" src="https://github.com/user-attachments/assets/02e65a80-e3cd-49d6-bb8c-f49817079e21">

  ```tcl
    set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_A]
    set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_B]
  ```
  > After modeling the inputs
     <img width="726" alt="Screenshot 2024-10-29 at 8 41 57 PM" src="https://github.com/user-attachments/assets/23c4521e-d2a1-48c2-9907-fc99f75ef6e3">

  `report_timing -from IN_A`
    <img width="650" alt="Screenshot 2024-10-29 at 8 45 35 PM" src="https://github.com/user-attachments/assets/24992d5c-96b8-4d85-8da9-2b4ac60d29c7">

  **Delay**
  ```tcl
    set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports IN_B]
    set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports IN_A]
  ```
  <img width="736" alt="Screenshot 2024-10-29 at 8 52 22 PM" src="https://github.com/user-attachments/assets/b5b9e1e5-8536-4206-89bc-ac9798477757">
  <img width="628" alt="Screenshot 2024-10-29 at 8 54 15 PM" src="https://github.com/user-attachments/assets/12544743-e7cd-4dbc-9322-983df3ba566b">

  **Input Transition**
  ```tcl
    set_input_transition max 0.3 [get_ports IN_A]
    set_input_transition max 0.3 [get_ports IN_B]
    set_input_transition min 0.1 [get_ports IN_A]
    set_input_transition min 0.1 [get_ports IN_B]
  ```
  <img width="584" alt="Screenshot 2024-10-29 at 9 00 20 PM" src="https://github.com/user-attachments/assets/f0769d95-c598-4070-8788-2921c3f2320e">

  **Output Delay**
  ```tcl
    set_output_ delay -max 5 -clock [get_clocks MYCLK] [get_ports OUT_Y]
    set_output_delay -min 1 -clock [get_clocks MYCLK] [get_ports OUT_Y]
  ```
  <img width="624" alt="Screenshot 2024-10-29 at 9 04 32 PM" src="https://github.com/user-attachments/assets/0d508787-066f-422f-a965-34acc90c9776">

  **Load**
  `set_load -min 0.1 [get_ports OUT_Y]`
    <img width="616" alt="Screenshot 2024-10-29 at 9 06 26 PM" src="https://github.com/user-attachments/assets/acee1fa4-4f74-4722-b8a6-c23d7f47c35e">

</details>

----

<details>
  <summary>SDC Part 3: Generated Clocks</summary>

  - **SDC Part 3**: `generated_clk`, `generated_clocks`
    <img width="1437" alt="Screenshot 2024-10-29 at 9 11 05 PM" src="https://github.com/user-attachments/assets/4e9f7666-496e-4ef6-bc86-0121d2ee4e4f">

    **Creating generated clock**
    <img width="1418" alt="Screenshot 2024-10-29 at 9 12 03 PM" src="https://github.com/user-attachments/assets/3a6ccb40-4c0e-496c-8339-8b19e7fe0624">

    **Constraining the design**
    <img width="888" alt="Screenshot 2024-10-29 at 9 13 13 PM" src="https://github.com/user-attachments/assets/dccda2d3-9b81-40d2-9b12-bbd66073f033">
    - IN_DATA, IN_CLK has 2 functionalities
    - In one functionality the IN_DATA and IN_CLK gets the data and clock corresponding to A and in other functionality it gets data and clock corresponding to B
    - Same for OUT_DATA, OUT_CLK (can get from A or from B) .
    - Note the common sel line !

      **How the clocks are propogated**
        - Once a clock is created on a pin / port, DC will propagate that clock downstream based on the timing arcs.
        - All the timing arcs from the definition point will see the clock propagation by default.

      > In the above design, while operating for 'A', the clock and data from the input goes only towards A <br>
      > While operating for 'B', the clock and data from input goes only towards 'B'.<br>
      > Never to both places simultaneously!<br>

    `create_generated_clock -name MYGEN_CLK -master MYCLK -source [get_ports clk] -div 1 [get_ports out_clk]`
    <img width="588" alt="Screenshot 2024-10-29 at 9 17 59 PM" src="https://github.com/user-attachments/assets/890a0833-e498-4d3d-8966-bc93b7a8d45f">

    `get_attribute [get_clocks MYGEN_CLK] is_generated`<br>
    True

    `get_attribute [get_clocks MYCLK] is_generated`<br>
    False

    ```tcl
    set_ clock_latency -max 1 [get_clocks MYGEN_CLK]
    set_output_delay -max 5 [get_ports OUT_Y] -clock [get_clocks MYGEN_CLK] 
    set_output_delay -min 1 [get_ports OUT_Y] -clock [get_clocks MYGEN_CLK]
    ```
    <img width="516" alt="Screenshot 2024-10-29 at 9 24 25 PM" src="https://github.com/user-attachments/assets/58daa98b-74e1-4499-a2e4-076128d36186">

    **All used commands**
    ```tcl
    create_clock -name MYCLK - per 10 [get_ports clk];
    set_clock_latency -source 2 [get_clocks MYCLK];
    set_clock_latency 1 [get_clocks MYCLK]:
    set_clock_uncertainty -max 0.5 [get_clocks MYCLK];
    set_clock_uncertainty -min 0.1 [get_clocks MYCLK];
    set input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_A];
    set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_B];
    set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports IN_A];
    set_input_delay -min 1 -clock [get_clocks MYCLK] [get ports IN B];
    set_input_transition -max 0.4 [get_ports IN_A];
    set_input_transition -max 0.4 [get_ports IN A];
    set_input_transition -min 0.1 [get_ports IN_B];
    set input transition -min 0.1 [get ports IN B];
    create_generated_clock -name MYGEN_CLK -master MYCLK -source [get_ports clk] -div 1 [get_ports out_clk];
    create_generated_clock -name MYGEN_DIV_CLK -master MYCLK -source [get_ports clk] -div 2 [get_ports out_div_clk];
    set_output_delay -max 5 -clock [get_clocks MYGEN_CLK] [get_ports OUT_Y];
    set_output_delay -min 1 -clock [get_clocks MYGEN_CLK] [get_ports OUT_Y];
    set load -max 0.4 [get ports OUT_Y];
    set_load -min 0.1 [get_ports OUT_Y];
    ```
    <img width="563" alt="Screenshot 2024-10-29 at 9 30 43 PM" src="https://github.com/user-attachments/assets/743bfa51-70eb-4b4c-8fd1-92ae5adf902a">

</details>

----

<details>
  <summary>SDC Part 4: VCLK and IO Delays</summary>

  - **SDC Part 4**: `vclk`, max_latency, rise_fall IO Delays
  - Part 1: Set_Max_delay
  - `VCLK`
    
    **Input Delays**
    <img width="1440" alt="Screenshot 2024-10-29 at 9 51 22 PM" src="https://github.com/user-attachments/assets/149bf919-5957-4e40-b484-4854723d1e97">

    **Output Delays**
    <img width="1440" alt="Screenshot 2024-10-29 at 9 53 40 PM" src="https://github.com/user-attachments/assets/9b6101fa-7c97-4504-8bad-69d05f5a00e3">
    
    <img width="1420" alt="Screenshot 2024-10-29 at 9 56 00 PM" src="https://github.com/user-attachments/assets/c972a16f-d139-4097-b02f-0aaf3685eeb0">
    
    <img width="1404" alt="Screenshot 2024-10-29 at 9 56 25 PM" src="https://github.com/user-attachments/assets/a0603a9b-c36d-456e-8969-89f6d1ce7860">

    **set_driving_cell**
    <img width="867" alt="Screenshot 2024-10-29 at 9 57 27 PM" src="https://github.com/user-attachments/assets/de7cd147-2d42-4351-b993-68f88c6434e9">
    **Recommended for Top level primary IOs**
    `set_input_transition -max 0.15 [get_ports IN_A]`

    **Recommended for module level IOs**
    ```tcl
    set_driving_cell -lib_cell <lib_cell_name>, <ports>
    set_driving_cell -lib_cell sky130_fd_sc_hd_buf_1 [all_inputs]
    ```

    `all_fanout -flat -endpoints_only -from IN_A`
    <img width="963" alt="Screenshot 2024-10-29 at 10 02 55 PM" src="https://github.com/user-attachments/assets/6a0f54c8-55df-4530-8bcd-3a4f715a34b6">
    <img width="739" alt="Screenshot 2024-10-29 at 10 03 27 PM" src="https://github.com/user-attachments/assets/6e1850d4-1feb-4eb0-bb4f-07f394483763">
    `report_timing -to OUT_Z -sig 4`
    <img width="539" alt="Screenshot 2024-10-29 at 10 04 00 PM" src="https://github.com/user-attachments/assets/ea55a410-d289-44d4-9860-09fcaad2734c">

    `design_vision`
    <img width="663" alt="Screenshot 2024-10-29 at 10 05 00 PM" src="https://github.com/user-attachments/assets/0b30939f-1730-49c1-88c9-34391bc6188a">

    `report_timing -from IN_C - to OUT_Z`
    <img width="541" alt="Screenshot 2024-10-29 at 10 06 03 PM" src="https://github.com/user-attachments/assets/08bdb98a-e6e0-4a83-8ed8-82c99dd8a9a7">

</details>
