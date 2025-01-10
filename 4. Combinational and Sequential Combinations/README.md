<details>
<summary>Part 1: Introduction to Optimization</summary>

- Sequencing the logic to achieve the most optimized design.
- Techniques used in optimization:
  - **Constant Propagation**: Direct optimization method where constant values are substituted in expressions.
  - **Boolean Logic Optimization**: Techniques such as K-map and Quine McKluskey for simplifying Boolean expressions.

<details>
<summary>Combinational Logic Optimization</summary>

1. **Constant Propagation**: is an optimization technique that replaces variables that are known to be constant with their values. This can reduce the complexity of expressions and eliminate unnecessary calculations. For example, if a signal is always `1` in a certain context, any expression dependent on that signal can be simplified accordingly.

<img width="972" alt="Constant Propagation" src="https://github.com/user-attachments/assets/663928e8-f40a-4ce4-8bf9-354a4448f1bd">   

2. **Boolean Logic Optimization**: refers to techniques used to simplify Boolean expressions using methods such as Karnaugh maps (K-maps) or the Quine-McCluskey algorithm. This helps reduce the number of logic gates required in a circuit, leading to lower area and power consumption. 

<img width="980" alt="Boolean Logic Optimization" src="https://github.com/user-attachments/assets/b543e047-afa3-4f7a-b38d-83b46b1e7f79">
</details>

<details>
<summary>Sequential Logic Propagation</summary>

1. **Basic**: Sequential constant propagation.
2. **Advanced Techniques**:
   - State Optimization: Optimization of unused states.
   - Retiming: Adjusting the timing of sequential elements.
   - Sequential Logic Cloning: Floor plan-aware synthesis.

### Sequential Constant Propagation
![Sequential Constant Propagation](https://github.com/user-attachments/assets/6f0949cc-22ae-4043-b4cd-465033abb36a)    

### Advanced Optimization Techniques
![Advanced Optimization](https://github.com/user-attachments/assets/ee9774bb-423b-4e28-b078-030f0c95b1d3)
</details>
</details>

<details>
<summary>Part 2: Combinational Logic Optimization</summary>

<details>
<summary>opt_check</summary>

```verilog
module opt_check (input a , input b , output y);
    assign y = a ? b : 0;
endmodule
```

**Explanation**: This module outputs b if a is true; otherwise, it outputs 0.

![opt_check Synthesized Output](https://github.com/user-attachments/assets/4d648d23-6ed2-4463-b0fd-4756b0122880)

**After Synthesizing**:<br>
<img width="308" alt="opt_check Synthesized Logic" src="https://github.com/user-attachments/assets/ca5dbd42-287f-41cf-a12b-b328d697c975">

**Optimization Command**: <br>
```bash
opt_clean -purge
```
<br>
<img width="450" alt="opt_clean Command Output" src="https://github.com/user-attachments/assets/17fb5e3d-ba0d-4963-8b39-13b0fd62d64f">

**Link to Liberty File**:<br>
<img width="424" alt="Liberty File Link" src="https://github.com/user-attachments/assets/5abbf967-f295-41d2-a67d-23e208ff9da8">

**Final Output**:<br>
<img width="890" alt="Final Output for opt_check" src="https://github.com/user-attachments/assets/e47ba631-63f0-492d-bc56-4ee15c150f20">
</details>

<details>
<summary>opt_check2</summary>

```verilog
module opt_check2 (input a , input b , output y);
    assign y = a ? 1 : b;
endmodule
```

**Explanation**: This module outputs 1 if a is true; otherwise, it outputs b.

![opt_check2 Explanation](https://github.com/user-attachments/assets/2489d15e-de50-422b-88e4-1b4855c6eae1)

**After Synthesizing**:<br>
<img width="308" alt="opt_check2 Synthesized Logic" src="https://github.com/user-attachments/assets/b60b8139-0764-4d91-a285-1b54d95ba965">

**Optimization Command**: <br>
```bash
opt_clean -purge
```
<br>
<img width="446" alt="opt_clean Command Output for opt_check2" src="https://github.com/user-attachments/assets/fdf8f8fd-16a3-4e81-b897-fd65e6c5f058">

**Link to Liberty File**:<br>
<img width="399" alt="Liberty File Link for opt_check2" src="https://github.com/user-attachments/assets/6acc8ecf-23f9-48ce-87ba-70e6b898115b">

**Final Output**:<br>
<img width="858" alt="Final Output for opt_check2" src="https://github.com/user-attachments/assets/06c46dfd-cabd-4e53-8b0d-6a34c11e763d">
</details>

<details>
<summary>opt_check3</summary>

```verilog
module opt_check3 (input a , input b, input c , output y);
    assign y = a ? (c ? b : 0) : 0;
endmodule
```

**Explanation**: This module outputs b if both a and c are true; otherwise, it outputs 0.

![opt_check3 Explanation](https://github.com/user-attachments/assets/9e123187-9495-4ef1-a82f-31f3ee78dd48)

**After Synthesizing**:<br>
<img width="422" alt="opt_check3 Synthesized Logic" src="https://github.com/user-attachments/assets/82785d0f-6540-40dd-a5a7-1cae34869bac">

**Optimization Command**: <br>
```bash
opt_clean -purge
```
<br>
<img width="448" alt="opt_clean Command Output for opt_check3" src="https://github.com/user-attachments/assets/0ea8b987-bcbc-4f48-9c17-66ab06e85f72">

**Link to Liberty File**:<br>
<img width="431" alt="Liberty File Link for opt_check3" src="https://github.com/user-attachments/assets/87340cae-8950-4b05-96be-131f6a6b2d92">

**Final Output**:<br>
<img width="904" alt="Final Output for opt_check3" src="https://github.com/user-attachments/assets/0b13c93b-09f6-427f-af3c-17a1133a231a">
</details>

<details>
<summary>opt_check4</summary>

```verilog
module opt_check4 (input a , input b , input c , output y);
    assign y = a ? (b ? (a & c) : c) : (!c);
endmodule
```

**Explanation**: This module implements a more complex logic based on the values of a, b, and c.

![opt_check4 Explanation](https://github.com/user-attachments/assets/911fa2f2-7bdc-40ce-8c7f-dbb13fc6b2c4)

**After Synthesizing**:<br>
<img width="358" alt="opt_check4 Synthesized Logic" src="https://github.com/user-attachments/assets/2530afaa-c817-4983-9cc5-d46db42c8a09">

**Optimization Command**: <br>
```bash
opt_clean -purge
```
<br>
<img width="453" alt="opt_clean Command Output for opt_check4" src="https://github.com/user-attachments/assets/8eb2ae94-f398-4572-86e5-6e0035cba033">

**Link to Liberty File**:<br>
<img width="416" alt="Liberty File Link for opt_check4" src="https://github.com/user-attachments/assets/824a20b4-00b3-4854-9ddc-ed9de77a1c47">

**Final Output**:<br>
<img width="1022" alt="Final Output for opt_check4" src="https://github.com/user-attachments/assets/d41c1e0d-b0cb-4eba-be32-eb8908423dfa">
</details>
</details>


<details>
<summary>Part 3: Sequential Logic Optimizations</summary>
<details>
<summary>dff_const1</summary>

```verilog
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end

endmodule
```
**Expected Waveform**
![WhatsApp Image 2024-10-22 at 22 40 43](https://github.com/user-attachments/assets/9cdb1c3a-f0cb-4f82-a257-77252c629916)
<br>
**Output Waveform**
<img width="1287" alt="Screenshot 2024-10-22 at 10 43 08 PM" src="https://github.com/user-attachments/assets/143a27d7-c1f9-49d6-bbf1-ffa6385f8785">
<br>

**After Synthesizing**:<br>
<img width="320" alt="Screenshot 2024-10-22 at 10 47 05 PM" src="https://github.com/user-attachments/assets/823608a2-378b-407a-a844-cf1451848bdf">

**Optimization Command**: <br>
```bash
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
<br>
<img width="597" alt="Screenshot 2024-10-22 at 10 49 03 PM" src="https://github.com/user-attachments/assets/2d0995ba-5b42-422a-8ef7-d1e331baf301">

**Link to Liberty File**:<br>
<img width="427" alt="Screenshot 2024-10-22 at 10 51 05 PM" src="https://github.com/user-attachments/assets/753cfb99-af11-421e-804d-cff9d5da955c"><br>

**Final Output**:<br>
<img width="1150" alt="Screenshot 2024-10-22 at 10 52 26 PM" src="https://github.com/user-attachments/assets/b039c39e-0de1-4b9c-85c8-ba461781a90a"><br>
</details>

<details>
<summary>dff_const2</summary>

```verilog
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end

endmodule
```
**Expected Waveform**
![WhatsApp Image 2024-10-22 at 22 40 44](https://github.com/user-attachments/assets/fee60c75-1788-44fa-a15e-ac344f9a507a)
<br>

**Output Waveform**
<br>
<img width="1287" alt="Screenshot 2024-10-22 at 11 04 08 PM" src="https://github.com/user-attachments/assets/1fdc4a43-6f55-4549-a77d-870522cb7601">

**After Synthesizing**:<br>
<img width="313" alt="Screenshot 2024-10-22 at 11 09 01 PM" src="https://github.com/user-attachments/assets/03fd4ec1-6519-4e9b-a47b-1740142f2330">

**Optimization Command**: <br>
```bash
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
<br>
<img width="588" alt="Screenshot 2024-10-22 at 11 09 26 PM" src="https://github.com/user-attachments/assets/ab80df34-1495-4347-9915-35ae8f2ac5b4">

**Link to Liberty File**:<br>
<img width="637" alt="Screenshot 2024-10-22 at 11 11 45 PM" src="https://github.com/user-attachments/assets/9398f8f9-fcec-4377-93c1-2189ed6f8f78"><br>

**Final Output**:<br>
<img width="611" alt="Screenshot 2024-10-22 at 11 12 30 PM" src="https://github.com/user-attachments/assets/a4ac80a7-30a6-4c98-b0b0-52690c4f1b91"><br>

</details>

<details>
<summary>dff_const3</summary>

```verilog
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```
**Expected Waveform**
<img width="376" alt="Screenshot 2024-10-22 at 11 54 53 PM" src="https://github.com/user-attachments/assets/c974fc7e-52e3-44f3-a82d-a240fe6e934d">

<br>

**Output Waveform**
<br>
<img width="1286" alt="Screenshot 2024-10-22 at 11 59 12 PM" src="https://github.com/user-attachments/assets/9cd238cf-4acc-4ed4-b135-5de4235cf8f7">


**After Synthesizing**:<br>
<img width="305" alt="Screenshot 2024-10-23 at 12 00 36 AM" src="https://github.com/user-attachments/assets/e2f2a01b-3a54-4382-95df-3580243fc8ce">


**Optimization Command**: <br>
```bash
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
<br>
<img width="582" alt="Screenshot 2024-10-23 at 12 01 07 AM" src="https://github.com/user-attachments/assets/f8022384-3eb3-427b-a8c9-f8ef69eee002">


**Link to Liberty File**:<br>
<img width="432" alt="Screenshot 2024-10-23 at 12 01 44 AM" src="https://github.com/user-attachments/assets/9ce42105-b793-4271-ad0a-eea8133dca36">


**Final Output**:<br>
<img width="1325" alt="Screenshot 2024-10-23 at 12 02 20 AM" src="https://github.com/user-attachments/assets/d2de502f-c9b1-46cd-821c-8e14990e83a0">


</details>

<details>
<summary>dff_const4</summary>

```verilog
module dff_const4(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b1;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```
**Expected Waveform**
![WhatsApp Image 2024-10-23 at 00 10 23](https://github.com/user-attachments/assets/a7714426-eb75-49d2-bfd9-3dd61362d8d7)


<br>

**Output Waveform**
<br>
<img width="1286" alt="Screenshot 2024-10-23 at 12 13 57 AM" src="https://github.com/user-attachments/assets/447d7895-c7a0-4a49-bd9d-085694639c41">



**After Synthesizing**:<br>
<img width="325" alt="Screenshot 2024-10-23 at 12 11 46 AM" src="https://github.com/user-attachments/assets/773084eb-9ed5-45c2-878b-a6bb3e55e063">


**Optimization Command**: <br>
```bash
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
<br>
<img width="576" alt="Screenshot 2024-10-23 at 12 12 24 AM" src="https://github.com/user-attachments/assets/31633906-13ab-45bc-b08e-d665f5f3fd0a">


**Link to Liberty File**:<br>
<img width="662" alt="Screenshot 2024-10-23 at 12 12 50 AM" src="https://github.com/user-attachments/assets/92ebaa3e-b8e8-4cb5-995a-2c0bd6f9bf3c">



**Final Output**:<br>
<img width="612" alt="Screenshot 2024-10-23 at 12 13 14 AM" src="https://github.com/user-attachments/assets/1a8f460a-13fa-43ed-87e4-f6ed1817cb0c">



</details>

<details>
<summary>dff_const5</summary>

```verilog
module dff_const5(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b0;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```
**Expected Waveform**
![WhatsApp Image 2024-10-23 at 00 24 55](https://github.com/user-attachments/assets/3efde1f6-4a20-43c0-b8f9-14b06ba2e3a5)



<br>

**Output Waveform**
<br>
<img width="1286" alt="Screenshot 2024-10-23 at 12 25 12 AM" src="https://github.com/user-attachments/assets/0f76055b-6abd-4d3d-8ebc-a199e3cbb2e6">

**After Synthesizing**:<br>
<img width="337" alt="Screenshot 2024-10-23 at 12 26 15 AM" src="https://github.com/user-attachments/assets/9af99fb3-1fa9-4a58-bfd1-307f8e521c9e">

**Optimization Command**: <br>
```bash
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
<br>
<img width="621" alt="Screenshot 2024-10-23 at 12 26 43 AM" src="https://github.com/user-attachments/assets/82385fa2-a1ed-48bf-8a44-ad943f1cb63c">

**Link to Liberty File**:<br>
<img width="440" alt="Screenshot 2024-10-23 at 12 27 22 AM" src="https://github.com/user-attachments/assets/c58258ba-6f90-4ebb-9f9e-e699d2530f68">

**Final Output**:<br>
<img width="867" alt="Screenshot 2024-10-23 at 12 28 29 AM" src="https://github.com/user-attachments/assets/ab4841de-c155-4ff5-b648-3e445c78eb95">

</details>
</details>
<details>
<summary>Part 4: Sequential Optimizations for Unused Outputs</summary>
<details>
<summary>counter_opt</summary>

```verilog
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end

endmodule
```
**Expected Waveform**
<img width="984" alt="Screenshot 2024-10-23 at 1 03 08 AM" src="https://github.com/user-attachments/assets/5cf45a39-6350-47c8-b804-c89bd8846823">
<br>

**Output Waveform**
<img width="1284" alt="Screenshot 2024-10-23 at 1 05 40 AM" src="https://github.com/user-attachments/assets/24a9d1e2-b5af-4194-9cca-c9167adc448e">

<br>

**After Synthesizing**:<br>
<img width="370" alt="Screenshot 2024-10-23 at 1 06 45 AM" src="https://github.com/user-attachments/assets/98cbf3aa-1595-4cac-bfb1-efcc0a943115">


**Optimization Command**: <br>
```bash
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
<br>
<img width="637" alt="Screenshot 2024-10-23 at 1 07 34 AM" src="https://github.com/user-attachments/assets/0e612b4b-33b8-4926-90fa-f6e0009f9caa">


**Link to Liberty File**:<br>
<img width="464" alt="Screenshot 2024-10-23 at 1 07 57 AM" src="https://github.com/user-attachments/assets/75551731-3713-414c-885f-ad315f2eedd9">
<br>


**Final Output**:<br>
<img width="1229" alt="Screenshot 2024-10-23 at 1 08 45 AM" src="https://github.com/user-attachments/assets/febebd0f-db4b-4961-a968-3e76f4d98ecd">
<br>
</details>


</details>
