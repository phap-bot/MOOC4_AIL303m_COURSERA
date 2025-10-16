Notes – Supervised Machine Learning (Part 12): Intuitive Understanding of Regularization

1. Purpose of This Section

Develop an intuitive grasp of how regularization works beyond the math.

Three complementary perspectives:

Analytical view – how penalties restrict coefficient size and reduce complexity.

Geometric view – why LASSO zeros out coefficients but Ridge does not.

Probabilistic view – how regularization relates to assumptions about coefficient distributions (Bayesian perspective, to be covered later).

2. Analytical View – Shrinking Coefficients

Regularization adds a penalty term to the cost function, forcing coefficients to become smaller.

Smaller coefficients → smaller effect of features → simpler model with lower variance.

Intuition:

Large coefficients → high sensitivity (small change in X causes large change in prediction).

Small coefficients → low sensitivity → more stable predictions.

Restricting coefficient magnitude limits the range of possible solutions, improving generalization.

If coefficients approach zero, that feature contributes little to predicting Y.

3. Geometric View – Why LASSO Zeros Out Coefficients
<img width="997" height="581" alt="image" src="https://github.com/user-attachments/assets/09649656-b539-4014-b9c5-cb0eaea5ce7c" />


Optimization reframed:

Minimize OLS error (sum of squared residuals)
subject to a constraint on coefficient size.
<img width="1227" height="462" alt="image" src="https://github.com/user-attachments/assets/822af4ce-c8ab-4c65-94d1-1dba2d1ff7cb" />

The optimal solution occurs at the intersection of:

The OLS cost function contours (ellipses of equal error).

The regularization constraint (circle for Ridge, diamond for LASSO).

4. Intuitive Explanation of the Geometry
<img width="1100" height="594" alt="image" src="https://github.com/user-attachments/assets/8c316a0c-5829-46e3-b0a0-7f59107de413" />

For Ridge:

The intersection can occur anywhere on the circular boundary.

Coefficients are reduced but rarely become exactly zero.

Effect: smooth shrinkage of all parameters.

For LASSO:

The diamond has sharp corners (where one coefficient = 0).

The OLS contour is likely to touch one of those corners → one coefficient becomes zero.

Effect: feature elimination — LASSO tends to produce sparse models.

In higher dimensions, this same logic holds: corners correspond to multiple coefficients being zero.

5. Relation Between Complexity and Regularization

Both Ridge and LASSO restrict how large coefficients can be → limit complexity.

As regularization strength (λ) increases:

Coefficients shrink toward zero.

Variance decreases.

Bias increases.

The goal is to find the λ that gives the lowest total error on the holdout set (balance between bias and variance).

6. Summary

Analytical view: penalizes coefficient magnitude → simpler model.

Geometric view: explains why LASSO sets coefficients to zero (sharp edges of constraint region).

Ridge → circular constraint → shrinks all coefficients smoothly.

Notes – Supervised Machine Learning (Part 13): Probabilistic View of Regularization

1. Overview

This section provides a Bayesian interpretation of regularization.

Regularization can be viewed as imposing prior distributions on model coefficients before fitting them to data.

By defining these priors, we express prior beliefs about how large or small coefficients should be — usually centered around zero.
<img width="1196" height="567" alt="image" src="https://github.com/user-attachments/assets/1270474a-bd20-4216-9743-7af5e28ca037" />
3. Priors for Ridge and LASSO
Regularization	Prior Distribution on Coefficients	Effect on Model
Ridge (L2)	Gaussian (Normal)	Coefficients likely near 0 but can vary smoothly — shrinkage
LASSO (L1)	Laplacian (Double Exponential)	Strong peak at 0 → encourages exact zeros → feature elimination

Both distributions are centered at zero, implying that most coefficients are small or zero.

LASSO’s sharper peak means it’s more likely to force coefficients exactly to zero → sparse model.

Ridge’s smooth bell shape allows coefficients to remain small but nonzero → continuous shrinkage.

4. Relationship Between λ (Lambda) and Variance

λ acts as a regularization strength and is related to the variance of the prior distribution:

Higher λ → smaller variance → tighter distribution → coefficients closer to zero → simpler model.

Lower λ → larger variance → coefficients allowed to vary more → more complex model.

So increasing λ reduces variance but increases bias.

5. Summary of Regularization Insights
Perspective	Key Idea	Outcome
Analytical View	Smaller coefficients → simpler model → lower variance	Controls model sensitivity
Geometric View	LASSO’s diamond constraint zeros out coefficients; Ridge’s circle only shrinks	Explains why LASSO performs feature selection
Probabilistic View	Regularization = imposing priors on coefficients	Connects to Bayesian reasoning

Regularization helps manage the bias–variance trade-off:

Adds bias (simplifies the model).

Reduces variance (improves generalization).

The goal is to find the right balance where both training and test errors are low.
<img width="871" height="397" alt="image" src="https://github.com/user-attachments/assets/7e1a87d0-a47e-446d-98be-d088ae3d1ece" />



LASSO → diamond constraint → zeros out some coefficients entirely.

Regularization reduces overfitting and improves generalization by controlling how much each feature can influence predictions.
