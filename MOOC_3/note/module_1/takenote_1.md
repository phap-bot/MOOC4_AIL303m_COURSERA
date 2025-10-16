Machine Learning (ML) Overview

Machine Learning (ML) allows computers to learn from data rather than relying on explicitly programmed instructions.

In traditional statistics, we understand the underlying process → we can build a model that fits it.

In machine learning, the process is often unknown or too complex → the algorithm learns the relationship from data (function approximation).

<img width="474" height="339" alt="image" src="https://github.com/user-attachments/assets/80b792ee-7674-4120-8df1-eb9d0a2b19bd" />


Caption: Comparison between traditional modeling and machine learning — ML learns patterns directly from data.

Artificial Intelligence (AI) – broader concept

Based on Russell & Norvig’s four quadrants:

Rows: thinking vs acting
Columns: human-like vs rational

Machine Learning fits in the “thinking” area (machines that learn → can reason, decide, act).

Depending on the goal:

Marketing → simulate human thinking (how people react).

Supply chain → aim for rational thinking (optimize decisions).
<img width="474" height="266" alt="image" src="https://github.com/user-attachments/assets/3d8a0843-612b-4779-8003-0e0edfe122de" />

Caption: Russell & Norvig’s AI framework – where Machine Learning fits among “thinking” systems.

Key Idea – Learning as the Core

“Learning” is the foundation of all intelligent behavior — from decision-making to perception and reasoning.

<img width="474" height="330" alt="image" src="https://github.com/user-attachments/assets/b737f531-11f8-4bba-8195-2d1a78c8b1e5" />


Caption: The learning cycle – Data → Train → Predict → Improve.

Model Concept

A model is a simplified representation of something larger (like a map of a territory).

A good model:

Omits unimportant details.

Keeps essential relationships and structures.

Balances complexity reduction and information preservation.

Example: a map shows borders and water bodies but not every landmark — enough to understand spatial relations.

<img width="474" height="275" alt="image" src="https://github.com/user-attachments/assets/d43eb2f8-1826-4414-8f49-bd07a18b7b17" />


Caption: A model captures the key structure of reality while omitting unnecessary complexity.

Applications of ML in Daily Life

Spam filtering (classify emails).

Web search ranking.

Route optimization (logistics).

Fraud detection.

Movie recommendation systems.

Many more — increasingly common and ongoing.
1. Parameters vs. Hyperparameters

Parameters (fit parameters):
→ Values learned directly from data during training (e.g., regression coefficients β₀, β₁, … in linear regression).

Hyperparameters:
→ Settings chosen before training that control the model’s behavior (e.g., learning rate, tree depth, number of neighbors).
→ Not learned from data, but they affect how the model learns.

2. Two Main Types of Supervised Learning

Regression: Predict numeric / continuous outcomes.
→ Examples: stock prices, box office revenue, geographic coordinates.

Classification: Predict categorical outcomes.
→ Examples:

Face recognition → which person?

Customer churn → churn or not churn?

Next word prediction → which word next?

3. Supervised Learning Framework

Equation structure:

<img width="1602" height="734" alt="image" src="https://github.com/user-attachments/assets/a7182244-8a58-4548-9e7c-9fe4292b0363" />


X: Input features.

Ω (Omega): Model parameters (learned).

f(·): The ML model (e.g., linear regressor, decision tree).

yₚ: Predicted output.

The goal is to learn parameters Ω that best map X → y.

4. Training Process

Use past (labeled) data → find parameters that best fit.

Each training sample (Xᵢ, yᵢ) helps the model learn the mapping.
<img width="1710" height="974" alt="image" src="https://github.com/user-attachments/assets/48804ace-8743-4615-b05c-7e43b4769e80" />


More data → better estimation of underlying patterns.

After training → use model on new, unseen data for prediction.

5. Avoiding Overfitting

Don’t train on all historical data → model may memorize specific cases (e.g., “Customer named Daniel Mandel will churn”).

Split dataset:

Training set → learn parameters.

Test/Validation set → check generalization ability.

Goal: balance between fitting past data and generalizing to future data.

6. Loss Function and Optimization

Loss function (J(y, yₚ)) → measures how far prediction yₚ is from actual y.

Training = minimizing loss (i.e., reducing prediction error).

Optimization algorithm updates parameters Ω to minimize J.
→ Example: Gradient Descent.

Interpretation vs. Prediction

In supervised learning, there are two main approaches:
→ Interpretation: understanding the mechanism and relationships between variables.
→ Prediction: focusing on maximizing predictive accuracy, even if the model is less interpretable.

1. When the goal is Interpretation

Objective: gain insights from data — understand which features influence the outcome the most.

Focus on model parameters to interpret how the system behaves.

Usually prefer simpler, more transparent models (e.g., linear regression, logistic regression, shallow decision trees).

Optimize for interpretability, not necessarily the best predictive score.

Examples:

Analyzing customer demographics to understand factors affecting loyalty.

Identifying which safety features reduce accidents most effectively.

Evaluating how marketing budget impacts movie revenue.

2. When the goal is Prediction

Focus on how well predictions match actual values (ŷ vs. y).

Evaluate using performance metrics (accuracy, precision, recall, RMSE, etc.).

Interpretability is less important — models may become “black boxes” (e.g., deep learning).

Goal: get the most accurate prediction, even if we don’t fully understand why it works.

Examples:

Predicting whether a customer will churn.

Predicting credit default risk.

Forecasting future purchases based on transaction history.

3. Trade-off: Interpretability vs. Predictive Power

Simple models → easier to explain but often less accurate.

Complex models → higher predictive performance but harder to interpret.

The choice depends on the business objective:

If decisions require reasoning and justification → prioritize interpretability.

If accuracy is the main goal → prioritize prediction.
<img width="1102" height="508" alt="image" src="https://github.com/user-attachments/assets/b3adc5b2-2552-4596-bf99-141cdc381bbf" />

Notes – Supervised Machine Learning (Part 4): Linear Regression

1. Introduction
<img width="1060" height="473" alt="image" src="https://github.com/user-attachments/assets/230e10ec-e12e-40d0-b3ad-61f6fe352e72" />


First model in supervised learning: Linear Regression.

Learning goals:

Understand how linear regression is built.

Learn how coefficients are chosen to fit data.

Understand how error (loss) is measured — especially Mean Squared Error (MSE).

2. Example: Predicting Movie Revenue from Marketing Budget

Dataset: each movie has

Input (X): marketing budget

Target (Y): box office revenue

Goal: find the best-fit line

<img width="509" height="367" alt="image" src="https://github.com/user-attachments/assets/f5db9988-e428-4418-bc8c-c83f49bd3a24" />

where

β₀ (intercept): revenue when marketing = 0

β₁ (slope): how much revenue increases per extra dollar spent on marketing

We choose β₀ and β₁ to minimize the total error between predicted and actual Y.

Error (residual):
<img width="1102" height="401" alt="image" src="https://github.com/user-attachments/assets/4dd58cc6-3621-4053-b47c-eae470a95eeb" />

	​


It measures the distance between a data point and the fitted line.

The “best” line is the one with smallest total distance between all actual points and the line.

4. Measuring Error

Error can be positive or negative → need a measure of magnitude (distance).

Two main norms:

L1 norm: absolute error (|ŷ − y|)

L2 norm: squared error ((ŷ − y)²)

Linear regression typically uses L2 norm → Mean Squared Error (MSE):

𝑀

Sometimes written as
<img width="1014" height="400" alt="image" src="https://github.com/user-attachments/assets/6230d5e1-10cb-4523-817d-c05d3c3e9d7d" />


The ½ term simplifies derivative calculations, but both forms are equivalent in optimization.
