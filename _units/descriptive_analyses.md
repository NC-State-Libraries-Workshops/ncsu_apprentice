---
layout: page
title: Getting To Know Your Data

include_site_title: FALSE

order: 5

supporting_files:
  - file: 'id1'
    href: 'https://github.com/psu-data-workshops/introduction_to_r/blob/master/scripts/descriptive_analsis.R'
    name: Examples script for this unit.  
    
    
---


In this unit we'll learn how to view, select and transform data. We'll also 
do some basic descriptive analysis and visualizations. This will not only
get you more comfortable with R, but the first thing you should do with any
data set is get to know it, *very well*.

Our first data set will be a built in data set in R. R comes with a lot of 
packages you can use to learn R. Most packages you install and load either 
use these or have their own data included to use in their examples. We will
learn how to import external data sets in the next unit.

To see what packages are available just type `data()` into your console, 
a page called R Data Sets will display in your top left view port. You 
can also use `data(package = .packages(all.available = TRUE))` and R will
display all the data sets included in your packages, grouped by the package.
While most data sets in packages for provided as an example, there are also
packaages where the data set IS the package, the **ISOcodes** package for 
example consist only of lists of various standard codes such as country codes.

### Learning About Your Data

We'll start with the iris data included in R. In your console type the following.
Technically you can just use the iris data as is. I like to create a copy of it,
treating the original file as immutable. This helps prevent me from overwriting
the original file on accident.

```R
    iris_data <- iris  # Assings the iris data frame to a new variable
    
    View(iris_data)  # Display the entire data set
```

If the data set is very large you may not want to open the entire thing at
once in your viewer. You can still peak at it though.

```R
    head(iris_data)     # Displays the first 6 rows plus the headers
    tail(iris_data)     # Displays the last 6 rows plaus the headers
```

We are starting to learn about the data. We can tell that this appears to be
flower morphology data for some iris species. Before we can do a useful analysis
we need to learn a lot more. First lets look at the help file. Note that we have
to use the original copy.

```R
    help(iris)
```

We get some back ground about the data, format, some citations and examples 
of use. I suspect the units are millimeters, but unfortunately the help file
doesn't tell us. Referring to the Fisher (1936) paper I see that the units are
actually centimeters! R.A. Fisher was one of the early and most influential 
geneticists, evolutionary biologists and statisticians. He has a few statistical
methods named after him.

As a side note, when you create your own data, you should keep a README file
that gives information about your data set as well. These can not only help
others understand your data, but also ensure that details about your data
aren't lost over time time.

One other thing I see is the use of dot case (i.e. Sepal.Length). This works
fine in R, but it will break just about every other programming language. If we
are going to use this data elsewhere, or share it, it would be good to make it more
interoperable. This is easily done.

```R
    > names(iris_data) <- c("sepal_length", "sepal_width", "petal_length", 
                            "petal_width", "species")
    > head(iris_data)
      sepal_length sepal_width petal_length petal_width species
    1          5.1         3.5          1.4         0.2  setosa
    2          4.9         3.0          1.4         0.2  setosa
    3          4.7         3.2          1.3         0.2  setosa
    4          4.6         3.1          1.5         0.2  setosa
    5          5.0         3.6          1.4         0.2  setosa
    6          5.4         3.9          1.7         0.4  setosa
```

### Exploring The Data

Lets start to do some preliminary descriptive analyses. The most basic,
and often the first thing to do with quantitative data is just to get things
like mean and median.

```R
    > summary(iris_data)
      sepal_length    sepal_width     petal_length    petal_width          species  
     Min.   :4.300   Min.   :2.000   Min.   :1.000   Min.   :0.100   setosa    :50  
     1st Qu.:5.100   1st Qu.:2.800   1st Qu.:1.600   1st Qu.:0.300   versicolor:50  
     Median :5.800   Median :3.000   Median :4.350   Median :1.300   virginica :50  
     Mean   :5.843   Mean   :3.057   Mean   :3.758   Mean   :1.199                  
     3rd Qu.:6.400   3rd Qu.:3.300   3rd Qu.:5.100   3rd Qu.:1.800                  
     Max.   :7.900   Max.   :4.400   Max.   :6.900   Max.   :2.500  
```
 
One thing to look for is that the mean and median are close to each other. 
This is true for all but *petal_length*, where the two differ by more than half
a centimeter. We would also like to know other parameters such as variance,
standard deviation, skew and kurtosis. We can do it one by one.

```R
    > sd(iris_data$sepal_length)
    [1] 0.8280661
    > sd(iris_data$sepal_length[which(iris_data$species == "setosa")])
    [1] 0.3524897
```

This gets tedious. Fortunately, as is usually the case there are one or more
packages to do this for us. We'll use the `describe` and `describeBy` functions
in the `psych` package. 

```R
    # Assuming you have installed and loades psych
    > help("describe")
    
    # We only get columns 1 through 4. The fifth species column isnt numeric.
    > describe(iris_data[, c(1:4)])
                 vars   n mean   sd median trimmed  mad min max range  skew kurtosis   se
    sepal_length    1 150 5.84 0.83   5.80    5.81 1.04 4.3 7.9   3.6  0.31    -0.61 0.07
    sepal_width     2 150 3.06 0.44   3.00    3.04 0.44 2.0 4.4   2.4  0.31     0.14 0.04
    petal_length    3 150 3.76 1.77   4.35    3.76 1.85 1.0 6.9   5.9 -0.27    -1.42 0.14
    petal_width     4 150 1.20 0.76   1.30    1.18 1.04 0.1 2.5   2.4 -0.10    -1.36 0.06
    
    # We can group by species too.
    > describeBy(iris_data[, c(1:4)], iris_data$species)

     Descriptive statistics by group 
    group: setosa
                 vars  n mean   sd median trimmed  mad min max range skew kurtosis   se
    sepal_length    1 50 5.01 0.35    5.0    5.00 0.30 4.3 5.8   1.5 0.11    -0.45 0.05
    sepal_width     2 50 3.43 0.38    3.4    3.42 0.37 2.3 4.4   2.1 0.04     0.60 0.05
    petal_length    3 50 1.46 0.17    1.5    1.46 0.15 1.0 1.9   0.9 0.10     0.65 0.02
    petal_width     4 50 0.25 0.11    0.2    0.24 0.00 0.1 0.6   0.5 1.18     1.26 0.01
    ------------------------------------------------------------------------------------------------- 
    group: versicolor
                 vars  n mean   sd median trimmed  mad min max range  skew kurtosis   se
    sepal_length    1 50 5.94 0.52   5.90    5.94 0.52 4.9 7.0   2.1  0.10    -0.69 0.07
    sepal_width     2 50 2.77 0.31   2.80    2.78 0.30 2.0 3.4   1.4 -0.34    -0.55 0.04
    petal_length    3 50 4.26 0.47   4.35    4.29 0.52 3.0 5.1   2.1 -0.57    -0.19 0.07
    petal_width     4 50 1.33 0.20   1.30    1.32 0.22 1.0 1.8   0.8 -0.03    -0.59 0.03
    ------------------------------------------------------------------------------------------------- 
    group: virginica
                 vars  n mean   sd median trimmed  mad min max range  skew kurtosis   se
    sepal_length    1 50 6.59 0.64   6.50    6.57 0.59 4.9 7.9   3.0  0.11    -0.20 0.09
    sepal_width     2 50 2.97 0.32   3.00    2.96 0.30 2.2 3.8   1.6  0.34     0.38 0.05
    petal_length    3 50 5.55 0.55   5.55    5.51 0.67 4.5 6.9   2.4  0.52    -0.37 0.08
    petal_width     4 50 2.03 0.27   2.00    2.03 0.30 1.4 2.5   1.1 -0.12    -0.75 0.04
```

Next we'll do some simple visualizations to get a visual description of our data.

    







