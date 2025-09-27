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

<img width="2780" height="1620" alt="sky130_fd_sc_hd__tt_025C_1v80_lib " src="https://github.com/user-attachments/assets/6f23843a-e05a-4458-8012-384917a1a012" />

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
<img width="2780" height="1620" alt="Hierarchical multiple_modules" src="https://github.com/user-attachments/assets/e638623c-d348-49c9-a541-2936ac69bc78" />

### Example of Flat Synthesis
<img width="2780" height="1620" alt="Flatten Multiple_modules" src="https://github.com/user-attachments/assets/95b6e5ee-d808-4fe0-a2a3-7d60c9969036" />

## Flip-Flop Coding Styles
Flip-flops are the memory elements of digital circuits, and the way you write them in Verilog directly impacts how tools map them into hardware. Writing them properly ensures:

Correct mapping to library flip-flops.

Efficient area and timing results.

Fewer unwanted gates inserted by synthesis.

Here are some commonly used styles:

#### 1. Asynchronous Reset D Flip-Flop

Output (Q) updates on the clock edge.

Reset takes effect immediately, independent of the clock.

Great for initializing circuits quickly after power-up.

#### 2. Asynchronous Set D Flip-Flop

Similar to async reset, but instead of clearing, the output is immediately forced to 1.

Useful when a circuit must start in a logic-high state.

#### 3. Synchronous Reset D Flip-Flop

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
<img width="2780" height="1620" alt="dff_asyncres_waveform" src="https://github.com/user-attachments/assets/548a9b79-b404-4dfa-ba28-7007e78fd869" />

Run the same commands for asyn and syncres...
<img width="2780" height="637" alt="dff_async_set v" src="https://github.com/user-attachments/assets/189e6411-8eb0-4c2a-abe4-be814a03e52a" />

<img width="2780" height="637" alt="dff_syncres v" src="https://github.com/user-attachments/assets/a0dde951-a54b-46ad-b572-742c67043c2e" />


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
<img width="2780" height="1281" alt="dff_asyncres_netlist" src="https://github.com/user-attachments/assets/0e3930c9-5b81-4a35-8754-b6ac8abca92b" />

Run the same commands for asyn and syncres...

<img width="2780" height="1281" alt="dff_async_set_netlist" src="https://github.com/user-attachments/assets/739233c1-d093-4b9d-a913-4d5ff6be52a2" />


<img width="2780" height="1281" alt="dff_syncres_netlist" src="https://github.com/user-attachments/assets/164fcae8-3a3c-4e3d-8de3-214de78b0439" />

## What I Learned Today


Timing libraries are the bridge between RTL and real hardware.

Hierarchical synthesis = modular and clean, Flat synthesis = highly optimized.

Flip-flop coding style has a huge impact on synthesis quality.

Simulation + synthesis together help visualize how coding choices affect area, timing, and power.

In short: Design discipline in RTL pays off later in performance, power, and reusability.

