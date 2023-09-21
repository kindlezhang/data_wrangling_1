Simple document
================

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

I’m an R Markdown document!

# the address

if the file and pro is in the same document, you can use name directly

``` r
getwd()
```

    ## [1] "D:/Study/master lecture/data science/ds_project/data_wrangling_1"

``` r
my_data = read.csv(file = "FAS_litters.csv")
```

or you can use some shorthand notation \* ~ Home directory \* . Current
working directory \* .. One directory up from current working directory
\* ../.. Two directories up from current working directory

or u can just use a absolute address

``` r
my_data2 = read.csv("./data_import_examples/data_import_examples/FAS_litters.csv")
my_data3 = read.csv("../data_wrangling_1/data_import_examples/data_import_examples/FAS_litters.csv")
```

# Section 2

This function call also prints information about the column parsing.

``` r
my_data = read_csv("FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

use `janitor::clean_names()` to clean up variable names after importing
data. Doing so will take whatever the column names are and convert them
to lower snake case.

``` r
names(my_data)
```

    ## [1] "Group"             "Litter Number"     "GD0 weight"       
    ## [4] "GD18 weight"       "GD of Birth"       "Pups born alive"  
    ## [7] "Pups dead @ birth" "Pups survive"

``` r
my_data = janitor::clean_names(my_data)
names(my_data)
```

    ## [1] "group"           "litter_number"   "gd0_weight"      "gd18_weight"    
    ## [5] "gd_of_birth"     "pups_born_alive" "pups_dead_birth" "pups_survive"

The `package::function` syntax lets you use a function from a package
without loading the whole library. That’s really helpful, because some
packages have functions with the same name.

# view the data

``` r
my_data
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
view(my_data)
head(my_data)
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## 4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ## 5 Con7  #4/2/95/3-3         NA          NA            20               6
    ## 6 Con7  #2/2/95/3-2         NA          NA            20               6
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
tail(my_data, n = 5)
```

    ## # A tibble: 5 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Low8  #100                20          39.2          20               8
    ## 2 Low8  #4/84               21.8        35.2          20               4
    ## 3 Low8  #108                25.6        47.5          20               8
    ## 4 Low8  #99                 23.5        39            20               6
    ## 5 Low8  #110                25.5        42.7          20               7
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
skimr::skim(my_data)
```

|                                                  |         |
|:-------------------------------------------------|:--------|
| Name                                             | my_data |
| Number of rows                                   | 49      |
| Number of columns                                | 8       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |         |
| Column type frequency:                           |         |
| character                                        | 2       |
| numeric                                          | 6       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |         |
| Group variables                                  | None    |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| group         |         0 |             1 |   4 |   4 |     0 |        6 |          0 |
| litter_number |         0 |             1 |   3 |  15 |     0 |       49 |          0 |

**Variable type: numeric**

| skim_variable   | n_missing | complete_rate |  mean |   sd |   p0 |   p25 |   p50 |   p75 | p100 | hist  |
|:----------------|----------:|--------------:|------:|-----:|-----:|------:|------:|------:|-----:|:------|
| gd0_weight      |        15 |          0.69 | 24.38 | 3.28 | 17.0 | 22.30 | 24.10 | 26.67 | 33.4 | ▃▇▇▆▁ |
| gd18_weight     |        17 |          0.65 | 41.52 | 4.05 | 33.4 | 38.88 | 42.25 | 43.80 | 52.7 | ▃▃▇▂▁ |
| gd_of_birth     |         0 |          1.00 | 19.65 | 0.48 | 19.0 | 19.00 | 20.00 | 20.00 | 20.0 | ▅▁▁▁▇ |
| pups_born_alive |         0 |          1.00 |  7.35 | 1.76 |  3.0 |  6.00 |  8.00 |  8.00 | 11.0 | ▁▃▂▇▁ |
| pups_dead_birth |         0 |          1.00 |  0.33 | 0.75 |  0.0 |  0.00 |  0.00 |  0.00 |  4.0 | ▇▂▁▁▁ |
| pups_survive    |         0 |          1.00 |  6.41 | 2.05 |  1.0 |  5.00 |  7.00 |  8.00 |  9.0 | ▁▃▂▇▇ |

read\_\* function: \* col_names: usually TRUE. If FALSE, column names
are X1, X1, … . You can also supply column names. \* na: string vector
containing character expressions for missing values. \* skip: number of
rows to skip before reading data.

``` r
litters_data = read_csv(file = "FAS_litters.csv",
  skip = 10, col_names = FALSE, na = c(" ", "NA"))
```

    ## Rows: 40 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): X1, X2
    ## dbl (6): X3, X4, X5, X6, X7, X8
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

you can give explicit column specifications

``` r
litters_data = read_csv(file = "FAS_litters.csv",
  col_types = cols(
    Group = col_character(),
    `Litter Number` = col_character(),
    `GD0 weight` = col_character(),
    `GD18 weight` = col_double(),
    `GD of Birth` = col_integer(),
    `Pups born alive` = col_integer(),
    `Pups dead @ birth` = col_integer(),
    `Pups survive` = col_integer()
  )
)
tail(litters_data)
```

    ## # A tibble: 6 × 8
    ##   Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##   <chr> <chr>           <chr>                <dbl>         <int>
    ## 1 Low8  #79             25.4                  43.8            19
    ## 2 Low8  #100            20                    39.2            20
    ## 3 Low8  #4/84           21.8                  35.2            20
    ## 4 Low8  #108            25.6                  47.5            20
    ## 5 Low8  #99             23.5                  39              20
    ## 6 Low8  #110            25.5                  42.7            20
    ## # ℹ 3 more variables: `Pups born alive` <int>, `Pups dead @ birth` <int>,
    ## #   `Pups survive` <int>

Note that you don’t have to specify the variable type for every column,
and can only focus on ones that are difficult:

``` r
litters_data = read_csv(file = "FAS_litters.csv",
  col_types = cols(
    Group = col_factor()
  )
)
head(litters_data)
```

    ## # A tibble: 6 × 8
    ##   Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##   <fct> <chr>                  <dbl>         <dbl>         <dbl>
    ## 1 Con7  #85                     19.7          34.7            20
    ## 2 Con7  #1/2/95/2               27            42              19
    ## 3 Con7  #5/5/3/83/3-3           26            41.4            19
    ## 4 Con7  #5/4/2/95/2             28.5          44.1            19
    ## 5 Con7  #4/2/95/3-3             NA            NA              20
    ## 6 Con7  #2/2/95/3-2             NA            NA              20
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

# other file formats

excel

``` r
library(readxl)
mlb11_data = read_excel("mlb11.xlsx", n_max = 20)
head(mlb11_data, 5)
```

    ## # A tibble: 5 × 12
    ##   team         runs at_bats  hits homeruns bat_avg strikeouts stolen_bases  wins
    ##   <chr>       <dbl>   <dbl> <dbl>    <dbl>   <dbl>      <dbl>        <dbl> <dbl>
    ## 1 Texas Rang…   855    5659  1599      210   0.283        930          143    96
    ## 2 Boston Red…   875    5710  1600      203   0.28        1108          102    90
    ## 3 Detroit Ti…   787    5563  1540      169   0.277       1143           49    95
    ## 4 Kansas Cit…   730    5672  1560      129   0.275       1006          153    71
    ## 5 St. Louis …   762    5532  1513      162   0.273        978           57    90
    ## # ℹ 3 more variables: new_onbase <dbl>, new_slug <dbl>, new_obs <dbl>

SAS

``` r
library(haven)
pulse_data = read_sas("public_pulse_data.sas7bdat")
head(pulse_data, 5)
```

    ## # A tibble: 5 × 7
    ##      ID   age Sex   BDIScore_BL BDIScore_01m BDIScore_06m BDIScore_12m
    ##   <dbl> <dbl> <chr>       <dbl>        <dbl>        <dbl>        <dbl>
    ## 1 10003  48.0 male            7            1            2            0
    ## 2 10015  72.5 male            6           NA           NA           NA
    ## 3 10022  58.5 male           14            3            8           NA
    ## 4 10026  72.7 male           20            6           18           16
    ## 5 10035  60.4 male            4            0            1            2

# Base R …

don’t do this

In short, `read_csv` produces tibbles which are very similar to the base
R data frames produced by `read.csv`. However, tibbles have some
features that can help prevent mistakes and unwanted behavior.

``` r
pups_base = read.csv("FAS_pups.csv")
pups_readr = read_csv("FAS_pups.csv")
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
View(pups_base)
View(pups_readr)

pups_base
```

    ##       Litter.Number Sex PD.ears PD.eyes PD.pivot PD.walk
    ## 1               #85   1       4      13        7      11
    ## 2               #85   1       4      13        7      12
    ## 3         #1/2/95/2   1       5      13        7       9
    ## 4         #1/2/95/2   1       5      13        8      10
    ## 5     #5/5/3/83/3-3   1       5      13        8      10
    ## 6     #5/5/3/83/3-3   1       5      14        6       9
    ## 7       #5/4/2/95/2   1      NA      14        5       9
    ## 8       #4/2/95/3-3   1       4      13        6       8
    ## 9       #4/2/95/3-3   1       4      13        7       9
    ## 10      #2/2/95/3-2   1       4      NA        8      10
    ## 11  #1/5/3/83/3-3/2   1       4      NA       NA       9
    ## 12  #1/5/3/83/3-3/2   1       4      NA        7       9
    ## 13  #1/5/3/83/3-3/2   1       4      NA        7       9
    ## 14  #1/5/3/83/3-3/2   1       4      NA        7       9
    ## 15  #1/5/3/83/3-3/2   1       4      NA        7       9
    ## 16              #85   2       4      13        6      11
    ## 17        #1/2/95/2   2       4      13        7       9
    ## 18        #1/2/95/2   2       4      13        7      10
    ## 19        #1/2/95/2   2       5      13        8      10
    ## 20        #1/2/95/2   2       5      13        8      10
    ## 21        #1/2/95/2   2       5      13        6      10
    ## 22    #5/5/3/83/3-3   2       5      13        8      10
    ## 23    #5/5/3/83/3-3   2       5      14        7      10
    ## 24    #5/5/3/83/3-3   2       5      14        8      10
    ## 25      #5/4/2/95/2   2      NA      14        7      10
    ## 26      #5/4/2/95/2   2      NA      14        7      10
    ## 27      #5/4/2/95/2   2      NA      14        7      10
    ## 28      #4/2/95/3-3   2       4      13        5       7
    ## 29      #4/2/95/3-3   2       4      13        7       9
    ## 30      #4/2/95/3-3   2       4      13        6       8
    ## 31      #4/2/95/3-3   2       4      13        7       9
    ## 32      #2/2/95/3-2   2       4      NA        7      10
    ## 33      #2/2/95/3-2   2       4      NA        8      10
    ## 34      #2/2/95/3-2   2       4      NA        8      11
    ## 35  #1/5/3/83/3-3/2   2       4      NA        7       9
    ## 36  #1/5/3/83/3-3/2   2       4      NA        7       9
    ## 37  #1/5/3/83/3-3/2   2       4      NA        7       9
    ## 38  #1/5/3/83/3-3/2   2       4      NA        7       9
    ## 39        #3/83/3-3   1       3      13        4       7
    ## 40        #3/83/3-3   1       3      13       NA       7
    ## 41        #3/83/3-3   1       3      13        5       7
    ## 42        #3/83/3-3   1       3      12        5       8
    ## 43        #3/83/3-3   1       4      13        7       9
    ## 44          #2/95/3   1       4      13        6       9
    ## 45          #2/95/3   1       3      13        4       8
    ## 46          #2/95/3   1       3      13        4       8
    ## 47          #2/95/3   1       3      12        6       8
    ## 48      #3/5/2/2/95   1       4      13        6       8
    ## 49      #3/5/2/2/95   1       4      13        5       8
    ## 50      #3/5/2/2/95   1       4      13        5       8
    ## 51      #3/5/2/2/95   1       4      13        5       8
    ## 52      #5/4/3/83/3   1       4      13        7      10
    ## 53      #5/4/3/83/3   1       4      14        7       9
    ## 54      #5/4/3/83/3   1       4      14        6       9
    ## 55      #5/4/3/83/3   1       4      14        6      10
    ## 56      #5/4/3/83/3   1       4      14        7       9
    ## 57    #1/6/2/2/95-2   1       3      13        7       9
    ## 58    #1/6/2/2/95-2   1       4      13        7       9
    ## 59  #3/5/3/83/3-3-2   1       4      13        8      10
    ## 60  #3/5/3/83/3-3-2   1       4      13        7       9
    ## 61  #3/5/3/83/3-3-2   1       4      13        8      10
    ## 62  #3/5/3/83/3-3-2   1       4      13        8      10
    ## 63        #2/2/95/2   1       5      14        7       9
    ## 64        #2/2/95/2   1       4      14        8      11
    ## 65    #3/6/2/2/95-3   1       3      13        7       9
    ## 66    #3/6/2/2/95-3   1       3      13        7       9
    ## 67    #3/6/2/2/95-3   1       3      13        6       8
    ## 68    #3/6/2/2/95-3   1       3      12        6       8
    ## 69    #3/6/2/2/95-3   1       3      14        6       8
    ## 70        #3/83/3-3   2       3      13       NA       8
    ## 71        #3/83/3-3   2       3      13        4       7
    ## 72        #3/83/3-3   2       3      12        6       8
    ## 73          #2/95/3   2       3      12        6       9
    ## 74          #2/95/3   2       3      13        6       8
    ## 75          #2/95/3   2       4      12        6       9
    ## 76          #2/95/3   2       3      13        6       8
    ## 77      #3/5/2/2/95   2       4      13        6       9
    ## 78      #3/5/2/2/95   2       4      12        5       7
    ## 79      #3/5/2/2/95   2       3      13        5       9
    ## 80      #3/5/2/2/95   2       4      13        5       9
    ## 81      #5/4/3/83/3   2       4      13        7       9
    ## 82      #5/4/3/83/3   2       4      13        7      10
    ## 83      #5/4/3/83/3   2       4      13        7       9
    ## 84    #1/6/2/2/95-2   2       3      13        7       9
    ## 85    #1/6/2/2/95-2   2       3      13        5       8
    ## 86    #1/6/2/2/95-2   2       4      13        7       9
    ## 87    #1/6/2/2/95-2   2       4      13        8      10
    ## 88  #3/5/3/83/3-3-2   2       4      13        4       9
    ## 89  #3/5/3/83/3-3-2   2       4      13        7       9
    ## 90  #3/5/3/83/3-3-2   2       4      13        7      10
    ## 91  #3/5/3/83/3-3-2   2       4      13        7       9
    ## 92        #2/2/95/2   2       4      13        6       8
    ## 93        #2/2/95/2   2       4      13        9      11
    ## 94    #3/6/2/2/95-3   2       3      12        6       8
    ## 95    #3/6/2/2/95-3   2       3      12        7       9
    ## 96            #84/2   1       3      13        5       8
    ## 97            #84/2   1       3      13        7      10
    ## 98            #84/2   1       3      13        4       7
    ## 99             #107   1       4      13        9      11
    ## 100            #107   1       4      13        9      11
    ## 101            #107   1       4      13       10      12
    ## 102            #107   1       4      13        9      11
    ## 103            #107   1       4      13        9      11
    ## 104            #107   1       4      13        9      11
    ## 105            #107   1       4      13       10      12
    ## 106           #85/2   1       4      13        9      11
    ## 107           #85/2   1       4      13       10      12
    ## 108             #98   1       3      13        7      10
    ## 109             #98   1       4      13        9      11
    ## 110             #98   1       4      13        9      11
    ## 111             #98   1       4      13       NA      10
    ## 112             #98   1       3      13        9      11
    ## 113            #102   1       4      13        7      11
    ## 114            #102   1       4      13        9      11
    ## 115            #101   1       3      12       10      12
    ## 116            #101   1       3      13        7       9
    ## 117            #101   1       4      12        6       8
    ## 118            #101   1       4      12        6      11
    ## 119            #111   1       4      13        5      10
    ## 120           #84/2   2       3      13        5      12
    ## 121           #84/2   2       3      13        6       8
    ## 122           #84/2   2       3      12        8      10
    ## 123           #84/2   2       3      13        5       8
    ## 124           #84/2   2       3      13        9      11
    ## 125            #107   2       4      13        8      10
    ## 126           #85/2   2       4      12        9      11
    ## 127           #85/2   2       4      13       10      12
    ## 128           #85/2   2       4      13        9      11
    ## 129           #85/2   2       4      13       10      12
    ## 130             #98   2       2      13        7      10
    ## 131             #98   2       4      13        9      11
    ## 132             #98   2       4      13        7      10
    ## 133             #98   2       3      13        9      11
    ## 134            #102   2       4      14        9      11
    ## 135            #102   2       3      13        8      11
    ## 136            #102   2       3      13        9      11
    ## 137            #102   2       4      13        8      10
    ## 138            #102   2       3      13        9      11
    ## 139            #101   2       3      12        9      12
    ## 140            #101   2       3      14        9      11
    ## 141            #101   2       3      12        6      10
    ## 142            #101   2       4      12        9      11
    ## 143            #101   2       4      12        8      11
    ## 144            #111   2       4      13        5      10
    ## 145            #111   2       4      13        5      10
    ## 146             #59   1       4      14       10      12
    ## 147             #59   1       4      14        8      11
    ## 148             #59   1       4      13       12      12
    ## 149            #103   1       4      13        8      10
    ## 150            #103   1       4      14        7       9
    ## 151            #103   1       3      13        8      10
    ## 152       #1/82/3-2   1       4      13        5      10
    ## 153       #1/82/3-2   1       4      13       NA       8
    ## 154       #3/83/3-2   1       4      13        6       9
    ## 155       #3/83/3-2   1       4      13        6       9
    ## 156       #3/83/3-2   1       4      13        6       8
    ## 157       #3/83/3-2   1       4      13        6       8
    ## 158       #3/83/3-2   1       4      13        6       8
    ## 159       #3/83/3-2   1       4      12        6       9
    ## 160       #2/95/2-2   1       4      13        6       8
    ## 161       #2/95/2-2   1       4      13        6       8
    ## 162       #2/95/2-2   1       4      13        6       8
    ## 163       #2/95/2-2   1       4      13        7       9
    ## 164       #3/82/3-2   1       3      13        6       8
    ## 165       #3/82/3-2   1       4      13        6       8
    ## 166       #4/2/95/2   1       4      14        8      10
    ## 167       #4/2/95/2   1       4      14       NA      11
    ## 168       #4/2/95/2   1       4      14       NA      11
    ## 169       #4/2/95/2   1       4      14        7       9
    ## 170     #5/3/83/5-2   1       4      13        6      10
    ## 171     #5/3/83/5-2   1       4      14       NA      10
    ## 172     #5/3/83/5-2   1       4      14        4      10
    ## 173      #8/110/3-2   1       3      13        6       8
    ## 174      #8/110/3-2   1       3      13        6       8
    ## 175      #8/110/3-2   1       3      13        6       8
    ## 176      #8/110/3-2   1       4      13        6       8
    ## 177            #106   1       3      13       10      12
    ## 178           #94/2   1      NA      13       NA       9
    ## 179             #62   1       5      14       11      13
    ## 180             #62   1       5      15       10      12
    ## 181             #62   1       5      15       11      13
    ## 182             #59   2       4      13       10      12
    ## 183             #59   2       4      13        8      10
    ## 184            #103   2       3      13        7       9
    ## 185            #103   2       3      12        7       9
    ## 186            #103   2       3      13        7       9
    ## 187            #103   2       3      12        7       9
    ## 188            #103   2       3      13        8      10
    ## 189            #103   2       4      13        6       9
    ## 190       #1/82/3-2   2       4      13        8      10
    ## 191       #1/82/3-2   2       4      13        5      10
    ## 192       #1/82/3-2   2       5      13        6      10
    ## 193       #1/82/3-2   2       4      13        8      10
    ## 194       #3/83/3-2   2       4      12       NA       8
    ## 195       #3/83/3-2   2       4      12        6       8
    ## 196       #2/95/2-2   2       4      13        6       9
    ## 197       #2/95/2-2   2       4      13        6       8
    ## 198       #2/95/2-2   2       4      13        5       8
    ## 199       #3/82/3-2   2       4      13        5       8
    ## 200       #3/82/3-2   2       3      12        4       8
    ## 201       #3/82/3-2   2       3      12        6       8
    ## 202       #4/2/95/2   2       4      14        8      11
    ## 203       #4/2/95/2   2       4      14        7       9
    ## 204       #4/2/95/2   2       4      14        7      10
    ## 205     #5/3/83/3-2   2       3      12       NA       8
    ## 206     #5/3/83/3-2   2       3      13       NA      10
    ## 207      #8/110/3-2   2       3      12        4       9
    ## 208      #8/110/3-2   2       3      13        6       8
    ## 209      #8/110/3-2   2       4      14        6       9
    ## 210      #8/110/3-2   2       4      13        6       8
    ## 211      #8/110/3-2   2       4      13        6       8
    ## 212            #106   2       3      14        8      10
    ## 213           #94/2   2      NA      14       11      13
    ## 214           #94/2   2      NA      13       NA       9
    ## 215             #62   2       5      13       10      12
    ## 216             #53   1       4      13       10      12
    ## 217             #53   1       3      13        9      12
    ## 218             #53   1       4      13        8      12
    ## 219             #53   1       3      13       10      12
    ## 220             #53   1       4      13        9      11
    ## 221             #79   1       4      14        9      11
    ## 222             #79   1       4      14       12      14
    ## 223             #79   1       4      14        8      10
    ## 224             #79   1       4      14        6       9
    ## 225             #79   1       4      14       10      13
    ## 226            #100   1       3      13        7       9
    ## 227            #100   1       3      13        8      10
    ## 228           #4/84   1       3      13        7       9
    ## 229           #4/84   1       3      13        6      10
    ## 230           #4/84   1       4      13        7      10
    ## 231            #108   1       3      13        5       7
    ## 232            #108   1       3      12        6       8
    ## 233            #108   1       3      13        6       8
    ## 234            #108   1       3      13        6       8
    ## 235             #99   1      NA      12        8      10
    ## 236             #99   1      NA      13        7       9
    ## 237             #99   1      NA      13        5       9
    ## 238             #99   1      NA      12        6       9
    ## 239            #110   1      NA      12        6       8
    ## 240             #53   2       3      13       11      13
    ## 241             #53   2       4      13       10      12
    ## 242             #79   2       4      13        9      11
    ## 243             #79   2       4      14       12      14
    ## 244            #100   2       4      13        9      11
    ## 245            #100   2       3      13        9      11
    ## 246            #100   2       3      12        9      11
    ## 247            #100   2       3      13        8      10
    ## 248            #100   2       4      12        9      11
    ## 249           #4/84   2       3      13        6      10
    ## 250            #108   2       3      13        6       8
    ## 251            #108   2       3      14        6       8
    ## 252            #108   2       3      13        6      10
    ## 253             #99   2      NA      13        7       9
    ## 254            #110   2      NA      12        7       9
    ## 255            #110   2      NA      12        6       8
    ## 256            #110   2      NA      12        7       9
    ## 257            #110   2      NA      12        7       9
    ## 258            #110   2      NA      12        7       9
    ## 259             #97   1       3      12        7       9
    ## 260             #97   1       3      12        6       8
    ## 261             #97   1       3      12        6       9
    ## 262             #97   1       3      12        7       9
    ## 263             #97   1       3      12        7       9
    ## 264             #97   1       3      12        7       9
    ## 265           #5/93   1       3      12        8      10
    ## 266           #5/93   1       3      13        7       9
    ## 267           #5/93   1       3      13        7       9
    ## 268         #5/93/2   1       4      13        7       9
    ## 269       #7/82/3-2   1       3      12        6       8
    ## 270       #7/82/3-2   1       4      13        5       8
    ## 271       #7/82/3-2   1       3      13        6       8
    ## 272      #7/110/3-2   1       3      14        8      10
    ## 273      #7/110/3-2   1       3      14        8      10
    ## 274      #7/110/3-2   1       4      14        8      10
    ## 275      #7/110/3-2   1       3      14        7      10
    ## 276      #7/110/3-2   1       3      14        8      10
    ## 277      #7/110/3-2   1       3      14        8      10
    ## 278         #2/95/2   1       4      13        7       9
    ## 279         #2/95/2   1       4      13        7       9
    ## 280         #2/95/2   1       4      13        7       9
    ## 281           #82/4   1       4      13        8      10
    ## 282           #82/4   1       3      13        7       9
    ## 283           #82/4   1       4      13        7       9
    ## 284             #97   2       3      12        7       9
    ## 285             #97   2       3      12        6       8
    ## 286           #5/93   2       4      13        7       9
    ## 287           #5/93   2       3      12        7       9
    ## 288           #5/93   2       4      13        7       9
    ## 289           #5/93   2       3      13        7       9
    ## 290           #5/93   2       3      12        7       9
    ## 291           #5/93   2       3      12        7       9
    ## 292         #5/93/2   2       4      14        7       9
    ## 293         #5/93/2   2       5      14        7       9
    ## 294         #5/93/2   2       4      13        7       9
    ## 295         #5/93/2   2       5      14        7       9
    ## 296         #5/93/2   2       4      13        7       9
    ## 297         #5/93/2   2       4      14        6       9
    ## 298         #5/93/2   2       5      13        7       9
    ## 299       #7/82/3-2   2       3      13        6       8
    ## 300       #7/82/3-2   2       3      12        6       8
    ## 301       #7/82/3-2   2       3      12        6       8
    ## 302       #7/82/3-2   2       3      12        6       8
    ## 303      #7/110/3-2   2       4      14        8      10
    ## 304      #7/110/3-2   2       4      14        7       9
    ## 305         #2/95/2   2       4      12        7       9
    ## 306         #2/95/2   2       4      12        6       8
    ## 307         #2/95/2   2       4      13        7       9
    ## 308         #2/95/2   2       4      12        7       9
    ## 309         #2/95/2   2       3      13        6       8
    ## 310         #2/95/2   2       3      13        7       9
    ## 311           #82/4   2       4      13        7       9
    ## 312           #82/4   2       3      13        7       9
    ## 313           #82/4   2       3      13        7       9

``` r
pups_readr
```

    ## # A tibble: 313 × 6
    ##    `Litter Number`   Sex `PD ears` `PD eyes` `PD pivot` `PD walk`
    ##    <chr>           <dbl>     <dbl>     <dbl>      <dbl>     <dbl>
    ##  1 #85                 1         4        13          7        11
    ##  2 #85                 1         4        13          7        12
    ##  3 #1/2/95/2           1         5        13          7         9
    ##  4 #1/2/95/2           1         5        13          8        10
    ##  5 #5/5/3/83/3-3       1         5        13          8        10
    ##  6 #5/5/3/83/3-3       1         5        14          6         9
    ##  7 #5/4/2/95/2         1        NA        14          5         9
    ##  8 #4/2/95/3-3         1         4        13          6         8
    ##  9 #4/2/95/3-3         1         4        13          7         9
    ## 10 #2/2/95/3-2         1         4        NA          8        10
    ## # ℹ 303 more rows

``` r
pups_base$Sex
```

    ##   [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
    ##  [38] 2 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2
    ##  [75] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
    ## [112] 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1
    ## [149] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2
    ## [186] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1
    ## [223] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1
    ## [260] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2
    ## [297] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

``` r
pups_readr$Sex
```

    ##   [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
    ##  [38] 2 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2
    ##  [75] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
    ## [112] 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1
    ## [149] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2
    ## [186] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1
    ## [223] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1
    ## [260] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2
    ## [297] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

# Export data

As a final point, you will sometimes need to export data after you have
imported and cleaned it. The `write_*` functions in `readr` address this
problem.