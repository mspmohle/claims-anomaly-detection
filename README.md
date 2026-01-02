Claims Anomaly Detection

Data Analytics Internship – Highmark Health (Fraud, Waste & Abuse Identification)
Author: Michael S. Mohle
Repository: claims-anomaly-detection

1. Research Question

How can healthcare claims data be analyzed to detect anomalous billing patterns that may indicate fraud, waste, or abuse (FWA)?
Specifically, can statistical and machine-learning anomaly-detection methods (such as Isolation Forests) accurately flag a small subset of suspicious claims for further review?

2. Background Research

Healthcare systems face persistent financial losses due to improper or fraudulent billing.
Traditional rule-based fraud detection often fails to identify subtle, emerging, or complex behaviors among providers.
Recent studies demonstrate that unsupervised learning methods—particularly Isolation Forests and Autoencoders—can uncover outliers in high-dimensional claims data without labeled examples.

This project simulates that analytical workflow, using synthetic data modeled after claims, providers, and members, similar in structure to the datasets used in payor fraud analytics environments.

3. Hypothesis

If anomaly-detection algorithms are applied to standardized healthcare claim features (e.g., claim cost, frequency, and diagnosis score),
then a small but meaningful percentage (~3–7 %) of claims will emerge as statistical outliers — potentially representing high-risk or fraudulent patterns.

4. Experiment / Methodology
4.1 Data Generation

A synthetic dataset of 3,000 claims was generated to mimic real-world healthcare billing data.

Key variables:

claim_id, provider_id, member_id, procedure_code

claim_cost, diagnosis_score, claim_frequency

Dataset saved under: data/raw/synthetic_claims.csv

4.2 Exploratory Data Analysis (EDA)

Visualized cost distributions and identified skew toward a minority of high-value claims.

Plotted provider-level averages to detect cost variance across provider IDs.

Stored output visuals under /figures/.

4.3 Anomaly Detection Model

Applied Isolation Forest using scikit-learn.

Model trained on normalized features (claim_cost, diagnosis_score, claim_frequency).

Outliers defined as claims with anomaly score < 0 (typically the lowest 5 % quantile).

Evaluation focused on anomaly rate, distribution, and high-cost concentration among outliers.

4.4 Validation & Analysis

Computed top anomalous providers and compared their mean claim costs to overall averages.

Verified that anomaly clusters corresponded to significant deviations (> 3σ from mean).

5. Results & Findings
Metric	Result
Total claims analyzed	3,000
Anomalous claims detected	150 (≈ 5.0 %)
Top provider mean anomaly cost	$8,977
Typical provider mean cost	$1,450
Key indicators of anomaly	High claim frequency, elevated diagnosis scores

Summary:

About 5 % of claims exhibited highly unusual cost patterns.

The top decile of anomalous providers showed costs 5–6× higher than normal peers.

This supports the hypothesis that unsupervised models can isolate high-risk claims even without labeled fraud data.
6. Conclusion

The experiment demonstrates that Isolation Forest–based anomaly detection provides a viable approach to highlight suspicious claim behavior for manual review.
While this prototype uses synthetic data, the same workflow can be extended to real claims datasets to:

Prioritize provider audits.

Support Fraud, Waste & Abuse (FWA) investigations.

Integrate anomaly scores into continuous monitoring dashboards.

Next Steps:

Incorporate temporal variables (claim date, rolling averages).

Introduce unsupervised neural models (autoencoders).

Evaluate precision/recall on labeled historical data.
```text

7. Repository Structure
claims-anomaly-detection/
│
├── data/
│   ├── raw/                 <- Synthetic input data
│   └── processed/           <- Aggregated summaries and model outputs
│
├── figures/                 <- Generated charts and visualizations
│
├── notebooks/
│   └── 01_claims_anomaly_detection.ipynb
│
├── requirements.txt         <- Python dependencies
├── .gitignore               <- Environment and data exclusions
└── README.md                <- Project documentation
```
8. Environment Setup
Create environment
conda create -n claims python=3.11 -y
conda activate claims

Install dependencies
pip install -r requirements.txt

Launch notebook
jupyter lab

9. Key Technologies

Python 3.11

pandas, NumPy, matplotlib, seaborn — Data processing & visualization

scikit-learn — Isolation Forest anomaly detection

Jupyter Lab — Interactive analytics environment

10. License

MIT License © 2025 Michael S. Mohle
