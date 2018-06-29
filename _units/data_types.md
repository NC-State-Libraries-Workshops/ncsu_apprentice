---
layout: page
title: R Basics - Data Types

include_site_title: FALSE

order: 3
    
supporting_files:
  - file: id1
    file_name: data_types.R
    link_text: Example script for this unit.
    
---

R is a dynamically typed language. In some languages, like C++ or Java
you have to tell the program if the variable is intended to be an **integer**, 
(1), a **floating point value** (3.14), **string** ("a string") etc. Languages like R 
infer the type for you. This is both good and bad. You don't have to worry 
about getting it wrong. However, sometimes it leads to weird problems, one of 
which we'll see below. Also, there is a slight reduction in performance. 
In practice, the weird problems are rare enough and the reduction is slight 
enough that you probably won't notice them.


Despite not having to tell R what the data type is, you still need to know
about data types. Different data types can be worked with in different ways,
have different uses and limitations. Core R has a fair number of data types,
a couple are unique to R. We won't cover them here, but there are even more
that have been developed and available as R packages.

### Scalars

Scalars are the most basic type. Essentially a fancy name for a number of 
some sort. R also converts from an integer to a floating point value as needed.

```R
    > a <- 1            # an integer
    > b <- 2.0          # a float
    > c <- 2            # another integer
    
    > print(a/b)        # Dividing integer by an integer
    [1] 0.5           # Returns a float
```

### Vectors

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


### Matrixes

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

### Arrays

Arrays work pretty much like matrixes, but they can be multidimensional. 

```
    # Array creation is pretty much like matrix creation.
    > array_one <- array(c(1:60), dim=c(4,3,5))
    > array_one
    , , 1
    
         [,1] [,2] [,3]
    [1,]    1    5    9
    [2,]    2    6   10
    [3,]    3    7   11
    [4,]    4    8   12
    
    , , 2
    
         [,1] [,2] [,3]
    [1,]   13   17   21
    [2,]   14   18   22
    [3,]   15   19   23
    [4,]   16   20   24
    
    # Print out continues...
    # ... its pretty long sometimes, one slice at a time.
    
    # This is a three dimensional array 4x3x5 so we can access it as follows
    > array_one[2,3,4]
    [1] 46
    
    > array_one[2,,]
         [,1] [,2] [,3] [,4] [,5]
    [1,]    2   14   26   38   50
    [2,]    6   18   30   42   54
    [3,]   10   22   34   46   58
    
    
    > array_one[2,,4]
    [1] 38 42 46
```

### Lists

A collection of things that are all of the same type is useful, but sometimes
you want to collect things of different types. For this, R gives us lists. 

```R
    # Creating a list, notice we have lots of types, even a vector. 
    # could be another list even.
    > my_list <- list("Random", "Citizen", 70, c("Stochastic", "Chance"))
    > my_list
    [[1]]
    [1] "Random"
    
    [[2]]
    [1] "Citizen"
    
    [[3]]
    [1] 70
    
    [[4]]
    [1] "Stochastic" "Chance"   
```

You can name the items in a list as well. This can greatly improve the 
transparency of your code (along with renaming the variable).

```R
    > person_data <- list(first_name="Random", last_name="Citizen", 
                          weight_kg="70", kids=c("Stochastic", "Chance"))
    > person_data
    $first_name
    [1] "Random"
    
    $last_name
    [1] "Citizen"
    
    $weight_kg
    [1] "70"
    
    $kids
    [1] "Stochastic" "Chance"    
```

Accessing parts of a list is a little different than vectors, matrixes or arrays.
We have to double square bracket it `[[]]`.

```R
    > person_data[[2]]
    [1] "Citizen"
    
    # The power of naming again...more readable
    > person_data[["weight_kg"]]
    [1] "70"
    
    # Even more readable using this notation.
    > person_data$first_name
    [1] "Random"
```

### Data Frames

Data frames are probably the most commonly used data type used in R. They
are essentially the "spreadsheet" of R, equivalent to datasets in other
statistical packages like SAS or SPSS. When you import a CSV or Excel file
it will most like be as a data frame. The "columns" of a data frame 
are essentially vectors, so a data frame can be thought of as a list of 
vectors. The only constraint is that all the vectors (columns) are the same 
length.

```R
    # creating a data frame
    > a <- c("Random", "General", "Person", "Robert", "Sideshow")
    > b <- c("Citizen", "Disarray", "Of Interest", "Terwilliger", "Bob")
    > c <- c(35, 20, 32, 55, 55)
    > d <- c(FALSE, TRUE, FALSE, TRUE, TRUE)
    > my_data <- data.frame(a,b,c,d)
    > my_data
             a           b  c     d
    1   Random     Citizen 35 FALSE
    2  General    Disarray 20  TRUE
    3   Person Of Interest 32 FALSE
    4   Robert Terwilliger 55  TRUE
    5 Sideshow         Bob 55  TRUE
    
    
    # Again naming is important. Notice the original vector names are used.
    > persons <- my_data
    > names(persons) <- c("first_name", "last_name", "age", "villain")
    > persons
      first_name   last_name age villain
    1     Random     Citizen  35   FALSE
    2    General    Disarray  20    TRUE
    3     Person Of Interest  32   FALSE
    4     Robert Terwilliger  55    TRUE
    5   Sideshow         Bob  55    TRUE
    
```

Accessing parts of the data frames can be accomlished in a variety of ways.

```R
    # Getting a column
    persons[1]
      first_name
    1     Random
    2    General
    3     Person
    4     Robert
    5   Sideshow
    
    # Getting a column a different way. More about levels in a bit.
    > persons[[1]]
    [1] Random   General  Person   Robert   Sideshow
    Levels: General Person Random Robert Sideshow
    
    # Getting a column a third way
    > persons$age
    [1] 35 20 32 55 55
   
    # Getting a row of data
    > persons[3,]
    first_name   last_name age villain
    3     Person Of Interest  32   FALSE
    
    # Getting a value
    > persons[3,3]
    [1] 32
    
    # Getting a value another way
    > persons$age[3]
    [1] 32
    
    # Getting a value the most readable way 
    > persons$age[which(persons$last_name == 'Terwilliger')]
   [1] 55

```

### Factors

Finally we have factors. When creating a dataframe R tends to assume strings
are factors, or categories and will create them for you. Likewise, R assumes
strings in vectors, matrixes and arrays are strings. These default behaviors are
useful until they are not. Fortunately you can control it.

```R
    # Creating a factor from a vector of strings.
    > gender <- c("male", "female", "male", "male", "female")
    > gender
    [1] "male"   "female" "male"   "male"   "female"
    
    > gender <- factor(gender)
    > gender
    [1] male   female male   male   female
    Levels: female male
    
    > summary(gender)
    female   male 
         2      3 
         
    # Names aren't useful factors so we can change that.
    
    # Conversts first names to character, not factor
    > persons$first_name <- as.character(persons$first_name)
    > persons$first_name
    [1] "Random"   "General"  "Person"   "Robert"   "Sideshow"
    
    # Last names are still factors.
    > persons$last_name
    [1] Citizen     Disarray    Of Interest Terwilliger Bob        
    Levels: Bob Citizen Disarray Of Interest Terwilliger


```




