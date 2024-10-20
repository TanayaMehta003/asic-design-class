RTL design using Verilog with SKY130 Technology

## Icarus Verilog-Based Simulation Flow

A simulator is used to validate whether a design aligns with its intended specifications by running simulations on the code. It monitors changes in input signals, and whenever these inputs vary, the corresponding outputs are recalculated. RTL (Register Transfer Level) design refers to the Verilog code that describes the behavior and structure of a digital circuit. To ensure correctness, a testbench is developed to test the design through simulation using Icarus Verilog.

During the simulation, a VCD (Value Change Dump) file is generated, which logs signal transitions. This file is analyzed using GTKWave, a waveform viewer that assists in debugging and verifying circuit behavior. GTKWave allows users to explore signal interactions, inspect timing relationships, and validate the overall operation of the design by visualizing the waveforms created during simulation.

<details>
	  <summary>Setup</summary>
	 Enter the following commands in the Ubuntu terminal 
	  
