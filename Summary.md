# L1: Introduction to iverilog Design and Testbench

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
