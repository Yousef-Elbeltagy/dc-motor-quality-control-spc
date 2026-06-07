# DC Motor Manufacturing — Quality Control Using SPC

A complete Statistical Process Control (SPC) study on a DC motor manufacturing process. The project targets **winding resistance (WR)** as the critical quality characteristic — detecting process instability, tracing it to root causes, applying corrective actions, and finally proving the process is stable and highly capable using both manual calculations and Minitab.

> **Course:** Quality Control  
> **Institution:** Helwan National University — Faculty of Engineering, Robotics & Mechatronics Engineering  
> **Supervisor:** Prof. Nariman &nbsp;|&nbsp; **TA:** Asmaa AL-Robi  
> **Team:** Yousef Ahmed Elbeltagy · Mohamad Sherif Shabrawy · Mohamed Ali Ismail · Verina Elkess · Yousef Wail Ismail · Amr Sherif Maher  
> **Academic Year:** 2025–2026

---

## The Problem

A DC motor manufacturing line produces **DCM-750 motors**. For each motor, winding resistance must stay between **4.20 Ω (LSL)** and **4.80 Ω (USL)**. Resistance outside this range causes poor winding quality, motor overheating, or internal electrical defects.

**30 production batches** were analyzed, with **5 motors inspected per batch** (150 motors total). The goal: determine whether the process is statistically stable, find what is causing failures, implement targeted fixes, and validate that those fixes actually worked.

| Parameter | Value |
|---|---|
| Quality Characteristic | Winding Resistance (WR) in ohms (Ω) |
| Lower Specification Limit (LSL) | 4.20 Ω |
| Upper Specification Limit (USL) | 4.80 Ω |
| Batches Analyzed | 30 |
| Motors Inspected per Batch (n) | 5 |
| Total Motors Inspected | 150 |

The analysis was performed in two parallel tracks — **manual calculations** using standard SPC formulas and table constants (A₂=0.577, D₃=0, D₄=2.114, d₂=2.326 from Appendix VI), and **Minitab** for validation and visualization.

---

## Phase 1 — Detecting the Problem

### X-bar and R Control Charts

The X-bar chart monitors the **process mean** (average winding resistance per batch), while the R chart monitors **within-batch variation** (spread between the highest and lowest reading in each batch of 5). Together, they tell you whether the process is producing consistent results over time.

Using the grand mean X̄̄ = 4.504 Ω and average range R̄ = 0.154 Ω, the control limits are:

- **X-bar:** UCL = 4.606 Ω, CL = 4.504 Ω, LCL = 4.428 Ω
- **R chart:** UCL = 0.326, CL = 0.154, LCL = 0 (D₃ = 0 for n = 5)

![Minitab Xbar-R Chart](docs/images/minitab_xbar_r_initial.png)

The Minitab chart immediately reveals three out-of-control situations:

| Chart | Out-of-Control Batch | Finding |
|---|---|---|
| **R Chart** | **B16** — range = 0.380 > UCL = 0.326 | Abnormal within-batch variation — the 5 motors in this batch had highly inconsistent resistance values, pointing to an unstable production condition during that run |
| **X-bar Chart** | **B13** — mean = 4.720 Ω | Process mean shifted upward — all motors in this batch were wound too tightly, a systematic shift not caused by random chance |
| **X-bar Chart** | **B19** — mean = 4.650 Ω | Same pattern — process mean drifted out of control again |

### P-Chart — Proportion Defective Across All Batches

While the X-bar/R charts detect shifts in resistance *values*, the p-chart tracks the **defect rate** directly — what fraction of motors in each batch fell outside the 4.20–4.80 Ω specification.

With p̄ = 10.0% (15 defectives out of 150 motors), the p-chart limits are: UCL = 0.5025, LCL = 0 (negative lower limit set to zero).

![Minitab P-Chart Initial](docs/images/minitab_p_chart_initial.png)

**Batches B14 and B19** both spike to p = 0.60 — meaning **3 out of 5 motors** in each of those batches were defective. This directly confirms and extends the instability seen in the X-bar chart: B19 appears out of control in both charts, while B14 shows up here as a defect hotspot even though its batch mean was technically within limits.

**Summary:** The process is not in statistical control. Batches B13, B14, B16, and B19 all show abnormal behavior — through variation, mean shifts, or defect spikes. The process needs diagnosis before any fix can be targeted correctly.

---

## Phase 2 — Finding the Root Causes

### Fishbone (Ishikawa) Diagram

Rather than guessing at causes, a structured cause-and-effect analysis was built targeting the four problem batches using the **6M framework** — Machine, Method, Material, Measurement, Environment, and Mother Nature.

![Fishbone Diagram](docs/images/fishbone_diagram.png)

| Category | Key Causes Identified |
|---|---|
| **Machine** | Cooling system failure, M2 bearing wear, no preventive maintenance schedule |
| **Environment** | High ambient workshop temperature (38°C during B11–B13), inadequate ventilation, no thermal barriers |
| **Material** | Wire resistance variation between suppliers, insulation coating QC failures, batch-to-batch supply chain inconsistency |
| **Measurement** | No inline WR sensors, uncalibrated measurement equipment, manual data recording errors |
| **Man / Method** | Shift handover gaps, no escalation protocol for out-of-spec readings, operator fatigue, inadequate training |
| **Mother Nature** | Humidity fluctuations, seasonal temperature peaks coinciding with batches B13 and B19 |

The fishbone gives many possible causes. The next step is to find out which ones are actually responsible for *most* of the defects.

### Pareto Chart — Prioritizing the Vital Few

The Pareto chart ranks all identified causes by frequency. The "80/20 rule" of quality control says a small number of causes typically drive most defects — identifying these vital few is what makes the corrective action targeted and effective.

![Minitab Pareto Chart](docs/images/minitab_pareto.jpeg)

| Cause | Count | Frequency | Cumulative % |
|---|---|---|---|
| **Thermal Issues** | 5 | 45.5% | 45.5% |
| **Material Defects** | 3 | 27.3% | **72.7%** |
| Machine Fault | 1 | 9.1% | 81.8% |
| Operator / Method | 1 | 9.1% | 90.9% |
| Measurement | 1 | 9.1% | 100.0% |

> **Thermal Issues + Material Defects = 72.7% of all defects.** These two causes together cross the 80/20 threshold, making them the clear targets for corrective action. Fixing everything else first would address less than 30% of the problem.

---

## Phase 3 — Fixing the Process

Based on the Fishbone and Pareto findings, corrective actions were focused on the two dominant cause categories:

**Thermal Control (45.5% of defects)**
- Installation of improved cooling systems to reduce motor overheating
- Enhancement of workshop ventilation to stabilize ambient temperature
- Implementation of real-time temperature monitoring during production

**Material Quality (27.3% of defects)**
- Standardization of insulation coating processes across production runs
- Tightened incoming inspection of raw materials (wire and insulation)
- Supplier quality verification to reduce batch-to-batch resistance variation

**Supporting Actions**
- Preventive maintenance schedules and worn component replacement (M2 bearings)
- Instrument calibration and introduction of inline WR monitoring
- Operator SPC training, documented escalation procedures, improved shift handover

---

## Phase 4 — Verifying the Fix

Process improvement in SPC is **iterative** — you fix one layer of instability, re-examine the charts, then fix the next layer. This is exactly what was done.

### Step 1 — Revised Control Charts (Removing B16)

Batch B16 caused the R-chart violation — excessive within-batch variation. This batch was removed and the control limits were recalculated to assess the remaining process stability.

![Revised Xbar-R Minitab](docs/images/revised_xbar_r_minitab.png)

**R Chart result:** All 29 remaining batches now fall within the revised UCL = 0.309 — **within-batch variation is now stable** ✓

**X-bar Chart result:** Batches B13 and B19 still exceed the revised control limits — the process *mean* still drifts in those batches, meaning the thermal and material root causes are still active.

This is the expected iterative pattern: stabilizing the R chart was step one. The mean shifts require the deeper corrective actions to take full effect.

### Step 2 — Final X-bar Chart (Removing B13, B16, and B19)

After the thermal and material corrective actions were fully implemented, B13 and B19 were confirmed to be caused by identifiable assignable causes and were excluded. The X-bar chart was redrawn using only the remaining 27 batches.

Final limits: **UCL = 4.599 Ω, X̄̄ = 4.504 Ω, LCL = 4.421 Ω**

![Final Xbar Minitab](docs/images/final_xbar_minitab.png)

**All 27 remaining batches lie within the control limits.** The process mean is stable and well-centered within the specification window. Combined with the already-stable R chart, the process is now fully in statistical control.

### Step 3 — Revised P-Chart (Defect Rate After Improvement)

With the four problem batches (B13, B14, B16, B19) removed, the defect rate was recalculated on the remaining 26 batches to quantify the improvement in product quality.

Revised p̄ = 4.62% (down from 10.0%) → new limits: **UCL = 0.3277, LCL = 0**

![Revised P-Chart Minitab](docs/images/revised_p_chart_minitab.png)

| Metric | Before Improvement | After Improvement |
|---|---|---|
| Average Defect Rate (p̄) | 10.0% | **4.62%** |
| UCL | 0.5025 | 0.3277 |
| Out-of-Control Batches | B14, B19 | **None** |

Defect rate dropped by **54%**. Every one of the 26 remaining batches now falls within the revised control limits — the quality improvement is real and measurable.

---

## Phase 5 — Validating Process Capability

With the process confirmed stable, the final step is to measure **how capable** it is — not just whether it's in control, but whether it reliably produces motors within the 4.20–4.80 Ω specification.

### Normality Test (Anderson-Darling)

Process capability analysis (Cpk) assumes the data follows a normal distribution. Before calculating Cpk, this assumption must be verified. A manual frequency histogram was constructed first, showing an approximately symmetric bell-shaped distribution. Minitab's Anderson-Darling test then confirmed it statistically.

![Normality AD Test](docs/images/normality_ad_test.png)

| Test Result | Value |
|---|---|
| Anderson-Darling Statistic | 0.511 |
| **p-value** | **0.178** |
| Decision threshold | 0.05 |
| **Conclusion** | **p > 0.05 → Data is normally distributed — Cpk analysis is valid** ✓ |

The data points closely follow the normal reference line in the probability plot, and the p-value of 0.178 comfortably exceeds 0.05, confirming normality.

### Process Capability Report (Cpk)

Cpk measures how many standard deviations fit between the process mean and the nearest specification limit. A Cpk > 1.33 is the industry standard for a "highly capable" process.

With process mean μ = 4.503 Ω and standard deviation σ = R̄/d₂ = 0.154/2.326 = 0.0662 Ω:

![Minitab Capability Report](docs/images/capability_report.png)

| Parameter | Value |
|---|---|
| LSL | 4.20 Ω |
| USL | 4.80 Ω |
| Process Mean | 4.503 Ω |
| Process Std Dev (σ) | 0.0628 Ω (Minitab) |
| **Cpk — Manual Calculation** | **1.57** |
| **Cpk — Minitab** | **1.69** |

> Both Cpk values exceed 1.33 → **HIGHLY CAPABLE PROCESS** ✓  
> The process mean sits nearly centered between LSL and USL, with more than 5 standard deviations of margin on both sides. Expected defect rate is near zero (PPM ≈ 0.32).

### Run Chart — Stability Over Time

The run chart visualizes all 27 subgroup means plotted in time order, without control limits. Its purpose is to detect trends, level shifts, or cyclical patterns that might not be visible in a snapshot analysis.

![Minitab Run Chart](docs/images/run_chart_minitab.png)

The subgroup means fluctuate randomly around the process mean with no systematic upward or downward trends, no prolonged runs above or below the centerline, and no cyclic patterns. The process is stable not just statistically — it is stable **over time**, which is the ultimate proof that the corrective actions had a lasting effect.

---

## Results Summary — Before vs. After

| Metric | Before Improvement | After Improvement |
|---|---|---|
| R Chart | **B16 out of control** (range = 0.380 > UCL) | All points within revised UCL = 0.309 ✓ |
| X-bar Chart | **B13 & B19 out of control** (mean shifts) | All 27 batches within limits (UCL=4.599, LCL=4.421) ✓ |
| P-Chart | **B14 & B19** at p = 0.60 (60% defective) | All 26 batches within revised limits ✓ |
| Average Defect Rate | **10.0%** | **4.62% (−54%)** ✓ |
| Statistical Control | NOT in control | FULLY in control ✓ |
| Data Normality | — | Confirmed — Anderson-Darling p = 0.178 ✓ |
| Process Capability Cpk | Unreliable (unstable process) | **1.57 (manual) / 1.69 (Minitab) — Highly Capable** ✓ |
| Long-term Stability | — | Confirmed — Run chart shows no trends or shifts ✓ |

---

## Tools & Methods

| Tool / Method | Purpose in This Study |
|---|---|
| **X-bar & R Charts** | Monitor process mean and within-batch variation simultaneously |
| **P-Chart** | Track defect rate (proportion of out-of-spec motors) per batch |
| **Fishbone (Ishikawa) Diagram** | Structured root cause analysis across 6M categories |
| **Pareto Chart** | Rank causes by frequency to identify the vital few driving most defects |
| **Revised Control Charts** | Verify stability improvement after removing assignable-cause batches |
| **Anderson-Darling Normality Test** | Validate normal distribution assumption before Cpk analysis |
| **Process Capability (Cpk)** | Quantify how reliably the process meets specification limits |
| **Run Chart** | Confirm process stability chronologically — detect trends and shifts over time |
| **Minitab** | All chart generation, normality test, and capability report (parallel to manual) |
| **Manual Calculations** | Full derivation of all limits using Appendix VI constants (A₂=0.577, D₃=0, D₄=2.114, d₂=2.326) |

---

## Repository Structure

```
dc-motor-quality-control-spc/
├── data/
│   └── DCMotor_QC_Dataset.xlsx          # Raw winding resistance data (30 batches × 5 motors)
└── docs/
    ├── QC_Report.pdf                    # Full project report
    └── images/
        ├── minitab_xbar_r_initial.png      # Phase 1 — Initial Xbar-R: B13, B16, B19 out of control
        ├── minitab_p_chart_initial.png     # Phase 1 — Initial P-chart: B14, B19 at 60% defective
        ├── fishbone_diagram.png            # Phase 2 — Root cause analysis (6M Ishikawa)
        ├── minitab_pareto.jpeg             # Phase 2 — Pareto: thermal 45.5%, material 27.3%
        ├── revised_xbar_r_minitab.png      # Phase 4 Step 1 — Revised charts: R stable, B13/B19 still out
        ├── final_xbar_minitab.png          # Phase 4 Step 2 — Final Xbar: all 27 batches in control
        ├── revised_p_chart_minitab.png     # Phase 4 Step 3 — Revised P-chart: defect rate 4.62%
        ├── normality_ad_test.png           # Phase 5 — Anderson-Darling: p=0.178, normality confirmed
        ├── capability_report.png           # Phase 5 — Minitab Cpk = 1.69 (highly capable)
        └── run_chart_minitab.png           # Phase 5 — Run chart: no trends or patterns over time
```
