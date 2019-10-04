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

1.  To check the data type of the object:

<!-- -->

1.  `str`() function

``` r
str(input)  # data structure of the object
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    10 obs. of  14 variables:
    ##  $ first_name      : chr  "Carol" "Bruno" "William" "Robin" ...
    ##  $ last_name       : chr  "Davis" "Horan" "Moody" "Steel" ...
    ##  $ birthday        : chr  "9/29/1996" "6/11/1995" "2/27/1997" "8/3/1989" ...
    ##  $ age             : int  23 24 22 57 24 19 28 21 24 23
    ##  $ state           : chr  "Illinois" "California" "Illinois" "Texas" ...
    ##  $ address         : chr  "1674 Carolyns Circle" "1561 Still Street" "541 Jade wood Drive" "1674 Caroly  ns Circle" ...
    ##  $ City            : chr  "Burr Ridge, Illinois(IL), 60527" "San Diego, California(CA), 92111" "Arlington Heights, Illinois(IL), 60004" "Josephine, Texas(TX), 75173" ...
    ##  $ phone           : chr  "312-295-1941" "858-449-3324" "979-614-4038" "214-694-7864" ...
    ##  $ email           : chr  "curt1995@gmail.com" "guadalupe1974@yahoo.com" "roosevelt.fee@hotmail.com" "lloyd2009@hotmail.com" ...
    ##  $ car_1           : chr  "6ZUA618" "982KRK" "PS9-S917" "na" ...
    ##  $ gpa             : num  2.85 3.47 2.78 4.33 3.75 3.6 2.32 3.93 3.85 1.74
    ##  $ year            : chr  "1" "2" "2" "4" ...
    ##  $ class_of        : int  2022 2021 2021 2019 2019 2021 2020 2020 2020 2021
    ##  $ online_signiture: chr  "Don't aim for success if you want it just do what you love and believe in" "In any investment, you expect to have fun and make money." "It's not my fault that people don't appreciate the art of unpunctuality." "The press is the hired agent of a monied system" ...
    ##  - attr(*, "spec")=List of 2
    ##   ..$ cols   :List of 14
    ##   .. ..$ first_name      : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   .. ..$ last_name       : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   .. ..$ birthday        : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   .. ..$ age             : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_integer" "collector"
    ##   .. ..$ state           : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   .. ..$ address         : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   .. ..$ City            : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   .. ..$ phone           : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   .. ..$ email           : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   .. ..$ car_1           : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   .. ..$ gpa             : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_double" "collector"
    ##   .. ..$ year            : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   .. ..$ class_of        : list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_integer" "collector"
    ##   .. ..$ online_signiture: list()
    ##   .. .. ..- attr(*, "class")= chr  "collector_character" "collector"
    ##   ..$ default: list()
    ##   .. ..- attr(*, "class")= chr  "collector_guess" "collector"
    ##   ..- attr(*, "class")= chr "col_spec"

1.  `summary`() function:

``` r
summary(input)  # summary statistics of the object
```

    ##   first_name         last_name           birthday              age       
    ##  Length:10          Length:10          Length:10          Min.   :19.00  
    ##  Class :character   Class :character   Class :character   1st Qu.:22.25  
    ##  Mode  :character   Mode  :character   Mode  :character   Median :23.50  
    ##                                                           Mean   :26.50  
    ##                                                           3rd Qu.:24.00  
    ##                                                           Max.   :57.00  
    ##     state             address              City          
    ##  Length:10          Length:10          Length:10         
    ##  Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character  
    ##                                                          
    ##                                                          
    ##                                                          
    ##     phone              email              car_1                gpa       
    ##  Length:10          Length:10          Length:10          Min.   :1.740  
    ##  Class :character   Class :character   Class :character   1st Qu.:2.797  
    ##  Mode  :character   Mode  :character   Mode  :character   Median :3.535  
    ##                                                           Mean   :3.262  
    ##                                                           3rd Qu.:3.825  
    ##                                                           Max.   :4.330  
    ##      year              class_of    online_signiture  
    ##  Length:10          Min.   :2019   Length:10         
    ##  Class :character   1st Qu.:2020   Class :character  
    ##  Mode  :character   Median :2020   Mode  :character  
    ##                     Mean   :2020                     
    ##                     3rd Qu.:2021                     
    ##                     Max.   :2022

1.  `class`() and `typeof`() functions

``` r
class(input$first_name)  # class of the object
```

    ## [1] "character"

``` r
typeof(input$first_name)  # type of the object
```

    ## [1] "character"

``` r
class(input$age)  # class of the object
```

    ## [1] "integer"

``` r
typeof(input$age)  # type of the object
```

    ## [1] "integer"

1.  Type coercion:

`as.numeric`, `as.logical`, `as.integer`, `as.double`, `as.factor`, and `as.character`

1.  examples:

``` r
age <- input$age 
summary(age)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   19.00   22.25   23.50   26.50   24.00   57.00

``` r
as.double(age)
```

    ##  [1] 23 24 22 57 24 19 28 21 24 23

``` r
as.logical(age)   # to a logical vector
```

    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE

``` r
as.character(age) # to a character vector
```

    ##  [1] "23" "24" "22" "57" "24" "19" "28" "21" "24" "23"

``` r
as.factor(age)    # to a factor
```

    ##  [1] 23 24 22 57 24 19 28 21 24 23
    ## Levels: 19 21 22 23 24 28 57

1.  `as.logical`:

-   if the input is numeric: 0 is converted to FALSE, else converted to TRUE
-   if the input is character: NA produced

1.  `as.factor`:

-   the order of the levels is in alpha-numeric order

1.  Datetime object: `lubridate` library

``` r
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following object is masked from 'package:base':
    ## 
    ##     date

``` r
dates <- c("15/02/2013", "15 Feb 13", "It happened on 15 02 '13")
dmy(dates)
```

    ## [1] "2013-02-15" "2013-02-15" "2013-02-15"

``` r
mdy(input$birthday)
```

    ##  [1] "1996-09-29" "1995-06-11" "1997-02-27" "1989-08-03" "1995-07-17"
    ##  [6] "2000-03-27" "1991-03-15" "1997-01-02" "1995-03-16" "1996-08-02"

Note: There are similar functions for all permutations of d, m and y. Explicitly, all of the following functions exist: `dmy myd ydm mdy dym ymd`.

1.  character manipulation:

<!-- -->

1.  string normalization

``` r
library(stringr)
str_trim(" hello world ")
```

    ## [1] "hello world"

``` r
str_trim(" hello world ", side = "left")
```

    ## [1] "hello world "

``` r
str_trim(" hello world ", side = "right")
```

    ## [1] " hello world"

``` r
toupper("Hello world")
```

    ## [1] "HELLO WORLD"

``` r
tolower("Hello World")
```

    ## [1] "hello world"

``` r
input$City[5]
```

    ## [1] "Portland, Oregon(OR), 97217\n\n"

``` r
input$City[5] = str_trim(input$City[5], side = "right")
input$City[5]
```

    ## [1] "Portland, Oregon(OR), 97217"

1.  approximate string matching

``` r
gender <- c("M", "male ", "Female", "fem.")
grepl("m", gender)
```

    ## [1] FALSE  TRUE  TRUE  TRUE

``` r
grep("m", gender)
```

    ## [1] 2 3 4
