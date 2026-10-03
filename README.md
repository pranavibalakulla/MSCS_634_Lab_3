# Lab 3 -- Clustering: K-Means and K-Medoids

## Purpose

The purpose of this lab was to implement and compare two clustering
algorithms, K-Means and K-Medoids, using a dataset with three target
classes. The analysis used Python and Jupyter Notebook to prepare and
scale the data, perform clustering with **k = 3**, and evaluate the
resulting clusters using the **Silhouette Score** and **Adjusted Rand
Index (ARI)**. The final step used PCA to create side-by-side
two-dimensional visualizations of the clusters and their centroids or
medoids.

## Key Insights

Both algorithms successfully produced three clusters, but their results
were different. K-Means produced a **Silhouette Score of 0.2849** and an
**ARI of 0.8975**, while K-Medoids produced a **Silhouette Score of
0.2660** and an **ARI of 0.7263**. The results show that the K-Means
cluster assignments had higher agreement with the known class labels and
slightly stronger cluster separation for this dataset.

The PCA visualizations showed three broad groups in the data. The
K-Means centroids were positioned near the centers of their respective
groups, whereas the K-Medoids representatives were actual observations
from the dataset. Some observations were assigned differently by the two
algorithms, particularly near the boundaries between groups. These
differences demonstrate how the choice of clustering method can affect
cluster membership and the location of representative points.

## Challenges and Decisions

One challenge was ensuring that the clustering algorithms were applied
consistently to the same scaled dataset so that the comparison would be
meaningful. A fixed `random_state = 42` was used for both algorithms to
improve reproducibility. K-Means was configured with three clusters and
`n_init = 10`, while K-Medoids was configured with three clusters,
`random_state = 42`, and Euclidean distance.

Another decision was to use PCA to reduce the scaled dataset to two
dimensions for visualization. This made it possible to display both
clustering results side by side while marking the K-Means centroids and
K-Medoids medoids. The same Silhouette Score and ARI metrics were
calculated for both algorithms to provide a consistent basis for
comparison.

## Final Results

  Metric                        K-Means   K-Medoids
  --------------------------- --------- -----------
  Number of Clusters                  3           3
  Silhouette Score               0.2849      0.2660
  Adjusted Rand Index (ARI)      0.8975      0.7263

Overall, the lab demonstrated the practical differences between
centroid-based K-Means clustering and medoid-based K-Medoids clustering.
For the dataset and configuration used in this lab, K-Means produced
higher values for both evaluation metrics, while K-Medoids provided
cluster representatives that correspond to actual observations in the
dataset.
