## Matplotlib, Seaborn and Basemap Reference
### Matplotlib
Matplotlib was designed to be effective at understanding your intent, no matter the level of abstraction. There are many ways to create the same plot in Matplotlib and most of the differences come down to the level of abstraction you want to work with for a specific task.

Most of the use features matplotlib are in the pyplot module.

    import matplotlib.pyplot as plt

If using IPython notebook / Jupyter, add the following magic command:

    %matplotlib inline
[](http://ipython.readthedocs.io/en/stable/interactive/magics.html?commands#magic-matplotlib)

#### Common Graphs
    plt.scatter(x_var, y_var)   # scatter
    plt.plot(x_var, y_var)      # line
    plt.bar(x_var, y_var)       # bar
    plt.barh(x_var, y_var)      # horizontal bar

    plt.show()    # output graph, call this last

#### Chart Labels
    plt.title("Title")
    plt.xlabel("X axis label")
    plt.ylabel("Y axis label")
    plt.xticks(rotation=90)     # adjusts orientation of x-axis units
    plt.yticks(rotation=90)     # adjusts orientation of y-axis units

#### Vertical Lines
    plt.axvline(x_val, color='r')

#### Using Styles
    plt.style.use("style_name")
Good styles

    fivethirtyeight
    ggplot
    dark_background
    bmh

### Matplotlib Figures, Subplots, and Axes
Figures, subplots, and axes belong to a lower level of abstraction compared to PyPlot.

#### Figures
The figure is the canvas upon which graphs are drawn.

    fig = plt.figure(figsize=(5,7))   # x,y in inches

#### Subplots
Subplots are the individual graphs.

    ax = fig.add_subplot(1,1,1)
    ax = fig.add_subplot(nrows=1, ncols=1, plot_number=1)
Each figure may have one or multiple subplots.

    ax1 = fig.add_subplot(2,1,1)
    ax2 = fig.add_subplot(2,1,2)
Plot numbers are assigned row-wise

#### Axes    
Axes contain the contents (data, ticks, units, and labels) for any given subplot.

    ax.set_title("Some Title")
    ax.set_xlim([0,14])
    ax.set_xlabel("X values")
    ax.scatter(x_var, y_var, color='darkblue', marker='o')
    plt.show()

### Seaborn
Seaborn is a Python library supported by Stanford University that enables you to create beautiful, presentation-ready data visualizations. While Seaborn uses Matplotlib under the hood to represent, manipulate, and customize plots, it exposes a high-level API that abstracts away a lot of the internal Matplotlib logic.

Simply importing seaborn overrides the default graph style

    import seaborn as sns
When output plots use Seaborn's show() function instead of matplotlib's

    sns.plt.show()

#### Histograms
    sns.distplot(data, kde=False)

#### Boxplots
    sns.boxplot('x_var', 'y_var', data=dataframe, ax=ax1)

#### Labels
    sns.plt.axlabel('x axis label', 'y axis label')

#### Set styles
[](https://stanford.edu/~mwaskom/software/seaborn/generated/seaborn.set_style.html#seaborn.set_style)

    sns.set_style('style_name')     #darkgrid, whitegrid, dark, white

#### Pair Plots
Plots every permutation of pairwise scatter plots

    sns.pairplot(dataframe, vars=['col1', 'col2', 'col3'])

### Basemap
Basemap makes it easy to convert from the spherical coordinate system (latitudes & longitudes) to the Mercator projection. While Basemap uses Matplotlib to actually draw and control the map, the library provides many high-level methods that enable us to work with maps quickly.

Reference Image for Latitude/Longitude:
![Lat Lon Image](http://survival-mastery.com/wp-content/uploads/2015/04/img2.png)

    from mpl_toolkits.basemap import Basemap

Calling the constructor. Specifying Mercator projection and lat/lon for lower left and upper right corners.

    m = Basemap(projection='merc', llcrnrlat=-80, urcrnrlat=80, llcrnrlon=-180, urcrnrlon=180)

The Basemap object can now be used to transform lat/lon to x,y coordinates.

    x,y = m(longitudes, latitudes)

#### Drawing Functions
Coordinates can be put on a scatterplot

    m.scatter(x,y,s=1)    # s specifies the size of dots

Adding coastlines

    m.drawcoastlines()

Adding great circle curves

    m.drawgreatcircle(start_lon, start_lat, end_lon, end_lat, linewidth=1)

Use pyplot to customize and display the map

    plt.show()
