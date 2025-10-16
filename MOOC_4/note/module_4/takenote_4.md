Introduction to Dimensionality Reduction & PCA (Part 1)

This section introduces a new branch of unsupervised learning called dimensionality reduction, focusing on reducing the number of features (dimensions) in a dataset while preserving as much useful information as possible.
<img width="989" height="609" alt="image" src="https://github.com/user-attachments/assets/747388fb-333f-4a93-a071-3ba882cae1d2" />
1. Why Dimensionality Reduction Matters

Real-world business and enterprise datasets often have many features (high-dimensional data).

As the number of dimensions increases, we encounter the Curse of Dimensionality — meaning:

Distance metrics become less meaningful.

Outliers become more frequent.

Models may perform worse, not better.

Computational cost increases exponentially.
Example (Intuitive Explanation):
If one dimension has 10 possible positions:

To fill 60% of that space → only 6 observations are needed.

In 2D (10×10 grid) → need 60 observations.

In 3D → need 600 observations.
2. Goals of Dimensionality Reduction

Dimensionality reduction helps to:

Simplify models and reduce noise.

Improve interpretability and visualization.

Enhance computational efficiency.

Preserve the core structure and variance of the data.

Two main strategies:

Feature Selection: Keep only the most important original features.

Feature Extraction / Transformation: Combine or transform existing features into new ones (e.g., PCA, NMF).

3. Introducing PCA (Principal Component Analysis)

PCA = a linear transformation technique that reduces dimensions by creating new features (called principal components) — each being a weighted combination of the original features.
Example:

Suppose we have two correlated features:
 Phone usage

 Data usage
They form a diagonal line in 2D space — meaning one can almost predict the other.

Step-by-step intuition:

Find correlation: The two features are highly correlated, so they contain overlapping information.

Project onto a line: Draw a line through the points that captures the direction of maximum variance.

Compute projections: Project all points onto that line — this becomes the new 1D feature.

Result:

Reduced from 2D → 1D.

Maintains the most important information (maximum variance).

This projection process generalizes:

From 3D → 2D, or

From 100D → 10D, etc.
4. Conceptual Summary of PCA
| **Concept**             | **Explanation**                                                            |
| ----------------------- | -------------------------------------------------------------------------- |
| **Purpose**             | Reduce feature count while keeping most information.                       |
| **Transformation Type** | Linear (projects data onto new axes).                                      |
| **Output**              | New features = *Principal Components* (combinations of original features). |
| **Selection Rule**      | Choose components that retain the most **variance** in the data.           |
| **Result**              | Fewer dimensions, but similar data structure and interpretability.         |
<img width="923" height="501" alt="image" src="https://github.com/user-attachments/assets/f2143a82-d759-407d-af59-e572bb7ab38d" />
How PCA Works (Linear Principal Component Analysis)

This section explains how PCA (Principal Component Analysis) mathematically reduces dimensionality by projecting data onto new axes (principal components) that capture the maximum variance in the dataset.
<img width="654" height="414" alt="image" src="https://github.com/user-attachments/assets/1fd58f08-07a8-4c7a-b5e2-76e19061a45d" />
1. From Two Features → One Principal Component

Starting from two correlated features (e.g.,  phone usage and  data usage),
PCA projects the data onto a new single axis that captures the most variance.

This projection reduces the feature space from 2D → 1D, while keeping most of the information.

The same principle scales to higher dimensions — e.g., projecting 100 features → 10 key components.
2. Finding the Right Axes (Principal Components)

To mathematically find these axes, PCA uses linear algebra — specifically, Singular Value Decomposition (SVD).

Key Idea:

The direction of maximum variance is the first principal component (v₁).

The second component (v₂) is orthogonal (perpendicular) to the first and explains the next highest variance.

Each new component is orthogonal to all previous ones.

So, if you imagine your dataset spread across a plane:

Projecting onto v₁ preserves most of the information.

Projecting onto v₂ would lose information because variance in that direction is small.
3. The Math Behind PCA – Singular Value Decomposition (SVD)
The dataset 
A (size 𝑚×𝑛) can be decomposed as:<img width="166" height="47" alt="image" src="https://github.com/user-attachments/assets/3fd0791c-5558-4646-b71e-1d40808ee977" />
| **Matrix** | **Meaning**                                   | **Shape**      | **Role**                                        |
| ---------- | --------------------------------------------- | -------------- | ----------------------------------------------- |
| ( U )      | Left singular vectors (rotation in m-space)   | ( m \times m ) | Helps align rows                                |
| ( S )      | Diagonal matrix of singular values            | ( m \times n ) | Represents *importance* (variance strength)     |
| ( V^T )    | Right singular vectors (principal directions) | ( n \times n ) | Defines new feature axes (principal components) |
The larger the singular value in 
𝑆
S, the more variance that component explains.
For example:
If S=[9,5,2], then:

The first component (v₁) explains the most variance.

The second (v₂) explains some.

The third (v₃) adds little new information.

Summary
Dimensionality Reduction
As a result of the curse of dimensionality, too many features can lead to worse performance. Often, data can be represented by fewer dimensions (features). There are two ways to reduce dimensionality:

Select a subset of features that are "important"

Combine features using linear/non-linear transformations

Principal Component Analysis
Principal component analysis (PCA) is a dimensionality reduction technique that creates new features by applying linear transformations on a combination of the original features. The resulting features are called principal components, on which the original data will be projected.

Each principal component is a vector and are orthogonal to each other. Their relative importance is determined by comparing how much of the variance within the original data they each explain/preserve. 

Singular value decomposition (SVD) enables us to find this information by obtaining the diagonal matrix. Its non-zero entries along the diagonal represent each eigenvector(principal component)'s eigenvalue/length. The bigger the value, the more important the vector.

*Note: It is important to scale the data prior to applying PCA because distance is an important aspect considered for the algorithm.

 Syntax
 The syntax consists of importing the class containing the method:

   from sklearn.decomposition import PCA

 creating the instance of the class:

    pca=PCA(n_components=3)

and fit the instance and create a transformed version of the data:

   X_trans=pca.fit_transform(X_train)  

