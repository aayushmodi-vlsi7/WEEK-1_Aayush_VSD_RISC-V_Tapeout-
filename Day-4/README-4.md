
<div align="center">

# Day 4: Gate-Level Simulation (GLS), Blocking vs. Non-Blocking in Verilog, and Synthesis-Simulation Mismatch

</div>

## Overview
In Day 4, we dive into the critical aspects of RTL design verification, focusing on:

Gate-Level Simulation (GLS) – Ensuring your synthesized design works as intended.

Synthesis-Simulation Mismatches – Understanding why RTL and hardware sometimes disagree.

Verilog Assignment Types – Correct usage of blocking and non-blocking statements.

Hands-on labs are integrated to reinforce concepts through practical experiments, helping you connect theory to real-world RTL design challenges.

### 1. Gate-Level Simulation (GLS)
GLS is the process of verifying a synthesized digital design at the gate level before moving to physical design. It provides confidence that the design behaves as expected, both functionally and temporally.

#### Why it matters:

Detects functional errors after synthesis.

Reveals timing issues like setup and hold violations.

Confirms proper implementation of test structures (e.g., scan chains).

#### Types of GLS:

Functional GLS: Focuses purely on logic correctness; ignores realistic delays.

Timing GLS: Incorporates gate delays and timing constraints, exposing potential real-world issues.

Key Point: GLS bridges the gap between RTL simulation and actual hardware behavior.
 ### 2. Synthesis-Simulation Mismatch
 Sometimes, a design that works perfectly in RTL simulation behaves differently once synthesized. This is called a synthesis-simulation mismatch.


#### Common reasons:

RTL contains constructs that synthesis tools cannot interpret.

Sensitivity lists are incomplete or signals are missing in combinational blocks.

Conflicting interpretations between simulation and synthesis tools.

#### Best Practices to Avoid Mismatch:

Write fully synthesizable RTL.

Keep coding explicit and unambiguous.

Regularly verify designs using GLS.

### 3. Verilog Assignment Guidelines
Verilog offers two primary assignment types within procedural blocks:
|   Assignment Type   |   Syntax   |   Behavior                                        |   Use Case               |
| ------------------- | ---------- | ------------------------------------------------- | ------------------------ |
| Blocking            | `=`        | Executes immediately, step by step                | Combinational logic      |
| Non-Blocking        | `<=`       | Updates at the end of the time step, concurrently | Sequential/clocked logic |
#### Rules of Thumb:

Use blocking (=) in combinational always blocks to ensure logic flows as expected.

Use non-blocking (<=) in clocked always blocks to correctly model flip-flop behavior.

#### Why it matters:
Incorrect usage can lead to subtle bugs, such as temporary variables using outdated values, causing mismatch between simulation and synthesized hardware.
 ### 4. Hands-On Labs
#### Lab 1: 2x1 MUX Implementation

Objective: Understand the impact of RTL coding on GLS results.

Experiment: Implement a MUX using a ternary operator.

##### Observations:

RTL simulation shows correct output.

Yosys synthesis confirms netlist correctness.

GLS validates gate-level behavior aligns with RTL.

 2*1 Mux using a ternery operator is given below:

 <img width="2780" height="323" alt="gvim_ternary_operator_mux v" src="https://github.com/user-attachments/assets/ae63f5a6-4a58-48f6-8cf4-d7b8fc4ad4a8" />
<img width="2780" height="1031" alt="gvim_tb_ternary_operator_mux v" src="https://github.com/user-attachments/assets/64565c3d-0560-40ae-a4ea-6ebaabb80a2c" />
GTKwave files are given below:
<img width="2780" height="1616" alt="gtkwave_ternary_operator_mux" src="https://github.com/user-attachments/assets/b3014405-91cd-4561-9017-8a995fdb65a0" />
<img width="2780" height="1616" alt="gtkwave_ternary_operator_mux2" src="https://github.com/user-attachments/assets/d65abd13-a698-4af5-8ce3-b5ad7f233cf6" />

YOSYS synthesis is given below:
<img width="2780" height="1616" alt="ternary_operator_mux_netlist" src="https://github.com/user-attachments/assets/4f8816e0-03a1-4d9c-b6ed-62e512e13fb5" />


##### Common Pitfalls Introduced:

Incomplete sensitivity lists (i0, i1, sel should be included).

Using non-blocking assignments in combinational logic instead of blocking.

#### Lab 2: Sequential Logic with Blocking Assignments

Scenario: Using blocking assignments inside a clocked always block.

Issue: Sequential dependencies may use previous values, leading to incorrect outputs after synthesis.

Example of Bad Mux is given below:
<img width="2780" height="527" alt="gvim_bad_mux v" src="https://github.com/user-attachments/assets/5c5462da-c1d0-4046-b395-c0cf619ff805" />
GTKwaveform
<img width="2780" height="1616" alt="gtkwave_bad_mux" src="https://github.com/user-attachments/assets/66402f7b-b727-4d15-aaaf-a9b8faa9b22b" />
<img width="2780" height="1616" alt="gtkwave_bad_mux2" src="https://github.com/user-attachments/assets/dc2c0cac-ea62-4c95-8555-504c71463e6e" />
YOSYS



##### Solution:

Use non-blocking assignments for clocked logic.

Calculate all intermediate values before updating dependent signals.

Observation: Correcting assignment types eliminates mismatch and ensures RTL simulation matches GLS.

For the Blocking Caveat
<img width="2780" height="496" alt="gvim_blocking_caveat v" src="https://github.com/user-attachments/assets/a3d941c3-f3fe-4b8d-a15a-8e0f61d6ee5c" />
GTKwaveform:
<img width="2780" height="1613" alt="gtkwave_blocking_caveat" src="https://github.com/user-attachments/assets/331c18e1-8c4f-4cd2-a0d1-de9209afc728" />
<img width="2780" height="1613" alt="gtkwave_blocking_caveat2" src="https://github.com/user-attachments/assets/a07932d0-2835-4bbe-b14b-4fb34565df60" />
YOSYS:
<img width="2780" height="1613" alt="blocking_caveat_netlist" src="https://github.com/user-attachments/assets/ca778321-e147-4faf-b13f-b871b3f89431" />



### 5. Key Takeaways
GLS ensures post-synthesis correctness before physical design.

Synthesis-simulation mismatches arise from unclear or non-synthesizable RTL.

Correct assignment usage is essential:

Blocking (=) → combinational logic

Non-blocking (<=) → sequential logic

Hands-on labs reinforce understanding of proper RTL coding and verification techniques.

Bottom Line: Mastering these practices ensures that your RTL behaves predictably in both simulation and actual hardware, reducing bugs and design iterations.
