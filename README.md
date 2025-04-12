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
