# FemtoRV32-Single-Cycle-Processor
This project implements a 32-bit RISC-V Single-Cycle Processor that supports that supports the base integer instruction set according to the specifications found here: https://riscv.org/technical/specifications/, covering a variety of arithmetic, logical, memory, and control operations.
- supporting R- type instructions
- supporting I- type instructions
- supporting B-type instructions
- supporting Store-type instructions
- supporting load-type instructions
- supporting JAL instruction
- supporting JALR instruction
- supporting AUIPC instruction
- supporting AUIPC instruction

## Design Architecture

![](https://github.com/3a3del/FemtoRV32-Single-Cycle-Processor/blob/main/Arch.png)
  
## Features
 - Instruction Set: Supports 40 RISC-V instructions, including arithmetic, logic, memory access, and branching.
 - 2-bit Data Path: Designed for 32-bit operations across all components like registers, ALU, and memory.
 - Single-Cycle Execution: Each instruction is executed within one clock cycle.                                         
 - Control Unit: Decodes the opcode and generates control signals for all components.
 - ALU: Performs arithmetic and logic operations based on control signals.
 - Register File: Contains 32 registers, each 32-bits wide, allowing two simultaneous read operations and one write operation.
 - Memory: Data Memory and Instruction Memory modules for loading/storing data and fetching instructions.
 - PC Control: Handles Program Counter (PC) updates for sequential and branch/jump instructions.  
  
## Supported Instructions

![](https://github.com/3a3del/FemtoRV32-Single-Cycle-Processor/blob/main/InstructionSets.png)
  
## Design Structure  
 - `ControlUnit.v`: Verilog code for the Control Unit that generates control signals.                     
 - `ALU.v`: Arithmetic Logic Unit for performing operations.
 - `RegisterFile.v`: 32x32 register file implementation.
 - `DataMemory.v`: Memory module for data load/store instructions.
 - `InstructionMemory.v`: Stores program instructions.
 - `top.v`: Top module integrating all the components.                                                            
  
## Testing
All Testing Source Codes in `Src` folder and the verification's pictures.

## How to Run
  1. Clone the Repo
 ```bash
  git clone https://github.com/username/risc-v-32-bit-processor.git
  cd risc-v-32-bit-processor
  ```                    
  2. Write any assembly code that you need the processor to excute it, write it in .text Section the `code.S` in `firmware`.
  3. Run first Commond in `gcc_commands.sh`, that assemble the source code to object code by `riscv32 compilar`
 ```bash
riscv32-unknown-elf-gcc -c -mabi=ilp32 -march=rv32i -o code.o code.S
  ```
4. Linking Step to get the Binary file
 ```bash
riscv32-unknown-elf-gcc -Og -mabi=ilp32 -march=rv32i -ffreestanding -nostdlib -o code.elf -Wl,--build-id=none,-Bstatic,-T,sections.lds,-Map,code.map,--strip-debug code.o -lgcc
  ```
5. After get the .elf file convert it to dumpfile to get the readable instruction file
 ```bash
riscv32-unknown-elf-objdump -d code.elf > dumpfile
 ```                    
  
6. Get the risc-v Machine code file
```bash
riscv32-unknown-elf-objcopy  -O binary code.elf code.bin
  ```                    
7. Convert the Machine code instructions to Hex code to be read in our processor
 ```bash
python3 makehex.py code.bin 1024 > code.hex
```
8. First .py to convert the hex to bin 64 line as our instruction memory bear up to 32 x 64 inst, Second .py convert to 64 lines, third .py the get the random Memory data for our data memory
 ```bash
python3 HextoBin.py
python3 lines64.py
python3 randomMEMgen.py
```
