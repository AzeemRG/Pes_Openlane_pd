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


## Installation of OpenLane

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


<details>
<summary>#Day2: Good vs Bad Floorplan and Intro to Library cells </summary>
<br>


















