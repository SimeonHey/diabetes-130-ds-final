## Andrew Long's Medium Article

- Feature engineering - rename chapter
  - He does binary classification - and indeed my models often confuse >30 with NO. Could make a pipeline that first predicts <30 or other, and then tries to split >30 and NO
  - Look at `discharge_disposition_id` - "`11,13,14,19,20,21` are related to death or hospice. We should remove these samples from the predictive model since they cannot be readmitted."
  - `admission_type_id,discharge_disposition_id,admission_source_id` are numerical here, but are IDs (see IDs_mapping). They should be considered categorical.
  - About `diag`s: you could group these ICD codes to reduce the dimension. We will use number_diagnoses to capture some of this information.  
  - `medical_speciality` — has many categorical variables, so we should consider this when making features. He preserves top 10 and groups the rest
  - Mention `admission_type_id` and the other `id`s - that you treat them like categorical
  - He introduces a `has_weight` value
  - BTW: In case the output variable is of un-uniform distribution, could: sub-sample the dominant classes, over-sample the imbalanced classes (like bagging), or create synthetic data for the underrepresented data. BUT isn't the under-representativeness representative of the data too?
  - `StandardScaler` - standard!
- Models (only new ones)
  - Using dev test for testing the trained while developin
  - `from sklearn.neighbors import KNeighorsClassifier` - look the k nearest neighbours, and determine the class by considering the fraction of them that are positive
  - `from sklearn.ensemble import GradientBoostingClassifier`
- Evaluation (binary classification ofc)
  - `roc_auc_score`
  - `prevalence` - fraction of positive samples
  - `accuracy` - fraction that was correctly predicted (TP + TN / all)
  - `recall` - fraction of all positives that were positively predicted (recollected)
  - `specificity` - the complete opposite of recall - fraction of all negatives that were negatively predicted
  - `precision` - when you predict something positive, in what fraction is it true?
  - `specificity` and `sensitivity (recall)` are not affected by `prevalence`. precision tends to fall with it?
  - Plots the AUC against # of training samples on the training and cross validation scores. This gives power for some asymptotic conclusions. He concludes that the model is a victim of high bias - underfitting.
- Tuning
  - Considers `feature_importance`
  - In real life, could go to experts and ask them about features that are important but I don't understand
  - Could use `feature_importance` to reduce variance (that is, overfitting) - choose top N, or do a PCA on them and choose K new features (which will be complex combinations of those before)
  - Optimizes SGD, Random Forests and Gradient Boosting, since others perform worse (or take a lot to train)
  - Uses `RandomizedSearchCV` (needs a scorer and `auc` is good) to find the most optimal hyperparameters, but could also use `GridSearchCV`
  - uses `pickle`ing to save trained models - clever guy

## Usman Raza

* Uses log transformations
* Creates/derives features from existing ones
* Drops `payer_code` and `medical_speciality`
* Drops rows of`diag_1,2,3` only when the 3 of them are missing
* Drops rows of missing `gender`
* Only removes dead patients `discharge_disposition` = 11
* New feature = `number_outpatient + number_emergency + number_inpatient` to reflect how often this person has been to the hospital
* New feature = number of changes (which are `Yes` and `No` values)
* New feature = number of medications used
* New feature = uses knowledge about the diag_noses to combine them... but there should be a cleverer way!!!!!
* **Ordinal Categorical Variables** and **Nominal Categorical Variables**
* New feature = combine admission types by similar types e.g Emergency, Urgent Care & Trauma (but I believe this is not my job but that of experts)
* Similar for `A1Cresult, max_glu_serum`
* Drops  the subsequent patient visits`df2 = df.drop_duplicates(subset= ['patient_nbr'], keep = 'first')`
* Log Transformations:
  * **Kurtosis** is a measure of the combined weight of a distribution's tails relative to the center of the distribution.
  * **Skewness** is a measure of the asymmetry of the probability distribution
  * Use `np.log1p(thing)` to calculate log(1+x)
  * After taking log transformations, they remove outliers (more than 3SD apart from the mean)
* synthetic minority over-sampling technique (SMOTE) - wow what a duche.. might be the reason for the high results
* Models:
  * 60% with Logistic Regression
  * fucking 90% with Decision Trees
  * fucking 94% with Random Forests

## Lectures rev

* AdaBoost and other boosting methods
* PolynomialFeatures with Logistic regression/classification
* `Perceptron`, `Support Vector Machines`
* Kernel tricks (shit performance so fat)
* precision-recall trade off curve
* ROC
* OvA and OvO tests
* Bias (constant error due to underfitting), Variance(variable error due to overfitting) and Irreducible error
* Bias - Variance trade off - overfitting will reduce bias but increase variance
* But aggregation reduces both bias and variance
* "further randomness can be introduced by training on
  random subsets of the features (supported in sklearn)":
  * I Random Patches method when sampling both training instances and
    features
  * I Random Subspaces method when keeping all training instances but
    sampling features
* Boosting
  * Train predictors sequentially, so that each next classifier tries to
    correct the errors from its predecessor
  * Different learning rates for Adaptive Boost
  * Early stopping & optimal parameter with Gradient Boost
  * 

