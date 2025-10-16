<img width="816" height="546" alt="image" src="https://github.com/user-attachments/assets/8b3b472a-df05-4c11-9747-bd675f502a22" />
Hierarchical Agglomerative Clustering (HAC)

Hierarchical Agglomerative Clustering (HAC) is a bottom-up clustering algorithm that builds a hierarchy of clusters by repeatedly merging the closest pairs of points or clusters until only one large cluster remains—or until a chosen stopping point.

1. Key Idea

HAC starts with each data point as its own cluster.

It then merges the two closest clusters step by step based on a chosen distance metric (e.g., Euclidean, Manhattan, Cosine).

This process continues iteratively, forming larger and larger clusters until:

All points are merged into one single cluster, or

A stopping criterion (e.g., desired number of clusters) is reached.

2. Step-by-Step Process

Initialize: Treat every point as an individual cluster.

Find closest pair: Identify the two clusters (or points) with the smallest distance.

Merge: Combine them into a single cluster.

Recalculate distances: Compute distances between the new cluster and all other clusters.

This depends on a linkage criterion (see below).

Repeat: Continue merging until reaching the desired number of clusters or one final cluster.

3. Linkage Criteria (How Distance Between Clusters Is Defined)

When determining how far apart two clusters are, HAC can use different linkage methods:

Single linkage: Minimum distance between any two points (one from each cluster).

Complete linkage: Maximum distance between any two points.

Average linkage: Mean of all pairwise distances between points in the two clusters.

Centroid linkage: Distance between the centroids (average positions) of the clusters.

The choice of linkage affects the final cluster shapes:

Single linkage → may create “chain-like” clusters.

Complete linkage → prefers compact, spherical clusters.

Average linkage → balances both.

<img width="811" height="497" alt="image" src="https://github.com/user-attachments/assets/64bde95f-bf19-44f8-a17d-89f53743df9e" />
Hierarchical Clustering: Stopping Criteria & Linkage Methods

This section expands on how to decide when to stop merging clusters in hierarchical agglomerative clustering and introduces the main linkage methods used to calculate distances between clusters.

1. Determining When to Stop Merging

In hierarchical clustering, we start by merging the closest points and clusters, but we need a rule for when to stop combining them.

At each step, we can measure the average distance between all points within each cluster.

A threshold (gray line) is set for this average cluster distance.

The algorithm continues merging clusters until all average cluster distances exceed this threshold.

When the minimum average cluster distance rises above the threshold, the algorithm converges — meaning we’ve reached the final clustering structure.

This stopping criterion ensures clusters remain tight and well-separated before merging further.
<img width="844" height="475" alt="image" src="https://github.com/user-attachments/assets/929abdca-d956-467f-91d0-0fb647d1007c" />

2. The Need for Linkage Criteria

When merging clusters, we must define how to measure the distance between two clusters — not just between individual points.
These definitions are called linkage methods, and they greatly affect the shape and structure of the resulting clusters.
| **Linkage Type**     | **Definition**                                                                                             | **Pros**                                                                                                        | **Cons**                                                                                                       |
| -------------------- | ---------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Single Linkage**   | Distance = *minimum pairwise distance* between any two points (one from each cluster).                     | - Captures fine-grained structure.<br>- Good for detecting elongated or irregular clusters.                     | - Sensitive to noise/outliers.<br>- Can produce “chaining effect” (clusters connected by single close points). |
| **Complete Linkage** | Distance = *maximum pairwise distance* between any two points in the clusters.                             | - Produces compact, well-separated clusters.<br>- Less sensitive to noise.                                      | - Can break apart large clusters.<br>- May underestimate cluster similarity.                                   |
| **Average Linkage**  | Distance = *average of all pairwise distances* between points in both clusters.                            | - Balances single and complete linkage.<br>- Reasonably stable.                                                 | - Still somewhat affected by outliers.<br>- May blur cluster boundaries.                                       |
| **Ward Linkage**     | Distance = *increase in total inertia* (sum of squared distances to centroids) if two clusters are merged. | - Minimizes total variance within clusters.<br>- Often yields spherical, compact clusters (similar to K-Means). | - Sensitive to scale and centroid-based assumption (works best with Euclidean distance).                       |


HAC results are often visualized using a dendrogram — a tree-like diagram showing how clusters merge at different distance levels.
By “cutting” the dendrogram at a certain height, we can choose the desired number of clusters (K).
<img width="740" height="476" alt="image" src="https://github.com/user-attachments/assets/d8427aca-cd09-4940-82ce-cb80c3192bde" />
Introduction to DBSCAN (Density-Based Spatial Clustering of Applications with Noise)

DBSCAN is a density-based unsupervised learning algorithm designed to identify clusters of arbitrary shapes and detect outliers (noise) — making it distinct from methods like K-Means that simply partition data.

1. Core Concept

DBSCAN groups together points that are closely packed (dense regions) and marks points that lie alone in low-density regions as noise.

It works well for data that contains outliers or irregularly shaped clusters.

Unlike partitioning methods, DBSCAN can ignore noise instead of forcing every point into a cluster.

2. How DBSCAN Works

Randomly pick a starting point in the dataset.

Check how many points fall within a specified distance (ε, epsilon) around that point — this defines its neighborhood.

If the number of neighboring points is greater than or equal to a minimum number of samples (MinPts), that point becomes a core point.

The algorithm expands the cluster by recursively including all nearby points within ε of any current cluster members.

Points that are within ε of a core point but do not have enough neighbors themselves are called border (density-reachable) points.

Points that are not within ε of any core point are labeled as noise.

The process repeats until all points are classified as either core, border, or noise.
Key Input Parameters
| **Parameter**                    | **Meaning**                                                                               | **Effect**                                                                                                             |
| -------------------------------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Distance Metric**              | Defines similarity between points (e.g., Euclidean, Manhattan, Cosine).                   | Affects cluster shape and boundary.                                                                                    |
| **Epsilon (ε)**                  | The maximum distance between two points for one to be considered a neighbor of the other. | Controls **cluster tightness** — smaller ε → more clusters, larger ε → fewer clusters.                                 |
| **MinPts (N_clu / min_samples)** | Minimum number of points required to form a dense region (including the point itself).    | Controls **cluster density sensitivity** — small values detect smaller clusters, large values require denser clusters. |
 Types of Points in DBSCAN
| **Type**                             | **Definition**                                            | **Role in Clustering**                             |
| ------------------------------------ | --------------------------------------------------------- | -------------------------------------------------- |
| **Core Point**                       | Has ≥ MinPts neighbors within ε distance.                 | Forms the center of a cluster.                     |
| **Border (Density-Reachable) Point** | Lies within ε of a core point but has < MinPts neighbors. | Belongs to a cluster but is not a core.            |
| **Noise (Outlier)**                  | Not within ε of any core point.                           | Ignored by the model, not assigned to any cluster. |

<img width="1093" height="641" alt="image" src="https://github.com/user-attachments/assets/5cdb2f4c-13c4-48e6-9e1c-feea3da00263" />
DBSCAN Visualization, Workflow & Python Implementation

This section visually and practically explains how DBSCAN (Density-Based Spatial Clustering of Applications with Noise) works, how it identifies core, border, and outlier points, and how to implement it using Python.

1. How DBSCAN Works (Step-by-Step Visual Logic)

Start at a random point in the dataset.

Draw a circle around it with radius ε (epsilon) — the distance threshold.

Example: ε = 1.75.

Check neighbors inside the ε-radius.

If a point has at least MinPts (n_clu) neighbors (including itself), it becomes a core point.

All points within ε of a core point are added to the same cluster.

Expand the cluster.
<img width="1032" height="605" alt="image" src="https://github.com/user-attachments/assets/0467f13a-0383-43c4-a1b4-25a3052f2d18" />

Each new point inside the cluster is checked in the same way — if it also has ≥ MinPts neighbors, it becomes another core point.

Points within ε of any core point, even if they are not cores themselves, become border points (density-reachable).

When no more points can be added, start a new cluster from another unvisited point.

Outliers (noise) are any points that do not fall within ε of any core point.

These are labeled as noise and not assigned to any cluster.
| **Type**                             | **Definition**                                   | **Example in Visualization**                     |
| ------------------------------------ | ------------------------------------------------ | ------------------------------------------------ |
| **Core Point**                       | Has ≥ MinPts neighbors within ε.                 | Dark-colored points in the dense region.         |
| **Border (Density-Reachable) Point** | Within ε of a core point but < MinPts neighbors. | Lighter-colored points near cluster edges.       |
| **Noise Point (Outlier)**            | Not within ε of any core point.                  | Gray points — isolated or distant from clusters. |


Mean Shift Clustering Algorithm

The Mean Shift algorithm is the final clustering method covered in the unsupervised learning section. It identifies clusters by shifting centroids toward areas of highest data density, without needing to predefine the number of clusters.

1. Core Idea

Mean Shift is similar to K-Means, but instead of using the mean of assigned points as the cluster center,
it moves each centroid toward the densest region (highest data density) within a given window (bandwidth).

It is a density-based, non-parametric, and model-free algorithm.

2. Step-by-Step Algorithm

Initialize:
Select a random starting point and define a window (bandwidth) that determines neighborhood size.

Compute the weighted mean:

For all points inside the window, calculate the weighted average of their positions.

Points closer to the center get higher weights (using a kernel function like RBF/Gaussian).

Shift the window:
Move the window so its center aligns with this new weighted mean.

Repeat until convergence:
Continue shifting until the mean (centroid) stops moving, meaning the local maximum density (mode) is reached.
<img width="423" height="411" alt="image" src="https://github.com/user-attachments/assets/68ac20e3-1e3d-4d73-a502-f6b7800e898a" />

Repeat for all points:
All points that lead to the same local maximum are grouped into the same cluster.
Kernel Function (Weighting Mechanism)

The kernel assigns importance to points based on their distance from the current mean.

Most common: RBF (Radial Basis Function) or Gaussian kernel.

Points close to the center → higher weight.

Points far away → lower weight.

Mathematically:<img width="304" height="114" alt="image" src="https://github.com/user-attachments/assets/3c98013b-9202-41af-a0da-0742afccbde5" />
Where K is the kernel function, and m(x) is the new shifted mean.
<img width="1002" height="589" alt="image" src="https://github.com/user-attachments/assets/0205745e-ac98-4ad6-9301-72a7367fbd1a" />

Comparison of All Clustering Algorithms

This final section reviews and compares the main clustering algorithms covered — K-Means, Mean Shift, Hierarchical (Ward), and DBSCAN — including their advantages, limitations, scalability, and best use cases in real-world business and data applications.
<img width="1035" height="506" alt="image" src="https://github.com/user-attachments/assets/d1c27725-69c7-4af3-aa42-c7de11cf656a" />
