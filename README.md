# CS547--Deep-Learning-Project
Work performed as part of CS547-Deep-Learning coursework.

Team Members (in order of contribution)
Siva Kumar Valluri
and Dimitrios Bralios |
Pallav Ranjan |
Pratik Sinha |


## Problem Statement ##
Due to the recent economic and supply-chain turmoil gasoline prices across the world have been on the rise. This has impacted the price of every commodity, and contributed to inflation which in turn feeds back to further impact gas prices. Thus, the ability to predict future gasoline prices would be crucial to prepare and device measures to ameliorate the situation. We have identified that gasoline prices are primarily driven by classical economic theory of supply and demand. The supply of gasoline to the US is primarily from domestic crude oil wells and imports from other nations. The US also maintains a strategic petroleum reserve to handle the disruptions in the crude oil supply chain. Demand of gasoline is primarily reflected by domestic consumption. Other than these, inflation limits the purchasing power thus affecting both production/import and consumtion of gasoline. It is usually measured as Consumer Price Index (CPI) by the Federal Bank of the US. Further, changes in taxation at federal and state level will also impact the prices, however it remains constant over a long duration. Finally, we will also use historical trends in gasoline prices to capture any missing features. 

### To summarize, we are building a Recurrent Neural Network (RNN) to predict the weekly gasoline price based on the following features: ###

    - Weekly crude oil import (Supply)
    - Strategic Petroleum Reserve (Supply)
    - Domestic Production (Supply)
    - Domestic Consumption of Gas (Demand)
    - Domestic Inflation as CPI
    - Historical Price of Gasoline
    
##  Highlights (not exhaustive) ##

Dataset insights:

Seasonality in data:

![image](https://github.com/user-attachments/assets/09252bc4-5ed5-4d18-b592-97cd2bd04daa)

Trends in data:

![image](https://github.com/user-attachments/assets/8805035e-32ac-46d7-9fc4-66799f1b923d)

Correlation between features chosen:

![image](https://github.com/user-attachments/assets/702ffda6-caca-4f78-b010-8ab391638a7a)

Feature importance:
Principal component analysis (shown as an example)

![image](https://github.com/user-attachments/assets/94111fe5-de3b-4632-95bf-cc143411b9d3)

Baseline linear regression model: 

![Screenshot 2024-09-03 153952](https://github.com/user-attachments/assets/8ab24a2b-afb0-43c1-9dc4-2d86e85a4cae)

Testing different 'shallow' models using smaller data snippets (using repurposed tensorflow code) for initial direction: 

I. Multi-variate Multi-time Long/Short Term Memory (LSTM) Flavored RNN (Optimized) model:

![image](https://github.com/user-attachments/assets/33f8c6a9-b835-4273-959a-9aa960019ee4)

II. Multi-time Long/Short Term Memory (LSTM) Flavored RNN (unpotimized) model:

![image](https://github.com/user-attachments/assets/bbb32732-1e90-46d3-93e4-372f99981430)

III. Multi time-step last prince baseline model:

![image](https://github.com/user-attachments/assets/185390a7-9588-4216-af80-d537d9f5df66)

IV. Multi-time step linear model:

![image](https://github.com/user-attachments/assets/bf2c0787-0107-481b-a3fa-2034865d4bdd)

V. Convolution neural network (unoptimized) model: 

![image](https://github.com/user-attachments/assets/333d4a1f-2161-4a45-8329-ab3a364fe882)

VI. Convolution neural network (optimized) model: 

![image](https://github.com/user-attachments/assets/f2c020a8-e6e1-4fa7-ad94-57a4a2051ba9)

VII. Dense neural netwrok model: 

![image](https://github.com/user-attachments/assets/37d22cd4-4185-4f47-99f0-5c09b353c974)

Comparing performance obtained by different models to work on most promising models:

![image](https://github.com/user-attachments/assets/63cbdd1b-860a-4820-9c3a-0744c4d40144)

Deep Neural Networks tested-

Final DNN model that predicts gas prices:
![image](https://github.com/user-attachments/assets/f829e86d-bb70-46ab-85be-7a02269751f2)

Final CNN model that predicts gas prices:
![image](https://github.com/user-attachments/assets/4b0dc2b9-da8f-4aa9-bd31-88753e857b89)

## License ##
Copyright 2022 University of Illinois Team Oglesby

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.


## Data Preprocessing ##
This code performs the following steps for predicting weekly gasoline prices:

### 1. Library Imports

    - Data Handling and Visualization: numpy, pandas, matplotlib, scipy
    
    - Machine Learning: tensorflow, sklearn
    
    - Additional Utilities: datetime, time, random

### 2. Plotting Parameters

    Sets default plot parameters using matplotlib to adjust font size and line width for better visualization.

### 3. Data Loading Function (getfile)

    - Purpose: Loads data from Google Drive links or a local version if available.
    
    = How: Uses pandas.read_pickle to read binary pickle files.
    
### 4. Data Import 
    - CPI: Consumer Price Index data, a measure of inflation. 
    
    - Consumption: Domestic gasoline consumption.  
    
    - Price: Historical gasoline prices.
    
    - Imports: Weekly crude oil import data.
    
    - Reserve: Strategic Petroleum Reserve data.
    
    - Production: Domestic gasoline production data.
    
    - Each dataset is loaded, processed (e.g., renaming columns, converting dates), and prepared for alignment.

### 5. Data Alignment and Truncation 

    - Aligns all features to the date range of the price data.
    
    - Truncates earlier data to match the date range of the price data.
    
### 6. Data Matching

    - Matches each price data point with the closest earlier data points for each feature.
    
    - Creates a combined dataset where each row contains price and corresponding feature values.

### 8. Normalization and Visualization

    - Normalization: Standardizes features by subtracting the mean and dividing by the standard deviation. 
    
    - Visualization: Plots the normalized dataset to visualize trends and seasonality.
    
### 9. Data Splitting

    - Splits the dataset into training (70%), validation (20%), and test (10%) sets.
    
    - Drops the date column for model training and validation.
    
### 10. Linear Regression Baseline

    - Initial Model: Trains a linear regression model using features excluding historical prices.
    
    - Augmented Model: Adds the previous week’s price as a feature, improving the model's performance.
    
    - Visualization: Plots the predicted vs. actual values for training, validation, and test sets.
    
### 11. Feature Importance Analysis
    - Pearson Correlation: Examines correlations between features and the target variable.
    
    - ANOVA: Uses statistical tests to rank feature importance.
    
    - Principal Component Analysis (PCA): Reduces dimensionality and identifies key features based on variance explained.
    
    - Recursive Feature Elimination (RFE): Identifies the most important features by recursively removing the least important ones.
    
### Key Findings
    - Best Features: CPI is identified as the most significant feature affecting gasoline prices, with other features like Reserve and Consumption also important.
    
    - Model Improvement: Including historical prices in the linear regression model improves predictions.
    
    - Feature Analysis: Various methods confirm that CPI, Production, and Reserve are crucial features for predicting gasoline prices.
    
    - Overall, the code demonstrates a structured approach to data preprocessing, model training, and feature analysis to predict gasoline prices effectively.

## Initial Deep Learning Testing ##

### Overview

The code snippet you provided is focused on developing and evaluating multiple simple models to predict gasoline prices over an 8-week period using recurrent neural networks (RNNs). It involves preparing time series data, building models, and evaluating their performance to identify the best model based on the lowest mean absolute error (MAE). Here’s a more detailed breakdown:

### Components and Workflow

    - Objective:
    
    - Goal: Predict 8 weeks of gasoline prices using various simple models.
    
    - Evaluation Metric: Mean Absolute Error (MAE).

### Data Preparation:

    - WindowGenerator Class: (Obtained from Tensorflow documentation)
    
    Purpose: Generates windows of input and label data from the time series for training, validation, and testing.
    
    Key Methods:
        split_window(): Splits the data into inputs and labels based on the defined window sizes.
        plot(): Visualizes the inputs, labels, and predictions.
        make_dataset(): Converts data into a TensorFlow dataset with appropriate windowing.
        Properties: train, val, test, example - Return datasets and an example batch for plotting.
    
    -Model Training and Evaluation:
        compile_and_fit() Function:
        Purpose: Compiles and trains a given model with early stopping to avoid overfitting.
        Parameters: Model, window object, patience for early stopping, maximum epochs, optimizer.
        Performance Tracking:
        multi_val_performance and multi_performance: Dictionaries to store validation and test performance metrics for different models.
        
### Model Definition:

    modular_lstm_model() Function:
        Purpose: Constructs a modular LSTM model.
        Parameters: Number of neurons, dropout rate, activation functions for LSTM and Dense layers.
        Architecture: Single LSTM layer followed by a Dense layer to produce predictions.
    
    Hyperparameter Optimization:
        Optimization Process:
        Goal: Test various activation functions and input steps to optimize model performance.
        Parameters: Different activation functions for LSTM and Dense layers, varying input window sizes.
        Loop: Trains models with different hyperparameters and evaluates their performance.
        Performance Visualization:
    
        performance_plotter() Function:
        Purpose: Plots the performance of different models based on MAE.
        Parameters: Dictionaries with performance metrics, choice of plot type, width of bars.

### Summary of the Workflow

    - Initialize Data: Define the WindowGenerator to handle data preparation.
    
    - Model Construction: Create a modular LSTM model suitable for time series prediction.
    
    - Training: Use compile_and_fit() to train the model and evaluate it using the validation and test sets.
    
    - Hyperparameter Optimization: Iterate over different configurations to find the best-performing model.
    
    - Visualization: Plot the performance of different models to compare their effectiveness based on MAE.

This code aims to identify the best simple RNN model for predicting gasoline prices over a multi-week horizon by experimenting with different configurations and tracking performance through rigorous evaluation and visualization.
