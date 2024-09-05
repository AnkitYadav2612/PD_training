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







