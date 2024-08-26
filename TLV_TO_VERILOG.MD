
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

This outlines a straightforward approach for converting TL-Verilog code and validating it through Verilog simulation.
