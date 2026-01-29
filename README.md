# 🌫️ Air Pollution Clustering in Indian Cities 

**Unsupervised Learning Project** to discover hidden air pollution patterns across Indian cities using real daily data — **no AQI labels used**.

### Project Overview
This project applies unsupervised machine learning to group days and cities based on pollutant levels (PM2.5, PM10, NO₂, CO, etc.) and reveal natural patterns like:
- High-pollution winter days in northern cities
- Cleaner monsoon periods
- Differences between urban/industrial vs. coastal/southern areas

**Goal**: Find meaningful clusters without any predefined categories, to support better air quality monitoring and policy decisions.

### Dataset
- **Source**: [Air Quality Data in India (Kaggle)](https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india)
- **File**: `city_day.csv`
- **Key features**: PM2.5, PM10, NO, NO₂, NOx, NH₃, CO, SO₂, O₃, Benzene, Toluene, Xylene, AQI (ignored for clustering)
- **Time range**: Multi-year daily data from multiple Indian cities
- **Challenges**: Heavy right skew + extreme outliers (e.g., PM2.5 > 500–900 µg/m³ in winter smog)

### Key Decisions & Why
- **Scaler chosen**: **MinMaxScaler** (applied directly on raw data)  
  → Data has very high skew (most > 2–5, some > 10–23) and many extreme high values (real severe pollution events).  
  → MinMax keeps these extremes strong → better cluster separation (higher silhouette score).  
  → StandardScaler / RobustScaler / outlier removal → flattens important tails → worse results.

- **Best model**: **Agglomerative Hierarchical Clustering** (ward linkage, 4 clusters)  
  → Manually trained & tuned each model one by one: K-Means, DBSCAN, Agglomerative, GMM  
  → Compared using silhouette score (~0.51–0.57 best), Davies-Bouldin, PCA/t-SNE visuals, and domain meaning (seasonal/city patterns)  
  → Agglomerative won: highest score, clear dendrogram hierarchy, no spherical assumption, robust to skewed data

### Main Results
- Clear separation of **severe pollution** (winter, northern cities) vs. **moderate** vs. **clean** (monsoon, southern/coastal)
- Strong seasonal pattern: high Cluster 0 share in Nov–Jan, low in Jun–Sep
- Cities grouped logically (e.g., Delhi often in high-pollution cluster)

### Notebook Structure
- Data loading & exploration (skew, boxplots → confirmed need for MinMax)
- Preprocessing (missing values, MinMaxScaler)
- Dimensionality reduction (PCA)
- Model comparison & tuning (manual)
- Final clustering with Agglomerative
- Interpretation: seasonal & city-wise cluster distribution

### How to Run
1. Clone the repo:
   ```bash
   git clone https://github.com/yourusername/air-pollution-clustering.git
   cd air-pollution-clustering
