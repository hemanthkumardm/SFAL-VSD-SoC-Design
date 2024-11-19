# CMOS Inverter Design and Characterization Labs

This repository contains labs and projects related to CMOS design, simulation, and layout creation using Magic, ngspice, and Sky130 technology files.

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

**SPICE deck creation for CMOS invertor**

---

### Component connectivity

<img width="285" alt="Screenshot 2024-11-19 at 8 58 11 PM" src="https://github.com/user-attachments/assets/79a09ed5-3c80-4be3-a236-02e77cb08fc6">

### Component values

<img width="312" alt="Screenshot 2024-11-19 at 8 58 41 PM" src="https://github.com/user-attachments/assets/7ad77073-1356-4c1f-bc53-14cc3b4b3473">

<img width="388" alt="Screenshot 2024-11-19 at 8 59 08 PM" src="https://github.com/user-attachments/assets/f93f1a74-292f-4885-9649-8df6b9a7376a">

### Identify the nodes

<img width="483" alt="Screenshot 2024-11-19 at 8 59 26 PM" src="https://github.com/user-attachments/assets/1394a1e5-baaa-4461-9278-57089e6cc2df">

### Naming nodes

<img width="343" alt="Screenshot 2024-11-19 at 8 59 43 PM" src="https://github.com/user-attachments/assets/ec15f6e9-1e07-4f50-b4db-2831af3417dc">

---

## SPICE DECK

```
*** MODEL Descriptions ***
*** NETLIST Description ***
Ml out in vdd vdd pmos W=0.375u L=0.25u
M2 out in 0 0 nmos W=0.375u L=0.25u

cload out 0 10f

vdd udd 0 2.5
Vin in 0 2.5
*** SIMULATION Commands ***
.op
.dc Vin 0 2.5 0.05
*** .include tsmc_025um _model.mod ***
.LIB "tsmc 025um model.mod" CMOS_MODELS
.end
```

## SPICE simulation

SPICE waveform : Wn=Wp=0.375u, Ln,p=0.25u device (Wn/Ln=Wp/Lp = 1.5)

<img width="871" alt="Screenshot 2024-11-19 at 9 04 28 PM" src="https://github.com/user-attachments/assets/c4dda6a3-4317-4ddf-bdc8-97fe451efbd0">

SPICE waveform : Wn=0.375, Wp=0.9375u, Ln,p=0.25u device (Wn/Ln=1.5, Wp/Lp = 2.5)

<img width="871" alt="Screenshot 2024-11-19 at 9 05 40 PM" src="https://github.com/user-attachments/assets/cfcf9cb3-37ec-4e54-8d76-f9e0e51feaf6">

---

## Switching threshold VM

<img width="1385" alt="Screenshot 2024-11-19 at 9 09 24 PM" src="https://github.com/user-attachments/assets/a40c953f-0469-4d5d-9d4f-79ba9f7e380a">

<img width="1440" alt="Screenshot 2024-11-19 at 9 11 14 PM" src="https://github.com/user-attachments/assets/cd642a28-4d41-4991-bad5-3815aa8d2de1">

---

`git clone https://github.com/nickson-jose/vsdstdcelldesign.git`

 copy the sky130A.tech from `/openlane_working_dir/pdks/sky130A/libs.tech/magic` file to `/openlane_working_dir/vsdstdcelldesign/` directory

 `magic -T sky130A.tech sky130_inv.mag &`
 
 <img width="375" alt="Screenshot 2024-11-19 at 9 30 06 PM" src="https://github.com/user-attachments/assets/adae7058-a395-4781-b509-fc8d6c8d4cbf">

</details>

<details>
<summary><strong>3. Inception of Layout – CMOS Fabrication Process</strong></summary>

This lab introduces the basics of CMOS layout design, covering:
- The CMOS fabrication process steps (oxidation, diffusion, etching, etc.).
- Understanding design layers in Magic.
- Creating the layout of a simple CMOS circuit (e.g., an inverter) using design rules.

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
