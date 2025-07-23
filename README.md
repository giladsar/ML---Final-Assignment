# Predicting Ghosting in Tinder Data – Course Project

This repository contains the materials for the final assignment in a graduate course on machine learning. The goal of the project is to demonstrate how to build end‑to‑end predictive models in **R**, including feature engineering, model training, cross‑validation, model comparison and interpretation.

## Research question

Online dating platforms generate rich behavioural data. In this project we investigate **ghosting** – the tendency of a user to abandon a conversation without warning. Using anonymised usage statistics from the Tinder dating app, we ask:

> **Can the tendency to ghost after an initial message be predicted from users’ demographic information and app usage patterns?**

To answer this question we build and compare two tree‑based models (Random Forest and Gradient Boosting) using cross‑validation. We evaluate each model’s predictive performance, perform hyper‑parameter tuning, estimate out‑of‑sample performance, and interpret variable importance.

## Dataset

The data come from the anonymised **Tinder Usage Statistics** dataset by Ashley Xu on Kaggle. It contains records for 1 209 Tinder users with 31 columns describing demographic and behavioural variables. A few examples are:

| Column | Description |
|------------------------------------|------------------------------------|
| `sum_app_opens` | Total number of times the user opened the app |
| `no_of_days` | Number of days the user was active on the platform |
| `nrOfConversations` | Count of conversations the user had |
| `nrOfGhostingsAfterInitialMessage` | Number of times the user ghosted someone after a first message (target) |
| `no_of_msgs_sent`, `no_of_msgs_received` | Counts of messages sent and received |
| `swipe_likes`, `swipe_passes` | Number of “like” and “pass” swipes |
| `birthDate`, `gender`, `education`, `jobTitle` | Demographic and profile features |

The full cleaned dataset is stored in `Tinder_Data_v3_Clean_Edition.csv` at the repository root. For privacy, no personally identifiable information is included; user identifiers are anonymised and job titles are free‑text descriptions such as “Research Assistant” and “Physician”.

## Repository structure

```         

.  
├── README.md # This file  
├── report.docx # Word report of the project (6 pages maximum)  
├── analysis.R # R script containing data import, preprocessing, modelling and evaluation  
├── Tinder_Data_v3_Clean_Edition.csv # Dataset used in the analysis  
└── figures/ # Folder for generated figures and plots
```

### Word report (`ML_FINAL.docx`)

The report is the main deliverable and is limited to six pages. It includes:

1.  **Introduction** – brief context for why we care about ghosting on dating apps and a statement of the research question.
2.  **Methods and results** – detailed description of preprocessing, feature engineering, hyper‑parameter tuning, model training, cross‑validation, comparison of models on relevant metrics (e.g., accuracy, F1, AUC) and variable importance/SHAP analysis.
3.  **Discussion** – interpretation of the findings and reflections on differences (or similarities) between models.

### Analysis script (`ML_FINAL.qmd`)

The script can be executed to reproduce the analysis. It is organised as follows:

1.  **Load packages and data** – uses `tidyverse` and `tidymodels` for data manipulation and modelling. Additional packages such as `ranger` (random forest), `xgboost` (gradient boosting), `vip` or `DALEX` (model explanation) are loaded as required.
2.  **Preprocessing pipeline** – handles missing values, encodes categorical variables (e.g., converts `jobTitle` strings into factors and performs one‑hot encoding), scales or transforms features where appropriate, and constructs new features (e.g., message ratios).
3.  **Resampling** – splits the data into training and test sets and defines bootstrap or k‑fold resampling for hyper‑parameter tuning. Hyper‑parameter search grids are specified for each model.
4.  **Model training and tuning** – fits Random Forest and Gradient Boosting models on the training data, performs tuning using cross‑validation, and selects the best hyper‑parameters based on a chosen metric.
5.  **Model comparison** – evaluates both tuned models using repeated resampling on the test set to estimate out‑of‑sample performance and compares them using metrics such as accuracy and F1.
6.  **Model interpretation** – extracts variable importance and uses model‑agnostic methods (e.g., SHAP values) to identify which predictors are most influential.
7.  **Saving outputs** – writes tables and figures to the `figures/` directory for inclusion in the report.

To run the analysis from a fresh R session:

``` r
# Install required packages (if not already installed)
install.packages(c("tidyverse", "tidymodels", "ranger", "xgboost", "DALEX", "vip"))

# Source the script
source("ML_FINAL.qmd")
```

All preprocessing steps are performed within resampling folds to avoid data leakage. Results should be reproducible on any system with R 4.0 or higher.

## Reproducing the study

1.  Clone or download this repository.

2.  Ensure that `Tinder_Data_v3_Clean_Edition.csv` is present in the working directory.

3.  Open the R script (`ML_FINAL.qmd`) and run it. This will generate the models and save figures used in the report.

4.  Open `ML_FINAL.docx` for the full write‑up of methods and results.

## Dependencies

This project was developed using R 4.3 and the following packages:

-   `tidyverse` – data manipulation and visualization

-   `tidymodels` – cohesive framework for modelling and machine learning

-   `ranger` – fast implementation of Random Forest

-   `xgboost` – gradient boosting

-   `vip` / `DALEX` – variable importance and explanatory analysis

Additional dependencies may be specified at the top of the analysis script.

## License

The code and report in this repository are released under the **MIT License**. The dataset is provided for educational and research purposes only; please refer to the original Kaggle licence and terms of use.

## Acknowledgements

This project is part of the coursework for a machine learning class. We thank Ashley Xu for releasing the Tinder usage dataset on Kaggle and Christoph Molnar, Timo Freiesleben, and the authors of *Explanatory Model Analysis* and *An Introduction to Statistical Learning* for their freely available materials that guided our methodology.
