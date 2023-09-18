# Water-quality-analysis-for-the-Thames-River

## Introduction
In this project, we compare numerous effective existing forecast models with the recently developed transformer, namely Informer, which is the state-of-the-art machine learning techniques. This marks the first application of this model to sequential dissolved oxygen forecasting. 

## How to use
1. Download real-time water quality measurements from the Meteor Data Cloud at "https://telemetry-data.com/viewer2," provided by the environmental agency. Choose the river, time span, and water quality indicators as needed. This project specifically focuses on data from the Thames River between December 1, 2017, and December 1, 2022, but the methodology can be extended to other rivers.

2. Process the data: Import the raw data into a Jupyter Notebook file named *dataframe.ipynb*. Apply robust filtering techniques to remove any faulty or inaccurate measurements. Save the cleaned data for further analysis.

3. Choose a specific dataset from one site and import it into another Jupyter Notebook file named time_series_forecasting.ipynb. Execute the notebook ten times and calculate the average of the mean absolute error (MAE) to evaluate model performance.

4. Finnaly,import the data to *Informer2020* folder, and run the *informer.ipynb*, where you can set the input, label and prediction lengths. The performance evaluation will be saved in the *metrics.npy* in the *results* folder.

5. Compare the MAE from all models and deduce the model with the best predictive capability.

