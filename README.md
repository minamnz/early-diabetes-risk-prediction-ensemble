# Early-Stage Diabetes Risk Prediction with Ensemble Machine Learning

**Partial reproduction of a published research study | University machine learning course project | Python & scikit-learn**

This repository documents an educational exploration of early-stage diabetes risk classification, inspired by Palabaş (2024). It compares standard machine-learning classifiers, ensemble methods, and feature-selection approaches using the **UCI Early Stage Diabetes Risk Prediction dataset** (520 questionnaire-based records). The notebook retrieves the public dataset directly via `ucimlrepo` (dataset ID **529**).

> **Scope:** This is an independent course-project implementation, not the authors' official code or an exact reproduction of their WEKA experiments. Models and feature-selection procedures use scikit-learn approximations. Results describe the saved notebook run; the repository has not been independently rerun or clinically validated.

## Implemented workflow

1. Load the dataset with `ucimlrepo`, inspect fields and missing values, and encode categorical variables.
2. Evaluate **Gaussian Naive Bayes**, an entropy-based **Decision Tree** (J48-inspired, not the actual WEKA J48), **k-Nearest Neighbors**, and an RBF **SVM** (SMO-inspired) using **15-fold stratified cross-validation**.
3. Compare **AdaBoost**, **Bagging**, and **Random Subspace** ensemble wrappers; record accuracy, Cohen's kappa, RMSE, and ROC AUC.
4. Plot ROC curves and explore feature importance and backward sequential feature selection as an approximation to WEKA's Wrapper Subset Evaluation.
5. Evaluate an additional manually reduced feature set. This is distinct from the automatically selected feature subset.

## Selected saved results

| Experiment | Model | Mean cross-validation accuracy |
|---|---|---:|
| Baseline | Entropy decision tree (J48-inspired) | 97.88% |
| Ensemble | Random Subspace + decision tree | 98.07% |
| Ensemble | AdaBoost + decision tree | 97.88% |
| Ensemble | Bagging + decision tree | 97.69% |
| Manually reduced features | AdaBoost + decision tree | 97.31% |

These figures are from the notebook's saved outputs; they are **not** a fresh independent execution. The source paper reports different experiments and results, so these values should not be presented as reproducing its reported 99% accuracy.

## Limitations and interpretation

- The original publication uses **WEKA** algorithms; scikit-learn's entropy decision tree and SVC are **approximations**, not identical implementations of J48/SMO.
- The paper's Wrapper Subset Evaluation is approximated by backward sequential selection; the manually excluded three features in the final experiment are **not** the same set selected by the automated step.
- The preprocessing and feature-selection steps are performed before or outside some cross-validation evaluations. This workflow has **potential information leakage**, so scores should be treated as exploratory rather than unbiased generalization estimates. A leakage-safe replication would fit encoding/feature selection within each training fold using pipelines or nested validation.
- The data are questionnaire responses, not clinical diagnostic records. This code is **not a medical diagnostic tool** or suitable for patient care.
- AdaBoost with kNN is skipped in the ensemble comparison because the chosen scikit-learn estimator does not support the required sample weights.

## Repository structure

```text
notebooks/
  diabetes_ensemble_reproduction.ipynb
requirements.txt
.gitignore
README.md
```

## Run locally or in Google Colab

```bash
pip install -r requirements.txt
```

Open `notebooks/diabetes_ensemble_reproduction.ipynb` and run the cells in order. An internet connection is required to fetch the UCI dataset. Some ensemble estimators require a compatible scikit-learn version; the notebook has been preserved unchanged rather than refactored.

## Reference and dataset

- Palabaş, T. (2024). *Early-Stage Diabetes Risk Prediction Using Machine Learning Techniques Based on Ensemble Approach*. **Eskişehir Technical University Journal of Science and Technology C – Life Sciences and Biotechnology**, 13(2), 74–85. https://doi.org/10.18036/estubtdc.1320922
- UCI Machine Learning Repository: [Early Stage Diabetes Risk Prediction (ID 529)](https://archive.ics.uci.edu/dataset/529/early+stage+diabetes+risk+prediction+dataset).

## Academic context

Completed as a university course project for the **Machine Learning** course at **Amirkabir University of Technology (Tehran Polytechnic)**.

**Project author:**
- Mina Moazenzadeh

This project is independent of the paper's authors and acknowledges the original article above.
