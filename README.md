# Flood Susceptibility Analysis and DFSI Estimation Using Machine Learning

## Project Overview

This project analyzes district-level flood indicators in India and applies machine learning regression techniques to estimate the District Flood Susceptibility Index (DFSI) from selected flood-related variables.

The project uses Python for data cleaning, exploratory data analysis (EDA), visualization, model development, evaluation, and model saving.

**Note:** This is a preliminary DFSI estimation project, not a validated system for forecasting future flood events.

## Objectives

- Analyze district-level flood data and identify patterns in flood indicators.
- Explore relationships between flooded area, permanent water coverage, flood duration, and DFSI.
- Build and compare machine learning regression models.
- Evaluate model performance using MAE, RMSE, and R².
- Identify influential features using Random Forest feature importance.
- Save the trained model for future use.

## Tools and Technologies

- **Language:** Python
- **Libraries:** Pandas, NumPy, Matplotlib, Scikit-learn, Joblib
- **Environment:** Jupyter Notebook
- **Machine Learning:** Random Forest Regression, Gradient Boosting Regression
- **Evaluation:** MAE, RMSE, R², 5-fold cross-validation

## Dataset

The analysis combines district-level datasets containing flood-related information, including:

- Percentage of flooded area
- Permanent water coverage
- Corrected percentage of flooded area
- Mean flood duration
- Human fatalities and injuries
- Population
- District Flood Susceptibility Index (DFSI)

Data cleaning included district-name normalization, handling missing values, and reviewing ambiguous district matches.

## Project Workflow

1. **Data preparation:** Load and clean the source datasets.
2. **Exploratory data analysis:** Review descriptive statistics, distributions, and correlations.
3. **Dataset integration:** Combine flood-area, flood-impact, and DFSI information at district level.
4. **Feature preparation:** Select four flood-related features and impute missing feature values using the median.
5. **Model development:** Train Random Forest and Gradient Boosting regression models.
6. **Model evaluation:** Compare both models with a mean-baseline model.
7. **Cross-validation:** Evaluate Random Forest using five-fold cross-validation.
8. **Interpretation:** Visualize actual versus predicted DFSI and examine feature importance.
9. **Model saving:** Save the trained model and imputer using Joblib.

## Model Performance

Random Forest achieved the best results among the three models evaluated on the held-out test set.

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Random Forest | 1.766 | 2.383 | 0.364 |
| Gradient Boosting | 1.910 | 2.439 | 0.334 |
| Mean Baseline | 2.444 | 2.988 | ≈ 0.000 |

### Cross-Validation

Random Forest five-fold cross-validation results:

- **Mean MAE:** 1.752
- **Standard deviation:** 0.146

MAE and RMSE measure prediction error, so lower values are better. R² measures how much variation the model explains relative to a baseline, with higher values generally preferred.

## Feature Importance

The fitted Random Forest model ranked the selected features as follows:

| Feature | Importance |
|---|---:|
| Mean Flood Duration | 38.50% |
| Corrected Flooded Area | 23.39% |
| Permanent Water | 19.32% |
| Percentage of Flooded Area | 18.79% |

These values describe the model's relative use of the features; they do not establish causal relationships.

## Key Findings

- Random Forest outperformed Gradient Boosting and the mean baseline on the test split.
- Flood duration had the highest feature importance in the fitted model.
- Cross-validation produced a mean MAE close to the single test-split MAE.
- The test R² of 0.364 indicates that substantial variation in DFSI remains unexplained.

## Limitations

- District-level matching needs further validation, particularly for districts with identical names across different states.
- Some DFSI values are missing.
- The DFSI calculation methodology and its relationship to the selected input features must be confirmed.
- Flood-related input features may overlap with the methodology used to calculate DFSI, potentially causing target leakage.
- Random cross-validation does not establish performance on geographically independent districts.
- The current model estimates existing DFSI scores; it does not forecast future flood events.

## Future Improvements

- Validate source records and district-state mappings.
- Confirm the DFSI definition and calculation methodology.
- Investigate potential target leakage.
- Incorporate independent rainfall, elevation, slope, river proximity, land-use, and other geospatial predictors where reliable data are available.
- Evaluate generalization using geographically separated validation data.
- Develop a map-based dashboard after the data and model have been validated.

## Saved Model Files

- `flood_dfsi_model.pkl` — trained Random Forest regression model.
- `flood_duration_imputer.pkl` — imputer used to handle missing feature values.

## Conclusion

This project demonstrates a complete preliminary machine learning workflow, from district-level data preparation and exploratory analysis to regression modeling, evaluation, interpretation, and model persistence.

The results provide a starting point for further research into district-level flood indicators. Additional data validation and independent environmental predictors are necessary before the model can be considered reliable for real-world flood-susceptibility assessment.
