# What is First ML?
First ML is a Notebook that is designed to help people who are new to machine learning learn and use a simple Multi-layer Perceptron regressor model. 

The Multi-layer Perceptron model used in this Notebook is built from the sklearn.mlpregressor module.

## Before starting
Make sure that all the necessary modules mentioned in the [requirements section](../_build//html/docs/Requirements.html) are installed properly before continuing further.

It is also expected that you have already 'cleaned' your training data properly.

## Import all necessary modules
This should be the first cell you run whenever you open the Notebook. Run this cell to import all necessary modules used in this Notebook.
````
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

## Read and prepare training data
Training data is loaded and split in this cell. You might want to split the data if you want to work with a smaller training data size or if you want to test your model with multiple different sets of training data.  

There are 4 
```
# filename: name of file of training data
filename = 'Test1.fits'

# f: format name (see astropy.Table documentation for more details)
f = 'fits'

# bsize: batch size
bsize = 10000

# n: number of batches
n = 2
```