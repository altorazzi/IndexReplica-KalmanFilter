# Portfolio Replication Project

This project contains all materials related to my final Fintech project on Black Box Index replication using machine learning and Kalman filtering techniques

## Installation

No installation is required.  
The notebook can be executed directly on [Kaggle](https://www.kaggle.com) or on [Google Colab](https://colab.research.google.com) with minimal setup.

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

The notebook is ready to run on **Kaggle** with no modification.  
Simply upload the Excel file to the working directory.

To run on **Google Colab**, follow these steps:

```python
from google.colab import drive
drive.mount('/content/drive')

file_path = '/content/drive/MyDrive/path_to/Dataset3_PortfolioReplicaStrategy.xlsx'
