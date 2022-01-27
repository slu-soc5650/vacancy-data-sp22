Create 2022 Data - Vacancy
================
Christopher Prener, Ph.D.
(January 27, 2022)

## Introduction

This notebook creates the vacancy data for the Spring 2022 final
projects.

## Dependencies

This notebook requires:

``` r
# tidyverse packages
library(dplyr)
library(readr)

# other packages
library(here)
```

## Raw Data

This notebook requires data that can be automatically downloaded from
the [Vacancy Collaborative’s](https://www.stlvacancytools.com) open data
portal:

``` r
vacant <- read_csv("https://www.publicgoodness.org/stlv/csv/stl_vacancy_data.csv",
                   col_types = cols(Handle = col_character()))
```

    ## Warning: One or more parsing issues, see `problems()` for details

## Subset

There are some variables that we’ll get rid of before exporting the
data:

``` r
vacant %>% 
  select(-c("Ward20", "Ward10", "NhdName", "CensTract20", "CensTract10")) %>%
  relocate(Lat, Lng, .after = last_col()) -> vacant
```

## Write Data

Finally, we’ll write the data to `.csv`:

``` r
write_csv(vacant, here("data", "vacant.csv"))
```
