# Pipelined RISC-V CPU
> 5-Stage Pipeline, Data Hazard Bypassing, Memory Operations & Full RV32I Implementation

![Tool](https://img.shields.io/badge/Tool-TL--Verilog-blue)
![Tool](https://img.shields.io/badge/Tool-Makerchip-blue)
![ISA](https://img.shields.io/badge/ISA-RISC--V%20RV32I-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

<h2>🔍 Overview</h2>

- Extended the single-cycle RISC-V datapath to a fully pipelined architecture in TL-Verilog — implementing `$valid` signal control, PC redirection for branches and loads, data hazard resolution through register file bypassing, complete RV32I instruction decode and ALU, all branch conditions, JAL/JALR jump handling, and data memory interface for load/store operations.
- Verified functional correctness with an automated testbench — executing the sum 1–9 program with store/load round-trip check, confirming x10 = 45 and x15 = 45 via the final working `riscv_pipelined_cpu.tlv` implementation. Further optimised for improved pipeline efficiency and correctness.

<h2>⚙️ Tasks Covered</h2>

| Task | Description |
|:---|:---|
| 3-Cycle $valid & PC Redirection | Valid signal generation, branch PC redirect, debug |
| Register File Bypass | Data forwarding from EX stage to resolve RAW hazards |
| PC Increment Every Cycle | Continuous PC increment replacing 3-cycle gap |
| Complete Instruction Decode | Full RV32I decode — all R/I/S/B/U/J types, $is_load |
| Complete ALU Implementation | All arithmetic, logical, shift, compare, jump operations |
| Redirect Loads | Load-use bubble insertion, $inc_pc redirect |
| Connect Data Memory Interface | dmem_rd_en, dmem_wr_en, addr[5:2], load/store |
| Load/Store in Program | SW/LW test — store result, load to x15, verify x15 = 45 |
| Final Save | JAL/JALR support, jump bubbles, complete pipelined CPU |
| Optimised Final CPU | Improved pipeline efficiency, waveform & viz verification |

<h2>📝 Stage Details</h2>

**Task 1 — 3-Cycle $valid & PC Redirection** &nbsp;|&nbsp; `$valid` `$start` `Branch Redirect` `Debug`

Generated the `$start` signal — high for one cycle immediately after reset deassertion — to produce the first `$valid` pulse that propagates through the 3-cycle pipeline. Introduced `$valid_taken_br = $valid && $taken_br` to prevent invalid branch instructions from redirecting the PC. Debugged and refined the `$inc_pc` signal for correct sequential flow.

**Task 2 — Register File Bypass** &nbsp;|&nbsp; `Data Forwarding` `RAW Hazard` `EX→ID`

Updated `$src1_value` and `$src2_value` with forwarding logic — if the previous instruction wrote to the register file (`>>1$rf_wr_en`) and the destination matches the current source register, the forwarded `>>1$result` is used instead of the stale register file output. Eliminates read-after-write data hazards without stalling.

**Task 3 — PC Increment Every Cycle** &nbsp;|&nbsp; `Pipeline Throughput` `$valid` `Bubbles`

Changed PC to increment every cycle (`>>1$pc + 4`) instead of every 3 cycles, maximizing pipeline throughput. Moved `$valid` to stage `@3` — set low when in the shadow of a taken branch (`>>1$valid_taken_br || >>2$valid_taken_br`) — correctly inserting pipeline bubbles for control hazards.

**Task 4 — Complete Instruction Decode** &nbsp;|&nbsp; `RV32I` `All Types` `$is_load` `Immediate`

Extended the decode stage to cover the full RV32I base instruction set — all R-type, I-type, B-type, S-type, U-type, and J-type instructions. All loads handled with a single `$is_load` signal based on opcode. Implemented immediate generation for all formats.

**Task 5 — Complete ALU Implementation** &nbsp;|&nbsp; `Arithmetic` `Logical` `Shifts` `Compare` `Jumps`

Implemented the full `$result` mux covering all RV32I ALU operations — arithmetic, logical, shifts, compare, upper immediate, and jump return address. Extended branch logic to all six conditions (BEQ, BNE, BLT, BGE, BLTU, BGEU) with signed/unsigned intermediate results.

**Task 6 — Redirect Loads** &nbsp;|&nbsp; `Load-Use Hazard` `Bubble` `$inc_pc`

Cleared `$valid` in the two pipeline cycles following a load instruction — inserting bubbles to prevent load-use hazards. Updated the PC mux to redirect to `>>3$inc_pc` on load completion, ensuring correct instruction re-fetch after the load data is available.

**Task 7 — Connect Data Memory Interface** &nbsp;|&nbsp; `dmem` `addr[5:2]` `Load` `Store`

Enabled the data memory module (`m4+dmem(@4)`) and connected all interface signals — `$dmem_rd_en` for loads, `$dmem_wr_en` for stores, `$dmem_addr[3:0]` from `$result[5:2]` (word-aligned), `$dmem_wr_data` from `$src2_value`, and `$ld_data` from `$dmem_rd_data`.

**Task 8 — Load/Store in Program** &nbsp;|&nbsp; `SW` `LW` `x15` `Testbench`

Added SW and LW instructions to the test program — stores the sum result to memory, then loads it back into x15. Updated the testbench passing condition to verify `xreg[15] == 45`, validating the complete store/load round-trip through data memory.

**Task 9 — Final Save** &nbsp;|&nbsp; `JAL` `JALR` `Jump Bubbles` `Complete CPU`

Added JAL/JALR jump support — jump bubble insertion in `$valid` logic, jump target PC calculation (`$br_tgt_pc` for JAL, `$jalr_tgt_pc = $src1_value + $imm` for JALR), and return address write-back (`$pc + 4`). Completed and saved the fully functional pipelined RISC-V CPU.

**Task 10 — Optimised Final CPU** &nbsp;|&nbsp; `Pipeline Optimisation` `Waveform Verification` `CPU Visualisation`

Further optimised the complete pipelined CPU implementation — refined pipeline control logic for improved efficiency and correctness. Verified the final design using Makerchip's waveform viewer (timing diagram showing all CPU signals across clock cycles) and the block-level CPU visualisation (imem, register file, dmem, and pipeline stage blocks). Confirmed correct execution of the sum 1–9 program with full RV32I instruction coverage.

<h2>📊 Final CPU Implementation Metrics</h2>

| Metric | Result |
|:---|:---|
| Pipeline Stages | 5 |
| ISA Support | Full RV32I (except FENCE/ECALL/EBREAK) |
| Hazard Resolution | Bypassing (data) + Bubble insertion (control/load) |
| Test Program | Sum 1–9 — x10 = 45, x15 = 45 (load/store verified) |
| Verification | Automated Makerchip testbench — PASSED |

<h2>🖼️ Implementation Results</h2>

### 3-Cycle $valid & PC Redirection
![LE1_1_Task_diagram](LE1_1_Task_diagram.png)
![LE1_1_Task_1](LE1_1_Task_1.png)
![LE1_1_Task_2](LE1_1_Task_2.png)
![LE1_2_Task_diagram](LE1_2_Task_diagram.png)
![LE1_2_Task_1](LE1_2_Task_1.png)
![LE1_2_Task_2](LE1_2_Task_2.png)
![LE1_2_Task_3](LE1_2_Task_3.png)
![LE1_3_Task_diagram](LE1_3_Task_diagram.png)
![LE1_3_Task_1](LE1_3_Task_1.png)
![LE1_3_Task_2](LE1_3_Task_2.png)
![LE1_3_Task_3](LE1_3_Task_3.png)

### Register File Bypass
![LE2_1_Task_diagram](LE2_1_Task_diagram.png)
![LE2_1_Task_1](LE2_1_Task_1.png)
![LE2_1_Task_2](LE2_1_Task_2.png)
![LE2_1_Task_3](LE2_1_Task_3.png)

### PC Increment Every Cycle
![LE2_2_Task_diagram](LE2_2_Task_diagram.png)
![LE2_2_Task_1](LE2_2_Task_1.png)
![LE2_2_Task_2](LE2_2_Task_2.png)
![LE2_2_Task_3](LE2_2_Task_3.png)

### Complete Instruction Decode
![LE2_3_Task_diagram](LE2_3_Task_diagram.png)
![LE2_3_Task_1](LE2_3_Task_1.png)
![LE2_3_Task_2](LE2_3_Task_2.png)
![LE2_3_Task_3](LE2_3_Task_3.png)
![LE2_3_Task_4](LE2_3_Task_4.png)

### Complete ALU Implementation
![LE2_4_Task_1](LE2_4_Task_1.png)
![LE2_4_Task_2](LE2_4_Task_2.png)
![LE2_4_Task_3](LE2_4_Task_3.png)

### Redirect Loads
![LE3_1_Task_diagram](LE3_1_Task_diagram.png)
![LE3_1_Task_1](LE3_1_Task_1.png)
![LE3_1_Task_2](LE3_1_Task_2.png)
![LE3_1_Task_3](LE3_1_Task_3.png)

### Connect Data Memory Interface
![LE3_2_Task_diagram](LE3_2_Task_diagram.png)
![LE3_2_Task_1](LE3_2_Task_1.png)
![LE3_2_Task_2](LE3_2_Task_2.png)
![LE3_2_Task_3](LE3_2_Task_3.png)

### Load/Store in Program
![LE3_3_Task_1](LE3_3_Task_1.png)
![LE3_3_Task_2](LE3_3_Task_2.png)
![LE3_3_Task_3](LE3_3_Task_3.png)

### Final Save — Complete Pipelined RISC-V CPU
![LE3_4_Task_1](LE3_4_Task_1.png)
![LE3_4_Task_2](LE3_4_Task_2.png)
![LE3_4_Task_Final Five-Stage Pipelined RISC-V CPU](LE3_4_Task_Final%20Five-Stage%20Pipelined%20RISC-V%20CPU.png)

### Optimised Final CPU
![LE4_1](LE4_1.png)
![LE4_2](LE4_2.png)
![LE4_3](LE4_3.png)

<h2>🔗 Navigation</h2>

[Back to Repository Overview](../README.md) &nbsp;|&nbsp; [Previous : 04 : Basic RISC-V CPU](../04%20:%20Basic%20RISC-V%20CPU)
