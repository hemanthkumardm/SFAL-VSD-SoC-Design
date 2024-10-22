# Day 3: Combinational and Sequential Combinations

<details>
  <summary>Part 1: Introduction to Optimization</summary>

   - Sequencing the logic to achieve the most optimized design.
   - Techniques used in optimization:
     - **Constant Propagation**: Direct optimization method where constant values are substituted in expressions.
     - **Boolean Logic Optimization**: Techniques such as K-map and Quine McKluskey for simplifying Boolean expressions.

  <details>
    <summary>Combinational Logic Optimization</summary>
    
    1. **Constant Propagation**: 
    <img width="972" alt="Constant Propagation" src="https://github.com/user-attachments/assets/663928e8-f40a-4ce4-8bf9-354a4448f1bd">
    
    2. **Boolean Logic Optimization**:
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
    <img width="982" alt="Sequential Constant Propagation" src="https://github.com/user-attachments/assets/6f0949cc-22ae-4043-b4cd-465033abb36a">
    
    ### Advanced Optimization Techniques
    <img width="1440" alt="Advanced Optimization" src="https://github.com/user-attachments/assets/ee9774bb-423b-4e28-b078-030f0c95b1d3">
  
  </details>
</details>

<details>
  <summary>Part 2: Combinational Logic Optimization</summary>
  
  <details>
    <summary>opt_check</summary>
    
    ```bash
    module opt_check (input a , input b , output y);
      assign y = a ? b : 0;
    endmodule
    ```
    **Explanation**: This module outputs \(b\) if \(a\) is true; otherwise, it outputs 0.
    
    ![opt_check Synthesized Output](https://github.com/user-attachments/assets/4d648d23-6ed2-4463-b0fd-4756b0122880)

    **After Synthesizing**:
    <img width="308" alt="opt_check Synthesized Logic" src="https://github.com/user-attachments/assets/ca5dbd42-287f-41cf-a12b-b328d697c975">

    **Optimization Command**: 
    ```bash
    opt_clean -purge
    ```

    <img width="450" alt="opt_clean Command Output" src="https://github.com/user-attachments/assets/17fb5e3d-ba0d-4963-8b39-13b0fd62d64f">

    **Link to Liberty File**:
    <img width="424" alt="Liberty File Link" src="https://github.com/user-attachments/assets/5abbf967-f295-41d2-a67d-23e208ff9da8">

    **Final Output**:
    <img width="890" alt="Final Output for opt_check" src="https://github.com/user-attachments/assets/e47ba631-63f0-492d-bc56-4ee15c150f20">

  </details>

  <details>
    <summary>opt_check2</summary>
    
    ```bash
    module opt_check2 (input a , input b , output y);
      assign y = a ? 1 : b;
    endmodule
    ```
    **Explanation**: This module outputs 1 if \(a\) is true; otherwise, it outputs \(b\).
    
    ![opt_check2 Explanation](https://github.com/user-attachments/assets/2489d15e-de50-422b-88e4-1b4855c6eae1)

    **After Synthesizing**:
    <img width="308" alt="opt_check2 Synthesized Logic" src="https://github.com/user-attachments/assets/b60b8139-0764-4d91-a285-1b54d95ba965">

    **Optimization Command**: 
    ```bash
    opt_clean -purge
    ```

    <img width="446" alt="opt_clean Command Output for opt_check2" src="https://github.com/user-attachments/assets/fdf8f8fd-16a3-4e81-b897-fd65e6c5f058">

    **Link to Liberty File**:
    <img width="399" alt="Liberty File Link for opt_check2" src="https://github.com/user-attachments/assets/6acc8ecf-23f9-48ce-87ba-70e6b898115b">

    **Final Output**:
    <img width="858" alt="Final Output for opt_check2" src="https://github.com/user-attachments/assets/06c46dfd-cabd-4e53-8b0d-6a34c11e763d">

  </details>

  <details>
    <summary>opt_check3</summary>
    
    ```bash
    module opt_check3 (input a , input b, input c , output y);
      assign y = a ? (c ? b : 0) : 0;
    endmodule
    ```
    **Explanation**: This module outputs \(b\) if both \(a\) and \(c\) are true; otherwise, it outputs 0.
    
    ![opt_check3 Explanation](https://github.com/user-attachments/assets/9e123187-9495-4ef1-a82f-31f3ee78dd48)

    **After Synthesizing**:
    <img width="422" alt="opt_check3 Synthesized Logic" src="https://github.com/user-attachments/assets/82785d0f-6540-40dd-a5a7-1cae34869bac">

    **Optimization Command**: 
    ```bash
    opt_clean -purge
    ```

    <img width="448" alt="opt_clean Command Output for opt_check3" src="https://github.com/user-attachments/assets/0ea8b987-bcbc-4f48-9c17-66ab06e85f72">

    **Link to Liberty File**:
    <img width="431" alt="Liberty File Link for opt_check3" src="https://github.com/user-attachments/assets/87340cae-8950-4b05-96be-131f6a6b2d92">

    **Final Output**:
    <img width="904" alt="Final Output for opt_check3" src="https://github.com/user-attachments/assets/0b13c93b-09f6-427f-af3c-17a1133a231a">

  </details>

  <details>
    <summary>opt_check4</summary>
    
    ```bash
    module opt_check4 (input a , input b , input c , output y);
      assign y = a ? (b ? (a & c) : c) : (!c);
    endmodule
    ```
    **Explanation**: This module implements a more complex logic based on the values of \(a\), \(b\), and \(c\).
    
    ![opt_check4 Explanation](https://github.com/user-attachments/assets/911fa2f2-7bdc-40ce-8c7f-dbb13fc6b2c4)

    **After Synthesizing**:
    <img width="358" alt="opt_check4 Synthesized Logic" src="https://github.com/user-attachments/assets/2530afaa-c817-4983-9cc5-d46db42c8a09">

    **Optimization Command**: 
    ```bash
    opt_clean -purge
    ```

    <img width="453" alt="opt_clean Command Output for opt_check4" src="https://github.com/user-attachments/assets/8eb2ae94-f398-4572-86e5-6e0035cba033">

    **Link to Liberty File**:
    <img width="416" alt="Liberty File Link for opt_check4" src="https://github.com/user-attachments/assets/824a20b4-00b3-4854-9ddc-ed9de77a1c47">

    **Final Output**:
    <img width="1022" alt="Final Output for opt_check4" src="https://github.com/user-attachments/assets/d41c1e0d-b0cb-4eba-be32-eb8908423dfa">

  </details>
  
</details>
