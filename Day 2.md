# Timing libs, hierarchial vs flat synthesis and efficient flop coding styles

## Introduction to Timing libs

```
gvim ../lib/sky130_fd_sc_hd_tt__025C_1v80.lib
// use :syn off if you find the red irritating
```
- .lib is a bucket of various cells (logics)
- Here 130 is for 130nm, this library is for 130 nm device
- Libraries are characterized based on PVT (process, voltage, temperature) 
- Process = Variations due to fabrication changes
- Voltage = Variations due to voltage
- Temperature = Variations due to temperature
 
- tt stands for typical in the .lib (fast/slow/typical)
- 025C stands for temperature of 25 C in the .lib name 
- 1v80 stands for voltage of 1.8V in the .lib name

<img width="1292" height="629" alt="image" src="https://github.com/user-attachments/assets/743759d3-85c5-487c-8543-eeb1c9d1fb93" />


- Cell defines the attributes of the cell.
- Leakage power based on the combination of inputs
- Area
- Power ports
- Input capacitance
- Power associated with the pin
- Transition
- Delay

<img width="569" height="153" alt="image" src="https://github.com/user-attachments/assets/06b66ecd-dc4c-4682-97b6-361e9f2e1244" />

- Also there are some predefined attributes in there,
- Technology = cmos
- Delay model = lookup table (a predefined result)
- Unit of time = **1ns**
- Unit of Voltage= **1V**
- Unit of leakage power = **1nW**
- Unit of Current = **1mA**
- Unit of resistance= **1k ohm**
- Unit of capacitance= **1pF**

- The different flavours of same gate gives us different area numbers, to vary the delay and area.

## Hierarchial synthesis vs Flat synthesis

- Now taking a look at the multiple modules file

```
gvim multiple_modules.v   // when in verilog_files
```

<img width="1043" height="355" alt="image" src="https://github.com/user-attachments/assets/909fead7-c827-44af-9953-f7414426048b" />

- There are 2 Submodules,
- Submodule 2 is an OR gate.
- Submodule 1 is an AND gate.
- Then we can analyze the structure of multiple module.

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_0250_1v80.lib
read_ verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_0250_1v80.lib
show
```

<img width="1281" height="278" alt="image" src="https://github.com/user-attachments/assets/431648e1-459b-475a-a35b-0213634180c8" />

- this we see is a hierarchial design, as we see submodule u1 and u2 instead of and, or gates.
```
write_verilog -noattr multiple_modules_hier.v
!gvim multiple_modules_hier.v
```

<img width="1297" height="630" alt="image" src="https://github.com/user-attachments/assets/5713a6dd-7619-487f-9b84-4f51c6ddfd9d" />

- here we see use of NAND gate  instead of NOR , due to the stacking of PMOS in the NOR IS bad.

now open the flat model

```
flatten
write_verilog -noattr multiple_modules_flat.v
!gvim multple_modules_flat.v

```

<img width="1297" height="598" alt="image" src="https://github.com/user-attachments/assets/a7379953-b86c-44c8-88ea-eeeaf627e9f1" />

- Now, comparing this we can see the hier.v conserves the hierarchy and the flat.v show and/or gates in netlist.

now again do synthesis and flatten after to get,

<img width="1083" height="141" alt="image" src="https://github.com/user-attachments/assets/d251dc24-92d9-4956-ac1e-81315ae2e084" />

- You can also indivisually see the synthesis of sub modules

<img width="785" height="175" alt="image" src="https://github.com/user-attachments/assets/c85eca7b-70d6-4d4c-bfd2-fb762155666c" />

- Why sub module level synthesis is good?

- Multiple same modules in the logic.
- Divide and conquer approach.

## Various flop coding styles and optimizations:

### Why flops and flop coding styles

Glitches can occur in digital circuits due to signal delays, noise or timing issues. Flops prevent glitches during the operation by:

- Synchronization: Flops are edge-triggered devices, meaning they respond only to transitions of the input signal (e.g., rising edge, falling edge). This synchronization ensures that the output changes only at specific points, reducing the likelihood of glitches caused by transient signal variations.
- Timing Control: Flops are typically controlled by a clock signal, ensuring that all circuit operations occur synchronously. This eliminates timing issues that could lead to glitches due to data arriving at different times.

<img width="665" height="557" alt="image" src="https://github.com/user-attachments/assets/34cc3381-c817-470b-8f8c-3e25ef937bf1" />

- To initialize flops, we need to `set` and `reset` which can be synchronous or asynchronous.

<img width="1274" height="822" alt="image" src="https://github.com/user-attachments/assets/a4d5b6bd-c0f4-48ab-be02-7020d7ed0d1a" />

<img width="991" height="625" alt="image" src="https://github.com/user-attachments/assets/4cf27be4-a620-42b5-ad53-20889bfba94e" />

<img width="999" height="620" alt="image" src="https://github.com/user-attachments/assets/6767a4e4-2049-4b00-8e29-c554c7324371" />

<img width="991" height="622" alt="image" src="https://github.com/user-attachments/assets/ce60ce48-86fd-4ec4-83af-47a6d2d2a0da" />

<img width="1271" height="192" alt="image" src="https://github.com/user-attachments/assets/55d100f0-29d0-4d80-a634-c12deda73c47" />

<img width="1274" height="202" alt="image" src="https://github.com/user-attachments/assets/026913c5-3bf6-4ae6-aa10-91f709171978" />

<img width="1296" height="245" alt="image" src="https://github.com/user-attachments/assets/b6a3bbb5-4046-48d6-bb27-c627d6251aad" />

### Optimizations:

<img width="1055" height="212" alt="image" src="https://github.com/user-attachments/assets/3fd4b557-cb2e-4f68-a93f-1ecd32be607a" />
