# DSC180B-Capstone-Project

## Installation and Setup

1. **Create Conda Environment:**
   - Open a terminal and navigate to your project directory.
   - Create a conda environment (replace 'myenv' with your preferred environment name):
     ```bash
     conda create --name myenv python=3.8
     ```

2. **Activate Conda Environment:**
   - Activate the created environment:
     ```bash
     conda activate myenv
     ```

3. **Install Required Packages:**
   - Install the necessary packages using pip within the activated conda environment:
     ```bash
     %%capture
     !pip install 'aif360[LawSchoolGPA]' > /dev/null
     !pip install 'aif360' > /dev/null
     !pip install --upgrade tensorflow aif360 > /dev/null
     !pip install protobuf==3.19.0 > /dev/null
     !pip install 'aif360[AdversarialDebiasing]' > /dev/null
     !pip install scikit-surprise > /dev/null
     ```

4. **Verify Installation:**
   - Ensure all packages are installed correctly by running the following imports in a Jupyter notebook or Python script:
     ```python
     import warnings
     warnings.filterwarnings("ignore")

     # Your existing import statements
     import random
     from sklearn import linear_model
     from matplotlib import pyplot as plt
     from collections import defaultdict
     import gzip
     from sklearn.linear_model import LogisticRegression
     from sklearn.model_selection import train_test_split
     from sklearn.metrics import accuracy_score, balanced_accuracy_score
      
     import json
     import numpy
     import math
     import pandas as pd
     from sklearn.linear_model import LinearRegression
     from sklearn.model_selection import train_test_split
     from sklearn.metrics import mean_squared_error
      
     import scipy.optimize
     from sklearn import svm
     import string
     import random
      
     from surprise import Dataset, Reader, accuracy
     from surprise.model_selection import train_test_split
     from surprise.prediction_algorithms.matrix_factorization import SVD
     import numpy as np
     import os
     import tarfile
     import warnings
     from sklearn.model_selection import train_test_split
     from sklearn.linear_model import LinearRegression
     from sklearn.metrics import mean_squared_error
     from sklearn.metrics import jaccard_score
      
     from aif360.datasets import StandardDataset
     from aif360.metrics import BinaryLabelDatasetMetric, ClassificationMetric
     from aif360.algorithms.preprocessing import Reweighing
     from aif360.algorithms.preprocessing import DisparateImpactRemover
     from sklearn.ensemble import RandomForestClassifier
     from sklearn.model_selection import train_test_split, GridSearchCV
     from sklearn.metrics import accuracy_score, classification_report
     from IPython.display import Markdown, display
     from sklearn.metrics import roc_curve, auc, precision_recall_curve, average_precision_score
     from sklearn.inspection import permutation_importance
      
     from surprise import Reader, Dataset, SVD
     from surprise.model_selection import cross_validate, train_test_split
     from surprise import accuracy
     from sklearn.metrics.pairwise import cosine_similarity
     from scipy.stats import pearsonr
      
     from sklearn.ensemble import RandomForestClassifier
     from sklearn.metrics import accuracy_score, classification_report
     from sklearn.model_selection import train_test_split as sklearn_train_test_split
     from IPython.display import Markdown, display
     ```

5. **Acquire Data:**
   - Navigate to [the provided URL](https://grouplens.org/datasets/movielens/1m/) and download the data. Place both .csv files in the same folder as the notebook.

6. **Launch Jupyter Notebook:**
   - Start Jupyter Lab within the conda environment:
     ```bash
     jupyter-lab
     ```

7. **Open Notebook:**
   - Navigate to the notebook in Jupyter Lab and launch it.

## Troubleshooting:
   - If you encounter any issues, check for common errors like version conflicts or missing dependencies. The documentation for each package can provide more specific guidance.

Remember to regularly update your packages to get the latest features and bug fixes.

## Notes:
   - This project assumes you have Conda installed. If not, you can install it by following the instructions at [Conda Installation Guide](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html).

   - Make sure to activate your conda environment before working on the project:
     ```bash
     conda activate myenv
     ```

   - Adjust the environment name ('myenv') and Python version according to your preferences.

   - If you encounter issues related to Jupyter Lab, ensure that you have launched it from within the conda environment where you installed the project dependencies.

Happy coding!
