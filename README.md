# 📞 Outbound Call Effectiveness Analysis — Healthcare Screening Compliance

> **DataCamp Data Analyst Professional Certification — Practical Exam**  
> Analysis of a nursing team's outbound call campaign to evaluate its impact on patient screening compliance.

---

## 📌 Project Overview

**Universal Healthy Humans Company (UHHC)** is a partially government-funded healthcare company that runs an outbound call center staffed by nurses. Their goal is to improve compliance rates for five preventive health screenings among patients over 50. This project evaluates whether their phone outreach strategy is actually working — and where to focus efforts going forward.

**Business questions answered:**
- How many patients were reached successfully?
- Does screening load (number of required screenings) affect compliance?
- Are contacted patients more likely to complete their screenings than those not reached?
- How should the team optimize their outbound calls to maximize compliance?

---

## 🗂️ Dataset

**File:** `DA_outbound_call_nursing_team.csv` — 1,988 rows, 6 columns

| Column | Type | Description |
|---|---|---|
| `patient_id` | Numeric (len 22) | Unique patient identifier |
| `screening_type` | String | One of: BCS, COL, EED, CBP, OMW |
| `screening_completed_ind` | Boolean | 0 = not completed, 1 = completed, null = not eligible |
| `screening_date` | Date (YYYY-MM-DD) | Date screening was completed |
| `latest_call_date` | Date (YYYY-MM-DD) | Date of last outbound call attempt |
| `reached_ind` | Boolean | 0 = not reached, 1 = reached, null = not called |

**Screening types:**

| Code | Screening |
|---|---|
| BCS | Bowel Cancer Screening |
| COL | Colorectal Cancer |
| CBP | Controlling High Blood Pressure |
| OMW | Osteoporosis Management in Women |
| EED | Early Elective Delivery Prevention |

---

## 🛠️ Tools & Libraries

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![SQL](https://img.shields.io/badge/SQL-DuckDB-orange)
![pandas](https://img.shields.io/badge/pandas-2.x-150458?logo=pandas)
![seaborn](https://img.shields.io/badge/seaborn-visualization-4C72B0)
![matplotlib](https://img.shields.io/badge/matplotlib-visualization-11557c)

---

## 🧹 Data Validation & Cleaning

| Column | Issue Found | Action Taken |
|---|---|---|
| `screening_type` | 1 record with invalid value `'A1C'` (not in scope) | Record removed |
| `screening_completed_ind` | 5 records with value `'s'` (invalid boolean) | Records excluded |
| `screening_completed_ind` | 1 record entered as integer `1` instead of float `1.0` | Standardized to `1.0` |
| `reached_ind` | 1 record with value `'1 and reached'` (text, not boolean) | Standardized to `1.0` — intent was clear |
| `screening_date` / `latest_call_date` | Temporal consistency check | Confirmed all screening dates occurred *after* call dates — no violations found |

**Cleaning in Python:**
```python
df['reached_ind'] = df['reached_ind'].replace({'1 and reached': 1.0})
df = df[df['screening_type'] != 'A1C']
df = df[df['screening_completed_ind'] != 's']
```

---

## 📊 Key Findings

### 1 — Outreach Success Rate
~**72% of patients** who received a call attempt were successfully reached.

![Patients reached successfully](images/patients_reached_successfully.png)

### 2 — Screening Load vs. Compliance
Patients with **1 assigned screening had 100% completion**. Beyond that, no meaningful correlation between screening volume and compliance was found.

![Completion rate by screening load](images/image2_completion_rate_by_screening_load.png)

### 3 — Impact of Calls on Compliance ⭐
The **"Never Called" group showed the highest compliance** — outperforming both contacted and failed-attempt groups by a meaningful margin.

![Screening completion rate by call status](images/image3_screening_completion_rate_by_call_status.png)

### 4 — Impact by Screening Type
![Impact of outreach by screening type](images/image4_impact_of_outreach_by_screening_type.png)

- **OMW (Osteoporosis):** The **only screening where calls positively drive compliance.**
- **EED (Early Elective Delivery):** Non-contacted patients showed *higher* compliance...

---

## 📐 Business KPI

**Recommended metric: Screening Compliance Rate by Contact Channel, segmented by screening type**

| Screening | Call Impact | Recommended Action |
|---|---|---|
| OMW | Positive ✅ | Prioritize — focus nursing resources here |
| EED | Negative ❌ | Replace calls with SMS/email |
| CBP / COL / BCS | Negligible ➡️ | Test digital alternatives |

**Current baseline:** ~72% contact success rate. Monitor monthly compliance per screening type comparing contacted vs. non-contacted cohorts.

---

## ✅ Recommendations

1. **Prioritize OMW outreach** — highest measurable ROI for nursing team calls
2. **Redirect EED resources** — switch to digital channels (SMS, email) for this demographic
3. **Diversify contact channels** for CBP, COL, BCS — lower cost, similar results
4. **Investigate the Never Called group** — understanding their self-service pathway could unlock a scalable model

---

## 📁 Repository Structure

```
outbound-nursing-call-analysis/
├── README.md
├── notebook.ipynb
├── data/
│   └── DA_outbound_call_nursing_team.csv
└── images/
    ├── patients_reached_successfully.png
    ├── completion_rate_by_screening_load.png
    ├── screening_completion_rate_by_call_status.png
    └── impact_of_outreach_by_screening_type.png
```

---

## 👤 Author

**Leonardo Farfán** · Associate Data Analyst · DataCamp Certified  
[LinkedIn](https://linkedin.com/in/leofarfan) · leofarfan2604@gmail.com

*DataCamp Data Analyst Professional Certification — Practical Exam*
