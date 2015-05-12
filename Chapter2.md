# Introduction to Statistical Learning - Chapter 2 #

## Question 8 ##
Read data from `College.csv`


```r
setwd("~/Dropbox/Code/R/IntroductionToStatisticalLearning")
df = read.csv(file = 'College.csv')
head(df)
```

```
##                              X Private Apps Accept Enroll Top10perc
## 1 Abilene Christian University     Yes 1660   1232    721        23
## 2           Adelphi University     Yes 2186   1924    512        16
## 3               Adrian College     Yes 1428   1097    336        22
## 4          Agnes Scott College     Yes  417    349    137        60
## 5    Alaska Pacific University     Yes  193    146     55        16
## 6            Albertson College     Yes  587    479    158        38
##   Top25perc F.Undergrad P.Undergrad Outstate Room.Board Books Personal PhD
## 1        52        2885         537     7440       3300   450     2200  70
## 2        29        2683        1227    12280       6450   750     1500  29
## 3        50        1036          99    11250       3750   400     1165  53
## 4        89         510          63    12960       5450   450      875  92
## 5        44         249         869     7560       4120   800     1500  76
## 6        62         678          41    13500       3335   500      675  67
##   Terminal S.F.Ratio perc.alumni Expend Grad.Rate
## 1       78      18.1          12   7041        60
## 2       30      12.2          16  10527        56
## 3       66      12.9          30   8735        54
## 4       97       7.7          37  19016        59
## 5       72      11.9           2  10922        15
## 6       73       9.4          11   9727        55
```

Use column `X` as row names and remove it.


```r
rownames(df) = df[,1]
df$X = NULL
head(df)
```

```
##                              Private Apps Accept Enroll Top10perc
## Abilene Christian University     Yes 1660   1232    721        23
## Adelphi University               Yes 2186   1924    512        16
## Adrian College                   Yes 1428   1097    336        22
## Agnes Scott College              Yes  417    349    137        60
## Alaska Pacific University        Yes  193    146     55        16
## Albertson College                Yes  587    479    158        38
##                              Top25perc F.Undergrad P.Undergrad Outstate
## Abilene Christian University        52        2885         537     7440
## Adelphi University                  29        2683        1227    12280
## Adrian College                      50        1036          99    11250
## Agnes Scott College                 89         510          63    12960
## Alaska Pacific University           44         249         869     7560
## Albertson College                   62         678          41    13500
##                              Room.Board Books Personal PhD Terminal
## Abilene Christian University       3300   450     2200  70       78
## Adelphi University                 6450   750     1500  29       30
## Adrian College                     3750   400     1165  53       66
## Agnes Scott College                5450   450      875  92       97
## Alaska Pacific University          4120   800     1500  76       72
## Albertson College                  3335   500      675  67       73
##                              S.F.Ratio perc.alumni Expend Grad.Rate
## Abilene Christian University      18.1          12   7041        60
## Adelphi University                12.2          16  10527        56
## Adrian College                    12.9          30   8735        54
## Agnes Scott College                7.7          37  19016        59
## Alaska Pacific University         11.9           2  10922        15
## Albertson College                  9.4          11   9727        55
```

Look at summary.


```r
summary(df)
```

```
##  Private        Apps           Accept          Enroll       Top10perc   
##  No :212   Min.   :   81   Min.   :   72   Min.   :  35   Min.   : 1.0  
##  Yes:565   1st Qu.:  776   1st Qu.:  604   1st Qu.: 242   1st Qu.:15.0  
##            Median : 1558   Median : 1110   Median : 434   Median :23.0  
##            Mean   : 3002   Mean   : 2019   Mean   : 780   Mean   :27.6  
##            3rd Qu.: 3624   3rd Qu.: 2424   3rd Qu.: 902   3rd Qu.:35.0  
##            Max.   :48094   Max.   :26330   Max.   :6392   Max.   :96.0  
##    Top25perc      F.Undergrad     P.Undergrad       Outstate    
##  Min.   :  9.0   Min.   :  139   Min.   :    1   Min.   : 2340  
##  1st Qu.: 41.0   1st Qu.:  992   1st Qu.:   95   1st Qu.: 7320  
##  Median : 54.0   Median : 1707   Median :  353   Median : 9990  
##  Mean   : 55.8   Mean   : 3700   Mean   :  855   Mean   :10441  
##  3rd Qu.: 69.0   3rd Qu.: 4005   3rd Qu.:  967   3rd Qu.:12925  
##  Max.   :100.0   Max.   :31643   Max.   :21836   Max.   :21700  
##    Room.Board       Books         Personal         PhD       
##  Min.   :1780   Min.   :  96   Min.   : 250   Min.   :  8.0  
##  1st Qu.:3597   1st Qu.: 470   1st Qu.: 850   1st Qu.: 62.0  
##  Median :4200   Median : 500   Median :1200   Median : 75.0  
##  Mean   :4358   Mean   : 549   Mean   :1341   Mean   : 72.7  
##  3rd Qu.:5050   3rd Qu.: 600   3rd Qu.:1700   3rd Qu.: 85.0  
##  Max.   :8124   Max.   :2340   Max.   :6800   Max.   :103.0  
##     Terminal       S.F.Ratio     perc.alumni       Expend     
##  Min.   : 24.0   Min.   : 2.5   Min.   : 0.0   Min.   : 3186  
##  1st Qu.: 71.0   1st Qu.:11.5   1st Qu.:13.0   1st Qu.: 6751  
##  Median : 82.0   Median :13.6   Median :21.0   Median : 8377  
##  Mean   : 79.7   Mean   :14.1   Mean   :22.7   Mean   : 9660  
##  3rd Qu.: 92.0   3rd Qu.:16.5   3rd Qu.:31.0   3rd Qu.:10830  
##  Max.   :100.0   Max.   :39.8   Max.   :64.0   Max.   :56233  
##    Grad.Rate    
##  Min.   : 10.0  
##  1st Qu.: 53.0  
##  Median : 65.0  
##  Mean   : 65.5  
##  3rd Qu.: 78.0  
##  Max.   :118.0
```

Plot `Outstate` versus `Private`.


```r
library(ggplot2)
ggplot(data = df, mapping = aes(x=Outstate, y=Private)) + geom_point()
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 

Create `Elite` variable.


```r
df$Elite = df$Top10perc>50
ggplot(data = df, mapping = aes(x=Outstate, y=Elite)) + geom_point()
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 

## Question 9 ##

Read `Auto` data and remove rows with missing values.


```r
auto = read.csv(file = 'Auto.csv', header = T, na.strings = '?')
# look at rows containing NA
auto[apply(is.na(auto), MARGIN = 1, FUN = any),]
```

```
##      mpg cylinders displacement horsepower weight acceleration year origin
## 33  25.0         4           98         NA   2046         19.0   71      1
## 127 21.0         6          200         NA   2875         17.0   74      1
## 331 40.9         4           85         NA   1835         17.3   80      2
## 337 23.6         4          140         NA   2905         14.3   80      1
## 355 34.5         4          100         NA   2320         15.8   81      2
##                     name
## 33            ford pinto
## 127        ford maverick
## 331 renault lecar deluxe
## 337   ford mustang cobra
## 355          renault 18i
```

```r
# remove rows containing NA
auto = na.omit(auto)
```

`mpg, displacement, horsepower, weight` and `acceleration` are quantitative variables. Rest are qualitative. Convert qualitative variables to factors.


```r
auto$cylinders = as.factor(auto$cylinders)
auto$year = as.factor(auto$year)
auto$origin = as.factor(auto$origin)
# name is already a factor
# look at ranges of quantitative variables
range(auto$mpg)
```

```
## [1]  9.0 46.6
```

```r
range(auto$displacement)
```

```
## [1]  68 455
```

```r
range(auto$horsepower)
```

```
## [1]  46 230
```

```r
range(auto$weight)
```

```
## [1] 1613 5140
```

```r
range(auto$acceleration)
```

```
## [1]  8.0 24.8
```

Look at summary. 


```r
summary(auto)
```

```
##       mpg       cylinders  displacement   horsepower        weight    
##  Min.   : 9.0   3:  4     Min.   : 68   Min.   : 46.0   Min.   :1613  
##  1st Qu.:17.0   4:199     1st Qu.:105   1st Qu.: 75.0   1st Qu.:2225  
##  Median :22.8   5:  3     Median :151   Median : 93.5   Median :2804  
##  Mean   :23.4   6: 83     Mean   :194   Mean   :104.5   Mean   :2978  
##  3rd Qu.:29.0   8:103     3rd Qu.:276   3rd Qu.:126.0   3rd Qu.:3615  
##  Max.   :46.6             Max.   :455   Max.   :230.0   Max.   :5140  
##                                                                       
##   acceleration       year     origin                  name    
##  Min.   : 8.0   73     : 40   1:245   amc matador       :  5  
##  1st Qu.:13.8   78     : 36   2: 68   ford pinto        :  5  
##  Median :15.5   76     : 34   3: 79   toyota corolla    :  5  
##  Mean   :15.5   75     : 30           amc gremlin       :  4  
##  3rd Qu.:17.0   82     : 30           amc hornet        :  4  
##  Max.   :24.8   70     : 29           chevrolet chevette:  4  
##                 (Other):193           (Other)           :365
```

Remove observations 10 to 85, and look at the summary.


```r
summary(auto[-c(10:85),])
```

```
##       mpg       cylinders  displacement   horsepower      weight    
##  Min.   :11.0   3:  3     Min.   : 68   Min.   : 46   Min.   :1649  
##  1st Qu.:18.0   4:166     1st Qu.:100   1st Qu.: 75   1st Qu.:2214  
##  Median :23.9   5:  3     Median :146   Median : 90   Median :2792  
##  Mean   :24.4   6: 71     Mean   :187   Mean   :101   Mean   :2936  
##  3rd Qu.:30.6   8: 73     3rd Qu.:250   3rd Qu.:115   3rd Qu.:3508  
##  Max.   :46.6             Max.   :455   Max.   :230   Max.   :4997  
##                                                                     
##   acceleration       year     origin                         name    
##  Min.   : 8.5   73     : 39   1:194   ford pinto               :  5  
##  1st Qu.:14.0   78     : 36   2: 54   toyota corolla           :  5  
##  Median :15.5   76     : 34   3: 68   amc matador              :  4  
##  Mean   :15.7   75     : 30           chevrolet chevette       :  4  
##  3rd Qu.:17.3   82     : 30           amc hornet               :  3  
##  Max.   :24.8   79     : 29           chevrolet caprice classic:  3  
##                 (Other):118           (Other)                  :292
```

Look at pairwise scatterplots.


```r
pairs(auto)
```

![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10.png) 

## Question 10 ##

Load `Boston` dataset from `MASS` package.


```r
library(MASS)
head(Boston)
```

```
##      crim zn indus chas   nox    rm  age   dis rad tax ptratio black lstat
## 1 0.00632 18  2.31    0 0.538 6.575 65.2 4.090   1 296    15.3 396.9  4.98
## 2 0.02731  0  7.07    0 0.469 6.421 78.9 4.967   2 242    17.8 396.9  9.14
## 3 0.02729  0  7.07    0 0.469 7.185 61.1 4.967   2 242    17.8 392.8  4.03
## 4 0.03237  0  2.18    0 0.458 6.998 45.8 6.062   3 222    18.7 394.6  2.94
## 5 0.06905  0  2.18    0 0.458 7.147 54.2 6.062   3 222    18.7 396.9  5.33
## 6 0.02985  0  2.18    0 0.458 6.430 58.7 6.062   3 222    18.7 394.1  5.21
##   medv
## 1 24.0
## 2 21.6
## 3 34.7
## 4 33.4
## 5 36.2
## 6 28.7
```

How many rows and columns?


```r
dim(Boston)
```

```
## [1] 506  14
```

Look at some pairwise scatterplots of crime rate.


```r
par(mfrow = c(2,2))
plot(Boston$medv, Boston$crim)
plot(Boston$rm, Boston$crim)
plot(Boston$ptratio, Boston$crim)
plot(Boston$age, Boston$crim)
```

![plot of chunk unnamed-chunk-13](figure/unnamed-chunk-13.png) 

Some suburbs have unusually high crime rates.


```r
summary(Boston$crim)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    0.01    0.08    0.26    3.61    3.68   89.00
```

```r
hist(Boston$crim, breaks = 50)
```

![plot of chunk unnamed-chunk-14](figure/unnamed-chunk-14.png) 

Look at suburbs with low median value of homes.


```r
head(Boston[order(Boston$medv),], 20)
```

```
##        crim zn indus chas   nox    rm   age   dis rad tax ptratio  black
## 399 38.3518  0 18.10    0 0.693 5.453 100.0 1.490  24 666    20.2 396.90
## 406 67.9208  0 18.10    0 0.693 5.683 100.0 1.425  24 666    20.2 384.97
## 401 25.0461  0 18.10    0 0.693 5.987 100.0 1.589  24 666    20.2 396.90
## 400  9.9166  0 18.10    0 0.693 5.852  77.8 1.500  24 666    20.2 338.16
## 415 45.7461  0 18.10    0 0.693 4.519 100.0 1.658  24 666    20.2  88.27
## 490  0.1834  0 27.74    0 0.609 5.414  98.3 1.755   4 711    20.1 344.05
## 386 16.8118  0 18.10    0 0.700 5.277  98.1 1.426  24 666    20.2 396.90
## 402 14.2362  0 18.10    0 0.693 6.343 100.0 1.574  24 666    20.2 396.90
## 416 18.0846  0 18.10    0 0.679 6.434 100.0 1.835  24 666    20.2  27.25
## 388 22.5971  0 18.10    0 0.700 5.000  89.5 1.518  24 666    20.2 396.90
## 417 10.8342  0 18.10    0 0.679 6.782  90.8 1.819  24 666    20.2  21.57
## 491  0.2075  0 27.74    0 0.609 5.093  98.0 1.823   4 711    20.1 318.43
## 404 24.8017  0 18.10    0 0.693 5.349  96.0 1.703  24 666    20.2 396.90
## 426 15.8603  0 18.10    0 0.679 5.896  95.4 1.910  24 666    20.2   7.68
## 420 11.8123  0 18.10    0 0.718 6.824  76.5 1.794  24 666    20.2  48.45
## 439 13.6781  0 18.10    0 0.740 5.935  87.9 1.821  24 666    20.2  68.95
## 398  7.6720  0 18.10    0 0.693 5.747  98.9 1.633  24 666    20.2 393.10
## 405 41.5292  0 18.10    0 0.693 5.531  85.4 1.607  24 666    20.2 329.46
## 438 15.1772  0 18.10    0 0.740 6.152 100.0 1.914  24 666    20.2   9.32
## 385 20.0849  0 18.10    0 0.700 4.368  91.2 1.440  24 666    20.2 285.83
##     lstat medv
## 399 30.59  5.0
## 406 22.98  5.0
## 401 26.77  5.6
## 400 29.97  6.3
## 415 36.98  7.0
## 490 23.97  7.0
## 386 30.81  7.2
## 402 20.32  7.2
## 416 29.05  7.2
## 388 31.99  7.4
## 417 25.79  7.5
## 491 29.68  8.1
## 404 19.77  8.3
## 426 24.39  8.3
## 420 22.74  8.4
## 439 34.02  8.4
## 398 19.92  8.5
## 405 27.38  8.5
## 438 26.45  8.7
## 385 30.63  8.8
```

Look at suburbs with high average number of rooms per dwelling.


```r
head(Boston[order(Boston$rm, decreasing = T),], 20)
```

```
##        crim zn indus chas    nox    rm  age   dis rad tax ptratio black
## 365 3.47428  0 18.10    1 0.7180 8.780 82.9 1.905  24 666    20.2 354.6
## 226 0.52693  0  6.20    0 0.5040 8.725 83.0 2.894   8 307    17.4 382.0
## 258 0.61154 20  3.97    0 0.6470 8.704 86.9 1.801   5 264    13.0 389.7
## 263 0.52014 20  3.97    0 0.6470 8.398 91.5 2.288   5 264    13.0 386.9
## 164 1.51902  0 19.58    1 0.6050 8.375 93.9 2.162   5 403    14.7 388.4
## 233 0.57529  0  6.20    0 0.5070 8.337 73.3 3.838   8 307    17.4 385.9
## 268 0.57834 20  3.97    0 0.5750 8.297 67.0 2.422   5 264    13.0 384.5
## 225 0.31533  0  6.20    0 0.5040 8.266 78.3 2.894   8 307    17.4 385.1
## 254 0.36894 22  5.86    0 0.4310 8.259  8.4 8.907   7 330    19.1 396.9
## 234 0.33147  0  6.20    0 0.5070 8.247 70.4 3.652   8 307    17.4 378.9
## 98  0.12083  0  2.89    0 0.4450 8.069 76.0 3.495   2 276    18.0 396.9
## 227 0.38214  0  6.20    0 0.5040 8.040 86.5 3.216   8 307    17.4 387.4
## 205 0.02009 95  2.68    0 0.4161 8.034 31.9 5.118   4 224    14.7 390.6
## 167 2.01019  0 19.58    0 0.6050 7.929 96.2 2.046   5 403    14.7 369.3
## 284 0.01501 90  1.21    1 0.4010 7.923 24.8 5.885   1 198    13.6 395.5
## 196 0.01381 80  0.46    0 0.4220 7.875 32.0 5.648   4 255    14.4 394.2
## 204 0.03510 95  2.68    0 0.4161 7.853 33.2 5.118   4 224    14.7 392.8
## 187 0.05602  0  2.46    0 0.4880 7.831 53.6 3.199   3 193    17.8 392.6
## 99  0.08187  0  2.89    0 0.4450 7.820 36.9 3.495   2 276    18.0 393.5
## 281 0.03578 20  3.33    0 0.4429 7.820 64.5 4.695   5 216    14.9 387.3
##     lstat medv
## 365  5.29 21.9
## 226  4.63 50.0
## 258  5.12 50.0
## 263  5.91 48.8
## 164  3.32 50.0
## 233  2.47 41.7
## 268  7.44 50.0
## 225  4.14 44.8
## 254  3.54 42.8
## 234  3.95 48.3
## 98   4.21 38.7
## 227  3.13 37.6
## 205  2.88 50.0
## 167  3.70 50.0
## 284  3.16 50.0
## 196  2.97 50.0
## 204  3.81 48.5
## 187  4.45 50.0
## 99   3.57 43.8
## 281  3.76 45.4
```










