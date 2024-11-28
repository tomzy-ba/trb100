+++
title = Machine Learning
date = 2024-11-28
draft = false
tags = 'study'
+++
## Decision tree
A decision tree is where you structure a decision making process with many different nodes which ask questions, the answer given will decide which node you go to next. In machine learning, data is used to determine the nodes.

## Data exploration
Pandas is a data analysis library, the most important feature it has is the **DataFrame**, this holds data in a table and this library can do powerful things with said data.
In datasets, there will normally be rows that are named "25%", "75%", or "50%" the latter refers to the median, because it is bigger than 50% of values within the data;  25% and 75% are analogous.

## Selecting data for modeling
You can pick out a variable from a data set, you can use the dot notation, e.g y = melbourne_data.Price, this is called the prediction target.
The columns that are inputted to a model and later used to make predictions are called "Features". Sometimes, you will use all columns except the target as features.

## Building your model
The Scikit-learn library is very helpful for creating models, it models the types of data stored in DataFrames.
You can decide what type of model you want it to be, e.g DecisionTreeRegressor

## Model validation
Almost every model will need to be validated, this is normally checking to see if the predictive accuracy of a model is good enough.
To understand predictive accuracy, you need to summarize it into a single metric, there are many metrics you can use for example **Mean Absolute Error**.
The error of the **MAE** is the (actual - predicted) value, so if a house cost 150,000 and a model predicted it was 100,000 the error would be 50,000. Then using the MAE metric, we get the absolute value of each error, this just means converting it to a positive; and take the average of it.

## Problem with In-sample scores
An in-sample score is a prediction score that is trained on the dataset it is trying to predict, this can be inaccurate because other samples might not have the same correlations as the sample a model was trained on.
The scikit-learn library has a function **train_test_split** to break the data into two pieces, some of that data is used to fit the model, and some to calculate the MAE.

## Experimenting with different models
Now that you have a way to measure model accuracy, you can experiment with different models and see which gives the best predictions. The decision tree has many models, the most important thing being the tree's depth. It's common for a tree to have 10 splits, as the tree gets deeper the data gets sliced up into leaves with fewer houses. These leaves will make predictions that are quite close to those homes' actual values, however they make unreliable predictions for new data, because each prediction is based too specifically on the training data. This is called **overfitting**, where a model matches the training data almost perfectly, but does poorly in validation and other new data. If a tree doesn't divide data into enough leaves, and each group has a wide variety of houses, this will also make predictions inaccurate because it will fail to capture important patterns in the data. This is called **underfitting**, it will perform badly in both training data and other data.
The sci-kit learn *max_leaf_nodes* argument provides a way to control overfitting vs underfitting, the more leaves you allow the model to make, the more specific it becomes.

You can use a for loop to compare the MAE using different max_leaf_nodes:
```Python
for max_leaf_nodes in [5, 50, 500, 5000]:
    my_mae = get_mae(max_leaf_nodes, train_X, val_X, train_y, val_y)
    print("Max leaf nodes: %d  \t\t Mean Absolute Error:  %d" %(max_leaf_nodes, my_mae))
```

## Random Forests
Decision trees leave you with two choices, a deep tree with lots of leaves will overfit, but a shallow tree with few leaves will perform poorly because it fails to capture as many distinctions in the raw data.
Even today's most sophisticated modelling techniques face the problem between underfitting and overfitting.
The random forest uses many trees to make predictions by averaging the predictions of each component tree. It generally has much better predictive accuracy than a single decision tree. 