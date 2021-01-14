# IG titer quantification from fitted sigmoidal curves

## Table of contents
* [Overview](#Overview)
* [Input](#Input)
* [Output](#Output)

## Overview


## Input
The input file is an excel file where the first column "Sample" describes the sample name, the second column "Titer" shows the experimentally determined titers and the third column "Absorbance" shows the corresponding absorbances at a given dilution point:


<p align="center">
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/input.png"
	width="400" title="Input example"><br>
	Overview of the input dataset used in this study<br>
</p>


## Output
### Processed input data


### Fitted model

<p align="center">
	<img src="https://github.com/gorkaLasso/Ig_titer_sigmoid_fit/blob/master/Images/fitted_sigmoidal.png"
	width="500" title="Input example"><br>
	Experimental data and its fitted sigmoidal<br>
</p>


### Evaluation of fitted model by X-Fold cross-validation
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

