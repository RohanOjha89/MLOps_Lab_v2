# MLflow Lab
This directory contains code for running MLflow experiments
The lab demonstrates an end-to-end model experimentation workflow using MLflow Tracking, focusing on handling class imbalance in a binary classification problem.

I evaluated multiple modeling strategies and imbalance-handling techniques to observe how performance metrics (especially recall and F1) change across setups.

| # | Experiment Type                              | Description                                                                                                                                    | Why                                                                             |
| - | -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| 1 | **Original Dataset (No Balancing)**          | Train baseline models on raw imbalanced dataset                                                                                                | Establish raw model behavior without intervention                               |
| 2 | **SMOTE Oversampling**                       | Apply SMOTE to synthetically increase minority class                                                                                           | Improve recall by balancing dataset                                             |
| 3 | **Class-Weighted / Scale-Pos-Weight Models** | No oversampling — models trained with: <br>• `class_weight="balanced"` (Random Forest, Logistic Regression) <br>• `scale_pos_weight` (XGBoost) | Penalize misclassification of minority class to force models to learn imbalance |

## Metrics Tracked
accuracy
precision
recall (primary focus for imbalance)
f1_score
roc_auc_score

Goal: Understand real trade-offs between precision-recall-AUC across imbalance techniques.

## Observations Summary
| Setting                           | Behavior                                                                         |
| --------------------------------- | -------------------------------------------------------------------------------- |
| Raw Data                          | High accuracy, **very low recall** (classic imbalance issue)                     |
| SMOTE                             | Recall and F1 improved significantly, slight precision drop (expected trade-off) |
| Class-Weighted / Scale Pos Weight | Best **recall-precision balance**, especially in XGBoost                         |

## How to Run
### Run MLflow Tracking server:
mlflow server \
--backend-store-uri sqlite:///mlflow.db \
--default-artifact-root ./mlartifacts \
--host 0.0.0.0 \
--port 5000

### Execute experiment script / notebook:
python run_mlflow.sh

### Open MLflow UI:
http://127.0.0.1:5001

## Folder Structure
Mlflow_Labs_User/
    ├── Model_Techniques_MLflow.ipynb
    ├── run_mlflow.sh
    ├── mlruns/         # ignored
    ├── mlartifacts/    # ignored
    ├── mlflow.db       # ignored
    └── README.md

> Note: MLflow artifacts (`mlruns`, `mlartifacts`, `mlflow.db`) are intentionally excluded via `.gitignore`.