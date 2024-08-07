# Water quality analysis for the Thames River

## Introduction
In this project, we employ superstatistical methods and machine learning to analyze measured time series data of water quality indicators from the River Thames. Particular emphasis is placed on unraveling the complex underlying dynamics of water quality indicators.

## Requirements
* Python 3.9
* numpy==1.20.1
* pandas==1.2.3
* scikit-learn==1.4.2
* matplotlib==3.3.4
* seaborn==0.13.2
* tensorflow==2.11.0
* lightgbm==3.3.5
* xgboost==1.7.3
* torch==2.0.0

To install the required dependencies, use the following command:
```bash
pip install -r requirements.txt
```

## Data
Download real-time water quality measurements from the Meteor Data Cloud at "https://telemetry-data.com/viewer2," provided by the Environmental Agency out of their generous courtesy. Contact the agency directly to obtain the necessary access credentials. Choose the river, time span, and water quality indicators as needed. This project specifically focuses on data from the Thames River between December 1, 2017, and December 1, 2022, but the methodology can be extended to other rivers.

In our project, we use the following water quality indicators:

1. Dissolved oxygen (DO), measured in milligrams per liter (mg/L).
2. Temperature (Temp), measured in degrees Celsius (°C).
3. Electrical conductivity (COND), measured in microsiemens per centimeter (μS/cm).
4. pH (PH), ranging from 0 to 14.
5. Ammonium (AMMONIUM), measured in milligrams per liter (mg/L).
6. Turbidity (TURBIDITY), measured in nephelometric turbidity units (NTU).

For a geographical overview of our water quality monitoring sites as well as rainfall collection sites along the River Thames, run Map.ipynb to recreate the interactive HTML map. You can hover over the map to check locations.

## The data processing
Process the data: Import the raw data into the Jupyter Notebook file named *dataframe.ipynb*. Apply robust filtering techniques to remove any faulty or inaccurate measurements. 
The data sets retrieved contain several problems. Below are some of the main issues and the ways in which we rectify them:
1. DO and DO-MGL parameters not considered, instead use the DOO-MGL parameter measured with an optical optode for more reliable data. 'DOO-MGL' is equivalent to the commonly known 'DO' in this project.
1. DO measurements exceeding 25mg/L are deemed faulty and discarded, as achieving a concentration as high as 25mg/L is generally unlikely under standard conditions.
2. Remove non-positive measurements for ’COND’, ’PH’, ’AMMONIUM’, ’Turbidity’ and ’DO’ indicators.
3. Remove large spikes and sudden dropouts due to probe faults or human activities, such as the
oxygen pumped into the river from a boat in August 2022.
4. COND measurements in ms/cm unit, change to us/cm.
5. Remove data outages, which were caused by sonde changes.

Save the cleaned data in your folder for further analysis.

Here is a table showing the descriptive statistics of cleaned DO levels data for different sites:

<img src="https://github.com/hurst0415/Water-quality-analysis-for-the-Thames-River/blob/main/stats.png?raw=true" alt="Descriptive Statistics" width="500" height="400">

## Superstatistical analysis
### Statistical Anlysis
Run the "Statistical_analysis.ipynb" notebook to visualize the trajectories and probability density functions (PDFs) of the time series data from the measured sites.

### Detrending
Our approach focuses on describing fluctuations around the mean rather than modeling the complete distribution. Execute the notebooks "Detrending-additive.ipynb" and "Detrending-multiplicative.ipynb" for additive and multiplicative detrending methods, respectively.

### Superstatistical Results
The fluctuations deduced from the detrending methods can be well modeled by q-Gaussian distributions, as demonstrated by the results in "Detrending-additive.ipynb" and "Detrending-multiplicative.ipynb". Save the log-likelihood results and parameters for the best-fitting q-Gaussians, then run "Superstatistical results.ipynb". This notebook compares the robustness of different detrending methods and displays the spatial plot of parameters.


## Regression analysis

In this section, we compare the LGBM regression model to the XGBoost and linear regression baselines, in both SMAPE and the SHAP values of each of the features. Each model has its own notebook file: LGBM_basic.ipynb for LGBM regression, XGBoost_baseline.ipynb for XGBoost, and Linear_Regression_baseline.ipynb for linear regression. For each method, set the path to your local path to the site data being tested and uncomment the appropriate features.



## Sequential forecasting 

In this section, we compare numerous effective existing forecast models with the recently developed transformer, namely Informer, which is the state-of-the-art machine learning techniques. This techinques are based on [Time series forecasting](https://github.com/tensorflow/docs/blob/master/site/en/tutorials/structured_data/time_series.ipynb) and [Informer2020](https://github.com/zhouhaoyi/Informer2020). Modifications were made to suit the water quality time series.

1. Choose a specific dataset from one site and import it into another Jupyter Notebook file named time_series_forecasting.ipynb. Execute the notebook ten times and calculate the average of the mean absolute error (MAE) to evaluate model performance.
   
2. Finnaly,import the data to *Informer2020* folder, and run the *informer.ipynb*, where you can set the input, label and prediction lengths. The performance evaluation will be saved in the *metrics.npy* in the *results* folder.

3. Compare the MAE from all models and deduce the model with the best predictive capability.

