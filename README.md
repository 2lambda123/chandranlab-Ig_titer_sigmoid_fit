# IG titer quantification from fitted sigmoidal curves

## Table of contents
* [Overview](#Overview)
* [Input](#Input)
* [Output](#Output)

## Overview
fit\_and_evaluate.ipynb fits a sigmoidal data to a given input file describing antibody titers and the corresponding absorbance readout using the following equation:


y = ymin + (ymax - ymin) / (1 + 10<sup>((log<sub>10</sub>EC<sub>50</sub> - x)*Hill)</sup>)
 
 
Where y corresponds to the absorbance; ymin and ymax are the minimum and maximum absorbances respectively; EC50 is the IgG titer that gives half of maximum absorbance ymax ; Hill describes the slope of the curve and; x is the log10 of the IgG titer. 

Evaluation of the model is carried out by X-fold cross-validation carried out N number of times. Both X and N parameters can be tuned by the user.

This is part of a laboratory-developed antibody test that uses readily available research-grade reagents to detect SARS-CoV-2 exposure in patient blood samples with high sensitivity and specificity. We further show that this test affords the estimation of viral spike-specific IgG titers from a single sample measurement, thereby providing a simple and scalable method to measure the strength of an individual's immune response.

Link to the preprint: https://www.medrxiv.org/content/10.1101/2020.09.10.20192187v1


## Input
The input file is an excel file, the column titles need to be as described in the figure:

    Column A   "Sample": Describes the sample name
    
    Column B   "Titer": shows the experimentally determined titers
    
    Column C   "Absorbance": shows the corresponding absorbances at a given dilution point


<p align="center">
	<b>Overview of the input dataset used in this study</b><br>
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/input.png"
	width="400" title="Input example"><br>
	
</p>


## Output
The output (model fit and evaluation) is saved in a user-defined directory

#### Processed input data
The transformed data used to train and test the fitted sigmoidal curve is saved saved as a separate excel file "*_processed.xlsx":

    Column A   Sample name

    Column B   Observed titers

    Column C   Observed Absorbance

    Column D   Log10 transformed titers


#### Fitted model
Using the entire dataset, the script fits a first sigmoidal curve. The parameters of the sigmoidal curve (minimum y, maximum y, EC50, Hill coefficient) are saved in a text file '*_model.txt'. A plot is also generated to visualize both the experimental data (blue dots) and the fitted sigmoidal curve (black line):

<p align="center">
	<b>Experimental data and its fitted sigmoidal</b><br>
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/fitted_sigmoidal.png"
	width="500" title="Input example"><br>
</p>


#### Evaluation of fitted model by X-Fold cross-validation
The non-linear model is evaluated by X-fold (user-defined) cross-validation, where the original dataset is randomly partitioned into X equal size subsets, and one of the subsets serves as the testing set while the remaining nine subsets are used for training the non-linear model. This process is repeated 10 times, using subsets for testing and training each time to ensure that all data points in our dataset have been used once for testing. In addition, evaluation is also performed iteratively: the nonlinear model is evaluated by 10-fold cross-validation n (user-defined) number of times. Non-linear regression was performed using the scipy library (Virtanen et al. 2020).


At each evaluation round the algorithm computes the R<sup>2</sup> and Root Mean Squared Error (RMSE) value between the observed and predicted IgG titers and plots a histogram ('histogram.pdf') of the R2 values:


<p align="center">
	<b>R<sup>2</sup> Example of R<sup>2</sup> histogram after evaluating the sigmoidal curve by 10-Fold cross-validation 100 times</b><br>
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/histogram.png"
	width="500" title="Input example"><br>

</p>


A summary file ('output\_dir/summary.xlsx') describes the R<sup>2</sup> and RMSE at each round of evaluation carried out:

    Column A   Dataframe row index (disregard)

    Column B   Evaluation round

    Column C   R<sup>2</sup>

    Column D   Root Mean Squared Error (RMSE)

<p align="center">
	<b>Example of a summary describing the evaluation of the sigmoidal model</b><br>
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/summary.png"
	width="500" title="Input example"><br>
	
</p>


In addition, observed and predicted titers are plotted, along with the fitted regression model, at each evaluation round ('output\_dir/iter\_n\_X-fold\_Observed\_Vs_Predicted.pdf'):

<p align="center">
	<b>Example of observed Vs predicted titers at a given iteration of X-fold cross-validation</b><br>
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/iter_0_10-fold_Observed_Vs_Predicted.png"
	width="500" title="Input example"><br>
	
</p>


Observed and predicted values are also reported in an excel file ('output\_dir/iter\_n\_X-fold\_predictions.xlsx') at any given evaluation round:

    Column A   Sample name

    Column B   Observed titers

    Column C   Observed Absorbance

    Column D   Log10 transformed titers
    
    Column E   Predicted titers (Log10 transformed)



<p align="center">
	<b>Example of the evaluation summary describing R<sup>2</sup> and RMSE at each round of 10-fold cross-validation</b><br>
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/output_xfold_eval.png"
	width="500" title="Input example"><br>
	
</p>



