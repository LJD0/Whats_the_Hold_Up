![plane.png](https://github.com/Adam-Warrick/Causes_of_Flight_Delays_and_Cancellations/blob/main/Resources/images/plane.png)

## Rememener your last flight?

    How long did you wait in the terminal? How long on the runway? It always feels like forever. Some of us have been unfortunate enough to have our flights cancelled. This analysis  aims to help identify factors that keep you held up on the plane and the airlines and airports that delays and concellations happen with the most.

## [Flights](https://www.kaggle.com/datasets/robikscube/flight-delay-dataset-20182022) Analysis

- This study uses all of the csv files in the 'raw' folder from the flight data linked above.
- Section 1 of the Notebook imports and selects the relevant columns for the analysis from those csvs
- Section 2 Cleans this data to be used in the database
- Section 3 will load to the database
- Section 4 preps the data to be analyzed in the Balanced Random forest Classifier

  - This model was used to analyze which features most impacted a flights punctuality

- Section 5 executes the ML model and returns analytics.
- Section 6 generates the vizualizations you will see below

### First look at flights

Total flights

Total dealys/ cancellations (maybe averge here too)

percentage delays/cancellation

### Delay and cancellation types

- Highest % cause of delays/cancellations

### Airports

### Airlines

## Summary

    Here will discuss the outcome of the ML model in comparison to help better identify underlying causes of delays and cancels.

(To determine an answer to the primary question that encapsulates all features of the data and how they may interact to lead to a flight being delayed or cancelled we used a classification model to predict outcomes into 3 target classes. Since the focus is understanding what are the main causes that determine flight outcomes a model that is hierarchical in its a structure was desired, and due to the number of features being used ultimately a random forest classifier was chosen. Exploratory data analysis found that while the on-time and delayed classes were similar in sample size, cancellations accounted for a small proportion of the data, so to counteract this we chose Imblearn's Balanced Random Forest Classifier that randomly under-samples the data to form decision trees.)

list of the features and their importances. (screenshot)

### What we can do

discuss airports and airlines. and underlying causes

discuss how model did or didnt relate to the outcomes of the data

(The biggest surprise the model gave is the Day of the month (irrespective of which month it is) is the 2nd highest ranked feature. Viewing this as a time series there does seem to be something to the flucations in flight outcomes when the days are aggregated for the entire period under examination, however with the data currently available to us and the scope of this analysis the causes for those fluctuations are indeterminable.

    Based on the results many more questions arise that are worth exploring. With weather being the top factor, what weather patterns lead to delays or cancellations? This factor is likely closely linked with the 4th and 5th features the model deemed important, the destination and origin airports. Why is day such a huge factor? We envision another important feature not avaiable in this data set, the number of seats sold per flight, being a large factor both overall and one that might relate to this. For the time being, consumers can make reasonable assumptions on which airlines they risk a delay or cancellation riding with, and which airports they may be delayed flying out of:)
