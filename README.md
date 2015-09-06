
## Overview

Reads data from [www.stockassessment.org](www.stockassessment.org).

There are only two functions in this package:

* `get_sam`: Get a full copy of an assessment directory and stores it on the local computer. 
* `read_sam`: Reads the primary assessment results into R either directly from [www.stockassessment.org](www.stockassessment.org) or from a local directory. The functions returns a `list` that contains two data frames:

    * __rby__: Results by year, columns should be self explanatory for those familar with `sam` output.
    * __rbya__: Results by year and age with the following variables:
        * year
        * age
        * cW: Catch weights
        * dW: Discard weights
        * lW: Landings weights
        * sW: Stock weights
        * fL: Fraction landed
        * m:  Natural mortality
        * mat: Maturity
        * pF: Partial fishing mortality before spawning
        * pM: Partial natural mortality before spawning
        * n:  Stock in numbers
        * f:  Fishing mortality
        * oC: Observed catch
        * pC: Predicted catch
        * rC: Log catch residuals
        * oU1: Observed index 1
        * pU1: Predicted index 1
        * rU1: Log residuals of index 1
        * oU2: ...



## Installing

```
devtools::install_github("einarhjorleifsson/ramsam")
```

## Examples

__Read only principle data from the web and return object to R__:
```
library(ramsam)

d <- read_sam(directory = "WBcod_2015_short", from_web = TRUE)

d$rby
Source: local data frame [21 x 22]

     ssb ssb_std ssb_low ssb_hig  year   fbar fbar_std fbar_low fbar_hig   bio
   (dbl)   (dbl)   (dbl)   (dbl) (int)  (dbl)    (dbl)    (dbl)    (dbl) (dbl)
1  29481  3943.5 21594.0 37368.0  1994 1.0372 0.109390 0.818420 1.255980 45832
2  30400  3166.9 24066.2 36733.8  1995 1.1940 0.119420 0.955160 1.432840 50242
3  38104  4030.6 30042.8 46165.2  1996 1.1194 0.095805 0.927790 1.311010 55911
4  38210  4984.2 28241.6 48178.4  1997 1.1237 0.095138 0.933424 1.313976 56903
5  26513  2575.6 21361.8 31664.2  1998 1.0996 0.097133 0.905334 1.293866 57233
6  37067  3753.5 29560.0 44574.0  1999 1.2050 0.105170 0.994660 1.415340 57761
7  39272  4621.9 30028.2 48515.8  2000 1.1693 0.100100 0.969100 1.369500 52310
8  33923  3187.4 27548.2 40297.8  2001 1.2420 0.109170 1.023660 1.460340 45964
9  26214  2537.8 21138.4 31289.6  2002 1.2203 0.108620 1.003060 1.437540 39053
10 22121  2027.9 18065.2 26176.8  2003 1.0918 0.096837 0.898126 1.285474 37518
..   ...     ...     ...     ...   ...    ...      ...      ...      ...   ...
Variables not shown: bio_std (dbl), bio_low (dbl), bio_hig (dbl), r (dbl),
  r_std (dbl), r_low (dbl), r_hig (dbl), yield (dbl), yield_std (dbl),
  yield_low (dbl), yield_hig (dbl), oY (dbl)


d$rbya
Source: local data frame [168 x 22]

    year   age    cW    dW    fL    lW     m   mat    pF    pM    sW    oC
   (int) (int) (dbl) (dbl) (dbl) (dbl) (dbl) (dbl) (dbl) (dbl) (dbl) (dbl)
1   1994     0 0.114 0.114 0.000 0.114 0.800  0.00     0     0 0.005    NA
2   1994     1 0.404 0.404 0.154 0.404 0.266  0.04     0     0 0.063  5611
3   1994     2 0.799 0.799 0.627 0.799 0.200  0.38     0     0 0.301  7677
4   1994     3 1.341 1.341 0.904 1.341 0.200  0.75     0     0 0.874 15886
5   1994     4 2.377 2.377 0.949 2.377 0.200  0.76     0     0 2.377  2285
6   1994     5 3.903 3.903 0.659 3.903 0.200  1.00     0     0 3.903   119
7   1994     6 4.851 4.851 0.480 4.851 0.200  1.00     0     0 4.851    38
8   1994     7 4.753 4.753 0.591 4.753 0.200  1.00     0     0 4.753    33
9   1995     0 0.044 0.044 0.000 0.044 0.800  0.00     0     0 0.005    NA
10  1995     1 0.358 0.358 0.158 0.358 0.286  0.04     0     0 0.063  4514
..   ...   ...   ...   ...   ...   ...   ...   ...   ...   ...   ...   ...
Variables not shown: oU1 (dbl), oU2 (dbl), pC (dbl), pU1 (dbl), pU2 (dbl), rC
  (dbl), rU1 (dbl), rU2 (dbl), n (dbl), f (dbl)
```

__Get a full copy of the directory onto local computer__:
```
get_sam(directory = "WBcod_2015_short")
dir("WBcod_2015_short")
 [1] "baserun"            "conf"               "data"              
 [4] "index.html?C=D;O=A" "index.html?C=D;O=D" "index.html?C=M;O=A"
 [7] "index.html?C=M;O=D" "index.html?C=N;O=A" "index.html?C=N;O=D"
[10] "index.html?C=S;O=A" "index.html?C=S;O=D" "LO"                
[13] "log"                "make.R"             "Makefile"          
[16] "res"                "RETRO"              "run"               
[19] "SIM"                "src"                "test"     
```
Here one can then read data from local computer into R via:
```
d <- read_sam(directory = "WBcod_2015_short", from_web = FALSE)
```


