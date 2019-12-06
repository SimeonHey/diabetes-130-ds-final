## Feature exploration

* Correlation scatter matrix
* Correlation with the output - plot the most important features and look for linearly separable data

## Feature engineering

* Remove consecutive patient visits with `patient_nbr`
* Introduce a `has_weight` feature
* Compress `diag_1,2,3` and `medical_specialty`
* Remove rows with `discharge_disposition` in `[11,13,14,19,20,21]`
* Do stuff with medicine changes
  * Remove all medicine columns
  * Keep counts for No, Steady, Up, Down
  * Remove medicine that have mostly NO values
  * DO BOTH

## Models

Standard ones:

* Logistic Regression -> PolynomialFeatures ->  RBFSampler
*  SGDClassifier with Perceptron -> SVM -> RBFSampler 
* `from sklearn.naive_bayes import GaussianNB, MultinomialNB`

Ensembles:

* RandomForestClassifier
* ExtraTreesClassifier

* VotingClassifier between 3 in the standard; try with soft and hard voting. Correlate the predictions of the base classifiers
* 

## Conclusions

