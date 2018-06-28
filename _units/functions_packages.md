---
layout: page
title: R Basics - Functions and Packages

include_site_title: FALSE

order: 4
    
supporting_files:
  - file: 'id1'
    href: 'https://github.com/psu-data-workshops/introduction_to_r/blob/master/scripts/data_types.R'
    name: Examples script for this unit.  
---

### Functions

While R has some object oriented aspects, most of what you will do revolves 
around functions. So far we have been using functions in our examples without
really explaining what we are doing. Before we write a function, lets first
look at how they are used.

All functions have a name. In R, functions differ from variables in that they
are always followed by parentheses.

```R
    function_name()
```

A function will typicall have an input and and output. The inputs goes in
the parentheses and are called arguments. Some arguments don't have names, others do.
Unnamed arguments are entered first and are often required. If there is more
than one, the order determines what they are. Named arguments are often, but
not always, optional. They go after the unnamed arguments are can go in 
any order. 

Before we use a function, we need to learn how to use it. We'll use the 
function `runif()` that is standard to R. First lets get the help page

```R
    help(runif)
```

You will see the documentation page on the lower right panel. Most R functions 
follow this pattern for documetation. You get a description of what the function
does, How to use it, details on the arguments, more detail about the function
the value(s) it returns and examples. 

We see that there are a family of functions. The function `runif()` requires
one argument, and the determines how many numbers to generate. We also see 
we can specify a minimum and maximum in the options. So lets try it out!



```R
   # Generates one random number from 0 to 1. The input is 1
    > runif(1)
    [1] 0.2060029
    
    # Generate a vector of 3 numbers
    > runif(3)
    [1] 0.7542035 0.4055190 0.1036249
    
    # Specify a lower value, notice 0 is assumed to be the max
    > runif(10, min=-3)
     [1] -0.2819697  0.5594857 -1.5450629  0.9111235 -1.5341340 -1.2352929  0.8539003 -2.6672495 -0.1213483 -2.2647624
     
     # 0 is assumed to be the minimum
    > runif(10, max=3)
     [1] 0.3910408 0.6122325 2.0391485 1.4172306 0.5622353 2.1464744 1.0864376 1.2396556 1.8573487 1.8418561
     
     # Specifying both
    > runif(10, min=-3, max=3)
     [1]  0.4700406 -2.3025641  1.9064524 -0.2096750  0.4171140  2.2916133  0.7480566 -2.0999288 -1.9003916  1.5339751
     
     # What happens when we supply bad input
    > runif(10, min=3, max=-3)
     [1] NaN NaN NaN NaN NaN NaN NaN NaN NaN NaN
   
```

You can also write your own functions. This can be really useful for collecting
repetitive code in one place, or just making things more organized. In R you
store your functions in variables as in the example below.

```R
    # Not very interesting, but at least its friendly by default!
    my_multiply <- function(x, y, say_hi = TRUE) {
      return(x * y)
    }
    
    > my_multiply(3, 4)
    [1] "Howdy!"
    [1] 12
    > my_multiply(-3, 4, say_hi = FALSE)
    [1] -12
```


### Packages

A package is a collection of functions bundled together to allow easier
sharing and reuse. To use a package you need to install it, if it hasn't been
already, then load it. 

To install it, click the install icon in 
the **_Packages_** tab on the lower left of your RStudio window. Enter **r2d2**
in the [Packages] input box. Leave the defaults and make sure []Install dependencies
is checked. Click install. If it asks you to install other things choose Yes.

Now find it in your list of installed packages and check the box to load it.
You can click on the link and find out more about the package too.

For projects where I have lots of dependencies, I use a couple auto loading 
functions. This ensures I always get the packages installed and loaded even
if I have to clean my environment or switch computers. Also, when I share 
my script, it automatically loads everything for them too.

```R
    ###################
    ## Automate package install and load
    
    # Feel free and copy and paste this, or grab it from the supplementary files.
    
    # Checks to see if the packages has already installed
    is_installed <- function(package_name) is.element(package_name, installed.packages()[,1])
    
    # If a package is not installed, install it. Then load the package.
    install_and_load <- function(package_name) {
      if(!is_installed(package_name)) {
        install.packages(package_name)
      }
      library(package_name, character.only = TRUE)
    }
    
    # Takes a vector of packages and installs and loads them if needed.
    install_packages <- function(packages) {
      for(package in packages) {
        install_and_load(package)
      }
    }
    
    # Calls the function, substitute your own packages.
    install_packages(c("rvest", "TMDb", "countrycode"))
```

The sheer number of packages is one of the main benefits to using R. Usually 
when I am starting on a project, I will search the internet for packages or 
code snippets that do what I need, or at least come close. The less code you
have to write, the faster you will be and also the fewer errors you will have 
to deal with. If you ever find yourself in the position of writing a lot of 
related functions, consider giving back to the community and publishing them 
as a package yourself!








