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

