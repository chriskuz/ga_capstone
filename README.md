# Determining Airline Prices
By: Chirstopher Kuzemka : [Github](https://github.com/chriskuz/ga_capstone)

## Problem Statement

Aviation is one of the largest industries dominating our global market today. Commercial aviation has made it possible for people to connect with each other in ways that may have been unimaginable over a century ago. However, a lot of thought must be put into the FAA standards and routes that modern planes must make today to make such connections possible.

Consider the case example where a startup airliner, known as "Kruze", wants to establish itself as a top competitor against existing airliners today. A part of this startup process focuses on understanding the costs that will come into play when managing flights. Our job as data scientists today is to help Kruze determine the minimum threshold cost the airliner must charge their passengers in order to break even with a profit. To do this, we are going to analyze seven different locations where Kruze would like to establish themselves and examine existing flight route data as well as existing flight ticket prices (as a prediction) to help us create a supervised learning model. 

To start, we will approach the project with the intention of expressing a minimum proof of concept. With such introduction, we will make some limitations to our study and decrease the potential for scope increase by:

- only analyzing the seven airports as destination hubs for different flights: 
    - New York John F. Kennedy Airport (KJFK)
    - Chicago O'Hare International Airport (KORD)
    - Los Angeles International Airport (KLAX) 
    - Houston George Bush Intercontinental Airport (KIAH)
    - Miami International Airport (KMIA)
    - Hatsfield-Jackson Atlanta International Airport (KATL)
    - Portland International Airport (KPDX)
- assuming external costs from the study (including maintenance/crew salary) to be negligible
- using price data from future flights as opposed to previous flights as previous flight pricing is not readily available


All current assumptions labeled are set to allow us to achieve (or attempt to achieve) our goal within a certain time frame, as Kruze is requiring an answer from us quickly! With this in mind, we will consider discussing how such assumptions can contribute to any error throughout our study, as well as remind ourselves that integrating negated features for future work may actually be very beneficial to us in achieving a stronger prediction.

As we are working with what is considered to be a continuous variable, we will analyze common price trends utilizing a supervised regression model, such as Linear Regression, KNNRegression, Bagging Regression, and Decision Tree Regression. We will ultimately be using the Mean Absolute Error against our predictions to help us gauge how well our selected model predicts the price and discuss what issues may be observed from the limitations of this study. The Mean Absolute Error seems the most appropriate to analyze pricing values as the error is in the scale of our predictions and is much clearer for anyone to understand the general error of the model in absolute terms. 



## Executive Summary

A study was conducted on flight data and flight pricing data to help the startup airliner, known as Kruze, determine ticket price thresholds for passengers. The data was gathered through an API, produced by, FlightAware.com known as "FlightXML2." FligthXML2 is a popular API utilized by various companies affiliated with the airline and travel business to observe different types of flight data. With this API, a search was conducted on the seven destination airports explained in the problem statement above where up to 15 flights were searched on a real-time basis on a given day in May. These 15 different flights (origin-destination combinations) per airport were then searched through the API again to determine their May 2020 schedule on an 8 hour frequency. The search ultimately costed the data scientist approximately $120. The data returned were different departure and arrival times for every flight combination discovered within the month of May, including airline data, aircraft type data, technical details, and more. 

To gather quotes on flights, the Skyscanner API was utilized. It was impossible to determine the pricing data of past flights, so future quotes were substituted for the flight pricing -- this meant past flight information was utilizing future pricing. The Skyscanner search analyzed the best monthly quote for every origin-destination combination from June 2020 to December 2021. Various features including actual city names, carrier id's, and country information was also gathered from this quotes search. This dataframe containing quotes was combined with the flight scheduling dataframe to create a large dataframe directly meant for modeling. Through some bootstrapping methods, where different prices were sampled randomly onto the flight scheduling dataframe, an approximate 5,000 row dataframe was ultimately utilized to show pattern relationships between features and our main target, the pricing.

After all the arduous cleaning necessary to create a dataframe for modeling, four different supervised models were implemented: Linear Regression, KNN Regression, Bagging Regression, and Decision Tree Regression. The Bagging regression model was considered to be the best performing model out of all of the models due to the smaller differences found in the mean absolute error scores in the training, testing, and cross validated scores. With all this mentioned, the study has room for improvement. Much bias exists in the data, mainly regarding the role the Covid-19 pandemic has played, as well as how such bias combatted by implementing other biases into the search. The bootstrapping method was also contributing to inaccuracies with regard to proper carrier identification implementation. 


## Data Dictionary
|__Data Variable__|__Type__|__Significance__|
|---|---|---|
|`ident`|__String Object__|*identification of a flight*|
|`actual_ident`|__String Object__|*original identification of a codeshared flight*|
|`departuretime`|__String Object__|*departure time of flight including date, hours, and minutes*|
|`arrival_time`|__String Object__|*arrival time of flight including date, hours, and minutes*|
|`origin`|__String Object__|*origin ICAO code*|
|`destination`|__String Object__|*destination ICAO code*|
|`aircrafttype`|__String Object__|*type of aircraft flown*|
|`meal_service`|__String Object__|*type of meal service provided on flight*|
|`seats_cabin_first`|__Integer__|*number of first class seats available*|
|`seats_cabin_business`|__Integer__|*number of business class seats available*|
|`seats_cabin_coach`|__Integer__|*number of coach class seats available*|
|`origin_IATA`|__String Object__|*origin IATA code*|
|`destination_IATA`|__String Object__|*destination IATA code*|
|`flight_duration`|__String Object__|*flight duration in seconds*|
|`MinPrice`|__Float__|*minimum price for a ticket on the flight*|
|`Direct`|__Boolean Object__|*boolean state if the route was direct or had stops*|
|`OriginName`|__String Object__|*origin airport name*|
|`OriginCityName`|__String Object__|*origin city name*|
|`OriginCountryName`|__String Object__|*origin country name*|
|`DestinationName`|__String Object__|*destination airport name*|
|`DestinationCityName`|__String Object__|*destination city name*|
|`DestinationCountryName`|__String Object__|*destination country name*|
|`CarrierName`|__String Object__|*carrier name affiliated with quote*|

## Conclusions and Future Work

The model performed well, but there was a great cost to the performance of this model. We must remember that:

- this study was conducted during the Covid-19 pandemic where data gathered was affecting domain

- the prices were bootstrapped in a manner where some Carrier Id's do not accurately depict the true carrier of a flight

- we are using past flights performed to predict future flight pricing. Coordination on this end would be needed for more accurate models (considering grabbing future quotes first, then grabbing flight data to search upon for each quote when the flight occurs.)

- there are many skews in our data and biases including geographical location limitations, dominating imbalances in different categorical types, risk of overfitting.

With such mentions above, which isn't inclusive of naming all of the various issues across this study, there is much future work to be done to create a better model and create a better platform for Kruze. For the future, some considerations would be to incorporate more relevant features, such as: jet fuel pricing, passenger data, jet engine analysis, more routes, travel trends, seasonality, housing prices of planes, and more. The project was semi-successful in that it showcases a minimum proof of concept, but fails to serve as a reliable model for price prediction. 