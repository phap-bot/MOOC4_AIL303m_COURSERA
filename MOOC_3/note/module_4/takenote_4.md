Notes – Supervised Machine Learning (Part 9): Bias–Variance Trade-off

1. Overview

This section explains how model complexity, bias, and variance interact to determine model performance.

Goal: find the optimal balance between bias, variance, and total error to avoid both underfitting and overfitting.

2. Model Complexity vs. Error
 <img width="890" height="497" alt="image" src="https://github.com/user-attachments/assets/2a900ec7-3737-48ea-b7ff-0081cb63e823" />

Too simple (left side) → both training and test errors are high → underfitting.

Too complex (right side) → training error low but test error high → overfitting.

Middle (sweet spot) → both training and test errors are relatively low → best generalization.

As complexity increases, training error decreases continuously, but test error follows a U-shaped curve.
<img width="1079" height="574" alt="image" src="https://github.com/user-attachments/assets/678fd249-01f2-4947-870a-1cdeca1099db" />


3. Definitions

Bias:

The model’s tendency to miss the true relationship between X and Y.

High bias → model is too simple or missing key patterns.

Associated with underfitting.

Example behavior: consistent but wrong predictions (systematic error).

Variance:

The model’s sensitivity to small fluctuations in the training data.

High variance → model overreacts to noise.

Associated with overfitting.

Example behavior: predictions change drastically with small data changes.

4. Visualization (Conceptually)
<img width="1068" height="591" alt="image" src="https://github.com/user-attachments/assets/85ea7853-5e1f-407c-b401-fd1da74824db" />


High Bias, Low Variance: consistent but far from target → misses systematically.

Low Bias, High Variance: sometimes hits target but scattered → unstable predictions.

High Bias, High Variance: worst case → wrong and inconsistent.

Low Bias, Low Variance: ideal case → accurate and consistent predictions.

5. Sources of Model Error
<img width="988" height="615" alt="image" src="https://github.com/user-attachments/assets/3a28aa5e-b4a2-4b81-b9d0-8c55f8a872b9" />


Bias Error – due to wrong model assumptions or missing patterns.

Variance Error – due to excessive model complexity fitting noise.

Irreducible Error – randomness inherent in real-world data; cannot be removed.

Total error = Bias² + Variance + Irreducible error.

<img width="871" height="575" alt="image" src="https://github.com/user-attachments/assets/9f35b202-9422-4658-8f92-c25dd32ad603" />


6. Relationship Between Bias, Variance, and Complexity

As model complexity increases:

Bias decreases (better fit to training data).

Variance increases (less stable, more sensitive to noise).

As model complexity decreases:

Bias increases (misses real patterns).

Variance decreases (more stable but less accurate).

The bias–variance trade-off lies in finding the point of minimum combined error.

7. Key Takeaways

Notes – Supervised Machine Learning (Part 10): Regularization & Model Selection

1. Overview

Goal: use regularization to control model complexity and balance bias and variance.

Regularization helps prevent overfitting — when a model fits the training data too closely but fails to generalize.

This section introduces Ridge, Lasso, Elastic Net, and Recursive Feature Elimination (RFE) as tools for managing complexity and selecting important features.

2. Recap: Complexity vs. Error

Increasing complexity → training error ↓, test error ↑ (overfitting).

Simpler model → higher bias, lower variance (underfitting).

Regularization provides a way to fine-tune complexity without discarding the entire model.

Underfitting → high bias, low variance → overly simplistic model.

Overfitting → low bias, high variance → overly complex model.

The goal is to locate the balance point where total error (bias² + variance) is minimal.

Perfect accuracy is impossible due to irreducible noise in real-world data; good modeling accepts small error for better generalization.


What is Regularization
<img width="1027" height="462" alt="Screenshot 2025-10-04 234926" src="https://github.com/user-attachments/assets/348e6104-57c9-43d1-968a-0ed9666be438" />


In standard training, we minimize a cost function such as Mean Squared Error (MSE):
λ (lambda): regularization strength.

R(w): penalty function based on parameter size.

Larger λ → stronger penalty → simpler model (higher bias, lower variance).

Smaller λ → weaker penalty → more complex model (lower bias, higher variance).

4. Intuition

Notes – Supervised Machine Learning (Part 11): LASSO, Ridge, and Elastic Net Regularization

1. Overview

Introduces LASSO regression as another regularization technique for linear models.

Builds upon Ridge regression — both control model complexity by adding a penalty to the cost function.

The key difference lies in how the penalty is applied:

Ridge uses the squared values of coefficients (L2 norm).

LASSO uses the absolute values of coefficients (L1 norm).

The combination of both forms the Elastic Net, a hybrid regularization method.

2. Ridge (L2) vs. LASSO (L1)
Aspect	Ridge Regression (L2)	LASSO Regression (L1)
Penalty	Sum of squared coefficients	Sum of absolute coefficients
Effect	Shrinks coefficients smoothly	Shrinks some to zero (feature elimination)
Feature Selection	No – keeps all features	Yes – automatically removes some features
Computation Speed	Faster, converges quickly	Slower, due to optimization complexity
Sensitivity to Outliers	More affected (squares large values)	Less affected (absolute values)
3. LASSO: Least Absolute Shrinkage and Selection Operator

Adds a L1 penalty term to the cost function:

<img width="1106" height="518" alt="image" src="https://github.com/user-attachments/assets/7d1b9627-7816-4cfd-b2fa-ab2cb1d6c0cb" />

Larger λ → stronger penalty → smaller (or zero) coefficients.

Behavior:

Small λ → weak penalty → model similar to unregularized linear regression.

Large λ → strong penalty → most coefficients forced toward zero (simpler model).

This selective shrinking results in automatic feature selection, improving interpretability.

4. Ridge Recap (L2 Penalty)

Cost function:

<img width="1099" height="459" alt="image" src="https://github.com/user-attachments/assets/029854e4-92f7-4ad6-b3ee-1d4f952a3fcc" />
​


Penalizes large coefficients more aggressively due to squaring.

Shrinks all coefficients but rarely removes any completely.

More computationally efficient and stable than LASSO.

5. Understanding the Effect of λ (Regularization Strength)


<img width="1168" height="592" alt="image" src="https://github.com/user-attachments/assets/193faf16-fa94-4034-a74b-37e609881e39" />

λ = 0 → no regularization → model fits training data exactly (risk of overfitting).

λ too high → over-regularization → model too simple, high bias.

λ optimal → balances bias and variance → best generalization on the holdout set.

In LASSO, increasing λ rapidly zeroes out weaker features, while Ridge simply scales them down.

6. Multicollinearity Effects

In datasets with correlated predictors:

LASSO tends to pick one variable and drop the rest.

Ridge keeps all but distributes weight among correlated variables.

During tuning, coefficients may fluctuate temporarily as λ increases before stabilizing.

7. Choosing Between Ridge and LASSO

Use Ridge when:

Many small but relevant predictors exist.

You need stable coefficients and fast computation.

Use LASSO when:

You want feature selection or a sparse model.

Interpretability is important.

Trade-offs:

Ridge → smoother shrinkage, better for continuous relationships.

LASSO → simpler, interpretable models, but slower convergence.

8. Elastic Net (Hybrid Approach)

Combines L1 (LASSO) and L2 (Ridge) penalties:

<img width="1332" height="427" alt="image" src="https://github.com/user-attachments/assets/9a4e360e-f606-4378-885e-3ff7558d2dc4" />

Controlled by two parameters:

λ (regularization strength): overall penalty.

α (mix ratio): proportion of L1 vs. L2 contribution.

α = 1 → pure LASSO

α = 0 → pure Ridge

Benefits:

Balances Ridge’s stability with LASSO’s feature selection.

Handles correlated features better than LASSO alone.

Allows fine-tuning via cross-validation to find optimal λ and α.

9. Summary

Regularization controls overfitting by penalizing large coefficients.

Ridge (L2) → smooth coefficient shrinkage.

LASSO (L1) → selective coefficient elimination.

Elastic Net → hybrid model combining benefits of both.

Choosing the right regularization method depends on goals:

Prediction accuracy: use cross-validation to tune λ and α.

Interpretability: LASSO or Elastic Net preferred.

Computation speed: Ridge preferred.

Regularization discourages large coefficients → limits how much each feature can influence predictions.

This reduces model variance and improves generalization to unseen data.

It acts as an automatic complexity control.
