# Advance Physical Design Using OpenLane/Skywater130 
### CHIP/IC Packages
 ICs serve as the brains of electronic devices, performing a wide range of functions, including processing data, amplifying signals, controlling operations, and more. 
 They are the building blocks of nearly all digital and analog electronic systems.

 Let us take Arduino for example
 ![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/7fbafe61-0727-46d0-98fe-aaa9e27f1b08)

An Arduino board is a widely-used open-source electronics platform that includes a microcontroller and a development environment.
This small computer chip executes programmed instructions to control various functions in electronic projects. 
Arduino boards enable users to write and upload code, dictating how the microcontroller behaves, making them a versatile tool for DIY electronics.

### Understanding key components and process of CHIP

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/ff7d98fb-b79a-4463-822a-d13fc43706a8)

Chip consist of Macros , GPIO pads/pins , Foundary IPs etc

  Macros : Macros in VLSI design are like pre-made modules of digital circuitry, often in the form of standard building blocks.
 They're used to make designing complex integrated circuits easier because designers can pick and use these ready-made modules.

  Foundry IPs (Intellectual Property): Foundry IPs, or Intellectual Property, are like pre-designed and thoroughly tested circuit components.
 Think of them as circuit components that you can purchase a license for. 
 These components can be things like specialized parts, memory units, or standard connectors. Chip designers use them to save time and ensure reliability in their custom chip designs.

 GPIOs:  Imagine a chip as a tiny computer. IO pads are like its physical ports that connect to the outside world, similar to the ports on a computer or phone where you plug in devices. 
  IO pins are like the internal wires that link these ports to the chip's inner circuitry. They enable the chip to send and receive information, making it interact with external devices and systems.

 ## ASIC Flow / RTL to GDS

 ![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/ec3389d0-6eef-432f-872f-98e6b26526ef)

 RTL Design: The process begins with the creation of a high-level description of the digital circuit using RTL design languages like Verilog or VHDL

 Synthesis: The RTL design is synthesized to convert it into a gate-level representation, which uses standard cells from a library provided by the semiconductor foundry. 
 This step optimizes the design for area, power, and timing.

 Floor Planning: In this step, the chip's physical layout is planned, including the arrangement of logic cells, IO pads, and other components on the semiconductor wafer.

 Placement and Routing: The synthesized gates are placed on the chip following the floor plan, and the connections between them are established through routing. 
 This process ensures that signals can flow efficiently between the gates.

 Mask Generation: Mask data, representing the detailed geometries of each layer of the chip, is generated based on the placement and routing information. 
 These masks guide the lithography process during manufacturing.

 Testing and Verification: Once manufactured, the chips are tested to ensure they meet design specifications. Any defective chips are usually marked and discarded.

 Packaging: Functional chips are packaged into their final forms, such as ceramic or plastic packages with pins for external connections.

 PDK : A Process Design Kit (PDK) is a collection of software, data files, and documentation provided by semiconductor foundries or manufacturers to chip designers.
 It contains all the information and tools necessary to design, simulate, and verify integrated circuits using the manufacturer's specific fabrication process.

 ## Introduction to OpenLane

 ![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/27289ae7-7a24-49ed-baf0-ffed0b8bdcc2)

 OpenLane is an open-source, automated digital ASIC (Application-Specific Integrated Circuit) design flow framework. 
 It plays a pivotal role in simplifying and streamlining the process of designing custom integrated circuits, making it more accessible to a wider range of engineers and designers.

 Here is the basic OpenLane Design Flow
 
RTL Design

Synthesis

Floor Planning

Placement and Routing

Clock Tree Synthesis

Power Planning

Physical Verification

GDSII Generation

Manufacturing

Testing

Packaging

Deployment


# Installation of OpenLane

Step1: Install any Virtual Machine(VM ware or Oracle Virtual Box)

Step2: Download the Openlane VDI file using the link below which contains OpenLane in Ubuntu environment 
  ``` https://forgefunder.com/~kunal/openlane.zip ```

Step3: Setup the VM with the VDI file by selecting it as a pre-built disc. We are ready to start...

Note: Allocate atleast 100 GB of disc space and 2gb memory 

# Course Content

<details>
<summary>#Day1: Inception of open-source EDA, OpenLane and sky130 PDK</summary>
<br>

#### Intoduction to skywater 130 pdk 

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/a126f74a-f65e-4718-831e-588defd6bbc1)

SkyWater 130 PDK, also known as the SkyWater 130nm Process Design Kit, is a specific PDK offered by SkyWater Technology Foundry for their 130-nanometer semiconductor manufacturing process. 
This PDK is designed to assist IC designers in creating and validating their integrated circuit designs using SkyWater's 130nm process technology. 

### Exploring OpenLane

Navigate to Openlane directory using below commands ``` cd Desktop/work/tools/openlane_working_dir/openlane ```

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/4169804b-fc21-4405-8f91-57c38b76962c)

Use command ``` docker ``` to enter the shell.

Use command ``` ./flow.tcl -interactive ``` to invoke Openlane 

Let us see the design files present by default in openlane 

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/a22a75fe-b549-40dc-b087-f8a9790c79c7)

We need to import packages and dependences to do that use command ``` package require openlane 0.9 ```.

We are using picorv32a for example. To prepare the design use command ``` prep -design picorv32a ```

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/0bec1cb2-9323-469e-bacc-440d75ac8111)


#### Synthesis 

Once design is prepared we can see runs executable in design directory.
![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/9d2d4323-abd0-49fe-89c5-2dccc1087ec2)


Use ``` run_synthesis ```

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/20a27075-959f-43fa-8d33-560fab52a298)


We can see final printing stats and get to know different factors.

One intresting factors can be seen is flop ratio , Flop ratio = 1613/14876 = 0.108 , in our its approx 11% which mean 11% of flops are getting utilized.


</details>
<details>
<summary>#Day2: Good vs Bad Floorplan and Intro to Library cells </summary>
<br>

## Chip Floorplan 

  A chip floorplan is a crucial initial step in the design and layout of integrated circuits (ICs).
  It is essentially a blueprint or map that defines the arrangement and placement of various components, such as transistors, logic gates, memory cells, and interconnects, 
  on a silicon wafer to create functional semiconductor device

  ![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/36d7b924-92da-466f-aa11-1cc1facebfec)

 #### Important Consideration during Floorplaning

1. Define Size and Location of Pre-Placed cells

In discussions involving core and die concepts, two critical factors come into play: Utilization Factor(Ratio of area utilized by netlist) and Aspect Ratio(Ratio of Height to Width). 
Pre-Placed Cells are specific blocks or cells like memories, clock gating cells, comparator, mux etc within an integrated circuit layout that are manually placed by the chip designer in predetermined locations
before the automated placement and routing tools are used to complete the rest of the design.

2. De-coupling capacitors

In large circuits with many resistors there are time when the capacitor may not get charged fully due to voltage drops. The solution for this is to use de- coupling capacitors. Decoupling capacitors store and 
discharge electrical energy quickly or decoupling capacitors absorb excess charge to filter out high- frequency noise and transient voltage fluctuations.

3. Power Planning
Power planning during the Floorplanning phase is essential to lower noise in digital circuits attributed to voltage droop and ground bounce.When a transition occurs on a net, charge associated with coupling 
capacitors may be dumped to ground. If there are not enough ground taps charge will accumulate at the tap and the ground line will act like a large resistor, raising the ground voltage and lowering our noise 
margin. To bypass this problem a robust PDN with many power strap taps are needed to lower the resistance associated with the PDN.

4. Pin Placement
Pin placement is an essential part of floorplanning to minimize buffering and improve power consumption and timing delays we use the HDL netlist to determine where a specific pin should be placed in the
circuit. We join the common pins and try to keep the connections as effecient as possible.

## Floorplan in OpenLane

 After completion of synthesis, this is the next step.
 Use command ```run_floorplan``` to start the floorplan.

 We can can that all the steps are done and floorplan is successful.
 ![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/fb4b1e75-0ac9-4f64-b7b7-b99edc9310d6)

 Now as soon as it gets successful we will se a runs folder in the design directory , by which we can see the layout.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/9da0bbeb-34b6-4480-8434-e71d89617f93)

Use command to see layout through magic tool
```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &```

Layout looks like this
![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/751e7a29-ee83-4906-90a0-e4fabe779728)

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/53772ec2-b1d6-4f08-b4ce-a8a36f24282a)

## Library Binding and Placement 

#### Netlist Binding , Initial Placement

Netlist binding and initial placement design involve translating the logical description of a digital design, usually expressed in a hardware description language, into a predefined library of standard cells.

Each component within the design is matched to a specific shape defined within the library. Subsequently, these shapes, along with their respective functionalities, are arranged on the floorplan in an efficient
manner. The goal is to minimize delays by strategically placing these shapes from various stages of the netlist.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/a7acefe4-40bd-4796-8d48-6175fbc7e761)

#### Placement Optimization

 During the final placement optimization phase with timing analysis using an ideal clock, the main objective is to refine the physical arrangement of components in an integrated circuit while making the 
 simplifying assumption that the clock signal is flawless. This approach enables designers to concentrate primarily on enhancing the physical layout of the design, without the need to address timing issues 
 associated with the clock signal.

 Use command ```run_placement``` to start placement execution.

 We can see the stats after completion

 ![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/77388f05-653b-459d-89b8-cd4f94801df2)
 
 This is how it looks 

 ![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/f5902e5d-3a9d-472c-b1a3-4fd5794294f8)

To see in magic tool

```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &```
 ![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/a6e5460b-79b4-4bbd-95ea-461d6322dce4)

 ## Cell Design and Standard Characterizations Flow 

  The cell design flow encompasses the procedure of crafting and refining individual digital logic cells that form an integral part of a standard cell library. 
  
  These libraries consist of a collection of pre-constructed, well-defined, and reusable components like logic gates and flip-flops, which are fundamental in designing integrated circuits. 
  
  Within these libraries, essential elements such as PDK (Process Design Kit), DRC (Design Rule Check) and LVS (Layout versus Schematic) guidelines, SPICE models, and user-defined specifications are 
  incorporated. 
  
  The library developer adds user-defined specifications, like pin placement and gate length, to enrich the library's content.

 Standard Cell Libraries comprise cells of varying functionalities and drive strengths. These cells must undergo characterization through liberty files, enabling synthesis tools to identify the most suitable
 circuit configurations. Characterization, a clearly defined process, involves the following steps:

Associating a model file with CMOS properties.

Defining the process corner(s) for the target cell's characterization.

Setting thresholds for cell delay and slew, expressed as percentages.

Defining timing and power tables.

Incorporating the parasitic-extracted netlist.

Applying input signals or stimuli.

Issuing the requisite simulation commands.

#### Timing Threshold 

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/cdc1222e-a145-4173-8f22-b2072b67e412)

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/f84db5e5-f519-4d8f-aae4-5a9533c9a577)

slew_low_rise_thr - 20% from bottom power supply when the signal is rising

slew_high_rise_thr - 20% from top power supply when the signal is rising

slew_low_fall_thr - 20% from bottom power supply when the signal is falling

slew_high_fall_thr - 20% from top power supply when the signal is falling

in_rise_thr - 50% point on the rising edge of input

in_fall_thr - 50% point on the falling edge of input

out_rise_thr - 50% point on the rising edge of ouput

out_fall_thr - 50% point on the falling edge of ouput

Based on the above parameters these are the important factors 

propogation delay  - time(out_thr) - time(in_thr)

Transition time - time(slew_high_rise_thr) - time(slew_low_rise_thr)


</details>
<details>
<summary>#Day3: Design library cell using Magic Layout and ngspice characterization </summary>
<br>

## SPICE deck creation for CMOS inverter


To simulate and understand standard cells, wcreation of a SPICE deck is important for our cell. The SPICE deck will contain the following information:

- Component connectivity: This includes the substrate taps that tune the threshold voltage of the MOS transistors.
- Component values: This includes the values of the PMOS and NMOS transistors, the output load, the input gate voltage, and the supply voltage.
- Node names: These are required to define the SPICE netlist.
- Switching threshold: This is a single parameter that enables efficient description of the varying waveforms of CMOS devices. It is defined at the intersection of Vin = Vout.
- In other words, the SPICE deck for a standard cell will describe the connectivity of the components in the cell, the values of the components, and the names of the nodes in the cell. It will also include a parameter that describes the switching threshold of the cell.

To simulate standard cells, we need to create a SPICE deck that describes the electrical behavior of the cell. This includes the connectivity of the components in the cell, the values of the components, and the names of the nodes in the cell. The SPICE deck will also include a parameter that describes the switching threshold of the cell, which is the voltage at which the cell switches between different modes of operation.

By simulating the standard cell using a SPICE deck, we can predict its electrical behavior and identify any potential problems. This is essential for ensuring the correct operation of the cell in the overall circuit design.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/1e42f136-954f-4d8d-8804-661dc169788a)

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/abcb0c80-e812-4f1f-9a5f-4c013b3883ea)

## CMOS fabrication process

- Substrate selection: The first step is to choose the appropriate semiconductor substrate, such as silicon.
- Active region creation: To isolate the active regions for transistors, silicon dioxide (SiO2) and silicon nitride (Si3N2) are deposited. Pockets are then created using photoresist and lithography.
- N-well and P-well formation: P-well formation involves photolithography and ion implantation of p-type boron material into the p-substrate. N-well is formed similarly with n-type phosphorus material. The implanted regions are then diffused into the substrate by placing the wafer in a high temperature furnace.
- Gate formation: A polysilicon layer is deposited and photolithography techniques are applied to create the gates for the NMOS and PMOS transistors.
- Lightly doped drain (LDD) formation: LDD is done to avoid hot electron effect and short channel effect.
- Source and drain formation: Thin oxide layers are added to avoid channel effects during ion implantation. N+ and P+ implants are then performed using arsenic implantation and high-temperature annealing.
- Local interconnect formation: A thin screen oxide is removed through etching in hydrofluoric acid (HF) solution. Titanium is then deposited through sputtering. Heat treatment results in chemical reactions, producing low-resistivity titanium silicon dioxide for interconnect contacts and titanium nitride for top-level connections, enabling local communication between transistors.
- Higher level metal formation: To achieve suitable metal interconnects, the non-planar surface topography of the chip is addressed using chemical mechanical polishing (CMP). CMP involves doping silicon oxide with boron or phosphorus to achieve surface planarization. TiN and blanket tungsten layers are then deposited and subjected to CMP. An aluminum (Al) layer is then added and subjected to photolithography and CMP.
- Dielectric layer addition: Finally, a dielectric layer, typically Si3N4, is applied to safeguard the chip.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/07ff261b-5881-438d-9440-5003c60b8894)

## LAB Work

Installation
```git clone https://github.com/nickson-jose/vsdstdcelldesign.git```

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/744abfaa-3449-40f3-b398-fe0edc9c76d5)

To see the layout of CMOS invertor use command
```magic -T sky130A.tech sky130_inv.mag &```

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/da0fb344-f42a-4efb-9906-d6b1e892fe8c)

##### Checking DRC errors

To check drc we to press DRC update and it show the errors in tkon window.
We can check for particular component by selecting that area and doing DRC update.
![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/a909d115-5584-42d4-b21f-b23c8d555d25)


### Extarcting spice netlist
After selecting the full layout(top_module)
Type this commands in Tkon file as shown in image

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/57e16b30-321e-4757-9f02-8215148ab327)

U will see the .ext and .spice file

Here is the .spice file
![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/197138f4-8341-49dc-8e90-1464e2acf999)

Modified spice file
![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/fd028537-b838-466f-8c90-36df725ad8fe)


Use command ```ngspice sky130_inv.spice``` to run the netlist.
Use command to plot the waveform ```plot y vs time a```.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/f7fb4ca7-d01f-49b9-ab75-62bc4c6e9b20)


</details>
<details>
<summary>#Day4: Pre-layout timing analysis and importance of good clock tree</summary>
<br>

## Timing Modeling

Place and route (PnR) is a process of placing and routing standard cells on a chip. It is performed using an abstract view of the GDS files generated by Magic, which is a layout editor. The PnR tool will use the abstract view information, formally defined as LEF information, to perform interconnect routing.

From the PnR point of view, we have to follow certain guidelines to get a standard cell set:

- Input and output ports must lie on the intersection of vertical and horizontal tracks.
- Width of the standard cell should be an odd multiple of the track pitch.
- Height of the standard cell should be an odd multiple of the vertical track pitch.

###### LEF Extraction

- Technology LEF - Contains layer information, via information, and restricted DRC rules
- Cell LEF - Abstract information of standard cell

To see track info used in routing use command navigate to ``` cd Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130fd_sc_hd ``` 

- 1st numeric column indicates the offset and 2nd indicates the pitch along provided direction

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/9acdba10-6a73-49b9-a11f-4ebb2fe1adbd)

##### Setting user defined grid values

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/93148a4d-bcb2-46e2-8694-2a8e53648176)

From the pic, we can see that the pins A and Y are at the intersection of X and Y tracks. So the first condition is met. The next requirement is that the width of the cell should be the odd multiple of xpitch 
which is '0.46' as seen in the tracks.info file.

### Magic Layout to Standard Cell LEF

To generate the LEF file for a perfect layout:

Save the modified layout with the new grid.
In the console, type:
```save sky130_vsdinv.mag```

This saves the modified layout in the current working directory.

Open the file and extract the LEF.
Open the file using the following command:

```magic -T sky130A.tch sky130_vsdinv.mag```

In the console that opens, type the following command:

```lef write```

This will generate a LEF file.

It will look like this

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/cc76d033-31af-4d1b-9e43-4bade4fc2806)

- Now we copy the lef file in picorv32a

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/2c664561-c544-4d71-bd67-f8f4f2cc9142)


Now lets modify the config file

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/dc85a234-7644-4270-81ef-c28de6842964)


## Now lets follow the design flow in OPENLANE

Synthesis

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/b3fa58c1-3f56-41c1-99fd-f49174b009a0)

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/635cf3d9-1e5d-429e-839c-6168fcdd64d6)

Slack Violations and Improvement


Slack violations are timing violations in digital designs. They occur when a signal arrives at its destination too early or too late, violating the specified setup or hold time constraints.

When referring to pre-clock tree synthesis STA analysis, we are mainly concerned with setup timing in regards to a launch clock. STA will report problems such as worst negative slack (WNS) and total negative 
slack (TNS). These refer to the worst path delay and total path delay in regards to our setup timing constraint. Fixing slack violations can be debugged through performing STA analysis with OpenSTA, which is 
integrated in the OpenLANE tool. The desired value of slack is above or equal to 0.

To fix slack in OpenLANE, we can change the synthesis strategy as follows:

- Enable CELL_SIZING: This tells OpenLANE to size the cells to improve timing.
- Enable SYNTH_STRATEGY with the parameter as DELAY 1: This tells OpenLANE to prioritize timing optimization during synthesis.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/9fde1bbc-634c-48af-9f91-79c435c77c2a)

The slack has reduced a lot but still didnt meet the requirement. 
The sdc file used is ```my_base.sdc``` defined in pre_sta.conf using the command ```sta pre_sta.conf```

###### Perform manual cell replacement on our WNS path with the OpenSTA tool

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/f7d4d37e-96a8-45c0-9aae-a5dffcb016f3)

Placement

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/e9e9a713-a244-4948-acf3-1771cda5a8c7)

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/9bbd9a41-473c-4570-8f10-c6bad3d9f1ab)



## Delay Tables

Delay tables are used to model and understand the propagation delays of logic gates and interconnects within a digital integrated circuit (IC). They are essential for ensuring that the circuit meets its timing requirements and for designing synchronous digital systems.

Purpose of delay tables:

- Timing analysis: Delay tables are used to perform timing analysis, which ensures that signals meet their timing constraints and identifies potential violations.
- Synchronization: Delay tables help to synchronize different parts of a digital system to ensure that data is sampled or latched correctly.
- Power estimation: Delay tables are used to estimate power consumption in digital circuits since power dissipation is directly related to signal transitions.
- Components of delay tables:

- Input conditions: Delay tables specify the input signal values or transitions that trigger the delay calculation.
- Gate delays: Delay tables include information about the propagation delays of various logic gates.
- Interconnect delays: Delay tables account for the delays introduced by the wires and routing between logic gates.
- Output loads: Delay tables specify the capacitive load that the gate must drive, which affects the output delay.

## Timing Analysis and more with OpenSTA

- Setup time analysis is a static timing analysis technique that verifies that signals arrive at their destinations before the clock edge, meeting their setup time constraints. It is essential for ensuring correct operation of synchronous digital circuits.
- Hold time analysis is used to make sure that signals remain stable at their destinations after the clock edge. This is important for ensuring that the circuit works correctly.
- Clock jitter is the variation in the timing of a clock signal. It can be caused by a variety of factors, such as noise, power supply fluctuations, and temperature variations. Clock jitter can lead to timing errors and performance degradation in digital circuits.
- Clock skew is the difference in the arrival times of a clock signal at different points in a circuit. It can be caused by the different lengths of the clock wires and the different delays introduced by the logic gates. Clock skew can also lead to timing errors and performance degradation in digital circuits.

## Clock Tree Synthesis

Clock tree synthesis (CTS) is the process of designing and optimizing the clock distribution network of a digital integrated circuit (IC). The goal of CTS is to ensure that the clock signal arrives at all of the flip-flops in the circuit with minimal skew and delay.
- Read the design netlist, standard cell library, and clock constraints.
- Generate different clock tree topologies.
- Perform clock buffering and clock gating.
- Verify the clock tree design.
- Generate clock tree reports.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/e4a98836-a497-44d6-9b20-ce5970394a0d)


After placement next step is CTS , use command ```run_cts``` to run the flow

### STA-Analysis using OpenSTA

Summary of the key steps in the post-CTS STA analysis flow:

- Generate the post-CTS netlist and SDF file.
- Invoke OpenSTA and load the library file.
- Set the timing constraints.
- Perform the STA analysis.
- Review the STA results.
- Post-CTS STA analysis is an important step in the physical design flow. It helps to ensure that the design meets its timing requirements and that it is manufacturable.

Here are some additional tips for post-CTS STA analysis:

- Make sure to use the most up-to-date library file.
- Use realistic timing constraints.
- Review the STA results carefully and fix any timing violations.
- Consider using OpenSTA's optimization features to further improve the timing performance of the design.

```
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/18-09_06-26/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/18-09_06-26/results/cts/picorv32a.cts.def
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/16-09_19-58/results/synthesis/picorv32a.synthesis_cts.v
read_liberty -max $::env(LIB_SLOWEST)
read_liberty -max $::env(LIB_FASTEST)
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/a5cd0210-b007-4fd7-87fd-7a89dc5127a4)

Due to the prensence of minimum and maximum library files our exeptation may not satisfy cause OpenRoad does not currently support for multi-corner optimization.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/641e1b93-f044-4663-bf7b-e4c28b7da2ff)

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/1534224c-65dc-4c09-a6ff-a12bd490cb04)

Stats : This shows Clock Reconvergence Pessimism Removal (CRPR) , Latency and skew
![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/ce85a948-e5f8-474b-ac27-ad39641534b6)


</details>
<details>
<summary>#Day5: Final Step RTLtoGDS using OpenSTA </summary>
<br>

## PDN and Routing

Power Distribution Network (PDN)

- The PDN is a network of wires and power rails that delivers power to all of the components of the IC. The PDN must be designed to provide adequate power to all of the components, while also minimizing voltage drop and noise.
- OpenLANE provides a variety of features for designing and optimizing the PDN. For example, OpenLANE can automatically generate the PDN grid and place the power rails. OpenLANE can also calculate the voltage drop and noise in the PDN, and identify any potential problems.

Routing

- Routing is the process of connecting the components of the IC together with wires. The routing must be done according to a variety of constraints, such as the physical dimensions of the IC, the timing requirements of the design, and the manufacturing rules.
- OpenLANE provides a variety of features for routing the design. For example, OpenLANE can automatically route the wires according to the specified constraints. OpenLANE can also generate a variety of routing reports, such as congestion reports and timing reports.
-Once the PDN and routing have been completed, it is important to verify the design to ensure that it meets all of the requirements.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/9eb91035-dcd4-4a5b-b3cd-2c3a39625ac0)

To start the flow use ``` run_pdn```

for routing use ```run_routing``` 

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/f9efd406-5333-4911-8d9f-283eff81bd3a)

Ending step of this journey is SPEF Extarction.

SPEF extraction in OpenLANE is the process of generating a SPEF file from a post-CTS design. The SPEF file contains information about the parasitic resistances, capacitances, and inductances of the nets in the design. This information is used by the placement and routing tools to ensure that the design meets its timing and power requirements.

- Make sure to use the most up-to-date library file.
- Use realistic extraction parameters.
- Review the SPEF file carefully and fix any errors.
- Consider using OpenLANE's SPEF optimization features to further improve the timing and power performance of the design.

Unfortunately SPEF extractor is not present in OpenLane.

These are some efficiant rounting called Triton Route 

TritonRoute is a detailed router that is part of the OpenROAD project. It is used to route the wires in a digital integrated circuit (IC) according to the specified constraints. OpenSTA is a static timing analysis (STA) tool that is also part of the OpenROAD project. It is used to analyze the timing performance of a digital IC design.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/c2bb0ffe-b584-4669-9b8f-e218282391d8)

In our process we have use Triton Route strategy as zero. Which means there will be some violatins , but using triton Route Strategy will be time consuming and heavy.

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/b5a7fe9a-8ca9-4100-9d2a-21ef69c0cc18)

- Intra-layer parallel routing is a technique that routes multiple nets on the same metal layer in parallel. This can be done using a variety of different algorithms, such as maze routing and channel routing. Intra-layer parallel routing can help to improve routing congestion and reduce routing time.

- Inter-layer sequential panel routing is a technique that routes nets on different metal layers in sequence. This technique is typically used for complex designs with high routing congestion. Inter-layer sequential panel routing can help to improve routing quality and reduce routing violations.

Thank you.. 

END of the flow........

</details>

## References:

https://openlane.readthedocs.io/en/latest/

This is very good documentation that helps to debug basic errors.


































































