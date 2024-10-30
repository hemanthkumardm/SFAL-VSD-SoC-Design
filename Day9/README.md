# Day 9 - Quality Checks

<details>
  <summary>DC_D5SK1</summary>
  
  - **Lecture - Report Timing**
    **Generating Timing Reports**
    ```tcl
    report_timing-from DFF_A/clk
    report_timing -from DFF_A/clk -to DFF_C/d
    report_timing -fall_from DFF_A/clk
    report_timing -rise_from DFF_B/clk
    report_timing -delay_type min -to DFF_C/d
    report_timing -delay_type min -through INV/a
    report_timing -delay_type max -through AND/b
    report_timing -rise_from DFF_B/clk -delay_type max -nets -cap -trans -sig 4
    ```

    **Timing Paths**
  - **Lab - Report Timing**
  - **Lab - Check_timing, Check_design, Set_max_capacitance, HFN**

</details>
