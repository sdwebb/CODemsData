# CO Legislative Forecasting

Trying to forecast state legislative elections based on data available from the [Colorado Secretary of State's office](https://www.sos.state.co.us/pubs/elections/resultsData.html?menuheaders=5)

This project entails projections of both Senate and House legislative races, and is broken into four Jupyter notebooks. 

## Exploring Trends in Registration and Vote Outcome

[2018_reg_results_trends.ipynb](./notebooks/2018_reg_results_trends.ipynb) looks at whether there is any way to forecast an outcome with the County-District combination from just registration data. There is a clear trend:

<p align="center">
  <img width="550" height="550" src="./figs/votes_vs_regs.png?raw=true">
</p>

although predictions from a simple logistic regression on this data leads to a wide range of predictions.

## Cleaning the Data

To run the models, we have to first clean the raw data from the spreadsheets from the Colorado SoS's office. This is done with the [data_cleaning_house.ipynb](./notebooks/data_cleaning_house.ipynb) and [data_cleaning_senate.ipynb](./notebooks/data_cleaning_senate.ipynb) notebooks, which should be run through once to generate the cleaned data for the model notebooks.

## Bagging Models for Election Outcomes

Once the data are cleaned, we fit neural network with a single hidden layer to predict for each COUNTY-DISTRICT the vote share for each party for the current election, using as features the vote share from the prior election, the registration composition of the prior election, and the registration composition for the current election. Because the data are not strongly correlated, our model is an ensemble of neural networks trained on only part of the data. This leads to a spread in predictions, but can be used to determine if races are close (lots of overlap in the figure below) or safe. Close races should receive more resources than safe races.
