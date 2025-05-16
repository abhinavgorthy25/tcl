# TCL Scripting for VLSI Design and Synthesis: From Fundamentals to Advanced Techniques
Tool Command Language (TCL) is a powerful scripting language widely used in the field of VLSI for automating EDA tool flows, particularly in synthesis, placement, routing, timing analysis, and verification. 

The primary goal of this repository  is to develop an automation tool that takes a CSV input files containing paths and Standard Design Constraints (SDC) and generates a corresponding TCL script. This script will then be used for automating digital synthesis using Yosys, an open-source RTL synthesis tool for Verilog designs.

## Module 1: Introduction and VSDSYNTH Toolbox Usage
### TASKS:
- Create command (for eg. vsdsynth) and pass csv from UNIX shell to TCL script
- Convert all inputs to format [1] & SDC format, and pass to synthesis tool 'Yosys'
- Convert format [1] & SDC to format [2] and pass to timing tool 'Opentimer'
- Generate output report
### SUB TASKS INVOLVED IN TASK 2 and 3: 
- Create variables
- Check if directories and files mentioned in .csv, exists or not
- Read "Constraints File" for above .csv and convert to SDC format
- Read all files in "Netlist Directory"
- Create main synthesis script in format|2]
- Pass this script to Yosys 

Instead of VSDSYNTH, I’ve created a name called “TCL_TOOL,” and I’ve also created an ASCII logo for it.
![Screenshot 2025-05-07 at 10 21 46 PM](https://github.com/user-attachments/assets/d9b67388-e6c5-4bf7-8fb1-5c58fe04f88a)

The following is used in the tcl_tool.tcl indicating that it is a UNIX Script. Make sure the files of tcl_tool (UNIX COMMANDS) and tcl_tool.tcl files are in the working directory and make sure the paths are proper. 


```
#!/bin/tcsh -f
```
In this scenario, the user does not enter the CSV file (no arguments) and executes only ./tcl_tool and -help as arguments.
![Screenshot 2025-05-07 at 10 29 17 PM](https://github.com/user-attachments/assets/a6ef4bb1-6c53-40df-8d7b-9b0ca174c72b)
if you face an error while executing ./tcl_tool , use the following command that provides necessary permissions:
```
chmod -R 777 tcl_tool
```
This is the case when user enters wrong csv file name:
![Screenshot 2025-05-07 at 10 30 38 PM](https://github.com/user-attachments/assets/1acd147c-d104-4180-8bc6-e5abd9e2a4e3)

## Module 2: Variable Creation and Processing Constraints from CSV: 

- Auto creation of variable: 
![image](https://github.com/user-attachments/assets/f5123ed4-78ad-437b-9f89-4694a68e6740)
- Variables successfully created in the tcl_tool.tcl script and the directories as set. 
![Created Variables](https://github.com/user-attachments/assets/631502ca-3844-4b0c-be64-6b73072c3a04)
- Checking if the directories exist or not:
![Checking id the directories exist or not](https://github.com/user-attachments/assets/6558eca3-d810-47fd-94f2-7be18f7acbac)
- Error if the file is in the wrong directory:
![Error if not right directory](https://github.com/user-attachments/assets/065733c9-6906-402a-895f-28c4cd77e858)
The process of converting csv file to the matrix and count the number of rows and columns:
![image](https://github.com/user-attachments/assets/73664e17-a80d-412c-a4fe-b09bb6ffa968)

## Module 3: Standard Design Constraints (SDC Creation):
Standard Design Constraints is a Tcl-based format used to define timing, clock, and design constraints for synthesis and  pre - static timing analysis (STA).
Here is a basic template of the SDC:
```
create_clock
set_input_delay
set_output_delay
set_driving_cell
set_load
set_false_path
set_multicycle_path
set_clock_uncertainty
set_clock_latency
```
### Algorithm used: 
From the constarints matrix, a rectangular search spacer is created and then the names along the values are grepped (searched) and then extracted to the SDC format. 
![image](https://github.com/user-attachments/assets/1b060b3d-13de-4ac0-adac-dbb0f3b24432)

- Clock creation: 
![Screenshot 2025-05-08 at 9 49 49 PM](https://github.com/user-attachments/assets/46f2c29b-f50d-4bde-9fb4-a35c32b1c35f)
![Screenshot 2025-05-08 at 9 50 13 PM](https://github.com/user-attachments/assets/37b8d792-7c17-4b8f-a28f-8621f70a41c9)
- Inputs: 
 Reading:
![Screenshot 2025-05-08 at 10 16 43 PM](https://github.com/user-attachments/assets/c75e983c-fde0-4efd-9472-8beee4fd6189)
![Screenshot 2025-05-08 at 10 19 18 PM](https://github.com/user-attachments/assets/255c5844-1eee-4cc8-8909-5c6e26f68a47)
After Uniquifying and sorting:
![Screenshot 2025-05-08 at 10 22 01 PM](https://github.com/user-attachments/assets/bed7e8ac-beaf-487d-af78-79f3e840d21e)
After Joining:
![Screenshot 2025-05-08 at 10 24 21 PM](https://github.com/user-attachments/assets/f3fff352-03d8-42bc-a882-e28e4f3905bc)
Print statements (puts) used:
![Screenshot 2025-05-08 at 10 25 40 PM](https://github.com/user-attachments/assets/6f21cd99-699d-4047-ba62-81534bb9fe62)

Categorizing as Single Bit or Multi Bit: 
![Screenshot 2025-05-08 at 10 28 45 PM](https://github.com/user-attachments/assets/55b20e1f-c38c-4025-a409-9c565b52db4d)
![Screenshot 2025-05-08 at 10 31 31 PM](https://github.com/user-attachments/assets/2dc56add-f11b-4051-9019-095ff52fb261)

Since we have all the information in the sdc.csv file, it is converted to a SDC script that will be useful for the further process like synthesis:
- Screenshot of SDC creation in Linux:
![SDC Constarints Created](https://github.com/user-attachments/assets/6f4c5b00-0318-40cb-8d83-b569cb500f0b)
- Sample Code snippet of SDC Creation:
![Code snippet of Generated SDC](https://github.com/user-attachments/assets/8058baf0-99ca-4003-b529-d85401b61c85)
## Module 4: YOSYS Synthesis
Yosys is an open source tool that can synthesize the RTL design (Verilog or VHDL) into gate - level netlist based on different technology.
![image](https://github.com/user-attachments/assets/7c2e5aa7-38a1-4311-9b01-a53cf93cb620)
The inputs for Synthesis are: 
- RTL (.v, vhdl)
- Timing Libraries (.lib files)
- SDC
- Technology files (for technology mapping)
- Unified Power Format (if needed for power analysis)

YOSYS creates technology dependent DAGs (Directed Acyclic Graphs) and maps to the technology file and generates a minimized gate-level netlist using standard cells.
Here, there is an example for MEMORY WRITE at the first positive edge of the clock
![image](https://github.com/user-attachments/assets/f732b951-e382-4634-bf1e-a77243a99c98)
Memory Read at the second positive edge of the clock
![image](https://github.com/user-attachments/assets/a2adfba7-ad73-4753-b331-0f7d517e9e3a)
Hierarchical check: Analyses and verifies the design's hierarchical structure:
![image](https://github.com/user-attachments/assets/63833b7f-ee0c-42d9-95ae-ac0527706226)
![image](https://github.com/user-attachments/assets/4a59f19b-a6ab-4eb1-a17c-12ae13b99752)
- Checking the error - Error Flag is Zero
![image](https://github.com/user-attachments/assets/1ebac623-2ccd-49ff-bb10-10278bf0d16b)
We are creating an error in the verilog file
![image](https://github.com/user-attachments/assets/c9620264-aa03-4022-a66b-bebf3d3c0953)
Error flag is 1
![image](https://github.com/user-attachments/assets/6906314e-1656-419a-9cfd-39eff35a7bc7)
We can grep out the error message directly in the tcl from the log file
![image](https://github.com/user-attachments/assets/753bb1f2-7dbe-4dcd-b08a-0d8a9165e7b9)
Repeat the same by creating an error
![image](https://github.com/user-attachments/assets/30023dc5-fc9a-43d0-84a0-f754623965fc)

## Module 5: Synthesis and Creating a Script for OpenTimer and perform STA Analysis and Generation of Quality of Results (QoR)
Completed Synthesis Successfully.
![image](https://github.com/user-attachments/assets/ab4aeb90-909d-4e54-96f3-baa279850ed7)
Here, the '*' generated in the synthesized verilog file cannot be used for Opentimer, therefore after necessary scripting the unnecessary commands are removed. 
Before removing:
![image](https://github.com/user-attachments/assets/b8eb6b87-812e-416f-b2c8-e4cb7c9fb1cf)
After removing:
![image](https://github.com/user-attachments/assets/38806fc5-9342-4e25-9d9f-d98688adc1e4)
### Introduction to Procs
![image](https://github.com/user-attachments/assets/dcf5a7fd-9f64-477b-9fa5-8d7d3e5415de)
The proc command creates a new Tcl procedure named name, replacing any existing command or procedure there may have been by that name. It is similar to the concept of functions in programming languages. 
We have used various procs in our scripting: 
1. reopenStdout.proc and set_multi_cpu_usage.proc:
These procs are used for opening a new window and closes the existing log file and also use multi-threading
  ![image](https://github.com/user-attachments/assets/6312abf1-746b-484c-bf1c-a320af9bd91d)
Executing these procs in the test.tcl and understanding the arguements passed to it in the tcl script
![image](https://github.com/user-attachments/assets/d6a4b373-b21e-40ff-8303-609749c11344)
![image](https://github.com/user-attachments/assets/e56c6b51-df34-45f7-a611-1a12a6bf908d)
Executing these in the main script provides a .conf file which is crucial for the Opentimer tool for STA
![image](https://github.com/user-attachments/assets/53ab8c84-54cb-4800-9cd3-b0c340c3fea5)
conf file:
![image](https://github.com/user-attachments/assets/65eefda9-a6b9-4a24-8333-22a058b7f8c7)
2. read_lib.proc:
This is used to read the early lib and late lib for Opentimer
![image](https://github.com/user-attachments/assets/032cb452-dee7-47c5-a49c-d8d4bf6d8b5c)
.conf file:
![image](https://github.com/user-attachments/assets/0084c3a4-11b2-428b-bbf8-8dcbacf6edea)
3.  read_verilog.proc:
![image](https://github.com/user-attachments/assets/826bf57c-30fd-4c0c-b155-ae47cb581d48)
.conf file:
![image](https://github.com/user-attachments/assets/a83c36c6-2a28-49b7-a93e-a6dafb9b85a2)
4. read_sdc.proc:
 The read_sdc function is a substantial function file that will be divided into sections. This approach is employed to convert the sdc file into OpenTimer format by grepping the statements in the .proc file ![image](https://github.com/user-attachments/assets/c44afef7-12dc-499c-b26c-d20565e9341d)
Creation of timing report from SDC to a Opentimer compatible format:
![image](https://github.com/user-attachments/assets/1e72f032-cdab-4c6c-8c94-098f4a829ba1)
.conf file:
![image](https://github.com/user-attachments/assets/49917845-cc4b-4a52-a108-912cd6b7f7bc)
### Quality of Results (QoR):
- vertical QoR generation:
  ![image](https://github.com/user-attachments/assets/768515ec-75fd-4577-b745-aeb586dfc10d)
- Horizontal QoR generation:
  ![image](https://github.com/user-attachments/assets/4d1b23b3-d127-4c48-93cb-ba5ba9cad91e)

## Conclusion:
Finally, I was able to successfully automate the process for Synthesis, STA and generate a quality report using TCL BOX
![image](https://github.com/user-attachments/assets/79eb8686-0f59-4c26-a6e9-97089a1d8ff2)

## Acknowledgements: 
I extend my sincere gratitude to Kunal Ghosh and the VSD team for their guidance.
Github: 
https://github.com/Visruat/VSD-TCL.git

## Certificate of Completition
![5_VSD TCL Wokrshop Certificate 2025VSD-TCL Workshop Certificate](https://github.com/user-attachments/assets/58f24847-4213-4e2d-a0d2-fc99703750c3)



