``` r
steps <- aggregate(activity$steps, by = list(Category = activity$date), FUN=sum)
hist(steps$x,main = "Histogram of total number of steps taken each day",xlab = "Range of Steps")
```

![](PA1_template_files/figure-markdown_github/unnamed-chunk-1-1.png)

``` r
mean(activity$steps, na.rm = TRUE)
```

    ## [1] 37.3826

``` r
median(activity$steps, na.rm = TRUE)
```

    ## [1] 0

The histogram have some missing values. After range from 550 to 700 all values are zero. Also the meadian and the mean values are NA values because they have missing values.

``` r
df = na.omit(activity)
freq = group_by(df, date) %>% summarise(mean = mean(steps))
plot(freq[,1:2],type = 'l')
```

![](PA1_template_files/figure-markdown_github/unnamed-chunk-2-1.png)

``` r
summary(freq)
```

    ##       date                 mean        
    ##  Min.   :2012-10-02   Min.   : 0.1424  
    ##  1st Qu.:2012-10-16   1st Qu.:30.6979  
    ##  Median :2012-10-29   Median :37.3785  
    ##  Mean   :2012-10-30   Mean   :37.3826  
    ##  3rd Qu.:2012-11-16   3rd Qu.:46.1597  
    ##  Max.   :2012-11-29   Max.   :73.5903

The max values was in 2012-11-23 with 73.6 steps average.

``` r
summary(activity$steps)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##    0.00    0.00    0.00   37.38   12.00  806.00    2304

``` r
ave =cbind(activity$steps,activity$interval)
ave = rowMeans(ave, na.rm=TRUE)
df = na.omit(activity)
freq = group_by(df, date) %>% summarise(mean = mean(steps))
new_df = activity
for(i in seq(length(new_df$steps))){
  if(is.na(new_df$steps[i])){
    new_df$steps[i] = ave[i]
  }
}

hist(new_df$steps, main = "Histogram of total number of steps taken each day",xlab = "Range of Steps")
```

![](PA1_template_files/figure-markdown_github/unnamed-chunk-3-1.png)

``` r
mean(new_df$steps)
```

    ## [1] 186.9062

``` r
median(new_df$steps)
```

    ## [1] 0

In the activity dataframe exist 2304 missing values. To replace all values I used the cross mean interval values. The histogram now do not have the missing values, now is more constant. The results are very different that the first part of the assingment. Remove all missing values change the output.
