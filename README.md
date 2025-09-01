Project Overview

This project explores the identification of sailing ships (1849) versus powered ships (1949) using historical ICOADS (International Comprehensive Ocean-Atmosphere Data Set) observations.
We analyze ship speed and its relationship with wind direction and speed to determine whether a vessel is wind-driven (sailing) or mechanically powered. Machine learning models (Random Forest and SVC) are used to classify ships based on derived features.

Data Source :

ICOADS Dataset: International Comprehensive Ocean-Atmosphere Data Set

Format: IMMA (International Maritime Meteorological Archive)

Files Used:

1849 data: sailing ships

1949 data: powered ships

Data contains ship positions (LAT, LON), time (YR, MO, DY, HR), wind speed (W), wind direction (D), and other metadata.

Procedure
Step 1: Data Loading

Read all IMMA files for 1849 and 1949 using the IMMA Python package.

Convert IMMA data to Pandas DataFrames and concatenate monthly files.

Fill missing hours in 1849 data assuming noon (HR = 12).

Check dataset sizes.

Step 2: Derived Features

Ship Speed and Heading: Calculated from consecutive latitude/longitude positions using Haversine formula and bearing calculation.

Relative Speed:

relative speed = ship speed × cos(ship heading − wind direction)

Filter out unrealistic speeds (>40 km/h) and invalid time differences.

Step 3: Exploratory Data Analysis (EDA)

Histograms of ship speed for 1849 and 1949.

Polar plots of ship speed vs bearing relative to wind.

Scatter plots of ship speed vs wind speed.

Correlation analysis between ship speed and wind speed.

Step 4: Feature Engineering

Five-number summary of ship speed or relative speed (min, Q1, median, Q3, max) per ship.

Correlation between ship speed and wind speed per ship.

Year labels added (1849 = 0, 1949 = 1) for classification.

Step 5: Machine Learning Experiments

Experiment 1: Random Forest on ship speed summary.

Experiment 2: Random Forest and SVC on relative speed summary.

Experiment 3: Random Forest and SVC using ship speed summary + speed-wind correlation.

Experiment 4: Random Forest and SVC using relative speed summary + speed-wind correlation.

Data split: 70% training, 30% testing (stratified).

Evaluation metrics: Classification report (precision, recall, F1-score, accuracy) and confusion matrix.

Feature importance visualizations for Random Forest models.

Code Overview :

Data Loading and Preprocessing

drive.mount to access Google Drive

Load IMMA files, convert to DataFrame, concatenate

Fill missing hours

Feature Calculations

great_circle_distance for ship displacement

calculate_bearing for heading

calculate_distances_bearings to compute speed and heading

EDA

Histograms of ship speed

Polar plots of speed vs wind-relative bearing

Scatter plots and correlation checks

Machine Learning

Random Forest and SVC classifiers

Feature engineering (five-number summary, relative speed, speed-wind correlation)

Train/test split, scaling (for SVC), median imputation

Classification report and confusion matrix

Feature importance plots

Results :

Sailing ships (1849) show lower speeds and stronger dependence on wind direction.

Powered ships (1949) show higher speeds and lower wind dependence.

Both Random Forest and SVC models successfully classify ships with high accuracy.

Including wind correlation improves model performance, highlighting the effect of environmental conditions on sailing ships.

Conclusion :

The experiments demonstrate that historical ship data can reliably distinguish sailing vs powered vessels using speed and wind-related features.

Ship speed and relative speed distributions show clear differences between eras.

Machine learning classifiers achieve strong performance, confirming the predictive power of these features.

Feature importance analysis confirms that relative speed and wind correlations are key indicators of propulsion type.

Dependencies :

Python 3.x

pandas

numpy

matplotlib

scikit-learn

IMMA package (!pip install git+https://github.com/philip-brohan/pyIMMA.git)

Google Colab for running large datasets and accessing Google Drive

How to Run :

Mount Google Drive containing ICOADS IMMA files.

Install the IMMA package.

Load 1849 and 1949 datasets.

Run preprocessing and feature calculation cells.

Perform EDA (optional).

Run machine learning experiments (1–4).

View evaluation results and plots.
