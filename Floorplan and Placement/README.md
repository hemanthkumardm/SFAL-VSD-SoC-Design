
### **Tasks Overview:**
1. Perform floorplan for the `picorv32a` design using OpenLANE and generate the outputs.
2. Calculate the die area in microns using floorplan values.
3. Load and explore the generated floorplan in the Magic tool.
4. Perform congestion-aware placement for the design using OpenLANE and generate the outputs.
5. Load and explore the generated placement in the Magic tool.

---

### **Key Formula:**
To calculate the **die area in microns**:
```math
Area\ of\ die = Die\ width\ in\ microns \times Die\ height\ in\ microns
```

---

# Logs and Results

Perform Floorplan Using OpenLANE

```
run_floorplan
```

<img width="684" alt="Screenshot 2024-11-27 at 2 12 12 AM" src="https://github.com/user-attachments/assets/5d6b2366-6af4-470a-b18e-21c4bf068757">

---
# Calculate Die Area in Microns

	1.	Use the floorplan DEF file to find the die width and die height in unit distances.
	2.	Convert the values into microns (1 micron = 1000 unit distance).
	3.	Apply the formula to calculate the die area.

**Sample Calculation**

  - Die Width in Units: 660685
  - Die Height in Units: 671405

```math
Die\ width\ in\ microns = \frac{660685}{1000} = 660.685
```
```math
Die\ height\ in\ microns = \frac{671405}{1000} = 671.405
```
```math
Area\ of\ die = 660.685 \times 671.405 = 443587.21\ \text{Square Microns}
```

---
# Load Floorplan in Magic Tool

Load the floorplan DEF file into Magic using the following commands:

```
# Go to the directory with the generated floorplan DEF
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Load floorplan DEF in Magic
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

<img width="361" alt="Screenshot 2024-11-27 at 2 16 15 AM" src="https://github.com/user-attachments/assets/cd9fa85b-75f2-4937-b56e-ccc94399ce2f">

---

# Placement

`run_placement`

![Screenshot from 2024-11-20 12-56-23](https://github.com/user-attachments/assets/1585dcae-6d8e-496d-b97c-07f48ee713ad)

**Load Placement in Magic Tool**

```
# Go to the directory with the generated placement DEF
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

# Load placement DEF in Magic
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

![Screenshot from 2024-11-20 12-57-05](https://github.com/user-attachments/assets/57c043c5-753a-4106-96d4-595a1de5c782)

![Screenshot from 2024-11-20 12-57-34](https://github.com/user-attachments/assets/8d127ce3-8c96-4f31-925e-6c3983ed99af)

---



