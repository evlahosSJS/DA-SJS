Data Visualization
================
Emile Vlahos
8/21/2020

# Data Visualization

### 3.1 Introduction

``` r
# we must load the tidyverse library every session
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.1     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

### 3.2 First steps

QUESTION: Do cars with big engines use more gas than cars with small
engines?

##### 3.2.1 The mpg data frame

A data frame is a rectangular collection of variables (in the columns)
and observations (in the rows). mpg contains observations collected by
the US Environmental Protection Agency on 38 models of car.

``` r
mpg
```

    ## # A tibble: 234 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl    class
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr> <chr>
    ##  1 audi         a4         1.8  1999     4 auto(l… f        18    29 p     comp…
    ##  2 audi         a4         1.8  1999     4 manual… f        21    29 p     comp…
    ##  3 audi         a4         2    2008     4 manual… f        20    31 p     comp…
    ##  4 audi         a4         2    2008     4 auto(a… f        21    30 p     comp…
    ##  5 audi         a4         2.8  1999     6 auto(l… f        16    26 p     comp…
    ##  6 audi         a4         2.8  1999     6 manual… f        18    26 p     comp…
    ##  7 audi         a4         3.1  2008     6 auto(a… f        18    27 p     comp…
    ##  8 audi         a4 quat…   1.8  1999     4 manual… 4        18    26 p     comp…
    ##  9 audi         a4 quat…   1.8  1999     4 auto(l… 4        16    25 p     comp…
    ## 10 audi         a4 quat…   2    2008     4 manual… 4        20    28 p     comp…
    ## # … with 224 more rows

``` r
?mpg
```

### 3.2.2 Creating a ggplot

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

With ggplot2, you begin a plot with the function ggplot(). ggplot()
creates a coordinate system that you can add layers to. The first
argument of ggplot() is the dataset to use in the graph. So ggplot(data
= mpg) creates an empty graph, but it’s not very interesting so I’m not
going to show it here.

You complete your graph by adding one or more layers to ggplot(). The
function geom\_point() adds a layer of points to your plot, which
creates a scatterplot. ggplot2 comes with many geom functions that each
add a different type of layer to a plot. You’ll learn a whole bunch of
them throughout this chapter.

Each geom function in ggplot2 takes a mapping argument. This defines how
variables in your dataset are mapped to visual properties. The mapping
argument is always paired with aes(), and the x and y arguments of aes()
specify which variables to map to the x and y axes. ggplot2 looks for
the mapped variables in the data argument, in this case, mpg.

### 3.2.3 A Graphing Template

ggplot(data = <DATA>) + <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>))

##### Exercises

1.  Run ggplot(data = mpg). What do you see?

<!-- end list -->

``` r
ggplot(data = mpg)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

When this code is run a gray rectangle is displayed. This is because
ggplot creates a background in which plots can be put onto, however, as
no plots are coded the plot remains a template

2.  How many rows are in mpg? How many columns?

There are 234 rows and 11 columns

3.  What does the drv variable describe? Read the help for ?mpg to find
    out.

?mpg states that drv describes the type of drive train, where f =
front-wheel drive, r = rear wheel drive, and 4 = 4 wheel drive.

4.  Make a scatterplot of hwy vs cyl.

<!-- end list -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = hwy, y = cyl))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

5.  What happens if you make a scatterplot of class vs drv? Why is the
    plot not useful?

<!-- end list -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = class, y = drv))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

The plot is not useful as the variables had no correlation.

### 3.3 Aesthetic mappings

You can convey information about your data by mapping the aesthetics in
your plot to the variables in your dataset. For example, you can map the
colors of your points to the class variable to reveal the class of each
car.

To map an aesthetic to a variable, associate the name of the aesthetic
to the name of the variable inside aes(). ggplot2 will automatically
assign a unique level of the aesthetic to each unique value of the
variable, a process known as scaling. ggplot2 will also add a legend
that explains which levels correspond to which values.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = hwy, y = displ, color = class))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

In this case, the variable class is casted to color, meaning that the
color of each point reflects a different class represented in the
legend.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, size = class)) 
```

    ## Warning: Using size for a discrete variable is not advised.

![](Data-Visualization_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

Simililarly to before, but instead using size to order variable.
However, We get a warning here, because mapping an unordered variable
(class) to an ordered aesthetic (size) is not a good idea.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, alpha = class))
```

    ## Warning: Using alpha for a discrete variable is not advised.

![](Data-Visualization_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

Alpha here controls the transparency of the variable class similar to
before

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, shape = class))
```

    ## Warning: The shape palette can deal with a maximum of 6 discrete values because
    ## more than 6 becomes difficult to discriminate; you have 7. Consider
    ## specifying shapes manually if you must have them.

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](Data-Visualization_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

This time it controls the shape of the variable class

For each aesthetic, you use aes() to associate the name of the aesthetic
with a variable to display. The aes() function gathers together each of
the aesthetic mappings used by a layer and passes them to the layer’s
mapping argument. The syntax highlights a useful insight about x and y:
the x and y locations of a point are themselves aesthetics, visual
properties that you can map to variables to display information about
the data.

Once you map an aesthetic, ggplot2 takes care of the rest. It selects a
reasonable scale to use with the aesthetic, and it constructs a legend
that explains the mapping between levels and values. For x and y
aesthetics, ggplot2 does not create a legend, but it creates an axis
line with tick marks and a label. The axis line acts as a legend; it
explains the mapping between locations and values.

You can also set the aesthetic properties of your geom manually. For
example, we can make all of the points in our plot blue:

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy), color = "blue")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

##### 3.3.1 Exercises

1.  What’s gone wrong with this code? Why are the points not blue?

<!-- end list -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = "blue"))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

The color assignment has to be outside of the parenthesis, and therefore
this code gives the wrong color. The code should read: ggplot(data =
mpg) + geom\_point(mapping = aes(x = displ, y = hwy), color = “blue”)

2.  Which variables in mpg are categorical? Which variables are
    continuous? (Hint: type ?mpg to read the documentation for the
    dataset). How can you see this information when you run mpg?

<!-- end list -->

``` r
?mpg
```

Categorical variables in the data set include: Manufacturer, model,
transmission, type of drive train, fuel type and class. The remaining
ones are all continuous

> 3.  Map a continuous variable to color, size, and shape. How do these
>     aesthetics behave differently for categorical vs. continuous
>     variables?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = hwy, y = displ, color = cty))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->
Good graph , works

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = hwy, y = displ, size = cty))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->
A bit more cluttered, but still works

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = hwy, y = displ, shape = trans))
```

    ## Warning: The shape palette can deal with a maximum of 6 discrete values because
    ## more than 6 becomes difficult to discriminate; you have 10. Consider
    ## specifying shapes manually if you must have them.

    ## Warning: Removed 96 rows containing missing values (geom_point).

![](Data-Visualization_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

Useless, can not compare sizes of different shapes.

> 4.  What happens if you map the same variable to multiple aesthetics?

It becomes redundant

> 6.  What happens if you map an aesthetic to something other than a
>     variable name, like aes(colour = displ \< 5)? Note, you’ll also
>     need to specify x and y.

Aesthetics can also be mapped to expressions like displ \< 5. The
ggplot() function behaves as if a temporary variable was added to the
data with values equal to the result of the expression. In this case,
the result of displ \< 5 is a logical variable which takes values of
TRUE or FALSE.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = displ < 5))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

### 3.5 Facets

One way to add additional variables is with aesthetics. Another way,
particularly useful for categorical variables, is to split your plot
into facets, subplots that each display one subset of the data.

To facet your plot by a single variable, use facet\_wrap(). The first
argument of facet\_wrap() should be a formula, which you create with \~
followed by a variable name (here “formula” is the name of a data
structure in R, not a synonym for “equation”). The variable that you
pass to facet\_wrap() should be discrete.

ggplot(data = mpg) + geom\_point(mapping = aes(x = displ, y = hwy)) +
facet\_wrap(\~ class, nrow = 2)

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_wrap(~ class, nrow = 2)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

To facet your plot on the combination of two variables, add
facet\_grid() to your plot call. The first argument of facet\_grid() is
also a formula. This time the formula should contain two variable names
separated by a \~.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(drv ~ cyl)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

If you prefer to not facet in the rows or columns dimension, use a .
instead of a variable name, e.g. + facet\_grid(. \~ cyl).

##### 3.5.1 Exercises

> 1.  What happens if you facet on a continuous variable?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(year ~ cty)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->
The graph becomes extremely cluttered and hard to understand when more
continuous variables are introduced

> 2.  What do the empty cells in plot with facet\_grid(drv \~ cyl) mean?
>     How do they relate to this plot?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = drv, y = cyl))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

The empty cells (facets) in this plot are combinations of drv and cyl
that have no observations. These are the same locations in the scatter
plot of drv and cyl that have no points.

> 3.  What plots does the following code make? What does . do?

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(. ~ cyl)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-22-2.png)<!-- -->
Produces a graph of hwy vs displ, while also categorizing the number of
cyliders. It’s a very effective graph and is formatted well. The period
is a replacement for what could be another variable where

> 4.Take the first faceted plot in this section:

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, nrow = 2)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

Advantages of encoding class with facets instead of color include the
ability to encode more distinct categories. For me, it is difficult to
distinguish between the colors of “midsize” and “minivan”.

Given human visual perception, the max number of colors to use when
encoding unordered categorical (qualitative) data is nine, and in
practice, often much less than that. Displaying observations from
different categories on different scales makes it difficult to directly
compare values of observations across categories. However, it can make
it easier to compare the shape of the relationship between the x and y
variables across categories.

Disadvantages of encoding the class variable with facets instead of the
color aesthetic include the difficulty of comparing the values of
observations between categories since the observations for each category
are on different plots. Using the same x- and y-scales for all facets
makes it easier to compare values of observations across categories, but
it is still more difficult than if they had been displayed on the same
plot. Since encoding class within color also places all points on the
same plot, it visualizes the unconditional relationship between the x
and y variables; with facets, the unconditional relationship is no
longer visualized since the points are spread across multiple plots.

The benefit of encoding a variable with facetting over encoding it with
color increase in both the number of points and the number of
categories. With a large number of points, there is often overlap. It is
difficult to handle overlapping points with different colors color.
Jittering will still work with color. But jittering will only work well
if there are few points and the classes do not overlap much, otherwise,
the colors of areas will no longer be distinct, and it will be hard to
pick out the patterns of different categories visually. Transparency
(alpha) does not work well with colors since the mixing of overlapping
transparent colors will no longer represent the colors of the
categories. Binning methods already use color to encode the density of
points in the bin, so color cannot be used to encode categories.

As the number of categories increases, the difference between colors
decreases, to the point that the color of categories will no longer be
visually distinct.

> 5.  Read ?facet\_wrap. What does nrow do? What does ncol do? What
>     other options control the layout of the individual panels? Why
>     doesn’t facet\_grid() have nrow and ncol arguments?

The arguments nrow (ncol) determines the number of rows (columns) to use
when laying out the facets. It is necessary since facet\_wrap() only
facets on one variable.

The nrow and ncol arguments are unnecessary for facet\_grid() since the
number of unique values of the variables specified in the function
determines the number of rows and columns.

> 6.  When using facet\_grid() you should usually put the variable with
>     more unique levels in the columns. Why?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(cyl ~ cty)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

There will be more space horizontally

### 3.6 Geometric objects

A geom is the geometrical object that a plot uses to represent data.
People often describe plots by the type of geom that the plot uses. For
example, bar charts use bar geoms, line charts use line geoms, boxplots
use boxplot geoms, and so on. Scatterplots break the trend; they use the
point geom. As we see above, you can use different geoms to plot the
same data.

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy)) 
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

Every geom function in ggplot2 takes a mapping argument. However, not
every aesthetic works with every geom. You could set the shape of a
point, but you couldn’t set the “shape” of a line. On the other hand,
you could set the linetype of a line. geom\_smooth() will draw a
different line, with a different linetype, for each unique value of the
variable that you map to linetype.

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

Here geom\_smooth() separates the cars into three lines based on their
drv value, which describes a car’s drivetrain. One line describes all of
the points with a 4 value, one line describes all of the points with an
f value, and one line describes all of the points with an r value. Here,
4 stands for four-wheel drive, f for front-wheel drive, and r for
rear-wheel drive

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, group = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, color = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + geom_smooth(mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = drv)) + geom_smooth(mapping = aes(x = displ, y = hwy, color = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

Many geoms, like geom\_smooth(), use a single geometric object to
display multiple rows of data. For these geoms, you can set the group
aesthetic to a categorical variable to draw multiple objects. ggplot2
will draw a separate object for each unique value of the grouping
variable. In practice, ggplot2 will automatically group the data for
these geoms whenever you map an aesthetic to a discrete variable (as in
the linetype example). It is convenient to rely on this feature because
the group aesthetic by itself does not add a legend or distinguishing
features to the geoms.

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + geom_point() + geom_smooth() 
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_smooth() + geom_point(mapping = aes(color = class))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->

> 1.  What geom would you use to draw a line chart? A boxplot? A
>     histogram? An area chart?

For Line charts you would use geom\_line(). For a boxplot you would use
geom\_boxplot(). For a histogram you would use geom.histogram(). For an
area chart you would use geom\_line() again, however, you would need to
fill in the area under the lines \> 2. Run this code in your head and
predict what the output will look like. Then, run the code in R and
check your predictions.

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + geom_point() + geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->
My prediction was nearly right, however, I did not know what se was. By
the looks of the graph, se refers to the standard error of the graph

> 3.  What does show.legend = FALSE do? What happens if you remove it?
>     Why do you think I used it earlier in the chapter?

removes the key, you don’t know otherwise what each color means

> 4.  What does the se argument to geom\_smooth() do?

Removes the standard error shaded part of the line graph

> 5.  Will these two graphs look different? Why/why not?

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-34-1.png)<!-- -->

``` r
ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-35-1.png)<!-- -->

No, they both use the same data and maaping so therefore they will be
the same

``` r
diamonds
```

    ## # A tibble: 53,940 x 10
    ##    carat cut       color clarity depth table price     x     y     z
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1 0.23  Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
    ##  2 0.21  Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
    ##  3 0.23  Good      E     VS1      56.9    65   327  4.05  4.07  2.31
    ##  4 0.290 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
    ##  5 0.31  Good      J     SI2      63.3    58   335  4.34  4.35  2.75
    ##  6 0.24  Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
    ##  7 0.24  Very Good I     VVS1     62.3    57   336  3.95  3.98  2.47
    ##  8 0.26  Very Good H     SI1      61.9    55   337  4.07  4.11  2.53
    ##  9 0.22  Fair      E     VS2      65.1    61   337  3.87  3.78  2.49
    ## 10 0.23  Very Good H     VS1      59.4    61   338  4     4.05  2.39
    ## # … with 53,930 more rows

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut, fill = cut))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-37-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + geom_bar(alpha = 0.2, position = "dodge")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-38-1.png)<!-- -->
