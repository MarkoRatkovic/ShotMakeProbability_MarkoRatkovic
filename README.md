# ShotMakeProbability_MarkoRatkovic
This project trains and fits a model on 425,719 non-fouled field goal shots in the NBA across two seasons and then tests it on 213,977 shots to return shot make probabilities with the goal of minimizing log loss by eliminating imprecision in the probability prediction. Three files are used in the generation of this model and the output of its predictions for shot make probability of the 213,977 shots it is tested on: 

  - training.csv: Holds data for 425,719 non-fouled field goal shots with 28 features including the target variable of the shot's binary outcome
  - testing.csv: Holds data for 213,977 non-fouled field goal shots with 27 features identical to those in training set but no target variable
  - submission.txt: Text file with shot IDs corresponding to those in testing set that is populated with each shot's predicted make probability
    
The model loads in the training and testing files, performs the same changes on both under one function to eliminate features, encode them or engineer new ones and 
