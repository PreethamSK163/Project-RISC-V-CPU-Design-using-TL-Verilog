# RISC-V CPU Design Using TL-Verilog

> A hands-on implementation of a RISC-V CPU — progressing from ISA fundamentals and GNU toolchain to a fully functional 5-stage pipelined processor with hazard resolution, bypassing, and memory operations, designed using TL-Verilog on the Makerchip platform.

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Tool](https://img.shields.io/badge/Tool-Makerchip-blue)
![Tool](https://img.shields.io/badge/Tool-TL--Verilog-blue)
![Tool](https://img.shields.io/badge/Tool-Spike-blue)
![Tool](https://img.shields.io/badge/Tool-GNU%20Toolchain-blue)
![ISA](https://img.shields.io/badge/ISA-RISC--V%20RV32I-orange)
![Program](https://img.shields.io/badge/Program-VSD%20MYTH%20Workshop-red)

<h2>🔍 Overview</h2>

- Implemented a complete **RISC-V RV32I CPU** from scratch — starting from ISA fundamentals, GNU toolchain usage, and ABI conventions, progressing through single-cycle micro-architecture to a fully pipelined 5-stage processor.
- Designed and verified the pipelined CPU in **TL-Verilog on Makerchip** — implementing instruction fetch, decode, register file, ALU, branch logic, data hazard bypassing, memory operations, and automated testbench verification.

<h2>🛠️ Tools & Technology Stack</h2>

| Category | Tool / Technology |
|:---|:---|
| HDL | TL-Verilog |
| IDE | Makerchip (Cloud-based) |
| ISA | RISC-V RV32I |
| Compiler | RISC-V GCC (riscv64-unknown-elf-gcc) |
| Simulator | Spike RISC-V ISA Simulator |
| Debugger | GDB + Spike interactive debug |
| Disassembler | riscv64-unknown-elf-objdump |
| Waveform Viewer | GTKWave |
| OS | Ubuntu Linux |

<h2>⚙️ Complete Implementation Flow</h2>

| Stage | Description | Status |
|:---|:---|:---|
| RISC-V ISA & Toolchain | GCC compilation, Spike simulation, disassembly, number representation | ✅ Complete |
| ABI & Verification | Calling conventions, C-to-assembly interfacing, co-simulation | ✅ Complete |
| Digital Logic (TL-Verilog) | Combinational, sequential, pipelined logic, validity, Makerchip | ✅ Complete |
| Single-Cycle CPU | PC, fetch, decode, register file, ALU, branch logic, testbench | ✅ Complete |
| Pipelined CPU | 5-stage pipeline, hazard detection, bypassing, memory ops, full RV32I | ✅ Complete |

<h2>📊 Key Results — Pipelined RISC-V CPU</h2>

| Metric | Result |
|:---|:---|
| Pipeline Stages | 5 (IF, ID, EX, MEM, WB) |
| ISA Support | Full RV32I (except system instructions) |
| Hazard Resolution | Data forwarding (bypassing) + bubble insertion |
| Branch Handling | Static prediction + pipeline flush |
| Test Program | Sum 1 to 9 — verified x10 = 45 and x15 = 45 (load/store) |
| Verification | Automated Makerchip testbench — PASSED |

<h2>📁 Repository Structure</h2>

## 📁 Repository Structure
```
Project-RISC-V-CPU-Design-using-TL-Verilog/
├── 01 : RISC-V ISA & GNU Toolchain     → GCC, Spike, disassembly, number representation
├── 02 : ABI & Verification Flow        → Calling conventions, C-ASM interfacing, co-simulation
├── 03 : Digital Logic with TL-Verilog  → Combinational, sequential, pipelined logic, Makerchip
├── 04 : Basic RISC-V CPU               → PC, fetch, decode, ALU, branches, single-cycle datapath
├── 05 : Pipelined RISC-V CPU           → 5-stage pipeline, hazards, bypassing, memory operations
├── riscv_pipelined_cpu.tlv             → Final working pipelined CPU implementation
└── README.md
```

<h2>📝 Stage Details</h2>

**01 — RISC-V ISA & GNU Toolchain** &nbsp;|&nbsp; `GCC` `Spike` `objdump` `Number Representation`

Explored RISC-V ISA fundamentals — instruction formats (R, I, S, B, U, J), register file, and modular extensions. Cross-compiled C programs using the RISC-V GCC toolchain, disassembled binaries with objdump, and simulated execution on Spike. Analyzed signed/unsigned number representation and data type limits in C for 64-bit RISC-V.
> 📁 [View Implementation Results](./01%20:%20RISC-V%20ISA%20%26%20GNU%20Toolchain)

**02 — ABI & Verification Flow** &nbsp;|&nbsp; `ABI` `Calling Conventions` `ELF` `Co-Simulation`

Studied the RISC-V Application Binary Interface — function argument passing (a0–a7), return values, callee/caller-saved registers, and stack management. Implemented C-to-assembly function calls following ABI conventions and verified execution on a simulated RISC-V CPU. Explored compliance testing and step-and-compare co-simulation methodology.
> 📁 [View Implementation Results](./02%20:%20ABI%20%26%20Verification%20Flow)

**03 — Digital Logic with TL-Verilog** &nbsp;|&nbsp; `TL-Verilog` `Makerchip` `Pipeline` `Validity`

Designed combinational and sequential digital logic circuits using TL-Verilog on the Makerchip platform — implementing logic gates, multiplexers, counters, and a sequential calculator. Built pipelined logic with validity signals for clock gating and hazard control. Developed a 2-cycle calculator with memory recall as preparation for CPU pipeline design.
> 📁 [View Implementation Results](./03%20:%20Digital%20Logic%20with%20TL-Verilog)

**04 — Basic RISC-V CPU** &nbsp;|&nbsp; `Program Counter` `Instruction Fetch` `ALU` `Branch Logic`

Implemented a single-cycle RISC-V datapath from scratch — PC logic with reset and branch redirection, instruction memory interface, instruction type decoding (R/I/S/B/U/J), field extraction, register file read/write, ALU for ADD/ADDI, branch logic for BLT, and automated testbench verification. Verified correct execution of the sum 1–9 program with result in x10 = 45.
> 📁 [View Implementation Results](./04%20:%20Basic%20RISC-V%20CPU)

**05 — Pipelined RISC-V CPU** &nbsp;|&nbsp; `5-Stage Pipeline` `Bypassing` `Hazard Detection` `Memory`

Extended the single-cycle design to a fully pipelined 5-stage architecture — implementing valid signal control, PC redirection for branches and loads, data hazard resolution through register file bypassing, complete RV32I instruction decode and ALU, all branch conditions, data memory interface for load/store operations, JAL/JALR jump handling, and automated testbench verification with store/load round-trip check.
> 📁 [View Implementation Results](./05%20:%20Pipelined%20RISC-V%20CPU)

<h2>📚 References</h2>

| **TL-Verilog Shell Library** | [github.com/BalaDhinesh/RISC-V_MYTH_Workshop](https://github.com/BalaDhinesh/RISC-V_MYTH_Workshop) |
|:---|:---|
| **Makerchip IDE** | [makerchip.com](https://makerchip.com) |
| **RISC-V ISA Spec** | [riscv.org/specifications](https://riscv.org/specifications/) |

<h2>🤝 Connect</h2>

| **Author** | Preetham SK |
|:---|:---|
| **Program** | NASSCOM FutureSkills Prime — VSD (VLSI System Design) |
| **LinkedIn** | [linkedin.com/in/preethamsk16](https://www.linkedin.com/in/preethamsk16) |
| **GitHub** | [github.com/PreethamSK163](https://github.com/PreethamSK163) |
| **Email** | preethamsk163@gmail.com |
