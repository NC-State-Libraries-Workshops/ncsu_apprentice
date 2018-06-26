---
layout: page
title: An Overview of R

include_site_title: FALSE

links:
  next:
    href: getting_started
    text: Getting Started With R
  root:
    href: 'https://github.com/psu-data-workshops/start_here'
    text: Workshop List

---

### A Brief History of R

R is derived from the S programming language, that was created by John Chambers 
at Bell Labs in 1976. The R project was initiated in 1992 and was officially 
released as a [GNU licensed](https://www.gnu.org) 
open source project in 1997 and available in the
[CRAN repository](https://cran.r-project.org/) with 12 packages.

R has increased steadily in popularity and functionality. As of 2016 R 
has become one of the most commonly used software tools in the researc literature
and is also a highly sought after skill among employers ([Muenchen 2012](https://r4stats.com/articles/popularity/)).

<img src="/assets/img/r_publications.png" class="two_col"/><img src="/assets/img/r_jobs.png" class="two_col"/>


Along with, and perhaps in part driving its popularity is the number of packages
available with for R. Along with what comes in the default installations, there is a
dizzying array of packages for just about anything you would want. Also, because
R is open source and comes with a large open source community, it is possible to 
create other packages you need and could be useful to others ([Muenchen 2012](https://r4stats.com/articles/popularity/)).

<img src="/assets/img/r_package_growth.png" class="one_col center"/>



### What R is (and is not)

It is important to understand what R is, what it can do and what it doesn't do.

#### A Programming Language

First and foremost R is a statistical programming language. As a formal and
probably [Turing Complete](https://en.wikipedia.org/wiki/Turing_completeness) programming language
there is probably no programming problem it can't tackles. That being said,
as a programming language, it lacks some of the object oriented aspects and other 
features that standard programming languages today typically have. If your needs
lean more to developing full fledged web pages or applications, there are probably 
better solutions for you.

#### Comman Line Driven

R is commnad line driven. There is no Graphical User Interface (GUI) that some 
other statistical packages have. This might be daunting at first, but over time
its is probably faster, especially as your needs become more specialized. Also,
being command line focused, and scriptable means that it forces you to write
your steps down as you do them. This not only makes it less likely you will lose
your work, but it makes it much easier for you to share what you have done.

#### Open Source

R is open source and free to use. That means you don't have to buy software packages. Nor do 
do you have to buy them again when they are updated. This can save you money. Also,
it means work you have done in R is easily shared because others will not have to
also buy a software package to reuse or replicate your work. They can just get R 
too if they don't already have it.

#### Community Driven

R is supported by a large active community. While commericial products provide
dedicated support as one of their selling features (and a useful feature it is), 
there is considerable support online for R users. Core R functionality is very well
covered and a web search will usually get you exactly the answer you need. 
[StackOverflow](https://stackoverflow.com/), a very popular technical question 
and answer site, has its own R channels. That being said, some less popular 
packages may not enjoy the same support or documentation.

It also give you the opportunity to become part of the community. You can do this
by 

* Publishing your own work on the web
* Asking your own questions on sites such as stackoverflow.com
* Suggesting fixes and features to existing packages
* Implementing your own fixes and features to existing packages
* Writing your own packages


### What Is RStudio?

RStudio is an Integerated Development Environment (IDE) for R. Essentially,
what it does is wrap the functionality of R up into a unified window. It 
also integrates some additional functionality such as integrating version 
control systems such as Git or CVS. It also adds an file editor for creating 
scripts and other text files, a interface into the package management system,
and an interface into the objects in memory (this all will make more sense soon).

Most of this functionality can be accomplished via external applications.
For instance version control can be accomplished via the command line. Editing
of scripts can be done with any text editor. RStudio just brings them all into
one place. Some people like this a lot, some people prefer to use a pure
command line R. Most people probably mix and match to suit their tastes.



### References and Related Information

[CRAN R Package Repository](https://cran.r-project.org/)

[The GNU Software Foundation](https://www.gnu.org/)

Muenchen, R.A. (2012). The popularity of data science software. _r4data_.  <https://r4stats.com/articles/popularity/>




