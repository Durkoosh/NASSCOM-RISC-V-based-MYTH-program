# NASSCOM-RISC-V-based-MYTH-program

Welcome to this hands-on journey into digital logic design! We're diving into TL-Verilog, an innovative design language pioneered by Redwood EDA. We will use the Makerchip online IDE to design, simulate, and visualize circuits. Let’s start from the basics and quickly ramp up to more advanced concepts.

## Table of Contents 
- [Day 1 ](#day-1)
- [Day 2 ](#day-2)
- [Day 3 ](#day-3)
- [Day 4 ](#day-4)
- [Day 5 ](#day-5)

# Day 1


# Course Introduction – Summary of Key Concepts

## Section Overview
This section introduces how computers understand and execute instructions using the **Instruction Set Architecture (ISA)** — the foundational language between software and hardware.

---

## From C Program to Hardware Execution

1. A **C program** is first **compiled into assembly code**.  
2. The **assembly code** is then **assembled into machine code** — binary numbers (1s and 0s).  
3. The machine code is interpreted and executed by the **hardware**, typically a chip in your device.  
4. The chip processes the instructions and produces the **output**.

**Program Execution Flow:**

C Program → Assembly Code → Machine Code (Binary) → Execution on Chip → Output

This flow transforms high-level instructions into low-level commands that the hardware understands.

---

## Role of Hardware Description Language (HDL)

- **HDL** defines and implements hardware behavior.
- Translates architecture into logic gates and **Register Transfer Level (RTL)** operations.
- Tasks like number swapping are expressed in HDL and realized at RTL level for hardware execution.

---

## Real-World Chip Implementation

- Chip architecture is designed using HDL and synthesized into a physical hardware layout.
- User applications interact with this architecture.
- The chip executes the program and produces the output.

---

## System Software, ISA, and Application Interaction

### Application vs. System Software

- **Application software**: Programs like apps on your laptop.
- **System software**: Includes the **Operating System (OS)**, **Compiler**, and **Assembler**, which bridge applications and hardware.

### Responsibilities of the Operating System

- Manages resources like memory.
- Converts application code into machine-executable format using tools like compilers and assemblers.

---

## Compiler and ISA

- The **compiler** translates high-level programming languages (e.g., C) into instructions specific to the **ISA**.
- The syntax of these instructions depends on the hardware architecture (e.g., **RISC-V** or **x86**).

### Assembler and Machine Language

- The **assembler** converts the compiler’s instructions into **binary machine code**.
- These binary instructions control hardware components like **logic gates** and **flip-flops**.

---

## Example: Stopwatch App

- A simple stopwatch function written in C is compiled into ISA instructions.
- These instructions are assembled into binary and executed by the chip to perform the stopwatch operation.

---

## ISA as a Bridge Between Software and Hardware

- ISA serves as the **interface** between high-level software and low-level hardware.
- It abstracts the complexity of hardware and provides a usable set of instructions for software.

---

## Design Flow: High-Level to Physical Implementation

1. **ISA & Architecture**: Define the required behavior of hardware.
2. **HDL Implementation**: Express those tasks using a hardware-specific language.
3. **Physical Design**: Convert HDL into actual hardware components (flip-flops, logic gates).

---

## Course Content Overview

### Basic Arithmetic Operations

- The course starts with basic operations like addition, multiplication, and division.
- These are foundational for building applications like a scientific calculator.

### Instruction Sets

- Different instruction sets are used depending on the hardware architecture:
  - **ARM**: ARM 64-bit instructions.
  - **RISC**: Follows the RISC-specific instruction sets.
- ARM 64 instructions handle 64-bit digital data with **ARM 64 integer instructions**.

### Instruction Extensions

- Advanced operations like multiplication and division are handled through **instruction extensions**.
- Example: **ARM 64 MCP (Multiplication and Control Program)** instructions.

### Floating-Point Instructions

- Floating-point operations are handled using **Floating Point Extensions**, including single and double precision.
- Extensions like **DFAW** and **F** provide floating-point capabilities.

---

## Application Binary Interface (ABI)

- The ABI defines a standard interface for applications to interact with hardware.
- This ensures consistent access to system resources and functions.

---

## Memory Management & Data Representation

- The course explores **memory allocation** and how the stack is used to manage data.
- It also discusses **signed vs. unsigned** integers and how these are handled in the instruction set.

---

## Compilation to Execution Flow

Source Code (C) → Compiler → Architecture-Specific Instruction Set → Assembler → Machine Code (Binary)

This flow shows how a program written in C is compiled, assembled, and executed by the hardware.

---

## Tool chain 

## Step 1: Setting Up Ubuntu within VMBox

1. Install Ubuntu on VMBox.
2. Launch Ubuntu's terminal.

## Step 2: Install Leafpad

```bash
$ sudo apt install leafpad
```
Navigate to the home directory:
```
$ cd
```
```
$ leafpad filename.c &
```
![1 1](https://github.com/user-attachments/assets/543bca53-599c-4a19-befc-5debe059240d)

## Step 3: Compile and Run the C Code
Compile the C code:

```

$ gcc filename.c

```
Run the compiled program:
```
$ ./a.out
```
![1 2](https://github.com/user-attachments/assets/f62fddff-7fe7-48ab-b7c4-5ee047391004)

## Step 4: Compile C Code with RISC-V Compiler
Compile the C code using the RISC-V compiler:
```
$ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o filename.o filename.c
```
| Part                       | Meaning                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------|
| `riscv64-unknown-elf-gcc`  | The **RISC-V GCC cross-compiler** used to compile code for RISC-V (not your host machine).   |
| `-O1`                      | Enables **optimization level 1** (moderate optimization for performance and size).           |
| `-mabi=lp64`               | Sets the **ABI (Application Binary Interface)** to `lp64`:                                   |
|                            | • `l` = long integers (64-bit)                                                               |
|                            | • `p` = pointers (64-bit)                                                                    |
| `-march=rv64i`             | Targets the **RISC-V 64-bit architecture** with the base **integer (I)** instruction set.    |
| `-o sum1ton.o`             | Specifies the **output file name**, which will be an object file (`.o`).                     |
| `sum1ton.c`                | The **input source file** written in C.                                                      |

List the compiled object file:

```
$ ls -ltr filename.o
```

![1 3](https://github.com/user-attachments/assets/4c98864d-ee55-4156-aff3-03b9b49020cf)
![1 4](https://github.com/user-attachments/assets/a7ae9278-05de-456c-92f7-ecc23ff891f0)


## Step 5: Display Assembly Code


Display the optimized assembly code for the main function:

```
$ riscv64-unknown-elf-objdump -d filename.o | less
```

![1 5](https://github.com/user-attachments/assets/077535f6-2e9b-4314-8f29-63e6b8137a83)

# Integer Number Representation

## Introduction to 64-bit Binary Numbers

- **Binary vs. Decimal**: While humans use decimal numbers, computers operate using binary. A translation mechanism is necessary for conversion between the two.
- **Example Usage**: A 64-bit binary number is typically used to represent data such as CPU instructions.
- **Why It Matters**: Understanding binary representation is key to grasping how data is stored, processed, and transmitted in computing systems.

---

## Structure of a 64-bit Binary Number

- **Word**: A fixed unit of data, usually 32 or 64 bits.
- **Least Significant Bit (LSB)**: The rightmost (lowest value) bit.
- **Most Significant Bit (MSB)**: The leftmost (highest value) bit.
- **Byte Breakdown**: 
  - 1 Byte = 8 bits  
  - 4 Bytes = 1 Word  
  - 2 Words = 1 Double Word

---

## Unsigned Binary Numbers

- **Bit Patterns**: With `n` bits, we can form `2^n` unique patterns.
  - Example: With 3 bits → 2³ = 8 values → Range: 0 to 7
- **64-bit Unsigned Range**: With 64 bits, we get `2^64` distinct values.

---

## Representing Large Values

- **Bit-Level Calculation**: Each bit in a binary number contributes to the final decimal value based on its position.
- **Overflow**: If an operation exceeds the maximum representable number (e.g., `2^64 - 1`), an overflow occurs.

---

## Maximum Value in 64-bit Unsigned Format

- The largest value representable with 64 unsigned bits is `2^64 - 1`.

---

## Signed vs. Unsigned Integers

- **Unsigned**: Only non-negative values, ranging from 0 to `2^64 - 1`.
- **Signed**: Can represent both negative and positive numbers using a scheme like **two’s complement**.

---

## Negative Number Representation with Two’s Complement

### Key Concepts

1. **What is Two’s Complement?**
   - A widely used method for representing negative integers in binary.
   - To compute: Invert all bits (1’s complement) and add 1.

2. **Role of MSB (Most Significant Bit)**
   - Indicates the sign:
     - MSB = 0 → Positive number
     - MSB = 1 → Negative number

3. **Converting Negative Values**
   - Invert the binary bits (1's complement) and add 1 to get the two’s complement.
   - Used to represent negative numbers internally.

4. **Binary Format**
   - Positive integers are stored as-is.
   - Negative integers use the two’s complement representation.

---

## Range of Signed 64-bit Integers

- **Positive Range**: From 0 to `2^63 - 1`
- **Negative Range**: From `-2^63` to -1

---

## Converting Between Binary and Decimal

- **Positive Numbers**: Convert the binary directly to decimal.
- **Negative Numbers**:
  - Identify MSB = 1
  - Perform two’s complement to find magnitude
  - Apply a negative sign to get the decimal value

---

## Important Observations

- **MSB** is the key to identifying signed values.
- **Positive numbers** follow standard binary representation.
- **Negative numbers** rely on two’s complement for interpretation.

---

## Integer Representation in RISC-V (RV64)

1. **RISC-V and Integer Handling**
   - Follows the same binary and two’s complement principles for signed/unsigned representation.
   - Uses MSB to determine sign in 64-bit values.

2. **Instruction Behavior**
   - Integer instructions operate correctly based on the signedness and follow hardware-level binary logic.

3. **RV64 Integer Range**
   - **Unsigned**: 0 to `2^64 - 1`
   - **Signed**: `-2^63` to `2^63 - 1`

---

# Day 2

# ABI Basics

## What is ABI?

- The **Application Binary Interface (ABI)** defines how application programs interact with the operating system and the hardware.
- It is important for both hardware designers and software developers.
- ABI specifies:
  - System call conventions
  - Register usage
  - Calling conventions
  - Binary file formats

---

## ABI vs. Architecture

- ABI is like the visible layout of a building — it's the part users interact with.
- Architecture is the internal structure — how the system is actually built (like plumbing and wiring).
- Similarly, users are concerned with what the system does, not how it is implemented internally.

---

## Layered Abstraction in Software-Hardware Interaction

Software communicates with hardware through a series of layers:

- **API (Application Programming Interface)**: Interfaces like `stdio.h` in C or Java libraries.
- **ABI (Application Binary Interface)**: Connects system-level software to machine instructions.
- **ISA (Instruction Set Architecture)**: Defines the set of machine-level instructions (e.g., RISC-V, x86).
- **RTL (Register Transfer Level)**: Describes how the ISA is implemented in hardware.

---

## Accessing System Resources via ABI

- Programs use **system calls** defined by the ABI to access hardware resources.
- This includes operations such as memory access, register usage, and I/O handling.

---

# Memory and Register Basics in RISC-V

## RISC-V Register Overview

- RISC-V defines **32 general-purpose registers**, each 64 bits wide in a 64-bit system (XLEN = 64).
- These registers are used to store data, addresses, and intermediate values during computation.

### Why 32 Registers?

- 32 registers provide a balance between hardware complexity and performance.
- With 5 bits, you can uniquely address all 32 registers (2⁵ = 32).

---

## Register and Memory Interaction

### Byte-Addressable Memory

- Memory in RISC-V is **byte-addressable**: each address points to a single byte.
- A 64-bit (8-byte) value is stored across 8 consecutive memory locations.

### Endianness

- RISC-V systems typically use **Little Endian** format:
  - The **least significant byte (LSB)** is stored at the **lowest memory address**.
  - The **most significant byte (MSB)** is stored at the **highest memory address**.

---

## Loading and Storing Data

### Loading Data from Memory

- Data is loaded from memory into registers using **load instructions**.
- Example:
  ```assembly
  ldw x0, 16(x23)
  ```
  - Loads a 64-bit value from the address `x23 + 16` into register `x0`.

### Storing Data to Memory

- Data is saved from registers to memory using **store instructions**.
- Example:
  ```assembly
  stw x0, 8(x23)
  ```
  - Stores the content of `x0` into memory at address `x23 + 8`.

---

# RISC-V Instruction Types and Registers

## Instruction Formats

- **R-Type**: Uses only registers (e.g., `add x0, x1, x2`)
- **I-Type**: Uses registers and an immediate value (e.g., `ldw x0, 16(x23)`)
- **S-Type**: Used for store operations (e.g., `stw x0, 8(x23)`)

Each format is 32 bits wide and includes:
- Opcode
- Source/destination registers
- Immediate values or function codes

---

## Register Naming and ABI Conventions

- RISC-V registers (`x0` to `x31`) have specific roles and aliases defined by the ABI:

| Register | Alias | Purpose              |
|----------|-------|----------------------|
| x0       | zero  | Constant zero        |
| x1       | ra    | Return address       |
| x2       | sp    | Stack pointer        |
| x3       | gp    | Global pointer       |
| x4       | tp    | Thread pointer       |
| x5–x7    | t0–t2 | Temporaries          |
| x10–x17  | a0–a7 | Function arguments   |
| x18–x27  | s2–s11| Saved registers      |
| x28–x31  | t3–t6 | More temporaries     |

- The ABI ensures consistent register usage across system-level software and applications.

---

## Execution Process
When running a program in SPIKE:
1. The simulator loads the program and its data into memory.
2. Instructions go through the fetch-decode-execute cycle.
3. Register values update according to the executed instructions.
4. Memory operations occur as needed.
5. System calls are processed via the proxy kernel.

## Debugging in SPIKE
SPIKE comes with a built-in debugger, which you can launch using:

```bash
spike -d pk sum1to9
```

### Essential Debugging Commands
- **Run to a specific address**: `until pc 0 10098`
- **Inspect registers**: `reg 0` (all) or `reg 0 a0` (specific register)
- **Check memory content**: `mem 0 2020`
- **View current instruction pointer**: `pc 0`
- **Step through execution**: `step`
- **Disassemble instructions**: `disasm 0 10098 20`

### Debugging Walkthrough
Example of debugging the `sum1to9` loop:

```
# Identify loop location
(spike) disasm 0 10098 20

# Pause execution at loop condition
(spike) until pc 0 100a8

# View key variables
(spike) reg 0 s0    # sum value
(spike) reg 0 s1    # loop counter

# Execute a few steps
(spike) step 10

# Continue execution to next loop iteration
(spike) until pc 0 100a8
```

## Advanced Features
### Performance Tracking
To monitor instruction counts and other metrics, run:

```bash
spike --ic pk sum1to9
```

### Handling Larger Projects
For programs with multiple source files:

```bash
# Compile individual files
riscv64-unknown-elf-gcc -c -O2 -march=rv64i file1.c -o file1.o
riscv64-unknown-elf-gcc -c -O2 -march=rv64i file2.c -o file2.o

# Link compiled files into a final executable
riscv64-unknown-elf-gcc file1.o file2.o -o program
```

---
This toolchain allows developers to write and test RISC-V applications without needing actual hardware. It’s a valuable resource for exploring CPU design and optimizing custom RISC-V implementations.

## Sample Programs
### Finding the Max and Min 64-bit Signed Integer
```c
#include <stdio.h>
#include <math.h>

int main() {
    long long int max = (long long int)(pow(2, 63) - 1);
    long long int min = (long long int)(-pow(2, 63));
    printf("Maximum Signed 64-bit Integer: %lld\n", max);
    printf("Minimum Signed 64-bit Integer: %lld\n", min);
    return 0;
}
```

### Summing Numbers from 1 to 9 in C
```c
#include <stdio.h>

extern int sum1to9_ASS(int x, int y);

int main() {
    int total = 0;
    int upper_limit = 9;
    total = sum1to9_ASS(0x0, upper_limit + 1);
    printf("Sum of numbers from 1 to %d is %d\n", upper_limit, total);
    return 0;
}
```

### Assembly Implementation of Summing 1 to 9
```assembly
.section .text
.global load
.type load, @function

load:
        add     a4, a0, zero  # Initialize sum register a4 to 0
        add     a2, a0, a1    # Load the loop count into a2
        add     a3, a0, zero  # Initialize intermediate register a3 to 0

loop:
        add     a4, a3, a4    # Add intermediate sum to total
        addi    a3, a3, 1     # Increment loop counter
        blt     a3, a2, loop  # Repeat if counter is below limit
        add     a0, a4, zero  # Store final result in a0
        ret
```

![2 1](https://github.com/user-attachments/assets/29b2272d-7f50-42f4-891b-e17cfac0a43e)
![2 2](https://github.com/user-attachments/assets/a559e09a-3347-46d2-8200-ffee06141bfa)
![2 3](https://github.com/user-attachments/assets/a872a8ae-ecfe-4c71-ac3f-4dfbec768c53)



