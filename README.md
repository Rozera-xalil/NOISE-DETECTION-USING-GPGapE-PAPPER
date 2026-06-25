GPGapE+ — Noisy Data Detection Using Triple Ensemble
📌 Overview

GPGapE+ is an advanced framework for detecting and correcting noisy labels in regression datasets using a hybrid Triple Ensemble approach:

Gaussian Process Regression (from scratch)
Mahalanobis Distance
Isolation Forest

The system is designed to improve data quality by identifying corrupted samples and replacing them with statistically reliable predictions.

📊 Dataset

This project uses the Energy Efficiency Dataset (ENB2012) from the UCI Machine Learning Repository:

768 samples
8 input features (building geometry parameters)
2 target variables (Heating & Cooling load)
Regression task

🔗 Dataset Source: https://archive.ics.uci.edu/dataset/242/energy+efficiency

⚙️ Methodology
1. Data Preprocessing
Standardization using StandardScaler
Train/test preparation
Feature correlation analysis
2. Noise Injection

To simulate real-world corrupted data:

15% of labels are intentionally corrupted
Additive structured noise:
Random amplitude scaled by dataset range
Both positive and negative perturbations
3. Gaussian Process (From Scratch)

A full Gaussian Process Regression model implemented using NumPy only:

No external GP libraries used
Optimized using Negative Log Marginal Likelihood (L-BFGS-B)
Produces:
Predictive mean (μ)
Predictive uncertainty (σ²)
4. GPGapE Noise Scoring

Noise detection is based on:

NoiseScore
i
	​

=
σ
i
2
	​

+ϵ
(y
i
	​

−μ
i
	​

)
2
	​


High score → likely noisy sample

5. Triple Ensemble Detection

Final noise decision is made using:

Gaussian Process anomaly score
Mahalanobis Distance (statistical outliers)
Isolation Forest (tree-based anomaly detection)

Majority voting improves robustness.

6. Label Correction

Detected noisy samples are corrected using GP predictions:

y
i
corrected
	​

={
μ
^
	​

i
	​

y
i
	​

	​

if noisy
otherwise
	​

📈 Explainability

For each flagged sample, the model provides:

Original vs noisy value
GP predicted value
Uncertainty (standard deviation)
Noise score explanation

This improves interpretability and debugging.

🧪 Robustness Analysis

The model is tested under different noise levels:

5% → 30% corrupted labels
Evaluates stability of detection performance
Shows consistent robustness across increasing noise
📌 Pipeline Summary
Load ENB2012 dataset
Inject synthetic noise (15%)
Train Gaussian Process model
Compute predictions & uncertainty
Calculate noise score
Apply Mahalanobis + Isolation Forest
Detect noisy samples (ensemble voting)
Correct labels using GP predictions
Evaluate RMSE improvement
📦 Requirements
numpy
pandas
matplotlib
seaborn
scikit-learn
🚀 Key Features
✔ Gaussian Process built from scratch (no GP libraries)
✔ Triple ensemble anomaly detection
✔ Real-world noise simulation
✔ Automatic label correction
✔ Explainable predictions
✔ Robustness evaluation across noise levels
🧠 Project Goal

To build a robust noisy-label detection system that:

Works on regression datasets
Handles real-world uncertainty
Improves dataset quality before training ML models
👩‍💻 Author

Developed as a machine learning research project focused on:

Probabilistic modeling
Anomaly detection
Data cleaning pipelines
