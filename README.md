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


![riscv_diagram.png](https://github.com/JeromeStephenson/RISC-V-5-stage-pipelined-processor-/blob/main/riscv_diagram.png)


## DISCUSSIONS



**1. Fetch Cycle Datapath**

The first phase of the instruction execution process is called the fetch cycle. The fetch cycle's primary objective is to get the subsequent instruction from memory so that the processor can decode and execute it.

**2. Decode Cycle Datapath**

The second phase of executing an instruction is called the decode cycle. Interpreting the fetched instruction and setting up the required inputs (registers, control signals) for later stages are the primary goals of this level.

**3. Execution Cycle Datapath**

The third phase of the instruction execution process is known as the execution cycle. Its primary functions include determining the result of a branch, calculating memory addresses for load/store operations, and carrying out the arithmetic or logical operation specified by the instruction.

**4. Memory Read/Write Cycle Datapath** 

The fourth step in the execution of an instruction is called the Memory Read or Write Cycle. When loading or storing instructions, this step is in charge of communicating with data memory. The processor skips this step and proceeds to the writeback stage if the instruction is not a memory operation.

**5. Write Back Cycle Datapath**

The fifth and last phase of the instruction execution process is the writeback cycle. Writing the outcome of an instruction—whether it comes from an arithmetic operation or a memory load—back to the destination register is the primary goal of this stage.

Note: Hazard Unit

**Structural Hazard**

Instruction execution inside a single clock cycle is not supported by hardware.
The RISC-V pipelining design will be structurally hazardous without two memories.

**Data Risk**

There is no data available for execution.
could happen if a pipeline stalls.
Use the forwarding or bypassing strategy to solve the problem.

**A remedy for the data Hazard.** 1. Using nops to solve data hazards 2. Using forwarding or bypassing to solve data hazards

Forwarding and Bypassing are used to address the data hazard.

**Condition Table**
![condition table.png](https://github.com/JeromeStephenson/RISC-V-5-stage-pipelined-processor-/blob/main/condition%20table.png)

**Condition for data hazard**
![condition for data hazard.png](https://github.com/JeromeStephenson/RISC-V-5-stage-pipelined-processor-/blob/main/condition%20for%20data%20hazard.png)



# SIMULATION RESULTS AND TOOLS USED
The simulation has been done in Modelsim that supports verilog simulation.

The output waveform is : 
![condition table.png](





  
