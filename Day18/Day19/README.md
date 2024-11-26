![Screenshot from 2024-11-26 13-43-51](https://github.com/user-attachments/assets/a1596dd9-d938-4746-a844-63bd8f8c9007)# Pre-layout Timing Analysis and Importance of Good Clock Tree

This section outlines the process of performing pre-layout timing analysis and emphasizing the importance of a good clock tree in VLSI design. It covers the necessary steps to ensure that the design is ready for further stages in the OpenLane flow, including the integration of custom-designed cells and timing optimization.


### Fix Small DRC Errors and Verify the Design

Before proceeding with the custom-designed cell layout, we verify that the design meets specific DRC (Design Rule Check) conditions:

1. The input and output ports of the standard cell should lie at the intersection of the vertical and horizontal tracks.
2. The width of the standard cell should be an odd multiple of the horizontal track pitch.
3. The height of the standard cell should be an even multiple of the vertical track pitch.

#### Commands to Open the Custom Inverter Layout

```bash
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

**Screenshot Verification:**

  - Condition 1: Verified with the ports on the intersection of the tracks.
    <img width="792" alt="Screenshot 2024-11-27 at 3 15 37 AM" src="https://github.com/user-attachments/assets/e1190ab0-0f30-4cb6-aeaa-fcac1d08e74c">

  - Condition 2: Verified with a cell width of 1.38µm (0.46 * 3).
    <img width="761" alt="Screenshot 2024-11-27 at 3 15 51 AM" src="https://github.com/user-attachments/assets/a93e9597-a9b8-4041-bd36-0e33e54e2c4d">

  - Condition 3: Verified with a cell height of 2.72µm (0.34 * 8).
    <img width="753" alt="Screenshot 2024-11-27 at 3 16 07 AM" src="https://github.com/user-attachments/assets/0258e8a5-f6ef-4bc2-9e52-f624793fb171">
    
#### Save Finalized Layout

After verifying the design, save the layout with a custom name.
```
# Command to save the layout with a custom name
save sky130_vsdinv.mag
# Command to open the newly saved layout
magic -T sky130A.tech sky130_vsdinv.mag &
```

Screenshot of Saved Layout:

  - The layout has been saved as sky130_vsdinv.mag for further steps.

#### Generate LEF from Layout

Generate a LEF (Library Exchange Format) file from the layout for integration into the OpenLane flow.

![Screenshot from 2024-11-25 18-51-06](https://github.com/user-attachments/assets/d55cf418-2c37-44af-9f69-aad09a89011d)
![Screenshot from 2024-11-25 18-49-03](https://github.com/user-attachments/assets/79c07942-5be7-4af1-9989-1c62a2e257ea)
![Screenshot from 2024-11-25 18-37-25](https://github.com/user-attachments/assets/04d2e011-c7d9-423e-90f6-2020d46eedad)
![Screenshot from 2024-11-25 18-37-00](https://github.com/user-attachments/assets/c98497b0-d68a-4bc8-9151-8acfc36db269)
![Screenshot from 2024-11-25 18-51-42](https://github.com/user-attachments/assets/bc5a5bf2-df63-4227-b931-fbb6e82c84b3)

---

#### Copy LEF and Library Files to the picorv32a Design

Copy the generated LEF and associated library files to the picorv32a design’s src directory.

```
# Copy LEF file to src directory
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Check if the files were copied successfully
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy library files to src directory
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Check if the library files were copied successfully
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

<img width="760" alt="Screenshot 2024-11-27 at 3 18 26 AM" src="https://github.com/user-attachments/assets/5b491344-62be-43ec-9aee-3107b8299dbc">

---

#### Edit config.tcl to Include Custom Cells

Modify the config.tcl file to include the custom LEF file and change the libraries to the ones we have added.

![Screenshot from 2024-11-25 20-04-13](https://github.com/user-attachments/assets/aed52c27-7629-4974-b87f-673d7ae7ad82)

---

#### Run OpenLane Flow Synthesis

Run the OpenLane flow to perform synthesis with the newly inserted custom inverter cell.

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```

<img width="765" alt="Screenshot 2024-11-27 at 3 25 52 AM" src="https://github.com/user-attachments/assets/64412f29-0df9-43b7-aa6e-2f44e56999b1">
<img width="585" alt="Screenshot 2024-11-27 at 3 26 11 AM" src="https://github.com/user-attachments/assets/9abb6c6c-5465-4f30-8815-51fcea072094">
<img width="517" alt="Screenshot 2024-11-27 at 3 26 34 AM" src="https://github.com/user-attachments/assets/ab1d9bfa-267f-48ba-a20d-1003d9236871">

---

#### Handle Violations Introduced by Custom Cell

After inserting the custom inverter, there may be violations introduced. Modify design parameters to fix these violations.

<img width="759" alt="Screenshot 2024-11-27 at 3 30 16 AM" src="https://github.com/user-attachments/assets/feb5deaa-32fe-459b-ac11-c9bda9c28e59">

---

# VLSI Design with OpenLane: Custom Inverter and Timing Analysis

This repository demonstrates the process of creating and integrating a custom inverter into a VLSI design using OpenLane. It covers the steps of design preparation, synthesis, floorplanning, placement, timing analysis, and fixing timing violations.


## Prerequisites

- **OpenLane** toolchain for physical design and synthesis.
- **Magic** tool for viewing placement and routing.
- **OpenSTA** for static timing analysis.
- **Docker** for running the OpenLane flow.
- **Custom LEF file** containing the custom inverter.

## Design Setup

1. **Prepare the design** by running the following command to set up the necessary files and directories:

    ```tcl
    prep -design picorv32a
    ```
<img width="650" alt="Screenshot 2024-11-27 at 3 34 16 AM" src="https://github.com/user-attachments/assets/287dc6f0-2ea2-41a4-a4a7-1c34eef74e00">

--

2. **Add the custom LEF** file to the design flow:
    ```tcl
    set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
    add_lefs -src $lefs
    ```

---

3. **Set synthesis parameters** to optimize the design:
    ```tcl
    set ::env(SYNTH_STRATEGY) "DELAY 3"
    set ::env(SYNTH_SIZING) 1
    ```


## Custom Inverter Integration

1. **Create a custom inverter** and merge it into the design by updating the LEF file:
    - Use the `merged.lef` file for the integration of the custom inverter.
    - Update the OpenLane flow to include the newly added LEF file.

2. **Run synthesis** to ensure that the custom inverter is accepted by the flow:
    ```tcl
    run_synthesis
    ```
---

<img width="318" alt="Screenshot 2024-11-27 at 3 35 15 AM" src="https://github.com/user-attachments/assets/b63054e5-006b-4d0e-a951-c31ec514298e">
![Screenshot from 2024-11-26 13-23-02](https://github.com/user-attachments/assets/f65ed3f8-14d9-4554-ad88-1b421edb78a5)


3. **Check the results** by observing the slack and area improvements. The slack should become 0, and area might increase due to the custom inverter.

## Synthesis and Timing Optimization

1. **Modify synthesis parameters** to optimize timing:
    ```tcl
    set ::env(SYNTH_MAX_FANOUT) 4
    ```

2. **Run synthesis again** to observe the improvements:
    ```tcl
    run_synthesis
    ```

3. **Perform timing analysis** with OpenSTA to verify improvements:
    ```bash
    sta pre_sta.conf
    ```


## Post-Synthesis Timing Analysis

1. **OpenSTA** is used to analyze the timing of the design post-synthesis. Ensure the design is prepped and run the synthesis before performing STA.

2. **Generate a timing report**:
    ```bash
    report_checks -fields {net cap slew input_pins} -digits 4
    ```

3. **Fix violations** by replacing cells (e.g., OR gates with higher drive strength):
    ```tcl
    replace_cell _14510_ sky130_fd_sc_hd__or3_4
    ```

## Floorplanning and Placement

1. **Run floorplan** and place IOs:
    ```tcl
    run_floorplan
    ```

2. **Use alternative commands** for floorplan if errors occur:
    ```tcl
    init_floorplan
    place_io
    tap_decap_or
    ```

3. **Run placement**:
    ```tcl
    run_placement
    ```

4. **View placement in Magic**:
    - Load the placement definition into Magic for visualization:
    ```bash
    magic -T $PDK_ROOT/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
    ```
---

# Tb be continued 

![Screenshot from 2024-11-26 13-43-26](https://github.com/user-attachments/assets/fe0f9a6f-4fed-48ec-8b0c-10cabd465d87)
![Screenshot from 2024-11-26 22-38-34](https://github.com/user-attachments/assets/8770a234-f302-4f74-ba0f-3100f63fa117)
![Screenshot from 2024-11-26 22-38-30](https://github.com/user-attachments/assets/93752807-d58c-499d-908c-1ab301db9bf5)
![Screenshot from 2024-11-26 22-37-10](https://github.com/user-attachments/assets/a6b27f16-d692-4ef5-8441-35364b213593)
![Screenshot from 2024-11-26 22-36-55](https://github.com/user-attachments/assets/5738fe3c-be9f-4849-90d7-cab47e1baca0)
![Screenshot from 2024-11-26 22-34-42](https://github.com/user-attachments/assets/27a1b7a6-ef78-4e66-afb6-1e00dcd176e8)
![Screenshot from 2024-11-26 22-28-03](https://github.com/user-attachments/assets/3ed7387f-62ac-4ca3-88e4-d92057c8289c)
![Screenshot from 2024-11-26 22-13-10](https://github.com/user-attachments/assets/05b9323b-3e46-4710-b291-e89d71c5be9d)
![Screenshot from 2024-11-26 22-12-44](https://github.com/user-attachments/assets/851fe7e1-a0db-4223-9da2-d224b50a369a)
![Screenshot from 2024-11-26 21-48-10](https://github.com/user-attachments/assets/9ae29208-2105-4f1c-a982-321967e649ef)
![Screenshot from 2024-11-26 21-48-00](https://github.com/user-attachments/assets/748e7ed4-b86e-4312-a884-d7030aac007c)
![Screenshot from 2024-11-26 21-45-31](https://github.com/user-attachments/assets/84881e0a-6a3f-49a0-a22c-6935a6e40fd0)
![Screenshot from 2024-11-26 21-40-34](https://github.com/user-attachments/assets/f0bd4b84-a1b0-4d2b-94b9-ccbbb6b38ea1)
![Screenshot from 2024-11-26 21-28-57](https://github.com/user-attachments/assets/197ee219-1d18-4e72-9459-be8d901df074)
![Screenshot from 2024-11-26 14-49-58](https://github.com/user-attachments/assets/d2214ee8-1235-4a2f-be25-274370da234f)
![Screenshot from 2024-11-26 14-35-53](https://github.com/user-attachments/assets/a3c2cddd-f955-4652-8074-f406b763273f)
![Screenshot from 2024-11-26 14-35-45](https://github.com/user-attachments/assets/a3c7d8e0-6af1-46da-bb2a-b38510f9a61d)
![Screenshot from 2024-11-26 14-07-18](https://github.com/user-attachments/assets/995ee156-d65c-4d25-8b8d-4cd8353df5a9)
![Screenshot from 2024-11-26 14-07-13](https://github.com/user-attachments/assets/50413000-2e5a-45d4-87f3-21ffd98c9337)
