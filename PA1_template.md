# PA1_template
dddbbb  
The date  
##What is mean total number of steps taken per day?

* Calculate the total number of steps taken per day

* Make a histogram of the total number of steps taken each day


```r
data = read.csv('activity.csv')
hist(tapply(data$steps, factor(data$date), sum), xlab="Daily steps", main="Histogram daily steps", breaks = 10)
```

![](PA1_template_files/figure-html/unnamed-chunk-1-1.png) 

* Calculate and report the mean and median of the total number of steps taken per day

```r
mean(tapply(data$steps, factor(data$date), sum), na.rm=T)
```

```
## [1] 10766.19
```

```r
median(tapply(data$steps, factor(data$date), sum), na.rm=T)
```

```
## [1] 10765
```

##What is the average daily activity pattern?

* Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

```r
mean_interval_daily <- tapply(data$steps, factor(data$interval), mean, na.rm=T)
plot(mean_interval_daily, type="l", xlab="5-minutes Interval", ylab="Mean of steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 


* Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
mean_interval_daily[which.max(mean_interval_daily)]
```

```
##      835 
## 206.1698
```
##Imputing missing values

* Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

```r
sum(is.na(data))
```

```
## [1] 2304
```
* Strategy for filling in all of the missing values in the dataset is set the mean for that 5-minute interval.

* Create a new dataset that is equal to the original dataset but with the missing data filled in.

* Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?


```r
data2 <- merge(data, as.data.frame(mean_interval_daily), by.x = "interval", by.y = "row.names")
data2$steps[is.na(data2$steps)] = data2$mean_interval_daily[is.na(data2$steps)]

data2$mean_interval_daily = NULL
hist(tapply(data2$steps, factor(data2$date), sum), xlab="Daily steps", main="Histogram daily steps", breaks = 10)
```

![](PA1_template_files/figure-html/unnamed-chunk-6-1.png) 

```r
mean(tapply(data2$steps, factor(data2$date), sum), na.rm=T)
```

```
## [1] 10766.19
```

```r
median(tapply(data2$steps, factor(data2$date), sum), na.rm=T)
```

```
## [1] 10766.19
```


