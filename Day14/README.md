# Day 14 OpenLANE EDA Tool: Simplified Overview

This file provides a basic understanding of the open-source EDA, the RTL to GDSII flow, and the key components used in digital ASIC design with the Sky130 PDK.

---

<details>
<summary>Inception of Open-Source EDA, OpenLANE, and Sky130 PDK</summary>

#### How to Talk to Computers


- **QFN-48 Package**: Outer part of a chip for connecting to the outside world.
<img width="416" alt="Screenshot 2024-11-15 at 3 42 19 PM" src="https://github.com/user-attachments/assets/e866dfb1-e6e1-4790-9c68-59c1ff2b660d">
<img width="791" alt="Screenshot 2024-11-15 at 3 42 30 PM" src="https://github.com/user-attachments/assets/b75909ff-c09d-4b36-98e4-0d1e45943cc2">

- **Chip**: Contains pads and the core (where digital logic resides
<img width="699" alt="Screenshot 2024-11-15 at 3 42 46 PM" src="https://github.com/user-attachments/assets/9ca6fb7c-b1dc-4f17-b1f2-a0971976f12e">
<img width="560" alt="Screenshot 2024-11-15 at 3 42 57 PM" src="https://github.com/user-attachments/assets/8a8ffbc9-1c6e-44b2-8ff6-8f0a8a8af30a">

- **IP (Intellectual Property)**: Pre-designed, reusable circuit blocks.
  - **Soft IP**: Synthesizable HDL code.
  - **Hard IP**: Fixed, pre-verified layout designs.
  - **Firm IP**: A mix of soft and hard IP.
<img width="477" alt="Screenshot 2024-11-15 at 3 44 53 PM" src="https://github.com/user-attachments/assets/7612eee1-420a-49b9-a48f-7242cd2571d7">


#### Introduction to RISC-V
- A processor architecture implemented using HDLs like Verilog.
- Programs are compiled from C to assembly, then to binary for execution.
<img width="875" alt="Screenshot 2024-11-15 at 3 53 24 PM" src="https://github.com/user-attachments/assets/a439df06-e183-4db1-accd-bd4c5b88a7de">
<img width="982" alt="Screenshot 2024-11-15 at 3 54 39 PM" src="https://github.com/user-attachments/assets/7271f0ae-757e-4c09-bdc9-04e877beb038">
<img width="982" alt="Screenshot 2024-11-15 at 3 55 06 PM" src="https://github.com/user-attachments/assets/206bd345-0c3b-418a-9c78-2ec7673f09b1">


#### From Software Applications to Hardware
- Applications (e.g., Microsoft Excel) run through system software:
  - **Compiler**: Converts high-level code to hardware instructions.
  - **Assembler**: Converts instructions to machine-readable binary.
<img width="980" alt="Screenshot 2024-11-15 at 3 56 23 PM" src="https://github.com/user-attachments/assets/65bbb347-df5c-4933-affe-2a07ced7762b">
<img width="914" alt="Screenshot 2024-11-15 at 3 57 12 PM" src="https://github.com/user-attachments/assets/a017f97d-aa1b-455e-9056-2679ebe33d2a">
<img width="985" alt="Screenshot 2024-11-15 at 3 59 00 PM" src="https://github.com/user-attachments/assets/997200b1-fe00-4d6b-b25a-0429aa75607c">


</details>

<details>
<summary>SoC Design and OpenLANE</summary>

### Components of Digital ASIC Design

In digital ASIC design, three key components play a crucial role: **RTL**, **EDA tools**, and **PDK**.

<img width="559" alt="Screenshot 2024-11-15 at 5 15 06 PM" src="https://github.com/user-attachments/assets/2302a238-ea24-4c88-8e1c-079990bc74db">

#### **1. RTL (Register Transfer Level)**
RTL represents the hardware design's functional description written in high-level hardware description languages like Verilog or VHDL. It describes the digital circuits in terms of data flow between registers and logical operations.

- **Sources of RTL**:
  - [LibreCores](https://librecores.org): Open community for hardware IPs.
  - [OpenCores](https://opencores.org): Repository for open-source RTL projects.
  - [GitHub](https://github.com): Platform to find numerous RTL designs shared by developers worldwide.

#### **2. EDA (Electronic Design Automation) Tools**
EDA tools are software applications used for designing, simulating, verifying, and synthesizing digital circuits. Open-source EDA tools like **OpenLANE** streamline the RTL to GDSII design process.

#### **3. PDK (Process Design Kit)**
PDK acts as the bridge between chip designers and the semiconductor fabrication facilities (FABs). It provides all the necessary rules, files, and resources needed to design manufacturable chips.

- **Definition**:
  - During the early days of IC design ("age of Gods"), chip design was tightly integrated with proprietary manufacturing processes.
  - Pioneers like Lynn Conway and Carver Mead introduced the concept of separating design from technology, leading to the evolution of pure-play fabs (independent manufacturers) and fabless design companies.
  - The PDK represents the interface between the FAB and designers, enabling this separation.

- **Open-Source PDK Example**:
  - [Google Skywater 130nm PDK](https://github.com/google/skywater-pdk): Open-source production PDK for the 130nm process node.

#### **Is 130nm Old?**
Yes, 130nm is considered an older technology node, but it is still widely used for educational, research, and low-cost applications.

#### **Is 130nm Fast?**
Yes, despite being older:
- **Intel's Pentium 4 Extreme Edition (2004)** achieved 3.46 GHz using 130nm technology.
<img width="149" alt="Screenshot 2024-11-15 at 5 11 54 PM" src="https://github.com/user-attachments/assets/11f75594-5d0a-4c5b-9f6a-ffb8678b0903">

- **OSU Research** reported a post-layout clock frequency of 327 MHz for a single-cycle RV32 CPU on 130nm, with potential for >1 GHz in a pipelined design.
<img width="602" alt="Screenshot 2024-11-15 at 5 12 03 PM" src="https://github.com/user-attachments/assets/2dc39846-19b2-4a5f-bd54-0a576e2a0430">

---

### ASIC Design Flow (RTL to GDSII)

<img width="414" alt="Screenshot 2024-11-15 at 5 16 22 PM" src="https://github.com/user-attachments/assets/0893d67a-76a2-43b2-8caf-ca706dff1768">

1. **Synthesis**: Transform RTL code into a gate-level netlist.
2. **Floor/Power Planning**: Organize functional blocks and design the power distribution network.
3. **Placement**: Determine the exact positions of standard cells and macros.
   - **Global Placement**: Approximate positioning of cells.
   - **Detailed Placement**: Final legal positioning of cells.
4. **Clock Tree Synthesis (CTS)**: Design the clock distribution network for synchronized operation.
5. **Routing**: Connect the placed cells using metal layers.
6. **Sign-Off**: Perform final verification checks before fabrication.


#### PDK Key Components
- **Technology Files**: Define process parameters.
- **Design Rules**: Guidelines for manufacturability.
- **Device Models**: SPICE models for simulation.
- **Standard Cell Libraries**: Basic building blocks.
- **IO Libraries**: For communication with the external world.
- **Memory Compilers**: Tools for creating memory blocks.

#### Simplified RTL to GDSII Flow

### Key Components of ASIC Design

#### **Technology Files**:
These define the physical and electrical parameters of the semiconductor process. They include the layer stack, design rules, and process variations.

#### **Design Rules**:
Guidelines that ensure the manufacturability of a design. They include constraints like minimum width, spacing, and enclosure for different layers and features, making sure that the chip can be successfully fabricated.

#### **Device Models**:
SPICE (Simulation Program with Integrated Circuit Emphasis) models are used for simulating the behavior of devices like transistors, capacitors, and resistors under different operating conditions.

#### **Standard Cell Libraries (SCL)**:
These are collections of pre-designed and characterized logic gates (AND, OR, NOT), flip-flops, and other essential components used to build complex digital circuits.

#### **IO Libraries**:
These libraries contain pre-designed input/output (I/O) cells that allow communication between the chip and the outside world. They include various types of I/O cells like power pads and analog interfaces.

#### **Memory Compilers**:
These tools are used to generate customized memory blocks (e.g., SRAM, ROM) based on specific design requirements, allowing for flexibility and optimization.

---

### **Synthesis**
Synthesis is the process of converting **RTL** (Register Transfer Level) code into a gate-level netlist using components from the **Standard Cell Library (SCL)**. The result is a functional representation of the circuit, mapped onto physical components.

<img width="899" alt="Screenshot 2024-11-15 at 5 18 15 PM" src="https://github.com/user-attachments/assets/9943eb9d-9d04-4510-9d15-7d1986460cef">

- **Standard Cells**: Have a regular, predefined layout.
- Each standard cell can have multiple views/models:
  - **Electrical Model**: Describes how the cell behaves electrically.
  - **HDL Model**: Describes the functionality of the cell in hardware description languages (Verilog/VHDL).
  - **SPICE Model**: Simulates the electrical behavior in detail.
  - **Layout Models**: Include abstract and detailed views, showing how the cell fits into the physical design.
<img width="349" alt="Screenshot 2024-11-15 at 5 18 43 PM" src="https://github.com/user-attachments/assets/6f0cc644-1cb0-4eb4-93b7-e49bbc05e773">
---

### **Floor and Power Planning**

#### **Chip Floor-Planning**:
In this step, the chip die is partitioned into different system building blocks, and the **I/O pads** (pads used for external connections) are placed.

<img width="867" alt="Screenshot 2024-11-15 at 5 20 45 PM" src="https://github.com/user-attachments/assets/c0bb4baa-e18c-428e-9174-68a77a8f1b6f">

#### **Macro Floor-Planning**:
This focuses on defining the **dimensions**, **pin locations**, and **row definitions** for the macros used in the design.

<img width="277" alt="Screenshot 2024-11-15 at 5 21 09 PM" src="https://github.com/user-attachments/assets/8f10c98d-da7c-4445-af4e-f65709d11059">

#### **Power Planning**:
Power planning involves designing the distribution of power throughout the chip, ensuring that all components receive sufficient and stable power. This includes defining the power grid and routing the necessary metal layers to distribute power efficiently.

<img width="502" alt="Screenshot 2024-11-15 at 5 21 57 PM" src="https://github.com/user-attachments/assets/6f0b55fe-46ee-4fe4-905c-ba24b8aefd2b">

---

### **Placement**
Placement involves placing the standard cells on the floorplan rows, aligning them with designated sites. Placement is done in two main steps:

<img width="716" alt="Screenshot 2024-11-15 at 5 23 10 PM" src="https://github.com/user-attachments/assets/cf8178d6-aff6-4ce6-aecb-3f3c83d1fea7">

- **Global Placement**: Places cells in approximate positions.
- **Detailed Placement**: Fine-tunes the placement to ensure legal positioning of cells and optimization of area, power, and timing.

<img width="620" alt="Screenshot 2024-11-15 at 5 25 51 PM" src="https://github.com/user-attachments/assets/dabae384-194d-4324-b4be-a1a33b22199e">

---

### **Clock Tree Synthesis (CTS)**
Clock Tree Synthesis is responsible for creating a **clock distribution network** that ensures all sequential elements (e.g., flip-flops) receive a synchronized clock signal. The goal is to minimize clock skew, which is the difference in timing of the clock signal at various parts of the chip. Achieving zero skew is difficult, but minimizing it is critical.
- The clock distribution network is usually structured as a tree (H-tree, X-tree, etc.).

<img width="258" alt="Screenshot 2024-11-15 at 5 26 26 PM" src="https://github.com/user-attachments/assets/0545e625-08ad-4943-b8e5-823529f3a864">

---

### **Routing**
Routing implements the interconnects between placed cells using the available metal layers. A **routing grid** is established for the chip, and the metal tracks are used to create the physical connections between cells.
- **Global Routing**: Generates routing guides that show the preferred routing paths.
- **Detailed Routing**: Uses the global routing guides to implement the actual wiring between the cells.

 <img width="778" alt="Screenshot 2024-11-15 at 5 27 02 PM" src="https://github.com/user-attachments/assets/888ab9b0-2cfd-492d-8936-5d084159a0e2">

---

### **Sign-Off**
At this stage, various physical and timing verifications are performed to ensure that the design is ready for fabrication.

#### **Physical Verifications**:
- **Design Rule Checking (DRC)**: Ensures that the design adheres to the manufacturing process's design rules.
- **Layout vs. Schematic (LVS)**: Verifies that the layout matches the schematic and that the design functions as intended.

#### **Timing Verification**:
- **Static Timing Analysis (STA)**: Ensures that the chip meets the required timing constraints, like ensuring data paths between registers are fast enough for the clock frequency.

---

### Introduction to OpenLANE and Strive Chipsets

#### **OpenLANE**
OpenLANE began as an open-source flow designed for a true open-source tape-out experiment. It provides a complete digital ASIC design flow, enabling users to design chips with open-source tools and resources. OpenLANE supports the SkyWater 130nm Open PDK (Process Design Kit), allowing users to design ASICs using a freely available process.

The flow is containerized for ease of use and designed to be functional out of the box. It is designed to produce clean GDSII files with no human intervention, ensuring that there are no LVS (Layout vs. Schematic) or DRC (Design Rule Checking) violations. The flow is continually improved, and new design examples are added regularly.

<img width="858" alt="Screenshot 2024-11-15 at 5 54 46 PM" src="https://github.com/user-attachments/assets/14e2a7dc-089b-4e8c-ba16-638b72545b99">

#### **Strive SoC Family**
The Strive family is a collection of open-source SoCs (System on Chips), designed to support the OpenLANE flow. Strive SoCs aim to provide a completely open ecosystem for hardware design, supporting Open PDK, Open EDA (Electronic Design Automation), and Open RTL.

**Strive SoC Models:**
| SoC Model     | Features                                     |
|---------------|----------------------------------------------|
| **Strive**    | Sky130 SCL + Synthesized 1 Kbytes SRAM       |
| **Strive 2**  | Sky130 SCL + 1 Kbytes OpenRAM block          |
| **Strive 2a** | Strive 2 with a single chip core module      |
| **Strive 3**  | OSU SCL + Synthesized 1 Kbytes SRAM         |
| **Strive 5**  | Sky130 SCL + 8 x 1 Kbytes OpenRAM banks     |
| **Strive 6**  | Strive 2 with DFT (Design for Test)         |

#### **OpenLANE ASIC Flow**
The main goal of OpenLANE's ASIC flow is to produce a clean GDSII file with no human intervention. This means that the flow ensures:
- No LVS Violations
- No DRC Violations
- Timing Violations: Currently a work-in-progress

**Key Features of OpenLANE:**
- **Tuned for SkyWater 130nm Open PDK**: OpenLANE is optimized for the SkyWater 130nm open-source process, but it also supports other process nodes like XFAB180 and GF130G.
- **Containerized**: The flow comes in a containerized format, ensuring it works immediately without complicated setup. It also includes instructions for building and running the flow natively.
- **Macro and Chip Hardening**: OpenLANE can be used to harden macros and chips, making them ready for production.
- **Two Modes of Operation**:
  - **Design Space Exploration**: This mode provides a large number of design examples with configurations optimized for performance and area.
  - **43 Designs**: The flow currently includes 43 design examples, each with its best configuration. More examples are continuously being added.

<img width="901" alt="Screenshot 2024-11-15 at 5 51 41 PM" src="https://github.com/user-attachments/assets/a48f4024-19ca-45c3-902d-69db4010791a">

This open-source toolset ensures that users can design digital ASICs with minimal manual intervention, supporting a variety of use cases from basic exploration to complex chip design.

---

### Introduction to OpenLANE Detailed ASIC Design Flow

The OpenLANE ASIC design flow starts with RTL synthesis, where tools like **Yosys** and **ABC** are used to convert RTL (Register Transfer Level) code into a gate-level netlist.

#### **Synthesis Exploration:**
This phase generates reports that provide insights into the design’s performance, area, and power consumption.

<img width="836" alt="Screenshot 2024-11-15 at 5 59 35 PM" src="https://github.com/user-attachments/assets/dd44932d-9ab8-47e0-b832-6cc213b6293e">


**Design Exploration**:  
Used to evaluate different design configurations to optimize for various goals, such as power, performance, and area.
  
<img width="810" alt="Screenshot 2024-11-15 at 5 59 41 PM" src="https://github.com/user-attachments/assets/d169387e-3d42-40de-82cb-36e6c39a6efc">

#### **OpenLANE Regression Testing:**
The design exploration utility is also used for regression testing. OpenLANE runs on approximately 70 different designs and compares the results to previously known best configurations, ensuring consistency and reliability across different design iterations.

<img width="339" alt="Screenshot 2024-11-15 at 6 11 59 PM" src="https://github.com/user-attachments/assets/bf81cdaa-ee67-4663-b18e-dea9493cf53e">

#### **DFT (Design for Test):**
- **Scan Insertion**: Adds scan chains to the design for testing its functionality during manufacturing.
- **ATPG (Automatic Test Pattern Generation)**: Automatically generates test patterns to verify the functionality of the design.
- **Test Patterns Compaction**: Reduces the number of test patterns while maintaining fault coverage.
- **Fault Coverage**: Measures how well the generated tests cover potential faults in the design.
- **Fault Simulation**: Simulates potential faults to ensure the design works as expected.

<img width="870" alt="Screenshot 2024-11-15 at 6 01 14 PM" src="https://github.com/user-attachments/assets/ae7948a4-d21d-4d79-a4a1-a95a985e8d8b">


#### **Physical Implementation (Automated Place and Route):**
Physical implementation, also known as **Place and Route (PnR)**, involves the following steps:
- **Floor/Power Planning**: Defines the chip's layout and power distribution network.
- **End Decoupling Capacitors and Tap Cells Insertion**: Ensures the power network is stable and that the chip is properly grounded.
- **Placement (Global and Detailed)**: Places standard cells and macros onto the floorplan in two stages—global and detailed placement.
- **Post-Placement Optimization**: Refines placement to reduce wire lengths and improve performance.
- **Clock Tree Synthesis (CTS)**: Designs the clock network to synchronize the operation of sequential elements.
- **Routing (Global and Detailed)**: Routes the metal connections between placed cells in two stages—global routing and detailed routing.

These steps are all carried out using **OpenROAD**, a suite of open-source tools for physical design.


#### **Logic Equivalence Check (LEC):**
Every time the netlist is modified (e.g., during CTS or post-placement optimization), it is crucial to perform a **Logic Equivalence Check (LEC)** to verify that the function of the design has not changed. This is done using **Yosys** to ensure that modifications do not introduce logical errors.

#### **Dealing with Antenna Rules Violations:**
When a metal wire segment is fabricated, it can accumulate charge during the etching process, potentially damaging transistor gates. This phenomenon is known as **Antenna Effect**.

<img width="504" alt="Screenshot 2024-11-15 at 6 04 56 PM" src="https://github.com/user-attachments/assets/99bf61b7-497f-42f2-b819-9f0ebacf74fd">
<img width="604" alt="Screenshot 2024-11-15 at 6 06 02 PM" src="https://github.com/user-attachments/assets/f7e18852-f467-4381-bd3c-26c4bd650278">

To prevent this:
- A **Fake Antenna Diode** is added next to every cell input after placement.
- **Magic**, a layout verification tool, is used to run an **Antenna Checker** on the routed layout.
- If a violation is detected, the Fake Antenna Diode is replaced with a real one.

<img width="347" alt="Screenshot 2024-11-15 at 6 14 38 PM" src="https://github.com/user-attachments/assets/2eb1d07b-2d58-49ca-8c89-33599b6d7941">

#### **Physical Verification: DRC & LVS**
- **Design Rules Checking (DRC)**: Performed using **Magic** to ensure that the design meets all the manufacturing process rules.
- **LVS (Layout vs. Schematic)**: Ensures that the layout matches the original schematic design. This is done using **Magic** and **Netgen**.
- **SPICE Extraction**: Magic also extracts the SPICE model from the layout to simulate and verify the design’s electrical behavior.

![Physical Verification Image](image-link) <!-- Image for DRC and LVS -->

---

</details>

<details>
<summary>Get Familiar with Open-Source EDA</summary>

---

#### OpenLANE Directory Structure

The directory structure of OpenLANE is organized as follows:

`cd /Desktop/work/tools/openlane_working_dir/`
```txt
│
├── openlane/
│   └── (OpenLANE related tools and scripts)
│
└── pdks/
├── skywater-pdk/
│   └── (SkyWater 130nm PDK files)
│
├── open_pdks/
│   └── (General open-source PDKs for other technologies)
│
└── sky130A/
└── (Specific to SkyWater 130nm technology, contains design libraries
```

## Explanation of Each Directory and Its Contents

### **openlane/**

This directory contains the main OpenLANE tools and scripts for the digital ASIC design flow. It includes the following major components:
- **Synthesis tools** (e.g., Yosys, ABC)
- **Floorplanning and placement tools** (e.g., OpenROAD)
- **Routing tools** (e.g., OpenROAD routing)
- **Timing and verification tools** (e.g., OpenSTA)
- **Regression testing and design exploration tools**
- **Script and configuration files** for managing the entire design flow, from RTL to GDSII.

OpenLANE works by orchestrating these tools to automate the ASIC design flow, aiming to produce clean GDSII files with no human intervention. The **openlane/** folder acts as the core of the OpenLANE flow.

### **pdks/**

This directory contains the Process Design Kits (PDKs) needed for designing chips. These kits are specific to different foundries and process nodes, and they provide the necessary design rules, libraries, and resources to ensure that the designs are manufacturable.

#### **skywater-pdk/**

The **skywater-pdk/** directory contains the PDK for the **SkyWater 130nm** process. This directory includes:
- **Technology files**: Contain design rules and specifications for the 130nm process.
- **Standard cell libraries**: Pre-designed logic cells for digital designs.
- **Device models**: SPICE models used for simulations.
- **IO libraries**: Pre-designed I/O cells for communication between the chip and external components.
- **Memory compilers**: Tools for generating memory blocks (e.g., SRAM, ROM) for use in the design.

This PDK is critical for creating designs that are compatible with the SkyWater 130nm process.

#### **open_pdks/**

This directory holds general open-source PDKs for different technologies. These PDKs provide the basic components and design rules for various semiconductor processes. The **open_pdks/** folder may contain multiple subdirectories for different processes and technologies, which allows for flexible support of various design flows.

#### **sky130A/**

The **sky130A/** directory is specific to the **SkyWater 130nm** technology and contains important files and resources for this process node. It includes:
- **Design libraries**: Collections of pre-designed digital logic cells optimized for the SkyWater 130nm process.
- **Design rules**: Guidelines on minimum sizes, spacing, and other constraints for chip manufacturing at 130nm.
- **Process information**: Details on process technology, including transistor models and performance characteristics.

This directory is essential for ensuring that designs meet the requirements of the SkyWater 130nm foundry and that they are manufacturable using the corresponding technology.

---

#### Design Preparation

```
cd /Desktop/work/tools/openlane_working_dir/openlane`
docker
```
<img width="523" alt="Screenshot 2024-11-15 at 7 04 18 PM" src="https://github.com/user-attachments/assets/035a4006-9f6b-4060-b368-9bba9c0c8a08">

Run the script `./flow.tcl -interactive`
<img width="498" alt="Screenshot 2024-11-15 at 7 06 32 PM" src="https://github.com/user-attachments/assets/34b5f4bb-1871-47d4-b2bd-29686333ba21">

`package require 0.9`
<img width="212" alt="Screenshot 2024-11-15 at 7 07 44 PM" src="https://github.com/user-attachments/assets/918e91e0-56af-43a6-a9ec-6859f125b60c">

Prepare the design (picorv32a) `prep -design picorv32a`
<img width="625" alt="Screenshot 2024-11-15 at 7 14 56 PM" src="https://github.com/user-attachments/assets/6271af91-ebab-4dd0-9a40-31d45c07ab96">

After preparation runs dir will be created
<img width="723" alt="Screenshot 2024-11-15 at 7 18 45 PM" src="https://github.com/user-attachments/assets/8a648798-586e-4ca6-931d-59da8a6d0de9">

Each runs will have each dir with date and runtime
<img width="686" alt="Screenshot 2024-11-15 at 7 20 05 PM" src="https://github.com/user-attachments/assets/a6614f8e-896c-40cd-9c85-820a8319b50d">

Start the synthesis `run_synthesis`
<img width="1328" alt="Screenshot 2024-11-15 at 7 24 59 PM" src="https://github.com/user-attachments/assets/c04adc40-8a0c-437e-8939-576882b62617">

Detailed explanation [here](https://github.com/efabless/openlane)
Detailed explanation [video-1](https://www.youtube.com/watch?v=EczW2IWdnOM) [video-2](https://www.youtube.com/watch?v=Vhyv0eq_mLU)

Finding flop ratio:
```
  flop ratio = number of DFF/total number of cell
               1613 / 14876 = 0.1084296854
               in percentile 10.84296854%
```

Synthesized netlist
`cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/`
Check reports/synthesis/.stat.rpt and results/synthesis/picorv32a.synthesis.v

<img width="820" alt="Screenshot 2024-11-15 at 7 45 49 PM" src="https://github.com/user-attachments/assets/74416ac3-98b7-4184-9500-e871bc0ee427">

<img width="399" alt="Screenshot 2024-11-15 at 7 47 09 PM" src="https://github.com/user-attachments/assets/b07be4ee-2815-4851-b87b-872a5b791496">

---
#### Tools in OpenLANE
- **Yosys**: Converts RTL to a gate-level netlist.
- **OpenROAD**: Physical design tools (placement, CTS, routing).
- **Magic**: Layout and physical verification.
- **OpenSTA**: Timing analysis.

---
</details>
