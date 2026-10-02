# FinGuard Fraud Detection

This repository currently documents the **Exploratory Data Analysis (EDA)** phase for fraud detection using the notebook:

- `notebooks/01_EDA.ipynb`

The notebook analyzes transaction patterns, fraud imbalance, feature behavior, and baseline rule-based fraud flags.

---

## 1) EDA Objective

The EDA notebook is designed to:

- Understand data structure and quality
- Measure fraud class imbalance
- Explore fraud distribution by transaction type, amount, and time
- Detect outliers and feature skewness
- Study correlations with the target (`isFraud`)
- Evaluate the built-in business rule (`isFlaggedFraud`) as a baseline detector

---

## 2) Notebook Workflow (Code Explanation)

### A. Setup and Styling

The first cells import:

- `numpy`, `pandas`
- `matplotlib`, `seaborn`
- `warnings`

Then plotting style is set:

- `plt.style.use('seaborn-v0_8-darkgrid')`
- `sns.set_palette('viridis')`

### B. Environment Checks

The notebook prints:

- Python executable path
- Package versions (`matplotlib`, `pandas`, `numpy`)
- `torch` version and CUDA/GPU availability (if installed)

### C. Data Loading

Dataset is loaded from:

- `./data/raw/finguard-fraud-detection-dataset.csv`

Preview is shown with `df.head()`.

### D. Data Inspection and Quality Checks

The notebook runs:

- `df.info()`
- missing value counts: `df.isnull().sum()`
- numeric summary: `df.describe()`
- categorical summary: `df.describe(include='object')`
- duplicate row checks

It also prints a compact overview table:

- rows, columns
- total missing values
- duplicates
- fraud count and fraud rate

### E. Missing Value Analysis

Two visuals are created:

- Bar chart of missing counts per feature
- Missing-value heatmap (`df.isnull()`)

Saved as:

- `reports/figures/missing_values.png`

### F. Target Distribution (`isFraud`)

The notebook plots:

- Fraud vs non-fraud bar chart (with percentages)
- Pie chart of class split

Saved as:

- `reports/figures/fraud_distribution.png`

### G. Transaction Type Analysis

The notebook examines fraud by `type` using:

- Count plots (with and without `hue='isFraud'`)
- Crosstabs and grouped aggregations
- Stacked bar chart from grouped counts

Saved as:

- `reports/figures/transaction_type.png`
- `reports/figures/transaction_type_distribution.png`

### H. Amount Analysis

For `amount`, it includes:

- Raw histogram
- Log-scale histogram (`np.log1p`)
- Fraud vs non-fraud density-style histograms
- Boxplot and violin plot
- Grouped statistics table (count/mean/median/std/min/max)

Saved as:

- `reports/figures/amount_analysis.png`

### I. Time-Based Analysis

Creates:

- `hour = step % 24`
  Then visualizes:
- total transactions over `step`
- fraud over `step`
- transactions by hour
- fraud by hour

Saved as:

- `reports/figures/time_analysis.png`

### J. Numeric Feature Distribution and Outliers

Generates:

- Histograms for all numeric columns
- Boxplots for major monetary balance features

Saved as:

- `reports/figures/numeric_distributions.png`
- `reports/figures/outlier_boxplots.png`

### K. Correlation Analysis

Builds:

- full numeric correlation matrix heatmap with in-cell values
- horizontal bar chart of correlation with `isFraud`

Saved as:

- `reports/figures/correlation_matrix.png`
- `reports/figures/correlation_with_target.png`

### L. Rule-Based Baseline (`isFlaggedFraud`)

Compares business-rule flags vs actual fraud with:

- flagged/not-flagged bar plot
- confusion-style heatmap using `pd.crosstab(isFraud, isFlaggedFraud)`

Saved as:

- `reports/figures/rule_based_detection.png`

Also prints baseline detection stats:

- total flagged
- actual frauds
- detected frauds
- missed frauds
- false positives
- detection rate

---

## 3) Generated EDA Artifacts

After running the notebook, figures are exported to:

- `reports/figures/missing_values.png`
- `reports/figures/fraud_distribution.png`
- `reports/figures/transaction_type.png`
- `reports/figures/transaction_type_distribution.png`
- `reports/figures/amount_analysis.png`
- `reports/figures/time_analysis.png`
- `reports/figures/numeric_distributions.png`
- `reports/figures/outlier_boxplots.png`
- `reports/figures/correlation_matrix.png`
- `reports/figures/correlation_with_target.png`
- `reports/figures/rule_based_detection.png`

---

## 3.1) Quick Figure Preview

<table>
  <tr>
    <td align="center">
      <img src="reports/figures/missing_values.png" width="260"><br>
      <sub>Missing Values</sub>
    </td>
    <td align="center">
      <img src="reports/figures/fraud_distribution.png" width="260"><br>
      <sub>Fraud Distribution</sub>
    </td>
    <td align="center">
      <img src="reports/figures/transaction_type.png" width="260"><br>
      <sub>Transaction Type</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="reports/figures/transaction_type_distribution.png" width="260"><br>
      <sub>Transaction Type Distribution</sub>
    </td>
    <td align="center">
      <img src="reports/figures/amount_analysis.png" width="260"><br>
      <sub>Amount Analysis</sub>
    </td>
    <td align="center">
      <img src="reports/figures/time_analysis.png" width="260"><br>
      <sub>Time Analysis</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="reports/figures/numeric_distributions.png" width="260"><br>
      <sub>Numeric Distributions</sub>
    </td>
    <td align="center">
      <img src="reports/figures/outlier_boxplots.png" width="260"><br>
      <sub>Outlier Boxplots</sub>
    </td>
    <td align="center">
      <img src="reports/figures/correlation_matrix.png" width="260"><br>
      <sub>Correlation Matrix</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="reports/figures/correlation_with_target.png" width="260"><br>
      <sub>Correlation with Target</sub>
    </td>
    <td align="center">
      <img src="reports/figures/rule_based_detection.png" width="260"><br>
      <sub>Rule-Based Detection</sub>
    </td>
    <td></td>
  </tr>
</table>

---

## 4) How to Run (VS Code / Windows)

1. Open project in VS Code.
2. Ensure dependencies are installed:
   - `pandas`, `numpy`, `matplotlib`, `seaborn` (and optional `torch`)
3. Confirm dataset exists at:
   - `data\raw\finguard-fraud-detection-dataset.csv`
4. Run notebook:
   - `notebooks\01_EDA.ipynb`
5. Check outputs in:
   - `reports\figures\`

---

## 5) EDA Summary

From this notebook:

- Fraud is highly imbalanced
- Transaction type has strong fraud pattern differences
- Amount is skewed; log transform is useful
- Time-derived features from `step` are informative
- Some numeric features are strongly correlated
- `isFlaggedFraud` is a useful but limited rule-based baseline

---

## 6) Note

In the final print-summary cell, `fraud_flagged` is referenced but not defined in earlier cells.  
Use the crosstab matrix variable (for example `cm`) or define `fraud_flagged` before that section to avoid runtime errors.
