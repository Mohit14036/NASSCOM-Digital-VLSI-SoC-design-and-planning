<img width="951" height="1120" alt="image" src="https://github.com/user-attachments/assets/889693e7-ea1d-4e61-92dd-963b6a11f1db" /># NASSCOM-Digital-VLSI-SoC-design-and-planning

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

## Day 2 - Good floorplan vs bad floorplan and introduction to library cells

<details>
<summary><b>IMPLEMENTATION</b></summary>
1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2. Calculate the die area in microns from the values in floorplan def.
3. Load generated floorplan def in magic tool and explore the floorplan.
4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
5. Load generated placement def in magic tool and explore the placement.

```math
Area\ of\ die\ in\ microns = Die\ width\ in\ microns * Die\ height\ in\ microns
```

#### 1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform floorplan

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

# Now we can run floorplan
run_floorplan
```

Screenshot of floorplan run



<img width="1279" height="593" alt="Screenshot 2025-12-20 230907" src="https://github.com/user-attachments/assets/82ea2b51-7574-4756-bd58-71d2937c94d8" />

<img width="733" height="484" alt="Screenshot 2025-12-21 201450" src="https://github.com/user-attachments/assets/efdf480d-b891-48d5-a9f1-b4294247e892" />

#### 2. Calculate the die area in microns from the values in floorplan def.

Screenshot of contents of floorplan def
<img width="1448" height="834" alt="image" src="https://github.com/user-attachments/assets/4f35f6b3-df2b-4666-82f8-19dbfed1b813" />

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
Area\ of\ die\ in\ microns = 660.685 * 671.405 = 443587.212425\ Square\ Microns
```

#### 3. Load generated floorplan def in magic tool and explore the floorplan.

Commands to load floorplan def in magic in another terminal

```bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

Screenshots of floorplan def in magic
<img width="689" height="783" alt="Screenshot 2025-12-21 202236" src="https://github.com/user-attachments/assets/a1f002aa-f036-496b-882f-a71d2f809454" />

Equidistant placement of ports

<img width="1426" height="820" alt="image" src="https://github.com/user-attachments/assets/bcda528d-41c0-4c7c-a0f5-768ae326891a" />

Port layer as set through config.tcl

<img width="1427" height="831" alt="image" src="https://github.com/user-attachments/assets/b1394646-bd5c-4743-875e-ee402618c8a4" />


Decap Cells and Tap Cells

<img width="248" height="644" alt="image" src="https://github.com/user-attachments/assets/013e9bee-f22f-4d66-b87d-6ed2fb3e52ec" />

Diogonally equidistant Tap cells
<img width="1370" height="823" alt="image" src="https://github.com/user-attachments/assets/020f6841-b2c3-4120-824d-8e45eb31a130" />

Unplaced standard cells at the origin
<img width="1431" height="830" alt="image" src="https://github.com/user-attachments/assets/d2469a3b-3ce2-43d7-bae2-85f9b02e9131" />

#### 4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

```tcl
# Congestion aware placement by default
run_placement
```

Screenshots of placement run

<img width="1344" height="812" alt="image" src="https://github.com/user-attachments/assets/34a291c1-75d3-4184-b8ff-9fd5c5cca608" />

<img width="1367" height="793" alt="image" src="https://github.com/user-attachments/assets/5a19d669-caf0-4d04-bb1f-1a0c2e3e31a0" />

#### 5. Load generated placement def in magic tool and explore the placement.

Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

Screenshots of placement def in magic


<img width="1355" height="817" alt="image" src="https://github.com/user-attachments/assets/6551580c-f3e6-4359-b35d-067d542b834a" />



Standard cells legally placed 

<img width="1320" height="813" alt="image" src="https://github.com/user-attachments/assets/c8583c21-6da7-4e74-9fab-5a8ee0a71868" />


Commands to exit from current run

```tcl
# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```
</details>

## Day3 - Design library cell using Magic Layout and ngspice characterization 
<details>
  <summary>
 IMPLEMENTATION
  </summary>

1. Clone custom inverter standard cell design from github repository: [Standard cell design and characterization using OpenLANE flow](https://github.com/nickson-jose/vsdstdcelldesign).
2. Load the custom inverter layout in magic and explore.
3. Spice extraction of inverter in magic.
4. Editing the spice model file for analysis through simulation.
5. Post-layout ngspice simulations.
6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.


#### 1. Clone custom inverter standard cell design from github repository

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Check contents whether everything is present
ls

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

Screenshot of commands run
<img width="1365" height="829" alt="image" src="https://github.com/user-attachments/assets/68dc55b6-6008-480b-ad67-23c559fa9761" />

#### 2. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic
<img width="717" height="768" alt="Screenshot 2025-12-21 215255" src="https://github.com/user-attachments/assets/60f7a1bb-7fb6-46ff-8fdb-e2f7a29acab4" />

NMOS and PMOS identified

<img width="1344" height="832" alt="image" src="https://github.com/user-attachments/assets/8d5dc57a-a181-4cf5-b1a2-e6bda478172d" />
<img width="1359" height="813" alt="image" src="https://github.com/user-attachments/assets/a230a44c-ca68-4ceb-b661-8727eaaff204" />

Output Y connectivity to PMOS and NMOS drain verified

<img width="1918" height="978" alt="image" src="https://github.com/user-attachments/assets/4c9cf7b7-7206-465d-a54b-632bd12c77ad" />

PMOS source connectivity to VDD (here VPWR) verified

<img width="1919" height="1105" alt="image" src="https://github.com/user-attachments/assets/eb35757b-8b69-40b4-9b3f-5c6a4ba1c4ac" />

Deleting necessary layout part to see DRC error
<img width="1919" height="1130" alt="image" src="https://github.com/user-attachments/assets/d8a2fd87-aff3-41eb-9583-1b016190d468" />


#### 3. Spice extraction of inverter in magic.

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

```tcl
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```

Screenshot of tkcon window after running above commands

<img width="1916" height="1123" alt="image" src="https://github.com/user-attachments/assets/80be4ec2-5164-4381-a903-5f5267cc4cf4" />


Screenshot of created spice file

<img width="781" height="534" alt="image" src="https://github.com/user-attachments/assets/30a8a7a9-c243-44b4-89b4-84ff94f7b833" />
#### 4. Editing the spice model file for analysis through simulation.

Measuring unit distance in layout grid
<img width="1911" height="1120" alt="image" src="https://github.com/user-attachments/assets/b9041bc2-2c8d-4206-a070-44cf5014c000" />
Final edited spice file ready for ngspice simulation

<img width="741" height="529" alt="image" src="https://github.com/user-attachments/assets/aad6b6b8-bff2-4264-bb54-028b8d318149" />
<img width="742" height="542" alt="image" src="https://github.com/user-attachments/assets/175ff37b-7751-4f7a-97fd-4007e17db390" />


#### 5. Post-layout ngspice simulations.

Commands for ngspice simulation

```bash
# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```

Screenshots of ngspice run

<img width="865" height="1086" alt="Screenshot 2025-12-21 230834" src="https://github.com/user-attachments/assets/a6f006e3-f586-471f-be99-f34ef16a118f" />
Screenshot of generated plot

<img width="935" height="1113" alt="Screenshot 2025-12-21 230952" src="https://github.com/user-attachments/assets/3547e853-252e-40f7-84b9-764fea59014a" />

Rise transition time calculation

```math
Rise\ transition\ time = Time\ taken\ for\ output\ to\ rise\ to\ 80\% - Time\ taken\ for\ output\ to\ rise\ to\ 20\%
```
```math
20\%\ of\ output = 660\ mV
```
```math
80\%\ of\ output = 2.64\ V
```

20% Screenshots
<img width="1281" height="738" alt="Screenshot 2025-12-21 231446" src="https://github.com/user-attachments/assets/95f40a46-5387-4450-b90f-63312b2fdad4" />

80% Screenshots

<img width="1728" height="947" alt="Screenshot 2025-12-21 231654" src="https://github.com/user-attachments/assets/83513442-4906-435a-8d02-ff4ed3e110f9" />

```math
Rise\ transition\ time = 2.246 - 2.18269 = 0.06331\ ns = 63.31\ ps
```

Fall transition time calculation

```math
Fall\ transition\ time = Time\ taken\ for\ output\ to\ fall\ to\ 20\% - Time\ taken\ for\ output\ to\ fall\ to\ 80\%
```
```math
20\%\ of\ output = 660\ mV
```
```math
80\%\ of\ output = 2.64\ V
```

20% Screenshots

<img width="1916" height="1089" alt="image" src="https://github.com/user-attachments/assets/08cf7fc8-c4d6-47a9-b1db-44b319edaed2" />

80% Screenshots
<img width="1851" height="1079" alt="image" src="https://github.com/user-attachments/assets/5f028298-f415-4f85-a5d2-351aa8d1ce50" />


```math
Fall\ transition\ time = 4.0953 - 4.05149 = 0.04381\ ns = 43.81\ ps
```

Rise Cell Delay Calculation

```math
Rise\ Cell\ Delay = Time\ taken\ for\ output\ to\ rise\ to\ 50\% - Time\ taken\ for\ input\ to\ fall\ to\ 50\%
```
```math
50\%\ of\ 3.3\ V = 1.65\ V
```

50% Screenshots
<img width="1919" height="1124" alt="image" src="https://github.com/user-attachments/assets/0c5bc241-d0e9-4658-b1c3-4118f2fc1810" />

```math
Rise\ Cell\ Delay = 2.20465 - 2.13134 = 0.07331\ ns = 73.31\ ps
```

Fall Cell Delay Calculation


```math
Fall\ Cell\ Delay = Time\ taken\ for\ output\ to\ fall\ to\ 50\% - Time\ taken\ for\ input\ to\ rise\ to\ 50\%
```
```math
50\%\ of\ 3.3\ V = 1.65\ V
```

50% Screenshots

<img width="1919" height="1128" alt="image" src="https://github.com/user-attachments/assets/74c4e849-fcbb-4ce7-b20a-8ae13e087184" />


```math
Fall\ Cell\ Delay = 4.07442 - 4.03 = 0.04442\ ns = 40.42\ ps
```



#### 6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

Link to Sky130 Periphery rules: [https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)

Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

```bash
# Change to home directory
cd

# Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

# Since lab file is compressed command to extract it
tar xfz drc_tests.tgz

# Change directory into the lab folder
cd drc_tests

# List all files and directories present in the current directory
ls -al

# Command to view .magicrc file
gvim .magicrc

# Command to open magic tool in better graphics
magic -d XR &
```

Screenshots of commands run
<img width="1919" height="1127" alt="image" src="https://github.com/user-attachments/assets/d428bbf2-6409-4bce-8371-784ba1a61b81" />


Screenshot of .magicrc file

<img width="1914" height="1030" alt="image" src="https://github.com/user-attachments/assets/1c484af9-df97-4e10-a35d-5b6fac05f4e7" />

**Incorrectly implemented poly.9 simple rule correction**

Screenshot of poly rules

<img width="1114" height="379" alt="image" src="https://github.com/user-attachments/assets/c9b6bae0-19bb-4a85-a31b-52ca3eff4ce2" />

Incorrectly implemented poly.9 rule no drc violation even though spacing < 0.48u

<img width="1852" height="995" alt="image" src="https://github.com/user-attachments/assets/882b20f5-9894-460b-bfff-07eee160182e" />
New commands inserted in sky130A.tech file to update drc
<img width="1919" height="1127" alt="image" src="https://github.com/user-attachments/assets/2ae74555-eb91-4659-a99d-bdc0f4a4224e" />





Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```

Screenshot of magic window with rule implemented
<img width="1917" height="1128" alt="Screenshot 2025-12-23 122204" src="https://github.com/user-attachments/assets/61dcc4a8-c8de-4ae0-a797-0fc11318d9c0" />

**Incorrectly implemented difftap.2 simple rule correction**

Screenshot of difftap rules

<img width="1133" height="792" alt="image" src="https://github.com/user-attachments/assets/8c629027-fc86-450e-9d35-f71374423e81" />

Incorrectly implemented difftap.2 rule no drc violation even though spacing < 0.42u

<img width="1919" height="1127" alt="image" src="https://github.com/user-attachments/assets/011ed21a-b6a1-4704-a9bf-d8a14a87ff5a" />

New commands inserted in sky130A.tech file to update drc

<img width="1919" height="1129" alt="image" src="https://github.com/user-attachments/assets/86eb74c3-651f-46e7-9141-86e816bf0165" />

Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```

Screenshot of magic window with rule implemented

<img width="1919" height="1120" alt="Screenshot 2025-12-23 122825" src="https://github.com/user-attachments/assets/2e3d2130-85db-4df7-8153-84c6f10312ef" />

**Incorrectly implemented nwell.4 complex rule correction**

Screenshot of nwell rules

<img width="1133" height="841" alt="image" src="https://github.com/user-attachments/assets/a62873a1-34bd-4a69-a15f-562d05500482" />

Incorrectly implemented nwell.4 rule no drc violation even though no tap present in nwell

<img width="1919" height="1127" alt="image" src="https://github.com/user-attachments/assets/4742047a-6c32-4149-9b85-0e0332430eba" />

New commands inserted in sky130A.tech file to update drc

<img width="642" height="597" alt="image" src="https://github.com/user-attachments/assets/67d0ca2b-6d78-46a7-a1f8-df940999ccd1" />
<img width="638" height="595" alt="image" src="https://github.com/user-attachments/assets/b2903e82-30ab-46f9-9885-14e33886a14d" />

Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Change drc style to drc full
drc style drc(full)

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```

Screenshot of magic window with rule implemented

<img width="1808" height="839" alt="image" src="https://github.com/user-attachments/assets/60d5c6e6-661b-4bd9-be24-5465d7e7dd91" />

</details>

## Day 4 - Pre-layout timing analysis and importance of good clock tree 

<details>
  <summary>
 IMPLEMENTATION
  </summary>

* Day 4 tasks:-
1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
2. Save the finalized layout with custom name and open it.
3. Generate lef from the layout.
4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
6. Run openlane flow synthesis with newly inserted custom inverter cell.
7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
9. Do Post-Synthesis timing analysis with OpenSTA tool.
10. Make timing ECO fixes to remove all violations.
11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
12. Post-CTS OpenROAD timing analysis.
13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.


#### 1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.

Conditions to be verified before moving forward with custom designed cell layout:
* Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
* Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
* Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.

Commands to open the custom inverter layout

```bash
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

Screenshot of tracks.info of sky130_fd_sc_hd

<img width="650" height="591" alt="image" src="https://github.com/user-attachments/assets/d989b4fc-2c21-4b13-8a95-be970d1e3ec0" />

commands for tkcon window to set grid as tracks of locali layer

```tcl
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```

Screenshot of commands run
<img width="976" height="469" alt="image" src="https://github.com/user-attachments/assets/80b567ce-6a36-488e-a05a-8254f8e9b65f" />

Condition 1 verified

<img width="552" height="236" alt="image" src="https://github.com/user-attachments/assets/dc2cd5d1-0a02-409a-aee4-0fb92bba0575" />

Condition 2 verified

```math
Horizontal\ track\ pitch = 0.46\ um
```
<img width="1042" height="603" alt="image" src="https://github.com/user-attachments/assets/343add73-fb48-4407-813e-c3dd38624312" />

```math
Width\ of\ standard\ cell = 1.38\ um = 0.46 * 3
```

Condition 3 verified

```math
Vertical\ track\ pitch = 0.34\ um
```

<img width="1615" height="836" alt="image" src="https://github.com/user-attachments/assets/7b22cc91-8c54-4ad9-931d-2a0cb1cd3ba3" />

```math
Height\ of\ standard\ cell = 2.72\ um = 0.34 * 8
```

#### 2. Save the finalized layout with custom name and open it.

Command for tkcon window to save the layout with custom name

```tcl
# Command to save as
save sky130_vsdinv.mag
```

Command to open the newly saved layout
```bash
# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_vsdinv.mag &
```
#### 3. Generate lef from the layout.

Command for tkcon window to write lef

```tcl
# lef command
lef write
```

Screenshot of command run

<img width="966" height="470" alt="image" src="https://github.com/user-attachments/assets/49b76cac-ef14-41e7-95ec-870eacb4a587" />


Screenshot of newly created lef file
<img width="728" height="518" alt="Screenshot 2025-12-23 124834" src="https://github.com/user-attachments/assets/e2377a7c-3850-432d-93f9-580347e3395d" />




#### 4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.

Commands to copy necessary files to 'picorv32a' design 'src' directory

```bash
# Copy lef file
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

Screenshot of commands run

<img width="722" height="521" alt="image" src="https://github.com/user-attachments/assets/41f39962-6e1e-4830-a413-94a0dc829ff4" />


#### 5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.

Commands to be added to config.tcl to include our custom cell in the openlane flow

```tcl
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

Edited config.tcl to include the added lef and change library to ones we added in src directory

<img width="1893" height="1128" alt="image" src="https://github.com/user-attachments/assets/8e8a5cdf-8a34-4083-81bb-eaafa9ce0066" />

#### 6. Run openlane flow synthesis with newly inserted custom inverter cell.

Commands to invoke the OpenLANE flow include new lef and perform synthesis 

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

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshots of result run

<img width="1851" height="955" alt="image" src="https://github.com/user-attachments/assets/0b19316c-494c-436c-96f8-2eaf85879cb7" />


#### 7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.

Noting down current design values generated before modifying parameters to improve timing\

<img width="953" height="1127" alt="image" src="https://github.com/user-attachments/assets/9cfc3681-1518-4307-a965-6ea70f17abef" />
<img width="438" height="239" alt="image" src="https://github.com/user-attachments/assets/793dd089-84b0-4e75-a001-c54a818b3a03" />

Commands to view and change parameters to improve timing and run synthesis

```tcl
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 23-12_07-25 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshot of merged.lef in `tmp` directory with our custom inverter as macro

<img width="891" height="923" alt="image" src="https://github.com/user-attachments/assets/4ef3a8eb-a2ff-4e37-93ad-f183bcd6b2db" />

Screenshots of commands run

<img width="452" height="260" alt="Screenshot 2025-12-23 125839" src="https://github.com/user-attachments/assets/c4cb67c8-4515-4203-b12f-c0ea571daec2" />

Comparing to previously noted run values area has increased and worst negative slack has become 0

<img width="883" height="243" alt="image" src="https://github.com/user-attachments/assets/f2d8e64c-ff6c-4b7d-ba25-983dab5d6b4b" />
<img width="884" height="670" alt="image" src="https://github.com/user-attachments/assets/c2538dc1-b6e4-47f5-8687-529b39fd3937" />


#### 8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.

Now that our custom inverter is properly accepted in synthesis we can now run floorplan using following command

```tcl
# Now we can run floorplan
run_floorplan
```

Screenshots of command run

<img width="367" height="126" alt="image" src="https://github.com/user-attachments/assets/a694bf8c-e8dd-4fb6-b23a-386406bd745c" />
<img width="892" height="517" alt="image" src="https://github.com/user-attachments/assets/39cc9db3-3836-45c7-b34e-b97e82488b4b" />


Since we are facing unexpected un-explainable error while using `run_floorplan` command, we can instead use the following set of commands available based on information from `Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl` and also based on `Floorplan Commands` section in `Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md`

```tcl
# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or
```

Screenshots of commands run

<img width="739" height="515" alt="image" src="https://github.com/user-attachments/assets/b10c4904-e9e1-4a7e-bf6f-69c969e837dc" />
<img width="957" height="1128" alt="image" src="https://github.com/user-attachments/assets/b7631f16-9b61-46ba-b13e-f9708522b517" />
<img width="948" height="1122" alt="Screenshot 2025-12-23 163716" src="https://github.com/user-attachments/assets/0c1bc271-466d-4fcb-8af8-fdbf5d219f4c" />

Now that floorplan is done we can do placement using following command

```tcl
# Now we are ready to run placement
run_placement
```

Screenshots of command run
<img width="956" height="1130" alt="image" src="https://github.com/user-attachments/assets/ac0e972e-14ef-4c10-beb6-e41853b91e0c" />
<img width="951" height="1119" alt="image" src="https://github.com/user-attachments/assets/d9c3134f-d648-403d-af74-6d7f06b53a4a" />
<img width="957" height="1133" alt="image" src="https://github.com/user-attachments/assets/e34e4e96-d165-466d-9110-538dff7cf26d" />

Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

Screenshot of placement def in magic

<img width="947" height="1122" alt="image" src="https://github.com/user-attachments/assets/3a5ddfa9-b61c-45e0-8861-bba6d70180f9" />


Screenshot of custom inverter inserted in placement def with proper abutment

<img width="1046" height="1076" alt="image" src="https://github.com/user-attachments/assets/84a455ca-4331-484c-addb-80affe30de52" />


Command for tkcon window to view internal layers of cells

```tcl
# Command to view internal connectivity layers
expand
```

Abutment of power pins with other cell from library clearly visible

<img width="530" height="387" alt="image" src="https://github.com/user-attachments/assets/cd80f642-9b16-4b7e-ae15-d3989f4064e0" />



#### 9. Do Post-Synthesis timing analysis with OpenSTA tool.

Since we are having 0 wns after improved timing run we are going to do timing analysis on initial run of synthesis which has lots of violations and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform synthesis 

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

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Commands run final screenshot

<img width="956" height="1123" alt="Screenshot 2025-12-23 170624" src="https://github.com/user-attachments/assets/2859088a-b15d-40de-b76c-681f51febf74" />

Newly created `pre_sta.conf` for STA analysis in `openlane` directory

<img width="723" height="518" alt="image" src="https://github.com/user-attachments/assets/0214f74d-8e31-4eb4-844e-692c53911df1" />


Newly created `my_base.sdc` for STA analysis in `openlane/designs/picorv32a/src` directory based on the file `openlane/scripts/base.sdc`

<img width="720" height="521" alt="image" src="https://github.com/user-attachments/assets/9ba36665-0411-4b05-8e00-e0c1463caf72" />

<img width="951" height="1120" alt="image" src="https://github.com/user-attachments/assets/5400d910-a010-49da-a277-4e48ecddef48" />


Commands to run STA in another terminal

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

Screenshots of commands run

<img width="742" height="189" alt="image" src="https://github.com/user-attachments/assets/98553b1d-d111-4449-8b31-8853de8a9807" />
<img width="733" height="470" alt="image" src="https://github.com/user-attachments/assets/66e0cbc9-176b-40b9-a321-cd3cad3e6c53" />

Since more fanout is causing more delay we can add parameter to reduce fanout and do synthesis again

Commands to include new lef and perform synthesis 

```tcl
# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a -tag 23-12_11-20 -overwrite

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to set new value for SYNTH_MAX_FANOUT
set ::env(SYNTH_MAX_FANOUT) 4

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Commands run final screenshot

<img width="731" height="518" alt="image" src="https://github.com/user-attachments/assets/85bfd9a4-7428-46a6-8e3d-76ae127b0dc8" />

Commands to run STA in another terminal

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

Screenshots of commands run
<img width="740" height="509" alt="image" src="https://github.com/user-attachments/assets/ff9f1b0c-468f-406e-90c2-3c52f05e4b2b" />

<img width="745" height="525" alt="image" src="https://github.com/user-attachments/assets/e40024c9-ff9b-405b-91e4-5767936a5ab1" />


#### 10. Make timing ECO fixes to remove all violations.

OR gate of drive strength 2 is driving 4 fanouts

<img width="778" height="533" alt="image" src="https://github.com/user-attachments/assets/884beab0-1c1a-4622-8ad7-052f70a87186" />


Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11672_

# Checking command syntax
help replace_cell

# Replacing cell
replace_cell _14510_ sky130_fd_sc_hd__or3_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced
<img width="763" height="545" alt="image" src="https://github.com/user-attachments/assets/715a3aa6-7aab-4d5f-89ee-33a115b9b7dd" />
<img width="1039" height="529" alt="image" src="https://github.com/user-attachments/assets/d84aaca2-4fb0-4135-aa2b-8010a2a447c5" />
<img width="1054" height="524" alt="image" src="https://github.com/user-attachments/assets/3259a2ad-fa32-4d82-862d-a35bf72448e5" />

OR gate of drive strength 2 is driving 4 fanouts

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11675_

# Replacing cell
replace_cell _14514_ sky130_fd_sc_hd__or3_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced

<img width="797" height="526" alt="image" src="https://github.com/user-attachments/assets/1a5a86a1-0164-4697-a6b6-8a58c1cde27d" />
<img width="810" height="521" alt="image" src="https://github.com/user-attachments/assets/3a32ec1f-52f0-4702-a36a-96a9dcb47127" />
<img width="796" height="546" alt="image" src="https://github.com/user-attachments/assets/8e341168-c710-44d9-b652-16e8a9fab594" />
OR gate of drive strength 2 driving OA gate has more delay

<img width="815" height="517" alt="image" src="https://github.com/user-attachments/assets/25212cc7-f09f-4e49-99be-1dd9ab947905" />





Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11643_

# Replacing cell
replace_cell _14481_ sky130_fd_sc_hd__or4_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced
<img width="813" height="275" alt="image" src="https://github.com/user-attachments/assets/4b085fd1-c687-40f1-ab02-a141d2b5e6cd" />
<img width="857" height="434" alt="image" src="https://github.com/user-attachments/assets/8b98fac3-781c-4184-a48e-a9c8911d5fdd" />

OR gate of drive strength 2 driving OA gate has more delay

<img width="826" height="454" alt="image" src="https://github.com/user-attachments/assets/c13dee1e-4f6a-4def-a7ad-be47795f46c7" />

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11668_

# Replacing cell
replace_cell _14506_ sky130_fd_sc_hd__or4_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced
<img width="814" height="426" alt="image" src="https://github.com/user-attachments/assets/c868b285-46ca-48cd-b138-c9cd39fa04ef" />

<img width="819" height="471" alt="image" src="https://github.com/user-attachments/assets/d03f1c03-5f98-41a4-b47f-2d81d80b08ef" />

Commands to verify instance `_14506_`  is replaced with `sky130_fd_sc_hd__or4_4`

```tcl
# Generating custom timing report
report_checks -from _29043_ -to _30440_ -through _14506_
```

Screenshot of replaced instance

<img width="650" height="548" alt="image" src="https://github.com/user-attachments/assets/02cfd203-6946-43d5-ad10-d04b1070c052" />

*We started ECO fixes at wns -23.9000 and now we stand at wns -22.6173 we reduced around 1.2827 ns of violation*

#### 11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.

Now to insert this updated netlist to PnR flow and we can use `write_verilog` and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist

Commands to make copy of netlist

```bash
# Change from home directory to synthesis results directory
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/

# List contents of the directory
ls -ltr

# Copy and rename the netlist
cp picorv32a.synthesis.v picorv32a.synthesis_old.v

# List contents of the directory
ls -ltr
```

Screenshot of commands run

<img width="1060" height="334" alt="image" src="https://github.com/user-attachments/assets/5286e63e-2062-480a-9ffa-37095639e525" />


Commands to write verilog

```tcl
# Check syntax
help write_verilog

# Overwriting current synthesis netlist
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/23-12_11-20/results/synthesis/picorv32a.synthesis.v

# Exit from OpenSTA since timing analysis is done
exit
```



Verified that the netlist is overwritten by checking that instance `_14506_`  is replaced with `sky130_fd_sc_hd__or4_4`

<img width="570" height="537" alt="image" src="https://github.com/user-attachments/assets/4cc374e2-663a-4ba4-acbf-8df2655a5d65" />


Since we confirmed that netlist is replaced and will be loaded in PnR but since we want to follow up on the earlier 0 violation design we are continuing with the clean design to further stages

Commands load the design and run necessary stages

```tcl
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 23-12_11-20 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts
```

Screenshots of commands run
<img width="980" height="531" alt="image" src="https://github.com/user-attachments/assets/4d84d5cc-e838-48ad-86ee-821d81740f89" />
<img width="1058" height="509" alt="image" src="https://github.com/user-attachments/assets/e479fda4-77b6-41e1-be83-b398665e7dd7" />
<img width="1064" height="548" alt="image" src="https://github.com/user-attachments/assets/6a7143b0-3e55-4679-a727-d7b7902be342" />
<img width="977" height="189" alt="image" src="https://github.com/user-attachments/assets/65fb9d9c-b0f3-4c65-b86d-fae8d856a3a6" />
<img width="1063" height="505" alt="image" src="https://github.com/user-attachments/assets/4371b850-f264-4c55-99a2-414c994080db" />


#### 12. Post-CTS OpenROAD timing analysis.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```tcl
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/23-12_11-20/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/23-12_11-20/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/23-12_11-20/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Check syntax of 'report_checks' command
help report_checks

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```

Screenshots of commands run and timing report generated

<img width="1048" height="386" alt="image" src="https://github.com/user-attachments/assets/29ffef28-888d-4679-9540-fb010d8a00e7" />
<img width="1138" height="506" alt="image" src="https://github.com/user-attachments/assets/b72250bf-474c-432a-b5dd-bc16b6e8e4de" />

<img width="1052" height="507" alt="image" src="https://github.com/user-attachments/assets/3b3b94aa-68f8-4ed0-935b-d19a7338b91a" />

#### 13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis after changing `CTS_CLK_BUFFER_LIST`

```tcl
# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Removing 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Checking current value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Setting def as placement def
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/23-12_11-20/results/placement/picorv32a.placement.def

# Run CTS again
run_cts

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/23-12_11-20/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/23-12_11-20/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts1.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/23-12_11-20/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Report hold skew
report_clock_skew -hold

# Report setup skew
report_clock_skew -setup

# Exit to OpenLANE flow
exit

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Inserting 'sky130_fd_sc_hd__clkbuf_1' to first index of list
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)
```

Screenshots of commands run and timing report generated

<img width="1170" height="235" alt="image" src="https://github.com/user-attachments/assets/f6608912-81cb-41f7-8526-9dc1a636dbcb" />
<img width="889" height="532" alt="image" src="https://github.com/user-attachments/assets/38430cef-6224-49ed-a5ea-42ca05a8f88c" />
<img width="883" height="511" alt="image" src="https://github.com/user-attachments/assets/6258a479-ac62-4088-a9f6-740735110e6b" />
<img width="889" height="517" alt="image" src="https://github.com/user-attachments/assets/e7032c96-8c8c-47d9-8895-c03673e7f2d3" />
<img width="891" height="172" alt="image" src="https://github.com/user-attachments/assets/b53b6bbe-48c0-49a2-8d32-b04d52e9c409" />


</details>
