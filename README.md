# NASSCOM-Digital-VLSI-SoC-design-and-planning

## Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK

<details>
<summary><b>How to talk to computers</b></summary>

<img width="806" height="811" alt="image" src="https://github.com/user-attachments/assets/bd5e7f08-339c-4081-a9f4-c02af247bbc2" />
The development board is a complete hardware platform that hosts the main processing chip along with essential support components such as power regulation, clock sources, external memory, and communication interfaces. It allows users to work with the chip easily without designing the entire hardware from scratch.


<img width="1587" height="863" alt="Screenshot 2025-12-20 170404" src="https://github.com/user-attachments/assets/340c4846-0f4e-44cc-baa4-8097f47b6b47" />


The physical form of this SoC is realized through its package, which exposes the internal functionality to the outside world via pins. The actual silicon die is located at the center of the package and is electrically connected to the package pins using fine wire-bond connections. Each pin is assigned a specific role such as power, ground, clock, analog reference, communication signals, or general-purpose I/O. This packaged chip is what gets soldered onto the development board, serving as the link between the internal SoC architecture and the external PCB circuitry.

<img width="919" height="848" alt="image" src="https://github.com/user-attachments/assets/de35821f-fd93-4754-a8c2-5d31e1abb532" />

Inside the chip mounted on the board lies a fully integrated System on Chip (SoC) rather than just a standalone processor. Along with the CPU core, the SoC contains multiple peripheral blocks such as GPIO controllers, UART, I2C, QSPI, PWM modules, clock and reset logic, and interfaces for external memories like SDRAM and Flash. These internal blocks are interconnected through internal buses and multiplexers, enabling flexible pin sharing and efficient communication with external devices. This high level of integration significantly reduces system complexity, power consumption, and board area.
<img width="994" height="855" alt="Screenshot 2025-12-20 171047" src="https://github.com/user-attachments/assets/991e08a2-9556-4eaa-87cd-bf6e106ec4fe" />



The package view shows the external pins of the chip placed around its edges, where each pin is assigned to functions like GPIO, power, clock, analog signals, or communication interfaces. This pin arrangement defines how the chip connects to the board and external components.
<img width="1271" height="842" alt="Screenshot 2025-12-20 171110" src="https://github.com/user-attachments/assets/88ab7199-7b1e-412b-8a72-a266be99c184" />

The die view shows the actual silicon inside the package, with pads placed around the boundary and the core logic at the center. Signals travel from the core to the pads and then through wire bonds to the package pins, forming the link between internal circuitry and the outside world.
<img width="1213" height="869" alt="image" src="https://github.com/user-attachments/assets/904d7148-24a1-4c36-9baf-0253907079af" />
A foundry is the facility where semiconductor chips are physically manufactured using a specific fabrication process. Foundry IPs are technology-specific intellectual property blocks provided or qualified for that foundry, such as I/O cells, ADCs, DACs, PLLs, and memory interfaces, which require deep process knowledge and high design expertise to develop. In contrast, commonly used and repeatable digital logic blocks, such as standard cells or pre-designed functional blocks, are referred to as macros, as they can be reused across designs with minimal modification within the same technology node.






## Instruction Set Architecture (ISA)

An **Instruction Set Architecture (ISA)** acts as the formal interface between software and hardware. It defines **what the processor can do**, not how it is physically implemented. The ISA specifies the supported instructions, register set, data types, addressing modes, and how instructions interact with memory and I/O.

In the case of **RISC-V**, the ISA follows a reduced instruction set philosophy, using simple and efficient instructions that are easy to decode and execute in hardware. RISC-V is modular and extensible, allowing designers to include only the required instruction subsets while maintaining software compatibility.

Because software is written targeting an ISA rather than a specific chip layout, the same program can run on different processors as long as they implement the same ISA. This abstraction enables portability, scalability, and independent evolution of software and hardware designs.

<img width="1869" height="1130" alt="image" src="https://github.com/user-attachments/assets/2d25b92a-9c16-4e36-a1ca-24c2480ed7f6" />



<img width="1826" height="1139" alt="image" src="https://github.com/user-attachments/assets/3958029f-4e29-49b3-aeab-3f7d62096239" />

To run an application on hardware, the program passes through several stages of system software. Application programs written in high-level languages such as C, C++, VB, or Java are managed by the Operating System and given to the compiler. The compiler converts the source code into assembly instructions, which are specific to the target hardware architecture. These instructions are then processed by the assembler, which translates them into binary machine code. Finally, the hardware executes the program based on the received binary instructions.

<img width="1783" height="1124" alt="image" src="https://github.com/user-attachments/assets/299afa95-421b-4a9e-a38b-75d404a675f8" />

## Course Structure

This course is structured into three major components:

1. **RISC-V Instruction Set Architecture (ISA)**  
   Introduction to the RISC-V ISA, including instruction formats, addressing modes, and architectural principles.

2. **RTL Design and Synthesis of a RISC-V–Based CPU Core (picorv32)**  
   Design, simulation, and synthesis of the picorv32 processor core using Register Transfer Level (RTL) methodologies.

3. **Physical Design Implementation of picorv32**  
   Backend physical design flow including floorplanning, placement, routing, and layout generation for the picorv32 core.


</details>

<details>
<summary><b>SoC design and OpenLANE</b></summary>

<img width="1806" height="825" alt="image" src="https://github.com/user-attachments/assets/715a0ceb-5315-4d10-95f6-5547a03505b6" />


In the early years of integrated circuit (IC) development, the **design and fabrication processes were tightly coupled** and carried out by only a few vertically integrated companies such as Intel and Texas Instruments. This limited IC development to organizations that owned fabrication facilities.

In 1979, Lynn Conway and Carver Mead proposed a revolutionary idea to **separate IC design from fabrication**. They introduced **structured VLSI design methodologies** based on λ-based (lambda-based) design rules and published the seminal book *Introduction to VLSI Systems*. This work laid the foundation for formal VLSI education and modern digital IC design practices.

This separation of concerns led to the emergence of **fabless design companies**, which focus exclusively on IC design, and **pure-play foundries**, which specialize solely in fabrication. Communication between designers and fabrication facilities evolved into a standardized interface consisting of data files and documentation known as **Process Design Kits (PDKs)**.

A PDK includes, but is not limited to:
- Device and SPICE models  
- Technology and process information  
- Design rules  
- Digital standard cell libraries  
- I/O libraries and verification decks  

Due to the proprietary and sensitive nature of this information, PDKs have traditionally been distributed under **Non-Disclosure Agreements (NDAs)**, making them inaccessible to the public and academic community.

In a major step toward open hardware enablement, Google collaborated with SkyWater Technology to open-source the **130 nm process PDK**. As a result, on **June 30, 2020**, Google released the **first fully open-source PDK**, significantly lowering the barrier to entry for VLSI education, research, and open silicon development.
<img width="1785" height="829" alt="image" src="https://github.com/user-attachments/assets/d48f631e-9f5e-46f3-8e2c-73182d92dcd4" />
We will be using 130nm technology since it is open-source and it is still being used in industry

<img width="1789" height="915" alt="image" src="https://github.com/user-attachments/assets/bc81e4d2-b781-44f3-b1cb-28384e9b9bb7" />
In this course we will be doing many things from rtl to gds so we will use many open-source eda tools
<img width="1249" height="550" alt="image" src="https://github.com/user-attachments/assets/ef69851b-c353-413c-9d1d-00e411c42492" />
Synthesis
It is the process of converting rtl into netlist with the help of lib file of sky130.
<img width="1772" height="833" alt="image" src="https://github.com/user-attachments/assets/78c00d63-9761-441e-8b54-25e9283dfc2e" />
Floor and Power Planning
<img width="1253" height="513" alt="image" src="https://github.com/user-attachments/assets/1c343735-f02e-4b21-af4f-d54e4db12a74" />
Power planning is typically implemented using the **upper metal layers** of the chip, as these layers are thicker and therefore exhibit **lower resistance** compared to lower metal layers. Utilizing upper metal layers enables efficient distribution of power across the design. Proper power planning is essential to **minimize IR drops** and to **prevent electromigration**, thereby ensuring reliable and robust circuit operation.
Floorplanning is the physical design stage where the chip’s size, shape, and placement of major blocks are defined to optimize area, timing, power distribution, and routability.
<img width="1772" height="902" alt="image" src="https://github.com/user-attachments/assets/a12de10b-03a6-4e92-83c8-0beed2590462" />
Clock Tree Synthesis
<img width="1784" height="850" alt="image" src="https://github.com/user-attachments/assets/5b361d76-f305-4974-9cb5-520d9371ac2c" />
Routing
skywater PDK has 6 routing layers in which the lowest layer is called the local interconnect layer which is a Titanium Nitride layer the following 5 layers are all Aluminium layers
<img width="1785" height="962" alt="image" src="https://github.com/user-attachments/assets/4565dc9e-e4bc-4219-84be-8bc0fe024a1f" />

At the last step in sign off we will test it with DRC and TVS and timing statistics and send it to tape-out
* OPENLANE
OpenLane is an open-source digital ASIC design flow that automates the process from RTL to GDSII (chip layout). It integrates several tools like Yosys, OpenROAD, Magic, and KLayout to perform synthesis, floorplanning, placement, routing, and signoff checks.
It’s widely used for academic and research purposes to design and tape-out chips using open-source PDKs such as SkyWater 130nm (Sky130).

<img width="1786" height="823" alt="image" src="https://github.com/user-attachments/assets/84e6cb16-8941-453b-9157-4f8a2903968f" />
<img width="1773" height="797" alt="image" src="https://github.com/user-attachments/assets/c6da9ee1-efdf-4bb9-b424-782b49bdb467" />
<img width="1255" height="533" alt="image" src="https://github.com/user-attachments/assets/0828c7f9-4b1a-4ded-ad7f-56283833aee6" />
 
 ## OpenLane ASIC Design Flow

The OpenLane flow automates the complete RTL-to-GDSII process for ASIC design using open-source tools. It covers all major design stages — from logic synthesis to final layout generation — ensuring Design Rule Check (DRC) and Layout vs. Schematic (LVS) clean results.

 ## Major Stages in the Flow:

Synthesis – Converts RTL (Verilog) into a gate-level netlist using Yosys.

Floorplanning – Defines chip area, power grid, and placement regions.

Placement – Places standard cells optimally using OpenROAD.

Clock Tree Synthesis (CTS) – Builds a balanced clock distribution network.

Routing – Connects all placed cells following design rules.

Physical Verification – Performs DRC and LVS checks using Magic and Netgen.

GDSII Generation – Produces the final mask layout file for fabrication.
<img width="1190" height="514" alt="image" src="https://github.com/user-attachments/assets/04592d6f-1b52-4f2c-8465-d4459652dbfb" />
<img width="1783" height="838" alt="image" src="https://github.com/user-attachments/assets/f0f5a99c-a793-4f34-a47b-9a6cb5a0ebf2" />
<img width="1785" height="788" alt="image" src="https://github.com/user-attachments/assets/897cae99-525b-4227-b736-f8d3694ca09a" />
We will use magic for dealing this
<img width="1162" height="511" alt="image" src="https://github.com/user-attachments/assets/2c22d1e4-a9be-480b-9db4-8af48b673723" />

</details>

<details>
<summary><b>Getting familiar with open-source EDA tools</b></summary>



Day  1 Labs :- 
1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
2. Calculate the flop ratio.

```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```
```math
Percentage\ of\ DFF's = Flop\ Ratio * 100
```

#### 1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform synthesis

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```


<img width="901" height="573" alt="image" src="https://github.com/user-attachments/assets/3615b60e-ddf6-423e-980f-d7c4cc1a4948" />

<img width="784" height="471" alt="image" src="https://github.com/user-attachments/assets/9c060b69-d053-46fb-a2a8-47f334d8fc0e" />


#### 2. Calculate the flop ratio.

Screenshots of synthesis statistics report file with required values highlighted
<img width="1724" height="687" alt="image" src="https://github.com/user-attachments/assets/2500f574-6a07-4dfc-82ca-a5138cae5950" />


Calculation of Flop Ratio and DFF % from synthesis statistics report file

```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```
```math
Percentage\ of\ DFF's = 0.108429685 * 100 = 10.84296854\ \%
```

#### 3. Reports
<img width="785" height="582" alt="image" src="https://github.com/user-attachments/assets/23f35fe6-0503-4291-969e-38dadcb74403" />






</details>
