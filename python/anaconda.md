### Anaconda Reference
Anaconda allows for multiple Python environments.

This useful for having 3.x.x and 2.x.x installed and switching between them.

#### Check current Python version
via command line

    python -V

#### Update packages
    conda update --all

#### List current environments
[](http://conda.pydata.org/docs/using/envs.html#list-all-environments)

    conda info --envs
or

    conda env list

The default installed environment is named root

#### Creating a new Python environment
[](http://conda.pydata.org/docs/py2or3.html#create-python-2-or-3-environments)

    conda create -n environment_name python=x.x anaconda

Replace environment_name with the desired environment name and x.x with the version of the Python.

Anaconda will automatically download the specified version of Python if it is not yet installed.

#### Activating (switching) a Python environment
[](http://conda.pydata.org/docs/py2or3.html#use-a-different-version-of-python)

    source activate environment_name
