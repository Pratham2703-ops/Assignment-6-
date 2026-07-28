Weather Condition Classification using SVM and Open-Meteo API
AI-ML Assignment - 6
Author: Pratham Dholi 
Registration Number: 23BAI11220
Batch: 2B 
Date: 28 July 2026
Objective
Develop a Support Vector Machine (SVM) Classification model to classify weather conditions as Cool or Warm based on meteorological observations collected from the Open-Meteo API. The target variable is derived from temperature readings where:
Warm → Temperature ≥ 25°C
Cool → Temperature < 25°C
API Documentation
Open-Meteo Weather API (Free, No API Key Required)
Website: https://open-meteo.com/
Example API Request:
plain
https://api.open-meteo.com/v1/forecast?latitude=28.6139&longitude=77.2090&hourly=temperature_2m,relative_humidity_2m,surface_pressure,wind_speed_10m&forecast_days=7
Libraries Used
Table
Library	Purpose
requests	Fetch weather data from Open-Meteo API
pandas	Data manipulation and analysis
numpy	Numerical computations
scikit-learn	SVM model, preprocessing, evaluation metrics
matplotlib	Data visualization
seaborn	Statistical data visualization
Methodology
Task 1: Data Collection and Understanding (2 Marks)
Fetched weather data from Open-Meteo API for 8 Indian locations (Delhi, Shimla, Manali, Mumbai, Bangalore, Leh, Ooty, Gangtok) to ensure a balanced dataset.
Converted JSON response into a Pandas DataFrame with 1,344 records.
Created target variable Weather_Class based on temperature threshold (25°C).
Identified input features and target variable.
Input Features:
Temperature (temperature_2m)
Relative Humidity (relative_humidity_2m)
Surface Pressure (surface_pressure)
Wind Speed (wind_speed_10m)
Target Variable:
Weather_Class (Cool / Warm)
Task 2: Data Preprocessing (2 Marks)
Missing Values Check: No missing values found in the dataset.
Column Removal: Removed time and location columns as they are not needed for classification.
Target Encoding: Used LabelEncoder to encode target variable (Cool = 0, Warm = 1).
Train-Test Split: Split dataset into 80% training (1,075 samples) and 20% testing (269 samples) with stratification.
Feature Scaling: Applied StandardScaler to standardize features to zero mean and unit variance.
Task 3: Model Development (3 Marks)
Built an SVM Classifier with RBF (Radial Basis Function) Kernel.
Hyperparameters used:
kernel = 'rbf'
C = 1.0
gamma = 'scale'
Trained the model on standardized training data.
Predicted weather classes for the test dataset.
Task 4: Model Evaluation (2 Marks)
Evaluated the model using the following metrics:
Table
Metric	Score
Accuracy	98.88%
Precision	0.9890
Recall	0.9888
F1-Score	0.9888
Confusion Matrix:
plain
          Predicted
           Cool  Warm
Actual Cool  189     0
       Warm    3    77
3 Key Observations:
High Accuracy (98.88%): The SVM model achieved exceptional accuracy, correctly classifying 266 out of 269 test samples, indicating that meteorological features are highly discriminative.
Excellent Precision and Recall: Both metrics exceed 0.98 with balanced performance across classes. Only 3 misclassifications occurred (all false negatives).
Temperature Dominance: Temperature is the strongest predictor, while humidity, pressure, and wind speed refine the decision boundary for edge cases near 25°C.
Task 5: Conclusion (1 Mark)
This assignment successfully demonstrates the application of Support Vector Machine (SVM) classification for weather condition prediction using real-time meteorological data from the Open-Meteo API. The SVM model with an RBF kernel achieved an exceptional accuracy of 98.88%, with precision, recall, and F1-score all exceeding 0.98, indicating robust and balanced classification performance across both Cool and Warm weather classes.
Feature scaling using StandardScaler proved critical for SVM performance. Since SVM relies on distance-based optimization (maximizing the margin between support vectors), features with different scales—such as temperature (~11-32°C), surface pressure (~678-1006 hPa), and wind speed (~0-26 km/h)—would disproportionately influence the model without normalization. StandardScaler transformed all features to zero mean and unit variance, ensuring each feature contributed equally to the decision boundary.
One key advantage of SVM is its effectiveness in high-dimensional spaces and its ability to handle non-linear relationships through kernel tricks like RBF, making it versatile for complex datasets. However, a notable limitation is its computational cost—training time scales quadratically with the number of samples, making it less suitable for very large datasets. Additionally, SVM is sensitive to hyperparameter tuning (C and gamma), requiring careful selection for optimal results.
Files in this Repository
Table
File	Description
Assignment-6.py	Complete Python script with all tasks
README.md	Project documentation
confusion_matrix_and_metrics.png	Confusion matrix and performance metrics visualization
weather_data_analysis.png	Exploratory data analysis visualizations
How to Run
Install required libraries:
bash
pip install pandas numpy scikit-learn matplotlib seaborn requests
Run the script:
bash
python Assignment-6.py
The script will:
Fetch real-time weather data from Open-Meteo API
Preprocess the data
Train the SVM model
Evaluate and display results
Save visualization plots
Results Summary
Model: Support Vector Machine (SVM) with RBF Kernel
Dataset Size: 1,344 samples from 8 locations
Accuracy: 98.88%
Precision: 0.9890
Recall: 0.9888
F1-Score: 0.9888
Misclassifications: 3 out of 269 test samples
