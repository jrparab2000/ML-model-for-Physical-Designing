# Physical Design Automation: Accelerating Chip Layout Optimization using ML 🚀

<div align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-blue.svg" alt="Python Version">
  <img src="https://img.shields.io/badge/Machine%20Learning-Random%20Forest-orange.svg" alt="ML Model">
  <img src="https://img.shields.io/badge/EDA-Semiconductor-green.svg" alt="Domain">
</div>

## 📌 Table of Contents
- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Proposed Solution](#proposed-solution)
- [Dataset & Preprocessing](#dataset--preprocessing)
- [Machine Learning Models](#machine-learning-models)
- [Repository Structure](#repository-structure)
- [How to Run](#how-to-run)
- [Author](#author)

## 📖 Overview
Designing microchips begins as code, which must be painstakingly translated into a physical blueprint of billions of transistors and wires—a stage known as **Physical Design**. Because engineers must constantly tweak this blueprint to prevent overheating and power drain, the process becomes a massive, time-consuming game of trial and error. 

This project bypasses this costly feedback loop by introducing a Machine Learning model to act as a fast predictive proxy for Electronic Design Automation (EDA) software. 

## ⚠️ Problem Statement
In the semiconductor industry, the physical design stage is incredibly time-consuming. Modern EDA software suites can take **days** to process inputs, place components, and route wires for a single layout. 

A major bottleneck is its iterative, "black-box" nature. Engineers can only evaluate whether a physical layout is acceptable (in terms of area, timing, and power constraints) *after* the execution run completes entirely. If suboptimal, the multi-day process restarts, drastically slowing down time-to-market.

## 💡 Proposed Solution
By predicting layout characteristics early in the design cycle, we enable real-time architectural exploration without waiting for full physical implementation. 

- **Current Process:** Synthesis (few hours) ➡️ Physical Design (few days) ➡️ Issue with design ➡️ Repeat.
- **New ML Pipeline:** Synthesis (few hours) ➡️ **Predict Physical Design Results (few minutes)** ➡️ Validate if values feel right.

This eliminates weeks of guesswork and drastically speeds up the journey from code to silicon by instantly predicting critical performance parameters like **Area**, **Power**, and **Wire Length**.

## 📊 Dataset & Preprocessing
The dataset consists of roughly **30,000 JSON files** collected from GitHub, which were merged into a single CSV format.
- **Data Scope:** The model maps the structural properties and specific configurations of different chip design families (e.g., 180nm and 130nm tech nodes) directly to their final physical footprints.
- **Cleaning Steps:**
  - Merged all individual JSON files into one comprehensive CSV.
  - Removed unwanted columns not relevant to the target features.
  - Handled missing values (NaNs) and dropped incomplete records.
  - Filtered out extreme outlying data.
  - Final processed dataset size: **20,729 rows**.

## 🧠 Machine Learning Models
Several regression models were tested to find the best fit for predicting non-linear chip scaling behaviors:

1. **Linear Regression:**
   - Evaluated as a baseline. Performed poorly initially ($R^2$ score $\approx$ 0.5). 
   - Showed slight improvement after dropping high-correlation features, outliers, and NA rows.
2. **Polynomial Regression:**
   - Attempted to capture non-linearity but performed terribly on raw data ($R^2$ score $\approx$ -11.51).
   - Improved significantly after strict data cleaning, though still prone to overfitting.
3. **Random Forest Regressor (Winner 🏆):**
   - The ensemble tree-based approach perfectly handled the complex, non-linear relationships of physical chip scaling.
   - Showed excellent results even on raw data ($R^2$ score $\approx$ 0.95).
   - **Final Cleaned Data Results:** Achieved an **$R^2$ score of ~0.999**, making it a highly reliable predictive proxy for EDA verification.

## 📁 Repository Structure

```text
📦 Repository Root
 ┣ 📂 main                 # Main project folder
 ┃ ┣ 📜 main.ipynb         # Jupyter Notebook containing the full ML pipeline & EDA
 ┃ ┗ 📂 data               # Folder containing the merged dataset
 ┗ 📜 README.md            # Project documentation (this file)