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

# Day2
