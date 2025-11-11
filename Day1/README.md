# 🚀 Sky130 Day 1 – Inception of Open-Source EDA, OpenLANE and Sky130 PDK

### 🧾 Overview

This document summarizes the learning outcomes and lab practice from **Day 1**, which introduces the fundamentals of open-source VLSI design. You’ll understand how OpenLANE automates the RTL-to-GDSII process, explore the **Sky130 PDK**, and learn how open-source EDA tools form the backbone of modern SoC (System-on-Chip) design.

---

## 1️⃣ How to Talk to Computers 🖥️

Every computer system interprets human logic through multiple abstraction layers. High-level programming languages like **C**, **Python**, or **Java** must eventually be converted into **binary instructions** the hardware can execute.

**Flow of Translation:**

```
High-Level Code → Compiler → Assembly Language → Assembler → Machine Code (0s and 1s)
```
<img width="1920" height="1080" alt="img1" src="https://github.com/user-attachments/assets/13709f5d-db44-4a1a-8387-afca10e47a99" />

Each step reduces human readability but increases machine interpretability — enabling hardware such as CPUs or microcontrollers to perform defined tasks precisely.

---

## 2️⃣ Introduction to QFN-48 Package, Chip, Pads, Core, Die and IPs 📦

A chip is more than just its silicon—it’s a complete **miniaturized system** encapsulated inside a protective package.
<img width="1546" height="846" alt="img2" src="https://github.com/user-attachments/assets/f5cfa765-525d-4729-a1c4-e20ef6d011fc" />
<img width="1522" height="835" alt="img3" src="https://github.com/user-attachments/assets/2d1e1002-3d2a-49f7-aee4-54c57188c122" />


**Hierarchy Overview:**

* **Package:** The outer protective casing (e.g., QFN-48, 7×7 mm) that interfaces the chip to the PCB.
* **Die:** The actual silicon wafer slice hosting the integrated circuit.
* **Core:** The central region where the primary logic, processors, or memory blocks reside.
* **Pads:** Metal contact points that connect internal signals to external pins.
* **IPs (Intellectual Properties):** Pre-verified logic blocks reused across designs.

  * *Foundry IPs:* Provided by fabrication plants (e.g., SRAMs, ADC/DAC).
  * *Custom Macros:* Designer-specific modules like SPI controllers or RISC-V CPUs.

---

## 3️⃣ Introduction to RISC-V 🏛️

**RISC-V** is an open and royalty-free **Instruction Set Architecture (ISA)**. Unlike proprietary architectures such as ARM or x86, it allows developers to design, modify, and extend hardware without licensing costs.

It serves as the fundamental blueprint of a processor—defining how software instructions are executed in hardware. The openness of RISC-V perfectly complements the open-source EDA ecosystem, enabling end-to-end transparency from ISA to silicon layout.
<img width="1920" height="1080" alt="img4" src="https://github.com/user-attachments/assets/48951da4-ef03-4b8e-90ea-6ef868f3f17e" />
<img width="1920" height="1080" alt="img5" src="https://github.com/user-attachments/assets/24262e61-1caa-447d-9a0d-0ea5584c3283" />


---

## 4️⃣ From Software Applications to Hardware 🔄

Consider a simple **C program** (like a stopwatch). The journey from code to silicon involves:

1. **Compiler:** Converts C code to architecture-specific assembly.
2. **Assembler:** Translates assembly into binary instructions.
3. **Processor Hardware:** Executes the binary using transistor-level logic gates within the RISC-V core.

This process embodies the link between **software logic** and **physical hardware execution**.

---

# 🧱 SoC Design and OpenLANE

## 5️⃣ Introduction to Components of Open-Source Digital ASIC Design 🧩

A complete ASIC (Application-Specific Integrated Circuit) design flow integrates three essential parts:

* **RTL Designs:** Hardware description using Verilog or VHDL.
* **EDA Tools:** Suites like OpenLANE, Yosys, OpenROAD, Magic, Netgen handle synthesis, layout, and verification.
* **PDK (Process Design Kit):** Foundry-specific data that defines design rules, layer information, and cell libraries (e.g., SkyWater 130 nm PDK).

### 💡 What PDK Contains

* Design-rule files for **DRC, LVS, PEX**.
* Device models and **SPICE parameters**.
* Standard cell libraries and I/O definitions.
* Technology files for metal layers and density rules.

---

## 6️⃣ Simplified RTL2GDS Flow 🗺️

The **RTL-to-GDSII** sequence automates digital design creation from Verilog code to physical mask layout.

**Stages Overview:**

1. **Synthesis:** Converts Verilog RTL to gate-level netlist using standard cells.
<img width="1856" height="1006" alt="img6" src="https://github.com/user-attachments/assets/dac94b3c-8bb2-46ba-b64f-523339c97a45" />

2. **Floor & Power Planning:** Defines chip core area, places macros, creates PDN rings and straps.
3. **Placement:** Positions standard cells—first globally, then in detail without overlaps.
4. **Clock Tree Synthesis (CTS):** Builds a balanced clock network (often H-Tree or X-Tree).
<img width="1170" height="412" alt="img7" src="https://github.com/user-attachments/assets/d6ebbee6-59b1-47e9-8c67-9a606b49dcf6" />

5. **Routing:** Connects nets using available metal layers (Sky130 has 6).
6. **Sign-Off:** Performs DRC, LVS, and STA to confirm design correctness and manufacturability.

---

## 7️⃣ Introduction to OpenLANE and Strive Chipsets 🏎️

**OpenLANE** is an automated open-source ASIC flow built on tools like Yosys, OpenROAD, Magic, and Netgen. It enables complete **RTL-to-GDSII** processing within Docker.

The **Strive SoC family** (Strive, Strive2, Strive3) are practical chips fabricated using OpenLANE + Sky130 PDK—demonstrating the success of open-source silicon projects.
<img width="1721" height="881" alt="img8" src="https://github.com/user-attachments/assets/827fd3ba-9f4d-4da8-83c5-32ede1bfc43c" />

---

## 8️⃣ OpenLANE Detailed ASIC Design Flow and Modes 📋

The OpenLANE workflow can be executed in:

* **Autonomous Mode:** Fully automated push-button flow.
* **Interactive Mode:** Step-by-step execution for detailed inspection.
<img width="1777" height="948" alt="img9" src="https://github.com/user-attachments/assets/3e498763-0231-4bdc-a1bd-d44fa5721ca0" />

The flow integrates multiple stages—import, synthesis, floorplan, placement, CTS, routing, and sign-off—while managing design data within structured directories.

**Note:** Issues like the **Antenna Effect** are mitigated by inserting antenna diodes during routing to prevent charge buildup.

---

# 🔬 Get Familiar with Open-Source EDA Tools

## 9️⃣ OpenLANE Directory Structure in Detail 📂

When OpenLANE is installed, it maintains a structured workspace:

```
openlane_working_dir/
│
├── openlane/             → Flow scripts and tool integrations  
├── pdks/                 → Sky130 PDK files and libraries  
├── designs/              → Project-specific RTL designs  
├── runs/                 → Auto-generated folders for each execution  
│    ├── results/         → Layouts, DEFs, GDSII  
│    ├── reports/         → Logs & timing summaries  
│    └── tmp/             → Intermediate files  
└── scripts/              → Helper or custom automation scripts  
```

---

## 🔟 Design Preparation Step ⚙️

Before launching OpenLANE, configure your working environment:

```bash
cd ~/Desktop/work/tools/openlane_working_dir
export PDK_ROOT=$(pwd)/pdks
```

Then access the Docker shell and start OpenLANE interactively:

```bash
cd openlane
./flow.tcl -interactive
```

Inside the TCL shell:

```tcl
package require openlane 0.9
prep -design picorv32a
```

This initializes configuration, merges defaults, and creates a unique run directory (e.g., `RUN_2025-11-11_14-35-00`).

---

## 1️⃣1️⃣ Review Files after Design Prep and Run Synthesis 📊

Once preparation completes, execute:

```tcl
run_synthesis
```

This uses **Yosys** to generate a gate-level netlist and **OpenSTA** to perform timing analysis.

Inspect results:

```bash
cd runs/<latest_run>/results/synthesis
ls -ltr
```

Reports and logs are located under:

```bash
cd runs/<latest_run>/reports/synthesis
```

You’ll find synthesis statistics including total cells, flip-flop counts, and area reports.

To calculate **Flop Ratio**:
[
\text{Flop Ratio} = \frac{\text{No. of D-Flip-Flops}}{\text{Total Cells}} \times 100
]
Typical ratios range between **5%–15%**; a healthy design falls within this range.

---

## 1️⃣2️⃣ OpenLANE Project Git Link Description 🔗

You can explore OpenLANE and reference designs via:
👉 [OpenLANE GitHub Repository](https://github.com/The-OpenROAD-Project/OpenLane)
It contains flow scripts, Docker build files, configuration templates, and active community support for open-source VLSI projects.

---

## 1️⃣3️⃣ Steps to Characterize Synthesis Results 📈

1. Open the `synthesis/reports` folder.
2. Compare **pre-synthesis** (generic cell types) and **post-synthesis** (mapped Sky130 cells) statistics.
3. Identify key metrics:

   * Total Standard Cells
   * Number of Flip-Flops (e.g., `sky130_fd_sc_hd__dfxtp_2`)
4. Compute the **Flop Ratio** and interpret timing slack values.
5. Use this data to validate design efficiency before proceeding to floorplanning.

---

## 🏁 Summary

Day 1 established the groundwork for understanding open-source ASIC design using **OpenLANE** and **Sky130 PDK**. By exploring theory and executing the synthesis stage interactively, we bridged the gap between **RTL logic** and **physical implementation**—marking the first step toward a complete open-source chip design flow.

---
