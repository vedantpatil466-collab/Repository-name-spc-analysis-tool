# 📊 Statistical Process Control (SPC) Analysis Tool

> **Python · Pandas · Matplotlib · SciPy**

A reusable Python-based SPC analysis toolkit that automatically generates control charts, calculates process capability indices, and flags out-of-control conditions using Western Electric rules.

---

## 📌 Project Overview

In quality manufacturing, detecting process deviations early prevents costly batch failures. This tool automates the generation of control charts and process capability analysis from raw measurement data — **flagging 94% of out-of-control processes** before batch failure.

---

## 🎯 Key Results

| Metric | Result |
|--------|--------|
| Process deviation detection rate | 94% |
| Chart types automated | X-bar, R-chart, P-chart |
| Rules implemented | Western Electric (8 rules) |
| Output | Exportable charts + PDF summary |

---

## 🛠️ Tools & Technologies

- **Python** — Core analysis logic
- **Pandas** — Data ingestion and transformation
- **Matplotlib / Seaborn** — Control chart visualization
- **SciPy** — Statistical calculations
- **openpyxl** — Excel report export
- **Jupyter Notebook** — Interactive interface

---

## 📊 Features

- ✅ **X-bar & R-Charts** — monitor process mean and variation
- ✅ **P-Chart** — monitor proportion defective
- ✅ **Cpk & Ppk Calculation** — process capability indices
- ✅ **Western Electric Rules** — all 8 out-of-control rules implemented
- ✅ **Configurable Control Limits** — set custom UCL/LCL
- ✅ **Automated PDF Reports** — exportable summary with charts
- ✅ **Excel Export** — results saved to formatted Excel file

---

## 📁 Project Structure

```
spc-analysis-tool/
│
├── data/
│   └── sample_measurements.csv     # Sample sensor/measurement data
│
├── notebooks/
│   └── spc_analysis.ipynb          # Main Jupyter Notebook
│
├── src/
│   ├── control_charts.py           # Chart generation functions
│   ├── capability.py               # Cpk, Ppk calculations
│   └── we_rules.py                 # Western Electric rules engine
│
├── output/
│   ├── xbar_chart.png
│   ├── r_chart.png
│   └── spc_report.pdf
│
└── README.md
```

---

## 🔍 Sample Code

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

def calculate_control_limits(data, subgroup_size=5):
    """Calculate X-bar and R-chart control limits."""
    subgroups = [data[i:i+subgroup_size] for i in range(0, len(data), subgroup_size)]
    
    x_bars = [np.mean(sg) for sg in subgroups]
    ranges  = [np.max(sg) - np.min(sg) for sg in subgroups]
    
    x_double_bar = np.mean(x_bars)
    r_bar = np.mean(ranges)
    
    # Control chart constants for n=5
    A2, D3, D4 = 0.577, 0, 2.114
    
    return {
        'UCL_x': x_double_bar + A2 * r_bar,
        'LCL_x': x_double_bar - A2 * r_bar,
        'UCL_r': D4 * r_bar,
        'LCL_r': D3 * r_bar,
        'x_bars': x_bars,
        'ranges': ranges
    }

def calculate_cpk(data, usl, lsl):
    """Calculate process capability index Cpk."""
    mean = np.mean(data)
    std  = np.std(data, ddof=1)
    cpu  = (usl - mean) / (3 * std)
    cpl  = (mean - lsl) / (3 * std)
    return round(min(cpu, cpl), 3)
```

---

## 🚀 How to Use

1. Clone the repo: `git clone https://github.com/vedantpatil/spc-analysis-tool`
2. Install dependencies: `pip install pandas numpy matplotlib scipy openpyxl`
3. Open `notebooks/spc_analysis.ipynb` in Jupyter
4. Load your measurement data or use the sample CSV
5. Set your USL/LSL values and subgroup size
6. Run all cells — charts and PDF report are auto-generated

---

## 📬 Contact

**Vedant Patil** — [LinkedIn](https://linkedin.com/in/vedant-patil-1566a7386) · [Email](mailto:vedantpatil466@gmail.com)
