Data Wrangling in R
================
Kaixin Wang
OSCR - Summer Session C 2019

**Note**: Some contents are based on the book *An introduction to data cleaning with R*, by Edwin de Jonge and Mark van der Loo.

1.  To import the input dataset:

``` r
library(readr)
input = read_csv("person_info.csv")
input
```

    ## # A tibble: 10 x 14
    ##    first_name last_name birthday    age state  address  City   phone email
    ##    <chr>      <chr>     <chr>     <int> <chr>  <chr>    <chr>  <chr> <chr>
    ##  1 Carol      Davis     9/29/1996    23 Illin… 1674 Ca… Burr … 312-… curt…
    ##  2 Bruno      Horan     6/11/1995    24 Calif… 1561 St… San D… 858-… guad…
    ##  3 William    Moody     2/27/1997    22 Illin… 541 Jad… Arlin… 979-… roos…
    ##  4 Robin      Steel     8/3/1989     57 Texas  1674 Ca… Josep… 214-… lloy…
    ##  5 Michelle   Roberts   7/17/1995    24 Oregon 1372 Ga… "Port… 503-… ben1…
    ##  6 June       Sneed     3/27/2000    19 Arizo… 2411 Cl… Phoen… 256-… kath…
    ##  7 Curtis     Campbell  3/15/1991    28 Idahol 2760 Sc… Pocat… 979-… just…
    ##  8 Dorothy    Schott    1/2/1997     21 Calif… 2742 Su… Santa… 501-… mega…
    ##  9 Mae        Skinner   3/16/1995    24 Penns… <NA>     Newar… 501-… enri…
    ## 10 David      Victoria  8/2/1996     23 Maine  3327 Ch… Harps… 207-… caro…
    ## # ... with 5 more variables: car_1 <chr>, gpa <dbl>, year <chr>,
    ## #   class_of <int>, online_signiture <chr>

1.  To find the location of the NAs:

``` r
idx = which(is.na(input))   # find the position of the NAs
idx   
```

    ## [1]  59  98 115 118

1.  To find the location where the character "NA", "na", "N/A", or "n/a" are:

``` r
# NAs = c("na", "n/a", "NA", "N/A")
nas = which(input$car_1 == "na" | input$car_1 == "n/a" | input$car_1 == "NA" | input$car_1 == "N/A")
nas
```

    ## [1] 4 6

1.  To find whether one row contains a missing value:

``` r
complete.cases(input$car_1)
```

    ##  [1]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE

1.  To impute the missing values with NA:

``` r
input$car_1[nas] <- NA   # impute with NAs
input$car_1
```

    ##  [1] "6ZUA618"  "982KRK"   "PS9-S917" NA         "6XNK620"  NA        
    ##  [7] "PS9-S917" NA         "WCE-2823" "VDS-5639"

1.  To omit row with missing value(s):

``` r
na.omit(input)   # remove rows that contain any NA
```

    ## # A tibble: 5 x 14
    ##   first_name last_name birthday    age state  address  City   phone email 
    ##   <chr>      <chr>     <chr>     <int> <chr>  <chr>    <chr>  <chr> <chr> 
    ## 1 Carol      Davis     9/29/1996    23 Illin… 1674 Ca… Burr … 312-… curt1…
    ## 2 Bruno      Horan     6/11/1995    24 Calif… 1561 St… San D… 858-… guada…
    ## 3 William    Moody     2/27/1997    22 Illin… 541 Jad… Arlin… 979-… roose…
    ## 4 Curtis     Campbell  3/15/1991    28 Idahol 2760 Sc… Pocat… 979-… juste…
    ## 5 David      Victoria  8/2/1996     23 Maine  3327 Ch… Harps… 207-… carol…
    ## # ... with 5 more variables: car_1 <chr>, gpa <dbl>, year <chr>,
    ## #   class_of <int>, online_signiture <chr>

1.  Typical approaches to handle missing values:

-   impute with `NA`
-   impute with the median/mean of the data

1.  To ignore missing values in calculations:

``` r
# example:
vars <- c(10, 20, NA, 25, 5, 8, NA, 11)
mean(vars)   # NA introduced
```

    ## [1] NA

``` r
mean(vars, na.rm = T)  # ignore the NAs and compute the summary statistics
```

    ## [1] 13.16667
