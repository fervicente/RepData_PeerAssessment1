# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

Define global options for the whole document

```r
knitr::opts_chunk$set(echo=TRUE, warning=FALSE, output=TRUE)
```

Load used libraries, unzip and read data to a data.table variable

```r
library(data.table)
library(ggplot2)
unzip('./activity.zip')
file <- './activity.csv'

data <- data.table(read.csv(file))
str(data)
```

```
## Classes 'data.table' and 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Factor w/ 61 levels "2012-10-01","2012-10-02",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
##  - attr(*, ".internal.selfref")=<externalptr>
```

## What is mean total number of steps taken per day?

Histogram of number of steps per day

```r
daySteps <- data[,list(total=sum(steps)),by=date]
qplot(daySteps$total, geom="histogram") 
```

```
## stat_bin: binwidth defaulted to range/30. Use 'binwidth = x' to adjust this.
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 

Mean and standard deviation number of steps per day:

```r
mean(daySteps$total,na.rm = TRUE)
```

```
## [1] 10766.19
```

```r
sd(daySteps$total,na.rm = TRUE)
```

```
## [1] 4269.18
```

## What is the average daily activity pattern?

Histogram of number of steps per day

```r
dayActivity <- data[,list(total=mean(steps,na.rm=TRUE)),by=interval]
str(dayActivity)
```

```
## Classes 'data.table' and 'data.frame':	288 obs. of  2 variables:
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
##  $ total   : num  1.717 0.3396 0.1321 0.1509 0.0755 ...
##  - attr(*, ".internal.selfref")=<externalptr>
```

```r
max(dayActivity$total,na.rm=TRUE)
```

```
## [1] 206.1698
```

```r
#ggplot2(dayActivity$interval,dayActivity$total) 
#qplot(interval, total, data=dayActivity, geom=c("point"), xlab="5 min day interval", ylab="# steps")
#   main="Average activity pattern in 5 min day interval", 

 qplot(interval, total, data=dayActivity) 
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png) 

```r
#                 xlab("5 min day interval") +
#                 ylab("Average number of steps") +
#                 ggtitle("Average activity pattern in 5 min day interval")
```

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
