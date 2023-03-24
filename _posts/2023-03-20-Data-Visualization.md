---
layout: post
title: "Basic Data Visualization in R"
author: "Minjeong Kim"
date: "2023-02-22"
output:
  md_document:
    variant: markdown_github
    preserve_yaml: true

toc: true
toc_sticky: true
---

<style type="text/css">

body, td {
   font-family: times, serif; font-size: 14px;
}
code.r{
  font-family: times, serif; font-size: 12px;
}
pre {
  font-family: times, serif; font-size: 12px
}
h1 {text-align: center;}
h3 {text-align: center;}
</style>


# **Data Visualization in R**


This is a lecture note for a data science course (“Data Science for
Psychology Major”) at San Francisco State University (lectured by
Dr. Gaurav Suri). This lecture was intended to learn different methods
of data visualization to gather graphical interpretation on given data.

Data Used: mpg, Orange, swiss, a self-created data frame Package Used:
tidyverse

``` r
knitr::opts_knit$set(base.dir = "D:/MJ/study/Personal Project/Github Portfolio/Github Blog/mj-kim904.github.io/_posts", base.url = "/")
knitr::opts_chunk$set(fig.path = "images/")
```

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.4.0      ✔ purrr   1.0.0 
    ## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
    ## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
    ## ✔ readr   2.1.3      ✔ forcats 0.5.2 
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
head(mpg)
```

    ## # A tibble: 6 × 11
    ##   manufacturer model displ  year   cyl trans      drv     cty   hwy fl    class 
    ##   <chr>        <chr> <dbl> <int> <int> <chr>      <chr> <int> <int> <chr> <chr> 
    ## 1 audi         a4      1.8  1999     4 auto(l5)   f        18    29 p     compa…
    ## 2 audi         a4      1.8  1999     4 manual(m5) f        21    29 p     compa…
    ## 3 audi         a4      2    2008     4 manual(m6) f        20    31 p     compa…
    ## 4 audi         a4      2    2008     4 auto(av)   f        21    30 p     compa…
    ## 5 audi         a4      2.8  1999     6 auto(l5)   f        16    26 p     compa…
    ## 6 audi         a4      2.8  1999     6 manual(m5) f        18    26 p     compa…

``` r
# The head() function returns truncated rows.

summary(mpg)
```

    ##  manufacturer          model               displ            year     
    ##  Length:234         Length:234         Min.   :1.600   Min.   :1999  
    ##  Class :character   Class :character   1st Qu.:2.400   1st Qu.:1999  
    ##  Mode  :character   Mode  :character   Median :3.300   Median :2004  
    ##                                        Mean   :3.472   Mean   :2004  
    ##                                        3rd Qu.:4.600   3rd Qu.:2008  
    ##                                        Max.   :7.000   Max.   :2008  
    ##       cyl           trans               drv                 cty       
    ##  Min.   :4.000   Length:234         Length:234         Min.   : 9.00  
    ##  1st Qu.:4.000   Class :character   Class :character   1st Qu.:14.00  
    ##  Median :6.000   Mode  :character   Mode  :character   Median :17.00  
    ##  Mean   :5.889                                         Mean   :16.86  
    ##  3rd Qu.:8.000                                         3rd Qu.:19.00  
    ##  Max.   :8.000                                         Max.   :35.00  
    ##       hwy             fl               class          
    ##  Min.   :12.00   Length:234         Length:234        
    ##  1st Qu.:18.00   Class :character   Class :character  
    ##  Median :24.00   Mode  :character   Mode  :character  
    ##  Mean   :23.44                                        
    ##  3rd Qu.:27.00                                        
    ##  Max.   :44.00

``` r
# The summary() function tells you the various fields and summarizes the quantitative fields.
```

Here is the code for visualization using the ggplot() function.

**[Code]** ggplot(data = <DATA>) + <GEOM_FUNCTION>(mapping =
aes(<MAPPINGS>))

### **Scatter Plot**

**[Code]** ggplot(data = <DATA>) + geom_point(mapping = aes(<MAPPINGS>))

**[Example]**

``` r
#Highway Miles per Gallon vs. Engine Displacement (in litre)
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy))
```

<img src= "../_posts/images/unnamed-chunk-3-1.png">

``` r
#Highway Miles per Gallon vs. City Miles per Gallon
ggplot(data = mpg) +
  geom_point(mapping = aes(x = cty, y = hwy))
```

![](/_posts/images/unnamed-chunk-3-2.png)

### **Bar Graph**

``` r
survey <- data.frame(fruit = c("Apple", "Banana", "Grapes", "Kiwi", "Orange", "Pears"), people=c(40, 50, 30, 15, 35, 20))
survey
```

    ##    fruit people
    ## 1  Apple     40
    ## 2 Banana     50
    ## 3 Grapes     30
    ## 4   Kiwi     15
    ## 5 Orange     35
    ## 6  Pears     20

**[Code]** ggplot(data = <DATA>, aes(<MAPPINGS>)) + geom_bar(stat =
“identity”)

**[Example]**

``` r
ggplot(data = survey, aes(x=fruit, y=people)) +
  geom_bar(stat = "identity")
```

![](/_posts/images/unnamed-chunk-4-1.png)

``` r
#The argument "stat = identity" is telling it not to transform the data.
```

Additional Arguments

``` r
#Make bars with color
ggplot(survey, aes(x=fruit, y=people, fill=fruit)) + 
  geom_bar(stat="identity")
```

![](/_posts/images/unnamed-chunk-5-1.png)

``` r
#Make bars with specific color
ggplot(survey, aes(x=fruit, y=people, fill=fruit)) + 
  geom_bar(stat="identity") +
  scale_fill_manual(values = c("red2", "yellow2", "slateblue4", "green3", "orange", "olivedrab2"))
```

![](/_posts/images/unnamed-chunk-5-2.png)

``` r
#Make bars with grey scale
ggplot(survey, aes(x=fruit, y=people, fill=fruit)) + 
  geom_bar(stat="identity") +
  scale_fill_grey()
```

![](/_posts/images/unnamed-chunk-5-3.png)

``` r
#Make it in different theme
ggplot(survey, aes(x=fruit, y=people, fill=fruit)) + 
  scale_fill_manual(values=c("red2", "yellow2", "slateblue4", "green3", "orange", "olivedrab2")) +
  geom_bar(stat="identity") +
  theme_classic()
```

![](/_posts/images/unnamed-chunk-5-4.png)

``` r
#Modify bar width
ggplot(survey, aes(x=fruit, y=people, fill=fruit)) + 
  scale_fill_manual(values=c("red2", "yellow2", "slateblue4", "green3", "orange", "olivedrab2")) +
  geom_bar(stat="identity", width = 0.5) +
  theme_classic()
```

![](/_posts/images/unnamed-chunk-5-5.png)

``` r
#Add titiles and label axes
ggplot(survey, aes(x=fruit, y=people, fill=fruit)) + 
  scale_fill_manual(values=c("red2", "yellow2", "slateblue4", "green3", "orange", "olivedrab2")) +
  geom_bar(stat="identity", width = 0.5) +
  theme_classic() +
  ggtitle("Favorite fruit survey") +
  xlab("Fruits") +
  ylab("Number of People")
```

![](/_posts/images/unnamed-chunk-5-6.png)

``` r
#add labels 

ggplot(survey, aes(x=fruit, y=people, fill=fruit)) + 
  scale_fill_manual(values=c("red2", "yellow2", "slateblue4", "green3", "orange", "olivedrab2")) +
  geom_bar(stat="identity", width = 0.5) +
  geom_text(aes(label=people), vjust=-0.3, size=3.5) +
  theme_classic() +
  ggtitle("Favorite fruit survey") +
  xlab("Fruits") +
  ylab("Number of People")
```

![](/_posts/images/unnamed-chunk-5-7.png)

### **Line Graph**

Here, we will use a different data set called “Orange”.

**[Code]** ggplot(data = <DATA>) + geom_line(mapping = aes(<MAPPINGS>))

**[Example]**

``` r
#Circumference vs. Age
ggplot(data = Orange) +
  geom_line(mapping = aes(x = age, y = circumference, color = Tree))
```

![](/_posts/images/unnamed-chunk-6-1.png)

Now, we will create a line graph for tree 1 only.

``` r
head(Orange)
```

    ##   Tree  age circumference
    ## 1    1  118            30
    ## 2    1  484            58
    ## 3    1  664            87
    ## 4    1 1004           115
    ## 5    1 1231           120
    ## 6    1 1372           142

``` r
#Select the data for tree 1 and create a new data frame with it
tree_1 <- Orange[which(Orange$Tree==1),]
tree_1
```

    ##   Tree  age circumference
    ## 1    1  118            30
    ## 2    1  484            58
    ## 3    1  664            87
    ## 4    1 1004           115
    ## 5    1 1231           120
    ## 6    1 1372           142
    ## 7    1 1582           145

``` r
ggplot(data = tree_1) +
  geom_line(mapping = aes(x = age, y = circumference))
```

![](/_posts/images/unnamed-chunk-8-1.png)

Additional Arguments

``` r
#Give color to the line
ggplot(data = tree_1) +
  geom_line(mapping = aes(x = age, y = circumference), color = "blue") +
  theme_classic() +
  ggtitle("Tree 1: Circumference vs. Age") +
  xlab("Age") +
  ylab("Circumference")
```

![](/_posts/images/unnamed-chunk-9-1.png)

### **Scatter Plot with Line Added**

In the section, we will use “swiss” data set and learn how to add a line
to a scatter plot.

This data set shows the standardized fertility measure and
socio-economic indicators for each of 47 French-speaking provinces of
Switzerland at about 1888.

``` r
head(swiss)
```

    ##              Fertility Agriculture Examination Education Catholic
    ## Courtelary        80.2        17.0          15        12     9.96
    ## Delemont          83.1        45.1           6         9    84.84
    ## Franches-Mnt      92.5        39.7           5         5    93.40
    ## Moutier           85.8        36.5          12         7    33.77
    ## Neuveville        76.9        43.5          17        15     5.16
    ## Porrentruy        76.1        35.3           9         7    90.57
    ##              Infant.Mortality
    ## Courtelary               22.2
    ## Delemont                 22.2
    ## Franches-Mnt             20.2
    ## Moutier                  20.3
    ## Neuveville               20.6
    ## Porrentruy               26.6

``` r
summary(swiss)
```

    ##    Fertility      Agriculture     Examination      Education    
    ##  Min.   :35.00   Min.   : 1.20   Min.   : 3.00   Min.   : 1.00  
    ##  1st Qu.:64.70   1st Qu.:35.90   1st Qu.:12.00   1st Qu.: 6.00  
    ##  Median :70.40   Median :54.10   Median :16.00   Median : 8.00  
    ##  Mean   :70.14   Mean   :50.66   Mean   :16.49   Mean   :10.98  
    ##  3rd Qu.:78.45   3rd Qu.:67.65   3rd Qu.:22.00   3rd Qu.:12.00  
    ##  Max.   :92.50   Max.   :89.70   Max.   :37.00   Max.   :53.00  
    ##     Catholic       Infant.Mortality
    ##  Min.   :  2.150   Min.   :10.80   
    ##  1st Qu.:  5.195   1st Qu.:18.15   
    ##  Median : 15.140   Median :20.00   
    ##  Mean   : 41.144   Mean   :19.94   
    ##  3rd Qu.: 93.125   3rd Qu.:21.70   
    ##  Max.   :100.000   Max.   :26.60

``` r
str(swiss)
```

    ## 'data.frame':    47 obs. of  6 variables:
    ##  $ Fertility       : num  80.2 83.1 92.5 85.8 76.9 76.1 83.8 92.4 82.4 82.9 ...
    ##  $ Agriculture     : num  17 45.1 39.7 36.5 43.5 35.3 70.2 67.8 53.3 45.2 ...
    ##  $ Examination     : int  15 6 5 12 17 9 16 14 12 16 ...
    ##  $ Education       : int  12 9 5 7 15 7 7 8 7 13 ...
    ##  $ Catholic        : num  9.96 84.84 93.4 33.77 5.16 ...
    ##  $ Infant.Mortality: num  22.2 22.2 20.2 20.3 20.6 26.6 23.6 24.9 21 24.4 ...

``` r
plot(swiss)
```

![](/_posts/images/Swiss%20data-1.png)

First, we will use basic function called “plot()” to graph.

**[Code]** plot(<MAPPINGS>) abline(lm(MAPPINGS)) - For the mapping of
plot() function, x variable comes first followed by y variable. - For
the mapping of abline() function, y variable comes first followed by x
variable.

**[Example]**

``` r
#1) Education vs. Fertility
plot(swiss$Fertility, swiss$Education)
#Add line
abline(lm(swiss$Education ~ swiss$Fertility))
```

![](/_posts/images/plot%20function%20with%20line-1.png)

``` r
#2) Fertility vs. Education
plot(swiss$Education, swiss$Fertility)
#Add line
abline(lm(swiss$Fertility ~ swiss$Education))
```

![](/_posts/images/plot%20function%20with%20line-2.png)

Now we will create the same plot using ggplot()

**[Code]** coef(lm(<VAR2>\~<VAR1>, data = <DATA>))

ggplot(data = <DATA>) + geom_point(mapping = aes(<MAPPINGS>)) +
geom_abline(slope = <SLOPE>, intercept = <INTERCEPT>)

**[Example]**

``` r
ggplot(data = swiss) + 
  geom_point(mapping = aes(x = Education, y = Fertility))
```

![](/_posts/images/unnamed-chunk-10-1.png)

``` r
#Find slope and intercept using coef() function
coef(lm(Fertility ~ Education, data = swiss))
```

    ## (Intercept)   Education 
    ##  79.6100585  -0.8623503

``` r
ggplot(data = swiss) +
  geom_point(mapping = aes(x = Education, y = Fertility)) +
  geom_abline(slope = -0.862, intercept = 79.61)
```

![](/_posts/images/unnamed-chunk-10-2.png)

\*More information about the line can be found in the posting for the
linear regression.
