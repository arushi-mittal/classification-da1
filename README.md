# Data Analytics I - Assignment 1

### Arushi Mittal (2019101120)

## Overview

Using various classification algorithms to determine which one has the greatest accuracy for predicting whether an earthquake occured using various input features as a parameter from the input file `Indian Earthquakes List Update_Magnitudes.csv`.

The data given was extremely sparse, with many columns filled with `NaN` values, duplicate columns and redundant information. This was cleaned up in the following way:

- The first `9` rows of the csv file were omitted in order to remove the redundant data about titles, sources, etc.
- The column names were assigned to the dataframe for easier reference.
- Columns with duplicate names were removed from the database to reduce redundancy and dimensionality of the data.
- The 'MB', 'MS', and 'ML' columns were dropped because they were just conversions of the magnitude.
- The 'IST' time column was dropped because it was the same as 'UTC' time.
- The 'INTENSITY' column was dropped along with 'MME' and 'MMI' because they were extremely sparse compared to the other columns and could not add much value. Additionally, MMI and MME are other units of intensity.
- 'UTC' was also dropped because of formatting issues and sparsity of the column. Considering the time range of thousands of years, it did not add any value anyway.
- 'REFERENCE' was dropped because it did not add much value since organizations do not have any bearing on the occurence of an earthquake, and the data given was very low to begin with. Additionally, calculating distance between strings can be complicated.
- 'LOCATION' was dropped because locations can be spelt differently, with different degrees of specificity (eg: state names, region names, etc.) and we already have coordinates which are more useful than location names.

The other parameters were included ('DATE', 'DEPTH', 'LAT (N)', 'LON (E)', 'MONTH', 'YEAR') because all of them are relevant to the magnitude of an earthquake and have an impact on the model.

## Tasks

### 1. ROC

The ROC curves were plotted by plotting the `TPR` (True Positive Rate) against the `FPR` (False Positive Rate) for each parameter value and classification algorithm.

They can be seen in the code.ipynb file with all the information under the classification algorithm.


### 2. Best Classifier

Decision trees with a preprune depth of 5 were the most accurate model with an accuracy greater than 88.85%, whereas Decision Trees with 300 estimators had over 87.99 % accuracy. KNN had 88.25% accuracy. 

Decision trees tend to lay out the problem clearly,


### 3. Best Values

The best number of neighbors is 14, best preprune depth is 5, and the best number of estimators is 300 according to the accuracy percentage and also according to the ROC curves. 

The smoothness and perfect shape of the ROC curve increases with higher parameter value, however there is not much improvement observed beyond the best performing values. This is especially evident in the Adaboost classifier.

Additionally, the parameters ranked highest across a wide range of values and were large enough to make the dataset accurate, and small enough to make computation easy while ensuring the data was not overfit or overly complicated.

### 4. Feature Subset

The features included were 'DATE', 'DEPTH', 'LAT (N)', 'LON (E)', 'MONTH', 'YEAR' because they were relevant and added a lot of information to the different classifiers.

### 5. Result Analysis

Decision trees with a preprune depth of 5 were the most accurate model with an accuracy greater than 88.85%, whereas Decision Trees with 300 estimators were close with over 87.99 % accuracy. KNN had 88.25% accuracy.

Input features: 'DATE', 'DEPTH', 'LAT (N)', 'LON (E)', 'MONTH', 'YEAR'

After using SelectKBestFeatures to find the best features, we find the relevance of all the features in order of their usefulness to the model, and the score to determine their importance.

| Specs |       Score|
|------|--------|
|YEAR | 1244.538184|
| LON (E)|   463.297486|
|    DEPTH   | 66.529405|
| LAT (N)|    16.460592|
| MONTH   | 12.732038|
| DATE  |   2.389331|

Therefore, the next model uses 'YEAR', 'LON (E)', 'DEPTH', and 'LAT (N)' on a decision tree model with maximum depth of 5, and the improvement is `0.004560608919922049`, which is slightly under half a percentage point.

