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
  * Shortcut: command + return Mac
  * Shortcut: Control + enter PC
* Save button

## Etherpad:
List of shortcuts for RStudio:
https://support.rstudio.com/hc/en-us/articles/200711853-Keyboard-Shortcuts


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

# Shortcut: Assignment operator: mac option-, PC alt-

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

# Navigate to sections delineated with ----
# Lets go to the Mathematical Functions section.


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

3. Install the packages plyr and gapminder.

```
## Time for a break
============================================================================================================================

### Seeking Help in R
There are several built in ways to find more information about functions in r:
The Help panel.
```
# Getting Help----

?ls
help(ls)

# Fuzzy search:
??ls


# Many packages have vignettes:
vignette(ggplot2)

# If there are no vignettes:
help("ggplot2")

```

## Etherpad:

```
Some resources for getting help:

Quick R: https://www.statmethods.net
RStudio cheat sheets: http://www.rstudio.com/resources/cheatsheets/
Cookbook for R: http://www.cookbook-r.com
```

============================================================================================================================

### Project Managment in R Studio:

Project organization can be something of an art form. R Studio has tools that can help with project organization by creating self-contained projects.

Without project organization (of some form):
1. It's hard to tell which version of data is the original and which is modified.
2. Different file types might be mixed together.
3. It takes time to find files and the code used to generate those files.

Good project layout can:
1. Help ensure integrity of data.
2. Makes it simpler to share your code.
3. Encourages practices that makes uploading code during manuscript submission more streamlined.
4. Makes it easier to pick up a project after a break.

### Create a new project:

1. Click the “File” menu button, then “New Project”.
2. Click “New Directory”.
3. Click “New Project”.
4. Type in the name of the directory to store your project, e.g. “my_project”. Make sure this is a subdirectory of Desktop
5. If available, select the checkbox for “Create a git repository.”
6. Click "Open in New Session" button.
7. Click the “Create Project” button.

* Look for the new directory on your Desktop. Put up OK sticky when you have the directory on your Desktop.

## Etherpad:

Best Practices Tips from https://github.com/swcarpentry/good-enough-practices-in-scientific-computing/blob/gh-pages/good-enough-practices-for-scientific-computing.pdf
1. Treat data as read only. Keep the original data files stored separately and don't do any data cleaning directly on the original data file.
2. Treat generated output as disposable. You should keep and document all code used to generate output used in analyses. Subdirectories are a good way to do this.
3. Put each project in its own directory, which is named after the project.
4. Put text documents associated with the project in the doc directory.
5. Put raw data and metadata in the data directory, and files generated during cleanup and analysis in a results directory.
6. Put source for the project’s scripts and programs in the src directory, and programs brought in from elsewhere or compiled locally in the bin directory.
7. Name all files to reflect their content or function.

### Now let's make a new directory for data in our project folder.
1. Inside the Gapminder_Project directory, make a new directory called data.
2. Make another directory called scripts.
2. Go to the ku-swc-files-master directory you cloned from GitHub this morning.
3. Go to the data-gapminder-r subdirectory.
4. Move the gapminder_data.csv file to your Gapminder_Project/data/ directory.

Put up OK Sticky when done.

## Etherpad:
If you are waiting, practice the tools you learned earlier in the command line.

1. What is the size of the gapminder_data.csv file?
2. How many rows of data does it contain?
3. What kinds of values are stored in this file?

## Solution:
```
ls -lh data/gapminder_data.csv
# 80K

wc -l data/gapminder_data.csv
# 1705 lines

head data/gapminder_data.csv
# Gives first 10 lines in the file.
```

### Data Structures:
We've set up a project and a data directory, and we are working towards learning how to visualize data, something that R is especially good for. Before we start working with the large gapminder data, let's practice with a smaller dataset.

We are going to start by making this play data set from scratch in R and then saving it in our data/ directory:

```
# Make a data frame
cats <- data.frame(coat = c("calico", "black", "tabby"), 
                    weight = c(2.1, 5.0, 3.2), 
                    likes_string = c(1, 0, 1))
    
# Take a look at the data frame
cats

# Write cats to data/
write.csv(x = cats, file = "data/feline-data.csv", row.names = False

# Check the data/. There should be a file there. Open it. It is comma-separated.

# Most of the time, the data is generated with a different program.
# Read in data:

# First remove cats
rm(cats)

# Load Data:
cats <- read.csv(file = "data/feline-data.csv", header = TRUE)
cats

# Explore Data:
class(cats)
# there are several other data object types: Lists, Arrays, Matrices.

cats$weight

cats$coat

# How many rows?
nrow(cats)

# How many columns?
ncol(cats)



# Mathematical operations can be performed on numeric data
cats$weight + 2

# You can also do math across columns in the data if they are the correct data type.

cats$weight + cats$coat
Error

class(cats$weight)
class(cats$coat)

# One is a number and one is a factor. 
```

### Data Frames:
Each column in a data frame is a vector. Each vector should have data of the same type.

```
# Look at the data structure
str(cats$weight)

str(cats$likes_string)

str(cats$coat)
```

### Factors:
Factors usually look like character data but represent categories that the data are grouped into. We often use factors to make informative plots.

Let's look at the difference between character vectors and factors:
```
coats <- c('calico', 'black', 'tabby')
coats

str(coats)

# Turn coats into a factor
CATegories <- factor(coats)
class(CATegories)
str(CATegories)

# What do the numbers mean?
# R replaced the names of each category with a number "under the hood"
# This can have consequences for the order that categories are plotted and for the order of comparisons made in statistical tests. If you get an unexpected order or comparison, the class and ordering of factors is a good place to start troubleshooting.

```

## Etherpad:

1. Read in gapminder_data.csv. Hint: make sure you specify the data directory.
2. What type of data object is gapminder_data?
3. What is the structure of each variable in the dataset?

## Solution:

```
1. gapminder <- read.csv(file = "data/gapminder_data.csv", header = TRUE)

2. class(gapminder)


3. 
head(gapminder)

str(gapminder$country)
str(gapminder$year)
str(gapminder$pop)
str(gapminder$continent)
str(gapminder$lifeExp)
str(gapminder$gdpPercap)

```

### Exploring Data Frames:
Now you know how to load data into R and check to make sure it looks the way you expect it to. Next, we will give you some tips for how you can manipulate your data frame.

### 1. Adding columns:

```
# start with a new vector:

age <- c(2, 3, 5)
cats

# add the new column:
cbind(cats, age)

# Note that the new column needs to match the row dimensions of the data frame:
age <- c(2, 3, 5, 12)
cbind(cats, age)

nrow(cats)
length(age)

age <- c(2, 3, 5)
cats <- cbind(cats, age)
cats
```

### 2. Adding new rows:

```
newRow <- list("tortoiseshell", 3.3, TRUE, 9)
cats <- rbind(cats, newRow)

Error warning message

cats
# unexpected result

str(cats$coat)

levels(cats$coat)

# Add a new factor level:
levels(cats$coat) <- c(levels(cats$coat), "tortoiseshell")
cats <- rbind(cats, list("tortoiseshell", 3.3, TRUE, 9)

cats

```

### 3. Remove rows:

```
# remove 4th row:
cats[-4, ]

# remove 4th and 5th row:
cats[c(-4,-5), ]

# remove 2nd column:
cats[ ,-2]

# Drop rows with NA
na.omit(cats)

cats <- na.omit(cats)
```

### 4. Realistic Example:

```
gapminder <- read.csv("data/gapminder_data.csv", header = TRUE)

str(gapminder)

# Get a summary of country:
summary(gapminder$country)

# Check the dimenions:
dim(gapminder)

# Ask for column names:
colnames(gapminder)

# look at the first 6 lines:
head(gapminder)

## Etherpad:

It’s good practice to also check the last few lines of your data and some in the middle. How would you do this?
Searching for ones specifically in the middle isn’t too hard but we could simply ask for a few lines at random. How would you code this?

## Solution:

# look at last lines:
tail(gapminder)
tail(gapminder, n = 15)

# look at a set of lines near the middle:
nrow(gapminder)/2
gapminder[845:858, ]

# Random sample of lines:
gapminder[sample(nrow(gapminder), 5), ]
```
## Break.
============================================================================================================================

### Control Flow
There are often times when you may need to perform an operation over and over again. We can use conditional statements to do this. There are three main types that we will discuss today: if(), else(), and for().

### Building if() else() statements:

```
x <- 8

if (x >= 10) {
  print("x is greater than or equal to 10")
}

# No output. why?

if (x >= 10) {
  print("x is greater than or equal to 10")
} else {
  print("x is less than 10")
}

```

### test multiple conditions:

```
if (x >= 10) {
  print("x is greater than or equal to 10")
} else if (x > 5) {
  print("x is greater than 5, but less than 10")
} else {
  print("x is less than 5')
}

```

## Ether pad:

Use an if() statement to print a suitable message reporting whether there are any recods from 2002 in the gapminder dataset.

## Solution:
```
# First, we need a logical vector describing which element of gapminder$year is equal to 2002:
gapminder[(gapminder$year == 2002), ]

# Next, count the number of rows in this subset:
rows2002_number <- nrow(gapminder[(gapminder$year == 2002), ])

# Write the if statement:
if(rows2002_number >=1) {
  print("Records for year 2002 found")
}

```

### ifelse()

```
# ifelse combines if and else:

y <- -3

ifelse(y < 0, "y is negative", "y is positive or 0")
```

### For loops:
For loops let you perform the same set of operations over each element in a vector. They work similar to how you used them earlier today. For loops are very flexible, but there are also lots of ways to get tangled up in them. My advice is to build each part separately and test it on a subset of the data before running it on the entire dataset.

```
# Syntax:
# for(iterator in a set of values) {
#   do a thing
# {

for(i in 1:10){
  print(i)
}

# for loops can be nested:
for(i in 1:5){
  for(j in c('a','b','c','d','e')){
    print(paste(i,j))
  }
}

# When the index i is 1, the second index iterates through the set of letters. Once that is complete, the index i moves to the next value and the loop repeats.



# Writing an output object:

# First make an empty vector
output_vector <- c()

# Second run the loop:
for(i in 1:5){
  for(j in c('a','b','c','d','e')){
    temp_output <- print(paste(i,j))
    output_vector <- c(output_vector, temp_output)
  }
}

output_vector

# Growing your results using a completely empty vector can cost time. When you have a very large dataset to iterate through, this time can start to add up to minutes or hours. 

# Get set up:
output_matrix <- matrix(nrow = 5, ncol = 5)
j_vector <- c('a','b','c','d','e')

# Run loop:
for(i in 1:5){
  for(j in 1:5){
    temp_j_value <- j_vector[j]
    temp_output <- paste(i, temp_j_value)
    output_matrix[i, j] <- temp_output
  }
}

output_matrix
output_vector2 <- as.vector(output_matrix)
output_vector2

```

### While loops:
These are useful for performing an operation while a condition is true. We can use while loops for this:

```
# Syntax:
# while(this condition is true){
#   do a thing
# }

z <- 1
runif(z)
# this function samples random numbers from a uniform distribution between 0 and 1. We want to print out these sampled numbers while the number is greater than 0.1

while(z > 0.1){
  z <- runif(1)
  cat(z, "\n")
}

```

## Etherpad:

Challenge question:
Write a script that loops through the gapminder data by continent and prints out the mean life expectancy.

## Solution:

```
Step 1. get the unique values for continent:
head(gapminder)
unique(gapminder$continent) 

Step 2. loop over each continent and calculate the average life expectancy for each continent subset:

for(iContinent in unique(gapminder$continent)){   # Loop over each unique continent
  tmp <- gapminder[gapminder$continent == iContinent, ]   # subset the data to one of the continents
  cat(iContinent, mean(tmp$lifeExp, na.rm = TRUE), "\n")  # make a string with the continent name and the mean life expectance, ignore NAs, then move to the next line for the next continent
  rm(tmp)   # remove tmp
}

```

## Wrap up:
save your R script in the scripts folder.

Write something we did well this afternoon, and something that we can improve.
