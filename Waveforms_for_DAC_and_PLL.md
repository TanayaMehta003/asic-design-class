# Generating Waveforms for DAC and PLL Peripherals on RISC-V Processor

## VSDBabySoC Overview

The **VSDBabySoC** is a small but robust System on Chip (SoC) built around the **RISC-V architecture**. It is specifically designed to integrate and test three open-source IP cores together for the first time, with a focus on fine-tuning the analog components. The SoC features an **RVMYTH microprocessor**, an **8x Phase-Locked Loop (PLL)** for reliable clock generation, and a **10-bit Digital-to-Analog Converter (DAC)** for interfacing with external analog devices.

# BabySoC Simulation

Simulating and developing the entire micro-architecture of a RISC-V CPU is a challenging endeavor. For this simulation, we will concentrate on integrating two essential IP blocks: the Phase-Locked Loop (PLL) and the Digital-to-Analog Converter (DAC).

## Phase-Locked Loop (PLL)

A **Phase-Locked Loop (PLL)** is an electronic circuit that aligns the phase and frequency of its output signal with a reference signal. It consists of three core components:

- **Phase Detector**: Compares the phase of the reference signal with the output signal and generates an error signal based on their phase difference.
- **Loop Filter**: Smooths out the error signal to reduce noise and improve the stability of the system.
- **Voltage-Controlled Oscillator (VCO)**: Adjusts its output frequency in response to the filtered error signal, working to minimize the phase difference between the signals.

PLLs are widely utilized in applications like clock generation, frequency synthesis, and data recovery within communication systems.

## Digital-to-Analog Converter (DAC)

A **Digital-to-Analog Converter (DAC)** converts digital signals, typically in binary form, into analog signals such as voltage or current. This conversion is essential in systems where digital information must interface with analog devices or be presented in a format understandable by humans, such as audio or video outputs.

DACs are commonly employed in a variety of applications, including audio playback, video display, and signal processing.

1. Clone the given repo: https://github.com/Subhasis-Sahu/BabySoC_Simulation.git using the below command.
```
git clone https://github.com/Subhasis-Sahu/BabySoC_Simulation.git
```
```bash
cd BabySoC_Simulation
```
![image](https://github.com/user-attachments/assets/9f4509fd-0efa-4712-824b-122dae4a1b44)

2. Udate the `rvmyth.v` file from the previous labs into existing folder Edit the clock name appended with your name in vsdbabysoc.v.

3.Commands used to run the rvmyth.v file
```bash
iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/
```
4. Run the following commands:
   ```
   ./pre_synth_sim.out
   gtkwave pre_synth_sim.vcd

   ```
![image](https://github.com/user-attachments/assets/b7ea917b-8aa9-4037-bbb2-3e8e588d2822)

## Waveform

![image](https://github.com/user-attachments/assets/f1aaffd4-039c-43a2-8aec-96c23a62fb22)

