Notes – Supervised Machine Learning (Part 5): Train–Test Split & Cross-Validation

1. Purpose of Train/Test Split
<img width="1631" height="1035" alt="image" src="https://github.com/user-attachments/assets/09e3f8fa-5f3e-4b53-b255-01b403408c2f" />

We divide our dataset into training and testing subsets.

Training set: used to fit the model and learn parameters.

Test set: held out to evaluate performance on unseen data.

This helps estimate how the model will perform in the real world, not just on data it has already seen.

<img width="1853" height="1017" alt="image" src="https://github.com/user-attachments/assets/b47804ce-aabe-4f99-80a7-481698670158" />

2. Overfitting and Generalization

If we train on the entire dataset, the model can perfectly “memorize” the data → 100% accuracy on training, but fails on new data.

Splitting ensures we can detect overfitting — when a model performs well on training but poorly on unseen samples.

Goal: achieve a model that generalizes well beyond the training examples.

3. Data Leakage

Always ensure training and test sets are independent.

If information from the test set “leaks” into training (e.g., duplicate or correlated records), evaluation becomes invalid.

Data leakage causes unrealistically high accuracy and poor real-world performance.

4. Evaluation Process

Train the model on the training set → learn parameters.

Use the model to predict outcomes for the test set.

Compare predictions with the true values (since test data still has known labels).

Calculate an error metric (e.g., MSE, accuracy, etc.) to evaluate performance on unseen data.

5. Cross-Validation

Extension of the train/test idea — instead of one split, perform multiple splits (e.g., k-fold cross-validation).

Train and test the model on different subsets several times → average the performance.

Gives a more reliable estimate of real-world model performance.

6. Model Complexity vs. Error

As model complexity increases, training error decreases, but test error may rise after a point (overfitting).

<img width="1142" height="595" alt="image" src="https://github.com/user-attachments/assets/b033a6ce-7327-4c7b-a3a3-97c3a7569379" />

The goal is to find the optimal balance — a model complex enough to capture patterns but simple enough to generalize.

7. Summary

Train/test split and cross-validation are essential to evaluate model performance fairly.

Avoid data leakage, watch for overfitting, and use appropriate validation to ensure the model performs well on truly unseen data.
1. Training Data Workflow

Training data includes X_train (features) and Y_train (labels).

We fit a model to this data using the .fit() method (common in scikit-learn).

The model learns parameters that describe the relationship between X and Y.

Example syntax structure:

model.fit(X_train, Y_train)


After fitting, the model is ready to make predictions on unseen data.

2. Testing Data Workflow

Use the test data (X_test) to check how well the model generalizes.

Pass X_test into the trained model to get predictions:

Y_pred = model.predict(X_test)


Compare these predictions with the true labels Y_test.

Evaluate the difference using an error metric (e.g., accuracy, MSE).

This gives the test error, showing expected real-world performance.

3. Using train_test_split in Python

Import the function:

from sklearn.model_selection import train_test_split


Basic syntax:

X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.3)


test_size=0.3 → 30% of data used for testing.

Values between 0 and 1 represent proportions; integer values specify exact sample counts.

4. Other Splitting Methods

ShuffleSplit:

Generates multiple random train/test splits.

Useful for evaluating model stability across different subsets.

StratifiedShuffleSplit:

Ensures that class proportions remain consistent between training and testing sets.

Important when dealing with imbalanced datasets (e.g., 99% non-cancer vs. 1% cancer).

Maintains representative distribution across both splits.

5. Key Takeaways

Always separate training and testing data to evaluate generalization.

Use train_test_split as the standard method in scikit-learn.

For imbalanced data, prefer stratified splitting to avoid bias.

The goal: simulate how the model performs on unseen, real-world data while preserving data integrity.

Notes – Supervised Machine Learning (Part 7): Polynomial Regression & Model Complexity

1. Overview/
<img width="1022" height="527" alt="image" src="https://github.com/user-attachments/assets/690dec2b-406c-47f8-9c4d-83fd6e13023b" />


Extends linear regression by introducing polynomial and interaction features.

Goal: capture nonlinear relationships between variables while still using a linear model.

This section connects polynomial regression with cross-validation and the bias–variance trade-off.

2. Concept of Polynomial Regression

Still based on linear regression, but we transform the input features.

Example: instead of using only budget, we add new features like budget², budget³, or budget × runtime.

The model remains linear in parameters — the equation is still a linear combination of all features (original + transformed).

This helps model curved patterns in data (nonlinear effects).

3. Creating Polynomial and Interaction Features

Generate new variables using feature transformations:

Squaring or cubing features.

Multiplying features together to form interaction terms.

These transformations can reveal relationships that simple linear regression misses.

To manage complexity, use cross-validation to evaluate how added features affect performance on the holdout set.

4. Implementation in Python (scikit-learn)

Import and use PolynomialFeatures:

from sklearn.preprocessing import PolynomialFeatures

polyFeat = PolynomialFeatures(degree=2)
X_poly = polyFeat.fit_transform(X)


degree determines the maximum power (e.g., 2 → squared, 3 → cubic).

Output includes:

Original features.

Squared/cubed features.

Interaction terms (feature₁ × feature₂).

5. Choosing the Right Functional Form

Many possible transformations exist; selection depends on:

Correlation or relationship with target variable.

Domain knowledge — which interactions make sense.

Empirical performance via cross-validation.

Avoid adding unnecessary terms that increase complexity without improving predictive power.

6. Link to Bias–Variance Trade-off

Adding polynomial and interaction terms increases model complexity.

Too simple → underfitting, misses real patterns.

Too complex → overfitting, memorizes noise.

Cross-validation helps identify the “sweet spot” between bias and variance.

7. Broader Application

This framework applies to all future models:

Logistic Regression, KNN, Decision Trees, SVM, Random Forests, Ensembles, Deep Learning.

Regardless of algorithm, the same principle remains:
Balance complexity and generalization using transformations, validation, and regularization.

8. Summary

Polynomial regression = extending linear regression to model nonlinear effects.

Still a linear model but with expanded feature space.

Core takeaway: learn to control complexity through feature engineering and cross-validation — a foundation for all advanced ML models.
