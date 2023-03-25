---
layout: single
title: "Mini Project Collection"
author: "Minjeong Kim"
date: "2023-03-21"
output:
  md_document:
    variant: markdown_github
    preserve_yaml: true
editor_options: 
  chunk_output_type: inline
---

<style type="text/css">

body, td {
   font-family: 'Merriweather', serif; font-size: 14px;
}
code.r{
  font-family: 'Merriweather', serif; font-size: 12px;
}
pre {
  font-family: 'Merriweather', serif; font-size: 12px
}
h1 {text-align: center;}
h3 {text-align: center;}

</style>

##1. Mini Project 1: Prime Number Generator

The purpose of this mini project is to create a function generating all
prime numbers in a given range. 

**Creating the Function**

``` r
PrimeNum <- function(integers){
  numbers <- rep(TRUE, integers)
  numbers[1] <- FALSE
    beginning.num <-2
  for(i in beginning.num:sqrt(integers)){
    numbers[seq(from = 2 * beginning.num, to = integers, by = beginning.num)] <-FALSE
    beginning.num <- beginning.num + min(which(numbers[3 : integers]))
  }
  return(which(numbers))
}
```

**Results of the Function**

``` r
PrimeNum(30)
```

    ##  [1]  2  3  5  7 11 13 17 19 23 29

``` r
PrimeNum(100)
```

    ##  [1]  2  3  5  7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97

``` r
PrimeNum(1000)
```

    ##   [1]   2   3   5   7  11  13  17  19  23  29  31  37  41  43  47  53  59  61
    ##  [19]  67  71  73  79  83  89  97 101 103 107 109 113 127 131 137 139 149 151
    ##  [37] 157 163 167 173 179 181 191 193 197 199 211 223 227 229 233 239 241 251
    ##  [55] 257 263 269 271 277 281 283 293 307 311 313 317 331 337 347 349 353 359
    ##  [73] 367 373 379 383 389 397 401 409 419 421 431 433 439 443 449 457 461 463
    ##  [91] 467 479 487 491 499 503 509 521 523 541 547 557 563 569 571 577 587 593
    ## [109] 599 601 607 613 617 619 631 641 643 647 653 659 661 673 677 683 691 701
    ## [127] 709 719 727 733 739 743 751 757 761 769 773 787 797 809 811 821 823 827
    ## [145] 829 839 853 857 859 863 877 881 883 887 907 911 919 929 937 941 947 953
    ## [163] 967 971 977 983 991 997

## Mini Project 2: Counting the number of divisors

#### 1. Basic Generator

``` r
Count.div <- function(value) {
  n <- c(1:value)
  ifelse(value%%n == 0,TRUE,FALSE)
  div <- c(ifelse(value%%n == 0,TRUE,FALSE))
  sum(div)
}
```

**Results of the Function**

``` r
Count.div(4)
```

    ## [1] 3

``` r
Count.div(12)
```

    ## [1] 6

``` r
Count.div(13)
```

    ## [1] 2

#### 2. Generator Using For Loop

``` r
#Using for loop

num.div <- function(value) {
  for (i in 1:value) {
    numbers <- 1:value
    ifelse(i%%numbers == 0,TRUE,FALSE)
    div <- c(ifelse(i%%numbers == 0,TRUE,FALSE))
  } 
  sum(div)
}

num.div(4)
```

    ## [1] 3

``` r
num.div(7)
```

    ## [1] 2

#### 3. Generator within Given Range

Counting the number of divisors for all numbers less than and equal to a
given number.

``` r
num.div.all <- function(value){
  seq.num <- 1:value
  num.div <- function(value) {
    for (i in 1:value) {
      numbers <- 1:value
      ifelse(i%%numbers == 0,TRUE,FALSE)
      div <- c(ifelse(i%%numbers == 0,TRUE,FALSE))
    } 
    sum(div)
  } 
  list.div <- lapply(seq.num, num.div)
  unlist(list.div)
}

num.div.all(5)
```

    ## [1] 1 2 2 3 2

## Mini Project 3: Generating numbers with odd number of divisor

**Creating the Function**

``` r
odd.divs <- function(value){
  seq.num <- 1:value
  num.div <- function(value) {
    for (i in 1:value) {
      numbers <- 1:value
      ifelse(i%%numbers == 0,TRUE,FALSE)
      div <- c(ifelse(i%%numbers == 0,TRUE,FALSE))
    } 
    sum(div)
  } 
  list.div <- lapply(seq.num, num.div)
  result <- c(ifelse(as.numeric(list.div)%%2 != 0, T, F))
  which(result)
}
```

**Results of the Function**

``` r
odd.divs(17)
```

    ## [1]  1  4  9 16

``` r
odd.divs(100)
```

    ##  [1]   1   4   9  16  25  36  49  64  81 100

``` r
odd.divs(1000)
```

    ##  [1]   1   4   9  16  25  36  49  64  81 100 121 144 169 196 225 256 289 324 361
    ## [20] 400 441 484 529 576 625 676 729 784 841 900 961

## Mini Project 4: Hotel Problem

If the number of divisors of each door number is even, then the door
would be closed in the end. If the number of divisors of each door
number is odd, then the door would be opened in the end.

**Creating the Function**

``` r
Count.door <- function(value) {
  #Define the number of hotels/employees as seq.num
  seq.num <- 1:value
  #function to count divisor
  num.div <- function(value) {
    for (i in 1:value) {
      numbers <- 1:value
      ifelse(i%%numbers == 0,TRUE,FALSE)
      div <- c(ifelse(i%%numbers == 0,TRUE,FALSE))
    } 
    sum(div)
  }
  #apply "num.div" function to all the number in "seq.num"
  list.div <- lapply(seq.num, num.div)
  #Find if the number of divisors is even or odd
  result <- c(ifelse(as.numeric(list.div)%%2 == 0, FALSE, TRUE))
  #Count number of doors open
  count.result <- sum(result)
  Status <- c(count.result , value-count.result)
  Status
}
```

**Results of the Function**

``` r
Count.door(100)
```

    ## [1] 10 90

``` r
Count.door(200)
```

    ## [1]  14 186
