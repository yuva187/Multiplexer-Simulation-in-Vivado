# SIMULATION AND IMPLEMENTATION OF MULTIPLEXER

## AIM
To design and simulate a 4:1 Multiplexer (MUX) using Verilog HDL in four different modeling styles—Gate-Level, Data Flow, Behavioral, and Structural—and to verify its functionality through a testbench using the Vivado 2023.1 simulation environment. The experiment aims to understand how different abstraction levels in Verilog can be used to describe the same digital logic circuit and analyze their performance.

## APPARATUS REQUIRED
- **Vivado 2023.1**

## Procedure
### Launch Vivado
- Open Vivado 2023.1 from the Start menu or desktop icon.

### Create a New Project
1. Click **"Create Project"**.
2. Enter the project name (e.g., `Mux4_to_1`) and choose a location. Click **Next**.
3. Select **RTL Project** and click **Next**.
4. Add Verilog files (e.g., `mux4_to_1_gate.v`, `mux4_to_1_dataflow.v`) and enable **"Copy sources into project"**. Click **Next**.
5. Skip the Constraints step and proceed.
6. Select a default FPGA part (e.g., `xc7a35ticsg324-1L`). Click **Next**, then **Finish**.

### Add Source Files (if needed)
- In the Sources window, right-click on **"Design Sources"** → **Add Sources**.
- Add Verilog files and the testbench (`mux4_to_1_tb.v`).

### Check Syntax
- In the Flow Navigator, under **Synthesis**, click **"Run Synthesis"**.
- Correct any errors or warnings, then re-run the synthesis.

### Simulate the Design
- In the Flow Navigator, under **Simulation**, click **"Run Behavioral Simulation"**.

### Analyze Simulation Results
- View waveform signals (e.g., `S1`, `S0`, `A`, `B`, `C`, `D`, etc.).
- Use the waveform controls to zoom, scroll, and analyze results.

### Adjust Simulation Time
- Click **"Simulation"** → **"Simulation Settings"** to modify the run time (e.g., 1000ns).

### Generate Report
- Right-click the simulation window → **"Export Simulation Results"**.

### Save and Document
- Click **File** → **Save Project**.
- Capture screenshots of the waveform window for your lab report.

### Close Simulation
- Go to **"Simulation"** → **"Close Simulation"** when finished.

---

## Logic Diagram
![image](https://github.com/user-attachments/assets/d4ab4bc3-12b0-44dc-8edb-9d586d8ba856)

---

## Truth Table
![image](https://github.com/user-attachments/assets/c850506c-3f6e-4d6b-8574-939a914b2a5f)

---

## Verilog Code

### 4:1 MUX Gate-Level Implementation
```verilog
module mux4_to_1_gate (
    input wire A,
    input wire B,
    input wire C,
    input wire D,
    input wire S0,
    input wire S1,
    output wire Y
);
    wire not_S0, not_S1;
    wire A_and, B_and, C_and, D_and;

    not (not_S0, S0);
    not (not_S1, S1);

    and (A_and, A, not_S1, not_S0);
    and (B_and, B, not_S1, S0);
    and (C_and, C, S1, not_S0);
    and (D_and, D, S1, S0);

    or (Y, A_and, B_and, C_and, D_and);
endmodule
