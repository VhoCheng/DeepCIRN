# DeepCIRN: Spatiotemporal Residual Learning for Intersection Conflict Intensity Prediction

<p align="center">
  <img src="figures/DeepCIRN_overall_framework.png" width="95%">
</p>

<p align="center">
  <b>A spatiotemporal residual learning framework for intersection conflict intensity prediction and traffic safety evaluation.</b>
</p>

---

## Overview

**DeepCIRN** is a spatiotemporal residual learning framework designed for **intersection conflict intensity prediction** and **proactive traffic safety evaluation**.

Instead of relying only on historical crash records, DeepCIRN transforms UAV-based intersection trajectory data into structured road-user conflict intensity matrices and predicts future conflict risks through a multi-branch temporal learning architecture.

The framework is designed to support:

- proactive traffic safety evaluation;
- road-user interaction risk prediction;
- intersection-level conflict intensity forecasting;
- management-oriented traffic safety decision support;
- interpretable visualization of conflict patterns.

---

## Motivation

Urban intersections are high-risk traffic areas where heterogeneous road users, including cars, buses, trucks, motorcycles, bicycles, pedestrians, vans, and trailers, interact within limited space and time.

Traditional traffic safety analysis usually relies on crash records. However, crashes are sparse, delayed, and insufficient for short-term safety management. Traffic conflicts provide a more proactive surrogate safety indicator because they can reveal near-crash risk before actual crashes occur.

With UAV-based trajectory data, it becomes possible to observe high-resolution road-user movements from a bird’s-eye view and construct interaction-level conflict intensity matrices. DeepCIRN aims to model the temporal evolution of these matrices and provide interpretable future conflict predictions.

---

## Framework

DeepCIRN consists of five major components:

1. **Input and Data Processing**  
   UAV-based trajectory data are processed into road-user interaction records.

2. **Conflict Intensity Construction**  
   Road-user interactions are transformed into conflict intensity matrices based on surrogate safety measurements such as time-to-collision-related indicators.

3. **Multi-branch Spatiotemporal Residual Learning**  
   Three temporal branches are used to capture different temporal patterns:
   - closeness branch for recent dynamics;
   - period branch for repeated temporal patterns;
   - trend branch for longer-term temporal tendencies.

4. **Learnable Fusion and Auto-regressive Pathway**  
   The outputs of different temporal branches are fused using learnable weights and combined with an auto-regressive pathway to preserve local temporal continuity.

5. **Prediction and Safety Evaluation**  
   The model predicts future conflict intensity matrices and supports interaction-specific traffic safety evaluation.

---

## Methodology

Given a sequence of historical conflict intensity matrices:

\[
\mathcal{X} = \{X_1, X_2, ..., X_T\}
\]

DeepCIRN aims to predict the future conflict matrix:

\[
\hat{X}_{t+1} = f(X_t, X_{t-1}, ..., X_{t-L+1})
\]

where each matrix element represents the conflict intensity between two road-user categories.

The model uses three temporal components:

- **Closeness:** recent conflict matrices;
- **Period:** lagged matrices capturing repeated temporal patterns;
- **Trend:** longer-term lagged matrices capturing broader temporal changes.

The final prediction is obtained by combining residual convolutional representations and an auto-regressive component.

---

## Experimental Design

The experiments evaluate DeepCIRN using the following regression metrics:

- Mean Absolute Error;
- Root Mean Square Error;
- Coefficient of Determination.

Baseline models include:

- ARIMA;
- Random Forest;
- XGBoost;
- LSTM;
- GRU.

Ablation studies are conducted by removing:

- the closeness branch;
- the period branch;
- the trend branch;
- the auto-regressive pathway.

---

## Main Findings

The experimental results suggest that:

- recent temporal information plays the most important role in short-term conflict intensity prediction;
- the period and trend branches provide complementary temporal information;
- the auto-regressive pathway helps preserve local temporal continuity;
- matrix-level prediction outputs are useful for identifying high-risk road-user interaction pairs;
- DeepCIRN can support proactive and interpretable intersection safety evaluation.

---

## Repository Structure

```text
DeepCIRN/
├── README.md
├── requirements.txt
├── src/
│   ├── data_preprocessing/
│   ├── models/
│   ├── train.py
│   ├── evaluate.py
│   └── utils.py
├── figures/
│   ├── DeepCIRN_overall_framework.jpeg
│   ├── benchmark_summary_clean.pdf
│   ├── ablation_summary_clean.pdf
│   └── time_series_sample.pdf
├── results/
│   ├── benchmark_results.csv
│   ├── ablation_structure.csv
│   └── metrics_summary.csv
├── data/
│   └── README.md
└── paper/
    └── DeepCIRN.pdf
