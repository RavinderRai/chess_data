![chess image](https://images.ctfassets.net/3s5io6mnxfqz/wfAz3zUBbrcf1eSMLZi8u/c03ac28c778813bd72373644ee8b8b02/AdobeStock_364059453.jpeg)

# Analyzing Chess Games to Improve Player Strategies

The game of chess has been arouund since the 6th century CE, and would eventually become one of the most commonly played board games. Now chess may be known more for being a solved game - in a sense - since aritificial intelligence has the capability to beat the best players, but this has not stopped people from playing it competitively. Although out highly advanced computer programs may be good at chess, there is still room for A.I. to come in and help players get better themselves. This is where projects like these come in, where datasets of tens of thousands of chess games are compiled and analyzed, to find better strategies for players, and improve their chances of victory.

## Data Wrangling

[Data Wrangling Notebook](https://github.com/RavinderRai/Chess_Data/blob/main/Data_Wrangling_on_the_Kaggle_Chess_Dataset.ipynb)

This project is analyzing the chess data set from kaggle: https://www.kaggle.com/datasets/datasnaek/chess?select=games.csv. The ultimate aim of the project is to find strategies to improve the chances of victory for a player, given they are playing as white or black. Luckily, this dataset had no null values. It did have a few features with a large amount of outliers, though in chess having some rare games that run longer than normal, or have many more turns than normal, are not that uncommon. Thus, it made sense to keep these so no outliers were removed. 

The only faulty data here was that there were two features, one with values of the start times of the chess game, and one with end times. The column with end times data had a lot of values that were the same as the start time values, making games effectively last 0 seconds. This of course made no sense. A new features that took the difference of these two features to get the total time of a game was made in place of these features, and the decision to keep or remove it would be left after some EDA was done.

## EDA

[Exploratory Data Analysis Notebook](https://github.com/RavinderRai/Chess_Data/blob/main/EDA_on_the_Kaggle_Chess_Dataset.ipynb)

Some of the first things done here was exploring some of the issues noticed in the Data Wrangling step, but this time with visual aids. A feature that had a lot of outliers can be seen below. This is the increment feature, which is a value that represents the amouunt of extra time each player is alloted every turn.

![boxplot example](figures/increment_boxplot.jpg)

You can see here all the outliers. If it was just a few outliers, it may have been reasonable to simply remove those games, but with so many outliers it was deemed worth keeping the data. The same is ture for a few other features as well. 

Another thing worth noting here, was that the total time feature created before was dropped in the end. Also, perhaps the most important features in this dataset were of long form text values, so they were handled in the pre-processing step.

## Pre-Processing

[Pre-Processing Notebook](https://github.com/RavinderRai/Chess_Data/blob/main/Pre-Processing_and_Training_Data_Development.ipynb)

In this step there were three text columns to handle. A count vectorizer function in Python was used to do this. The features were ones that described the moves of a game, as well as the opening moves. Aside from that, dummy variables were created for some categorical features, and all numeric features were standardized. Finally, the target variable, which was a category with values as white, black, or draw, describing the winner, was labeled.

## Modeling

[Modeling Notebook](https://github.com/RavinderRai/Chess_Data/blob/main/Modelling.ipynb)

In the modeling step many different models were tried, but mostly focusing on logistic regression, random forest, and XGBoost. With the help of grid search, the best model parameters for each model was obtained and compared in the end. That being said, the scoring metric was a bit non-traditional, in that the Cohen Kappa score was used here. Since this dataset is imbalanced (significanly less games ended in draws then white or black winning) with multiple labels, this scoring metric was a much better option than something like accuracy. The Cohen Kappa score measures how similar in agreement two raters are, where you can think of raters as people who are rating certain things, like movies. This can then be naturally used for classification problems, where one rater is the actual values of the target variable, and the other is the predicted values of the model. Thus, we can now report the Cohen Kappa scores for each of the best models.

## Applying the Model

[Model Utilization Notebook](https://github.com/RavinderRai/Chess_Data/blob/main/Final_Model_Review.ipynb)
