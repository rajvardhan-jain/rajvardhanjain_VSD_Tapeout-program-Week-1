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

##SKY 130 RTL

<img width="807" height="594" alt="image" src="https://github.com/user-attachments/assets/1b02ccb5-dd15-49fe-9269-d93fdbd52f16" />

## L2 Introduction to iverilog and gtkwave part 1

### iVerilog:

<img width="1276" height="639" alt="image" src="https://github.com/user-attachments/assets/8411075d-9be5-453c-8135-c1eec61b29ba" />

### gtkwave:

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
- The guidance offered to the synthesizer is known as **Contraints**

<img width="1009" height="759" alt="image" src="https://github.com/user-attachments/assets/5fc3a4e7-6de8-4050-a9fd-b5129733ccbd" />


# Labs using Yosys and SKY130PDKs:

















