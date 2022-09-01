## R Markdown

    ##TASK 11. Cluster Analysis
    ##Using the Iris Dataset
    #Load Iris
    data("iris")

    ##Remove "species" column
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
    NewIris<- select(iris, -Species)

    ##Conduct cluste analysis using 3 clusters
    irisCluster<- kmeans(NewIris, centers = 3, nstart = 20)

    ##We can compare the predicted clusters with the original data.
    table(irisCluster$cluster, iris$Species)

    ##    
    ##     setosa versicolor virginica
    ##   1      0         48        14
    ##   2     50          0         0
    ##   3      0          2        36

    ##Visualize Clusters 
    library(cluster)
    clusplot(iris, irisCluster$cluster, color = T, shade = T, labels = 0, lines = 0)

![](TASK-11--Cluster-Analysis_files/figure-markdown_strict/unnamed-chunk-5-1.png)
\##Notably, setosa cluster perfectly elaborated, while virginica and
versicolor have a little noise between their clusters

    ##Some other visual plots
    plot(NewIris[c("Sepal.Length", "Sepal.Width")], col= irisCluster$cluster)

![](TASK-11--Cluster-Analysis_files/figure-markdown_strict/unnamed-chunk-6-1.png)
