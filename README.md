![plane](https://github.com/Adam-Warrick/Causes_of_Flight_Delays_and_Cancellations/blob/main/Resources/images/plane.png)

## Remember your last flight?

How long did you wait in the terminal? How long on the runway?

It always feels like forever. Some of us have been unfortunate enough to have our flights cancelled.

This analysis aims to identify factors that keep you held up on the plane and the airlines and airports that delays and concellations happen with the most.

## Analysis of [flight data](https://www.kaggle.com/datasets/robikscube/flight-delay-dataset-20182022) from Jan 2018 through Jul 2022

Analysis Notebook Outline

- Section 1 imports and selects the relevant columns for analysis from the Kaggle Data
- Section 2 Cleans this data to be used in the tables
- Section 3 generates vizualizations of the airline and airport data
- Section 4 preps the data to be analyzed in the Balanced Random forest Classifier
  - This model was used to analyze which features most impacted a flights punctuality
- Section 5 executes the ML model

### First look at flights

The biggest question to answer is what is the hold up?
This analysis looks at approx 30 million flights to determine just that.

Cancelled flights make up approx. 2.7% of all the flights
Delays make up approx. 40.7%.

![category_breakdown](https://github.com/LJD0/Whats_the_Hold_Up/blob/main/Resources/images/category_breakdown.png)

Cancels were classified into four categories:

- Carrier
- NAS (National Airspace System)
- Weather
- Security

Delays were classified similarly with 'Late Aircrafts' included as an additional feature

As the data suggests, The carrier you fly with with determine if you are delayed greatly.

Conversly, weather and security greatly determine the likelihood of a flight being cancelled

### Airports

Becasue weather reasons make up such a large perentage of the cancellation causes looking at airport data is our next step.

![airport count](https://github.com/LJD0/Whats_the_Hold_Up/blob/main/Resources/images/airport_total_count.png)

The data shows that the number of times an airport is flown into and out of are roughly the same.
The top five airports each represent a different part of the country seeming to diprove that weather hinders air travel.

![airport cancel count](https://github.com/LJD0/Whats_the_Hold_Up/blob/main/Resources/images/airport_cancel_count.png)

The airports with the highest number of cancellations correlate with the most flown to and from airports.
Seeing Denver and Chicago in the top cancelled airports lends credence to weather being a factor.

![airport delay count](https://github.com/LJD0/Whats_the_Hold_Up/blob/main/Resources/images/airport_delay_count.png)

Delays seem to follow the same pattern of airports. Although a shuffle does occur
Denver moving up the list of departure delays could be weather related. When each airport gets flown out of or flown to will be analyzed below.

### Airlines

While knowing which airports have more hinderances can limit our hold ups, destination alone cant always be the deciding factor of air travel.
Looking at who we can fly with may lend more insight into how to get from A to B the quickest.

![airline total count](https://github.com/LJD0/Whats_the_Hold_Up/blob/main/Resources/images/airline_total_count.png)

Soutwest Airlines has been the flight operator of choice for the time of our dataset; greatly outnumbering the next airlines in total flights.
Above,quantity of flights correlated with quantity of delays and cancellations. We will see if that holds true within airlines as well.

![airline cancel delay count](https://github.com/LJD0/Whats_the_Hold_Up/blob/main/Resources/images/airline_cancel_delay_count.png)

It comes as no surprise that the correlation holds true. Southwest has the most delays and cancellations.
Looking at percentages of delays and cancellations may prove more helpful.

![airline cancel percentage](https://github.com/LJD0/Whats_the_Hold_Up/blob/main/Resources/images/airline_cancel_percentage.png)

Cancellations make up such a small percentage of overall flights it is hard to extrapolate useful information. But the information is worth viewing.

![airline delay percentage](https://github.com/LJD0/Whats_the_Hold_Up/blob/main/Resources/images/airline_delay_percentage.png)

Delay percentages is where we are best able to gain some inferences.
As shown, most of the top airlines have over 40% of their flights delayed.
This information blurs the line between expectations of punctuality and expectation of delays.
The percentage of total flights delayed was 40.7%, using that as a benchmark, we are able to determine which airlines may not have as many hold ups.
Southwest again leads the charge with a near 50% delay chance.
Choosing to fly with an airline that falls below that 40.7% benchmark, like Delta Airlines, or SkyWest, could be a decision that saves you time in the long run.

Unfortunately the percentage of flights that get delayed is so high that we can all almost expect to have delays of some kind on our travels. Looking at how long each airlines average delay is may also help to inform our travelling schedules.

![airline_average_delay](https://github.com/LJD0/Whats_the_Hold_Up/blob/main/Resources/images/airline_average_delay.png)

While this data is shown as an representation of how long each delay can be from each operator, it is worth noting that Southwest does not make the top ten airlines in terms of delay time, even though they are number one in number of cancels and delays by a large margin.

## Can we predict hold ups?

Looking at our data through a different lens could prove useful. being able to gain more insight into which aspects of a flight best predict its delay or cancellation.
The lens being Machine Learning

Using a classification model to predict outcomes into 3 target classes: On Time, Delayed, or Cancelled, could help ascertain what the main causes that determine flight outcomes.
A model that is hierarchical in its a structure, due to the number of features being used, was deemed necessary, and ultimately a random forest classifier was chosen. Previously we found that while the on-time and delayed classes were similar in sample size, cancellations accounted for a small proportion of the data, so to counteract this we chose Imblearn's Balanced Random Forest Classifier that randomly under-samples the data to form decision trees.)

The initial run of the model using all the features was about 74% accurate

![first model run](https://github.com/LJD0/Whats_the_Hold_Up/blob/main/Resources/images/MLOutput_all.png)

In an attempt to aid the model, the features that had low importances were removed, both iterations of this process were unsuccesful, with the accuracy dropping each time.

[MLO limit1] [MLO limit2]

A model was run with features that a passenger would have a knowledge of. This model also wasnt successful.

[MLO passenger]


Even without the success of the models' predictions, the feature importances showed an interesting trend with "Day" consistently being listed as a top feature.
This is a detail that while was included in the training of the model we had deemed irrelevant, but left in anyway. The Day of the month is not a detail that one would consider having any significance in the outcome of a delay, as the First of July and the first of January have polar opposite weather conditions; each suggesting a differnet outcome.
This led to the conclusion this feature could be causing our model to be overfit and thus the innaccuracy.
Running the model without "Day" was attempted with incresingly worse results.
Attemptnig to remove dates and times in any format also proved equally unhelpful, if not worse.

[ML subset1] [ML subset2]


### What we can do?


    Based on the results, there are more questions worth exploring. With weather being the top factor, what weather patterns lead to delays or cancellations? This factor is likely closely linked with why day is such a heavily weighted feature in our models. Another important feature not avaiable in this data set, the number of seats sold per flight, might be a large unnacounted for factor as well.

For the time being, consumers can make reasonable assumptions on which airlines they risk a delay or cancellation riding with, and which airports they may be delayed flying out of based on the percentage of occurences. 

Unfortunately, with how often flights are delayed, it would seem that any expected departure or arrival times will just become wider and wider approximations.
