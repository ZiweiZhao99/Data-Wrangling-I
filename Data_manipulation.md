Data manipulation
================

## Import some data

I want to import `FAS_litters.csv`

``` r
litters_df <- read.csv("data/FAS_litters.csv")
litters_df <-janitor::clean_names(litters_df)

pups_df <- read_csv("data/FAS_pups.csv")
```

    ## Rows: 313 Columns: 6

    ## ─ Column specification ────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
pups_df <- janitor::clean_names(pups_df)
```

``` r
select(litters_df, group, gd0_weight:gd_of_birth)
select(litters_df, starts_with("pups"))
select(litters_df, -pups_survive)
rename(litters_df, GROUP = group, LiTtEr_NuMbEr = litter_number)
relocate(litters_df, litter_number, pups_survive)
```

``` r
filter(litters_df, gd_of_birth == 20)
filter(litters_df, group == "Con7")
filter(litters_df, gd0_weight > 23)
filter(litters_df, pups_survive !=4)
filter(litters_df, !(group == "Con7"))
filter(litters_df, group %in% c("Con7", "Con8"))
filter(litters_df, group == "Con7", gd_of_birth ==20)
filter(litters_df, group == "Con7" | gd_of_birth ==20)
```

``` r
drop_na(litters_df)
drop_na(litters_df, gd0_weight)
```

Add or change columns

``` r
mutate(litters_df,
       weight_change = gd18_weight - gd0_weight,
       group = str_to_lower(group))
```

    ##    group   litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ## 1   con7             #85       19.7        34.7          20               3
    ## 2   con7       #1/2/95/2       27.0        42.0          19               8
    ## 3   con7   #5/5/3/83/3-3       26.0        41.4          19               6
    ## 4   con7     #5/4/2/95/2       28.5        44.1          19               5
    ## 5   con7     #4/2/95/3-3         NA          NA          20               6
    ## 6   con7     #2/2/95/3-2         NA          NA          20               6
    ## 7   con7 #1/5/3/83/3-3/2         NA          NA          20               9
    ## 8   con8       #3/83/3-3         NA          NA          20               9
    ## 9   con8         #2/95/3         NA          NA          20               8
    ## 10  con8     #3/5/2/2/95       28.5          NA          20               8
    ## 11  con8     #5/4/3/83/3       28.0          NA          19               9
    ## 12  con8   #1/6/2/2/95-2         NA          NA          20               7
    ## 13  con8 #3/5/3/83/3-3-2         NA          NA          20               8
    ## 14  con8       #2/2/95/2         NA          NA          19               5
    ## 15  con8   #3/6/2/2/95-3         NA          NA          20               7
    ## 16  mod7             #59       17.0        33.4          19               8
    ## 17  mod7            #103       21.4        42.1          19               9
    ## 18  mod7       #1/82/3-2         NA          NA          19               6
    ## 19  mod7       #3/83/3-2         NA          NA          19               8
    ## 20  mod7       #2/95/2-2         NA          NA          20               7
    ## 21  mod7       #3/82/3-2       28.0        45.9          20               5
    ## 22  mod7       #4/2/95/2       23.5          NA          19               9
    ## 23  mod7     #5/3/83/5-2       22.6        37.0          19               5
    ## 24  mod7      #8/110/3-2         NA          NA          20               9
    ## 25  mod7            #106       21.7        37.8          20               5
    ## 26  mod7           #94/2       24.4        42.9          19               7
    ## 27  mod7             #62       19.5        35.9          19               7
    ## 28  low7           #84/2       24.3        40.8          20               8
    ## 29  low7            #107       22.6        42.4          20               9
    ## 30  low7           #85/2       22.2        38.5          20               8
    ## 31  low7             #98       23.8        43.8          20               9
    ## 32  low7            #102       22.6        43.3          20              11
    ## 33  low7            #101       23.8        42.7          20               9
    ## 34  low7            #111       25.5        44.6          20               3
    ## 35  low7            #112       23.9        40.5          19               6
    ## 36  mod8             #97       24.5        42.8          20               8
    ## 37  mod8           #5/93         NA        41.1          20              11
    ## 38  mod8         #5/93/2         NA          NA          19               8
    ## 39  mod8       #7/82-3-2       26.9        43.2          20               7
    ## 40  mod8      #7/110/3-2       27.5        46.0          19               8
    ## 41  mod8         #2/95/2       28.5        44.5          20               9
    ## 42  mod8           #82/4       33.4        52.7          20               8
    ## 43  low8             #53       21.8        37.2          20               8
    ## 44  low8             #79       25.4        43.8          19               8
    ## 45  low8            #100       20.0        39.2          20               8
    ## 46  low8           #4/84       21.8        35.2          20               4
    ## 47  low8            #108       25.6        47.5          20               8
    ## 48  low8             #99       23.5        39.0          20               6
    ## 49  low8            #110       25.5        42.7          20               7
    ##    pups_dead_birth pups_survive weight_change
    ## 1                4            3          15.0
    ## 2                0            7          15.0
    ## 3                0            5          15.4
    ## 4                1            4          15.6
    ## 5                0            6            NA
    ## 6                0            4            NA
    ## 7                0            9            NA
    ## 8                1            8            NA
    ## 9                0            8            NA
    ## 10               0            8            NA
    ## 11               0            8            NA
    ## 12               0            6            NA
    ## 13               0            8            NA
    ## 14               0            4            NA
    ## 15               0            7            NA
    ## 16               0            5          16.4
    ## 17               1            9          20.7
    ## 18               0            6            NA
    ## 19               0            8            NA
    ## 20               0            7            NA
    ## 21               0            5          17.9
    ## 22               0            7            NA
    ## 23               0            5          14.4
    ## 24               0            9            NA
    ## 25               0            2          16.1
    ## 26               1            3          18.5
    ## 27               2            4          16.4
    ## 28               0            8          16.5
    ## 29               0            8          19.8
    ## 30               0            6          16.3
    ## 31               0            9          20.0
    ## 32               0            7          20.7
    ## 33               0            9          18.9
    ## 34               2            3          19.1
    ## 35               1            1          16.6
    ## 36               1            8          18.3
    ## 37               0            9            NA
    ## 38               0            8            NA
    ## 39               0            7          16.3
    ## 40               1            8          18.5
    ## 41               0            9          16.0
    ## 42               0            6          19.3
    ## 43               1            7          15.4
    ## 44               0            7          18.4
    ## 45               0            7          19.2
    ## 46               0            4          13.4
    ## 47               0            7          21.9
    ## 48               0            5          15.5
    ## 49               0            6          17.2

## `arrange`

Rearrange the data

``` r
arrange(litters_df, gd_of_birth, gd0_weight)
```

    ##    group   litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ## 1   Mod7             #59       17.0        33.4          19               8
    ## 2   Mod7             #62       19.5        35.9          19               7
    ## 3   Mod7            #103       21.4        42.1          19               9
    ## 4   Mod7     #5/3/83/5-2       22.6        37.0          19               5
    ## 5   Mod7       #4/2/95/2       23.5          NA          19               9
    ## 6   Low7            #112       23.9        40.5          19               6
    ## 7   Mod7           #94/2       24.4        42.9          19               7
    ## 8   Low8             #79       25.4        43.8          19               8
    ## 9   Con7   #5/5/3/83/3-3       26.0        41.4          19               6
    ## 10  Con7       #1/2/95/2       27.0        42.0          19               8
    ## 11  Mod8      #7/110/3-2       27.5        46.0          19               8
    ## 12  Con8     #5/4/3/83/3       28.0          NA          19               9
    ## 13  Con7     #5/4/2/95/2       28.5        44.1          19               5
    ## 14  Con8       #2/2/95/2         NA          NA          19               5
    ## 15  Mod7       #1/82/3-2         NA          NA          19               6
    ## 16  Mod7       #3/83/3-2         NA          NA          19               8
    ## 17  Mod8         #5/93/2         NA          NA          19               8
    ## 18  Con7             #85       19.7        34.7          20               3
    ## 19  Low8            #100       20.0        39.2          20               8
    ## 20  Mod7            #106       21.7        37.8          20               5
    ## 21  Low8             #53       21.8        37.2          20               8
    ## 22  Low8           #4/84       21.8        35.2          20               4
    ## 23  Low7           #85/2       22.2        38.5          20               8
    ## 24  Low7            #107       22.6        42.4          20               9
    ## 25  Low7            #102       22.6        43.3          20              11
    ## 26  Low8             #99       23.5        39.0          20               6
    ## 27  Low7             #98       23.8        43.8          20               9
    ## 28  Low7            #101       23.8        42.7          20               9
    ## 29  Low7           #84/2       24.3        40.8          20               8
    ## 30  Mod8             #97       24.5        42.8          20               8
    ## 31  Low7            #111       25.5        44.6          20               3
    ## 32  Low8            #110       25.5        42.7          20               7
    ## 33  Low8            #108       25.6        47.5          20               8
    ## 34  Mod8       #7/82-3-2       26.9        43.2          20               7
    ## 35  Mod7       #3/82/3-2       28.0        45.9          20               5
    ## 36  Con8     #3/5/2/2/95       28.5          NA          20               8
    ## 37  Mod8         #2/95/2       28.5        44.5          20               9
    ## 38  Mod8           #82/4       33.4        52.7          20               8
    ## 39  Con7     #4/2/95/3-3         NA          NA          20               6
    ## 40  Con7     #2/2/95/3-2         NA          NA          20               6
    ## 41  Con7 #1/5/3/83/3-3/2         NA          NA          20               9
    ## 42  Con8       #3/83/3-3         NA          NA          20               9
    ## 43  Con8         #2/95/3         NA          NA          20               8
    ## 44  Con8   #1/6/2/2/95-2         NA          NA          20               7
    ## 45  Con8 #3/5/3/83/3-3-2         NA          NA          20               8
    ## 46  Con8   #3/6/2/2/95-3         NA          NA          20               7
    ## 47  Mod7       #2/95/2-2         NA          NA          20               7
    ## 48  Mod7      #8/110/3-2         NA          NA          20               9
    ## 49  Mod8           #5/93         NA        41.1          20              11
    ##    pups_dead_birth pups_survive
    ## 1                0            5
    ## 2                2            4
    ## 3                1            9
    ## 4                0            5
    ## 5                0            7
    ## 6                1            1
    ## 7                1            3
    ## 8                0            7
    ## 9                0            5
    ## 10               0            7
    ## 11               1            8
    ## 12               0            8
    ## 13               1            4
    ## 14               0            4
    ## 15               0            6
    ## 16               0            8
    ## 17               0            8
    ## 18               4            3
    ## 19               0            7
    ## 20               0            2
    ## 21               1            7
    ## 22               0            4
    ## 23               0            6
    ## 24               0            8
    ## 25               0            7
    ## 26               0            5
    ## 27               0            9
    ## 28               0            9
    ## 29               0            8
    ## 30               1            8
    ## 31               2            3
    ## 32               0            6
    ## 33               0            7
    ## 34               0            7
    ## 35               0            5
    ## 36               0            8
    ## 37               0            9
    ## 38               0            6
    ## 39               0            6
    ## 40               0            4
    ## 41               0            9
    ## 42               1            8
    ## 43               0            8
    ## 44               0            6
    ## 45               0            8
    ## 46               0            7
    ## 47               0            7
    ## 48               0            9
    ## 49               0            9

``` r
litters_data_raw <- read_csv("data/FAS_litters.csv")
litters_clean_name <- janitor::clean_names(litters_data_raw)
litters_select <- select(litters_clean_name, group, pups_survive)
litters_filtered <- filter(litters_select, group == "Con7")

litters_df <-
  read_csv("data/FAS_litters.csv") %>%
  janitor::clean_names() %>%
  select(group, pups_survive) %>%
  filter(group == "Con7")

litters_filtered
```

    ## # A tibble: 7 × 2
    ##   group pups_survive
    ##   <chr>        <dbl>
    ## 1 Con7             3
    ## 2 Con7             7
    ## 3 Con7             5
    ## 4 Con7             4
    ## 5 Con7             6
    ## 6 Con7             4
    ## 7 Con7             9

``` r
litters_df
```

    ## # A tibble: 7 × 2
    ##   group pups_survive
    ##   <chr>        <dbl>
    ## 1 Con7             3
    ## 2 Con7             7
    ## 3 Con7             5
    ## 4 Con7             4
    ## 5 Con7             6
    ## 6 Con7             4
    ## 7 Con7             9

``` r
litters_df <-
  read_csv("data/FAS_litters.csv") %>%
  janitor::clean_names() %>%
  select(-pups_survive) %>%
  mutate(
    weight_change = gd18_weight - gd0_weight,
    group = str_to_lower(group)
  )%>%
  drop_na(weight_change)%>%
  filter(group %in% c("con7", "con8"))%>%
  select(litter_number, group, weight_change, everything())
```

    ## Rows: 49 Columns: 8

    ## ─ Column specification ────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
