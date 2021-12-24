---
title: "Test R Markdown"
subtitle: ""
slug: test-rmarkdown-in-blog
summary: "Đơn giản là nghịch thôi mà!"
date: 2021-05-10
lastmod: 2021-05-10
draft: false
authors: ["Tuyen Kieu"]
images: ["featured.png"]
toc:
  enable: true
license: ''  
hiddenFromHomePage: false
lightgallery: true
---

## 1. Sometimes I Write Crap

Code Inline: \$a^2 + b^2 = c^2$

\$$f(x)=\int_{-\infty}^{\infty} \hat{f}(\xi) e^{2 \pi i \xi x} d \xi$$

## 2. R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

You can embed an R code chunk like this:


```r
summary(cars)
```

```
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
```

```r
fit <- lm(dist ~ speed, data = cars)
fit
```

```
## 
## Call:
## lm(formula = dist ~ speed, data = cars)
## 
## Coefficients:
## (Intercept)        speed  
##     -17.579        3.932
```

## 3. Including Plots

You can also embed plots. See Figure <a href="#fig:pie">1</a> for example:


```r
par(mar = c(0, 1, 0, 1))
pie(
  c(280, 60, 20),
  c('Sky', 'Sunny side of pyramid', 'Shady side of pyramid'),
  col = c('#0292D8', '#F7EA39', '#C4B632'),
  init.angle = -50, border = NA
)
```

<div class="figure" style="text-align: center">
<img src="{{< blogdown/postref >}}index.vi_files/figure-html/pie-1.png" alt="A fancy pie chart." width="672" />
<p class="caption">Figure 1: A fancy pie chart.</p>
</div>

## 4. SQL in R Markdown


```r
library(DBI)
con <- dbConnect(odbc::odbc(),
                 Driver = "ODBC Driver 17 for SQL Server",
                 Server = "KTUYEN-PC\\DSSQL2019",
                 Database = "AdventureWorks2019",
                 Trusted_Connection = "Yes")
```


```sql
SELECT TOP 10 Name, CreditRating
FROM Purchasing.Vendor
WHERE CreditRating < 3
```


<div class="knitsql-table">


Table: Table 1: Displaying records 1 - 10

|Name                       | CreditRating|
|:--------------------------|------------:|
|Australia Bike Retailer    |            1|
|Allenson Cycles            |            2|
|Advanced Bicycles          |            1|
|Trikes, Inc.               |            2|
|Morgan Bike Accessories    |            1|
|Cycling Master             |            1|
|Chicago Rent-All           |            2|
|Greenwood Athletic Company |            1|
|Compete Enterprises, Inc   |            1|
|International              |            1|

</div>

## 5. Python


```python
import numpy as np
import matplotlib.pyplot as plt

r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
fig, ax = plt.subplots(subplot_kw={'projection': 'polar'})
ax.plot(theta, r)
ax.set_rticks([0.5, 1, 1.5, 2])
ax.grid(True)
plt.show()
```

<img src="{{< blogdown/postref >}}index.vi_files/figure-html/unnamed-chunk-3-1.png" width="672" style="display: block; margin: auto;" />
