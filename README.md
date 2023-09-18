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

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/95b5d2db-66b5-4698-ab92-29b4daea1691)


Use command ``` docker ``` to enter the shell.

Use command ``` ./flow.tcl -interactive ``` to invoke Openlane 

Let us see the design files present by default in openlane 

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/a22a75fe-b549-40dc-b087-f8a9790c79c7)

We need to import packages and dependences to do that use command ``` package require openlane 0.9 ```.

We are using picorv32a for example. To prepare the design use command ``` prep -design picorv32a ```

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/c69045b4-e69e-4d83-aa05-603d51b8139b)

#### Synthesis 

Once design is prepared we can see runs executable in design directory.
![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/05e2d2c3-1914-4a27-9df7-ea1a50021e27)

Use ``` run_synthesis ```

![image](https://github.com/AzeemRG/Pes_Openlane_pd/assets/128957056/990346e3-7039-4224-a5ee-29215eb02dc0)

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

Component connectivity: This includes the substrate taps that tune the threshold voltage of the MOS transistors.
Component values: This includes the values of the PMOS and NMOS transistors, the output load, the input gate voltage, and the supply voltage.
Node names: These are required to define the SPICE netlist.
Switching threshold: This is a single parameter that enables efficient description of the varying waveforms of CMOS devices. It is defined at the intersection of Vin = Vout.
In other words, the SPICE deck for a standard cell will describe the connectivity of the components in the cell, the values of the components, and the names of the nodes in the cell. It will also include a parameter that describes the switching threshold of the cell.

Here is a rephrased version of the original passage:

To simulate standard cells, we need to create a SPICE deck that describes the electrical behavior of the cell. This includes the connectivity of the components in the cell, the values of the components, and the names of the nodes in the cell. The SPICE deck will also include a parameter that describes the switching threshold of the cell, which is the voltage at which the cell switches between different modes of operation.

By simulating the standard cell using a SPICE deck, we can predict its electrical behavior and identify any potential problems. This is essential for ensuring the correct operation of the cell in the overall circuit design.



























