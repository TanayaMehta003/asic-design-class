# Synthesize RISC-V and Compare Output with Functional Simulations



## Steps before Synthesizing the RISC-V Core

1. **Copy the `src` Folder:**  
   Transfer the `src` folder from the **VSDBabySoC** directory to the **ASIC** directory.

2. **Navigate to the Target Directory:**  
   Change to the appropriate directory where the synthesis will be performed. Use the following command:

``` 
 cd /Desktop/ASIC/sky130RTLDesignAndSynthesisWorkshop
```

![Screenshot from 2024-10-24 02-42-53](https://github.com/user-attachments/assets/200ad7ad-b04d-4e55-b3d0-13f87f1d8e9b)
![Screenshot from 2024-10-24 02-45-57](https://github.com/user-attachments/assets/4a4940c0-fbaa-4984-8069-da429a21b729)

3.**Run Pre-Synthesis Simulation:**
    Execute the simulation on the design prior to synthesis using the following command:
    
  ```
    cd VSDBabySoC  
   iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/  
   ./pre_synth_sim.out  
   gtkwave pre_synth_sim.vcd
```

![Screenshot from 2024-10-24 03-36-49](https://github.com/user-attachments/assets/fcab4e06-60f4-4386-b137-e733e9ce42f0)
![Screenshot from 2024-10-24 11-44-26](https://github.com/user-attachments/assets/d47c8a69-e750-4b63-b777-9d9a204a0cc2)


## Steps for Synthesizing the RISC-V Core

1. **Navigate to the Target Directory:**
```
cd /Desktop/ASIC/sky130RTLDesignAndSynthesisWorkshop/src/module
```
 2. **Synthesis:**
Run the following commands for synthesis
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog clk_gate.v
read_verilog rvmyth.v
synth -top rvmyth
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr rvmyth_net.v
!gvim rvmyth_net.v
```
![Screenshot from 2024-10-24 11-36-48](https://github.com/user-attachments/assets/05913a5b-464c-4995-8b30-9778bee6eae1)

![Screenshot from 2024-10-24 03-19-03](https://github.com/user-attachments/assets/646f13a0-0989-4195-a235-adfea8c50e27)

Netlist:
![Screenshot from 2024-10-24 11-31-33](https://github.com/user-attachments/assets/641bddce-2fd8-4383-9a02-9892d330d44d)

![Screenshot from 2024-10-24 03-21-08](https://github.com/user-attachments/assets/3789c276-f5d6-4b06-a4f5-870adf77d921)

3. **Simulate the Synthesized Design:**
Run the following commands:
```
   iverilog ../../my_lib/verilog_model/primitives.v ../../my_lib/verilog_model/sky130_fd_sc_hd.v rvmyth.v testbench.v vsdbabysoc.v avsddac.v avsdpll.v clk_gate.v  
   ./a.out  
   gtkwave dump.vcd
```
![Screenshot from 2024-10-24 03-33-01](https://github.com/user-attachments/assets/c086c985-49a5-4dce-9ce0-467ef233021a)
![Screenshot from 2024-10-24 11-33-51](https://github.com/user-attachments/assets/7a23bee9-51b6-40fe-8694-1ed81737b839)

We can see that pre-synthesis simulation and post-synthesis simulation, show the same results. Hence, verifying o1=o2.

