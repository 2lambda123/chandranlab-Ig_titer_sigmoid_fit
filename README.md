# IG titer quantification from fitted sigmoidal curves

## Table of contents
* [Overview](#Overview)
* [Input](#Input)
* [Output](#Output)

## Overview


## Input
The input file is an excel file, the column titles need to be as described in the figure:

    Column A   "Sample": Describes the sample name
    
    Column B   "Titer": shows the experimentally determined titers
    
    Column C   "Absorbance": shows the corresponding absorbances at a given dilution point


<p align="center">
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/input.png"
	width="400" title="Input example"><br>
	Overview of the input dataset used in this study<br>
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
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/fitted_sigmoidal.png"
	width="500" title="Input example"><br>
	Experimental data and its fitted sigmoidal<br>
</p>


#### Evaluation of fitted model by X-Fold cross-validation
The nonlinear model is evaluated by X-fold (user-defined) cross-validation, where the original dataset is randomly partitioned into X equal size subsets, and one of the subsets serves as the testing set while the remaining nine subsets are used for training the non-linear model. This process is repeated 10 times, using subsets for testing and training each time to ensure that all data points in our dataset have been used once for testing. In addition, evaluation is also performed iteratively: the nonlinear model is evaluated by 10-fold cross-validation n (user-defined) number of times; at each iteraction the algorithm computes the R2 and Root Mean Squared Error (RMSE) value between the observed and predicted IgG titers. Non-linear regression was performed using the scipy library (Virtanen et al. 2020).

<p align="center">
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/histogram.png"
	width="500" title="Input example"><br>
	Histograme<br>
</p>

dd

<p align="center">
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/iter_0_10-fold_Observed_Vs_Predicted.png"
	width="500" title="Input example"><br>
	Observed Vs Predicted titers at a given iteration of X-fold cross-validation<br>
</p>


dd

