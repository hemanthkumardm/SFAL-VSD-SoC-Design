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

$ cd yosys
$ sudo apt install make # If make is not installed
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make config-gcc
$ make
$ sudo make install
```
<img width="885" alt="Screenshot 2024-10-20 at 2 28 47 PM" src="https://github.com/user-attachments/assets/4d156b86-d67e-4521-a554-2058dde5387c">



