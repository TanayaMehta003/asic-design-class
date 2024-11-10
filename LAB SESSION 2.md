2. [TASK-2](#TASK-2)

# TASK-2

## AIM

Compile sum1ton.c into sum1ton.o for RISC-V with -Ofast optimization, execute sum1ton.o using Spike, and run sum1ton.o on Spike in debug mode to observe register values.

## TOOLS:

GCC (GNU Compiler Collection), RISC-V GCC Compiler, Spike Simulator, Ubuntu OS

## STEPS:

- **STEP 1:** Compile a C source file (sum1ton.c) into an object file (sum1ton.o) for the RISC-V architecture, on -Ofast and O1 levels of optimization.
  **###CASE 1: -Ofast level***
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
  - To go to next line of assembly code press Enter and then use the below query to verify the data in the register a0 and register sp before and after execution:
    ```bash
    reg 0 a0
    reg 0 sp
    ```
- **Output:**
   
    ![OUTPUT3](https://github.com/user-attachments/assets/0ff08437-858f-4869-a317-29027455960f)

  **###CASE 1: -O1 level***
 ```bash
    riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sumton.o sumton.c
 ```

 - Query to get object dump
 ```bash
    riscv64-unknown-elf-objdump -d sumton.o | less
 ```
- Screenshot of assembly code
 
  ![Screenshot 2024-07-28 105351](https://github.com/user-attachments/assets/80bebee1-4e6b-469a-838d-2bc3638bacd6)

- **Step 2:** Execute the compiled RISC-V object file (sum1ton.o) using Spike.
  ```bash
    spike pk sumton.o
  ```
- **Output:**
  
![Screenshot 2024-07-28 105804](https://github.com/user-attachments/assets/62d60dcc-3af9-4051-a384-589b01c8b403)

- **Step 3:** Run the assembly code in sum1ton.o on the Spike simulator in debug mode inorder to observe the register values.
   ```bash
    spike -d pk sumton.o
    ```
- **Output:**

![Screenshot 2024-07-28 110506](https://github.com/user-attachments/assets/c0dae508-f6f4-4f56-98e7-789ad0d1ac48)

- **Run the following Commands and Observe the Register Values:**
  - To go to next line of assembly code press Enter and then use the below query to verify the data in the register a0 and register sp before and after execution:
    ```bash
       reg 0 sp
    ```
- **Output:**
   
![Screenshot 2024-07-28 110506](https://github.com/user-attachments/assets/c0dae508-f6f4-4f56-98e7-789ad0d1ac48)

##Observation: Here we can observe that the number of instructions are reduced in o1 level to 9 as compared to 12 in the -ofast level.

