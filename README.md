# Anyfin Data Science Case Solution

## Overview
The goal was to build a predictive model that assigns default probabilities to loan applications. 

**Optimization:** It was assumed that the business cares a lot more about accurately predicting defaulters rather than non-defaulters. Therefore, the predictive model was optimized for sensitivity (recall).

## Approach
In order to tackle this problem, the dataset provided was used to train a classification model. I began by doing some exploratory data analysis in order to better understand it's features and clean the data in preparation for the model building step. During the model building step, the data was transformed to get it ready for training. I trained Several classification models then compared them each other using accuracy, sensitivity and precision scores. Here is how the problem was approached in more detail:

### EDA and Cleaning
Exploratory data analysis and cleaning to prepare for the model building step.

1. **Data Gathering:** I connected to the postgresql database using a python model to query the entire table and save it a pandas dataframe.
2. **Exploratory Data Analysis (EDA):** Visualizing the data to understand the distribution and correlation of different features.
3. **Data Cleaning:** Basic pre-processing techniques which include removing rows with missing values and dropping columns that may not provide any value during prediction.

More details can be found on the `1-Data-Cleaning-And-EDA.ipynb` notebook.

### Model Building
Model Selection and building the final model.

1. **Data Prepation:** The data was prepared for training by standardizing data types, doing one-hot encoding and splitting the features from the target.   

2. **Model Selection**

    First, four different classfication models were compared to each other using accuracy, sensitivity, and precision scores. No hyperparameter tuning was performed on this step since it is computationally costly and we might be able to identify poor performing models and exclude them. Here are the results:

    <img src="Plots/class_comp.png">

    **Observations:** Since our goal is to optimize our model for sensitivity (more accurately predict defaults), it seems like the best algorithm would be the SVC. The problem is that it has a very low precision score, which means that it won't do a good job generalizing to new data and we still want to accurately predict no defaults (acquire new customers). On the other hand, Random Forest Classifier has a high sensitivity and an even higher precision score, and since both scores are inversely related, improving the sensitivity will still leave us with a decent precision score, giving us a good model overall.

    Only considering the top three classifiers, I did some basic hyperparameter tuning and the best combinations were used to retrain the models and compare them to each other again. Here are the results:
    
    <img src="Plots/class_comp_tuned.png">

    **Observations:** As we can see, all three models performed similarly, but we will choose Random Forest Classifier as our final model.

    Here is some more information about the different techniques used during the model selection step:

    * **Over-sampling:** The SMOTE technique was used to over-sample to data since no-defaulters were the majority class.
    * **Model Validation:** Cross-validation (K-Fold) was used as opposed to hold-out validation since our dataset was fairly small and I wanted to get an accurate scoring.
    * **Feature Selection:** No feature selection, aside from dropping some columns during the data cleaning step, was performed. 
    * **Hyperparameter Tuning:** Grid Search Cross Validation was used to fine tune the hyperparameters for each of the classification models that were being trained. This method was used since it was the easiest to implement. 

3. Building Final Model
The final classification model selected was Random Forest Classifier. It was retrained on the entire dataset (not just training data) and then saved as a pickle file for later use.

More details can be found on the `2-Model-Building.ipynb` notebook.

## Final Model


### Potential ways to further improve the model:
* More Data
* Better Feature Selection
* More Hyperparameter tuning