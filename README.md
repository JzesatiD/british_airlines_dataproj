# British Airways Machine Learning Project

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

