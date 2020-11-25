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

</details>
  
  
<a name="Evaluation"></a>
### Performance Comparison:
<details open>
<summary>Show/Hide</summary>
<br>
  
</details>

</details>

## Summary and Conclusions
<details open>
  <a name="Summary"></a>
  <summary>Show/Hide</summary>
  <br>
  
  </details>



