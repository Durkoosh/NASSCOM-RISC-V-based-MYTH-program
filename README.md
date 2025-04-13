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

# Day 3 

# Introduction to Logic Gates

## Digital Logic Fundamentals

Digital logic is the foundation of all digital systems and is based on binary values: `1` (high) and `0` (low). These binary values are manipulated using **logic gates**, the essential components of digital circuits.

---

## Logic Gates

Logic gates perform basic Boolean functions such as AND, OR, and NOT. These gates are the fundamental building blocks used in designing digital circuits.

![Logic Gates](https://github.com/user-attachments/assets/5d48018c-4dd3-4a65-889d-0a6a7d8cddef)

---

## Combinational Logic

Combinational logic circuits produce outputs based entirely on current input values, without involving memory or state.

### Example: Full Adder

A **3-input full adder** calculates the sum and carry-out of binary addition.

- **Inputs**: A, B, Cin (carry-in)
- **Outputs**: S (sum), Cout (carry-out)

![Full Adder Logic](https://github.com/user-attachments/assets/e9e4b6a4-2215-41da-9295-cddc36df31da)
![Full Adder Truth Table](https://github.com/user-attachments/assets/ebfbee27-6328-45d7-a812-4633c05d55be)

---

## Sequential Logic

Sequential circuits introduce memory into the system and operate based on a clock signal. The outputs depend not only on current inputs but also on past states.

- Registers store values at the rising or falling edge of the clock signal.

![Sequential Logic](https://github.com/user-attachments/assets/beaad135-9637-4e22-8c87-133ed5fa214c)

---

## Pipeline Logic

Pipelining breaks a process into multiple stages, each handled in a separate clock cycle. This allows for parallel processing and improved system performance.

- Each stage passes its result to the next stage on each clock edge.

---

## Hierarchical Design

Complex digital systems are built by composing smaller, reusable modules. For example, a full adder can be reused as a component in an arithmetic logic unit (ALU).

- This modular approach simplifies design and improves scalability.

![Hierarchical Design](https://github.com/user-attachments/assets/8555eb5c-1343-452d-b4ee-093040893933)

---

## TL-Verilog Syntax Overview

TL-Verilog supports both single-bit and multi-bit data operations. The syntax varies based on the width of the data being processed.

![TL-Verilog Syntax](https://github.com/user-attachments/assets/4c3e7d89-d0fc-480e-bdbf-93ae009e3940)

# Notes on Sequential Logic and D Flip-Flop

## 1. Introduction to Sequential Logic

Sequential logic incorporates a **clock signal** to regulate the flow of data through logic circuits. This clock ensures operations are synchronized and executed in a deterministic manner.

![Sequential Logic](https://github.com/user-attachments/assets/4ffdcfe5-a341-4845-8279-a15fd21d5dda)

---

## 2. D Flip-Flop

- The **D (Data) Flip-Flop** is the simplest and most commonly used flip-flop.
- It stores a binary value (0 or 1) based on the clock's rising edge.
- Once set, it holds that value until the next clock cycle updates it.

---

## 3. Importance of Reset in Sequential Circuits

- **Reset** brings a sequential system to a known starting state.
- It can be asynchronous or synchronous, depending on the design.
- Useful in initializing flip-flops or state machines when the system boots or restarts.

---

## 4. Sequential Circuits as State Machines

Sequential circuits can be understood as **finite state machines (FSMs)**:
- **Combinational logic** determines outputs and next states.
- **State registers** store current states and update on each clock cycle.

![State Machine](https://github.com/user-attachments/assets/e2052cd6-e69f-47ea-8686-a976286d3e9e)

---

## 5. Fibonacci Series Circuit Example

The Fibonacci series is computed using two prior values. In hardware:

- Two registers store the last two values.
- On each clock cycle, the circuit computes and stores the new value.

![Fibonacci Circuit](https://github.com/user-attachments/assets/9030c3d2-a2d4-4ef6-844b-a37017ef0f16)

---

## 6. Reset in the Fibonacci Circuit

- The **reset signal** initializes the two registers with the first two Fibonacci values (typically 1 and 1).
- Once reset is deasserted, the circuit continues the series.

![Fibonacci Reset](https://github.com/user-attachments/assets/7d621313-7942-4815-b73d-0142c5499782)

---

## 7. TL-Verilog Representation of Fibonacci Circuit

In TL-Verilog:

- Use conditional expressions to inject initial values on reset.
- Use shift (`>>`) operators to refer to past values.

```tlv
$op = $reset ? 32'b1 : >>1$op + >>2$op;
```

![3 2](https://github.com/user-attachments/assets/c5316e45-bc12-4fa0-9537-8c9bc9962311)


---

# Labs

## 8. Exercise: Free-Running Counter

A free-running counter:

- Starts from zero.
- Increments by one each clock cycle.

![Free Running Counter](https://github.com/user-attachments/assets/6d025fcd-ae17-482a-a925-73406f09e167)
![Counter Values](https://github.com/user-attachments/assets/87054e9d-4462-470e-9303-2094ba62bc8f)
![Counter Waveform](https://github.com/user-attachments/assets/d7569c90-ca84-4ea2-8245-d16cf8705121)

---

## 9. Expressing Values in Verilog

### Verilog Value Notation

Specify bit-width and format explicitly:

- Format: `<width>'<format><value>`
- Examples:
  - `8'd15` → 8-bit decimal 15
  - `4'b1010` → 4-bit binary 1010

![Verilog Value Example](https://github.com/user-attachments/assets/6405d6ee-367d-4897-9d25-12be0554d41f)

### Shortcuts

- `'0` → Verilog infers required bits
- `'x` → “Don't care” value, useful for debugging unknown states

### Default Width

- Without explicit width, values are assumed 32 bits.

### Simulation vs. Synthesis

- Verilator (used by MakerChip) supports only two states: `0` and `1`.
- No support for `'x` in simulation — be mindful of missing debug behavior.

---

## 10. Calculator Example Using Flip-Flop (Sequential Circuit)

### Overview

This circuit mimics a calculator that retains its previous result and performs a new operation using that stored value.

![Calculator Circuit](https://github.com/user-attachments/assets/f2cd35c0-9ea5-457b-aaa1-8e1a4042f7cc)

### Functionality

- A flip-flop stores the previous output.
- The result of a new operation uses this stored value.
- On **reset**, the stored value is cleared (like hitting "C" on a calculator).

---

### 11. TL-Verilog Lab Solution: Calculator

```tlv
\m5_TLV_version 1d: tl-x.org
\m5

// =================================================
// Welcome!  New to MakerChip? Try the "Learn" menu.
// =================================================

//use(m5-1.0)   // Uncomment to use M5 macro library.
\SV
m5_makerchip_module
\TLV

$reset = *reset;

// Sequential Calculator
$in1[31:0] = >>1$op;  // Memory element storing the previous result
$in2[31:0] = $rand2[3:0];
$sel[1:0]  = $rand3[1:0];

$sum[31:0]  = $in1 + $in2;
$diff[31:0] = $in1 - $in2;
$prod[31:0] = $in1 * $in2;
$quot[31:0] = $in1 / $in2;

$temp[31:0] = ($sel == 2'b00) ? $sum :
              ($sel == 2'b01) ? $diff :
              ($sel == 2'b10) ? $prod : $quot;

$op[31:0] = $reset ? 32'b0 : $temp;

*passed = *cyc_cnt > 40;
*failed = 1'b0;

\SV
endmodule
```

---

## Output

![3 3](https://github.com/user-attachments/assets/f02aacdf-4ea4-4c99-9289-f32a94965ec2)


---

# Pipelining: Pythagoras Theorem Example

## 1. **Computation Goal: Pythagoras Theorem**
   - The task is to calculate the distance `c` using the Pythagoras theorem:
     ![image](https://github.com/user-attachments/assets/d8551168-7b33-4a1a-af04-5f999aef2c37)
   - To perform this computation, the hardware must:
     - Square values `a` and `b`.
     - Add the squared results.
     - Take the square root of the sum.
   - In a modern processor running at 1 GHz, only a limited amount of logic (approximately 20 gates deep) can be processed within a single clock cycle. If the logic is deeper, it won't complete before the next cycle starts, causing incorrect behavior.

## 2. **Pipeline Concept: Distributing Logic Across Clock Cycles**
   - The computation is too complex for a single clock cycle, so we spread the operations over **multiple clock cycles**.
   - Breakdown of the pipeline stages:
     ![image](https://github.com/user-attachments/assets/258ca49c-123c-4d7b-badf-13dab0c9d31e)
     - **Cycle 1**: Square `a` and `b`, storing the results in flip-flops.
     - **Cycle 2**: Add the squared values and store the result in new flip-flops.
     - **Cycle 3**: Calculate the square root of the sum (for simplicity, assume it takes one cycle).
   - Each clock cycle advances the computation, with intermediate values captured in flip-flops to prevent data loss.

## 3. **RTL Approach (Register Transfer Level)**:
   - In **traditional RTL design**, logic operations and **flip-flops** that store intermediate results are explicitly defined.
   - Example:
     - **Cycle 1**: Squaring `a` and `b`, storing results in flip-flops.
     - **Cycle 2**: Adding `a^2` and `b^2`, storing the sum.
     - **Cycle 3**: Calculating the square root.
   - RTL design requires careful timing management to ensure each stage captures the correct values at the appropriate clock edge, which can complicate the design.

## 4. **TL-Verilog: Pipeline Abstraction and Simplification**
   - **TL-Verilog** provides a higher-level abstraction for pipeline stages. Instead of manually coding flip-flops, TL-Verilog automatically handles them between stages.
   - Example in TL-Verilog:
     - Define a pipeline named `calc` with stages: `stage 1`, `stage 2`, and `stage 3`.
     - Logic is specified within each stage, and TL-Verilog automatically infers the flip-flops.
   - **Pipeline abstraction** focuses on the operations (e.g., squaring, adding, square rooting), simplifying the design and reducing the need for low-level details like flip-flop placement.

## 5. **Example: Code and Logic Comparison**
   - The TL-Verilog code aligns with the conceptual pipeline diagram, with stages defined for squaring, adding, and square rooting.
     ![image](https://github.com/user-attachments/assets/20de4c1a-a9df-4ce6-89cf-3bddf6d7dd1b)
   - **Traditional RTL Code**:
     - Requires explicit management of logic and flip-flops.
   - **TL-Verilog Code**:
     - Defines the stages abstractly, with flip-flops automatically handled.
   - **Benefits**: TL-Verilog reduces code complexity, improves readability, and reduces bugs, speeding up the design process.
     ![image](https://github.com/user-attachments/assets/319a2db0-bcfa-43e6-ac73-4828e06cb67d)

## 6. **Timing Abstraction and Flexibility in TL-Verilog**
   ![image](https://github.com/user-attachments/assets/3352ee0d-4d0f-4c7f-9504-4ef59eb0f525)
   - **TL-Verilog's main advantage** is its separation of **function** from **timing**:
     - **Function**: The operations (squaring, adding, square rooting) remain unchanged.
     - **Timing**: The number of pipeline stages and their timing can be adjusted independently without modifying the logic.
   - This separation allows you to **adjust timing** (e.g., adding more stages for signal propagation delays) without altering the circuit’s behavior.
   - In traditional RTL, modifying the pipeline timing requires extensive rewiring and logic adjustments, which increases the risk of errors.

## 7. **Why Adjust Pipeline Staging?**
   - **Design Adaptation**: If the signal `a` is far from the result `c`, signal propagation across the chip may take **multiple cycles** (e.g., 25 cycles).
   - **Timing Flexibility**: TL-Verilog allows you to extend the pipeline by adding more stages to accommodate signal delays. The logic remains the same, only the **timing** is adjusted.
   - This flexibility is crucial in modern designs where signal propagation can span a considerable distance.

## 8. **Guarantee of Circuit Behavior**
   - TL-Verilog guarantees that the circuit behavior remains consistent despite changes in pipeline stages. The only concern is timing—ensuring data is consumed after it's produced.
   - The core logic stays unchanged, and the abstraction minimizes bugs related to timing alterations.

## 9. **Challenges in Traditional RTL Design**
   - In traditional RTL, changing pipeline timing requires:
     - **Rewiring flip-flops**.
     - Modifying logic to match new timing.
     - Ensuring the circuit behaves correctly post-change.
   - These tasks are **error-prone** and time-consuming, with high potential for bugs if not carefully handled.
   - **TL-Verilog** simplifies this process, allowing easier timing changes through **pipeline abstraction**, saving time and reducing errors.

---

### Key Takeaways:
- **Pipeline logic** helps break down complex computations into manageable stages over multiple clock cycles.
- **TL-Verilog** provides a **timing abstraction** that simplifies the design process, reducing code complexity and bugs.
- **Flexibility**: TL-Verilog allows easy adjustments to pipeline staging without affecting the logic of the circuit.
- **Timing abstraction** separates logic from timing, making designs more adaptable to hardware environments with varying signal propagation delays.

# Understanding Pipeline Benefits and Waveform Analysis

## 1. **Pipelining for High Clock Frequency & Performance**
![image](https://github.com/user-attachments/assets/d8d81130-5445-49b3-acf1-b1126d415292)

- When the clock runs too fast for the logic to complete within a single clock cycle, **pipelining** is necessary.
- **Pipelining** addresses timing issues and boosts **performance** by enabling designs to run at **higher clock frequencies**.
- The **combinational logic** between flip-flops limits the clock speed, with the **time between flip-flops** defining the **clock frequency**.
- **Pipelining** divides computation into smaller tasks across **multiple stages**, allowing for faster clock speeds. By shortening the logic path between flip-flops, a **new set of inputs** can be processed each clock cycle.

## 2. **Throughput vs. Latency**
- While pipelining increases the number of clock cycles (stages) needed to compute a result (increased **latency**), it improves **throughput**.
- Throughput improves because a **new set of data** can be processed every clock cycle. Thus, **more data** is handled per second, even though individual results take longer to compute due to the multiple stages.

## 3. **Pipeline Example: Pythagoras Theorem**
- In this example, we compute the distance `c` using the **Pythagoras theorem** (`c = sqrt(a^2 + b^2)`).
- The logic is distributed across stages:
  - **Stage 1**: Square values `a` and `b`.
  - **Stage 2**: Add the squared results.
  - **Stage 3**: Compute the square root of the sum.

## 4. **Waveform Viewer in Makerchip**
![3 4](https://github.com/user-attachments/assets/2331ac77-9112-4b54-a071-a7eed895bfbe)


- Makerchip provides a **waveform viewer** to visualize pipeline behavior over time.
  ![image](https://github.com/user-attachments/assets/10ef5aa4-9d74-4779-aefe-d3694b357fa0)
- In a pipeline, **data is distributed across time**, meaning inputs at earlier stages impact outputs at later stages.
- The **waveform viewer** lets you track how inputs (e.g., `a` and `b`) at different stages of the pipeline correspond to outputs (e.g., `c`) a few clock cycles later.

## 5. **Understanding Timing and Signal Alignment**
- **Combinational Logic (Single Cycle)**: If all computations are done in **one cycle** (non-pipelined), the logic to compute `c` (squaring `a` and `b`, adding, and taking the square root) occurs in a single clock cycle.
  - In the waveform viewer, you would see that inputs `a = 9` and `b = 12` (represented as `C` in hexadecimal) result in an output `c = F` (hexadecimal) in the same cycle.
- **Pipelined Logic**: When pipelined, the logic is spread across **multiple stages**.
  - For example, in a 3-stage pipeline, you would see:
    - **Stage 1**: Inputs `a` and `b`.
    - **Stage 2**: The intermediate result from squaring `a` and `b`.
    - **Stage 3**: The final output `c` two clock cycles later.
  - The pipeline adds **flip-flops** between stages to store intermediate results and propagate data.

## 6. **Tagging Signals by Stage**
- In the waveform, each signal is **tagged** with the stage at which it was generated (e.g., `@1` for stage 1, `@3` for stage 3).
- For instance:
  - Input `a` in **Stage 1** (tagged `@1`) affects the output `c` in **Stage 3** (tagged `@3`) two clock cycles later.
- This **stage tagging** helps you understand how **intermediate results** progress through the pipeline and when final results appear.

## 7. **Pipelining in TL-Verilog**
- **TL-Verilog** simplifies pipeline design by allowing you to focus on the **logical operations** at each stage without manually managing flip-flops.
- In TL-Verilog, a signal like `a_squared` in stage 1 automatically gets propagated to later stages (e.g., stage 2) through flip-flops, which are implied by the pipeline structure.
- The **timing abstraction** in TL-Verilog treats these signals as part of a **single pipeline**, but under the hood (SystemVerilog level), they are **separate signals** for each stage.

## 8. **Example: Retiming**
- **Retiming** adjusts the **position of flip-flops** in the pipeline to better distribute the logic across stages.
- For example, if `a_squared` is computed in stage 1 and needs to be used in stage 2, a flip-flop is placed between the stages to hold the result of `a_squared` and propagate it to the next stage.

## 9. **Sequential Logic and Feedback in Pipelining**
- Beyond pipelining, **sequential logic** involves **feeding back** data from later stages to earlier stages (e.g., Fibonacci sequence).
- For instance, if a feedback loop is added to the pipeline (e.g., feeding back the value of `a`), it allows the current stage’s logic to depend on results computed **several cycles earlier**.
- In this case, **delayed versions** of signals (e.g., `a_4`, `a_12`) are used, indicating data that has passed through the pipeline for several stages.

## 10. **Visualizing Feedback and Pipeline Depth**
![image](https://github.com/user-attachments/assets/d3b3f688-4d87-4744-9cae-4fb5d1a9e49a)

- In the Makerchip platform, you can visualize **feedback loops** and track how signals are staged through multiple flip-flops.
- The feedback loop might refer to the version of a signal from **4, 12, or more cycles ahead**, creating complex interactions across different stages.

## 11. **Benefits of Pipeline Diagrams**
- **Pipeline diagrams** help in visualizing how **flip-flops** are implied in your design and how data flows across different stages.
- These diagrams are useful for understanding:
  - Where logic operations are occurring.
  - How flip-flops store and propagate data.
  - How the feedback mechanism works, especially in sequential logic.

---

### **Key Takeaways:**
- **Pipelining** allows designs to run at **higher clock frequencies** by dividing computations into smaller tasks across multiple stages.
- The **throughput** of the design improves with pipelining, even though individual computations take longer (increased latency).
- **TL-Verilog** simplifies pipeline design by abstracting the timing of operations, reducing the complexity of managing flip-flops.
- The **waveform viewer** in Makerchip helps correlate inputs and outputs at different stages of the pipeline, allowing designers to track data flow over time.
- **Feedback loops** enable more complex sequential logic, where later-stage results are fed back into earlier stages for future computations.

#### 1. **TL-Verilog Syntax Basics: Pipe Signals**
   - **Naming Conventions**:
     ![image](https://github.com/user-attachments/assets/47a81fd6-ff51-453f-aec3-3894a48ee397)

     - TL-Verilog identifiers follow specific syntax rules based on their roles in the design.
     - **Pipe Signals**: These signals represent values moving through pipeline stages. They are named using **lowercase letters** with **underscores** separating the tokens.
       - **Example**: A pipe signal is named `a_pipe_signal`, where `a` is the base and `pipe_signal` represents the role and function.
     - **State Signals**: These signals store state information and follow either **camelCase** or **PascalCase** conventions. TL-Verilog prefers **PascalCase** (capitalizing the first letter of each token).
       - **Example**: `StateSignal` or `ComputeValue` represent state signals.
     - **Uppercase Identifiers**: Although not covered here, uppercase identifiers follow the convention of full capitalization with underscores, typically used for constants or macros.
       - **Example**: `CONSTANT_VALUE` or `MAX_DEPTH`.
   
   - **Numeric Identifiers**:
     - TL-Verilog allows **numbers** in signal names, but only at the **end of a token**. For example, `base64` is valid, but identifiers cannot **begin with a number** or stand alone with numbers.

---

#### 2. **Pipeline Stages in TL-Verilog**
   - **Implicit vs Explicit Pipelining**:
     - TL-Verilog inherently places all logic in a pipeline, even without explicit definitions. By default, computations are assigned to **stage 0** unless otherwise specified.
     - **Explicit Pipeline Declaration**:
       - When explicitly defining pipeline stages, you specify where each logic block belongs in the pipeline.
       - **Example**:
         - Instead of performing all operations in stage 0, you can assign specific logic to **pipeline stage 1** using `@1`.
         - For multi-cycle operations, stages can be divided, with stage 1 performing computation and stage 3 handling checks (like overflow detection).
       - **Pipeline Depth**: Deep pipelines (multi-cycle operations) improve performance and clock speed by executing logic in different stages.

   - **Pipeline Signals**:
     - Signals processed at various pipeline stages are **propagated** through flip-flops between the stages, where values are calculated sequentially.

---

#### 3. **Example: Fibonacci Series in a Pipeline**
![image](https://github.com/user-attachments/assets/57813154-9388-441e-a5f6-4545d2049023)

   - **Pipeline Setup**:
     - The Fibonacci series is calculated sequentially, with each term dependent on the previous terms.
     - The pipeline stages manage these calculations.
       - **Stage 1**: Calculate the sum of the last two Fibonacci numbers.
       - **Stage 2 (optional)**: Store the result for the next iteration.
     - **Simplified Example**: In Fibonacci `Fn = Fn-1 + Fn-2`, stage 1 computes the value, while stage 2 stores it for further processing.
   
   - **Comparison to Non-Pipelined Version**:
     - In the non-pipelined design, all logic resides in **stage 0**, making it harder to manage deep pipelines and more complex calculations.
     - The **pipelined version** assigns specific logic to stages (e.g., `@1`, `@2`), enhancing modularity and scalability.

---

#### 4. **Error Handling in Deep Pipelines**
   - **Multi-Stage Error Conditions**:
     - Pipelines may encounter errors at different stages, such as:
       - **Bad Input**: Detected in stage 1.
       - **Overflow**: Detected in stage 3.
       - **Divide-by-Zero**: Detected in stage 6.
   
   - **Aggregating Error Signals**:
     - Errors detected at various stages must be aggregated into a single signal indicating any error.
     - **Example**:
       - In stages 3 and 6, errors are captured as `error_stage3` and `error_stage6`.
       - These errors are combined using an OR gate, triggering the `error` signal in stage 6.

   - **TL-Verilog Code**:
     - Error detection can be implemented as:
```
  @1
     $err1 = ($bad_input || $illegal_op) ? 1 : 0;
   
  @3
     $err2 = ($err1 || $overflow) ? 1 : 0;
 
  @6
     $err3 = ($divby0 || $err2) ? 1 : 0;
```

![image](https://github.com/user-attachments/assets/864fdec2-cf95-4d71-ab64-f84e735a7e6f)
       
  - The error conditions from stages 3 and 6 are ORed together to produce the final error signal in stage 6.
   
   - **Using the Waveform Viewer**:
     - The **waveform viewer** in Makerchip helps visualize how error signals propagate. When an error is detected in any stage, the final `error` signal will reflect the condition, aiding in debugging and validation.

---

#### 5. **Coding Logic for Error Handling**
   - **Example Scenario**:
     - This example handles error conditions in a **six-stage** pipeline.
     - Error conditions are detected in:
       - **Stage 3**: Overflow or illegal operation.
       - **Stage 6**: Divide by zero.
     - The final error signal (`error3`) in stage 6 will indicate whether an error occurred.
   
   - **Logic for Error Conditions**:
     - The **blue circles** in the diagram represent OR gates used to combine error conditions.
     - The **red circles** represent predefined input conditions.
     - The logic could be implemented as:
       ```verilog
       @3
       error_stage3 <= illegal_operation | overflow;
       
       @6
       error_stage6 <= divide_by_zero;
       
       @6
       error3 <= error_stage3 | error_stage6;
       ```
     - **Waveform Check**:
       - After implementing the logic, use the waveform viewer to examine the behavior of error signals.
       - The **final error signal (`error3`)** should assert when any of the error conditions in stages 3 or 6 are triggered.

## Pipeline Calculator Circuit Example in TL-Verilog

#### 1. **Starting Point: Calculator and Counter in Pipeline**
   - **Objective**: Integrate the calculator circuit you previously designed into a **named pipeline** (`calc`), placing it in **stage 1**. Similarly, integrate the **counter** into the same pipeline stage, **stage 1**.
   - After placing both the **calculator** and **counter** in the same stage, simulate the circuit to verify their functionality within the pipeline.

#### 2. **Next Steps: High-Frequency Operation Adjustments**
   - When working with a **high-frequency circuit**, it's necessary to break down computations over multiple clock cycles to ensure proper timing.
   - **Calculator Circuit Modifications**:
     - Split the calculator operation into **two stages**:
       - **Stage 1**: Perform the arithmetic operation (e.g., addition, subtraction, multiplication, or division).
       - **Stage 2**: Use a **multiplexer** to select the appropriate result based on the selected operation.
   - By dividing the operation into two stages, the circuit can handle **higher frequencies**, ensuring that the timing constraints of each stage are satisfied.

#### 3. **Introducing Two-Cycle Latency**
   - Since the circuit now requires **two cycles** to perform a computation, the **input-output loopback** must be adjusted accordingly.
   - Modify the design to:
     - Implement a **two-cycle latency** for the output loopback (instead of a one-cycle latency).
     - This ensures that the computation result is available after two cycles and can be used as the input for the next cycle, maintaining continuity in the iterative process.

#### 4. **Step-by-Step Breakdown of Circuit Changes**
   - **Step 1**: **Output Loopback**
     - Modify the output alignment to loop back with a two-cycle latency.
     - Initially, the **multiplexer** remains in the same stage as the arithmetic operations (addition, subtraction, etc.).
     - The loopback introduces two **staging flip-flops**, which hold intermediate results and return them to the input after two cycles.

   - **Step 2**: **Single-Bit Counter for Cycle Tracking**
     - To track whether the current cycle is a **computation cycle** or a **meaningless cycle** (no valid computation), use a **single-bit counter**.
     - This counter alternates between **0** and **1**, distinguishing **even cycles** (computation) and **odd cycles** (idle).
     - This counter acts as an **oscillator**, controlling which cycles perform calculations (even cycles) and which cycles are idle (odd cycles).
     - The output of this counter is a **valid signal**, which is `1` during computation cycles and `0` during idle cycles.

   - **Step 3**: **Valid Signal and Reset Logic**
     - Connect the **valid signal** and **reset signal** to control when to drive the output with a **zero value**:
       - If the system is in reset or the cycle is invalid (odd cycle), the output should be set to `0`.
       - This ensures that during idle cycles, the circuit outputs zero, maintaining system stability during non-computation cycles.

   - **Step 4**: **Re-Timing the Multiplexer**
     - Move the **multiplexer** logic from **stage 1** to **stage 2**, completing the two-stage pipeline design.
     - By shifting the multiplexer, the selection of the arithmetic operation result happens in **stage 2**, while the actual computation occurs in **stage 1**.
     - Once these changes are implemented, you can verify the circuit’s behavior through simulation.

#### 5. **Expected Behavior in Simulation**
   - The pipeline will now perform a **calculation every other cycle**:
     - During **even cycles** (valid cycles), the circuit performs computations.
     - During **odd cycles** (invalid cycles), the inputs are meaningless, and the output is set to zero.
   - In the **waveform viewer**, you should observe the calculator executing operations on **valid cycles**, outputting results every other cycle, and outputting zero during invalid cycles.

#### 6. **Key Concepts Reinforced in This Example**
   - **Pipeline Staging**: Dividing the computation into two pipeline stages allows the circuit to operate at **higher frequencies** by distributing the workload across multiple clock cycles.
   - **Two-Cycle Latency**: The output is looped back with a two-cycle delay, indicating that the computation now spans two cycles.
   - **Single-Bit Counter**: The use of a single-bit counter creates a simple oscillator to track which cycles are valid for computation.
   - **Valid Signal**: The **valid signal** ensures computations only occur during designated cycles, while idle cycles produce zero outputs.
   - **Multiplexer Re-Timing**: Moving the multiplexer to stage 2 separates the operation and result selection, ensuring timing constraints are met without overloading a single pipeline stage.
  
# Labs
![image](https://github.com/user-attachments/assets/9ff380e3-fb31-4299-955f-4339d7023c60)
![image](https://github.com/user-attachments/assets/de0a94aa-9026-462f-b5ee-d6b186c03938)
![image](https://github.com/user-attachments/assets/d76909fb-3a7f-471b-8290-d85e07d4f133)
![image](https://github.com/user-attachments/assets/7eb0357c-a8d1-4088-9b06-e12921b7687d)
![image](https://github.com/user-attachments/assets/f7920203-dff4-45b4-9e1b-eb356442678a)
