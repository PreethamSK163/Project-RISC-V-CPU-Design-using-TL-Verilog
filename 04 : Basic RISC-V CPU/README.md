# Basic RISC-V CPU
> Program Counter, Instruction Fetch, Decode, ALU, Register File & Branch Logic in TL-Verilog

![Tool](https://img.shields.io/badge/Tool-TL--Verilog-blue)
![Tool](https://img.shields.io/badge/Tool-Makerchip-blue)
![ISA](https://img.shields.io/badge/ISA-RISC--V%20RV32I-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

<h2>🔍 Overview</h2>

- Implemented a single-cycle RISC-V datapath from scratch in TL-Verilog — covering program counter logic, instruction memory fetch, instruction type decoding (R/I/S/B/U/J), field extraction, register file read/write, ALU operations, and branch control flow.
- Built and verified a functional RISC-V core capable of executing the sum 1–9 program — validating correct PC redirection on BLT branch, ALU results for ADD/ADDI, register file write-back, and automated testbench verification with x10 = 45.

<h2>⚙️ Tasks Covered</h2>

| Task | Description |
|:---|:---|
| Program Counter & Instruction Fetch | PC reset/increment logic, instruction memory interface |
| Instruction Types Decode | R/I/S/B/U/J type identification from opcode patterns |
| Instruction Field Extraction | funct7, funct3, rs1, rs2, rd, opcode extraction |
| Instruction Decode & Detection | dec_bits, BEQ/BNE/BLT/BGE/ADD/ADDI detection |
| Branches & Control Flow | Register file, ALU, branch logic, PC update, testbench |

<h2>📝 Stage Details</h2>

**Task 1 — Program Counter & Instruction Fetch** &nbsp;|&nbsp; `PC` `imem` `Reset` `Fetch`

Implemented PC logic with reset (to 0) and sequential increment (by 4). Connected the instruction memory interface — word-aligned address from PC bits, read enable when not in reset — to fetch `$instr[31:0]` from `$imem_rd_data`. Added the sum 1–9 test program and enabled CPU visualization. Verified PC values 0, 4, 8… in simulation waveform.

**Task 2 — Instruction Types Decode** &nbsp;|&nbsp; `R-type` `I-type` `S-type` `B-type` `U-type` `J-type`

Implemented instruction type identification logic using `instr[6:2]` opcode bit patterns — detecting all six RISC-V base instruction formats (R, I, S, B, U, J) using bitwise don't-care matching (`==?`). This enables the CPU to correctly route instructions to the appropriate decode and execution paths.

**Task 3 — Instruction Field Extraction** &nbsp;|&nbsp; `funct7` `funct3` `rs1` `rs2` `rd` `opcode`

Extended the decode stage to extract all instruction fields from the 32-bit instruction word — `$opcode[6:0]`, `$rs1[4:0]`, `$rs2[4:0]`, `$rd[4:0]`, `$funct3[2:0]`, and `$funct7[6:0]` — providing the operand indices and function codes needed for register file access and ALU control.

**Task 4 — Instruction Decode & Detection** &nbsp;|&nbsp; `dec_bits` `BEQ` `BNE` `BLT` `BGE` `ADD` `ADDI`

Built `$dec_bits[10:0]` from `{instr[30], funct3, opcode}` and used it to detect specific instructions — BEQ, BNE, BLT, BGE, BLTU, BGEU, ADD, ADDI — using don't-care bit pattern matching. This forms the instruction control signals driving the ALU and control flow logic.

**Task 5 — Branches & Control Flow** &nbsp;|&nbsp; `Register File` `ALU` `BLT` `Branch Target` `Testbench`

Completed the full single-cycle datapath across 7 progressive tasks — register file read (rs1/rs2), source value assignment, ALU for ADD/ADDI, register file write-back with x0 protection, BLT branch condition, branch target PC calculation, and PC mux update on taken branch. Verified correct execution with automated testbench: `*passed = |cpu/xreg[10]>>5$value == 45`.

<h2>🖼️ Implementation Results</h2>

### Program Counter & Instruction Fetch
![LE1_1_Task_diagram](LE1_1_Task_diagram.png)
![LE1_1_Task_1](LE1_1_Task_1.png)
![LE1_1_Task_2](LE1_1_Task_2.png)
![LE1_2_Task_diagram](LE1_2_Task_diagram.png)
![LE1_2_Task_1](LE1_2_Task_1.png)
![LE1_2_Task_2](LE1_2_Task_2.png)
![LE1_3_Task_diagram](LE1_3_Task_diagram.png)
![LE1_3_Task_1](LE1_3_Task_1.png)
![LE1_3_Task_2](LE1_3_Task_2.png)
![LE1_3_Task_3](LE1_3_Task_3.png)

### Instruction Types Decode
![LE2_1_Task_diagram](LE2_1_Task_diagram.png)
![LE2_1_Task_1](LE2_1_Task_1.png)
![LE2_1_Task_2](LE2_1_Task_2.png)

### Instruction Field Extraction
![LE3_1_Task_diagram](LE3_1_Task_diagram.png)
![LE3_1_Task_1](LE3_1_Task_1.png)
![LE3_1_Task_2](LE3_1_Task_2.png)
![LE3_1_Task_3](LE3_1_Task_3.png)

### Instruction Decode & Detection
![LE4_1_Task_diagram](LE4_1_Task_diagram.png)
![LE4_1_Task_1](LE4_1_Task_1.png)
![LE4_1_Task_2](LE4_1_Task_2.png)

### Branches & Control Flow
![LE5_1_Task_diagram](LE5_1_Task_diagram.png)
![LE5_1_Task_1](LE5_1_Task_1.png)
![LE5_1_Task_2](LE5_1_Task_2.png)
![LE5_2_Task_diagram](LE5_2_Task_diagram.png)
![LE5_2_Task_1](LE5_2_Task_1.png)
![LE5_2_Task_2](LE5_2_Task_2.png)
![LE5_3_Task_diagram](LE5_3_Task_diagram.png)
![LE5_3_Task_1](LE5_3_Task_1.png)
![LE5_3_Task_2](LE5_3_Task_2.png)
![LE5_3_Task_3](LE5_3_Task_3.png)
![LE5_3_Task_4](LE5_3_Task_4.png)
![LE5_4_Task_diagram](LE5_4_Task_diagram.png)
![LE5_4_Task_1](LE5_4_Task_1.png)
![LE5_4_Task_2](LE5_4_Task_2.png)
![LE5_5_Task_diagram](LE5_5_Task_diagram.png)
![LE5_5_Task_1](LE5_5_Task_1.png)
![LE5_5_Task_2](LE5_5_Task_2.png)
![LE5_6_Task_diagram](LE5_6_Task_diagram.png)
![LE5_6_Task_1](LE5_6_Task_1.png)
![LE5_6_Task_2](LE5_6_Task_2.png)
![LE5_7_Task_1](LE5_7_Task_1.png)
![LE5_7_Task_2](LE5_7_Task_2.png)

<h2>🔗 Navigation</h2>

[Back to Repository Overview](../README.md) &nbsp;|&nbsp; [Previous : 03 : Digital Logic with TL-Verilog](../03%20:%20Digital%20Logic%20with%20TL-Verilog) &nbsp;|&nbsp; [Next : 05 : Pipelined RISC-V CPU](../05%20:%20Pipelined%20RISC-V%20CPU)
