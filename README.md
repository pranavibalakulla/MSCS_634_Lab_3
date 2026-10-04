# Lab 3: Clustering Analysis Using K-Means and K-Medoids

**Course:** MSCS 634 – Your Course Title  
**Author:** Pranavi Balakulla

## Purpose

This lab applies and compares two partition-based clustering algorithms, **K-Means** and **K-Medoids**, on the **Wine dataset** from scikit-learn (`sklearn.datasets.load_wine`). The dataset contains 178 wines described by 13 chemical features, grown by three different cultivators (3 classes).

The work follows four steps:

1. **Load and prepare the data:** explore the features and class distribution, check for missing values, duplicates, and outliers, and standardize the features with z-score normalization.
2. **K-Means clustering** with k = 3.
3. **K-Medoids clustering** with k = 3.
4. **Visualize and compare** the two models using PCA scatter plots and two evaluation metrics:
   - **Silhouette Score**, which measures how compact and well separated the clusters are, without using the true labels.
   - **Adjusted Rand Index (ARI)**, which measures how well the clusters match the true wine classes, corrected for chance.

## Repository Contents

| File | Description |
|---|---|
| `Lab3_Clustering_KMeans_KMedoids.ipynb` | Jupyter Notebook with all code, outputs, visualizations, and analysis |
| `README.md` | This summary |

## Results

| Metric | K-Means | K-Medoids |
|---|---|---|
| Number of Clusters | 3 | 3 |
| Silhouette Score | 0.2849 | 0.2660 |
| Adjusted Rand Index (ARI) | 0.8975 | 0.7263 |
| Wines placed in the wrong cluster | 6 of 178 | 17 of 178 |

## Key Insights

- **K-Means performed better on both metrics.** Its ARI of about 0.90 means its clusters closely match the three wine cultivars. K-Medoids reached 0.73.
- **All of the disagreement is in one class.** Both algorithms clustered `class_0` and `class_2` perfectly. The difference comes from `class_1`, which sits between the other two classes and overlaps with both. K-Means misplaced 6 of the 71 `class_1` wines, while K-Medoids misplaced 17, 14 of them into the `class_0` cluster.
- **Medoids vs. centroids.** K-Means centroids are calculated means and sit at the center of each group. K-Medoids medoids must be real wines (rows 174, 106 and 35), so they are positioned off-center. In the PCA plot, the K-Medoids `class_0` medoid sits closer to `class_1` than the K-Means centroid does, which pulls borderline `class_1` wines into the wrong cluster.
- **The clusters overlap.** Both Silhouette Scores are only around 0.27–0.28. The groups look fairly distinct in the 2-D PCA plot, but that view keeps only about 55% of the total variance (PC1 36.2%, PC2 19.2%). In the full 13-dimensional space, the clusters overlap more.
- **Why K-Means wins here.** After scaling, the Wine data forms compact, roughly round groups, which suits K-Means. There are very few outliers, so K-Medoids' main advantage, robustness to extreme values, does not come into play.
- **When to use each.** K-Means suits large numeric datasets with compact clusters and few outliers. K-Medoids is a better fit when the data is noisy or has many outliers, when a non-Euclidean distance is needed, or when each cluster must be represented by a real example, at the cost of slower computation.

## Challenges and Decisions

- **Data cleaning:** The dataset has no missing values and no duplicate rows. A z-score check found 11 values in 10 rows with |z| > 3. These rows were **kept**, because they are plausible chemical measurements, removing them would shrink a small dataset by about 6%, and outlier sensitivity is one of the differences this lab is meant to examine.
- **Standardization:** The features are on very different scales (for example, `proline` ranges from about 278 to 1680, while `hue` stays between 0.48 and 1.71). Both algorithms use Euclidean distance, so `StandardScaler` was applied to keep any single feature from dominating.
- **Installing K-Medoids:** `KMedoids` is not part of core scikit-learn. It comes from the separate `scikit-learn-extra` package, which had to be installed.
- **Fair comparison:** Both models used the same scaled data, k = 3, Euclidean distance, and `random_state = 42`. K-Means used `n_init = 10` so the best of 10 initializations is kept. K-Medoids used its default `alternate` method and `heuristic` initialization.
- **Visualization:** PCA was used to reduce the data to two dimensions for plotting only; the models were trained on all 13 features. Because cluster numbers are arbitrary, each cluster is colored by the true class most of its members belong to, so the K-Means, K-Medoids, and true-class plots can be compared side by side.

## How to Run

```bash
pip install numpy pandas scikit-learn scikit-learn-extra matplotlib jupyter
jupyter notebook Lab3_Clustering_KMeans_KMedoids.ipynb
```
