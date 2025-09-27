<div align="center">

# Day 5: Optimization in Synthesis

</div>

We focus on improving Verilog design quality and synthesis efficiency. The session emphasizes writing robust if-else and case statements, using for loops and generate blocks effectively, and avoiding pitfalls like inferred latches. Practical labs provide hands-on experience to see how coding practices impact both simulation and synthesized hardware.

## Session Overview
Importance of complete conditional coverage in combinational circuits.

Using loops and generate blocks to simplify repetitive hardware.

Avoiding unintended latches and synthesis mismatches.

Hands-on lab exercises with Verilog files, GTKWAVE, and Yosys outputs.

## Conditional Constructs
Conditional statements control circuit behavior based on inputs.

### If-Else Statements

Executes code for true conditions; else if chains allow multiple options; else provides a default.

Missing coverage may cause inferred latches in combinational logic.

Common uses: multiplexers, conditional signal assignments.

### Case Statements

Selects actions based on variable values.

Variants: casez (don’t care bits), casex (unknown states).

Ensure all inputs are covered; include default to avoid latches.

Common uses: FSMs, decoders, large multiplexers.

### Key Points:

Complete coverage prevents unintended storage elements.

Constructs can be nested for complex logic.

Proper usage ensures predictable combinational behavior.

### Labs: Incomplete If-Else Cases

Problem: Not all inputs handled → inferred latches.

Solution: Add all branches or a default assignment.

Observation: GTKWAVE and Yosys show outputs holding previous values for unhandled cases.

Lab Examples: incomp_if Verilog file and simulation outputs.

### Labs: Incomplete or Overlapping Case Statements

Problem: Missing input combinations or overlapping cases.

Impact: May produce latches or unpredictable hardware.

Prevention: Ensure mutually exclusive cases and include default.

Lab Examples: comp_case Verilog file and simulation/synthesis outputs.

### For Loops and Generate Blocks
For Loops

Procedural construct to repeat statements in always or initial blocks.

Simulation executes sequentially; synthesis unrolls loops into hardware.

Ensure loop bounds are constant or determinable at compile time.

## Labs: For Loops and Generate

4x1 MUX – iterative assignment with a for loop.

1x8 DEMUX – loop for efficient output control.

8-bit Ripple Carry Adder – generate block for repeated adders.

### Observation:

GTKWAVE confirms correct simulation behavior.

Yosys output shows clean hardware replication.

Labs demonstrate scalable and synthesizable designs using loops and generate blocks.

### Key Takeaways

Cover all conditions in if-else and case statements to prevent inferred latches.

Use for loops for iterative procedural logic.

Use generate blocks for systematic, repeated hardware.

Hands-on labs link coding practices to simulation and synthesis results.

Thoughtful RTL coding combined with these techniques results in predictable, efficient, and maintainable Verilog designs.
