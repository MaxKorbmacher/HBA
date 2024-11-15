# Hemispheric Brain Age Lifespan Models
## General
The presented generalized additive models (GAMs) are trained on tabular Desikan Kileany atlas region averaged grey matter surface area, cortical thickness and volume values. The original (N=58,387) lifespan training set (mean age = 49.85±24.89 ,range: 5.11-90.10) was upsampled to N=150,517.
The model files can be found here: https://osf.io/3f4md/ (file size too large for github).

## Model usage
For usage of the models, please refer to the doi of the OSF repository (10.17605/OSF.IO/3F4MD) until there will be an associated publication to refer to.

## Validation
Fit in training data (N=150,517) and validation data (N = 6,608, mean age = 49.49±25.04, range: 5.28-86.7) for corrected brain age (c) and uncorrected brain age (u). Corrected brain age, is the individual level brain age where the training sample bias was regressed out (see: https://doi.org/10.1101/2024.09.11.612523, https://doi.org/10.1002/hbm.25837).

All training and validation data were obtained from healthy controls! Fit metrics are comparable to other models trained on similar data and corrected brain age estimates produce naturally better fit indices. However, the advantage of the presented models is their generalizability to other, external, datasets (see below) and their explainablity, since the models have a simple architecture of added splines which allowing polynomials up to the 4th order / k=4 knots.

We also want to highlight that hemisphere-specific models perform similar to models of both hemispheres (also highlighted previously: https://doi.org/10.1038/s41467-024-45282-3).

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

Fit in external validation data, which are all healthy controls (N = 751, mean age=38.83±9.77, range: 18.63-87.5):

| Hemisphere and Correction | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
|  :----------------------: | :---------: |  :---: |  :---: |  :---: |
|    both u    | 0.756130 |	0.571732 |	5.9837012 |	7.5361807 |
|    both c    | 0.998197 |	0.996397 |	1.1057842 |	1.2598217 |
|    both u    | 0.738188 |	0.544922 |	6.1625854 |	7.8137746 |
|    both c    | 0.997289 |	0.994586 |	1.3135404 |	1.5083689 |
|    right u   | 0.698197 |	0.487479 |	6.8279494 |	8.5589816 |
|    right c   | 0.996170 |	0.992355 |	1.3952090 |	1.6329008 |

An example of data fit for a single disease group, here multiple sclerosis patients (N = 748, mean age=38.63±9.46, range: 18.46-70.34):

| Hemisphere and Correction | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
|  :----------------------: | :---------: |  :---: |  :---: |  :---: |
|    both u    | 0.462638 |	0.214034 |	10.408278 |	12.496954 |
|    both c    | 0.998090 |	0.996185 |	0.5534728 |	0.6958106 |
|    both u    | 0.429159 |	0.184177 |	10.288801 |	12.525579 |
|    both c    | 0.996933 |	0.993876 |	0.7026801 |	0.8788364 |
|    right u   | 0.429137 |	0.184158 |	11.422675 |	13.760504 |
|    right c   | 0.995369 |	0.990759 |	0.8369094 |	1.0625441 |

Finally, we were interested in how our model performs in longitudinal data looking at three healthy individuals scanned in total 103 times over a 1.5 years period (mean age per subject: 30.66, 28.09, 40.66).
|Subject|	Both Pearson's r|	p	|Rigth Pearson's r|	p	|Left Pearson's r|	p|
| :---: |:---: |:---: |:---: |:---: |:---: |:---: |
|sub-1 u	|0.223207|	0.177966|	0.132640|	0.427283|	0.153016|	0.359058|
|sub-2 u	|0.208589|	0.196474|	0.270274|	0.091659|	0.135290|	0.405211|
|sub-3 u	|0.523605|	0.007227|	0.344758|	0.091462|	0.409404|	0.042125|
|sub-1 c	|0.966508|	7.418*10^-23|	0.917191|	5.882*10^-16|	0.935485|	7.660*10^-18|
|sub-2 c	|0.956229|	7.033*10^-22|	0.900784|	2.437*10^-15|	0.924323|	1.750*10^-17|
|sub-3 c	|0.916193|	1.309*10^-10|	0.772431|	6.064*10^-06|	0.819871|	5.299*10^-07|

Longitudinal results suggest slightly better individual-level model fit than previous models (e.g., https://doi.org/10.1002/brb3.3219).

Interrim conclusion from the model validation: We recommend using corrected brain age estimates, especially in the case of longitudinal analyses.

## Explainability
An important advantage of the utilzed GAMs is that their model coefficients can be fairly easily interpreted. The degrees of freedom are directly indicative of the polinomial degree of each spline (established for each variable).
