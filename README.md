# RV32I Single-Cycle Processor — SystemVerilog

An independent implementation following the module contracts of the course's
RISC-V single-cycle assignment. The design is divided into IF, ID, EX and WB
stages. Instruction and data memories are external to the core.

## Repository structure

- `IF_Stage/rtl.sv` — program counter and next-PC selection
- `Decoder/rtl.sv` — instruction field extraction
- `Immediate_Generator/rtl.sv` — sign extension and immediate formatting
- `Register_File/rtl.sv` — 32 × 32-bit register file
- `Main_Control/rtl.sv` — opcode control decoder
- `ID_Stage/rtl.sv` — decode-stage integration
- `ALU/rtl.sv` — arithmetic, logical and branch operations
- `ALU_Control/rtl.sv` — ALU operation decoder
- `EX_Stage/rtl.sv` — ALU, branch and jump target logic
- `WB_Stage/rtl.sv` — write-back data selection
- `Single_Cycle_RISCV/rtl.sv` — complete core integration
- `rnr-stage.yaml` — assignment CI module/source mapping

## Important architecture notes

- Reset sets the PC to `0x80000000`.
- Register x0 always reads as zero and ignores writes.
- Instruction memory supplies `instruction` using `address`.
- Data memory is external and supplies `mem_out`; the core exposes
  `alu_out`, `rs2_data`, `mem_read`, `mem_write`, and `fn3`.
- The core supports the instruction set specified by the course contract.
- Vivado is suitable for local simulation. The assignment CI uses Yosys;
  avoid SystemVerilog constructs unsupported by the CI toolchain.

## Use

Add the folders and `rnr-stage.yaml` to the root of your assignment repository.
Commit and push, then open the repository's **Actions** tab to inspect the
course CI result.
