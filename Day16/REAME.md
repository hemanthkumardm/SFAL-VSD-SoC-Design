# CMOS Inverter Design and Characterization Labs

This repository contains labs and projects related to CMOS design, simulation, and layout creation using Magic, ngspice, and Sky130 technology files. Below is a brief explanation of each component in a dropdown format.

<details>
<summary><strong>1. Design Library Cell using Magic Layout and ngspice Characterization</strong></summary>

This lab focuses on designing a library cell, such as a CMOS inverter, using Magic Layout editor. The key steps include:
- Creating a physical layout of the circuit.
- Extracting netlists from the layout.
- Characterizing the cell using **ngspice** simulations for delay, power, and performance metrics.

**Key Deliverables**:
- A functional library cell with verified design rules (DRC) and layout-versus-schematic (LVS) checks.
- Simulated performance metrics.

</details>

<details>
<summary><strong>2. Labs for CMOS Inverter ngspice Simulations</strong></summary>

This lab covers the theoretical and practical aspects of CMOS inverter simulation using **ngspice**. Topics include:
- DC Analysis: Understanding the transfer characteristics of the inverter.
- Transient Analysis: Simulating the switching behavior under load.
- Parametric Analysis: Studying how the inverter behaves under variations in supply voltage and input capacitance.

**Key Deliverables**:
- Waveforms for DC, transient, and parametric analysis.
- Detailed observations and analysis reports.

</details>

<details>
<summary><strong>3. Inception of Layout – CMOS Fabrication Process</strong></summary>

This lab introduces the basics of CMOS layout design, covering:
- The CMOS fabrication process steps (oxidation, diffusion, etching, etc.).
- Understanding design layers in Magic.
- Creating the layout of a simple CMOS circuit (e.g., an inverter) using design rules.

**Key Deliverables**:
- A basic CMOS layout designed in Magic.
- Insights into the CMOS fabrication process and its impact on design.

</details>

<details>
<summary><strong>4. Sky130 Tech File Labs</strong></summary>

Sky130 is an open-source PDK (Process Design Kit) provided by Google and SkyWater Technology. This lab includes:
- Setting up the Sky130 technology file in Magic.
- Designing and simulating circuits using Sky130-specific layers.
- Verifying designs with Sky130 rules and extracting netlists for simulation.

**Key Deliverables**:
- Layouts and simulations compliant with the Sky130 PDK.
- Insights into the open-source workflow for chip design.

</details>

---

## Tools and Technologies Used
- **Magic**: For layout design and DRC/LVS checks.
- **ngspice**: For circuit simulations and characterization.
- **Sky130 PDK**: For technology-specific design rules and layer definitions.

## Getting Started
1. Install Magic and ngspice using your preferred package manager or from their official websites.
2. Clone this repository and navigate to the respective lab folder.
3. Follow the instructions in the respective subdirectories for running the simulations and layouts.

Feel free to contribute or raise issues if you encounter any problems!
