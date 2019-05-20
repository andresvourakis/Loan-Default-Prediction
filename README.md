# Anyfin Data Science Case Solution

## Overview
The goal was to build a predictive model that assigns default probabilities to loan applications. 

**Optimization:** It was assumed that the business cares a lot more about accurately predicting defaulters rather than non-defaulters. Therefore, the predictive model was optimized for sensitivity (recall).

## Approach
In order to tackle this problem, the dataset provided was used to train a classification model. I began by doing some exploratory data analysis in order to better understand it's features and clean the data in preparation for the model building step. During the model building step, the data was transformed to get it ready for training. I trained Several classification models then compared them each other using accuracy, sensitivity and precision scores. Here is how the problem was approached in more detail:

### EDA and Cleaning
Exploratory data analysis and cleaning to prepare for the model building step.

1. Data Gathering
2. Exploratory Data Analysis (EDA)
3. Data Cleaning

More details can be found on the `1-Data-Cleaning-And-EDA.ipynb` notebook.

### Model Building
Model Selection and building the final model.

1. Data Prepation:

    * One-hot Encoding    

2. Model Selection

    First, four different classfication models were compared to each other using accuracy, sensitivity, and precision scores. No hyperparameter tuning was performed on this step since it can be computationally costly and I first wanted to identify the models that were worth tuning.

    <img src="Plots/class_comp.png">

    **Observations:** Since our goal is to optimize our model for sensitivity (more accurately predict defaults), it seems like the best algorithm would be the RandomForestClassifier. It has a high sensitivity and an even higher precision score, and since both scores are inversely related, improving the sensitivity will still leave us with a decent precision score, giving us a good model overall. SVC has an almost perfect sensitivity score, but a very low precision score. This probably means that there is some bias and that it won't do a good job generalizing. Although we care about accurately predicting defaults, we don't want this to have a huge effect on our ability to accurately predict no defaults (acquire new customers).

    Now, only taking the top three performind classifiers, basic hyperparameter tuning was performed, and the best combinations were used to retrain the models and compare them to each other

    <img src="Plots/class_comp_tuned.png">

    **Observations:** 

    Here are some of the techniques used:

    * Over-sampling: The SMOTE technique was used to over-sample to data.
    * Model Validation: Cross-validation was used to 
    * Feature Selection: No feature selection, aside from dropping some columns during the data cleaning step.
    * Hyperparameter Tuning: Grid Search Cross Validation was used to fine tune the hyperparameters for each of the classification models that were being trained.


3. Building Final Model

More details can be found on the `2-Model-Building.ipynb` notebook.

## Final Model
The final classification model selected was Random Forest Classifier.

### Potential ways to further improve the model:
* More Data
* Better Feature Selection
* More Hyperparameter tuning