
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

##### Common Pitfalls Introduced:

Incomplete sensitivity lists (i0, i1, sel should be included).

Using non-blocking assignments in combinational logic instead of blocking.

#### Lab 2: Sequential Logic with Blocking Assignments

Scenario: Using blocking assignments inside a clocked always block.

Issue: Sequential dependencies may use previous values, leading to incorrect outputs after synthesis.

##### Solution:

Use non-blocking assignments for clocked logic.

Calculate all intermediate values before updating dependent signals.

Observation: Correcting assignment types eliminates mismatch and ensures RTL simulation matches GLS.

### 5. Key Takeaways
GLS ensures post-synthesis correctness before physical design.

Synthesis-simulation mismatches arise from unclear or non-synthesizable RTL.

Correct assignment usage is essential:

Blocking (=) → combinational logic

Non-blocking (<=) → sequential logic

Hands-on labs reinforce understanding of proper RTL coding and verification techniques.

Bottom Line: Mastering these practices ensures that your RTL behaves predictably in both simulation and actual hardware, reducing bugs and design iterations.
