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
<img width="2780" height="387" alt="gvim_opt_check v" src="https://github.com/user-attachments/assets/e4045c89-a69b-47ae-9c56-700d9a78b718" />
<img width="2780" height="387" alt="gvim_opt_check4 v" src="https://github.com/user-attachments/assets/f6b97db1-2b80-4a32-84c9-c18883a291a5" />
<img width="2780" height="387" alt="gvim_opt_check3 v" src="https://github.com/user-attachments/assets/f23b1074-b2cf-4a84-8621-414ade7d15b4" />
<img width="2780" height="387" alt="gvim_opt_check2 v" src="https://github.com/user-attachments/assets/c6760198-55bb-407f-93dd-2d9a7e226506" />
<img width="2780" height="968" alt="gvim_multiple_module_opt2" src="https://github.com/user-attachments/assets/476bc728-386d-4ee9-9bf7-b518aeae79b4" />
<img width="2780" height="968" alt="gvim_multiple_module_opt" src="https://github.com/user-attachments/assets/6ebbe861-122d-458d-8724-d98d945f5431" />

Take the steps from the Day 1 Synthesis Lab, and insert the following commands in the flow right after abc -liberty but before synth -top.
```bash
opt_clean -purge
```
Do the same for all 6 files and observe the yosys output:
<img width="2780" height="1243" alt="opt_check_netlist" src="https://github.com/user-attachments/assets/809f7f39-dd30-46fd-8706-5ed47b568cf6" />
<img width="2780" height="1370" alt="opt_check4_netlist" src="https://github.com/user-attachments/assets/0e70282c-8c1e-4a4a-be65-23466ac18315" />
<img width="2780" height="1370" alt="opt_check3_netlist" src="https://github.com/user-attachments/assets/cb3d561b-3b64-4e41-b0f6-cf1f8d8a9f45" />
<img width="2780" height="1243" alt="opt_check2_netlist" src="https://github.com/user-attachments/assets/f426eae7-ba19-4f40-888e-a14ce1d2afdb" />
<img width="2780" height="1611" alt="multiple_module_netlist" src="https://github.com/user-attachments/assets/633f1290-674e-4f38-bbb8-d4bca4bf2662" />
<img width="2780" height="1611" alt="multiple_opt2_netlist" src="https://github.com/user-attachments/assets/4492a079-1627-444f-9b70-88ce8dd0f7bb" />


## Sequential Logic Optimization
Sequential circuits use memory elements like flip-flops and latches. Optimizing them improves speed, area, and power.

Main strategies:

Retiming Flip-Flops → move registers to shorten critical paths.

State Optimization → reduce FSM size and choose efficient encoding.

Register Sharing or Removal → eliminate unused flip-flops to save resources.

Example: A D flip-flop-based counter can be optimized to remove bits that don’t contribute to outputs.

Observe in GTKWave and verify functionality.

Compare synthesized netlists to see unnecessary logic removed.

Eg:
<img width="2780" height="653" alt="gvim_dff_const4 v" src="https://github.com/user-attachments/assets/82a650fb-6d75-45f2-9be4-abfd0ae08f77" />

<img width="2780" height="1620" alt="gtkwave_dff_const4" src="https://github.com/user-attachments/assets/c0936fba-fdc5-427a-a08b-a1357030f4f5" />

<img width="2780" height="1620" alt="dff_const4_netlist" src="https://github.com/user-attachments/assets/2c42d953-705c-46a4-95a0-bc4fbd28152d" />



## Removing Unused Outputs
Unused outputs can occupy gates and flip-flops unnecessarily. Synthesis tools automatically:

Detect these outputs.

Remove the associated logic.

Keep the functional behavior intact.

Illustration:

If a counter has only count[0] driving outputs, Yosys removes other bits.

If all bits are used, the full counter logic remains.

eg:
<img width="2780" height="656" alt="gvim_counter_opt v" src="https://github.com/user-attachments/assets/23db32aa-b14c-404a-985b-7278fda4a100" />
<img width="2780" height="656" alt="gvim_counter_opt2" src="https://github.com/user-attachments/assets/85fca7a8-d080-473d-a5b5-ea02726e2057" />
Synthesis of Counter_opt files are given below
<img width="2780" height="1178" alt="counter_opt_netlist" src="https://github.com/user-attachments/assets/3d80134b-f796-4108-8a75-beb4dbf870ec" />
<img width="2780" height="1178" alt="counter_opt2_netlist" src="https://github.com/user-attachments/assets/9a9bad10-1f09-4b59-bcf0-3a47d507ef81" />


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

