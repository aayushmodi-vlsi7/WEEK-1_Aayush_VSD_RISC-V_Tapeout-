<div align="center">

# Day 2 – Timing Libraries, Synthesis Styles & Flip-Flops
</div>
After exploring the basics of RTL simulation, we now move one step deeper into the design flow. Today is all about understanding how RTL translates into real hardware and how different coding and synthesis choices affect the final circuit.

## What We’re Covering
Get familiar with the .lib timing library (Sky130 PDK example).

See how timing libraries guide synthesis and analysis.

Compare Hierarchical vs. Flat Synthesis approaches.

Practice different flip-flop coding styles in Verilog and learn why they matter.
## Timing Libraries (.lib)
In digital design, a timing library is like a dictionary for the synthesis tool. It describes how every standard cell (logic gate, flip-flop, multiplexer, etc.) behaves in terms of:

Functionality (what it does)

Timing (delays, setup, hold times)

Power consumption

Without this information, the synthesis tool wouldn’t know how fast or efficient the real hardware would
To peek inside the Sky130 library, simply open the .lib file:
```bash
gvim sky130_fd_sc_hd__tt_025C_1v80.lib
```

![Alt Text](Palak_ysoys.png)

## Hierarchical vs. Flat Synthesis
When it comes to synthesis, there are two main strategies:
### Hierarchical Synthesis
The design is divided into modules or blocks.

Each block is synthesized separately and then stitched together.

Advantages: Modular, easier to debug, reusable.

Limitation: Less optimization across module boundaries
### Flat Synthesis
The tool treats the entire design as one big circuit.

Optimizations can be done globally.
Advantages: Better area and performance results.
Limitation: Harder to debug or reuse
Think of it like building with Lego blocks (hierarchical) vs. melting everything into one solid structure (flat).

### Example of Hierarchical Synthesis
![Alt Text](Palak_ysoys.png)

### Example of Flat Synthesis
![Alt Text](Palak_ysoys.png)

## Flip-Flop Coding Styles
Flip-flops are the memory elements of digital circuits, and the way you write them in Verilog directly impacts how tools map them into hardware. Writing them properly ensures:

Correct mapping to library flip-flops.

Efficient area and timing results.

Fewer unwanted gates inserted by synthesis.

Here are some commonly used styles:

####1. Asynchronous Reset D Flip-Flop

Output (Q) updates on the clock edge.

Reset takes effect immediately, independent of the clock.

Great for initializing circuits quickly after power-up.

####2. Asynchronous Set D Flip-Flop

Similar to async reset, but instead of clearing, the output is immediately forced to 1.

Useful when a circuit must start in a logic-high state.

####3. Synchronous Reset D Flip-Flop

Reset only happens along with the clock edge.

More predictable timing → easier analysis.
To view the gtkwave of these Flip-Flop, run the following commands:
```bash
iverilog dff_asyncres.v tb_dff_asyncres.v
```
```bash
./a.out
```
```bash
gtkwave tb_dff_asyncres.vcd
```
![Alt Text](Palak_ysoys.png)

Run the same commands for asyncres and syncres...
![Alt Text](Palak_ysoys.png)

![Alt Text](Palak_ysoys.png)


To view the synthesis with Yosys of these Flip-Flop, run the following commands:
```bash
yosys
```
```bash
read_liberty -lib /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
```
```bash
read_verilog /path/to/dff_asyncres.v
```
```bash
synth -top dff_asyncres
```
```bash
dfflibmap -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
```
```bash
abc -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
```
```bash
show
```
![Alt Text](Palak_ysoys.png) 

Run the same commands for asyncres and syncres...

![Alt Text](Palak_ysoys.png) 

![Alt Text](Palak_ysoys.png) 

## What I Learned Today


Timing libraries are the bridge between RTL and real hardware.

Hierarchical synthesis = modular and clean, Flat synthesis = highly optimized.

Flip-flop coding style has a huge impact on synthesis quality.

Simulation + synthesis together help visualize how coding choices affect area, timing, and power.

In short: Design discipline in RTL pays off later in performance, power, and reusability.

