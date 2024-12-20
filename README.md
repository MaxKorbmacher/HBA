# Hemispheric Brain Age Lifespan Models
## General
The presented generalized additive models (GAMs) are trained on tabular Desikan Kileany atlas region averaged _cortical_ grey matter surface area, cortical thickness and volume values. The original (N=58,387) lifespan training set (mean age = 49.85±24.89 ,range: 5.11-90.10) was upsampled (using [SMOGNR](https://github.com/nickkunz/smogn)) to N=150,517 to provide a more even distribution.
The model files can be found [here](https://osf.io/3f4md/) (file size too large for github).

_Why using these models and not other models with lower error (e.g., RMSE, MAE)?_ Besides the large training sample, providing a better representation of the true population, we took several steps to make the models as **simple, explainable and generalizable** as possible.
- [x] Multiple approaches of explaining the model provided.
- [x] Training sample age bias corrected age outputted.
- [x] Largest samples ever used for brain age training.
- [x] Robust to acquisition variability: Multiple scanners, sites.
- [x] Robust to field strength differences: 1.5T and 3T data used.
- [x] Robust to software version: Multiple FreeSurfer version used.

## Model usage: from raw image to brain age prediction
1. After the FreeSurfer recon-all call or similar, e.g. using FastSurfer, tabular information are available per subject. We use the averages of the parcels of the Desikan-Killiany atlas as specified in the FreeSurfer output per subject for each hemisphere (no whole brain or hemispheric averages).
2. Whether a brain age shall be predicted for a single subject or several, the obtained tables can be merged to a table per metric (e.g., thickness) using stats2table_bash.sh
3. Now, the resulting tables need to be merged (again!) into a single table. There is a provided merge.py script in the repository that can be used for that purpose: run 'python3 merge.py "path/where/recon-all/output/tables/are"' (without apostrophes) from your terminal. You end up with tables which can be used as input to predict age / to obtain the desired brain age predictions. Simply add "age" as a variable and you will also obtain corrected brain age predictions. The data frame can contain additional variables which will not be used by the model. The output file will contain all input data + the brain age predictions. **For an example of the minimum input data for predictions see example_data.csv** (note that this is example does **not** contain real data).
4. Run 'Rscript predict.R /path/to/your/data.csv /path/to/the/output.csv /path/to/the/model.rda /path/to/the/training/sample/bias/correction/params.csv' (without apostrophes) from your terminal and you will obtain the predictions in the current/working directory. You can add additional arguments to change paths and the output file name. Note, the bias correction parameters are in the files bias_correction_params_both.csv, bias_correction_params_left.csv, and bias_correction_params_right.csv. The bias correction file needs to match the model, i.e. bias_correction_params_left.csv for Lsim_model.rda. sim_model.rda is the model using both hemispheres, Rsim_model.rda the model using the right hemisphere.

*For usage of the models, please refer to the OSF repository "Korbmacher, M. (2024). Hemispheric Brain Age Lifespan Models. OSF. https://doi.org/10.17605/OSF.IO/3F4MD" until there will be an associated publication to refer to.*
*Please consider also citing our paper introducing hemispheric brain age: "Korbmacher, M., van der Meer, D., Beck, D. et al. Brain asymmetries from mid- to late life and hemispheric brain age. Nat Commun 15, 956 (2024). https://doi.org/10.1038/s41467-024-45282-3"*

## Validation
Fit in training data (N=150,517) and validation data (N = 6,608, mean age = 49.49±25.04, range: 5.28-86.7) for corrected brain age (c) and uncorrected brain age (u). Corrected brain age, is the individual level brain age where the training sample bias was regressed out ([de Lange et al.](https://doi.org/10.1002/hbm.25837), practical example: [Korbmacher et al.](https://doi.org/10.1101/2024.09.11.612523)).

All training and validation data were obtained from healthy controls! Fit metrics are comparable to other models trained on similar data and corrected brain age estimates produce naturally better fit indices. However, the advantage of the presented models is their generalizability to other, external, datasets (see below) and their explainablity, since the models have a simple architecture of added splines which allowing polynomials up to the 4th order / k=4 knots.

We also want to highlight that hemisphere-specific models perform similar to models of both hemispheres ([also highlighted previously](https://doi.org/10.1038/s41467-024-45282-3)).

|    Sample and BA    | Hemisphere | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
| :---------: |  :-------: | :---------: |  :---: |  :---: |  :---: |
|Training u   |    both    | 0.9568|0.9154|5.0935|6.5013|
|Training c   |    both    | 0.9634|0.9281|4.8933|6.2186|
|Test u |    both    | 0.9622|0.9259|5.2827|6.8292|
|Test c |    both    | 0.9680|0.9370|5.2034|6.6508|
|Training u   |    right   | 0.9419|0.8871|5.8880|7.5089|
|Training c   |    right   | 0.9534|0.9090|5.5863|7.0712|
|Test u |    right   | 0.9528|0.9078|5.9051|7.6266|
|Test c |    right   | 0.9621|0.9256|5.7657|7.3501|
|Training u   |    left   | 0.9477|0.8981|5.5930|7.1343|
|Training c   |    left   | 0.9572|0.9162|5.3303|6.7600|
|Test u |    left   | 0.9564|0.9148|5.6361|7.3319|
|Test c |    left   | 0.9642|0.9297|5.5712|7.1221|

<sub> (R2 = Variance explained, MAE = Mean Absolute Error, RMSE = Root Mean Squared Error) </sub>

Fit in external validation data, which are all healthy controls (N = 751, mean age=38.83±9.77, range: 18.63-87.5):

| Hemisphere and Correction | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
|  :----------------------: | :---------: |  :---: |  :---: |  :---: |
|    both u    | 0.7561|0.5717|5.9837|7.5362|
|    both c    | 0.7849|0.6161|5.9661|7.4548|
|    left u    | 0.7382|0.5449|6.1626|7.8138|
|    left c    | 0.7744|0.5997|6.1404|7.7003|
|    right u   | 0.6982|0.4875|6.8279|8.5590|
|    right c   | 0.7425|0.5513|6.6580|8.3101|

An example of data fit for a single disease group, here multiple sclerosis patients (N = 748, mean age=38.63±9.46, range: 18.46-70.34):

| Hemisphere and Correction | Pearson's r	|   R2   |	 MAE  |	 RMSE  |
|  :----------------------: | :---------: |  :---: |  :---: |  :---: |
|    both u    | 0.4626|0.2140|10.4083|12.4970|
|    both c    | 0.5357|0.2870|9.5808|11.5617|
|    left u    | 0.4292|0.1842|10.2888|12.5256|
|    left c    | 0.5163|0.2666|9.3252|11.4368|
|    right u   | 0.4291|0.1842|11.4227|13.7605|
|    right c   | 0.5153|0.2656|10.3816|12.5946|

Finally, we were interested in how our model performs in longitudinal data looking at three healthy individuals scanned in total 103 times over a 1.5 years period (mean age per subject: 30.66, 28.09, 40.66).
|Subject|	Both Pearson's r|	p	|Right Pearson's r|	p	|Left Pearson's r|	p|
| :---: |:---: |:---: |:---: |:---: |:---: |:---: |
|sub-1 u	|0.2232	|0.1780|	0.1326|	0.4273|	0.1530|	0.3591|
|sub-2 u	|0.2086|	0.1965|	0.2703|	0.0917	|0.1353	|0.4052|
|sub-3 u	|0.5236|	0.0072	|0.3448|	0.0915	|0.4094	|0.0421|
|sub-1 c	|0.2466|	0.1356	|0.1595|	0.3389	|0.1779	|0.2852|
|sub-2 c	|0.2290|	0.1552	|0.2905|	0.0690	|0.1583	|0.3292|
|sub-3 c	|0.5310|	0.0063	|0.3536|	0.0828  |0.4171	|0.0380|

Longitudinal results suggest slightly better individual-level model fit than previous models (e.g., https://doi.org/10.1002/brb3.3219).

Interrim conclusion from the model validation: We recommend using corrected brain age estimates, especially in the case of longitudinal analyses.

Another reasoning for using corrected estimates is boosting effect sizes for group differences. Let's take the mentioned MS sample as an example again:
As an example how corrected brain age estimates boost predictions:
Corrected BAG differences between MS (mean age = 38.63±9.46 years) and HC (mean age = 38.73±9.61) are more clearly expressed when correcting for the training age bias:
See for that first the corrected BAG differences between MS and HC (paired samples t-tests):

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

### 1. Degrees of freedom per region
![splineshape](https://github.com/user-attachments/assets/349fb647-ad89-4ee1-ab31-0d1cde895562)
The degrees of freedom are directly indicative of the polinomial degree of each spline (established for each variable): 1=linear, 2=quadratic, 3=cubic
Mean scores for volumes=2.496281, thickness=2.869149, surface area=2.878631 (i.e., most splines are somewhere between quadratic and cubic).

### 2. Feature weight maps
![feature_importance](https://github.com/user-attachments/assets/6fac246d-9421-4402-9daf-5ae084a1babd)
The presented feature weights are the direct model coefficients from the GAMs. Based on these maps, precentral/motor cortex, pericalcarine, caudal anterior cingulate, lateral occipital regions are of importance to the model.

### 3. Knockout importance
![knock](https://github.com/user-attachments/assets/b25c5c7a-f70d-40c1-8e92-4dd4205296de)

Top row: brain age from both hemispheres. Middle and bottom rows: brain ages from single hemispheres.
The Cohen's d values from paired samples t-tests represent the difference between brain predicted age from the whole model compared to the predictions from the "lesion model", where volume, surface area and thickness are set to 0. 
The mean values represent the mean(lesion brain prediction) minus mean(in-tact brain predictions). We chose to present the differences between means, as these come closest to how predictions could be compared on a single-subject level. How to interpret the figure: red colour indicates a higher brain age caused by the lesion/knockout, blue colour the opposite. This procedure answers the question "Is the predicted age higher or lower when region X is knocked out?" and can thereby inform about the importance of a single region for predictions.

### 4. Age stratified knowckouts

One can also stratify by age groups to compare whether there age-group specific feature importances.

![stratified_knockout](https://github.com/user-attachments/assets/3fcb8f88-cffe-47c5-8ecf-59f5f9e86e2e)

### 5. Age-specific individual-level variability

As another stringent test, one can manipulate individual subject data to range values within a plausible spectrum (the training sample's minimum and mximum values) within a single brain's regions. Here, we vary the values of a single metric one region at a time in 1000 steps from the observed minimum to maximum values in the training sample in a single representative individual of the model for each year in the training set age distribution. Representative subjects were defined as subjects with the lowest brain age gap. The Resulting brain age predictions for each of the 1000 steps were then correlated with the respective metric. These corerlations were equal for all the subjects, indicating a stable model performance independent of the age (which confirms the findigs above).
![single_sub](https://github.com/user-attachments/assets/74c68e6e-f590-4b66-be9a-fc9e755698e1)


For more information or questions contact Max Korbmacher: max.korbmacher[at]gmail.com
