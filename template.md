Simple document
================

## Import some data

I want to import `FAS_litters.csv`

``` r
litters_df <- read.csv("data/FAS_litters.csv")
```

better names:

``` r
#litters_df
head(litters_df)
```

    ##   Group Litter.Number GD0.weight GD18.weight GD.of.Birth Pups.born.alive
    ## 1  Con7           #85       19.7        34.7          20               3
    ## 2  Con7     #1/2/95/2       27.0        42.0          19               8
    ## 3  Con7 #5/5/3/83/3-3       26.0        41.4          19               6
    ## 4  Con7   #5/4/2/95/2       28.5        44.1          19               5
    ## 5  Con7   #4/2/95/3-3         NA          NA          20               6
    ## 6  Con7   #2/2/95/3-2         NA          NA          20               6
    ##   Pups.dead...birth Pups.survive
    ## 1                 4            3
    ## 2                 0            7
    ## 3                 0            5
    ## 4                 1            4
    ## 5                 0            6
    ## 6                 0            4

``` r
tail(litters_df)
```

    ##    Group Litter.Number GD0.weight GD18.weight GD.of.Birth Pups.born.alive
    ## 44  Low8           #79       25.4        43.8          19               8
    ## 45  Low8          #100       20.0        39.2          20               8
    ## 46  Low8         #4/84       21.8        35.2          20               4
    ## 47  Low8          #108       25.6        47.5          20               8
    ## 48  Low8           #99       23.5        39.0          20               6
    ## 49  Low8          #110       25.5        42.7          20               7
    ##    Pups.dead...birth Pups.survive
    ## 44                 0            7
    ## 45                 0            7
    ## 46                 0            4
    ## 47                 0            7
    ## 48                 0            5
    ## 49                 0            6

``` r
view(litters_df)

#names(litters_df)

#litters_df <- janitor::clean_names(litters_df)
```

Here’s `skimr`

``` r
skimr::skim(litters_df)
```

|                                                  |             |
|:-------------------------------------------------|:------------|
| Name                                             | litters\_df |
| Number of rows                                   | 49          |
| Number of columns                                | 8           |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |             |
| Column type frequency:                           |             |
| character                                        | 2           |
| numeric                                          | 6           |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |             |
| Group variables                                  | None        |

Data summary

**Variable type: character**

| skim\_variable | n\_missing | complete\_rate | min | max | empty | n\_unique | whitespace |
|:---------------|-----------:|---------------:|----:|----:|------:|----------:|-----------:|
| Group          |          0 |              1 |   4 |   4 |     0 |         6 |          0 |
| Litter.Number  |          0 |              1 |   3 |  15 |     0 |        49 |          0 |

**Variable type: numeric**

| skim\_variable  | n\_missing | complete\_rate |  mean |   sd |   p0 |   p25 |   p50 |   p75 | p100 | hist  |
|:----------------|-----------:|---------------:|------:|-----:|-----:|------:|------:|------:|-----:|:------|
| GD0.weight      |         15 |           0.69 | 24.38 | 3.28 | 17.0 | 22.30 | 24.10 | 26.67 | 33.4 | ▃▇▇▆▁ |
| GD18.weight     |         17 |           0.65 | 41.52 | 4.05 | 33.4 | 38.88 | 42.25 | 43.80 | 52.7 | ▃▃▇▂▁ |
| GD.of.Birth     |          0 |           1.00 | 19.65 | 0.48 | 19.0 | 19.00 | 20.00 | 20.00 | 20.0 | ▅▁▁▁▇ |
| Pups.born.alive |          0 |           1.00 |  7.35 | 1.76 |  3.0 |  6.00 |  8.00 |  8.00 | 11.0 | ▁▃▂▇▁ |
| Pups.dead…birth |          0 |           1.00 |  0.33 | 0.75 |  0.0 |  0.00 |  0.00 |  0.00 |  4.0 | ▇▂▁▁▁ |
| Pups.survive    |          0 |           1.00 |  6.41 | 2.05 |  1.0 |  5.00 |  7.00 |  8.00 |  9.0 | ▁▃▂▇▇ |

## Arugumets in `read_csv`

``` r
#litters_df <-
 # read_csv(
  #  "data/FAS_litters.csv",
   # skip = 5,
    #col_names = FALSE,
    #na = "Low8"
  #)
```

## Reading from Excel

``` r
mlb11_df <- read_excel("data/mlb11.xlsx")
```

LotR words

``` r
fellow_df <- read_excel("data/LotR_Words.xlsx", range = "B3:D6")
```

## Read a SAS file

``` r
#pulse_df <- read_sas("data/public_pulse_data.sas7bdat")
```
