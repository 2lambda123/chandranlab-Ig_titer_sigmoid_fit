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
The output of a given run (model fit and evaluation) is saved in a user-defined directory

#### Processed input data
The transformed data used to train and test the fitted sigmoidal curve is saved saved as a separate excel file "*_processed.xlsx":

    Column A   Sample name

    Column B   Observed titers

    Column C   Observed Absorbance

    Column D   Log10 transformed titers


### Fitted model
Using the entire dataset, the script fits a first sigmoidal curve. The parameters of the sigmoidal curve (minimum y, maximum y, EC50, Hill coefficient) are saved in a text file '*_model.txt'

<p align="center">
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/fitted_sigmoidal.png"
	width="500" title="Input example"><br>
	Experimental data and its fitted sigmoidal<br>
</p>


#### Evaluation of fitted model by X-Fold cross-validation
dd

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

