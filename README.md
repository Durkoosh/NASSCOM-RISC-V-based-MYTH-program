# NASSCOM-RISC-V-based-MYTH-program

Welcome to this hands-on journey into digital logic design! We're diving into TL-Verilog, an innovative design language pioneered by Redwood EDA. We will use the Makerchip online IDE to design, simulate, and visualize circuits. Let’s start from the basics and quickly ramp up to more advanced concepts.

## Table of Contents 
- [Day 1 ](#day-1)
- [Day 2 ](#day-2)
- [Day 3 ](#day-3)
- [Day 4 ](#day-4)
- [Day 5 ](#day-5)

## Day 1
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
