# **MAXIMIZING REVENUE FOR TAXI CAB DRIVERS THROUGH PAYMENT TYPE ANALYSIS**

### **PURPOSE**

 Analyze whether payment method (Card vs Cash) is associated with differences in fare amounts to inform strategies that could increase driver revenue.

 ### **METHODOLOGY**

 ***Descriptive Analysis*** : Performed statistical analysis to summarize key aspects of the data, focusing on fare amounts and payment types.

***Hypothesis Testing*** : Conducted a T-test to evaluate the relationship between payment type and fare amount, testing the hypothesis that different payment methods influence fare.

### **STEPS**

***preprocessing***:
- Convert datetime columns, compute trip duration (minutes), remove duplicates, filter invalid/zero values, and remove outliers using the IQR rule for fare_amount, trip_distance, and duration.

***EDA***:
- Visualizations include histograms of fare by payment type, distribution plots for trip distance, pie chart for payment preference, and stacked/annotated bar visualizations by passenger count.

***Hypothesis Testing***
- Null: No difference in average fare between Card and Cash payment groups.
Alternative: There is a difference in average fare between the groups.
Test used: Welch's t-test (scipy.stats.ttest_ind(..., equal_var=False)).

### **KEY FINDINGS**

- Payment Preference: Card payments are substantially more common than cash in the sample.
- Fare & Distance: Card-paying customers tend to have higher average trip distances and higher mean fares.
- Statistical Result: Welch's t-test produced a very small p-value (≈ 0), leading to rejection of the null hypothesis — average fares differ between Card and Cash payers (Card higher on average).

### **CONCLUSION AND RECOMENDATIONS**

- Payment method is significantly associated with fare amount; card payments correspond to higher average fares.

- Encourage and facilitate card payments (e.g., improved card-processing UX, promotions).
Consider targeted incentives to nudge customers toward card use for higher-revenue rides.
Preserve a positive customer experience while promoting preferred payment methods.

### **LIMITATIONS**

- Causality: Analysis is observational; correlation does not imply causation.
- Other variables (time of day, ride purpose, passenger demographics) were not controlled and may influence the result.
- Data Scope: Single-month snapshot (2015-01); results may not generalize across seasons/years or markets.
