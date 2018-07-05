---
layout: page
title: Data Analysis 2

order: 9

supporting_files: 
  - file: id1
    file_name: 'analysis_2.R'
    link_text: Example script for this unit.  
---

### Loading And Saving Data

We'll start off with learning how to load and save data. We'll do it a bit 
backwards and save a built in data set first, then load it again. We will use some
United States state data from 1977 `state.x77`.

```R
    > state_data <- state.x77
    > View(state_data)
    > help("state.x77")
```

According to the help file, the data is in matrix form. I prefer data frames
so we'll convert it to to one.

```R
    > state_data <- data.frame(state_data)
    > View(state_data)
```

Saving, or writing this data to your computer is easy. Here are a few options.

```R
    ### Export it to a file in different ways

    # Write to a comma separated file, usually preferred
    write.csv(state_data, "state_data.csv")
    
    # Substitutes commas for decimals in number and semicolons for commas
    # as a delimiter, useful for Europeans
    write.csv2(state_data, "state_data_eur.csv")
    
    # You can specify your own delimiters too
    write.table(state_data, "state_data_tab.txt", sep="\t")
```

Importing data is usually as easy. However, in practice you will often find 
data that is poorly or inconsistently formatted, this can take some time to 
fix.

```R
    # Notice R adds an X for the state name in some instances.
    
    > new_state_data <- read.csv("state_data.csv")
    > head(new_state_data)
                   X Population Income Illiteracy Life.Exp Murder HS.Grad Frost   Area
        1    Alabama       3615   3624        2.1    69.05   15.1    41.3    20  50708
        2     Alaska        365   6315        1.5    69.31   11.3    66.7   152 566432
        3    Arizona       2212   4530        1.8    70.55    7.8    58.1    15 113417
        4   Arkansas       2110   3378        1.9    70.66   10.1    39.9    65  51945
        5 California      21198   5114        1.1    71.71   10.3    62.6    20 156361
        6   Colorado       2541   4884        0.7    72.06    6.8    63.9   166 103766
    > eur_state_data <- read.csv2("state_data_eur.csv")
    > head(eur_state_data)
                   X Population Income Illiteracy Life.Exp Murder HS.Grad Frost   Area
        1    Alabama       3615   3624        2.1    69.05   15.1    41.3    20  50708
        2     Alaska        365   6315        1.5    69.31   11.3    66.7   152 566432
        3    Arizona       2212   4530        1.8    70.55    7.8    58.1    15 113417
        4   Arkansas       2110   3378        1.9    70.66   10.1    39.9    65  51945
        5 California      21198   5114        1.1    71.71   10.3    62.6    20 156361
        6   Colorado       2541   4884        0.7    72.06    6.8    63.9   166 103766
    > tab_state_data <- read.table("state_data_tab.txt", sep = "\t")
    > head(tab_state_data)
                   Population Income Illiteracy Life.Exp Murder HS.Grad Frost   Area
        Alabama          3615   3624        2.1    69.05   15.1    41.3    20  50708
        Alaska            365   6315        1.5    69.31   11.3    66.7   152 566432
        Arizona          2212   4530        1.8    70.55    7.8    58.1    15 113417
        Arkansas         2110   3378        1.9    70.66   10.1    39.9    65  51945
        California      21198   5114        1.1    71.71   10.3    62.6    20 156361
        Colorado         2541   4884        0.7    72.06    6.8    63.9   166 103766
```

### More Analyses

#### Correlations and Plot Matrixes

There are a number of variables in this data. A common thing to do is to 
create a correlation matrix among them. A correlation measures a linear 
relationship between two variables. A positive correlation suggests that as one 
parameter goes up so does the other. A negative correlation suggests that
as one parameter increases the other decreases. We measure the strength of the 
correlation with a correlation coefficient *R*, no relation to the statistical 
language. The correlation coefficient varies from -1 to 1. A coefficient of zero
means there is no relationship between the two variables. The closer the 
coefficient is to -1 or 1, the stronger the relationshop. A value of -1 or 1 
would have all the points in a line. We can compute them all at once using
the `cor()` function.

```R
    > cor(state_data)
                    Population     Income  Illiteracy    Life.Exp     Murder     HS.Grad      Frost        Area
        Population  1.00000000  0.2082276  0.10762237 -0.06805195  0.3436428 -0.09848975 -0.3321525  0.02254384
        Income      0.20822756  1.0000000 -0.43707519  0.34025534 -0.2300776  0.61993232  0.2262822  0.36331544
        Illiteracy  0.10762237 -0.4370752  1.00000000 -0.58847793  0.7029752 -0.65718861 -0.6719470  0.07726113
        Life.Exp   -0.06805195  0.3402553 -0.58847793  1.00000000 -0.7808458  0.58221620  0.2620680 -0.10733194
        Murder      0.34364275 -0.2300776  0.70297520 -0.78084575  1.0000000 -0.48797102 -0.5388834  0.22839021
        HS.Grad    -0.09848975  0.6199323 -0.65718861  0.58221620 -0.4879710  1.00000000  0.3667797  0.33354187
        Frost      -0.33215245  0.2262822 -0.67194697  0.26206801 -0.5388834  0.36677970  1.0000000  0.05922910
        Area        0.02254384  0.3633154  0.07726113 -0.10733194  0.2283902  0.33354187  0.0592291  1.00000000
```

We can also plot a matrix. There are lots of ways to do this. Here is one, found
after a quick web search on "R correlation plot matrix". It is a good practice
to research what you want to do before you do it. Often most of the hard work
will be done for you. This method arranges and color codes the boxes by the 
strength of the correlation. The result is shown in Figure 1.

```R
   # install and load "gclus" first.
   
   # Use the help() function to learn details about these functions
    # Need to get absolute values of correlations for sorting 
    state_correlations <- abs(cor(state_data))
    
    # dmat.color creates nice color palettes
    state_colors <- dmat.color(state_correlations)
    ordered_correlations <- order.single(state_correlations)
    
    # From gclus creates a matrix of the pairs. Since the middle
    # row will all be ones and not very interesting, it uses the names
    cpairs(
      state_data,
      ordered_correlations,
      panel.colors = state_colors,
      gap = 0.5,
      main="Correlations Bewteen Population Variables"
    )
    dev.copy(png, "corr_matrix.png")
    dev.off()
```

<div class="row fig-array">
    <div class="col col-lg">
        <figure>
          <img src="{{ site.baseurl }}/assets/img/analysis_2/corr_matrix.png" alt="Correlation plot matrix of state data"/>
          <figcaption>Figure 1. A plot matrix showing the correlations between the variable in the state.x77 data. The plots are arranged with
                      the strongest correlations in the center and color coded so that the red are strongest and the yellow are the 
                      weakest correlations.</figcaption>
        </figure>
    </div>
</div>

Looking at our correlations we see murder rate is associated with a few things,
illiteracy, life expectancy, high school graduation rate and income. There 
are a lot of things we can do here. We'll get a bit more advanced but not too 
fancy. 

#### Regressions

Regressions appear to be like correlations but there is a subtle and very 
important difference. Correlations measure a relationship, but not a causal
relationship. So from our data, some things make sense as a causal relationship,
others don't. There is a relationship between murder and frost for instance,
but it is hard to imagine that murders cause frost to change, but the reverse
could be true. The same is true of illiteracy and murder and income and murder. 
We will treat murder as our *dependent variable*, the variable that depends on 
the other *independent variables*. Starting simply with one variable we'll
work up.

```R
    > reg_one <- lm(murder_rate ~ illiteracy, data = state_data)
    > summary(reg_one)
    
    Call:
    lm(formula = murder_rate ~ illiteracy, data = state_data)
    
    Residuals:
        Min      1Q  Median      3Q     Max 
    -5.5315 -2.0602 -0.2503  1.6916  6.9745 
    
    Coefficients:
                Estimate Std. Error t value Pr(>|t|)    
    (Intercept)   2.3968     0.8184   2.928   0.0052 ** 
    illiteracy    4.2575     0.6217   6.848 1.26e-08 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 2.653 on 48 degrees of freedom
    Multiple R-squared:  0.4942,	Adjusted R-squared:  0.4836 
    F-statistic: 46.89 on 1 and 48 DF,  p-value: 1.258e-08
```

This should look similar to our last analysis. The primary thing we are 
interested in is the illiteracy coefficient, specifically **Pr(>|t|)**. This is 
our *p value*. We see that it is less than 0.05 so we can accept the idea that the
murder rate is dependent on the rate of illiteracy among states. If it were 
greater than 0.05, we would conclude illiteracy has no effect. We do not typically
worry too much about the intercept, although here we can surmize that if 
everyone could read, there will still be a murder rate of 2.3938 murders per
100,000 people and that this estimate is statistically greater than zero.

We easily plot this as shown in Figure 2.

```R
    > plot(state_data$illiteracy, state_data$murder_rate, 
                        xlab="Illiteracy (1970, percent of population)", 
                        ylab="Murder Rate(1976, per 100,000)")
                        
      # Plots the line derived form our regression using the intercept and 
      # slope (y = mx + b).
    > abline(reg_one)
```

<div class="row fig-array">
    <div class="col col-lg">
        <figure>
          <img src="{{ site.baseurl }}/assets/img/analysis_2/murder_by_literacy.png" alt="Correlation plot matrix of state data"/>
          <figcaption>Figure 2. The relationship between statewide murder rates and state wide illiteracy is shown ( Regression, p < 0.05, df = (1, 48))</figcaption>
        </figure>
    </div>
</div>

Our final level of complexity is to add another variable, mean number of days
below freezing. This part isn't actually that hard.

Graphically we'll also use another package, `ggplot2`. This is
a widely used package so you should know about. Don't worry about understanding
everything at this point. It takes some practice and exposure. There are several
advantages to `ggplot2`. First, it takes a modular approach. You can add (and 
subtract) elements to your graphics using what ggplot calls aesthetics (`aes()`)
using a plus sign. This makes for cleaner more readable code. Also, it enforces
a common interface among all the functions in the package, something that is 
lacking in built in R graphical functions. It does take some getting used to 
though, and there is nothing inherently wrong with the built in packages. 

First lets regress murder rate and frost.

```R
    # First lets see what frost alone looks like.
    > reg_frost <- lm(murder_rate ~ frost, data = state_data)
    > summary(reg_frost)
    
    Call:
    lm(formula = murder_rate ~ frost, data = state_data)
    
    Residuals:
        Min      1Q  Median      3Q     Max 
    -5.8510 -2.6336 -0.2825  2.2983  7.3191 
    
    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 11.375689   1.005494  11.314 3.83e-15 ***
    frost       -0.038270   0.008635  -4.432 5.40e-05 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 3.142 on 48 degrees of freedom
    Multiple R-squared:  0.2904,	Adjusted R-squared:  0.2756 
    F-statistic: 19.64 on 1 and 48 DF,  p-value: 5.405e-05

```

We see a significant relationship! It would suggest that murder rate decreases
in colder climates. However, lets do a multiple regression
as shown below. The code and interpretation are fairly straight forward.

```R
    > multi_reg <- lm(murder_rate ~ illiteracy + frost, data = state_data)
    > summary(multi_reg)
    
        Call:
        lm(formula = murder_rate ~ illiteracy + frost, data = state_data)
        
        Residuals:
            Min      1Q  Median      3Q     Max 
        -5.2732 -1.7953 -0.2699  1.7013  7.3633 
        
        Coefficients:
                     Estimate Std. Error t value Pr(>|t|)    
        (Intercept)  3.873964   1.880853   2.060    0.045 *  
        illiteracy   3.763897   0.841564   4.473 4.88e-05 ***
        frost       -0.008613   0.009868  -0.873    0.387    
        ---
        Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
        
        Residual standard error: 2.659 on 47 degrees of freedom
        Multiple R-squared:  0.5022,	Adjusted R-squared:  0.4811 
        F-statistic: 23.71 on 2 and 47 DF,  p-value: 7.585e-08
```

Now we see that while illiteracy is still a significant predictor of murder rate,
days below freezing is not. The multiple regression is accounting for the relationship
between illiteracy and frost, and once that is removed, only illiteracy is significant.
It would appear that colder states are just more literate. We can leave it to you
to do that regression.

### Visualization with GGPlot2

Now we will use `ggplot2` to create a visualization for this analysis. Of course
there are multiple ways to display this data, so feel free and explore. We'll
take a step-by-step approach, that is not only a good workflow with ggplot2,
but also demonstrates one of its advantages.


<div class="row fig-array">
    <div class="col col-md">
        <figure>
          <img src="{{ site.baseurl }}/assets/img/analysis_2/ggdemo_1.png" alt="Plot with points added"/>
          <figcaption>Figure 3a. GGPlot2 showing illitracy vs murder rates with points added.</figcaption>
        </figure>
    </div>
    <div class="col col-md">
        <figure>
          <img src="{{ site.baseurl }}/assets/img/analysis_2/ggdemo_2.png" alt="Plot with the regression line added."/>
          <figcaption>Figure 3b. The regression line was added with geom_smooth().</figcaption>
        </figure>
    </div>
</div>
<div class="row fig-array">
    <div class="col col-md">
        <figure>
          <img src="{{ site.baseurl }}/assets/img/analysis_2/ggdemo_theme.png" alt="Use of a theme demonstrated on ggplot2"/>
          <figcaption>Figure 3c. A theme was applied to the plot.</figcaption>
        </figure>
    </div>
    <div class="col col-md">
        <figure>
          <img src="{{ site.baseurl }}/assets/img/analysis_2/ggdemo_color_size.png" alt="Size and color demonstrated."/>
          <figcaption>Figure 3d. Frost and income are given by changing the color 
                      and size of the points respectively. A title as added and 
                      sthe axis labels were also improved.</figcaption>
        </figure>
    </div>
</div>

```R
    # Make sure you install and load ggplot2
    
    > frost_by_illiteracy <- ggplot(state_data, aes(x=illiteracy, y=murder_rate))
    > frost_by_illiteracy
    
```

Notice you don't see anything but an empty graph. Ggplot2 requires each element
be add individually. This is actually a very good thing, it gives you tons
of control, and also makes it easier to build up very complicated visualizations.
Let's add our points and line next, take note of the changes with each line 
(Figure 3a, Figure 3b).

```R
    > frost_by_illiteracy <- frost_by_illiteracy + geom_point()
    > frost_by_illiteracy
    > frost_by_illiteracy <- frost_by_illiteracy + geom_smooth(method = lm, se = FALSE)
    # The se = FALSE turns off standard error lines for the plot. Turn it on and see what happenes.
    > frost_by_illiteracy
```

The geometries (*geoms* in R speak) are the standard way of adding elements to a plot. There 
are a lot of built in geometries you can find on the [GGPlot2 geoms page](https://ggplot2.tidyverse.org/reference/#section-layer-geoms).
Each geom can just be added to your existing plot, you need to save it to a 
variable though to keep the change.

The default plotting may not be to your taste. You can tweak the options
individually, or take the easy way out and use `ggthemes()`. As with the geoms
there are a number of [built-in themes](https://ggplot2.tidyverse.org/reference/#section-themes), 
and more you can find in packages with a web search (Figure 3c). 

```R
    > frost_by_illiteracy <- frost_by_illiteracy + theme_classic()
    > frost_by_illiteracy
```

We can incorporate more information by adding color and point size. Notice
the use of an aesthetic (`aes()`) to modify a geom. We'll also fix the 
labels.

```R
    > frost_by_illiteracy <- frost_by_illiteracy + 
                                geom_point(aes(color = frost, size = income)) +
                                labs(
                                   x = "Illiteracy\nPercent of Population", 
                                   y = "Murder Rate\nPer 100,000 People", 
                                   title = "Factors Affecting The Murder Rate in the USA"
                                   )
    > frost_by_illiteracy
```

And finally we can do this all in a neat, easy to read statement. The following
does the same thing as the lines above, plus we add a save (Figure 3d).

```R
    > frost_by_illiteracy <- ggplot(state_data, aes(x=illiteracy, y=murder_rate)) +
                             geom_point(aes(color = frost, size = income)) +
                             geom_smooth(method = lm, se = FALSE) + 
                             theme_classic() + 
                             labs(  x = "Illiteracy\nPercent of Population", 
                                    y = "Murder Rate\nPer 100,000 People", 
                                    title = "Factors Affecting The Murder Rate in the USA"
                                  )
    > frost_by_illiteracy
    > ggsave("fancy_plot.png", plot = frost_by_illiteracy)
         Saving 8.15 x 9.75 in image
```

    




   

        
        

    







