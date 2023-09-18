# Water-quality-analysis-for-the-Thames-River

## Introduction
In this project, we compare numerous effective existing forecast models with the recently developed transformer, namely Informer, which is the state-of-the-art machine learning techniques. This marks the first application of this model to sequential dissolved oxygen forecasting. 

## How to use
1. Download real-time water quality measurements from Meteor Data Cloud at "https://telemetry-data.com/viewer2", by environmnental agency, where you can choose the river and, time sapn and water quality indicators. This project focused on analysing data from the Thames River between 01/12/2017-01/12/2022, but the methodology can be applied similarly to other rivers.

2. Process the data. the data has to undergo robust filtering to remove faulty measurements. Import the data to dataframe.ipynb and save the cleansed data.

3. Select the dataset from one particluar site, and import to the time_series_forecasting.ipynb. After running 10 times, calculate the average of the mean absolute error for the performance.

4. Finnaly,import the data to Informer.ipyynb 

