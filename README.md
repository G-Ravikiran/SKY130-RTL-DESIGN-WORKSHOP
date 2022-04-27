# [SKY130-RTL-DESIGN-WORKSHOP](https://github.com/G-Ravikiran/SKY130-RTL-DESIGN-WORKSHOP/blob/main/README.md)
![Verilog-flyer (1)](https://user-images.githubusercontent.com/104474928/165444531-7100dd83-27a8-4cf3-a2f8-f574f72e82fd.png)

## Table Of Contents 
  * ### [Project Scope](https://github.com/G-Ravikiran/SKY130-RTL-DESIGN-WORKSHOP/blob/main/README.md#project-scope)
  * ### [Getting Started](https://github.com/G-Ravikiran/SKY130-RTL-Design-Workshop/blob/main/README.md#getting-started)
  * ### [Introduction to Verilog RTL Design & Synthesis](https://github.com/G-Ravikiran/SKY130-RTL-Design-Workshop/blob/main/README.md#day-1----introduction-to-verilog-rtl-design-and-synthesis)
   * #### [Setting up libraries & lab instances](https://github.com/G-Ravikiran/SKY130-RTL-Design-Workshop/blob/main/README.md#part-1----setup-the-lab-instance-with-libraries-and-verilog-files)
   * #### [iverilog Simulation of 2:1 MUX RTL Design](https://github.com/G-Ravikiran/SKY130-RTL-Design-Workshop/blob/main/README.md#part-2---simulation-using-iverilog-simulator---21-multiplexer-rtl-design)
   * #### [Synthesis using YOSYS Tool](https://github.com/G-Ravikiran/SKY130-RTL-Design-Workshop/blob/main/README.md#part-3----synthesis-using-yosys-open-source-tool)











## Day 1 -  Introduction to Verilog RTL Design and Synthesis

The first day covers the basics of RTL Design, Testbench, Simulation and Synthesis. Open-Source softwares like iverilog (simulator) and YOSYS (Synthesis) are provided through remote access in the portal to practice labs.

RTL Design -  It consists of an actual verilog code / a set of verilog codes that have the functionality to meet the required design specifications of the circuit
TestBench - Testbench is a setup that one uses to apply a set of stimuli (test-case vector) to check the functional working of the design file

We do the above processes using a simulator software. The simulator is loaded with the design and its respective testbench file after which it looks for changes in the input signals and depending on the change, the output is evaluated. These changes in input and corresponding output values are dumped in a special format file called "value change dump" (.vcd) file. This file can be pictorially represented in waveforms using a waveform tool like gtkwave. 


### Part 1 -  Setup the lab instance with libraries and verilog files

Firstly, we have to clone 2 separate repositories namely [vsdflow](https://github.com/kunalg123/vsdflow) and [sky130RTLDesignAndSynthesisWorkshop](https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop) which contain the required library files and verilog design files to perform the simulations and logic synthesis parts of the workshop. It can be done using basic linux command gitclone ex: git clone https://github.com/kunalg123/vsdflow.git .
We are given a default set of files and libraries shown below to work on using the practical lab instance

![verilog and lib ](https://user-images.githubusercontent.com/104474928/165447064-3c6e79bd-a9b1-4805-ba91-4561ee2762b6.png)

### Part 2 - Simulation using iverilog simulator - 2:1 multiplexer rtl design

After cloning the respective repositories in our lab instance, we perform a simulation run of 2:1 multiplexer rtl file namely good_mux.v and its corresponding testbench file tb_good_mux.v to obtain .vcd files and analyze the waveform in gtkwave to see the change in output instances with respect to change in input values.

![mux](https://user-images.githubusercontent.com/104474928/165448514-0cda36d8-d5ca-4b07-9a8f-de7c7ee1d5fd.png)

![tbmux](https://user-images.githubusercontent.com/104474928/165448530-94fb4ea6-650a-41ec-8c1a-9301ad491c2d.png)

![simulation](https://user-images.githubusercontent.com/104474928/165448547-8cf2edd3-b7f2-4f9b-a1bb-ac8f2da7113d.png)
![gtk](https://user-images.githubusercontent.com/104474928/165448654-892f62b8-de51-4980-b543-fe19b2aaf049.png)

Part 3 - Synthesis using YOSYS open-source tool
After simulation of the rtl design with the respective testbench, we perform a synthesis of the design using Synthesizer. A Synthesizer is a tool used to convert the RTL Design into a netlist file (Standard Cell Format). To be more specific, a netlist is a standard gate level file that consists of nets, sequential and combinational cells and their connectivity of the corresponding RTL file coded using a HDL. In simple words, an rtl file is a code that describes the functionality of the design and a netlist is a file that expresses the same code in the form of logic cells like logic gates, flipflops, multiplexers with net connections etc.

Here, we use a synthesizer tool called YOSYS which is a part of Qflow (open-source) tool chain for complete RTL2GDS transformation. The basic input files to YOSYS include the RTL Design file and .lib (library) files.

What is a .lib file?

--> .lib files are a collection of logical modules which include logic gates like AND, OR, NOT, NAND, NOR etc. Each logic gate is stored in one or more flavours depending on the number of inputs and speed of the circuit (slow, fast & medium).

Why do we need different flavours of the same logic gate?

--> Combinational delays present in a logic path determine the maximum speed and performance of a logic circuit. For Example, to get a maximum performance from a circuit, we need to design the circuit with minimum clock delays.

Inorder to obtain minimum clock delays, we require very fast cells to minimize the clock delays.

In the same way, inorder to avoid Hold violations in a logic path, we have to use SLOW cells to synchronize the hold time for logic path.

All these different types of fast and slow cells are present in a .lib file to be used by the synthesis software tool

Faster Cells vs Slower Cells
A cell delay in the digital logic circuit depends on the load of the circuit which here is Capacitance.

Faster the charging / discharging of the capacitance --> Lesser is the Cell Delay

Inorder to charge/discharge the capacitance faster, we use wider transistors that can source more current. This will help us reduce the cell delay but at the same time, wider transistors consumer more power and area. Similarly, using narrower transistors help in reduced area and power but the circuit will have a higher cell delay. Hence, we have to compromise on area and power if we are to design a circuit with low cell delay.

Constraints
A Constraint is a guidance file given to a synthesizer inorder to enable an optimum implementation of the logic circuit by selecting the appropriate flavour of cells (fast or slow).

Practical Synthesis using YOSYS
We perform a synthesis of the 2:1 Multiplexer RTL design using YOSYS with appropriate library files from SKY130 technology that we cloned into the directory.

![yosys](https://user-images.githubusercontent.com/104474928/165450982-730c0966-e4b3-4537-9c1f-ab1b5bc43db2.png)

![yosys commands](https://user-images.githubusercontent.com/104474928/165451008-4319c388-768f-41bd-98df-5c2d44dce68e.png)

![Screenshot 2022-04-27 112503](https://user-images.githubusercontent.com/104474928/165451150-790f5155-796d-4f43-9d0d-3fc9450f6dd6.png)

![Screenshot 2022-04-27 112536](https://user-images.githubusercontent.com/104474928/165451165-69a81772-6cd2-47c1-b825-8ef336fa150e.png)

![netlist](https://user-images.githubusercontent.com/104474928/165451232-9b13fb5f-c3f5-4213-bfca-60eeaa9d916d.png)

![netlistcode](https://user-images.githubusercontent.com/104474928/165451249-091978a1-f314-489e-8f89-e8eb1845a0d5.png)



