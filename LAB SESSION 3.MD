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
