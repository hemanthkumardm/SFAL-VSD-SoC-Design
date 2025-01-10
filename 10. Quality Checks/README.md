<details>
  <summary>Quality Checks</summary>
  
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

  `report timing -sig 4 -nosplit -trans -cap -nets - inp > tl.rpt`
  <img width="594" alt="Screenshot 2024-10-30 at 8 17 50 AM" src="https://github.com/user-attachments/assets/7d5300b4-b032-48c6-9104-5c9f880b8eca">

  `report_timing -sig 4 -nosplit -trans -cap -nets -inp -from IN_A > t1. rpt`
  <img width="594" alt="Screenshot 2024-10-30 at 8 18 26 AM" src="https://github.com/user-attachments/assets/b3d142bf-4e9a-424c-a28f-026424dfa5cd">

  `report_timing - rise_from IN_A -sig 4 -trans -cap -nets - inp > t2. rpt`
  <img width="597" alt="Screenshot 2024-10-30 at 8 18 58 AM" src="https://github.com/user-attachments/assets/1607fcd9-8a02-417e-8af3-1aeafffaab8f">

  `report_timing -delay min -from IN_A1`
  <img width="529" alt="Screenshot 2024-10-30 at 8 20 06 AM" src="https://github.com/user-attachments/assets/7d5e2261-ad7b-4a3f-bc68-114e13eda2d3">

  `report_timing - thr U15/Y`
  <img width="533" alt="Screenshot 2024-10-30 at 8 26 15 AM" src="https://github.com/user-attachments/assets/88486d96-8cbb-4e18-a00f-47073f3766d6">

</details>
