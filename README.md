# Anyfin Data Science Case Solution

## Overview
The goal was to build a predictive model that assigns default probabilities to loan applications. 

**Optimization:** It was assumed that the business cares a lot more about accurately predicting defaulters rather than non-defaulters. Therefore, the predictive model was optimized for sensitivity (recall).

## Approach
In order to tackle this problem, the dataset provided was used to train a classification model. I began by doing some exploratory data analysis in order to better understand it's features and clean the data in preparation for the model building step. During the model building step, the data was transformed to get it ready for training. The data was then used to train several classification models which were then compared to each other using accuracy, sensitivity and precision scores. Here is how the problem was approached in more detail:

### EDA and Cleaning

1. Data Gathering
2. Exploratory Data Analysis (EDA)
3. Data Cleaning

More details can be found on the 1-Data-Cleaning-And-EDA.ipynb notebook.

### Model Building
Optimizing for Sensitivity (Recall)

1. Data Prepation:

    * One-hot Encoding    

2. Model Selection

    * Over-sampling
    * Model Validation
    * Feature Selection
    * Hyperparameter Tuning


3. Building Final Model

More details can be found on the 2-Model-Building.ipynb notebook.

## Final Model
The final classification model selected was Random Forest Classifier.

### Potential ways to further improve the model:
* More Data
* Better Feature Selection
* More Hyperparameter tuning