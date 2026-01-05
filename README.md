# Proactive Health Forecasting for Elderly Care
May 2025 - June 2025

## Overview
This undergraduate research project, conducted in collaboration with a graduate student, analyzed public Kaggle datasets to predict when a critical health metric will cross a dangerous threshold in elderly patients, enabling timely interventions to prevent adverse events.

## Objective
- Predict when health metrics will cross dangerous thresholds.
- Allow for intervention to prevent elderly injury and improve elderly quality of life.
- Determine which health metrics are the best indicators of risk.

## Data
Three datasets were downloaded from Kaggle. They were published by Suvradeep Das, and can be found here: https://www.kaggle.com/datasets/suvroo/ai-for-elderly-care-and-support/data. The data (roughly 10,000 observations) primarily related to safety alerts and reminders from devices worn by elderly individuals living independently.

Generally, the format of these datasets were:
- Daily Reminder: ID, timestamp, type of reminder (hydrate, exercise, etc.), reminder acknowledged
- Health Monitoring: ID, timestamp, heart rate, blood pressure, glucose levels, oxygen saturation
- Safety Monitoring: ID, timestamp, movement activity, fall detected, fall impact, fall location, alert triggered, caregiver notified

The goal was to predict if a fall could be predicted based on health metrics and safety alerts.

## The Analysis
- **Data Cleaning**
  - Merged datasets by ID.
  - Separated blood pressure from mm/Hg to separate Systolic and Diastolic variables.
  - Checked for NA values and removed duplicate variables.
- **SMOTE (Synthetic Minority Oversampling Technique)**
  - Initial models appeared good only because the model always predicted No Fall (due to only a Fall only happening 5% of the time).
  - SMOTE was used to create synthetic data points to balance the dataset.
  - The following models all used the new SMOTE dataset.
- **Logistic Regression**
  - The important health metrics and safety reminders/alerts were used to predict either Fall or No Fall.
  - Oxygen Saturation was found to be the only significant predictor.
- **Decision Tree**
   - A simple decision tree that allowed for easy visualization to predict Fall or No Fall.
   - Now, we find that No Movement and Oxygen Saturaton were the main predictors.
![name](visualizations/name.png)
- **XGBoost**
  - Combines multiple decision trees and uses gradient boosting to optimize the final output.
  - Created a SHAP plot to analyze feature importance.
  - Again, No Movement and Oxygen Saturation were the main predictors.
- **Conclusion**
  - Individuals with no movement activity and low oxygen saturation were the most at risk for a potential fall.
  - From personal research, more information (such as Body Mass Index) would be high beneficial to incorporate into these models.

 ## References
 Some articles and journals were used for personal research throughout the project.
 - Maklin, Cory. “Synthetic Minority Over-Sampling Technique (Smote).” Medium, Medium, 14 May 2022, medium.com/@corymaklin/synthetic-minority-over-sampling-technique-smote-7d419696b88c.
 - Vold, Monica Linea, et al. “Low Oxygen Saturation and Mortality in an Adult Cohort: The Tromsø Study.” BMC Pulmonary Medicine, U.S. National Library of Medicine, 12 Feb. 2015, pmc.ncbi.nlm.nih.gov/articles/PMC4342789/.
 - Vuori, Ilkka. “PHYSICAL INACTIVITY IS A CAUSE AND PHYSICAL ACTIVITY IS A REMEDY FOR MAJOR PUBLIC HEALTH PROBLEMS.” HRCAK, UKK Institute for Health Promotion Research, University of Tampere, Finland, 20 Apr. 2004, hrcak.srce.hr/file/6846?ev=pub_ext_prw_xdl.
