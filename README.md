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
![Screenshot from 2024-10-12 07-49-09](https://github.com/user-attachments/assets/73245535-31ec-4781-9114-45b3c1c6d87a)

**Fig6: Floorplan success**

#### 2. Calculate the die area in microns from the values in floorplan def.

![image](https://github.com/user-attachments/assets/47276ee4-ea46-4c2e-8683-082e9b3ade3c)

**Fig7: Contents of floorplan**


According to floorplan def
```math
1000\ Unit\ Distance = 1\ Micron
```
```math
Die\ width\ in\ unit\ distance = 660685 - 0 = 660685
```
```math
Die\ height\ in\ unit\ distance = 671405 - 0 = 671405
```
```math
Distance\ in\ microns = \frac{Value\ in\ Unit\ Distance}{1000}
```
```math
Die\ width\ in\ microns = \frac{660685}{1000} = 660.685\ Microns
```
```math
Die\ height\ in\ microns = \frac{671405}{1000} = 671.405\ Microns
```
```math
Area\ of\ die\ in\ microns = 660.685 * 671.405 = 443587.212\ Square\ Microns
```

#### Commands to load floorplan def in magic in another terminal

```bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-10_02-16/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![Screenshot from 2024-10-16 02-44-54](https://github.com/user-attachments/assets/5c51deeb-b426-4200-9712-ea4e26ab7844)

**Fig8: Floorplan def in magic tool**

#### 4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

```tcl
# Congestion aware placement by default
run_placement
```
![Screenshot from 2024-10-16 02-58-33](https://github.com/user-attachments/assets/a5ffb598-45eb-4c98-9af6-50568f7195cc)

**Fig9: Placement successful**

Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```



