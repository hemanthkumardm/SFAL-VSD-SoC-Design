# Day 7 - Advanced Constraints

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

  


  


</details>

----

<details>
  <summary>SDC Part 3: Generated Clocks</summary>

  - **SDC Part 3**: `generated_clk`, `generated_clocks`

</details>

----

<details>
  <summary>SDC Part 4: VCLK and IO Delays</summary>

  - **SDC Part 4**: `vclk`, max_latency, rise_fall IO Delays
  - Part 1: Set_Max_delay
  - `VCLK`

</details>
