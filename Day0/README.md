# Day 0: Tool Installation

## Overview
On Day 0, Setting up the necessary tools for the SFAL-VSD-SoC-Design. This document outlines the installation steps for each tool required.

## System Details
- **RAM**: 16GB
- **Storage**: 256GB SSD
- **OS**: macOS

## Tools Setup

<ul>
    <li>
        <details>
            <summary>Yosys</summary>
            <p>Instructions:</p>
            <pre>
```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
$ git clone https://github.com/YosysHQ/yosys.git
$ brew install cmake gcc gawk tcl-tk libtool bison flex make
$ brew install graphviz
$ cd yosys
$ git submodule update --init
$ make
$ yosys --version
        </pre>
        <img width="870" alt="Yosys Installation Screenshot" src="https://github.com/user-attachments/assets/1d38c5b6-e74d-4e15-9380-0fdf94153099">
    </details>
</li>
<li>
    <details>
        <summary>Iverilog</summary>
        <p>Instructions:</p>
        <pre>
$ brew install icarus-verilog
        </pre>
        <img width="1376" alt="Iverilog Installation Screenshot" src="https://github.com/user-attachments/assets/2c9e56af-bbc6-425c-b3db-317dc7d9b6a4">
    </details>
</li>
<li>
    <details>
        <summary>GTKWave</summary>
        <p>Instructions:</p>
        <pre>
$ brew install gtkwave
        </pre>
        <img width="1386" alt="GTKWave Installation Screenshot" src="https://github.com/user-attachments/assets/552f76c7-920f-4930-98e7-5d804b43d3ee">
    </details>
</li>
</ul>
