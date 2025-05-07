# TCL Scripting for VLSI Design and Synthesis: From Fundamentals to Advanced Techniques
Tool Command Language (TCL) is a powerful scripting language widely used in the field of VLSI for automating EDA tool flows, particularly in synthesis, placement, routing, timing analysis, and verification. 

The primary goal of this repository  is to develop an automation tool that takes a CSV input files containing paths and Standard Design Constraints (SDC) and generates a corresponding TCL script. This script will then be used for automating digital synthesis using Yosys, an open-source RTL synthesis tool for Verilog designs.

## TASKS:
- Create command (for eg. vsdsynth) and pass csv from UNIX shell to TCL script
- Convert all inputs to format [1] & SDC format, and pass to synthesis tool 'Yosys'
- Convert format [1] & SDC to format [2] and pass to timing tool 'Opentimer'
- Generate output report
