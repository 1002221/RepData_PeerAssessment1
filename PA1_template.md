# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

Read csv, put into data.frame.

```r
activity = read.csv('activity.csv')
df = data.frame(activity)
```

## What is mean total number of steps taken per day?


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
df_steps <- data.frame(df %>% 
  group_by(date) %>% 
  summarise(count = sum(steps),
            mean = mean(steps, na.rm=TRUE),
            median = median(steps, na.rm=TRUE)))
rownames(df_steps) = df_steps$date
df_steps$date = NULL
df_steps[,'count', drop=FALSE]
```

```
##            count
## 2012-10-01    NA
## 2012-10-02   126
## 2012-10-03 11352
## 2012-10-04 12116
## 2012-10-05 13294
## 2012-10-06 15420
## 2012-10-07 11015
## 2012-10-08    NA
## 2012-10-09 12811
## 2012-10-10  9900
## 2012-10-11 10304
## 2012-10-12 17382
## 2012-10-13 12426
## 2012-10-14 15098
## 2012-10-15 10139
## 2012-10-16 15084
## 2012-10-17 13452
## 2012-10-18 10056
## 2012-10-19 11829
## 2012-10-20 10395
## 2012-10-21  8821
## 2012-10-22 13460
## 2012-10-23  8918
## 2012-10-24  8355
## 2012-10-25  2492
## 2012-10-26  6778
## 2012-10-27 10119
## 2012-10-28 11458
## 2012-10-29  5018
## 2012-10-30  9819
## 2012-10-31 15414
## 2012-11-01    NA
## 2012-11-02 10600
## 2012-11-03 10571
## 2012-11-04    NA
## 2012-11-05 10439
## 2012-11-06  8334
## 2012-11-07 12883
## 2012-11-08  3219
## 2012-11-09    NA
## 2012-11-10    NA
## 2012-11-11 12608
## 2012-11-12 10765
## 2012-11-13  7336
## 2012-11-14    NA
## 2012-11-15    41
## 2012-11-16  5441
## 2012-11-17 14339
## 2012-11-18 15110
## 2012-11-19  8841
## 2012-11-20  4472
## 2012-11-21 12787
## 2012-11-22 20427
## 2012-11-23 21194
## 2012-11-24 14478
## 2012-11-25 11834
## 2012-11-26 11162
## 2012-11-27 13646
## 2012-11-28 10183
## 2012-11-29  7047
## 2012-11-30    NA
```

## What is the average daily activity pattern?

Histogram of steps taken per day:

```r
hist(df_steps$count)
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)<!-- -->
Mean and median of steps per day:

```r
df_steps[, 'mean', drop=FALSE]
```

```
##                  mean
## 2012-10-01        NaN
## 2012-10-02  0.4375000
## 2012-10-03 39.4166667
## 2012-10-04 42.0694444
## 2012-10-05 46.1597222
## 2012-10-06 53.5416667
## 2012-10-07 38.2465278
## 2012-10-08        NaN
## 2012-10-09 44.4826389
## 2012-10-10 34.3750000
## 2012-10-11 35.7777778
## 2012-10-12 60.3541667
## 2012-10-13 43.1458333
## 2012-10-14 52.4236111
## 2012-10-15 35.2048611
## 2012-10-16 52.3750000
## 2012-10-17 46.7083333
## 2012-10-18 34.9166667
## 2012-10-19 41.0729167
## 2012-10-20 36.0937500
## 2012-10-21 30.6284722
## 2012-10-22 46.7361111
## 2012-10-23 30.9652778
## 2012-10-24 29.0104167
## 2012-10-25  8.6527778
## 2012-10-26 23.5347222
## 2012-10-27 35.1354167
## 2012-10-28 39.7847222
## 2012-10-29 17.4236111
## 2012-10-30 34.0937500
## 2012-10-31 53.5208333
## 2012-11-01        NaN
## 2012-11-02 36.8055556
## 2012-11-03 36.7048611
## 2012-11-04        NaN
## 2012-11-05 36.2465278
## 2012-11-06 28.9375000
## 2012-11-07 44.7326389
## 2012-11-08 11.1770833
## 2012-11-09        NaN
## 2012-11-10        NaN
## 2012-11-11 43.7777778
## 2012-11-12 37.3784722
## 2012-11-13 25.4722222
## 2012-11-14        NaN
## 2012-11-15  0.1423611
## 2012-11-16 18.8923611
## 2012-11-17 49.7881944
## 2012-11-18 52.4652778
## 2012-11-19 30.6979167
## 2012-11-20 15.5277778
## 2012-11-21 44.3993056
## 2012-11-22 70.9270833
## 2012-11-23 73.5902778
## 2012-11-24 50.2708333
## 2012-11-25 41.0902778
## 2012-11-26 38.7569444
## 2012-11-27 47.3819444
## 2012-11-28 35.3576389
## 2012-11-29 24.4687500
## 2012-11-30        NaN
```

```r
df_steps[,'median', drop=FALSE]
```

```
##            median
## 2012-10-01     NA
## 2012-10-02      0
## 2012-10-03      0
## 2012-10-04      0
## 2012-10-05      0
## 2012-10-06      0
## 2012-10-07      0
## 2012-10-08     NA
## 2012-10-09      0
## 2012-10-10      0
## 2012-10-11      0
## 2012-10-12      0
## 2012-10-13      0
## 2012-10-14      0
## 2012-10-15      0
## 2012-10-16      0
## 2012-10-17      0
## 2012-10-18      0
## 2012-10-19      0
## 2012-10-20      0
## 2012-10-21      0
## 2012-10-22      0
## 2012-10-23      0
## 2012-10-24      0
## 2012-10-25      0
## 2012-10-26      0
## 2012-10-27      0
## 2012-10-28      0
## 2012-10-29      0
## 2012-10-30      0
## 2012-10-31      0
## 2012-11-01     NA
## 2012-11-02      0
## 2012-11-03      0
## 2012-11-04     NA
## 2012-11-05      0
## 2012-11-06      0
## 2012-11-07      0
## 2012-11-08      0
## 2012-11-09     NA
## 2012-11-10     NA
## 2012-11-11      0
## 2012-11-12      0
## 2012-11-13      0
## 2012-11-14     NA
## 2012-11-15      0
## 2012-11-16      0
## 2012-11-17      0
## 2012-11-18      0
## 2012-11-19      0
## 2012-11-20      0
## 2012-11-21      0
## 2012-11-22      0
## 2012-11-23      0
## 2012-11-24      0
## 2012-11-25      0
## 2012-11-26      0
## 2012-11-27      0
## 2012-11-28      0
## 2012-11-29      0
## 2012-11-30     NA
```
Plot average steps for each 5-minute interval:

```r
df_intervals = data.frame(df %>% 
  group_by(interval) %>% 
  summarise(mean = mean(steps, na.rm=TRUE)))
df$date = as.Date(df$date)
```

```
## Warning in strptime(xx, f <- "%Y-%m-%d", tz = "GMT"): unknown timezone
## 'zone/tz/2018c.1.0/zoneinfo/Europe/London'
```

```r
plot(df_intervals$interval, y = df_intervals$mean, plot.type = 'l')
```

```
## Warning in plot.window(...): "plot.type" is not a graphical parameter
```

```
## Warning in plot.xy(xy, type, ...): "plot.type" is not a graphical parameter
```

```
## Warning in axis(side = side, at = at, labels = labels, ...): "plot.type" is
## not a graphical parameter

## Warning in axis(side = side, at = at, labels = labels, ...): "plot.type" is
## not a graphical parameter
```

```
## Warning in box(...): "plot.type" is not a graphical parameter
```

```
## Warning in title(...): "plot.type" is not a graphical parameter
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
apply(df_intervals, MARGIN = 2, function(x) max(x, na.rm=TRUE))
```

```
##  interval      mean 
## 2355.0000  206.1698
```

## Imputing missing values
Number of missing values

```r
sum(is.na(df$steps))
```

```
## [1] 2304
```
Impute mean of each 5-minute interval:

```r
df_copy = cbind(df)
for (i in unique(df_copy$interval))
    df_copy[df_copy$interval==i & is.na(df_copy$steps),'steps']=df_intervals[df_intervals$interval==i,'mean']
df_copy_steps <- data.frame(df_copy %>% 
  group_by(date) %>% 
  summarise(count = sum(steps),
            mean = mean(steps, na.rm=TRUE),
            median = median(steps, na.rm=TRUE)))
```

```r
hist(df_copy_steps$count)
```

![](PA1_template_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

## Are there differences in activity patterns between weekdays and weekends?

Make weekdays variable:


```r
df_copy$weekday = weekdays(df_copy$date)
df_copy$day_type = ifelse(df_copy$weekday=='Saturday' | df_copy$weekday=='Sunday', 'Weekend', 'Weekday')

df_copy_intervals = data.frame(df_copy %>% 
  group_by(interval, day_type) %>% 
  summarise(mean = mean(steps, na.rm=TRUE)))
```
Plot:

```r
library('ggplot2')
ggplot(data=df_copy_intervals, aes(x=interval, y=mean))+geom_line()+facet_wrap(~day_type, nrow=2)
```

![](PA1_template_files/figure-html/unnamed-chunk-10-1.png)<!-- -->
