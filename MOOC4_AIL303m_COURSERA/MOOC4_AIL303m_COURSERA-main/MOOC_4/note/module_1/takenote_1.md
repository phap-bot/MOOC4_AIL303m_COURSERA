Introduction to Unsupervised Learning

Definition:
Unsupervised learning refers to algorithms that work without labeled outcomes, aiming to discover hidden structures or natural groupings within data.

Main Categories:
<img width="893" height="419" alt="image" src="https://github.com/user-attachments/assets/ebeead75-23c0-4e2d-a52b-c7aec64a2306" />

Clustering: Divides data into groups based on similarity.

Dimensionality Reduction: Reduces the number of features while preserving most information.

Key Algorithms:

Clustering: K-Means, Hierarchical, DBSCAN, Mean Shift.

Dimensionality Reduction: PCA, NMF.

Curse of Dimensionality:
When the number of features increases:

Noise and spurious correlations appear.

More data is required to maintain coverage.

Computation slows down and outliers increase.

Solution:
Apply dimensionality reduction to:

Common Use Cases of Unsupervised Learning (Clustering & Dimensionality Reduction)
<img width="815" height="511" alt="image" src="https://github.com/user-attachments/assets/1cfc0594-0d70-4df4-b925-0d7f71036586" />

Clustering – Main Applications:

Classification for Unlabeled Data:
Used when class labels are missing — helps group similar items (e.g., detect spam or review types).

Anomaly Detection:
Identifies unusual patterns, such as irregular credit card transactions that may indicate fraud.

Customer Segmentation:
Groups customers by behavior or demographics (e.g., visit frequency, spending habits, life stage) to guide marketing strategies.

Improving Supervised Models:
Clustering can divide data into subgroups; separate models trained on each segment can improve prediction accuracy.

Dimensionality Reduction – Main Applications:

Commonly used in image processing and computer vision to compress high-resolution images while retaining key information.

PCA (Principal Component Analysis) helps remove noise, extract essential features, and speed up computations.
<img width="853" height="517" alt="image" src="https://github.com/user-attachments/assets/7f971ecc-ad49-4651-ba09-f2083c9ed787" />

Simplify models and avoid overfitting.

Improve speed and interpretability.

Introduction to Clustering Example
<img width="768" height="456" alt="image" src="https://github.com/user-attachments/assets/5119eaf4-ced5-47e2-89b2-129dec2857a7" />


To introduce the idea of clustering, we begin with a simple example:
A company wants to segment its customers using one feature — the number of visits to the website.

By applying clustering, we can divide these customers into groups based on their visit frequency:

If we choose two clusters, the data splits into two distinct groups — for example, low-activity and high-activity users.

If we select three clusters, we may get an additional medium-activity group.

Similarly, choosing five clusters would divide the data into even smaller, more specific segments.

The visual separation of these groups is intuitive, but the goal of clustering is to formalize this grouping mathematically and algorithmically, allowing a model to determine the best cluster boundaries automatically.

In upcoming lessons, we will:

Learn how clustering algorithms work internally,

Understand how to decide the appropriate number of clusters (K),
Introduction to the K-Means Algorithm
<img width="883" height="568" alt="image" src="https://github.com/user-attachments/assets/5f79365f-d00f-4221-a046-deb97bbd380d" />


K-Means is one of the most widely used unsupervised learning algorithms for clustering. It groups data points into a predefined number of clusters (K) based on feature similarity.

In this example, we use two features — number of visits and recency (how recently a customer visited).
Visually, the data appears to form two clusters, but K-Means helps us find these clusters algorithmically through an iterative process.
<img width="869" height="554" alt="image" src="https://github.com/user-attachments/assets/60a18a80-d3dd-4901-92e9-eb2fd15b4e1a" />

How K-Means Works: Step by Step

Initialization:
Choose K random points as initial centroids (cluster centers).
Example: two centroids for K=2 — one pink, one blue.

Assignment Step:
For each data point, calculate the distance (usually Euclidean) to each centroid and assign it to the nearest cluster.
<img width="926" height="517" alt="image" src="https://github.com/user-attachments/assets/c044cc32-527b-468e-a5e8-31b30d14a653" />

Update Step:
Recalculate the centroid position for each cluster by taking the mean of all points within that cluster.

Iteration:
Repeat the assignment and update steps until cluster assignments no longer change — this is called convergence.

Key Points

Convergence:
Occurs when centroids stop moving; clusters are now stable.

Multiple Solutions:
K-Means is sensitive to initial centroid positions — different random starting points can lead to different final clusters (local minima).

Scalability:
The process can be extended to more clusters (e.g., 3 or 5), but the algorithm’s effectiveness depends on choosing an appropriate value for K.

Improving K-Means Initialization (K-Means++)<img width="885" height="522" alt="image" src="https://github.com/user-attachments/assets/38497786-321a-4cf7-bed9-200ae8ef22db" />


When running the K-Means algorithm, we may get different cluster results each time.
This happens because the algorithm starts with random initial centroids, and different starting points can lead to different final groupings (local optima).

To address this issue, we need:

A method to evaluate which clustering result is best.

A smarter initialization strategy to improve convergence and avoid poor solutions.

Problem: Random Initialization

Randomly chosen centroids can start too close to each other.

When this happens, clusters can overlap or converge to non-optimal boundaries.

Solution: K-Means++ Initialization

K-Means++ improves centroid initialization by spreading them out before starting iterations.

Steps:<img width="922" height="532" alt="image" src="https://github.com/user-attachments/assets/6a06b781-b0b3-4e6a-87f4-193fe531d8cb" />


Choose the first centroid randomly.

For the next centroid, compute the distance squared from each data point to the nearest chosen centroid.

Select the next centroid with probability proportional to that squared distance — points farther away are more likely to be chosen.

Repeat this process until K centroids are selected.

Each new centroid is chosen to be far from all previously selected centroids (using the minimum distance rule).

This ensures that:

Centroids start far apart.

The algorithm is less likely to get stuck in a local optimum.

Results are more stable and accurate across runs.

And start with our first algorithm: K-Means Clustering.
General Workflow:
Unlabeled data → Fit unsupervised model → Extract structure or clusters → Apply to new data.
Choosing the Right Number of Clusters (K) in K-Means

After understanding how K-Means works, the next key question is:
👉 How do we choose the correct number of clusters (K)?
<img width="740" height="351" alt="image" src="https://github.com/user-attachments/assets/950706d4-74f6-42e8-bd69-a6aa6e3e6972" />

1. Fixed Number of Clusters

Sometimes, K is predetermined by business or technical needs:

Example: A computer with 4 cores → set K = 4

A company wants 10 customer groups for marketing → K = 10

A research interface divides topics into 20 categories → K = 20

However, in many real-world cases, the optimal number of clusters is unknown, so we must estimate it using evaluation metrics.

2. Metrics for Evaluating Cluster Quality
(a) Inertia

Definition: The total sum of squared distances between each point and its assigned cluster centroid.

Measures how tightly the points are grouped around their centroids.

Lower inertia = better clustering (tighter, more compact groups).

Drawback: Inertia increases automatically as more points are added, even if those points fit well.

(b) Distortion

Definition: The average of squared distances from points to their cluster centroid.

Also favors tighter clusters but is not sensitive to the number of points.

Useful when similarity between points within clusters matters more than equal cluster size.

In short:

Use inertia if you want clusters of similar size.

Use distortion if you care more about internal similarity.

Using Inertia & the Elbow Method to Choose K in K-Means
<img width="890" height="528" alt="image" src="https://github.com/user-attachments/assets/9ce3db99-422d-4d9d-9593-bc47fc02a4e5" />


Once we understand inertia and distortion, we can use them to determine the optimal number of clusters (K) in K-Means through a method called the Elbow Method.

1. Why We Need the Elbow Method

As we increase K, the inertia (or distortion) — which measures the average distance of points to their cluster centroids — will always decrease.

This happens because more clusters mean smaller groups, and points are naturally closer to their centroids.

In the extreme case where each point is its own cluster, the inertia becomes 0, which is meaningless.

So, we need a way to find the balance point — where adding more clusters doesn’t significantly improve the fit.

2. The Elbow Method

We plot number of clusters (K) on the x-axis and inertia/distortion on the y-axis.

As K increases, the curve drops sharply at first, then levels off.

The “elbow point” — where the rate of decrease slows dramatically — indicates the optimal K.
This is where we achieve a good balance between model accuracy and simplicity.

🧠 Interpretation:

Before the elbow → adding clusters greatly improves the model.

After the elbow → improvement becomes marginal, so extra clusters only add complexity.

Both inertia and distortion can be used for this:

Inertia favors balanced cluster sizes.

Distortion focuses on similarity within clusters.

<img width="883" height="528" alt="image" src="https://github.com/user-attachments/assets/d1b9ae8a-565a-4dc9-a061-a3502a2f78aa" />
