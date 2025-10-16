<img width="1013" height="561" alt="image" src="https://github.com/user-attachments/assets/ad840be8-5394-4ab6-b0e6-984fbe74f2a5" />
Notes – Supervised Machine Learning (Part 8): Cross-Validation & Model Complexity

1. Why Cross-Validation

Instead of relying on a single train/test split, we perform multiple splits to test the model’s consistency.

The dataset is divided into several pairs of training and validation sets.

The model is trained and evaluated on each split → errors are averaged to get a more reliable performance estimate.

This reduces the risk of a model appearing good by chance on one lucky test set.

2. Process Overview

Split data into multiple folds (train/test pairs).

For each fold:

Train on the training portion.

Evaluate on the validation portion.

Record the error (e.g., MSE).

Average all validation errors to get the final performance score.

Each sample is used for both training and testing at different times → more statistically significant result.

3. Terminology
<img width="1085" height="584" alt="image" src="https://github.com/user-attachments/assets/183cea97-8a09-42ed-9584-b4ebd80ece0f" />


Training data: used to learn model parameters.

Validation data: temporary “test-like” subset used to tune and compare models.

Test data: kept aside until the end — used only for final evaluation after modeling is complete.

4. Complexity vs. Error Relationship
<img width="1242" height="601" alt="image" src="https://github.com/user-attachments/assets/cfe226bc-c035-4e62-9483-665cc7afe3fd" />

Training error always decreases with higher model complexity.

Validation error decreases up to a point, then rises again (overfitting).

Curve interpretation:

Left side: underfitting — model too simple, high error on both training and validation.

Middle (sweet spot): balanced — low training and validation error (good generalization).

Right side: overfitting — low training error, high validation error.

The goal: find the “just right” (Goldilocks) point where the model is complex enough to capture patterns but still generalizes well.

5. Common Cross-Validation Methods

K-Fold Cross-Validation:

Split data into K folds (e.g., K=4).

Train on K-1 folds, test on the remaining fold, repeat K times.

Average performance across folds.

Leave-One-Out Cross-Validation (LOOCV):

Each observation is used once as the test set; all others are training.

Provides many test sets but is computationally expensive.

Stratified K-Fold:

Used for categorical outcomes.

Maintains the same class proportions (e.g., 80% true / 20% false) in every fold.

Ensures balanced representation across splits.

6. Implementation in Python (scikit-learn)
from sklearn.model_selection import cross_val_score, KFold, StratifiedKFold
from sklearn.linear_model import LinearRegression

model = LinearRegression()
scores = cross_val_score(
    model,
    X, Y,
    cv=4,  # number of folds
    scoring='neg_mean_squared_error'  # negative MSE so higher = better
)


cross_val_score automatically performs training/testing across folds and averages the results.

For stratified splits, pass a StratifiedKFold object as the cv argument.

7. Key Takeaways

Cross-validation provides a more robust estimate of model performance.

Prevents misleading results from a single random split.

Always monitor both training and validation errors to find the right model complexity.

Core goal: balance bias and variance to achieve strong generalization on unseen data.

Summary/Review
Cross Validation

The three most common cross validation approaches are:

k-fold cross validation

leave one out cross validation

stratified cross validation


Cross validation method involves dividing the dataset into 3 parts:

training set - is a portion of the data used for training the model

validation set - is a portion of the data used to optimize the hyper-parameters of the model

test set - is a portion of the data used to evaluate the model 


Cross Validation Syntax

`Scikit Learn` library contains many methods that can perform the splitting of the data into training, testing and validation sets. The most popular methods that we covered in this module are:

*   train_test_split - creates a single split into train and test sets

*   K-fold - creates number of k-fold splits, allowing cross validation

*   cross_val_score - evaluates model's score through cross validation

*   cross_val_predict – produces the out-of-bag prediction for each row

*   GridSearchCV – scans over parameters to select the best hyperparameter set with the best     

     out-of-sample score
