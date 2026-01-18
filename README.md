# Real-Time-Traffic-Route-ETA-Prediction-
A production-style machine learning system that forecasts(15 mins ahead) highway traffic speeds using XGBoost and converts them into reliable segment-level and route-level travel time (ETA), evaluated against a strong weekday–hour historical baseline on the METR-LA dataset.

* This project builds a machine learning pipeline that:

     * Predicts traffic speed 15 minutes ahead for highway sensors

     * Converts speed into segment travel time

     * Aggregates multiple segments to compute full-route ETA

     * Quantifies uncertainty to estimate reliability
# Dataset
The dataset that I have used is METR-LA Traffic Dataset which is available in Kaggle, link: https://www.kaggle.com/datasets/annnnguyen/metr-la-dataset<br>
Contains:
* 207 highway loop detector sensors, where each sensor is a road segment

* 5-minute interval speed data

* ~34K timestamps

* Stored in HDF5 format
# Pipeline
Raw Speed Data<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&darr;<br>
Sliding Window Feature Engineering (60 min history)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&darr;<br>
ML Speed Forecasting (15 min ahead)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&darr;<br>
Speed To Segment ETA<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&darr;<br>
Route ETA Aggregation (sum of segments)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&darr;<br>
Baseline Comparison + Uncertainty Estimation<br>
# Segment Level (5 km simulated highway segments)
| Method   | ETA MAE  |
| -------- | -------- |
| Baseline | 0.49 min |
| ML       | 0.29 min |
  --------   --------
~40% improvement per segment
# Route Level (30 km synthetic route)
| Method   | Route ETA MAE |
| -------- | ------------- |
| Baseline | 2.81 min      |
| ML       | 1.49 min      |
  --------   -------------
 ~47% reduction in trip-level travel time error
 # Uncertainty
 Segment residual variability was propagated through the ETA formula:
   * Segment uncertainty: ±7–35 seconds
   * Route uncertainty: ±1.1 minutes

The estimation reliability is similar to real navigation systems.
# Summary 
* The ML model reacts much faster than simple historical averages when traffic suddenly worsens or clears up.
* Even small improvements in segment-level predictions add up to noticeably better accuracy for full-route travel time.
* Adding uncertainty helps the system recognize when predictions are less reliable, similar to real navigation apps.
