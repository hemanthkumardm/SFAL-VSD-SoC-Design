# DAY16 Labs

### Design Synthesis and Flop Ratio Calculation**

#### **Tasks Overview:**
1. Perform synthesis on the `picorv32a` design using the OpenLANE flow and generate the necessary outputs.
2. Calculate the **Flop Ratio** and the percentage of D Flip-Flops (DFFs).

#### **Formulas:**
The **Flop Ratio** is calculated as:
```math
Flop\ Ratio = \frac{\text{Number of D Flip-Flops}}{\text{Total Number of Cells}}
```

The percentage of DFFs is:

```math
Percentage\ of\ DFF's = Flop\ Ratio * 100
```
---

### Logs and Results

**1. PerformSynthesis on picorv32a Design**

Follow these commands to run synthesis using OpenLANE:

---

# Step 1: Navigate to the OpenLANE directory

```
cd Desktop/work/tools/openlane_working_dir/openlane
```

<img width="1172" alt="Screenshot 2024-11-27 at 1 41 53 AM" src="https://github.com/user-attachments/assets/a15944ae-2484-47f8-9ec0-5013269684c0">

---

# Step 2: Launch the OpenLANE Docker container

```
docker
```

<img width="1299" alt="Screenshot 2024-11-27 at 1 46 49 AM" src="https://github.com/user-attachments/assets/a54133be-3d7e-419f-9853-9bf79adb1c95">

---

# Step 3: Start OpenLANE in interactive mode

```
./flow.tcl -interactive
```

<img width="613" alt="Screenshot 2024-11-27 at 1 48 57 AM" src="https://github.com/user-attachments/assets/a77f457c-9e36-4bc1-96b9-3e2b2726c80b">

---

# Step 4: Load the required packages

```
package require openlane 0.9
```

<img width="331" alt="Screenshot 2024-11-27 at 1 50 26 AM" src="https://github.com/user-attachments/assets/49e605ce-e2b1-4f95-b633-38b6f7b6c2de">

---

# Step 5: Prepare the 'picorv32a' design

```
prep -design picorv32a
```

<img width="734" alt="Screenshot 2024-11-27 at 1 52 08 AM" src="https://github.com/user-attachments/assets/9e8d62c8-086f-4814-b4ad-ed6d830dc14b">

---

# Step 6: Run synthesis

```
run_synthesis
```

<img width="1328" alt="Screenshot 2024-11-27 at 1 53 48 AM" src="https://github.com/user-attachments/assets/35acde85-6383-42a4-9371-4b50f3017c2e">

---

# Calculate the Flop Ratio

From the statistics report:

  - Number of DFFs = 1613
  - Total Number of Cells = 14876
```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```

```math
Percentage\ of\ DFFs = 0.108429685 \times 100 = 10.84\%
```

![Screenshot from 2024-11-26 13-08-36](https://github.com/user-attachments/assets/c1aa637c-02cc-4f79-a60d-47fc2c08d7a9)

---










