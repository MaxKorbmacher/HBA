# Hemispheric Brain Age Lifespan Models
## General
The presented models are trained on tabular Desikan Kileany atlas region averaged grey matter surface area, cortical thickness and volume values.
The original (N=58,387) lifespan training set was upsampled to N=150,517.
The model files can be found here: https://osf.io/3f4md/ (file size too large for github).

## Validation
Fit in training data (N=150,517) and validation data (N = 6,608) for corrected brain age (c) and uncorrected brain age (u):
(R2 = Variance explained, MAE = Mean Absolute Error, RMSE = Root Mean Squared Error)
|    Model    | Hemisphere | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
| :---------: |  :-------: | :---------: |  :---: |  :---: |  :---: |
|Training u   |    both    | 0.967649	| 0.936345	| 4.837419	| 6.278804|
|Training c   |    both    | 0.999892	| 0.999783	| 1.321781	| 1.538669|
|Validation u |    both    | 0.968058	| 0.937137  | 4.849361	| 6.278737|
|Validation c |    both    | 0.999893	| 0.999785	| 1.333005	| 1.551646|

2. Fit in the external validation data


For usage please refer to the doi of the OSF repository until there will be an associated publication to refer to.
