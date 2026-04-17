# ECVT Spectral Feature Extraction and Clustering for Gas–Solid Flow Regimes

## Overview

This repository contains a full pipeline for analyzing spatiotemporal ECVT data to identify underground gas flow regimes using spectral analysis and clustering.

The workflow processes volumetric data, extracts frequency-domain features using periodograms, and applies clustering algorithms to identify distinct physical regimes.



## Pipeline Description

The analysis follows these main steps:

1. **Data Loading**

   * ECVT data is loaded from MATLAB (`.mat`) files
   
3. **Spectral Analysis**
   * Time series are extracted from spatial regions
   * Power spectral density (PSD) is computed using:

     * Periodogram
     * Welch method (optional)
       
   * PSD is log-transformed (`log10`)
  
4. **Clustering**
   Multiple clustering approaches are implemented:

   * TimeSeriesKMeans (DTW-based)
   * K-Medoids
   * Hierarchical Clustering (Euclidean and DTW)

5. **Clustering Stability Framework**

   * DTW threshold applied to enforce centroid dissimilarity
   * Hamming distance used to identify stable clustering families
   * Only stable runs are retained for final analysis

6. **Evaluation**

   * Silhouette score
   * Davies–Bouldin index
   * Computational time
   * Centroids similarity (min DTW, and proportion)
   * Periodogram features: Area under the curve (AUC), Standard deviation (SD), Mean, slope

8. **Visualization**

   * Centroid periodograms
   * Feature-based regime maps (AUC, SD, slope)
   * Elbow method for optimal cluster selection

## Key Parameters

```python
n_clusters = 4
dtw_similarity_threshold = 3.5
hamming_threshold = 0.05
target_family_size = 3
p or powers
```

* **DTW threshold** ensures clusters are physically distinct
* **Hamming threshold** ensures label stability across runs
* **Target family size** defines how many consistent runs are required
* **p or powers** PSD of the periodogram used to define the length of the data based on the configuration

## Repository Structure

* `ECVT-Feature extraction-Clustering code.ipynb`
  Main notebook containing the full pipeline:

  * feature extraction
  * clustering
  * evaluation
  * visualization
  
## Requirements

Install the required Python packages:

```
numpy
scipy
pandas
matplotlib
scikit-learn
tslearn
sklearn-extra
kneed
```

## How to Run

1. Place input `.mat` files in the working directory
2. Open the notebook:

   ```
   ECVT-Feature extraction-Clustering code.ipynb
   ```
3. Run cells sequentially:

   * Data loading
   * Feature extraction
   * Clustering
   * Visualization

## Outputs

The pipeline produces:

* Cluster labels for each run
* Centroid periodograms
* Feature distributions (AUC, SD, slope)
* Regime maps
* Clustering evaluation metrics

## Notes

* PSD is analyzed in log scale to capture power-law behavior
* DTW is used to compare spectral shapes rather than absolute values
* Clustering stability is enforced through repeated runs and filtering
* The final number of clusters is selected based on both:

  * statistical metrics
  * physical interpretability

## Purpose

This code supports data-driven identification of gas–solid flow regimes in subsurface gas release experiments using ECVT measurements.


