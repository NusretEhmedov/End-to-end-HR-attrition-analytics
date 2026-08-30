# note.md — HR Analytics: Employee Attrition Executive Summary

## Dataset
IBM HR Analytics Employee Attrition dataset (`WA_Fn-UseC_-HR-Employee-Attrition.csv`) — 1,470 employees, 35 columns, no missing values, no duplicates.

## Overall KPIs
| Metric | Retained (No) | Churned (Yes) | Overall |
|---|---|---|---|
| Headcount | 1,233 | 237 | 1,470 |
| Attrition rate | — | — | **16.1%** |
| Avg Monthly Income | $6,833 | $4,787 | $6,503 |
| Avg Years at Company | 7.37 | 5.13 | 7.01 |
| Avg Job Satisfaction (1–4) | 2.78 | 2.47 | 2.73 |

## Attrition Rate by Dimension
**Department:** Sales 20.6% · HR 19.0% · R&D 13.8%
**OverTime:** Yes 30.5% vs. No 10.4% (2.9x gap)
**Marital Status:** Single 25.5% · Married 12.5% · Divorced 10.1%
**Gender:** Male 17.0% vs. Female 14.8%
**Top/bottom Job Roles:** Sales Representative 39.8% (highest) → Research Director 2.5% (lowest)

## Tenure Segmentation
| Tenure Group | Attrition Rate |
|---|---|
| 0–2 yrs | 29.8% |
| 3–5 yrs | 13.8% |
| 6–10 yrs | 12.3% |
| 11+ yrs | 8.1% |

## Income Quartile Segmentation (Q1 = lowest income)
| Quartile | Attrition Rate |
|---|---|
| Q1 | 29.3% |
| Q2 | 14.2% |
| Q3 | 10.6% |
| Q4 | 10.3% |

## Top 10 Numeric Correlations with Attrition (absolute value)
1. TotalWorkingYears — 0.171
2. JobLevel — 0.169
3. YearsInCurrentRole — 0.161
4. MonthlyIncome — 0.160
5. Age — 0.159
6. YearsWithCurrManager — 0.156
7. StockOptionLevel — 0.137
8. YearsAtCompany — 0.134
9. JobInvolvement — 0.130
10. JobSatisfaction — 0.103

All ten are negative correlations — every one of these factors reduces attrition risk as it increases.

## Top 3 Highest-Risk Employee Profiles
| Rank | Profile | n | Attrition Rate |
|---|---|---|---|
| 1 | OverTime=Yes & Single & Income Q1 (lowest) | 41 | **70.7%** |
| 2 | Sales Representative & OverTime=Yes | 24 | **66.7%** |
| 3 | OverTime=Yes & Income Q1 (lowest) | 106 | **58.5%** |

## Follow-up Risk Profile: OverTime × JobSatisfaction × Low Income
Testing whether `OverTime=Yes` AND `JobSatisfaction=1` (lowest) AND low income also compounds:

| Definition of "low income" | n | Attrition Rate | vs. Baseline (16.1%) |
|---|---|---|---|
| Lowest income quartile (Q1) | 23 | **65.2%** | **4.0x** |
| Below median income | 41 | **46.3%** | **2.9x** |

Confirms the same compounding pattern as the top-3 profiles above — overtime plus financial strain plus a negative signal (satisfaction or marital status) reliably pushes attrition into the 45–70% range.

## 6 Key Findings
1. **Overall attrition is 16.1%** (237 of 1,470 employees), but risk is highly concentrated — several segments run 2–4x the company average.
2. **OverTime is the single strongest behavioral driver**: 30.5% vs. 10.4% for those who don't work overtime — nearly a 3x gap.
3. **New hires are the most fragile population**: 0–2 year tenure churns at 29.8%, over triple the 8.1% rate for 11+-year veterans.
4. **Compounding risk is severe**: overtime + single + lowest income quartile churns at 70.7% — over 4x baseline (n=41).
5. **Sales Representatives are the highest-risk role** at 39.8%, climbing to 66.7% when combined with overtime.
6. **Low satisfaction and poor work-life balance compound within Sales**: JobSatisfaction=1 employees in Sales churn at 26.7%, and WorkLifeBalance=1 employees in Sales churn at 37.5%, both well above the department's already-elevated 20.6% baseline.

## 5 HR Recommendations
1. **Audit and cap overtime for Sales Representatives and Laboratory Technicians** — the highest-leverage single intervention given how these roles combine high baseline attrition with the overtime multiplier.
2. **Build a structured 0–2 year onboarding and retention program** to blunt the steepest part of the attrition curve.
3. **Review compensation for the lowest income quartile, especially combined with overtime** — Q1 earners churn at 29.3% alone and 58.5% with overtime added.
4. **Create a proactive retention watchlist for compounding-risk profiles** (overtime + single/low-satisfaction + Q1 income) — small, well-resourced outreach to these 23–41 person segments could meaningfully move total attrition.
5. **Prioritize job-satisfaction and work-life-balance interventions in Sales** — it carries both the highest department-level attrition and the largest volume of severely at-risk employees.

## Caveats
- Correlations are linear (Pearson) on numeric/ordinal columns; treat as directional signals rather than precise effect sizes.
- Risk-profile segments with n<30 (e.g. n=23–24) are small samples — directional, not statistically robust.
- This is a single point-in-time snapshot, not a survival/tenure-based model — it correlates who has historically left, not who will leave next.
