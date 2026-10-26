# 8bit_RISC-CPU-Core
8-Bit RISC CPU Core (Custom 5-Stage Pipeline) 🚀

Author: Nguyen Phuc Bao Khang (Roll Number: SE203511)

Architecture: 8-bit Datapath | 16-bit Instruction Set | Harvard Architecture | 5-Stage Pipeline

Implementation: Verilog HDL (Xilinx Vivado)

📌 Project Overview

This project is a highly optimized, custom 8-bit RISC microprocessor. Starting from a standard base architecture, this design introduces significant hardware enhancements, including a Hardware Multiplier, Memory-Mapped I/O (MMIO), and an Advanced Hazard Resolution Unit (Forwarding & Flushing). These upgrades eliminate the need for software stalls and loops, achieving a highly efficient execution cycle.

📂 Repository Structure

The repository is organized into three main directories for clean project management:

1_SourceCode/: Contains all raw Verilog files and machine code.

RTL/: The core hardware modules.

cpu_5stage_top.v (Top-level CPU wrapper)

alu_core.v (ALU with integrated Combinational Multiplier)

ctrl_decode.v (Control Unit & Instruction Decoder)

hazard_ctrl.v (Hazard Unit for Forwarding and Flushing)

data_mem.v, inst_mem.v, reg_bank.v (Memory and Registers)

Testbench/: Advanced verification environment.

tb_cpu_5stage.v (Event-logging and Auto-Verification testbench)

program.hex: The compiled 16-bit machine code loaded into ROM.

2_Document/: Project documentation and presentation materials.

8-bit-RISC-Processor.pptx (Final presentation slides containing execution traces, waveforms, and architecture diagrams).

3_VivadoProject/: The ready-to-run Xilinx Vivado environment.

8Bit.xpr (Open this file in Vivado to instantly load the project, source files, and simulation settings).

✨ Key Hardware Upgrades

1. Hardware Multiplier

Introduced a custom MUL instruction and combinational multiplier logic.

Calculates 8-bit multiplication (yielding a 16-bit product, keeping the lower 8 bits) in a single cycle, completely replacing costly software accumulation loops.

2. Memory-Mapped I/O (MMIO)

Integrates physical peripheral communication directly into the data memory address space without needing dedicated IN/OUT instructions.

0xFE: Hardwired to Input Switches.

0xFF: Hardwired to Output LEDs. Features a hardware RAM-bypass multiplexer to protect internal memory from being overwritten during I/O operations.

3. Advanced Hazard Resolution

Data Hazards: A Hardware Forwarding unit resolves Read-After-Write (RAW) dependencies by routing data directly from MEM/WB stages back to the EX stage (0-cycle and 1-cycle delays).

Control Hazards: Automatic Hardware Flushing inserts NOP (0x0000) bubbles upon taken branches to discard invalid instructions, optimizing the pipeline without software intervention.

📊 Performance Metrics

Tested against a heavy validation workload (Math, Branching, and I/O), the CPU achieved exceptional performance metrics, verified via Vivado Waveforms:

Total Cycles: 31

Instructions Retired: 22

CPI (Cycles Per Instruction): 1.41

Pipeline Stalls: 1

Branch Flushes: 2

Data Forwards: 8

🛠️ How to Run the Simulation

Open Vivado.

Navigate to 3_VivadoProject/ and open 8Bit.xpr.

Click Run Simulation -> Run Behavioral Simulation.

Open the TCL Console to view the real-time Execution Trace. The custom testbench (tb_cpu_5stage.v) will automatically log ALU calculations, I/O events, and branch flushes in readable English, followed by an Auto-Verification Pass/Fail summary.
