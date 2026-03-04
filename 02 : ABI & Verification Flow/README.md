# ABI & Verification Flow
> RISC-V Application Binary Interface, C-to-Assembly Interfacing & Processor Verification

![Tool](https://img.shields.io/badge/Tool-RISC--V%20GCC-blue)
![Tool](https://img.shields.io/badge/Tool-Spike-blue)
![Tool](https://img.shields.io/badge/Tool-Verilog-blue)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

<h2>🔍 Overview</h2>

- Explored the RISC-V Application Binary Interface (ABI) — covering calling conventions, register usage (a0–a7, s0–s11, t0–t6), stack management, ELF binary format, and DWARF debugging standards — establishing the foundation for hardware-software integration.
- Implemented C-to-assembly function calls following RISC-V ABI conventions, simulated execution using Spike, and ran custom C firmware on a simulated RISC-V CPU — validating the complete hardware-software co-simulation workflow.

<h2>⚙️ Tasks Covered</h2>

| Task | Description |
|:---|:---|
| Review ASM Function Call | C-to-assembly interfacing using RISC-V calling conventions |
| Simulate New C Program With Function Call | Cross-compilation, linking, Spike simulation and disassembly |
| Program On RISC-V CPU | Firmware generation, memory loading, CPU simulation and output verification |

<h2>📝 Stage Details</h2>

**Task 1 — Review ASM Function Call** &nbsp;|&nbsp; `ABI` `Calling Convention` `Assembly` `a0–a7`

Implemented a C-to-assembly function call following the RISC-V ABI — `main.c` passes the argument N to an external assembly function `load.s` via register `a0`, the assembly computes the sum using a loop and register operations, and returns the result via `a0` for the C program to print. Verified correct argument passing, register preservation, and return value handling.

**Task 2 — Simulate New C Program With Function Call** &nbsp;|&nbsp; `GCC` `Spike` `objdump` `Linking`

Wrote a C program calling an external assembly subroutine to compute the sum of a range, compiled and linked both files using the RISC-V GCC toolchain, and simulated execution on Spike. Disassembled the generated object file with objdump to verify correct function linkage, argument passing, and assembly-level translation.

**Task 3 — Program On RISC-V CPU** &nbsp;|&nbsp; `Verilog` `Testbench` `Firmware` `HEX` `Co-Simulation`

Demonstrated the complete hardware-software integration workflow — prepared Verilog testbench and CPU design files, compiled a C program to generate firmware in HEX format, loaded it into the simulated RISC-V CPU memory, ran the simulation script, and verified program output. This exercise validated memory initialization, instruction execution, and hardware-software co-simulation for a custom RISC-V processor.

<h2>🖼️ Implementation Results</h2>

### Review ASM Function Call
![1](1_Review%20ASM%20Function%20Call_1.png)
![2](1_Review%20ASM%20Function%20Call_2.png)
![3](1_Review%20ASM%20Function%20Call_3.png)

### Simulate New C Program With Function Call
![1](2_Simulate%20New%20C%20Program%20With%20Function%20Call_1.png)
![2](2_Simulate%20New%20C%20Program%20With%20Function%20Call_2.png)
![3](2_Simulate%20New%20C%20Program%20With%20Function%20Call_3.png)
![4](2_Simulate%20New%20C%20Program%20With%20Function%20Call_4.png)

### Program On RISC-V CPU
![1](3_Program%20On%20RISC-V%20CPU_1.png)
![2](3_Program%20On%20RISC-V%20CPU_2.png)
![3](3_Program%20On%20RISC-V%20CPU_3.png)
![4](3_Program%20On%20RISC-V%20CPU_4.png)
![5](3_Program%20On%20RISC-V%20CPU_5.png)
![6](3_Program%20On%20RISC-V%20CPU_6.png)
![7](3_Program%20On%20RISC-V%20CPU_7.png)
![8](3_Program%20On%20RISC-V%20CPU_8.png)
![9](3_Program%20On%20RISC-V%20CPU_9.png)
![10](3_Program%20On%20RISC-V%20CPU_10.png)
![11](3_Program%20On%20RISC-V%20CPU_11.png)
![12](3_Program%20On%20RISC-V%20CPU_12.png)

<h2>🔗 Navigation</h2>

[Back to Repository Overview](../README.md) &nbsp;|&nbsp; [Previous : 01 : RISC-V ISA & GNU Toolchain](../01%20:%20RISC-V%20ISA%20%26%20GNU%20Toolchain) &nbsp;|&nbsp; [Next : 03 : Digital Logic with TL-Verilog](../03%20:%20Digital%20Logic%20with%20TL-Verilog)
