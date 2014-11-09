---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---
Reproducible Research: Assignment 1
====================================

Steven L. Senior


## Installing required packages
I like to use dplyr for manipulating data frames and lubridate for dealing with dates.


```r
# install.packages(c("dplyr", "lubridate"))
library(dplyr)
library(lubridate)
```

## Loading and preprocessing the data
For completeness, I have also included the code to download the zip file from the course website and unzip it.


*If data not already downloaded, download and unzip it:*

```r
if(!file.exists("activity.csv")){
	file_url <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
	download.file(file_url, "activity.zip", method = "curl")
	unzip("activity.zip")
}
```

*Read in and preview data:*

```r
activity <- read.csv("activity.csv", stringsAsFactors = F, header = T)
head(activity, n = 5)
```

```
##   steps       date interval
## 1    NA 2012-10-01        0
## 2    NA 2012-10-01        5
## 3    NA 2012-10-01       10
## 4    NA 2012-10-01       15
## 5    NA 2012-10-01       20
```

*Preprocess data - convert to data.tbl so I can use dplyr, and convert the date to a date variable:*

```r
activity  <- as.tbl(activity) 
activity <- mutate(activity, date = ymd(date))
```

## What is mean total number of steps taken per day?

*Calculate the number of steps on each day, then calculate mean for all days

```r
steps <- activity %>% group_by(date) %>% summarize(steps = sum(steps, na.rm = TRUE))
mean_steps  <- mean(steps$steps)
median_steps <- median(steps$steps)
hist(steps$steps, breaks  = 15)
```

![plot of chunk Calculate mean steps per day](figure/Calculate mean steps per day.png) 

The mean number of steps taken each day is 9354.2295 and the median number of steps taken is 10395. I found it interesting that the default number of breaks for the histogram (5) hid quite a lot of variation in the data. Using breaks = 15 reveals this better. What it shows is that many days had zero steps.

## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?


