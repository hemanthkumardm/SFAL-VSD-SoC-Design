# Day 10: Introduction to BabySoC and SoC Fundamentals

### Problem Statement
This work discusses the different aspects of designing a small SoC based on **RVMYTH** (a RISCV-based processor). This SoC will leverage a **PLL** as its clock generator and controller and a **10-bit DAC** to interface with external devices. This small, fully open-source SoC, fabricated under Sky130 technology, can be used for educational purposes, allowing integration with devices like televisions and mobile phones for multimedia output.

## Learning Objectives

<details>
<summary>1. What is an SoC?</summary>
A System on Chip (SoC) is an integrated circuit (IC) that combines all components of a computer or other electronic systems onto a single chip. SoCs integrate various components such as a processor, memory, input/output ports, and secondary storage to operate within embedded systems, mobile devices, and various consumer electronics.
</details>

<details>
<summary>2. Types of SoCs</summary>

   - **SoC built around a Microcontroller**: Contains a microcontroller as its main processing unit, ideal for applications with low power and computational needs.
   - **SoC built around a Microprocessor**: Centers on a microprocessor, suitable for more complex processing tasks.
   - **Application-Specific SoC**: Designed for particular applications that don’t fit into general-purpose categories. These are tailored for specialized tasks with optimized performance.

</details>

<details>
<summary>3. BabySoC Components</summary>

   - **RVMYTH**: A RISC-V based CPU acting as the main processing unit of BabySoC.
   - **PLL (Phase-Locked Loop)**: A control system that generates an output signal whose phase is related to the phase of an input signal. PLLs are widely used in clock generation and distribution for synchronization purposes.
   - **DAC (Digital-to-Analog Converter)**: A system that converts digital signals into analog signals, enabling the generation of digitally defined transmission signals commonly used in modern communication systems.

</details>

## Introduction to BabySoC Operation

1. **PLL Activation**: The initial input signals activate BabySoC, triggering the PLL to generate a synchronized clock for the circuit.
2. **RVMYTH Processing**: The `r17` register in RVMYTH cycles through values, feeding data to the DAC.
3. **DAC Output**: Using the values from RVMYTH, the DAC generates an output file named `OUT`, representing the analog signal for external devices.

---

This structured layout provides clear, accessible documentation for BabySoC and SoC fundamentals, making it easy to follow your learning journey.
