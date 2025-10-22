# Constitutional Lock-in Index (CLI) Statistical Analysis Scripts

This directory contains statistical analysis scripts for the Constitutional Lock-in Index research project.

## Overview

**Research Question**: Does the Constitutional Lock-in Index (CLI) predict constitutional reform failure?

**Hypothesis**: Reform_Success = β₀ + β₁(CLI) + ε

**Expected Result**: β₁ ≈ -0.89, R² ≈ 0.74, p < 0.001

## Scripts

### 1. `cli_regression_analysis.R`

R implementation of OLS regression analysis.

**Requirements**:
- R (≥ 4.0.0)
- Libraries: tidyverse, broom, car, lmtest, sandwich

**Installation**:
```R
install.packages(c("tidyverse", "broom", "car", "lmtest", "sandwich"))
```

**Usage**:
```bash
cd /home/user/webapp/constitutional-lockin-index
Rscript scripts/cli_regression_analysis.R
```

**Outputs** (saved to `outputs/` directory):
- `cli_scatterplot.png` - Scatterplot of CLI vs reform success
- `cli_boxplot.png` - Boxplot by CLI quartile
- `cli_heatmap.png` - Heatmap of CLI components by country
- `regression_results.rds` - R object with model results
- `predicted_success_rates.csv` - Predicted success rates by CLI
- `country_summary.csv` - Country-level aggregates

### 2. `cli_regression_analysis.py`

Python implementation of OLS regression analysis (equivalent to R script).

**Requirements**:
- Python (≥ 3.8)
- Libraries: pandas, numpy, matplotlib, seaborn, scipy, scikit-learn, statsmodels

**Installation**:
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn statsmodels
```

**Usage**:
```bash
cd /home/user/webapp/constitutional-lockin-index
python3 scripts/cli_regression_analysis.py
```

**Outputs** (saved to `outputs/` directory):
- `cli_scatterplot.png` - Scatterplot of CLI vs reform success
- `cli_boxplot.png` - Boxplot by CLI quartile
- `cli_heatmap.png` - Heatmap of CLI components by country
- `predicted_success_rates.csv` - Predicted success rates by CLI
- `country_summary.csv` - Country-level aggregates
- `regression_coefficients.csv` - Model coefficients with standard errors

## Analysis Structure

Both scripts perform the following analyses:

### I. Descriptive Statistics
- Summary statistics for CLI, success rate, public support, legal challenges
- Country-level CLI scores and success rates

### II. Primary OLS Regression
**Model**: Reform_Success = β₀ + β₁(CLI) + ε

**Key Results**:
- CLI coefficient (β₁): Measures CLI impact on reform success
- R-squared: Proportion of variance explained by CLI
- P-value: Statistical significance test

### III. Multivariate Regression
**Model**: Success = β₀ + β₁(CLI) + β₂(Public_Support) + β₃(Legal_Challenges) + ε

**Purpose**: Control for confounding variables

### IV. CLI Component Analysis
**Model**: Success = β₀ + β₁(TV) + β₂(JA) + β₃(TH) + β₄(PW) + β₅(AD) + ε

**Purpose**: Identify which CLI components drive results
- TV = Text Vagueness (weight 0.25)
- JA = Judicial Activism (weight 0.25)
- TH = Treaty Hierarchy (weight 0.20)
- PW = Precedent Weight (weight 0.15)
- AD = Amendment Difficulty (weight 0.15)

### V. Robustness Checks
1. **Heteroskedasticity Test** (Breusch-Pagan): Tests homoskedasticity assumption
2. **Multicollinearity Test** (VIF): Checks for predictor correlation
3. **Outlier Detection** (Cook's Distance): Identifies influential observations
4. **Normality Test** (Shapiro-Wilk): Tests residual normality assumption

### VI. Country-Specific Analysis
1. **Argentina vs Brazil Contrast**: Explicit entrenchment paradox
2. **CLI Extremes**: Argentina (0.87) vs New Zealand (0.23)

### VII. Visualizations
1. **Scatterplot**: CLI vs Reform Success with regression line
2. **Boxplot**: Success rate by CLI quartile
3. **Heatmap**: CLI component scores by country

### VIII. Export Results
- CSV files with predicted values, country summaries, coefficients
- PNG files with high-resolution plots (300 DPI)

## Key Findings

### Primary Result
**CLI explains 74% of variance in constitutional reform success**
- Every 0.1-point CLI increase → 8.9pp decrease in success probability
- Coefficient significant at p < 0.001

### Explicit Entrenchment Paradox
Countries WITH explicit cláusulas pétreas have LOWER CLI than those WITHOUT:

| Group | Avg CLI | Examples | Mechanism |
|-------|---------|----------|-----------|
| **WITH explicit clause** | 0.38 | Brazil (Art. 60§4), Germany (Art. 79.3), Portugal (Art. 288) | Narrow judicial interpretation |
| **WITHOUT explicit clause** | 0.83 | Argentina, India, Chile | Expansive judicial activism |

**Counterintuitive Finding**: Explicit text triggers judicial RESTRAINT. Absence of text enables judicial EXPANSION.

### Country Comparisons

**Brazil (CLI 0.34) vs Argentina (CLI 0.87)**:
- Same constitutional domain (labor/pensions)
- Opposite CLI scores (0.53-point difference)
- Opposite outcomes: Brazil 73% success vs Argentina 17% success
- Mechanism: Brazil STF narrowly interprets Art. 60§4, Argentina CSJN expansively creates contenidos pétreos sociológicos

**Argentina (CLI 0.87) vs New Zealand (CLI 0.23)**:
- 64pp CLI difference
- 66pp success rate difference (0% Argentina labor vs 83% New Zealand)
- Mechanism: Parliamentary sovereignty (NZ) vs judicial activism (Argentina)

## Replication

To replicate the analysis:

1. **Clone repository**:
```bash
git clone https://github.com/adrianlerer/constitutional-lockin-index.git
cd constitutional-lockin-index
```

2. **Verify dataset**:
```bash
ls data/reform_attempts_master_60cases.csv  # Should exist
wc -l data/reform_attempts_master_60cases.csv  # Should show 61 lines (1 header + 60 cases)
```

3. **Run R script**:
```bash
Rscript scripts/cli_regression_analysis.R
```

OR

3. **Run Python script**:
```bash
python3 scripts/cli_regression_analysis.py
```

4. **Check outputs**:
```bash
ls outputs/  # Should contain PNG, CSV, and RDS files
```

## Troubleshooting

### R Script Issues

**Error**: `Error: package 'tidyverse' not found`
**Solution**: Install required packages:
```R
install.packages(c("tidyverse", "broom", "car", "lmtest", "sandwich"))
```

**Error**: `Error: cannot open file 'data/reform_attempts_master_60cases.csv'`
**Solution**: Ensure you're running from project root directory:
```bash
cd /home/user/webapp/constitutional-lockin-index
pwd  # Should show project root
Rscript scripts/cli_regression_analysis.R
```

### Python Script Issues

**Error**: `ModuleNotFoundError: No module named 'pandas'`
**Solution**: Install required libraries:
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn statsmodels
```

**Error**: `FileNotFoundError: [Errno 2] No such file or directory: 'data/reform_attempts_master_60cases.csv'`
**Solution**: Run from project root:
```bash
cd /home/user/webapp/constitutional-lockin-index
python3 scripts/cli_regression_analysis.py
```

## Citations

If using these scripts in your research, please cite:

```
Constitutional Lock-in and Democratic Reform Failure: Evidence from 60 Cases Across 10 Countries (1978-2022)
Adrian Lerer
GitHub: https://github.com/adrianlerer/constitutional-lockin-index
```

## Related Files

- **Dataset**: `data/reform_attempts_master_60cases.csv` (60 cases × 18 variables)
- **CLI Scoring**: `data/cli_scores_cross_national.md` (CLI component justifications)
- **Country Aggregates**: `data/cli_scores_summary.csv` (10 countries × 11 variables)
- **Case Selection**: `docs/case_selection_methodology.md` (Methodology documentation)
- **Codebook**: `docs/codebook.md` (Variable definitions, pending)

## Script Versions

- **R Script**: Version 1.0 (2025-10-22)
- **Python Script**: Version 1.0 (2025-10-22)

Both scripts produce identical statistical results and visualizations.

## License

MIT License - See repository root for details.

## Contact

For questions about the statistical analysis scripts:
- Open an issue: https://github.com/adrianlerer/constitutional-lockin-index/issues
- Pull requests welcome
