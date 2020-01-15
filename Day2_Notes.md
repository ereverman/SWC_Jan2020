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

### Etherpad:

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
