# PD_training
Git Hub link : https://github.com/efabless/openlane

Youtube video : https://www.youtube.com/watch?v=EczW2IWdnOM&list=PLUg3wIOWD8yoZCg9XpFSgEgljx6MSdm9L&index=1

OpenLane Flow:

![image](https://github.com/user-attachments/assets/54a4d783-2a63-4818-85d3-17ae6176da4b)

# Day1
Items done on day1:

1) Went through flow.tcl, tech lef and other inputs
![image](https://github.com/user-attachments/assets/17baac1a-ea64-4595-b000-30bc62106370)

2) Opened OpenLane, went through the contents of designs dir (config.tcl, sky130A_sky130_fd_sc_hd_config.tcl) and setup the design data (prep -design picorv32a)
![image](https://github.com/user-attachments/assets/cfaa2599-55e4-45bb-a1d8-6454474604dc)

![image](https://github.com/user-attachments/assets/9c5f9221-e681-4c0c-8de9-eded7a6d5bd8)

![image](https://github.com/user-attachments/assets/6959c36d-3cc9-46d9-afce-b540d9993516)

3) Reviewed the contents of the generated runs dir inside picorv32a design dir (merged.lef inside tmp dir that has design+tech lef, config.tcl which has all the settings used on top of the ones provided in design dir)
![image](https://github.com/user-attachments/assets/1d115738-6579-4b40-a193-75dc496d53d3)

4) Ran synthesis (run_synthesis)
![image](https://github.com/user-attachments/assets/f5d6ac12-b52e-4196-8f60-892191a834ed)

5) Reviewed the above Git Hub Link and video while synthesis progressed
6) After synthesis completed successfully, opened the results dir and reviewed picorv32a.syntheseis.v file.
 ![image](https://github.com/user-attachments/assets/fd8628f5-ab2f-41ee-a4e7-7c6a2f15e9e4)

7) Also reviewed reports (1-yosys_4.stat.rpt from which we found the flop ratio, 2-opensta.timing.rpt,i.e, the timing file)
![image](https://github.com/user-attachments/assets/9a57bc54-97ed-41c6-9518-7d1093425b2e)

# Flop ratio: number of d flops/ total no of cells = 1613/14876 = 0.0108429 = 10.8429 %
![image](https://github.com/user-attachments/assets/2fff59e5-6d97-495d-85fa-6496ee1f7691)


# Day2

# Overview of Physical Design flow

The physical design flow consists of several key steps, with each step optimizing different aspects of the chip's performance, power, and area (PPA). Here is an overview of the major steps involved in the physical design flow:

# 1. Design Import and Floorplanning
Design Import: The process starts by importing the logical netlist, technology libraries, and design constraints (e.g., timing constraints, area constraints) into the physical design tool.
Floorplanning: This step involves defining the chip's layout, including the placement of macros (large blocks like memory or IPs), I/O pads, and the core area. The floorplan sets the foundation for the entire design, determining how different modules will be placed and interconnected.
Power Planning: Power distribution networks (PDN) are designed to ensure stable power delivery to all parts of the chip. This includes creating power rings and straps across the floorplan.
Pin Placement: I/O pins are placed on the chip's periphery to connect the internal logic to the external world.
# 2. Placement
Standard Cell Placement: After the floorplanning, the standard cells (logic gates, flip-flops, etc.) are placed in the core area based on the logical netlist and the floorplan. The placement engine optimizes cell locations to minimize wirelength, power consumption, and meet timing constraints.
Optimization: After placement, the design undergoes various optimizations, including timing (setup and hold), signal integrity, and power optimizations.
# 3. Clock Tree Synthesis (CTS)
Clock Tree Design: Clock Tree Synthesis involves creating a clock distribution network that ensures that the clock signal reaches all sequential elements (e.g., flip-flops) with minimal skew and latency.
Buffer Insertion: Buffers are added into the clock tree to drive the large fan-out and ensure that the clock signal propagates uniformly across the design.
Skew Management: The clock tree is optimized to minimize clock skew (the difference in clock arrival times across different parts of the chip) and clock insertion delay.
# 4. Routing
Global Routing: The first step in routing is global routing, which determines the general paths that the wires will take across the chip without assigning specific metal layers or routes.
Detailed Routing: In this step, the exact routes of the wires are determined, including the specific metal layers and vias (connections between layers) to be used. The goal is to ensure that all signal nets are routed without violations such as shorts or opens.
Design Rule Check (DRC): After routing, a check is performed to ensure that the design adheres to the technology-specific design rules, such as spacing, width, and density requirements for metal layers.
# 5. Sign-Off Verification
Timing Analysis (STA): Static Timing Analysis is performed to ensure that the design meets all timing constraints, including setup and hold times. Timing violations are identified and fixed in this step.
Power Analysis: Power consumption analysis is done to ensure that the chip meets the required power specifications. This includes dynamic power (due to switching activity) and static power (due to leakage currents).
Signal Integrity (SI) Analysis: Signal integrity analysis ensures that issues like crosstalk and noise do not affect the design's functionality. If necessary, design adjustments are made to mitigate these issues.
Physical Verification: This includes Design Rule Checking (DRC), Layout vs. Schematic (LVS) checks, and Antenna Rule Checking (ARC) to ensure that the physical layout is correct and manufacturable.




# Day3
1) Change the floorplan variable on the fly making it 1 to 2 and viewing the results:

![image](https://github.com/user-attachments/assets/ac1e0246-fcf3-4831-86ee-efb9fbfe5448)

2) Git clone the vsdstdcelldesign
![image](https://github.com/user-attachments/assets/31fcfba4-bd51-415b-8a5d-002efd8336bb)

3) Opening the inverter layout in Magic 
![image](https://github.com/user-attachments/assets/d9646d75-9d67-412c-90c2-7cb370485650)

![image](https://github.com/user-attachments/assets/aa64b450-ebf4-4222-a76c-3b4a792f474b)

4) Selecting the complete connection in Magic by pressing 's' button three times:
![image](https://github.com/user-attachments/assets/a9238f83-fa0c-4eea-9ed5-c426096cc521)

5) Command to extract all parametrs of this inverter using Magic: 'extract all'
sky130_inv.txt file:

![image](https://github.com/user-attachments/assets/9b8cb3d6-03a6-4d85-8e22-0776265be19c)

6) Command to extract spice modal of this inverter:

'ext2spice' is the command
![image](https://github.com/user-attachments/assets/aebb8c7b-3ecf-4470-b4bb-8689b0f23c72)
![image](https://github.com/user-attachments/assets/789bfcd3-ee17-4f74-8c9b-93b743623da7)

7) Transient analysis of inverter:
Changes in spice file

![image](https://github.com/user-attachments/assets/38029685-c909-45fa-a1b3-3e818a6bfd2b)

![image](https://github.com/user-attachments/assets/34938e48-d113-443d-8391-150d7485cc65)

![image](https://github.com/user-attachments/assets/beecdb39-3f6d-4dba-a850-fccb187f439d)

# Rise transition time calculation: 80% of 3.3V- 20% of 3.3V of output waveform on rising edge = 2.24557e-09 - 2.18201e-09 = 0.06356e-09
# Fall transition time calculation: 20% of 3.3V - 80% of 3.3V of output waveform on falling edge= 4.09476e-09 - 4.04216e-09 = 0.04216e-09

# Cell delay calculation
![image](https://github.com/user-attachments/assets/b52b0e9c-e990-4895-8509-4e44e5e94adf)

# Cell rise delay: 50% of output waveform on rising edge - 50% of input waveform on rising edge = 2.21103e-09 - 2.14926e-09 = 0.06177e-09

# Cell fall delay: 50% of output waveform on falling edge - 50% of input waveform on falling edge = 4.07721e-09 - 4.05e-09 = 0.02721

8) SkyWater SKY130 PDK’s documentation

![image](https://github.com/user-attachments/assets/c8f6e4ca-2952-4cbf-96ca-d6fd014380ae)

9) Visualize net.mag files in Magic
Command to invoke Magic: magic -d XR

![image](https://github.com/user-attachments/assets/d370080a-744a-42a5-832a-99c12a4a9893)

![image](https://github.com/user-attachments/assets/228eeca1-cd3e-4d31-a9c5-7439399e8f80)

10) Check DRC voilations:

![image](https://github.com/user-attachments/assets/1a373a97-f960-4aa8-a526-4de92605fdb1)

Select a box and then type drc why in other panel to check the reason of that drc

![image](https://github.com/user-attachments/assets/c4ed7fb4-e9b4-4e91-a974-a0b93d6508e9)

Adding a box and clicking on metal3 with middle mouse button or hover over the metal3 and press p button to get the rectangle shape added in metal3. Both methods tried, top metal3 box with middle button in mouse and bottom one with pressing p key.
![image](https://github.com/user-attachments/assets/419caab4-e66b-415d-bdb8-caf8e4ac0ebf)

![image](https://github.com/user-attachments/assets/0751cb25-ebfa-4d0e-877c-fde7ea9dd581)

12) Closed and opened the magic again and checked the drc again. Checked the via issue drc but via is not seen.
![image](https://github.com/user-attachments/assets/8ce69b3b-218d-41d9-b931-f13e0214a4c6)

13) Error in the distance between the metal is identified as shown here:
![image](https://github.com/user-attachments/assets/3b737c56-0618-4ab9-bd56-a903eb4724d8)

14) The command “feed clear” or “feedback clear” clears the earlier selections
![image](https://github.com/user-attachments/assets/731e77bf-c535-4654-8044-10cb2bd31fe5)
![image](https://github.com/user-attachments/assets/6e982d06-23e8-44c0-b0f1-6b2125b9d5ee)

15) Lab exercise to implement poly resistor spacing to diff and tap
![image](https://github.com/user-attachments/assets/91e113cc-81f9-4f56-9aa4-7c40d2881ee0)

Move the curser before pressing c to make sure that they are placed at that location.

![image](https://github.com/user-attachments/assets/523398db-74a7-4da1-a1df-208863dbdbec)

Added a new layer by clicking mouse center

![image](https://github.com/user-attachments/assets/fed462f8-c411-4799-8b11-18a328b97961)

Total drc gone to 46 now, also drc why helps in identifying the drc violations,

![image](https://github.com/user-attachments/assets/155fde6a-a956-474f-94c0-b79675c342d7)

16) DRC error as geometrical construct

![image](https://github.com/user-attachments/assets/60d36873-1c43-4509-a14a-fc2974da5866)

Correcting the error by changing sky130.tech file

![image](https://github.com/user-attachments/assets/c7d934db-0fcd-4bc8-869d-109b52c74003)
![image](https://github.com/user-attachments/assets/06cf63f9-1e2e-4b64-a306-568c2b89d6f6)

![image](https://github.com/user-attachments/assets/c6ffe5f3-7840-4b6d-aae0-32acc8d385e3)
![image](https://github.com/user-attachments/assets/de56f562-4a5d-4e90-bc58-1550cb102e7f)

# Day4

1) Checking tracks info:
![image](https://github.com/user-attachments/assets/67471c35-7340-4d0d-9115-760e8a1b058a)

2) Enabling the grid info:

![image](https://github.com/user-attachments/assets/e08b2a22-2aed-4f9d-a599-5f312a45db6c)

![image](https://github.com/user-attachments/assets/be1b391c-9b3a-421c-b98d-5613c4247368)

3) Converting Magic layout to std cell lef

first defining port definition and type:

![image](https://github.com/user-attachments/assets/175b6f54-bead-4e38-9f44-44ffa778b5f9)

Saving the mag file to a custom/user defined name using 'save' command:
![image](https://github.com/user-attachments/assets/7f0b677a-acf7-4347-a46c-a906156771a7)

Extracing a lef file:

![image](https://github.com/user-attachments/assets/8a09dca9-d88c-4a2d-8a37-49395f9b9a90)
![image](https://github.com/user-attachments/assets/f9b8ef4d-85cc-4f9b-9411-4fa99fe1c440)
![image](https://github.com/user-attachments/assets/d13eab23-c99a-41b5-ab97-3c98ea0c17da)

Running the OpenLane flow using the defined custom inverter:
a) First copy the generated lef, libs in ...../designs/picorv32a/src/ directory
b) modify the config.tcl

![image](https://github.com/user-attachments/assets/d96d13e3-719a-4dcf-ba2f-4497fdcb3ab7)

Fixing slack/timing violations:
![image](https://github.com/user-attachments/assets/3f41f445-5c8d-491a-a8fc-9c038db04a6d)

Checking the variables values and setting them to 1:

![image](https://github.com/user-attachments/assets/2dfe68dd-8cf4-47d2-8cf6-a41ba91f8d34)

![image](https://github.com/user-attachments/assets/894d231a-a970-4bb3-a926-e06899e53546)

After setting default "SYNTH_STRATEGY" to "AREA 1" |"DELAY 1" results are:

![image](https://github.com/user-attachments/assets/377aa6e6-7845-4ab2-aee2-2c3173b51ed9)
![image](https://github.com/user-attachments/assets/9d4323d3-a23b-4c56-a92d-b674b8b3663b)

Visualizing our custom cell 'sky130_vsdinv' after placement:

![image](https://github.com/user-attachments/assets/a87f99c8-ad4d-410f-ae44-9ac0d643712b)

Slack violation fixed pre CTS:
![image](https://github.com/user-attachments/assets/a23b73de-53c1-4ece-856a-fff9a67bd2a9)

# CTS
run_cts command for running CTS:

![image](https://github.com/user-attachments/assets/9f449653-2700-4e75-9c03-ad74a7e5cd88)

Checking timing again after real clocks in openroad:
command used: set_propagated_clock [all_clocks]

Slack is positive

![image](https://github.com/user-attachments/assets/57176e7c-dbb9-4152-a2af-514d44cd0bd6)

# Routing

"run_routing" command is used for routing












