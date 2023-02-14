Activity 5 - Mini-competition Explorations
================

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
    ## ✔ tibble  3.1.8     ✔ dplyr   1.0.9
    ## ✔ tidyr   1.2.0     ✔ stringr 1.5.0
    ## ✔ readr   2.1.2     ✔ forcats 0.5.2
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

# Loading data

``` r
data <- read_csv('data/allendale-students.csv');
```

    ## Rows: 200 Columns: 7
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): housing, major
    ## dbl (5): distance, scholarship, parents, car, debt
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(data)
```

    ## # A tibble: 6 × 7
    ##   distance scholarship parents   car housing    major     debt
    ##      <dbl>       <dbl>   <dbl> <dbl> <chr>      <chr>    <dbl>
    ## 1       40        1532   0.44      6 off campus STEM     26389
    ## 2       30        7479   0.265     7 on campus  STEM     21268
    ## 3      130        2664   0.115     3 on campus  business 32312
    ## 4      120        1998   0.325     9 on campus  business 28539
    ## 5       30        1462   0.105    10 off campus other    34867
    ## 6        0        3053   0.335     9 off campus STEM     18193

## Coding non-numeric variables

``` r
# Taking off-campus as 0 and on-campus as 1
data %>% mutate(housing_coded = if_else(housing == 'off campus', 0, 1))
```

    ## # A tibble: 200 × 8
    ##    distance scholarship parents   car housing    major     debt housing_coded
    ##       <dbl>       <dbl>   <dbl> <dbl> <chr>      <chr>    <dbl>         <dbl>
    ##  1       40        1532   0.44      6 off campus STEM     26389             0
    ##  2       30        7479   0.265     7 on campus  STEM     21268             1
    ##  3      130        2664   0.115     3 on campus  business 32312             1
    ##  4      120        1998   0.325     9 on campus  business 28539             1
    ##  5       30        1462   0.105    10 off campus other    34867             0
    ##  6        0        3053   0.335     9 off campus STEM     18193             0
    ##  7       30        1301   0.375     5 off campus business 29990             0
    ##  8       50        1948   0.185     6 off campus business 34333             0
    ##  9       10        2295   0.225     8 on campus  STEM     27717             1
    ## 10       10        4653   0.185     3 off campus STEM     21398             0
    ## # … with 190 more rows

``` r
# Taking major other=0, business=1, STEM=2
data %>% mutate(major_coded = if_else(major == 'other', 0, if_else(major == 'business', 1, 2)))
```

    ## # A tibble: 200 × 8
    ##    distance scholarship parents   car housing    major     debt major_coded
    ##       <dbl>       <dbl>   <dbl> <dbl> <chr>      <chr>    <dbl>       <dbl>
    ##  1       40        1532   0.44      6 off campus STEM     26389           2
    ##  2       30        7479   0.265     7 on campus  STEM     21268           2
    ##  3      130        2664   0.115     3 on campus  business 32312           1
    ##  4      120        1998   0.325     9 on campus  business 28539           1
    ##  5       30        1462   0.105    10 off campus other    34867           0
    ##  6        0        3053   0.335     9 off campus STEM     18193           2
    ##  7       30        1301   0.375     5 off campus business 29990           1
    ##  8       50        1948   0.185     6 off campus business 34333           1
    ##  9       10        2295   0.225     8 on campus  STEM     27717           2
    ## 10       10        4653   0.185     3 off campus STEM     21398           2
    ## # … with 190 more rows
