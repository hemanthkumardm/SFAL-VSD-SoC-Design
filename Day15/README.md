 # Day 15 - Good Floorplan vs Bad Floorplan and Introduction to Library Cells

---
<details>
  <summary>Chip Floor Planning Considerations</summary>

### Key Considerations
1. **Macro Placement**:
   - Logical and physical proximity to the relevant standard cells.
2. **Power Planning**:
   - Ensure sufficient power delivery using top-level metal layers.
3. **Area Utilization**:
   - Optimal utilization to minimize chip size without causing congestion.
4. **Clock Distribution**:
   - Proper CTS design to minimize skew and latency.


# Chip Floor Planning Considerations

This document provides a explanation of chip floor planning concepts, focusing on defining **core and die dimensions**, calculating the **utilization factor**, and understanding the **aspect ratio**.

---

## Step 1: Define Width and Height of Core and Die

The first step in chip floor planning is defining the **width (W)** and **height (H)** of the core and die. These dimensions are essential to arranging the components effectively.

### Example Setup
- **Netlist**: Contains:
  - 2 Flip-Flops (Launch and Capture)
  - Logic gates between them.

The **dimensions** of the logic gates and flip-flops determine the size of the core. These components are represented as **standard cells**, which typically have a square or rectangular shape.

### Steps to Calculate Dimensions
1. **Assign unit sizes** to standard cells:
   - Assume each standard cell occupies **1 square unit**.
   - Flip-Flops also occupy **1 square unit**.

2. **Calculate total area**:
   - Place all cells together and determine their dimensions:
     - Length = **2 units**
     - Width = **2 units**

3. **Core and Die**:
   - The **core** is the region where all the logic is placed.
   - The **die** encapsulates the core and serves as the silicon base for fabrication.

---

## Utilization Factor

The **utilization factor** measures how efficiently the core area is used by the netlist.

### Formula:

$$
\text{Utilization Factor} = \frac{\text{Area Occupied by Netlist}}{\text{Total Core Area}}
$$

#### Example:

- **Area of Netlist:** `2 x 2 = 4 units²`
- **Total Core Area:** `2 x 2 = 4 units²`
- **Utilization Factor:** `4 / 4 = 1.0` (100% utilization)

**Important Note**: In practical scenarios, utilization factors of **50%-60%** are preferred to allow space for additional cells and optimization.

---

## Aspect Ratio

The **aspect ratio** defines the shape of the core and is calculated as:

\[ \text{Aspect Ratio} = \frac{\text{Height}}{\text{Width}} \]

### Examples:

1. **Square Core**:
   - Height = 2
   - Width = 2
   - Aspect Ratio: `2 / 2 = 1.0` (Square shape)

2. **Rectangular Core**:
   - Height = 2
   - Width = 4
   - Aspect Ratio: `2 / 4 = 0.5` (Rectangle shape)

---

## Practical Observations

1. **100% Utilization**:
   - Core is completely occupied.
   - No extra cells can be added.

2. **50% Utilization**:
   - Core has space for additional logic or optimization.

3. **Aspect Ratio of 1**:
   - Indicates a square core, ideal for uniform designs.

4. **Aspect Ratio < 1 or > 1**:
   - Indicates a rectangular core.

---

## Visual Examples

### Core and Die
<img width="980" alt="Screenshot 2024-11-18 at 7 55 10 AM" src="https://github.com/user-attachments/assets/2c7ba53f-0387-4ad7-9a64-74ca0917f21b">

### converting symbols to physical dimensions
<img width="891" alt="Screenshot 2024-11-18 at 7 57 07 AM" src="https://github.com/user-attachments/assets/c067b057-ba87-4501-b755-4fcc995e60ba">

<img width="920" alt="Screenshot 2024-11-18 at 7 57 28 AM" src="https://github.com/user-attachments/assets/cbda7d28-e44d-4d2e-8149-2512f2a2ab98">


### 100% Utilization Example
<img width="406" alt="Screenshot 2024-11-18 at 7 57 54 AM" src="https://github.com/user-attachments/assets/cd570faf-704f-464b-9b95-8cf30a2654b4">

### 50% Utilization Example
<img width="689" alt="Screenshot 2024-11-18 at 7 58 15 AM" src="https://github.com/user-attachments/assets/183ca829-fdb1-4a7b-850d-d3a76bbbb86c">

### Aspect Ratio Demonstration
<img width="1219" alt="Screenshot 2024-11-18 at 7 58 54 AM" src="https://github.com/user-attachments/assets/11cdea7e-143e-40b5-865e-4d43252c465e">

# Concept of Preplaced Cells

Preplaced cells are critical components in chip design and floor planning. They are specific circuit blocks placed on the chip at predefined locations before the automatic placement and routing process. This ensures their locations remain fixed during further stages of the design.

---

## Understanding Utilization Factor and Aspect Ratio

### Example with a Square Core:
- **Core Dimensions:**
  - Height = 4 units
  - Width = 4 units
- **Netlist Area:**
  - \(2 \times 2 = 4 \, \text{units}^2\)
- **Core Area:**
  - \(4 \times 4 = 16 \, \text{units}^2\)
- **Utilization Factor:**
  - \(4 / 16 = 0.25\) (25% utilization)
  - 25% of the chip is utilized by the netlist, leaving 75% available for additional cells and routing.
- **Aspect Ratio:**
  - Height / Width = \(4 / 4 = 1.0\) (Square shape)
    
<img width="761" alt="Screenshot 2024-11-18 at 8 20 12 AM" src="https://github.com/user-attachments/assets/b74aea74-b35d-4a73-8dc6-bbe8b382860c">

---

## What are Preplaced Cells?

Preplaced cells are specific blocks or components that perform essential functions in the circuit. These can include memory units, multipliers, clock dividers, or other reusable modules. 

<img width="612" alt="Screenshot 2024-11-18 at 8 20 44 AM" src="https://github.com/user-attachments/assets/efd00cbb-f3eb-41f4-8588-661d6fca903b">

<img width="738" alt="Screenshot 2024-11-18 at 8 21 02 AM" src="https://github.com/user-attachments/assets/2c231fe5-dc77-49d8-a76b-13d7b6e67dcc">


### Why Use Preplaced Cells?
1. **Reusability:** 
   - Preplaced cells allow certain circuit blocks to be implemented once and reused multiple times in the design.
   - This avoids redundancy and saves chip area.
2. **Isolation:** 
   - These blocks are separated from the main netlist, making them modular and easier to manage.
3. **Fixed Locations:** 
   - The placement of these cells is fixed before the automatic placement and routing process, ensuring no movement or modification by design tools.
     
<img width="375" alt="Screenshot 2024-11-18 at 8 21 22 AM" src="https://github.com/user-attachments/assets/a74e702c-059b-4136-9651-d4d8d4eb5286">

<img width="594" alt="Screenshot 2024-11-18 at 8 21 46 AM" src="https://github.com/user-attachments/assets/953ec970-ea44-4c1b-82e8-bd63a4902c06">

---

## Example of Preplaced Cells

### Step-by-Step Process:
1. **Circuit Segmentation:**
   - Divide a large circuit (e.g., 100K gates) into smaller, manageable blocks (e.g., 50K gates each).
   - Each block is treated as an independent module.

2. **Blackboxing:**
   - The individual blocks are black-boxed, meaning their internal design is hidden from the top-level design.
   - Input and output pins of these blocks are clearly defined.

3. **Placement on Chip:**
   - The blocks are placed at predefined locations on the chip.
   - The placement ensures optimal connectivity and routing.

4. **Fixing Locations:**
   - Once placed, these cells are locked in position.
   - Automatic placement and routing tools are configured not to alter these locations.

---

## Key Advantages of Preplaced Cells
- **Modularity:** Allows for easier design and debugging.
- **Reusability:** Common blocks can be reused across designs.
- **Optimization:** Frees up remaining chip area for other functions.
- **Routing Simplification:** Ensures clear and efficient interconnections.

---

## Practical Examples of Preplaced Cells
- **Memory Blocks:** Critical for storing data and instructions.
- **Clock Gating Cells:** Used for power optimization.
- **Comparators:** Perform specific comparisons as part of the circuit.
- **Other IPs (Intellectual Properties):** Vendor-provided components integrated into the design.

---

## Why Are They Called Preplaced Cells?
- These cells are placed before the automatic placement and routing process.
- Their positions are fixed during the floor planning stage, and no tool or process moves them afterward.

---

## Decoupling Capacitors in Physical Design

<img width="1123" alt="Screenshot 2024-11-18 at 8 37 56 AM" src="https://github.com/user-attachments/assets/f5b4c892-8b5b-44ae-a494-0c3fcc4af2a1">

Decoupling capacitors are essential components in integrated circuits that ensure the stability and proper functionality of the design by managing power supply noise during switching activities.

### Purpose of Decoupling Capacitors

1. **Supply Stability**:
   - When a circuit transitions (e.g., from logic 0 to logic 1), it requires a sudden surge of current.
   - The primary power supply may not be able to deliver this current instantly due to the physical resistance and inductance of the wires, causing voltage drops. This can result in unstable or incorrect logic levels.

2. **Noise Suppression**:
   - Voltage drops in the power supply can create noise in the circuit, which may cause the logic levels to become undefined. Decoupling capacitors help to mitigate these issues by providing immediate current when the circuit switches, ensuring stable voltage levels.
     
<img width="1158" alt="Screenshot 2024-11-18 at 8 38 42 AM" src="https://github.com/user-attachments/assets/7d5915df-6a8d-4b55-91c4-ff6ba9609270">


### How Decoupling Capacitors Work

- **Charge Reservoir**: A decoupling capacitor acts as a reservoir of charge. It gets charged up to the supply voltage and discharges when the circuit switches, providing the necessary current for the transition.
  
- **Reducing Voltage Drops**: When the power supply cannot deliver the required current in time, the decoupling capacitor supplies the charge to the circuit, minimizing voltage drops and ensuring that the circuit can detect correct logic levels.

- **Replenishing Charge**: After the switching activity, the decoupling capacitor replenishes its charge from the main power supply, preparing for the next switch.
- 
<img width="1357" alt="Screenshot 2024-11-18 at 8 39 04 AM" src="https://github.com/user-attachments/assets/488d48eb-e22f-4eab-af95-8a23298c48f2">

### Placement of Decoupling Capacitors

- Decoupling capacitors should be placed physically close to the blocks that require them, reducing the distance between the power source and the circuit to minimize any potential voltage drops.

- They are commonly placed around the power grid, near sensitive blocks like memories or complex logic, to provide stable and continuous power supply during switching activities.
- 
<img width="994" alt="Screenshot 2024-11-18 at 8 39 26 AM" src="https://github.com/user-attachments/assets/82ad7217-637b-4ed9-abbd-d1f51b806e8a">

#### **Example of Placement**:

```plaintext
Power supply  -->  Decoupling Capacitors  -->  Logic Block
```

#### Benefits of Decoupling Capacitors

  - Stable Switching: They ensure that logic transitions (0 to 1 or 1 to 0) happen without interference from supply noise or voltage drops.
  - Prevent Logic Errors: By maintaining stable voltage levels, decoupling capacitors prevent logic errors that may arise from undefined voltage levels.
  - Improved Reliability: Their presence increases the overall reliability of the circuit by minimizing the effects of power supply fluctuations.

---

## Power Planning in Physical Design

In this section, we explore the problem of current demand and how power planning can help manage voltage drop issues in complex circuits. Specifically, we discuss the effects of having a single power supply line versus multiple power supply lines in a design.

### Problem Statement

We start by considering a circuit where each element requires current. A decoupling capacitor is typically used to supply this current during switching activities. However, when multiple instances of a macro are repeated across the chip, this creates a larger current demand for each element within the circuit. 

For instance, assume we have a macro repeated four times on the chip. Each of these blocks will need to tap into the power supply to maintain the signal integrity when logic transitions occur.

### Signal Integrity and Power Supply Challenges

When a signal transitions from logic 0 to logic 1 (or vice versa), the entire signal line must maintain its integrity to ensure that the load receives the same shape of the signal. This signal line is typically connected to a power supply, which provides the necessary current. However, if the distance between the signal line and the power supply is too long, the signal might suffer from **voltage drops** due to the resistance of the connecting lines.

#### Voltage Drop Scenario

In a typical scenario, a power supply is placed at one point of the circuit, and the power is distributed across multiple blocks. However, if there are multiple blocks and each is demanding current at the same time, there can be a **voltage droop** because the power supply may not be able to meet the demand of all blocks simultaneously. 

Consider the example of a 16-bit bus:

- When the logic of the bus switches, the capacitors that were charged to a logic 1 will discharge to logic 0.
- Since all capacitors switch at the same time, they all demand current from the power supply simultaneously. 
- This can cause a **ground bounce** or voltage droop, which is similar to the situation where multiple water taps are opened at the same time, leading to an increase in water level temporarily before settling down. If the voltage droop exceeds the noise margin, the system may enter an **undefined state**.

#### Effect of Voltage Droop

The voltage droop occurs because a single power supply is expected to meet the demands of all blocks at once. If the power supply is too far away or cannot provide enough current, the voltage on the signal line might drop below the required level. This can result in improper logic levels being received by the load, leading to potential errors or undefined behavior.

### Solution: Multiple Power Supplies

To address this problem, **multiple power supplies** are introduced across the chip. Instead of relying on a single power source, power is supplied to each block from its nearest power supply pin. This approach helps to minimize voltage drops by distributing the current demand across multiple power sources, ensuring that each block gets the power it needs without causing significant voltage droop.

#### How Multiple Power Supplies Solve the Problem

1. **Reduced Voltage Droop**: By using multiple power supply lines (VDD, VSS) throughout the chip, each logic block can tap into the nearest power supply, reducing the overall load on any single power supply line.
2. **Signal Integrity**: With power supplies located closer to the logic blocks, the signal lines retain their integrity as the distance between the power supply and the load is minimized.
3. **Decoupling Capacitors**: While decoupling capacitors are still used, they are more effectively placed when multiple power supplies are available, ensuring that the signal transitions remain stable and noise-free.

### Power Planning Strategy

In modern chip designs, the power supply layout involves carefully planning the **VDD** (power) and **VSS** (ground) lines. These lines are distributed across the chip in a grid-like pattern to ensure that power is available as close as possible to each logic block. 

#### Key Points in Power Planning:

- **Multiple Power Lines**: A combination of vertical and horizontal VDD/VSS lines are laid out to ensure uniform power distribution across the chip.
- **Decoupling Capacitors**: Capacitors are strategically placed near the critical logic blocks to provide additional current during switching activities.
- **Power Supply Proximity**: Each logic block should have access to the nearest power supply to minimize the impact of voltage drops and ensure reliable signal integrity.

</details>

---

<details>
  <summary>Library Binding and Placement</summary>

### Library Binding
- The process of linking RTL (Register Transfer Level) code to specific standard cells in the library.
- Ensures that logic gates used in the design match the technology specifications.

### Placement
- Arranging standard cells in the defined rows of the chip's floorplan.
- Two types:
  - **Global Placement**: Approximate locations of cells.
  - **Detailed Placement**: Final legal placement in rows with spacing rules.

### Tools Used
- **Yosys**: For synthesis.
- **OpenROAD**: For placement and routing.


</details>

---

<details>
  <summary>Cell Design and Characterization Flows</summary>

### Design Flow
1. **Design Entry**: Define the cell's functionality using Verilog or VHDL.
2. **Simulation**: Validate logical correctness.
3. **Synthesis**: Convert high-level description into gates.
4. **Layout Design**: Create a physical representation of the cell.

### Characterization Flow
1. **SPICE Simulation**: Measure the cell's electrical characteristics.
2. **Library Creation**:
   - Generate `.lib` files with timing, power, and area details.
3. **Integration**:
   - Add the characterized cell to the standard cell library.

</details>

---

<details>
  <summary>General Timing Characterization Parameters</summary>

### Key Parameters
- **Setup Time**:
  - Minimum time before the clock edge for the input to be stable.
- **Hold Time**:
  - Minimum time after the clock edge for the input to remain stable.
- **Propagation Delay**:
  - Time taken for a signal to travel from input to output.
- **Clock Skew**:
  - Difference in clock arrival times across the chip.

### Importance
- Helps in meeting timing constraints for synchronous designs.
- Ensures reliability and performance of the design under different conditions.

</details>
