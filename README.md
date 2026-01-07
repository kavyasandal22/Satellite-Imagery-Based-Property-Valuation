Satellite Imagery Based Property Valuation
=========================================

Project Overview
----------------
This project implements a multimodal regression pipeline to predict residential
property prices using both structured tabular data and satellite imagery.

Traditional house price models rely only on numerical features such as bedrooms,
bathrooms, and living area. This project explores whether satellite images can
provide additional environmental context to improve prediction accuracy.

The project compares a tabular-only baseline model with a multimodal model that
combines tabular features and CNN-based image features.

--------------------------------------------------

Dataset
-------
The dataset consists of housing records with the following:

Tabular Features:
- Bedrooms
- Bathrooms
- Living area (sqft_living)
- Latitude
- Longitude
- Other structural attributes

Target Variable:
- Price (available only in training data)

Satellite Images:
- One satellite image per property
- Images are fetched programmatically using coordinates

The test dataset does not contain the target price.

--------------------------------------------------

Project Structure
-----------------
notebooks/
01_preprocessing_data_understanding.ipynb and 02_preprocessing_tabular_baseline.ipynb
- Data loading and cleaning
- Exploratory Data Analysis (EDA)
- Visualizations of price distribution and feature relationships

03_data_fetcher.ipynb
- Downloads satellite images using latitude and longitude
- Stores images locally for model use

04_model_training.ipynb
- Trains a tabular baseline model (Linear Regression)
- Extracts image features using a pretrained ResNet-50 CNN
- Trains a multimodal regression model using fused features
  
05_prediction_generation.ipynb
- Generates predictions on the test dataset
- Applies post-processing to ensure non-negative prices
- Saves final predictions as CSV

data/
- Contains datasets, satellite images, and output files
- Final prediction file: 23116042_final.csv

--------------------------------------------------

Models Used
-----------
- Tabular Baseline: Linear Regression
- Multimodal Model:
  - ResNet-50 (pretrained) for image feature extraction
  - Linear Regression for final prediction

The CNN is used as a fixed feature extractor without fine-tuning.

--------------------------------------------------

Evaluation Metrics
------------------
- Root Mean Squared Error (RMSE)
- R² Score

--------------------------------------------------

Results Summary
---------------
Tabular Baseline Model:
- RMSE ≈ 231,000
- R² ≈ 0.57

Multimodal Model (Tabular + Images):
- RMSE ≈ 123,000
- R² ≈ 0.52

The multimodal model reduces absolute prediction error but shows a slight decrease
in explained variance compared to the baseline.

--------------------------------------------------

Final Output
------------
Prediction File:
- Name: 23116042_final.csv
- Format: id, predicted_price
- No missing values
- No negative prices (post-processing applied)

--------------------------------------------------

Notes
-----
- Linear Regression was chosen for simplicity and interpretability.
- Satellite imagery is used to capture environmental context.
- Grad-CAM and advanced explainability techniques were not implemented.
- Negative predictions from linear regression were clipped to zero during
  post-processing to ensure realistic outputs.

--------------------------------------------------

How to Run
----------
1. Run preprocessing.ipynb
2. Run data_fetcher.ipynb
3. Run model_training.ipynb
4. Run 05_final_predictions.ipynb

--------------------------------------------------
