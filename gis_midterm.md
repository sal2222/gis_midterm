gis\_midterm
================
Stephen Lewandowski
October 24, 2018

-   [1. Spatial relationship between age and disability in NYC](#spatial-relationship-between-age-and-disability-in-nyc)

1. Spatial relationship between age and disability in NYC
---------------------------------------------------------

Load and tidy the data.

``` r
age <- read_csv(file = "./data/ACS_16_5YR_S0101_with_ann.csv", skip = 1) %>% 
  janitor::clean_names() %>%
  select("id2", "geography", "total_estimate_summary_indicators_median_age_years") %>%
  rename(median_age = total_estimate_summary_indicators_median_age_years) %>% 
  separate(geography, into = c("tract", "county", "state"), sep = ",") %>%
  separate(tract, into = c("drop1", "drop2", "tract"), sep = " ") %>%
  mutate(county = str_trim(county, side = "left")) %>% 
  separate(county, into = c("county", "drop3"), sep = " ") %>%
  select(-(c(drop1, drop2, drop3, state))) %>%
  filter(county == c("New York", "Bronx", "Kings", "Queens", "Richmond")) 

age
```

    ## # A tibble: 376 x 4
    ##            id2 tract county median_age
    ##          <dbl> <chr> <chr>  <chr>     
    ##  1 36005001600 16    Bronx  36.9      
    ##  2 36005002500 25    Bronx  30.4      
    ##  3 36005003300 33    Bronx  26.6      
    ##  4 36005004001 40.01 Bronx  40.2      
    ##  5 36005004600 46    Bronx  33.6      
    ##  6 36005005200 52    Bronx  31.1      
    ##  7 36005006000 60    Bronx  31.0      
    ##  8 36005006500 65    Bronx  30.0      
    ##  9 36005007100 71    Bronx  31.4      
    ## 10 36005007600 76    Bronx  32.5      
    ## # ... with 366 more rows

``` r
disability <- read_csv(file = "./data/ACS_16_5YR_S1810_with_ann.csv")
```
