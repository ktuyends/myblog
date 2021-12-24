# Test R Markdown


Bài viết này cũng như vậy, tôi tóm tắt lại một số nội dung trong quyển sách *bookdown: Authoring Books and Technical Documents with R Markdown* của ([Xie 2016](#ref-bookdown2016))

## 1. Sometimes I Write Crap

Code Inline: \$a^2 + b^2 = c^2\$

\$$f(x)=\int_{-\infty}^{\infty} \hat{f}(\xi) e^{2 \pi i \xi x} d \xi$\$

## 2. R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

You can embed an R code chunk like this:

``` r
summary(cars)
```

    ##      speed           dist       
    ##  Min.   : 4.0   Min.   :  2.00  
    ##  1st Qu.:12.0   1st Qu.: 26.00  
    ##  Median :15.0   Median : 36.00  
    ##  Mean   :15.4   Mean   : 42.98  
    ##  3rd Qu.:19.0   3rd Qu.: 56.00  
    ##  Max.   :25.0   Max.   :120.00

``` r
fit <- lm(dist ~ speed, data = cars)
fit
```

    ## 
    ## Call:
    ## lm(formula = dist ~ speed, data = cars)
    ## 
    ## Coefficients:
    ## (Intercept)        speed  
    ##     -17.579        3.932

## 3. Including Plots

You can also embed plots. See Figure <a href="#fig:pie">1</a> for example:

``` r
par(mar = c(0, 1, 0, 1))
pie(
  c(280, 60, 20),
  c('Sky', 'Sunny side of pyramid', 'Shady side of pyramid'),
  col = c('#0292D8', '#F7EA39', '#C4B632'),
  init.angle = -50, border = NA
)
```

<div class="figure">

<img src="{{< blogdown/postref >}}index.vi_files/figure-html/pie-1.png" alt="A fancy pie chart." width="672" />
<p class="caption">
Figure 1: A fancy pie chart.
</p>

</div>

## 4. SQL in R Markdown

``` r
library(DBI)
con <- dbConnect(odbc::odbc(),
                 Driver = "ODBC Driver 17 for SQL Server",
                 Server = "KTUYEN-PC\\DSSQL2019",
                 Database = "AdventureWorks2019",
                 Trusted_Connection = "Yes")
```

``` sql
SELECT TOP 10 Name, CreditRating
FROM Purchasing.Vendor
WHERE CreditRating < 3
```

<div class="knitsql-table">

| Name                       | CreditRating |
|:---------------------------|-------------:|
| Australia Bike Retailer    |            1 |
| Allenson Cycles            |            2 |
| Advanced Bicycles          |            1 |
| Trikes, Inc.               |            2 |
| Morgan Bike Accessories    |            1 |
| Cycling Master             |            1 |
| Chicago Rent-All           |            2 |
| Greenwood Athletic Company |            1 |
| Compete Enterprises, Inc   |            1 |
| International              |            1 |

Table 1: Displaying records 1 - 10

</div>

## 5. Python

## References

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-bookdown2016" class="csl-entry">

Xie, Yihui. 2016. *Bookdown: Authoring Books and Technical Documents with R Markdown*. Boca Raton, Florida: Chapman; Hall/CRC. <https://bookdown.org/yihui/bookdown>.

</div>

</div>

