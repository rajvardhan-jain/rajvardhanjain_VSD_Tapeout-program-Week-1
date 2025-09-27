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
rea
```

<img width="1281" height="278" alt="image" src="https://github.com/user-attachments/assets/431648e1-459b-475a-a35b-0213634180c8" />




