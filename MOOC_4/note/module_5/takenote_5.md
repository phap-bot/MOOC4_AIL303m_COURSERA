Nonlinear Dimensionality Reduction: Kernel PCA & Manifold Learning

This section expands PCA beyond linear transformations — introducing Kernel PCA and Manifold Learning techniques that handle nonlinear data structures, preserving relationships or geometry that standard PCA would lose.
1. Why Move Beyond Linear PCA?

Traditional PCA only works with linear relationships.
<img width="870" height="563" alt="image" src="https://github.com/user-attachments/assets/829a0d73-f666-4980-9dce-975fd4385713" />


Many real-world datasets contain nonlinear patterns (curves, spirals, clusters).

When PCA is applied directly, it fails to preserve variance or structure in nonlinear data.
Example:
A curved dataset (like a spiral) projected linearly will flatten and lose key relationships
2. Introducing Kernel PCA (kPCA)

Goal: Use kernel functions to perform nonlinear transformations before applying PCA.

How It Works

Apply a kernel function to map the original nonlinear data into a higher-dimensional space.

In that space, the data becomes linearly separable.

Perform standard PCA to project it down into a lower-dimensional space, without losing curvature information.

This approach mirrors the idea behind Support Vector Machines (SVMs) — where kernels are used to handle nonlinearity.
| **Kernel**                               | **Usage**                                  |
| ---------------------------------------- | ------------------------------------------ |
| `linear`                                 | Same as standard PCA                       |
| `poly`                                   | Adds polynomial curvature                  |
| `rbf` (Radial Basis Function / Gaussian) | Captures complex nonlinear relationships   |
| `sigmoid`                                | Works for certain activation-like mappings |
3. Manifold Learning – Nonlinear Dimensionality Reduction Techniques

Unlike PCA (which preserves variance), manifold learning preserves geometric or neighborhood structure in the data.

A. Multidimensional Scaling (MDS)

Preserves pairwise distances between points, not variance.

For example, mapping a 3D sphere to a 2D disk while maintaining relative distances.
