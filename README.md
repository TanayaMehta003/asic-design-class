# asic-design-class

## CONTENTS

1. [Task 1](#task-1)
2. [TASK-2](#TASK-2)
3. 
## **TASK 1:**

### **Compiling the C program using GCC and RISC-V**

- Execute a C code that calculates the sum of numbers upto 23 is run on terminal of virtual box as discussed.

### **Code snippet:**


![code](https://github.com/user-attachments/assets/1ee03da1-e00b-46c9-a604-a10a475dadb7)


### **The results are displayed as shown below:**


![1 1](https://github.com/user-attachments/assets/1145d88b-5c94-4679-92c2-1a2d1ef4d7bb)


## **TASK 2:**
### **Compile and Verify C Code using RISC-V GNU Compiler Toolchain**

- **CASE 1: O1**

Compile using RISCV gcc compiler and run using emulator as shown:

![2 11](https://github.com/user-attachments/assets/2bcf76c7-2c62-4c78-8a79-4b755bd7fc9c)

  - **Output:**

![2 8](https://github.com/user-attachments/assets/27ba1e93-9651-4404-9c8b-5e566ca3fd3f)


- **CASE 2: OFAST**


Compilation in this case gets optimised.


 - **Output:**


![2 10](https://github.com/user-attachments/assets/d060345c-7af3-4804-8b4b-2b47833c38f5)






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



