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



## Conclusions

