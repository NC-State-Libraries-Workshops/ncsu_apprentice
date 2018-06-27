---
layout: page
title: R Basics - Variables And Data Types

include_site_title: FALSE

order: 3

links:
  back:
    href: getting_started
    text: Getting Started
    
  next: 
    href: data_types
    text: R Basics - Data Types

  root:
    href: 'https://github.com/psu-data-workshops/start_here'
    text: Workshop List
    
supporting_files:
  - file: 'id1'
    href: 'https://github.com/psu-data-workshops/introduction_to_r/blob/master/scripts/variables.R'
    name: Examples script for this unit.

    
---


### Variables

#### Usage

Variables in R work like variables in any other programming language you may 
have used. In R you can store **ANYTHING** in a variable. If you don't store
something in a variable, it will be gone, into the air, and you can never
use it it again. We have already used a variable once, but lets start again.
In your **_Console_** type the fullowing

```r
  > var_one <- 42
  > print(var_one)
```

A few things to note. First, R likes to use the arrow `<-` to assign variables.
You can actually use an equals sign `=` as well, but the R convention has 
been to use the arrow.

Also note that the 42 isn't displayed until you use the `print()` function. 
Assigning a value to a variable prevents it's immediate display. Fianlly,
the variable should be in your **_Environment_**, and the commands should be in your
**_History_**. Now try the following. 

```r
  > var_two <- 3
  > var_one * var_two
```

In this case, the result of the multiplication is printed to the **_Console_** 
because it wasn't assigned to a variable. Also, its not in the **_Environment_**.
It is lost now.

#### Naming Rules

As with any other programming language there are rules about naming.
There are also various naming conventions to consider. While you must follow
the naming rules for R to function properly, naming conventions are important as
well. When you name consistently and use a standard convention, it makes it
easier for others to understand and reuse your work.

If you type `?make.names()` into your **_Console_**  you will see a good 
explanation there, the most important part excerpted below.

> A syntactically valid name consists of letters, numbers and the dot or 
> underline characters and starts with a letter or the dot not followed by a 
> number. Names such as ".2way" are not valid, and neither are the reserved words.

The following are some working and non-working examples of variable names. 
Type them into your **_Console_** and see what happens.

```r
  > good_name <- "foo"      # snake case
  > good.name <- 37         # dot case
  > goodName                # lower camel case
  > GoodName                # upper camel case
  > _good_name              # leading underscore
  > good_4_u                # using some number
  
  > 4_u_bad_name <- 0       # can't start with a number
  > _bad_name <- 1          # doesn't like to start with underscores either
  > bad-name <- 2           # R thinks it is a minus sign
  > .bad.name <- 3          # Don't lead with a dot
  > bad_name                # Looks like a good name, but will throw an error unless you assign a value to it.
  
```
  
In reality, you can even break these rules, but don't! See the discussion 
about naming conventions below.

As noted in the quotes text above you can't use reserved words. Reserved words,
also a part of every programming language, are words that the language itself
uses. In R they are...

> if else repeat while function for in next break

> TRUE FALSE NULL Inf NaN NA NA_integer_ NA_real_ NA_complex_ NA_character_

Finally, you can use names that were already used. This can lead to bad things
because you may not even know you are renaming a variable! Good naming 
conventinos (see below) help but don't entirely remove this problem.

**NOTE: ** The pounds signs or hash tags are comments in R. R ignores them. 
Use comments, but judciously, to document and explain your code. You can 
start a comment anywhere on a line, but everything after it will be ignored.

#### Naming Conventions

The rules given above still leave a nearly infinite space to name your variables.
Over time, programmers and coders of various kinds and stripes have converged 
on conventions that help them write more readable code. Readable code helps
you understand what you have done, even years later. Helps you work with 
collaborators more effeciently, and helps you share your work more openly as well.
Well crafted names greatly reduce the time and effort you need to spend writing
documentation as well.

R has a few communities of practice here (Bååth 2012) and an established 
[guide on CRAN](https://cran.r-project.org/doc/manuals/R-ints.html#R-coding-standards). 
This tutorial focuses on one that works well, and also looks a lot like 
conventions in other programming languages. 

* Use whole words
  * Single letters and abbreviations lead to confusion
  * Words should describe what is being named
* Use snake_case for variables and functions
  * Dot case works, but other languages use the dot for other purposes
  * Its easy to readable
  * Is fairly standard across languages
* Use CamelCase for package names
  * Easy to read. 
  * Capitalization emphasizes the scale
  * Fairly standard across languages
* Use snake_case for file names
  * URLS may ignore case
  * Hyphens are often used too and are ok

### References and Related Information

Bååth, R. (2012). The State of Naming Conventions in R. _The R Journal 4(2)_. <https://journal.r-project.org/archive/2012-2/RJournal_2012-2_Baaaath.pdf>


R coding standards. <https://cran.r-project.org/doc/manuals/R-ints.html#R-coding-standards>







