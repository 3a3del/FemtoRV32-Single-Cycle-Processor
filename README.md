# FemtoRV32-Single-Cycle-Processor
This project implements a 32-bit RISC-V Single-Cycle Processor that supports that supports the base integer instruction set according to the specifications found here: https://riscv.org/technical/specifications/, covering a variety of arithmetic, logical, memory, and control operations.
# Design Architecture

![](https://github.com/3a3del/FemtoRV32-Single-Cycle-Processor/blob/main/Arch.png)
  
## Features
 - "Instruction Set:" Supports 40 RISC-V instructions, including arithmetic, logic, memory access, and branching.
 - 32-bit Data Path: Designed for 32-bit operations across all components like registers, ALU, and memory.
 - Single-Cycle Execution: Each instruction is executed within one clock cycle.                                         
 - Control Unit: Decodes the opcode and generates control signals for all components.
 - ALU: Performs arithmetic and logic operations based on control signals.
 - Register File: Contains 32 registers, each 32-bits wide, allowing two simultaneous read operations and one write operation.
 - Memory: Data Memory and Instruction Memory modules for loading/storing data and fetching instructions.
 - PC Control: Handles Program Counter (PC) updates for sequential and branch/jump instructions.  
  
  
  
  
  
  
  
