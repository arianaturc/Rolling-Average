# 🎛️ Rolling Average (VHDL, Vivado)

## 📖 Overview
This project implements a **rolling average digital filter** on a  
**Xilinx/Digilent Spartan 3 XC3S200 FPGA** using **VHDL in Vivado**.

The system takes an 8-bit parallel data stream, computes the rolling average  
over a configurable number of samples, and displays both the **current input**  
and the **calculated average** on the FPGA’s **seven-segment display (SSD)**.

This project was originally developed in 2024, in the **first year of university**.

## ✨ Features
- ➗ **Rolling Average Filter**: Supports 2, 4, 8, or 16 sample averages.  
- 🔀 **Multiple Data Sources**:
  - Constant 0 (test mode)  
  - Square wave  
  - Repeated student ID sequences  
  - Pseudo-random sequences (LFSR, 4-bit and 8-bit)  
- 🔢 **Seven-Segment Display Output**: Shows input value + average in real time.  
- ⏱ **Clock Management**: Divided down for 1 Hz data clock operation.  



## 🏗 Project Structure
The design is modular and built from the following main components:

- `Clock_Divider` → Generates slower clock signals  
- `Freq_Divider_ssd` → Handles SSD refresh multiplexing  
- `MUX_8_to_1_with_Generator` → Selects between input data sources  
- `Compute_average` → Calculates the rolling average  
- `D_FF` → Stores/delays values for buffering  
- `mux_catod` & `mux_anod` → Drive SSD cathodes/anodes  
- `decoder` → Converts binary values into seven-segment codes  
- `RollingAverage.vhd` → **Top-level entity**, integrating all modules  

---

## ⚙️ How It Works
1. **Data Source Selection**  
   - `sel1` (3-bit): Chooses the data generator mode.  
   - `sel2` (3-bit): Sets averaging window (2, 4, 8, 16 samples).  

2. **Rolling Average Calculation**  
   - Input data is buffered.  
   - Oldest sample discarded when new sample arrives.  
   - Running total is divided by buffer size.  

3. **Output Display**  
   - Current value + average are packed into a 16-bit signal.  
   - Multiplexed and displayed on the SSD.  

## 🎮 Controls
- `reset1` → Resets the data generator  
- `reset2` → Resets the averaging filter  
- `sel1` (3 bits) → Selects input data source  
- `sel2` (3 bits) → Selects buffer length  

