# DC Motor Manufacturing Quality Control — SPC Analysis

Statistical Process Control (SPC) analysis of a DC motor manufacturing process, focusing on **winding resistance (WR)** as the key quality characteristic. The study detects process instability, identifies root causes using the 6M Fishbone framework, applies corrective actions, and validates the improved process through capability analysis.

> **Course:** Quality Control  
> **Institution:** Helwan National University — Robotics & Mechatronics Department  
> **Supervisor:** Prof. Nariman &nbsp;|&nbsp; **TA:** Asmaa AL-Robi  
> **Team:** Yousef Ahmed Elbeltagy · Mohamad Sherif Shabrawy · Mohamed Ali Ismail · Verina Elkess · Yousef Wail Ismail · Amr Sherif Maher

---

## Dataset

30 production batches of **DCM-750 DC motors**, 5 motors inspected per batch. For each batch: 5 winding resistance (WR) measurements in ohms + number of defective units.

| Parameter | Value |
|---|---|
| Quality Characteristic | Winding Resistance (WR) in ohms (Ω) |
| Specification Limits | LSL = 4.20 Ω · USL = 4.80 Ω |
| Production Batches | 30 |
| Subgroup Size (n) | 5 motors per batch |
| Total Units Inspected | 150 |

---

## Analysis Workflow

| Step | Tool | Purpose |
|---|---|---|
| 1 | X-bar & R Charts | Monitor process mean and variation |
| 2 | P-Chart | Track proportion of defective units |
| 3 | Fishbone Diagram (6M) | Identify root causes of variation |
| 4 | Pareto Chart | Rank causes — vital few vs. trivial many |
| 5 | Process Improvement | Apply corrective actions |
| 6 | Revised Control Charts | Verify stability after improvements |
| 7 | Anderson-Darling Normality Test | Validate normality assumption |
| 8 | Process Capability (Cpk) | Assess whether process meets spec limits |
| 9 | Run Chart | Visualize trends over time |

---

## Step 1 — X-bar and R Charts (Initial)

Both charts were constructed manually and verified with Minitab. The **red points** indicate out-of-control batches detected by Minitab's violation rules.

![Xbar-R Chart Initial](docs/images/xbar_r_initial_minitab.jpg)

**Findings — process is NOT in statistical control:**
- **X-bar Chart:** B13 (X̄ = 4.720) and B19 (X̄ = 4.650) exceed UCL = 4.606 → process mean shifted upward
- **R Chart:** B16 (R = 0.380) exceeds UCL = 0.326 → abnormal within-batch variability

---

## Step 2 — P-Chart (Proportion Defective)

The p-chart tracks the proportion of defective motors across all 30 batches.

![P-Chart Initial](docs/images/p_chart_initial_minitab.jpg)

**p̄ = 0.10** · UCL = 0.5025 · LCL = 0

Batches **B14** and **B19** spike above the UCL (p = 0.60) — confirming that the process instability identified in the X-bar/R charts directly drives high defect rates.

---

## Step 3 — Root Cause Analysis (Fishbone Diagram)

A Fishbone (Ishikawa) diagram investigated the causes of instability across the 6M framework, targeting out-of-control batches B13, B14, B16, and B19.

![Fishbone Diagram](docs/images/fishbone_diagram.jpg)

| Category | Key Causes Identified |
|---|---|
| **Machine** | Cooling system failure, bearing wear, no preventive maintenance |
| **Material** | Wire resistance variation, insulation coating defects, supply inconsistency |
| **Environment** | High ambient temperature, poor ventilation, no temperature monitoring |
| **Man / Method** | Operator fatigue, inadequate training, no escalation protocol |
| **Measurement** | No inline WR sensor, uncalibrated equipment, manual recording errors |
| **Mother Nature** | Humidity variation, seasonal temperature peaks |

---

## Step 4 — Pareto Analysis

The Pareto chart ranks defect causes by frequency to identify the vital few that drive most of the problem.

![Pareto Chart](docs/images/pareto_minitab.jpg)

| Cause | Frequency | Cumulative % |
|---|---|---|
| **Thermal Issues** | 45.5% | 45.5% |
| **Material Defect** | 27.3% | 72.7% |
| Machine Fault | 9.1% | 81.8% |
| Operator/Method | 9.1% | 90.9% |
| Measurement | 9.1% | 100.0% |

> **Thermal Issues + Material Defects = 72.7% of all defects → primary improvement targets.**

---

## Step 5 — Corrective Actions

- **Thermal Control** — Improved cooling systems, enhanced workshop ventilation, real-time temperature monitoring
- **Material QC** — Standardized insulation coating, rigorous raw material inspection, supplier quality verification
- **Equipment Maintenance** — Preventive maintenance schedules, worn bearing replacement, instrument calibration
- **Operator Training** — SPC training programs, clear escalation procedures for abnormal conditions

---

## Step 6 — Revised Control Charts (After Improvement)

Out-of-control batches (B13, B14, B16, B19) were removed and control limits recalculated. The final X-bar chart confirms the process mean is fully stable.

| Final X-bar Chart | Revised P-Chart |
|:---:|:---:|
| ![Final X-bar](docs/images/xbar_final_minitab.jpg) | ![Revised P-Chart](docs/images/p_chart_revised_minitab.jpg) |
| All 27 remaining batches within UCL=4.5867 / LCL=4.4214 ✓ | All defect proportions within UCL=0.3277 · Revised p̄ = 4.62% (down from 10.0%) ✓ |

---

## Step 7 — Process Capability Analysis (Cpk)

The Minitab Capability Report evaluates whether the improved process reliably produces motors within the 4.20–4.80 Ω specification range.

![Capability Report](docs/images/capability_report.jpg)

| Parameter | Value |
|---|---|
| LSL | 4.20 Ω |
| USL | 4.80 Ω |
| Process Mean | 4.503 Ω |
| **Cpk (Manual)** | **1.57** |
| **Cpk (Minitab)** | **1.69** |

> Both values exceed 1.33 → **HIGHLY CAPABLE PROCESS ✓**  
> The bell curve is well-centered within the spec limits with minimal spread.

---

## Step 8 — Run Chart

The run chart plots subgroup means in chronological order to detect trends, shifts, or patterns over time.

![Run Chart](docs/images/run_chart_minitab.jpg)

Subgroup means fluctuate randomly around the process mean — **no trends, shifts, or patterns** detected after corrective actions ✓

---

## Before vs. After Improvement

| Metric | Before | After |
|---|---|---|
| R Chart | **B16 out of control** (R = 0.380 > UCL) | All points within limits ✓ |
| X-bar Chart | **B13 & B19 out of control** | All points within limits ✓ |
| P-Chart | **B14 & B19** exceed UCL (p = 0.60) | All points within limits ✓ |
| Average Defect Rate | **10.0%** | **4.62%** (−54%) ✓ |
| Process Capability (Cpk) | Not reliable | **1.57 – 1.69 (Highly Capable)** ✓ |

---

## Repository Structure

```
dc-motor-quality-control-spc/
├── data/
│   └── DCMotor_QC_Dataset.xlsx     # Raw dataset: 30 batches, n=5, WR + defect counts
└── docs/
    ├── QC_Report.pdf               # Full report with all calculations and analysis
    └── images/                     # Control charts, Fishbone, Pareto, Capability report
```

---

## Tools Used

- **Minitab** — Control charts, normality test, Pareto chart, process capability report
- **Manual Calculations** — All SPC formulas by hand using Appendix VI constants (A₂, D₃, D₄, d₂)
- **SPC Methods** — X-bar/R charts, P-chart, Fishbone (6M), Pareto, Anderson-Darling, Cpk, Run chart
