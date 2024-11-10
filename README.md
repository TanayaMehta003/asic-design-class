# asic-design-class

## CONTENTS

1. [TASK 1](#task-1)
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







