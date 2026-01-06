# Taxi Zone Segmentation & Urban Mobility Analysis (NYC)

## Project Overview
This project performs **zone-level segmentation of NYC taxi pickup locations** using historical TLC trip data.  
The goal is to uncover **distinct urban mobility patterns** across taxi zones based on demand intensity, trip characteristics, and temporal behavior.

Using feature engineering and unsupervised learning (K-Means), NYC taxi zones are grouped into functionally meaningful clusters such as high-demand commercial hubs, airport zones, nightlife areas, and low-demand residential zones.

---

## Dataset Source
The data comes from the **NYC Taxi & Limousine Commission (TLC)** public trip records.

- **Primary dataset**:  
  Yellow Taxi Trip Records (2023–2024)  
  https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

- **Taxi zone lookup**:  
  `taxi_zone_lookup.csv` (maps LocationID → zone & borough)

Only **aggregated, processed features** are committed to this repository.  
Raw trip data is intentionally excluded.

---

## Project Structure

* **data/artifacts/**
    - zone_features.parquet
    - zone_clusters.parquet

* **notebooks/**
    - 1_data_processing.ipynb
    - 2_zone_feature_engineering.ipynb
    - 3_zone_clustering.ipynb
    - 4_cluster_analysis.ipynb

* **gitattributes**
* **gitignore**
* **README.md**



---

## Notebook Breakdown

### 1. Data Loading
- Loads TLC trip data
- Filters required columns
- Joins pickup `LocationID` with taxi zone metadata
- Converts timestamps and basic trip fields

### 2. Zone Feature Engineering
Aggregates trip-level data into **zone-level features**, including:
- Average trips per day
- Average trip distance
- Average trip duration
- Average fare amount
- Percentage of night trips
- Percentage of weekend trips
- Percentage of high-fare trips

Final output:
- `zone_features.parquet`

### 3. Zone Clustering
- Feature scaling using `StandardScaler`
- K-Means clustering
- Cluster count selection using:
  - Inertia (Elbow method)
  - Silhouette score
- Assignment of cluster IDs to zones

Final output:
- `zone_clusters.parquet`

### 4. Cluster Interpretation
- Cluster-level statistical comparison
- Identification of dominant behavioral patterns
- Qualitative interpretation of each cluster’s urban function

---

## Key Insights

- NYC taxi demand is **highly concentrated** in a small subset of zones.
- Zones naturally segment into:
  - **High-demand commercial hubs** with frequent short trips
  - **Airport & long-haul zones** with long distances and high fares
  - **Nightlife / mixed-use zones** with strong night and weekend activity
  - **Residential low-demand zones** with sparse usage
- Unsupervised clustering effectively captures **functional urban geography** using mobility data alone.

---

## Technologies Used

- Python
- pandas, numpy
- PySpark (for large-scale aggregation)
- scikit-learn (K-Means, scaling, metrics)
- Parquet for data storage
- Git LFS for large artifact tracking

---

## Reproducibility Notes

- Raw TLC data is **not included** in the repository.
- To reproduce from scratch:
  1. Download TLC Yellow Taxi trip data from the official source
  2. Place raw files under `data/raw/` (ignored by Git)
  3. Run notebooks sequentially (1 → 4)

---

## Why This Project Matters
This project demonstrates:
- Real-world feature engineering on transactional data
- Proper handling of large datasets
- Unsupervised learning for pattern discovery
- Clean data pipeline design
- Production-quality Git and artifact management

---

## Author
**Sushmit Kar**

