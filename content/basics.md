---
layout: default
title: Concepts and tools
parent: Outline
nav_order: 1
---

## Why should I learn Python?

Python is easy to learn and has a clean syntax. Therefore, its recommendable for both beginners and experienced programmers.
Data scientists, software engineers, and even hackers use Python because of its versatility, flexibility, and its many other features.. [source](https://www.codingdojo.com/blog/why-you-should-learn-python)

<img src="{{site.baseurl}}/content/figures/why_python.jpg">


***

## SYZYGY Environment

Members of the UBC community (anyone with a CWL) have access to UBC Syzygy.

Syzygy is a collection of research tools that are accessible through a web browser. One of these tools is `Jupyter` which is an electronic notebook that lets you run scripts in common programming languages and see the output immediately with no additional installation or setup required. Syzygy effectively gives you a robust Pythonenvironment to test and run simple scripts in.


<img src="{{site.baseurl}}/content/figures/ubc-syzygy.png">

Once you log in, you will probably see an empty folder. 


<img src="{{site.baseurl}}/content/figures/landing-page.png">

We will soon create a Python script and upload the data for this workshop on SYZYGY.

***

### Create a new Python 3 script


new > Python 3

<img src="{{site.baseurl}}/content/figures/python-script.png">

* Each cell holds either python code or text.

    * You can change between code and text in menu

* The empty bracket indicates that the cell has not been run

    * Once you run the code (run button), it will show a number indicating the order in which the command was run

    * You can go back to a cell and run it as many times as you desire. However, this might affect other parts of your script, so use this with caution!


**Tips and shortcuts**

* `esc` goes to the command palette. While on command mode:
    * `A` to insert cell above
    * `B` to insert cell below
    * `M` to change cell to markdown
    * `D` + `D` to delete current cell

* `shift` + `enter` runs the code in the current cell

* While typing a command press `tab` to have suggestions for auto-completion    

* In a cell containing code, the `#` serves as annotations or comments and they will not be executed


***


### Upload Data Files

Click the upload button > navigate to the folder containing the workshop data > select the files

<img src="{{site.baseurl}}/content/figures/upload.png">

For each upload file, SYZYGY will show the file name and a blue upload button. Click to upload!

***


## Packages

<img src="{{site.baseurl}}/content/figures/libs.jpg">

### Python packages

Python has many packages that provide helper functions that can facilitate your work. Some common data science packages are listed below:


* **Pandas** is a common module to load and manipulate data

* **Matplotlib** and **Seaborn** are plotting modules

* **Numpy** and **Scipy** are often used for statistical tests

* **Jupyter** provides facilities for writing Python code as notebooks, often used in teaching environments. SYZYGY uses Jupyter.

***

### Importing a Python Package or Module

1. First it's often suggested to setup a plotting package

Input
{: .label .label-green }
```python
# Matplotlib for plotting
from matplotlib import pyplot as plt
%matplotlib notebook
```

1. Then, we can load conventional packages

Input
{: .label .label-green }
```python
import csv # spreadsheet manipulation
import json # a common data structure in many programming languages
import pandas as pd # data processing, csv file I/O (e.g. pd.read_csv)
import numpy as np # linear algebra
from scipy import stats # statistics
from datetime import datetime # date time manipulation
```


