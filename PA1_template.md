---
title: "Reproducible Research: Peer Assessment 1"
author: "WendyD"
output: 
  html_document:
    keep_md: true
---

## Loading and preprocessing the data
first load the data

```r
data1<-read.csv("activity.csv", header = TRUE, sep = ",")
str(data1)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : chr  "2012-10-01" "2012-10-01" "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

see how many rows the data has

```r
nrow(data1)
```

```
## [1] 17568
```

## What is mean total number of steps taken per day?

```r
sumstep <- aggregate(data1$steps~data1$date,data= data1, FUN = sum)
colnames(sumstep)<- c("date", "steps")
```


Making a histogram for the total number of steps taken per day

```r
hist(sumstep$steps, main = "Total Steps taken each day", xlab="Number Steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

The mean total number of steps taken per day

```r
meanstep<- mean(sumstep$steps)
meanstep
```

```
## [1] 10766.19
```

```r
medianstep<-median(sumstep$steps)
medianstep
```

```
## [1] 10765
```


## What is the average daily activity pattern?
Make a time series plot of the 5-minute interval(x axis) and the average 
number of steps taken, averaged across all days (y-axis)

```r
meanstep_interval <- aggregate(data1$steps~data1$interval, data=data1, mean)
```
Assigning name to the new data frame containing average steps by time interval

```r
colnames(meanstep_interval)<-c("interval", "steps")
```

Plot graph showing average steps across different interval (X axis)

```r
plot(meanstep_interval$interval, meanstep_interval$steps, type="l",xlab="Interval", ylab="Steps", main= "Average Daily Activity Pattern ")
```

![](PA1_template_files/figure-html/unnamed-chunk-8-1.png)<!-- -->
Whoch 5 minute time interval contains the most step

```r
max_step<-max(meanstep_interval$steps)
max_interval<-meanstep_interval$interval[meanstep_interval$steps == max_step]
max_interval
```

```
## [1] 835
```
The 5 minute interval where there is max of average steps taken is 835

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
