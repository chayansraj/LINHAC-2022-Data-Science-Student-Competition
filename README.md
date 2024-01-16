# Linköping Hockey Analytics Conference - LINHAC 2022
<p align="center"> 
  <img width="460" height="300" src="https://c.tenor.com/yTPSA6UadckAAAAd/ice-hockey-hockey.gif"> <h6 align = "center" > Source: google </h6>
  
</p>

Competition Link - https://www.ida.liu.se/research/sportsanalytics/LINHAC/LINHAC22/studentcompetition.html





# Task

Given the event data, generate findings/patterns related to sequences of events leading up to a particular outcome. You can choose the kind of outcome. For instance, find characteristics of sequences of events leading to, e.g., a goal or a successful zone entry or a shot.<br/> 
<br/>
<br/>


## My idea: 


# Temporal activity outcome prediction of players in Ice Hockey 
<p align="center">
  <img width="350" height="250" src="https://user-images.githubusercontent.com/22219089/198964949-efbb30cc-0713-4d64-8722-608eb786e3c0.png">
  <h6 align = "center" > Source: google </h6>
</p>


Temporal activity prediction is a challenging task in sports especially in sports like ice hockey because of its fast dynamics and interactions among the players. In this paper, I am trying to predict whether the next action of the players will be successful or not given the various parameters describing its location and other factors. Basically, it is the process of predicting if the player’s next action/move would be a success or not.
<br/>

# Data
The data was provided by Sportlogiq with permission of SHL, the Swedish Hockey League, representing event data from the 2020-2021 SHL season. It consists of 76041 rows and 22 features describing each game with a unique game id and time stamps. It consists of match time stamps between two teams, where every time stamp describes the event played by any one of the players in one of teams from a certain point on the field and whether it was successful or not. Keeping in mind the structure of the data, I have used a different idea of separating training, validation and test sets as different matches uniquely defined by their ‘gameid’. It means, if one match is used as a validation data and the other is used as testing data, then all the other matches are used as training data. This allows our model to analyze whole data space and extract complex patterns in each match. A summary dictionary is as below: 
<p align="center">
  <img width="200" height="300" src="https://user-images.githubusercontent.com/22219089/168465951-878b1f05-0580-459c-9291-72fab1bf503a.png">
  <h6 align = "center" > source: Author </h6>
</p>

# Methodology

## Exploratory data analysis

Firstly, an exhaustive exploratory data analysis was performed using one of the ‘gameid’ e.g. 66445. It consists of match time stamps between two teams encoded as 742 and 916, where every time stamp describes the event played by any one of the players in one of teams from a certain point on the field and whether it was success-ful or not.

## Algorithms
I first trained an ensemble of four Residual neural networks that will loop over all the ‘gameid’ with a stride of 2. So, first ensemble works on ‘gameid’ 0 and 1, then next on 2 and 3 and so on for test and validation sets respectively. We then average the accuracy of the 4 NN ensemble models and choose the games that produced highest accuracy. This is done because neural networks are powerful algorithms and can learn complex patterns with enough data, so we are feeding our data first to this ensemble to understand the best explainable data blocks for our next ensemble step. 

<p align="center">
  <img width="400" height="200" src="https://user-images.githubusercontent.com/22219089/168466168-50fe617d-0558-42ca-9304-800a6bc4aa74.png">
  <h6 align = "center" > source: google </h6>
</p>

Ensemble learning often proves to be performing superior to any one machine learn-ing algorithm and hence final model/algorithms chosen for this paper is again an ensemble of 4 very powerful classification algorithms, namely, K-Nearest Neighbors, Logistic Regression, Random Forests, Support Vector Machines. The structure of the setup looks like this: 

<p align="center">
  <img width="700" height="500" src="https://user-images.githubusercontent.com/22219089/168466635-a6155fe0-b0e4-45ba-97c5-2ba7d27970d7.png">
  <h6 align = "center" > source: Author </h6>
</p>

<br/>

## Tools 

1. Tensorflow (An end-to-end open source machine learning platform - https://www.tensorflow.org/) 
2. Keras (Python deep learning API - https://keras.io/)
3. Optuna (Hyperparameter optimization framework to automate hyperparameter search - https://optuna.org/)
4. SHAP (Interpretable Machine Learning Framework - https://github.com/slundberg/shap)
5. sklearnex (Intel® Extension for Scikit-learn - https://intel.github.io/scikit-learn-intelex/)
6. Graphviz (Open source graph visualization software - https://graphviz.org/ )

<br/>

## Result

The evaluation of the models is done with the evaluation metrics accuracy, precision, recall and F1-score. In our case, we have binary classification where accuracy shows the total correct classification out of total values, precision and recall capture the limitations of accuracy and considers the curse of imbalanced class labels. Finally, F1-score encapsulates and keeps the the limitations of accuracy at bay and provides the best metric for our classifier which ranges from 0 to 1, higher the value, better the predictions.

<p align="center">
  <img width="300" height="150" src="https://user-images.githubusercontent.com/22219089/168467136-faccb5c8-007e-434b-bca1-6c782940c15d.png">
  <h6 align = "center" > source: Author </h6>
</p>

with final F1- Score of 0.85

<br/>

Post optimizing the hyperparameter space, we evaluated our model on test data and achieved a weighted average F1 score of 0.85 which is ~3% higher than simply using residual neural networks. Attempting to interpret the feature influence on model output using SHAP gives an insight into important features in further analysis.

Importance of each feature: To get an overview of which features are most important for a model we can plot the SHAP values of every feature for every sample. 

<p align="center">
  <img width="600" height="400" src="https://user-images.githubusercontent.com/22219089/168466954-596abc34-bb64-4e59-b4ad-67ca561246d1.png">
  <h6 align = "center" > source: Author </h6>
</p>

<br/>

Contribution of each feature: The above explanation shows features each contributing to push the model output from the base value (the average model output over the training dataset we passed) to the model output. Features pushing the prediction higher are shown in red, those pushing the prediction lower are in blue. 

<p align="center">
  <img width="600" height="400" src="https://user-images.githubusercontent.com/22219089/168467071-5973fa3b-8bc2-4234-825b-fdf1523a0252.png">
  <h6 align = "center" > source: Author </h6>
</p>


# Thanks! 

## Ps: Reached finals - https://www.ida.liu.se/research/sportsanalytics/LINHAC/LINHAC22/program.html  :heart_eyes:

<p align="center">
  <img src="https://user-images.githubusercontent.com/22219089/187165073-1e3d1227-1583-43ee-ae4c-0d6fac9d7d7e.png">
  <h6 align = "center" > Source: Author </h6>
</p>

## Pps: Published paper - https://www.ida.liu.se/research/sportsanalytics/LINHAC/LINHAC22/LINHAC2022-proceedings-preprint.pdf
