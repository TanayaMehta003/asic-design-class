
# Converting TLV to Verilog with Sandpiper-SaaS Compiler

This guide provides instructions on converting TLV code to Verilog and running pre-synthesis simulations using the GTKWave tool to verify the design.

## Steps

### 1. Install Necessary Packages
Start by installing the required packages:

```bash
sudo apt install make python python3 python3-pip git iverilog gtkwave
sudo apt-get install python3-venv
python3 -m venv .venv
source ~/.venv/bin/activate
pip3 install pyyaml click sandpiper-saas
```

### 2. Clone the Repository
Download the VSDBabySoC design files and testbench by cloning the GitHub repository, then navigate to the project directory:

```bash
git clone https://github.com/manili/VSDBabySoC.git
cd VSDBabySoC
```
![image](https://github.com/user-attachments/assets/83f3bb63-c331-4a48-ab3e-8539feb6fcd6)

### 3. Replace the `rvmyth.tlv` File
In the `VSDBabySoC` directory, navigate to `/home/vsduser/VSDBabySoC` and replace the existing `rvmyth.tlv` file with your own.

### 4. Convert `.tlv` to `.v` using Sandpiper-SaaS
The TL-Verilog (`.tlv`) code needs to be converted to Verilog (`.v`). Run the following command:

```bash
sandpiper-saas -i /home/vsduser/VSDBabySoC/tanaya_rvmyth.tlv -o tanaya_rvmyth.v --bestsv --noline -p verilog --outdir /home/vsduser/VSDBabySoC/
```

![image](https://github.com/user-attachments/assets/af068206-ee44-4fb2-8813-a1e60b4334c6)

### 5. Generate Pre-Synthesis Simulation (`pre_synth_sim.vcd`)
To create the simulation waveform file, run:

```bash
make pre_synth_sim
```

The output, `pre_synth_sim.vcd`, will be located in the `output/pre_synth_sim` directory.

### 6. Compile and Simulate the RISC-V Design
To compile and simulate the VSDBabySoC design, run:

```bash
iverilog -o output/pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module
cd output
./pre_synth_sim.out
```

This generates the `pre_synth_sim.vcd` file.

### 7. Open the Simulation File in GTKWave
Open the waveform file using GTKWave:

```bash
gtkwave pre_synth_sim.vcd
```

## Key Signals in the Diagram

- **clk_tan**: Clock input to the RISC-V core.
- **reset**: Input reset signal to the RISC-V core.
- **OUT[9:0]**: 10-bit output port of the RISC-V core.

---
![image](https://github.com/user-attachments/assets/6fc29cb4-9477-4d1a-8a07-3c7fbb70827d)

![image](https://github.com/user-attachments/assets/8c75fbb3-a9bc-47ab-a0c2-b48b1fd5cf82)

This outlines a straightforward approach for converting TL-Verilog code and validating it through Verilog simulation.

## Waveforms from Makerchip platform IDE by running .tlv file for comparison

As shown in the screenshot, the output of the sum 1 to 9 program is observed in register r10, which holds the value 45. It can be observed that the CPU took 56 cycles to execute the program for calculating the sum of numbers from 1 to 9.

![image](https://github.com/user-attachments/assets/659127fe-b039-4497-97f0-5150ce277b19)

The following shows the sum on waveform:

![image](https://github.com/user-attachments/assets/af1a3a62-6e69-406a-b474-97a34a982ab1)


The following screenshot shows the reset signal

![image](https://github.com/user-attachments/assets/9c9c0ef7-f299-43e9-a29a-2475d3c77f79)


