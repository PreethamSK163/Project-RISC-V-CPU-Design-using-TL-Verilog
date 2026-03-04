# RISC-V ISA & GNU Toolchain
> RISC-V Architecture Fundamentals, GCC Cross-Compilation, Spike Simulation & Number Representation

![Tool](https://img.shields.io/badge/Tool-RISC--V%20GCC-blue)
![Tool](https://img.shields.io/badge/Tool-Spike-blue)
![Tool](https://img.shields.io/badge/Tool-objdump-blue)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

<h2>🔍 Overview</h2>

- Explored RISC-V ISA fundamentals — instruction formats (R, I, S, B, U, J), 32-register file, and modular extensions (M, F/D, Custom) — establishing the conceptual base for hardware-level processor design and cross-compilation workflows.
- Cross-compiled C programs using the RISC-V GCC toolchain, analyzed generated binaries with objdump, simulated and debugged execution on Spike, and studied signed/unsigned number representation behavior in 64-bit RISC-V.

<h2>⚙️ Tasks Covered</h2>

| Task | Description |
|:---|:---|
| C Program to Compute Sum from 1 to N | GCC compilation and Linux terminal workflow |
| RISC-V GCC Compile and Disassemble | Cross-compilation and objdump disassembly |
| Spike Simulation and Debug | ISA simulation and interactive register debugging |
| Signed and Unsigned Numbers | Data type limits, overflow behavior, format specifiers |

<h2>📝 Stage Details</h2>

**Task 1 — C Program to Compute Sum from 1 to N** &nbsp;|&nbsp; `GCC` `Linux` `C Programming`

Wrote a simple C program to compute the sum of the first N natural numbers, compiled it using GCC on Linux, and executed it from the terminal. This established familiarity with command-line development workflows before transitioning to RISC-V cross-compilation.

```c
#include <stdio.h>

int main() {
    int sum = 0, i;
    for(i = 1; i <= 100; i++) {
        sum = sum + i;
    }
    printf("The sum of the first 5 numbers is: %d\n", sum);
    return 0;
}
```

**Task 2 — RISC-V GCC Compile and Disassemble** &nbsp;|&nbsp; `riscv64-unknown-elf-gcc` `objdump` `Assembly`

Cross-compiled the C program for RISC-V using `riscv64-unknown-elf-gcc` and disassembled the generated object file using `riscv64-unknown-elf-objdump`. Analyzed how high-level C code maps to RISC-V assembly instructions — examining function prologues, epilogues, register usage, and memory layout.

**Task 3 — Spike Simulation and Debug** &nbsp;|&nbsp; `Spike` `pk` `Interactive Debug`

Simulated the compiled RISC-V binary using Spike with the proxy kernel (`pk`). Used Spike's interactive debug mode (`spike -d`) to step through instructions, inspect register values, and analyze program execution at the instruction level — validating correct ISA behavior.

**Task 4 — Signed and Unsigned Numbers** &nbsp;|&nbsp; `Data Types` `Overflow` `limits.h` `Two's Complement`

Compiled and executed 8 C programs exploring the behavior of signed and unsigned integer types — `int`, `long`, `long long`, and their unsigned counterparts. Analyzed overflow behavior, typecasting precision loss, and correct use of format specifiers (`%llu`, `%lld`). Used `<limits.h>` to verify maximum and minimum values for all types.

| Type | Max Value | Min Value |
|:---|:---|:---|
| `int` | 2,147,483,647 | −2,147,483,648 |
| `unsigned int` | 4,294,967,295 | 0 |
| `long long int` | 9,223,372,036,854,775,807 | −9,223,372,036,854,775,808 |
| `unsigned long long int` | 18,446,744,073,709,551,615 | 0 |

<h2>🖼️ Implementation Results</h2>

### C Program to Compute Sum from 1 to N
![1](1_C%20Program%20To%20Compute%20Sum%20From%201%20to%20N_1.png)
![2](1_C%20Program%20To%20Compute%20Sum%20From%201%20to%20N_2.png)
![3](1_C%20Program%20To%20Compute%20Sum%20From%201%20to%20N_3.png)
![4](1_C%20Program%20To%20Compute%20Sum%20From%201%20to%20N_4.png)

### RISC-V GCC Compile and Disassemble
![1](2_RISCV%20GCC%20compile%20And%20Disassemble_1.png)
![2](2_RISCV%20GCC%20compile%20And%20Disassemble_2.png)
![3](2_RISCV%20GCC%20compile%20And%20Disassemble_3.png)
![4](2_RISCV%20GCC%20compile%20And%20Disassemble_4.png)
![5](2_RISCV%20GCC%20compile%20And%20Disassemble_5.png)
![6](2_RISCV%20GCC%20compile%20And%20Disassemble_6.png)
![7](2_RISCV%20GCC%20compile%20And%20Disassemble_7.png)
![8](2_RISCV%20GCC%20compile%20And%20Disassemble_8.png)

### Spike Simulation and Debug
![1](3_Spike%20Simulation%20And%20Debug_1.png)
![2](3_Spike%20Simulation%20And%20Debug_2.png)
![3](3_Spike%20Simulation%20And%20Debug_3.png)

### Signed and Unsigned Numbers
![1](4_Signed%20And%20Unsigned%20Numbers_1.png)
![2](4_Signed%20And%20Unsigned%20Numbers_2.png)
![3](4_Signed%20And%20Unsigned%20Numbers_3.png)

<h2>🔗 Navigation</h2>

[Back to Repository Overview](../README.md) &nbsp;|&nbsp; [Next : 02 : ABI & Verification Flow](../02%20:%20ABI%20%26%20Verification%20Flow)
