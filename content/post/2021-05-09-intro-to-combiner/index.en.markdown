---
title: Intro to {combineR}
author: ''
date: '2021-06-09'
slug: intro-to-combiner
categories: []
tags:
  - rstats
  - sports science
subtitle: ''
summary: ''
authors: []
lastmod: '2021-06-09T21:28:32-05:00'
featured: yes
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---



**{combineR}** is a small package developed to easily gather and explore over 20 years of NFL Draft Combine data from [Pro Football Reference.](https://www.pro-football-reference.com/) In addition to being able to pull data, the package also currently supports benchmarking tables for all NFL combine tests by position. This post will walk you through the current functions.

***

## Installation

``` r
#Not yet on CRAN

  
#Install the development version from GitHub  
install.packages("devtools")
devtools::install_github("rmcurtis43/combineR") 
```

***

## How to use combineR

### `pull_combine_data()`


You can pull single season data by simply entering a year (e.g., `2021`) in the `pull_combine_data()` function. 






```r
# piping in the head() function to display just the first few rows
pull_combine_data(2021) %>% 
  head()
```

```
## # A tibble: 6 x 20
##   player   draft_year school   draft_team  draft_round draft_overall_p~ position
##   <chr>         <dbl> <chr>    <chr>             <dbl>            <dbl> <chr>   
## 1 Trevor ~       2021 Clemson  Jacksonvil~           1                1 QB      
## 2 Zach Wi~       2021 BYU      New York J~           1                2 QB      
## 3 Trey La~       2021 North D~ San Franci~           1                3 QB      
## 4 Kyle Pi~       2021 Florida  Atlanta Fa~           1                4 TE      
## 5 Ja'Marr~       2021 LSU      Cincinnati~           1                5 WR      
## 6 Penei S~       2021 Oregon   Detroit Li~           1                7 OL      
## # ... with 13 more variables: position2 <chr>, height_in <dbl>,
## #   height_ft_in <chr>, weight_lbs <dbl>, weight_kg <dbl>, vertical_in <dbl>,
## #   vertical_cm <dbl>, broad_jump_in <dbl>, broad_jump_cm <dbl>, bench <dbl>,
## #   x3cone <dbl>, shuttle <dbl>, x40yd <dbl>
```


You can get data between user defined seasons by using start_year and end_year...


```r
pull_combine_data(start_year = 2019, end_year = 2021) %>%
  head()
```

```
## # A tibble: 6 x 20
##   player   draft_year school  draft_team   draft_round draft_overall_p~ position
##   <chr>         <dbl> <chr>   <chr>              <dbl>            <dbl> <chr>   
## 1 Kyler M~       2019 Oklaho~ Arizona Car~           1                1 QB      
## 2 Nick Bo~       2019 Ohio S~ San Francis~           1                2 DL      
## 3 Quinnen~       2019 Alabama New York Je~           1                3 DL      
## 4 Clelin ~       2019 Clemson Las Vegas R~           1                4 EDGE    
## 5 Devin W~       2019 LSU     Tampa Bay B~           1                5 LB      
## 6 Daniel ~       2019 Duke    New York Gi~           1                6 QB      
## # ... with 13 more variables: position2 <chr>, height_in <dbl>,
## #   height_ft_in <chr>, weight_lbs <dbl>, weight_kg <dbl>, vertical_in <dbl>,
## #   vertical_cm <dbl>, broad_jump_in <dbl>, broad_jump_cm <dbl>, bench <dbl>,
## #   x3cone <dbl>, shuttle <dbl>, x40yd <dbl>
```


Or if you want to pull all data (i.e. 2000-current) then just use `pull_combine_data()` without entering start_year or end_year.


```r
pull_combine_data() %>%
  head()
```

```
## # A tibble: 6 x 20
##   player   draft_year school  draft_team   draft_round draft_overall_p~ position
##   <chr>         <dbl> <chr>   <chr>              <dbl>            <dbl> <chr>   
## 1 Courtne~       2000 Penn S~ Cleveland B~           1                1 DE      
## 2 LaVar A~       2000 Penn S~ Washington ~           1                2 OLB     
## 3 Chris S~       2000 Alabama Washington ~           1                3 OT      
## 4 Peter W~       2000 Florid~ Cincinnati ~           1                4 WR      
## 5 Jamal L~       2000 Tennes~ Baltimore R~           1                5 RB      
## 6 Corey S~       2000 Florid~ Philadelphi~           1                6 DT      
## # ... with 13 more variables: position2 <chr>, height_in <dbl>,
## #   height_ft_in <chr>, weight_lbs <dbl>, weight_kg <dbl>, vertical_in <dbl>,
## #   vertical_cm <dbl>, broad_jump_in <dbl>, broad_jump_cm <dbl>, bench <dbl>,
## #   x3cone <dbl>, shuttle <dbl>, x40yd <dbl>
```


***

### `benchmark_table()`


The `benchmark_table()` funtion was written to provide practitioners with practical scores for benchmarking their athletes performance. Benchmarking is critical to the athlete evaluation process as it provides objective feedback as to how an athlete's physical performance or anthropometrics compare to NFL Combine norms.

The function accepts a single test (e.g. test = '40yd'), followed by a list of positions to be included in the table (e.g. positions = c('DB', 'DL', 'LB', 'OL', 'QB', 'RB', 'TE', 'WR')). Please note tests and positions must be wrapped in parentheses, also the 'positions' input requires a string of characters between c() (i.e., indicates a vector of positions to include in the table).

Accepted inputs for **test** include:

* Height
* Weight
* Vertical Jump
* Broad Jump
* Bench
* 3cone
* Shuttle
* 40yd


Accepted inputs for **positions** include any combination of:

* DB
* DL
* LB
* OL
* QB
* RB
* TE
* WR
* PK
* LS
 


Example below.


```r
benchmark_table(test = '40yd', positions = c('DB', 'DL', 'LB', 'OL', 'QB', 'RB', 'TE', 'WR'))
```
![percentile-table-example](percentile_table_example.png)


You can create a table with a single position as well...

```r
benchmark_table(test = 'Broad Jump', positions = c('LB'))
```
![percentile-table-example-single](percentile_table_example_single.png)



***

This package continues to be developed and will change over time. The goal is to make this as useful to sports scientists, coaches, and practitioners as possible. Please reach out to me on social medial (I'm on [twitter](https://twitter.com/RyanM_Curtis) and [LinkedIn](https://www.linkedin.com/in/ryan-curtis-phd-atc-cscs-d-420aa989/), email, or open up an issue on this [github repo](https://github.com/rmcurtis43/combineR) if you have ideas on how to improve. Thanks and look forward to hearing from you.


![combineR-twitter](combineR_twitter.png)
