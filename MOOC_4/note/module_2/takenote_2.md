Understanding Distance Metrics in Clustering (Part 1)

Clustering algorithms depend heavily on how we define the distance (or similarity) between data points.
This section introduces several distance metrics and explains when and why to use each one.
Learning Goals

In this topic, we focus on:

Understanding different distance measures used in clustering.

Knowing how these distances affect algorithm behavior and outcomes.

Exploring use-cases for each type of metric.

1. Why Distance Matters
<img width="859" height="503" alt="image" src="https://github.com/user-attachments/assets/98f27b56-53bf-4da8-bda4-7e80a44c74c4" />

All clustering methods — like K-Means, DBSCAN, or hierarchical clustering — depend on measuring how “close” or “similar” points are.
The choice of distance metric directly influences:

How clusters are formed,

How compact or separate they are,

And how the algorithm interprets relationships in the data.

Sometimes, the right metric must be found through empirical testing to see which gives the best performance.

2. Euclidean Distance (L2 Norm)

The most intuitive and common metric (used in K-Means).

Measures the straight-line distance between two points.

Formula:

<img width="147" height="61" alt="image" src="https://github.com/user-attachments/assets/f801b060-6f28-4338-a9f9-2db427bd2409" />


It can be extended to more dimensions by squaring the difference for each feature, summing, and taking the square root.

Works well in low-dimensional spaces where relationships between points are geometric and continuous.

3. Manhattan Distance (L1 Norm)

Also known as the city-block distance — you move along grid-like paths rather than diagonally (like city streets).

Formula:
d=∣x1−x2∣+∣y1−y2∣

Always greater than or equal to Euclidean distance unless points lie on the same axis.

Performs better than Euclidean in high-dimensional datasets, where traditional distance measures struggle to distinguish between points (a problem called the “curse of dimensionality”).
<img width="979" height="631" alt="image" src="https://github.com/user-attachments/assets/f9dee027-14d2-4ac8-b9ac-791da0ccfcc7" />
Cosine and Jaccard Distance Metrics in Clustering

This section introduces two less intuitive but highly useful distance metrics — Cosine Distance and Jaccard Distance — and explains when each should be used.

1. Cosine Distance (or Cosine Similarity)

Focuses on the angle between vectors, not the magnitude (length).

Measures how similar two points are in direction, regardless of their scale or distance from the origin.

Formula (for two vectors A and B):

Cosine Similarity
<img width="384" height="88" alt="image" src="https://github.com/user-attachments/assets/75158f19-e200-4ae6-9718-a3b82762d0cf" />
→ Cosine Distance = 1 − Cosine Similarity
Key Properties

Insensitive to scale:
Moving a point further from the origin (along the same line) does not change its cosine distance.
→ Two points on the same ray from the origin have distance = 0.

Captures direction, not magnitude:
Two points with proportional features (like 3× larger values) are treated as identical in orientation.

Best for text or word-frequency data:
Example:

Document A: 3 counts of “data science”, 10 of “application”

Document B: 30 of “data science”, 100 of “application”
→ Cosine distance treats them as very similar because their ratio (direction) is the same.

Advantage:
Works well in high-dimensional spaces (like NLP or embeddings) where Euclidean distance loses interpretability due to the curse of dimensionality.

2. Jaccard Distance

Measures dissimilarity between sets.

Often used for text, keywords, or categorical data, where features are presence/absence-based.

Formula:<img width="359" height="84" alt="image" src="https://github.com/user-attachments/assets/c9339b48-0c91-4170-8faa-2e7da995c4ba" />
→ The more overlap (shared elements), the smaller the distance.

Example:
Sentence A: “I like chocolate ice cream”
→ Set A = {I, like, chocolate, ice, cream}
Sentence B: “Do I want chocolate cream or vanilla cream”
→ Set B = {do, I, want, chocolate, cream, or, vanilla}
Intersection = {I, chocolate, cream} (3 words)
Union = 9 unique words


