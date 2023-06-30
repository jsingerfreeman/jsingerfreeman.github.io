Interesting R
================
Jose Singer-Freeman
2023-06-30

I believe that the coolest thing I’ve learned about programming in R
this semester is the long wide format. The following is an example.

``` r
data(mtcars)



long.data_num<-mtcars%>%pivot_longer(-vs,names_to="variables",values_to="value")


#Simultaneous Wilcoxon rank-sum tests (variables are not normally distributed)
wilcox_test <- long.data_num %>%
  group_by(variables) %>%
  wilcox_test(value ~ vs)%>%
  adjust_pvalue(method = "BH") %>%
   add_significance()

wilcox_test
```

    ## # A tibble: 10 × 10
    ##    variables .y.   group1 group2    n1    n2 statistic          p    p.adj
    ##    <chr>     <chr> <chr>  <chr>  <int> <int>     <dbl>      <dbl>    <dbl>
    ##  1 am        value 0      1         18    14     105   0.36       0.36    
    ##  2 carb      value 0      1         18    14     216.  0.000451   0.000752
    ##  3 cyl       value 0      1         18    14     237   0.00000647 0.000057
    ##  4 disp      value 0      1         18    14     232   0.0000607  0.000152
    ##  5 drat      value 0      1         18    14      60.5 0.0134     0.0168  
    ##  6 gear      value 0      1         18    14      88   0.12       0.133   
    ##  7 hp        value 0      1         18    14     236   0.000031   0.000103
    ##  8 mpg       value 0      1         18    14      22.5 0.0000903  0.000181
    ##  9 qsec      value 0      1         18    14      10   0.0000114  0.000057
    ## 10 wt        value 0      1         18    14     212   0.00116    0.00166 
    ## # ℹ 1 more variable: p.adj.signif <chr>
