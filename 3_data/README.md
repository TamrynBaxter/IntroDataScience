    ##Load required packages
    library(tidyverse)

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.6     v purrr   0.3.4
    ## v tibble  3.1.6     v dplyr   1.0.9
    ## v tidyr   1.2.0     v stringr 1.4.0
    ## v readr   2.1.2     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

    library(dplyr)

    ##TASK 3

    #Dataset 1
    #Our first data comes from R (It is inbuilt)
    ##Load any pre-loaded data in R
    data(msleep)

    ##Let's do some analysis on the msleep dataset
    ##Check the number of observations
    dim(msleep)

    ## [1] 83 11

    ##Check the structure of the data, that is, check the datatypes
    str(msleep)

    ## tibble [83 x 11] (S3: tbl_df/tbl/data.frame)
    ##  $ name        : chr [1:83] "Cheetah" "Owl monkey" "Mountain beaver" "Greater short-tailed shrew" ...
    ##  $ genus       : chr [1:83] "Acinonyx" "Aotus" "Aplodontia" "Blarina" ...
    ##  $ vore        : chr [1:83] "carni" "omni" "herbi" "omni" ...
    ##  $ order       : chr [1:83] "Carnivora" "Primates" "Rodentia" "Soricomorpha" ...
    ##  $ conservation: chr [1:83] "lc" NA "nt" "lc" ...
    ##  $ sleep_total : num [1:83] 12.1 17 14.4 14.9 4 14.4 8.7 7 10.1 3 ...
    ##  $ sleep_rem   : num [1:83] NA 1.8 2.4 2.3 0.7 2.2 1.4 NA 2.9 NA ...
    ##  $ sleep_cycle : num [1:83] NA NA NA 0.133 0.667 ...
    ##  $ awake       : num [1:83] 11.9 7 9.6 9.1 20 9.6 15.3 17 13.9 21 ...
    ##  $ brainwt     : num [1:83] NA 0.0155 NA 0.00029 0.423 NA NA NA 0.07 0.0982 ...
    ##  $ bodywt      : num [1:83] 50 0.48 1.35 0.019 600 ...

\##As evident, we can see the datatypes of the variables, for instance,
the name, genus, and vore are all categorical variables while the rest
are numerical variables. Sleep\_total, awake, brainnt, and bodywt are
quantitative while sleep\_cycle is qualitative in nature.

    ##Do some descriptive statistics of the data (this is its description in terms of statistical variables)
    summary(msleep)

    ##      name              genus               vore              order          
    ##  Length:83          Length:83          Length:83          Length:83         
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##  conservation        sleep_total      sleep_rem      sleep_cycle    
    ##  Length:83          Min.   : 1.90   Min.   :0.100   Min.   :0.1167  
    ##  Class :character   1st Qu.: 7.85   1st Qu.:0.900   1st Qu.:0.1833  
    ##  Mode  :character   Median :10.10   Median :1.500   Median :0.3333  
    ##                     Mean   :10.43   Mean   :1.875   Mean   :0.4396  
    ##                     3rd Qu.:13.75   3rd Qu.:2.400   3rd Qu.:0.5792  
    ##                     Max.   :19.90   Max.   :6.600   Max.   :1.5000  
    ##                                     NA's   :22      NA's   :51      
    ##      awake          brainwt            bodywt        
    ##  Min.   : 4.10   Min.   :0.00014   Min.   :   0.005  
    ##  1st Qu.:10.25   1st Qu.:0.00290   1st Qu.:   0.174  
    ##  Median :13.90   Median :0.01240   Median :   1.670  
    ##  Mean   :13.57   Mean   :0.28158   Mean   : 166.136  
    ##  3rd Qu.:16.15   3rd Qu.:0.12550   3rd Qu.:  41.750  
    ##  Max.   :22.10   Max.   :5.71200   Max.   :6654.000  
    ##                  NA's   :27

    ##The summary statistics shows the mean, max, min, 1st and 3rd quartiles of the data.

    ##Dataset 2

    #The second dataset we will be exploring is made available on <https://www.kaggle.com/>
    ##Import the first dataset
    Loan_default_Data<- read.csv("Loan_Default.csv")

    ##Check the number of observations
    dim(Loan_default_Data)

    ## [1] 148670     34

    ##Check the structure of the data (Check datatypes)
    str(Loan_default_Data)

    ## 'data.frame':    148670 obs. of  34 variables:
    ##  $ ID                       : int  24890 24891 24892 24893 24894 24895 24896 24897 24898 24899 ...
    ##  $ year                     : int  2019 2019 2019 2019 2019 2019 2019 2019 2019 2019 ...
    ##  $ loan_limit               : chr  "cf" "cf" "cf" "cf" ...
    ##  $ Gender                   : chr  "Sex Not Available" "Male" "Male" "Male" ...
    ##  $ approv_in_adv            : chr  "nopre" "nopre" "pre" "nopre" ...
    ##  $ loan_type                : chr  "type1" "type2" "type1" "type1" ...
    ##  $ loan_purpose             : chr  "p1" "p1" "p1" "p4" ...
    ##  $ Credit_Worthiness        : chr  "l1" "l1" "l1" "l1" ...
    ##  $ open_credit              : chr  "nopc" "nopc" "nopc" "nopc" ...
    ##  $ business_or_commercial   : chr  "nob/c" "b/c" "nob/c" "nob/c" ...
    ##  $ loan_amount              : int  116500 206500 406500 456500 696500 706500 346500 266500 376500 436500 ...
    ##  $ rate_of_interest         : num  NA NA 4.56 4.25 4 ...
    ##  $ Interest_rate_spread     : num  NA NA 0.2 0.681 0.304 ...
    ##  $ Upfront_charges          : num  NA NA 595 NA 0 ...
    ##  $ term                     : num  360 360 360 360 360 360 360 360 360 360 ...
    ##  $ Neg_ammortization        : chr  "not_neg" "not_neg" "neg_amm" "not_neg" ...
    ##  $ interest_only            : chr  "not_int" "not_int" "not_int" "not_int" ...
    ##  $ lump_sum_payment         : chr  "not_lpsm" "lpsm" "not_lpsm" "not_lpsm" ...
    ##  $ property_value           : num  118000 NA 508000 658000 758000 ...
    ##  $ construction_type        : chr  "sb" "sb" "sb" "sb" ...
    ##  $ occupancy_type           : chr  "pr" "pr" "pr" "pr" ...
    ##  $ Secured_by               : chr  "home" "home" "home" "home" ...
    ##  $ total_units              : chr  "1U" "1U" "1U" "1U" ...
    ##  $ income                   : num  1740 4980 9480 11880 10440 ...
    ##  $ credit_type              : chr  "EXP" "EQUI" "EXP" "EXP" ...
    ##  $ Credit_Score             : int  758 552 834 587 602 864 860 863 580 788 ...
    ##  $ co.applicant_credit_type : chr  "CIB" "EXP" "CIB" "CIB" ...
    ##  $ age                      : chr  "25-34" "55-64" "35-44" "45-54" ...
    ##  $ submission_of_application: chr  "to_inst" "to_inst" "to_inst" "not_inst" ...
    ##  $ LTV                      : num  98.7 NA 80 69.4 91.9 ...
    ##  $ Region                   : chr  "south" "North" "south" "North" ...
    ##  $ Security_Type            : chr  "direct" "direct" "direct" "direct" ...
    ##  $ Status                   : int  1 1 0 0 0 0 0 0 0 0 ...
    ##  $ dtir1                    : num  45 NA 46 42 39 40 44 42 44 30 ...

    ##Do descriptive statistics of the data
    summary(Loan_default_Data)

    ##        ID              year       loan_limit           Gender         
    ##  Min.   : 24890   Min.   :2019   Length:148670      Length:148670     
    ##  1st Qu.: 62057   1st Qu.:2019   Class :character   Class :character  
    ##  Median : 99225   Median :2019   Mode  :character   Mode  :character  
    ##  Mean   : 99225   Mean   :2019                                        
    ##  3rd Qu.:136392   3rd Qu.:2019                                        
    ##  Max.   :173559   Max.   :2019                                        
    ##                                                                       
    ##  approv_in_adv       loan_type         loan_purpose       Credit_Worthiness 
    ##  Length:148670      Length:148670      Length:148670      Length:148670     
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##  open_credit        business_or_commercial  loan_amount      rate_of_interest
    ##  Length:148670      Length:148670          Min.   :  16500   Min.   :0.00    
    ##  Class :character   Class :character       1st Qu.: 196500   1st Qu.:3.62    
    ##  Mode  :character   Mode  :character       Median : 296500   Median :3.99    
    ##                                            Mean   : 331118   Mean   :4.05    
    ##                                            3rd Qu.: 436500   3rd Qu.:4.38    
    ##                                            Max.   :3576500   Max.   :8.00    
    ##                                                              NA's   :36439   
    ##  Interest_rate_spread Upfront_charges        term       Neg_ammortization 
    ##  Min.   :-3.64        Min.   :    0.0   Min.   : 96.0   Length:148670     
    ##  1st Qu.: 0.08        1st Qu.:  581.5   1st Qu.:360.0   Class :character  
    ##  Median : 0.39        Median : 2596.4   Median :360.0   Mode  :character  
    ##  Mean   : 0.44        Mean   : 3225.0   Mean   :335.1                     
    ##  3rd Qu.: 0.78        3rd Qu.: 4812.5   3rd Qu.:360.0                     
    ##  Max.   : 3.36        Max.   :60000.0   Max.   :360.0                     
    ##  NA's   :36639        NA's   :39642     NA's   :41                        
    ##  interest_only      lump_sum_payment   property_value     construction_type 
    ##  Length:148670      Length:148670      Min.   :    8000   Length:148670     
    ##  Class :character   Class :character   1st Qu.:  268000   Class :character  
    ##  Mode  :character   Mode  :character   Median :  418000   Mode  :character  
    ##                                        Mean   :  497893                     
    ##                                        3rd Qu.:  628000                     
    ##                                        Max.   :16508000                     
    ##                                        NA's   :15098                        
    ##  occupancy_type      Secured_by        total_units            income      
    ##  Length:148670      Length:148670      Length:148670      Min.   :     0  
    ##  Class :character   Class :character   Class :character   1st Qu.:  3720  
    ##  Mode  :character   Mode  :character   Mode  :character   Median :  5760  
    ##                                                           Mean   :  6957  
    ##                                                           3rd Qu.:  8520  
    ##                                                           Max.   :578580  
    ##                                                           NA's   :9150    
    ##  credit_type         Credit_Score   co.applicant_credit_type     age           
    ##  Length:148670      Min.   :500.0   Length:148670            Length:148670     
    ##  Class :character   1st Qu.:599.0   Class :character         Class :character  
    ##  Mode  :character   Median :699.0   Mode  :character         Mode  :character  
    ##                     Mean   :699.8                                              
    ##                     3rd Qu.:800.0                                              
    ##                     Max.   :900.0                                              
    ##                                                                                
    ##  submission_of_application      LTV              Region         
    ##  Length:148670             Min.   :   0.967   Length:148670     
    ##  Class :character          1st Qu.:  60.475   Class :character  
    ##  Mode  :character          Median :  75.136   Mode  :character  
    ##                            Mean   :  72.746                     
    ##                            3rd Qu.:  86.184                     
    ##                            Max.   :7831.250                     
    ##                            NA's   :15098                        
    ##  Security_Type          Status           dtir1      
    ##  Length:148670      Min.   :0.0000   Min.   : 5.00  
    ##  Class :character   1st Qu.:0.0000   1st Qu.:31.00  
    ##  Mode  :character   Median :0.0000   Median :39.00  
    ##                     Mean   :0.2464   Mean   :37.73  
    ##                     3rd Qu.:0.0000   3rd Qu.:45.00  
    ##                     Max.   :1.0000   Max.   :61.00  
    ##                                      NA's   :24121

    ##Dataset 3
    #The third dataset we will be exploring is also made available on <https://www.kaggle.com/>
    ##Import the dataset
    SalaryInfor<- read.csv("salary.csv")

    ##Check the number of observations
    dim(SalaryInfor)

    ## [1] 32561    15

    ##Check the dataset datatypes
    str(SalaryInfor)

    ## 'data.frame':    32561 obs. of  15 variables:
    ##  $ age           : int  39 50 38 53 28 37 49 52 31 42 ...
    ##  $ workclass     : chr  " State-gov" " Self-emp-not-inc" " Private" " Private" ...
    ##  $ fnlwgt        : int  77516 83311 215646 234721 338409 284582 160187 209642 45781 159449 ...
    ##  $ education     : chr  " Bachelors" " Bachelors" " HS-grad" " 11th" ...
    ##  $ education.num : int  13 13 9 7 13 14 5 9 14 13 ...
    ##  $ marital.status: chr  " Never-married" " Married-civ-spouse" " Divorced" " Married-civ-spouse" ...
    ##  $ occupation    : chr  " Adm-clerical" " Exec-managerial" " Handlers-cleaners" " Handlers-cleaners" ...
    ##  $ relationship  : chr  " Not-in-family" " Husband" " Not-in-family" " Husband" ...
    ##  $ race          : chr  " White" " White" " White" " Black" ...
    ##  $ sex           : chr  " Male" " Male" " Male" " Male" ...
    ##  $ capital.gain  : int  2174 0 0 0 0 0 0 0 14084 5178 ...
    ##  $ capital.loss  : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ hours.per.week: int  40 13 40 40 40 40 16 45 50 40 ...
    ##  $ native.country: chr  " United-States" " United-States" " United-States" " United-States" ...
    ##  $ salary        : chr  " <=50K" " <=50K" " <=50K" " <=50K" ...

    ##Descriptive statistics of the data
    summary(SalaryInfor)

    ##       age         workclass             fnlwgt         education        
    ##  Min.   :17.00   Length:32561       Min.   :  12285   Length:32561      
    ##  1st Qu.:28.00   Class :character   1st Qu.: 117827   Class :character  
    ##  Median :37.00   Mode  :character   Median : 178356   Mode  :character  
    ##  Mean   :38.58                      Mean   : 189778                     
    ##  3rd Qu.:48.00                      3rd Qu.: 237051                     
    ##  Max.   :90.00                      Max.   :1484705                     
    ##  education.num   marital.status      occupation        relationship      
    ##  Min.   : 1.00   Length:32561       Length:32561       Length:32561      
    ##  1st Qu.: 9.00   Class :character   Class :character   Class :character  
    ##  Median :10.00   Mode  :character   Mode  :character   Mode  :character  
    ##  Mean   :10.08                                                           
    ##  3rd Qu.:12.00                                                           
    ##  Max.   :16.00                                                           
    ##      race               sex             capital.gain    capital.loss   
    ##  Length:32561       Length:32561       Min.   :    0   Min.   :   0.0  
    ##  Class :character   Class :character   1st Qu.:    0   1st Qu.:   0.0  
    ##  Mode  :character   Mode  :character   Median :    0   Median :   0.0  
    ##                                        Mean   : 1078   Mean   :  87.3  
    ##                                        3rd Qu.:    0   3rd Qu.:   0.0  
    ##                                        Max.   :99999   Max.   :4356.0  
    ##  hours.per.week  native.country        salary         
    ##  Min.   : 1.00   Length:32561       Length:32561      
    ##  1st Qu.:40.00   Class :character   Class :character  
    ##  Median :40.00   Mode  :character   Mode  :character  
    ##  Mean   :40.44                                        
    ##  3rd Qu.:45.00                                        
    ##  Max.   :99.00
