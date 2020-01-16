## Introduction to R:

```
# Use R as a calculator:----

3 + 5 * 2

(3 + 5) * 2

2/10000

5e3

# syntax for functions:
# function_name(argument)

sin(1)

log(1)

log10(10)

exp(0.5)

# Comparing things:----

1 == 1 

1 != 2

1 < 2

1 > 2

1 >= -9

# Variables and Assignment:----

x <- 1/40
x

# shortcut for assignment operator
# mac: option -
# pc: alt -

log(x)

x <- 100

x <- x + 1
x

y <- x * 2

# Vectors:----

1:5

2^(1:5)

x <- 1:5

2^x

# Managing your environment:----

ls()

rm(x)
ls()

# R packages:----

installed.packages()

# install a package:
install.packages("ggplot2")
update.packages("ggplot2")

library("ggplot2")

# Getting Help:----

?ls

vignette("ggplot2")
vignette("colorspace")

help("ggplot2")
```

## Practice with Dataframes:

```
# Practice dataframes:----

cats <- data.frame(coat = c("calico", "black", "tabby"),
                   weight = c(2.1, 5.0, 3.2),
                   likes_string = c(1, 0, 1))
cats

# write cats to file:
write.csv(cats, file = "data/feline_data.csv", row.names = FALSE)

rm(cats)
cats

# read in data files:
cats <- read.csv(file = "data/feline_data.csv")
cats

# for tab-delimited data:
# dat <- read.table(file = "PATH TO DATA", header = TRUE, sep = " ")

cats$coat
cats$weight
cats$likes_string

class(cats)

class(cats$coat)
class(cats$weight)
class(cats$likes_string)


# Dimensions:
nrow(cats)
ncol(cats)
dim(cats)


# Math:
cats$weight + 2
cats$weight

cats$weight + 
  cats$likes_string

cats$weight + 
  cats$coat

# structure of object
str(cats)
str(cats$weight)

# Factors:

coats <- c('calico', 'black', 'tabby')
coats
str(coats)
str(cats$coat)

CATegories <- factor(coats)
str(CATegories)

coats_2 <- c('calico', 'black', 'tabby', 'black')
str(coats_2)
CAT_2 <- factor(coats_2)
str(CAT_2)



# Challenge:
# 1. read in gapminder data.
gapminder <- read.csv(file = "data/gapminder_data.csv", header = TRUE)

# 2. what is the data type of gapminder?
class(gapminder)

# 3. what is the structure of each variable in the dataset?
str(gapminder$country)
head(gapminder)
dim(gapminder)


install.packages("gapminder")

# Add columns:
cats <- read.csv("data/feline_data.csv")

cats
age <- c(2, 3, 5)

cbind(cats, age)

age <- c(2, 3, 5, 12)
cbind(cats, age)

age <- c(2, 3, 5)
cats <- cbind(cats, age)

cats

# Add rows:

newRow <- list("tortoiseshell", 3.3, 1, 9)

cats <- rbind(cats, newRow)  
cats  
str(cats$coat)

levels(cats$coat)

levels(cats$coat) <- c(levels(cats$coat), "tortoiseshell")

cats <- rbind(cats, newRow)
cats

# Remove rows:
cats$coat
cats[4, ]
cats[-4, ]

cats[c(-4,-5), ]
cats[4, 3]

cats[ , 2]

cats <- na.omit(cats)
cats

# Realistic Example:
head(gapminder)

summary(gapminder)
tail(gapminder)

set.seed(5)
gapminder[sample(nrow(gapminder),5), ]



# if() and else():----

x <- 8

if(x >= 10){
  print("x is greater than or equal to 10")
}

if(x >=10){
  print("x id greater than or equal to 10")
} else {
  print("x is less than 10")
}


# multiple conditions:
if(x >= 10){
  print("x is greater or equal to 10")
} else if(x > 5){
  print("x is greater than 5 but less than 10")
} else{
  print("x is less than 5")
}


# Example from gapminder data:
# are there any records from 2002?
cats
gapminder[(gapminder$year == 2002), ]

if(nrow(gapminder[(gapminder$year == 2002), ]) >= 1){
  print("Data found for 2002")
}

row2002 <- nrow(gapminder[(gapminder$year == 2002), ])
row2002

if(row2002 >= 1){
  print("Data found for 2002")
}

# ifelse() 

y <- -3
ifelse(y < 0, "y is negative", "y is positive or 0")

y <- 6
ifelse(y < 0, "y is negative", "y is positive or 0")


# For loops:----

# Syntax
# for(iterator in "a set of things"){
# do something
# }
1:10

for(i in 1:10){
  print(i)
}

# nesting for loops:

for(i in 1:5){
  for(j in c('a','b','c','d','e')){
    print(paste(i,j))
  }
}

# Make for loops more efficient:

output_vector <- c()

for(i in 1:5){
  for(j in c('a','b','c','d','e')){
    temp_output <- print(paste(i,j))
    output_vector <- c(output_vector, temp_output)
  }
}

output_vector

# while loops:

# Syntax
# while(this condition is true){
# do something
# }

z <- 1
runif(z)

set.seed(5)

while(z > 0.1){
  z <- runif(1)
  cat(z, "\n")
}
```

