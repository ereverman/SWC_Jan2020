## Follow up for day 1 and notes on ggplot2:
```

# Load Data:----

gapminder <- read.csv("data/gapminder_data.csv", header = TRUE)
head(gapminder)

cats <- read.csv("data/feline_data.csv", header = TRUE)
cats

# Libraries:----
# if needed, install.packages("ggplot2")
library(ggplot2)

# Challenges and Followup:----

# 1. How many rows and columns are in gapminder?
# 2. Calculate the log10 of gdpPercap and store it in a new variable called gdpPercap_log
# 3. Add gdpPercap_log as a new column to gapminder. Check the dimensions of the data and head.
# 4. Find the mean of lifeExp for the entire gapminder dataset.
# 5. Find the min and max lifeExp for the entire gapminder dataset.
# 6. How many years are present in the data?
# 7. Subset the data for only Africa in 2002.
# 8. Find the mean of each continents lifeExp.


# Solutions:----


# 1. How many rows and columns are in gapminder?

dim(gapminder)

# 2. Calculate the log10 of gdpPercap and store it in a new variable called gdpPercap_log

gdpPercap_log <- log10(gapminder$gdpPercap)

# 3. Add gdpPercap_log as a new column to gapminder. Check the dimensions of the data and head.

gapminder <- cbind(gapminder, gdpPercap_log)
head(gapminder)
dim(gapminder)

# Another way, do the calculation and the add column at the same time.

gapminder$gdpPercap_sqrt <- sqrt(gapminder$gdpPercap)
head(gapminder)

# 4. Find the mean of lifeExp for the entire gapminder dataset.

mean(gapminder$lifeExp)

# 5. Find the min and max lifeExp for the entire gapminder dataset.
min(gapminder$lifeExp)
max(gapminder$lifeExp)
# or, if you are super cool,
summary(gapminder$lifeExp)

# 6. How many years are present in the data?

gapminder$year
unique(gapminder$year)
length(unique(gapminder$year))

# 7. Subset the for only Africa in 2002:

x <- gapminder[(gapminder$continent == "Africa"), ]
y <- x[(x$year == 2002), ]

Africa2002 <- gapminder[(gapminder$continent == "Africa" & gapminder$year == 2002), ]

# 8. Find the mean of each continents lifeExp.

# For loops can help.
# First, how do we subset the data.
# yesterday, gapminder[(gapminder$year == 2002), ]

# What continents are in our dataset?
str(gapminder$continent) # not very helpful...
levels(gapminder$continent) # Ah ha!

gapminder[(gapminder$continent == "Africa"), ] # gives us every line in Africa, reaches max print
gapminder[(gapminder$continent == "Africa"), 5] # gives us every line in Africa, and only lifeExp

# Syntax for for loop:
# for(iterator in "set of things"){
# do something
# }

SetOfThings <- levels(gapminder$continent)
SetOfThings

# do something:
mean(gapminder[(gapminder$continent == "Africa"), 5])

# Now make this calculation for each of the continents:

for(continent in SetOfThings){
 print(mean(gapminder[(gapminder$continent == continent), 5]))
}

# Almost, but which continent is which?

for(continent in SetOfThings){
  print(paste(continent,mean(gapminder[(gapminder$continent == continent), 5])))
}

# Wow that was a lot of work. Surely it can be simpler?

MeanLifeExp <- aggregate(lifeExp ~ continent, gapminder, mean)
MeanLifeExp

MeanLifeExp_byYear <- aggregate(lifeExp ~ continent + year, gapminder, mean)
MeanLifeExp_byYear


# Bonus:
# Question about finding duplicate data:

# make a test case:
# nativate to the data files section.
cats <- read.csv("data/feline_data.csv", header = TRUE)
cats

# make a duplicate row in cats:

cats_dup <- rbind(cats, cats[1, ])
cats_dup


duplicated(cats_dup)
anyDuplicated(cats_dup)

# pull all the data that are unique, considering the entire row.
cats_clean <- unique(cats_dup)


# Plotting using ggplot2:----
# Three elements to keep track of:
# 1. dataset
# 2. coordinate system
# 3. geoms (what you want to plot)

# Activate Libraries
library(ggplot2)

head(gapminder)

# Whats the relationship between gdp and life expectancy?
# Syntax:
# ggplot(DATA, aes(XVar, YVar)) +
# geoms

ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point()

# This is the same information but cleaner:
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point()

# What if no geom:
ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp))
# just a coordinate system.


# CHALLENGE: Plot the change in life expentancy over time:----

ggplot(gapminder, aes(year, lifeExp)) +
  geom_point()

# Now change the color of the points:

ggplot(gapminder, aes(year, lifeExp)) +
  geom_point(aes(color = continent))

ggplot(MeanLifeExp_byYear, aes(year, lifeExp)) +
  geom_point(aes(color = continent))

# Line Plots:----
# visualize data over time
ggplot(gapminder,aes(x=year, y=lifeExp, by=country, color=continent)) +
  geom_line()

# you can keep adding layers to some extent:
ggplot(data = gapminder, mapping = aes(x=year, y=lifeExp, by=country, color=continent)) +
  geom_line() + geom_point()

ggplot(data = MeanLifeExp_byYear, mapping = aes(x=year, y=lifeExp, color=continent)) +
  geom_line() + geom_point()

# but the order matters.
# For example:

ggplot(data = gapminder, mapping = aes(x=year, y=lifeExp, by=country)) +
  geom_line(aes(color = continent)) + geom_point()

ggplot(data = gapminder, mapping = aes(x=year, y=lifeExp, by=country)) +
  geom_point() +
  geom_line(aes(color = continent))

# Transformations and Statistics:----
ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point()

# This is hard to read because of outliers. 
ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.5) + scale_x_log10()

# Remember earlier we added this new column to the data set. Is it the same?
head(gapminder)
ggplot(data = gapminder, mapping = aes(x = gdpPercap_log, y = lifeExp)) +
  geom_point(alpha = 0.5)


# Do some light statistics:
ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point() + scale_x_log10() + geom_smooth(method="lm")

# We can change elements of how the best fit line looks as well:

ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point() + scale_x_log10() + geom_smooth(method="lm", size=1.5)

# What if you are interested in diffences among your groups?

ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.3) + 
  scale_x_log10() + 
  geom_smooth(method="lm", aes(color = continent))

# CHALLENGE: Change the points to orange (or your favorite color) and make them larger. Change the color of the best fit line to black:----
ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point(color = "orange", size = 2) + scale_x_log10() + 
  geom_smooth(method="lm", color = "black")


# What if you are interested in diffences among your groups? Hint: try using an aes with geom_smooth.

ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.3) + 
  scale_x_log10() + 
  geom_smooth(method="lm", aes(color = continent))

# Including information about 3 variables:----
head(gapminder)

ggplot(gapminder, aes(lifeExp, gdpPercap_log)) +
  geom_point(aes(size = pop, color = continent), alpha = 0.5)


# Can we make this more clear?

CountryAvgs <- aggregate(cbind(lifeExp, gdpPercap_log, pop) ~ continent + country, gapminder, mean)
CountryAvgs

ggplot(CountryAvgs, aes(lifeExp, gdpPercap_log)) +
  geom_point(aes(size = pop, color = continent), alpha = 0.5)

ggplot(CountryAvgs, aes(lifeExp, gdpPercap_log)) +
  geom_point(aes(size = pop, color = continent), alpha = 0.5) +
  guides(size = FALSE)

# Add the trend line:

ggplot(CountryAvgs, aes(lifeExp, gdpPercap_log)) +
  geom_point(aes(size = pop, color = continent), alpha = 0.5) +
  geom_smooth(method = "lm", color = "black")

# Boxplots:----
head(gapminder)

ggplot(gapminder, aes(continent, lifeExp)) +
  geom_boxplot()

# Add some color:
ggplot(gapminder, aes(continent, lifeExp)) +
  geom_boxplot(aes(fill = continent))

# Add some color:
ggplot(gapminder, aes(continent, lifeExp)) +
  geom_boxplot(aes(fill = continent, color = continent), alpha = 0.5)

# What if you want to specify the color:

# Add some color:
ggplot(gapminder, aes(continent, lifeExp)) +
  geom_boxplot(aes(fill = continent, color = continent), alpha = 0.5) +
  scale_fill_manual(values = c("purple","orange","blue","red","green")) +
  scale_color_manual(values = c("purple","orange","blue","red","green"))

# CHALLENGE: plot the relationship between year and gpdPercap and specify the colors:----

ggplot(data = gapminder, mapping = aes(x=year, y=lifeExp, by=country, color=continent)) +
  geom_line() + geom_point() +
  scale_color_manual(values = c("purple","orange","blue","red","green"))

# Plot distributions:----

ggplot(gapminder, aes(lifeExp)) +
  geom_density(aes(fill = continent), alpha = 0.3)

# Plot with facets:-----
americas <- gapminder[gapminder$continent == "Americas",]
ggplot(data = americas, mapping = aes(x = year, y = lifeExp)) +
  geom_line() + 
  facet_wrap( ~ country) + 
  theme(axis.text.x = element_text(angle = 45))


# CHALLENGE: Make a facets plot for the distributions:-----
ggplot(gapminder, aes(lifeExp)) +
  geom_density(aes(fill = continent), alpha = 0.3) +
  facet_wrap( ~ continent)

ggplot(gapminder, aes(lifeExp)) +
  geom_density(aes(fill = factor(year)), alpha = 0.3) +
  facet_wrap( ~ continent, scales = "free")

# Change the appearance of text:------
ggplot(data = americas, mapping = aes(x = year, y = lifeExp)) +
  geom_line() + 
  facet_wrap( ~ country) + 
  theme(axis.text.x = element_text(angle = 45))


ggplot(data = americas, mapping = aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country) +
  labs(
    x = "Year",              # x axis title
    y = "Life expectancy",   # y axis title
    title = "Figure 1",      # main title of figure
    color = "Continent"      # title of legend
  ) +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))

# What else about this plot do you want to change?

ggplot(data = americas, mapping = aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country) +
  labs(
    x = "Year",              # x axis title
    y = "Life expectancy",   # y axis title
    title = "Figure 1",      # main title of figure
    color = "Continent"      # title of legend
  ) +
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) +
  theme(plot.title = element_text(hjust = 0.5)) +
  theme_classic()


# Save the plot:----

# Make a directory called results/

lifeExp_plot <- ggplot(data = americas, mapping = aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country) +
  labs(
    x = "Year",              # x axis title
    y = "Life expectancy",   # y axis title
    title = "Figure 1",      # main title of figure
    color = "Continent"      # title of legend
  ) +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))

ggsave(filename = "lifeExp.png", 
       plot = lifeExp_plot, 
       width = 20, 
       height = 14, 
       dpi = 300, 
       units = "cm")



# Resources:----
# https://www.data-to-viz.com
# https://rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf

# more general cheatsheets:
# https://rstudio.com/wp-content/uploads/2016/05/base-r.pdf
# https://sites.ualberta.ca/~ahamann/teaching/renr690/R_Cheat_Data.pdf
# https://github.com/rstudio/cheatsheets/blob/master/data-import.pdf


# Helpful Packages for data wrangling and resources:
# Tidyverse: Merging and subsetting data: 
    # https://rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf
    # https://rstudio.com/resources/cheatsheets/
# Rmisc: Calculating summary statistics (mean, 95% confidence intervals, standard error, standard deviation): Rmisc https://cran.r-project.org/web/packages/Rmisc/Rmisc.pdf

# If you want access to my notes:
# https://github.com/ereverman/SWC_Jan2020
```
