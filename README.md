# Hemispheric Brain Age Lifespan Models
## General
The presented models are trained on tabular Desikan Kileany atlas region averaged grey matter surface area, cortical thickness and volume values.
The original (N=58,387) lifespan training set was upsampled to N=150,517.
The model files can be found here: https://osf.io/3f4md/ (file size too large for github).

## Validation
1. Fit in training data (N=150,517) and validation data (N = 6,608) for corrected brain age (c) and uncorrected brain age (u):
|Model	   | Hemisphere | Pearson's r	| Variance explained|	Mean Absolute Error |	Root Mean Squared Error |
| :---: |  :---: | :---: |  :---: |  :---: |  :---: |
|Training u:    | 0.967648963	| 0.936344516	|4.837418543	|6.278804198|
|Training c:    | 0.999891698	|0.999783408	|1.321780908	|1.538669359|
|Validation u:  | 0.968058192	|0.937136663|	4.849361137	|6.278737074|
|Validation c: | 0.999892633	|0.999785278	|1.333004607	|1.55164662|

2. Fit in the external validation data


For usage please refer to the doi of the OSF repository until there will be an associated publication to refer to.
