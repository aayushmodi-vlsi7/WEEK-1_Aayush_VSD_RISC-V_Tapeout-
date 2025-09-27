<div align="center">

# Day 1 - Introduction to Verilog RTL Design & Synthesis

</div>  

## Introduction: 
You’ll start writing hardware descriptions in Verilog, run your first simulations with Icarus Verilog, and even peek into logic synthesis with Yosys.

This first step is designed to be simple and hands-on, so you can build confidence while learning the fundamentals of RTL design.

## What We’ll Cover
Understanding Simulator, RTL Design, Testbench, and Icarus Verilog

Running your first simulation with Icarus Verilog + GTKWave

Introduction to Yosys and the idea of synthesis

Practice synthesis using Yosys with the SKY130 PDK

## Step 1: Simulator, Design, and Testbench Basics
Simulator: A program that lets you test how your circuit behaves without touching real hardware. You provide input signals and see how the circuit responds.

Design: The Verilog code you write. It defines the logical functionality—how inputs are processed to produce outputs.

Testbench: A kind of “experiment setup” where you feed test inputs into your design and check the outputs. It’s like a lab assistant that verifies if your circuit works.

Icarus Verilog (iverilog): An open-source tool that simulates your Verilog design. It generates a .vcd file that can be opened in GTKWave to view waveforms.

<div align="center"> 
  
  <img src="https://github.com/user-attachments/assets/93927b96-df80-4da5-b801-284fc2cc6757" alt="Design & Testbench Overview" width="70%">

  </div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/3ca190fb-cfa4-4abb-b9e1-0151b3c4bdba" alt="iverilog Simulation Flow" width="70%">
</div>

## Step 2: Practical Work with Icarus Verilog + GTKWave
We’ll use a 2-to-1 multiplexer (MUX) as our example.

### 1) Clone the repository
```bash
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
```
### 2) Install gvim (for editing Verilog files)
```bash
sudo apt update
sudo apt install vim-gtk3
```
### 3) Compile, run, and view waveforms
```bash
iverilog good_mux.v tb_good_mux.v
```
```bash
./a.out
```
```bash
gtkwave tb_good_mux.vcd
```

![Alt Text](Day 1 gtkwave.png)

![Alt Text](Day 1 gtkwave.png)

### How the 2x1 MUX Works
Inputs: i0, i1 (data signals), sel (control)

Output: y

Logic:

If sel = 0 → y = i0

If sel = 1 → y = i1

This simple design shows how selection logic works in hardware.

## Step 3: Introduction to Yosys and Synthesis
So far, we’ve tested functionality. But what if we want to actually build the circuit?
That’s where synthesis comes in.

Yosys takes your RTL (Verilog code) and converts it into a netlist of logic gates.

It uses a cell library (like the SKY130 PDK) that provides the actual building blocks (AND, OR, MUX, etc.).

## Step 4: Running Yosys with SKY130
Inside a terminal:
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
This flow takes your multiplexer RTL and maps it into gates from the SKY130 standard cell library. The show command will display the gate-level schematic.

![Alt Text](Day 1 gtkwave.png)
## Key Takeaways from Day 1
Learned what a simulator does and why it’s useful.

Understood what “design” means in Verilog.

Saw how a testbench helps in verifying circuits.

Wrote and simulated your first Verilog program (2x1 MUX).

Generated waveforms and analyzed them in GTKWave.

Got introduced to Yosys for synthesis.

Discovered that gate libraries come in different versions for different needs.

Connected the complete flow:

