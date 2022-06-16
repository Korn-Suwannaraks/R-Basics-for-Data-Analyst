# R-Basics-for-Data-Analyst
I am documenting the basics of R for Data analytical task. The Tidyverse package will be the main package used for this purpose.

# Download and install the `Tidyverse` package
``` r
install.packages('tidyverse')
library(tidyverse)
```
# Reading data

Tabular data store in csv format can be saved as a Tibble (a special type of dataframe)
For this tutorial, we shall use the palmer penguin database as an example
``` r
penguins <- read_csv("palmer_penguins.csv")
```
Let us see the first few records of penguins and its data types using `head`
``` r
head(penguins)
```
![head(penguin)](https://user-images.githubusercontent.com/107392735/174004223-ea0c35e8-f052-42ee-a8f9-c38b6cb4eca3.PNG)


# Column level manipulation

We can create new column using `mutate` 
``` r
penguins %>% 
  mutate(body_mass_kg = body_mass_g/1000)
```
We can change the name of column with `rename`
``` r
penguins <- penguins %>% rename( body_mass = body_mass_g)
```
We can select only certain column with `select`
``` r
new_penguins <- penguins %>% select( id,species,island,sex)
```

# Filtering data

Data can be filter via `filter` 
``` r
penguins %>% 
  filter(island == "biscoe")
```
& = AND , | = OR operator
``` r
penguins %>% 
  filter(island == "biscoe" | species == "Gentoo")
```
Filter using `%in%` in conjuction with a list
``` r
penguins %>% 
  filter(id %in% c(10,20,30))
```

# Ordering data

Data can be order using `arrange`
``` r
penguins %>% 
  arrange(flipper_length_mm , desc(body_mass_g))
```

# Data Aggregation

Common data aggregation that can be perform with `summarize` includes:

-sum()
-mean()
-max()
-min()
-sd()
-n()

Example use of `summarize`
``` r
penguins %>% 
  summarize(max_weight = max(body_mass_g))
```
To store output of `summarize` as numeric value for further calculation, use `as.numeric`
``` r
max_weight <- penguins %>% 
  summarize( max(body_mass_g) ) %>%
  as.numeric()
```

# Group data

Data can be grouped using `group_by` in conjuction with aggregation
``` r
penguins %>% 
  group_by(species) %>%
  summarize( mean_mass = mean(body_mass_g))
```

# Count data

Counting data using n() will not impose any additional grouping
``` r
penguins %>% 
  summarize( number = n() )
```
Counting data using `count()` will automatically perform group by before counting
``` r
penguins %>% 
  count(species)
```

# Miscellaneous manipulation function

## top_n 

return top n number of row based on a field 
``` r
penguins %>% 
  top_n(3,body_mass_g)
```

# Visualization

Visualization can be created using `ggplot` package (part of the core Tidyverse package)
GGPLOT is designed to directly utilize data inside of a Tibble 
Note that ggplot() can be used inside pipe %>% structure

## Scatter plot

Create scatter plot with grouping by color, by size and by sex

``` r
ggplot(penguins , aes(x = flipper_length_mm, y = body_mass_g, color = species, size = island, shape = sex)) +
  geom_point()
```
![Rplot](https://user-images.githubusercontent.com/107392735/174025905-976c4aac-73de-4163-9e3c-41fd27a9aded.png)
## Line plot

Create line plot, point-by-point
``` r
ggplot(penguins , aes(x = id, y = body_mass_g)) +
  geom_line()
```

## Bar plot

create bar plot with `+geom_bar`
need only one input, group_by and counts n() will apply automatically
``` r
ggplot(penguins , aes(x = species)) +
  geom_bar()
```

create bar plot with `+geom_col`
need two input, can be create after using aggregate function such as `summarize`
``` r
result <- penguins %>% 
  group_by(species) %>%
  summarize(avgweight=mean(body_mass_g))
  
ggplot(result , aes(x=species,y=avgweight)) +
  geom_col()
```

## Histogram
``` r
ggplot(penguins, aes(x = body_mass_g)) +
  geom_histogram(bins = 10)
```

## Boxplot
``` r
ggplot(penguins, aes(x = species, y = body_mass_g)) +
  geom_boxplot()
```

# Adding Text

Add title, subtitle and caption
``` r
+labs( title = " ", subtitle = " ", caption = " ")
```
Add text at specified location
``` r
+annotate( "text", x= ,y= , label = " ")
```

# Faceting

Multiple charts can be shown at the same time by using `facet_grid`
``` r
ggplot(penguins,aes(x=flipper_length_mm,y=body_mass_g)) +
  geom_point() + facet_grid(species ~ island)
```
![Rplot01](https://user-images.githubusercontent.com/107392735/174031260-76862a87-2e67-4637-9ea5-37111ca458f9.png)
# Editing axis

Convert axis to logarithmic scale
``` r
+ scale_x_log10()
```
Indicate starting value of an axis
``` r
+ expand_limits( x = 50 )	
```







