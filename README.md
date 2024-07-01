# Water quality analysis for the Thames River

## Introduction
In this project, we employ superstatistical methods and machine learning to analyze measured time series data of water quality indicators from the River Thames. Particular emphasis is placed on unraveling the complex underlying dynamics of water quality indicators.

## Data
Download real-time water quality measurements from the Meteor Data Cloud at "https://telemetry-data.com/viewer2," provided by the Environmental Agency. Contact the agency directly to obtain the necessary access credentials. Choose the river, time span, and water quality indicators as needed. This project specifically focuses on data from the Thames River between December 1, 2017, and December 1, 2022, but the methodology can be extended to other rivers.

In our project, we use the following water quality indicators:

1. Dissolved oxygen (DO), measured in milligrams per liter (mg/L).
2. Temperature (Temp), measured in degrees Celsius (°C).
3. Electrical conductivity (COND), measured in microsiemens per centimeter (μS/cm).
4. pH (PH), ranging from 0 to 14.
5. Ammonium (AMMONIUM), measured in milligrams per liter (mg/L).
6. Turbidity (TURBIDITY), measured in nephelometric turbidity units (NTU).

The data sets retrieved contain several problems. Below are some of the main issues and the ways in which we rectify them:
1. DO and DO-MGL parameters not considered, instead use the DOO-MGL parameter measured with an optical optode for more reliable data. 'DOO-MGL' is equivalent to the commonly known 'DO' in this project.
1. DO measurements exceeding 25mg/L are deemed faulty and discarded, as achieving a concentration as high as 25mg/L is generally unlikely under standard conditions.
2. Remove non-positive measurements for ’COND’, ’PH’, ’AMMONIUM’, ’Turbidity’ and ’DO’ indicators.
3. Remove large spikes and sudden dropouts due to probe faults or human activities, such as the
oxygen pumped into the river from a boat in August 2022.
4. COND measurements in ms/cm unit, change to us/cm.
5. Remove data outages, which were caused by sonde changes.

## The data processing
Process the data: Import the raw data into the Jupyter Notebook file named *dataframe.ipynb*. Apply robust filtering techniques to remove any faulty or inaccurate measurements. Save the cleaned data for further analysis.

## Superstatistical analysis



## Regression analysis
In this section, we compare the LGBM regression model to the XGBoost and linear regression baselines, in both SMAPE and the SHAP values of each of the features. Each model has its own notebook file: LGBM_basic.ipynb for LGBM regression, XGBoost_baseline.ipynb for XGBoost, and Linear_Regression_baseline.ipynb for linear regression. For each method, set the path to your local path to the site data being tested and uncomment the appropriate features.



## Sequential forecasting 

In this section, we compare numerous effective existing forecast models with the recently developed transformer, namely Informer, which is the state-of-the-art machine learning techniques. This techinques are based on [Time series forecasting](https://github.com/tensorflow/docs/blob/master/site/en/tutorials/structured_data/time_series.ipynb) and [Informer2020](https://github.com/zhouhaoyi/Informer2020). Modifications were made to suit the water quality time series.

1. Choose a specific dataset from one site and import it into another Jupyter Notebook file named time_series_forecasting.ipynb. Execute the notebook ten times and calculate the average of the mean absolute error (MAE) to evaluate model performance.
   
2. Finnaly,import the data to *Informer2020* folder, and run the *informer.ipynb*, where you can set the input, label and prediction lengths. The performance evaluation will be saved in the *metrics.npy* in the *results* folder.

3. Compare the MAE from all models and deduce the model with the best predictive capability.

