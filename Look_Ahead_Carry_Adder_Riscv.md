# Carry_Look-Ahead-_Adder_RISCV


A carry-look ahead adder (CLA) or fast adder is a type of adder used in digital logic. A carry-look ahead adder improves speed by reducing the amount of time required to determine to carry bits. It calculates one or more carries before the sum, which reduces the wait time/Ripple delay to calculate the result of the larger value bits of the adder.

**The 4-bit carry look-ahead carry adder is shown in the figure given below:**

![CLA_1](https://github.com/user-attachments/assets/bf4728c5-288f-4080-a636-bd8c107ac929)


**The following shows the block diagram of 4-bit carry look-ahead adder:**

![BLOCK_DGM_1](https://github.com/user-attachments/assets/673adda9-a045-481e-a10b-e870135fec14)


**The below shows two-level logic circuit diagram of a carry look ahead adder:**

![ckt_dgm_1](https://github.com/user-attachments/assets/5edca1a7-34ec-46dd-9dab-fed9845275b6)

##**C-CODE**

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
##**Compilation of the C-program with GCC compiler:**

```bash
gcc -Ofast -o cla cla.c
./cla
```

![Screenshot 2024-08-14 184029](https://github.com/user-attachments/assets/2256e92a-3255-4911-9835-47b4c45e9c13)

**Creating the Objdump file**

```bash
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o cla.o cla.c
riscv64-unknown-elf-objdump -d cla.o | less
```

**Assembly code**

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
