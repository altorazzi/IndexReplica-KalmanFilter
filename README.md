# Dynamic Index Replication via Kalman Filter

## Project Overview
This project implements a **Black Box Index Replication strategy** using a universe of liquid Futures contracts. The goal is to replicate the returns of an unknown target index while minimizing tracking error and transaction costs.

## Methodology

### 1. Cost-Adaptive Kalman Filter
Implement a state-space model to estimate time-varying portfolio weights ($\beta_t$) without explicit retraining.

* **Cost-Aware Observation:** Unlike standard filters, we inject transaction costs directly into the observation equation. The model learns to track the **net-of-cost return**, penalizing high-turnover rebalancing.
* **Ridge Initialization:** $x_0$ seeded via Ridge Regression for faster convergence.
* **Beta Scaling:** Weights are dynamically scaled to match the target's volatility profile.
* **Buffering:** A "dead-zone" threshold prevents rebalancing if weight deltas are negligible, reducing execution churn.
* **Shrinkage:** The final weights are a convex combination of the model-derived weights and an equal-weight ($1/N$) portfolio.
  $$w_{final} = \lambda w_{equal} + (1-\lambda) w_{ensemble}$$
* **Bias Correction:** A rolling mean of past residuals is added to the forecast to correct persistent systematic tracking errors.

### 2. Statistical Arbitrage - Pair Trading
A mean-reversion strategy built on top of the replication engine.

* **Setup:** Two independent Kalman Filters are trained on **disjoint subsets** of the asset universe to track the same target.
* **Signal:** We monitor the rolling correlation between the two replicators.
* **Execution:** When correlation drops below a threshold (divergence), we enter a **Long/Short** position, betting on the convergence of the two portfolios.

## Installation

No installation is required.  
The notebook can be executed directly on [Kaggle] or on [Google Colab] with minimal setup.

## Usage

### Contents

- **Long_Abstract.pdf**  
  A detailed report describing the methodology, model design, and key findings. It highlights the differences between the Kalman Filter-based strategy and the Ensembling approach.

- **Presentation.pdf**  
  A summary presentation for academic or public discussion, focusing on the core ideas and results.

- **Notebook.ipynb**  
  A fully executable Python notebook (developed on Kaggle) that contains all data processing steps, model training, and performance evaluation.

- **Dataset3_PortfolioReplicaStrategy.xlsx**  
  The dataset used in the notebook, including asset prices, index returns, and other relevant data.

### How to Run

The notebook was natively developed on Kaggle. It requires no environment setup. simply upload `Dataset3_PortfolioReplicaStrategy.xlsx` to the working directory.

To run on **Google Colab**:

1. Upload the `.ipynb` file to Colab.
2. Upload the dataset to your Google Drive.
3. Mount the drive using the snippet below:

```python
from google.colab import drive
drive.mount('/content/drive')

# Update this path to match your Drive structure
file_path = '/content/drive/MyDrive/path_to/Dataset3_PortfolioReplicaStrategy.xlsx'
