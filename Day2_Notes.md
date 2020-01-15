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


