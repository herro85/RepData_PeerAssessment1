---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---

## Loading and preprocessing the data


```r
library(datasets)
library(dplyr)
library(ggplot2)

wd <- "~/R Work"
if (!file.exists(wd)) {
  dir.create(wd)
}
setwd(wd)

dataFileZip <-"repdataActivity.zip"
dataFile <- "activity.csv"
if (!file.exists(dataFile)) {
fileUrl <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
download.file(fileUrl, dataFileZip, method="internal")
unzip(dataFileZip)
}
```

Load csv data into data frame. Clean up by removing NA from steps

```r
dataFile <- "~/R Work/activity.csv"
df <- read.csv(dataFile)
clean_data <- filter(df, !is.na(steps))
```
##What is mean total number of steps taken per day?
1. Calculate the total number of steps taken per day

```r
steps_total <- summarise(group_by(clean_data, date), sum(steps))
names(steps_total) <- c("date", "steps")
steps_total
```

```
## Source: local data frame [53 x 2]
## 
##          date steps
## 1  2012-10-02   126
## 2  2012-10-03 11352
## 3  2012-10-04 12116
## 4  2012-10-05 13294
## 5  2012-10-06 15420
## 6  2012-10-07 11015
## 7  2012-10-09 12811
## 8  2012-10-10  9900
## 9  2012-10-11 10304
## 10 2012-10-12 17382
## 11 2012-10-13 12426
## 12 2012-10-14 15098
## 13 2012-10-15 10139
## 14 2012-10-16 15084
## 15 2012-10-17 13452
## 16 2012-10-18 10056
## 17 2012-10-19 11829
## 18 2012-10-20 10395
## 19 2012-10-21  8821
## 20 2012-10-22 13460
## 21 2012-10-23  8918
## 22 2012-10-24  8355
## 23 2012-10-25  2492
## 24 2012-10-26  6778
## 25 2012-10-27 10119
## 26 2012-10-28 11458
## 27 2012-10-29  5018
## 28 2012-10-30  9819
## 29 2012-10-31 15414
## 30 2012-11-02 10600
## 31 2012-11-03 10571
## 32 2012-11-05 10439
## 33 2012-11-06  8334
## 34 2012-11-07 12883
## 35 2012-11-08  3219
## 36 2012-11-11 12608
## 37 2012-11-12 10765
## 38 2012-11-13  7336
## 39 2012-11-15    41
## 40 2012-11-16  5441
## 41 2012-11-17 14339
## 42 2012-11-18 15110
## 43 2012-11-19  8841
## 44 2012-11-20  4472
## 45 2012-11-21 12787
## 46 2012-11-22 20427
## 47 2012-11-23 21194
## 48 2012-11-24 14478
## 49 2012-11-25 11834
## 50 2012-11-26 11162
## 51 2012-11-27 13646
## 52 2012-11-28 10183
## 53 2012-11-29  7047
```

2. If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day

```r
qplot(steps, data = steps_total)
```

```
## stat_bin: binwidth defaulted to range/30. Use 'binwidth = x' to adjust this.
```

![plot of chunk Steps Histogram](figure/Steps Histogram-1.png) 

3. Calculate and report the mean and median of the total number of steps taken per day
Mean

```r
summarise(group_by(clean_data, date), mean(steps))
```

```
## Source: local data frame [53 x 2]
## 
##          date mean(steps)
## 1  2012-10-02   0.4375000
## 2  2012-10-03  39.4166667
## 3  2012-10-04  42.0694444
## 4  2012-10-05  46.1597222
## 5  2012-10-06  53.5416667
## 6  2012-10-07  38.2465278
## 7  2012-10-09  44.4826389
## 8  2012-10-10  34.3750000
## 9  2012-10-11  35.7777778
## 10 2012-10-12  60.3541667
## 11 2012-10-13  43.1458333
## 12 2012-10-14  52.4236111
## 13 2012-10-15  35.2048611
## 14 2012-10-16  52.3750000
## 15 2012-10-17  46.7083333
## 16 2012-10-18  34.9166667
## 17 2012-10-19  41.0729167
## 18 2012-10-20  36.0937500
## 19 2012-10-21  30.6284722
## 20 2012-10-22  46.7361111
## 21 2012-10-23  30.9652778
## 22 2012-10-24  29.0104167
## 23 2012-10-25   8.6527778
## 24 2012-10-26  23.5347222
## 25 2012-10-27  35.1354167
## 26 2012-10-28  39.7847222
## 27 2012-10-29  17.4236111
## 28 2012-10-30  34.0937500
## 29 2012-10-31  53.5208333
## 30 2012-11-02  36.8055556
## 31 2012-11-03  36.7048611
## 32 2012-11-05  36.2465278
## 33 2012-11-06  28.9375000
## 34 2012-11-07  44.7326389
## 35 2012-11-08  11.1770833
## 36 2012-11-11  43.7777778
## 37 2012-11-12  37.3784722
## 38 2012-11-13  25.4722222
## 39 2012-11-15   0.1423611
## 40 2012-11-16  18.8923611
## 41 2012-11-17  49.7881944
## 42 2012-11-18  52.4652778
## 43 2012-11-19  30.6979167
## 44 2012-11-20  15.5277778
## 45 2012-11-21  44.3993056
## 46 2012-11-22  70.9270833
## 47 2012-11-23  73.5902778
## 48 2012-11-24  50.2708333
## 49 2012-11-25  41.0902778
## 50 2012-11-26  38.7569444
## 51 2012-11-27  47.3819444
## 52 2012-11-28  35.3576389
## 53 2012-11-29  24.4687500
```

Median

```r
summarise(group_by(clean_data, date), median(steps))
```

```
## Source: local data frame [53 x 2]
## 
##          date median(steps)
## 1  2012-10-02             0
## 2  2012-10-03             0
## 3  2012-10-04             0
## 4  2012-10-05             0
## 5  2012-10-06             0
## 6  2012-10-07             0
## 7  2012-10-09             0
## 8  2012-10-10             0
## 9  2012-10-11             0
## 10 2012-10-12             0
## 11 2012-10-13             0
## 12 2012-10-14             0
## 13 2012-10-15             0
## 14 2012-10-16             0
## 15 2012-10-17             0
## 16 2012-10-18             0
## 17 2012-10-19             0
## 18 2012-10-20             0
## 19 2012-10-21             0
## 20 2012-10-22             0
## 21 2012-10-23             0
## 22 2012-10-24             0
## 23 2012-10-25             0
## 24 2012-10-26             0
## 25 2012-10-27             0
## 26 2012-10-28             0
## 27 2012-10-29             0
## 28 2012-10-30             0
## 29 2012-10-31             0
## 30 2012-11-02             0
## 31 2012-11-03             0
## 32 2012-11-05             0
## 33 2012-11-06             0
## 34 2012-11-07             0
## 35 2012-11-08             0
## 36 2012-11-11             0
## 37 2012-11-12             0
## 38 2012-11-13             0
## 39 2012-11-15             0
## 40 2012-11-16             0
## 41 2012-11-17             0
## 42 2012-11-18             0
## 43 2012-11-19             0
## 44 2012-11-20             0
## 45 2012-11-21             0
## 46 2012-11-22             0
## 47 2012-11-23             0
## 48 2012-11-24             0
## 49 2012-11-25             0
## 50 2012-11-26             0
## 51 2012-11-27             0
## 52 2012-11-28             0
## 53 2012-11-29             0
```

##What is the average daily activity pattern?
1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

```r
steps_interval <- summarise(group_by(clean_data, interval), mean(steps))
names(steps_interval) <- c("interval", "steps")
qplot(interval, steps, data = steps_interval, geom="line")
```

![plot of chunk Steps Interval plot](figure/Steps Interval plot-1.png) 

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
filter(steps_interval, steps == max(steps))
```

```
## Source: local data frame [1 x 2]
## 
##   interval    steps
## 1      835 206.1698
```
##Imputing missing values

Note that there are a number of days/intervals where there are missing values (coded as NA). The presence of missing days may introduce bias into some calculations or summaries of the data.

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

```r
nrow(filter(df, is.na(steps)))
```

```
## [1] 2304
```

2. Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

Solution: 
Use the mean for that 5-minute interval, to replace missing values of the same interval.


3. Create a new dataset that is equal to the original dataset but with the missing data filled in.

```r
fill_df <- inner_join(df, steps_interval, by="interval")
fill_df$steps.x[is.na(fill_df$steps.x)] <- fill_df$steps.y[is.na(fill_df$steps.x)]
fill_df <- fill_df[, c(1:3)]
names(fill_df) <- c("steps", "date", "interval")
```

4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

Histogram

```r
fill_steps_total <- summarise(group_by(fill_df, date), sum(steps))
names(fill_steps_total) <- c("date", "steps")
qplot(steps, data = fill_steps_total)
```

```
## stat_bin: binwidth defaulted to range/30. Use 'binwidth = x' to adjust this.
```

![plot of chunk Steps Fill Histogram](figure/Steps Fill Histogram-1.png) 

Mean

```r
summarise(group_by(fill_df, date), mean(steps))
```

```
## Source: local data frame [61 x 2]
## 
##          date mean(steps)
## 1  2012-10-01  37.3825996
## 2  2012-10-02   0.4375000
## 3  2012-10-03  39.4166667
## 4  2012-10-04  42.0694444
## 5  2012-10-05  46.1597222
## 6  2012-10-06  53.5416667
## 7  2012-10-07  38.2465278
## 8  2012-10-08  37.3825996
## 9  2012-10-09  44.4826389
## 10 2012-10-10  34.3750000
## 11 2012-10-11  35.7777778
## 12 2012-10-12  60.3541667
## 13 2012-10-13  43.1458333
## 14 2012-10-14  52.4236111
## 15 2012-10-15  35.2048611
## 16 2012-10-16  52.3750000
## 17 2012-10-17  46.7083333
## 18 2012-10-18  34.9166667
## 19 2012-10-19  41.0729167
## 20 2012-10-20  36.0937500
## 21 2012-10-21  30.6284722
## 22 2012-10-22  46.7361111
## 23 2012-10-23  30.9652778
## 24 2012-10-24  29.0104167
## 25 2012-10-25   8.6527778
## 26 2012-10-26  23.5347222
## 27 2012-10-27  35.1354167
## 28 2012-10-28  39.7847222
## 29 2012-10-29  17.4236111
## 30 2012-10-30  34.0937500
## 31 2012-10-31  53.5208333
## 32 2012-11-01  37.3825996
## 33 2012-11-02  36.8055556
## 34 2012-11-03  36.7048611
## 35 2012-11-04  37.3825996
## 36 2012-11-05  36.2465278
## 37 2012-11-06  28.9375000
## 38 2012-11-07  44.7326389
## 39 2012-11-08  11.1770833
## 40 2012-11-09  37.3825996
## 41 2012-11-10  37.3825996
## 42 2012-11-11  43.7777778
## 43 2012-11-12  37.3784722
## 44 2012-11-13  25.4722222
## 45 2012-11-14  37.3825996
## 46 2012-11-15   0.1423611
## 47 2012-11-16  18.8923611
## 48 2012-11-17  49.7881944
## 49 2012-11-18  52.4652778
## 50 2012-11-19  30.6979167
## 51 2012-11-20  15.5277778
## 52 2012-11-21  44.3993056
## 53 2012-11-22  70.9270833
## 54 2012-11-23  73.5902778
## 55 2012-11-24  50.2708333
## 56 2012-11-25  41.0902778
## 57 2012-11-26  38.7569444
## 58 2012-11-27  47.3819444
## 59 2012-11-28  35.3576389
## 60 2012-11-29  24.4687500
## 61 2012-11-30  37.3825996
```

Median

```r
summarise(group_by(fill_df, date), median(steps))
```

```
## Source: local data frame [61 x 2]
## 
##          date median(steps)
## 1  2012-10-01      34.11321
## 2  2012-10-02       0.00000
## 3  2012-10-03       0.00000
## 4  2012-10-04       0.00000
## 5  2012-10-05       0.00000
## 6  2012-10-06       0.00000
## 7  2012-10-07       0.00000
## 8  2012-10-08      34.11321
## 9  2012-10-09       0.00000
## 10 2012-10-10       0.00000
## 11 2012-10-11       0.00000
## 12 2012-10-12       0.00000
## 13 2012-10-13       0.00000
## 14 2012-10-14       0.00000
## 15 2012-10-15       0.00000
## 16 2012-10-16       0.00000
## 17 2012-10-17       0.00000
## 18 2012-10-18       0.00000
## 19 2012-10-19       0.00000
## 20 2012-10-20       0.00000
## 21 2012-10-21       0.00000
## 22 2012-10-22       0.00000
## 23 2012-10-23       0.00000
## 24 2012-10-24       0.00000
## 25 2012-10-25       0.00000
## 26 2012-10-26       0.00000
## 27 2012-10-27       0.00000
## 28 2012-10-28       0.00000
## 29 2012-10-29       0.00000
## 30 2012-10-30       0.00000
## 31 2012-10-31       0.00000
## 32 2012-11-01      34.11321
## 33 2012-11-02       0.00000
## 34 2012-11-03       0.00000
## 35 2012-11-04      34.11321
## 36 2012-11-05       0.00000
## 37 2012-11-06       0.00000
## 38 2012-11-07       0.00000
## 39 2012-11-08       0.00000
## 40 2012-11-09      34.11321
## 41 2012-11-10      34.11321
## 42 2012-11-11       0.00000
## 43 2012-11-12       0.00000
## 44 2012-11-13       0.00000
## 45 2012-11-14      34.11321
## 46 2012-11-15       0.00000
## 47 2012-11-16       0.00000
## 48 2012-11-17       0.00000
## 49 2012-11-18       0.00000
## 50 2012-11-19       0.00000
## 51 2012-11-20       0.00000
## 52 2012-11-21       0.00000
## 53 2012-11-22       0.00000
## 54 2012-11-23       0.00000
## 55 2012-11-24       0.00000
## 56 2012-11-25       0.00000
## 57 2012-11-26       0.00000
## 58 2012-11-27       0.00000
## 59 2012-11-28       0.00000
## 60 2012-11-29       0.00000
## 61 2012-11-30      34.11321
```

Yes, the values are changed. More date rows are introduced and the values differs as the imputted values are using the interval means. Median count changes from all zeros to some with the replaced interval mean value.

##Are there differences in activity patterns between weekdays and weekends?

*For this part the weekdays() function may be of some help here. Use the dataset with the filled-in missing values for this part.*

*1. Create a new factor variable in the dataset with two levels - "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.*

```r
fill_df$date <- as.Date(fill_df$date, format="%Y-%m-%d")
fill_df$weekday  <- factor(ifelse(weekdays(fill_df$date) %in% c("Saturday", "Sunday"), "weekend", "weekday"))
```

*2. Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.*

```r
fill_df_interval <- summarise(group_by(fill_df, interval, weekday), mean(steps))
names(fill_df_interval) <- c("interval", "weekday", "steps")
qplot(interval, steps, data = fill_df_interval, geom="line", facets=weekday~.)
```

![plot of chunk Weekday Plot](figure/Weekday Plot-1.png) 
