# Temporal Early Warning of Sepsis Deterioration in ICU Patients

## Overview
This project implements a prospective, patient-level early warning system for predicting imminent sepsis deterioration in ICU patients using high-frequency longitudinal clinical data.

Rather than retrospective sepsis detection, the task is formulated as time-dependent risk prediction within a fixed future horizon.

## Problem Formulation

At each ICU hour t, the model predicts whether a patient will develop sepsis within the next 6 hours, without using any post-onset information.

Labels are constructed prospectively to reflect a realistic clinical early warning scenario.
This formulation highlights:
- Temporal dependency across observations
- Explicit definition of prediction horizon
- Avoidance of label leakage common in retrospective setups

## Dataset
- Source: PhysioNet Sepsis Challenge dataset
- Data type: Multivariate time-series (hourly ICU measurements)
- Features include vital signs and laboratory values
- Missingness is handled using simple imputation strategies suitable for baseline modeling

## Methodology
The analysis pipeline includes:
- Source: PhysioNet Sepsis Challenge dataset
- Resolution: Hourly ICU measurements
- Cohort split: Patient-level train/test separation

## Modeling Approach
- Algorithm: LightGBM (gradient-boosted decision trees)
- Missing data: Median imputation (train-only)
- Class imbalance: Native LightGBM handling
- Evaluation: AUROC, PR-AUC, recall-oriented thresholding

## Results 
- AUROC: ~0.65
- PR-AUC: Low, reflecting extreme outcome imbalance
- Thresholds chosen to prioritize sensitivity, consistent with early warning objectives

## Interpretability

Global and local explanations are generated using SHAP to identify dominant physiological drivers of short-term sepsis risk.

## Limitations
- Single-horizon prediction
- No explicit temporal feature engineering
- No external validation

## Purpose
This repository is intended as a research-oriented implementation demonstrating correct temporal framing, leakage avoidance, and clinically grounded evaluation for early warning modeling.
