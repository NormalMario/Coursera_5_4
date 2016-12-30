# Storm Data Analysis
Mario  
18 Dezember 2016  



### Synopsis



### Background

This analysis is based on data provided by the U.S. National Oceanic and Atmospheric
Administration (NOAA). The database contains information on major storms and weather
events in the United States between 1950 and 2011. The goal of this study is
to find out which types of events are most harmful with respect to human
and economic damage.

### Data Processing

Data Analysis is done with the help of R, a software for statistical programming. 
To be reproducible we include the code being used to obtain the results.

#### Data Extraction

We first load the raw data and select those variables relevant to the research question.


```r
myData <- read.csv("repdata_data_StormData.csv.bz2", header = TRUE, sep = ",", quote = "\"")
library(dplyr) # load data manipulation functionality
myData2 <- select(myData, EVTYPE, FATALITIES, INJURIES, PROPDMG,
                        PROPDMGEXP) # extract relevant variables
```

#### Data Manipulation

Then we need to prepare the data for further analysis:


```r
head(myData2) # extract relevant variables
```

```
##    EVTYPE FATALITIES INJURIES PROPDMG PROPDMGEXP
## 1 TORNADO          0       15    25.0          K
## 2 TORNADO          0        0     2.5          K
## 3 TORNADO          0        2    25.0          K
## 4 TORNADO          0        2     2.5          K
## 5 TORNADO          0        2     2.5          K
## 6 TORNADO          0        6     2.5          K
```

```r
sort(table(myData2$PROPDMGEXP), decreasing = TRUE) # examine unit of property damage
```

```
## 
##             K      M      0      B      5      1      2      ?      m 
## 465934 424665  11330    216     40     28     25     13      8      7 
##      H      +      7      3      4      6      -      8      h 
##      6      5      5      4      4      4      1      1      1
```

According to the storm data documentation, 'K' (Thousand Dollar), 'M' (Million Dollar),
and 'B' (Billion Dollar) are valid units for property damage. While we can assume that
'm' is meant to be 'M' there is no clear interpretation available for 
'B', '0', '1', '2', '5', '?'. We will therefore ignore these cases while we're
going to treat 'm' as 'M'.


```r
head(myData2) # extract relevant variables
```

```
##    EVTYPE FATALITIES INJURIES PROPDMG PROPDMGEXP
## 1 TORNADO          0       15    25.0          K
## 2 TORNADO          0        0     2.5          K
## 3 TORNADO          0        2    25.0          K
## 4 TORNADO          0        2     2.5          K
## 5 TORNADO          0        2     2.5          K
## 6 TORNADO          0        6     2.5          K
```

```r
sort(table(myData2$PROPDMGEXP), decreasing = TRUE) # examine unit of property damage
```

```
## 
##             K      M      0      B      5      1      2      ?      m 
## 465934 424665  11330    216     40     28     25     13      8      7 
##      H      +      7      3      4      6      -      8      h 
##      6      5      5      4      4      4      1      1      1
```


## Results






## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:


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

## Including Plots

You can also embed plots, for example:

![](storms_files/figure-html/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
