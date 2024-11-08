# Day 5 - Introduction to Logic Synthesis

## PART 1
<details>
  <summary>SYNTHESIS</summary>
  
  **Illustration**
  <img width="931" alt="Screenshot 2024-10-25 at 8 59 57 PM" src="https://github.com/user-attachments/assets/a54f67eb-370c-4196-a4dd-57d8b23444f7">

   > **Note:** Use Non-blocking assignments while writing sequential circuits.
**Logic Synthesis Basics**
```verilog
module model_code (input a, input b, input c, output z);
assign y = (a&b) | (b&c)|(c&a);
endmodule
```
<img width="1365" alt="Screenshot 2024-10-25 at 9 06 22 PM" src="https://github.com/user-attachments/assets/2a42c4e0-9e5f-47fe-9a91-54d1066ca802">
which is the best Implementation?<br>
The below values are for illustration purpose
<img width="1042" alt="Screenshot 2024-10-25 at 9 07 16 PM" src="https://github.com/user-attachments/assets/835b9b40-78f3-44cd-b72a-d1fba677f9e6">

**Comparision**
<img width="1302" alt="Screenshot 2024-10-25 at 9 09 07 PM" src="https://github.com/user-attachments/assets/c2d01898-ae66-4f4b-9f8d-d38c2bfe70e5">

Is implementation 3 the best implementation always?

Implementation 3 meets all the criteria 

- Working Digital Logic Circuit
  - Logically Correct
  - Electrically Correct
  - Timing met
- Implementation 3 offers very less area and delay. Definitely a good choice
- Say this logic is present in hold sensitive path
  - Is implementation 3 the best ?
  - Additional delay buffers to meet hold, will add additional area !!
 
So what is the correct recipie?

Constraints:
  - Constraints are the guide to the synthesizer to pick the correct library cells which is most appropriate for the design
  - As illustrated implementation 1, 2, 3 all are correct and will be picked based on need.

</details>

--------------------------------------------------------------------------------------------------------------------------

<details>
  <summary>DC (Design Compiler)</summary>

**What is DC?**
Design Compiler (DC) : Synthesis tool targeted for ASIC design flow from Synopsys.

**Features of DC?**
-  Established as a premium synthesis tool across semiconductor industry
- Interoperability with various backend tools from Synopsys
- Has the ability to perform DFT Scan stitch.
- Can handle huge designs with extreme complexity and provide very good QoR

**Common Technologies associated with DC?**
 - SDC : (Synopsys Design Constraints) These are the design constraints which are supplied to DC to enable appropriate optimization suitable for achieving the best implementation.
 - .LIB : Design Library which contains the standard cells.
 - DB : Same as lib but in a different format. DC understand libraries in .db format.
 - DDC: Synopsys proprietary format for storing the design information . DC can write out and read in DDC.

**SDC (Synopsys Design Constraints):** 
  -  Synopsys Design Constraints (SDC) format
  -  Design intent in terms of timing, power and area constraints .
  -  Supported by different EDA tools across semiconductor industry.
  -  SDC is based on Tool Command Language (Tcl).

**DC setup**
<img width="1367" alt="Screenshot 2024-10-25 at 9 21 07 PM" src="https://github.com/user-attachments/assets/d1f5ac6a-d871-40ad-bac3-96ee12084349">

</details>

---------------------------------------------------------------------------------------------------------------------------------

## PART 2
<details>
  <summary>Invoking DC basic setup</summary>

Invocking DC shell
```bash
csh
dc_shell
```
<img width="1440" alt="Screenshot 2024-10-25 at 9 35 00 PM" src="https://github.com/user-attachments/assets/fb226667-ddec-4a0a-9aa5-d821c5b7aae3">

Technology libraries are linked in target libraries and link libraries
<img width="420" alt="Screenshot 2024-10-25 at 9 37 47 PM" src="https://github.com/user-attachments/assets/63741a98-895c-4ee9-99f0-4101ed2475d5">

These your_library.db is imaginary non-existance library

To read design
`read_verilog DC_WORKSHOP/lib/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab1_flop_with_en.v `
<img width="1406" alt="Screenshot 2024-10-25 at 9 49 51 PM" src="https://github.com/user-attachments/assets/51645005-d68b-4dae-b511-ae41c0aff3f7">

```verilog
module lab1_flop_with_en ( input res , input clk , input d , input en , output reg q);
always @ (posedge clk , posedge res)
begin
	if(res)
		q <= 1'b0;
	else if(en)
		q <= d;	
end
endmodule
```


**Expecting Output**
<img width="583" alt="Screenshot 2024-10-25 at 9 48 58 PM" src="https://github.com/user-attachments/assets/98405b7d-1a29-446b-8f4e-77ecaae3dbdc">

**Writing Verilog**
`write -f verilog -out lab1_net.v`
<img width="1287" alt="Screenshot 2024-10-25 at 9 53 16 PM" src="https://github.com/user-attachments/assets/9b5c40cc-2c96-4a2e-bdb1-3dd85467298c">

**Linking sky130 library**
<img width="1366" alt="Screenshot 2024-10-25 at 10 01 26 PM" src="https://github.com/user-attachments/assets/d1c99c5d-1b50-4e90-8d58-3c5b24784b74">

**After linking and compiling to sky130 library**
<img width="1285" alt="Screenshot 2024-10-25 at 10 05 17 PM" src="https://github.com/user-attachments/assets/ef777096-6ed8-4f5f-8bda-a38c5733e4f5">

</details>

-----------------------------------------------------------------------------------------------------------------------------

<details>
  <summary>Introduction to DDC GUI with Design Vision</summary>
  
  **Invocking Design Vision**
  ```bash
  csh
  design_vision
  ```
  <img width="802" alt="Screenshot 2024-10-25 at 10 09 10 PM" src="https://github.com/user-attachments/assets/bd9d5535-26b8-41b2-bb43-5d68d7e5dd49">

  Design requires the .ddc file
  **Creating .ddc file**
  `write -f ddc -out lab1_net.ddc`
  <img width="496" alt="Screenshot 2024-10-25 at 10 12 34 PM" src="https://github.com/user-attachments/assets/6602a081-1efb-4104-9344-c40232917509">

  **Read ddc**
  `read_ddc lab1_net.ddc`
  <img width="806" alt="Screenshot 2024-10-25 at 10 14 52 PM" src="https://github.com/user-attachments/assets/db49c942-b4bb-4122-905e-4226a592f33e">

  **Schematic View**
  <img width="805" alt="Screenshot 2024-10-25 at 10 15 49 PM" src="https://github.com/user-attachments/assets/72b2fc79-3d00-47a1-b71f-0ac8f402c725">

</details>

---------------------------------------------------------------------------------------------------------------------------------

<details>
  <summary>DC Synopsys DC setup</summary>
  <br>
  Everytime we invoke dc_shell we need to set target_library and linking_library, When we have multiple .db files its very hard to target each time. So to avoid that problem we should create `.synopsys_dc.setup` file in user home directory.
  
  > **note:** All repeatative tasks which is needed for tool setup can be printed in this file.

  **Steps:**
  
  `gvim .synopsys_dc.setup`
  ```bash
  set target_library ~/DC_WORKSHOP/lib/sky130_fd_sc_hd_tt_025C_1v80.db
  set link_library {* $target_library }
  ```

</details>

## PART 3
<details>
  <summary>TCL quick refresher</summary>
  
**TCL : Tool Command Language**
  - Used to write SDC and all the internal command are based on TCL.

**set**
  -  For creating and storing information in variables
  -  Eg. `set a 5` → a = 5
  -  `set a [expr $a + $b]` → a = a + b.
  - Note square brackets are used for nesting the commands in TCL

**Conditional Statements**
```tcl
if {condition} {
  statements if true
} else {
  statements if false
}
```
**Example**
```tcl
if {Sa < 10} {
  echo "$a is less than 10";
} else {
  echo "$a is greater than 10";
}
```

**Looping Statements**
```tcl
while {condition} {
  statements
}
```
**Example**
```tcl
set i0
while {$i < 10}{
  echo $i; 
  incr i;
}
```

**Example 2**
```tc;
set i0
while {$i < 10}{
  echo $i; 
  incr j; // wrong manipulation of variables could lead to infinite loops
}
```

**for loop**
```tcl
for {looping var} {condition} (looping var modification} {
  statements
}
```

**Example**
for {set i O} {$i < 10} {iner i} {
  echo $i;
}

**foreach loop**
```tcl
foreach var list {
  statements
}
```
> **Note:** very useful in Design Compiler

**Example**
```tcl
set my_design _list [list u_top/u_mod1\ u_top/u_mod3]
foreach my_module $my_design_list {
set_size_only $my_module;
}
```

**DC specific TCL Commands**
```tcl
foreach_in_collection var collection {
  statements
}
```
**Example**
```tcl
foreach_in_collection cell_name [get_cells* -hier] {
  set cell_name [get_object_name $cell_name];
  set ref_name [get_attribute [get_cells $cell_name] ref_name];
  echo Scell_name, Sref_name;
}
```
>**Note:** Nesting of TCL Commands (Very much used in DC)

</details>

--------------------------------------------------------------------------------------------------------------------------------

<details>
  <summary>TCL scripting</summary>
  <img width="171" alt="Screenshot 2024-10-25 at 10 54 46 PM" src="https://github.com/user-attachments/assets/73568e5f-a4b3-4a6c-958c-aa2cde1d53f8">
  <br>
  ------------------------------------------------------------------------------------------------------------------------------
  <img width="355" alt="Screenshot 2024-10-25 at 10 55 18 PM" src="https://github.com/user-attachments/assets/81b918fd-52be-45e5-a53a-d86fe82b3b66">
  <br>
  ------------------------------------------------------------------------------------------------------------------------------
  <img width="324" alt="Screenshot 2024-10-25 at 10 55 45 PM" src="https://github.com/user-attachments/assets/7c546f99-41a5-4f64-8180-4ed81a8f356b">
  <br>
  ------------------------------------------------------------------------------------------------------------------------------
  <img width="242" alt="Screenshot 2024-10-25 at 10 56 47 PM" src="https://github.com/user-attachments/assets/14b9d100-95ea-4bb2-9f22-4575f46030d6">
  <br>
  ------------------------------------------------------------------------------------------------------------------------------
  <img width="334" alt="Screenshot 2024-10-25 at 10 57 43 PM" src="https://github.com/user-attachments/assets/3fa5210e-946c-4657-9875-14376da43531">
  <br>
  ------------------------------------------------------------------------------------------------------------------------------
  
  **Collection**
  <img width="1127" alt="Screenshot 2024-10-25 at 10 58 20 PM" src="https://github.com/user-attachments/assets/a226fb1d-be74-45f0-ae3e-7f28d1becbab">
  <br>
  
------------------------------------------------------------------------------------------------------------------------------
  <img width="1127" alt="Screenshot 2024-10-25 at 10 58 57 PM" src="https://github.com/user-attachments/assets/7a3afce3-b5e3-470e-9dda-780ea7d0be79">
  <br>
  Because it works as a pointer and refering address.<br>
------------------------------------------------------------------------------------------------------------------------------

  **Correct format**
  <img width="1128" alt="Screenshot 2024-10-25 at 11 01 36 PM" src="https://github.com/user-attachments/assets/b144afe7-496b-49cc-b4b9-04461c9ef784">
  
</details>
