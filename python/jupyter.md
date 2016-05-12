### Jupyter Reference

    jupypter notebook

Runs in web browser
#### Inline Matplotlib
Execute in cell

    %matplotlib inline
[](http://ipython.readthedocs.io/en/stable/interactive/magics.html?commands#magic-matplotlib)

#### Autocomplete on TAB
Execute in cell

    %config IPCompleter.greedy=True

Or to turn on permanently, modify ~/.ipython/profile_default/ipython_config.py, around lines 506-514

    #------------------------------------------------------------------------------
    # Completer configuration
    #------------------------------------------------------------------------------

    # Activate greedy completion
    #
    # This will enable completion on elements of lists, results of function calls,
    # etc., but can be unsafe because the code is actually evaluated on TAB.
    c.Completer.greedy = True # <-- uncomment this line and set it to True

If there is no ipython_config.py in ~/.ipython/profile_default/, create one with:

    ipython profile create
[](http://stackoverflow.com/questions/33498591/ipython-autocompletion-for-list-or-dict-of-objects)
