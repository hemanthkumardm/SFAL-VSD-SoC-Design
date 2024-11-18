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

### Best Practices
- Use higher metal layers for power routing.
- Maintain buffer zones for heat dissipation.
- Align clock and power domains to reduce interference.

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
