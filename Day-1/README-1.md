<div align="center">

# Day 1 - Introduction to Verilog RTL Design & Synthesis

</div>  

## Introduction: 
This session is your launchpad into the world of digital logic design. We’ll describe hardware in Verilog, run quick simulations, and then translate designs into real hardware primitives using Yosys. By the end, you’ll understand how ideas written in code turn into circuits.

## Roadmap for the Session
Why simulation matters before hardware.

What makes up a design (RTL, testbenches, tools).

Hands-on: Simulating a multiplexer using Icarus Verilog + GTKWave.

First steps into synthesis with Yosys.

Exploring the SKY130 library and seeing how RTL becomes gates.
## Part 1: What’s in the Toolbox?
Let’s break down the players:

Simulation software → Like a virtual lab, it lets us test ideas without building physical circuits.

RTL design → The Verilog code you write. This is your description of how signals interact.

Testbench → Think of it as an automated script that feeds your design with input patterns and observes results.

Icarus Verilog (iverilog) → The engine that compiles and simulates Verilog. It creates .vcd files (waveform dumps).

GTKWave → A viewer that turns the .vcd file into waveforms so you can visually check what’s happening.

<div align="center"> <img src="https://github.com/user-attachments/assets/93927b96-df80-4da5-b801-284fc2cc6757" alt="Design & Testbench Overview" width="65%"> </div>

## Part 2: First Circuit – A Simple MUX
Instead of jumping into a complex design, let’s start with a 2:1 multiplexer.

### Clone the source files:
```bash
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
### Install an editor (optional):
```bash
sudo apt update
sudo apt install vim-gtk3
```
### Simulate it:
```bash
iverilog good_mux.v tb_good_mux.v
```
```bash
./a.out
```
```bash
gtkwave tb_good_mux.vcd
```
<div align="center"> <img src="Day 1 gtkwave.png" alt="MUX GTKWave Output" width="65%"> </div>

![Alt Text](Day 1 gtkwave.png)

![Alt Text](Day 1 gtkwave.png)

### Understanding the Multiplexer
Inputs: Two data signals (i0, i1) and one selector (sel).

Output: Single result (y).

Logic rule:

If sel = 0 → output = i0.

If sel = 1 → output = i1.

This is a great starter circuit because it shows how decision-making logic works in hardware.

## Part 3: What Is Synthesis?
Simulation confirms functionality, but it doesn’t tell us how the circuit looks in silicon.

That’s where synthesis comes in.

Yosys: An open-source synthesizer. It takes Verilog RTL and maps it to real gates.

Standard cell library (SKY130 PDK): Provides actual building blocks (AND, OR, NAND, flops, MUXes, etc.).

Together, they turn your high-level Verilog into something that could physically exist.

## Part 4: Yosys Flow with SKY130
Open a terminal and try:
```bash
yosys
```
```bash
read_liberty -lib /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
```
```bash
read_verilog /home/vsduser/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/good_mux.v
```
```bash
synth -top good_mux
```
```bash
abc -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
```
```bash
show
```
The final step opens a schematic showing how the RTL multiplexer is realized using gates from the SKY130 library.

<div align="center"> <img src="Day 1 gtkwave.png" alt="MUX Gate-Level" width="65%"> </div>

![Alt Text](Day 1 gtkwave.png)

## Wrap-Up Learnings
Here’s what you’ve accomplished today:

Explored simulation as a safe test environment for circuits.

Learned how RTL (Verilog code) captures logic.

Saw the role of a testbench in automatically verifying designs.

Built and simulated your first Verilog circuit (MUX).

Visualized outputs as waveforms in GTKWave.

Got introduced to Yosys for gate-level synthesis.

Understood that cell libraries (like SKY130) provide the building blocks for actual hardware.

Connected the full flow: RTL → Simulation → Synthesis → Gate-Level Netlist.
