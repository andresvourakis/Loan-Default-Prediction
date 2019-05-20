# Anyfin Data Science Case Solution

## Overview
The goal was to build a predictive model that assigns default probabilities to loan applications. 

**Optimization:** It was assumed that the business cares a lot more about accurately predicting defaulters rather than non-defaulters. Therefore, the predictive model was optimized for sensitivity (recall).

## Approach
In order to tackle this problem, the dataset provided was used to train a classification model. I began by doing some exploratory data analysis of the dataset in order to better understand it's features and then cleaned it to prepare it for the model building step. During the model building step, the data was transformed to get it ready for training. I trained several classification models and then compared them to each other using accuracy, sensitivity and precision scores. Here is how the problem was approached in more detail:

### 1. EDA and Cleaning
Exploratory data analysis and cleaning to prepare for the model building step.

1. **Data Gathering:** I connected to the postgresql database using a python model and then saved the entire table into a pandas dataframe.
2. **Exploratory Data Analysis (EDA):** Visualized the data to understand the distribution and correlation of different features.
3. **Data Cleaning:** Performed basic pre-processing techniques which include removing rows with missing values and dropping columns that may not provide any value during prediction.

More details can be found on the `1-Data-Cleaning-And-EDA.ipynb` notebook.

### 2. Model Building
Model Selection and building of the final model.

1. **Data Prepation:** The data was prepared for training by standardizing data types, doing one-hot encoding and splitting the features from the target.   

2. **Model Selection**

    First, four different classfication models were compared to each other using accuracy, sensitivity, and precision scores. No hyperparameter tuning was performed on this step since it is computationally costly and the goal was to first identify poor performing models to exclude. Here are the results:

    <img src="Plots/class_comp.png">

    **Observations:** Since our goal is to optimize for sensitivity (more accurately predict defaults), it seems like the best algorithm would be the SVC. The problem is that it has a very low precision score, which means that it won't do a good job generalizing to new data and we still want to accurately predict non-defaulters (acquire new customers). On the other hand, Random Forest Classifier has a high sensitivity and an even higher precision score, and since both scores are inversely related, improving the sensitivity will still leave us with a decent precision score,giving us a good model overall.

    From our previous analysis, we decided to only focus on the top three classifiers. This time, I did some basic hyperparameter tuning and used the best hyperparameters to retrain the models and compare them to each other once again. Here are the results:

    <img src="Plots/class_comp_tuned.png">

    **Observations:** As we can see, all three models performed similarly, but we will choose Random Forest Classifier as our final model.

    Here is some more information about the different techniques used during the model selection step:

    * **Over-sampling:** The SMOTE technique was used to over-sample to data since no-defaulters were the majority class.
    * **Model Validation:** Since our dataset is fairly small Cross-validation (K-Fold) was used as opposed to hold-out validation in order to get a more accurate valdation of our model.
    * **Feature Selection:** No feature selection, aside from dropping some columns during the data cleaning step, was performed. This step was excluded for time saving purposes. Recursive Feature Elimination could've been used.
    * **Hyperparameter Tuning:** Grid Search Cross Validation was used to fine tune the hyperparameters for each of the top classification models. This method was used as opposed to Bayesian Optimization since it is the easiest to implement. 

3. **Building Final Model**

    The final classification model selected was Random Forest Classifier. 
    * Accuracy: 0.881492
    * Sensitivity: 0.825752
    * Precision: 0.837636

It was retrained on the entire dataset (not just training data) and then saved as `loan_default_predictor.pkl` (pickle file) for later use.

More details can be found on the `2-Model-Building.ipynb` notebook.

## Final Model

Our final model is able to predict the probability that a customer is
going to default (target=1) or not (target=0). We can plot an ROC curve to help us choose a threshold that balances sensitivity and specificity in a way that makes for our business purpose.

### Ways to further improve the model:
* **More Data:** Our dataset was faily small (12000 data points) and more data could help improve the accuracy of our model.
* **Feature Selection:** Applying a technique such as RFE could help us minimize the number of features needed for training and help us improve the overall accuracy.
* **More Hyperparameter tuning:** More parameter combinations could be used as part of Grid Search or perhaps a non brute force apprach such as Bayesian Optimization.  