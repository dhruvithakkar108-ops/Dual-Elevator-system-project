# Dual Elevator System Project

An FPGA-based dual-elevator controller designed and implemented in Verilog HDL. The system manages two elevators (A and B) across four floors, dispatching whichever elevator is closer to a requested floor and driving 7-segment displays plus up/down direction indicators for each car.

Designed and simulated in ModelSim-Altera and synthesized using Intel Quartus Prime, with combinational and sequential logic modules verified for correct functionality and timing.

## Features

- **Four-floor coverage** (floors 0–3) for two independent elevators
- **Nearest-car dispatch logic** — compares the distance from each elevator to the requested floor and moves whichever car is closer
- **Synchronous floor movement** — one floor per clock cycle, driven by a manual clock input
- **7-segment displays** showing the current floor for each elevator
- **Direction indicators** (up/down arrows) for each elevator based on request vs. current floor
- **Reset behavior** — Elevator A resets to floor 0, Elevator B resets to floor 3

## Repository Contents

| File | Description |
|---|---|
| `Code for the system on Quartus Altera Modelsim` | Verilog source for the elevator controller and 7-segment decoder |
| `Dual_Elevator_FPGA_Report.pdf` | Project report detailing design, simulation, and synthesis results |
| `README.md` | Project overview and documentation |

## Module Overview

### `Elevator_system`

Top-level module handling request capture, distance calculation, elevator movement, and arrow/display logic.

**Inputs**
- `clk` — manual clock
- `reset` — synchronous reset
- `floor_req [1:0]` — binary floor request (00–11)

**Outputs**
- `seg_A [6:0]`, `seg_B [6:0]` — 7-segment display outputs for Elevator A and B
- `up_arrow_A`, `down_arrow_A` — direction indicators for Elevator A
- `up_arrow_B`, `down_arrow_B` — direction indicators for Elevator B

**Core logic**
1. The requested floor is captured on each clock edge.
2. The absolute distance from the request to each elevator's current floor is computed.
3. Whichever elevator has the shorter (or equal) distance moves one floor toward the request per clock cycle.
4. Direction arrows update combinationally based on whether the request is above or below each elevator's current floor.

### `seven_segment_decoder`

Converts a 2-bit floor value into a 7-bit pattern for driving a 7-segment display (floors 0–3).

## Tools Used

- **Verilog HDL** — hardware description and logic design
- **Intel Quartus Prime** — synthesis and FPGA implementation
- **ModelSim-Altera** — functional simulation and timing verification

## Getting Started

1. Open the project in **Intel Quartus Prime**.
2. Add the Verilog source file to a new project targeting your FPGA board.
3. Assign `clk`, `reset`, `floor_req`, `seg_A`, `seg_B`, and the arrow outputs to appropriate pins/switches/LEDs.
4. Compile and program the FPGA, or simulate first in **ModelSim-Altera** using a testbench that toggles `floor_req` and `clk`.

## Report

See `Dual_Elevator_FPGA_Report.pdf` for the full write-up, including design rationale, simulation waveforms, and synthesis results.

## Author

**Dhruvi Thakkar**
