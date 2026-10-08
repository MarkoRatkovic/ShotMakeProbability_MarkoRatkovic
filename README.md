# ShotMakeProbability_MarkoRatkovic
This project trains and fits a model on 425,719 non-fouled field goal shots in the NBA across two seasons and then tests it on 213,977 shots to return shot make probabilities with the goal of minimizing log loss by eliminating imprecision in the probability prediction. Three files are used in the generation of this model and the output of its predictions for shot make probability of the 213,977 shots it is tested on: 

  - training.csv: Holds data for 425,719 non-fouled field goal shots with 28 features including the target variable of the shot's binary outcome
  - testing.csv: Holds data for 213,977 non-fouled field goal shots with 27 features identical to those in training set but no target variable
  - submission.txt: Text file with shot IDs corresponding to those in testing set that is populated with each shot's predicted make probability
    
The model loads in the training and testing files, performs the same changes on both under one function to eliminate features, encode them or engineer new ones and then applies the changes identically to the data sets to ensure data alignment before loading them again.
  - A Softmax weighting approach through Euler's number is used on a feature holding four floats in an array to return value by exponential prioritization of higher index of values in array

A Gradient Boosting Classifier is used to train the model on the training set before applying it to the testing set. This Classifier specifies the learning rate of the model and number of leaf nodes per iteration to not overfit or underfit the model. The predicted shot make probabilities are generated and read into each one's corresponding shot ID of the testing set. These results are populated in the text file with precise predictions for each shot. 

The target variable of the shot's binary outcome is numerically encoded to evaluate the fit of the model by the Gradient Boosting Classifier. The log loss score is computed by measuring the predicted shot make probability against actual binary outcome values.
  - A log loss score of only 0.49672164765935883 is computed, denoting significant predictive value in the model far below a baseline rate of about 0.693 if a 0.5 probability prediction was assigned to each shot
  - Fitting on distance of shot from basket, number of shot contesters, distance of the contester(s) to shooter or shot type (layup, jumper, floater) would only incrementally minimize computed log loss of predicted probability, necessitating combination of encoded features
  - Computed log loss minimized through engineering of features with high predictive value and correlation with other highly predictive features, including pairing as a feature shot type and distance from basket or calculation of shot angle using shooter's position

Log loss score of 0.49672164765935883 is achieved through combination of incremental improvements to predictive ability of model, boosted iteratively by creation of small decision trees that fit to correct what the model has been predicting incorrectly. Shrinkage in trees resulting from the Gradient Boosting Classifier is seen in hundreds of smaller decision trees being created so each improves on results of previous one, closing gap between the predicted probability and actual probability to reduce log loss. 
