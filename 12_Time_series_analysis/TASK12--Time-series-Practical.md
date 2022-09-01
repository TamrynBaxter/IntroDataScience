## R Markdown

    ##TASK 12 . Time-Series Practical
    ##Load the AirPassengers dataset that is inbuilt in R
    data("AirPassengers")

    ##Assign it to an object
    Air.ts<- AirPassengers

    ##Explore the dataset
    ##Check the class for the data
    class(Air.ts)

    ## [1] "ts"

    ##Structure
    str(Air.ts)

    ##  Time-Series [1:144] from 1949 to 1961: 112 118 132 129 121 135 148 148 136 119 ...

    ##First few rows
    start(Air.ts)

    ## [1] 1949    1

    ##Last few rows
    end(Air.ts)

    ## [1] 1960   12

    ##Frequency
    frequency(Air.ts)

    ## [1] 12

    ##Check the summary of the data
    summary(Air.ts)

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   104.0   180.0   265.5   280.3   360.5   622.0

    ##Now, plot the time series
    library(tseries)

    ## Registered S3 method overwritten by 'quantmod':
    ##   method            from
    ##   as.zoo.data.frame zoo

    plot(Air.ts, ylab= "Air Passengers (\'000s)", lwd= 2)

![](TASK12--Time-series-Practical_files/figure-markdown_strict/unnamed-chunk-9-1.png)

    ##Create the AutoCorrelation plot
    acf(Air.ts)

![](TASK12--Time-series-Practical_files/figure-markdown_strict/unnamed-chunk-10-1.png)

    ##Autoregressive model
    adf.test(Air.ts, k= 12)

    ## 
    ##  Augmented Dickey-Fuller Test
    ## 
    ## data:  Air.ts
    ## Dickey-Fuller = -1.5094, Lag order = 12, p-value = 0.7807
    ## alternative hypothesis: stationary

    ##Conduct the PACF
    pacf(Air.ts)

![](TASK12--Time-series-Practical_files/figure-markdown_strict/unnamed-chunk-12-1.png)
\##Evaluation \#The best model to use in this task is the autoregressive
model since it allows us to also see the p-value and the statistical
results.
