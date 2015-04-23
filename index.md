---
title       : Developing Data Products Project
subtitle    : Vehicle Fuel Consumption Calculation
author      : Antonios Papoutsakis
job         : Wind Energy Engineer
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Overview

A Shiny application is developed to calculate fuel consumption of vehicles. For this purpose mtcars dataset is used with data extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973-74 models). The scope of this work is to create regression models for fuel consumption of automatic and manual transmission and develop a shiny application through which relevant calculations can be done. 

Here is a sample of the first four vehicles.

```r
head(mtcars,4)
```

```
##                 mpg cyl disp  hp drat    wt  qsec vs        am gear carb
## Mazda RX4      21.0   6  160 110 3.90 2.620 16.46  0    Manual    4    4
## Mazda RX4 Wag  21.0   6  160 110 3.90 2.875 17.02  0    Manual    4    4
## Datsun 710     22.8   4  108  93 3.85 2.320 18.61  1    Manual    4    1
## Hornet 4 Drive 21.4   6  258 110 3.08 3.215 19.44  1 Automatic    3    1
```

--- .class #id 

## Variable Selection
All variables are originally numeric. We will transfrom to factor the transmission "am", the nuumber of cylinders "cyl", the number of carburetors  "carb" and the number of forward gear "gear". Then We will apply a stepwise algorithm to check all possible models and select the best according to AIC (Akaike information criterion). 

```r
fit1<-lm(mpg~.,mtcars);fit2<-step(fit1)
```

```r
fit2$call
```

```
## lm(formula = mpg ~ cyl + hp + wt + am, data = mtcars)
```
According to the result the model that best describes fuel consumption has four variables. Number of cylinders (factor), horse power (number), weight (number) and gear type (factor).

--- .class #id 

## Model Creation
The two models are developed seperatelly be dividing our dataset into manual and automatic transmission. Then by using predict function from caret package we can calculate projected fuel consumtion values. 



```r
round(autoFit$coef,1)
```

```
## (Intercept)        cyl6        cyl8          hp          wt 
##        30.4        -2.1        -2.7         0.0        -1.8
```

```r
round(manualFit$coef,1)
```

```
## (Intercept)        cyl6        cyl8          hp          wt 
##        43.7        -1.5         2.0         0.0        -6.5
```

As expected increase of weight is a major factor increasing fuel consumption while number of cylinders and horsepower have less impact. 

--- .class #id 

## Shiny Appication
In the developed shiny application the user can insert the 3 independent variables and receive the results of fuel consuption for Automatic and Manual transmission car, an example screenshot is shown below:

 <iframe src = 'https://antonis77.shinyapps.io/Motor-Trend-Shiny-Prediction/'></iframe>
 
 --- .class #id 





