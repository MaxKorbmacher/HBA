# Hemispheric Brain Age Lifespan Models
## General
The presented models are trained on tabular Desikan Kileany atlas region averaged grey matter surface area, cortical thickness and volume values.
The original (N=58,387) lifespan training set was upsampled to N=150,517.
The model files can be found here: https://osf.io/3f4md/ (file size too large for github).

## Validation
Fit in training data (N=150,517) and validation data (N = 6,608) for corrected brain age (c) and uncorrected brain age (u).
These are all healthy controls! Fit metrics are comparable to other models trained on similar data and corrected brain age estimates produce naturally better fit indices. However, the advantage of the presented models is their generalizability to other, external, datasets (see below) and their explainablity, since the models have a simple architecture of added splines which allowing polynomials up to the 4th order / k=4 knots.


|    Sample and BA    | Hemisphere | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
| :---------: |  :-------: | :---------: |  :---: |  :---: |  :---: |
|Training u   |    both    | 0.956751 |	0.915372 |	5.093497 |	6.501277 |
|Training c   |    both    | 0.999760 |	0.999520 |	1.612139 |	1.813835 |
|Validation u |    both    | 0.962232 |	0.925891 |	5.282685 |	6.829246 |
|Validation c |    both    | 0.999784 |	0.999567 |	1.796074 |	2.065603 |
|Training u   |    right   | 0.941864 | 0.887105	| 5.888029 | 7.508926|
|Training c   |    right   | 0.999472 |	0.998944	| 2.082605 |	2.379014|
|Validation u |    right   | 0.952799 |	0.907827 |	5.905113	| 7.626600|
|Validation c |    right   | 0.999554	| 0.999109 |	2.342847	| 2.718069|
|Training u   |    left   | 0.947675 |	0.898088	| 5.592969	| 7.134335| 
|Training c   |    left   | 0.999600	| 0.999201	| 1.905326	| 2.160859| 
|Validation u |    left   | 0.956443	| 0.914783	| 5.636057	| 7.331873| 
|Validation c |    left   | 0.999653	| 0.999306	| 2.140207	| 2.473550| 
(R2 = Variance explained, MAE = Mean Absolute Error, RMSE = Root Mean Squared Error)

Fit in external validation data, which are all healthy controls (N = 751):


An example of data fit for a single disease group, here multiple sclerosis patients (N = 748):

| Hemisphere and Correction | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
|  :----------------------: | :---------: |  :---: |  :---: |  :---: |
|    both u    | 0.462638 |	0.214034 |	10.408278 |	12.496954 |
|    both c    | 0.998090 |	0.996185 |	0.5534728 |	0.6958106 |
|    both u    | 0.429159 |	0.184177 |	10.288801 |	12.525579 |
|    both c    | 0.996933 |	0.993876 |	0.7026801 |	0.8788364 |
|    right u   | 0.429137 |	0.184158 |	11.422675 |	13.760504 |
|    right c   | 0.995369 |	0.990759 |	0.8369094 |	1.0625441 |



For usage please refer to the doi of the OSF repository (10.17605/OSF.IO/3F4MD) until there will be an associated publication to refer to.
