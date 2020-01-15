### Creating graphics with ggplot2
Plotting data is a good way to start exploring and looking for relationships between variables. 
There are 3 main plotting systems in R: base plotting system, lattice package, ggplot2 package.

ggplot2 is most effective for making publication quality graphics.

### ggplot2 has a grammar system:
3 parts:
1. data set
2. coordinate system
3. set of geoms which specify the visual representation of the data points

* The key is to think about a plot in layers:

```
gapminder <- read.csv("data/gapminder_data.csv", header = TRUE)

library("ggplot2)

ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point()

```
#### Dissect:
1. ggplot function
2. data, mapping, geoms

### Question:

Show how life expectancy has changed over time:

### Solution:
```
head(gapminder)

ggplot(data = gapminder, mapping = aes(x = year, y = lifeExp)) +
geom_point()

```
How would we add color to the points in the plot?

```
ggplot(data = gapminder, mapping = aes(x = year, y = lifeExp, color = continent)) +
  geom_point()
  
```

Is there a better way to show how data changes over time?

```
ggplot(data = gapminder, mapping = aes(x=year, y=lifeExp, by=country, color=continent)) +
  geom_line()


# what is by argument doing?
ggplot(data = gapminder, mapping = aes(x=year, y=lifeExp, color=continent)) +
  geom_line()
```

Can we have both?

```
ggplot(data = gapminder, mapping = aes(x=year, y=lifeExp, by=country, color=continent)) +
  geom_line() + geom_point()
  
# Does order matter? Yes. If you plot points before lines, the lines will show up on top of the points.

ggplot(data = gapminder, mapping = aes(x=year, y=lifeExp, by=country)) +
  geom_line(mapping = aes(color=continent)) + geom_point()
  
```
### try this:

Switch the order of points and line layers and see what happened:

### Solution:
```
ggplot(data = gapminder, mapping = aes(x=year, y=lifeExp, by=country)) +
 geom_point() + geom_line(mapping = aes(color=continent))
```

## Transformations and Statistics

We can nest data transformations within the ggplot command. This is a good option if you don't want to change your data frame.

```
ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point()


# It is hard to see the relationship between points, so let's change the scale of the x axis:

ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.5) + scale_x_log10()


# Now, we see that the spread of the data has been condensed and we can start to see a pattern. We can fit a trend line to these data with ggplot:

ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point() + scale_x_log10() + geom_smooth(method="lm")
  


# We can change the way the line looks:

ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
  geom_point() + scale_x_log10() + geom_smooth(method="lm", size=1.5)
  
```

### Question:
Change the color of all of the points to orange.
Change the color of the line to black.


### Solution:
```
ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp)) +
 geom_point(size=3, color="orange") + scale_x_log10() +
 geom_smooth(method="lm", size=1.5)
```


## Multipanel figures

There is a lot of information in the previous plots. It is sometimes desirable to split the information into separate plots.

```
# make a subset of the data:

americas <- gapminder[gapminder$continent == "Americas", ]
head(americas)
unique(americas$continent)


ggplot(data = americas, mapping = aes(x = year, y = lifeExp)) +
geom_line() +
facet_wrap( ~ country)

# This split up the data by country, but now the x axis is hard to read.

ggplot(data = americas, mapping = aes(x = year, y = lifeExp)) +
geom_line() +
facet_wrap( ~ country) +
theme(axis.text.x = element_text(angle = 45))

```
This looks pretty good, but what else would you change if you were going to put this in a journal manuscript?

```
# modify the axes labels:

ggplot(data = americas, mapping = aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country) +
  labs(
    x = "Year",              # x axis title
    y = "Life expectancy",   # y axis title
    title = "Figure 1",      # main title of figure
    color = "Continent"      # title of legend
  ) +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))

# center the title:

ggplot(data = americas, mapping = aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country) +
  labs(
    x = "Year",              # x axis title
    y = "Life expectancy",   # y axis title
    title = "Figure 1",      # main title of figure
    color = "Continent"      # title of legend
  ) +
  theme(axis.text.x = element_text(angle = 90, hjust = 1),
  plot.title = element_text(hjust = 0.5))
  
  
# remove the legend:

ggplot(data = americas, mapping = aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country) +
  labs(
    x = "Year",              # x axis title
    y = "Life expectancy",   # y axis title
    title = "Figure 1",      # main title of figure
    color = "Continent"      # title of legend
  ) +
  theme(axis.text.x = element_text(angle = 90, hjust = 1),
  plot.title = element_text(hjust = 0.5)) +
  guides(color = FALSE)
  
  
# change the plot background and remove grid lines:

ggplot(data = americas, mapping = aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country) +
  labs(
    x = "Year",              # x axis title
    y = "Life expectancy",   # y axis title
    title = "Figure 1",      # main title of figure
    color = "Continent"      # title of legend
  ) +
  theme(axis.text.x = element_text(angle = 90, hjust = 1),
  plot.title = element_text(hjust = 0.5)) +
  guides(color = FALSE) +
  theme_classic()
  
```

### Export the plot:

Make a results/ directory in your gapminder-project directory.

```
LifeExp_plot <- ggplot(data = americas, mapping = aes(x = year, y = lifeExp, color=continent)) +
  geom_line() + facet_wrap( ~ country) +
  labs(
    x = "Year",              # x axis title
    y = "Life expectancy",   # y axis title
    title = "Figure 1",      # main title of figure
    color = "Continent"      # title of legend
  ) +
  theme(axis.text.x = element_text(angle = 90, hjust = 1),
  plot.title = element_text(hjust = 0.5)) +
  guides(color = FALSE) +
  theme_classic()
  
ggsave(filename = "results/lifeExp.png", plot = lifeExp_plot, width = 12, height = 10, dpi = 300, units = "cm")
