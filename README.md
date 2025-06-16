# British Airways Booking Sales Conversion Machine Learning - Project Overview


This project aimed to evaluate whether customer booking data could be used to predict the likelihood of a holiday purchase. The goal was to build an interpretable machine learning model that could support proactive engagement strategies by identifying high-intent customers before they leave the booking flow.
---
British Airways, a major global airline, faces increasing competition and changing consumer behavior in the travel industry. As customers now have access to a wealth of options online, booking decisions are more fragmented and price-sensitive than ever. The airline wanted to shift from reactive marketing efforts to a more proactive strategy that leverages data to anticipate when and which customers are most likely to convert.

The project was framed around a realistic data simulation involving 50,000 customer interactions, with a focus on predicting whether a customer would complete a holiday booking. The company sought to understand which early-stage behaviors (e.g., trip type, purchase lead time, interest in extras) could be used to build a reliable predictive model. The end goal was to enable targeted interventions and marketing efforts before customers abandon the booking process.

## Executive Summary

This project analyzed 50,000 customer holiday booking records to determine the feasibility of predicting purchase behavior based on booking patterns and customer interactions. The overall booking conversion rate was approximately 15%, prompting a focus on identifying high-intent segments. A supervised machine learning model was developed and calibrated to improve recall, ultimately identifying 39% of actual bookers while maintaining a precision of 36%. The model’s ROC AUC score of 0.76 indicates strong discriminatory power in ranking likely bookers above non-bookers. 

Key behavioral drivers included purchase lead time, customer add-on selections, and trip type, particularly round trips. These insights support the use of predictive modeling to proactively engage customers before booking abandonment.

![dashboard](https://github.com/JzesatiD/british_airlines_dataproj/blob/main/assets/dashb.png?raw=true)
---
### Plan: 
We need a "proactive" approach to acquiring customers before they embark on their holiday. 
- A data PREDICTIVE model
- y = β₀ + β₁x₁ + β₂x₂ + ...

### Method: 
- Build a predictive model
- Use Machine Learning to train it
- Evaluate the model’s performance and output how each variable contributes to the predictive model’s power.
- Interpret results to measure the model's predictive effectiveness

## Target: 
Predict the target outcome (customers buying holidays). 

## Explanatory Variables Info

RangeIndex: 50000 entries, 0 to 49999
Data columns (total 14 columns):
 #   Column                 Non-Null Count  Dtype  
---  ------                 --------------  -----  
 0   num_passengers         50000 non-null  int64  
 1   sales_channel          50000 non-null  object 
 2   trip_type              50000 non-null  object 
 3   purchase_lead          50000 non-null  int64  
 4   length_of_stay         50000 non-null  int64  
 5   flight_hour            50000 non-null  int64  
 6   flight_day             50000 non-null  object 
 7   route                  50000 non-null  object 
 8   booking_origin         50000 non-null  object 
 9   wants_extra_baggage    50000 non-null  int64  
 10  wants_preferred_seat   50000 non-null  int64  
 11  wants_in_flight_meals  50000 non-null  int64  
 12  flight_duration        50000 non-null  float64
 13  booking_complete       50000 non-null  int64  
dtypes: float64(1), int64(8), object(5)

**Context**
num_passengers = number of passengers travelling
sales_channel = sales channel booking was made on
trip_type = trip Type (Round Trip, One Way, Circle Trip)
purchase_lead = number of days between travel date and booking date
length_of_stay = number of days spent at destination
flight_hour = hour of flight departure
flight_day = day of week of flight departure
route = origin -> destination flight route
booking_origin = country from where booking was made
wants_extra_baggage = if the customer wanted extra baggage in the booking
wants_preferred_seat = if the customer wanted a preferred seat in the booking
wants_in_flight_meals = if the customer wanted in-flight meals in the booking
flight_duration = total duration of flight (in hours)
booking_complete = flag indicating if the customer completed the booking


## Phases: 

PHASE 1: Data Understanding & Preparation
1. Understand the Target
Plot and calculate the % of bookings (booking_complete)

Recognize imbalance (~5–10% positive class)

Why: Sets the baseline for your evaluation strategy later (i.e., don't rely on accuracy).

2. Explore Numeric Features
Features: num_passengers, purchase_lead, length_of_stay, flight_hour, flight_duration

Visualize with histograms

Run logistic regression to see which are predictive

Why: Understand customer behavior patterns and identify strong predictors.

3. Explore Categorical Features
Features: sales_channel, trip_type, route, booking_origin

Plot conversion rates by category using groupby(...).mean()

Why: See which categories tend to lead to bookings; helps you decide how to encode.

4. Encode Categorical Variables
One-hot encode sales_channel, trip_type, and booking_origin

For route, group top 10 most common routes; label others as "Other", then one-hot encode

Why: Translates categories into model-readable format while avoiding overfitting via too many dummies.

5. Prepare Final Dataset
Drop or rename unnecessary columns

Split into X (features) and y (target)

If using logistic regression or distance-based models, normalize numeric columns with StandardScaler

Why: Ensures clean input for modeling

PHASE 2: Build & Evaluate the Model
6. Train/Test Split
Use train_test_split (e.g., 80/20, stratified on target)

Why: Simulates how your model performs on new, unseen customers.

7. Choose and Train Model
Use RandomForestClassifier with class_weight='balanced' to handle imbalance and get feature importances

Optional: Try LogisticRegression if interpretability is your top priority

Why: Random Forest is robust, interpretable, and handles mixed types well

8. Evaluate Model Performance
Use:

Classification report (precision, recall, F1)

ROC AUC score

Confusion matrix (optional)

Why: These metrics are more meaningful than accuracy with imbalanced classes.

9. Interpret Feature Importance
Plot top 10 most important features from the model

Why: Helps explain the business value — which customer attributes actually predict bookings?

PHASE 3: Communicate the Findings (Slide)
10. Single-Slide Summary (per instructions)
Include:

Objective: “Predict likelihood of booking based on customer and booking data”

Key drivers: e.g., “Short lead time, extra baggage, mobile channel”

Model used: Random Forest, balanced, basic tuning

Performance: e.g., “AUC = 0.78; Precision = 0.42 on booking class”

Business impact: “Allows early targeting of high-intent customers before checkout”

Why: Clear, digestible summary for your “manager” (per prompt) with actionable insight

