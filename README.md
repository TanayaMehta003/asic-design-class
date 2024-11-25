# asic-design-class

## CONTENTS

1. [TASK-1](#task-1)
2. [TASK-2](#TASK-2)
3. [TASK-3](#TASK-3)
4. [TASK-4](#TASK-4)
5. [TASK-5](#TASK-5)
6. [TASK-6](#TASK-6)
7. [TASK-7](#TASK-7)
8. [TASK-8](#TASK-8)
9. [TASK-9](#TASK-9)
10. [TASK-10](#TASK-10)
11. [TASK-11](#TASK-11)
12. [TASK-12](#TASK-12)
13. [TASK-13](#TASK-13)
# **TASK 1:**

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


# TASK-3

# Lab session 3

# Identifying Instruction Types

In this activity, we identify instruction types based on the provided instructions. The 32-bit code helps in this identification process, with each instruction type having its own format.

## What are Instruction Formats in RISC-V?

Instruction formats in RISC-V act as a "contract" between the assembly language and the hardware. When the assembly language executes an instruction, the hardware knows exactly how to handle it. These formats, composed of sequences of 0s and 1s, define the type of operation, the location of data, and more. RISC-V has six types of instruction formats:

### R Type

- **Purpose**: Used for arithmetic and logical operations involving three registers.
- **Structure**: Consists of two source registers, one destination register, a function code for the operation, and an opcode.
- **Examples**: ADD, SUB, OR, XOR, etc.
- **Format**:
  - `func7` (7 bits): Function code for additional differentiation.
  - `rs2` (5 bits): Second source register.
  - `rs1` (5 bits): First source register.
  - `func3` (3 bits): Primary function code.
  - `rd` (5 bits): Destination register.
  - `opcode` (7 bits): Basic operation code (e.g., 0110011 for integer operations).

The instruction format is as follows:
![rtype](https://github.com/user-attachments/assets/eb798598-352d-4120-8f51-8f5ed6c0ac6a)

### I Type

- **Purpose**: Handles operations with an immediate value and one or two registers, such as arithmetic, load operations, and certain branches.
- **Format**:
  - `immediate` (12 bits): Immediate value for operations.
  - `rs1` (5 bits): Source register.
  - `funct3` (3 bits): Instruction differentiation code.
  - `rd` (5 bits): Destination register.
  - `opcode` (7 bits): Basic operation code.

The instruction format is as follows:
![itype](https://github.com/user-attachments/assets/fad5185b-47ef-45b6-b0b1-aa65cc9490dd)

### S Type

- **Purpose**: Used for store operations, transferring data from a register to memory.
- **Format**:
  - `imm[11:5]` (7 bits): Upper 7 bits of the immediate value.
  - `rs2` (5 bits): Data source register.
  - `rs1` (5 bits): Base address register.
  - `func3` (3 bits): Instruction differentiation code.
  - `imm[4:0]` (5 bits): Lower 5 bits of the immediate value.
  - `opcode` (7 bits): Basic operation code.

The instruction format is as follows:
![stype](https://github.com/user-attachments/assets/74bc4565-925a-419e-ae46-516b840feca0)

### B Type

- **Purpose**: Executes conditional branch operations based on register comparisons.
- **Format**:
  - `imm[12]` (1 bit): 12th bit of the immediate value.
  - `imm[10:5]` (6 bits): 10th to 5th bits of the immediate value.
  - `rs2` (5 bits): Second source register.
  - `rs1` (5 bits): First source register.
  - `func3` (3 bits): Instruction differentiation code.
  - `imm[4:1]` (4 bits): 4th to 1st bits of the immediate value.
  - `imm[11]` (1 bit): 11th bit of the immediate value.
  - `opcode` (7 bits): Basic operation code.

The instruction format is as follows:
![btype](https://github.com/user-attachments/assets/eb8ac4cd-1676-4e75-b7bf-7f33727a9427)

### U Type

- **Purpose**: For operations with large immediate values, like loading upper immediate values or address computations.
- **Format**:
  - `immediate[31:12]` (20 bits): Upper 20 bits of the immediate value.
  - `rd` (5 bits): Destination register.
  - `opcode` (7 bits): Operation code.
  - Note: Immediate value occupies the upper 20 bits of a 32-bit word; lower 12 bits are zero in calculations.

The instruction format is as follows:
![utype](https://github.com/user-attachments/assets/3fd90c56-54e9-4bc8-9e10-faf9c03b23d5)

### J Type

- **Purpose**: Manages jump operations, altering program control flow.
- **Format**:
  - `imm[20]` (1 bit): 20th bit of the immediate value.
  - `imm[10:1]` (10 bits): 10th to 1st bits of the immediate value.
  - `imm[11]` (1 bit): 11th bit of the immediate value.
  - `imm[19:12]` (8 bits): 19th to 12th bits of the immediate value.
  - `rd` (5 bits): Register for storing the return address.
  - `opcode` (7 bits): Operation code.

The instruction format is as follows:
![jtype](https://github.com/user-attachments/assets/f73f30b2-6e50-4c79-b444-145c819b8694)

# Analyzing the provided instruction types:

1. **ADD r7, r8, r9**

   - **Opcode for ADD**: `0110011`
   - **rd**: `r7 = 00111`
   - **rs1**: `r8 = 01000`
   - **rs2**: `r9 = 01001`
   - **func3**: `000`
   - **func7**: `0000000`
   - **R Type**
   - **32 Bit Instruction**: `0000000_01001_01000_000_00111_0110011`

2. **SUB r9, r7, r8**

   - **Opcode for SUB**: `0110011`
   - **rd**: `r9 = 01001`
   - **rs1**: `r7 = 00111`
   - **rs2**: `r8 = 01000`
   - **func3**: `000`
   - **func7**: `0100000`
   - **R Type**
   - **32 Bit Instruction**: `0100000_01000_00111_000_01001_0110011`

3. **AND r8, r7, r9**

   - **Opcode for AND**: `0110011`
   - **rd**: `r8 = 01000`
   - **rs1**: `r7 = 00111`
   - **rs2**: `r9 = 01001`
   - **func3**: `111`
   - **func7**: `0000000`
   - **R Type**
   - **32 Bit Instruction**: `0000000_01001_00111_111_01000_0110011`

4. **OR r8, r8, r5**

   - **Opcode for OR**: `0110011`
   - **rd**: `r8 = 01000`
   - **rs1**: `r8 = 01000`
   - **rs2**: `r5 = 00101`
   - **func3**: `110`
   - **func7**: `0000000`
   - **R Type**
   - **32 Bit Instruction**: `0000000_00101_01000_110_01000_0110011`

5. **XOR r8, r7, r4**

   - **Opcode for XOR**: `0110011`
   - **rd**: `r8 = 01000`
   - **rs1**: `r7 = 00111`
   - **rs2**: `r4 = 00100`
   - **func3**: `100`
   - **func7**: `0000000`
   - **R Type**
   - **32 Bit Instruction**: `0000000_00100_00111_100_01000_0110011`

6. **SLT r10, r2, r4**

   - **Opcode for SLT**: `0110011`
   - **rd**: `r10 = 01010`
   - **rs1**: `r2 = 00010`
   - **rs2**: `r4 = 00100`
   - **func3**: `010`
   - **func7**: `0000000`
   - **R Type**
   - **32 Bit Instruction**: `0000000_00100_00010_010_01010_0110011`

7. **ADDI r12, r3, 5**

   - **Opcode for ADDI**: `0010011`
   - **rd**: `r12 = 01100`
   - **rs1**: `r3 = 00011`
   - **immediate**: `000000000101`
   - **func3**: `000`
   - **I Type**
   - **32 Bit Instruction**: `000000000101_00011_000_01100_0010011`

8. **SW r3, r1, 4**

   - **Opcode for SW**: `0100011`
   - **rs1**: `r1 = 00001`
   - **rs2**: `r3 = 00011`
   - **immediate**: `000000000100`
   - **func3**: `010`
   - **S Type**
   - **32 Bit Instruction**: `0000000_00011_00001_010_00000_0100011`

9. **SRL r16, r11, r2**

   - **Opcode for SRL**: `0110011`
   - **rd**: `r16 = 10000`
   - **rs1**: `r11 = 01011`
   - **rs2**: `r2 = 00010`
   - **func3**: `101`
   - **func7**: `0000000`
   - **R Type**
   - **32 Bit Instruction**: `0000000_00010_01011_101_10000_0110011`

10. **BNE r0, r1, 20**

    - **Opcode for BNE**: `1100011`
    - **rs1**: `r0 = 00000`
    - **rs2**: `r1 = 00001`
    - **immediate**: `000000010100`
    - **func3**: `001`
    - **B Type**
    - **32 Bit Instruction**: `0000000_00001_00000_001_00010_1100011`

11. **BEQ r0, r0, 15**

    - **Opcode for BEQ**: `1100011`
    - **rs1**: `r0 = 00000`
    - **rs2**: `r0 = 00000`
    - **immediate**: `000000001111`
    - **func3**: `000`
    - **B Type**
    - **32 Bit Instruction**: `0000000_00000_00000_000_00011_1100011`

12. **LW r13, r11, 2**

    - **Opcode for LW**: `0000011`
    - **rd**: `r13 = 01101`
    - **rs1**: `r11 = 01011`
    - **immediate**: `000000000010`
    - **func3**: `010`
    - **I Type**
    - **32 Bit Instruction**: `000000000010_01011_010_01101_0000011`

13. **SLL r15, r11, r2**

    - **Opcode for SLL**: `0110011`
    - **rd**: `r15 = 01111`
    - **rs1**: `r11 = 01011`
    - **rs2**: `r2 = 00010`
    - **func3**: `001`
    - **func7**: `0000000`
    - **R Type**
    - **32 Bit Instruction**: `0000000_00010_01011_001_01111_0110011`

Thus, each instruction has been associated with its respective type, and its 32-bit layout has been designed according to its format.

## Executing assembly instructions based on a given Verilog code in a RISC-V processor.

Below are the bit patterns and the corresponding ISA for the given Verilog code and instructions.

| Operation  | Hardcoded ISA | Bit Pattern                        |
|------------|---------------|------------------------------------|
| ADD R6, R1, R2 | 32'h02208300 | 0000001 00010 00001 000 00110 0000000 |
| SUB R7, R1, R2 | 32'h02209380 | 0000001 00010 00001 001 00111 0000000 |
| AND R8, R1, R3 | 32'h0230a400 | 0000001 00011 00001 010 01000 0000000 |
| OR R9, R2, R5  | 32'h02513480 | 0000001 00101 00010 011 01001 0000000 |
| XOR R10, R1, R4 | 32'h0240c500 | 0000001 00100 00001 100 01010 0000000 |
| SLT R1, R2, R4 | 32'h02415580 | 0000001 00100 00010 101 01011 0000000 |
| ADDI R12, R4, 5 | 32'h00520600 | 000000000101 00100 000 01100 0000000 |
| BEQ R0, R0, 15 | 32'h00f00002 | 0 000000 01111 00000 000 0000 0 0000010 |
| SW R3, R1, 2   | 32'h00209181 | 0000000 00010 00001 001 00011 0000001 |
| LW R13, R1, 2  | 32'h00208681 | 000000000010 00001 000 01101 0000001 |
| SRL R16, R14, R2 | 32'h00271803 | 0000000 00010 01110 001 10000 0000011 |
| SLL R15, R1, R2 | 32'h00208783 | 0000000 00010 00001 000 01111 0000011 |

### Custom RISC-V Instructions

| Operation        | Type | RISCV ISA | Bit Pattern                        |
|------------------|------|---------------|------------------------------------|
| ADD r6, r7, r8   | R    | 32'h00838033  | 0000000 01000 00111 000 00110 0110011 |
| SUB r8, r6, r7   | R    | 32'h40E302B3  | 0100000 00111 00110 000 01000 0110011 |
| AND r7, r6, r8   | R    | 32'h008373B3  | 0000000 01000 00110 111 00111 0110011 |
| OR r8, r7, r5    | R    | 32'h0053E2B3  | 0000000 00101 00111 110 01000 0110011 |
| XOR r8, r6, r4   | R    | 32'h004322B3  | 0000000 00100 00110 100 01000 0110011 |
| SLT r10, r2, r4  | R    | 32'h004112B3  | 0000000 00100 00010 010 01010 0110011 |
| ADDI r12, r3, 5  | I    | 32'h00518193  | 000000000101 00011 000 01100 0010011  |
| SW r3, r1, 4     | S    | 32'h00312223  | 0000000 00011 00001 010 00100 0100011 |
| SRL r16, r11, r2 | R    | 32'h0025D833  | 0000000 00010 01011 101 10000 0110011 |
| BNE r0, r1, 20   | B    | 32'h0010A463  | 0000000 00001 00000 001 01010 1100011 |
| BEQ r0, r0, 15   | B    | 32'h00007C63  | 0000000 00000 00000 000 01111 1100011 |
| LW r13, r11, 2   | I    | 32'h0025A193  | 000000000010 01011 010 01101 0000011  |
| SLL r15, r11, r2 | R    | 32'h0025B933  | 0000000 00010 01011 001 01111 0110011 |

###  Implementaion through verilog.

1. Compile the Verilog Code using the below command

 ```bash
 iverilog -o iiitb_rv32i iiitb_rv32i.v iiitb_rv32i_tb.v
 ```
2. Run this command to execute the test bench and generate a .vcd file:
 ```bash
  vvp iiitb_rv32i_tb
 ```
3.View the Test Bench in GTKWave:
```bash
gtkwave iiitb_rv32i.vcd
```
  ### PFB the appropriate wafeforms of hardcoded ISA:

`ADD R6, R2, R1`
![Screenshot from 2024-07-30 00-19-28](https://github.com/user-attachments/assets/4ce41c79-5d4d-4278-b7c1-0eea74b51adc)

`SUB R7, R1, R2`
![Screenshot from 2024-07-30 00-22-00](https://github.com/user-attachments/assets/1b86b7c1-1594-44ad-963e-14831c774bca)

`AND R8, R1, R3`
![Screenshot from 2024-07-30 00-26-22](https://github.com/user-attachments/assets/877bdc98-f86e-40c4-8d5a-8365b0e64b5f)

`OR R9, R2, R5`
![Screenshot from 2024-07-30 00-29-43](https://github.com/user-attachments/assets/bd10f36b-7f3d-40c1-9f55-f9a94d3da25c)

`xor r10,r1,r4`
![Screenshot from 2024-07-30 00-30-53](https://github.com/user-attachments/assets/16d4d79b-b486-476c-a05a-d87db3d8c764)

`SLT R1, R2, R4`
![Screenshot from 2024-07-30 00-32-19](https://github.com/user-attachments/assets/5b82a335-31bd-4a92-bfc5-1c2611a1be4d)

`ADDI R12, R4, 5 `
![Screenshot from 2024-07-30 00-33-56](https://github.com/user-attachments/assets/f8b3a0e3-edfd-48d0-9a5f-11265f1e9db6)

`BEQ R0, R0, 15`
![Screenshot from 2024-07-30 00-35-59](https://github.com/user-attachments/assets/e3b8004f-90ad-45eb-920a-e03dce40d408)

`SW R3, R1, 2 `
![Screenshot from 2024-07-30 00-38-42](https://github.com/user-attachments/assets/131e9c90-ae9c-4620-8726-d97f518a8249)

`LW R13, R1, 2`
![Screenshot from 2024-07-30 00-40-03](https://github.com/user-attachments/assets/c55fcc30-e526-4052-8655-f6f63562798d)

We observe a variation between bit pattern of RISCV code and hardcoded ISA.


# TASK 4

# Carry_Look-Ahead-_Adder_RISCV


A carry-look ahead adder (CLA) or fast adder is a type of adder used in digital logic. A carry-look ahead adder improves speed by reducing the amount of time required to determine to carry bits. It calculates one or more carries before the sum, which reduces the wait time/Ripple delay to calculate the result of the larger value bits of the adder.

**The 4-bit carry look-ahead carry adder is shown in the figure given below:**

![CLA_1](https://github.com/user-attachments/assets/bf4728c5-288f-4080-a636-bd8c107ac929)


**The following shows the block diagram of 4-bit carry look-ahead adder:**

![BLOCK_DGM_1](https://github.com/user-attachments/assets/673adda9-a045-481e-a10b-e870135fec14)


**The below shows two-level logic circuit diagram of a carry look ahead adder:**

![ckt_dgm_1](https://github.com/user-attachments/assets/5edca1a7-34ec-46dd-9dab-fed9845275b6)

## **C-CODE**

 ```bash
#include <stdio.h>
#include <stdlib.h>

// Function to read a single character
int getch(void) {
    return getchar();
}

// Function to get a positive integer from the user
int get1(int a) {
    char ch = 'B';
    if (a == 1) {
        ch = 'A';
    }
    
    do {
        printf("\n\tENTER VALUE OF %c: ", ch);

        // Read integer from user and check if input is valid
        if (scanf("%d", &a) != 1) {
            // Clear the input buffer if input is invalid
            while (getchar() != '\n');
            printf("Invalid input. Please enter a positive integer.\n");
            a = -1; // Repeat the loop
        } else if (a <= 0) {
            printf("The number must be greater than zero. Try again.\n");
            a = -1; // Repeat the loop
        }
    } while (a <= 0);

    return a;
}

// Function to perform a logical AND operation
int and(int a, int b) {
    return (a < b) ? a : b;
}

// Function to perform a logical OR operation
int or(int a, int b) {
    return (a > b) ? a : b;
}

// Function to perform an exclusive OR (XOR) operation
int exor(int a, int b) {
    return (a == b) ? 0 : 1;
}

// Function to add two numbers using binary addition with carry
void add() {
    int i, A, B, a, b, cin, num;
    int n1[8] = {0}, n2[8] = {0}, cg[8] = {0}, cp[8] = {0}, sum[8] = {0};

    // Get two positive integers from the user
    A = a = get1(1);
    B = b = get1(0);

    // Convert the integers to binary and store them in arrays
    i = 7;
    do {
        n1[i] = a % 2;
        a = a / 2;
        n2[i] = b % 2;
        b = b / 2;
        i--;
    } while ((a != 0) || (b != 0));

    // Display binary representation of the numbers
    printf("\n\t\t Binary Form");
    printf("\n\t A = %d : ", A);
    for (i = 0; i < 8; i++) {
        printf("%d ", n1[i]);
    }
    printf("\n\t B = %d : ", B);
    for (i = 0; i < 8; i++) {
        printf("%d ", n2[i]);
    }

    // Perform binary addition
    cin = 0;
    for (i = 7; i >= 0; i--) {
        sum[i] = exor(cin, exor(n1[i], n2[i])); // Calculate sum
        cg[i] = and(n1[i], n2[i]); // Calculate carry generate
        cp[i] = or(n1[i], n2[i]); // Calculate carry propagate
        cin = or(cg[i], and(cp[i], cin)); // Update carry in
    }

    // Display the sum
    printf("\n\n\t\t SUM: ");
    num = 0;
    for (i = 0; i < 8; i++) {
        printf(" %d", sum[i]);
        num += sum[i] * (1 << (7 - i)); // Convert binary to decimal
    }
    printf("\n\n\t\t SUM: %d + %d = %d\n", A, B, num);
    printf("\t\t The Carry Is: %d\n\n", cin);
}

int main() {
    int ch;

    while (1) {
        // Display the menu
        printf("*** MENU FOR LOOK AHEAD CARRY ADDER ***");
        printf("\n\t\t1. ADDITION OF TWO NUMBERS");
        printf("\n\t\t2. EXIT\n");
        printf("*");
        printf("\n\t\tEnter Your Option: ");

        // Read the user's choice and check if input is valid
        if (scanf("%d", &ch) != 1) {
            // Clear the input buffer if input is invalid
            while (getchar() != '\n');
            printf("Invalid input. Please enter a number.\n");
            continue; // Skip to the next iteration of the loop
        }

        // Process the user's choice
        switch (ch) {
            case 1:
                add(); // Call the addition function
                printf("\nPress any key to continue...");
                getch(); // Wait for a key press
                break;

            case 2:
                exit(0); // Exit the program
                break;

            default:
                printf("ERROR!!!!!!!!! INVALID ENTRY...\n");
                printf("Back To Main Menu\n\n");
                printf("\nPress any key to continue...");
                getch(); // Wait for a key press
                break;
        }
    }

    return 0;
}
```
## **Compilation of the C-program with GCC compiler:**

```bash
gcc -Ofast -o cla cla.c
./cla
```

![Screenshot 2024-08-14 184029](https://github.com/user-attachments/assets/2256e92a-3255-4911-9835-47b4c45e9c13)

## **Compilation of the C-program with RISC-V GCC compiler:**

```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o cla.o cla.c
spike pk cla.o
```
![Screenshot 2024-08-17 121035](https://github.com/user-attachments/assets/14e21496-933f-44a7-9f66-6257adfa4319)

## **Results**

Results when compared between the output from both GCC and RISC-V compiler are same, which is expected.

## **Creating the Objdump file**

```bash
riscv64-unknown-elf-objdump -d cla.o | less
```

## **Assembly instructions from RISC-V GCC compiler**

```bash
cla.o:     file format elf64-littleriscv


Disassembly of section .text:

00000000000100b0 <main>:
   100b0:       f8010113                addi    sp,sp,-128
   100b4:       06813823                sd      s0,112(sp)
   100b8:       06913423                sd      s1,104(sp)
   100bc:       07213023                sd      s2,96(sp)
   100c0:       05313c23                sd      s3,88(sp)
   100c4:       05413823                sd      s4,80(sp)
   100c8:       05513423                sd      s5,72(sp)
   100cc:       05613023                sd      s6,64(sp)
   100d0:       03713c23                sd      s7,56(sp)
   100d4:       03813823                sd      s8,48(sp)
   100d8:       03913423                sd      s9,40(sp)
   100dc:       03a13023                sd      s10,32(sp)
   100e0:       01b13c23                sd      s11,24(sp)
   100e4:       06113c23                sd      ra,120(sp)
   100e8:       0002bbb7                lui     s7,0x2b
   100ec:       0002bb37                lui     s6,0x2b
   100f0:       0002bab7                lui     s5,0x2b
   100f4:       0002ba37                lui     s4,0x2b
   100f8:       0002b9b7                lui     s3,0x2b
   100fc:       0002b937                lui     s2,0x2b
   10100:       00100493                li      s1,1
   10104:       00a00413                li      s0,10
   10108:       0002bd37                lui     s10,0x2b
   1010c:       0002bcb7                lui     s9,0x2b
   10110:       00200c13                li      s8,2
   10114:       0002bdb7                lui     s11,0x2b
   10118:       6d8b8513                addi    a0,s7,1752 # 2b6d8 <__clzdi2+0x148>
   1011c:       35d000ef                jal     ra,10c78 <printf>
   10120:       700b0513                addi    a0,s6,1792 # 2b700 <__clzdi2+0x170>
:
```

**Note:** All the instructions have been generated by compiling in the RISC-V GCC compiler using the 'OFast' flag.

# TASK 5

### Makerchip and TL-Verilog introduction:

Makerchip utilizes the Transaction-Level Verilog (TL-Verilog) standard, which marks a major improvement by eliminating the need for outdated features of traditional Verilog and introducing a more concise syntax.
TL-Verilog boosts design productivity by incorporating robust constructs for pipelines and transactions, simplifying the development of complex digital circuits.

### Combinational Circuits in TL-Verilog

Starting with a basic example in combinational logic, an inverter is a good starting point. In TL-Verilog, the logic for an inverter can be expressed simply as $out = !$in;. Unlike traditional Verilog, there is no need to declare $out and $in. Additionally, there’s no need to assign values to $in since random stimulus is automatically generated, producing a warning.

Below is the screenshot of the combinational calculator.

![gates ](https://github.com/user-attachments/assets/3910e5b7-8cd2-4a41-b64e-dbb6f7a0f6c9)

### Launching makerchip IDE

[Try Makerchip Sandbox](https://makerchip.com/sandbox/#)

### Combinational calculator

```bash
\m4_TLV_version 1d: tl-x.org
\SV

   // =========================================
   // Welcome!  Try the tutorials via the menu.
   // =========================================

   // Default Makerchip TL-Verilog Code Template
   
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
   $reset = *reset;

   $val1 [31:0] = $rand1[3:0];
   $val2 [31:0] = $rand2[3:0];
   
   $sum [31:0] = $val1 + $val2;
   $diff[31:0] = $val1 - $val2;
   $prod[31:0] = $val1 * $val2;
   $quot[31:0] = $val1 / $val2;
   
   $out [31:0] = ($op[0] ? $sum : ($op[1] ? $diff : ($op[2] ? $prod : $quot ))) ;
                 
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
   endmodule
```


![Screenshot 2024-08-21 130613](https://github.com/user-attachments/assets/ed8b7868-d0a9-4ff2-a6e2-67ce0ce5d00d)

### Sequential Calculator

Calculators typically retain the previous result and apply it in the next operation. The sequential calculator follows this approach by feeding the output back as the input for the subsequent calculation. The corresponding code is shown below:

```bash
\m5_TLV_version 1d: tl-x.org
\m5
   
   // =================================================
   // Welcome!  New to Makerchip? Try the "Learn" menu.
   // =================================================
   
   //use(m5-1.0)   /// uncomment to use M5 macro library.
\SV
   // Macro providing required top-level module definition, random
   // stimulus support, and Verilator config.
   m5_makerchip_module   // (Expanded in Nav-TLV pane.)
	
\TLV
   //$count[31:0] = 32'b0;
   
   // Sequential Clock
   
   |calc
      @1
         $clk_tan = *clk;
         $reset = *reset;
         $val1[31:0] = >>1$result[31:0];
         $val2[31:0] = $rand2[3:0];
         $result[31:0] = $reset ? 32'b0 : ($sel[1:0] == 2'b00)
                         ? ($val1[31:0] + $val2[31:0]) : ($sel[1:0] == 2'b01)
                         ? ($val1[31:0] - $val2[31:0]) : ($sel[1:0] == 2'b10)
                         ? ($val1[31:0] * $val2[31:0]) : ($sel[1:0] == 2'b11)
                         ? ($val2[31:0] != 0 ? ($val1[31:0] / $val2[31:0]) : 32'bx) :  32'b0;
         //$count[31:0] = $reset  ? 0 : (>>1$count + 1);
   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
\SV
	endmodule;

```

Below is the waveform and block diagram:-

![Screenshot 2024-08-21 122845](https://github.com/user-attachments/assets/5ea4c793-eb29-4209-9042-3ead488799ae)

### Pipelined logic

Timing abstraction is a powerful feature of TL-Verilog that allows easy conversion of code into pipeline stages. The entire code is placed under a |pipe scope, with stages defined using @?.

Cycle_Calculator.tlv
```bash
\m4_TLV_version 1d: tl-x.org
\SV
  
   m4_include_lib(['https://raw.githubusercontent.com/stevehoover/RISC-V_MYTH_Workshop/bd1f186fde018ff9e3fd80597b7397a1c862cf15/tlv_lib/calculator_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)

\TLV
   |calc
      @1
         $clk_tan = *clk;
         $reset = *reset;
         
         
         $val1[31:0] = >>2$out[31:0];
         $val2[31:0] = $rand2[3:0];
         $op[1:0] = $rand3[1:0];
   
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot[31:0] = $val1[31:0] / $val2[31:0];
         
         $num = $reset ? 0 : >>1$num+1;
      @2   
         $out[31:0] = ($reset|!$num) ? 32'b0 : (($op[1:0]==2'b00) ? $sum :
                                       ($op[1:0]==2'b01) ? $diff :
                                          ($op[1:0]==2'b10) ? $prod : $quot);
         
         

         

      // Macro instantiations for calculator visualization(disabled by default).
      // Uncomment to enable visualisation, and also,
      // NOTE: If visualization is enabled, $op must be defined to the proper width using the expression below.
      //       (Any signals other than $rand1, $rand2 that are not explicitly assigned will result in strange errors.)
      //       You can, however, safely use these specific random signals as described in the videos:
      //  o $rand1[3:0]
      //  o $rand2[3:0]
      //  o $op[x:0]
      
   //m4+cal_viz(@3) // Arg: Pipeline stage represented by viz, should be atleast equal to last stage of CALCULATOR logic.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   

\SV
   endmodule
```

Below is a screenshot of a 2-cycle calculator, which alternately clears the output. The result of the given inputs is observed in the next cycle.

![Screenshot 2024-08-21 124520](https://github.com/user-attachments/assets/4fb04a2a-a4ba-4f87-a8f8-dfca78352abc)

### Validity of 2-Cycle Calculator

**Validity in TL-Verilog** indicates that a signal represents a valid transaction, described using a `when` scope. Otherwise, it operates as a don't-care condition. It is denoted as `?$valid`. Validity ensures easier debugging, cleaner design, improved error checking, and automated clock gating.

2-Cycle_Calculator_validity.tlv
```bash
\m4_TLV_version 1d: tl-x.org
\SV
   
   m4_include_lib(['https://raw.githubusercontent.com/stevehoover/RISC-V_MYTH_Workshop/bd1f186fde018ff9e3fd80597b7397a1c862cf15/tlv_lib/calculator_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)

\TLV
   |calc
      @0
         $clk_tan = *clk;
         $reset = *reset;
      @1 
         $valid = $reset ? 0 : >>1$valid+1;
         $valid_or_reset = $valid || $reset;  
      ?$valid   
         @1          
            $val1[31:0] = >>2$out[31:0];
            $val2[31:0] = $rand2[3:0];
            $op[1:0] = $rand3[1:0];

            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];            
      @2   
         $out[31:0] = $valid_or_reset ? (($op[1:0]==2'b00) ? $sum :
                                           ($op[1:0]==2'b01) ? $diff :
                                              ($op[1:0]==2'b10) ? $prod : $quot) : >>1$out[31:0];
 
      // Macro instantiations for calculator visualization(disabled by default).
      // Uncomment to enable visualisation, and also,
      // NOTE: If visualization is enabled, $op must be defined to the proper width using the expression below.
      //       (Any signals other than $rand1, $rand2 that are not explicitly assigned will result in strange errors.)
      //       You can, however, safely use these specific random signals as described in the videos:
      //  o $rand1[3:0]
      //  o $rand2[3:0]
      //  o $op[x:0]
      
   //m4+cal_viz(@3) // Arg: Pipeline stage represented by viz, should be atleast equal to last stage of CALCULATOR logic.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   

\SV
   endmodule
```
Below is a screenshot of a 2-cycle calculator with validity:

![Screenshot 2024-08-21 124725](https://github.com/user-attachments/assets/0bf6c658-f1fc-4bd8-b38b-e676295756f7)

## Basic RISC-V CPU micro-architecture

Designing the basic processor of 3 stages fetch, decode and execute based on RISC-V ISA.

### Fetch

**Program Counter (PC):** Holds the address of the next instruction.  
**Instruction Memory (IM):** Stores the set of instructions to be executed.  

During the Fetch stage, the processor retrieves the instruction from the IM at the address specified by the PC.

Fetch.tlv

```bash
\m4_TLV_version 1d: tl-x.org
\SV
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
         $clk_tan = *clk;
         $pc[31:0] = $reset ? '0 : >>1$pc + 32'd4;
         
         $imem_rd_en = !$reset ? 1 : 0;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];

      @1
         $instr[31:0] = $imem_rd_data[31:0];
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule
```
Below is a screenshot after completing the Fetch stage:

![Screenshot 2024-08-21 162058](https://github.com/user-attachments/assets/97559b29-bd28-45cc-9de9-1b8441a9e8f7)

### Decode

### 6 Types of Instructions

- **R-type**: Register
- **I-type**: Immediate
- **S-type**: Store
- **B-type**: Branch (Conditional Jump)
- **U-type**: Upper Immediate
- **J-type**: Jump (Unconditional Jump)

The instruction format includes the opcode, immediate value, source address, and destination address. During the decode stage, the processor interprets the instruction based on its format and type.

Decode.tlv
```bash
\m4_TLV_version 1d: tl-x.org
\SV
  
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
         $clk_tan = *clk;
         $pc[31:0] = $reset ? '0 : >>1$pc + 32'd4;
         
         $imem_rd_en = !$reset ? 1 : 0;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];

      @1
         $instr[31:0] = $imem_rd_data[31:0];
         
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==  5'b11001;
         
         $is_r_instr = $instr[6:2] ==  5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==  5'b10100;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_b_instr = $instr[6:2] ==  5'b11000;
         
         $is_j_instr = $instr[6:2] ==  5'b11011;
         
         $is_u_instr = $instr[6:2] ==?  5'b0x101;
         
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0}:
                      $is_u_instr ? {$instr[31], $instr[30:20], $instr[19:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                      32'b0;
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rs1_valid = $is_r_instr || $is_s_instr || $is_i_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         
         $opcode[6:0] = $instr[6:0];
         
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         $is_beq  = $dec_bits ==? 11'bx0001100011;
         $is_bne  = $dec_bits ==? 11'bx0011100011;
         $is_blt  = $dec_bits ==? 11'bx1001100011;
         $is_bge  = $dec_bits ==? 11'bx1011100011;
         $is_bltu = $dec_bits ==? 11'bx1101100011;
         $is_bgeu = $dec_bits ==? 11'bx1111100011;
         $is_addi = $dec_bits ==? 11'bx0000010011;
         $is_add  = $dec_bits ==  11'b00000110011;
                 
         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu $is_addi $is_add)
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule
```


Below is the screenshoot after executing the decode stage:

![Screenshot 2024-08-21 162858](https://github.com/user-attachments/assets/08b81786-b6c5-452e-8fa5-2076941c381a)

## Register File Read and Write

The Register File supports 2 read operations and 1 write operation simultaneously.

### Inputs:
  * **Read_Enable**: Enable signal to perform the read operation.
  * **Read_Address1**: Address from which data is read (Address 1).
  * **Read_Address2**: Address from which data is read (Address 2).
  * **Write_Enable**: Enable signal to perform the write operation.
  * **Write_Address**: Address where data is written.
  * **Write_Data**: Data to be written to the specified address.

### Outputs:
  * **Read_Data1**: Data from `Read_Address1`.
  * **Read_Data2**: Data from `Read_Address2`.

Register_File_Read_write.tlv

```bash
\m4_TLV_version 1d: tl-x.org
\SV
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
         $clk_tan = *clk;
         $pc[31:0] = (>>1$reset) ? '0 :
                     (>>1$taken_br) ? >>1$br_tgt_pc :
                     >>1$pc + 32'd4;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];

      @1
         $instr[31:0] = $imem_rd_data[31:0];
         
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==  5'b11001;
         
         $is_r_instr = $instr[6:2] ==  5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==  5'b10100;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_b_instr = $instr[6:2] ==  5'b11000;
         
         $is_j_instr = $instr[6:2] ==  5'b11011;
         
         $is_u_instr = $instr[6:2] ==?  5'b0x101;
         
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0}:
                      $is_u_instr ? {$instr[31:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                      32'b0;
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rs1_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $funct7_valid = $is_r_instr;
         
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         
         $opcode[6:0] = $instr[6:0];
         
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         $is_beq = $dec_bits ==? 11'bx0001100011;
         $is_bne = $dec_bits ==? 11'bx0011100011;
         $is_blt = $dec_bits ==? 11'bx1001100011;
         $is_bge = $dec_bits ==? 11'bx1011100011;
         $is_bltu = $dec_bits ==? 11'bx1101100011;
         $is_bgeu = $dec_bits ==? 11'bx1111100011;
         $is_add = $dec_bits ==? 11'b00000110011;
         $is_addi = $dec_bits ==? 11'bx0000010011;
         
         // Register File Read Logic
         $rf_rd_en1 = $rs1_valid;
         ?$rf_rd_en1
            $rf_rd_index1[4:0] = $rs1[4:0];
         
         $rf_rd_en2 = $rs2_valid;
         ?$rf_rd_en2
            $rf_rd_index2[4:0] = $rs2[4:0];
         
         $src1_value[31:0] = $rf_rd_data1[31:0];
         $src2_value[31:0] = $rf_rd_data2[31:0];
         
         //ALU
         
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add  ? $src1_value + $src2_value :
                         32'bx;
         
         // Register File Write
         $rf_wr_en = ($rd == 5'b0) ? 1'b0 : $rd_valid;
         ?$rf_wr_en
            $rf_wr_index[4:0] = $rd[4:0];
         
         $rf_wr_data[31:0] = $result[31:0];
         
         //Branch Instructions
         
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) : 1'b0;
         
         $br_tgt_pc[31:0] = $pc + $imm;
         
         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu)
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule
```
Below is the screenshot showing the Register File read operation followed by the write operation.

![Screenshot 2024-08-21 163544](https://github.com/user-attachments/assets/0330e1a6-76df-48d7-b49d-f8d2e573d25f)

![Screenshot 2024-08-21 163710](https://github.com/user-attachments/assets/785079b9-21ae-40a8-a0bc-8308f4279a47)

### Control Logic

During the Decode stage, the branch target address is calculated and fed into the PC multiplexer. Before the Execute stage, once the operands are ready, the branch condition is evaluated.

**Below is the screenshot after incorporating the control logic for branch instructions.**

![image](https://github.com/user-attachments/assets/155a51e8-bbf7-43a0-8601-16607f8682d7)

# Pipelined RISC-V CPU

Converting a non-pipelined CPU to a pipelined CPU using the timing abstraction feature of TL-Verilog enables seamless retiming without the risk of functional bugs. More inforamtion on timming abstract can be found in the IEEE paper ["Timing-Abstract Circuit Design in Transaction-Level Verilog" by Steven Hoover.](https://ieeexplore.ieee.org/document/8119264) by Steeve Hoover.

In this implementation, a single-cycle RISC-V CPU has been expanded into a 3-cycle architecture. Additionally, all potential pipelining hazards have been addressed.

As shown in the screenshot, the output of the sum 1 to 9 program is observed in register r10, which holds the value 45. It can be observed that the CPU took 56 cycles to execute the program for calculating the sum of numbers from 1 to 9.

![image](https://github.com/user-attachments/assets/659127fe-b039-4497-97f0-5150ce277b19)

The following shows the sum on waveform:

![image](https://github.com/user-attachments/assets/af1a3a62-6e69-406a-b474-97a34a982ab1)


The following screenshot shows the reset signal

![image](https://github.com/user-attachments/assets/9c9c0ef7-f299-43e9-a29a-2475d3c77f79)

Pipelined_RISCV_CPU.tlv
```bash
\m4_TLV_version 1d: tl-x.org
\SV
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
         $clk_tan = *clk;
         $start = >>1$reset ? !$reset ? '1 :'0 :'0;
         //$valid = $reset ? '0 : $start ? '1 : >>3$valid ? '1 : '0;
         
         $pc[31:0] = (>>1$reset) ? '0 :
                     (>>3$valid_taken_br) ? >>3$br_tgt_pc :
                     >>1$inc_pc;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];

      @1
         $inc_pc[31:0] = $pc[31:0] + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==  5'b11001;
         
         $is_r_instr = $instr[6:2] ==  5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==  5'b10100;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_b_instr = $instr[6:2] ==  5'b11000;
         
         $is_j_instr = $instr[6:2] ==  5'b11011;
         
         $is_u_instr = $instr[6:2] ==?  5'b0x101;
         
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0}:
                      $is_u_instr ? {$instr[31:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                      32'b0;
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rs1_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $funct7_valid = $is_r_instr;
         
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         
         $opcode[6:0] = $instr[6:0];
         
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         // Branch Instruction
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         
         // Arithmetic Instruction
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         
         // Load Instruction
         $is_load = $dec_bits ==? 11'bx_xxx_0000011;
         
         // Store Instruction
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         
         // Jump Instruction
         $lui = $dec_bits ==? 11'bx_xxx_0110111;
         $auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $jal = $dec_bits ==? 11'bx_xxx_1101111;
         $jalr = $dec_bits ==? 11'bx_000_1100111;
         
         
      @2
         
         $br_tgt_pc[31:0] = $pc + $imm;
         
         // Register File Read Logic
         $rf_rd_en1 = $rs1_valid;
         ?$rf_rd_en1
            $rf_rd_index1[4:0] = $rs1[4:0];
         
         $rf_rd_en2 = $rs2_valid;
         ?$rf_rd_en2
            $rf_rd_index2[4:0] = $rs2[4:0];
         
         $src1_value[31:0] = ((>>1$rd == $rs1) && (>>1$rf_wr_en ==1'b1)) ? >>1$result : $rf_rd_data1[31:0];
         $src2_value[31:0] = ((>>1$rd == $rs2) && (>>1$rf_wr_en ==1'b1)) ? >>1$result : $rf_rd_data2[31:0];
         
      @3
         
         //ALU
         $sltu_result = $src1_value < $src2_value ;
         $sltiu_result = $src1_value < $imm ;
         
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value :
                         $is_or ? $src1_value | $src2_value :
                         $is_ori ? $src1_value | $imm :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_xori ? $src1_value ^ $imm :
                         $is_and ? $src1_value & $src2_value :
                         $is_andi ? $src1_value & $imm :
                         $is_sub ? $src1_value - $src2_value :
                         $is_slti ? (($src1_value[31] == $imm[31]) ? $sltiu_result : {31'b0,$src1_value[31]}) :
                         $is_sltiu ? $sltiu_result :
                         $is_slli ? $src1_value << $imm[5:0] :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_srai ? ({{32{$src1_value[31]}}, $src1_value} >> $imm[4:0]) :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_slt ? (($src1_value[31] == $src2_value[31]) ? $sltu_result : {31'b0,$src1_value[31]}) :
                         $is_sltu ? $sltu_result :
                         $is_srl ? $src1_value >> $src2_value[5:0] :
                         $is_sra ? ({{32{$src1_value[31]}}, $src1_value} >> $src2_value[4:0]) :
                         $lui ? ({$imm[31:12], 12'b0}) :
                         $auipc ? $pc + $imm :
                         $jal ? $pc + 4 :
                         $jalr ? $pc + 4 : 32'bx;
         
         // Register File Write
         $rf_wr_en = $valid ? ($rd == 5'b0) ? 1'b0 : $rd_valid : 1'b0;
         ?$rf_wr_en
            $rf_wr_index[4:0] = $rd[4:0];
         
         $rf_wr_data[31:0] = $result[31:0];
         
         //Branch Instructions
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) : 1'b0;
         
         $valid_taken_br = $valid && $taken_br;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br);
         //`BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu)
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   //*passed = *cyc_cnt > 40;
   *passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule
```

# TASK-6


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
- **OUT[9:0]**: 10-bit output port of the RISC-V core(highlighted both in binary value and decimal)

---

![image](https://github.com/user-attachments/assets/8c75fbb3-a9bc-47ab-a0c2-b48b1fd5cf82)

This outlines a straightforward approach for converting TL-Verilog code and validating it through Verilog simulation.

## Waveforms from Makerchip platform IDE by running .tlv file for comparison

As shown in the screenshot, the output of the sum 1 to 9 program is observed in register r10, which holds the value 45. It can be observed that the CPU took 56 cycles to execute the program for calculating the sum of numbers from 1 to 9.

![image](https://github.com/user-attachments/assets/659127fe-b039-4497-97f0-5150ce277b19)

The following shows the sum on waveform:

![image](https://github.com/user-attachments/assets/af1a3a62-6e69-406a-b474-97a34a982ab1)


The following screenshot shows the reset signal

![image](https://github.com/user-attachments/assets/9c9c0ef7-f299-43e9-a29a-2475d3c77f79)


# TASK-7

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

![image](https://github.com/user-attachments/assets/9f9d386c-6a59-4d37-bef8-6e388f3b13aa)


# TASK-8

# RTL design using Verilog with SKY130 Technology

## Icarus Verilog-Based Simulation Flow

A simulator is used to validate whether a design aligns with its intended specifications by running simulations on the code. It monitors changes in input signals, and whenever these inputs vary, the corresponding outputs are recalculated. RTL (Register Transfer Level) design refers to the Verilog code that describes the behavior and structure of a digital circuit. To ensure correctness, a testbench is developed to test the design through simulation using Icarus Verilog.

During the simulation, a VCD (Value Change Dump) file is generated, which logs signal transitions. This file is analyzed using GTKWave, a waveform viewer that assists in debugging and verifying circuit behavior. GTKWave allows users to explore signal interactions, inspect timing relationships, and validate the overall operation of the design by visualizing the waveforms created during simulation.

### Setup

Enter the below command in the Ubuntu terminal:
	  
```
sudo -i
sudo apt-get install git
ls
cd Desktop
mkdir ASIC
cd ASIC
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
ls
```

We observe the following list of files present in the directory. 

![Screenshot from 2024-10-21 00-30-37](https://github.com/user-attachments/assets/ff904975-c47a-4500-9228-0c8362e08bf9)

## DAY 1
		  

### Introduction to Icarus Verilog and GTKWave

This tutorial covers the basics of simulating a 2x1 multiplexer design along with its testbench using Icarus Verilog (iverilog). Additionally, it demonstrates how to view the generated waveforms using GTKWave for better analysis and verification of the design.

   Run the following commands
```
iverilog good_mux.v tb_good_mux.v
./a.out
gtkwave tb_good_mux.vcd

 ```	
![Screenshot from 2024-10-21 00-51-22](https://github.com/user-attachments/assets/750fc0e4-2cfe-4de2-a4dc-1d004bcddaa6)


  #### MUX.V

```
  module good_mux (input i0, input i1, input sel, output reg y);
	  always@(*)
	  begin
	  	if(sel)
			y<=i1;
		else
			y<=i0;
	  end
  endmodule
```

  #### MUX_TB.V

  ```
  module tb_good_mux;
	reg i0,i1,sel;
	wire y;

     	good_mux uut(.sel(sel),.i0(i0),.i1(i1),.y(y));

	initial begin
		$dumpfile("tb_good_mux.vcd");
		$dumpvars(0,tb_good_mux);
		sel=0;
		i0=0;
		i1=0;
		#300 $finish;
	end
	always #75 sel = ~sel;
	always #10 i0 = ~i0;
	always #55 i1 = ~i1;
  endmodule
  ```

 
### Introduction to Yosys:

This tutorial demonstrates how to synthesize a Verilog design using Yosys, explore the generated netlists, and examine the cells used for building the circuit. The following commands were utilized throughout the process:

### Yosys 

1. **Launches the Yosys tool.**
 ```
yosys
```
![Screenshot from 2024-10-21 01-40-30](https://github.com/user-attachments/assets/adbbd872-5a0a-4b95-81be-65e7d6eb61d3)

2. **Load the Technology Library**
   Load the technology library file (in Liberty format) required for synthesis from the designated path.
   ```sh
   read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```

3. **Import the Verilog File**
   Import the Verilog file `good_mux.v` for synthesis purposes.
   ```sh
   read_verilog good_mux.v
   ```

4. **Execute Synthesis**
   Execute synthesis on the design, using `good_mux` as the top-level module.
   ```sh
   synth -top good_mux
   ```

5. **Enhance the Design**
   Utilize the ABC tool to enhance the synthesized design with the provided technology library.
   ```sh
   abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```

6. **Display the Synthesized Design**
   Show the synthesized design in the form of a schematic.
   ```sh
   show
   ```
![Screenshot from 2024-10-21 01-19-13](https://github.com/user-attachments/assets/9f582f40-1115-419e-82ec-69a9eb27d97e)

7. **Output the Synthesized Netlist**
   Write the synthesized netlist to the file `good_mux_netlist.v`, omitting attributes.
   ```sh
   write_verilog -noattr good_mux_netlist.v
   ```

8. **Open the Netlist File**
   Open the netlist file `good_mux_netlist.v` in the gvim text editor.
   ```sh
   !gvim good_mux_netlist.v

### Netlist generated

![Screenshot from 2024-10-21 01-20-27](https://github.com/user-attachments/assets/c5f94c7b-75c8-4be1-aebb-33c76a1e3864)
  
#### Yosys screenshots

![Screenshot from 2024-10-21 01-44-12](https://github.com/user-attachments/assets/e657c68f-4b36-4b35-aeec-06ade4035573)
![Screenshot from 2024-10-21 01-44-38](https://github.com/user-attachments/assets/81babc42-afdb-4cba-af14-efc23967fa77)
![Screenshot from 2024-10-21 01-45-04](https://github.com/user-attachments/assets/b87e8608-76a5-44dd-82b5-1e63551477b7)
 
 ## Day 2: Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

Run the commands mentioned to view the contents inside the .lib file:
```
cd ..
ls
cd lib
vim sky130_fd_sc_hd__tt_025C_1v80.lib
```

The (.lib) files contain PVT parameters—Process, Voltage, and Temperature. Variations in these parameters can have a substantial impact on circuit performance. Factors such as manufacturing inconsistencies, voltage fluctuations, and temperature shifts contribute to these effects.

![Screenshot from 2024-10-21 13-05-37](https://github.com/user-attachments/assets/53c8af6f-105b-421b-b055-cf879c8394b5)


### Hierarchical vs. Flat Synthesis

**Hierarchical synthesis** breaks down a complex design into multiple sub-modules. 
Each sub-module is synthesized separately into gate-level netlists, which are later 
integrated to form the complete design. This approach promotes better organization, 
enables the reuse of modules, and allows for incremental changes without impacting the entire system.

In contrast, **flat synthesis** treats the entire design as a single, unified block 
during the synthesis process, ignoring any hierarchical relationships. While this 
method can optimize certain designs, it can make the design more challenging to maintain, 
analyze, and modify due to the absence of modular structure.

Consider the Verilog file `multiple_modules.v` located in the `verilog_files` directory 
for a practical example of hierarchical synthesis.
  
### Yosys Synthesis for Multiple Modules

Execute the below mentioned yosys commands for multiple modules

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules
write_verilog -noattr multiple_modules_netlist.v
!gvim multiple_modules_netlist.v
```


#### multiple_modules.v

```

module sub_module2 (input a, input b, output y);
	assign y = a | b;
endmodule

module sub_module1 (input a, input b, output y);
	assign y = a&b;
endmodule

module multiple_modules (input a, input b, input c, output y);
	wire net1;
	sub_module1 u1(.a(a),.b(b),.y(net1)); //net1 = a&b
	sub_module2 u2(.a(net1),.b(c),.y(y)); //y = netic,ie y = a&b + c;
endmodule
```

#### Hierarchical generated Netlist
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module multiple_modules(a, b, c, y);
  input a;
  wire a;
  input b;
  wire b;
  input c;
  wire c;
  wire net1;
  output y;
  wire y;
  sub_module1 u1 (
    .a(a),
    .b(b),
    .y(net1)
  );
  sub_module2 u2 (
    .a(net1),
    .b(c),
    .y(y)
  );
endmodule

module sub_module1(a, b, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  wire a;
  input b;
  wire b;
  output y;
  wire y;
  sky130_fd_sc_hd__and2_0 _3_ (
    .A(_1_),
    .B(_0_),
    .X(_2_)
  );
  assign _1_ = b;
  assign _0_ = a;
  assign y = _2_;
endmodule

module sub_module2(a, b, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  wire a;
  input b;
  wire b;
  output y;
  wire y;
  sky130_fd_sc_hd__or2_0 _3_ (
    .A(_1_),
    .B(_0_),
    .X(_2_)
  );
  assign _1_ = b;
  assign _0_ = a;
  assign y = _2_;
endmodule
```

![Screenshot from 2024-10-21 01-53-12](https://github.com/user-attachments/assets/9180fbe6-6180-4ce6-a4ce-ef6f094555c0)

Yosys screenshot

![Screenshot from 2024-10-21 01-47-16](https://github.com/user-attachments/assets/6175c1ba-594f-43b1-8d36-474f891ffd7e)
![Screenshot from 2024-10-21 01-48-35](https://github.com/user-attachments/assets/07488850-0aa4-4d79-b7e0-ccc79f2676d7)
![Screenshot from 2024-10-21 01-49-06](https://github.com/user-attachments/assets/9e13a965-1026-454f-8bf9-fb55962e0ee1)
![Screenshot from 2024-10-21 01-54-08](https://github.com/user-attachments/assets/758e640c-138a-4498-bc30-4e5b970b4189)

To perform **flat synthesis** on the `multiple_modules.v` file, use the following commands:

 Merges all hierarchical modules in the design into a single module to create a flat netlist.
 
 ```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog multiple_modules.v
4. synth -top multiple_modules
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. flatten
7. show
8. write_verilog -noattr multiple_modules_netlist.v
9. !gvim multiple_modules_flat.v
```

![Screenshot from 2024-10-21 15-38-20](https://github.com/user-attachments/assets/fe06f2c7-ccb0-469f-afe8-35a4e5ef176a)


#### Flat synthesis generated Netlist
```
/* Generated by Yosys 0.7 (git sha1 61f6811, gcc 6.2.0-11ubuntu1 -O2 -fdebug-prefix-map=/build/yosys-OIL3SR/yosys-0.7=. -fstack-protector-strong -fPIC -Os) */

module multiple_modules(a, b, c, y);
  wire _00_;
  wire _01_;
  wire _02_;
  wire _03_;
  wire _04_;
  wire _05_;
  wire _06_;
  wire _07_;
  input a;
  input b;
  input c;
  wire net1;
  wire \u1.a ;
  wire \u1.b ;
  wire \u1.y ;
  wire \u2.a ;
  wire \u2.b ;
  wire \u2.y ;
  output y;
  sky130_fd_sc_hd__and2_2 _08_ (
    .A(_00_),
    .B(_01_),
    .X(_02_)
  );
  sky130_fd_sc_hd__clkinv_1 _09_ (
    .A(_03_),
    .Y(_06_)
  );
  sky130_fd_sc_hd__clkinv_1 _10_ (
    .A(_04_),
    .Y(_07_)
  );
  sky130_fd_sc_hd__nand2_1 _11_ (
    .A(_06_),
    .B(_07_),
    .Y(_05_)
  );
  assign \u1.a  = a;
  assign \u1.b  = b;
  assign net1 = \u1.y ;
  assign _00_ = \u1.b ;
  assign _01_ = \u1.a ;
  assign \u1.y  = _02_;
  assign \u2.a  = net1;
  assign \u2.b  = c;
  assign y = \u2.y ;
  assign _03_ = \u2.b ;
  assign _04_ = \u2.a ;
  assign \u2.y  = _05_;
endmodule
```

![Screenshot from 2024-10-21 15-46-44](https://github.com/user-attachments/assets/1b0b580f-b478-493a-aef6-18b18a55df57)
![Screenshot from 2024-10-21 15-47-09](https://github.com/user-attachments/assets/913ee2f5-3d7d-41c5-87b1-38012444b84c)

### Various Flip-Flop Coding Styles and Optimizations

Flip-flops play a crucial role in sequential logic circuits. They are used to store intermediate values, ensuring that inputs to combinational circuits remain stable until the next clock edge. This stability helps prevent glitches, ensuring proper operation of the circuit. By capturing and holding data, flip-flops help maintain the integrity of signals and facilitate the correct sequencing of operations in digital systems.

Simulations were conducted for three types of D-Flip-Flops:  
1. **Asynchronous Reset**  
2. **Asynchronous Set**  
3. **Synchronous Reset**  

These simulations demonstrate the behavior of each type, highlighting how they respond to different reset and set conditions, ensuring accurate storage and control of data during circuit operation.

### Asynchronous Reset

#### Verilog code:

```
module dff_asyncres(input clk, input async_reset, input d, output reg q);
	always@(posedge clk, posedge async_reset)
	begin
		if(async_reset)
			q <= 1'b0;
		else
			q <= d;
	end
endmodule
```

#### Testbench
```
module tb_dff_asyncres; 
	reg clk, async_reset, d;
	wire q;
	dff_asyncres uut (.clk(clk),.async_reset (async_reset),.d(d),.q(q));

	initial begin
		$dumpfile("tb_dff_asyncres.vcd");
		$dumpvars(0,tb_dff_asyncres);
		// Initialize Inputs
		clk = 0;
		async_reset = 1;
		d = 0;
		#3000 $finish;
	end
		
	always #10 clk = ~clk;
	always #23 d = ~d;
	always #547 async_reset=~async_reset; 
endmodule
```
Run the below commands for simulation:

```
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```
Output:

![Screenshot from 2024-10-21 16-44-26](https://github.com/user-attachments/assets/ea076a05-17d4-47aa-a94d-5f576a2ca9d4)

From the waveform, it can be observed that the **Q** output transitions to zero when the **asynchronous reset** is set high, regardless of the positive or negative clock edge. This demonstrates the independent nature of the asynchronous reset, allowing it to override other inputs to reset the output immediately.

Run the below commands to view netlist:

1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_asyncres.v
4. synth -top dff_asyncres
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_asyncres_netlist.v
9. !gvim dff_asyncres_netlist.v

Netlist:

![Screenshot from 2024-10-21 16-48-44](https://github.com/user-attachments/assets/1ba4e1d6-c534-4a0e-8446-4998649e2635)

Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module dff_asyncres(clk, async_reset, d, q);
  wire _0_;
  input async_reset;
  wire async_reset;
  input clk;
  wire clk;
  input d;
  wire d;
  output q;
  wire q;
  assign _0_ = ~async_reset;
  sky130_fd_sc_hd__dfrtp_1 _2_ (
    .CLK(clk),
    .D(d),
    .Q(q),
    .RESET_B(_0_)
  );
endmodule
```
Yosys screenshot			

![Screenshot from 2024-10-21 16-47-08](https://github.com/user-attachments/assets/29c16cd6-2b2a-4c0d-8633-281a4d956aea)

### Synchronous Reset

#### Verilog code:
```
module dff_syncres(input clk, input sync_reset, input d, output reg q);
	always@(posedge clk)
	begin
		if(sync_reset)
			q <= 1'b0;
		else
			q <= d;
	end
endmodule
```

#### Testbench

```
module tb_dff_syncres; 
	reg clk, syncres, d;
	wire q;
	dff_asyncres uut (.clk(clk),.sync_reset (sync_reset),.d(d),.q(q));

	initial begin
		$dumpfile("tb_dff_syncres.vcd");
		$dumpvars(0,tb_dff_syncres);
		// Initialize Inputs
		clk = 0;
		sync_reset = 1;
		d = 0;
		#3000 $finish;
	end
		
	always #10 clk = ~clk;
	always #23 d = ~d;
	always #547 sync_reset=~async_reset; 
endmodule
```

Run the below commands for simulation:
```
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd
```
Output

![Screenshot from 2024-10-21 17-46-28](https://github.com/user-attachments/assets/f394c882-9dd1-4d79-8ae1-af4c75bf69ba)

From the waveform, it can be observed that the **Q** output transitions to zero when the **synchronous reset** is set high, but only at the **positive clock edge**. This behavior illustrates that the synchronous reset affects the output in alignment with the clock, ensuring controlled and predictable operation.

Run the below commands to view netlist:

1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_syncres.v
4. synth -top dff_syncres
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_syncres_netlist.v
9. !gvim dff_syncres_netlist.v

Netlist:

![Screenshot from 2024-10-21 17-54-04](https://github.com/user-attachments/assets/268b6e9a-c895-41e4-b28f-fdddb9f2b33b)


Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module dff_syncres(clk, async_reset, sync_reset, d, q);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  input async_reset;
  wire async_reset;
  input clk;
  wire clk;
  input d;
  wire d;
  output q;
  wire q;
  input sync_reset;
  wire sync_reset;
  sky130_fd_sc_hd__nor2b_1 _4_ (
    .A(_2_),
    .B_N(_1_),
    .Y(_0_)
  );
  sky130_fd_sc_hd__dfxtp_1 _5_ (
    .CLK(clk),
    .D(_3_),
    .Q(q)
  );
  assign _1_ = d;
  assign _2_ = sync_reset;
  assign _3_ = _0_;
endmodule
```
Yosys screenshot			

![Screenshot from 2024-10-21 17-52-00](https://github.com/user-attachments/assets/e15240f9-8398-4104-b092-ff22cbd67dde)

      
### Asynchronous Set

#### Verilog code
```
module dff_async_set(input clk, input async_set, input d, output reg q);
	always@(posedge clk, posedge async_set)
	begin
		if(async_set)
			q <= 1'b1;
		else
			q <= d;
	end
endmodule
```

#### Testbench
```
module tb_dff_async_set; 
	reg clk, async_set, d;
	wire q;
	dff_async_set uut (.clk(clk),.async_set (async_set),.d(d),.q(q));

	initial begin
		$dumpfile("tb_dff_async_set.vcd");
		$dumpvars(0,tb_dff_async_set);
		// Initialize Inputs
		clk = 0;
		async_set = 1;
		d = 0;
		#3000 $finish;
	end
		
	always #10 clk = ~clk;
	always #23 d = ~d;
	always #547 async_set=~async_set; 
endmodule
```
Run the below commands for simulation:

```
iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
```

Output:

![Screenshot from 2024-10-21 17-59-15](https://github.com/user-attachments/assets/97adade9-b985-4314-86b8-445beaf752dc)

From the waveform, it can be observed that the **Q** output transitions to one when the **asynchronous set** is set high, regardless of the positive or negative clock edge. This demonstrates the independent nature of the asynchronous set, allowing it to override other inputs and immediately set the output to one.

Run the below commands to view netlist:

1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_async_set.v
4. synth -top dff_async_set
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_async_set_netlist.v
9. !gvim dff_syncres_netlist.v

Netlist:

![Screenshot from 2024-10-21 18-04-46](https://github.com/user-attachments/assets/9fd6ec4e-3f43-4940-b150-b357df4ed341)


Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module dff_syncres(clk, async_reset, sync_reset, d, q);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  input async_reset;
  wire async_reset;
  input clk;
  wire clk;
  input d;
  wire d;
  output q;
  wire q;
  input sync_reset;
  wire sync_reset;
  sky130_fd_sc_hd__nor2b_1 _4_ (
    .A(_2_),
    .B_N(_1_),
    .Y(_0_)
  );
  sky130_fd_sc_hd__dfxtp_1 _5_ (
    .CLK(clk),
    .D(_3_),
    .Q(q)
  );
  assign _1_ = d;
  assign _2_ = sync_reset;
  assign _3_ = _0_;
endmodule
```
Yosys screenshot			

![Screenshot from 2024-10-21 18-03-10](https://github.com/user-attachments/assets/21046dca-e89f-45e9-b1fc-973d67cb1433)


### Optimization

#### Multiplication by 2

In this tutorial, we learn that dedicated multiplier hardware is not necessary to multiply a number by 2. This operation can be efficiently performed by **concatenating a zero to the Least Significant Bit (LSB)** of the number, effectively shifting all bits to the left by one position.

verilog code 
```
module mul2(input [2:0]a, output [3:0]y);
	assign y=a*2;
endmodule
```

Run the below commands to view netlist:

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog mult_2.v
4. synth -top mul2
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. show
7. write_verilog -noattr mul2_net.v
8. !gvim mul2_net.v
```

Netlist:

![Screenshot from 2024-10-21 18-19-39](https://github.com/user-attachments/assets/f0277ae9-b267-46b3-91db-da16e6d20259)


Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module mul2(a, y);
  input [2:0] a;
  wire [2:0] a;
  output [3:0] y;
  wire [3:0] y;
  assign y = { a, 1'h0 };
endmodule
```
Yosys screenshot			

![Screenshot from 2024-10-21 18-18-24](https://github.com/user-attachments/assets/f39d7cb5-f0a4-414d-bfa7-2ed9ef73ccd6)


#### Multiplication by 9

In this tutorial, we learn that dedicated multiplier hardware is not needed to multiply a number by 9. This can be efficiently achieved by **concatenating the number with itself**, effectively performing the multiplication through bit manipulation.

verilog code 
```
module mult8 (input [2:0] a , output [5:0] y);
	assign y = a * 9;
endmodule
```

Run the below commands to view netlist:

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog mult_8.v
4. synth -top mult8
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. show
7. write_verilog -noattr mult_8_net.v
8. !gvim mult_8_net.v
```

Netlist:

![Screenshot from 2024-10-21 18-32-58](https://github.com/user-attachments/assets/24bd8001-1ae4-4539-adb3-6419da480f9a)


Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module mult8(a, y);
  input [2:0] a;
  wire [2:0] a;
  output [5:0] y;
  wire [5:0] y;
  assign y = { a, a };
endmodule
```
Yosys screenshot			

![Screenshot from 2024-10-21 18-30-32](https://github.com/user-attachments/assets/450c54c9-e7f3-41ba-b42a-b6a476e6ecd7)

 

## Day 3: Combinational and sequential Optimizationsof Various Designs

### Types of Optimizations: Combinational and Sequential

These optimizations aim to create designs that are efficient in terms of **area**, **power**, and **performance**.

#### Combinational Optimization  
The techniques used in this type of optimization include:

- **Constant Propagation (Direct Optimization):**  
  Simplifies logic by directly substituting known constant values, reducing unnecessary gates.

- **Boolean Logic Optimization:**  
  Minimizes logic expressions using methods such as **Karnaugh Maps (K-Map)** or the **Quine-McCluskey algorithm**, leading to fewer gates and improved efficiency.


 #### 2 input AND Gate:

Verilog code: 
```
module opt_check(input a, input b, output y);
	assign y = a?b:0;
endmodule
```
Commands for netlist:

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog opt_check.v
4. synth -top opt_check
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
8. write_verilog -noattr opt_check.v
9. !gvim opt_check.v
```
Netlist:

![Screenshot from 2024-10-21 22-17-00](https://github.com/user-attachments/assets/a80371af-ef59-4bf0-b66c-2b0d3aa627c9)

Netlist Code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module opt_check(a, b, y);
  input a;
  wire a;
  input b;
  wire b;
  output y;
  wire y;
  sky130_fd_sc_hd__and2_0 _0_ (
    .A(b),
    .B(a),
    .X(y)
  );
endmodule
```

Yosys screenshot

![Screenshot from 2024-10-21 22-15-31](https://github.com/user-attachments/assets/b0790e92-f1a5-422f-b06f-136ca85d5727)


#### 2 input OR Gate:

Verilog code:
```
module opt_check2(input a, input b, output y);
	assign y = a?1:b;
endmodule
```
Commands for netlist:

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog opt_check2.v
4. synth -top opt_check2
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
7. write_verilog -noattr opt_check2.v
8. !gvim opt_check2.v
```
Netlist:

![Screenshot from 2024-10-21 22-37-20](https://github.com/user-attachments/assets/e2a830de-7377-43c8-80a7-f7b0ba08a211)

Netlist Code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module opt_check2(a, b, y);
  input a;
  wire a;
  input b;
  wire b;
  output y;
  wire y;
  sky130_fd_sc_hd__or2_0 _0_ (
    .A(a),
    .B(b),
    .X(y)
  );
endmodule
```

Yosys screenshot

![Screenshot from 2024-10-21 22-35-49](https://github.com/user-attachments/assets/8585191a-9453-4aed-9660-b3327e18a8e8)

#### 3 input AND Gate:

Verilog code:
```
module opt_check2(input a, input b, input c, output y);
	assign y = a?(b?c:0):0;
endmodule
```
Commands for netlist:

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog opt_check3.v
4. synth -top opt_check3
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
8. write_verilog -noattr opt_check3.v
8. !gvim opt_check3.v
```
Netlist:

![Screenshot from 2024-10-21 22-45-42](https://github.com/user-attachments/assets/14451574-cbb5-4aa9-a01f-a68a75ef7d28)


Netlist Code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module opt_check3(a, b, c, y);
  input a;
  wire a;
  input b;
  wire b;
  input c;
  wire c;
  output y;
  wire y;
  sky130_fd_sc_hd__and3_1 _0_ (
    .A(b),
    .B(c),
    .C(a),
    .X(y)
  );
endmodule
```

Yosys screenshot

![Screenshot from 2024-10-21 22-44-13](https://github.com/user-attachments/assets/62d23c95-4675-4faf-9309-695a82b2ca46)


### 2 input XNOR Gate

Verilog code:
```
module opt_check2(input a, input b, input c, output y);
	assign y = a ? (b ? ~c : c) : ~c;
endmodule
```
Commands for netlist:

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog opt_check4.v
4. synth -top opt_check4
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
8. write_verilog -noattr opt_check4.v
8. !gvim opt_check4.v

```
Netlist:

![Screenshot from 2024-10-21 22-53-27](https://github.com/user-attachments/assets/9d5ec42c-bde1-49a6-86ee-7a7a5e415509)

Netlist Code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module opt_check4(a, b, c, y);
  input a;
  wire a;
  input b;
  wire b;
  input c;
  wire c;
  output y;
  wire y;
  sky130_fd_sc_hd__xnor2_1 _0_ (
    .A(c),
    .B(a),
    .Y(y)
  );
endmodule
```

Yosys screenshot:
![Screenshot from 2024-10-21 22-52-41](https://github.com/user-attachments/assets/eb555790-04b1-4668-8857-598df51826dd)


#### Multiple Module Optimization-1

Verilog code:
```
module sub_module1(input a, input b, output y);
	assign y = a & b;
endmodule

module sub_module2 (input a, input b output y);
	assign y = a^b;
endmodule

module multiple_module_opt(input a, input b input c, input d output y);
	wire n1,n2, n3;

	sub_module1 U1 (.a(a), .b(1'b1), .y(n1));
	sub_module2 U2 (.a(n1), .b(1'b0), .y(n));
	sub_module2 U3 (.a(b), .b(d), .y(n3));

	assign y = c | (b & n1);
endmodule
```
Commands for netlist:
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog multiple_module_opt.v
4. synth -top multiple_module_opt
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. flatten
8. show
9. write_verilog -noattr multiple_module_opt.v
10. !gvim multiple_module_opt.v
```
Netlist:

![Screenshot from 2024-10-21 23-05-35](https://github.com/user-attachments/assets/15d75143-e1b3-48e5-ba30-15a69aff9b9a)

Netlist Code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module multiple_module_opt(a, b, c, d, y);
  wire \U1.a ;
  wire \U1.b ;
  wire \U1.y ;
  input a;
  wire a;
  input b;
  wire b;
  input c;
  wire c;
  input d;
  wire d;
  wire n1;
  output y;
  wire y;
  sky130_fd_sc_hd__a21o_1 _0_ (
    .A1(n1),
    .A2(b),
    .B1(c),
    .X(y)
  );
  sky130_fd_sc_hd__and2_0 _1_ (
    .A(\U1.b ),
    .B(\U1.a ),
    .X(\U1.y )
  );
  assign \U1.a  = a;
  assign \U1.b  = 1'h1;
  assign n1 = \U1.y ;
endmodule
```

Yosys screenshot:
![Screenshot from 2024-10-21 23-01-06](https://github.com/user-attachments/assets/9a4684b9-78d6-43e2-b3ad-21f8ad9c43e6)

#### Multiple Module Optimization-2

Verilog code:

```
module sub_module(input a input b output y);
	assign y = a & b;
endmodule

module multiple_module_opt2(input a, input b input c, input d, output y);
	wire n1,n2, n3;

	sub_module U1 (.a(a), .b(1'b0), y(n));
	sub_module U2 (.a(b), .b(c), .y(n2));
	sub_module U3 (.a(n2), .b(d), .y(n));
	sub_module U4 (.a(n3), .b(n1), .y(y));
endmodule
```

Commands for netlist:
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog multiple_module_opt2.v
4. synth -top multiple_module_opt2
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. flatten
8. show
9. write_verilog -noattr multiple_module_opt2_net.v
10. !gvim multiple_module_opt2.v
```
Netlist:
![Screenshot from 2024-10-21 23-14-52](https://github.com/user-attachments/assets/061138ea-29c0-47c5-862d-6567af7ad2ca)

Netlist code:
```
module sub_module(input a , input b , output y);
 assign y = a & b;
endmodule

module multiple_module_opt2(input a , input b , input c , input d , output y);
wire n1,n2,n3;

sub_module U1 (.a(a) , .b(1'b0) , .y(n1));
sub_module U2 (.a(b), .b(c) , .y(n2));
sub_module U3 (.a(n2), .b(d) , .y(n3));
sub_module U4 (.a(n3), .b(n1) , .y(y));

endmodule
```

Yosys screenshot:
![Screenshot from 2024-10-21 23-13-01](https://github.com/user-attachments/assets/a08cded3-dafe-4798-a073-fd347db8ed21)


### Sequential Logic Optimizations


#### D-Flipflop Constant 1 with Asynchronous Reset (active low)

Verilog code:
```
module dff_const1(input clk, input reset, output reg q); 
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end
endmodule
```

Testbench:
```
module tb_dff_const1; 
	reg clk, reset;
	wire q;

	dff_const1 uut (.clk(clk),.reset(reset),.q(q));

	initial begin
		$dumpfile("tb_dff_const1.vcd");
		$dumpvars(0,tb_dff_const1);
		// Initialize Inputs
		clk = 0;
		reset = 1;
		#3000 $finish;
	end

	always #10 clk = ~clk;
	always #1547 reset=~reset;
endmodule
```
Simulation:

```
iverilog dff_const1.v tb_dff_const1.v
./a.out
gtkwave tb_dff_const1.vcd
```
![Screenshot from 2024-10-22 00-26-40](https://github.com/user-attachments/assets/06c70939-8c36-4324-b52b-932f9ecc8b42)

Commands for netlist:
   
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_const1.v
4. synth -top dff_const1
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_const1_net.v
9. !gvim dff_const1_net.v
```

Netlist:
![Screenshot from 2024-10-22 00-28-41](https://github.com/user-attachments/assets/b72fe889-02fd-4492-ac6d-6cca10b54220)


Netlist code:

```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module dff_const1(clk, reset, q);
  wire _0_;
  input clk;
  wire clk;
  output q;
  wire q;
  input reset;
  wire reset;
  assign _0_ = ~reset;
  sky130_fd_sc_hd__dfrtp_1 _2_ (
    .CLK(clk),
    .D(1'h1),
    .Q(q),
    .RESET_B(_0_)
  );
endmodule
```

Yosys screenshot:
![Screenshot from 2024-10-22 00-28-02](https://github.com/user-attachments/assets/ea89c56d-6276-42ec-9041-d0c287531353)


### D-Flipflop Constant 2 with Asynchronous Reset (active high)

Verilog code:

```
module dff_const2(input clk, input reset, output reg q); 
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end
endmodule
```
Testbench
```
module tb_dff_const2; 
	reg clk, reset;
	wire q;

	dff_const2 uut (.clk(clk),.reset(reset),.q(q));

	initial begin
		$dumpfile("tb_dff_const1.vcd");
		$dumpvars(0,tb_dff_const1);
		// Initialize Inputs
clk = 0;
		reset = 1;
		#3000 $finish;
	end

	always #10 clk = ~clk;
	always #1547 reset=~reset;
endmodule
```
Simulation:

```
iverilog dff_const2.v tb_dff_const2.v
./a.out
gtkwave tb_dff_const2.vcd
```
![Screenshot from 2024-10-22 00-30-10](https://github.com/user-attachments/assets/9c5bfad3-0575-49db-b73d-e36a671779cd)

Commands for netlist:

```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_const2.v
4. synth -top dff_const2
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_const2_net.v
9. !gvim dff_const2_net.v
```
Netlist:
![Screenshot from 2024-10-22 00-32-35](https://github.com/user-attachments/assets/da3ce576-1178-4de9-837f-278656e72ec4)

Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module dff_const2(clk, reset, q);
  input clk;
  wire clk;
  output q;
  wire q;
  input reset;
  wire reset;
  assign q = 1'h1;
endmodule
```
Yosys screenshot:
![Screenshot from 2024-10-22 00-31-40](https://github.com/user-attachments/assets/84dd7353-74e4-4ca3-9d0a-f7512a29287d)


### D-Flipflop Constant 3 with Asynchronous Reset (active low)

Verilog code:
```
module dff_const3(input clk, input reset, output reg q); 
	reg q1;

	always @(posedge clk, posedge reset)
	begin
		if(reset)
		begin
			q <= 1'b1;
			q1 <= 1'b0;
		end
		else
		begin	
			q1 <= 1'b1;
			q <= q1;
		end
	end
endmodule
```
Simulation:
```
iverilog dff_const3.v tb_dff_const3.v
./a.out
gtkwave tb_dff_const3.vcd
```
![Screenshot from 2024-10-22 00-34-15](https://github.com/user-attachments/assets/014d8a8d-ae10-4144-943f-7636258b2459)

Commands for netlist:
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_const3.v
4. synth -top dff_const3
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_const3_net.v
9. !gvim dff_const3_net.v
```
Netlist:
![Screenshot from 2024-10-22 00-35-53](https://github.com/user-attachments/assets/548d896d-7faa-4753-a333-364dd0c014e0)

Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module dff_const3(clk, reset, q);
  wire _0_;
  wire _1_;
  input clk;
  wire clk;
  output q;
  wire q;
  wire q1;
  input reset;
  wire reset;
  assign _0_ = ~reset;
  assign _1_ = ~reset;
  sky130_fd_sc_hd__dfstp_2 _4_ (
    .CLK(clk),
    .D(q1),
    .Q(q),
    .SET_B(_0_)
  );
  sky130_fd_sc_hd__dfrtp_1 _5_ (
    .CLK(clk),
    .D(1'h1),
    .Q(q1),
    .RESET_B(_1_)
  );
endmodule
```

Yosys screenshot:
![Screenshot from 2024-10-22 00-35-11](https://github.com/user-attachments/assets/6d054b53-6717-4b2a-9db8-c50afebf7246)


### D-Flipflop Constant 4 with Asynchronous Reset (active high)

Verilog code:
```
module dff_const4(input clk, input reset, output reg q); 
	reg q1;

	always @(posedge clk, posedge reset)
	begin
		if(reset)
		begin
			q <= 1'b1;
			q1 <= 1'b1;
		end
		else
		begin	
			q1 <= 1'b1;
			q <= q1;
		end
	end
endmodule
```
Simulation:
```
iverilog dff_const4.v tb_dff_const4.v
./a.out
gtkwave tb_dff_const4.vcd
```
![Screenshot from 2024-10-22 00-38-53](https://github.com/user-attachments/assets/ca850136-144c-46a7-8d28-f71a84ade6e4)


Commands for netlist:
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_const4.v
4. synth -top dff_const4
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_const4_net.v
9. !gvim dff_const4_net.v
```
Netlist:
![Screenshot from 2024-10-22 00-40-31](https://github.com/user-attachments/assets/701dffb3-979c-4fe6-8b69-14069bd30937)

Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module dff_const4(clk, reset, q);
  input clk;
  wire clk;
  output q;
  wire q;
  wire q1;
  input reset;
  wire reset;
  assign q = 1'h1;
  assign q1 = 1'h1;
endmodule
```
Yosys screenshot:
![Screenshot from 2024-10-22 00-39-56](https://github.com/user-attachments/assets/b23d4837-d1d7-440f-9831-ac3e7f17603f)

#### D-Flipflop Constant 5 with Asynchronous Reset

Verilog code:
```
module dff_const5(input clk, input reset, output reg q); 
	reg q1;

	always @(posedge clk, posedge reset)
	begin
		if(reset)
		begin
			q <= 1'b0;
			q1 <= 1'b0;
		end
		else
		begin	
			q1 <= 1'b1;
			q <= q1;
		end
	end
endmodule
```
Simulation:
```
iverilog dff_const5.v tb_dff_const5.v
./a.out
gtkwave tb_dff_const5.vcd
```
![Screenshot from 2024-10-22 00-42-05](https://github.com/user-attachments/assets/0de40b49-cf03-4e78-9336-32a10b942d36)


Commands for netlist:
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog dff_const5.v
4. synth -top dff_const5
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr dff_const5_net.v
9. !gvim dff_const5_net.v
```
Netlist:
![Screenshot from 2024-10-22 00-43-33](https://github.com/user-attachments/assets/fcd3a37b-ff8f-4b2d-81e2-b545cc87389f)

Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module dff_const5(clk, reset, q);
  wire _0_;
  wire _1_;
  input clk;
  wire clk;
  output q;
  wire q;
  wire q1;
  input reset;
  wire reset;
  assign _0_ = ~reset;
  assign _1_ = ~reset;
  sky130_fd_sc_hd__dfrtp_1 _4_ (
    .CLK(clk),
    .D(q1),
    .Q(q),
    .RESET_B(_0_)
  );
  sky130_fd_sc_hd__dfrtp_1 _5_ (
    .CLK(clk),
    .D(1'h1),
    .Q(q1),
    .RESET_B(_1_)
  );
endmodule
```
Yosys screenshot:
![Screenshot from 2024-10-22 00-42-51](https://github.com/user-attachments/assets/8229febb-ecef-455d-bd58-5e565926b1af)

### Counter Optimization 1:

Verilog code:
```
module counter_opt (input clk, input reset, output q);
	reg [2:0] count;
	assign q = count[0];
	
	always @(posedge clk,posedge reset)
	begin
		if(reset)
			count <= 3'b000;
		else
			count <= count + 1;
	end
endmodule
```
Simulation:

```
iverilog counter_opt.v tb_counter_opt.v
./a.out
gtkwave tb_counter_opt.vcd
```
Commands for netlist:
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog counter_opt.v
4. synth -top counter_opt
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show
8. write_verilog -noattr counter_opt.v
9. !gvim counter_opt.v

```

Netlist:
![Screenshot from 2024-10-22 00-47-14](https://github.com/user-attachments/assets/4f1711a2-c2ad-4fbf-b745-4c1b0d359519)

Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module counter_opt(clk, reset, q);
  wire [2:0] _0_;
  wire _1_;
  input clk;
  wire clk;
  wire [2:0] count;
  output q;
  wire q;
  input reset;
  wire reset;
  assign _0_[0] = ~count[0];
  assign _1_ = ~reset;
  sky130_fd_sc_hd__dfrtp_1 _4_ (
    .CLK(clk),
    .D(_0_[0]),
    .Q(count[0]),
    .RESET_B(_1_)
  );
  assign _0_[2:1] = count[2:1];
  assign q = count[0];
endmodule
```

Yosys screenshot:
![Screenshot from 2024-10-22 00-46-29](https://github.com/user-attachments/assets/9ed0a88c-fede-433f-910b-d120d0a18880)


#### Counter Optimization 2:

Verilog code:
```
module counter_opt2 (input clk, input reset, output q);
	reg [2:0] count;
	assign q = (count[2:0] == 3'b100);
	
	always @(posedge clk,posedge reset)
	begin
		if(reset)
			count <= 3'b000;
		else
			count <= count + 1;
	end
endmodule
```

Commands for netlist:
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog counter_opt2.v
4. synth -top counter_opt
5. dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
7. show

```
Netlist:
![Screenshot from 2024-10-22 00-56-48](https://github.com/user-attachments/assets/7e40c3a3-8881-4fe1-8bda-20f80b12a0c4)

Yosys screenshot:
![Screenshot from 2024-10-22 00-59-27](https://github.com/user-attachments/assets/784e3172-5954-4502-8aad-ba1f496d8c39)


### Day 4: GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

Verilog code	
```
module ternary_operator_mux(input i0, input i1, input sel, output y);
	assign y = sel?i1:i0;
endmodule
```
Simulation:
```
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```
![Screenshot from 2024-10-22 01-12-39](https://github.com/user-attachments/assets/e7b2e3e5-c54e-44f5-b6f1-a63dab9cf3a6)

Commands for netlist:
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog ternary_operator_mux.v
4. synth -top ternary_operator_mux
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
8. write_verilog -noattr ternary_operator_mux_net.v
9. !gvim ternary_operator_mux_net.v

```
Netlist:
![Screenshot from 2024-10-22 01-15-19](https://github.com/user-attachments/assets/d66b463b-d387-4a0e-8d6f-fa42f94e43b4)

Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module ternary_operator_mux(i0, i1, sel, y);
  input i0;
  wire i0;
  input i1;
  wire i1;
  input sel;
  wire sel;
  output y;
  wire y;
  sky130_fd_sc_hd__mux2_1 _0_ (
    .A0(i0),
    .A1(i1),
    .S(sel),
    .X(y)
  );
endmodule
```
Yosys screenshot:
![Screenshot from 2024-10-22 01-13-25](https://github.com/user-attachments/assets/6ddb8b06-eaf2-4675-ba18-fdb7afba43af)


#### Bad 2x1 MUX:

Verilog code:
```
module bad_mux(input i0, input i1, input sel, output reg y);
	always@(sel)
	begin
		if(sel)
			y <= i1;
		else
			y <= i0;
	end
endmodule
```
Simulation:
```
iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```
![Screenshot from 2024-10-22 01-16-08](https://github.com/user-attachments/assets/657ca9fa-3db2-40ad-a147-ce4d8431ac44)

Commands for netlist:
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog bad_mux.v
4. synth -top bad_mux
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
8. write_verilog -noattr bad_mux_net.v
9. !gvim bad_mux_net.v

```
Netlist:
![Screenshot from 2024-10-22 01-17-45](https://github.com/user-attachments/assets/d293eda8-6d1b-4df2-8129-a83caf9e13aa)

Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module bad_mux(i0, i1, sel, y);
  input i0;
  wire i0;
  input i1;
  wire i1;
  input sel;
  wire sel;
  output y;
  wire y;
  sky130_fd_sc_hd__mux2_1 _0_ (
    .A0(i0),
    .A1(i1),
    .S(sel),
    .X(y)
  );
endmodule
```
Yosys screenshot:
![Screenshot from 2024-10-22 01-17-05](https://github.com/user-attachments/assets/074edc54-eef7-4364-aa42-ce98fd7f3d58)

#### Blocking Caveat:

Verilog code:

```
module blocking_caveat(input a, input b, input c, output reg d);
	reg x;

	always@(*)
	begin
		d = x & c;
		x = a | b;
	end
endmodule
```
Simulation:
```
iverilog blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```
![Screenshot from 2024-10-22 01-19-40](https://github.com/user-attachments/assets/55dbb101-95ad-4bba-abb7-2d8791e84677)

Commands for netlist:
```
1. yosys
2. read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
3. read_verilog blocking_caveat.v
4. synth -top blocking_caveat
5. abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. opt_clean -purge
7. show
8. write_verilog -noattr blocking_caveat_net.v
9. !gvim blocking_caveat_net.v
```

Netlist:
![Screenshot from 2024-10-22 01-22-33](https://github.com/user-attachments/assets/b617df30-9ebf-4c75-b6cf-7a9629938dd1)

Netlist code:
```
/* Generated by Yosys 0.23 (git sha1 7ce5011c24b) */

module blocking_caveat(a, b, c, d);
  input a;
  wire a;
  input b;
  wire b;
  input c;
  wire c;
  output d;
  wire d;
  sky130_fd_sc_hd__o21a_1 _0_ (
    .A1(b),
    .A2(a),
    .B1(c),
    .X(d)
  );
endmodule
```

Yosys screenshot:
![Screenshot from 2024-10-22 01-21-07](https://github.com/user-attachments/assets/9bc04e56-4e4c-48de-a2ad-2b10315c9ec3)


# TASK-9

# Synthesize RISC-V and Compare Output with Functional Simulations



## Steps before Synthesizing the RISC-V Core

1. **Copy the `src` Folder:**  
   Transfer the `src` folder from the **VSDBabySoC** directory to the **ASIC** directory.

2. **Navigate to the Target Directory:**  
   Change to the appropriate directory where the synthesis will be performed. Use the following command:

``` 
 cd /Desktop/ASIC/sky130RTLDesignAndSynthesisWorkshop
```

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

# TASK-10

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





# TASK-11

## Task 11: Post Synthesis Static Timing Analysis using OpenSTA for all the sky130 lib files

### Constraints
![Screenshot from 2024-11-05 00-55-54](https://github.com/user-attachments/assets/b6b2c115-8a79-4dde-bf26-b19391d26529)

### TCL
![Screenshot from 2024-11-05 00-57-48](https://github.com/user-attachments/assets/857372e7-e369-4b12-bb3f-593e70b93683)

### To perform STA
![Screenshot from 2024-11-05 00-51-49](https://github.com/user-attachments/assets/a5f11cec-9226-45c8-bfce-539cd5af526d)

### Total negative slack
![Screenshot from 2024-11-05 01-27-15](https://github.com/user-attachments/assets/45ced20e-a7ad-4d55-af20-aa5f2bb6337b)

### Worst negative slack
![Screenshot from 2024-11-05 01-31-21](https://github.com/user-attachments/assets/637c16a1-4f06-4082-8228-10bcd8512ee2)

### STA worst max slack
![Screenshot from 2024-11-05 01-33-44](https://github.com/user-attachments/assets/38cba75d-72cc-437c-ba81-c7b7a363fee3)

### STA worst min slack
![Screenshot from 2024-11-05 01-43-04](https://github.com/user-attachments/assets/4c4aaf68-a52d-404e-b98e-debfb753ceab)


# TASK-12

## Theory

On an embedded board, what is commonly referred to as the "chip" is actually the package that houses the real chip. This package acts as a protective enclosure. The actual chip, manufactured separately, sits at the center of this package. Connections between the package and the chip are made using wire bonding, which involves basic wired connections.

![image](https://github.com/user-attachments/assets/cbae394d-b11c-4a98-98cb-9d12b8c1e757)

### Day-1: Inception of open-source EDA, OpenLane and Sky130 PDK

### QFN-48 Package

The Quad Flat No-leads (QFN) 48 package is a type of leadless integrated circuit (IC) package that features 48 connection pads along its perimeter. This design enhances thermal and electrical performance while maintaining a compact form factor, making it highly suitable for applications requiring high-density integration.

![image](https://github.com/user-attachments/assets/7ea9ae0c-e817-402f-820f-9a83fdd0802f)

### Chip

A chip, also known as an integrated circuit (IC), incorporates various functional blocks such as memory, processing units, and input/output (I/O) components within a silicon substrate. These chips are designed for specific applications in electronics.

![image](https://github.com/user-attachments/assets/2c3631bf-4393-4225-b126-86bbae179fab)

### Pads

Pads are small metallic areas on a chip or package that connect internal circuitry to external connections, facilitating the transfer of signals to and from the integrated circuit (IC).

### Core

The core is the central part of a chip that includes the main processing unit and functional logic. It is typically optimized for power and performance.

### Die

A die is a section of a silicon wafer containing an individual IC before it is packaged. It houses all the active circuits and elements necessary for the chip's functions.

![image](https://github.com/user-attachments/assets/97fbc8dd-c1dc-4389-b499-0bf4bce592c8)

### Foundry

A foundry is a facility where semiconductor chips are manufactured. Foundry IPs (Intellectual Properties) are specific to each foundry and require a certain level of expertise to produce. In this context, repeatable digital logic blocks are referred to as macros.

![image](https://github.com/user-attachments/assets/2eba1d13-c765-4333-b39c-2b5157cdc6d1)

### From Software Applications to Hardware Execution

Running an application on hardware involves several key steps. Initially, the application enters the system software layer, which prepares it for execution by converting the application program into a binary format that the hardware can understand. The main components of the system software include the Operating System (OS), Compiler, and Assembler.

1. **Operating System (OS)**: The OS starts the process by breaking down application functions written in high-level languages such as C, C++, Java, or Visual Basic.
2. **Compiler**: These functions are then passed to a compiler, which translates them into low-level instructions specific to the hardware architecture.
3. **Assembler**: The assembler converts these low-level instructions into binary format, known as machine language.
4. **Hardware Execution**: Finally, the binary code is fed to the hardware, enabling it to perform the tasks defined by the instructions.

This sequence ensures that high-level application code can be effectively executed by the hardware.

![image](https://github.com/user-attachments/assets/9bf73acb-aee1-472a-b425-c58545a07c05)

### Example: Stopwatch App on a RISC-V Core

Consider a stopwatch application running on a RISC-V core. The process involves several steps:

1. **Operating System (OS)**: The OS generates a small function written in C.
2. **Compiler**: This function is passed to a compiler, which produces RISC-V-specific instructions tailored to the architecture.
3. **Assembler**: These instructions are then processed by the assembler, converting them into binary code.
4. **Hardware Execution**: The binary code is fed into the chip layout, where the hardware executes the desired functionality.

This sequence ensures that the stopwatch app can effectively run on the RISC-V hardware.

![image](https://github.com/user-attachments/assets/c5f251b2-0690-4226-81fd-5c4996b0a4ff)

For the above stopwatch the below figure shows the input and output of the compiler and assembler.

![image](https://github.com/user-attachments/assets/233facdf-7f1c-41f8-b541-481ee5b15577)

The compiler generates instructions specific to the architecture, while the assembler converts these instructions into binary patterns. To execute these instructions on hardware, an RTL (Register Transfer Level) design, written in a Hardware Description Language (HDL), is used to interpret and implement the instructions. This RTL design is then synthesized into a netlist, which represents interconnected logic gates. Finally, the netlist undergoes physical design implementation to be fabricated onto the chip.

![image](https://github.com/user-attachments/assets/eca48de1-887b-4249-8ddd-5413a3ea1798)

## Components of ASIC Design

![image](https://github.com/user-attachments/assets/5bef3ab0-7e3b-42f7-a228-a687daf051c6)

### RTL IPs
Pre-designed and verified digital circuit blocks, such as adders, flip-flops, and memory, written in Hardware Description Languages (HDL) like Verilog or VHDL. These IPs save design time by providing ready-to-use components for complex circuits.

### EDA Tools
Software that automates various ASIC design tasks, including synthesis, optimization, placement, and timing analysis. These tools are essential for improving productivity and ensuring that performance and power requirements are met.

### PDK Data
A set of files and parameters provided by a semiconductor foundry, detailing its manufacturing process. This includes transistor models and design rules. PDKs ensure that ASIC designs are compatible with the foundry’s fabrication process.

### Simplified RTL to GDS flow

![image](https://github.com/user-attachments/assets/6c7e6fec-1bd5-47a2-bf9a-73650870f7d8)

### RTL Design
Describes the circuit's functional behavior using Hardware Description Languages (HDLs) like Verilog or VHDL, defining its logic and data paths.

### RTL Synthesis
Converts RTL code into a gate-level netlist, which is a collection of standard cells such as AND gates, flip-flops, and multiplexers. This process maps the RTL code to standard cells and optimizes for area, power, and timing.

### Floor and Power Planning
Partitions the chip area, places major components, and defines the power grid and I/O placement. This step optimizes the physical layout to reduce power consumption and improve signal integrity by considering the placement of I/O pads and power distribution cells.

### Placement
Assigns physical locations to cells, aiming to minimize wirelength, reduce signal delay, and meet design constraints. The placement tool arranges the cells to balance the overall chip design for optimal performance and area utilization.

### Clock Tree Synthesis (CTS)
Focuses on creating an optimized clock distribution network. CTS ensures the clock is distributed evenly to all flip-flops and registers, building an optimized clock network to balance clock signal distribution and reduce clock skew.

### Routing
Connects components based on placement, optimizing wire paths to ensure signal integrity, minimize congestion, and meet design rules.

### Sign-off
The final verification stage, ensuring the design meets functionality, performance, power, and reliability targets. Timing analysis checks setup and hold times, power analysis ensures the design doesn’t exceed power limits, and physical verification checks that the layout meets manufacturing rules. This stage confirms the design is ready for fabrication.

### GDSII File Generation
Creates the GDSII file containing the complete layout details needed for chip fabrication. This file represents the final physical design and is used by manufacturers to create the photomasks required for chip production. The GDSII file serves as the blueprint for the actual fabrication of the chip.

### OpenLane ASIC Flow:

![image](https://github.com/user-attachments/assets/a93ccf1c-cd36-4e01-8fb6-ffe832b47372)

### RTL Synthesis, Technology Mapping, and Formal Verification
- **Tools Used**: Yosys (for RTL synthesis), ABC (for technology mapping and formal verification).

### Static Timing Analysis
- **Tools Used**: OpenSTA (for static timing analysis).

### Floor Planning
- **Tools Used**: init_fp (initial floorplanning), ioPlacer (I/O placement), pdn (power distribution network planning), tapcell (tap cell insertion).

### Placement
- **Tools Used**: RePLace (global placement), Resizer (optional for resizing cells), OpenPhySyn (formerly used for placement), OpenDP (detailed placement).

### Clock Tree Synthesis
- **Tools Used**: TritonCTS (for clock tree synthesis).

### Fill Insertion
- **Tools Used**: OpenDP (for filler placement).

### Routing
- **Tools Used**: FastRoute or CU-GR (formerly used) for global routing, TritonRoute (for detailed routing) or DR-CU (formerly used).

### SPEF Extraction
- **Tools Used**: OpenRCX (or SPEF-Extractor, formerly used) for Standard Parasitic Exchange Format (SPEF) extraction.

### GDSII Streaming Out
- **Tools Used**: Magic and KLayout (for viewing and editing GDSII files).

### Design Rule Checking (DRC) Checks
- **Tools Used**: Magic and KLayout (for DRC checks).

### Layout vs. Schematic (LVS) Check
- **Tools Used**: Netgen (for LVS checks).

### Antenna Checks
- **Tools Used**: Magic (for antenna checks).

## Implementation

## Synthesis in Openlane

### Running Commands in VSD Virtual Box

To execute commands in the VSD Virtual Box, follow these steps:

1. **Open the VSD Virtual Box**: Ensure that the virtual machine is running.
2. **Run the following commands**:

   
```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
```

![image](https://github.com/user-attachments/assets/89e518d7-1221-4828-ad90-43d4b36d47db)

![image](https://github.com/user-attachments/assets/4fd9a13e-d70d-4d69-a131-0cf2280bd296)

To view the netlist:

```
cd designs/picorv32a/runs/11-11_19-02/results/synthesis/
gedit picorv32a.synthesis.v
```

![image](https://github.com/user-attachments/assets/85d4e2a8-b690-4da9-bea4-ad57f70220b4)



Netlist Code:

![Screenshot 2024-11-12 004552](https://github.com/user-attachments/assets/367450ce-ac5e-4af0-bca3-c9b7078b2c5a)


Yosys report:

```
cd /Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/11-11_19-02/reports/synthesis
gedit 1-yosys_4.stat.rpt
```

![image](https://github.com/user-attachments/assets/e951e4ba-66ae-4629-a834-8a406abb8013)

### Report:

![image](https://github.com/user-attachments/assets/1f6d202b-97b1-4407-828e-15951562b57a)

```
28. Printing statistics.

=== picorv32a ===

   Number of wires:              14596
   Number of wire bits:          14978
   Number of public wires:        1565
   Number of public wire bits:    1947
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:              14876
     sky130_fd_sc_hd__a2111o_2       1
     sky130_fd_sc_hd__a211o_2       35
     sky130_fd_sc_hd__a211oi_2      60
     sky130_fd_sc_hd__a21bo_2      149
     sky130_fd_sc_hd__a21boi_2       8
     sky130_fd_sc_hd__a21o_2        57
     sky130_fd_sc_hd__a21oi_2      244
     sky130_fd_sc_hd__a221o_2       86
     sky130_fd_sc_hd__a22o_2      1013
     sky130_fd_sc_hd__a2bb2o_2    1748
     sky130_fd_sc_hd__a2bb2oi_2     81
     sky130_fd_sc_hd__a311o_2        2
     sky130_fd_sc_hd__a31o_2        49
     sky130_fd_sc_hd__a31oi_2        7
     sky130_fd_sc_hd__a32o_2        46
     sky130_fd_sc_hd__a41o_2         1
     sky130_fd_sc_hd__and2_2       157
     sky130_fd_sc_hd__and3_2        58
     sky130_fd_sc_hd__and4_2       345
     sky130_fd_sc_hd__and4b_2        1
     sky130_fd_sc_hd__buf_1       1656
     sky130_fd_sc_hd__buf_2          8
     sky130_fd_sc_hd__conb_1        42
     sky130_fd_sc_hd__dfxtp_2     1613
     sky130_fd_sc_hd__inv_2       1615
     sky130_fd_sc_hd__mux2_1      1224
     sky130_fd_sc_hd__mux2_2         2
     sky130_fd_sc_hd__mux4_1       221
     sky130_fd_sc_hd__nand2_2       78
     sky130_fd_sc_hd__nor2_2       524
     sky130_fd_sc_hd__nor2b_2        1
     sky130_fd_sc_hd__nor3_2        42
     sky130_fd_sc_hd__nor4_2         1
     sky130_fd_sc_hd__o2111a_2       2
     sky130_fd_sc_hd__o211a_2       69
     sky130_fd_sc_hd__o211ai_2       6
     sky130_fd_sc_hd__o21a_2        54
     sky130_fd_sc_hd__o21ai_2      141
     sky130_fd_sc_hd__o21ba_2      209
     sky130_fd_sc_hd__o21bai_2       1
     sky130_fd_sc_hd__o221a_2      204
     sky130_fd_sc_hd__o221ai_2       7
     sky130_fd_sc_hd__o22a_2      1312
     sky130_fd_sc_hd__o22ai_2       59
     sky130_fd_sc_hd__o2bb2a_2     119
     sky130_fd_sc_hd__o2bb2ai_2     92
     sky130_fd_sc_hd__o311a_2        8
     sky130_fd_sc_hd__o31a_2        19
     sky130_fd_sc_hd__o31ai_2        1
     sky130_fd_sc_hd__o32a_2       109
     sky130_fd_sc_hd__o41a_2         2
     sky130_fd_sc_hd__or2_2       1088
     sky130_fd_sc_hd__or2b_2        25
     sky130_fd_sc_hd__or3_2         68
     sky130_fd_sc_hd__or3b_2         5
     sky130_fd_sc_hd__or4_2         93
     sky130_fd_sc_hd__or4b_2         6
     sky130_fd_sc_hd__or4bb_2        2

   Chip area for module '\picorv32a': 147712.918400
```

### Flop Ratio and Percentage of Flip Flops

```
-Flop Ratio: 1613/14876 = 0.108429685

-Percentage of Flip Flops: 0.108429685* 100 = 10.84296854%
```
## Day-2: Good floorplan vs bad floorplan and introduction to library cells

### Utilization Factor and Aspect Ratio

In IC floor planning, the utilization factor and aspect ratio are crucial parameters:

- **Utilization Factor**: This is the ratio of the area occupied by the netlist to the total core area. While a perfect utilization of 1 (100%) is ideal, practical designs typically target a factor of 0.5 to 0.6. This allows space for buffer zones, routing channels, and future adjustments.

Utilisation Factor =  Area occupied by netlist/Total area of core

- **Aspect Ratio**: Defined as the height divided by the width, this parameter indicates the chip’s shape. An aspect ratio of 1 denotes a square layout, while other values result in a rectangular layout. The aspect ratio is chosen based on functional, packaging, and manufacturing needs.

Aspect Ratio =  Height/ Width

### Pre-placed Cells
Pre-placed cells are critical functional blocks, such as memory units, custom processors, and analog circuits, that are manually positioned in fixed locations. These blocks are essential for the chip’s performance and remain stationary during placement and routing to maintain their functionality and layout integrity.

### Decoupling Capacitors
Decoupling capacitors are strategically placed near logic circuits to stabilize power supply voltages during transient events. They act as local energy reserves, helping to reduce voltage fluctuations, crosstalk, and electromagnetic interference (EMI), thereby ensuring reliable power delivery to sensitive circuits.

### Power Planning
Effective power planning involves creating a power and ground mesh to distribute VDD and VSS evenly across the chip. This ensures stable power delivery, minimizes voltage drops, and enhances overall efficiency. Multiple power and ground points help reduce the risk of instability and voltage drop issues, supporting the design’s power requirements effectively.

### Pin Placement
Pin placement, or I/O planning, is vital for functionality and reliability. Strategic pin assignment helps minimize signal degradation, preserve data integrity, and manage heat dissipation. Proper positioning of power and ground pins supports thermal management and enhances signal strength, contributing to overall system stability and manufacturability.

### Floorplanning using OpenLANE

To perform floorplanning using OpenLANE, follow these steps:

1. **Open the VSD Virtual Box**: Ensure that the virtual machine is running.
2. **Run the following commands**:

   ```
   cd Desktop/work/tools/openlane_working_dir/openlane
   docker
   ```
```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
run_floorplan
```

![image](https://github.com/user-attachments/assets/47e727c3-5172-4372-89c0-dd4c5424e65b)

Run the below commands in a new terminal:

```
cd /Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-11_09-39/results/floorplan
gedit picorv32a.floorplan.def
```

![Screenshot 2024-11-12 151931](https://github.com/user-attachments/assets/5b7604eb-f60a-426c-a274-1a9d1e4dc449)

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-11_09-39/results/floorplan/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

![Screenshot 2024-11-12 162617](https://github.com/user-attachments/assets/eedbf3d8-464e-445f-bda6-12bc16877a32)

![image](https://github.com/user-attachments/assets/2f0e204b-b90a-41e8-81fe-6e62b84e9705)

Equidistant placement of ports:

![image](https://github.com/user-attachments/assets/eb62f673-fcdf-466d-ad5e-b61ff8e21573)

Unplaced standard cells at origin:

Diagonally equidistant Tap cells
![image](https://github.com/user-attachments/assets/6f9a6cdc-84cb-4b2c-adaa-4ca1c1a06bd1)

![image](https://github.com/user-attachments/assets/84b4285a-d828-46c3-aae8-8a79e95f4668)

![image](https://github.com/user-attachments/assets/ca7d5e2b-90f2-4429-b9a0-0a341edb50c5)

![image](https://github.com/user-attachments/assets/0a34e930-2f36-428e-a05a-9ecfb4ee0a3b)

Command to run placement:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
run_floorplan
run_placement
```

![image](https://github.com/user-attachments/assets/729a3b90-e4e3-43ec-8a7e-2d4e5325571f)

![image](https://github.com/user-attachments/assets/13d7a9be-5cfc-4881-81a6-4de294a6c25b)

To view the placement in magic:

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-11_13-18/results/placement/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![image](https://github.com/user-attachments/assets/1d2382d4-57c9-406b-969b-22db474e9eb1)

![image](https://github.com/user-attachments/assets/801e2bf3-66ab-4089-8ff0-72d65ca0629c)

## Day-3: Design library cell using Magic Layout and ngspice characterization

## Steps

1. Clone the custom inverter standard cell design from the specified GitHub repository.
2. Load the custom inverter layout in Magic for examination and modification.
3. Extract the SPICE netlist of the inverter in Magic.
4. Edit the SPICE model file to prepare for simulation analysis.
5. Perform post-layout simulations in NGSPICE.
6. Identify and resolve any issues found in the DRC (Design Rule Check) section of the Magic tech file for the SkyWater process.

Clone the custom inverter standard cell design from the GitHub repository.

```
cd Desktop/work/tools/openlane_working_dir/openlane
git clone https://github.com/nickson-jose/vsdstdcelldesign
cd vsdstdcelldesign
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .
ls
magic -T sky130A.tech sky130_taninv.mag &
```

![image](https://github.com/user-attachments/assets/223bbcb9-d09a-458f-8cb7-1963711cc9fc)

NMOS and PMOS 

![image](https://github.com/user-attachments/assets/a83a8c7e-9ae4-4389-aa83-ebb97e663ace)

![image](https://github.com/user-attachments/assets/5efad971-36a2-4200-97dc-630e669859a8)

Output Y connectivity to PMOS and NMOS drain verified:
![image](https://github.com/user-attachments/assets/6442276a-7b45-4e90-9a2d-60f625b8b036)

PMOS source connectivity to VDD (here VPWR) verified
![image](https://github.com/user-attachments/assets/48eb8251-2fb3-4a3c-9b14-3a6ae3637fde)

NMOS source connectivity to VSS (here VGND) verified
![image](https://github.com/user-attachments/assets/0583fafa-4c0d-46e4-801a-debb58bf3220)

Spice extraction of inverter in Magic. Run these in the tkcon window:

```
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```
![image](https://github.com/user-attachments/assets/12635452-b6e3-46b5-bdfd-dd290d685401)

To view the spice file:

```
gedit sky130_taninv.spice
```

![image](https://github.com/user-attachments/assets/e8d20585-5f1c-415e-99eb-9044af838e8f)

Modify the sky130_taninv.spice file to find the transient respone:

```
* SPICE3 file created from sky130_taninv.ext - technology: sky130A

.option scale=0.01u
.include ./libs/pshort.lib
.include ./libs/nshort.lib

//.subckt sky130_taninv A Y VPWR VGND
M1000 Y A VGND VGND nshort_model.0 w=35 l=23
+  ad=1.44n pd=0.152m as=1.37n ps=0.148m
M1001 Y A VPWR VPWR pshort_model.0 w=37 l=23
+  ad=1.44n pd=0.152m as=1.52n ps=0.156m

VDD VPWR 0 3.3V
VSS VGND 0 0V
Va A VGND PULSE(0V 3.3V 0 0.1ns 0.1ns 2ns 4ns)

C0 A VPWR 0.0774f
C1 VPWR Y 0.117f
C2 A Y 0.0754f
C3 Y VGND 2f
C4 A VGND 0.45f
C5 VPWR VGND 0.781f
//.ends

.tran 1n 20n
.control
run
.endc
.end
```

Simulate the spice netlist

```
ngspice sky130_taninv.spice
```

![image](https://github.com/user-attachments/assets/4df99bd4-1160-4c35-85fd-d624c6c9d6c2)

Plot the waveform:

```
plot y vs time a
```

![image](https://github.com/user-attachments/assets/c62ee86e-75b1-4882-a131-92334a027141)

![image](https://github.com/user-attachments/assets/f44b095d-10b9-4308-88c0-1d17bb09bae7)

Using this transient response, we will now characterize the cell's slew rate and propagation delay:

Rise Transition: Time taken for the output to rise from 20% to 80% of max value Fall Transition: Time taken for the output to fall from 80% to 20% of max value Cell Rise delay: difference in time(50% output rise) to time(50% input fall) Cell Fall delay: difference in time(50% output fall) to time(50% input rise)

# Cell Characterization: Slew Rate and Propagation Delay

To characterize the cell's transient response, we will measure its slew rate and propagation delay as follows:

- **Rise Transition**  
  The time required for the output to rise from 20% to 80% of its maximum value.

- **Fall Transition**  
  The time required for the output to fall from 80% to 20% of its maximum value.

- **Cell Rise Delay**  
  The time difference between the input falling to 50% of its amplitude and the output rising to 50%.

- **Cell Fall Delay**  
  The time difference between the input rising to 50% of its amplitude and the output falling to 50%.

maxm value:3.3V

20% screenshot
![image](https://github.com/user-attachments/assets/b6409d9f-0fb5-4d7b-804e-70bce2d90917)

80% Screenshot

![image](https://github.com/user-attachments/assets/3f9e7c8e-696e-4eb9-9fb6-e7478a0cc7d5)

50% Screenshot

![image](https://github.com/user-attachments/assets/eafe2b82-ace5-4422-a636-ae52e91d4ddd)


Rise Transition : 2.24638 - 2.18242 =  0.06396 ns = 63.96 ps
Fall Transition : 4.0955 - 4.05536 =  0.0419 ns = 41.9 ps
Cell Rise Delay : 2.21144 - 2.15008 = 0.06136 ns = 61.36 ps
Cell Fall Delay : 4.07807 - 4.05 =0.02 ns = 20 ps

Magic Tool options and DRC Rules:

Go to home directory and run the below commands:

```
cd
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
cd drc_tests
ls -al
gvim .magicrc
magic -d XR &
```
![image](https://github.com/user-attachments/assets/acaed5f5-7d79-4700-abd4-486e3a931095)

Load the poly file by load poly.mag on tkcon window.

![image](https://github.com/user-attachments/assets/ae6122f7-02ad-453e-b84b-8515293420f1)

### Correction of Incorrectly Implemented `poly.9` Rule

The `poly.9` rule was not implemented correctly, requiring a simple correction. Please refer to the screenshot of the poly rules for specific details on the intended rule structure and constraints.

![image](https://github.com/user-attachments/assets/369b6c9d-79eb-40f0-a5bd-feac0626078f)

Add the below commands in the sky130A.tech

![image](https://github.com/user-attachments/assets/2a9eb0d3-1db7-4b0e-8e1d-8ac0915ea34b)

![image](https://github.com/user-attachments/assets/99e5f9cc-ae0f-4095-a868-413db1c989ab)

Run the commands in tkcon window:

```
tech load sky130A.tech
drc check
drc why
```

![image](https://github.com/user-attachments/assets/c6b7dca0-ae5d-4f6b-bed4-1b34407f2dcf)
![image](https://github.com/user-attachments/assets/1708b6c0-5f74-44d8-8547-439ca6cde1fa)


# Day-4: Pre-layout timing analysis and importance of good clock tree

Custom Inverter Cell Integration and Validation

### 1. Fix DRC Errors and Verify Layout Readiness
   - **Objective**: Correct minor DRC (Design Rule Check) errors to ensure the layout aligns with standard requirements and is ready for integration.
   - **Verification Conditions**:
     - **Condition 1**: The input and output ports of the standard cell must align with the intersection of vertical and horizontal tracks.
     - **Condition 2**: The width of the cell should be an odd multiple of the horizontal track pitch.
     - **Condition 3**: The height of the cell should be an even multiple of the vertical track pitch.
   - **Actions**:
     - Save the finalized layout with a custom name.
     - Open and verify the layout meets all required conditions.

### 2. Generate and Copy LEF Files
   - **Objective**: Generate a LEF (Library Exchange Format) file from the completed layout for use in the design flow.
   - **Actions**:
     - Generate the LEF file.
     - Copy the generated LEF file and associated `.lib` files to the `src` directory of the `picorv32a` design.

### 3. Update Configuration and Add New Files to OpenLane
   - **Objective**: Update the configuration to incorporate the custom inverter and library files.
   - **Actions**:
     - Open `config.tcl`.
     - Modify it to include the new library file and custom LEF file in the OpenLane flow.
     - Run OpenLane synthesis, integrating the custom inverter cell.

### 4. Reduce DRC and Other Violations
   - **Objective**: Resolve any violations introduced by the custom inverter cell.
   - **Actions**:
     - Analyze new violations and adjust design parameters to mitigate them.
     - Ensure synthesis completes successfully with the custom cell integrated.

### 5. Proceed with Floorplanning and Placement
   - **Objective**: Run floorplanning and placement to ensure the custom inverter is correctly placed.
   - **Actions**:
     - Begin floorplanning and placement once synthesis is complete and violations are addressed.
     - Verify that the custom cell is recognized and placed correctly in the Place and Route (PnR) flow.

### 6. Timing Analysis and Optimization
   - **Objective**: Perform timing analysis and apply fixes to optimize design timing.
   - **Actions**:
     - Run a post-synthesis timing analysis using OpenSTA.
     - Apply timing ECO (Engineering Change Order) fixes to remove any timing violations.
     - Replace the old netlist with the updated, timing-corrected netlist.
     - Implement the floorplan, placement, and clock tree synthesis (CTS).

### 7. Post-CTS Timing Analysis
   - **Objective**: Analyze timing performance post-CTS and explore potential optimizations.
   - **Actions**:
     - Perform a post-CTS timing analysis in OpenROAD.
     - Remove `sky130_fd_sc_hd__clkbuf_1` cell from the `CTS_CLK_BUFFER_LIST` to assess timing performance without this buffer.

## Commands and Tools
- Use OpenLane and OpenROAD for synthesis, placement, and timing analysis.
- Open the custom inverter layout to verify and modify as required to meet integration conditions.

Commands to extract tracks.info file:

```
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
cd ../../pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd/
less tracks.info
```

![image](https://github.com/user-attachments/assets/b60e9371-8418-48fd-9d1e-4054f0f2f2cf)

Commands to open the custom inverter layout

```
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_taninv.mag &
```

![image](https://github.com/user-attachments/assets/5a310200-ccec-4abd-9582-342fa3fa3b78)


Commands for tkcon window to set grid as tracks of locali layer
```
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```
The grid lines indicate where routing for the local interconnect layer is allowed, with spacing between grid lines representing the required wire pitch. The layout below demonstrates that these guidelines are adhered to.

Condition 1 verified
![image](https://github.com/user-attachments/assets/b138b7e8-44b8-4cf3-8d21-9dc02f1506dd)

Condition 2 verified

![image](https://github.com/user-attachments/assets/b2f60dd1-9443-48be-979f-3d92ee4723e7)

Type the following command in tkcon window:

```
lef write
```

![image](https://github.com/user-attachments/assets/0735f65f-71a3-44e3-bf9e-e818caaa57d1)

Screenshot of newly created lef file

![image](https://github.com/user-attachments/assets/2266dc24-ff94-4848-ad7f-7f111ef9e52d)

Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory. Commands to copy necessary files to 'picorv32a' design 'src' directory

```
cp sky130_taninv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
![image](https://github.com/user-attachments/assets/5cc32f2c-7229-4e94-baf6-5ca2a4e9e618)

Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow. Commands to be added to config.tcl to include custom cell in the openlane flow

```
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

Run openlane flow synthesis:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
```

```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```

![image](https://github.com/user-attachments/assets/ef2112e6-700e-42b7-a5d8-228caea662cc)

![image](https://github.com/user-attachments/assets/48a6be4d-0c94-4b7a-9604-3b320035ec9b)

![image](https://github.com/user-attachments/assets/77811830-b77b-41f1-b057-c43f39d16346)


Commands to view and change parameters to improve timing and run synthesis

```
prep -design picorv32a -tag 24-03_10-03 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
echo $::env(SYNTH_STRATEGY)
set ::env(SYNTH_STRATEGY) "DELAY 3"
echo $::env(SYNTH_BUFFERING)
echo $::env(SYNTH_SIZING)
set ::env(SYNTH_SIZING) 1
echo $::env(SYNTH_DRIVING_CELL)
run_synthesis
```
![image](https://github.com/user-attachments/assets/9501f822-6bae-4aa6-92bc-f6b50854c9b2)

![image](https://github.com/user-attachments/assets/067da430-c7dd-4f9b-979f-783200372f1d)

![image](https://github.com/user-attachments/assets/3ef70de4-bce7-4f3a-b0fa-b91b90c6b81e)


Run floorplan using following command:

```
run_floorplan
```
![WhatsApp Image 2024-11-14 at 04 22 50_d486d74c](https://github.com/user-attachments/assets/0d6944e8-afca-4bf9-af9f-8df39aacbba0)


```
init_floorplan
place_io
tap_decap_or
```
![image](https://github.com/user-attachments/assets/53ab6716-1da4-41fb-9bf7-4c76c77a6678)

![image](https://github.com/user-attachments/assets/1eea5d4f-e2ab-4681-8222-844473ccd886)

![image](https://github.com/user-attachments/assets/43cdee28-c7a9-4324-b331-cc93e93b567d)

![image](https://github.com/user-attachments/assets/7cc3dcfc-1b03-4955-a956-1652b83c1021)

![image](https://github.com/user-attachments/assets/3cb9c068-6a89-45af-851f-4121b8f89c45)

![image](https://github.com/user-attachments/assets/737989da-f8a6-4f90-823b-8a117783795f)

Open a new terminal and run the below commands to load placement def in magic

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_12-31/results/placement/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

```
![image](https://github.com/user-attachments/assets/58895c40-1be4-40e0-9908-e6cc59a38b60)

Custom inverter inserted in placement def
inverter: taninv

![WhatsApp Image 2024-11-14 at 04 47 02_650a002f](https://github.com/user-attachments/assets/e8564dcc-db1e-4c85-8d05-707ce9389f58)

![WhatsApp Image 2024-11-14 at 04 46 37_f00ce1a7](https://github.com/user-attachments/assets/f44b890e-0708-41c9-a0cb-742f2ea074e4)
![WhatsApp Image 2024-11-14 at 04 47 02_b34378a6](https://github.com/user-attachments/assets/22b10ef1-8918-4717-b988-1057c98a1841)

![WhatsApp Image 2024-11-14 at 17 15 11_ded699e1](https://github.com/user-attachments/assets/34888362-2ee7-4ea2-b795-77453845b6a0)

Select the cell and type expand in tkcon window to view internal layers of cells

![WhatsApp Image 2024-11-14 at 04 47 48_731a2bd6](https://github.com/user-attachments/assets/881bda06-4088-4682-b5e8-858d2585f43c)

![WhatsApp Image 2024-11-14 at 17 15 11_604a0db3](https://github.com/user-attachments/assets/2705653c-8a06-47f6-826f-c3e1f626a78a)

![WhatsApp Image 2024-11-14 at 04 47 48_5f41c4ce](https://github.com/user-attachments/assets/540f4288-035e-48bf-96b8-7d3d3db9fe54)

## Post-Synthesis timing analysis with OpenSTA tool.

Since we are getting 0 wns after improved timing run, we will be doing the timing analysis on initial run of synthesis which has lots of violations and no parameters added to improve timing.

Commands to invoke the OpenLANE flow include new lef and perform synthesis:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_SIZING) 1
run_synthesis

```
![image](https://github.com/user-attachments/assets/2c8d7e8a-b191-4909-969f-dfc4a49eed61)

![image](https://github.com/user-attachments/assets/31474149-d622-407c-936f-76f1564dfd6e)

Go to: Desktop/work/tools/openlane_working_dir/openlane and create a file pre_sta.conf. The contents of the file are:

```
set_cmd_units -time ns -capacitance pF -current mA -voltage V -resistance kOhm -distance um
read_liberty -max /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib
read_liberty -min /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib
read_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_13-41/results/synthesis/picorv32a.synthesis.v
link_design picorv32a
read_sdc /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/my_base.sdc
report_checks -path_delay min_max -fields {slew trans net cap input_pin}
report_tns
report_wns
```

![image](https://github.com/user-attachments/assets/ea065f95-82e0-4298-b73e-f991c94c0c9d)

base.sdc:

```
set ::env(CLOCK_PORT) clk
set ::env(CLOCK_PERIOD) 12.000
set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
set ::env(SYNTH_DRIVING_CELL_PIN) Y
set ::env(SYNTH_CAP_LOAD) 17.65
create_clock [get_ports $::env(CLOCK_PORT)]  -name $::env(CLOCK_PORT)  -period $::env(CLOCK_PERIOD)
set IO_PCT  0.2
set input_delay_value [expr $::env(CLOCK_PERIOD) * $IO_PCT]
set output_delay_value [expr $::env(CLOCK_PERIOD) * $IO_PCT]
puts "\[INFO\]: Setting output delay to: $output_delay_value"
puts "\[INFO\]: Setting input delay to: $input_delay_value"


set clk_indx [lsearch [all_inputs] [get_port $::env(CLOCK_PORT)]]
#set rst_indx [lsearch [all_inputs] [get_port resetn]]
set all_inputs_wo_clk [lreplace [all_inputs] $clk_indx $clk_indx]
#set all_inputs_wo_clk_rst [lreplace $all_inputs_wo_clk $rst_indx $rst_indx]
set all_inputs_wo_clk_rst $all_inputs_wo_clk


# correct resetn
set_input_delay $input_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] $all_inputs_wo_clk_rst
#set_input_delay 0.0 -clock [get_clocks $::env(CLOCK_PORT)] {resetn}
set_output_delay $output_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] [all_outputs]

# TODO set this as parameter
set_driving_cell -lib_cell $::env(SYNTH_DRIVING_CELL) -pin $::env(SYNTH_DRIVING_CELL_PIN) [all_inputs]
set cap_load [expr $::env(SYNTH_CAP_LOAD) / 1000.0]
puts "\[INFO\]: Setting load to: $cap_load"
set_load  $cap_load [all_outputs]
```

![image](https://github.com/user-attachments/assets/db252faa-b437-407a-a812-91ad48c6a13a)

Commands to run STA:

```
cd Desktop/work/tools/openlane_working_dir/openlane
sta pre_sta.conf
```

![image](https://github.com/user-attachments/assets/d8f78fd6-52ab-432f-acfe-903709633a6c)

![image](https://github.com/user-attachments/assets/7c41e16a-710e-4f72-b314-75e33cc55d56)

![image](https://github.com/user-attachments/assets/8143c826-33cf-4c54-9c70-59bbb198b9c2)

Optimise synthesis.

Go to new terminal and run the following commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
prep -design picorv32a -tag 13-11_13-41 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_SIZING) 1
set ::env(SYNTH_MAX_FANOUT) 4
echo $::env(SYNTH_DRIVING_CELL)
run_synthesis
```

![image](https://github.com/user-attachments/assets/29d96444-2941-4dd7-87ed-b848d2d36ec5)

Commands to run STA:

```
cd Desktop/work/tools/openlane_working_dir/openlane
sta pre_sta.conf
```
![image](https://github.com/user-attachments/assets/6f4efc72-ef0d-42df-b478-6853cbe47207)

![image](https://github.com/user-attachments/assets/095adea8-956a-4ecb-817c-a5d9c97ab041)

Basic timing ECO

OR gate of drive strength 2 is driving 3 fanouts

![image](https://github.com/user-attachments/assets/ac74a406-2c5a-43dc-b6b8-a5965da4a8d0)

Run the following commands to optimise timing:

```
report_net -connections _12196_
replace_cell _15215_ sky130_fd_sc_hd__or2_2
report_checks -fields {net cap slew input_pins} -digits 4
```
![image](https://github.com/user-attachments/assets/faed46d6-d772-40dc-9aa1-083c29254233)

![image](https://github.com/user-attachments/assets/bfff3257-5043-476d-886f-ea7610ee2860)

![image](https://github.com/user-attachments/assets/415b258b-4b67-422d-9b56-0a85eb000815)

The timing analysis shows improvements, with the **Total Negative Slack (TNS)** reduced from **-403.54** to **-402.45** and the **Worst Negative Slack (WNS)** reduced from **-5.59** to **-5.44**.

## Clock Tree Synthesis (CTS) and Signal Integrity

Clock Tree Synthesis (CTS) techniques are selected based on specific design requirements:

- **Balanced Tree CTS**: Utilizes a balanced, binary-like tree structure to ensure equal path lengths, which minimizes clock skew. This approach provides moderate power efficiency.
  
- **H-tree CTS**: Implements an "H"-shaped structure, which is effective for covering large areas while enhancing power efficiency.
- 
![image](https://github.com/user-attachments/assets/695bb4d1-8064-4528-8442-63d0cc58b2b9)

### Clock Tree Synthesis (CTS) Techniques

Various CTS techniques are used to manage clock distribution, with each offering unique advantages depending on design needs:

- **Star CTS**: Distributes the clock from a central point to reduce skew. However, it requires additional buffering near the clock source.
  
- **Global-Local CTS**: Combines star and tree topologies, using a global tree structure across clock domains and local trees within domains. This approach balances global and local timing.
  
- **Mesh CTS**: Employs a grid-like pattern, making it suitable for structured designs that need simplicity and skew reduction.
  
- **Adaptive CTS**: Dynamically adjusts based on timing and congestion. Although it adds complexity, it provides flexibility to meet timing constraints.

### Crosstalk

Crosstalk is interference that arises from overlapping electromagnetic fields between adjacent circuits, resulting in unwanted signal coupling. In VLSI design, crosstalk can cause data corruption, timing issues, and increased power consumption. Mitigation strategies include:

- Optimized layout and routing to reduce adjacent signal interference
- Shielding critical signal paths
- Using clock gating techniques to reduce dynamic power and minimize crosstalk effects.

![image](https://github.com/user-attachments/assets/6141aaf4-6abc-4195-83b3-ac4343615616)

### Clock Net Shielding

Clock net shielding is a technique used to prevent glitches by isolating the clock network. It involves placing shield wires, connected to either **VDD** or **GND**, around the clock signals. These shield lines do not switch, thus reducing interference by isolating the clock network from other signals.

Key aspects of clock net shielding include:

- **Dedicated Routing Layers**: Use of specific layers for clock routing to further reduce interference with other signals.
- **Clock Buffers**: Placement of buffers within the clock network to maintain signal integrity across different sections of the design.
- **Clock Domain Isolation**: By isolating different clock domains, cross-domain interference is minimized, reducing the risk of metastability and helping maintain synchronization between domains.
  
![image](https://github.com/user-attachments/assets/68eb26b1-9f14-439e-aefc-01f77d6e57b6)


To insert this updated netlist to PnR flow and we can use write_verilog and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist:

Run the following commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_13-41/results/synthesis/
ls
cp picorv32a.synthesis.v picorv32a.synthesis_old.v
ls
```

![image](https://github.com/user-attachments/assets/9156d032-491e-4c96-a0da-aa587f440be0)

Verified that the netlist is overwritten

![image](https://github.com/user-attachments/assets/e4e6c364-dc36-4431-a774-5e583c968114)

Run the following commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
prep -design picorv32a -tag 13-11_13-41 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_STRATEGY) "DELAY 3"
set ::env(SYNTH_SIZING) 1
run_synthesis
init_floorplan
place_io
tap_decap_or
run_placement
run_cts
```

![image](https://github.com/user-attachments/assets/e2905a70-00a3-4beb-80b5-a6450e032ee8)

![image](https://github.com/user-attachments/assets/a26f7b79-047f-4070-934b-4ec2c8e0af98)

![image](https://github.com/user-attachments/assets/078e4c0e-4323-4f27-b419-f619a6a2fd4d)

## Post-CTS OpenROAD timing analysis.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/13-11_13-41/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/13-11_13-41/results/cts/picorv32a.cts.def
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/13-11_13-41/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
exit

```

![image](https://github.com/user-attachments/assets/8b248ebe-6810-4668-b3e0-07b4c0a7cd62)

![image](https://github.com/user-attachments/assets/cfea6227-d708-406f-bea5-a0d160788901)

![image](https://github.com/user-attachments/assets/6605cc8f-c186-42fc-847d-a49b09dd65a3)

![image](https://github.com/user-attachments/assets/0308461e-2c99-4d27-a53b-443929e0328f)


## Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

```
echo $::env(CTS_CLK_BUFFER_LIST)
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]
echo $::env(CTS_CLK_BUFFER_LIST)
echo $::env(CURRENT_DEF)
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/placement/picorv32a.placement.def
run_cts
echo $::env(CTS_CLK_BUFFER_LIST)
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/13-11_13-41/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/13-11_13-41/results/cts/picorv32a.cts.def
write_db pico_cts1.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/13-11_13-41/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -fields {slew transd net cap input_pins} -format full_clock_expanded -digits 4
report_clock_skew -hold
report_clock_skew -setup
exit
echo $::env(CTS_CLK_BUFFER_LIST)
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]
echo $::env(CTS_CLK_BUFFER_LIST)
```
![image](https://github.com/user-attachments/assets/6dd8698d-89ee-4923-998a-d9130819aa63)

![image](https://github.com/user-attachments/assets/0971551a-3a23-41fa-a4ba-355e1efd9906)

## **Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA**

### Maze Routing and Lee's algorithm

### Routing in Physical Design

Routing establishes physical connections between pins on a routing grid, ensuring signal paths across the design. Algorithms such as **Maze Routing** (e.g., the Lee algorithm) are commonly employed to find efficient paths.

#### Lee Algorithm Overview

The **Lee algorithm** is a classic routing method that begins at a source pin and assigns incremental labels to adjacent cells, expanding until it reaches the target pin. It prioritizes **L-shaped routes** for simplicity but will use **zigzag paths** if needed to reach the destination.

- **Advantages**: The Lee algorithm is effective for finding the shortest path between two pins.
- **Limitations**: For large-scale designs, it can be slow, as it explores each grid cell incrementally, leading to increased computational load.

Due to these limitations, faster alternatives are often preferred for complex routing tasks to manage time and resource efficiency in large designs.

![image](https://github.com/user-attachments/assets/28bbd18e-fcb4-4690-926b-27c5a05948e4)

## Perform generation of Power Distribution Network (PDN) and explore the PDN layout.

![image](https://github.com/user-attachments/assets/28d6057b-1e19-48b3-b6ca-b30d90153e46)

Commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
```

```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_STRATEGY) "DELAY 3"
set ::env(SYNTH_SIZING) 1
run_synthesis
init_floorplan
place_io
tap_decap_or
run_placement
unset ::env(LIB_CTS)
run_cts
gen_pdn 
```

![image](https://github.com/user-attachments/assets/685fe370-94bb-46f6-848a-5091560c9bff)


![image](https://github.com/user-attachments/assets/9c037f24-8a88-4b1f-96bf-41a6d6d2a78a)

**Commands to load PDN def in magic in another terminal**

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_17-54/tmp/floorplan/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
```

screenshot pdn
![image](https://github.com/user-attachments/assets/6ed786ef-b39b-49d1-bbf3-8e10f5267adf)

![image](https://github.com/user-attachments/assets/db694da9-a3ac-4c09-8065-62ce543c39d4)

![image](https://github.com/user-attachments/assets/67b58375-a055-4d56-89cc-ccc209a21957)

![image](https://github.com/user-attachments/assets/14445597-50c7-4094-96db-cf14c3c9f3be)

## Perfrom detailed routing using TritonRoute and explore the routed layout.

Command:

```
echo $::env(CURRENT_DEF)
echo $::env(ROUTING_STRATEGY)
run_routing

```
![image](https://github.com/user-attachments/assets/b72fb237-3a27-4f92-8155-63ec37dd1d7d)

![image](https://github.com/user-attachments/assets/edcfe2cb-b04c-422f-b977-42ee1c9fa2a8)

### Load routed def in magic

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_17-54/results/routing/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &

```

Expanded layout showing custom inverter sky130_taninv

![image](https://github.com/user-attachments/assets/e61ee14c-a835-4665-9ed1-67f284fd01ec)

Fast route guide in openlane/designs/picorv32a/runs/13-11_17-54/tmp/routing directory

![image](https://github.com/user-attachments/assets/21c13d24-1c06-444e-9635-d91eaf8a68dc)

### Post-Route parasitic extraction using SPEF extractor.

Commands:

```
cd Desktop/work/tools/SPEF_EXTRACTOR
python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_17-54/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_17-54/results/routing/picorv32a.def
```

![image](https://github.com/user-attachments/assets/1037325d-d21f-4aa1-ae6c-e2764a09560b)

Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

Commands:

```
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/13-11_17-54/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/13-11_17-54/results/routing/picorv32a.def
write_db pico_route.db
read_db pico_route.db
read_verilog /openLANE_flow/designs/picorv32a/runs/13-11_17-54/results/synthesis/picorv32a.synthesis_preroute.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
read_spef /openLANE_flow/designs/picorv32a/runs/13-11_17-54/results/routing/picorv32a.spef
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
exit
```

![image](https://github.com/user-attachments/assets/736bb128-a7dd-4b1d-ba3b-2ad30c445297)

![image](https://github.com/user-attachments/assets/9b3d2540-104b-49ad-b703-2282fc7ba240)

![image](https://github.com/user-attachments/assets/c35e9ba6-5c90-44ed-aefc-f5fea12b0d64)



# **TASK-13**

## OpenROAD PHYSICAL DESIGN

# OpenROAD: Integrated Chip Physical Design Tool

OpenROAD is a comprehensive tool for integrated chip physical design, enabling a seamless transition from RTL to GDSII. It encompasses key stages of chip design, including synthesis, floorplanning, placement, routing, parasitic extraction, and timing analysis. 

Designed to minimize wire length using hierarchical placement algorithms, OpenROAD provides optimization features for both timing and power. Its modular architecture supports extensibility, allowing users to integrate custom algorithms and features.

## OpenROAD Flow Controllers

The OpenROAD project offers two primary flow controllers:

### 1. **OpenROAD-flow-scripts (ORFS)**

ORFS is a flow controller that provides a collection of open-source tools for automated digital ASIC design, enabling a fully automated RTL-to-GDSII design flow. Key features include:

- **Stages**: Synthesis, Placement and Routing (PnR), Static Timing Analysis (STA), Design Rule Check (DRC), and Layout Versus Schematic (LVS).
- **Flexibility**: Supports customization, allowing users to combine and configure tools based on project needs.
- **Physical Design Plugin**: Integrates OpenROAD as a plugin for physical design, offering advanced features such as hierarchical placement, global routing, and detailed routing optimization.
- **PDK Support**: Compatible with several public and private PDKs (under NDA). Publicly available PDKs include GF180, Skywater130, and ASAP7.

### 2. **OpenLane**

OpenLane, developed by Efabless, is another automated RTL-to-GDSII flow similar to ORFS. It is tailored for the Skywater130 MPW Program.

## High-Level ORFS Process (RTL to GDSII)

Below is a brief overview of the stages in the ORFS flow:

### 1. **Configuration**
   - Customize the framework to meet specific project requirements.
   - Define design parameters such as the target technology node, constraints, and tool settings.

### 2. **Design Entry**
   - Input design files in formats like Verilog.
   - Prepare design sources for further processing.

### 3. **Synthesis**
   - Convert RTL into a gate-level netlist using tools like **Yosys** and **ABC**.

### 4. **Floorplanning**
   - Determine the placement of design modules within the chip area.
   - Tools: **RePlAce**, **Capo**.

### 5. **Placement**
   - Precisely position each gate or cell in the chip area.
   - Tool: **OpenROAD**.

### 6. **Routing**
   - Connect gates and cells using metal wires to form a complete circuit.
   - Tools: **FastRoute**, **TritonRoute**.

### 7. **Layout Verification**
   - Verify the correctness of the layout using tools like **Magic**.

### 8. **GDSII Generation**
   - Generate the final GDSII layout file using tools like **Magic** and **KLayout**.

For additional details about the OpenROAD project, visit [OpenROAD's official documentation](https://theopenroadproject.org).

## Installation and setting up ORFS

### Clone and Install Dependencies

```
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts
cd OpenROAD-flow-scripts
sudo ./setup.sh
```
### Build

```
./build_openroad.sh --local
```

![Screenshot from 2024-11-23 22-37-34](https://github.com/user-attachments/assets/8a39b671-a14a-4c16-89ed-c70587e09b52)

### Verify Installation

```
source ./env.sh
yosys -help
openroad -help
exit
```
![Screenshot from 2024-11-23 22-48-51](https://github.com/user-attachments/assets/868e27ee-bef2-4355-831a-6b15058f0b2b)

![Screenshot from 2024-11-23 22-49-59](https://github.com/user-attachments/assets/b61b7269-b7b2-4162-82a7-21f24437fd23)


```
make gui_final
```


![Screenshot from 2024-11-24 21-27-58](https://github.com/user-attachments/assets/2fbe94e3-7b63-406a-85d8-f89e0fad7ba0)

### Flow structure

### ORFS Directory Structure and File formats

```
ORF/OpenROAD-flow-scripts$ source env.sh
cd flow
make
gvim Makefile
```
Commands for synthesis:

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk synth
```
![Screenshot from 2024-11-25 17-26-25](https://github.com/user-attachments/assets/032f979d-5a91-4b2c-8b88-2d24f078e1da)

![Screenshot from 2024-11-25 17-27-05](https://github.com/user-attachments/assets/ab678f83-7635-4486-95f6-378c9d5e1c88)

Synthesis netlist:

![Screenshot from 2024-11-25 17-28-52](https://github.com/user-attachments/assets/6929a168-6ceb-40b5-a930-fea619ff55db)

Synthesis log:

![Screenshot from 2024-11-25 17-32-17](https://github.com/user-attachments/assets/a9a333b9-08c6-4a9a-91e0-f0c434857e6d)

Synthesis Check:

![Screenshot from 2024-11-25 17-36-59](https://github.com/user-attachments/assets/140d7c28-f182-4329-ba89-cf4839438147)

Synthesis Stats:

![Screenshot from 2024-11-25 17-41-03](https://github.com/user-attachments/assets/11f5fa27-f961-407a-aafd-9c63bb8e9465)

![Screenshot from 2024-11-25 17-41-59](https://github.com/user-attachments/assets/368a402d-40aa-4638-a0fc-5b3801c25cfa)

Commands for floorplan:

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk floorplan
```

![Screenshot from 2024-11-25 23-08-27](https://github.com/user-attachments/assets/a008e5ca-43b7-4c96-af84-e0ff867c0417)

![Screenshot from 2024-11-25 23-07-47](https://github.com/user-attachments/assets/c2a0cde2-25d0-4330-b2dd-89ae892f761c)


```
make gui_floorplan
```
![Screenshot from 2024-11-25 23-06-31](https://github.com/user-attachments/assets/85515b4b-d0c5-46dc-8729-fcb96488e6d4)
![Screenshot from 2024-11-25 23-57-53](https://github.com/user-attachments/assets/00ee8468-8309-4c90-93c2-f757e610b2ba)
![Screenshot from 2024-11-25 23-58-22](https://github.com/user-attachments/assets/481e71c9-0fd7-463e-afaf-049a1a3e276a)


FLOORPLAN_LOG

![Screenshot from 2024-11-25 23-10-40](https://github.com/user-attachments/assets/2fb7aabc-0926-46e1-a6f6-6851bbe0b9f2)

FLOORPLAN TIMING REPORT

![Screenshot from 2024-11-26 02-32-04](https://github.com/user-attachments/assets/f4e38509-c0fe-4b69-8d9c-0dc0518e9244)
```

==========================================================================
floorplan final report_tns
--------------------------------------------------------------------------
tns 0.00

==========================================================================
floorplan final report_wns
--------------------------------------------------------------------------
wns 0.00

==========================================================================
floorplan final report_worst_slack
--------------------------------------------------------------------------
worst slack INF

==========================================================================
floorplan final report_checks -path_delay min
--------------------------------------------------------------------------
No paths found.

==========================================================================
floorplan final report_checks -path_delay max
--------------------------------------------------------------------------
No paths found.

==========================================================================
floorplan final report_checks -unconstrained
--------------------------------------------------------------------------
Startpoint: core.CPU_reset_a3$_DFF_P_ (rising edge-triggered flip-flop)
Endpoint: core.CPU_Xreg_value_a4[10][13]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop)
Path Group: unconstrained
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                  0.00    0.00    0.00 ^ core.CPU_reset_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   591    1.46   13.42    9.67    9.67 ^ core.CPU_reset_a3$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_reset_a3 (net)
                 13.42    0.00    9.67 ^ _10124_/A (sky130_fd_sc_hd__inv_1)
   464    1.04    0.00   21.17   30.85 v _10124_/Y (sky130_fd_sc_hd__inv_1)
                                         _04513_ (net)
                  0.00    0.00   30.85 v _10227_/A (sky130_fd_sc_hd__nand3_1)
    31    0.08    0.78    0.52   31.37 ^ _10227_/Y (sky130_fd_sc_hd__nand3_1)
                                         _04613_ (net)
                  0.78    0.00   31.37 ^ _10232_/B1 (sky130_fd_sc_hd__o221ai_1)
     1    0.00    0.20    0.22   31.59 v _10232_/Y (sky130_fd_sc_hd__o221ai_1)
                                         _00548_ (net)
                  0.20    0.00   31.59 v core.CPU_Xreg_value_a4[10][13]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                 31.59   data arrival time
-----------------------------------------------------------------------------
(Path is unconstrained)



==========================================================================
floorplan final report_power
--------------------------------------------------------------------------
Group                  Internal  Switching    Leakage      Total
                          Power      Power      Power      Power (Watts)
----------------------------------------------------------------
Sequential             7.92e-12   3.67e-12   1.45e-08   1.45e-08  58.0%
Combinational          1.01e-11   1.77e-11   1.04e-08   1.05e-08  42.0%
Clock                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Macro                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Pad                    0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
----------------------------------------------------------------
Total                  1.80e-11   2.13e-11   2.49e-08   2.49e-08 100.0%
                           0.1%       0.1%      99.8%
```
Commands for placement:

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk place
```
![Screenshot from 2024-11-26 00-01-03](https://github.com/user-attachments/assets/8641b14b-f8e5-4a35-836e-2627e1b7f1aa)
![Screenshot from 2024-11-26 00-07-54](https://github.com/user-attachments/assets/0e15a44b-6cfa-469e-9568-efb66f1e5879)

```
make gui_place
```
![Screenshot from 2024-11-26 00-07-18](https://github.com/user-attachments/assets/c74bdf7c-1455-4853-a88a-cd9f4a528f84)
![Screenshot from 2024-11-26 02-43-58](https://github.com/user-attachments/assets/9eefa08e-c0c5-44b1-bc55-36076af5ac19)

```

==========================================================================
detailed place report_tns
--------------------------------------------------------------------------
tns 0.00

==========================================================================
detailed place report_wns
--------------------------------------------------------------------------
wns 0.00

==========================================================================
detailed place report_worst_slack
--------------------------------------------------------------------------
worst slack INF

==========================================================================
detailed place report_checks -path_delay min
--------------------------------------------------------------------------
No paths found.

==========================================================================
detailed place report_checks -path_delay max
--------------------------------------------------------------------------
No paths found.

==========================================================================
detailed place report_checks -unconstrained
--------------------------------------------------------------------------
Startpoint: core.CPU_valid_taken_br_a4$_DFF_P_ (rising edge-triggered flip-flop)
Endpoint: core.CPU_Xreg_value_a4[15][18]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop)
Path Group: unconstrained
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                  0.76    0.00    0.00 ^ core.CPU_valid_taken_br_a4$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     2    0.01    0.04    0.46    0.46 v core.CPU_valid_taken_br_a4$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_valid_taken_br_a4 (net)
                  0.04    0.00    0.46 v _07913_/B (sky130_fd_sc_hd__or4_4)
    41    0.23    0.36    0.84    1.30 v _07913_/X (sky130_fd_sc_hd__or4_4)
                                         _02930_ (net)
                  0.36    0.02    1.31 v load_slew103/A (sky130_fd_sc_hd__buf_16)
    36    0.28    0.15    0.35    1.66 v load_slew103/X (sky130_fd_sc_hd__buf_16)
                                         net103 (net)
                  0.15    0.01    1.68 v max_cap102/A (sky130_fd_sc_hd__buf_16)
    24    0.27    0.14    0.26    1.94 v max_cap102/X (sky130_fd_sc_hd__buf_16)
                                         net102 (net)
                  0.16    0.04    1.97 v _07915_/A (sky130_fd_sc_hd__clkinv_16)
    43    0.48    0.31    0.25    2.22 ^ _07915_/Y (sky130_fd_sc_hd__clkinv_16)
                                         _02932_ (net)
                  0.37    0.11    2.33 ^ _09981_/C (sky130_fd_sc_hd__nor3_2)
     2    0.02    0.10    0.13    2.46 v _09981_/Y (sky130_fd_sc_hd__nor3_2)
                                         _04371_ (net)
                  0.10    0.00    2.46 v _09982_/B1 (sky130_fd_sc_hd__a21oi_4)
     6    0.10    0.69    0.57    3.02 ^ _09982_/Y (sky130_fd_sc_hd__a21oi_4)
                                         _04372_ (net)
                  0.69    0.00    3.02 ^ _09988_/A2 (sky130_fd_sc_hd__o21ai_4)
    16    0.12    0.32    0.36    3.39 v _09988_/Y (sky130_fd_sc_hd__o21ai_4)
                                         _04378_ (net)
                  0.32    0.00    3.39 v _11217_/A (sky130_fd_sc_hd__nor3_4)
    14    0.11    1.07    0.96    4.35 ^ _11217_/Y (sky130_fd_sc_hd__nor3_4)
                                         _05443_ (net)
                  1.07    0.00    4.35 ^ wire20/A (sky130_fd_sc_hd__buf_8)
    10    0.11    0.19    0.30    4.65 ^ wire20/X (sky130_fd_sc_hd__buf_8)
                                         net20 (net)
                  0.20    0.01    4.66 ^ _11238_/B (sky130_fd_sc_hd__nand2_4)
     5    0.04    0.22    0.13    4.79 v _11238_/Y (sky130_fd_sc_hd__nand2_4)
                                         _05460_ (net)
                  0.22    0.00    4.79 v _11253_/B1 (sky130_fd_sc_hd__o221ai_1)
     1    0.00    0.23    0.23    5.02 ^ _11253_/Y (sky130_fd_sc_hd__o221ai_1)
                                         _00713_ (net)
                  0.23    0.00    5.02 ^ core.CPU_Xreg_value_a4[15][18]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  5.02   data arrival time
-----------------------------------------------------------------------------
(Path is unconstrained)



==========================================================================
detailed place report_check_types -max_slew -max_cap -max_fanout -violators
--------------------------------------------------------------------------

==========================================================================
detailed place max_slew_check_slack
--------------------------------------------------------------------------
0.06809719651937485

==========================================================================
detailed place max_slew_check_limit
--------------------------------------------------------------------------
1.4951549768447876

==========================================================================
detailed place max_slew_check_slack_limit
--------------------------------------------------------------------------
0.0455

==========================================================================
detailed place max_fanout_check_slack
--------------------------------------------------------------------------
1.0000000150474662e+30

==========================================================================
detailed place max_fanout_check_limit
--------------------------------------------------------------------------
1.0000000150474662e+30

==========================================================================
detailed place max_capacitance_check_slack
--------------------------------------------------------------------------
0.007044170051813126

==========================================================================
detailed place max_capacitance_check_limit
--------------------------------------------------------------------------
0.19410200417041779

==========================================================================
detailed place max_capacitance_check_slack_limit
--------------------------------------------------------------------------
0.0363

==========================================================================
detailed place max_slew_violation_count
--------------------------------------------------------------------------
max slew violation count 0

==========================================================================
detailed place max_fanout_violation_count
--------------------------------------------------------------------------
max fanout violation count 0

==========================================================================
detailed place max_cap_violation_count
--------------------------------------------------------------------------
max cap violation count 0

==========================================================================
detailed place setup_violation_count
--------------------------------------------------------------------------
setup violation count 0

==========================================================================
detailed place hold_violation_count
--------------------------------------------------------------------------
hold violation count 0

==========================================================================
detailed place report_checks -path_delay max reg to reg
--------------------------------------------------------------------------
No paths found.

==========================================================================
detailed place report_checks -path_delay min reg to reg
--------------------------------------------------------------------------
No paths found.

==========================================================================
detailed place critical path target clock latency max path
--------------------------------------------------------------------------
0

==========================================================================
detailed place critical path target clock latency min path
--------------------------------------------------------------------------
0

==========================================================================
detailed place critical path source clock latency min path
--------------------------------------------------------------------------
0

==========================================================================
detailed place critical path delay
--------------------------------------------------------------------------
-1

==========================================================================
detailed place critical path slack
--------------------------------------------------------------------------
0

==========================================================================
detailed place slack div critical path delay
--------------------------------------------------------------------------
0.000000

==========================================================================
detailed place report_power
--------------------------------------------------------------------------
Group                  Internal  Switching    Leakage      Total
                          Power      Power      Power      Power (Watts)
----------------------------------------------------------------
Sequential             9.16e-12   1.10e-11   1.45e-08   1.46e-08  49.9%
Combinational          1.89e-11   4.94e-11   1.46e-08   1.46e-08  50.1%
Clock                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Macro                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Pad                    0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
----------------------------------------------------------------
Total                  2.80e-11   6.04e-11   2.91e-08   2.92e-08 100.0%
                           0.1%       0.2%      99.7%
```


Commands for cts:

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk cts
```

![Screenshot from 2024-11-26 00-13-01](https://github.com/user-attachments/assets/7d9ca9fe-3c9a-4604-bdf5-65e678a08c59)

![Screenshot from 2024-11-26 00-13-27](https://github.com/user-attachments/assets/6f344dd9-1695-4971-a9be-485747c54ecd)

```
make gui_cts
```

![Screenshot from 2024-11-26 00-14-34](https://github.com/user-attachments/assets/cf981f35-8eec-4be5-b259-9b63b3246799)
![Screenshot from 2024-11-26 02-24-28](https://github.com/user-attachments/assets/89ee1723-f878-4e0a-9ffb-87ae5d150b16)

![Screenshot from 2024-11-26 02-45-29](https://github.com/user-attachments/assets/162aaae8-5f76-44eb-9c45-8b7a5501180a)

Commands for route:

```
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk route
```

![Screenshot from 2024-11-26 00-33-55](https://github.com/user-attachments/assets/04a9f1e6-96fe-48d2-ba55-23cc855fab93)
![Screenshot from 2024-11-26 00-35-04](https://github.com/user-attachments/assets/dbd93c47-0a21-4178-ad84-13dc0b71506d)


