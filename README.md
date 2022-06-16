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







