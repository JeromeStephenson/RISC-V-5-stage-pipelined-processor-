# RISC-V-5-stage-pipelined-processor-

A high-performance, 5-stage pipelined processor implementing the RISC-V 32I (Base Integer) Instruction Set Architecture. This core is designed to maximize throughput by overlapping the execution of multiple instructions while effectively managing hardware hazards.

# Architectural Overview

The processor is divided into five distinct stages to ensure efficient instruction processing:

**Instruction Fetch (IF):** Accesses Instruction Memory to retrieve the next 32-bit instruction based on the Program Counter (PC).

**Instruction Decode (ID):** Translates the instruction, generates control signals, and reads operands from the Register File.

**Execute (EX):** Performs arithmetic/logic operations using the ALU and calculates branch target addresses.

**Memory (MEM):** Handles data memory access for Load and Store instructions.

**Write Back (WB):** Commits the final results back to the Register File


# Features
Supported Instruction Types

The core provides full support for the standard RISC-V instruction formats:

**R-Type:** Register-to-register operations (e.g., ADD, SUB, AND, OR).

**I-Type:** Immediate operations and Loads (e.g., ADDI, LW).

**S-Type:** Store operations (e.g., SW).

**B-Type:** Conditional branching (e.g., BEQ, BNE).

**J-Type:** Jump and Link (e.g., JAL).

**U-Type:** Upper Immediate instructions (e.g., LUI).

## Hazard Management Unit

To maintain the integrity of the pipeline and prevent "race conditions," a dedicated Hazard Unit is implemented to handle:

**Data Hazards:** Resolved via Forwarding (bypassing) logic to minimize stalls, allowing the EX stage to use results before they are written back to the register file.

**Structural Hazards:** Managed through efficient resource partitioning (separate Instruction and Data memories).

**Control Hazards:** Handled through pipeline flushing logic during branch mispredictions.


## IMPLIMENTATION AND PROCEDURE

To implement a 5-stage pipeline, synchronous pipeline registers must be strategically inserted between each stage of the datapath to buffer and propagate instruction data, control signals, and operands. These registers—IF/ID, ID/EX, EX/MEM, and MEM/WB—act as state-preserving boundaries that allow the processor to process five different instructions simultaneously in a single clock cycle. By dividing the execution flow into discrete temporal segments, each instruction part moves through the stages in a synchronized manner, ensuring that the correct control bits and calculated results reach their final destination without interference. This architecture is an evolved, high-throughput extension of the single-cycle datapath, where the logic is no longer completed in one cycle but is instead distributed across the pipeline to achieve much higher operating frequencies.
