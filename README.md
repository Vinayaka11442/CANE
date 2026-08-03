
<!-- README.md is generated from README.Rmd. Please edit that file -->

# CANE

<!-- badges: start -->

<!-- badges: end -->

The goal of CANE is to support pooled analysis of variance (ANOVA) for
the following designs: (1) ‘PooledCRD()’: completely randomized design;
(2) ‘PooledRBD()’: randomized block design; (3) ‘PooledLSD()’: Latin
square design; (4) ‘PooledSPD()’: split plot design; and (5)
‘PooledStPD()’: strip plot design.

## Installation

You can install the development version of CANE like so: package
installation can be done directly by calling
‘devtools::install_github(“Vinayaka11442/CANE”)’

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(CANE)
## basic example code
# Creating a sample dataset for Pooled Completely Randomized Design (CRD)
df <- data.frame(
Loc = factor(rep(c("L1", "L2"), each = 9)), # Locations
Treatment = factor(rep(c("T1", "T2", "T3"), times = 6)), # Treatments
Yield = c(18, 7, 11, 10, 19, 12, 15, 8, 13,
18, 5, 11, 7, 19, 21, 22, 9, 14) # Yield values
)
# Running PooledCRD function on the dataset
out <- PooledCRD(df, "Yield", "Loc", "Treatment", 0.05, 1)
# Print results
print(out)
#> $Individual_ANOVA
#> $Individual_ANOVA$L1
#>             Df Sum Sq Mean Sq F value Pr(>F)
#> Treatment    2  14.89   7.444   0.362   0.71
#> Residuals    6 123.33  20.556               
#> 
#> $Individual_ANOVA$L2
#>             Df Sum Sq Mean Sq F value Pr(>F)
#> Treatment    2  40.67   20.33    0.44  0.663
#> Residuals    6 277.33   46.22               
#> 
#> 
#> $Location_wise
#> $Location_wise$L1
#> $Location_wise$L1$statistics
#>    MSerror Df     Mean      CV     MSD
#>   20.55556  6 12.55556 36.1101 11.3583
#> 
#> $Location_wise$L1$parameters
#>    test    name.t ntr StudentizedRange alpha
#>   Tukey Treatment   3         4.339195  0.05
#> 
#> $Location_wise$L1$means
#>       Yield      std r       se Min Max  Q25 Q50  Q75
#> T1 14.33333 4.041452 3 2.617604  10  18 12.5  15 16.5
#> T2 11.33333 6.658328 3 2.617604   7  19  7.5   8 13.5
#> T3 12.00000 1.000000 3 2.617604  11  13 11.5  12 12.5
#> 
#> $Location_wise$L1$comparison
#> NULL
#> 
#> $Location_wise$L1$groups
#>       Yield groups
#> T1 14.33333      a
#> T3 12.00000      a
#> T2 11.33333      a
#> 
#> 
#> $Location_wise$L2
#> $Location_wise$L2$statistics
#>    MSerror Df Mean       CV      MSD
#>   46.22222  6   14 48.56209 17.03233
#> 
#> $Location_wise$L2$parameters
#>    test    name.t ntr StudentizedRange alpha
#>   Tukey Treatment   3         4.339195  0.05
#> 
#> $Location_wise$L2$means
#>       Yield      std r       se Min Max  Q25 Q50  Q75
#> T1 15.66667 7.767453 3 3.925227   7  22 12.5  18 20.0
#> T2 11.00000 7.211103 3 3.925227   5  19  7.0   9 14.0
#> T3 15.33333 5.131601 3 3.925227  11  21 12.5  14 17.5
#> 
#> $Location_wise$L2$comparison
#> NULL
#> 
#> $Location_wise$L2$groups
#>       Yield groups
#> T1 15.66667      a
#> T3 15.33333      a
#> T2 11.00000      a
#> 
#> 
#> 
#> $Bartlett_Test
#> 
#>  Bartlett test of homogeneity of variances
#> 
#> data:  residuals_values and group_labels
#> Bartlett's K-squared = 1.2036, df = 1, p-value = 0.2726
#> 
#> 
#> $Pooled_ANOVA
#> Analysis of Variance Table
#> 
#> Response: Yield
#>               Df Sum Sq Mean Sq F value Pr(>F)
#> Loc            1   9.39   9.389  0.2812 0.6056
#> Treatment      2  45.44  22.722  0.6805 0.5249
#> Loc:Treatment  2  10.11   5.056  0.1514 0.8611
#> Residuals     12 400.67  33.389               
#> 
#> $Treatments_Comparison
#> $statistics
#>    MSerror Df     Mean       CV      MSD
#>   33.38889 12 13.27778 43.51867 8.900286
#> 
#> $parameters
#>    test    name.t ntr StudentizedRange alpha
#>   Tukey Treatment   3         3.772929  0.05
#> 
#> $means
#>       Yield      std r       se Min Max   Q25  Q50   Q75
#> T1 15.00000 5.585696 6 2.358986   7  22 11.25 16.5 18.00
#> T2 11.16667 6.210207 6 2.358986   5  19  7.25  8.5 16.50
#> T3 13.66667 3.777124 6 2.358986  11  21 11.25 12.5 13.75
#> 
#> $comparison
#> NULL
#> 
#> $groups
#>       Yield groups
#> T1 15.00000      a
#> T3 13.66667      a
#> T2 11.16667      a
#> 
#> attr(,"class")
#> [1] "group"
```
