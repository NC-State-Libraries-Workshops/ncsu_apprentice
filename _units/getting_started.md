---
layout: page
title: Getting Started

include_site_title: FALSE

order: 0

---

### Installation

If you already have R and RStudio great! You can skip this. For the rest of us, 
fortunately installing R and RStudio is usually pretty straightforward, although
it will depend on your operating system. We'll just hit the main steps, but
you will need to go to the 
[R Installation and Administratin](https://cran.r-project.org/doc/manuals/r-release/R-admin.html#Obtaining-R)
for complete help.

There are two main steps to installing R. Downloading and Installing. 

1. Download the most recent version of R, make sure it is for the Operating
system you use. A list of mirror sites is found [here](https://CRAN.R-project.org/mirrors.html). 
It doesn't matter too much which one you choose, geographically closer ones 
will be faster and more reliable.

2. Install R. This will vary greatly depending on your operating system.
Just follow the instructions here

    * [Windows](https://cran.r-project.org/doc/manuals/r-release/R-admin.html#Installing-R-under-Windows)
    * [Mac OS](https://cran.r-project.org/doc/manuals/r-release/R-admin.html#Installing-R-under-macOS)
    * [Linux/Unix](https://cran.r-project.org/doc/manuals/r-release/R-admin.html#Installing-R-under-Unix_002dalikes)
    
    <br/>
3. Download the installer for RStudio Desktop for your correct operating system 
[here](https://www.rstudio.com/products/rstudio/download/#download). Make sure 
you use the open source (free version) and make sure it is the desktop version, 
unless you are sure you want to set up a server.

4. Run the installer, again this will vary depending on your operating system.


### A Whirlwind Tour

We will get to know RStudio more during the workshop/tutorial, but we'll 
touch on the main parts briefly here. If you start up RStudio, you should
see something like the screenshot below. Note: If you don't see a script 
panel thats normal, you will soon.

![Standard RStudio Panels](/assets/img/r_studio_panels.png "Standard RStudio Panels")


#### Console / Command Line

This is where you will typically enter your commands. The **_Console_** tab functions just
like a normal command line interface for R. There is also a **_Terminal_** tab
functions just like the terminal (Mac OS or *Nix) or command prompt (Windows).

Click on the **_Console_** tab and type `> 1 + 1` and return. You should see
it respond with the correct answer.

Click on the **_Terminal_** tab and type `$ ls` and return. You should see a 
list of the files and diretories in your current R project (results may vary).

#### Script Editor

If you don't already have an empty script, click on the **_New File_** icon on the top 
left of your RStudio window and choose **R script**. This is an R script, there are
many like it but this one is yours...

If you write `print(1 + 1)` in your script and then click on the **_Source_** 
button. This will run the script, the **print()** function outputs the result
to your console.

#### Storage

This group of tabs is called **Storage** as the mostly deals with content that is
either saved to your disk, or can be downloaded to your disk. We won't demo
them all now, but briefly

* **_Files:_** allows you to navigate and manage the files in your project.
* **_Plots:_** is where  your graphs and charts will appear when you create them.
* **_Packages_** allows you to manage the many R packages available to you.
* **_Help:_** displays help for functions and packages in R. 
* **_Viewer:_** displays local web content you create.

#### Memory

This is called **Memory** because it primarily deals with content that lives 
in your computer's memory or RAM. Technically speaking it goes away when you closer
RStudio or turn off your computer. However, RStudio seems to load some back into 
memory when you reload your project (pretty handy!).

* **_Environment:_** displays all the variables, functions and data currently
active in your memory. If you type `a <- 42` into your console, you will 
see the variable a and the value 42 displayed. The broom will clean your 
environment and let you start fresh.
* **_History:_** Everything you type in the console is stored here. If you choose
the last line `a <- 42` and click **_To Source_** it will copy that to your script...NOICE!!
The broom will clean your history. Make sure you don't lose anything!
* **_Connections:_** Allows you to connect to external databases and data stores.
* **_Git:_** This may not be on your installation, or may have a different name
depending on if you have set up versioning and what versioning system you use. 






