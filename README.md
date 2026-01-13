Geospatial Time-Series Reconstruction
This project implements a robust pipeline for reconstructing missing time-series data at specific geographic coordinates. By leveraging Fourier Seasonality Decomposition and a Dual-Filter K-Nearest Neighbors (KNN) approach, the model synthesizes highly accurate sensor data based on spatial proximity and temporal correlation.

Project Overview
In environmental monitoring, sensor failure often leads to spatial gaps. This project provides a solution to "fill in the blanks" by predicting the full 636-point time series for a target location using historical data from a sparse network of neighboring sensors.

Key Features:
Robust Pre-processing: Automated outlier removal using Median Absolute Deviation (MAD).

Fourier Seasonality: Models cyclic patterns (e.g., daily cycles) using sine/cosine harmonics.

Dual-Filter KNN: Filters neighbors first by physical distance, then by temporal correlation.

Residual Blending: Combines smooth seasonal trends with localized high-frequency residuals.

The Pipeline
The reconstruction process follows a sophisticated four-stage pipeline:

Data Cleaning:

Detects and removes measurement spikes using a robust Z-score based on the median.

Imputes small internal gaps using linear interpolation.

Harmonic Modeling:

Fits a 3-harmonic Fourier series to capture the "heartbeat" of the data.

Neighbor Selection:

Calculates Euclidean distances between the target and 990+ sensors.

Selects the top 10 most correlated sensors from the 50 closest neighbors.

Synthesis:

Generates the final prediction using a distance-weighted average of the neighbors' seasonal and residual components.

Visualizing the Methodology
Seasonality Modeling
The model separates the stable periodic signal from the stochastic noise. This ensures that the reconstruction isn't skewed by a single malfunctioning neighbor.

Spatial Correlation
The following plot shows the final reconstructed series (dashed) against its most physically proximate and temporally correlated neighbor.

Installation & Usage
Prerequisites
Python 3.x

Pandas, NumPy, Matplotlib, Scikit-learn

Setup
Bash

git clone https://github.com/niyimoluga/Spatial_temporary_reconstruction.git
cd Spatial_temporary_reconstruction
pip install -r requirements.txt
Running the Project
The primary logic is contained within the Jupyter Notebook. To generate the final 19_New.csv submission file:

Place your dataset in the project root.

Run all cells in test_5.ipynb.

Results and Evaluation
Baseline: K-Nearest Neighbors (KNN) Mean.

Improvement: Our method significantly reduces RMSE by accounting for temporal cycles that a simple spatial average misses.

Output: A 636-point reconstructed row optimized for submission.

License
Distributed under the MIT License. See LICENSE for more information.

Contributing
Contributions are welcome! If you have ideas for improving the Fourier fit or implementing a Transformer-based approach, please open an issue.
