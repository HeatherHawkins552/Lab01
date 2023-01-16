Lab 01 - Hello R
================
Heather Hawkins
01/12/2023

## Load packages and data

``` r
library(tidyverse) 
library(datasauRus)
```

## Exercises

------------------------------------------------------------------------

### Exercise 1

##### Datasaurus Dozen

1846 rows and 3 columns

3 variables:

dataset: indicates which dataset the data are from

x: x-values

y: y-value

### Exercise 2

Plotted data in the dino dataset:

``` r
dino_data <- datasaurus_dozen %>%
  filter(dataset == "dino")

ggplot(data = dino_data, mapping = aes(x = x, y = y)) +
  geom_point()
```

![](lab-01-hello-r_files/figure-gfm/plot-dino-1.png)<!-- -->

The correlation between `x` and `y` in this dataset:

``` r
dino_data %>%
  summarize(r = cor(x, y))
```

    ## # A tibble: 1 × 1
    ##         r
    ##     <dbl>
    ## 1 -0.0645

### Exercise 3

Plotted data in the star dataset:

``` r
star_data <- datasaurus_dozen %>%
  filter(dataset=="star")

ggplot(data=star_data, mapping=aes(x=x,y=y))+
  geom_point()
```

![](lab-01-hello-r_files/figure-gfm/plot-star-1.png)<!-- -->

Correlation of ‘x’ and ‘y’ for star_data

``` r
star_data %>%
  summarize(r = cor(x, y))
```

    ## # A tibble: 1 × 1
    ##         r
    ##     <dbl>
    ## 1 -0.0630

R seems to be less than the dino_dataset. (0.0015 less)

### Exercise 4

Plotted data for circle_data

``` r
circle_data <- datasaurus_dozen %>%
  filter(dataset=="circle")

ggplot(data=circle_data, mapping=aes(x=x,y=y))+
  geom_point()
```

![](lab-01-hello-r_files/figure-gfm/plot-circle-1.png)<!-- -->

Correlation for ‘x’ and ‘y’ for circle_dataset

``` r
circle_data %>%
  summarize(r = cor(x, y))
```

    ## # A tibble: 1 × 1
    ##         r
    ##     <dbl>
    ## 1 -0.0683

Compared to dino_data, circle data’s r value is slightly bigger (0.0038
more)

### Exercise 5

Plot of all datasets

``` r
ggplot(datasaurus_dozen, aes(x = x, y = y, color = dataset))+
  geom_point()+
  facet_wrap(~ dataset, ncol = 3) +
  theme(legend.position = "none")
```

![](lab-01-hello-r_files/figure-gfm/all%20plots-1.png)<!-- -->

Every dataset’s correlation coefficients

``` r
datasaurus_dozen %>%
  group_by(dataset) %>%
  summarize(r = cor(x, y)) %>%
  print(13)
```

    ## # A tibble:
    ## #   13 × 2
    ##    dataset   
    ##    <chr>     
    ##  1 away      
    ##  2 bullseye  
    ##  3 circle    
    ##  4 dino      
    ##  5 dots      
    ##  6 h_lines   
    ##  7 high_lines
    ##  8 slant_down
    ##  9 slant_up  
    ## 10 star      
    ## 11 v_lines   
    ## 12 wide_lines
    ## 13 x_shape   
    ## # … with 1
    ## #   more
    ## #   variable:
    ## #   r <dbl>
