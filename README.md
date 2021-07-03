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

<ins>s<ins>et <ins>l</ins>ess <ins>t</ins>han

## RISC-V Assembly Language

## RV32M: Multiply and Divide

## RV32FD: Single/Double Floating Point

## RV32A: Atomic

## RV32C: Compressed Instructions

## RV32V: Vector

## RV64: 64-bit Address Instructions

## RV32/64 Privileged Architecture

## Future RISC-V Optional Extensions
