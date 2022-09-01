## R Markdown

    ##TASK 9. Linear Models II
    ##Linear Mixed Models
    ##LOad dataset
    Takyodt<- read.csv("Tayko.csv")

    #Structure of data
    str(Takyodt)

    ## 'data.frame':    2000 obs. of  25 variables:
    ##  $ sequence_number     : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ US                  : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ source_a            : int  0 0 0 0 0 0 0 0 1 1 ...
    ##  $ source_c            : int  0 0 0 1 1 0 0 0 0 0 ...
    ##  $ source_b            : int  1 0 0 0 0 0 0 1 0 0 ...
    ##  $ source_d            : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ source_e            : int  0 1 0 0 0 0 0 0 0 0 ...
    ##  $ source_m            : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ source_o            : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ source_h            : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ source_r            : int  0 0 0 0 0 1 0 0 0 0 ...
    ##  $ source_s            : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ source_t            : int  0 0 1 0 0 0 0 0 0 0 ...
    ##  $ source_u            : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ source_p            : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ source_x            : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ source_w            : int  0 0 0 0 0 0 1 0 0 0 ...
    ##  $ Freq                : int  2 0 2 1 1 1 2 1 4 1 ...
    ##  $ last_update_days_ago: int  3662 2900 3883 829 869 1995 1498 3397 525 3215 ...
    ##  $ X1st_update_days_ago: int  3662 2900 3914 829 869 2002 1529 3397 2914 3215 ...
    ##  $ Web.order           : int  1 1 0 0 0 0 0 0 1 0 ...
    ##  $ Gender.male         : int  0 1 0 1 0 0 0 1 1 0 ...
    ##  $ Address_is_res      : int  1 0 0 0 0 1 1 0 0 0 ...
    ##  $ Purchase            : int  1 0 1 0 0 0 0 0 1 1 ...
    ##  $ Spending            : int  128 0 127 0 0 0 0 0 489 174 ...

\##The response variable \#In this data, my response variable is
“Spending”

\##Run a Linear Mixed Model now.

    ##First, check the independence of observations
    #Using the cor() function, test the relationship between independent variables to ensure they are not highly
    #correlated.
    cor(Takyodt$Freq, Takyodt$last_update_days_ago)

    ## [1] -0.3483025

    cor(Takyodt$Freq,  Takyodt$X1st_update_days_ago)

    ## [1] 0.06298279

    cor(Takyodt$Freq, Takyodt$Web.order)

    ## [1] 0.1033995

    cor(Takyodt$Freq, Takyodt$Gender.male)

    ## [1] -0.03806587

    cor(Takyodt$Freq, Takyodt$Address_is_res)

    ## [1] 0.2158084

    cor(Takyodt$Freq, Takyodt$Purchase)

    ## [1] 0.4696217

\#The correlation between the independent variables is small as
observed, so we can include the parameters in \#in regression model

    ##Check for Linearity
    ##The r/ship between the independent and dependent variables must be linear. We can test this visually
    #by drawing a scatter plot to see if the distribution of data points is linear
    #This can be checked using scatter plots

    plot(Spending ~ Freq, main = "A plot of Spending against Frequency", data = Takyodt)

![](TASK-9--Linear-Models-II_files/figure-markdown_strict/unnamed-chunk-4-1.png)

    plot(Spending ~ last_update_days_ago, main = "A plot of Spending against last_update_days_ago", data = Takyodt)

![](TASK-9--Linear-Models-II_files/figure-markdown_strict/unnamed-chunk-4-2.png)

    plot(Spending ~ X1st_update_days_ago, main = "A plot of Spending against X1st_update_days_ago", data = Takyodt)

![](TASK-9--Linear-Models-II_files/figure-markdown_strict/unnamed-chunk-4-3.png)

    plot(Spending ~ Web.order, main = "A plot of Spending against Web.order", data = Takyodt)

![](TASK-9--Linear-Models-II_files/figure-markdown_strict/unnamed-chunk-4-4.png)

    plot(Spending ~ Gender.male, main = "A plot of Spending against Gender.male", data = Takyodt)

![](TASK-9--Linear-Models-II_files/figure-markdown_strict/unnamed-chunk-4-5.png)

    plot(Spending ~ Address_is_res, main = "A plot of Spending against Address_is_res", data = Takyodt)

![](TASK-9--Linear-Models-II_files/figure-markdown_strict/unnamed-chunk-4-6.png)

    plot(Spending ~ Purchase, main = "A plot of Spending against Purchase", data = Takyodt)

![](TASK-9--Linear-Models-II_files/figure-markdown_strict/unnamed-chunk-4-7.png)

\#Although some relationships are a bit less clear, it still appears
linear \#so we can proceed with linear regression.

    ##Now, let's conduct the Linear Mixed Model analysis
    regmd<- lm(Spending ~ ., data = Takyodt)
    summary(regmd)

    ## 
    ## Call:
    ## lm(formula = Spending ~ ., data = Takyodt)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -402.73  -52.31   -3.29   37.79 1250.03 
    ## 
    ## Coefficients:
    ##                        Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)           11.828960  18.067988   0.655  0.51274    
    ## sequence_number       -0.004569   0.004734  -0.965  0.33461    
    ## US                    -7.344518   7.490169  -0.981  0.32693    
    ## source_a              -3.445123  15.573878  -0.221  0.82495    
    ## source_c             -56.377136  17.730064  -3.180  0.00150 ** 
    ## source_b             -12.409178  17.269775  -0.719  0.47250    
    ## source_d             -43.768176  18.940236  -2.311  0.02094 *  
    ## source_e             -22.332838  14.808736  -1.508  0.13169    
    ## source_m             -38.579076  25.008947  -1.543  0.12309    
    ## source_o              13.704531  19.987779   0.686  0.49302    
    ## source_h             -76.605458  19.281080  -3.973 7.35e-05 ***
    ## source_r              16.124381  16.852634   0.957  0.33879    
    ## source_s             -21.668849  18.172403  -1.192  0.23325    
    ## source_t             -42.385993  22.938062  -1.848  0.06477 .  
    ## source_u              -2.445896  15.482466  -0.158  0.87449    
    ## source_p             -58.247856  37.754528  -1.543  0.12304    
    ## source_x             -15.843130  24.151691  -0.656  0.51191    
    ## source_w             -21.286236  16.165150  -1.317  0.18806    
    ## Freq                  77.328582   3.019280  25.612  < 2e-16 ***
    ## last_update_days_ago  -0.015595   0.005616  -2.777  0.00554 ** 
    ## X1st_update_days_ago   0.005819   0.006149   0.946  0.34412    
    ## Web.order             -3.349784   5.673313  -0.590  0.55496    
    ## Gender.male           -1.586506   5.467136  -0.290  0.77170    
    ## Address_is_res       -63.610797   7.416956  -8.576  < 2e-16 ***
    ## Purchase              92.008164   6.797469  13.536  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 121.4 on 1975 degrees of freedom
    ## Multiple R-squared:  0.5825, Adjusted R-squared:  0.5774 
    ## F-statistic: 114.8 on 24 and 1975 DF,  p-value: < 2.2e-16

\#From the statistics witnessed in the model, it is evident that some
factors have no significant effect \#on the  
\#amount of spending \#A summary of the factors that have a significant
effect on spending are as follows \#The estimated effect of sequence
number on spending is -0.004569 \#The estimated effect of source u on
spending is -2.446 \#The estimated effect of Freq on spending is 77.329,
which is quite high. \#The estimated effect of last\_update\_days\_ago
on spending is -0.0155 \#The estimated effect of X1st\_update\_days\_ago
on spending is 0.0058 \#The estimated effect of Web.order on spending is
-3.35 \#The estimated effect of Gender.male on spending is -1.587 \#The
estimated effect of purchase on spending is 92.01, which is quite high

\#From the statistics above, frequency and purchase are the leading
factors that influence the amount of spending \#For instance, for every
1% of frequency, there is a 77.329% increase in spending, \#For every 1%
of purchase, there is a 92.01% increase in spending, \#The other factors
that least affect spending are; \#For every 1% of sequence number, there
is 2.446% decrease in spending \#For every 1% of
last\_update\_days\_ago, there is 3.35% decrease in spending \#For every
1% of Gender.male, there is 1.587% decrease in spending

    ##Lets now chekc for homoscedacity)
    #This involves checking whether the observed data meets our model assumptions.
    par(mfrow= c(2,2))
    plot(regmd)

![](TASK-9--Linear-Models-II_files/figure-markdown_strict/unnamed-chunk-6-1.png)

    par(mfrow= c(1,1))

\#The residuals show no bias, so the model fits the assumption of
homoscedasticity

    ##Let's now predict the models
    #Predicting the values of speding based on the linear model
    predict01<- predict.lm(regmd, data= Takyodt)

\#Reporting the results \##From the results of the model, there is a
significant relationship between price of vehicles and tax, \#price and
engine size since they have a p value of less than 0.005 (p&lt;0.005).

    ##Use the Random Forest Model
    library(stats)
    library(randomForest)

    ## randomForest 4.7-1.1

    ## Type rfNews() to see new features/changes/bug fixes.

    ##Split the data into testing and training 
    index<- sample(2, nrow(Takyodt), replace = TRUE, prob = c(0.7, 0.3))

    ##Training data
    Training<- Takyodt[index==1, ]

    ##Testing data
    Testing<- Takyodt[index== 2, ]

    ##Random Forest Model
    RMF<- randomForest(Spending ~., data = Training)

    ##Evaluating model accuracy
    Spending_pred<- predict(RMF, Testing)

    ##Confusion Matrix
    CFM<- table(Testing$Spending, Spending_pred)

    ##Let's use the Logistic Regression Model
    GLM<- glm(Purchase~ ., family = "binomial", data = Training)

    ## Warning: glm.fit: algorithm did not converge

    ## Warning: glm.fit: fitted probabilities numerically 0 or 1 occurred

    summary(GLM)

    ## 
    ## Call:
    ## glm(formula = Purchase ~ ., family = "binomial", data = Training)
    ## 
    ## Deviance Residuals: 
    ##        Min          1Q      Median          3Q         Max  
    ## -1.307e-03  -3.550e-06   2.000e-08   2.000e-08   1.926e-03  
    ## 
    ## Coefficients:
    ##                        Estimate Std. Error z value Pr(>|z|)
    ## (Intercept)          -4.289e+02  3.148e+05  -0.001    0.999
    ## sequence_number       6.435e-04  6.128e-01   0.001    0.999
    ## US                   -2.889e-01  7.984e+02   0.000    1.000
    ## source_a              3.966e+02  3.149e+05   0.001    0.999
    ## source_c              4.005e+02  3.147e+05   0.001    0.999
    ## source_b              3.933e+02  3.220e+05   0.001    0.999
    ## source_d              3.985e+02  3.151e+05   0.001    0.999
    ## source_e              3.992e+02  3.147e+05   0.001    0.999
    ## source_m              1.186e+02  3.371e+05   0.000    1.000
    ## source_o              2.167e+01  3.248e+05   0.000    1.000
    ## source_h              4.020e+02  3.147e+05   0.001    0.999
    ## source_r              4.050e+02  3.147e+05   0.001    0.999
    ## source_s              4.013e+02  3.149e+05   0.001    0.999
    ## source_t              3.949e+02  4.304e+05   0.001    0.999
    ## source_u              4.046e+02  3.147e+05   0.001    0.999
    ## source_p              2.214e+01  3.635e+05   0.000    1.000
    ## source_x              4.029e+02  3.149e+05   0.001    0.999
    ## source_w              4.009e+02  3.147e+05   0.001    0.999
    ## Freq                  3.828e+00  9.661e+02   0.004    0.997
    ## last_update_days_ago  4.672e-03  2.430e+00   0.002    0.998
    ## X1st_update_days_ago -4.617e-03  2.528e+00  -0.002    0.999
    ## Web.order             1.644e+00  7.451e+02   0.002    0.998
    ## Gender.male          -1.229e+00  7.894e+02  -0.002    0.999
    ## Address_is_res        1.098e+00  1.514e+03   0.001    0.999
    ## Spending              9.911e+00  1.482e+02   0.067    0.947
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1.9724e+03  on 1422  degrees of freedom
    ## Residual deviance: 1.6352e-05  on 1398  degrees of freedom
    ## AIC: 50
    ## 
    ## Number of Fisher Scoring iterations: 25

## Which model describes better your data? Explain

\#Undoubtedly, Linear Mixed Model describes my data appropriately. This
is because I was able to conduct an analysis and clearly understand the
effects of corresponsing variables on spending
