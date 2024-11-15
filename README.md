# Hemispheric Brain Age Lifespan Models

The presented models are trained on tabular Desikan Kileany atlas region averaged grey matter surface area, cortical thickness and volume values.
The original (N=58,387) lifespan training set was upsampled to N=150,517.

Fit in training data (N=150,517) and validation data (N = 6,608) for corrected brain age (c) and uncorrected brain age (u):
|Model	        | R	| R2|	MAE |	RMSE |
| :---: |  :---: |  :---: |  :---: |  :---: |
|training u:    | 0.967648963	| 0.936344516	|4.837418543	|6.278804198|
|training c:    | 0.999891698	|0.999783408	|1.321780908	|1.538669359|
|HC validation u:  | 0.968058192	|0.937136663|	4.849361137	|6.278737074|
|HC validation c: | 0.999892633	|0.999785278	|1.333004607	|1.55164662|

Fit in validation data similar to training data: 

The model files can be found here: https://osf.io/3f4md/ (file size too large for github).


For usage please refer to the doi of the OSF repository until there will be an associated publication to refer to.
