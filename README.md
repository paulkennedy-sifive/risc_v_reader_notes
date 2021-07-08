# RISC-V Reader Notes

## Why RISC-V?

### Introduction

- RISC-V belongs to an open, non-profit foundation
- The goal is to maintain the stability of RISC-V, evolve it slowly and carefully, solely for technical reasons, and to try to make it as popular for hardware as Linux is for operating systems

### Modular vs. Incremental ISAs

- RISC-V is modular, not incremental
- At the base is RV32I, which is frozen and will never change
- The modularity comes from optional standard extensions
- Compilers can generate the best code for a given configuration
- By analogy, RISC-V offers a menu, not a banquet
- When new choices appear on the menu, they remain optional, unlike with incremental ISAs

### ISA Design 101

- Measures:
  - Cost
  - Simplicity
  - Performance
  - Isolation of arch from impl
  - Room for growth
  - Code size
  - Programmability

## RV32I: RISC-V Base Integer ISA

### RV32I Instruction Formats

- See figure 2.1 for RV32I diagram
  - Example: <ins>s</ins>et <ins>l</ins>ess <ins>t</ins>han &#123; _, <ins>i</ins>mmediate &#125; &#123; _, <ins>u</ins>nsigned &#125;
- Instruction formats
  - R-type: register-register operations
  - I-type: short immediates and loads
  - S-type: stores
  - B-type: conditional branches
  - U-type: long immediates
  - J-type: unconditional branches
- Features which improve simplicity
  - All instructions are 32 bits long
  - 3 register operands making additional moves unnecessary
  - Source and dest fields are always in the same location
  - Immediate fields are always sign-extended
  - Opcodes are chosen so that common datapath operations share same bit values
- All 1s and all 0s are illegal instructions, aiding in debugging

### RV32I Registers

- 31 registers plus x0 which always has the value zero
- PC is not a GPR

### RV32I Integer Computation

- `lui`: loads a 20-bit constant into most significant 20 bits of a register
- `auipc`: supports two instruction sequences to access arbitrary offsets from the PC for both control-flow transfers and data accesses
  - The combination of an `auipc` and the 12-bit immediate in `jalr` can transfer control to any 32-bit PC-relative address, while an `auipc` plus the 12-bit immediate offset in regular load or store instructions can access any 32-bit PC-relative data address
- There are no byte or half-word integer computations; only 32-bit
  - Narrow data accesses save much time and energy, but narrow data operations do not
- No multiply and divide; these are in the RV32M extension
- No rotate instructions or detection of integer arithmetic overflow; can be done with instructions

### RV32I Loads and Stores

- RV32I has loads for signed and unsigned bytes, halfwords, and words and stores for bytes, halfwords, and words
  - Signed bytes and halfwords are sign-extended to 32 bits and written to destination registers
- Only addressing mode is adding a sign-extended 12-bit immediate to a register, called displacement addressing mode in x86-32
- No delay slots
- Misaligned accesses are permitted
- RISC-V is little-endian

### RV32I Conditional Branches

- Branch comparisons
  - `beq`, `bne`: equal, not equal
  - `bge`, `blt`: signed
  - `bgeu`, `bltu`: unsigned
- Branch addressing mode multiplies 12-bit immediate by 2, sign-extends, adds to PC
  - PC-relative addressing helps with position-independent code
- RISC-V excludes "condition codes" which adds state that is implicitly set by most instructions and complicates dependency checking

### RV32I Unconditional Jump

- `jal` serves two functions: to support procedure calls and unconditional jumps
  - Procedure calls: save address of the next instruction into the destination register, normally `ra`
  - Unconditional jumps: use the zero register instead of `ra` as the destination register
  - Uses same addressing mode as conditional branch instructions
- `jalr` can call a procedure to a dynamically calculated address or perform a procedure return
  - Procedure return: select `ra` as the source and the zero register as the destination
  - Switch/case statements can also use `jalr`

### RV32I Miscellaneous

- Control and Status Register instructions: `csrrc`, `csrrs`, `csrrw`, `csrrci`, `csrrsi`, `csrrwi`
- `ecall`: system calls, debuggers
- `fence`: sequences device I/O and memory accesses as viewed by other threads, external devices, and coprocessors
- RISC-V uses memory-mapped I/O, not `in`/`out` of x86
- RISC-V does not have string instructions such as `rep`, `movs`, etc.

## RISC-V Assembly Language

## RV32M: Multiply and Divide

## RV32FD: Single/Double Floating Point

## RV32A: Atomic

## RV32C: Compressed Instructions

## RV32V: Vector

## RV64: 64-bit Address Instructions

## RV32/64 Privileged Architecture

## Future RISC-V Optional Extensions
