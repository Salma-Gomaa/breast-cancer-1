# Clustering Mini Project — Breast Cancer & Insurance Datasets

A Jupyter notebook covering the full clustering workflow — reading,
preprocessing, feature selection, K-Means, Mean-Shift, and DBSCAN — across
two datasets. All cells have already been executed, so opening the
notebook shows the completed results without needing to run anything.

## Datasets

- **`data_refined.csv`** — the "previously preprocessed dataset" referenced
  in the assignment. This file contains the sklearn Breast Cancer Wisconsin
  dataset (569 real patient records, 30 diagnostic measurements + a
  diagnosis label), matching the dataset referenced later in the DBSCAN
  challenge section. **If your actual `data_refined.csv` from an earlier
  mission is different, replace this file with yours** — the rest of the
  notebook doesn't need to change, since it just reads whatever is in this
  CSV.
- **`insurance.csv`** — the real Kaggle Medical Cost Personal Dataset
  (1,338 rows: age, sex, bmi, children, smoker, region, charges).

## Setup

```bash
pip install -r requirements.txt
jupyter notebook Clustering_Mini_Project.ipynb
```
Then Cell → Run All if you want to re-run it yourself (not required to view results).

## What the notebook covers

1. **Reading the datasets** — both CSVs loaded into Pandas DataFrames.
2. **Preprocessing**
   - NaN check (both datasets are clean, no missing values)
   - Encoding (`sex`, `smoker` label-encoded; `region` one-hot encoded)
   - Scaling (`StandardScaler` applied to both datasets)
3. **Feature selection**
   - Breast Cancer: dropped 6 highly correlated size features
     (mean/worst perimeter & area, since they're redundant with radius)
   - Insurance: kept `age`, `bmi`, `children`, `smoker`, `charges`; dropped
     `sex` and `region` as weakly related to cost
4. **Clustering**
   - K-Means with an elbow curve to pick k for each dataset
   - Mean-Shift tried across 4 different bandwidths (quantiles 0.1–0.4)
5. **Challenge: DBSCAN**
   - Discussion of whether DBSCAN suits these datasets
   - Implementation on the Breast Cancer dataset, first on the full
     feature space (where it struggles — a real, useful negative result),
     then on a PCA-reduced 2D version (where it finds 3 meaningful
     clusters), demonstrating the effect of dimensionality on DBSCAN
