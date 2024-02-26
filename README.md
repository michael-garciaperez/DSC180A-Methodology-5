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
     !pip install seaborn > /dev/null
     ```

4. **Verify Installation:**
   - Ensure all packages are installed correctly by running the following imports in a Jupyter notebook or Python script:
     ```python
     import warnings
     warnings.filterwarnings("ignore")
     
     # Import statements
     import random
     import gzip
     import json
     import numpy as np
     import math
     import pandas as pd
     import scipy.optimize
     import string
     import random
     import os
     import re
     import tarfile
     import warnings
     import seaborn as sns

     from matplotlib import pyplot as plt
     from collections import defaultdict
     from sklearn import linear_model
     from sklearn.linear_model import LogisticRegression
     from sklearn.metrics import accuracy_score, balanced_accuracy_score
     from sklearn.linear_model import LinearRegression
     from sklearn.metrics import mean_squared_error
     from sklearn import svm
     from sklearn.metrics import jaccard_score
     from sklearn.ensemble import RandomForestClassifier
     from sklearn.model_selection import GridSearchCV
     from sklearn.metrics import accuracy_score, classification_report
     from sklearn.metrics import roc_curve, auc, precision_recall_curve, average_precision_score
     from sklearn.inspection import permutation_importance
     from sklearn.metrics.pairwise import cosine_similarity
     from sklearn.model_selection import train_test_split as sklearn_train_test_split
     
     from surprise import Dataset, Reader, accuracy
     from surprise.model_selection import cross_validate, train_test_split
     from surprise.prediction_algorithms.matrix_factorization import SVD
     from surprise import SVD
     from surprise import accuracy
     
     from aif360.datasets import StandardDataset
     from aif360.metrics import BinaryLabelDatasetMetric, ClassificationMetric
     from aif360.algorithms.preprocessing import Reweighing
     from aif360.algorithms.preprocessing import DisparateImpactRemover
     
     from scipy.stats import pearsonr
     from IPython.display import Markdown, display
     ```

5. **Acquire Data:**
   - Navigate to [the provided URL](https://grouplens.org/datasets/movielens/1m/) and download the data. Place both the movies.dat and ratings.dat files in the same folder as the notebook.
   - Navigate to [the provided URL](https://figshare.com/articles/dataset/U_S_movies_with_gender-disambiguated_actors_directors_and_producers/4967876) and download the data. Place the directors.json file in the same folder as the notebook.
   - Navigate to [the provided URL](https://datasets.imdbws.com/) and download the title.basics.tsv.gz file. Place the file in the same folder as the notebook.

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

   - The website for this can be found [here](https://michael-garciaperez.github.io/DSC180B-Capstone-Project/).
  
Happy coding!
