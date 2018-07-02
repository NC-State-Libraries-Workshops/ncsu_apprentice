---
layout: page
title: Modifying Data

include_site_title: FALSE

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

    







