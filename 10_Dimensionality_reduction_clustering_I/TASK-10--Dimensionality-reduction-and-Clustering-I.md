## R Markdown

    ##TASK 10. Dimensionality reduction and clustering I
    ##Load the iris dataset
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
    data(iris)

    ##Convert iris data into unlabelled dataset
    df<- iris
    dfIris<- select(df, -Species)

    ##Check the PCA eligibility
    cor(dfIris)

    ##              Sepal.Length Sepal.Width Petal.Length Petal.Width
    ## Sepal.Length    1.0000000  -0.1175698    0.8717538   0.8179411
    ## Sepal.Width    -0.1175698   1.0000000   -0.4284401  -0.3661259
    ## Petal.Length    0.8717538  -0.4284401    1.0000000   0.9628654
    ## Petal.Width     0.8179411  -0.3661259    0.9628654   1.0000000

    mean(cor(dfIris))

    ## [1] 0.4675531

    #The variables are eligible for PCA

\##Formulate two questions or hypotheses on the data, that you want to
answer by using a PCA \#1. Check whether the PCs capture the essence of
the original variable \#2. Check whether the PCs are independent

    ##Now, let's run PCA
    PCA<- princomp(dfIris)

    ##Inspect the loadings with the PCA object
    PCA$loadings

    ## 
    ## Loadings:
    ##              Comp.1 Comp.2 Comp.3 Comp.4
    ## Sepal.Length  0.361  0.657  0.582  0.315
    ## Sepal.Width          0.730 -0.598 -0.320
    ## Petal.Length  0.857 -0.173        -0.480
    ## Petal.Width   0.358        -0.546  0.754
    ## 
    ##                Comp.1 Comp.2 Comp.3 Comp.4
    ## SS loadings      1.00   1.00   1.00   1.00
    ## Proportion Var   0.25   0.25   0.25   0.25
    ## Cumulative Var   0.25   0.50   0.75   1.00

    ##Use the score to check principal components
    PCvalues<- PCA$scores

    ##Check correlation to see whether they are independent
    cor(PCvalues)

    ##               Comp.1        Comp.2        Comp.3        Comp.4
    ## Comp.1  1.000000e+00 -2.845751e-16 -3.269553e-16 -3.617947e-15
    ## Comp.2 -2.845751e-16  1.000000e+00  3.891797e-15  3.898034e-15
    ## Comp.3 -3.269553e-16  3.891797e-15  1.000000e+00 -1.116216e-14
    ## Comp.4 -3.617947e-15  3.898034e-15 -1.116216e-14  1.000000e+00

\##The correlation is almost zero, therefore, the variables are
independent.

    ##Visualize PCA
    #install.packages("ggfortify")
    library(ggfortify)

    PCAplot<- autoplot(PCA, data = iris, colour= 'Species')
    PCAplot

![](TASK-10--Dimensionality-reduction-and-Clustering-I_files/figure-markdown_strict/unnamed-chunk-9-1.png)

    ##Explain the variances with a scree plot
    library(ggplot2)

    ##calculate total variance explained by each principal component
    var_explained = PCA$sdev^2 / sum(PCA$sdev^2)

    ##Create a Scree plot
    qplot(c(1:4), var_explained) + 
      geom_line() + 
      xlab("Principal Component") + 
      ylab("Variance Explained") +
      ggtitle("Scree Plot") +
      ylim(0, 1)

![](TASK-10--Dimensionality-reduction-and-Clustering-I_files/figure-markdown_strict/unnamed-chunk-12-1.png)

    ##Investigate potential correlations of your PCs 
    biplot(PCA)

![](TASK-10--Dimensionality-reduction-and-Clustering-I_files/figure-markdown_strict/unnamed-chunk-13-1.png)

\##Comment what you can see on them and how you interpret the result

    print(var_explained)

    ##      Comp.1      Comp.2      Comp.3      Comp.4 
    ## 0.924618723 0.053066483 0.017102610 0.005212184

\##The first principal component explains 92.46% of the total variation
in the dataset. \##The second principal component explains 5.31% of the
total variation in the dataset. \##The third principal component
explains 1.71% of the total variation in the dataset. \##The first
principal component explains 0.5% of the total variation in the dataset.
