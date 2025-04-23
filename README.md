# Portfolio Stress Testing & Industry Risk Monitoring

## Overview

This project demonstrates a complete workflow for credit portfolio stress testing and industry risk monitoring using real-world Lending Club loan data. The goal is to estimate the impact of adverse economic scenarios on expected credit loss (ECL) and identify segments (by grade and purpose) most vulnerable to stress.

## Dataset

- **Source:** Lending Club (sampled 5,000 rows)
- **File:** PROJ-2-DATA-version-1.xlsx
- **Key Fields Used:**
  - `loan_amnt`: Loan amount
  - `int_rate`: Interest rate
  - `grade`, `sub_grade`: Credit grade assigned to loan
  - `purpose`: Loan purpose (e.g., debt_consolidation, small_business)
  - `annual_inc`: Borrower's annual income
  - `dti`: Debt-to-income ratio
  - `fico_range_low`, `fico_range_high`: FICO score range
  - `loan_status`: Current loan status
  - `out_prncp`: Outstanding principal
  - *(Other features as needed for analysis)*

## Workflow

### 1. Data Cleaning & Preparation
- Removed unnecessary columns (`url`, `desc`, `title`, `zip_code`, etc.).
- Filtered out rows with missing or zero values in critical fields (`loan_amnt`, `annual_inc`, `fico_range_low`, `dti`).
- Standardized categorical fields (e.g., `grade`, `purpose`).

### 2. Exploratory Data Analysis (EDA)
- Summarized portfolio by grade, purpose, and loan status.
- Calculated default rates by segment.
- Visualized distributions with bar charts and histograms.

### 3. Stress Scenario Definition
- Economic downturn scenario: Increased DTI by 10%, decreased FICO by 30 points, increased probability of default (PD) by 20% for grades B-G.
- Sector-specific scenario: Increased PD by 30% for loans with `purpose` = "small_business" or "medical".

### 4. Stress Testing & ECL Calculation
- Assigned base PDs by grade (A: 2%, B: 4%, C: 6%, D: 10%, E: 15%, F: 20%, G: 25%).
- Calculated `stressed_pd` for each loan based on scenario multipliers.
- Assumed Loss Given Default (LGD) of 50% and used `out_prncp` as Exposure at Default (EAD).
- Computed `stressed_ecl` = `stressed_pd` × `LGD` × `EAD`.

### 5. Industry/Sector Risk Monitoring
- Aggregated and visualized ECL by grade and purpose.
- Created a heatmap to highlight risk concentrations.

### 6. Dashboard & Reporting
- Developed an Excel dashboard with:
  - KPIs: Total ECL, % increase under stress, top risk segments
  - Heatmap: Stressed ECL by grade and purpose
  - Bar charts: ECL by segment
  - Slicers for interactive exploration

## Key Insights

- The heatmap highlights that certain grades and purposes (e.g., lower grades, small business loans) are more vulnerable under stress.
- Stress scenarios can significantly increase expected losses in specific portfolio segments.
- Portfolio managers can use these insights to adjust risk appetite and capital allocation.

## Visualization Notes

- **Darker red = higher expected credit loss under stress scenario.**
- All charts and tables are based on cleaned, filtered data.

## How to Use

1. Open `PROJ-2-DATA-version-1.xlsx` in Excel.
2. Review the `Raw_Data`, `Stress_Testing`, and `Dashboard` sheets.
3. Use slicers and filters to explore risk by segment and scenario.
4. Refer to this README for methodology and interpretation.

## Future Work

- Extend analysis using R or IBM SPSS for advanced modeling and scenario simulation.
- Incorporate additional macroeconomic variables for multi-factor stress testing.
- Automate reporting and dashboard updates.

## File Structure

portfolio-stress-testing/
│
├── PROJ-2-DATA-version-1.xlsx
├── README.md

## License

MIT License

---

*For questions or suggestions, please open an issue or contact the project maintainer.*
