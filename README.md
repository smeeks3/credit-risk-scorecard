# Credit Risk Scorecard

A full credit scoring pipeline built in Python for a simulated retail bank, developed for evaluating consumer credit applications.

## Overview

This project builds a logistic regression-based scorecard scaled using PDO/odds calibration — anchored at **500 points (20:1 odds)** with **50 points per doubling of odds**. The full business write-up is available in `reports/Homework1_FA.pdf`.

## Methodology

- **Oversampling correction** — the development sample is balanced (1,500 good / 1,500 bad) against a true population bad rate of 3.23%; good customers are upweighted (~30x) to restore correct population proportions
- **Variable selection** — features binned via Weight of Evidence (WoE) using `optbinning`; variables with IV < 0.1 excluded. Top predictors: Age (IV=0.39), Income (IV=0.27), Cards (IV=0.19), Time at Job (IV=0.18)
- **Reject inference** — hard cutoff method applied to correct for accept bias; rejected applicants scored by the initial model, labeled bad if predicted probability of default > 3%, then combined with accepted customers for final model training
- **Cutoff analysis** — score cutoffs evaluated across three business objectives using revenue of $2,000 per good customer and loss of $52,000 per bad customer

## Cutoff Recommendations

| Objective | Cutoff Score | Acceptance Rate | Default Rate | Est. Profit |
|---|---|---|---|---|
| Maximize Profit | 483 | 45% | 1.9% | $8.1M |
| Maintain 75% Acceptance | 342 | 75% | 7.4% | -$27.9M |
| Maintain 3.23% Default Rate | 428 | 58% | 3.3% | $2.6M |

## Repository Structure

```
retail-credit-scorecard/
├── Credit_Scorecard_Cutoff.ipynb
├── Credit_Scorecard_Fuzzy_WIP.ipynb
├── data/
│   ├── accepted_customers.csv
│   ├── rejected_customers.csv
│   └── weighting_rejects.xlsx
└── reports/
    ├── Final_Report.docx
    └── Scorecard_RFP.pdf
```

## Getting Started

```bash
pip install pandas numpy scikit-learn optbinning matplotlib
jupyter notebook Credit_Scorecard_Notebook.ipynb
```

## Tools & Libraries

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-logistic%20regression-orange)
![optbinning](https://img.shields.io/badge/optbinning-WoE%20%7C%20Scorecard-green)<img width="605" height="1022" alt="image" src="https://github.com/user-attachments/assets/cfb82ee2-ca48-490f-b7b0-5de4f38a9a60" />
