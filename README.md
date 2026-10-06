# NYPD Stop, Question and Frisk: Cluster Analysis

Cluster analysis of the 532,911 stops recorded by the NYPD in 2012, using K-means and DBSCAN in Python. Completed as Report 2 of the DATA 475 final project at SAIT.

## Questions

1. Where are robbery stops concentrated, and does that change between day and night?
2. Which combinations of stop reasons do officers record together, and how do outcomes differ between them?
3. Do precincts fall into distinct groups based on how often stops lead to a frisk, use of force, or an arrest?

## Models

| Model | Method | Data | Clusters |
|---|---|---|---|
| Robbery zones | K-means | X/Y coordinates of 113,734 robbery stops | 5 |
| Robbery hotspots | DBSCAN (750 ft radius) | Same coordinates | 28 |
| Reasons for stop | K-means | 10 yes/no reason flags, all stops | 5 |
| Precinct profiles | K-means | Frisk, force and arrest rates for 76 precincts (standardized) | 3 |

The number of clusters for each K-means model was chosen with the elbow and silhouette methods. All models were checked with silhouette, Davies-Bouldin and Calinski-Harabasz scores.

## Key findings

- **Robbery zones:** The largest zone is centred on Brooklyn and holds 37% of robbery stops. 64% of all robbery stops happened between 6 pm and 6 am.
- **Robbery hotspots:** 28 dense hotspots hold 31% of robbery stops. The largest is in Precinct 110 (Queens), where 81% of stops happened at night.
- **Reasons for stop:** The largest cluster (37% of stops) is built around "furtive movements". Stops in the "fits description" cluster had the highest arrest rate (11.6%), while the "acting as lookout" cluster had the lowest (2.8%).
- **Precinct profiles:** 20 precincts form a high-intensity group with a 66% frisk rate and 26% force rate. A separate group of 21 precincts, 14 of them in Manhattan, has lower frisk rates but the highest arrest rate (10.3%).

| Model | Silhouette | Davies-Bouldin | Calinski-Harabasz |
|---|---|---|---|
| Robbery zones (K-means) | 0.452 | 0.785 | 11,469 |
| Robbery hotspots (DBSCAN) | 0.609 | 0.487 | 92,564 |
| Reasons for stop (K-means) | 0.370 | 1.281 | 2,325 |
| Precinct profiles (K-means) | 0.326 | 1.045 | 42 |

## Data

The data file is not included in this repo because of its size.

Source: [NYPD Stop, Question and Frisk Data](https://www.nyc.gov/site/nypd/stats/reports-analysis/stopfrisk.page). Download the 2012 CSV, save it as `2012_SQF_Data.csv`, and place it in the same folder as the notebook.

## How to run

```
pip install numpy pandas matplotlib scikit-learn
jupyter notebook report2_clustering.ipynb
```

Run all cells from top to bottom. The notebook creates two folders:

- `figures/` with the 9 charts (elbow and silhouette plots, zone and hotspot maps, reason heatmap, precinct bubble chart)
- `tables/` with the cluster profiles and validation scores as CSV files

The random seed is fixed at 42 so results are reproducible.

## Tools

Python, pandas, NumPy, scikit-learn, matplotlib, Jupyter
