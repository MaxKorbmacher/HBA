# Hemispheric Brain Age Lifespan Models
## General
The presented models are trained on tabular Desikan Kileany atlas region averaged grey matter surface area, cortical thickness and volume values.
The original (N=58,387) lifespan training set was upsampled to N=150,517.
The model files can be found here: https://osf.io/3f4md/ (file size too large for github).

## Validation
Fit in training data (N=150,517) and validation data (N = 6,608) for corrected brain age (c) and uncorrected brain age (u):
(R2 = Variance explained, MAE = Mean Absolute Error, RMSE = Root Mean Squared Error)
|    Sample and BA    | Hemisphere | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
| :---------: |  :-------: | :---------: |  :---: |  :---: |  :---: |
|Training u   |    both    | 0.967649	| 0.936345	| 4.837419	| 6.278804|
|Training c   |    both    | 0.999892	| 0.999783	| 1.321781	| 1.538669|
|Validation u |    both    | 0.968058	| 0.937137  | 4.849361	| 6.278737|
|Validation c |    both    | 0.999893	| 0.999785	| 1.333005	| 1.551646|
|Training u   |    right   | 0.941864 | 0.887105	| 5.888029	| 7.508926|
|Training c   |    right   | 0.999472 |	0.998944	| 2.082605 |	2.379014|
|Validation u |    right   | 0.952799 |	0.907827 |	5.905113	| 7.626600|
|Validation c |    right   | 0.999554	| 0.999109 |	2.342847	| 2.718069|
|Training u   |    left   | 0.947675 |	0.898088	| 5.592969	| 7.134335| 
|Training c   |    left   | 0.999600	| 0.999201	| 1.905326	| 2.160859| 
|Validation u |    left   | 0.956443	| 0.914783	| 5.636057	| 7.331873| 
|Validation c |    left   | 0.999653	| 0.999306	| 2.140207	| 2.473550| 







For usage please refer to the doi of the OSF repository until there will be an associated publication to refer to.
