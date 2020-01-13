## Opening introduction:
  1. Postdoctoral Fellow in Macdonald Lab here at KU. I study quantitative and evolutionary genetics and genomics.
  2. The first coding language I learned is R, and this is where I am most comfortable. I have found other coding languages easier to learn having some basis to start from.


## Quick Survey:
Let's get a quick quage of experience level with R

*** Post in Etherpad:

```
In the last 6 months:
A. I have installed R and R Studio on my computer but haven't used it.
B. I have used R a few times.
C. I have used R frequently.

```


## Start the Lesson:
https://swcarpentry.github.io/r-novice-gapminder/

* Earlier today, you cloned the Git repository with the data you will need for today and tomorrow's R lesson. There should be a directory on your desktop named: ku-swc-files-master. We won't work with this yet, but will need it a little later.

* We asked you to download both R and R Studio. Please put up your help sticky if you haven't downloaded both of these programs. 
  * The reason that we use both R and R Studio:
    * R is a programming language and a software tool for data manipulation, statistics, and data visualization. When you downloaded R, you downloaded the base version of this tool. You don't need R Studio to use R. 
    * R Studio is an IDE for R. IDE is integrated development environment. R Studio has several additional tools that help you organize your data projects and keep track of the scripts you write to run specific analyses.
    
    
* The first thing we will do this afternoon is take a walkthrough of R Studio to give you an idea of some of these tools.
* Our primary goals are to get familiar with what you see when you use R Studio in each of the panes.
* We will:
  * Define variables
  * Learn how to manage the R Studio Session
  * Call Functions
  * Manage packages
  
  
  
### 1. Open R Studio
Give a brief tour of what you see:
* Three panes
* You can type directly in the Console pane, but what happens if you want to save a command and run it again?
  * The arrow up keys will work here the same way they did earlier to retrieve previously run commands, but this doesn't save the commands you wrote.
  * There is a better way to write commands in the form of an R script.
* End with new file button



### 2. Open a new R script file.
* Run button
* Save button



### 3. Using R as a calculator:
* Let's define a new section in our R script:

```
# Using R as a calculator----          
# Like this morning, # indicates a comment and will be ignored by R. The ---- help us 
# define a new section. We can use this tool to help navigate through sections of code.


# R follows order of operations:
3 + 5 * 2

# Spacing between numbers helps with readability and isn't required. This also works:
3+5*2

# We can force R to perform operations in a specific order with parentheses:
(3 + 5) * 2

# R uses scientific notation for large and small numbers:
2/10000

# You can give R numbers in scientific notation:
5e3

```



### 4. Mathematical Functions:
* R has several built in functions, similar to what you saw working with bash this morning.

```
# Mathematical Funtions----

# Calculate the sin:
sin(1)

# Calculate natural log:
log(1)

# Calculate base-10 logarithm:
log10(10)

# Calculate exponents:
exp(0.5)

```
* There are a lot of functions that are loaded automatically in R. I don't know them all, but they typically have memorable names.
* To find other functions you might need, you can:
  * Look them up in Google.
  * If you remember part of the function name, you can begin typing and then use tab-compete to look up the funtion in R Studio.
  
  
  
  
### 5. Comparing things:
```
# Making Comparisons----

# Are these things the same?
1 == 1   # == reads as "is equal to"

# Are these things different?
1 != 2   # != reads "is not equal to"

# Less than?
1 < 2

# Less than or equal to?
1 <= 2

# Greater than?
1 > 2

# Greater than or equal to?
1 >=-9

```
* Be careful with comparisons. Only use == for comparing integers (whole numbers). You may get unexpected results if you have any differences in rounding in decimals that are represented in your data.




### 6. Variables and Assignment:
```
# Assigning variables----

x <- 1/40
x

# Do Calculations with assigned variables:
log(x)

# Reassign variables:
x <- 100
x

# New variables can use information stored in variables:
x <- x + 1
y <- x * 2

# This also works, but is not recommended because it can be confusing:
x = 1/40
```

## In Etherpad:
```
* Rules for assigning variables:
  * Dont start with numbers.
  * Don't include spaces.
  * Do include letters, numbers, underscores and periods.
  * Be consistent.
  * Some examples of names:
    * periods.between.words
    * underscores_between_words
    * CaseToSeparateWords
    
 * Be descriptive with names, even if they are a little long. Remember tab-complete in R Studio will help you not have to type out long names
```



### 7. Vectorization:
* Much of the power of R relies on vectorization of information.
* In R, all of the information stored in a single vector is the same data type (ex. all integers, all characters)
* We will get a brief introduction here and will spend more time on this later.

```
# Explore vectors----

1:5     # Sequence, includes 1 and 5

2^(1:5) # Calculate 2 raised to the powers 1 thru 5

x <- 1:5  # assign a variable
2^x       # gives same answer as before

```



### 8. Managing your environment:
* ls() works in R Studio similar to what you saw this morning.

```
# Other tips----

ls()

# using rm to remove objects:
rm(x)

rm(list = ls()) # Removes everything in your environment

```



### 9. R Packages
* When you open R, several functions are already loaded.
* You can get access to functions that have been written by other community contributors by installing packages.
* This can be useful for running specific analyses, or getting additional tools that help with data processing.

```
# Installing Packages----

# what is installed?
installed.packages()

# Install a package:
install.packages("ggplot2")
# If prompted to select a cran mirror, select USA, KS


# Update packages:
update.packages()

# Remove packages:
remove.packages("ggplot2")

# After installing a package, make it available:
install.packages("ggplot2")
library(ggplot2)

```


### 10. Challenges:

## Etherpad:
```
1. Assign the following variables:

mass <- 47.5
age <- 122

2. What is the value of each variable?

mass <- mass * 2.3
age <- age
