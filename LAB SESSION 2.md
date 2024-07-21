## AIM

Compile sum1ton.c into sum1ton.o for RISC-V with -Ofast optimization, execute sum1ton.o using Spike, and run sum1ton.o on Spike in debug mode to observe register values.

## TOOLS:

GCC (GNU Compiler Collection), RISC-V GCC Compiler, Spike Simulator, Ubuntu OS

## STEPS:

- **STEP 1:** Compile a C source file (sum1ton.c) into an object file (sum1ton.o) for the RISC-V architecture, on -Ofast levels of optimization.
 ```bash
    riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sumton.o sumton.c
 ```

 - Query to get object dump
 ```bash
    riscv64-unknown-elf-objdump -d sumton.o | less
 ```
- Screenshot of assembly code
 
  ![2 10](https://github.com/user-attachments/assets/6d0da0aa-bcb3-41af-819f-621fa7ee2d38)

- **Step 2:** Execute the compiled RISC-V object file (sum1ton.o) using Spike.
  ```bash
    spike pk sumton.o
  ```
- **Output:**
  
 ![OUTPUT1](https://github.com/user-attachments/assets/5674491f-8685-4c44-8df7-4cac1321d6a2)

- **Step 3:** Run the assembly code in sum1ton.o on the Spike simulator in debug mode inorder to observe the register values.
   ```bash
    spike -d pk sumton.o
    ```
- **Output:**

 ![OUTPUT2](https://github.com/user-attachments/assets/34665bb1-aea4-4e5f-8866-0446033972a3)

- **Run the following Commands and Observe the Register Values:**
    - To go to next line of assembly code press Enter.
    - Use the following command to verify the data in the register a0 and register sp before and after execution:
    ```bash
    reg 0 a0
    reg 0 sp
    ```
- **Output:**
   
    ![OUTPUT3](https://github.com/user-attachments/assets/0ff08437-858f-4869-a317-29027455960f)



