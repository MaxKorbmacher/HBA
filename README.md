# Hemispheric Brain Age Lifespan Models
## General
The presented generalized additive models (GAMs) are trained on tabular Desikan Kileany atlas region averaged grey matter surface area, cortical thickness and volume values. The original (N=58,387) lifespan training set (mean age = 49.85±24.89 ,range: 5.11-90.10) was upsampled to N=150,517.
The model files can be found here: https://osf.io/3f4md/ (file size too large for github).

## Model usage: from raw image to brain age prediction
1. After the FreeSurfer recon-all call or similar, e.g. using FastSurfer, tabular information are available per subject. We use the averages of the parcels of the Desikan-Killiany atlas as specified in the FreeSurfer output per subject for each hemisphere (no whole brain or hemispheric averages).
2. Whether a brain age shall be predicted for a single subject or several, the obtained tables can be merged to a table per metric (e.g., thickness) using stats2table_bash.sh
3. Now, the resulting tables need to be merged (again!) into a single table. There is a provided merge.py script in the repository that can be used for that purpose: run 'python3 merge.py "path/where/recon-all/output/tables/are"' (without apostrophes) from your terminal. You end up with tables which can be used as input to predict age / to obtain the desired brain age predictions. Simply add "age" as a variable and you will also obtain corrected brain age predictions. The data frame can contain additional variables which will not be used by the model. The output file will contain all input data + the brain age predictions. **For an example of the minimum input data for predictions see example_data.csv**
4. Run 'Rscript predict.R /path/to/your/data.csv /path/to/the/output.csv /path/to/the/model.rda /path/to/the/training/sample/bias/correction/params.csv' (without apostrophes) from your terminal and you will obtain the predictions in the current/working directory. You can add additional arguments to change paths and the output file name. Note, the bias correction parameters are in the files bias_correction_params_both.csv, bias_correction_params_left.csv, and bias_correction_params_right.csv. The bias correction file needs to match the model, i.e. bias_correction_params_left.csv for Lsim_model.rda. sim_model.rda is the model using both hemispheres, Rsim_model.rda the model using the right hemisphere.

*For usage of the models, please refer to the OSF repository "Korbmacher, M. (2024). Hemispheric Brain Age Lifespan Models. OSF. https://doi.org/10.17605/OSF.IO/3F4MD" until there will be an associated publication to refer to.*

## Validation
Fit in training data (N=150,517) and validation data (N = 6,608, mean age = 49.49±25.04, range: 5.28-86.7) for corrected brain age (c) and uncorrected brain age (u). Corrected brain age, is the individual level brain age where the training sample bias was regressed out (see: https://doi.org/10.1002/hbm.25837).

All training and validation data were obtained from healthy controls! Fit metrics are comparable to other models trained on similar data and corrected brain age estimates produce naturally better fit indices. However, the advantage of the presented models is their generalizability to other, external, datasets (see below) and their explainablity, since the models have a simple architecture of added splines which allowing polynomials up to the 4th order / k=4 knots.

We also want to highlight that hemisphere-specific models perform similar to models of both hemispheres (also highlighted previously: https://doi.org/10.1038/s41467-024-45282-3).

|    Sample and BA    | Hemisphere | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
| :---------: |  :-------: | :---------: |  :---: |  :---: |  :---: |
|Training u   |    both    | 0.956750671687792|0.915371847775041|5.09349719782765|6.50127671123974|
|Training c   |    both    | 0.963398170008129|0.928136033975012|4.89328500185453|6.21857468360546|
|Validation u |    both    | 0.962232357394819|0.925891109617591|5.28268535093494|6.82924637097514|
|Validation c |    both    | 0.967967842137675|0.936961743412667|5.20338122552432|6.65083281740381|
|Training u   |    right   | 0.941862701440411|0.887105348364628|5.88802889069848|7.50892578376154|
|Training c   |    right   | 0.953412256989657|0.908994931778112|5.58627888939932|7.0712003066598|
|Validation u |    right   | 0.952799431861064|0.907826757354766|5.9051132058119|7.62660008676113|
|Validation c |    right   | 0.962059792149728|0.925559043671179|5.76566294913709|7.35008605125979|
|Training u   |    left   | 0.947675122347843|0.898088137516999|5.59296910712197|7.13433489642016|
|Training c   |    left   | 0.957168444522712|0.916171431190029|5.3302534400188|6.76003172428471|
|Validation u |    left   | 0.956442819006717|0.914782866029515|5.63605720772647|7.33187318454623|
|Validation c |    left   | 0.964227077399118|0.929733856789644|5.57121999591334|7.12215803497811|

(R2 = Variance explained, MAE = Mean Absolute Error, RMSE = Root Mean Squared Error)

Fit in external validation data, which are all healthy controls (N = 751, mean age=38.83±9.77, range: 18.63-87.5):

| Hemisphere and Correction | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
|  :----------------------: | :---------: |  :---: |  :---: |  :---: |
|    both u    | 0.756129919604673|0.571732455321369|5.98370121165647|7.53618066884458|
|    both c    | 0.784920399082748|0.616100032896221|5.96605257239848|7.45480676141757|
|    left u    | 0.738188083258667|0.544921646265104|6.16258544540482|7.81377459265903|
|    left c    | 0.774412123883334|0.599714137617496|6.14040058971738|7.70037265663554|
|    right u   | 0.698197155424722|0.487479267843173|6.82794944573506|8.55898161718222|
|    right c   | 0.742476964351839|0.551272042593122|6.65796764633157|8.31013770536209|

An example of data fit for a single disease group, here multiple sclerosis patients (N = 748, mean age=38.63±9.46, range: 18.46-70.34):

| Hemisphere and Correction | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
|  :----------------------: | :---------: |  :---: |  :---: |  :---: |
|    both u    | 0.462637902532409|0.214033828859586|10.4082787109805|12.4969539450843|
|    both c    | 0.535708898309448|0.286984023727923|9.58081588153022|11.5616606943567|
|    left u    | 0.429158637468531|0.184177136113846|10.2888006631915|12.5255791764549|
|    left c    | 0.516285702288648|0.266550926387682|9.32516867981733|11.4368185316271|
|    right u   | 0.429136769391267|0.184158366843574|11.4226751222381|13.7605043198014|
|    right c   | 0.515346555058868|0.265582071811042|10.381603146451|12.5945757584713|

Finally, we were interested in how our model performs in longitudinal data looking at three healthy individuals scanned in total 103 times over a 1.5 years period (mean age per subject: 30.66, 28.09, 40.66).
|Subject|	Both Pearson's r|	p	|Rigth Pearson's r|	p	|Left Pearson's r|	p|
| :---: |:---: |:---: |:---: |:---: |:---: |:---: |
|sub-1 u	|0.22320709	|0.177966078|	0.132639698|	0.427283165|	0.153016081|	0.3590577|
|sub-2 u	|0.208588882|	0.196474389|	0.270273605|	0.091659096	|0.13528954	|0.405211205|
|sub-3 u	|0.523604727|	0.007226934	|0.344758447|	0.091462119	|0.409403763	|0.042124956|
|sub-1 c	|0.246593076|	0.135573488	|0.159460294|	0.338930544	|0.177910042	|0.28523668|
|sub-2 c	|0.229019752|	0.155174112	|0.290541558|	0.068951919	|0.158322876	|0.329192221|
|sub-3 c	|0.530987825|	0.006313065	|0.353684003|	0.082838285|	0.417134587	|0.038028953|

Longitudinal results suggest slightly better individual-level model fit than previous models (e.g., https://doi.org/10.1002/brb3.3219).

Interrim conclusion from the model validation: We recommend using corrected brain age estimates, especially in the case of longitudinal analyses.

Another reasoning for using corrected estimates is boosting effect sizes for group differences. Let's take the mentioned MS sample as an example again:
As an example how corrected brain age estimates boost predictions:
Corrected BAG differences between MS (mean age = 38.63±9.46 years) and HC (mean age = 38.73±9.61) are more clearly expressed when correcting for the training age bias:
See for that first the corrected BAG differences between MS and HC:

| BAG | Cohen's d & 95% CI | t(df) | p|
|:---:|:---:|:---:|:---:|
|Both BAG c| d=-1.00[-1.11;-0.89] | t(1462)=-19.40| p<2.2*10^-16|
|L BAG c| d=-0.90[-1.17;-0.79]| t(1459.3)=-17.44| p<2.2*10^-16|
|R BAG c| d=-0.90[-1.16;-0.79]| t(1468.5)=-17.43| p<2.2*10^-16|
|Both BAG u| d=-0.89[-1.15;-0.79]| t(1466-7)=-17.29| p<2.2*10^-16|
|L BAG u| d=-0.77[-0.88;-0.67]| t(1465.5)=-15.00|  p<2.2*10^-16|
|R BAG u| d=-0.77[-0.87;-0.66]| t(1475.1)=-14.87|  p<2.2*10^-16|

We see clear differences between the outlined group differences.

## Explainability
An important advantage of the utilzed GAMs is that their model coefficients can be fairly easily interpreted using ANOVA test, the respective degrees of freedom and by knocking out regions by setting all feature values of a specific region to 0. See a summary of the findings below. The data used for the visulaisation are the training data. However, lesion-styled interpretability is also possible in any unseen data by simpy setting the values of a single region to zero.

1. Degrees of freedom per region
![splineshape](https://github.com/user-attachments/assets/349fb647-ad89-4ee1-ab31-0d1cde895562)
The degrees of freedom are directly indicative of the polinomial degree of each spline (established for each variable): 1=linear, 2=quadratic, 3=cubic
Mean scores for volumes=2.496281, thickness=2.869149, surface area=2.878631 (i.e., most splines are somewhere between quadratic and cubic).

2. Feature weight maps
![feature_importance](https://github.com/user-attachments/assets/6fac246d-9421-4402-9daf-5ae084a1babd)

3. Knockout importance
**Coming soon**

4. Age stratified knowckouts
4.1 The model considering **both** hemispheres
![knockout_imp](https://github.com/user-attachments/assets/12fb5f95-8c9f-4d18-9c65-4dedb12f9606)

The Cohen's d values represent the difference between brain predicted age from the whole model compared to the predictions from the lesion model. 
The mean values represent the mean(lesion brain prediction) minus mean(in-tact brain predictions). We chose to present the differences between means, as these come closest to how predictions could be compared on a single-subject level. This answers the question "Is the predicted age higher or lower when region X is knocked out?" and can thereby inform about the importance of a single region for predictions.
