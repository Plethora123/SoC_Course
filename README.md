# SoC_Course

Day 1

Basics of chip:

# System-on-Chip Design and Planning

This repository provides an in-depth exploration of SoC design processes, from the fundamental concepts of chip packaging and internal architecture to implementing RISC-V ISA, RTL synthesis, and physical design flow using open-source tools. 

## Contents
- [Introduction](#introduction)
- [Concept Overview](#concept-overview)
- [Implementation Steps](#implementation-steps)

## Introduction
This project explores key concepts in SoC design, leveraging open-source tools for building a RISC-V based CPU core, synthesizing RTL code, and carrying out physical design with OpenLANE.

## Concept Overview

### Package
In embedded systems, the **Package** is the protective layer that houses the actual chip. Connections from the package to the chip are established via **Wire Bonding**.

### Chip Architecture
A chip contains **PADS** for external connections and a **CORE** where digital logic resides. Both components form the **DIE**. Semiconductor chips are manufactured in **Foundries**, which develop specialized **Intellectual Properties (IPs)**.

### ISA (Instruction Set Architecture)
For executing software on hardware, a flow is followed: converting high-level code to assembly using **RISC-V ISA**, then translating it to binary for hardware interpretation, ultimately synthesized into RTL and implemented in silicon.

### Open-Source Implementation
Open-source SoC design involves RTL designs, EDA tools, and PDK data. With initiatives like Google-SkyWater’s open-source PDK, accessible 130nm fabrication is possible.

### ASIC Design Flow
ASIC design transitions from RTL to GDSII, the format for the final layout. Essential tasks include **Synthesis**, **Floor Planning**, **Placement**, **Clock Tree Synthesis**, **Routing**, and various Sign-off checks like **DRC**, **LVS**, and **STA**.

![image]()
### OpenLANE Flow
OpenLANE aids ASIC design, enabling RTL-to-GDSII implementation using synthesis and layout tools, culminating in a manufacturable layout.

## Implementation Steps

### Section 1: Synthesis with OpenLANE
Steps to run 'picorv32a' design synthesis:
```bash
# Enter OpenLANE directory
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
exit

```

![stats_of_final_synthesis_of_picorv32A](https://github.com/user-attachments/assets/3be7140b-e30a-4ff3-8776-e01dc517cead)

Calculation of Flop Ratio and DFF % from synthesis statistics report file

```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```
```math
Percentage\ of\ DFF's = 0.108429685 * 100 = 10.84296854\ \%
```
