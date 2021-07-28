# Introduction to First ML
In this section, we will go through the features of First ML. Each line under a comment in the Notebook is an object that you can change/edit.

## Before starting
Make sure that all the necessary modules mentioned in the [requirements section](Requirements) are installed properly before continuing further.

It is also expected that you have already 'cleaned' your training data properly.

## Import all necessary modules
This should be the first cell you run whenever you open the Notebook. Run this cell to import all necessary modules used in this Notebook.
````{admonition} The first code cell
```
%matplotlib inline

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns 
from pyfuncs import *
sns.set_style("darkgrid")

from sklearn.preprocessing import StandardScaler  
from sklearn.model_selection import train_test_split
from sklearn.neural_network import MLPRegressor
from astropy.io import fits
from astropy.table import Table
from IPython.display import display 
from pathlib import Path
import os
import PySimpleGUI as sg
import winsound, cellbell, joblib
```
````

(content:data-prepare)=
## Read and prepare training data
Training data is loaded and split into smaller batches in this cell. You might want to split the data if you want to work with a smaller training data size or if you want to test your model with multiple different sets of training data.  

There are 4 objects in this cell that you can change.
````{admonition} Top part of the second code cell
```
# filename: name of file of training data
filename = 'Test1.fits'

# f: file format name (see astropy.Table documentation for more details)
f = 'fits'

# bsize: batch size
bsize = 10000

# n: number of batches
n = 2
```
````

`filename` is a string of the name/path of your training data. Test1.fits is the sample data that is located in the same directory as the First ML Notebook.

`f` is a string that tells the file reader the format of the file that will be read. An extensive list of supported formats is listed in [astropy's documentation](https://docs.astropy.org/en/stable/io/unified.html#ascii-formats).

`bsize` is an integer. It determines the size of each batch.

`n` is an integer. It determines the number of batches that will be split into. This integer could be 1 if you just want to work with a part of the loaded data.

## Start training!
In this code cell, the loaded data will be standardised and then used to train the `mlpregressor` model. Each batch of data from the previous step will be seperated into training data and testing data. Each batch of training data is used to train a different model. Each model is then tested with their respective testing data. The scalers and models is saved in a folder within the folder, "Saved_models_and_scalers". The results from testing will also be saved. The scalers and models are saved as .pkl files while the test results are saved as .json files. Finally, a table that shows the data in the new `fwrite` will be displayed.

`mlp` is the Multi-layer Perceptron model used in the Notebook. See the [sklearn.mlpregressor documentation](https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPRegressor.html) for more details regarding its hyperparameters.

`tperc` is the percentage of data used for training in each batch. It is a float between 0 and 1. The rest is used for testing. For example, `tperc = 0.7` means that 70% of the data in each batch is used for training; the other 30% is used for testing.

`rdnum` determines the number of different random states of the `mlpregressor` that will be used. By default, the model will always run with `random_state=33`. By setting `rdnum` to an integer larger than 1, a new model will be trained with a different `random_state`, until you have a number of models equal to `rdnum`. See the [sklearn.mlpregressor documentation](https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPRegressor.html) for more details regarding how `random_state` affects the model.

`fread` and `fwrite` are strings of the name/path of a testing result generated (or will be generated) by this Notebook. The data from `fread` and the current model will be saved to `fwrite`. Leaving `fread` blank would result in only the testing result from the current model being saved in `fwrite`. If `fread` and `fwrite` are the same, this means that the testing result from the current model will be saved in `fread` in addition to its original testing results. `fwrite` should never be left blank.

`mlpfolder` is the name of the folder used to save the current models and scalers. It is located within the folder, "Saved_models_and_scalers", which is located in the same directory as the First ML Notebook.

`hddlsz` is the hidden layer size of the model. `hddlsz=[(10,10)]`means that the model will have 2 hidden layers, with each hidden layer containing 10 nodes. You could write multiple hidden layer sizes into a list so that a model will be trained for each hidden layer size configuration in said list. For example, `hddlsz=[(10),(10,10),(10,10,10)]` would result in 3 models; one for each hidden layer size configuration, (10), (10,10) and (10,10,10).

## Read testing result (.json file that is generated by the MLP above)
In this cell, the testing result file generated by First ML will be read.

`fread` is the name/path of the testing result file that will be read.

## Mean score (coefficient of determination $R^2$) of each hidden layer size configuration
Run this code cell to display a table that shows mean $R^2$ value of each hidde layer size configuration in the testing result file read in the previous cell.

## Plot graph of predicted data VS sample data
Run this code cell to produce a graph of the predicted data from testing the model (ypredict) against the actual data from the testing data (ytest). The code only compares testing results using the same random state and are from the same batch. 

`rdst` is the random state of the testing results that will be graphed.

`Tdata` is an integer that tells the code which batch will be graphed. During the [splitting of data](content:data-prepare), each batch is given a name (which can also be seen in the testing results), dataset 0, dataset 1 and so on. If `Tdata=0`, then results from dataset 0 will be plotted into a graph.

## Load model and scaler
In this code cell, a model and scaler can be read so that it can be used in the next section.
```{warning}
Make sure that the scaler being read is the same scaler as the scaler used when the model was being trained.
```
`modelname` is the path of the model that will be read.

`scalername` is the path of the scaler that will be read. 

## Test loaded model
The model that was read above will be used on new data. The results will be displayed as a table.

`filename` is a string of the name/path of your training data.

`f` is a string that tells the file reader the format of the file that will be read. An extensive list of supported formats is listed in [astropy's documentation](https://docs.astropy.org/en/stable/io/unified.html#ascii-formats).