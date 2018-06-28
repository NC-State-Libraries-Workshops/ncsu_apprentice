---
layout: page
title: Working With Data

include_site_title: FALSE

order: 5
    
    
---

### Getting Started

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
a centimeter.




