### Problem Statement & Approach
This project focuses on identifying malicious and benign network traffic using machine learning. The main objective was to build a reliable intrusion detection model capable of classifying network flows accurately using the features provided in the EGSPEC CyberGuard 2026 dataset.

The workflow followed in this project was:

Load and inspect the training and testing datasets.
Analyze the target distribution and feature structure.
Handle missing values and infinite values.
Separate numerical and categorical features.
Remove the Flow_ID column from model training because it acts only as an identifier.
Split the training data into training and validation sets using stratified sampling.
Train a CatBoost classification model.
Evaluate the model using Accuracy, F1-score, Classification Report and Confusion Matrix.
Retrain the final model using the complete training dataset.
Predict the attack labels for the test dataset.
Generate the final Kaggle submission file.
Data Exploration & Preprocessing
The training dataset contains network traffic records with multiple numerical and categorical attributes.

The target variable used for classification is:

Attack_Label

The two target classes are:

Benign
Malicious
During preprocessing:

Infinite values were replaced with missing values.
Numerical missing values were filled using the median of the corresponding training feature.
Categorical missing values were replaced with the value "Unknown".
Categorical variables were handled directly using CatBoost.
Flow_ID was preserved only for the final submission and excluded from training.
Feature Engineering & Selection
The available network traffic attributes were used as model features.

CatBoost was selected because it can efficiently process mixed numerical and categorical data without requiring extensive manual encoding.

Feature importance analysis was also performed after model training to understand which network characteristics contributed most to the predictions.

Machine Learning Model
The primary model used in this project was CatBoostClassifier.

Main parameters included:

Tree depth: 8
Learning rate: 0.05
Maximum iterations: 1200
Loss function: Logloss
Evaluation metric: F1
L2 regularization: 5
Early stopping: 150 rounds
Random seed: 42
A stratified 80:20 train-validation split was used so that the class distribution remained consistent across both sets.

Model Evaluation
The model was evaluated using:

Accuracy
F1-score
Precision
Recall
Classification Report
Confusion Matrix
Early stopping was used to prevent unnecessary training and reduce overfitting.

After validation, the best number of boosting iterations was selected and a final model was retrained using the entire training dataset.

Final Prediction and Submission
The trained model was applied to the competition test dataset.

The final submission contains two columns:

Flow_ID
Attack_Label

The prediction file was saved as:

submission.csv

This file was then used for the Kaggle competition submission.

Key Findings & Limitations
CatBoost performed well for this structured cybersecurity dataset because it can model nonlinear relationships between network traffic features and attack behaviour.

Important advantages of the approach include:

Minimal preprocessing
Native categorical feature support
Strong classification capability
Efficient training
Feature importance analysis
Good resistance to overfitting through regularization and early stopping
Possible future improvements include:

Cross-validation
Hyperparameter optimization
CatBoost, LightGBM and XGBoost ensemble models
Probability threshold optimization
Advanced feature engineering
Attack-type multiclass classification
