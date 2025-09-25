# ▸ Introduction to Verilog RTL Design and sysnthesis

## L1: Introduction to iverilog Design and Testbench

### ▸Simulator:

- RTL design is checked for adherence to the specifications by simulating the design.
- Simulator is the tool used for simulating the design, e.g iverilog.

### ▸Design:

- Design is the actual verilog code or set of verilog codes which has intended functionality to meet with the required specifications.

### ▸Testbench:

- Testbench is the setup to apply stimulus (test_vectors) to the design to check its functionality.

### How simulator works?

- Simulator looks for the changes on the input signals.
- Upon change to the input, the output is evaluated,
  i.e if no change to the input, no change to the output.
- Simulator is looking for change in the values of input.

## Simulation Procedure(Test bech Setup):

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/ccd23067-9ef1-4aa4-8aa5-857a05c93c67" />

## iVerilog based simulation flow:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/90b01dbc-7992-46c7-a2d9-85530d172d44" />

# ▸ Labs using iVerilog and gtkwave

## L1 Introduction to lab

## SKY 130 RTL

Folder structure of the git clone:
- `lib` - will contain sky130 cell library 
- `verilog_models` - will contain standard cell verilog model
- `verilog_files` -contains the lab experiments source files

<img width="807" height="594" alt="image" src="https://github.com/user-attachments/assets/1b02ccb5-dd15-49fe-9269-d93fdbd52f16" />

Design good_mux.v 

```
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
Testbench tb_good_mux.v 

```
`timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```
Command to run the design and testbench
```
iverilog good_mux.v tb_good_mux.v
```
The output of the iverilog is a .vcd file and a.out file is created. By executing a.out iverilog dump the vcd file.

## L2 Introduction to iverilog and gtkwave part 1

### iVerilog:

<img width="1276" height="639" alt="image" src="https://github.com/user-attachments/assets/8411075d-9be5-453c-8135-c1eec61b29ba" />

### gtkwave:

Command to view the vcd file in gtkwave 
```
gtkwave tb_good_mux.vcd
```

<img width="1283" height="662" alt="image" src="https://github.com/user-attachments/assets/e4d97f47-6848-4612-93cb-17946f9c114e" />

## L3 Introduction to iverilog and gtkwave part 2

### vimgtk file:

<img width="1282" height="658" alt="image" src="https://github.com/user-attachments/assets/cc6a2a49-69c4-4e93-9edc-770a57bdd1b0" />

# Introduction to Yosys and Logic synthesis

## L1 Introduction to Yosys:

### Synthesizer:

-  Tool used for converting RTL to netlist, e.g Yosys

### Yosys Flow:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/8e104579-7619-4410-baed-1115279bc456" />

### Verify Synthesis:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/c033470e-a985-4190-8ceb-ab8352371e67" />

- This stimulus should be same as output observed during RTL simulation.
- The set of Primary inputs/ primary outputs will remain same between the RTL design and Synthesized netlist, therefore same test bench can be used.

## L2 Introduction to Logic Synthesis part 1:

### RTL Design:

- RTL Design is the behavioural representation of the required specification.

- RTL is a code and we wand a hardware circuit so,

### Synthesis:

- RTL to Gate level translation
- The design is converted into gates and connections made between the gates.
- This is given out as a file called netlist.

<img width="467" height="647" alt="image" src="https://github.com/user-attachments/assets/ef5031c4-ef8f-4c60-84ca-12ab4de5a04d" />

### What is .lib?

- Collection of logical modules.
- It includes all the basic gates AND, OR, NAND, EXOR....
- Different flavours of same gate,
- e.g a. 2 input and gate, b. 3 input and gate... etc...

### Why different flavours of gate?

- Combinational delay in logic path determines the maximum speed of operation of digital logic circuit.
- T(CLK) should always be greater the  time delays cauled by Flip flops and combinational circuits comibned.
- f(clk)max = 1/ T(clk)min
- To get minimum Clock time period, the propogation delays and other delays should me minimum.

<img width="674" height="204" alt="image" src="https://github.com/user-attachments/assets/d179027b-2445-471f-963b-cc29feb59b85" />

## L3 Introduction to logic synthesis part 2:

### Why we need slow cells?

-  To ensure that there are no HOLD issues at DFF_B, we need cells that work slowly.
-  Hence we need cells that work fast to meet the required performance and we need cells that work slow to meet the HOLD.
-  The collection forms the .lib.

### Faster Cells vs Slower Cells:

- Load in Digital logic circuit = Capacitance.
- Faster the charging and discharging of capacitance = Lesser the cell delay.
- To charge/ discharge the capacitance fast, we need transistors capable of sourcing more current.
- Wider transistors = Low Delay = More Area and Power.
- Narrow transistors = More Dealy = Less Area and Power.
- Faster cells come at a cost of Area and Power.

### Selection of Cells:

- Need to guid the synthesizer to select the flavour of cells that is optimum for the implementation of logic circuit.
- More us of faster cells:
- Bad circuit interms of Power and Area.
- Hold time may be violated.
- More use of slower cells:
- Sluggish circuit may not meet the performance need.
- The guidance offered to the synthesizer is known as **Contraints**.

<img width="1009" height="759" alt="image" src="https://github.com/user-attachments/assets/5fc3a4e7-6de8-4050-a9fd-b5129733ccbd" />


# Labs using Yosys and SKY130PDKs:

- Synthesize Good_mux file using Yosys.
- Do the following commands under yosys.

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_0250_1v80.lib
read_ verilog good_mux.v
synth -top good_mux
opt; clean  //optional
abc -liberty ../lib/sky130_fd_sc_hd__tt_0250_1v80.lib
stat        // optional
show
```
<img width="1288" height="661" alt="image" src="https://github.com/user-attachments/assets/7a37b40e-c68f-49d2-89cd-c9916b1820a0" />

<img width="1296" height="660" alt="image" src="https://github.com/user-attachments/assets/85b76247-06c8-4ca2-a1b4-a516b8dbcfaa" />

<img width="1291" height="659" alt="image" src="https://github.com/user-attachments/assets/ad7cbf1e-1c1f-405c-896e-26a17074d1d0" />

- The result comes out as,

<img width="1275" height="410" alt="image" src="https://github.com/user-attachments/assets/62236b6e-d39a-4413-9fd2-bf5a9e0bbda3" />
























