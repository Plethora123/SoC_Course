# SoC_Course

## Day 1 Contents
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

![why-to-adopt-the-asic-design-flow-1](https://github.com/user-attachments/assets/f4a02ae5-5f6a-407e-9f19-de32ceb0bb71)

**Fig1: ASIC design flow**

![Screenshot 2024-10-16 014714](https://github.com/user-attachments/assets/da373cb0-0799-4410-a6f1-a87adfedf283)

**Fig2: Physical Design flow**

### OpenLANE Flow
OpenLANE aids ASIC design, enabling RTL-to-GDSII implementation using synthesis and layout tools, culminating in a manufacturable layout.

![Screenshot 2024-10-06 223314](https://github.com/user-attachments/assets/d48e7d4e-35ca-41cd-8fb6-fd791d44816a)

**Fig3: OpenLANE flow**

## Implementation Steps

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
![synthesis_success](https://github.com/user-attachments/assets/5c447652-307c-43cc-803b-75682d630527)

**Fig4: Synthesis Success**

![stats_of_final_synthesis_of_picorv32A](https://github.com/user-attachments/assets/3be7140b-e30a-4ff3-8776-e01dc517cead)

**Fig5: Final stats after synthesis**

Calculation of Flop Ratio and DFF % from synthesis statistics report file

```math
Flop\ Ratio = \frac{1613}{14876} = 0.1084
```
```math
Percentage\ of\ DFF's = 0.1084 * 100 = 10.84\ \%
```

## Day 2 contents

- [Implementation Steps of Floorplan](#implementation-steps-of-floorplan)

### Implementation

Section 2 tasks:- 
1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2. Calculate the die area in microns from the values in floorplan def.
4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
5. Load generated placement def in magic tool and explore the placement.

```math
Area\ of\ die\ in\ microns = Die\ width\ in\ microns * Die\ height\ in\ microns
```
#### 1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
# Now we can run floorplan
run_floorplan
```
