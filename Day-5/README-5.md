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

<img width="2780" height="521" alt="gvim_incomp_if2" src="https://github.com/user-attachments/assets/2f1ceba1-0513-43e0-8683-24f5742164af" />
<img width="2780" height="372" alt="gvim_incomp_if v" src="https://github.com/user-attachments/assets/0ce6d605-15f8-47b5-95a6-527e1c55ce4d" />
GTKwaveform:
<img width="2780" height="1618" alt="gtkwave_incomp_if2" src="https://github.com/user-attachments/assets/e3830238-c54a-428b-a1cf-fcb72b1baacc" />
<img width="2780" height="1618" alt="gtkwave_incomp_if" src="https://github.com/user-attachments/assets/615f0328-4565-4688-a1c0-0af9d9f7be63" />
YOSYS:
<img width="2780" height="1618" alt="incomp_if_netlist" src="https://github.com/user-attachments/assets/ad5a2a8d-dd62-42b9-81be-5da8f2a2dbf1" />
<img width="2780" height="1618" alt="incomp_if2_netlist" src="https://github.com/user-attachments/assets/3146c3de-3465-4a6a-9ebd-4cfe1a480210" />



### Labs: Incomplete or Overlapping Case Statements

Problem: Missing input combinations or overlapping cases.

Impact: May produce latches or unpredictable hardware.

Prevention: Ensure mutually exclusive cases and include default.

Lab Examples: comp_case Verilog file and simulation/synthesis outputs.

<img width="2780" height="557" alt="gvim_comp_case v" src="https://github.com/user-attachments/assets/d4be95b3-af06-4796-beac-cd4907a2bf77" />
GTKwaveform:
<img width="2780" height="1607" alt="gtkwave_comp_case" src="https://github.com/user-attachments/assets/bd335e2d-7592-44ad-94dd-988e3320c74b" />

YOSYS:
<img width="2780" height="1607" alt="comp_case_netlist" src="https://github.com/user-attachments/assets/f0500535-3bc5-45df-a348-e041a60d35e5" />

### For Loops and Generate Blocks
For Loops

Procedural construct to repeat statements in always or initial blocks.
```bash
for (initialization; condition; increment) begin
    // Statements to execute
end
```

Simulation executes sequentially; synthesis unrolls loops into hardware.


Ensure loop bounds are constant or determinable at compile time.

## Labs: For Loops and Generate

4x1 MUX – iterative assignment with a for loop.

1x8 DEMUX – loop for efficient output control.

8-bit Ripple Carry Adder – generate block for repeated adders.
```bash
genvar i;
generate
    for (i = 0; i < 4; i = i + 1) begin : gen_loop
        and_gate and_inst (.a(in[i]), .b(in[i+1]), .y(out[i]));
    end
endgenerate
```

### Observation:

GTKWAVE confirms correct simulation behavior.

Yosys output shows clean hardware replication.

Labs demonstrate scalable and synthesizable designs using loops and generate blocks.

4*1 Mux
GVIM file:
<img width="2780" height="588" alt="gvim_mux_generate v" src="https://github.com/user-attachments/assets/d092d330-bf35-4da5-8052-74ae8d3b2682" />
GTKwaveform:
<img width="2780" height="1613" alt="gtkwave_mux_generate" src="https://github.com/user-attachments/assets/18a210e1-1c50-4ab0-81d4-3d2942db801b" />
YOSYS:
<img width="2780" height="1613" alt="mux_generate_netlist" src="https://github.com/user-attachments/assets/91b17540-2128-4659-8c91-d5e2fd7eac9f" />

1*8 Demux
GVIM file:

<img width="2780" height="770" alt="gvim_demux_generate v" src="https://github.com/user-attachments/assets/7716dd12-bc90-451b-94d6-2f018dded318" />
GTKwaveform:

<img width="2780" height="1611" alt="gtkwave_demux_generate" src="https://github.com/user-attachments/assets/eb0a1533-bfb8-4e45-a711-d1b5f4573c64" />
YOSYS:

<img width="2780" height="1611" alt="demux_generate_netlist" src="https://github.com/user-attachments/assets/ef3389fe-ca1d-471d-b00d-fdab4fbfe204" />

RCA Verilog code:
<img width="2780" height="760" alt="gvim_rca v" src="https://github.com/user-attachments/assets/0d2e5bcb-b636-423b-bb19-234fed2a4b95" />

FA Verilog code:
<img width="2780" height="760" alt="gvim_fa v" src="https://github.com/user-attachments/assets/f6a2a962-b7ff-4b52-b514-dd0f7374b94e" />

GTKwaveform:
<img width="2780" height="1611" alt="gtwave_rca" src="https://github.com/user-attachments/assets/cce41451-4dbf-4c7e-852e-ab83ff742777" />

YOSYS:
<img width="2780" height="1611" alt="fa_netlist" src="https://github.com/user-attachments/assets/c4e1a05b-d589-4c7f-8c93-f0619a71347d" />


### Key Takeaways

Cover all conditions in if-else and case statements to prevent inferred latches.

Use for loops for iterative procedural logic.

Use generate blocks for systematic, repeated hardware.

Hands-on labs link coding practices to simulation and synthesis results.

Thoughtful RTL coding combined with these techniques results in predictable, efficient, and maintainable Verilog designs.
