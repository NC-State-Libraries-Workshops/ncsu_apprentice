---
layout: page
title: Modifying Data

order: 7
---

Now that we have spent some time getting to know our data, we may need
to modify, or subset it. Common reasons for doing this are, the data needs 
transformation, recoding data, removing outliers or reshaping for certain analyses. 
Whenever you change your data, it is important you do so in such a way that 
your changes are transparent, and reversible. Fortunately R makes this easy.

### Selecting Observations

Sometimes you only need certain records for an analyses. Perhaps your only
want to compare two species of iris, or after looking at your data it is clear
that some outliers were erroneous and should be excluded. We've already seen 
some of this before, here are a few ways to do this.

```R
    # Selecting a range for rows
    > iris_subset <- iris_data[c(3:10),]
    > iris_subset
       sepal_length sepal_width petal_length petal_width species
    3           4.7         3.2          1.3         0.2  setosa
    4           4.6         3.1          1.5         0.2  setosa
    5           5.0         3.6          1.4         0.2  setosa
    6           5.4         3.9          1.7         0.4  setosa
    7           4.6         3.4          1.4         0.3  setosa
    8           5.0         3.4          1.5         0.2  setosa
    9           4.4         2.9          1.4         0.2  setosa
    10          4.9         3.1          1.5         0.1  setosa
    
    # Selecting based on a value
    > iris_versicolor <- iris_data[which(iris_data$species == "versicolor"),]
    > head(iris_versicolor)
       sepal_length sepal_width petal_length petal_width    species
    51          7.0         3.2          4.7         1.4 versicolor
    52          6.4         3.2          4.5         1.5 versicolor
    53          6.9         3.1          4.9         1.5 versicolor
    54          5.5         2.3          4.0         1.3 versicolor
    55          6.5         2.8          4.6         1.5 versicolor
    56          5.7         2.8          4.5         1.3 versicolor
    
    # Selecting multiple criteria
    > iris_outlier <- iris_data[which(iris_data$species == "versicolor" & iris_data$sepal_length < 5),]
    > iris_outlier
       sepal_length sepal_width petal_length petal_width    species
    58          4.9         2.4          3.3           1 versicolor
    
    # Equivalent to above, also selecting only 2 columns.
    > iris_outlier_2 <- subset(iris_data, sepal_length < 5 & species == "versicolor", select=c(petal_length, petal_width))
    > iris_outlier_2
       petal_length petal_width
    58          3.3           1
    
    # Random Sample from our data
    
```

### Transforming A Variable

Sometimes it is necessary to apply a transformation to a variable. Here 
we apply a log transformation. Notice how easy it is to define a new column too.

```R
    > iris_data$log_petal_width <- log(iris_data$petal_width + 1)
    > head(iris_data)
      sepal_length sepal_width petal_length petal_width species log_petal_width
    1          5.1         3.5          1.4         0.2  setosa       0.1823216
    2          4.9         3.0          1.4         0.2  setosa       0.1823216
    3          4.7         3.2          1.3         0.2  setosa       0.1823216
    4          4.6         3.1          1.5         0.2  setosa       0.1823216
    5          5.0         3.6          1.4         0.2  setosa       0.1823216
    6          5.4         3.9          1.7         0.4  setosa       0.3364722
```

### Recoding A Variable

Recoding a variable works the same way. We'll expand the complexity a little 
bit at the same time. In this example lets call everthing with a petal shorter
than the first quartile "small", everthing bigger than the last quartile "big"
and everthing in the middle "medium". We also use `NA` as a default value, 
a built in value in R to denote a missing value.


```R
    # We can generate the quartiles and use these values.
    # NOTE: the percent sign causes some display problems here.
    > petal_quantile <- quantile(iris_data$petal_length)
    > petal_quantile
      0%  25%  50%  75% 100% 
      1.00 1.60 4.35 5.10 6.90 
    
    # First we initialize a new variable in this case.
    # We use "NA" as the default value.
    > iris_data$size <- NA
    
    # We recode petal_length in three steps
    > iris_data[
        which(iris_data$petal_length < petal_quantile["25%"]),]$size <- "small"
    > iris_data[
        which(iris_data$petal_length >= petal_quantile["25%"] & 
            iris_data$petal_length <= petal_quantile["75%"])
        ,]$size <- "medium"
    > iris_data[
        which(iris_data$petal_length > petal_quantile["75%"]),]$size <- "large"
    > iris_data$size
      [1] "small"  "small"  "small"  "small"  "small"  "medium" "small"  ... 
      ...
      [137] "large"  "large"  "medium" "large"  "large"  "medium" "medium" ...
      
    # Since size really is a factor we can make this variable a factor.
    > iris_data$size <- factor(iris_data$size)
    > iris_data$size
      [1] small  small  small  small  small  medium small  small  small ...
      ...
      [133] large  medium large  large  large  large  medium large  ...
      Levels: large medium small
      
```

Finally sometimes we need to *reshape* our data. Usually this is because
the statistical test, or function we want to use requires the data in a 
specific format. We are going to use two functions from the `reshape2` package,
`melt()` and `cast()`. First we will `melt()` the data converting it to
*long-form*, one measurement per row as opposed to four. If you omit
the `id.vars` option, it works as well but you get a warning. With more complex
data frames it might not work, so its a good habit to be explicit.

```R
    # Make sure you load reshape2
    
    > iris_data$id <- 1:nrow(iris_data)  # This will allow us to unmelt later
    > melted_iris <- melt(iris_data, id.vars = c("id", "species"), 
                                     variable.name = "floral_attribute", 
                                     value.name = "measurement")
    > head(melted_iris)
      id species floral_attribute measurement
      1  1  setosa     sepal_length         5.1
      2  2  setosa     sepal_length         4.9
      3  3  setosa     sepal_length         4.7
      4  4  setosa     sepal_length         4.6
      5  5  setosa     sepal_length         5.0
      6  6  setosa     sepal_length         5.4
    > tail(melted_iris)
      id   species floral_attribute measurement
      595 145 virginica      petal_width         2.5
      596 146 virginica      petal_width         2.3
      597 147 virginica      petal_width         1.9
      598 148 virginica      petal_width         2.0
      599 149 virginica      petal_width         2.3
      600 150 virginica      petal_width         1.8
```

Next we can cast the data, converting it to a *short-form*. This is harder than
melting so it can take some trial an error. Here we will create a table of 
means and also recreate the original data.


```R
    # Means table
    > iris_means <- dcast(melted_iris, species ~ floral_attribute, mean, 
                                value.var = "measurement")
    > iris_means
         species sepal_length sepal_width petal_length petal_width
        1     setosa        5.006       3.428        1.462       0.246
        2 versicolor        5.936       2.770        4.260       1.326
        3  virginica        6.588       2.974        5.552       2.026
         
         
    # Recreate original data
    > recast_iris <- dcast(melted_iris, id + species ~ floral_attribute, 
                                    value.var = "measurement")
    > head(recast_iris)
      id species sepal_length sepal_width petal_length petal_width
        1  1  setosa          5.1         3.5          1.4         0.2
        2  2  setosa          4.9         3.0          1.4         0.2
        3  3  setosa          4.7         3.2          1.3         0.2
        4  4  setosa          4.6         3.1          1.5         0.2
        5  5  setosa          5.0         3.6          1.4         0.2
        6  6  setosa          5.4         3.9          1.7         0.4
    
```



Now that we can describe, and manipulate our data, we can do some analyses
and accompany them with visualizations in the next couple units.
        
        

    







