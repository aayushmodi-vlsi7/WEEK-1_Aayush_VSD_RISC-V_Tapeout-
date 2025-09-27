<div align="center">
  
# Combinational and Sequential Optmizations
</div>
We dive into optimization strategies for digital designs. The goal is to enhance performance, save area, and reduce power while keeping the design behavior intact. We’ll explore both combinational and sequential circuits and see how smart coding and synthesis choices can make a big difference.

## Session Overview
Why optimization matters in modern VLSI.

Techniques to simplify combinational logic.

Methods to refine sequential circuits and FSMs.

Handling unused outputs to remove redundant logic.

Hands-on lab exercises with Verilog files and Yosys.

## Understanding Optimization
In VLSI design, optimization means improving a circuit’s efficiency without changing its functional behavior.

Key benefits:

Smaller circuit area → fewer gates.

Lower power consumption → less heat and energy.

Faster performance → shorter critical paths.

Cleaner designs → easier to maintain and reuse.

### Core Optimization Approaches
#### Constant Folding

Signals that are fixed (always 0 or 1) are replaced directly with those values.

Example: An AND gate with one input always 0 can be removed because its output will never change.

Result: fewer gates, shorter paths, lower power.

#### FSM Simplification

Finite State Machines can have redundant or unreachable states.

Techniques include merging equivalent states, removing unused ones, and choosing optimal state encoding (binary, one-hot, Gray).

Bonus: Clock gating can also cut down power.

#### Cloning Cells

Sometimes a single gate drives too many outputs, causing delays.

Duplicating (cloning) the gate splits the load, improving timing and sometimes saving power.

#### Retiming Registers

Flip-flops can be repositioned before or after logic without affecting function.

This reduces the longest path, improves clock speed, and balances delays between stages.

## Optimizing Combinational Logic
Combinational optimization focuses on pure logic gates: ANDs, ORs, XORs, etc.

Goal: Simplify expressions, remove redundancies, and shorten logic paths.

Common techniques: Boolean simplification, factoring, eliminating duplicated gates.

Hands-on example: We’ll optimize seven Verilog modules from previous labs.

We will perform the Combinational Logic Optimization for following verilog files:
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png)

Take the steps from the Day 1 Synthesis Lab, and insert the following commands in the flow right after abc -liberty but before synth -top.
```bash
opt_clean -purge
```
Do the same for all 7 files and observe the yosys output:
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png)
![Alt Text](Palak_ysoys.png) (multiple_module_opt)
![Alt Text](Palak_ysoys.png) (multiple_module_opt2)

## Sequential Logic Optimization
Sequential circuits use memory elements like flip-flops and latches. Optimizing them improves speed, area, and power.

Main strategies:

Retiming Flip-Flops → move registers to shorten critical paths.

State Optimization → reduce FSM size and choose efficient encoding.

Register Sharing or Removal → eliminate unused flip-flops to save resources.

Example: A D flip-flop-based counter can be optimized to remove bits that don’t contribute to outputs.

Observe in GTKWave and verify functionality.

Compare synthesized netlists to see unnecessary logic removed.

## Removing Unused Outputs
Unused outputs can occupy gates and flip-flops unnecessarily. Synthesis tools automatically:

Detect these outputs.

Remove the associated logic.

Keep the functional behavior intact.

Illustration:

If a counter has only count[0] driving outputs, Yosys removes other bits.

If all bits are used, the full counter logic remains.

## Hands-On Lab Summary
Combinational Circuits: Reduced gates, optimized paths.

FSMs: Smaller, better-encoded states.

Flip-Flops: Retimed and removed unused registers.

Yosys Verification: Observe waveform outputs and gate-level schematic.

Key Insight: Thoughtful design choices combined with synthesis optimization lead to leaner, faster, and more efficient digital circuits.

## Takeaways
Constant propagation eliminates unnecessary logic.

FSM state optimization simplifies sequential circuits.

Cloning balances load and improves timing.

Retiming strategically repositions registers for higher clock speeds.

Removing unused outputs reduces area and power without affecting functionality.

Optimizations work hand-in-hand with RTL coding discipline for best results.

