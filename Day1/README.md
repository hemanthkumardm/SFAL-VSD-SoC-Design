# Day 1: Tool Installation

## Overview
On Day 1, we focused on setting up the necessary tools for the SFAL-VSD-SoC-Design. This document outlines the installation steps for each tool required.

## System Details.
16GB RAM
256GB SSD
MAC

## Tools Setup

<details>
<summary>Yosys</summary>
    Instructions 

```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
$ git clone https://github.com/YosysHQ/yosys.git
$ brew install cmake gcc gawk tcl-tk libtool bison flex make
$ brew install graphviz
$ cd yosys
$ git submodule update --init
$ make
$ yosys --version
```
<img width="870" alt="Screenshot 2024-10-20 at 4 13 56 PM" src="https://github.com/user-attachments/assets/1d38c5b6-e74d-4e15-9380-0fdf94153099">

<details>
<summary>Iverilog</summary>
    Instructions 

```bash
$ brew install icarus-verilog
```
<img width="1376" alt="Screenshot 2024-10-20 at 4 13 06 PM" src="https://github.com/user-attachments/assets/2c9e56af-bbc6-425c-b3db-317dc7d9b6a4">

<details>
<summary>GTKWave</summary>
    Instructions 

```bash
$ brew install gtkwave
```
<img width="1386" alt="Screenshot 2024-10-20 at 4 16 47 PM" src="https://github.com/user-attachments/assets/552f76c7-920f-4930-98e7-5d804b43d3ee">





