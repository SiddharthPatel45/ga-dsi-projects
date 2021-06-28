# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Reddit API & Subreddit Classification

This is the third project done as part of the General Assembly's Data Science Immersive in June 2021.

## Overview

Using the text classification capabilities of some machine learning models, we try to analyse data collected from a public website on two _similar but different_ topics, and train an algorithm which will classify the text as belonging to one or the other topic. This category of machine learning is known as NLP, or natural language processing, where a piece of code learns to understand the language we humans speak. This project is a very shallow dip into this field, in the sense that we use some very basic tools to achieve something impressive. The goal here is to classify a post from reddit correctly by predicting which subreddit it belongs to.


### Problem Statement

**To resolve a bet among a group of friends, who is more _creative_ $-$ [Filmmakers](https://www.reddit.com/r/Filmmakers/) or [Screenwriting](https://www.reddit.com/r/Screenwriting/)? To answer this question, we get some posts from the two subreddits from [reddit.com](https://www.reddit.com/), and see if we can differentiate between the two roles simply by analysing the text in the posts from the members of those subreddits.**

---

## Executive Summary

Creativity is a subjective phenomenon, which can mean different things to different people. For the purpose of this project, however, we make certain assumptions to answer our main problem statement, like, we will check posts from which role talks more about new ideas, or characters, or techniques, and so on. We begin by scraping the reddit website using its API for our data collection process, which is collecting as much text from the two subreddits, **Filmmakers & Screenwriting**, as possible. The reddit API limits the maximum number of posts one can scrape at a time, and given that we need unique posts, we aim to collect about 700~1000 unique posts for both subreddits.

Then we use simple techniques to extract useful text information from the posts, which is the _Title, Subreddit, and Selftext_ and save all this info into a CSV through a `pandas` DataFrame. Next, we perform some primitive cleaning steps to remove any symbols, urls, numbers that are not english character, because these don't provide us any useful information. The data we are looking for are words and phrases which can be used to describe the topics we are exploring.

After getting all this setup, we move to model building, where we train the _classification_ models from the `sklearn` library and then pass the posts to models to predict which subreddit it belongs to. Since any machine learning model can only take numbers as inputs, we use **bag-of-words** model to vectorize the text into a frequency table of each individual _token_ (or words) for the entire dataset. This is one of the simplest and widely used method, in which the number of times a word appears in the text is stored in a table.

There are many parameters which can be changed for the vectorizer and the model, that are tuned using the `Pipeline` and `GridSearchCV` methods to "search" for the best set of parameters to give good results. The results here are scored in terms of _accuracy_, which is the default score for all classification models in the `sklearn` library. An accuracy score is the ratio of the number of predictions the model got correct, over the total number of predictions it made. It is an easy-to-understand metric and for this project is a good measure of model performance to show at quick glance how many observations did we classify correctly, but might not give the complete understanding of the way the model behaves, especially when it comes to analysing the _misclassified_ data. The conclusions of how our model classifies the two roles of _Filmmakers & Screenwriting_ along with some recommendations are made at the end.

## Conclusion and Recommendations

So, do we know who is more creative $-$ _Filmmakers or Screenwriting_? The short answer is _no_, but we do at least know what creative topics each group talks about and discussed with the community.

In this project, we used Reddit's API to scrape some posts from two subreddits, extracted relevant text info, cleaned and saved the data to analyse. We set out to see if we can figure out who is more creative between the two roles. We did some basic preprocessing of data and employed the _bag-of-words_ model to vectorize our text data into numbers that can be used to train the classification models.

Logistic Regression turned out to be the best estimator for this particular dataset we have in this project, along with the term frequency-inverse document frequency vectorizer. Our model had an accuracy of about 87% for train and 86% for test data. We can be satisfied with this result because we know we minimized the overfit and the gap between the train data (the data model was trained on) and test data (unseen data by model) is the smallest here. Also, among the two readily available stop words used in this project, the grid searching selected the `sklearn`'s in-built 'English' stop word list.

In total, there were about 60 misclassifications out of the 430 test data observations. The top features with highest preditive power for each class were identified and discussed. Each subreddit has its own set of disparate creative words that are unique to them but cannot be compared together. So, we conclude that we identified some keywords for both topics but are not sure who could be more creative.

Lastly, Logistic Regression does come with its caveats, like the assumption that the features have no/low multi-collinearity, the features have a linear relationship with the target variable, and generally it requires more data to capture the problem and even then it may not be able to build complex relationships. In the best model, according to grid search results, we use all the available tokens created by the vectorizer, and this is not a good choice because it may lead to overfitting with wider dataset. For these reasons, the other model used in this project, Multinomial Naive-Bayes, can give good results as well with a well-trimmed data. This can be looked into to improve the existing prediction capability.

We can make the following recommendations based on this conclusions:
1. We saw some plurals and words in different forms, which can be minimized by lemmatizing the text
2. Usually Decision Trees by themselves, if not parametrized properly, tend to overfit but used with boosting could be good classifiers, and can be used in this project.
3. Obtaining more data is always a good idea, but making "good" data by using more advanced text cleaning techniques can also be looked into.

---

### Contents

The contents of this notebook are as follows:

- 1 Data import
- 2 Preprocessing text
- 3 Building models
- 4 Pipelines & parameter tuning
- 5 Evaluation
- 6 Conclusion and Recommendations