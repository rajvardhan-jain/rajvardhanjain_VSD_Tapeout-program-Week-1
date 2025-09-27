# Timing libs, hierarchial vs flat synthesis and efficient flop coding styles

## Introduction to Timing libs

### Lab Introduction to .lib

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


- Cell defines the attributes of the cell.
- Leakage power based on the combination of inputs
- Area
- Power ports
- Input capacitance
- Power associated with the pin
- Transition
- Delay

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


