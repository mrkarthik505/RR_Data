
## Activity Monitoring Devices


### Introduction

It is now possible to collect a large amount of data about personal movement using activity monitoring devices such as a Fitbit, Nike Fuelband, or Jawbone Up. These type of devices are part of the "quantified self" movement - a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. But these data remain under-utilized both because the raw data are hard to obtain and there is a lack of statistical methods and software for processing and interpreting the data.

This assignment makes use of data from a personal activity monitoring device. This device collects data at 5 minute intervals through out the day. The data consists of two months of data from an anonymous individual collected during the months of October and November, 2012 and include the number of steps taken in 5 minute intervals each day.

### Data

The variables included in this dataset are:

    steps: Number of steps taking in a 5-minute interval (missing values are coded as NA)

    date: The date on which the measurement was taken in YYYY-MM-DD format

    interval: Identifier for the 5-minute interval in which measurement was taken

The dataset is stored in a comma-separated-value (CSV) file and there are a total of 17,568 observations in this dataset.

### Loading and Processing the data

First let us load the data into R

```r
data <- read.csv("./activity.csv")
```

### Mean total number of steps taken per day

To find mean total number of steps taken per day ,first let us calculate the total number 
of steps taken per day


```r
s <- tapply(data$steps,data$date,sum,na.rm = TRUE)
print(s)
```

```
## 2012-10-01 2012-10-02 2012-10-03 2012-10-04 2012-10-05 2012-10-06 
##          0        126      11352      12116      13294      15420 
## 2012-10-07 2012-10-08 2012-10-09 2012-10-10 2012-10-11 2012-10-12 
##      11015          0      12811       9900      10304      17382 
## 2012-10-13 2012-10-14 2012-10-15 2012-10-16 2012-10-17 2012-10-18 
##      12426      15098      10139      15084      13452      10056 
## 2012-10-19 2012-10-20 2012-10-21 2012-10-22 2012-10-23 2012-10-24 
##      11829      10395       8821      13460       8918       8355 
## 2012-10-25 2012-10-26 2012-10-27 2012-10-28 2012-10-29 2012-10-30 
##       2492       6778      10119      11458       5018       9819 
## 2012-10-31 2012-11-01 2012-11-02 2012-11-03 2012-11-04 2012-11-05 
##      15414          0      10600      10571          0      10439 
## 2012-11-06 2012-11-07 2012-11-08 2012-11-09 2012-11-10 2012-11-11 
##       8334      12883       3219          0          0      12608 
## 2012-11-12 2012-11-13 2012-11-14 2012-11-15 2012-11-16 2012-11-17 
##      10765       7336          0         41       5441      14339 
## 2012-11-18 2012-11-19 2012-11-20 2012-11-21 2012-11-22 2012-11-23 
##      15110       8841       4472      12787      20427      21194 
## 2012-11-24 2012-11-25 2012-11-26 2012-11-27 2012-11-28 2012-11-29 
##      14478      11834      11162      13646      10183       7047 
## 2012-11-30 
##          0
```

Now have the total number of steps taken per day.

Now we are making a histogram for total number of steps taken each day


```r
hist(s,xlab = "Number of steps taken each day",main = "Histogram for total number of steps taken each day")
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3-1.png) 

Mean of total number of steps taken per day 


```r
mean(s)
```

```
## [1] 9354.23
```

Median of total number of steps takend per day


```r
median(s)
```

```
## [1] 10395
```

## Average Daily activity pattern

Now we need to make a time series plot of the 5-minute interval which is on x- axis and the average number of steps taken, averaged across all days on y -axis


```r
s2 <- tapply(data$steps,data$interval,mean,na.rm = TRUE)
plot(unique(data$interval),s2,type = "l",xlab = "5 - minute interval",ylab = "average number of steps taken,averaged across all days", main = "Average daily pattern")
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-1.png) 

We need to find which 5 - minute interval, on average across all the days in the dataset, contains the maximum number of steps

The details of the interval which contains maximum number of steps

```r
a <- sort(s2,decreasing = TRUE)
a[1]
```

```
##      835 
## 206.1698
```

##Imputing missing values

First we calculate the total number of missing values in the dataset


```r
length(which(is.na(data[1])==T))
```

```
## [1] 2304
```

Now we are replacing all the missing values with the mean of steps taken for the interval and also created a dataset which is equal to the original dataset but with the missing data filled in



```r
data1 <- data
for(var in s2){
     data1[is.na(data1)] <- var
    }
```

I am creating a histogram of the total number of steps taken each day 


```r
p <- tapply(data1$steps,data1$date,sum)
hist(p,xlab = "Number of steps taken each day",main = "Histogram for total number of steps taken each day(after missing data filled in)")
```

![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10-1.png) 

Mean of total number of steps taken per day (after filling the missing values)


```r
mean(p)
```

```
## [1] 9419.081
```

Median of total number of steps takend per day(after filling the missing values)


```r
median(p)
```

```
## [1] 10395
```

As we can see we have slight difference in mean but where as the median is same. The mean has changed after imputing missing data with the mean of total number of steps for the interval




