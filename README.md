# 3DSA-5_DSA4158_Course-Project

# Graph-Based Clustering Approach for Modeling Spatial Accessibility Inequality Using OpenStreetMap Road Network Data in Asia

A large-scale geospatial machine learning pipeline that combines **graph-based transportation modeling**, **GIS accessibility analysis**, and **unsupervised clustering algorithms** to identify patterns of infrastructural inequality and accessibility deprivation across Asia using OpenStreetMap road network data.

---

## Overview

Rapid urbanization across Asia has intensified the demand for transportation infrastructure and equitable access to essential services. However, accessibility remains unevenly distributed across highly urbanized metropolitan centers and underserved rural or isolated communities.

This project develops a **graph-based computational framework** for modeling spatial accessibility inequality using transportation network data extracted from OpenStreetMap (OSM). Rather than relying solely on Euclidean distance, the study models road systems as weighted graph structures to capture realistic travel conditions and transportation connectivity.

The pipeline integrates:

- **Graph theory** for transportation network representation
- **GIS-based accessibility metrics**
- **Vectorized spatial computation**
- **Unsupervised machine learning**
- **Comparative clustering evaluation**

The framework aims to identify regions experiencing accessibility advantages and infrastructural deprivation while comparing how different clustering paradigms interpret accessibility conditions.

---

## Research Objectives

The project aims to:

1. Represent Asian transportation systems as graph structures using OpenStreetMap data.
2. Compute accessibility metrics using network-aware travel distances.
3. Compare clustering algorithms for modeling accessibility inequality.
4. Identify and profile underserved and well-connected regions.

---

## Research Questions

The study attempts to answer the following:

1. How can OpenStreetMap transportation data be transformed into graph structures suitable for accessibility analysis?
2. What accessibility patterns emerge when travel distance and network connectivity are modeled computationally?
3. How do K-Means, Agglomerative Clustering, DBSCAN, and OPTICS compare in identifying accessibility inequality?
4. Which regions exhibit characteristics of accessibility deserts or highly connected “15-minute city” conditions?

---

## Conceptual Foundation

This project is grounded in several accessibility and urban planning frameworks:

- **15-Minute City Framework**
  - Efficient access to essential services within short travel times
- **Transit Desert Analysis**
  - Identifying regions with inadequate transportation access
- **Food Desert Research**
  - Evaluating inequitable access to essential resources
- **Graph-Based Transportation Modeling**
  - Using weighted transportation networks instead of straight-line distance

The study operationalizes these concepts using computational geospatial analytics and machine learning.

---

## Dataset

### Primary Source

- **OpenStreetMap (OSM)**
  - Continental-scale transportation and infrastructure data

### Download Source

- Geofabrik Asia Extract:
  - `asia-latest.osm.pbf`

### Dataset Scale

- Approximate raw dataset size:
  - **14–15 GB**

### Extracted Features

The project extracts:

- Residential road networks
- Road intersections
- Transportation nodes
- Hospitals
- Schools
- Transit stations
- Food establishments
- Leisure facilities

---

## Accessibility Metrics

The framework computes accessibility features based on shortest travel distances to:

- Hospitals
- Schools
- Transit hubs
- Food sources
- Leisure facilities

Accessibility distances are calculated using:

- Spatial KD-Tree nearest-neighbor search
- Graph-aware travel approximation
- 50 km spatial winsorization cap

---

## Machine Learning Models

The project compares multiple clustering paradigms:

| Algorithm | Type | Purpose |
|---|---|---|
| K-Means | Centroid-based | Baseline accessibility segmentation |
| Agglomerative Clustering | Hierarchical | Hierarchical accessibility relationships |
| DBSCAN | Density-based | Accessibility outlier detection |
| OPTICS | Variable-density clustering | Adaptive density clustering |

---

## Evaluation Metrics

The models are evaluated using:

| Metric | Purpose |
|---|---|
| Silhouette Score | Cluster cohesion and separation |
| Davies-Bouldin Index | Cluster similarity measurement |
| Calinski-Harabasz Score | Cluster density and dispersion |

---

## Key Findings

### Best Performing Model

K-Means demonstrated the strongest overall clustering performance:

- Highest Silhouette Score
- Highest Calinski-Harabasz Score
- Most interpretable accessibility segmentation

### Accessibility Cluster Profiles

| Cluster | Interpretation |
|---|---|
| Cluster 0 | High Accessibility / “15-Minute City” |
| Cluster 1 | Moderate Accessibility |
| Cluster 2 | Underserved Regions |
| Cluster 3 | Severe Accessibility Deserts |

### Observed Accessibility Patterns

- Transit hubs exhibited the lowest median travel distances.
- Leisure facilities were consistently the least accessible service category.
- Severe accessibility deserts exhibited travel distances exceeding 40 km across all services.
- Certain clusters demonstrated transportation blind spots despite acceptable access to other services.

---

## Requirements

The notebook is designed for:

- **Google Colab**
- **High-RAM runtime**
- **Google Drive mounted storage**

### Recommended Runtime

- Colab High-RAM enabled
- 24 GB RAM recommended

---

## Dependencies

```python
pyspark
osmium
networkx
geopandas
folium
scipy
pandas
numpy
scikit-learn
matplotlib
seaborn
pyarrow
requests
tqdm
```

---

## Setup

### 1. Open Notebook in Google Colab

Upload or open the notebook in Colab.

---

### 2. Mount Google Drive

```python
from google.colab import drive
drive.mount('/content/drive')
```

---

### 3. Create Dataset Directory

```text
MyDrive/AsiaAccessibility/DATASETS
```

---

### 4. Run Notebook Cells Sequentially

The notebook will:

- Download the Asia OSM dataset
- Pre-filter transportation infrastructure using `osmium-tool`
- Build graph representations
- Extract accessibility features
- Train clustering models
- Evaluate clustering performance
- Generate visualizations and accessibility maps

---

## Pipeline Structure

| Stage | Description |
|---|---|
| Environment Setup | Install dependencies and initialize Spark |
| Dataset Download | Download continental OSM dataset |
| OSM Pre-Filtering | Extract relevant transportation infrastructure |
| Graph Construction | Convert transportation systems into graph structures |
| Spatial Aggregation | Aggregate geographic regions into macro-grid cells |
| Accessibility Computation | Compute nearest-service accessibility metrics |
| Feature Engineering | Generate machine learning-ready feature vectors |
| Clustering | Execute K-Means, Agglomerative, DBSCAN, and OPTICS |
| Evaluation | Compare models using clustering metrics |
| Visualization | Generate maps, radar charts, boxplots, and heatmaps |

---

## Spatial Aggregation Strategy

The framework aggregates transportation data into:

- **0.035-degree macro-grid cells**
- Approximate spatial resolution:
  - ~3.9 km per cell
  - ~15 km² catchment area

This scale was selected to:

- Reduce sparsity in rural areas
- Preserve intra-urban variation
- Support municipal-scale analysis
- Mitigate the Modifiable Areal Unit Problem (MAUP)

---

## Performance Optimizations

To handle continental-scale geospatial data efficiently, the project uses:

### C++ OSM Pre-Filtering

```bash
osmium tags-filter
```

This dramatically reduces memory usage before Python processing.

### Vectorized Spatial Search

- `scipy.spatial.cKDTree`
- Highly optimized nearest-neighbor computations

### Distributed Processing

- PySpark distributed computation
- Parallelized clustering workflows

---

## Generated Outputs

The notebook generates:

| Output | Description |
|---|---|
| Accessibility Maps | Geographic visualization of accessibility inequality |
| Cluster Profiles | Radar/spider accessibility cluster charts |
| Distance Distribution Plots | Service accessibility distributions |
| Heatmaps | Cluster-service deprivation matrices |
| Model Evaluation Charts | Comparative clustering validation metrics |

---

## Example Output Structure

```text
MyDrive/AsiaAccessibility/DATASETS/
├── asia-latest.osm.pbf
├── filtered-asia.osm.pbf
├── accessibility_features.parquet/
├── clustered_regions.parquet/
├── evaluation_results.parquet/
├── accessibility_maps/
│   └── Asia_Accessibility_Map.html
├── visualizations/
│   ├── radar_chart.png
│   ├── deprivation_heatmap.png
│   ├── silhouette_scores.png
│   └── accessibility_boxplots.png
└── outputs/
    └── summary_statistics.txt
```

---

## Visualizations Included

The notebook generates:

- Accessibility severity maps
- Distance distribution boxplots
- Radar charts for cluster profiling
- Clustering evaluation bar charts
- Cluster-service deprivation heatmaps

---

## Reproducibility

This project emphasizes reproducible geospatial machine learning workflows.

Included:

- Fully documented notebook pipeline
- Deterministic random seeds
- Version-controlled implementation
- Explicit preprocessing procedures
- Clearly defined hyperparameters

---

## Limitations

The study has several limitations:

- Dependent on OpenStreetMap data quality
- Road-only transportation modeling
- Excludes rail, maritime, and air transportation
- Accessibility approximations may vary across regions
- Computationally intensive at continental scale

---

## Future Improvements

Potential extensions include:

- Real road-network shortest-path routing
- Multi-modal transportation analysis
- Temporal mobility analysis
- Real-time traffic integration
- Deep learning-based spatial embeddings
- Hybrid clustering frameworks (e.g., OPTICS + K-Means)
- Socioeconomic and demographic integration

---

## References

Key references used in the project include:

- Moreno et al. (2021) — 15-Minute City
- Jiao & Dillivan (2013) — Transit Deserts
- Beaulac et al. (2009) — Food Deserts
- Zielstra & Hochmair (2012) — Network Accessibility
- Wang et al. (2021) — GIS Accessibility Modeling

See the manuscript references section for the complete bibliography.

---

## Repository Structure

```text
.
├── notebooks/
│   └── Asia_Urban_Accessibility_Notebook.ipynb
├── outputs/
├── visualizations/
├── README.md
├── requirements.txt
└── LICENSE
```

---

## License

This repository is intended for academic and research purposes.

Dataset usage is governed by:

- OpenStreetMap Open Database License (ODbL)
- Geofabrik download terms

---

## Authors

3DSA-5 — DSA4158 Course Project

Final Project for Big Data / Machine Learning Research

---

## Acknowledgements

Special thanks to:

- OpenStreetMap contributors
- Geofabrik
- PySpark and open-source GIS communities
- Research works referenced throughout the manuscript

---

## Related Manuscript Chapters

This repository accompanies the manuscript chapters:

- Chapter 1 — Introduction :contentReference[oaicite:0]{index=0}
- Chapter 2 — Review of Related Literature and Studies :contentReference[oaicite:1]{index=1}
- Chapter 3 — Research Design and Methodology :contentReference[oaicite:2]{index=2}

The implementation notebook is based on the computational framework described in:

- Asia Urban Accessibility Notebook :contentReference[oaicite:3]{index=3}
