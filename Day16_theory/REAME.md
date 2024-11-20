# CMOS Inverter Design and Characterization Labs

## Design Library Cell using Magic Layout and ngspice Characterization

<details>

<summary><strong>1. Labs for CMOS Inverter ngspice Simulations</strong></summary>

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

---

<details>
<summary><strong>2. Inception of Layout – CMOS Fabrication Process</strong></summary>

This lab introduces the basics of CMOS layout design, covering:
- The CMOS fabrication process steps (oxidation, diffusion, etching, etc.).
- Understanding design layers in Magic.
- Creating the layout of a simple CMOS circuit (e.g., an inverter) using design rules.

### Create active regions

**Step 1:** Selecting a substrate

<img width="918" alt="Screenshot 2024-11-19 at 9 37 27 PM" src="https://github.com/user-attachments/assets/a741bac3-2b7b-4505-b984-18f77fb6c706">

 > Substrate doping should be less than 'well' doping. Coming in further sections

<img width="911" alt="Screenshot 2024-11-19 at 9 38 15 PM" src="https://github.com/user-attachments/assets/ba70afcf-70ec-4e9c-820e-d11c7480c007">

---

**Step 2:** Creating active region for transistors

<img width="1440" alt="Screenshot 2024-11-19 at 9 53 34 PM" src="https://github.com/user-attachments/assets/ac4c774f-4327-4535-9e8e-a0b07f939d86">

<img width="1440" alt="Screenshot 2024-11-19 at 9 54 09 PM" src="https://github.com/user-attachments/assets/8131fd67-fcd8-418c-90e7-767014fd4d5f">

**Remove the mask**

<img width="1440" alt="Screenshot 2024-11-19 at 9 54 28 PM" src="https://github.com/user-attachments/assets/34e6748b-4fd2-4708-a967-c1ad2ce7f73e">

**Etched off Si3N4**

<img width="1440" alt="Screenshot 2024-11-19 at 9 55 40 PM" src="https://github.com/user-attachments/assets/4f1d5a0e-0192-4724-a79e-cd3697abcaf9">

**Remove photo resist**

<img width="1440" alt="Screenshot 2024-11-19 at 9 56 09 PM" src="https://github.com/user-attachments/assets/2208479c-aa35-433d-88b0-47d623017421">

**Placed in oxidation furnace**

<img width="1440" alt="Screenshot 2024-11-19 at 9 57 00 PM" src="https://github.com/user-attachments/assets/95932075-eca6-4f84-96c9-44182086f3a1">

Field oxide is grownThis process is called "LOCOS" "Local Oxidation of Silicon"

<img width="1440" alt="Screenshot 2024-11-19 at 9 58 22 PM" src="https://github.com/user-attachments/assets/d6a92ef3-6efe-4591-9f70-66fec8049fcb">

**Si3N4 stripped using hot phosphoric acid**

<img width="1440" alt="Screenshot 2024-11-19 at 9 58 46 PM" src="https://github.com/user-attachments/assets/cc3e88be-bb32-49db-8a9b-79a98dec466e">

---

**Step 3:** N-well and P-well formation

<img width="1440" alt="Screenshot 2024-11-19 at 10 00 00 PM" src="https://github.com/user-attachments/assets/b144a6d1-b560-4497-b76a-f2bfd0172032">

<img width="1440" alt="Screenshot 2024-11-19 at 10 01 13 PM" src="https://github.com/user-attachments/assets/d6f6328e-6bf7-4e30-8826-8c94f1014179">

<img width="1440" alt="Screenshot 2024-11-19 at 10 01 03 PM" src="https://github.com/user-attachments/assets/4a229ead-a445-45c4-82b8-4e2ac9ac49b1">

<img width="1440" alt="Screenshot 2024-11-19 at 10 01 27 PM" src="https://github.com/user-attachments/assets/5715c110-54c5-490f-b899-db108ec19579">

<img width="1440" alt="Screenshot 2024-11-19 at 10 01 39 PM" src="https://github.com/user-attachments/assets/48773ff6-deb5-48aa-a8fc-0f05e18f5cc8">

**Boron P type material**

<img width="1440" alt="Screenshot 2024-11-19 at 10 01 47 PM" src="https://github.com/user-attachments/assets/349da6f3-2e8d-4fe9-8f92-43b30754f80f">

<img width="1440" alt="Screenshot 2024-11-19 at 10 02 15 PM" src="https://github.com/user-attachments/assets/46209153-43c5-4145-854c-b5c69cfb9141">

**Phosphorous N type material**

<img width="1440" alt="Screenshot 2024-11-19 at 10 03 58 PM" src="https://github.com/user-attachments/assets/199c4787-53f4-4bd2-80e1-ed0bc67f3a3b">

<img width="1440" alt="Screenshot 2024-11-19 at 10 04 31 PM" src="https://github.com/user-attachments/assets/267cffa0-f1e1-4c1e-a01b-5e23d6606017">

**Twin tub process**

<img width="1440" alt="Screenshot 2024-11-19 at 10 04 52 PM" src="https://github.com/user-attachments/assets/18b2a33b-99c9-4b1e-9857-2abd780ff05f">

---

**Step 4:** Formation of Gate terminal

<img width="1440" alt="Screenshot 2024-11-19 at 10 06 22 PM" src="https://github.com/user-attachments/assets/a61c9e53-3ae8-4533-b3b1-9b557d80df40">

<img width="1440" alt="Screenshot 2024-11-19 at 10 08 12 PM" src="https://github.com/user-attachments/assets/e41244eb-eafd-4a19-9ea8-e09eb9373fb3">

<img width="1440" alt="Screenshot 2024-11-19 at 10 09 27 PM" src="https://github.com/user-attachments/assets/9d8b6a65-e3d3-43a2-aefa-8375a4b18d2a">

Original oxide etched/stripped using dilute hydrofluoric (HF) solution

<img width="1440" alt="Screenshot 2024-11-19 at 10 10 02 PM" src="https://github.com/user-attachments/assets/e1dfca0a-2b9f-4c4a-bc7d-17558c5f7ea9">

<img width="1440" alt="Screenshot 2024-11-19 at 10 10 27 PM" src="https://github.com/user-attachments/assets/2ace40c8-23fa-487a-b8e8-3ddaa8f9dba9">

<img width="1440" alt="Screenshot 2024-11-19 at 10 10 45 PM" src="https://github.com/user-attachments/assets/b272bc21-a42f-4ab8-9fda-6f7503544518">

<img width="1440" alt="Screenshot 2024-11-19 at 10 11 17 PM" src="https://github.com/user-attachments/assets/8dc3afa9-a436-4702-9411-15a1071d9175">

<img width="1440" alt="Screenshot 2024-11-19 at 10 11 33 PM" src="https://github.com/user-attachments/assets/a6812e5a-0302-4cc5-904e-25838a5a9ef1">

<img width="1440" alt="Screenshot 2024-11-19 at 10 12 01 PM" src="https://github.com/user-attachments/assets/7859df1d-dbd4-45a8-b91e-c3ddddb66787">

---

**Step 5:** Lightly doped drain (LDD) formation

<img width="1440" alt="Screenshot 2024-11-19 at 10 20 54 PM" src="https://github.com/user-attachments/assets/61c13d94-884b-4565-977b-6b413b990492">

<img width="1440" alt="Screenshot 2024-11-19 at 10 21 35 PM" src="https://github.com/user-attachments/assets/edd38155-b8a2-4d29-9a8c-0a707d9365cf">

<img width="1440" alt="Screenshot 2024-11-19 at 10 21 49 PM" src="https://github.com/user-attachments/assets/071a2f5f-8329-42dc-8e29-99c618e3e2fc">

<img width="1440" alt="Screenshot 2024-11-19 at 10 22 02 PM" src="https://github.com/user-attachments/assets/7a6b52e9-055b-4ae8-815d-b9923ca39c6b">

<img width="1440" alt="Screenshot 2024-11-19 at 10 22 25 PM" src="https://github.com/user-attachments/assets/34879903-1625-4848-8d71-e4f774818d6c">

**Step 6:** Source and Drain formation

<img width="1440" alt="Screenshot 2024-11-19 at 10 30 22 PM" src="https://github.com/user-attachments/assets/90d1c5f6-6492-4d5a-84d9-5d5983804e32">

<img width="1440" alt="Screenshot 2024-11-19 at 10 30 42 PM" src="https://github.com/user-attachments/assets/2a90a848-0db7-4541-8123-6659eea9a43e">

**Step 7:** Local interconnect formation

<img width="1440" alt="Screenshot 2024-11-19 at 10 32 28 PM" src="https://github.com/user-attachments/assets/c02251a2-a94a-4944-a04d-633b64455dcd">

<img width="1440" alt="Screenshot 2024-11-19 at 10 32 36 PM" src="https://github.com/user-attachments/assets/bdb5ccda-2b30-4594-bd2c-2bf7ab161f38">

<img width="1440" alt="Screenshot 2024-11-19 at 10 32 55 PM" src="https://github.com/user-attachments/assets/5709e558-494a-436e-aa72-f35f391ea3ad">

<img width="1440" alt="Screenshot 2024-11-19 at 10 34 20 PM" src="https://github.com/user-attachments/assets/7a097287-9642-42f4-8cd1-91b7ae39c2a6">

<img width="891" alt="Screenshot 2024-11-19 at 10 34 55 PM" src="https://github.com/user-attachments/assets/2b62bd24-aaa6-41ab-9a7b-4a151ca0c95d">

<img width="1440" alt="Screenshot 2024-11-19 at 10 35 12 PM" src="https://github.com/user-attachments/assets/514af00c-3970-4edd-8b29-b3ddf8c6bc76">

**Higer level metal formation**

<img width="1440" alt="Screenshot 2024-11-19 at 10 36 08 PM" src="https://github.com/user-attachments/assets/19c84433-a54a-4a23-afad-6dedce282932">

<img width="1440" alt="Screenshot 2024-11-19 at 10 36 48 PM" src="https://github.com/user-attachments/assets/f3ba54a8-5238-4b9c-8c2d-dcd190d4892e">

<img width="1440" alt="Screenshot 2024-11-19 at 10 37 15 PM" src="https://github.com/user-attachments/assets/4a3a8421-dd23-4d68-931a-622540c42a6f">

<img width="1440" alt="Screenshot 2024-11-19 at 10 37 51 PM" src="https://github.com/user-attachments/assets/196bda78-1c98-4406-9323-07de00c4800c">

<img width="1440" alt="Screenshot 2024-11-19 at 10 38 00 PM" src="https://github.com/user-attachments/assets/8f8d840a-335e-4b43-b178-166913f6f539">

Again Chemical mechanical polishing (CMP) technique for planarizing wafer surface

<img width="950" alt="Screenshot 2024-11-19 at 10 38 26 PM" src="https://github.com/user-attachments/assets/e50828a1-578a-499b-b461-8e6f15f4982b">

<img width="1440" alt="Screenshot 2024-11-19 at 10 39 16 PM" src="https://github.com/user-attachments/assets/4c828ed2-ff8c-4dd1-897c-0c8f88048eab">

<img width="1440" alt="Screenshot 2024-11-19 at 10 39 31 PM" src="https://github.com/user-attachments/assets/4c999562-590d-4faa-869e-15f86c4506f3">

<img width="1440" alt="Screenshot 2024-11-19 at 10 40 02 PM" src="https://github.com/user-attachments/assets/d9ae2a73-95b4-4077-a08b-1834349daadd">

---

In tkcon

`extract all`
to generate sky130_inv.ext

`ext2spice cthresh 0 rthresh 0`
`ext2spice sky130_inv.ext`
to generate sky130_inv.spice

<img width="283" alt="Screenshot 2024-11-19 at 11 04 51 PM" src="https://github.com/user-attachments/assets/c3cb59c0-45cb-4a35-a07b-9d25d1f85f61">

</details>

---

<details>
<summary><strong>3. Sky130 Tech File Labs</strong></summary>

Sky130 is an open-source PDK (Process Design Kit) provided by Google and SkyWater Technology. This lab includes:
- Setting up the Sky130 technology file in Magic.
- Designing and simulating circuits using Sky130-specific layers.
- Verifying designs with Sky130 rules and extracting netlists for simulation.

---

<img width="1440" alt="Screenshot 2024-11-19 at 11 07 36 PM" src="https://github.com/user-attachments/assets/2617ed9f-d460-4998-a730-98cc527e54d2">

<img width="298" alt="Screenshot 2024-11-20 at 12 26 54 AM" src="https://github.com/user-attachments/assets/d48cc13a-7a4e-40aa-bff7-d60b58cf370f">

<img width="379" alt="Screenshot 2024-11-20 at 12 28 36 AM" src="https://github.com/user-attachments/assets/c977b740-107d-43b8-ad7d-82f6a8e37233">

---

**Magic DRC**

[documentation](http://opencircuitdesign.com/magic/)

---

[Magic DRC](http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz)

<img width="636" alt="Screenshot 2024-11-20 at 7 24 49 AM" src="https://github.com/user-attachments/assets/a3a6e475-099a-47f9-a3fc-23a68d214118">





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
