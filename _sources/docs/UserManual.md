# Introduction to First ML
In this section, we will go through the features of First ML. Each line under a comment in the Notebook is an object that you can change/edit.

## Import all necessary modules
This should be the first cell you run whenever you open the Notebook. Run this cell to import all necessary modules used in this Notebook.
````{note}
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
The first cell
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