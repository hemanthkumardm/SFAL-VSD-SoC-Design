# VSDBabySoC Design and Modeling

VSDBabySoC is a small yet powerful RISC-V-based SoC designed to integrate three open-source IP cores. This project showcases the modeling, synthesis, and physical design flow of the SoC, leveraging open-source tools and Nangate45nm PDKs.

---

## Table of Contents

- <details>
  <summary>Introduction</summary>

  ### What is VSDBabySoC?
  VSDBabySoC is a compact SoC featuring:
  - **RVMYTH**: A simple RISC-V-based CPU core.
  - **PLL**: An 8x Phase-Locked Loop for stable clock generation.
  - **DAC**: A 10-bit Digital-to-Analog Converter for interfacing with analog devices.

  Its primary purpose is to integrate and test these IPs collaboratively and calibrate the analog part of the SoC.

  ![Diagram Placeholder]()

  ---
  
  ### What is an SoC?
  An SoC (System on Chip) is a single-die chip that combines multiple IP cores, ranging from digital microprocessors to analog broadband modems.

  ### Key Components
  - **RVMYTH**: A RISC-V-based CPU core created by students during a workshop by RedwoodEDA and VSD.
  - **PLL**: Synchronizes clock signals using phase relationships.
  - **DAC**: Converts digital signals to analog for communication with analog systems.

  </details>

- <details>
  <summary>VSDBabySoC Modeling</summary>

  ### Overview
  - **Design Flow**: Physical Design performed using IC Compiler II (ICC2).
  - **PDKs**: Initially planned with SAED32_28nm, switched to Nangate45nm due to compatibility issues.
  - **Workflow**: Integration of digital (RVMYTH) and analog (DAC, PLL) blocks.

  ### Workflow Breakdown
  1. Input signals initialize the SoC.
  2. PLL generates a stable clock for RVMYTH.
  3. RVMYTH processes instructions and sends values to the DAC.
  4. DAC outputs the final signal.

  ---
  
  **Note**: Currently, the modeling focuses on RVMYTH due to DAC and PLL compatibility challenges.

  </details>

- <details>
  <summary>Modeling Details</summary>

  ### RVMYTH Modeling
  - Created in **TL-Verilog** and converted to Verilog using SandPiper SaaS.
  - Reference repository: [RVMYTH GitHub](#)

  ### DAC Modeling
  - Synthesized with **Design Compiler** and verified with **PrimeWave**.
  - Reference repository: [DAC GitHub](#)

  ### PLL Modeling
  - Simulated using real datatype for analog design verification.
  - Reference repository: [PLL GitHub](#)

  </details>

- <details>
  <summary>Lab Instructions</summary>

  ### Getting Started with VSDBabySoC

  #### Exporting LEF Files
  - For DAC and PLL (Analog Blocks):
    1. Navigate to **Custom Compiler (CC)**.
    2. Go to `Export > LEF` and `Export > Stream`.
  - For RVMYTH (Digital Block):
    1. Use the `rvmyth.v` file.
    2. Write the `vsdbabysoc.v` code integrating `rvmyth`, `PLL`, and `DAC`.

  ---
  
  #### Gate-Level Synthesis
  - Run **Design Compiler**:
    ```bash
    dc_shell> source vsdbabysoc.tcl
    ```
    - Output: `vsdbabysoc_gtlvl.v` (Synthesis file)
  
  ---
  
  #### Physical Design
  - Run **IC Compiler II**:
    ```bash
    icc2_shell> source top.tcl
    ```
    - Executes the complete Physical Design Flow.

  ---
  
  **Notes**:
  - All `.tcl` scripts are available in the repository.
  - The results and methodology will be detailed in future updates.

  </details>

---

## Results, Conclusions, and Future Work

- Initial results and challenges faced during the design process are documented.
- Future iterations aim to integrate DAC and PLL files successfully.

---

### References
- [RVMYTH Reference](#)
- [DAC Reference](#)
- [PLL Reference](#)
