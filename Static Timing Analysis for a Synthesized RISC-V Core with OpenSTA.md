# Static Timing Analysis for a Synthesized RISC-V Core with OpenSTA

## Static Timing Analysis (STA) in ASIC Design

**Static Timing Analysis (STA)** plays a vital role in ASIC design, ensuring that the circuit meets all timing requirements without needing to perform dynamic simulations of actual data. STA confirms that data paths meet specified constraints, ensuring proper circuit operation under varying conditions.

## Timing Paths in STA

The primary objective of STA is to analyze **timing paths** and confirm that data travels correctly between points within designated time limits. Key types of timing paths include:

- **Setup Paths**: Ensure that data reaches the next stage before the triggering clock edge.
- **Hold Paths**: Ensure that data remains stable for a required duration following the clock edge.

## Clock Domains in STA

STA divides the design into **clock domains** to analyze timing relationships between elements operating under the same or different clocks. The handling of these paths depends on the nature of the clock domains:

- **Synchronous Domains**: Involves clocks with known relationships. Setup and hold checks are performed between these domains.
- **Asynchronous Domains**: Involves unrelated clocks. Special mechanisms such as **synchronizers** or **FIFO buffers** are often required to ensure proper data transfer between domains.

## Clock Skew and Jitter

- **Clock Skew**: Refers to differences in the arrival time of a clock signal at multiple flip-flops. It affects both setup and hold timing and is critical to STA.
- **Clock Jitter**: Represents variations in clock edge timing due to external factors like noise. STA incorporates jitter to ensure timing constraints are still met under such conditions.

## Essential Timing Checks

- **Setup Check**: Confirms that data arrives before the clock edge, leaving sufficient stabilization time.
- **Hold Check**: Verifies that data remains stable long enough after the clock edge to avoid glitches.

## Timing Margins and Slack

- **Slack**: The margin between the required time and the actual signal arrival time.
  - **Positive Slack**: Indicates that the timing constraints are satisfied.
  - **Negative Slack**: Signals a timing violation.

- **Setup Slack**: Measures how much time is left for setup constraints.
- **Hold Slack**: Represents the margin for hold timing requirements.

## Static Timing Analysis Tools

Popular STA tools include:
- **Synopsys PrimeTime**
- **Cadence Tempus**

These tools construct **timing graphs** to traverse all paths in the design, providing reports on **slack**, **critical paths**, and **violations**.

## PVT Corners in Timing Analysis

STA considers **Process, Voltage, and Temperature (PVT) variations** to ensure that the design meets timing constraints under all conditions, including worst-case scenarios.

## Optimization Techniques

- **Buffer Insertion**: Adds buffers to reduce delays in long paths.
- **Gate Sizing**: Resizes gates to improve performance on critical paths.
- **Clock Tree Optimization (CTO)**: Reduces clock skew and jitter within the distribution network.

## Key Timing Paths

### Reg2Reg Path

A **register-to-register (reg2reg) path** connects two sequential elements, typically flip-flops or registers, via combinational logic. These paths are crucial in ensuring proper data synchronization and flow across clock cycles, especially in pipelined circuits. Analyzing reg2reg paths ensures the circuit functions reliably.

### Clk2Reg Path

A **clock-to-register (clk2reg) path** refers to the connection between the clock signal and a register (flip-flop). This path ensures that the register reacts appropriately to clock events, allowing sequential logic to operate correctly.

## STA for the synthesized RISC-V Core:

Install openSTA

![Screenshot from 2024-10-28 22-37-16](https://github.com/user-attachments/assets/809e4293-f793-49c3-9b90-174bdaffaa86)



```
read_liberty /home/tanaya-mehta/OpenSTA/assignment10/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog /home/tanaya-mehta/OpenSTA/assignment10/rvmyth_net_list.v
link_design rvmyth

create_clock -name clk -period 9.35 [get_ports clk]
set_clock_uncertainty [expr 0.05 * 9.35] -setup [get_clocks clk]
set_clock_uncertainty [expr 0.08 * 9.35] -hold [get_clocks clk]
set_clock_transition [expr 0.05 * 9.35] [get_clocks clk]
set_input_transition [expr 0.08 * 9.35] [all_inputs]

report_checks -path_delay max
report_checks -path_delay min


```

![Screenshot from 2024-10-28 23-18-49](https://github.com/user-attachments/assets/df4a3883-40f0-4d99-a4b3-0d2c011dc0e1)

![Screenshot from 2024-10-28 23-20-06](https://github.com/user-attachments/assets/0c21aebc-05bd-4d25-9cdd-72464f644d8f)

![Screenshot from 2024-10-28 23-17-48](https://github.com/user-attachments/assets/538fc426-7b3f-4c5b-bce9-d405b0882e38)




