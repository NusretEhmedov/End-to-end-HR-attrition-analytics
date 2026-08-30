# HR Analytics: Employee Attrition Report

## Overview
A complete HR analytics report profiling employee attrition across all major dimensions, identifying the highest-risk employee segments, and delivering actionable recommendations for a People & Culture team. Built on the IBM HR Analytics Employee Attrition dataset (`WA_Fn-UseC_-HR-Employee-Attrition.csv`, 1,470 employees, 35 columns, no missing values).

## Objective
Attrition sits at 16.1% company-wide, but that single number hides where the real risk is concentrated. This project profiles attrition by department, role, tenure, income, and satisfaction — then combines factors to find the specific employee profiles most likely to leave, so retention effort can be targeted rather than spread thin.

## Method
1. Loaded and profiled the dataset; converted `Attrition` to a binary flag (`Attrition_Flag`).
2. Built a KPI summary table (headcount, income, tenure, satisfaction) split by churned vs. retained.
3. Calculated attrition rate by Department, Job Role, OverTime, Marital Status, and Gender.
4. Segmented employees into tenure groups (0–2 / 3–5 / 6–10 / 11+ years) and income quartiles (Q1–Q4).
5. Built two pivot tables: Department × Job Satisfaction, and Department × Work-Life Balance — both rendered as heatmaps.
6. Ranked all numeric columns by absolute correlation with attrition, top 10.
7. Identified and ranked the top 3 highest-risk employee profiles (2–3 factor combinations).
8. Tested a targeted follow-up question: OverTime + lowest Job Satisfaction + low income.

## Key Findings

**KPIs — churned vs. retained:**
| Metric | Retained | Churned | Overall |
|---|---|---|---|
| Headcount | 1,233 | 237 | 1,470 |
| Avg Monthly Income | $6,833 | $4,787 | $6,503 |
| Avg Years at Company | 7.37 | 5.13 | 7.01 |
| Avg Job Satisfaction (1–4) | 2.78 | 2.47 | 2.73 |
| **Attrition rate** | | | **16.1%** |

**By dimension:** Sales (20.6%) and HR (19.0%) run hotter than R&D (13.8%). OverTime nearly triples risk (30.5% vs. 10.4%). Single employees churn at 25.5% vs. 12.5% married. Sales Representative is the highest-risk role (39.8%).

**Tenure:** 0–2 years = 29.8% attrition, dropping steadily to 8.1% at 11+ years.

**Income:** Q1 (lowest) = 29.3%, falling to ~10% by Q3–Q4.

**Top correlations (all negative — higher value = lower risk):** TotalWorkingYears (-0.171), JobLevel (-0.169), YearsInCurrentRole (-0.161), MonthlyIncome (-0.160), Age (-0.159).

**Top 3 highest-risk profiles:**
| Rank | Profile | n | Attrition Rate |
|---|---|---|---|
| 1 | OverTime=Yes & Single & Income Q1 | 41 | 70.7% |
| 2 | Sales Representative & OverTime=Yes | 24 | 66.7% |
| 3 | OverTime=Yes & Income Q1 | 106 | 58.5% |

**Follow-up profile — OverTime=Yes & JobSatisfaction=1 & low income:** 65.2% attrition (n=23, strict Q1 income) / 46.3% (n=41, below-median income) — both roughly 3–4x baseline, confirming the same compounding pattern.

## Recommendations
1. Audit and cap overtime for Sales Representatives and Laboratory Technicians.
2. Build a structured 0–2 year onboarding and retention program.
3. Review compensation for the lowest income quartile, especially combined with overtime.
4. Create a proactive retention watchlist for the "triple-risk" profiles (overtime + single/low-satisfaction + low income).
5. Prioritize job-satisfaction and work-life-balance interventions in Sales.

## Caveats
- Correlations are linear (Pearson) on ordinal/continuous columns; read directionally, not as precise effect sizes.
- Risk-profile segments with small n (23–41 people) are directional signals, not statistically robust estimates.
- This is a point-in-time snapshot, not a survival model — it correlates who has left historically, not who will leave next.
