# DC Motor Manufacturing Quality Control — SPC Analysis

Statistical Process Control (SPC) analysis of a DC motor manufacturing process, focusing on **winding resistance (WR)** as the key quality characteristic. The study detects process instability, identifies root causes using the 6M Fishbone framework, applies corrective actions, and validates the improved process using Cpk capability analysis.

> **Course:** Quality Control  
> **Institution:** Helwan National University — Faculty of Engineering, Dept. of Mechatronics & Robotics Engineering  
> **Supervisor:** Prof. Nariman &nbsp;|&nbsp; **TA:** Asmaa AL-Robi  
> **Academic Year:** 2025–2026  
> **Team:** Yousef Ahmed Elbeltagy · Mohamad Sherif Shabrawy · Mohamed Ali Ismail · Verina Elkess · Yousef Wail Ismail · Amr Sherif Maher

---

## Dataset Overview

| Parameter | Value |
|---|---|
| Quality Characteristic | Winding Resistance (Ω) |
| Spec Limits | LSL = 4.20 Ω &nbsp;\|&nbsp; USL = 4.80 Ω |
| Production Batches | 30 |
| Subgroup Size (n) | 5 motors per batch |
| Total Units Inspected | 150 |
| Total Defectives (Initial) | 15 (10.0%) |

Each batch record includes 5 winding resistance measurements and the count of defective units, analyzed using both manual calculations and Minitab.

---

## SPC Tools Applied

| Step | Tool | Purpose |
|---|---|---|
| 1 | X-bar & R Charts | Monitor process mean and variation |
| 2 | P-Chart | Track proportion of defective units |
| 3 | Fishbone Diagram (6M) | Identify root causes of variation |
| 4 | Pareto Chart | Rank causes by frequency (vital few) |
| 5 | Process Improvement | Apply corrective actions |
| 6 | Revised Control Charts | Verify stability after improvements |
| 7 | Anderson-Darling Normality Test | Validate normality for Cpk |
| 8 | Process Capability (Cpk) | Assess capability vs. spec limits |
| 9 | Run Chart | Visualize trends over time |

---

## Key Results

### Initial Control Chart Analysis

**R Chart**
- UCL = 0.3256 Ω &nbsp;|&nbsp; CL = 0.154 Ω &nbsp;|&nbsp; LCL = 0
- **B16 out of control** — R = 0.380 Ω > UCL → abnormal within-batch spread

**X-bar Chart**
- UCL = 4.6059 Ω &nbsp;|&nbsp; CL = 4.517 Ω &nbsp;|&nbsp; LCL = 4.4281 Ω
- **B13 out of control** — X̄ = 4.720 Ω > UCL → process mean shifted up
- **B19 out of control** — X̄ = 4.650 Ω > UCL → process mean shifted up

**P-Chart**
- UCL = 0.5025 &nbsp;|&nbsp; CL (p̄) = 0.10 &nbsp;|&nbsp; LCL = 0
- **B14 and B19** exceeded UCL (p = 0.60) → abnormally high defect proportion

**Verdict:** Process NOT in statistical control — special causes present.

---

### Root Cause Analysis

Fishbone (Ishikawa) analysis focused on out-of-control batches B13, B14, B16, B19 across the 6M framework:

| Category | Key Causes |
|---|---|
| Machine | Cooling system failure, bearing wear, no preventive maintenance |
| Material | Wire resistance variation, insulation coating defects, supply chain delays |
| Environment | High ambient temperature, poor ventilation, no temp monitoring |
| Man / Method | Operator fatigue, inadequate training, no escalation protocol |
| Measurement | No inline WR sensor, uncalibrated equipment, manual data recording |
| Mother Nature | Humidity variation, seasonal temperature peaks |

### Pareto Analysis — Vital Few

| Cause | Frequency | Cumulative % |
|---|---|---|
| Thermal Issues | 45.5% | 45.5% |
| Material Defect | 27.3% | 72.7% |
| Machine Fault | 9.1% | 81.8% |
| Operator/Method | 9.1% | 90.9% |
| Measurement | 9.1% | 100.0% |

**Thermal Issues + Material Defects = 72.7% of all defects → primary improvement targets.**

---

### Corrective Actions Implemented

- **Thermal Control:** Improved cooling systems, enhanced ventilation, real-time temperature monitoring
- **Material QC:** Standardized insulation coating, rigorous raw material inspection, supplier verification
- **Equipment Maintenance:** Preventive maintenance schedules, worn-part replacement, instrument calibration
- **Operator Training:** Training programs, clear escalation procedures, SPC-based error reduction

---

### After Improvement — Final Results

| Metric | Before | After |
|---|---|---|
| R Chart | B16 exceeded UCL (R = 0.380) | All 29 points within limits ✓ |
| X-bar Chart | B13 & B19 above UCL | All 27 points within limits ✓ |
| P-Chart | B14 & B19 exceeded UCL (p = 0.60) | All points within revised limits ✓ |
| Average Defect Rate (p̄) | 10.0% | 4.62% (−53.8%) ✓ |
| Statistical Control | NOT in control | FULLY in control ✓ |
| Process Capability (Cpk) | Not reliable | 1.57 (manual) / 1.69 (Minitab) ✓ |

---

### Normality Test (Anderson-Darling)

- **AD Statistic:** 0.511
- **p-value:** 0.178 > 0.05 → Fail to reject H₀
- **Result:** Data is approximately normally distributed → Cpk analysis is valid ✓

### Process Capability (Cpk)

| Parameter | Value |
|---|---|
| LSL | 4.20 Ω |
| USL | 4.80 Ω |
| Final Process Mean (X̄̄) | 4.50346 Ω |
| Final Avg Range (R̄) | 0.146 Ω |
| σ = R̄ / d₂ | 0.0628 Ω |
| C_pu | 1.57 |
| C_pl | 1.61 |
| **Cpk (Manual)** | **1.57** |
| **Cpk (Minitab)** | **≈ 1.69** |

> Both values exceed 1.33 → **HIGHLY CAPABLE PROCESS** ✓

---

## Repository Structure

```
dc-motor-quality-control-spc/
├── data/
│   └── DCMotor_QC_Dataset.xlsx      # Raw dataset: 30 batches, n=5, WR measurements + defect counts
└── docs/
    ├── QC_Report.pdf                # Full written report with all calculations and analysis
    └── QC_Presentation.pdf          # Project presentation slides
```

---

## Tools Used

- **Minitab** — Control charts, normality test, process capability analysis
- **Manual Calculations** — All SPC formulas computed by hand with Appendix VI constants
- **Statistical Methods** — X-bar/R charts, P-chart, Fishbone diagram, Pareto analysis, Anderson-Darling test, Cpk
