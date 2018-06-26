---
layout: page
title: R Basics - Data Types

include_site_title: FALSE

links:
  back:
    href: variables
    text: R Basics - Variables
    
  next: 
    href: functions
    text: R Basics - Functions

  root:
    href: 'https://github.com/psu-data-workshops/start_here'
    text: Workshop List
    
---

R is a dynamically typed language. In some languages, like C++ or Java
you have to tell the program if the variable is intended to be an **integer**, 
(1), a **floating point value** (3.14), *string* etc. Languages like R 
infer the type for you. This is both good and bad. You don't have to worry 
about getting it wrong. However, sometimes it leads to weird problems, although
this is rare. 

Despite not having to tell R what the data type is, you still need to know
about data types, and you also need to know the type stored in a variable to
work with it. 

#### Scalars

Scalars are the most basic type. Essentially a fancy name for a number of 
some sort. R also converts from an integer to a floating point value as needed.

```R
  > a <- 1            # an integer
  > b <- 2.0          # a float
  > c <- 2            # another integer
  
  > print(a/b)        # Dividing integer by an integer
  [1] 0.5           # Returns a float
```

#### Vectors

Vectors are just what they sound like. A one dimensional array of the same data
type. There are lots of ways to create vectors. Below are some examples of 
creating and working with vectors. Vectors are very common, so we'll 
spend a little time on them.


```R
 # The c() function is very straight forward
 > vector_one <- c(0, 1, 1, 2)
 > print(vector_one)
 [1] 0 1 1 2
 
 > vector_two <- c(3, 5, 8)
 > print(vector_two)
 [1] 3 5 8
 
 # Combining vectors
 > vector_three <- c(vector)
 > print(vector_three)
 [1] 0 1 1 2 3 5 8
 
 
 # More vectors
 > vector_char <- c('one', 'of', 'these', 'days')
 > print(vector_char)
 [1] "one"   "of"    "these" "days" 
 > vector_string <- c('be', 'careful', 'with', 'that', 'axe', 'eugene')
 > print(vector_string)
 [1] "be"      "careful" "with"    "that"    "axe"     "eugene" 
 > vector_four <- c(vector_char, vector_string)
 > print(vector_four)
 [1] "one"     "of"      "these"   "days"    "be"      "careful" "with"    "that"    "axe"     "eugene" 
 
  # You cant mix types, weird things can happen.
  > bad_vector <- c(vector_one, vector_string)
 
 # Numbers become strings
 > print(bad_vector)
 [1] "0"       "1"       "1"       "2"       "be"      "careful" "with"    "that"    "axe"     "eugene" 
```

Creating a vector one element at the time is tedious. Often you will
use a series of values shown below.

```R
 # Creating a series with step one
 > series_one <- c(1:20)
 > print(series_one)
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
 
 # Creating series with different step sizes
 > sequence_half_step <- seq(1,10, 0.5)
 > print(sequence_half_step)
 [1]  1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0  6.5  7.0  7.5  8.0  8.5  9.0  9.5 10.0
 
 > sequence_two_step <- seq(1,10, 2)
 > print(sequence_two_step)
 [1] 1 3 5 7 9
 
```

Vectors are really useful because many of R's functions work directly on
the vector. Here are some examples. Don't worry too much about the 
details of the functions.

```R
 
 # Sum the numbers
 > sum(vector_three)
 [1] 20
 
 > mean(vector_three)
 [1] 2.857143
 
 
 > paste(vector_four, collapse=", ")
 [1] "one, of, these, days, be, careful, with, that, axe, eugene"
 

```

Members of a vector can be accessed using the `[index]` index notation. If you have
worked with vector like data types in other languages, you may be used to 
accessing the first item using the 0th index. R uses 1 instead.

```R
  > vector_string[1]
  [1] "be"
  
  > vector_string[3]
  [1] "with"

```

You can get multiple indexes by supplying a vector as the index.

```R
  > vector_string[c(1,3,5)]
  [1] "be"   "with" "axe" 
```


#### Matrixes

Matrices are are kind of like two dimensional vectors. Like vectors, all
of the members must be of the same type. The work mostly like vectors
so we'll just touch on it briefly here.

Creating a matrix. By default matrixes are filled from the top left, working
down the column then right to the next column. That can be changed as shown.
Also, if the vector is shorter than the matrix has elements, it just starts
over from the beginning of the matrix.

```R
  > matrix_1 <- matrix(1:20, nrow=5,ncol=4)
  > print(matrix_1)
        [,1] [,2] [,3] [,4] 
    [1,]    1    6   11   16
    [2,]    2    7   12   17
    [3,]    3    8   13   18
    [4,]    4    9   14   19
    [5,]    5   10   15   20
    
    # By rows in instead
  > matrix_2 <- matrix(1:20, nrow=5, ncol=4, byrow = TRUE)
  > print(matrix_2)
         [,1] [,2] [,3] [,4]
    [1,]    1    2    3    4
    [2,]    5    6    7    8
    [3,]    9   10   11   12
    [4,]   13   14   15   16
    [5,]   17   18   19   20
    
  # You get a warning, but this still works.
  > matrix_3 <- matrix(1:7, nrow=5, ncol=4)
  Warning message:
  In matrix(1:7, nrow = 5, ncol = 4) :
    data length [7] is not a sub-multiple or multiple of the number of rows [5]
  > print(matrix_3)
       [,1] [,2] [,3] [,4]
  [1,]    1    6    4    2
  [2,]    2    7    5    3
  [3,]    3    1    6    4
  [4,]    4    2    7    5
  [5,]    5    3    1    6

```

Accessing parts of a matrix is very similar to a vector.

```R
  # Getting one member
  > matrix_1[1,3]
  [1] 11
  
  # Getting a column
  > matrix_1[,3]
  [1] 11 12 13 14 15
  
  # Getting a row
  > matrix_1[2,]
  [1]  2  7 12 17
  
  # Getting a sub matrix. This is also a matrix.
  > matrix_1[2:4,1:3]
       [,1] [,2] [,3]
  [1,]    2    7   12
  [2,]    3    8   13
  [3,]    4    9   14
  
```

#### Arrays

#### Lists

#### DataFrames

#### Factors

### Functions
