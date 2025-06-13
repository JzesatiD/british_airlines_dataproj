# British Airways Machine Learning Sales Conversions
!['deliverable'](https://github.com/JzesatiD/british_airlines_dataproj/blob/main/diaz_final_deliverable.pdf)

### Insight & Recommendation

This analysis uncovered an alarmingly low overall holiday booking conversion rate of 15%, prompting a focused investigation into what factors drive or discourage bookings. By analyzing 50,000 customer records, we identified key behavioral and demographic indicators that significantly influence booking likelihood.

Key insights include:

Trip Type: RoundTrip selections converted at 15.1%, nearly 3x higher than OneWay or CircleTrip, making it a strong signal of booking intent.

Booking Origin: Customers from Malaysia, Indonesia, and Thailand showed the highest conversion rates (up to 34.4%), revealing geographic clusters of high-intent customers.

Customer Add-ons: Requests for extra baggage, preferred seating, and in-flight meals were consistently associated with higher booking rates, indicating stronger pre-purchase intent.

Trip Characteristics: Longer trips (duration and stay length) showed a negative correlation with booking, suggesting complexity or cost may deter follow-through.

Recommendation:
Use these predictive signals to proactively target customers more likely to convert, especially those selecting RoundTrips, traveling from high-performing countries, or exhibiting interest in add-ons. Segment-specific offers and earlier engagement (e.g., shorter lead time windows) can further improve booking outcomes.

### Why This Approach Was Taken

Exploratory Analysis

We began by investigating the target variable (booking_complete), discovering a strong class imbalance (roughly 85% non-bookers). This guided our choice to use proportional metrics and segment-level visualizations (e.g., booking rates by category) instead of raw counts, to better understand performance across customer groups.

Statistical Profiling

To determine whether observed trends were statistically meaningful or just noise, we used logistic regression. This allowed us to:

Confirm statistical significance of variables (e.g., booking origin, trip type)

Understand the direction of impact (positive or negative)

Verify that the predictors had real signal, not just volume

This insight was critical for selecting features with true predictive value and excluding or downweighting less relevant attributes (e.g., flight_hour).

Predictive Modeling

We used a Random Forest classifier due to its robustness to noise, ability to handle categorical data (after encoding), and built-in interpretability via feature importance scoring.

Our model achieved:

ROC AUC Score: 0.76 — meaning the model can correctly rank a booker higher than a non-booker 76% of the time

F1 Score: 0.37 (after threshold tuning) — balancing the tradeoff between precision and recall in predicting bookings

We adjusted the classification threshold to improve recall from 12% to 39%, enabling the model to catch more real booking cases while accepting slightly more false positives — a fair tradeoff in a proactive engagement scenario.

### Business Value

This model and analysis demonstrate that it is viable and effective to predict which customers are likely to book a holiday. Key findings have direct business applications:

Customer segmentation for retargeting or priority messaging

Channel prioritization based on conversion likelihood

Route-level and region-based marketing optimization

Early behavior (e.g., extra service selection) as signals of intent

Overall, this project provides a practical foundation for data-driven, proactive customer engagement in the travel booking lifecycle.


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

