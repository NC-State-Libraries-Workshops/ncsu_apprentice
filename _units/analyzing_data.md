---
layout: page
title: Analyzing Data

order: 8
---



In this unit we will do some basic analyses and visualizations on the iris 
data. In the next unit we will use another data set to get just a little
more advanced, including loading data from a CSV file.

Probably one of the first analyses that comes to mind is a to test for 
differences in flower morphology between the species. First lets just look
at one attribute, `sepal_length`.

```R
    > anova <- lm(iris_data$sepal_length ~ iris_data$species)
    > summary(anova)
    
    Call:
    lm(formula = iris_data$sepal_length ~ iris_data$species)
    
    Residuals:
        Min      1Q  Median      3Q     Max 
    -1.6880 -0.3285 -0.0060  0.3120  1.3120 
    
    Coefficients:
                                Estimate Std. Error t value Pr(>|t|)    
    (Intercept)                   5.0060     0.0728  68.762  < 2e-16 ***
    iris_data$speciesversicolor   0.9300     0.1030   9.033 8.77e-16 ***
    iris_data$speciesvirginica    1.5820     0.1030  15.366  < 2e-16 ***
    ---
    Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
    
    Residual standard error: 0.5148 on 147 degrees of freedom
    Multiple R-squared:  0.6187,	Adjusted R-squared:  0.6135 
    F-statistic: 119.3 on 2 and 147 DF,  p-value: < 2.2e-16
```

The results from the ANOVA can be daunting at first, and if you are unsure,
you should always consult a statistician or other knowledgeable person before
you publish an analysis. 

The first thing to look at is the *p-value*. This simple value, is a bit of 
a tricky concept and often misunderstood. To really understand it we'll use 
a coin toss as an example and we need to introduce the concepts of a 
*hypothesis* and a *null hypothesis*. In our coin example we could do an 
experiment and toss the coin 100 times. Our *null hypothesis* is what we expect
if the coin is true, which is to say that it will be 50/50. Our *hypothesis* 
is that the coin is loaded and lands on one side or the other more often. Of course
even with a true coin, it is unlikely to land exactly 50/50. The real question
is how big of a deviation can we accept before we reject our *null hypothesis* and
accept our *hypothesis*. The *p-value* is what we use to make this decision.
By convention, if the *p-value* is less than 0.05 we reject our *null hypothesis*
and accept our *hypothesis*. Or put more simply, in the case of the coin toss
experiment, we believe our coin is most likely loaded.

In our iris example. we see a very small value, so we accept the hypothesis that
the three species differ in sepal length. The coefficients give us some idea of
where the differences lie. Anything with more than one asterisk has a 
*p-value* less than 0.05, and we can accept that they differ. In this case,
they are all different.

The other values such as the R-squared, degrees of freedom, etc. are important
but really require an understanding of statistics that go beyond this tutorial.

This summary is informative, but its not really eye catching. A box plot
is a good way to visualize these difference, so we'll use that. Notice how
we display the results in the figure. We could also write that in our text.

```R
    > boxplot(sepal_length ~ species, 
                        data = iris_data, notch = TRUE, 
                        ylab="Sepal Length (cm)", xlab="Species", 
                        main="Differences In Sepal Length Among Iris Species")
```


<div class="row fig-array">
    <div class="col col-lg">
        <figure>
          <img src="{{ site.baseurl }}/assets/img/analyzing_data/sepal_length_by_species.png" alt="Boxplot of sepal length by species."/>
          <figcaption>Figure 1. Sepal length differs significantly among iris species (p < 0.05, n = 150).</figcaption>
        </figure>
    </div>
</div>

We can do another simple plot, and this time add some color. Remember in our
frequency plots, we saw an odd bimodal distribution in some characters. This
might be the result of some differences among species. We can visualize this 
using a scatter plot using a different color for each species. Saving the
plot is also shown. In R Studio you can save the plot using the GUI, but 
it is usually better to make everyting scripted so you don't have to worry
about remembering to save a new plot should you change something.

```R
    # Create the plot
    > plot(iris_data$sepal_length, iris_data$sepal_width, col=iris_data$species)
    # The legend is added, see help(legend) for an explanation of the options.
    > legend("topright", legend = levels(iris_data$species), 
                         col = 1:3, cex = 0.8, pch = 1)
                         
    # One way to save the plot.
    > dev.copy(png, 'sepal_by_species.png')
        quartz_off_screen 
                        4 
    # dev.copy actually changes where graphical output is sent to. To change it
    # back we need to do this.
    > dev.off()
        RStudioGD 
                2 
```


<div class="row fig-array">
    <div class="col col-lg">
        <figure>
          <img src="{{ site.baseurl }}/assets/img/analyzing_data/sepal_by_species.png" alt="Boxplot of sepal length by species."/>
          <figcaption>Figure 2. Sepal length and Sepal width shown colored by species. Setosa clusters differently from the other two species.</figcaption>
        </figure>
    </div>
</div>

Next we'll learn how to import and export data, do another analysis and look 
a little deeper into some visualizations.

        
        

    







