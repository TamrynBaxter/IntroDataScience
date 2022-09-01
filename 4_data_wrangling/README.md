    library(tidyverse)

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.6     v purrr   0.3.4
    ## v tibble  3.1.6     v dplyr   1.0.9
    ## v tidyr   1.2.0     v stringr 1.4.0
    ## v readr   2.1.2     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

    ##TASK 4: Wrangling 
    ##Let's use a dataset that is inbuilt from R
    data("starwars")

    ##Filter the data by two variables
    Newdata<- starwars %>%  
      filter(species== "Human" | species== "Droid")

    ##Select a subset of the columns
    Col_subset<- Newdata %>% 
      select(mass, eye_color, birth_year, gender)

    ##Display the first few rows of the dataframe(first 8 rows)
    head(Newdata, 8)

    ## # A tibble: 8 x 14
    ##   name         height  mass hair_~1 skin_~2 eye_c~3 birth~4 sex   gender homew~5
    ##   <chr>         <int> <dbl> <chr>   <chr>   <chr>     <dbl> <chr> <chr>  <chr>  
    ## 1 Luke Skywal~    172    77 blond   fair    blue       19   male  mascu~ Tatooi~
    ## 2 C-3PO           167    75 <NA>    gold    yellow    112   none  mascu~ Tatooi~
    ## 3 R2-D2            96    32 <NA>    white,~ red        33   none  mascu~ Naboo  
    ## 4 Darth Vader     202   136 none    white   yellow     41.9 male  mascu~ Tatooi~
    ## 5 Leia Organa     150    49 brown   light   brown      19   fema~ femin~ Aldera~
    ## 6 Owen Lars       178   120 brown,~ light   blue       52   male  mascu~ Tatooi~
    ## 7 Beru Whites~    165    75 brown   light   blue       47   fema~ femin~ Tatooi~
    ## 8 R5-D4            97    32 <NA>    white,~ red        NA   none  mascu~ Tatooi~
    ## # ... with 4 more variables: species <chr>, films <list>, vehicles <list>,
    ## #   starships <list>, and abbreviated variable names 1: hair_color,
    ## #   2: skin_color, 3: eye_color, 4: birth_year, 5: homeworld
    ## # i Use `colnames()` to see all variable names

    ##Display the last few rows of the data(last 8 rows)
    tail(Newdata, 8)

    ## # A tibble: 8 x 14
    ##   name         height  mass hair_~1 skin_~2 eye_c~3 birth~4 sex   gender homew~5
    ##   <chr>         <int> <dbl> <chr>   <chr>   <chr>     <dbl> <chr> <chr>  <chr>  
    ## 1 Jocasta Nu      167    NA white   fair    blue         NA fema~ femin~ Corusc~
    ## 2 R4-P17           96    NA none    silver~ red, b~      NA none  femin~ <NA>   
    ## 3 Raymus Anti~    188    79 brown   light   brown        NA male  mascu~ Aldera~
    ## 4 Finn             NA    NA black   dark    dark         NA male  mascu~ <NA>   
    ## 5 Rey              NA    NA brown   light   hazel        NA fema~ femin~ <NA>   
    ## 6 Poe Dameron      NA    NA brown   light   brown        NA male  mascu~ <NA>   
    ## 7 BB8              NA    NA none    none    black        NA none  mascu~ <NA>   
    ## 8 Padmé Amida~    165    45 brown   light   brown        46 fema~ femin~ Naboo  
    ## # ... with 4 more variables: species <chr>, films <list>, vehicles <list>,
    ## #   starships <list>, and abbreviated variable names 1: hair_color,
    ## #   2: skin_color, 3: eye_color, 4: birth_year, 5: homeworld
    ## # i Use `colnames()` to see all variable names

    ##Display the structure of the dataframe
    str(Newdata)

    ## tibble [41 x 14] (S3: tbl_df/tbl/data.frame)
    ##  $ name      : chr [1:41] "Luke Skywalker" "C-3PO" "R2-D2" "Darth Vader" ...
    ##  $ height    : int [1:41] 172 167 96 202 150 178 165 97 183 182 ...
    ##  $ mass      : num [1:41] 77 75 32 136 49 120 75 32 84 77 ...
    ##  $ hair_color: chr [1:41] "blond" NA NA "none" ...
    ##  $ skin_color: chr [1:41] "fair" "gold" "white, blue" "white" ...
    ##  $ eye_color : chr [1:41] "blue" "yellow" "red" "yellow" ...
    ##  $ birth_year: num [1:41] 19 112 33 41.9 19 52 47 NA 24 57 ...
    ##  $ sex       : chr [1:41] "male" "none" "none" "male" ...
    ##  $ gender    : chr [1:41] "masculine" "masculine" "masculine" "masculine" ...
    ##  $ homeworld : chr [1:41] "Tatooine" "Tatooine" "Naboo" "Tatooine" ...
    ##  $ species   : chr [1:41] "Human" "Droid" "Droid" "Human" ...
    ##  $ films     :List of 41
    ##   ..$ : chr [1:5] "The Empire Strikes Back" "Revenge of the Sith" "Return of the Jedi" "A New Hope" ...
    ##   ..$ : chr [1:6] "The Empire Strikes Back" "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith" ...
    ##   ..$ : chr [1:7] "The Empire Strikes Back" "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith" ...
    ##   ..$ : chr [1:4] "The Empire Strikes Back" "Revenge of the Sith" "Return of the Jedi" "A New Hope"
    ##   ..$ : chr [1:5] "The Empire Strikes Back" "Revenge of the Sith" "Return of the Jedi" "A New Hope" ...
    ##   ..$ : chr [1:3] "Attack of the Clones" "Revenge of the Sith" "A New Hope"
    ##   ..$ : chr [1:3] "Attack of the Clones" "Revenge of the Sith" "A New Hope"
    ##   ..$ : chr "A New Hope"
    ##   ..$ : chr "A New Hope"
    ##   ..$ : chr [1:6] "The Empire Strikes Back" "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith" ...
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr [1:2] "Revenge of the Sith" "A New Hope"
    ##   ..$ : chr [1:4] "The Empire Strikes Back" "Return of the Jedi" "A New Hope" "The Force Awakens"
    ##   ..$ : chr [1:3] "The Empire Strikes Back" "Return of the Jedi" "A New Hope"
    ##   ..$ : chr "A New Hope"
    ##   ..$ : chr [1:5] "The Empire Strikes Back" "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith" ...
    ##   ..$ : chr [1:3] "The Empire Strikes Back" "Attack of the Clones" "Return of the Jedi"
    ##   ..$ : chr "The Empire Strikes Back"
    ##   ..$ : chr [1:2] "The Empire Strikes Back" "Return of the Jedi"
    ##   ..$ : chr "The Empire Strikes Back"
    ##   ..$ : chr "Return of the Jedi"
    ##   ..$ : chr "Return of the Jedi"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr [1:2] "Attack of the Clones" "The Phantom Menace"
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr [1:2] "Attack of the Clones" "Revenge of the Sith"
    ##   ..$ : chr [1:2] "Attack of the Clones" "Revenge of the Sith"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr [1:2] "Attack of the Clones" "Revenge of the Sith"
    ##   ..$ : chr [1:2] "Revenge of the Sith" "A New Hope"
    ##   ..$ : chr "The Force Awakens"
    ##   ..$ : chr "The Force Awakens"
    ##   ..$ : chr "The Force Awakens"
    ##   ..$ : chr "The Force Awakens"
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##  $ vehicles  :List of 41
    ##   ..$ : chr [1:2] "Snowspeeder" "Imperial Speeder Bike"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Imperial Speeder Bike"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Tribubble bongo"
    ##   ..$ : chr [1:2] "Zephyr-G swoop bike" "XJ-6 airspeeder"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Snowspeeder"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Tribubble bongo"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Flitknot speeder"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##  $ starships :List of 41
    ##   ..$ : chr [1:2] "X-wing" "Imperial shuttle"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "TIE Advanced x1"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "X-wing"
    ##   ..$ : chr [1:5] "Jedi starfighter" "Trade Federation cruiser" "Naboo star skiff" "Jedi Interceptor" ...
    ##   ..$ : chr [1:3] "Trade Federation cruiser" "Jedi Interceptor" "Naboo fighter"
    ##   ..$ : chr(0) 
    ##   ..$ : chr [1:2] "Millennium Falcon" "Imperial shuttle"
    ##   ..$ : chr "X-wing"
    ##   ..$ : chr "X-wing"
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Slave 1"
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Millennium Falcon"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "A-wing"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Naboo fighter"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "T-70 X-wing fighter"
    ##   ..$ : chr(0) 
    ##   ..$ : chr [1:3] "H-type Nubian yacht" "Naboo star skiff" "Naboo fighter"

    ##Display data arranged by columns by having height column in ascending order
    ArrangeData<- Newdata[order(Newdata$height),]
    ##Now, let's just display the first 10 rows of the data
    head(ArrangeData, 10)

    ## # A tibble: 10 x 14
    ##    name        height  mass hair_~1 skin_~2 eye_c~3 birth~4 sex   gender homew~5
    ##    <chr>        <int> <dbl> <chr>   <chr>   <chr>     <dbl> <chr> <chr>  <chr>  
    ##  1 R2-D2           96    32 <NA>    white,~ red          33 none  mascu~ Naboo  
    ##  2 R4-P17          96    NA none    silver~ red, b~      NA none  femin~ <NA>   
    ##  3 R5-D4           97    32 <NA>    white,~ red          NA none  mascu~ Tatooi~
    ##  4 Leia Organa    150    49 brown   light   brown        19 fema~ femin~ Aldera~
    ##  5 Mon Mothma     150    NA auburn  fair    blue         48 fema~ femin~ Chandr~
    ##  6 Cordé          157    NA brown   light   brown        NA fema~ femin~ Naboo  
    ##  7 Shmi Skywa~    163    NA black   fair    brown        72 fema~ femin~ Tatooi~
    ##  8 Beru White~    165    75 brown   light   blue         47 fema~ femin~ Tatooi~
    ##  9 Dormé          165    NA brown   light   brown        NA fema~ femin~ Naboo  
    ## 10 Padmé Amid~    165    45 brown   light   brown        46 fema~ femin~ Naboo  
    ## # ... with 4 more variables: species <chr>, films <list>, vehicles <list>,
    ## #   starships <list>, and abbreviated variable names 1: hair_color,
    ## #   2: skin_color, 3: eye_color, 4: birth_year, 5: homeworld
    ## # i Use `colnames()` to see all variable names

    ##Description of any pattern in the data (if any)
    #The pattern I observed is that the Droid species have the lowest height as compared to human's height which starts from 150.
    #This is quite a huge gap in the height of the two species.

    ##Summarize your results and display them by mean(ascending order)
    Results<- Newdata %>% 
      group_by(species) %>% 
      summarise(mymean= mean(height, na.rm= TRUE))
    Results

    ## # A tibble: 2 x 2
    ##   species mymean
    ##   <chr>    <dbl>
    ## 1 Droid     131.
    ## 2 Human     177.

    ##Filter out the Na's in the dataset and report the no. of rows affected (removed)
    ##First, check the no. of observations inlcuding the Nas
    dim(Newdata)

    ## [1] 41 14

    ##Remove the Nas
    Filt<- Newdata %>% 
      na.omit()

    ##View the no. of observations after filtering
    dim(Filt)

    ## [1] 18 14

\##Output \#The no. of rows affected (removed are 23)

    ##Load two datasets and join them (made available on <https://www.kaggle.com/>)
    ##First, Import the datasets
    Test<- read.csv("test.csv")
    Training<- read.csv("training.csv")

    ##Now, merge the two datasets
    FinalData<- merge(Test, Training, by= "Sample.ID")

\##Describe how you could explore the relationship between two variables
in the combined dataset \#I would explore the variables “Download
Source” and “Actually Malicious”. The download sources may either \#have
been malicious or not malicious.
