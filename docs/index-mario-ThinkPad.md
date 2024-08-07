--- 
title: "Introduction to statistical data analysis in R (2024)"
author: "Mario Recker"
site: bookdown::bookdown_site
output:
    bookdown::gitbook:
        config:
            sharing: null
        css: 'style.css'
        includes:
            in_header: _toggle.html
        keep_md: TRUE
linkcolor: blue
documentclass: book
link-citations: yes
description: "Intro to Stats with R"
---

# About {-}




This workshop is intended to introduce the R/RStudio statistical programming environment and how to use it for efficient data handling, data visualisation and data analysis. It is aimed at individuals with little experience in R/Rstudio and basic statistics. For those who are interested in a general intro to R or a refresher, please have a look at the following site for a great introduction to R/RStudio [Introduction to R](https://exeter-data-analytics.github.io/IntroToR/index.html). Equally, much of the material on statistical data analysis are based on the [Statistical Modelling in R](https://exeter-data-analytics.github.io/StatModelling/) workshop. These workshops had been developed by [TJ McKinley](https://medicine.exeter.ac.uk/people/profile/index.php?web_id=TJ_McKinley) from the University of Exeter and JJ Valletta ($\dagger$).


## Workshop structure {-}

This workshop will loosely be structured into the following themes

1. Data handling and visualisation
    - importing data
    - plotting data with `ggplot`
    - data wrangling

2. Statistical analysis 
    - linear models
    - mixed effect models
    - generalised linear models
    - survivial analysis
    - latent class analysis


$~$

The workshop will consist of a mixture between (theoretical) background and hands-on practicals. Specific tasks, designed for you to test your new skills and understanding, are highlighted as

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
This task will be explained here </div></div>

The solution can be revealed by clicking 

<button id="displayTextunnamed-chunk-3" onclick="javascript:toggle('unnamed-chunk-3');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-3" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
A solution will appear here.</div></div></div>

However, please make sure you try before clicking on the `Solution` - this is the only way to make sure how fully understood the new concepts.


<!--chapter:end:index.Rmd-->


# General introduction to R/RStudio

R is an *object-orientated* programming language. This means that you create objects, and give them names. You can then do things to those objects: you can perform calculations, statistical tests, make tables or draw plots. Objects can be single numbers, characters, vectors of numbers, matrices, multi-dimensional arrays, lists containing different objects and so on.

Whilst R provides its own development environment, we will use a fantastic IDE (integrated desktop environment) provided by RStudio. This is free to download, provides some neat features, and crucially, looks the same on all operating systems!

The helpful folks at RStudio also produce a series of excellent [Cheat Sheets](https://www.rstudio.com/resources/cheatsheets/). Please note, these are updated semi-regularly as new packages are added or existing packages updated. Note also that these cheat sheets focus on the use of RStudio, and a small number of subset of packages that are developed by RStudio (e.g. `tidyverse`, `shiny` and `rmarkdown`). For example, a nice Cheat Sheet for RStudio itself can be found [here](https://www.rstudio.com/wp-content/uploads/2016/01/rstudio-IDE-cheatsheet.pdf).

$~$

## Setting up an R session
It is worthwhile getting into a workflow when using R. General guidelines I would suggest are:

 - Use a different folder for each new project / assignment. This helps to keep all data / script / output files in one self-contained place.
 - Set the Working Directory for R at the outset of each session to be the folder you’ve specified for the particular assignment you’re working on. This can be done in RStudio by going to *Session > Set Working Directory > Choose Directory*. This sets the default search path to this folder.
 - Always use **script files** to keep a record of your work, so that it can be reproduced at a later date. Put simply, R scripts are just text files that contain commands to run in R. 
 
## R packages

R has hundreds of add-on packages that provide functionality for a wide range of techniques. We will be using a number of packages that are not automatically installed when you first installed R, and a key part of becoming proficient with R is learning how to install and load packages.

To install an the `tidyverse` R package, for example, simply run
```
install.packages('tidyverse')
```

If it installs without any errors,  you can load the library using 
```
library(tidyverse) 
```

> **Note:** sometimes packages / libraries have *dependencies*, meaning that the require other libraries to be installed first before a package can be installed. This is usually communicated via error messages during the installation process.

$~$

## Variables, vectors and data frames in R

R makes use of symbolic variables, i.e. words or letters that can be used to represent or store other values or objects. We will use the assignment operator `<-` to ‘assign’ a value (or object) to a given word (or letter). Run the following commands to see how this works (don’t worry about the comments, these are for your understanding):


```r
## assign to x the value 5
x <- 5 

## print the value assigned to the 
## variable x to the screen
x 
```

```
## [1] 5
```



```r
## we can also assign text to a variable
y <- "Hello There" 

## print y
y
```

```
## [1] "Hello There"
```


```r
## we can re-assign variables
y <- sqrt(10)

## or assign a variable in terms 
## of other variables
ziggy <- x + y

## print variable "ziggy"
ziggy
```

```
## [1] 8.162278
```

You will notice that as we create each of these variables, they begin to appear in the environment pane in the top right-hand side of the RStudio window. This shows the current R workspace, which is a collection of objects that R stores in memory. We can remove objects from the workspace using the `rm()` function e.g.


```r
## remove the variables x and y
rm(x, y)
```

Notice that `x` and `y` have now disappeared from the workspace. The variable `ziggy` still contains the correct answer though (these are not relative objects, such as the macros assigned in a program like Excel).


```r
ziggy
```

```
## [1] 8.162278
```


Objects in R are not restricted to single values. Objects containing multiple values are commonly referred to as vectors, which are generally defined using the `c()` notation, e.g.


```r
# create a vector with 4 numbers
x <- c(2, 1, 3, 5)
x
```

```
## [1] 2 1 3 5
```

```r
# or a vector containing 4 strings
names <- c("Neil", "Ella", "John", "Grace")
names
```

```
## [1] "Neil"  "Ella"  "John"  "Grace"
```

One of the most important aspects about vectors is that we can directly access individual elements, or certain *slices* of a vector


```r
# get the second element of x
x[2]
```

```
## [1] 1
```


```r
# get the first 3 elements of names
names[1:3]
```

```
## [1] "Neil" "Ella" "John"
```


```r
# get last two elements of x
tail(x,2)
```

```
## [1] 3 5
```

> **Note:** vectors are not restricted to contain single data types, i.e. you can mix numbers with characters, strings, booleans etc.

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Being able to work with (vector or matrix) indices is crucial for effective data handling - please make sure that the notations are fully understood. The following exercises will help you practice:
    
    1. create a vector with 7 numbers and assign it to an object `myvec`
    2. add the 1st and 2nd elements of `myvec`
    3. multiply the 1st, 3rd and 5th element of `myvec`
    4. assing the first four elents of `myvec` to a new vector call `myvec_new`
    5. (advanced) using the above defined vectors `x` and `names`, assign a name with the corresponding age (matched by index, i.e. 1. name to the 1. number), such that a message "Neil is 2 years old" is printed out.   </div></div>

<button id="displayTextunnamed-chunk-14" onclick="javascript:toggle('unnamed-chunk-14');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-14" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
## 1.
myvec <- c(3.1, 2.7, 1, 99, 231, -176, 55)
```

```r
## 2.
myvec[1] + myvec[2]  
```

```
## [1] 5.8
```

```r
# equivalent to sum(myvec[1:2])
```

```r
## 3.
myvec[1] * myvec[3] * myvec[5] 
```

```
## [1] 716.1
```

```r
# equivalent to prod(myvec[1],myvec[3],myvec[5]) or prod(myvec[c(1,3,5)])
```

```r
## 4. 
myvec_new <- myvec[1:4]
# equivalent to myvec_new <- head(myvec,4)
```

```r
## 5. 
print(paste(names[3],"is",x[3],"years old"))
```

```
## [1] "John is 3 years old"
```

```r
## (5. Advanced)
for(i in 1:4){
    print(paste(names[i],"is",x[i],"years old"))
}
```

```
## [1] "Neil is 2 years old"
## [1] "Ella is 1 years old"
## [1] "John is 3 years old"
## [1] "Grace is 5 years old"
```
</div></div></div>

$~$

### Data frames

A data frame in R is a particular structure for storing datasets. You can think of them as lists of vectors or, more intuitively, similar to a spreadsheet in Excel. Although all vectors need to be of equal length, they can contain different types of data. Here is an example of a data frame


```r
df <- data.frame(ParticipantID = c('ID001', 'ID002', 'ID003', 'ID007', 'ID009'),
                 Age = c(12, 8, 9, 7, 11),
                 Episode = c('y', 'n', 'n', 'y', 'y'))
```


|ParticipantID | Age | Episode |
|:-------------|:---:|:-------:|
|ID001         | 12  |    y    |
|ID002         |  8  |    n    |
|ID003         |  9  |    n    |
|ID007         |  7  |    y    |
|ID009         | 11  |    y    |

Accessing individual columns of a data frame can be done by name and using the `$` operator, e.g.


```r
df$Age
```

```
## [1] 12  8  9  7 11
```

```r
# equivalent to
# df['Age']
```

whereas indexing works in a similar fashion as for vectors


```r
# get the ID of the second participant
df$ParticipantID[2]
```

```
## [1] "ID002"
```

```r
# equivalent to 
# df[2,'ParticipantID']
```

**Note:** using the double indexing follows the general `[row, column]` notation.

Adding or making changes to an existing columns is equally straightforward


```r
# changing the data type of the 'Episode' column to a factor
df$Episode <- factor(df$Episode, labels = c('no', 'yes'))

# adding a new column
df['Temperature'] <- c(39.1, 37.0, 35.3, 38.8, 37.9)

# equivalent to 
# df$Temperature <- c(39.1, 37.0, 35.3, 38.8, 37.9)

# display the first 3 rows of df
head(df, n = 3)
```

```
##   ParticipantID Age Episode Temperature
## 1         ID001  12     yes        39.1
## 2         ID002   8      no        37.0
## 3         ID003   9      no        35.3
```



<div class="panel panel-default"><div class="panel-heading"> Question </div><div class="panel-body"> 
We just changed the data type of the column `Episode` to a factor. What is a factor in R and what kind of data would we use it for? </div></div>

<button id="displayTextunnamed-chunk-21" onclick="javascript:toggle('unnamed-chunk-21');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-21" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
A factor is a data structure used for fields that takes only predefined, finite number of values. Factors are typically used for categorical data.</div></div></div>

$~$

## Functions in R

R has a many predefined and commonly used in-built functions, such as `mean()` or`sd()` to calculate the mean and standard deviation of of a vector: 


```r
# define a vector with numbers from 1 to 10
x <- 1:10

# note: this is short-hand for
# x <- seq(1, 10, by = 10)

# calculate the mean and sd of x
mu <- mean(x)
sigma <- sd(x)

# let's have a look
print(paste0("The mean (sd) of x is ",mu," (",round(sigma,3),")"))
```

```
## [1] "The mean (sd) of x is 5.5 (3.028)"
```


<div class="panel panel-default"><div class="panel-heading"> Question </div><div class="panel-body"> 
What do the functions `print()`, `paste0()` and `round()` do? </div></div>

<button id="displayTextunnamed-chunk-24" onclick="javascript:toggle('unnamed-chunk-24');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-24" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
  - `print(x)` prints out the *value* of a variable `x`, which could be numeric or, as in this case, a *string*
  - `paste0()` creates strings and allows you to combine text and variables
  - `round(x, y)` rounds up a number (here stored in `x`) to `y` significant digits 

If you are not sure what a particular function does, simply ask R for help, for example by using `?round()`, or *google it*</div></div></div>

$~$

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
The inbuilt function `seq(from, to, by = )` creates a sequence of numbers starting from `from` up to `to` in steps of `by`, whereas `seq(from, to, length.out = )` will create a sequence of `length.out` numbers that are evenly spaced between `from` and `to`.

Use this function to create the following sequences:
    
  1. 2, 4, 6, …, 30.
  2. A sequence of 14 numbers starting at -2.5 and ending at 15.34.
  3. A sequence of 7 numbers starting at 0, increasing in increments of 0.04.
  4. A sequence starting at 101, ending at -20, in decrements of 11. </div></div>

<button id="displayTextunnamed-chunk-26" onclick="javascript:toggle('unnamed-chunk-26');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-26" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

1. sequence 2, 4, 6, ... 30

```r
seq(2, 30, by = 2)
```

```
##  [1]  2  4  6  8 10 12 14 16 18 20 22 24 26 28 30
```

2. A sequence of 14 numbers starting at -2.5 and ending at 15.34.

```r
myseq <- seq(-2.5, 15.34, length.out=14)
```

3. A sequence of 7 numbers starting at 0, increasing in increments of 0.04.
  

```r
myseq <- seq(0, by = 0.04, length.out = 7)
```

4. A sequence starting at 101, ending at -20, in decrements of 11.

```r
myseq <- seq(101, -20, by =-11)
```
</div></div></div>


$~$

### Useful inbuilt functions

Here is a list of common, inbuilt functions that you will probably come across when working with data.


|Function     |Description                                                                                                                           |
|:------------|:-------------------------------------------------------------------------------------------------------------------------------------|
|`length(x)`  |returns the length of vector x (i.e. the number of elements in `x`)                                                                   |
|`names(x)`   |get or set names of x (i.e. we can give names to the individual elements of `x` as well as just having them numbered)                 |
|`min(x)`     |returns the smallest value in `x`                                                                                                     |
|`max(x)`     |returns the largest value in `x`                                                                                                      |
|`median(x)`  |returns the median of `x`                                                                                                             |
|`range(x)`   |returns a vector with the smallest and largest values in `x`                                                                          |
|`sum(x)`     |returns the sum of values in `x`                                                                                                      |
|`mean(x)`    |returns the mean of values in `x`                                                                                                     |
|`sd(x)`      |returns the standard deviation of `x`                                                                                                 |
|`var(x)`     |returns the variance of `x`                                                                                                           |
|`diff(x)`    |returns a vector with all of the differences between subsequent values of `x`. This vector is of length 1 less than the length of `x` |
|`summary(x)` |returns different types of summary output depending on the type of variable stored in `x`                                             |

### Custom functions

There will be instances when you need a specific function for a particular job which, unfortunately, is not readily provided. In this case you can write your own function and then use them in a similar fashion as inbuilt functions or those that come part of a package.

There general way to define your own functions is 

```
my_function <- function(...) {
    # list of statements 
    # return an object (optional) 
    return(...)
}
```

For example, the following function simply prints out a "Hello, world"


```r
hello <- function() {
    print("Hello, world")
}

hello()
```

```
## [1] "Hello, world"
```

And here is a more useful function to calculate the area of a circle with radius `r`


```r
circle <- function(r) {
    # calculate the area
    A <- pi * r^2
    
    # return the value of A 
    return(A)
}

radius <- 1
print(paste0("the area of a circle with radius r = ",radius," is A = ",round(circle(radius),5)))
```

```
## [1] "the area of a circle with radius r = 1 is A = 3.14159"
```


Important, the number of *arguments* that a function is not limited to one, and not all of them need to be provided if default values are defined. Here is an example of a function with three input arguments, with a default value set for the last one. 


```r
# define your function to compare means
compareMeans <- function(x, y, dostats = FALSE){
    
    # compare the means of vectors x and y
    mux <- mean(x)
    muy <- mean(y)
    if(mux > muy){
        print("the mean of x is greater than the mean of y")
    }else if(muy > mux){
        print("the mean of y is greater than the mean of x")
    }else{
        print("x and y have the same mean")
    }
    
    # run t-test if required
    if(dostats == TRUE){
        print("Here is the result of a two-sided t-test")
        t.test(x,y)
    }
}

# define two vectors, x and y
x <- c(1, 2, 3, 4, 5, 3, 1, 4, 5, 2)
y <- c(4, 1, 3, 5, 6, 2, 7, 3, 4, 5)

# call function, specify only first two arguments
compareMeans(x,y)
```

```
## [1] "the mean of y is greater than the mean of x"
```



```r
# call function, this time as to perform a t-test 
compareMeans(x,y,TRUE)
```

```
## [1] "the mean of y is greater than the mean of x"
## [1] "Here is the result of a two-sided t-test"
```

```
## 
## 	Welch Two Sample t-test
## 
## data:  x and y
## t = -1.3416, df = 17.308, p-value = 0.1971
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  -2.5704367  0.5704367
## sample estimates:
## mean of x mean of y 
##         3         4
```


<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Write a function that calculates the 95% confident intervals for the sample mean of a vector $y$, $\mu$, which are given as
$$
\begin{align}
    \mu &= \frac{\sum y_i}{n} \\
    CI &= \mu \pm 1.96 \sigma / \sqrt(n)
\end{align}
$$
     </div></div>

<button id="displayTextunnamed-chunk-33" onclick="javascript:toggle('unnamed-chunk-33');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-33" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
myseq <- seq(2, -2, by = 0.1)</div></div></div>

$~$


## Basic plotting in R

R provides basic functionalities for most of your plotting needs. There are three types of graphs commonly used for visualising data: scatter / line plots, barplots, boxplots. Rather than going into a detailed explanation of each of them work, here are a couple of examples, which you should try to run, interpret and modify to understand their notation and general use. 

### Scatter plot


```r
# define two vectors x and y
x <- runif(40, min = 2, max = 5)  # draw 40 samples from a uniform distribution U(2,5)
y <- x + rnorm(40, mean = x, sd = 1) # add Gaussian noise

# plot y against x
plot(x, y)
```

<img src="_main_files/figure-html/unnamed-chunk-34-1.png" style="display: block; margin: auto;" />


```r
# change plotting symbol, size and colour, add axes labels and increase axes limits
plot(x, y, 
     pch = 19, # solid circle, also try 15, 17, 20, ...
     cex = 2,  # size scaling factor
     col = 'red',  
     xlab = 'X values', 
     ylab = 'Y values',
     xlim = c(1, 6),
     ylim = c(0,11))
```

<img src="_main_files/figure-html/unnamed-chunk-35-1.png" style="display: block; margin: auto;" />

### Line graph


```r
# change plotting symbol, size and colour, add axes labels and increase axes limits
a <- 1:20
b <- a + rnorm(20, a, 2.5)

plot(a, b, 
     type = 'l', # change to line graph
     lwd = 2.5,  # line width
     lty = 'dotted',
     col = 'blue',
     xlab = 'X values',
     ylab = 'Y values')
```

<img src="_main_files/figure-html/unnamed-chunk-36-1.png" style="display: block; margin: auto;" />

### Combined graph


```r
# crate scatter plot and add line graph
# note: these statement have to be run / executed together
plot(x, y, 
     pch = 19, 
     cex = 1,
     xlab = 'X values',
     ylab = 'Y values',
     xlim = c(1, 6),
     ylim = c(0,11))
lines(x = 2:5, y = seq(4,10,by=2), lwd = 2, col = 'red')
legend(x = 4, y = 2, legend = 'trend line', col = 'red', lwd = 1)
```

<img src="_main_files/figure-html/unnamed-chunk-37-1.png" style="display: block; margin: auto;" />

### Barplot

> **Note:** barplots should only be used to represent counts and not for comparing continuous data that can take on any values  


```r
# create some count data
Year = c('2002', '2010', '2019', '2020', '2023')
Cases = c(101, 204, 178, 252, 277)

barplot(Cases, names.arg = Year, col = '#1b98e0',
        xlab = 'Year of sampling',
        ylab = 'Number of cases')
```

<img src="_main_files/figure-html/unnamed-chunk-38-1.png" style="display: block; margin: auto;" />

Grouped, stacked barplots are also possible but we revisit those once we introduce `ggplot` as this provides a more intuitive way to create complex graphs.


### Boxplots

Boxplots are commonly used to show the distribution of (stratified) data. Together with the sample medium, they also show interquartile ranges and outliers. Here is a simple example.


```r
df <- data.frame(Temperature = c(35.6, 37.1, 38.0, 36.7, 36.5, 35.9, 39.7, 38.3, 36.6),
                 Episode = factor(c('no', 'no', 'yes', 'yes', 'no', 'no', 'yes', 'no', 'no')))

boxplot(Temperature ~ Episode, data = df, 
        col = c('cyan', 'orange'),
        xlab = 'Clinical episode',
        ylab = expression("Temperature ["*~degree*C*"]"))
```

<img src="_main_files/figure-html/unnamed-chunk-39-1.png" style="display: block; margin: auto;" />

<!--chapter:end:1-Introduction.Rmd-->

# Data wrangling and visualisation

## Introduction

In the second part of this workshop we are dealing with the handling and visualisation of (complex) data. It is expected that you should feel comfortable with basic R and, specifically, the use of data.frame objects. If not, then please ask one of the demonstrators. 

At this point we are also saying goodbye to much of R's basic (i.e. inbuilt) functionalities for plotting and manipulating data and introduce you to the *tidyverse*, which is a suite of packages for performing a (growing) number of data science tasks. Here, we will introduce key `tidyverse` packages, including `dplyr` and `ggplot2`, and show how they can be used to efficiently process and visualise complex data.

Although each package can be installed and loaded separately, they are designed to work together. An easier approach is to simply install and load the `tidyverse` directly.

To install tidyverse, use:


```r
install.packages("tidyverse")
```

and once installed, it can be loaded using:


```r
library(tidyverse)
```


$~$

## Loading and saving data

An essential part of data handling is the ability to store and read (externally stored) data. There are a myriad of different ways this can be done, here we briefly introduce two of them:

  - saving data as an R object with `saveRDS` to create an `Rds` files and loading it with `load`
  - saving data as a *comma separated version* (CSV) file and loading it with `read_csv` or `read.table`

> **Note:** `tidyverse` also provides functions to handle Microsoft Excel files. For example, `read_excel()` lets you import xls or xlsx based data files. However, due to Excel often causing havoc with data (mostly due to it changing data types), we are urging caution when handling Excel files. 


The main difference between the two approaches is that an `Rds` file stores data in a (R specific) binary format, meaning that you need R to read it. CSV files, in comparison, are (human readable) text files that can be opened by a number of different programs. In fact, on most operating systems, these are opened by MS Excel or a text editor by default. Which approach should you use? This often depends on whether you are the only one working with the data or whether you like the added benefit of viewing (or manipulating) data outside the R environment.


### Save / load data as an R object

As a first step we need to create some data that we wish to store for future use. And as before, we are dealing almost exclusively with data.frames. Recall the simply data.frame we generated in the first session


```r
df <- data.frame(ParticipantID = c('ID001', 'ID002', 'ID003', 'ID007', 'ID009'),
                 Age = c(12, 8, 9, 7, 11),
                 Episode = c('y', 'n', 'n', 'y', 'y'))
```

To save this data as an R object, simply call


```r
saveRDS(df, file = 'myData.Rds')
```

> **Note:** the file will be saved in your current working directory. If you want to save it in a different folder you need to provide the full file path, e.g. `saveRDS(df, file = '.../StatsWithR//Data/myData.Rds')`.

Loading the data is equally simple:


```r
# first we remove the df object to make sure everything works
rm(df)

# load the data
readRDS('myData.Rds')
```

```
##   ParticipantID Age Episode
## 1         ID001  12       y
## 2         ID002   8       n
## 3         ID003   9       n
## 4         ID007   7       y
## 5         ID009  11       y
```

At first sight this looks like it has worked. However, you might also have noticed that there is no newly created object in your global environment. This means, although R successfully loaded the data, it was not assigned to an object and essentially lost (this is one of the key differences between `save`/`load` and `saveRDS`/`readRDS`). We therefore need to assign the read in data to an object


```r
# read data and assign to an object / data.frame called myData
myData <- readRDS('myData.Rds')

# see if it works
head(myData)
```

```
##   ParticipantID Age Episode
## 1         ID001  12       y
## 2         ID002   8       n
## 3         ID003   9       n
## 4         ID007   7       y
## 5         ID009  11       y
```

### Save / load as a CSV file

One of the advantages of saving data as an Rds file is that it is more space efficient. By default, `saveRDS` compresses the data, which can significantly shrink the size of the stored data. On the downside, it can also take a bit longer to load the data subsequently. The more preferred data format, however, is a CSV file.

There are two equivalent function pairs for saving / loading CSV files: `write.table()`/`read.table()` and `read_csv()`/`write_csv()` (the latter is essentially a wrapper for the former). Here we show you how to use the first function pair, but please familiarise yourself with the other one as well.

First we save our data.frame `myData` as a comma separated file


```r
# save data in CSV format
write.table(myData,  # data object
            file = 'myData.csv',  # file name
            sep = ',', # character used to separate columns
            row.names = F) # don't save row names as additional column
```

Check if this worked by importing the CSV file


```r
# first remove the object form our environment
rm(myData)

# read in data
df <- read.table('myData.csv',  # file name to be read
                 header = TRUE, # treat first row as header / column names
                 sep = ',')

# print out first three rows
head(df, n = 3)
```

```
##   ParticipantID Age Episode
## 1         ID001  12       y
## 2         ID002   8       n
## 3         ID003   9       n
```

>**Note:** here we used a comma (',') to separate individual data columns. Other commonly used characters are semi-colon (';') and tab ('\t'). If the separation is not explicitly provided via `sep = ...`, `read.table` will guess it - this is dangerous and often leads to errors. We therefore recommend to always state which character should be used - *explicit is better than implicit*!

### Handling Excel files

Although we strongly discourage the use of Excel for data handling, it is still one of the most common methods for storing data. We therefore briefly show you one method of how to read Excel files using the `readxl` package, which needs to be loaded explicitly, because it is not one of the core tidyverse packages that are loaded via `library(tidyverse)` 



```r
# load library
library(readxl)

# read in excel data file
irisDF <- read_excel('iris.xls')

# print first few rows
head(irisDF, n = 5)
```

```
## # A tibble: 5 × 5
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
##          <dbl>       <dbl>        <dbl>       <dbl> <chr>  
## 1          5.1         3.5          1.4         0.2 setosa 
## 2          4.9         3            1.4         0.2 setosa 
## 3          4.7         3.2          1.3         0.2 setosa 
## 4          4.6         3.1          1.5         0.2 setosa 
## 5          5           3.6          1.4         0.2 setosa
```

### Cheatsheet

For more information of how to import and export data have a look at this [cheat sheet](https://rstudio.github.io/cheatsheets/html/data-import.html), which also provides an overview of all essential functions and their usage as a PDF for download. 

$~$

## Visualisation using `ggplot`

We start with a motivating example to show, how using base R graphics can easily become cumbersome. For this we use the `iris` dataset, which we have imported in the previous section. This dataset contains the measurements of the sepal length, sepal width, petal length and petal width for 50 samples from each of three species of iris flowers (setosa, versicolor and virginica). 

Let's say we are interested in the relationship between the length and the width of the petals. The first port of call is therefore to plot one against the other. 


```r
plot(x = irisDF$Petal.Width, y = irisDF$Petal.Length)
```

<img src="_main_files/figure-html/unnamed-chunk-49-1.png" style="display: block; margin: auto;" />

We can see that there is a clear relationship between those two variables. One other thing we might notice is that there are (at least) two clusters, and we might further have the suspicion that this could be due to the fact that we different species of iris. One way of checking this is to colour the points in by species. Here we do this in a slightly convoluted way but it serves the purpose of highlighting how quickly things can become complicated in base R.

The first thing we want to do is to subset the data. Say, for example, we are interested in the relationship between petal length and width in *Iris setosa*. In other words, we want to only plot the data for which `Species=='setosa'`.


```r
plot(x = irisDF$Petal.Width[irisDF$Species=='setosa'], 
     y = irisDF$Petal.Length[irisDF$Species=='setosa'],
     col = 'blue', pch = 20)
```

<img src="_main_files/figure-html/unnamed-chunk-50-1.png" style="display: block; margin: auto;" />

We can now add point for samples from *Iris versicolor* in a similar fashion.


```r
plot(x = irisDF$Petal.Width[irisDF$Species=='setosa'], 
     y = irisDF$Petal.Length[irisDF$Species=='setosa'],
     col = 'blue', pch = 20)
points(x = irisDF$Petal.Width[irisDF$Species=='versicolor'], 
       y = irisDF$Petal.Length[irisDF$Species=='versicolor'],
       col = 'red', pch = 20)
```

<img src="_main_files/figure-html/unnamed-chunk-51-1.png" style="display: block; margin: auto;" />

What has happened?? The problem is that the axes limits are automatically set through the first `plot` call and not updated for any additional points added to the graph. We therefore need to manually set the limits to guarantee that all points are visible.


```r
plot(x = irisDF$Petal.Width[irisDF$Species=='setosa'], 
     y = irisDF$Petal.Length[irisDF$Species=='setosa'],
     col = 'blue', pch = 20,
     xlim = c(0, 2.5),
     ylim = c(1,7),
     xlab = 'Petal width',
     ylab = 'Petal length')
points(x = irisDF$Petal.Width[irisDF$Species=='versicolor'], 
       y = irisDF$Petal.Length[irisDF$Species=='versicolor'],
       col = 'red', pch = 20)
points(x = irisDF$Petal.Width[irisDF$Species=='virginica'], 
       y = irisDF$Petal.Length[irisDF$Species=='virginica'],
       col = 'darkgreen', pch = 20)
```

<img src="_main_files/figure-html/unnamed-chunk-52-1.png" style="display: block; margin: auto;" />


The only thing missing now is a legend to note which colour belongs to what species.


```r
plot(x = irisDF$Petal.Width[irisDF$Species=='setosa'], 
     y = irisDF$Petal.Length[irisDF$Species=='setosa'],
     col = 'blue', pch = 20,
     xlim = c(0, 2.5),
     ylim = c(1,7),
     xlab = 'Petal width',
     ylab = 'Petal length')
points(x = irisDF$Petal.Width[irisDF$Species=='versicolor'], 
       y = irisDF$Petal.Length[irisDF$Species=='versicolor'],
       col = 'red', pch = 20)
points(x = irisDF$Petal.Width[irisDF$Species=='virginica'], 
       y = irisDF$Petal.Length[irisDF$Species=='virginica'],
       col = 'darkgreen', pch = 20)
legend(x = 0, y = 7, 
       legend = c('setosa', 'versicolor', 'virginica'),
       pch = 20,
       col =  c('blue', 'red', 'darkgreen'))
```

<img src="_main_files/figure-html/unnamed-chunk-53-1.png" style="display: block; margin: auto;" />

Now we can see that there are indeed three clusters and also get a hint that the relationship between petal length and petal width is dependent on species. In the next part of this workshop we will show you how to test this statistically. 

Although you can see that we can make highly customised graphs using base R graphics, the steps needed to create the above graph were far from straight forward. So let's try to do the same using `ggplot2` instead


```r
ggplot(irisDF, aes(x = Petal.Width, y = Petal.Length, col = Species)) +
    geom_point()
```

<img src="_main_files/figure-html/unnamed-chunk-54-1.png" style="display: block; margin: auto;" />

So essentially with a lone-liner we can create a highly complex graph that required no manual subsetting of the data or manipulation of the plot. We did not have to specify the legend or its position, either; this is all being taken care of by the `ggplot2` package. 

Arguably, for most people `ggplot2` is not very intuitive to start with and it can take some time to get used to. However, once you have understood the basics, it becomes a very logical and powerful way to create complex and highly customised graphs.

The ethos of `ggplot2` is that plots can be broken down into different features, most notably:

  - **data**
  - **aesthetic mapping**
  - **geometric object**
  - faceting
  - scales
  - *statistical transformations*
  - *coordinate system*
  - *position adjustments*

The first three are the most most essential ingredients of a plot created with `ggplot2`. The next one (faceting) is a commonly used method when dealing with categorical data and for creating stratified graphs. The *scales* feature is useful for translating data values to visual properties and include, for example, log-transforms. The remaining features are only mentioned here but play no further part in this introductory workshop.

In order to explain some of these features is to break the above code apart and add features one-by-one. Let's start with setting up the plot


```r
ggplot(irisDF)
```

<img src="_main_files/figure-html/unnamed-chunk-55-1.png" style="display: block; margin: auto;" />

Although this creates an empty plot but you will not get an error message - because you have done nothing wrong, you just forgot to add crucial ingredients! 

>**Note:** In comparison to base R, `ggplot2` requires a data.frame (or tibble) object for plotting. As shown in the previous section, it is easy to manipulate most other data into an R data frame. We will revisit this at a later stage. 


### Aesthetics

The next key ingredient is how the data should be mapped onto the visual aesthetics of the plot. This was done through the `aes(x = Petal.Width, y = Petal.Length, col = Species)` argument to the `geom_point()` function (see next section). What we do here is x-coordinate to be `Petal.Width`, the y-coordinates to be `Petal.Length`, and the colour of the characters to be related to `Species`. In general, aesthetics include:

  - position
  - colour / color / col (border or line color)
  - fill (inside color)
  - shape
  - linetype
  - size.

Note that not all aesthetics arguments have to be provided. For example, leaving out the `col = ` argument generates the following graph


```r
ggplot(irisDF, aes(x = Petal.Width, y = Petal.Length)) +
    geom_point()
```

<img src="_main_files/figure-html/unnamed-chunk-56-1.png" style="display: block; margin: auto;" />


### Geoms

The next ingredient is the **geom**, which defines the type of plot we want. In the above example we used `geom_point()`, which produces a scatterplot. Here are the most common geoms:

  - `geom_point()`
  - `geom_jitter()`
  - `geom_line()`
  - `geom_bar()`
  - `geom_boxplot()`
  - `geom_violin()`
  - `geom_histogram()`
  - `geom_density()`

Let's try one of them: `geom_boxplot`. This creates a box-and-whisker plot, that we have already come across. Say for example we are interested in the distribution of sepal lengths but want to stratify this by species. 


```r
ggplot(irisDF, aes(x = Species, y = Sepal.Length, fill = Species)) +
    geom_boxplot()
```

<img src="_main_files/figure-html/unnamed-chunk-57-1.png" style="display: block; margin: auto;" />

Nice! Notice that we did not have to specify the actual x-positioning for the three species; instead, `ggplot2` recognised that `Species` was not a numerical variable and treated it internally as a categorical variable (even though we did not specify it as such).


As you will have noticed, `ggplot2` builds up plots by adding together components. Here we first set up "global" options for the plot using the `ggplot()` function, where we also specified the plot aesthetics, e.g. through `aes(x = Petal.Width, y = Petal.Length, col = Species)`. We then added (+) to this the type of plot we wanted, e.g. `geom_point()`. 
One of the advantages of `ggplot2` is that it allows us to layer geoms and thus let us built complex graphs in different ways. To demonstrate this, we are going to add the individual data points to the boxplot generated above using the `geom_jitter()` geom.


```r
ggplot(irisDF, aes(x = Species, y = Sepal.Length, fill = Species)) +
    geom_boxplot() +
    geom_jitter(width = 0.1, height = 0, size = 0.5)
```

<img src="_main_files/figure-html/unnamed-chunk-58-1.png" style="display: block; margin: auto;" />

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Three extra arguments were provided to `geom_jitter()`. By changing their respective values find out what they do? </div></div>

```(solution)
These arguments control the horizontal spread of the data (width), the vertical 'noise' added to each data point and the size of each point 
```

$~$

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Change the aesthetics setting such that the colour, and not the fill, are determined by `Species`. What do you observe? </div></div>

<button id="displayTextunnamed-chunk-61" onclick="javascript:toggle('unnamed-chunk-61');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-61" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```
ggplot(irisDF, aes(x = Species, y = Sepal.Length, col = Species)) +
    geom_boxplot() +
    geom_jitter(width = 0.1, height = 0, size = 0.5)
```

Specifying the colour aesthetics instead now changes the colour of each data point and the line colour of the boxplots.</div></div></div>

$~$

### Labels 

`ggplot2` generally does a good job decorating the plot with the right axes labels etc. However, this is still dependent on the variable (i.e. column) names, and sometimes we want to add a bit more information or change or even remove labels manually. This can easily done by *adding* labels in a similar way as adding geoms and other features.


```r
ggplot(irisDF, aes(x = Species, y = Sepal.Length, col = Species)) +
    geom_boxplot() +
    geom_jitter(width = 0.1, height = 0, size = 0.5) +
    labs(x = '',  # remove x label
         y = 'Sepal length',  # set y label
         col = 'Iris species', # set legend title)
         title = 'Distribution of sepal length by species') # set plot title
```

<img src="_main_files/figure-html/unnamed-chunk-62-1.png" style="display: block; margin: auto;" />

Note that providing a legend in this case is not strictly necessary, but `ggplot` adds a legend by default. If you want to remove the legend, you have various options. The two most intuitive ones are


```r
ggplot(irisDF, aes(x = Species, y = Sepal.Length, col = Species)) +
    geom_boxplot() +
    geom_jitter(width = 0.1, height = 0, size = 0.5) +
    labs(x = 'Iris species',
         y = 'Sepal length',
         title = 'Distribution of sepal length by species') +
    guides(col = "none")
```

<img src="_main_files/figure-html/unnamed-chunk-63-1.png" style="display: block; margin: auto;" />

or

```
ggplot(irisDF, aes(x = Species, y = Sepal.Length, col = Species)) +
    geom_boxplot() +
    geom_jitter(width = 0.1, height = 0, size = 0.5) +
    labs(x = 'Iris species',
         y = 'Sepal length',
         title = 'Distribution of sepal length by species') +
    theme(legend.position = "none")
```

As a quick aside, notice how we set the arguments in `geom_jitter()` not as an aesthetics but as a generic option that was applied to all the data. We can use this *mixing* of aesthetics and generic options to further customise our plot. For example, if we do not wish the individual data points to be coloured by species but simply plotted in black, we can set this as a generic argument


```r
ggplot(irisDF, aes(x = Species, y = Sepal.Length, col = Species)) +
    geom_boxplot() +
    geom_jitter(width = 0.1, height = 0, size = 0.5, col = 'black') +
    labs(x = 'Iris species',
         y = 'Sepal length',
         title = 'Distribution of sepal length by species') +
    theme(legend.position = "none")
```

<img src="_main_files/figure-html/unnamed-chunk-64-1.png" style="display: block; margin: auto;" />


<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Produce a density plot for `Sepal.Length` using `geom_density()`, which only requires an `x` aesthetics argument, and fill these in by species. Now add an alpha channel (by adding an argument `alpha = ...` to the `geom_density()` function), which controls the opacity of the fill colour, ranging from 0 (complete transparent) to 1 (complete opague). </div></div>

<button id="displayTextunnamed-chunk-66" onclick="javascript:toggle('unnamed-chunk-66');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-66" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
ggplot(irisDF, aes(x = Sepal.Length, fill = Species)) +
    geom_density(alpha=0.3) +
    labs(x = 'Sepal length',
         y = 'Density',
         fill = 'Iris species')
```

<img src="_main_files/figure-html/unnamed-chunk-341-1.png" style="display: block; margin: auto;" />
</div></div></div>

$~$


### Faceting

A very useful feature of `ggplot` is the ability to use faceting to display sub-plots according to some grouping variable. For example, let’s assume that we want to produce separate scatter plots of petal length vs. width for each of the three flower species. We can do this using faceting:


```r
ggplot(irisDF, aes(x = Petal.Width, y = Petal.Length)) +
    geom_point() +
    facet_wrap(~ Species)
```

<img src="_main_files/figure-html/unnamed-chunk-67-1.png" style="display: block; margin: auto;" />

> **Note:** there is also the `facet_grid()` option, which allows you to stratify your data by more than one (categorical) variable. 

As before, we can use the same aesthetics settings as before, which are then applied to each of the facets. 


```r
ggplot(irisDF, aes(x = Petal.Width, y = Petal.Length, col = Species)) +
    geom_point() +
    facet_wrap(~ Species) +
    labs(x = 'Petal width',
         y = 'Petal length',
         col = 'Iris species')
```

<img src="_main_files/figure-html/unnamed-chunk-68-1.png" style="display: block; margin: auto;" />

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
By default, `ggplot` will use the same x and y limits for each of the facets. This can be overwritten by explicitly setting the `scales = ` argument, which must set to one of "fixed" (default), "free_x", "free_y", or "free". Explore what happens when you change this argument.  </div></div>

<button id="displayTextunnamed-chunk-70" onclick="javascript:toggle('unnamed-chunk-70');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-70" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
Setting the `scales` argument is useful when the data are on very different scales and essentially allows you to *zoom in*. It is generally considered good practice *not* to use different scales, however, so always notify the reader in case you change this.</div></div></div>

$~$


<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Use the `geom_histogram()` function (geom) to produce a histogram plot of `Sepal.Width` and stratified (faceted) by `Species`. Explore what happens when you set extra arguments `bin = ...` (for the number of bins) *or* `binwidth = ...` (the width of each bin).   </div></div>

<button id="displayTextunnamed-chunk-72" onclick="javascript:toggle('unnamed-chunk-72');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-72" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
ggplot(irisDF, aes(x = Sepal.Width, fill = Species)) +
    geom_histogram(binwidth = 0.1) +
    facet_wrap(~ Species)
```

<img src="_main_files/figure-html/unnamed-chunk-353-1.png" style="display: block; margin: auto;" />
</div></div></div>

$~$

### Statistical transformation

A very useful feature of `ggplot2` is that it allows us to easily add *statistical transformations* on top of our data. Here we briefly introduce two (related) methods for adding trend lines to a scatterplot via `geom_smooth()`


```r
ggplot(irisDF, aes(x = Sepal.Length, y = Sepal.Width)) +
    geom_point() +
    stat_smooth()
```

```
## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'
```

<img src="_main_files/figure-html/unnamed-chunk-73-1.png" style="display: block; margin: auto;" />

By default, `geom_smooth()` adds a LOESS (*locally estimated scatterplot smoothing*) smoothed line together with a shaded area that highlights the confidence bounds (which can be turned off by setting `se = FALSE`.

If we are more interested in a linear trend line, we have to explicitly set the `method` to `lm`


```r
ggplot(irisDF, aes(x = Sepal.Length, y = Sepal.Width)) +
    geom_point() +
    stat_smooth(method = 'lm') 
```

```
## `geom_smooth()` using formula = 'y ~ x'
```

<img src="_main_files/figure-html/unnamed-chunk-74-1.png" style="display: block; margin: auto;" />

> **Note:** these trend lines can be added to our plot even if we do not need the scatterplot itself. That is, if, for some reason, you decide you do not want to show the actual data, you can run the above without `geom_point()` to only show the (linear) trend line.

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Produce a similar scatterplot as above but not stratified by `Species` (either faceted or simply coloured in a single graph). What do you observe? </div></div>

<button id="displayTextunnamed-chunk-76" onclick="javascript:toggle('unnamed-chunk-76');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-76" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
ggplot(irisDF, aes(x = Sepal.Length, y = Sepal.Width, col = Species)) +
    geom_point() +
    stat_smooth(method = 'lm')
```

```
## `geom_smooth()` using formula = 'y ~ x'
```

<img src="_main_files/figure-html/unnamed-chunk-361-1.png" style="display: block; margin: auto;" />

This is an example of [Simpson’s Paradox](https://en.wikipedia.org/wiki/Simpson%27s_paradox), where an apparent trend in the data disappears or even reverses (as in our case) when the trend is explored in subsets of the data. </div></div></div>


### Scales

Scales control the details of how data values are translated to visual properties and include features such as modifying axes limits and axis transformation. Here we only provide brief example but follow [this link](http://www.sthda.com/english/wiki/ggplot2-axis-scales-and-transformations) for a more in-depth tutorial. 

To manually set axes limits we can either directly specify which axis we want to modify (e.g. through `+ xlim(min, max)`) or go the more generic way such as


```r
ggplot(irisDF, aes(x = Sepal.Length, y = Sepal.Width)) +
    geom_point() +
    stat_smooth(method = 'lm') +
    lims(x = c(3.8, 8.3),
         y = c(1.5, 5))
```

```
## `geom_smooth()` using formula = 'y ~ x'
```

<img src="_main_files/figure-html/unnamed-chunk-77-1.png" style="display: block; margin: auto;" />

Much more control and customisation options over limits, axes labels, breaks (i.e. tick marks) etc are provided by the `scale_xx()` functions
```
scale_x_continuous(name, breaks, labels, limits, trans)
scale_y_continuous(name, breaks, labels, limits, trans)
```
For more information about these please have a look at the above mentioned tutorial or check R Help through the command `?scale_x_continuous`.

`ggplot2` offers various inbuilt functions to perform axis transformations, including:

  - `scale_x_log10()`, `scale_y_log10()` : for log10 transformation
  - `scale_x_sqrt()`, `scale_y_sqrt()` : for sqrt transformation
  - `scale_x_reverse()`, `scale_y_reverse()` : to reverse coordinates


Here is an easy example showing how these can be mixed in a single plot


```r
df <- data.frame(x = c(10, 100, 1000, 10000, 100000),
                 y = c(1, 4, 9, 16, 25))

ggplot(df, aes(x = x, y = y)) +
    geom_point() +
    scale_x_log10() +
    scale_y_sqrt() +
    stat_smooth(method = 'lm') 
```

```
## `geom_smooth()` using formula = 'y ~ x'
```

<img src="_main_files/figure-html/unnamed-chunk-78-1.png" style="display: block; margin: auto;" />


### Assigning plots to objects

So far we have used a separate code block for each plot. One thing to remember is that R is an object oriented language. This means that plots generated with `ggplot`, for example, can also be assigned as an object. This allows us to add extra layers / features to our plot without rewriting the entire code; here is an example. 


```r
p1 <- ggplot(df, aes(x = x, y = y)) +
    geom_point(size = 1.4, col = 'red')
p1
```

<img src="_main_files/figure-html/unnamed-chunk-79-1.png" style="display: block; margin: auto;" />
Next we add a line connecting the data points


```r
p2 <- p1 + geom_line(linewidth = 0.3, col = 'blue')
p2
```

<img src="_main_files/figure-html/unnamed-chunk-80-1.png" style="display: block; margin: auto;" />

and finally let's do some axis transformation


```r
p2 + scale_x_log10() + scale_y_sqrt()
```

<img src="_main_files/figure-html/unnamed-chunk-81-1.png" style="display: block; margin: auto;" />

### Putting it all together

As a final step we are going to show you how combining different aesthetics and features in `ggplot2` allows you to make very complex - but both informative and beautiful - graphs. For this we will use a different dataset (`LifeExpectancy.csv`), start with a simple plot of life expectancy against GDP and then add layers and modifications as we go along.


```r
# load data
LifeExpectancy <- read.table('LifeExpectancyData.csv', sep = ',', header = T)

# have a quick glimpse at the data
head(LifeExpectancy)
```

```
##       Country Continent Year     Status Life.expectancy Adult.Mortality
## 1 Afghanistan      Asia 2015 Developing            65.0             263
## 2 Afghanistan      Asia 2014 Developing            59.9             271
## 3 Afghanistan      Asia 2013 Developing            59.9             268
## 4 Afghanistan      Asia 2012 Developing            59.5             272
## 5 Afghanistan      Asia 2011 Developing            59.2             275
## 6 Afghanistan      Asia 2010 Developing            58.8             279
##   infant.deaths Alcohol percentage.expenditure Hepatitis.B Measles  BMI
## 1            62    0.01              71.279624          65    1154 19.1
## 2            64    0.01              73.523582          62     492 18.6
## 3            66    0.01              73.219243          64     430 18.1
## 4            69    0.01              78.184215          67    2787 17.6
## 5            71    0.01               7.097109          68    3013 17.2
## 6            74    0.01              79.679367          66    1989 16.7
##   under.five.deaths Polio Total.expenditure Diphtheria HIV.AIDS       GDP
## 1                83     6              8.16         65      0.1 584.25921
## 2                86    58              8.18         62      0.1 612.69651
## 3                89    62              8.13         64      0.1 631.74498
## 4                93    67              8.52         67      0.1 669.95900
## 5                97    68              7.87         68      0.1  63.53723
## 6               102    66              9.20         66      0.1 553.32894
##   Population thinness..1.19.years thinness.5.9.years
## 1   33736494                 17.2               17.3
## 2     327582                 17.5               17.5
## 3   31731688                 17.7               17.7
## 4    3696958                 17.9               18.0
## 5    2978599                 18.2               18.2
## 6    2883167                 18.4               18.4
##   Income.composition.of.resources Schooling
## 1                           0.479      10.1
## 2                           0.476      10.0
## 3                           0.470       9.9
## 4                           0.463       9.8
## 5                           0.454       9.5
## 6                           0.448       9.2
```

```r
# subset to only contain data from the year 2000
DF <- LifeExpectancy[LifeExpectancy$Year == 2000,]

# scatterplot of life expectancy against GDP
ggplot(DF, aes(x = GDP, y = Life.expectancy)) +
    geom_point() +
    ylab('Life expectancy (years)')
```

<img src="_main_files/figure-html/unnamed-chunk-82-1.png" style="display: block; margin: auto;" />
> Note: you might get a warning about rows being removed due to missing value. We will get on to this in the next section. For now you can just ignore this.

We can see a clear relationship between life expectancy and GDP. Next we want to see if there is a difference by status of a country (*developed* or *developing*)


```r
# scatterplot of life expectancy against GDP
ggplot(DF, aes(x = GDP, y = Life.expectancy, col = Status)) +
    geom_point() +
    ylab('Life expectancy (years)')
```

<img src="_main_files/figure-html/unnamed-chunk-83-1.png" style="display: block; margin: auto;" />
And again we see a clear patter whereby developed countries appear to have on average a higher life expectancy. Next we can add an additional aesthetics, or stratification, changing the size of each data point according to the respective country's population size.


```r
# scatterplot of life expectancy against GDP
ggplot(DF, aes(x = GDP, y = Life.expectancy, col = Status, size = Population)) +
    geom_point() +
    ylab('Life expectancy (years)')
```

<img src="_main_files/figure-html/unnamed-chunk-84-1.png" style="display: block; margin: auto;" />
Although there seems to be a relationship it is hard to see as most countries are squashed into the left-hand side of the graph. To the trained eye it also looks like the GDP data is not normally distributed (which in fact explains the clustering to the left) and we will therefore log-transform the x-axis


```r
# scatterplot of life expectancy against GDP
ggplot(DF, aes(x = GDP, y = Life.expectancy, col = Status, size = Population)) +
    geom_point() +
    scale_x_log10() +
    ylab('Life expectancy (years)')
```

<img src="_main_files/figure-html/unnamed-chunk-85-1.png" style="display: block; margin: auto;" />

Finally, we might be interested to see how life expectancy and its relationship with GDP and the size of the population has evolved over time and across the five continents. Let's say we want to compare the years 2000, 2005 and 2010. 


```r
# subset data to now contain information for 2000, 2005 and 2010
DF <- LifeExpectancy[LifeExpectancy$Year %in% c(2000, 2005, 2010),]

ggplot(DF, aes(x = GDP, y = Life.expectancy, col = Status, size = Population)) +
    geom_point() +
    facet_grid(Continent ~ Year) +
    scale_x_log10() +
    theme(legend.position = 'top')
```

<img src="_main_files/figure-html/unnamed-chunk-86-1.png" style="display: block; margin: auto;" />
NICE!


<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Explore the `LifeExpectancy` dataset using the different features that `ggplot` has to offer. Can you find any interesting relationships in the data? If so, take note and revist them when we are entering the statistics part of this workshop.  </div></div>


<!--chapter:end:2-Data_wrangling_pt1.Rmd-->

## Data wrangling

*Data wrangling*, or the process of cleaning and manipulating data for subsequent analysis, is a key component of modern statistical science and is becoming more important in the age of big (e.g. *high throughput*) data. The `tidyverse` incorporates a suite of packages, such as `tidyr` and `dplyr` that are designed to make common data wrangling tasks not only easier to achieve, but also easier to decipher. Readability of the code is at the core of the philosophy underpinning these packages.

> As always, there are plenty of resources to find useful information about the various data handling functions in the different `tidyverse` packages, including the [Data Import Cheat Sheet](https://github.com/rstudio/cheatsheets/raw/master/data-import.pdf) and [Data Transformation Cheat Sheet](https://github.com/rstudio/cheatsheets/raw/master/data-transformation.pdf).


If you haven't done so already, we first need to load the `tidyverse` library as well as the life expectancy dataset we introduced earlier.


```r
# load tidyverse
library(tidyverse)

# load dataset andassign to object LifeExp
LifeExp <- read.table('LifeExpectancyData.csv', sep = ',', header = T)
```


### Tidy data

The architect behind the tidyverse, Hadley Wickham, distinguishes between two types of data set: *tidy* and *messy*. Rather than being pejorative towards different ways in which people store and visualise data, the point here is to make a distinction between a specific way of arranging data that is useful to most R analyses, and anything else. In fact Hadley has a neat analogy to a famous Tolstoy quote:

> "Tidy datasets are all alike but every messy dataset is messy in its own way." — Hadley Wickham

In this context, a tidy data set is one in which:

  - rows contain different observations
  - columns contain different variables
  - cells contain values
  

Let's look at a simple example using the life expectancy data.


```r
head(LifeExp)
```

```
##       Country Continent Year     Status Life.expectancy Adult.Mortality
## 1 Afghanistan      Asia 2015 Developing            65.0             263
## 2 Afghanistan      Asia 2014 Developing            59.9             271
## 3 Afghanistan      Asia 2013 Developing            59.9             268
## 4 Afghanistan      Asia 2012 Developing            59.5             272
## 5 Afghanistan      Asia 2011 Developing            59.2             275
## 6 Afghanistan      Asia 2010 Developing            58.8             279
##   infant.deaths Alcohol percentage.expenditure Hepatitis.B Measles  BMI
## 1            62    0.01              71.279624          65    1154 19.1
## 2            64    0.01              73.523582          62     492 18.6
## 3            66    0.01              73.219243          64     430 18.1
## 4            69    0.01              78.184215          67    2787 17.6
## 5            71    0.01               7.097109          68    3013 17.2
## 6            74    0.01              79.679367          66    1989 16.7
##   under.five.deaths Polio Total.expenditure Diphtheria HIV.AIDS       GDP
## 1                83     6              8.16         65      0.1 584.25921
## 2                86    58              8.18         62      0.1 612.69651
## 3                89    62              8.13         64      0.1 631.74498
## 4                93    67              8.52         67      0.1 669.95900
## 5                97    68              7.87         68      0.1  63.53723
## 6               102    66              9.20         66      0.1 553.32894
##   Population thinness..1.19.years thinness.5.9.years
## 1   33736494                 17.2               17.3
## 2     327582                 17.5               17.5
## 3   31731688                 17.7               17.7
## 4    3696958                 17.9               18.0
## 5    2978599                 18.2               18.2
## 6    2883167                 18.4               18.4
##   Income.composition.of.resources Schooling
## 1                           0.479      10.1
## 2                           0.476      10.0
## 3                           0.470       9.9
## 4                           0.463       9.8
## 5                           0.454       9.5
## 6                           0.448       9.2
```

<div class="panel panel-default"><div class="panel-heading"> Question </div><div class="panel-body"> 
Is this data *tidy*? </div></div>

<button id="displayTextunnamed-chunk-91" onclick="javascript:toggle('unnamed-chunk-91');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-91" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
Yes, because each row corresponds to a single observation, each column corresponds to a single variable and each cell contains a value. </div></div></div>

$~$

In this workshop we will see various ways in which datasets can be manipulated to and from the *tidy* format.


### Filter rows

The first data manipulation we could do is to filter the data, as we have done earlier when plotting the data only for the year 2000. In base R this worked as


```r
LifeExp[LifeExp$Year == 2000,]
```

To do the equivalent in `tidyverse`, we use the `filter()` function


```r
filter(LifeExp, Year == 2000)
```

Note, one of the most distinctive / useful feature of `tidyverse` (or rather `migrittr`, which `tidyverse`/`dplyr` depends on) is the so-called piping operator, denoted as `%>%`. This operator allows you to *chain* one function after another without relying on nested parentheses or having to assign / store intermediate objects. So what it is doing is evaluating the expression on the right-hand side (or next line) of the `%>%` (pipe) using the expression on the left (or same line) as the first argument. If this sounds confusing then fear not - all will be made clearer once you see it in action! Using the same example as above we can get the same results with piping


```r
LifeExp %>% filter(Year == 2000)
```

Initially this might look more complicated but you will soon see how this is a very useful operator indeed.


### Sort rows

Another common operation is to sort rows according to some criterion. For example, we might wish to sort our data by `Status` and then `Life.expectancy`. In tidyverse this is done using the `arrange()` function.


```r
arrange(LifeExp, Status, Life.expectancy)
```

or using the piping operator


```r
LifeExp %>% arrange(Status, Life.expectancy)
```


### Select columns

The next common operation is the selection of columns, which also includes *de*selection of particular columns. Let's say we are interested only in the countries and their corresponding life expectancy, GDP, population size and the year of sampling. Before showing you how this can efficiently done in `tidyverse`, here are some options of how to achieve this in base R

```
## option 1
LifeExp[, match(c("Country", "Life.expectancy", "GDP", "Population"), colnames(LifeExp))]

## option 2
cbind(Country = LifeExp$Country, Life.expectancy = LifeExp$Life.expectancy, 
      GDP = LifeExp$GDP, Population = LifeExp$Population)

## option 3 (requires knowing which columns are which)
LifeExp[, c(1, 4, 16, 17)]
```

And here is how easy and hopefully by now intuitively this can be done using the `select()` function


```r
LifeExp %>% 
    select(Country, Continent, Life.expectancy, GDP, Population) %>% 
    head()
```

```
##       Country Continent Life.expectancy       GDP Population
## 1 Afghanistan      Asia            65.0 584.25921   33736494
## 2 Afghanistan      Asia            59.9 612.69651     327582
## 3 Afghanistan      Asia            59.9 631.74498   31731688
## 4 Afghanistan      Asia            59.5 669.95900    3696958
## 5 Afghanistan      Asia            59.2  63.53723    2978599
## 6 Afghanistan      Asia            58.8 553.32894    2883167
```

> **Note:** notice that we added one extra pipe at the end `%>% head()`. Remember that the `head()` function displays the first few rows of a data.frame. What we are doing here is that we first take the data.frame `LifeExp`, the apply the `filter()` function and then use the results of this as the argument in `head()` 

De-selection, or filtering out particular columns follows a similar structure but in this case the column to be removed is preceded by a '-'; for example


```r
LifeExp %>% 
    select(-Adult.Mortality) %>% 
    head()
```

As you will have noticed, we can easy combine various data manipulation functions using pipes without having to store any intermediate results or use excessive parenthesis. Let's try this out


```r
LifeExp %>% 
    filter(Year == 2000) %>%
    select(Country, Continent, Life.expectancy, GDP, Population) %>%
    arrange(Life.expectancy) %>%
    head(n = 10)
```

```
##                     Country Continent Life.expectancy       GDP Population
## 1              Sierra Leone    Africa            39.0 139.31477    4564297
## 2                    Malawi    Africa            43.1 153.25949   11376172
## 3                    Zambia    Africa            43.8 341.95562    1531221
## 4                    Angola    Africa            45.3 555.29694    1644924
## 5                   Eritrea    Africa            45.3  28.19695     339281
## 6  Central African Republic    Africa            46.0 243.54293    3754986
## 7                  Zimbabwe    Africa            46.0 547.35888   12222251
## 8                    Uganda    Africa            46.6 257.63369    2439274
## 9                   Nigeria    Africa            47.1 379.11933    1223529
## 10                     Chad    Africa            47.6 166.23179    8342559
```

Powerful stuff!


### Grouping and summarising

A common thing we might want to do is to produce summaries of some variable for different subsets of the data. For example, we might want to produce an estimate of the mean life expectancy for for each year. The `dplyr` package provides a function `group_by()`, which allows us to group data by one or more variables, and the `summarise()`, which allows us to summarise data. These can be used in combination get stratified summaries as shown here


```r
LifeExp %>% 
    group_by(Year) %>%
    summarise(mn = mean(Life.expectancy))
```

```
## # A tibble: 16 × 2
##     Year    mn
##    <int> <dbl>
##  1  2000  65.9
##  2  2001  66.2
##  3  2002  66.5
##  4  2003  66.5
##  5  2004  66.9
##  6  2005  67.5
##  7  2006  68.0
##  8  2007  68.5
##  9  2008  68.9
## 10  2009  69.3
## 11  2010  69.4
## 12  2011  70.1
## 13  2012  70.5
## 14  2013  70.9
## 15  2014  71.1
## 16  2015  71.2
```

The most commonly functions used for summarising data are

  - Center: `mean()`, `median()`
  - Spread: `sd()`, `IQR()`
  - Range: `min()`, `max()`,
  - Count: `n()`


<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Test your skills by

  1. calculating the mean life expectancy by continent
  2. calculating the mean life expectancy by continent and year
  3. calculating the mean and median of the GDP for each continent in the years 2000, 2005 and 2010

(note, for both the `mean()` and `median()` we have to add an extra argument `na.rm = TRUE` - what happens if we don't?) </div></div>

<button id="displayTextunnamed-chunk-102" onclick="javascript:toggle('unnamed-chunk-102');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-102" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

  1. calculating the mean life expectancy by continent

```r
LifeExp %>% 
    group_by(Continent, Year) %>%
    summarise(mn = mean(Life.expectancy))
```

```
## `summarise()` has grouped output by 'Continent'. You can override using the
## `.groups` argument.
```

```
## # A tibble: 80 × 3
## # Groups:   Continent [5]
##    Continent  Year    mn
##    <chr>     <int> <dbl>
##  1 Africa     2000  54.5
##  2 Africa     2001  55.0
##  3 Africa     2002  55.3
##  4 Africa     2003  55.0
##  5 Africa     2004  55.7
##  6 Africa     2005  57.0
##  7 Africa     2006  57.2
##  8 Africa     2007  57.9
##  9 Africa     2008  58.8
## 10 Africa     2009  59.6
## # ℹ 70 more rows
```

  2. calculating the mean life expectancy by continent and year

```r
LifeExp %>% 
    group_by(Continent) %>%
    summarise(mn = mean(Life.expectancy))
```

```
## # A tibble: 5 × 2
##   Continent    mn
##   <chr>     <dbl>
## 1 Africa     58.4
## 2 Americas   74.1
## 3 Asia       71.2
## 4 Europe     78.8
## 5 Oceania    81.6
```

  3. calculating the mean and median of the GDP for each continent in the years 2000, 2005 and 2010

```r
LifeExp %>% 
    filter(Year %in% c(2000, 2005, 2010)) %>%
    group_by(Year) %>%
    summarise(GDP_mn = mean(GDP, na.rm = T),
              GDP_md = median(GDP, na.rm = T))
```

```
## # A tibble: 3 × 3
##    Year GDP_mn GDP_md
##   <int>  <dbl>  <dbl>
## 1  2000  4847.   658.
## 2  2005  7562.  1286.
## 3  2010  8386.  1931.
```
</div></div></div>

$~$

### Reshaping datasets

Recall, a key philosophy of `tidyverse` is the notion of data being *tidy*. In fact, to get the most out of `ggplot`, datasets need to be in a specific format. More often than not, though, you will be dealing with *untidy* data. To give you an example, let's have a look at the data file `ExposureIndex.csv`, which contains the recorded malaria exposure index for 103 individuals in Junju, Kenya, between the years 2000 and 2010.


```r
EI <- read.csv('ExposureIndex.csv', check.names = F)  # the argument check.names=F prevents renaming of col names
head(EI)
```

```
##   Participant.ID      2000      2001         2002      2003         2004
## 1          N0004 0.7500000 0.5666667 4.705882e-01 0.4736842 1.578947e-01
## 2          N0007 0.9090909 0.6923077 3.333333e-01 0.1666667 9.770000e-15
## 3          N0016 0.7500000 0.8750000 3.750000e-01 0.6250000 1.000000e+00
## 4          N0024 0.7500000 0.5333333 5.294117e-01 0.4210526 1.052632e-01
## 5          N0041 0.5000000 0.3888889 8.690000e-13 0.3333333 6.400000e-13
## 6          N0055 0.7500000 0.5333333 5.294117e-01 0.4210526 1.578947e-01
##       2005     2006     2007 2008     2009     2010
## 1 0.00e+00 0.00e+00 8.70e-14    0 5.00e-02 1.00e-01
## 2 1.27e-14 9.77e-15 0.00e+00    0 0.00e+00 2.44e-14
## 3 5.00e-01 0.00e+00 2.00e-01    0 2.16e-14 3.60e-15
## 4 0.00e+00 0.00e+00 8.70e-14    0 5.00e-02 1.00e-01
## 5 1.56e-13 0.00e+00 4.25e-13    0 3.45e-13 5.74e-14
## 6 0.00e+00 0.00e+00 8.70e-14    0 5.00e-02 1.00e-01
```


<div class="panel panel-default"><div class="panel-heading"> Question </div><div class="panel-body"> 
Is this data in *tidy* format? And if not, why not? </div></div>

<button id="displayTextunnamed-chunk-105" onclick="javascript:toggle('unnamed-chunk-105');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-105" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
No, this data is not in *tidy’ format. We can see that each row corresponds to a different participant, but each column corresponds to a different year. For this to be *tidy*, we would need one column containing the participant, one column containing the year, and a third column containing the exposure index for participant in each year.</div></div></div>

$~$

Luckily, within `tidyverse` is it easy to *reshape* data to get it into the desired format. In this case we want to reshape it from a *wide format* into a *long format*. The necessary function to do this is called `gather()`, which takes two or more columns and gathers them into key-value pairs (here: year - exposure index). The columns to gather are `2000`, `2001`, ..., `2010`, which we can shorten to `2000:2010` (i.e. all columns from `2000` to `2010`)


```r
EI_long <- EI %>%
    gather(Year, ExposureIndex, '2000':'2010') 

head(EI_long, n = 10)
```

```
##    Participant.ID Year ExposureIndex
## 1           N0004 2000     0.7500000
## 2           N0007 2000     0.9090909
## 3           N0016 2000     0.7500000
## 4           N0024 2000     0.7500000
## 5           N0041 2000     0.5000000
## 6           N0055 2000     0.7500000
## 7           N0059 2000     0.7500000
## 8           N0067 2000     0.7500000
## 9           N0089 2000     0.4375000
## 10          N0096 2000     0.4375000
```

> **Note:** because the column names were numerical values and not strings, we have to encase them by ' '. This is not necessary if column names are in character format.


The converse of `gather()` is `spread()`, which takes two columns (`key` and `value`) and spreads them into multiple columns (dictated by the number of unique `values`). 


```r
EI_long %>%
    spread(Year, ExposureIndex) %>%
    head()
```

```
##   Participant.ID      2000      2001         2002      2003         2004
## 1          N0004 0.7500000 0.5666667 4.705882e-01 0.4736842 1.578947e-01
## 2          N0007 0.9090909 0.6923077 3.333333e-01 0.1666667 9.770000e-15
## 3          N0016 0.7500000 0.8750000 3.750000e-01 0.6250000 1.000000e+00
## 4          N0024 0.7500000 0.5333333 5.294117e-01 0.4210526 1.052632e-01
## 5          N0041 0.5000000 0.3888889 8.690000e-13 0.3333333 6.400000e-13
## 6          N0055 0.7500000 0.5333333 5.294117e-01 0.4210526 1.578947e-01
##       2005     2006     2007 2008     2009     2010
## 1 0.00e+00 0.00e+00 8.70e-14    0 5.00e-02 1.00e-01
## 2 1.27e-14 9.77e-15 0.00e+00    0 0.00e+00 2.44e-14
## 3 5.00e-01 0.00e+00 2.00e-01    0 2.16e-14 3.60e-15
## 4 0.00e+00 0.00e+00 8.70e-14    0 5.00e-02 1.00e-01
## 5 1.56e-13 0.00e+00 4.25e-13    0 3.45e-13 5.74e-14
## 6 0.00e+00 0.00e+00 8.70e-14    0 5.00e-02 1.00e-01
```


### Mutate

Last but not least we show you how to create, modify or even delete columns with `mutate()`. In fact, `mutate()` is probably one of the functions you will end up using the most. However, the functionality of `mutate()` is introduced here by means of two examples, which also introduce a few other useful features.

In the first example we are going to create a new column in our data.frame `EI_long`, where we categorise the exposure index into *high* and *low* depending on its value being above or below 0.5, respectively. One new function we are going to introduce is `ifelse()`; please use the help for more details, although its use should become apparent.


```r
EI_long <- EI_long %>%
    mutate(EI_cat = ifelse(ExposureIndex >= 0.5, 'high', 'low'))

head(EI_long, n=10)
```

```
##    Participant.ID Year ExposureIndex EI_cat
## 1           N0004 2000     0.7500000   high
## 2           N0007 2000     0.9090909   high
## 3           N0016 2000     0.7500000   high
## 4           N0024 2000     0.7500000   high
## 5           N0041 2000     0.5000000   high
## 6           N0055 2000     0.7500000   high
## 7           N0059 2000     0.7500000   high
## 8           N0067 2000     0.7500000   high
## 9           N0089 2000     0.4375000    low
## 10          N0096 2000     0.4375000    low
```


In the second example we going to use `mutate()` to modify three existing columns. First, we are going to round the `ExposureIndex` to two significant digits; then we are turning our new column `EI_cat` into a categorical variable using the function `factor()`; and finally we are going to change the `Year` column into a numeric format 


```r
EI_long <- EI_long %>%
    mutate(ExposureIndex = round(ExposureIndex, digits=2)) %>%
    mutate(EI_cat = factor(EI_cat)) %>%
    mutate(Year = as.numeric(Year))

# note, we could have done the same in a single mutate() call
# EI_long <- EI_long %>%
#     mutate(ExposureIndex = round(ExposureIndex, digits=2),
#            EI_cat = factor(EI_cat),
#            Year = as.numeric(Year))

head(EI_long, n=10)
```

```
##    Participant.ID Year ExposureIndex EI_cat
## 1           N0004 2000          0.75   high
## 2           N0007 2000          0.91   high
## 3           N0016 2000          0.75   high
## 4           N0024 2000          0.75   high
## 5           N0041 2000          0.50   high
## 6           N0055 2000          0.75   high
## 7           N0059 2000          0.75   high
## 8           N0067 2000          0.75   high
## 9           N0089 2000          0.44    low
## 10          N0096 2000          0.44    low
```

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 

  1. produce a `ggplot` line graph of the mean exposure index against time (2000 to 2010)
  2. show the distribution of the expsoure index over time by means of box-and-whisker plots

<infobutton id="displayTextunnamed-chunk-411" onclick="javascript:toggle('unnamed-chunk-411');">Show: Hint</infobutton>

<div id="toggleTextunnamed-chunk-411" style="display: none"><div class="panel panel-default"><div class="panel-body">
Hint: the first task involves a combination of `group_by()` and `summarise()`, and for the second task you might need to mutate the `Year` column into a categorical variable. Also, you can do this by either creating a new data.frame for each task, or by using the pipe to send your modified data.frame straight to `ggplot`, in which case you do not need to specifiy the data in the `ggplot()` function.</div></div></div>
 </div></div>

<button id="displayTextunnamed-chunk-111" onclick="javascript:toggle('unnamed-chunk-111');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-111" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

  1. a line graph of the mean exposure index against time (2000 to 2010)

```r
EI_long %>%
    group_by(Year) %>%
    summarise(meanEI = mean(ExposureIndex)) %>%
    ggplot(aes(x = Year, y = meanEI)) +
    geom_line()
```

<img src="_main_files/figure-html/unnamed-chunk-416-1.png" style="display: block; margin: auto;" />

  2. distribution of the expsoure index over time by means of box-and-whisker plots

```r
EI_long %>%
    mutate(Year = factor(Year)) %>%
    ggplot(aes(x = Year, y = ExposureIndex)) +
    geom_boxplot()
```

<img src="_main_files/figure-html/unnamed-chunk-417-1.png" style="display: block; margin: auto;" />
</div></div></div>

$~$

### Dealing with missing data

One recurring problem with data analysis is that data are often incomplete, leading to more or less serious downstream data analysis problems. That is, different functions deal with missing data in different ways, some simply ignore them whereas others fail completely. We therefore need to expand our data wrangling toolbox.

Missing data in R are usually referred to `NA`'s, and here is an example of where NA's can become problematic


```r
x = c(1, 4, 2, 9, NA, 4, 5)
mean(x)
```

```
## [1] NA
```

There are various ways to deal with missing data, of which we only touch upon a few

#### **Detecting missing data** {-}

The first thing we might want to know if there are any NA's, and a function for this is `is.na()`, which works on single variables, vectors, matrices and data.frames


```r
df <- data.frame(x = c(1, 4, 2, 9, NA, 4, 5),
                 y = c(0.2, 0.5, NA, 0.1, NA, 0.8, 0.9))

is.na(df)
```

```
##          x     y
## [1,] FALSE FALSE
## [2,] FALSE FALSE
## [3,] FALSE  TRUE
## [4,] FALSE FALSE
## [5,]  TRUE  TRUE
## [6,] FALSE FALSE
## [7,] FALSE FALSE
```

#### **Removing NA's** {-}

Going back to our previous example, if we want to calculate the mean of `x` we can either manually remove the offending entries or tell `mean()` to ignore them 


```r
# option 1: tell mean() to ignore NA
mean(x, na.rm = TRUE)
```

```
## [1] 4.166667
```

```r
# option 2: remove NA manually
x <- x[!is.na(x)]  # this means that x should be assigned to all entries of x that are not (!) NA
mean(x)
```

```
## [1] 4.166667
```

What about our data.frame `df`? As `df` has both rows and columns we cannot simply use the same method but have to be more specific. For example, to remove a row where `df$x` contains missing data


```r
df[!is.na(df$x),]
```

```
##   x   y
## 1 1 0.2
## 2 4 0.5
## 3 2  NA
## 4 9 0.1
## 6 4 0.8
## 7 5 0.9
```

or to remove all rows where either `df$x` *or* `df$y` contains missing data (note: for this we need a logical operator, which is in fact an *and*, `&`, because we neither want NA's in `x` nor in `y` so both conditions have to be safisfied together)


```r
df[!is.na(df$x) & !is.na(df$y),]
```

```
##   x   y
## 1 1 0.2
## 2 4 0.5
## 4 9 0.1
## 6 4 0.8
## 7 5 0.9
```

An easier way to achieve the same is by using the `complete.cases()` function, which selects only those rows where we have complete information (i.e. no missing data) 


```r
df[complete.cases(df),]
```

```
##   x   y
## 1 1 0.2
## 2 4 0.5
## 4 9 0.1
## 6 4 0.8
## 7 5 0.9
```

And finally here the same examples but done using `tidy` functionality


```r
df %>%
    filter(!is.na(x) & !is.na(y))
```

```
##   x   y
## 1 1 0.2
## 2 4 0.5
## 3 9 0.1
## 4 4 0.8
## 5 5 0.9
```

which is equivalent to 


```r
df %>%
    drop_na()
```

```
##   x   y
## 1 1 0.2
## 2 4 0.5
## 3 9 0.1
## 4 4 0.8
## 5 5 0.9
```

which is equivalent to 


```r
df %>% 
  filter_at(vars(x:y), all_vars(!is.na(.)))
```

```
##   x   y
## 1 1 0.2
## 2 4 0.5
## 3 9 0.1
## 4 4 0.8
## 5 5 0.9
```

which is equivalent to


```r
df %>% 
  filter_at(vars(x:y), all_vars(complete.cases(.)))
```

```
##   x   y
## 1 1 0.2
## 2 4 0.5
## 3 9 0.1
## 4 4 0.8
## 5 5 0.9
```

As they say in English: *"there is more than one way to skin a cat"*.



<!--chapter:end:2-Data_wrangling_pt2.Rmd-->

# Introduction to statistical modelling in R

The focus of this part of the workshop is how to fit statistical models in R. We will not go into underlying mathematics but instead introduce key concepts in statistical data analysis and how to do this in R. The internet is full of free and useful tutorials and resources related to statistics and statistical modelling in R. If you prefer physical books instead of computer screens, here is a list of recommendations:

  - [Linear models with R](https://www.crcpress.com/Linear-Models-with-R/Faraway/p/book/9781439887332)
  - [Data Analysis Using Regression and Multilevel/Hierarchical Models](http://www.stat.columbia.edu/~gelman/arm/)
  - [An Introduction to Statistical Learning](http://www-bcf.usc.edu/~gareth/ISL/)
  - [Mixed Effects Models and Extensions in Ecology with R](https://www.springer.com/gb/book/9780387874579)
  - [Extending the Linear Model with R](https://www.amazon.co.uk/Extending-Linear-Model-Generalized-Nonparametric/dp/158488424X)

## What is a statistical model? {-}

Now that we are experts in handling and visualising data in R, we can enter the beautiful world of *statistical data analysis* or *statistical modelling*. But first we need to answer the simple question: **what is a statistical model**? Here is one definition:

> A statistical model is a mathematical model that embodies a set of statistical assumptions concerning the generation of sample data and similar data from a larger population. It represents, often in considerably idealized form, the data-generating process. (taken from Wikipedia)

and another one:

> Statistical modeling helps data scientists approach data analysis in a strategic manner, providing intuitive visualizations that aid in identifying relationships between variables and making predictions. (taken from heavy.ai)

At this point this may not make much sense to you, but hopefully things should become clearer as we go along with this part of the workshop. In fact, we have already tapped into some of these concepts in the previous sections.

## Descriptive vs. inferential statistics {-}

The first thing we need to do is clarify the distinction between *descriptive* and *inferential* statistics. In simple terms, the former deals with the quantitative and/or visual *description* of a sample taken from the population, whereas the latter tries to make *inferences* about the properties of a population based on this sample. And this is an important point to remember: we usually never know the entire state of the population (or the underlying probability distribution that generated the data), we only have access to a (usually significantly smaller) sample of it. And statistics will help us to get a sense of how well this sample might represent the population and hence the uncertainty attached to any inferences we wish to make about it.


## Univariate analysis

As defined earlier, descriptive statistics is concerned with the quantitative and/or visual description of a data sample. We can boradly distinguish two cases: (i) a univariate analysis, where we describe a single variable, for example by its central tendency (e.g. mean or median) and dispersal (e.g. variance or quartiles), and (ii) multivariate analysis, where our data sample consist of more than one variable and where we are interested in the relationship between pairs of variables (e.g. correlation or covariance). 

Here we will introduce you the concept univariate analysis, and you are probably already familiar with most of the material dealt with in this section. We therefore only briefly touch upon some of them, showing how to do generate descriptive statistics in R. But first of all we will load required libraries and generate some data we wish to analyse.


```r
library(tidyverse)

# set a seed for random number generator
set.seed(31072023)

# generate random data from a normal distribution
normSample <- rnorm(50, mean = 10, sd = 1)

# generate random data from a Poisson distribution
poisSample <- rpois(50, lambda = 4)

# generate random data from an exponential distribution
expSample <- rexp(50, rate = 0.2)

# put into a data.frame for later use
sampleDF <- data.frame(Normal = normSample,
                       Poisson = poisSample,
                       Exponential = expSample)
```

Without going into any further detail, let's have a quick look at the data and see how they are distributed.<a name="densities"></a>


```r
# plot the density dsirtibutions
ggplot(sampleDF) +
    geom_density(aes(x = Normal, fill = 'Normal'), alpha = 0.4) +
    geom_density(aes(x = Poisson, fill = 'Poisson'), alpha = 0.4) +
    geom_density(aes(x = Exponential, fill = 'Exponential'), alpha = 0.4) +
    labs(fill = 'Distribution') +
    theme(legend.position = 'top')
```

<img src="_main_files/figure-html/densities-1.png" style="display: block; margin: auto;" />


### **Mean vs. median** {-}

As you will know, the mean and the mediam are two very different statistics. The first is the average value of a data sample, i.e. $\mu = 1/n \sum y_i$ (with $y_i$ being individual data points or values of your sample), whereas the median separates the lower half and upper half of a data sample (i.e. is the value in the middle if you were to order all values form smallest to biggest). How much these two differ, however, depends on how the data is distributed. To demonstrates this, let's calculate both and compare for different distributions


```r
# sample based on normal distribution
print(c(mean(normSample), median(normSample)))
```

```
## [1] 9.863772 9.811931
```

```r
# sample based on normal distribution
print(c(mean(poisSample), median(poisSample)))
```

```
## [1] 4.46 4.50
```

```r
# sample based on normal distribution
print(c(mean(expSample), median(expSample)))
```

```
## [1] 5.446247 3.070014
```

We can see that for the first two samples, both the mean and median are fairly similar. For the sample based on an exponential distribution, however, they are very different. In order to understand why this is the case, we have to look at how the data in each data sample are spread. Specifically, we will look at the *variance / standard deviation*, *interquartile range*, *skewness* and *kurtosis*.

### **Standard deviation** {-}

The standard deviation (SD) is a measure of the dispersal of a set of values and how much these values vary from the sample mean. A low standard variation means that most values are close to the mean, whereas a high standrad deviation means that values are spread far way from the mean (which in itself should give you an indication of the usefulness of using the mean to describe your samples in the first case). Relatedly, the variance is the square of the standard deviation. Mathematically, the standard deviation, usually denoted $\sigma^2$, is given as
$$ \sigma^2 = \frac{1}{n} \sum (y_i - \mu)^2 $$

However, it is much easier to understand visually, here demonstrated by two normal distributions with the same mean but one with SD=1 and one with SD=4


```r
data.frame(SD1 = rnorm(10000, sd = 1),
           SD4 = rnorm(10000, sd = 4)) %>%
    ggplot() +
    geom_density(aes(x = SD1, fill = 'SD=1'), alpha = 0.3) +
    geom_density(aes(x = SD4, fill = 'SD=4'), alpha = 0.3) +
    geom_vline(xintercept = 0, col = 'blue', linetype = 'dashed') +
    labs(x = '',
         fill = '') +
    theme(legend.position = 'top')
```

<img src="_main_files/figure-html/unnamed-chunk-124-1.png" style="display: block; margin: auto;" />

Now let's return to our previous data and compare the spread of each of our sample and see if this might have an influence on the observed difference between the mean and the median.


```r
# sample based on normal distribution
print(c(mean(normSample), median(normSample), sd(normSample)))
```

```
## [1] 9.863772 9.811931 1.091936
```

```r
# sample based on normal distribution
print(c(mean(poisSample), median(poisSample), sd(poisSample)))
```

```
## [1] 4.460000 4.500000 1.991922
```

```r
# sample based on normal distribution
print(c(mean(expSample), median(expSample), sd(expSample)))
```

```
## [1] 5.446247 3.070014 6.942839
```

This is interesting. The standard deviation of the sample based on the Poisson distribution is twice as high as the one based on the normal distribution, and the one based on the exponential distribution even seven times as high. Based on this, it is unlikely to explain our previous observations. 


### **Interquartile range** {-}

Another measure of the spread of data is the so-called interquartile range, or IQR for short. The IQR is defined as the difference between the 75th percentile (third quartile, or Q3) and the 25th percentiles of the data (lower quartile, or Q1). Therefore, the IQR = Q3 − Q1. In simpler terms, the Q1 is the median of the $n$ smallest values and Q3 is the median of the $n$ largest values. 

We have already come across quartiles when we produced box-and-whisker plots, where the boxes show the median (Q2) and interquartile range (Q1 and Q3) and the lower and upper whiskers are defined as $Q1 - 1.5 \times IQR$ and $Q3 + 1.5 \times IQR$, respectively.


```r
ggplot(sampleDF) +
    geom_boxplot(aes(x = 1, y = Normal), fill = 'green', alpha = 0.4) +
    geom_boxplot(aes(x = 2, y = Poisson), fill = 'blue', alpha = 0.4) +
    geom_boxplot(aes(x = 3, y = Exponential), fill = 'red', alpha = 0.4) +
    scale_x_continuous(breaks = c(1, 2, 3), 
                       labels = c('Normal', 'Poisson', 'Exponential')) +
    labs(x = 'Distribution',
         y = 'Value') +
    theme(legend.position = '')
```

<img src="_main_files/figure-html/unnamed-chunk-126-1.png" style="display: block; margin: auto;" />

From this we can already see that the IQR for the Poisson sample is bigger than the normal one, and the exponential one even bigger. In R we can easily calculate the IQR as


```r
# sample based on normal distribution
print(c(mean(normSample), median(normSample), sd(normSample), IQR(normSample)))
```

```
## [1] 9.863772 9.811931 1.091936 1.571149
```

```r
# sample based on normal distribution
print(c(mean(poisSample), median(poisSample), sd(poisSample), IQR(poisSample)))
```

```
## [1] 4.460000 4.500000 1.991922 3.000000
```

```r
# sample based on normal distribution
print(c(mean(expSample), median(expSample), sd(expSample), IQR(expSample)))
```

```
## [1] 5.446247 3.070014 6.942839 4.804575
```

The keen observer will have also noted that the difference between Q1 and Q2 for the exponential sample is much smaller than the difference between Q2 and Q3. That is, looking at the interquartile range cam indicate *skewness* of the data, as well as potential outliers i.e. data points that are below $Q1 - 1.5 \times IQR$ or above $Q3 + 1.5 \times IQR$.


### **Skewness** {-}

Skewness tells us whether the data is symmetric or asymmetrically distributed, an we can distinguish between a *positive skew*, where the right tail of the distribution is longer, and *negative skew*, where the left tail is longer.

<div class="panel panel-default"><div class="panel-heading"> Question </div><div class="panel-body"> 
Just from looking at the data distributions plotted [above](#densities), which samples are skewed, and if they are skewed, are they left or right skewed? </div></div>

<button id="displayTextunnamed-chunk-129" onclick="javascript:toggle('unnamed-chunk-129');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-129" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
The samples based on the normal distribution are not skewed but are symmetrically distributed around the mean. Both the samples based on the Poisson and exponential distribution show a *positive skew*, which is more pronounced in the exponential one.</div></div></div>

$~$

The R library `moments` provides useful functions to measure the shape of a distribution. Let's use this here and see whether it agrees with our assessment *by eye*


```r
# if you do not have this library, install it with install.packages("moments")
library(moments)

# calculate skewness of normal-based samples
skewness(normSample)
```

```
## [1] 0.258172
```

```r
# calculate skewness of normal-based samples
skewness(poisSample)
```

```
## [1] 0.4429934
```

```r
# calculate skewness of normal-based samples
skewness(expSample)
```

```
## [1] 3.448168
```

The results are (almost) as expected. In fact, we see that the samples based on the exponential distribution are by far the most skewed. And this offers one explanation for why the mean and median differs so much: although the bulk of the data lies on the left hand side, the long tail to the right has a significant effect on the mean, such that it is no longer representative of the average value of a data sampled from this distribution (i.e. most values would be smaller than the mean). 


Note, although the skewness for the samples based on the normal distribution is also positive, the value is very small. The same goes for the ones based on the Poisson distribution. What shall we do with this information? I.e. is there evidence that the they are all skewed and hence sufficiently different from a normal distribution? Thankfully the `moments` package provides us with the tool to check this statistically, which we will demonstrate when talking about *kurtosis*.  


### **Kurtosis** {-}

The kurtosis of a distribution is a measure of whether or not it is heavy-tailed or light-tailed *relative to a normal distribution*: 

  - the kurtosis of a normal distribution is 3
  - if the kurtosis is <3, this means that it has fewer and less extreme outliers than the normal distribution
  - if the kurtosis is >3, this means that it has more outliers than the normal distribution.

> **Note:** some formulars substract 3 from the kurtosis, resulting in either negative or positive values (with the normal distribution being 0)

The `moments` package also provides the functionality to calculate the kurtosis of a data sample. For our data this looks like


```r
# calculate skewness of normal-based samples
kurtosis(normSample)
```

```
## [1] 2.175165
```

```r
# calculate skewness of normal-based samples
kurtosis(poisSample)
```

```
## [1] 3.083975
```

```r
# calculate skewness of normal-based samples
kurtosis(expSample)
```

```
## [1] 17.42198
```

Once again, the last data sample stands out by having a kurtosis much greater than 3, meaning it has far more outliers than would be expected if the data came from a normal distribution. 

As mentioned earlier, `moments` offers a statistical test (the so-called Jarque-Bera Normality Test), which compare a given data sample to a normal distribution, with the **Null Hypothesis (H$_0$)** being that the data has a skewness and kurtosis that matches a normal distribution. Let's put this to the test for our three samples.


```r
# samples based on normal distribution
jarque.test(normSample)
```

```
## 
## 	Jarque-Bera Normality Test
## 
## data:  normSample
## JB = 1.9728, p-value = 0.3729
## alternative hypothesis: greater
```

```r
# samples based on Poisson distribution
jarque.test(poisSample)
```

```
## 
## 	Jarque-Bera Normality Test
## 
## data:  poisSample
## JB = 1.6501, p-value = 0.4382
## alternative hypothesis: greater
```

```r
# samples based on exponential distribution
jarque.test(expSample)
```

```
## 
## 	Jarque-Bera Normality Test
## 
## data:  expSample
## JB = 532.4, p-value < 2.2e-16
## alternative hypothesis: greater
```

And this provides evidence that the data sample based on the exponential distribution is statistically different from the normal distribution. On the other hand, there is no evidence to support our hypothesis that the sample based on the Poisson distribution is different from a normal distribution. 

<div class="panel panel-default"><div class="panel-heading"> Question </div><div class="panel-body"> 
What is your explanation for this unexpected finding? </div></div>

<button id="displayTextunnamed-chunk-134" onclick="javascript:toggle('unnamed-chunk-134');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-134" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
There are two parts to this. The first one is that the size of the sample is too small to detect a (statistically significant) difference. The second part is that this example clearly highlight some of the dangers of null hypothesis testing and overreliance on P values. To convince yourself that this is the case, create a new data set but increase the sample size to 150, for example, and rerun the test. 

```r
poisSample2 <- rpois(150, lambda = 4)
jarque.test(expSample)
```

```
## 
## 	Jarque-Bera Normality Test
## 
## data:  expSample
## JB = 532.4, p-value < 2.2e-16
## alternative hypothesis: greater
```

Et voila!</div></div></div>

$~$

## Multivariate analysis

In a multivariate analysis we are usually interested in the relationship between pairs of variables. Here we will briefly go through three commonly used methods to examine how two or more variables are related: contingency tables, Pearson correlation and Spearman rank correlation.

### **Contingency tables** {-}

Contingency tables are types of tables that display the frequency distribution of two variables against each other. As an example, say we had data from a clinical trial where patients were given either a treatment or a placebo and we are interested in how many people recovered from a disease within 5 days. In each arm we had 100 individuals and in the treatment group 73 individuals recovered and in the placebo group 64. In table format this would thus look like this

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> teatment </th>
   <th style="text-align:center;"> recovered </th>
   <th style="text-align:center;"> disease </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> drug A </td>
   <td style="text-align:center;"> 73 </td>
   <td style="text-align:center;"> 27 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> placebo </td>
   <td style="text-align:center;"> 64 </td>
   <td style="text-align:center;"> 36 </td>
  </tr>
</tbody>
</table>

We can see that there were more individuals who recovered in the treatment arm of the study. But how do we know that this was not due to chance? To answer this question we have to briefly tap into inferential statistics. And two common methods to provide functions to perform statistical tests on contingency tables: **Pearson's chi-squared test** and **Fisher's exact test**. We are not going into the details of where they differ but only mention that Fisher's exact test is non-parametric, typically defined on a 2 x 2 contingency table, and, importantly, works with small sample sizes. The chi-squared (or $\chi^2$) test, on the other hand, works on more than one variables but usualy requires larger sample sizes.

#### **Pearson's chi-squared test** {-}

Perform a chi-squared test in R is straightforward using the `chisq.test()` function.


```r
# define our contingency table
trial <- data.frame(recovered = c(73, 64),
                    disease = c(27, 36))

# add row names (not necessary)
row.names(trial) <- c('drug A', 'placebo')

# run test
chisq.test(trial)
```

```
## 
## 	Pearson's Chi-squared test with Yates' continuity correction
## 
## data:  trial
## X-squared = 1.483, df = 1, p-value = 0.2233
```

Because data can come in different formats, here we provide an example of how to create a simple contingency table if your data only had the recorded outcome, for example as *recovered / not recovered* or recovered *yes / no*, stored in two columns, one for the treatment arm and one for the placebo arm.


```r
# recorded outcome recovered yes / no
trialData <- data.frame(drug = c(rep('recovered',73), rep('not recovered', 27)),
                        placebo = c(rep('recovered',64), rep('not recovered', 36)))

# first turn into "tidy" format
trialData <- trialData %>%
    gather(treatment, outcome, drug:placebo)

# create a contingency table
contTable <- table(trialData)

# perform chi-sq test 
chisq.test(contTable)
```

```
## 
## 	Pearson's Chi-squared test with Yates' continuity correction
## 
## data:  contTable
## X-squared = 1.483, df = 1, p-value = 0.2233
```

#### **Fisher's exact test** {-}

Fisher's exact test work in a very similar way and directly on a 2 x 2 contingency table. For large sample sizes you will notice that both test give you similar test statistics, but as mentioned, it is more powerful when sample sizes are small.


```r
# run Fisher's exact test on previously defined contingency matrix
fisher.test(contTable)
```

```
## 
## 	Fisher's Exact Test for Count Data
## 
## data:  contTable
## p-value = 0.2232
## alternative hypothesis: true odds ratio is not equal to 1
## 95 percent confidence interval:
##  0.3438828 1.2516078
## sample estimates:
## odds ratio 
##  0.6589328
```

As you will have noticed, this test works on and also reports odds ratio, which is a handy "side effect" of using this function.


### **Pearson correlation** {-}

The aim of the *Pearson correlation coefficient*, or most commonly referred to simply as *correlation coefficient*, is to establish a line of best fit through a dataset of two variables and measure how far away the data are from the expected values (the best fit line). Values range between +1 (perfect positive correlation) to -1 (perfect negative correlation), and any value in between. Here are some examples


```
## `geom_smooth()` using formula = 'y ~ x'
```

<img src="_main_files/figure-html/unnamed-chunk-139-1.png" style="display: block; margin: auto;" />

To calculate the correlation coefficient in R between two vectors $x$ and $y$ we simply call the `cor(x,y)` function. And if we are further interested in whether the correlation (or lack of it) is statistically significant we can use the `cor.test(x,y)` function.

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Create a data.frame with two simulated (artifical) data samples. Plot this data using `ggplot` and add a linear regression line (remember `geom_smooth()`?). Then test whether there is a correlation between the two variables and if so, test whether this is statistically significant. </div></div>

<button id="displayTextunnamed-chunk-141" onclick="javascript:toggle('unnamed-chunk-141');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-141" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
# sample from uniform distribution
x <- runif(50, 1, 5)

# assume linear relationship between x and y plus some Gaussian noise
y <- 2.3*x + rnorm(50,0,1)

# create data.frame
df <- data.frame(x = x, y = y)

# plot
ggplot(df, aes(x, y)) +
    geom_point() +
    geom_smooth(method = 'lm', se=F)
```

```
## `geom_smooth()` using formula = 'y ~ x'
```

<img src="_main_files/figure-html/unnamed-chunk-459-1.png" style="display: block; margin: auto;" />

```r
# test for correlation
cor.test(x,y)
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  x and y
## t = 14.795, df = 48, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.8386875 0.9456033
## sample estimates:
##       cor 
## 0.9056209
```
</div></div></div>

$~$

### **Spearman's rank correlation** {-}

In comparison to Pearson's correlation, Spearman's rank correlation is a non-parametric measure of how the *ranking* of two variables are correlated. In fact, the Spearman correlation is equal to the Pearson correlation between the rank values of two variables. So instead of comparing the values, here we compare their ranks, or their indices when ordered from smallest to largest. As before, the values for Spearman's rho ($\rho$) can range from -1 to +1. Without providing any more detail, here is an example of how to calculate Spearman's rho in R


```r
Age <- c(9, 11, 1, 7, 6, 5, 10, 3, 4, 4)
OD <- c(478, 755, 399, 512, 458, 444, 716, 399, 491, 456)

# use the same function as before but define method = 'spearman'
cor(Age, OD, method = 'spearman')
```

```
## [1] 0.8597561
```

```r
# and test for significance
cor.test(Age, OD, method = 'spearman')
```

```
## Warning in cor.test.default(Age, OD, method = "spearman"): Cannot compute exact
## p-value with ties
```

```
## 
## 	Spearman's rank correlation rho
## 
## data:  Age and OD
## S = 23.14, p-value = 0.001424
## alternative hypothesis: true rho is not equal to 0
## sample estimates:
##       rho 
## 0.8597561
```

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Compare the two correlation coefficients for different data.  </div></div>

### **Correlation vs. causation** {-}

**Beware:** even a very high correlation between two variables does not infer causality - causality can only be inferred through careful experimental design in a well-controlled setting. A good example how looking purely at correlation can be misleading is this one (taken from [Spurious Correlations](https://tylervigen.com/spurious-correlations))

![$\rho = 0.947$!](images/bedsheet_correlation.png)


<!--chapter:end:3-Descriptive_statistics.Rmd-->

# Linear Models (LM)

## Simple linear regression

When analysing data, we are often interested in exploring the relationship between a single response variable and one or multiple explanatory variables (predictors). This can be done by fitting a linear model. In fact, we have already come across this in earlier sections of this workshop; here we will provide more information on what is unde the hood and how to do perform linear modelling in R.

The term *linear* in linear models refers to the fact that there is a *linear*, or straight line, relationship between a predictor, $x$, and the response $y$. In other words, we can write 
$$ y = \beta_0 + \beta_1 x $$
where $\beta_0$ is the so-called *intercept*, i.e. the value of $y$ when $x=0$, and $\beta_1$ is the *gradient*, which describes by how much $y$ varies with increasing or decreasing values of $x$.

<img src="_main_files/figure-html/unnamed-chunk-144-1.png" style="display: block; margin: auto;" />

What can be seen form the above graph is that the data points are not all on top of the regression line but spread above and below it. What this means is that an individual data point, $y_i$, can be described by the linear relationship
$$y_i = \beta_0 + \beta_1 x_i + \epsilon_i$$
where $\epsilon_i$ is the deviation, or (residual) error, between the best line fit and the actually observed value $y_i$. 

One on the key assumptions of a linear model is that all the $\epsilon_i$'s are normally distributed with a mean of 0 and some standard deviation $\sigma$. In mathematical terms, the linear regression model is therefore defined as 
$$
\begin{align}
y_i &= \beta_0 + \beta_1 x_i + \epsilon_i \\
\epsilon_i &\sim \mathcal{N}(0, \sigma^2)
\end{align}
$$

$\epsilon$ is also commonly referred as the **noise** term. This is because the response variable has usually some uncertainty associated with it (e.g quantifying gene expression using microarrays or RNA-seq, etc.). 

The general idea behind linear regression is to find the best fit line which minimises, or absorbs, the total (residual) noise. We are not going into the mathematical intricacies but rather show you how this is done in R, together with the general workflow of linear regression

  1. infer the model parameters $\beta_0$ and $\beta_1$
  2. check the model fit
  3. interpret the significance of the estimated parameters
  

## Linear regression in R

To show you how easy it is to linear regression in R we first create a fake dataset, which contains data of the height and weight of $N=100$ individuals randomly sampled from a population


```r
N <- 100
height <- runif(N, min = 135, max = 195)
weight <- 0.48 * height + rnorm(N, mean=0, sd=7)

sampleData <- data.frame(height = height,
                         weight = weight) 

ggplot(sampleData, aes(x = height, y = weight)) +
    geom_point() +
    labs(x = 'height (cm)',
         y = 'weight (kg)')
```

<img src="_main_files/figure-html/unnamed-chunk-145-1.png" style="display: block; margin: auto;" />

Judging by eye we would be confident to declare that there is a (linear) relationship between the height and weight of an individual. So let's fit a linear regression model and check whether this is indeed the case (in a statistical sense). To do this in R we will use the `lm()` function (please read the documentation for full details). This function requires a **formular** that describes the relationship between the predictor or explanatory variable (here height) and the response variable (here weight), which is given in the form `response ~ explanatory`, or in our case `weight ~ height`. With this, R will try to fit the following model
$$ weight_i = \beta_0 + \beta_1 \times height_i + \epsilon_i $$

And here is how this is done


```r
# fit linear model and assign to object 'fit'
fit <- lm(weight ~ height, data = sampleData)

# print output
print(fit)
```

```
## 
## Call:
## lm(formula = weight ~ height, data = sampleData)
## 
## Coefficients:
## (Intercept)       height  
##      8.8537       0.4204
```

The output of interest are the two numbers `(Intercept)`= 8.8537, which is our $\beta_0$ term, and `weight`= 0.4204, which is our $\beta_1$ term.

So far so good; but how do we get the regression line? There are, in principle, two ways: either we calculate this by hand using the beta-terms we just obtained, or we use the `predict()` function (please see R documentation for further details).


```r
# define the x-range for our regression line
bestFit <- data.frame(height = c(135, 195))

# Option 1: calculate the y-values by hand
bestFit["weight"] <- 5.0613 + 0.4471 * bestFit$height

# Option 2: use the predict() function
bestFit["weight"] <- predict(fit, newdata = bestFit)

ggplot(sampleData, aes(x=height, y=weight)) +
    geom_point() +
    geom_line(data=bestFit, aes(x=height, y=weight), col = 'blue', linewidth = 1)
```

<img src="_main_files/figure-html/unnamed-chunk-147-1.png" style="display: block; margin: auto;" />

> **Note:** this is essentially what `geom_smooth(method = 'lm')` would have done for us!

### **Using the `summary()` function**

Above the called `print(fit)` to obtain the fitted parameters of our model. However, if you check carefully in the *Environment* tab in RStudio, you will see that `fit` contains a lot more information. And this can be summarised in a much more informative fashion using the `summary()` function


```r
summary(fit)
```

```
## 
## Call:
## lm(formula = weight ~ height, data = sampleData)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -13.2130  -5.0512  -0.6079   4.6114  24.7020 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  8.85369    7.45411   1.188    0.238    
## height       0.42043    0.04554   9.232 5.63e-15 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 7.234 on 98 degrees of freedom
## Multiple R-squared:  0.4651,	Adjusted R-squared:  0.4597 
## F-statistic: 85.23 on 1 and 98 DF,  p-value: 5.627e-15
```

Let's go through this line-by-line

  - **Call** <br>
  This just states the arguments that were passed to the `lm()` function. Remember it’s `response ~ explanatory`.

  - **Residuals** <br>
  Some basic stats about the residuals (i.e the differences between the model fit and the observed data points). It is easier to plot a histogram of the residuals (shown in the next section), but these basic stats can already give us an indication of whether we have a symmetric distribution with zero mean (i.e we want the median to be close to zero, the third quartile (Q3) to be roughly equal to -Q1 (first quartile) and the max to be approximately -min).

  - **Coefficients** <br>
    
    - `Estimate` <br>
    `(Intercept)`= 8.8537 and `weight`= 0.4204 kg/cm are our regression parameters.
    
    - `Std. Error` <br>
    The standard errors for the two inferred parameters. They tells us how confident we are in our estimates: if the standard error is comparable or greater than the actual parameter estimate itself then that point estimate should not be trusted. We can also show the confidence intervals for the model parameters to highlight their uncertainty using the `confint()` function:
    
    ```r
    confint(fit, levels=0.95)
    ```
    
    ```
    ##                 2.5 %    97.5 %
    ## (Intercept) -5.938749 23.646134
    ## height       0.330056  0.510808
    ```

    - `t value` and `Pr(>|t|)` <br>
    This is the result of a hypothesis testing against the null hypothesis that the coefficient is zero.
    
  - **Residual standard error** <br>
  The square root of the residual sum of squares / degrees of freedom (here 98 = 100 (data points) - 2 (parameters needed for the regression line))
    
  - **Multiple R-squared** <br>
  The $R^2$ statistic, which is also referred to as as the coefficient of determination is the proportion of the total variation that is explained by the regression, i.e. <br>
  <center> **total variation** = **regression** (explained) variation + **residual** (unexplained) variation </center> <br>
  In regression with a single explanatory variable, this is the same as the Pearson correlation coefficient squared.

  - **F-statistic** <br>
  The F-statistic can be used to assess whether the amount of variation explained by the regression ($M_1$) is statistically significantly different compared to the null model ($M_0$), which in this case corresponds just taking the mean of the data. Large values of the F-statistic correspond to cases where the model fit is better for the more complex model compared to the null model. This test can be used to generate a P-value to assess whether the model fit is statistically significantly better given a pre-defined level of significance.


## Model checking

The next step in linear (or any statistical) modelling is the concept of **model checking**. In theory, we could fit any model to our data simply by changing our assumptions about how the response and predictor variables are related. What we would like to do, however, is to make **robust** inferences, and for this we must check our model, which essentially boils down to checking whether our assumptions are reasonable.

The main assumption in our model was that the residuals (the differences between the data points and the regression line) are normally distributed around 0. We can easily check whether this is the case 


```r
hist(fit$residuals)
```

<img src="_main_files/figure-html/unnamed-chunk-150-1.png" style="display: block; margin: auto;" />

We can see that the residuals are fairly evenly distributed and centered around 0, which is a good sign! 

R also provides us with some easy tools for further model diagnostics, which can be called simply through


```r
#setting up a 2x2 plot grid
par(mfrow=c(2,2))

# plot model diagnostics
plot(fit, pch = 20, cex = 0.5)
```

<img src="_main_files/figure-html/unnamed-chunk-151-1.png" style="display: block; margin: auto;" />
What do these plot tell us about the model fit, though?

### **Residuals vs Fitted** {-}

The first plot, *Residuals vs Fitted*, checks that the variance is constant along the fitted line and that there is no systematic pattern whereby the errors get bigger or smaller as dependent on the fitted values. In our case, everything seems to be OK, but here are some (extreme) examples where this is not the case:

<img src="images/02-funnel.png" width="600px" style="display: block; margin: auto;" />


### **Normal Q-Q** {-}

A Q–Q plot, or *quantile-quantile* plot, compares two probability distributions by plotting their quantiles against each other. If the two distributions are similar, then the points should fall approximately on the identity line $y = x$. In our case, we are plotting the quantiles of the residuals against their *assumed* distribution, which is the Normal distribution, and see that there is nothing to worry about (which we should know already from the histogram above).  

Here is an example when things go wrong (i.e. when our linear assumption is violated):

<img src="_main_files/figure-html/unnamed-chunk-153-1.png" style="display: block; margin: auto;" />

### **Scale-Location** {-}

The scale location graph is very similar to the first plot but on a different scale.


### **Residuals vs Leverage** {-}

The last plot examines the influence of individual data points on our inference. Ideally, all points should equally contribute to the fit. In some cases we might find outliers, which have an above *leverage* on the fitted line, which can be measured by *Cook's distance'. An extreme example is shown here

<img src="_main_files/figure-html/unnamed-chunk-154-1.png" style="display: block; margin: auto;" />

## Prediction

Making predictions about unknown or unobserved data is the key benefit of statistical modelling. In fact, we have already used this to overlay a regression line onto our data by using the `predict()` function. Going back to our original example, let's say we want to know the *average* weight for an individual who is 187cm tall. Note, the `predict()` function requires the new (to be predicted) data to be provided as a data.frame.


```r
predict(fit, data.frame(height=187))
```

```
##        1 
## 87.47447
```

Remember that our inference comes with a degree of uncertainties (because we can never know the true relationship based on a random sample from a population). A useful feature of the `predict()` function is that it can not only provide point estimates but also the **confidence** or **prediction** interval. Let' say we are intereted in the 95% confidence interval for our prediction


```r
predict(fit, data.frame(height=187), interval = 'confidence', level = 0.95)
```

```
##        fit      lwr      upr
## 1 87.47447 84.86624 90.08271
```

and to obtain the 96% prediction interval

```r
predict(fit, data.frame(height=187), interval = 'prediction', level = 0.95)
```

```
##        fit      lwr      upr
## 1 87.47447 72.88477 102.0642
```

As you can see, the prediction interval is significantly larger than the confidence interval.

### **Confidence vs prediction interval** {-}

The *confidence interval* corresponds to the uncertainty surrounding our estimate of an **average individual**; it represents the uncertainty in the mean (i.e. in our case the regression line): $y = \beta_0 + \beta_1 x$. In contrast, the *prediction interval* corresponds to the uncertainty surrounding an **Individual observation**. 

Here we show you how both intervals can be computed and added to your (linear) regression line. Although these are often not shown they are important for conveying uncertainties.


```r
newheight <- data.frame(height = seq(min(sampleData$height), max(sampleData$height), length.out=100))
newdata <- cbind(newheight, predict(fit, newdata = newheight, interval = 'confidence', level = 0.95)) %>%
    rename(weight = fit)

ggplot(mapping = aes(x = height, y = weight)) +
    geom_point(data = sampleData) +
    geom_ribbon(data = newdata, aes(ymin=lwr, ymax=upr), fill = 'grey', alpha = 0.7) +
    geom_line(data = newdata, col = 'blue', linewidth=1) 
```

<img src="_main_files/figure-html/unnamed-chunk-158-1.png" style="display: block; margin: auto;" />

... and now compare this to what `geom_smooth()` produces


```r
ggplot(sampleData, aes(x = height, y = weight)) +
    geom_point() +
    geom_smooth(method = 'lm')
```

<img src="_main_files/figure-html/unnamed-chunk-159-1.png" style="display: block; margin: auto;" />

They are the same - so now you know what `geom_smooth()` actually does!

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Produce a similar graph but now plot the 97% prediction interval instead of the confidence interval. Can you put them both in the same graph?  </div></div>

<button id="displayTextunnamed-chunk-161" onclick="javascript:toggle('unnamed-chunk-161');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-161" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
newheight <- data.frame(height = seq(min(sampleData$height), max(sampleData$height), length.out=100))
newdata_ci <- cbind(newheight, predict(fit, newdata = newheight, interval = 'confidence', level = 0.97)) %>%
    rename(weight = fit)
newdata_pi <- cbind(newheight, predict(fit, newdata = newheight, interval = 'prediction', level = 0.97)) %>%
    rename(weight = fit)

ggplot(mapping = aes(x = height, y = weight)) +
    geom_point(data = sampleData) +
    geom_ribbon(data = newdata_pi, aes(ymin=lwr, ymax=upr), fill = 'grey', alpha = 0.7) +
    geom_ribbon(data = newdata_ci, aes(ymin=lwr, ymax=upr), fill = 'red', alpha = 0.4) +
    geom_line(data = newdata_ci, col = 'blue', linewidth=1) 
```

<img src="_main_files/figure-html/unnamed-chunk-484-1.png" style="display: block; margin: auto;" />
</div></div></div>

$~$

## Multiple linear regression

So far we have only considered a single explanatory variable, for example *height*. In most scenarios, however, we will have measured more than variable that could affect the outcome (response). In this case, our linear regression model extends to 
$$ y_i = \beta_0 + \beta_1 x_{1i} + \beta_2 x_{2i} + ... + \beta_n x_{ni} + \epsilon_i $$

Let's make up some artificial data again to illustrate how to perform multiple linear regression in R. In this case we assume we had measure the total number of malaria episodes of 100 individuals aged between 1 and 10 living under different transmission intensities, measured as EIR and here for simplicity scaled to between 0 and 1. The model we are therefore trying to fit is
<center> episodes$_i$ = $\beta_0$ + $\beta_1$EIR$_i$ + $\beta_2$age$_i$ </center>

First, create our new dataset 

```r
# create random data points for age and EIR
age <- runif(100, 1, 10)
EIR <- runif(100, 0, 1)

# assume some linear relationship between episodes and age and EIR plus noise
episodes <- round(1.5*age + 4.1*EIR + rnorm(100, 0, 2))

# put into new data.frame
epiData <- data.frame(Age = age, Episodes = episodes, EIR = EIR)
```

As a 3D-scatterplot this looks like this


```r
library(scatterplot3d)
scatterplot3d(EIR, age, episodes, pch=19, ylab='Age (years)', 
              xlab='Transmission intensity', zlab='Malaria episodes', color='grey')
```

<img src="_main_files/figure-html/unnamed-chunk-163-1.png" style="display: block; margin: auto;" />
Note how we now spread our data along a third dimension, i.e. we go from 2D to 3D and from a best fit line to a best fit hyperplane. Adding more explanatory variables will effectively spread the data even further in more dimensions, which makes it much harder to make robust inferences. Another key objective in statistical modelling is therefore to find the *minimal adequate model*.

To fit the model in R we use exactly the same function and terminology as before


```r
fit <- lm(Episodes ~ EIR + Age, data = epiData)
```

which we can project onto our 3D-scatterplot

```r
hfig <- scatterplot3d(EIR, age, episodes, pch=19, ylab='Age (years)', 
              xlab='Transmission intensity', zlab='Malaria episodes', color='grey')
hfig$plane3d(fit, draw_polygon=T)
```

<img src="_main_files/figure-html/unnamed-chunk-165-1.png" style="display: block; margin: auto;" />

Next we are interested in the actual inference, i.e. the estimated parameters and some indication whether the two predictor variables (age and EIR) have a significant effect on the response (malaria episodes)


```r
summary(fit)
```

```
## 
## Call:
## lm(formula = Episodes ~ EIR + Age, data = epiData)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -5.2073 -1.4295 -0.2354  1.2642  5.4162 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  0.15704    0.63964   0.246    0.807    
## EIR          3.59941    0.71582   5.028 2.27e-06 ***
## Age          1.48781    0.08412  17.686  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.053 on 97 degrees of freedom
## Multiple R-squared:  0.7746,	Adjusted R-squared:   0.77 
## F-statistic: 166.7 on 2 and 97 DF,  p-value: < 2.2e-16
```

As before, using the `summary()` function we get a summary of everything that's important. 

  - the residuals appear symmetric and centered around 0
  - the estimates for $\beta_1$ (EIR) and $\beta_2$ (age) are both positive and in magnitude as expected
  - the estimate for $\beta_0$ is $\neq 0$ - what does this mean in practical terms? (we will revisit this at a later part of this workshop) 
  - the inferred effects of both EIR and age are statistically significant
  - the adjusted R-squared value suggests that $\sim 80$% of the variation is explained by our model
  
This all seems really good, but we should still have a look at model diagnostics to see whether our model, or rather its underlying assumptions are valid.   


```r
par(mfrow=c(2,2))
plot(fit)
```

<img src="_main_files/figure-html/unnamed-chunk-167-1.png" style="display: block; margin: auto;" />

The diagnostics all look reasonable and there is nothing that should make us doubt our model and assumed relationship between the response and explanatory variables. Note, these plots look exactly the same as in the simple linear model we have done earlier. This is because no matter how many (linear) predictors we put into our model, it is the behaviour of the residuals that we are interested in to make a statement about our model fit. 


<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 

  1. Calculate the predicted number of episodes plus 95% cofidence intervals for a 5 year old living in a transmission setting with EIR=0.5 

  2. Fit a new model `Episodes ~ Age`. Look at the total variation explained and compare this to the full model; what would you conclude from this?

  3. Fit a new model `Episodes ~ EIR`. Look at the estimate for the predictor variable and its associated P value and compare this to the ones based on the full model; what would you conclude from this? </div></div>

<button id="displayTextunnamed-chunk-169" onclick="javascript:toggle('unnamed-chunk-169');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-169" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
predict(fit, newdata = data.frame(Age=5, EIR=0.5))
```

```
##        1 
## 9.395781
```
</div></div></div>

<br>

## Categorical explanatory variables

So far we have only dealt with numerical predictor variables. But what about non-numerical or categorical variables? Turns out that these are as easily dealt with as numerical one. To show how to perform linear regression with one or more categorical explanatory variables, we slightly modify our malaria episode dataset to include one extra variable: bednet, which will be an indicator of whether the child sleeps under a bednet or not. 


```r
# create random data points for age and EIR
bednet <- sample(c('yes', 'no'), 100, replace=TRUE)

# assume some linear relationship between episodes and age and EIR plus noise
episodes <- ifelse(bednet=='yes', 0, 2) + 1.5*age + 4.1*EIR + rnorm(100, 0, 2)

# put into new data.frame
epiData <- data.frame(Episodes = episodes, 
                      Age = age, 
                      EIR = EIR,
                      Bednet = factor(bednet))
```

The model we are fitting now looks very similar to the one we fitted before 

<center> episodes$_i$ = $\beta_0$ + $\beta_1$EIR$_i$ + $\beta_2$age$_i$ + $\beta_3$bednet$_i$</center>

<br>

However, *bednet* is now a *dummy variable* that takes on a value of 0 (bednet = "no") or 1 (bednet = "yes"). So essentially we are fitting **two** regression lines, one for those who sleep under a bednet and one for those who do not (because the $\beta_3$ term will fall out).

In terms of fitting this model in R, nothing has changed and we do not need to explicitly specify if one or more of the variables is a categorical one, the `lm()` function will take care of this for us 


```r
fitCat <- lm(Episodes ~ EIR + Age + Bednet, data = epiData)
summary(fitCat)
```

```
## 
## Call:
## lm(formula = Episodes ~ EIR + Age + Bednet, data = epiData)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -3.379 -1.280  0.090  1.038  5.435 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  2.03776    0.57523   3.543 0.000614 ***
## EIR          4.68344    0.63706   7.352 6.52e-11 ***
## Age          1.54715    0.07706  20.076  < 2e-16 ***
## Bednetyes   -3.26666    0.37840  -8.633 1.28e-13 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 1.825 on 96 degrees of freedom
## Multiple R-squared:  0.8272,	Adjusted R-squared:  0.8218 
## F-statistic: 153.1 on 3 and 96 DF,  p-value: < 2.2e-16
```

As you will notice from the summary, we now get an estimate for `Bednetyes` but not for `Bednetno`, what is going on? Becauase `Bednet` can only take on two values (0/1 or no/yes), one is taken as the *reference case*. That is, the intercept can now be interpreted as the average number of episodes for 0-year old living in a setting with an EIR=0. The estimate `Bednetyes`=-3.2667 tells you how much lower the expected number of episodes is for those who do sleep under a bednet.

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Without using the `predict()` function, what is the predicted number of episodes for a 7-year old who sleeps under a bednet in a setting with an EIR of 0.8? </div></div>

<button id="displayTextunnamed-chunk-173" onclick="javascript:toggle('unnamed-chunk-173');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-173" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
This can be calculated as 

```r
fitCat$coefficients[[1]] + fitCat$coefficients[[2]]*0.8 + fitCat$coefficients[[3]]*7 + fitCat$coefficients[[4]]
```

```
## [1] 13.34791
```
</div></div></div>

<br>

To show the effect of the extra categorical variable, we can plot the data once by ignoring the effect of `Bednet` and once by colouring in the data points by bednet use.


```r
# very useful package for arranging multiple ggplots
library(patchwork)

# simply plot all data and ignore the effect of bednet use
# the lm function in this case would fit the model episodes ~ age + EIR
p1 <- ggplot(epiData, aes(x = Age, y = Episodes)) +
    geom_point() +
    geom_smooth(method='lm', se=F)

# create new dataset for predict()
newdata <- expand_grid(
    Age = seq(1, 10, length.out = 10),
    EIR = rep(median(epiData$EIR), 10),
    Bednet = factor(c("no", "yes")))

newdata <- newdata %>% 
    mutate(Episodes = predict(fitCat, newdata))

p2 <- ggplot(mapping = aes(x = Age, y = Episodes, col = Bednet)) +
    geom_point(data = epiData) +
    geom_line(data = newdata, linewidth=1)

p1 + p2
```

<img src="_main_files/figure-html/unnamed-chunk-174-1.png" style="display: block; margin: auto;" />

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Use `ggplot` to plot `Episodes` against `Age` stratified (coloured) by `Bednet` and add regression lines using `geom_smooth(method = 'lm')`. What do you notice? </div></div>

<button id="displayTextunnamed-chunk-176" onclick="javascript:toggle('unnamed-chunk-176');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-176" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
ggplot(epiData, aes(x = Age, y = Episodes, col = Bednet)) +
    geom_point() +
    geom_smooth(method = 'lm', se=F)
```

<img src="_main_files/figure-html/unnamed-chunk-511-1.png" style="display: block; margin: auto;" />

This graph looks very different to the one we preduced earlier. Although it still shows higher incidence for individuals without bednets, it suggests that the slopes are different (i.e. dependent on bednet use). Why this might be is subject of the next part dealing with interactions between predictor variables. </div></div></div>

<br>

## Interactions

Before we go on to the next big topics, *Mixed Effect Models* and *Generalised Linear Models*, we briefly show you how to consider possible interactions between two or more variables. That is, we have so far considered that the different predictors (e.g. age and EIR) had an independent effect on the response variable (e.g. episodes). There are situations where this is not the case and where the effect of one explanatory variable on the response depends on the value of another explanatory variable. We can estimate this dependency by including a so-called *interaction term* in our model.

To illustrate the importance of interactions and how to deal with them in our regression model, we will look at an example where our inferences can be very misleading when not accounting for possible interaction effects.

Let's consider another made up example, in this case a disease, which we believe is influenced by temperature and rainfall. Furthermore, let's assume rainfall is seasonal but temperature is not, such that rainfall can be represented as a categorical variable; the response variable will be disease incidence. 


```r
# create temperature and rinafall data
temperature <- runif(100, 28, 34)
rainfall <- sample(c('no', 'yes'), 100, replace = TRUE)

# define incidence as dependent on temperature, more so in rainy season 
incidence <- ifelse(rainfall == 'yes', 
                    101 + 2.7*temperature + rnorm(100, 0, 3), 
                    184 + 0.0*temperature + rnorm(100, 0, 3))

# put everything into data.frame
incDF <- data.frame(incidence = incidence,
                    temperature = temperature,
                    rainfall = factor(rainfall))
```

Note, in this example we have created data, where temperature *appears* to have an effect but rainfall does not.

If we were given this data we would usually start by visualising it, maybe with a boxplot showing the distribution of incidence for the off and on-season and a graph plotting incidence against temperature.


```r
p1 <- ggplot(incDF, aes(x = rainfall, y = incidence, fill = rainfall)) +
    geom_boxplot(alpha = 0.5)

p2 <- ggplot(incDF, aes(x = temperature, y = incidence)) +
    geom_point() +
    geom_smooth(method='lm')

p1 + p2
```

<img src="_main_files/figure-html/unnamed-chunk-178-1.png" style="display: block; margin: auto;" />

It would be reasonable to conclude that rainfall does not seem to have a strong effect on incidence whilst there seems to be a clear and positive correlation between temperature and incidence. Next we would put this through our statistical modelling machinery and test whether our predictions are right.


```r
fit <- lm(incidence ~ temperature + rainfall, data = incDF)

summary(fit)
```

```
## 
## Call:
## lm(formula = incidence ~ temperature + rainfall, data = incDF)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -8.8694 -1.7518  0.1403  2.6131  8.4056 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 147.0397     6.6019  22.272  < 2e-16 ***
## temperature   1.2146     0.2130   5.702 1.28e-07 ***
## rainfallyes  -0.3287     0.7309  -0.450    0.654    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.594 on 97 degrees of freedom
## Multiple R-squared:  0.2517,	Adjusted R-squared:  0.2363 
## F-statistic: 16.31 on 2 and 97 DF,  p-value: 7.814e-07
```

From this analysis we would conclude that temperature has a statistically significant effect on disease incidence (*P*<0.001), that rainfall does not have a statistically significant effect on disease incidence (*P*=0.91), and that would be the end of it. But what about the possibility that the effect of temperature is dependent on whether it is the on- or the off-season? That is, we are interested in the interaction term temperature $\times$ rainfall. In the `lm()` function we can do this either adding the term `temperature:rainfall` to our previous model, or use the notation `temperature*rainfall`, which is short for `temperature + rainfall + temperature:rainfall`


```r
fitInteraction <- lm(incidence ~ temperature*rainfall, data = incDF)

summary(fitInteraction)
```

```
## 
## Call:
## lm(formula = incidence ~ temperature * rainfall, data = incDF)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -8.3512 -1.1099  0.1151  1.5418  5.6447 
## 
## Coefficients:
##                         Estimate Std. Error t value Pr(>|t|)    
## (Intercept)             198.1774     6.9041  28.704   <2e-16 ***
## temperature              -0.4415     0.2232  -1.978   0.0508 .  
## rainfallyes             -93.4598     9.3205 -10.027   <2e-16 ***
## temperature:rainfallyes   3.0131     0.3011  10.007   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.528 on 96 degrees of freedom
## Multiple R-squared:  0.6338,	Adjusted R-squared:  0.6223 
## F-statistic: 55.37 on 3 and 96 DF,  p-value: < 2.2e-16
```

In the summary we can see one additional term: `temperature:rainfallyes`, and we see that this is highly significant (*P*<0.001). On the other hand, `temperature` does not appear to be a statistically significant predictor of `incidence` anymore! Beware: this would be the wrong conclusion because of the significance of the interaction term. I.e. removing `temperature` from our model, which would also remove the interaction term, would result in a much inferior model.

One other, and important, conclusion we can draw from this analysis is that interaction terms affect the **slope** of the regression line, which contrasts the additive effects we saw earlier and that only affected the **intersect**. And this also explains why adding linear regression lines with `geom_smooth` for stratified data we can get lines with different gradients.


```r
ggplot(incDF, aes(x = temperature, y = incidence, col = rainfall)) +
    geom_point() +
    geom_smooth(method = 'lm')
```

<img src="_main_files/figure-html/unnamed-chunk-181-1.png" style="display: block; margin: auto;" />

>**Note:** in this example we considered interaction between a continuous and a categorical variable. Interactions between two continuous or two categorical variables are also possible and are treated in exactly the same way in `lm()`. The only difference is the (biological) interpretation of the interaction term.


<!--chapter:end:4-Linear_models.Rmd-->

# Mixed Effect Models (MEM)

One of the key assumptions of linear models is that the data is independent and identically distributed (i.i.d.). This means that our data sample is a true representation of the underlying population and that we have sampled without any (intentional or unintentional) bias. Sometimes this is not the case, however, meaning that there could be some systematic difference between some of our samples. We have come across a situation like this in the previous example, where samples taken during the rainy season showed a different pattern with temperature than those sampled during the off-season. We dealt with this by adding `rainfall` as a categorical variable into our model. This worked not only because there were only two possible levels for `rainfall` but also because we care about the identity of those levels, i.e. we wanted to estimate how incidence changes for `rainfall = yes` and `rainfall = no`. In other cases we might still want to account for underlying differences in our data by including a categorical variable we believe is having an influence but without caring about their identity. These variables are referred to *random effect* variables, as opposed to *fixed effect* variables that we considered so far. And models that include random and fixed effects are known as *mixed effect models* or *random effect models*.  

  - **Fixed effects** are (continuous or categorical) exploratory variables that we believe have an effect on the response and that we are interested in making conclusions about. Their effects is constant (fixed) across individuals.
  - **Random effects** are categorical variables with many levels that are themselves drawn from a population of possible levels. Although they are believed to have an influence on the response, we are not interested in their identity.

Here we only briefly touch upon mixed effect models and how to analyse them in R using the `lme4` package and by means of the `sleepstudy` dataset that is provided by `lme4`, which contains experimental data on the effect of sleep deprivation on reaction time. The data file has three variables

  - `Reaction`: average reaction time (ms)
  - `Days`: number of days of sleep deprivation
  - `Subject`: subject number on which observation was made

You can find out more about this study through the help function `?sleepstudy`. 


```r
# load library for mixed effect modelling
library(lme4)

# get a summary of the sleep study dataset
summary(sleepstudy)
```

```
##     Reaction          Days        Subject   
##  Min.   :194.3   Min.   :0.0   308    : 10  
##  1st Qu.:255.4   1st Qu.:2.0   309    : 10  
##  Median :288.7   Median :4.5   310    : 10  
##  Mean   :298.5   Mean   :4.5   330    : 10  
##  3rd Qu.:336.8   3rd Qu.:7.0   331    : 10  
##  Max.   :466.4   Max.   :9.0   332    : 10  
##                                (Other):120
```

```r
# get the number of study participants
print(paste0("Number of participants: ",length(unique(sleepstudy$Subject))))
```

```
## [1] "Number of participants: 18"
```

From the data summary we see that there were 10 observations made for 18 individuals. Therefore, `Subject` fits our definition of a *random effect`: we believe that there is a difference between study participants but we do not care about the individuals themselves.

We can convince ourselves about the difference between study participants by plotting the data for two subjects:

<img src="_main_files/figure-html/unnamed-chunk-183-1.png" style="display: block; margin: auto;" />
<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Recreate the above graph but for all individuals in the study.  </div></div>

<button id="displayTextunnamed-chunk-185" onclick="javascript:toggle('unnamed-chunk-185');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-185" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
sleepstudy %>%
    filter(Subject %in% c(308, 309)) %>%
    ggplot(aes(x = Days, y = Reaction)) +
    geom_line(col = 'red', linetype = 'dashed') +
    geom_point(size=2) +
    scale_x_continuous(breaks = 0:9) +  # make scale discrete
    facet_wrap(~Subject)
```

<img src="_main_files/figure-html/unnamed-chunk-523-1.png" style="display: block; margin: auto;" />
</div></div></div>

$~$

How do we model this data? There are principally three approaches: (1) pool all the data and don't care about individual-level differences, (2) add `Subject` as a fixed effect as well as the interaction term `Days:Subject`, and (3) treat `Subject` as a *random effect*. Here we are only going to compare (1) and (3) and leave (2) as an exercise.

Before we start we need to make some minor modification to the data. First, we want to make sure that `Subject` is being treated like a categorical and not a continuous variable. Second, the first two days (day 0 and day 1) were for adaptation and training, meaning that sleep deprivation started counting at day 2 so we discard the first two days and then recode to make sure we start with day 0. 


```r
sleep <- sleepstudy %>%
    mutate(Subject = factor(Subject)) %>%
    mutate(Days = Days - 2) %>%
    filter(Days>=0)
```

The `lmer()` function (from the `lme4` package) uses a very similar syntax as the by now familiar `lm()` function but where the model formula now takes on the form
<center> `response ~ fixed1 + fixed2 + ... + (ran1 + ran2 + ...| ran_factor1) + ...` </center>

That is, fixed effects (and their interactions) are entered exactly as before. New is the presence of the term `(ran1 + ran2 + ...| ran_factor1)`, which represents the random effects associated with a particular random factor. For our dataset there are three possibilities for how the random effects might influence the response, given here together with the specific formula syntax:

  - *random intercepts only*: `Response ~ Days + (1 | Subject)`
  - *random slopes only*: `Response ~ Days + (0 Days | Subject)`
  - *random slope and intersect*: `Response ~ Days + (Days | Subject)`

The most reasonable model would be the last, which allows for both the intercept and the slope to vary between individuals. So let's fit this model


```r
fit_mm <- lmer(Reaction ~ Days + (Days|Subject), data = sleep)
summary(fit_mm)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: Reaction ~ Days + (Days | Subject)
##    Data: sleep
## 
## REML criterion at convergence: 1404.1
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -4.0157 -0.3541  0.0069  0.4681  5.0732 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev. Corr
##  Subject  (Intercept) 958.35   30.957       
##           Days         45.78    6.766   0.18
##  Residual             651.60   25.526       
## Number of obs: 144, groups:  Subject, 18
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  267.967      8.266  32.418
## Days          11.435      1.845   6.197
## 
## Correlation of Fixed Effects:
##      (Intr)
## Days -0.062
```

The model summary now contains a lot more information. Let's highlight the two most important sections.

#### **Fixed effects** {-}

There are two fixed effects: `(Intercept)` and `Days` which tell us the average reaction time without any sleep deprivation and the increase in reaction time with each day of sleep deprivation. You will notice that compared to the simpler modelling framework, *P* values are not provided anymore, and there are various reasons as to why. However, if you wish to make statements regarding the statistical significance of these estimates, you can either look at the confidence intervals (based on parametric boostrapping)


```r
confint(fit_mm, level=0.95)
```

```
## Computing profile confidence intervals ...
```

```
##                   2.5 %      97.5 %
## .sig01       19.0979934  46.3366599
## .sig02       -0.4051073   0.8058951
## .sig03        4.0079284  10.2487351
## .sigma       22.4666029  29.3494509
## (Intercept) 251.3443396 284.5904989
## Days          7.7245247  15.1463328
```

The ones you are most interested in are the two bottom ones, and as neither crosses 0 you can be sure that the effects are statistically significant.

The other option is to calculate *P* values from the *t* values (the underlying maths goes beyon the scope of this workshop)


```r
tvals <- fixef(fit_mm) / sqrt(diag(vcov(fit_mm)))
2 * (1 - pnorm(abs(tvals)))
```

```
## (Intercept)        Days 
## 0.00000e+00 5.75197e-10
```

This again provides strong evidence for rejecting the null hypotheses that sleep deprivation does not effect reaction time.

#### **Random effects** {-}

This part of the summary looks more unfamiliar and explaining each part of this is beyond this workshop, as it requires more indepth knowledge about variance and covariance matrices and stats in general. So the only part you might want to take a look at is the `Variance` of the two `Groups` entries `Subject` and `Residual`. This tells you how much of the total variance in your data is being absorbed by the random effects (on slope and intercept). In this case this amounts to $\sim 61$% (100% * (958.35 + 45.78)/(958.35 + 45.78 + 651.60)), meaning that inter-subject variation explain the majority of the 'noise' in your data. 

If we are interested in the estimated random effects, these can be pulled out using `ranef()` (similar to `fixef()` for accessing estimates of the fixed effects)


```r
ranef(fit_mm) 
```

```
## $Subject
##     (Intercept)        Days
## 308  24.4992891   8.6020000
## 309 -59.3723102  -8.1277534
## 310 -39.4762764  -7.4292365
## 330   1.3500428  -2.3845976
## 331  18.4576169  -3.7477340
## 332  30.5270040  -4.8936899
## 333  13.3682027   0.2888639
## 334 -18.1583020   3.8436686
## 335 -16.9737887 -12.0702333
## 337  44.5850842  10.1760837
## 349 -26.6839022   2.1946699
## 350  -5.9657957   8.1758613
## 351  -5.5710355  -2.3718494
## 352  46.6347253  -0.5616377
## 369   0.9616395   1.7385130
## 370 -18.5216778   5.6317534
## 371  -7.3431320   0.2729282
## 372  17.6826159   0.6623897
## 
## with conditional variances for "Subject"
```

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 

  1. Fit a linear regression model to the pooled data ignoring the effect of `Subject` and compare the estimated effect sizes.
  2. Fit a linear regression model using `Subject` as a categorical fixed effect and compare the estimated effect sizes
  3. Fit a mixed effect model as before but assume that `Subject` only affects the intersect. How does this compare to the previous model with random slope and intersect?
 </div></div>

<br>

## Model checking

We need to be just as conscious of testing the assumptions of mixed effects models as we are with any other model. These assumptions include:

  1. Within-group errors are independent and normally distributed with mean zero and variance  
  2. Within-group errors are independent of the random effects
  3. Random effects are normally distributed with mean zero

Two commonly used plots to check these assumptions are:

  1. A simple plot of residuals against fitted values, irrespective of random effects (note we have to do this “by hand” here):
  
  ```r
  plot(fit_mm)
  ```
  
  <img src="_main_files/figure-html/unnamed-chunk-191-1.png" style="display: block; margin: auto;" />

  2. Plotting the residuals against the fitted values, separately for each level of the random effect, using the `coplot()` function:
  
  ```r
  coplot(resid(fit_mm) ~ fitted(fit_mm) | sleep$Subject)
  ```
  
  <img src="_main_files/figure-html/unnamed-chunk-192-1.png" style="display: block; margin: auto;" />

## Further reading 

Due to time constraints we cannot go into more details of *random* or *mixed effects models*. The interested reader will find the following (free) resources useful:

  - [Introduction to Linear Mixed Models](https://ourcodingclub.github.io/tutorials/mixed-models/)
  - [Beyond Multiple Linear Regression](https://bookdown.org/roback/bookdown-BeyondMLR/)
  - [Mixed Models with R](https://m-clark.github.io/mixed-models-with-R/random_intercepts.html)
  

<!--chapter:end:5-Mixed_effect_models.Rmd-->

# Generalised Linear Models (GLM)

In the previous part of this workshop we have seen that linear models are a powerful modelling tool. However, we have to remember that these rely on the following assumptions:

  1. A linear mean function is relevant
  2. Variances are equal across all predicted values of the response (homoscedatic)
  3. Errors are normally distributed
  4. Samples are collected at random
  5. Errors are independent
  
If assumptions 1–3 are violated we can transform our response variable to try and fix this. Common transforms include the log and power (sqrt) transforms but also Tukey’s ladder-of-powers, Box-Cox transformation, or Tukey and Mosteller’s bulging rule. Here is a toy example showing the effect of log transforming (artificial) data on the distribution of the residuals.

<img src="_main_files/figure-html/unnamed-chunk-193-1.png" style="display: block; margin: auto;" />

However, in a lot of other cases this is either not possible, for example when the output is binary, or we want to explicitly model the underlying distribution, e.g. if we are dealing with count data. In these cases we have to use **Generalised Linear Models (GLMs)** instead, which allow us to change the *error structure* of our data by using different *link functions*.

**Generalised Linear Models** have:

  1. a linear mean
  2. a **link function**
  3. an **error structure**

## Link functions

A link functions is equivalent to an "internal" transformation, which links the *mean* (regression) function (i.e. the usual $\beta_0 + \beta_1 x_1 + \beta_2 x_2 + ...$) to the *scale* of the *observed data*. Take for example one of our previous examples of data containing the number of malaria episodes an individual has experienced. There is nothing that constraints our regression model to produce negative values; these, however, are obviously nonsensical. Or, imagine you are interested whether some treatment improves patient outcome, where the response would be a yes or no (which in modelling terms is interpreted as 1 or 0). Again, there is nothing to constrain the model to produce values outside this [0,1] range. And this is what we mean by the *scale* of the *observed data*.

>**Note:** The simple linear regression model is a special case of a GLM, i.e. 

```r
lm(weight ~ height)
```
is equivalent to

```r
glm(weight ~ height, family=gaussian(link=identity))
```

Compared to the `lm()` function, the `glm()` function takes an extra argument `family`, which identifies the **error structure** and the **link function**. 

The default link function for the normal (Gaussian) error structure is the *identity* function (equivalent to no transformation). In fact, we often do not need to specify the link function explicitly and instead use the defaults for the various families. Commonly used error structures and associated link functions are (defaults highlighted in **bold**) 


|     Family      |                Link                |
|:---------------:|:----------------------------------:|
|   `gaussian`    |           **`identity`**           |
|   `binomial`    | **`logit`**, `probit` or `cloglog` |
|    `poisson`    |  **`log`**, `identity` or `sqrt`   |
|     `Gamma`     | **`inverse`**, `identity` or `log` |
| `quasibinomial` |            **`logit`**             |
| `quasipoisson`  |             **`log`**              |

Don't worry if this sounds confusing to you. We will go through this in more detail, or rather by means of worked out examples, when we deal with modelling two different types of data: count data and binary data.

$~$

## Poisson regression (for count data)

There are many occasions where we encounter count data. Count data have two main characteristics: (1) they are discrete (we cannot have, say, 2.3 occurrences or entities), and (2) are bound below by zero (we cannot have less than 0 occurrences or entities). This needs to be taken into consideration when we are trying to fit statistical models to count data. The probability distribution that has these required properties is the *Poisson distribution*, and this is the distribution *family* we will have to specify in our GLM.

### Background
Let’s consider a single explanatory variable and omit the indices $i$, the simple linear regression model is given as
$$
\begin{align}
Y &= \beta_0 + \beta_1 X + \epsilon\\
\epsilon &\sim \mathcal{N}(\mu,\sigma^2)
\end{align}
$$
which can be rewritten as 
$$
\begin{align}
Y &\sim \mathcal{N}(\mu,\sigma^2)\\
\mu &= \beta_0 + \beta_1 X
\end{align}
$$

Recall that the mean (regression) function is unconstrained, meaning that the value of $\beta_0 + \beta_1 X$ can range from $-\infty$ to $\infty$. This obviously violated the constraints of count data. Taking the logarithm of the mean transforms this range to $(0, \infty]$, which is what we are after. To to be consistent with the statistics literature we will rename $\mu$ to $\lambda$ and thus get the Poisson regression model as: 
$$
\begin{align}
Y &\sim Pois(\lambda)\\
\log \lambda &= \beta_0 + \beta_1 X
\end{align}
$$
Following the rules of logarithms:
$$
\begin{align}
\log \lambda &= \beta_0 + \beta_1 X \\
\lambda &= e^{\beta_0 + \beta_1 X}
\end{align}
$$
This means that we are effectively modelling the observed count data using an exponential mean function.

<br>

### Poisson regression in R

Now we know what is behind the Poisson model and understand what link functions do we can concentrate on how to perform Poisson regression in R. For this we use our previous malaria episodes example but with a slightly modified dataset, where we discard the effect of different transmission settings(EIR).


```r
# create random data points for age and EIR
Age <- runif(100, 2, 10)
Bednet <- sample(c('yes', 'no'), 100, replace = T)

# assume there is an interaction between age and bednet use, which influences the number of episodes
episodes <- round(exp(ifelse(Bednet=='no', 0.32*Age, 0.22*Age) + rnorm(100, 0, 0.3)))

# put into new data.frame
epiData <- data.frame(Age = Age, Episodes = episodes, Bednet = factor(Bednet))

# plot data
ggplot(epiData, aes(x = Age, y = Episodes, col = Bednet)) +
    geom_point() 
```

<img src="_main_files/figure-html/unnamed-chunk-197-1.png" style="display: block; margin: auto;" />

There is a clear relationship between age and the number of recorded episodes, and we might be tempted to fit a linear regression to this data. So let's do this and then add the regression lines to this graph.


```r
# fit the model wuth lm() and consider an interaction term 
fit <- lm(Episodes ~ Age*Bednet, data = epiData)

# make model predictions
newdata <- expand.grid(Age = seq(0,10,length.out=20),
                       Bednet = c('no', 'yes'))
newdata <- mutate(newdata, Bednet = factor(Bednet))
newdata$Episodes <- predict(fit, newdata = newdata)

ggplot(mapping = aes(x = Age, y = Episodes, col = Bednet)) +
    geom_point(data = epiData) +
    geom_line(data = newdata)
```

<img src="_main_files/figure-html/unnamed-chunk-198-1.png" style="display: block; margin: auto;" />

Now we can start to appreciate the problem with fitting a linear model to count data: the intersects (number of episodes at age 0) are both negative in this case, which is biologically not feasible.

We can also see from the model diagnostics that the residuals do follow the assumptions of a linear model, as there are clear signs of *heteroscedasticiy* (here indicated by an increasing variance with increasing values of the fitted response variable).


```r
# plot model diagnostics
plot(fit, which = 1)
```

<img src="_main_files/figure-html/unnamed-chunk-199-1.png" style="display: block; margin: auto;" />


Now we fit a GLM to the data instead, assuming a Poisson error structure and using the (default) log link function.


```r
# fit data using Poisson regression with default link function
fit_glm <- glm(Episodes ~ Age*Bednet, data = epiData, family = poisson(link = log))

# when using default link functions, we can also call
# fit_glm <- glm(Episodes ~ Age*Bednet, data = epiData, family = "poisson")

# get model summary
summary(fit_glm)
```

```
## 
## Call:
## glm(formula = Episodes ~ Age * Bednet, family = poisson(link = log), 
##     data = epiData)
## 
## Deviance Residuals: 
##      Min        1Q    Median        3Q       Max  
## -1.61302  -0.59601  -0.08364   0.38847   2.07668  
## 
## Coefficients:
##               Estimate Std. Error z value Pr(>|z|)    
## (Intercept)   -0.02768    0.15931  -0.174   0.8621    
## Age            0.34247    0.02024  16.919   <2e-16 ***
## Bednetyes     -0.15752    0.34519  -0.456   0.6482    
## Age:Bednetyes -0.08893    0.04355  -2.042   0.0412 *  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for poisson family taken to be 1)
## 
##     Null deviance: 524.198  on 99  degrees of freedom
## Residual deviance:  63.666  on 96  degrees of freedom
## AIC: 438.39
## 
## Number of Fisher Scoring iterations: 4
```

At a first glance, the model summary looks very similar to the one based on linear regression. However, instead of information regarding R-squared or the residual standard error, we now have information on the null and residual variance, as well as something called the *AIC*, which stands for the *Akaike Information Criterion* and is an estimator of prediction error that takes model complexity into account (for model selection we aim to minimise the AIC).

One thing we need to remember is that we are still working on the log-scale. That is, making a prediction based on our inferred model estimates relies on a back-transformation. For example, to obtain an estimate of the average number of episodes for a 5-year old sleeping under a bednet we have to calculate
<center> Episodes = exp(-0.0277 + 5 $\times$ 0.3425 - 0.1575 - 5 $\times$ 0.0889) = 2.952</center>

In reality we would use the `predict()` function for this. But beware, as we are dealing with a link function that is not the *identity* function, we need to set an extra argument `type = 'response'` to back-transform the predicted values to the scale of our response variable.


```r
# make model predictions
newdata$Episodes <- predict(fit_glm, newdata = newdata, type='response')

ggplot(mapping = aes(x = Age, y = Episodes, col = Bednet)) +
    geom_point(data = epiData) +
    geom_line(data = newdata)
```

<img src="_main_files/figure-html/unnamed-chunk-201-1.png" style="display: block; margin: auto;" />

This looks like a much better fit to the data and also satisfies the necessary condition of a non-negative intersect.

$~$

## Logistic regression (for binary data)

So far we have  considered continuous and discrete data as the response variables. What if our response is a categorical variable, such as successful treatment / treatment failure or infected / protected? In this case we can model the probability *p* of being in one class or another as a function of the explanatory variables. Here we will only consider **binary** response data, i.e. where the response is one of two types. In this case we talk about binomial or simply *logistic regression*. Cases where the outcome has more than two levels we talk about multinomial regression; this, however, will not be considered here.

### Background

Recall the previous case of dealing with count data. We noted that the mean function $\beta_0 + \beta_1 X$ is unconstrained and thus needs to undergo internal transformation to make sure it fit the characteristic of count data. For a binary outcome, the restriction on the modelled response is that is needs to be within the range [0,1] because we are dealing with probabilities. A probability distribution that works for this is the **Bernouille distribution**, which has the following characteristics
$$ Y \sim \mathcal{Bern}(P) $$

  - binary variable, taking the values 0 or 1 (yes/no, pass/fail)
  - a probability parameter, $p$, where $0<p<1$
  - mean = $p$
  - variance = $p(1-p)$

Remember that for the case of count data (Poisson regression), we took the exponential of the mean function, or rather modelled the modeled the logarithm of the response. In the case of binary data, we are trying to model the probability, which has values between 0 and 1. Note that the possible range of $p/(1-p)$ is $(0,\infty)$, such that $\log p/(1-p) \in (-\infty,\infty)$, which is exactly what we want. This function is called **logit** and also known as **log odds**. Our regression model therefore becomes 

$$ 
\begin{align}
Y &\sim \mathcal{Bern}(P) \\
\log\left(\frac{p}{1-p}\right) &= \beta_0 + \beta_1 X
\end{align}
$$
Again, note that we are still fitting straight lines through our data, but this time in the log odds space. As a shorthand notation we write $\log\left(\frac{p}{1-p}\right) = \text{logit}(p) = \beta_0 + \beta_1 X$.

<br>

### Logistic regression in R

In order to show how to perform logistic regression we will use Haberman's Survival Data, which contains data from a study conducted between 1958 and 1970 at the University of Chicago’s Billings Hospital on the survival of patients who had undergone surgery for breast cancer. Our dataset contains data from 306 patients and has four columns:

  1. `Age`: age of the patient at the time of the operation 
  2. `Year`: year of the operation
  3. `Nodes`: number of positive axillary nodes detected
  4. `Survivial`: survival status (1 = survived for more than 5 years, 2 = died within 5 years)


```r
haberman <- read.csv('haberman.csv')
head(haberman)
```

```
##   Age Year Nodes Survival
## 1  30 1964     1        1
## 2  30 1962     3        1
## 3  30 1965     0        1
## 4  31 1959     2        1
## 5  31 1965     4        1
## 6  33 1958    10        1
```

As you will notice, `Survival` is currently treated like a numerical variable, so the first thing we need to do is turn this into a categorical one, which indicates whether the patient survived for more than 5 years or not


```r
haberman <- mutate(haberman, Survival = factor(ifelse(Survival==1, 'yes', 'no')))
```

Our intuition would be that the predictor variables of interest are `Age` and `Nodes`; so let's see how they relate with survival. 

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Plot the distribution of `Age` and `Nodes` stratified by `Survival`. </div></div>

<button id="displayTextunnamed-chunk-205" onclick="javascript:toggle('unnamed-chunk-205');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-205" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

**Option 1:** histograms

```r
p1 <- ggplot(haberman, aes(x = Age, col = Survival)) +
    geom_histogram(bins = 10, alpha = 0.7) +
    facet_wrap(~Survival) +
    theme(legend.position = '')

p2 <- ggplot(haberman, aes(x = Nodes, col = Survival)) +
    geom_histogram(binwidth = 1, alpha = 0.7) +
    facet_wrap(~Survival) +
    theme(legend.position = '')

p1 / p2
```

<img src="_main_files/figure-html/unnamed-chunk-549-1.png" style="display: block; margin: auto;" />

**Option 2:** box-and-whisker plots

```r
p1 <- ggplot(haberman, aes(y = Age, x = Survival, fill = Survival)) +
    geom_boxplot(alpha = 0.7) +
    theme(legend.position = '')

p2 <- ggplot(haberman, aes(y = Nodes, x = Survival, fill = Survival)) +
    geom_boxplot(alpha = 0.7) +
    theme(legend.position = '')

p1 + p2
```

<img src="_main_files/figure-html/unnamed-chunk-550-1.png" style="display: block; margin: auto;" />
</div></div></div>

$~$

From these graphs it is difficult to say if and by how much these variables had an influence on patient survival. But we cannot always trust our eyes so we are going to test this statistically by means of logistic regression. The syntax should be very familiar to you by now. In fact, the only argument we need to change from the previous GLM is to set the family to `binomial` and the link to `logit` (although this is not strictly necessary as it is the default link for this family).


```r
fit_bin <- glm(Survival ~ Age + Nodes, data = haberman, family = binomial(link='logit'))
summary(fit_bin)
```

```
## 
## Call:
## glm(formula = Survival ~ Age + Nodes, family = binomial(link = "logit"), 
##     data = haberman)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -1.9741  -0.9178   0.6547   0.7302   2.3361  
## 
## Coefficients:
##             Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  2.46290    0.70643   3.486  0.00049 ***
## Age         -0.01965    0.01269  -1.549  0.12144    
## Nodes       -0.08832    0.01982  -4.456 8.34e-06 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 353.69  on 305  degrees of freedom
## Residual deviance: 328.31  on 303  degrees of freedom
## AIC: 334.31
## 
## Number of Fisher Scoring iterations: 4
```

This suggests that patient age is not a statistically significant predictor of patient survival. We can also test this directly by comparing models with and without this predictor using `anova`


```r
fit_bin_b <- glm(Survival ~ Nodes, data = haberman, family = binomial(link='logit'))
anova(fit_bin, fit_bin_b, test = "Chisq")
```

```
## Analysis of Deviance Table
## 
## Model 1: Survival ~ Age + Nodes
## Model 2: Survival ~ Nodes
##   Resid. Df Resid. Dev Df Deviance Pr(>Chi)
## 1       303     328.31                     
## 2       304     330.72 -1  -2.4132   0.1203
```

This confirms that there is no statistical significant effect of Age, so we will drop this explanatory variable and proceed with the less complex model. Let's have a look at the model summary


```r
summary(fit_bin_b)
```

```
## 
## Call:
## glm(formula = Survival ~ Nodes, family = binomial(link = "logit"), 
##     data = haberman)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -1.8058  -0.9505   0.6602   0.6861   2.2845  
## 
## Coefficients:
##             Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  1.41250    0.16297   8.667  < 2e-16 ***
## Nodes       -0.08577    0.01955  -4.387 1.15e-05 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 353.69  on 305  degrees of freedom
## Residual deviance: 330.72  on 304  degrees of freedom
## AIC: 334.72
## 
## Number of Fisher Scoring iterations: 4
```

How do we interpret the model summary, and in particular the variable estimates. Remember that we are now working on the logit scale, and to make predictions about the probability of a patient surviving for more than 5 years we have to use the back-transform
$$
\begin{align}
\text{logit } p &= \beta_0 + \beta_1 X \\
\Rightarrow p &= \text{logit}^{-1} \beta_0 + \beta_1 X = \frac{e^{\beta_0 + \beta_1 X}}{1 + e^{\beta_0 + \beta_1 X}}
\end{align} \\
$$

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 

  1. Calculate the probability of survivial for a patient with 3 positive axillery nodes. 
  2. Calculate the decrease in the probability of survival for one additional positive node.
 </div></div>

<button id="displayTextunnamed-chunk-210" onclick="javascript:toggle('unnamed-chunk-210');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-210" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

1. The probability of survivial for a patient with 3 positive axillery nodes

```r
lin_mean <- exp(fit_bin_b$coefficients[[1]] + 3*fit_bin_b$coefficients[[2]])
p <- lin_mean / (1 + lin_mean)
print(p)
```

```
## [1] 0.7604547
```

2. The decrease in survivial probability for one additional positive axillery node

```r
p1 <- predict(fit_bin_b, newdata = data.frame(Nodes = 3), type = 'response')
p2 <- predict(fit_bin_b, newdata = data.frame(Nodes = 4), type = 'response')
round(p2-p1,4)
```

```
##      1 
## -0.016
```
</div></div></div>

$~$

The next thing we would like do is to plot the regression line. As before this involves making a new dataset for prediction and then add this to our graph of survival vs. nodes. Also, we need to make sure that the original response variable (`Survival`) is projected onto the same probability scale 0 to 1. 


```r
newdata <- data.frame(Nodes = seq(min(haberman$Nodes), max(haberman$Nodes)))
newdata$pSurvival <- predict(fit_bin_b, newdata = newdata, type = 'response')

haberman2 <- mutate(haberman, pSurvival = ifelse(as.numeric(Survival)==1, 1, 0))

ggplot(mapping = aes(x = Nodes, y = pSurvival)) +
    geom_point(data = haberman2, aes(col = Survival)) +
    geom_line(data = newdata)
```

<img src="_main_files/figure-html/unnamed-chunk-211-1.png" style="display: block; margin: auto;" />

### Odds ratios {-}
Another, and sometimes more and sometimes less intuitive interpretation of the coefficients of a logistic regression model is in terms of **odds ratios**:

**Odds:**
$$ \frac{P(\text{event happens})}{P(\text{event does not happen})} = \frac{P(\text{event happens})}{1 - P(\text{event happens})}$$

**Odds ratio:**
$$ \frac{\text{odds in one group}}{\text{odds in another group}} $$

From the previous task we could for example calculate the odds ratio (of survival) in individuals with 3 detected nodes compared to 2 detected nodes, which will leave to the interested reader to work out. It turns out that if you take the log of the odds ratio you will recover $\beta_1$, i.e. $e^{\beta_1}$ is the odds ratio for a unit increase.

As mentioned earlier, odds ratio are tricky to understand but generally make more sense and are easier to interpret for categorical variable than for numerical ones.



<div class="panel panel-default"><div class="panel-heading"> Practical </div><div class="panel-body"> 
Download the titanic dataset (titanic.csv), which contains data of over 800 passengers of the [Titanic](https://en.wikipedia.org/wiki/Titanic) together with information on whether they survived or not (0 and 1, respectively), their age, sex, passenger class, the fare they paid and whether they had siblings/spouse or children/parents on board. Perform a full logistic regression analysis (survival yes/no). </div></div>

<button id="displayTextunnamed-chunk-213" onclick="javascript:toggle('unnamed-chunk-213');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-213" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">
There are plenty of way this dataset can and should be analyed. Here we just show one example for a logistic regression analysis examining the survival probability as dependent on sex and age and their interaction.

```r
titanic <- read.csv('titanic.csv')

fit <- glm(Survived ~ Age * Sex, data = titanic, family = "binomial")
summary(fit)
```

```
## 
## Call:
## glm(formula = Survived ~ Age * Sex, family = "binomial", data = titanic)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -2.0256  -0.6891  -0.5904   0.7653   2.2467  
## 
## Coefficients:
##             Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  0.41192    0.28211   1.460 0.144254    
## Age          0.02423    0.00980   2.472 0.013437 *  
## Sexmale     -1.28930    0.37615  -3.428 0.000609 ***
## Age:Sexmale -0.04376    0.01265  -3.459 0.000541 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 1182.77  on 886  degrees of freedom
## Residual deviance:  903.49  on 883  degrees of freedom
## AIC: 911.49
## 
## Number of Fisher Scoring iterations: 4
```

```r
newdata <- data.frame(Age = rep(seq(min(titanic$Age), max(titanic$Age), length.out = 50),2),
                      Sex = rep(c('male', 'female'), each = 50))
newdata$Survived <- predict(fit, newdata = newdata, type = 'response')

ggplot(mapping = aes(x = Age, y = Survived, col = Sex)) +
    geom_point(data = titanic) +
    geom_line(data = newdata)
```

<img src="_main_files/figure-html/unnamed-chunk-569-1.png" style="display: block; margin: auto;" />
</div></div></div>

<!--chapter:end:6-Generalised_linear_models.Rmd-->

# Survival Analysis 

In the previous section we have learned how logistic regression can be used to analyse the influence of some factors (i.e. explanatory variables) on an observed event (the response variable). One example was how the number of positive detected anxillary nodes affected the probability of survival of cancer patients. Other studies, in particular clinical studies, are often more concerned with *when* an event happens and, relatedly, how specific covariates may influence the *time-to-event*. For example, how does treatment A affect the time to disease clearance compared to treatment B. This type of data requires a different analytic approach and is the subject of *survival analysis*.

Note, this part of our workshop was partially adapted from the excellent [Survival Analysis in R](https://www.emilyzabor.com/tutorials/survival_analysis_in_r_tutorial.html#Calculating_survival_times) tutorial by Emily C. Zabor, which also covers different methods and advanced topics than those briefly introduced here. 


## Terminology and notation 

Before we go into details on how to conduct survival analysis in R, we need to clarify some of the common notations and terminologies.

### Censoring

An important concept in survival analysis is *censoring*. Survival times are often incompletely determined for some individuals, for example because of withdrawal, loss to follow-up or the study ended before the event occurred. These are examples of *right censoring*. There are also **left censored** data, for example when an event happened before the study started, and **interval censored** data, for when we know that an event happened within a certain time interval but we are not exactly sure when. Including censored data in our analysis is important as they still provide important information and make our inferences more reliable. 

In this workshop we are only concerned with right censored data, and an example of how this might look like is given here

<img src="_main_files/figure-html/unnamed-chunk-214-1.png" style="display: block; margin: auto;" />
We could ask the question, what is the proportion of individuals who were event-free by day 6. We know that patients 5 and 7 experienced an event and that patients 2, 3, 4 and 8 did not experience an event by day 6. Patients 1 and 6, on the other hand, may have left the study before day 6. However, we do have some information about them, which is that they did not experience the event for a certain period of time, and we can use this information for our analysis. 

>**Note:** A key assumption about censoring is that it is non-informative about the event. That is, the censoring is caused by something other than the impending event.

### Survival and hazard functions

There are two related probabilities are used to describe survival data: the *survival probability* $S(t)$ and the *hazard probability* $h(t)$.

#### **Survival function** {-}

The survival probability, also known as the survival function $S(t)$, is the probability that an individual will survive beyond any given specified time $$ S(t) = Pr(T > t) = 1 − F(t) $$ with $F(t) = Pr(t \leq T)$ being the cumulative distribution function and seen as the compliment of the survival function. 

The survival function has the following properties:

  - it is not increasing
  - at time $t=0$, $S(t)=1$
  - at time $t=\infty$, $S(t)=0$

Note, as we usually measure time in discrete units, e.g days or years, the survival function is often discrete in practice.

#### **Hazard function** {-}

The hazard function, $h(t)$, describes the *hazard* at time $t$. It is the probability that an event occurs in the
neighborhood of time $t$ divided by the probability that the subject is alive at that time. It is a bit more difficult to illustrate because it measures the instantaneous risk of an event. However, we need the hazard function to consider  *covariates* when we compare survival of patient groups at a later section. 


### Calculating survival times in R

Datasets often do not readily contain survival times, or time-to-event, but rather have information of the start and end of the study or date of the event. Here, by means of an illustrative example, we briefly show you how to deal with dates in R. Imagine you had the following data, where we deliberately have two different date formats.


```r
trialDF <- data.frame(
    enrolled = c("2017-05-02", "2017-05-03", "2017-05-17"),  # date patient was enrolled in study
    last_fup = c("15/4/18", "4/7/18", "31/10/18"))   # date of last follow-up

head(trialDF)
```

```
##     enrolled last_fup
## 1 2017-05-02  15/4/18
## 2 2017-05-03   4/7/18
## 3 2017-05-17 31/10/18
```
You can see that the dates are currently in character format. The next step it to transform them into a date format, which we need to calculate the survival times.


```r
trialDF <- trialDF %>% 
    mutate(enrolled = as.Date(enrolled, format = "%Y-%m-%d"),
           last_fup = as.Date(last_fup, format = "%d/%m/%y"))

head(trialDF)
```

```
##     enrolled   last_fup
## 1 2017-05-02 2018-04-15
## 2 2017-05-03 2018-07-04
## 3 2017-05-17 2018-10-31
```

Now that we have the dates in the right format we can calculate the survival time simply by subtracting the enrollment date from the last follow-up date 


```r
trialDF$Surv_time <- as.numeric(trialDF$last_fup - trialDF$enrolled)

head(trialDF)
```

```
##     enrolled   last_fup Surv_time
## 1 2017-05-02 2018-04-15       348
## 2 2017-05-03 2018-07-04       427
## 3 2017-05-17 2018-10-31       532
```

### R libraries and example data

To implement survival analysis in R, we will make use of the `survival` and `survminer` packages, which provide all the necessary functionalities for our purposes. Also, we will use the `ovarian` dataset, that comes with the `survival` package and contains data on survival of 26 patients in a randomised trial comparing two treatments for ovarian cancer. It contains the following 6 variables:

  - `futime`: survival or censoring time
  - `fustat`: censoring status
  - `age`: in years
  - `resid.ds`: residual disease present (1=no, 2=yes)
  - `rx`: treatment group
  - `ecog.ps`: ECOG performance status (1 is better)


```r
library(survival)
library(survminer)

ovarianDF <- ovarian
head(ovarianDF)
```

```
##   futime fustat     age resid.ds rx ecog.ps
## 1     59      1 72.3315        2  1       1
## 2    115      1 74.4932        2  1       1
## 3    156      1 66.4658        2  1       2
## 4    421      0 53.3644        2  2       1
## 5    431      1 50.3397        2  1       1
## 6    448      0 56.4301        1  1       2
```

For downstream analysis we need to transform a few of these variables to the right format, i.e. from numeric to categorical


```r
ovarianDF <- ovarianDF %>%
    mutate(resid.ds = factor(resid.ds, labels = c('no', 'yes')),
           rx = factor(rx, labels = c('treatment A', 'treatment B')),
           ecog.ps = factor(ecog.ps))
```


## Kaplan-Meier

The (non-parametric) Kaplan-Meier method is the most common way to estimate survival probabilities from observed survival times. Using discrete times $t_i$, the survival probability at $t_i$, $S(t_i)$ can be calculated as
$$ S(t_i) = S(t_{i-1})\left(1 - \frac{d_i}{n_i}\right) $$
with

  - $S(t_{i-1})$ : the probability of being alive (or not having experienced the event) at time $t_{i-1}$
  - $n_i$: number of individuals alive just before $t_i$
  - $d_i$: number of events at $t_i$
  - $t_0=0, \, S(t_0)=1$

and results in a step function, where there is a step down each time an event occurs.

To implement this in R we first have to create a *survival object*, which is done by the `Surv()` function of the `survival` package.


```r
survObj <- Surv(time = ovarianDF$futime, event = ovarianDF$fustat)
survObj
```

```
##  [1]   59   115   156   421+  431   448+  464   475   477+  563   638   744+
## [13]  769+  770+  803+  855+ 1040+ 1106+ 1129+ 1206+ 1227+  268   329   353 
## [25]  365   377+
```

As you can see, some survival times are followed by a '+', which indicates that these individuals were censored. The next step is to fit the Kaplan-Meier curves, which is done by passing the `survObj` to the `survfit()` function and can be done in a stratified way, for example by treatment group (`rx`)


```r
sfit <- survfit(survObj ~ rx, data = ovarianDF)
summary(sfit)
```

```
## Call: survfit(formula = survObj ~ rx, data = ovarianDF)
## 
##                 rx=treatment A 
##  time n.risk n.event survival std.err lower 95% CI upper 95% CI
##    59     13       1    0.923  0.0739        0.789        1.000
##   115     12       1    0.846  0.1001        0.671        1.000
##   156     11       1    0.769  0.1169        0.571        1.000
##   268     10       1    0.692  0.1280        0.482        0.995
##   329      9       1    0.615  0.1349        0.400        0.946
##   431      8       1    0.538  0.1383        0.326        0.891
##   638      5       1    0.431  0.1467        0.221        0.840
## 
##                 rx=treatment B 
##  time n.risk n.event survival std.err lower 95% CI upper 95% CI
##   353     13       1    0.923  0.0739        0.789        1.000
##   365     12       1    0.846  0.1001        0.671        1.000
##   464      9       1    0.752  0.1256        0.542        1.000
##   475      8       1    0.658  0.1407        0.433        1.000
##   563      7       1    0.564  0.1488        0.336        0.946
```

From the summary we can see, amongst other things, survival times, the number of patients at risk, the proportion of surviving patients at every time point and the associated confidence intervals. 

Plotting survival curves is equally easy and done by passing the fitted Kaplan-Meier curves to `ggsurvplot()`


```r
ggsurvplot(sfit, data = ovarianDF, pval = T) 
```

<img src="_main_files/figure-html/unnamed-chunk-222-1.png" style="display: block; margin: auto;" />

The vertical lines indicate the time when censoring occurred and the $P$ value corresponds to a log-rank test, which here indicates that there is non-significant difference between the survival curves for the two different treatment arms, even though patients receiving treatment B appear to be doing better in the first few months of follow-up. 

Note, the log-rank test is a widely used method for comparing survival curves. It is a non-parametric test (i.e. it makes no assumptions about the survival distributions) and compares the observed number of events in each group to the expectation that the null hypothesis (the survival curves are identical) is true. We can get the statistic using the `survdiff()` function as follow:


```r
survdiff(survObj ~ rx, data = ovarianDF)
```

```
## Call:
## survdiff(formula = survObj ~ rx, data = ovarianDF)
## 
##                 N Observed Expected (O-E)^2/E (O-E)^2/V
## rx=treatment A 13        7     5.23     0.596      1.06
## rx=treatment B 13        5     6.77     0.461      1.06
## 
##  Chisq= 1.1  on 1 degrees of freedom, p= 0.3
```

which is exactly what has been added to the graph above.

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Redo the analysis but this time stratified by residual disease status (`resid.ds`). </div></div>

<button id="displayTextunnamed-chunk-225" onclick="javascript:toggle('unnamed-chunk-225');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-225" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
sfit2 <- survfit(survObj ~ resid.ds, data = ovarianDF)
ggsurvplot(sfit2, data = ovarianDF, pval = T) 
```

<img src="_main_files/figure-html/unnamed-chunk-585-1.png" style="display: block; margin: auto;" />

Although the $P$ value does not suggest significance at the 0.05 level, the curves clearly diverge early. One could therefore argue that a follow-up study with an increased sample size could validate that patients with negative residual disease status have a better prognosis compared to patients with residual disease.</div></div></div>

<br>

Note, the `ggsurvplot()` function provides a lot more tools to produce highly customised and informative outputs, as shown in the two examples below. As always, please refer to the help function (`?ggsurvplot()`) or the [online version](https://www.rdocumentation.org/packages/survminer/versions/0.4.9/topics/ggsurvplot) for full details.


```r
ggsurvplot(sfit,
           pval = TRUE,  # Add P value (log-rank test)
           pval.size = 4, # Size of P value
           conf.int = TRUE,  # Plot confidence intervals
           risk.table = TRUE, # Add risk table
           risk.table.col = "strata", # Change risk table color by groups
           linetype = "strata", # Change line type by groups
           ggtheme = theme_bw(base_size = 12), # Change ggplot2 theme
           palette = c("darkgreen", "orange"), # Change colour of strata
           xlab = 'Time (days)',  # Change label of x-axis
           legend.title = 'Treatment', # Change title of the legend
           legend.labs = c('A', 'B'))  # Change the name of the legend labels
```

<img src="_main_files/figure-html/unnamed-chunk-226-1.png" style="display: block; margin: auto;" />


```r
ggsurvplot(sfit,
           fun = "event", # Plot cumulative events
           conf.int = TRUE,  # Plot confidence intervals
           ncensor.plot = TRUE, # Plot the number of censored subjects at time t
           linetype = "strata", # Change line type by groups
           ggtheme = theme_classic(base_size = 12), # Change ggplot2 theme
           palette = c("darkgreen", "orange"), # Change colour of strata
           xlab = 'Time (days)',  # Change label of x-axis
           legend.title = 'Treatment', # Change title of the legend
           legend.labs = c('A', 'B'))  # Change the name of the legend labels
```

<img src="_main_files/figure-html/unnamed-chunk-227-1.png" style="display: block; margin: auto;" />

### **Median survival time**

We can calculate the median survival time, which corresponds to a survival probability of 0.5, directly from the `survfit` object. This is shown here for unstratified data, i.e. we ignore the two different treatment regimes (note the change in formula)


```r
survfit(survObj ~ 1, data = ovarianDF)
```

```
## Call: survfit(formula = survObj ~ 1, data = ovarianDF)
## 
##       n events median 0.95LCL 0.95UCL
## [1,] 26     12    638     464      NA
```

which we can also indicate on the graph


```r
ggsurvplot(survfit(survObj ~ 1, data = ovarianDF),
           conf.int = TRUE,
           risk.table = TRUE,
           surv.median.line = "hv", # specify horizontal and vertical line
           xlab = 'Time (days)',
           legend = 'none')
```

<img src="_main_files/figure-html/unnamed-chunk-229-1.png" style="display: block; margin: auto;" />

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Calculate the median survival times stratfied by residual disease status, what do you notice? </div></div>


<button id="displayTextunnamed-chunk-231" onclick="javascript:toggle('unnamed-chunk-231');">Show: Solution</button>

<div id="toggleTextunnamed-chunk-231" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
survfit(survObj ~ resid.ds, data = ovarianDF)
```

```
## Call: survfit(formula = survObj ~ resid.ds, data = ovarianDF)
## 
##               n events median 0.95LCL 0.95UCL
## resid.ds=no  11      3     NA     638      NA
## resid.ds=yes 15      9    464     329      NA
```

The `NA` indicates that we do not have enough data to robustly infer median survival times. A larger study would help remedy this problem.</div></div></div>

$~$

## Cox regression model

As we have seen, the Kaplan-Meier method is an easy way to compare survival data for different strata (e.g. treatment arms). However, this is restricted to categorical covariates. What we might want instead is a way to infer the effect of one or more different covariates, or explanatory variables. This is where Cox regression, or Cox proportional hazard analysis comes into play.

The Cox regression model is a (semi-parametric) model that allows us to fit uni- and multi-variable regression models that have survival outcomes. They are defined as
$$ h(t|X_i) = h_0(t) e^{\beta_1 X_{i1}+ ... + \beta_p X_{ip}} $$
with $h(t)$ being the *hazard*, or the instantaneous rate at which an events occur, and $h_0(t)$ being the underlying baseline hazard.

Without going deeper into the mathematical details, here we show how to fit Cox proportional hazard models to survival data using the `coxph()` function, which takes a survival object as the response variable and otherwise follows common syntax for regression models as we have used before. Here we are interested in the effect of all four covariates: `age`, `rx`, `resid.ds` and `ecog.ps`


```r
# fit cox proportional hazard ratio
cph <- coxph(survObj ~ age + rx + resid.ds + ecog.ps, data = ovarianDF)

# get model summary
summary(cph)
```

```
## Call:
## coxph(formula = survObj ~ age + rx + resid.ds + ecog.ps, data = ovarianDF)
## 
##   n= 26, number of events= 12 
## 
##                   coef exp(coef) se(coef)      z Pr(>|z|)   
## age            0.12481   1.13294  0.04689  2.662  0.00777 **
## rxtreatment B -0.91450   0.40072  0.65332 -1.400  0.16158   
## resid.dsyes    0.82619   2.28459  0.78961  1.046  0.29541   
## ecog.ps2       0.33621   1.39964  0.64392  0.522  0.60158   
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
##               exp(coef) exp(-coef) lower .95 upper .95
## age              1.1329     0.8827    1.0335     1.242
## rxtreatment B    0.4007     2.4955    0.1114     1.442
## resid.dsyes      2.2846     0.4377    0.4861    10.738
## ecog.ps2         1.3996     0.7145    0.3962     4.945
## 
## Concordance= 0.807  (se = 0.068 )
## Likelihood ratio test= 17.04  on 4 df,   p=0.002
## Wald test            = 14.25  on 4 df,   p=0.007
## Score (logrank) test = 20.81  on 4 df,   p=3e-04
```

The model summary looks slightly different to the ones we have come across before. Of interest here are the regression coefficients `coef` and `exp(coef)` and their associated $P$ values. From the output above we can conclude that 

  - age has statistically significant effect on survival probability, whereas the effects of treatment, residual disease status or ECOG performance status are not significant
  - age, residual disease and ECOG performance have *positive* (beta) coefficients, indicating that they are associated with *poorer* survival
  - treatment B has a *negative* (beta) coefficient, indicating that it is associated with *better* survival
  
Note, the quantity `exp(coef)` is known as the **hazard ratio (HR)**. It is best explained for categorical predictors, where it represents the ratio hazard between two groups at any point in time. A hazard ratio of HR>1 indicates increased hazard of an event, whereas HR<1 indicates a lower hazard. From the example above, the HR for treatment B was 0.4, which means that individuals in treatment group B had a 0.4 times lower rate of dying at any given time.

We can extract the regression results and put them into a nice table format using the `tbl_regression()` function from the `gtsummary` library


```r
gtsummary::tbl_regression(cph, exp=TRUE)
```

```{=html}
<div id="fmanrdmbpk" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>#fmanrdmbpk table {
  font-family: system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#fmanrdmbpk thead, #fmanrdmbpk tbody, #fmanrdmbpk tfoot, #fmanrdmbpk tr, #fmanrdmbpk td, #fmanrdmbpk th {
  border-style: none;
}

#fmanrdmbpk p {
  margin: 0;
  padding: 0;
}

#fmanrdmbpk .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#fmanrdmbpk .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#fmanrdmbpk .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#fmanrdmbpk .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#fmanrdmbpk .gt_heading {
  background-color: #FFFFFF;
  text-align: center;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#fmanrdmbpk .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#fmanrdmbpk .gt_col_headings {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#fmanrdmbpk .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#fmanrdmbpk .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#fmanrdmbpk .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#fmanrdmbpk .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#fmanrdmbpk .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#fmanrdmbpk .gt_spanner_row {
  border-bottom-style: hidden;
}

#fmanrdmbpk .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#fmanrdmbpk .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#fmanrdmbpk .gt_from_md > :first-child {
  margin-top: 0;
}

#fmanrdmbpk .gt_from_md > :last-child {
  margin-bottom: 0;
}

#fmanrdmbpk .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#fmanrdmbpk .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#fmanrdmbpk .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#fmanrdmbpk .gt_row_group_first td {
  border-top-width: 2px;
}

#fmanrdmbpk .gt_row_group_first th {
  border-top-width: 2px;
}

#fmanrdmbpk .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#fmanrdmbpk .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#fmanrdmbpk .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#fmanrdmbpk .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#fmanrdmbpk .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#fmanrdmbpk .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#fmanrdmbpk .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#fmanrdmbpk .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#fmanrdmbpk .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#fmanrdmbpk .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#fmanrdmbpk .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#fmanrdmbpk .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#fmanrdmbpk .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#fmanrdmbpk .gt_left {
  text-align: left;
}

#fmanrdmbpk .gt_center {
  text-align: center;
}

#fmanrdmbpk .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#fmanrdmbpk .gt_font_normal {
  font-weight: normal;
}

#fmanrdmbpk .gt_font_bold {
  font-weight: bold;
}

#fmanrdmbpk .gt_font_italic {
  font-style: italic;
}

#fmanrdmbpk .gt_super {
  font-size: 65%;
}

#fmanrdmbpk .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#fmanrdmbpk .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#fmanrdmbpk .gt_indent_1 {
  text-indent: 5px;
}

#fmanrdmbpk .gt_indent_2 {
  text-indent: 10px;
}

#fmanrdmbpk .gt_indent_3 {
  text-indent: 15px;
}

#fmanrdmbpk .gt_indent_4 {
  text-indent: 20px;
}

#fmanrdmbpk .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" scope="col" id="&lt;strong&gt;Characteristic&lt;/strong&gt;"><strong>Characteristic</strong></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="&lt;strong&gt;HR&lt;/strong&gt;&lt;span class=&quot;gt_footnote_marks&quot; style=&quot;white-space:nowrap;font-style:italic;font-weight:normal;&quot;&gt;&lt;sup&gt;1&lt;/sup&gt;&lt;/span&gt;"><strong>HR</strong><span class="gt_footnote_marks" style="white-space:nowrap;font-style:italic;font-weight:normal;"><sup>1</sup></span></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="&lt;strong&gt;95% CI&lt;/strong&gt;&lt;span class=&quot;gt_footnote_marks&quot; style=&quot;white-space:nowrap;font-style:italic;font-weight:normal;&quot;&gt;&lt;sup&gt;1&lt;/sup&gt;&lt;/span&gt;"><strong>95% CI</strong><span class="gt_footnote_marks" style="white-space:nowrap;font-style:italic;font-weight:normal;"><sup>1</sup></span></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_center" rowspan="1" colspan="1" scope="col" id="&lt;strong&gt;p-value&lt;/strong&gt;"><strong>p-value</strong></th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="label" class="gt_row gt_left">age</td>
<td headers="estimate" class="gt_row gt_center">1.13</td>
<td headers="ci" class="gt_row gt_center">1.03, 1.24</td>
<td headers="p.value" class="gt_row gt_center">0.008</td></tr>
    <tr><td headers="label" class="gt_row gt_left">rx</td>
<td headers="estimate" class="gt_row gt_center"><br /></td>
<td headers="ci" class="gt_row gt_center"><br /></td>
<td headers="p.value" class="gt_row gt_center"><br /></td></tr>
    <tr><td headers="label" class="gt_row gt_left">    treatment A</td>
<td headers="estimate" class="gt_row gt_center">—</td>
<td headers="ci" class="gt_row gt_center">—</td>
<td headers="p.value" class="gt_row gt_center"><br /></td></tr>
    <tr><td headers="label" class="gt_row gt_left">    treatment B</td>
<td headers="estimate" class="gt_row gt_center">0.40</td>
<td headers="ci" class="gt_row gt_center">0.11, 1.44</td>
<td headers="p.value" class="gt_row gt_center">0.2</td></tr>
    <tr><td headers="label" class="gt_row gt_left">resid.ds</td>
<td headers="estimate" class="gt_row gt_center"><br /></td>
<td headers="ci" class="gt_row gt_center"><br /></td>
<td headers="p.value" class="gt_row gt_center"><br /></td></tr>
    <tr><td headers="label" class="gt_row gt_left">    no</td>
<td headers="estimate" class="gt_row gt_center">—</td>
<td headers="ci" class="gt_row gt_center">—</td>
<td headers="p.value" class="gt_row gt_center"><br /></td></tr>
    <tr><td headers="label" class="gt_row gt_left">    yes</td>
<td headers="estimate" class="gt_row gt_center">2.28</td>
<td headers="ci" class="gt_row gt_center">0.49, 10.7</td>
<td headers="p.value" class="gt_row gt_center">0.3</td></tr>
    <tr><td headers="label" class="gt_row gt_left">ecog.ps</td>
<td headers="estimate" class="gt_row gt_center"><br /></td>
<td headers="ci" class="gt_row gt_center"><br /></td>
<td headers="p.value" class="gt_row gt_center"><br /></td></tr>
    <tr><td headers="label" class="gt_row gt_left">    1</td>
<td headers="estimate" class="gt_row gt_center">—</td>
<td headers="ci" class="gt_row gt_center">—</td>
<td headers="p.value" class="gt_row gt_center"><br /></td></tr>
    <tr><td headers="label" class="gt_row gt_left">    2</td>
<td headers="estimate" class="gt_row gt_center">1.40</td>
<td headers="ci" class="gt_row gt_center">0.40, 4.94</td>
<td headers="p.value" class="gt_row gt_center">0.6</td></tr>
  </tbody>
  
  <tfoot class="gt_footnotes">
    <tr>
      <td class="gt_footnote" colspan="4"><span class="gt_footnote_marks" style="white-space:nowrap;font-style:italic;font-weight:normal;"><sup>1</sup></span> HR = Hazard Ratio, CI = Confidence Interval</td>
    </tr>
  </tfoot>
</table>
</div>
```

A nicer way to display the results from a Cox regression model is by using the `ggforest()` function, which creates a *forest plot* that plots the hazard ratios, together with their associated confidence intervals and $P$ values for all model covariates and stratified for those that are categorical (indicating the level used as reference). 


```r
ggforest(cph, data = ovarianDF)
```

<img src="_main_files/figure-html/unnamed-chunk-234-1.png" style="display: block; margin: auto;" />

As a final step we show you how to get prediction based on our Cox proportional hazard model. As before we can use the `predict()` function but unfortunately this is slightly more complicated before as it does not work on vectors but rather individual parameter values, which need to be provided as a `list`. For example, to predict the survival probability of a 72 year old at time $t=300$ 


```r
# fit cox proportional hazard ratio based on age only
cph <- coxph(Surv(futime, fustat) ~ age, data = ovarianDF)
predict(cph, newdata = list(age = 80, futime = 300, fustat = 0), type='survival')
```

```
## [1] 0.03909436
```

And to get survival curves for all ages between 50 and 80 years


```r
age <- as.matrix(50:80, ncol=1)
pred_surv <- apply(age, 1, function(x) predict(cph, newdata = list(age = x, futime = 300, fustat = 0), type='survival'))

data.frame(Age = age,
           Survival = pred_surv) %>%
    ggplot(aes(x = Age, y = Survival)) +
    geom_line() +
    labs(y = 'Survival probability at t=300')
```

<img src="_main_files/figure-html/unnamed-chunk-236-1.png" style="display: block; margin: auto;" />


<div class="panel panel-default"><div class="panel-heading"> Practical </div><div class="panel-body"> 

  1. Modify the aboce code to plot survival probabilities of a 70 year old against time
  2. Perform an indepth survival analysis of the `colon` dataset (provided by the `survival` package), which contains data from one of the first successful trials of adjuvant chemotherapy for colon cancer. You can get more information on the data and the various variables using `?colon`. 
   </div></div>

<!--chapter:end:7-Survival_analysis.Rmd-->

