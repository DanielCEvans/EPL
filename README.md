<h1 align='center'>English Premier League Result Classifier</h1>

<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/Premier_League_Logo.svg.png" width = 600>
</p>

## Project Statement

The aim of this notebook is to construct a model which can accurately classify the result of an English Premier League Football match based on the statistics of the match. The target feature ‘result’ is multinomial. A result can be either win (w), loss (l), or draw (d) which is based on the number of goals scored by each team in the match. If your team scores more goals, then you win the match, and vice versa. If you score the same amount of goals then the match is a draw.

Note that we are not constructing a model which aims to predict the result of a match yet to be played, rather, a model which accurately classifies the result of a match which has already been played.

## Table of Contents
<details open>
<summary>Show/Hide</summary>
<br>

1. [ Technologies Used ](#Technologies_Used)    
2. [ Executive Summary ](#Executive_Summary)
   * [ 2.1. Data, Early EDA, and Cleaning ](#Data_Early_EDA_and_Cleaning) 
   * [ 2.2. Data Modelling and Hyperparameter Tuning ](#Modelling)
   * [ 2.3. Performance Comparison ](#Evaluation)
3. [Summary and Conclusions](#Summary)
</details>

## Technologies Used
<details>
<a name="Technologies_Used"></a> 
<summary>Show/Hide</summary>
<br>
  
* <strong>Python</strong>
* <strong>Pandas</strong>
* <strong>Numpy</strong>
* <strong>Matplotlib</strong>
* <strong>Seaborn</strong>
* <strong>Scikit-Learn</strong>
</details>

## Executive Summary
<details open>
  <a name="Executive_Summary"></a>
  <summary>Show/Hide</summary>
  <br>
  
<a name="Data_Early_EDA_and_Cleaning"></a>
### Data, Early EDA, and Cleaning:
<details open>
<summary>Show/Hide</summary>
<br>
The full dataset is a merge of two datasets which can be found here: https://github.com/vaastav/Fantasy-Premier-League and here:https://datahub.io/sports-data/english-premier-league). 
The dataset contains key information on each team for each match that has been played in the 2019/2020 season. The initial shape of the dataset was (576, 37). 
Certain features in the dataset were immediately removed as they provided either no assistance in predictive modelling or too much assistance thereby removing the necessity for modelling. The dataset was already ‘clean’ in that all datatypes were loaded correctly and there were no missing values, typos, additional whitespace, or unusual values in the data.

<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/matchday.png">
</p>
<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/wdl.png">
</p>
<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/goals.png">
</p>
<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/cards.png">
</p>
<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/ground.png">
</p>
<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/table.png" width = 600>
</p>

The following pieces of information were found from the exploratory data analysis:

* The most commonly occuring matchday is Saturday
* Liverpool have the highest number of wins while Norwich have the highest number of losses
* Interestingly, the team coming second has the highest number of goals scored while Norwich, the team in last position, has the highest number of goals conceded
* The number of yellow and red cards does not seem to affect the teams position in the league table
* A team is more likely to score more goals if they are playing at their home ground as opposed to the oppositions ground
* At the time of writing, Liverpool are at the top of the table while Norwich are at the bottom

</details>
  

  
<a name="Modelling"></a>
### Data Modelling and Hyperparameter Tuning:
<details open>
<summary>Show/Hide</summary>
<br>
The following different types of classifiers were analysed when trying to predict the outcome of a result:

* K-Nearest Neighbour (KNN)
* Decision Tree (DT)
* Naïve Bayes (NB)

Feature selection was then carried out using F-score, Mutual Information, and Random Forest importance. 

<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/fscore.png" width = 600>
</p>
<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/mutual.png" width = 600>
</p>
<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/rf.png" width = 600>
</p>

The performance of these feature selection techniques was then compared using paired t-tests by fitting a k-nearest neighbour model with the same parameters. 

Full Set of Features: 0.381
F-Score: 0.507
Mutual Information: 0.495
RFI: 0.495

By selecting the 5 best possible features using the various methods, the accuracy results of the model significantly increased. The features indicating the expected number of goals scored, the expected difference between goals scored and conceded, and the expected number of points earned seem to be the most important features in the data in terms of classifying the result. The t-tests all returned a p-value less than 0.05 indicating there was a significant difference between selecting all the features, and selecting the 5 best features using the various methods.

<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/knn.png" width = 600>
</p>
<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/dt.png" width = 600>
</p>
<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/nb.png" width = 500>
</p>

* The hyper parameter tuning of the k-nearest neighbour model using the gridsearcv method determined the best fitting model to have 5 nearest neighbours using Euclidean distance. 
* The hyper parameter tuning of the decision tree model using the gridsearcv method determined the best fitting model to have a maximum depth of 2, minimum samples split of 2, and using entropy criterion.
* The hyper parameter tuning of the naïve bayes model using the gridsearcv method determined the best fitting model to have a variance smoothing value of approximately 0.53.
</details>
  
  
<a name="Evaluation"></a>
### Performance Comparison:
<details open>
<summary>Show/Hide</summary>
<br>
<p align="center">
  <img src="https://github.com/DanielCEvans/English-Premier-League-result-classifier/blob/master/Images/confusion.png" width = 500>
</p>
The paired t-tests among all three models showed that there was no significant difference found between the decision tree and the naive bayes model (p > 0.05). There was a significant difference found between the k-nearest neighbour model and both the decision tree and naive bayes models (p < 0.05).<br>
The Decision Tree model returned the best mean result in terms of accuracy with a percentage of approximately 54.5%.
</details>

</details>

## Summary and Conclusions
<details open>
  <a name="Summary"></a>
  <summary>Show/Hide</summary>
  <br>
  This project set out to construct a model which could accurately classify the result of a football match based on the statistics from the match. From this notebook in can be concluded that it is very difficult to predict the outcome in sports. This certainly makes sense or else, why would we be watching it? If the outcome was almost certainly known before a match and hence, easily predicted, we certainly wouldn’t be devoting a lot of our lives to watching and participating in sports. It is the element of surprise and the excitement that keeps us coming back to watch.
  </details>



