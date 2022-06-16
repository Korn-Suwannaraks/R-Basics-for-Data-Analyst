# R-Basics-for-Data-Analyst
I am documenting the basics of R for Data analytical task. The Tidyverse package will be the main package understudy.

# Downloading data

Tabular data store in csv format can be saved as a Tibble (a special type of dataframe)
``` r
penguins <- read_csv("palmer_penguins.csv")
```
Let us see the first few records of penguins
``` r
head(penguins)
```
| id | species | island | bill\_length\_mm | bill\_depth\_mm | flipper\_length\_mm | body\_mass\_g | sex | year
|:------------|:-----------------|:--------------------|:----------------------|:--------------------|
| 00007f23    | E                | fitness\_training   | 2017-05-21            | 2017-06-29          |
| 00007f23    | A                | UX\_design          | 2018-09-05            | 2018-10-21          |
| 00007f23    | E                | website\_design     | 2016-06-23            | 2016-07-20          |
| 00007f23    | C                | bread\_baking       | 2018-03-03            | 2018-04-07          |
| 00007f23    | A                | metal\_welding      | 2017-11-29            | 2017-12-27          |
| 00007f23    | D                | metal\_welding      | 2016-03-09            | 2016-04-08          |
| 000080c8    | D                | contemporary\_dance | 2016-10-31            | 2016-11-09          |
| 000080c8    | B                | fitness\_training   | 2018-12-04            | 2019-01-09          |
| 0000ba9c    | D                | R\_beginner         | 2017-08-08            | 2017-09-08          |
| 0000ba9c    | C                | website\_design     | 2018-09-22            | 2018-10-05          |
