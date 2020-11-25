
![Premier_League_Logo svg](https://user-images.githubusercontent.com/65587875/100211678-88989900-2f60-11eb-9bbb-dece9b7bb672.png)

## Project Statement

The aim of this notebook is to construct a model which can accurately classify the result of an English Premier League Football match based on the statistics of the match. The target feature ‘result’ is multinomial. A result can be either win (w), loss (l), or draw (d) which is based on the number of goals scored by each team in the match. If your team scores more goals, then you win the match, and vice versa. If you score the same amount of goals then the match is a draw.

Note that we are not constructing a model which aims to predict the result of a match yet to be played, rather, a model which accurately classifies the result of a match which has already been played.

## Table of Contents
1. Technologies Used
2. Executive Summary
   2.1. Data, Early EDA, and Cleaning
   2.2. Data Modelling and Hyperparameter Tuning
   2.3. Performance Comparison
3. Summary and Conclusion
{:toc}

## Technologies Used
  
- Python
- Pandas
- Numpy
- Matplotlib
- Seaborn
- Scikit-Learn


## Executive Summary
  
### Data, Exploratory Data Analysis, and Cleaning

The full dataset is a merge of two datasets which can be found [here](https://github.com/vaastav/Fantasy-Premier-League) and [here](https://datahub.io/sports-data/english-premier-league). 
The dataset contains key information on each team for each match that has been played in the 2019/2020 season. The initial shape of the dataset was (576, 37). 
Certain features in the dataset were immediately removed as they provided either no assistance in predictive modelling or too much assistance thereby removing the necessity for modelling. The dataset was already ‘clean’ in that all datatypes were loaded correctly and there were no missing values, typos, additional whitespace, or unusual values in the data.

<img width="988" alt="matchday" src="https://user-images.githubusercontent.com/65587875/100291411-d0a3d400-2fd1-11eb-96e6-2652999d03cf.png">

<img width="995" alt="wdl" src="https://user-images.githubusercontent.com/65587875/100291654-7f481480-2fd2-11eb-846e-2cb7e42296df.png">

<img width="996" alt="goals" src="https://user-images.githubusercontent.com/65587875/100291682-8bcc6d00-2fd2-11eb-88ab-a67c4a7750eb.png">

<img width="988" alt="cards" src="https://user-images.githubusercontent.com/65587875/100291734-ae5e8600-2fd2-11eb-91e9-ee70e9ae20eb.png">

<img width="993" alt="ground" src="https://user-images.githubusercontent.com/65587875/100291752-bf0efc00-2fd2-11eb-86d7-a8ff1c2785ae.png">

<img width="674" alt="table" src="https://user-images.githubusercontent.com/65587875/100291782-cdf5ae80-2fd2-11eb-98be-b5c39bb55f06.png">

The following pieces of information were found from the exploratory data analysis:

* The most commonly occuring matchday is Saturday
* Liverpool have the highest number of wins while Norwich have the highest number of losses
* Interestingly, the team coming second has the highest number of goals scored while Norwich, the team in last position, has the highest number of goals conceded
* The number of yellow and red cards does not seem to affect the teams position in the league table
* A team is more likely to score more goals if they are playing at their home ground as opposed to the oppositions ground
* At the time of writing, Liverpool are at the top of the table while Norwich are at the bottom

### Data Modelling and Hyperparameter Tuning

The following different types of classifiers were analysed when trying to predict the outcome of a result:

- K-Nearest Neighbour (KNN)
- Decision Tree (DT)
- Naïve Bayes (NB)

Feature selection was then carried out using F-score, Mutual Information, and Random Forest importance. 

<img width="562" alt="fscore" src="https://user-images.githubusercontent.com/65587875/100291828-eb2a7d00-2fd2-11eb-8016-6ec86a4fb56d.png">

<img width="562" alt="mutual" src="https://user-images.githubusercontent.com/65587875/100291837-f087c780-2fd2-11eb-9b20-513209c269c7.png">

<img width="565" alt="rf" src="https://user-images.githubusercontent.com/65587875/100291841-f382b800-2fd2-11eb-92b9-55c762acfe0a.png">


The performance of these feature selection techniques was then compared using paired t-tests by fitting a k-nearest neighbour model with the same parameters. 

- Full Set of Features: 0.381
- F-Score: 0.507
- Mutual Information: 0.495
- RFI: 0.495

By selecting the 5 best possible features using the various methods, the accuracy results of the model significantly increased. The features indicating the expected number of goals scored, the expected difference between goals scored and conceded, and the expected number of points earned seem to be the most important features in the data in terms of classifying the result. The t-tests all returned a p-value less than 0.05 indicating there was a significant difference between selecting all the features, and selecting the 5 best features using the various methods.

<img width="540" alt="knn" src="https://user-images.githubusercontent.com/65587875/100291866-06958800-2fd3-11eb-9d5e-936af631a0ab.png">

<img width="525" alt="dt" src="https://user-images.githubusercontent.com/65587875/100291865-05fcf180-2fd3-11eb-9168-adeabcab6dee.png">

<img width="472" alt="nb" src="https://user-images.githubusercontent.com/65587875/100291863-04cbc480-2fd3-11eb-8ac3-20ca5d88bcdc.png">


- The hyper parameter tuning of the k-nearest neighbour model using the gridsearcv method determined the best fitting model to have 5 nearest neighbours using Euclidean distance. 
- The hyper parameter tuning of the decision tree model using the gridsearcv method determined the best fitting model to have a maximum depth of 2, minimum samples split of 2, and using entropy criterion.
- The hyper parameter tuning of the naïve bayes model using the gridsearcv method determined the best fitting model to have a variance smoothing value of approximately 0.53.
  
### Performance Comparison

<img width="347" alt="confusion" src="https://user-images.githubusercontent.com/65587875/100291858-01d0d400-2fd3-11eb-98dd-ed0f8ff3ea00.png">

The paired t-tests among all three models showed that there was no significant difference found between the decision tree and the naive bayes model (p > 0.05). There was a significant difference found between the k-nearest neighbour model and both the decision tree and naive bayes models (p < 0.05).<br>
The Decision Tree model returned the best mean result in terms of accuracy with a percentage of approximately 54.5%.

## Summary and Conclusions
This project set out to construct a model which could accurately classify the result of a football match based on the statistics from the match. From this notebook in can be concluded that it is very difficult to predict the outcome in sports. This certainly makes sense or else, why would we be watching it? If the outcome was almost certainly known before a match and hence, easily predicted, we certainly wouldn’t be devoting a lot of our lives to watching and participating in sports. It is the element of surprise and the excitement that keeps us coming back to watch.

