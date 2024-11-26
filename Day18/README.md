# Design Library Cell Using Magic Layout and Ngspice Characterization  

## Overview  
This section focuses on designing a custom inverter standard cell using Magic Layout and characterizing its performance with Ngspice simulations. It includes layout exploration, SPICE extraction, post-layout simulations, and addressing Design Rule Check (DRC) issues.  

---

## Tasks and Steps  

### Clone Custom Inverter Design Repository  
**Steps:**  
- Navigate to the OpenLane working directory.  
- Clone the repository containing the custom inverter design.  
- Copy the necessary Magic technology file (`sky130A.tech`) for the SkyWater PDK.  
- Open the custom inverter layout in Magic for exploration.  

**Commands:**  

```bash
cd Desktop/work/tools/openlane_working_dir/openlane
```
<img width="760" alt="Screenshot 2024-11-27 at 2 25 11 AM" src="https://github.com/user-attachments/assets/04f0fa7c-4ce3-4b82-852e-cd386de11850">

---

```
git clone https://github.com/nickson-jose/vsdstdcelldesign  
```
<img width="736" alt="Screenshot 2024-11-27 at 2 25 33 AM" src="https://github.com/user-attachments/assets/3b59ac0c-f266-4a13-a72d-dd5150e0ff9d">

---

```
cd vsdstdcelldesign  
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .  
magic -T sky130A.tech sky130_inv.mag &
```

<img width="732" alt="Screenshot 2024-11-27 at 2 26 22 AM" src="https://github.com/user-attachments/assets/27519ed7-1bec-402e-b4f8-26578076da61">

---

### Load and Explore the Custom Inverter Layout

  - Open the layout in Magic and identify key components:
    - PMOS and NMOS transistors.
      ![Screenshot from 2024-11-20 13-17-48](https://github.com/user-attachments/assets/9fae2dcd-06f9-42a6-9122-9d1c1140b50e)

    - Connectivity of the output (Y) to the drains of PMOS and NMOS.
      ![Screenshot from 2024-11-20 13-20-32](https://github.com/user-attachments/assets/65c59a32-2818-4246-b0a4-5bac2ce48d1a)

    - Source connections to VDD (PMOS) and VSS (NMOS).
      <img width="758" alt="Screenshot 2024-11-27 at 2 30 23 AM" src="https://github.com/user-attachments/assets/de4aab3f-6e11-491f-b61b-1b3ca13598eb">

  - Introduce layout errors deliberately to observe DRC violations.
    <img width="727" alt="Screenshot 2024-11-27 at 2 30 57 AM" src="https://github.com/user-attachments/assets/86b6de50-a758-4f29-be11-7f19bbbbfc88">

### SPICE Extraction of the Inverter Layout

  - Use Magic’s extract and ext2spice commands to extract a SPICE netlist.
  - Ensure parasitic elements are included in the extraction for accurate simulations.


**Commands (in Magic’s TKCon window)**

# Check current directory
`pwd`

<img width="698" alt="Screenshot 2024-11-27 at 2 35 49 AM" src="https://github.com/user-attachments/assets/379650a2-4636-4181-b001-802e1a4ab4cc">

# Extraction command to extract to .ext format
`extract all`

<img width="366" alt="Screenshot 2024-11-27 at 2 36 05 AM" src="https://github.com/user-attachments/assets/970639f0-87a2-41c1-b3bd-5356679bee64">

# Before converting ext to spice this command enable the parasitic extraction also
```
ext2spice cthresh 0 rthresh 0
ext2spice
```
<img width="285" alt="Screenshot 2024-11-27 at 2 36 57 AM" src="https://github.com/user-attachments/assets/c036f872-c3f9-4af0-85cc-4344ad2e4a3e">

## Spice file

```
* SPICE3 file created from sky130_inv.ext - technology: sky130A
.option scale=10m
.subckt sky130 inv A Y VPWR VGND
xo Y A VGND VGND sky130_fd_pr_nfet_01v8 ad=1.44n pd=0.152m as=1.37n ps=0.148m w=35 l=23
X1 Y A VPWR VPWR sky130
Co A VPWR 0.0774f
_fd_pr.
_pfet_01v8 ad=1.44n pd=0.152m as=1.52n ps=0.156m w=37 l=23
C1 Y VPWR 0.117f
C2 A Y 0.0754f
C3 Y VGND 0.279f
C4 A VGND 0.45f
C5 VPWR VGND 0.781f .ends
```

### Edit the SPICE Model for Simulation

  - Modify the SPICE file to ensure compatibility with Ngspice.
    
```
* SPICE3 file created from sky130 inv.ext - technology: sky130A
* Scale adjusted as per magic layout grid unit distance
-option scale=0.01u
* Including our custom inverter pmos and nmos libs .include ./libs/pshort.lib .include ./libs/nshort.lib
//.subckt sky130_inv A Y VPWR VGND
* Changing pmos and nmos to included library model names and subckt names
M1000 Y A VPwR VPWR pshort_model.0 w=37 l=23
*ad=1.44n pd=0.152m as=1.52n ps=0. 156m
M1001 Y A VGND VGND nshort_model. 0 w=35
1=23
* ad=1.44n pd=0.152m as=1.37n ps=0.148m
* Adding VDD & VSS for simulation
VDD VPWR 0 3.3V
VSS VGND 0 OV
* Adding load capacitance to remove spikes in output
C6 Y 0 2fF
* Defining input pulse
Va A VGND PULSE(OV 3.3V 0 0.1ns 0.1ns 2ns 4ns)
Co A VPWR 0.0774fF
C1 Y VPWR 0.117FF
C2 A Y 0.0754FF
C3 Y VGND 0.279fF
C4 A VGND 0.45fF
C5 VPWR VGND 0.781fF
// .ends
* Specifying the type of analysis to be performed
.tran in 20n
.control
run
.endc
.end
```

  - Measure unit distances in the layout grid for accuracy.
    ![Screenshot from 2024-11-25 15-21-04](https://github.com/user-attachments/assets/b8821845-9128-46f5-bdad-adbbe92cc131)

---

### Post-Layout Simulations Using Ngspice

Steps:

  - Load the SPICE netlist in Ngspice.
  - Simulate and plot output (y) vs. time.
  - Calculate:
    - Rise and fall transition times.
    - Rise and fall cell delays.
   
**Commands**

```
ngspice sky130_inv.spice  
plot y vs time a
```

![Screenshot from 2024-11-20 21-05-38](https://github.com/user-attachments/assets/deee9fdd-6670-4861-8d16-8c28230e4681)

**Formulas**

**Rise Transition Time:**

```math
Rise\ Time = Time\ at\ 80\% - Time\ at\ 20\%
```

**Fall Transition Time:**

```math
Fall\ Time = Time\ at\ 20\% - Time\ at\ 80\%
```

**Rise Cell Delay:**

```math
Rise\ Delay = Time\ at\ Output\ 50\% - Time\ at\ Input\ 50\%
```

**Fall Cell Delay:**

```math
Fall\ Delay = Time\ at\ Output\ 50\% - Time\ at\ Input\ 50\%
```

![Screenshot from 2024-11-20 21-24-02](https://github.com/user-attachments/assets/0af0ea85-25e6-4040-993d-c0880dce6796)
![Screenshot from 2024-11-20 21-23-52](https://github.com/user-attachments/assets/501c513b-7e8a-4724-a86a-308126d138c8)
![Screenshot from 2024-11-20 21-13-22](https://github.com/user-attachments/assets/7ef9ac72-9929-4cbe-ac02-9e7403e16fd0)
![Screenshot from 2024-11-20 21-11-47](https://github.com/user-attachments/assets/76257db8-6723-4dbb-b32d-634d37f2b9dd)
![Screenshot from 2024-11-20 21-11-21](https://github.com/user-attachments/assets/a913b317-2c5d-4d95-8c14-215ce641cc84)
![Screenshot from 2024-11-20 21-11-15](https://github.com/user-attachments/assets/8f3b7041-3b41-4ea8-a65e-c2c930390e80)

---

### Address DRC Issues in Magic Tech File

Steps:

	•	Download the drc_tests files for troubleshooting.
	•	Inspect and modify rules in the sky130A.tech file for correcting DRC checks.
	•	Reload the updated tech file in Magic and rerun DRC checks.


































