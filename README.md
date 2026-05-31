# HR Analytics — Data Mining Project

A complete data mining pipeline applied to an HR dataset, covering EDA, preprocessing, Genetic Algorithm feature selection, K-Medoid Clustering, Hierarchical Clustering, and Fuzzy Logic inference.

**Pipeline order:** GA → K-Medoid Clustering → Hierarchical Clustering → Fuzzy Logic

---

## Dataset

**File:** `hr_data_mining_dataset.csv`

**Numeric Features:** `age`, `experience_years`, `salary`, `attendance_rate`, `projects_completed`, `overtime_hours`, `performance_score`

**Categorical Features:** `department` (HR / IT / Finance / Operations / Marketing), `education_level` (High School / Bachelor / Master / PhD)

---

## Pipeline Steps

### Task 1 — Exploratory Data Analysis
- Missing values count and percentage per column
- Categorical inconsistency check — detects typo variants in `department` and `education_level`
- Outlier detection using IQR fences for all numeric features
- Duplicate row detection

### Task 2 — Data Preprocessing

| Step | Issue Found | Treatment |
|---|---|---|
| Step 1 | 168 missing values | Median imputation (numeric) + Mode imputation (categorical) |
| Step 2 | 9 duplicate rows | Deduplication (`drop_duplicates`) |
| Step 3 | 82 categorical typos | Standardisation mapping to canonical values |
| Step 4 | 40 numeric outliers | Winsorization (IQR capping) |
| Step 5 | Categorical encoding | Ordinal encoding for `education_level`; One-Hot for `department` |
| Step 6 | Feature magnitudes | StandardScaler (prevents `salary` dominating distance metrics) |
| Step 7 | Feature matrix | Final clean feature matrix constructed for clustering |

4 visualizations produced post-cleaning to drive algorithm decisions.

### Task 3 — Genetic Algorithm (Feature Selection)
- GA used to select the optimal feature subset before clustering
- Fitness function based on Silhouette Score from a baseline K-Medoids model
- Evolution tracked across generations (convergence plot included)

### Task 4 — K-Medoid Clustering
- Applied on GA-selected features
- Elbow method + Silhouette Score used to determine optimal K
- Cluster centers and profiles compared

### Task 5 — Hierarchical Clustering
- Linkage: Average
- Elbow method + Silhouette Score → K=3 chosen (consistent with K-Medoid)
- Dendrogram and cluster plot produced

### Task 6 — Fuzzy Logic Inference
- Fuzzy Logic control system built for HR promotion/risk scoring
- Input variables derived from cleaned features and cluster assignments
- Integrated into a comprehensive HR Analytics Pipeline function that accepts: `selected_features`, `promotion_sim`, `hier_centers`

---

## How to Run

1. Place `hr_data_mining_dataset.csv` at the path referenced in the notebook (update if needed).
2. Run `DataMiningFinal.ipynb` cell by cell from top to bottom.
3. The pipeline is sequential — each task depends on the output of the previous one.

---

## Requirements

```
numpy pandas matplotlib seaborn scipy scikit-learn scikit-fuzzy
```
