#Lab session 3

# Identifying Instruction Types

In this activity, we identify instruction types based on the provided instructions. The 32-bit code helps in this identification process, with each instruction type having its own format.

## What are Instruction Formats in RISC-V?

Instruction formats in RISC-V act as a "contract" between the assembly language and the hardware. When the assembly language executes an instruction, the hardware knows exactly how to handle it. These formats, composed of sequences of 0s and 1s, define the type of operation, the location of data, and more. RISC-V has six types of instruction formats:

### R Type

- **Purpose**: Used for arithmetic and logical operations involving three registers.
- **Structure**: Consists of two source registers, one destination register, a function code for the operation, and an opcode.
- **Examples**: ADD, SUB, OR, XOR, etc.
- **Format**:
  - `funct7` (7 bits): Function code for additional differentiation.
  - `rs2` (5 bits): Second source register.
  - `rs1` (5 bits): First source register.
  - `funct3` (3 bits): Primary function code.
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
  - `funct3` (3 bits): Instruction differentiation code.
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
  - `funct3` (3 bits): Instruction differentiation code.
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
