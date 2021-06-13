# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 2: Ames Housing Price Analysis

This is the second project done as part of the General Assembly's Data Science Immersive in June 2021.

This project is divided into two notebooks. In [part I](./code/ames-housing-analysis.ipynb) we define the problem statement, explore the data, perform EDA, clean the data, perform some feature engineering, and save it; then use it to predict the sale price of properties using **_Linear Regression_** models in [part II](./code/ames-housing-modeling.ipynb).

## Overview

Many factors affect the price of a property, whether it is an apartment or a  house, how many rooms does it have and how big they are. Property prices can fluctuate based on many extrinsic reasons like economic conditions, local policy changes, tax regulations, public infrastructure developments in the neighborhood, industrialisation, etc. However, the intrinsic properties of a real estate entity are what we have to work with and usually in our control. Quantifying and noting down some of them can help you keep a record of the price variations over a period of time.

One such use might be, case-in-point, when you work at a real estate agency in the city of Ames, Iowa. Traditionally, the house prices in small cities would be the highest bidder who knew about the sale. But with rise in technology and interest in automating such processes that can fetch higher and fairer prices for property sales, real estate agents in larger cities have been employing these modern methods and getting good returns.

## Problem Statement

**As a data analyst we are tasked with the challenge to use this quantified housing data, and make analytical predictions for the property sale prices in the city, using simple machine learning methods. At our agency, we use this data to predict house prices for any seller that intends to make a sale for their property based on the house's features.**

## Executive Summary

We start by dividing the data features into numerical & categorical types and explore them separately, look for missing data and make decision to either not consider the feature, if many values are missing, or impute them with sensible replacements. While we do this we need to make sure we don't _leak_ data from train to test dataset. After going through most of the features we are interested in to consider, we make decision based on evidence to select it for model training or not. Following that, we clean and save the data, which is then imported in part II of this project for modeling. There, we begin with establishing a _baseline_ score, followed by a simple linear regression model and then we build towards the actual modeling process. Some of these regression models would requrie us to _scale_ the data, and then the model performances are compared with each other based on metrics of choice as described below. Some interaction terms and polynomial scaling of features is also done. A best model is made as production-ready by retraining it on the _entire_ training data and the results uploaded to kaggle for getting the final __test__ score. The observations and conclusions are listed out at the end while explaining the learnings of this project.

### Data

In this project, we work on the Ames Housing data from [kaggle](https://www.kaggle.com/c/dsi-us-6-project-2-regression-challenge/overview). The data dictionary can be found [here](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).

The data is obtained from the kaggle competition webpage linked above. It contains the following three files:
- `train.csv`: contains all the features including the target, _SalePrice_. This is explored, cleaned and after feature selection used to train the models.
- `test.csv`: contains all the features except the target, _SalePrice_. Since the _true_ value of the target is unavailable, we solely use this data at the end for model evaluation and submissions to kaggle.
- `sample_sub_reg.csv`: a sample file for the kaggle submission format. Contains only the _Id_ & predicted _SalePrice_.

The data provided contains many features any potential buyer/seller might be interested in to judge it's price. Some of those things might be $-$ number of bedroom, bathrooms, square footage of the lot, how old the construction is, locality, quality of the house, and other amenities like, garage size, pool and fireplaces $-$ are among the features included in the dataset provided. Not all features contribute to the real value of the property and, thus, as someone who works at a real estate agency in this city, it is our job to clean the data, lookout for any possible disparities, interdependencies among various features, and build a model that best predicts the sale price of a property given this data.

### Types of models

The following types linear regression models were explored and evaluated for this project:
- Simple Linear Regression: Using a single feature in the model
- Multiple Linear Regression: Using multiple explanatory features to train the model
- Lasso Regression: Using penalty term $\alpha$ on the L1 norm to perform regularization
- Ridge Regression: Using penalty term $\alpha$ on the L2 norm to perform regularization
- ElasticNet Regression: Using penalty term $\alpha$ and `l1_ratio` to perform regularization using Lasso & Ridge regressions.

### Evaluation

The commonly used evaluation metrics for linear regression models are $R^2$, $\text{adj-}R^2$ and $MSE$ or $RMSE$. The former two are a measure of how closely the predicted target values "fit" the true target values, higher the better, while the latter is _root mean squared error_, which mathemcatically is an $L2$ norm and in english is a squared sum of the differences between the predicted and true target values, lower the better.

The models are cross-validated on the __train__ set to verify the consistency of errors/scores on the data the model hasn't seen.

### Feature sets

We use the train and test dataset in this notebook, which were cleaned in the part I of this project. The original data had 80 features and a target feature to be predicted. After performing EDA and feature engineering, we condensed the data to 26 features, which are then subdivided into subsets of different combinations to be tested in the models. The feature set with the specific model giving best results would be selected and presented.

The following table shows the different feature sets evaluated:

|    |Feature sets|
|:--:|:----------:|
|**Set I**|LotFrontage, LotArea, OverallQual, MasVnrArea, ExterQual, BsmtQual, TotalBsmtSF, HeatingQC, GrLivArea, KitchenQual, OpenPorchSF, PropertyAge, TotalBedsNBaths, HasFireplace, HasWoodDeck, HasMasonryVeneer, FoundationPConc, FoundationCBlock, FoundationBrkTil, FoundationOthers|
|**Set II**| LotFrontage, LotArea, OverallQual, MasVnrArea, ExterQual, BsmtQual, TotalBsmtSF, HeatingQC, GrLivArea, KitchenQual, OpenPorchSF, PropertyAge, TotalBedsNBaths, GarageCarsNArea, HasFireplace, HasWoodDeck, GarageAttached, FoundationPConc, FoundationCBlock, FoundationBrkTil, NH_NAmes, NH_CollgCr, NH_OldTown, NH_Others, HouseStyle_1Story, HouseStyle_2Story |

After running the inital trial on Multiple Linear Regression with __Set I__, we noticed that the difference between __train__ and __valid__ $RMSE$ is more than ususal, thus, we need to revisit the feature selection in part I. The typical performance is that if the __train__ error is usually slightly lower than the __valid__ because the former was used to train the model. If it is too low, then we have _overfit_ issue where the model predicts the data it observed very well but fails to match with any new data that it sees, while if the train error is higher than the test data, the model is not quite accurate or the split between train/valid has some issues. We can confirmed this by _cross validating_.

The feature set, __Set II__, is eventually used to train all the models, with scaling for regularization models. The linearity of features with the target variable is also touched upon.

### Modeling

A _baseline_ score is calculated from the train data, which is simply the mean _SalePrice_ value from the train set used a predictor for target on test data. Then we build a Simple Linear Regression model using a single feature to see if we can do any better than the baseline, and reason about using multiple features in the linear regression models.

This is followed by a series of Multiple Linear Regressions, including the regularization models, __Ridge, Lasso and ElasticNet__. These models require the data to be scaled and typically eliminates the coefficients of features, by penalizing them, that are not contributing to the model prediction. We also fit some of the models with polynomial and interaction features generated by _sklearn's_ `PolynomialFeatures` method.

The coefficients from these models are interpreted and plotted to infer their impact on the target. After comparing the scores and errors for these models, the _best model_ is selected for deploying in production, when it is trained with the complete __train__ dataset.

## Conclusions and Recommendations

In this project, we went through a whole lot of exploring & modeling, and understanding how selecting features, their interactions and knowing relationship between them and target variable can affect the results. In the end, we made a production ready model from polynomial features using Lasso regularization regression getting an $RMSE$ of $\$24362.76$ on the entire training data and $\$28435.67$ on the test data from kaggle.

The project deals with housing data from the city of Ames, Iowa. It consists of quantified details about property sales from 2006 to 2010, and we are tasked to use the features to predict sale price of the properties using various Linear Regression methods. We began the project by getting the orginal dataset from kaggle. It consisted of $80$ features, many of which had numerous null values and couldn't be used for regression models.

We performed EDA on all types of data $-$ numerical, ordinal and categorical. Many of the categorical columns that had no variety in data were not used in the model as they would contribute very little to the model building. Some features had interdependent relationships and they were dealth with by either combing them into single column or converting them to binary columns. We selected features based on evidence and dropped those that were thought not be siginificant for model training. We even revisited feature selection after seeing inital model results. Finally, $26$ distinct features were selected for building the models.

A baseline score was established, and then different linear regression models were built and compared on metrics like, $R^2$ and $MAE$, but mainly $RMSE$. The performance of selected models is shown in the table below:

| Predictor  | Train RMSE | Valid RMSE | Train / Valid ($R^2$) | Cross val RMSE |
|:----------:|:----------:|:----------:|:---------------------:|:--------------:|
| Baseline   |  77014.97  |  82507.10  |            -          |        -       |
|    SLR     |  72827.35  |  75595.17  |   0.10579 / 0.15811   |    73073.10    |
|    MLR     |  31475.19  |  31181.94  |   0.83287 / 0.85699   |    33546.18    |
|   Ridge    |  31605.43  |  31627.59  |   0.83159 / 0.85263   |    33321.36    |
|   Lasso    |  31792.82  |  31917.15  |   0.82958 / 0.84992   |    33385.82    |
|Lasso (poly)|  24470.15  |  28587.87  |   0.89905 / 0.8796    |    31003.54    |
| ElasticNet |  31751.30  |  31854.10  |   0.83003 / 0.85051   |    33379.99    |

The __production model__ that had the best performance was Lasso regularized regression with polynomial features. The polynomial features creates many interaction terms, 351 to be precise, and it is not always easy to interpret how each term affects the target, _SalePrice_ in this case. Therefore, we use Lasso and saw that about 306 coefficients were zeroed, hence the remaining features can be looked in detail in feature along with other features that were not part of modeling in this project.

The top five features, taken from MLR, that have the most impact on _SalePrice_ of the house are:

|   Feature 	| BsmtQual 	| ExterQual | KitchenQual |	HasFireplace | OverallQual |
|---------------|-----------|-----------|-------------|--------------|-------------|
|**Coefficient**| 16061.081 | 14064.274 |  13085.968  |	11930.744 	 | 11844.361   |

These values mean each unit increment in the feature value raises the house price by its respective coefficient value. Four of the top five coefficients are quality measures, so we would recommend any property seller to improve those ratings to get a better value for their real estate. Based on our analsis, some features that might not be as significant in determining the price are: _open porch, wood deck, garage type, foundation, neighborhood and house style_.

With more detailed feature engineering, which can be time-consuming yet fruitful, and exploring the underlying relationship among features and between target variable, a more accurate low error regression model can be developed in the future. For the purpose of this project, our production model would suffice based on our predictions.

### Contents

The contents of this project are as follows:
Part I
- 1 Load the Data
- 2 Data Munging & EDA
- 3 CSS $-$ Cleaning, Spliting & Saving

Part II
- 1 Data Import & Baseline Score
- 2 Model Preparation
- 3 Model Fitting & Evaluation
- 4 Production Model
- 5 Conclusions & Recommendations