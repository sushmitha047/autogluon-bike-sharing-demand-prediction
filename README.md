# Bike Sharing Demand Prediction with AutoGluon

This repository contains my solution for the AWS AI/ML Scholarship Program Nanodegree - "AWS Machine Learning Fundamentals" project demonstrating automated machine learning capabilities using AutoGluon. The project addresses Kaggle's Bike Sharing Demand prediction challenge, simulating real-world demand forecasting scenarios faced by mobility companies like Uber and Lyft.

--------------------------------------------------

### Table of Contents

- [Project Introduction](#project-introduction)
- [Solution Architecture](#solution-architecture)
- [Technical Implementation](#technical-implementation)
- [Model Evolution & Results](#model-evolution--results)
- [Review Highlights](#review-highlights)
- [License & Acknowledgments](#license--acknowledgments)

--------------------------------------------------

## Project Introduction

### Business Context
Bike-sharing demand forecasting helps optimize fleet management and staffing for urban mobility services. Accurate predictions:
- Reduce operational costs through proactive bike redistribution
- Improve customer experience by preventing station shortages
- Enable dynamic pricing strategies during demand spikes

### Technical Objective
Developed a prediction system that:
- Achieved **Kaggle Score 0.49549**
- Processes temporal patterns through feature engineering
- Automates model selection/tuning within **10-minute training window**
- Ensures production-ready predictions (non-negative values)

### Repository Structure

- `PredictBikeSharingDemandwithAutoGluon.ipynb`: Main notebook for data preparation, feature engineering, model training, and hyperparameter tuning
- `data/`: Contains train and test data
- `submissions/`: Kaggle submission files
- `visualizations/`: Model performance charts

--------------------------------------------------

## Solution Architecture

### Core Components
1. **Data Pipeline**
   - Kaggle API integration for dataset retrieval
   - Temporal feature extraction using pandas `dt` accessor
   - Categorical type conversions for optimal AutoGluon performance

2. **AutoML Engine**
   - AutoGluon's `TabularPredictor` with `best_quality` preset
   - Automated hyperparameter optimization
   - Multi-model stacking and weighting

3. **Validation System**
   - Temporal split validation
   - Kaggle score tracking across iterations
   - Negative prediction clipping for operational realism

--------------------------------------------------

## Technical Implementation

### Feature Engineering Impact
| Iteration | Added Features                          | Kaggle Score | Improvement |
|-----------|-----------------------------------------|--------------|-------------|
| Baseline  | Raw features                            | 1.80462      | -           |
| V1        | `hour`, `day`, `month`, `is_weekend`    | 0.62779      | **65.2%**   |
| V2        | `feels_like`, `temp_time_of_day`        | 0.61899      | 0.5%        |
| V3        | Dropped `temp_time_of_day`              | 0.63101      | -0.7%       |
| V4        | One-hot encoded categoricals            | 0.66145      | -1.7%       |
| Final     | Hyperparameter tuning                   | 0.49549      | **25.1%**   |

### AutoGluon Configuration

- **Preset Strategy**: `best_quality` mode for optimal model selection
- **Time Constraint**: `10-minute` training window
- **Evaluation Metric**: Root Mean Squared Error (RMSE)
- **Model Specific Tuning**:
  - Gradient Boosting: `num_boost_round= [100, 200]`
  - Category Encoders: `iterations= [100, 200]`

Key Insights:
- Temporal features provided **92% of total improvement**
- One-hot encoding hurt performance (-1.7%), justifying AutoGluon's automated handling
- Hyperparameter optimization (HPO) delivered final 25% improvement

--------------------------------------------------

## Review Highlights

The project received exceptional feedback for:

✅ **Data Pipeline Excellence**  
- Robust Kaggle API integration with secure credential management
- Efficient datetime parsing using pandas `parse_dates`
- Effective categorical type conversions for AutoGluon optimization

✅ **AutoGluon Mastery**  
- Correct implementation of `best_quality` preset for model stacking
- Strategic hyperparameter tuning
- Production-grade prediction post-processing

✅ **Analytical Rigor**  
- Clear demonstration of feature engineering impact through score tracking
- Comprehensive visualization of model performance trends
- Detailed hyperparameter optimization analysis

--------------------------------------------------

## License & Acknowledgments

**Educational Context**  
This project was completed as part of the [AWS AI/ML Scholarship Program](https://www.udacity.com/scholarships/aws-ai-ml-scholarship-program) through Udacity. 

**Intellectual Property**  
- Project specifications and requirements are Udacity/AWS intellectual property  
- Student implementations in `PredictBikeSharingDemandwithAutoGluon.ipynb` are shared for portfolio demonstration

**Usage Rights**  
As per scholarship guidelines:
- You may showcase this work in portfolios/job applications
- Commercial use requires written permission from Udacity/AWS
- Udacity/AWS retain all rights to project structure and evaluation criteria

**Gratitude**  
Special thanks to:
- AWS AI/ML team for providing the learning platform
- Udacity mentors for detailed technical feedback
- Kaggle community for maintaining the benchmark dataset
- AWS AutoGluon team for the powerful AutoML library

--------------------------------------------------