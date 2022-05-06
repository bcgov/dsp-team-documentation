[![img](https://img.shields.io/badge/Lifecycle-Maturing-007EC6)](https://github.com/bcgov/repomountie/blob/master/doc/lifecycle-badges.md)

# Basic Python Setup
---

This document will get python up and running on the Windows B.C. Government computers. After conda installation, Mac steps would be similar. 

## 1. Python Installer

We recommend using [conda](https://docs.conda.io/en/latest/) to install python and required packages. Conda allows the creation of virtual environments so that different projects requiring different dependencies will not interfere with each other. You can download it in multiple ways:

* [Anaconda](https://www.anaconda.com/) is a full GUI interface that will install a broad assortment of data science packages immediately. I find it slow and clunky, and end up using the CLI anyways so I would only go this route if you prefer the GUI aspect. 

* [Miniconda](https://docs.conda.io/en/latest/miniconda.html) is a lightweight version that installs conda, and not much else. From here you create your own conda environments, tailoring the environment to the specific packages that you require. This does require use of the CLI and more upfront setup, but ultimately gets you to the same place as the full Anaconda distribution.


## 2. Environment Creation

[Here is a good cheat sheet for managing your environments.](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) Here we will set up a basic environment that will have most of the useful base datascience packages installed. 

1. Open up an **Anaconda Powershell Prompt** (I prefer Powershell, but the regular Prompt is fine as well). 

2. Create a new environment:

```
conda create --name myenv
```

3. Activate the environment:

```
conda activate myenv
```

4. Install relevant packages into this environment. Note the use of `-c conda-forge` here. This is not always required, but some packages have their most up-to-date versions hosted on conda-forge instead of the default anaconda package repository, and so this first install I will typically pull from there. When installing more advanced packages, the install instructions will typically indicate which repo to pull from. 

```
conda install -c conda-forge python=3.9 packageA packageB packageC...
```

These are the packages that I will include in a standard environment:

* **scipy**: includes statistical modeling and other scientific features 
* **numpy**: the standard math package
* **pandas**: the standard dataframes package
* **matplotlib**: the standard plotting package
* **seaborn**: an additional plotting package with matplotlib compatability
* **scikit-learn**: the standard datascience package
* **jupyter**: gives you notebook options for coding
* **notebook**: the standard jupyter notebook
* **jupyterlab**: my favourite notebook environment
* **openpyxl**: a pandas add on required for reading excel files 

At this point you should be able to open a notebook and utilize any of these packages. To open up a notebook, navigate via the conda shell to the directory of the project, and initiate the notebook with:

```
jupyter lab
```

or if you prefer the traditional notebook,

```
notebook
```

## 3. Install an IDE

Install your IDE of choice. Some people like to use [VS Code](https://code.visualstudio.com/), others prefer to use [PyCharm](https://www.jetbrains.com/pycharm/). Both come with git interfaces, PEP-8 convention checking, built in terminals, etc. No matter which IDE you choose, you will likely want to include a few extensions to make it work smoothly with your python projections.

* [Instructions for setting up conda environments in VS Code](https://code.visualstudio.com/docs/python/environments)
* [Python extension to make the best of your VS Code experience](https://code.visualstudio.com/docs/languages/python)
