---
title       : Enerygy Statistics Database
subtitle    : Electric, net installed capacity of electric power plants | United Nations Statistics Division
author      : Trieu Tran
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides

--- .class #s1
## Introduction
"Energy Statistics Database" is a collective of data of energy production, trade, conversion and consumption of more than 220 countries/territories in the world.  The United Nation Statistics Division has developed this database and has made it publicly available.

This presentation provides a quick look at "Electricity, net installed capacity of electric power plants" data (as a subset of the "Energy Statistics Database"), and also comes with some R code snipets for the data exploration purpose.

--- .class #s2
## Data

### Where to get data
Download from URL: [Here](http://data.un.org/Data.aspx?d=EDATA&f=cmID%3aEC)

### Take a quick look at the data

```
## 'data.frame':	47591 obs. of  6 variables:
##  $ Country.or.Area        : Factor w/ 242 levels "1","Afghanistan",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ Commodity...Transaction: Factor w/ 38 levels "Electricity - net installed capacity of electric power plants public solar",..: 20 20 20 20 20 20 20 20 20 20 ...
##  $ Year                   : int  2013 2012 2011 2010 2009 2008 2007 2006 2005 2004 ...
##  $ Unit                   : Factor w/ 1 level "Kilowatts,  thousand": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Quantity               : num  431 431 431 489 489 489 489 489 489 489 ...
##  $ Quantity.Footnotes     : int  1 NA NA 1 1 NA 1 1 1 1 ...
```

--- .class #s3
## Data

### Data Description

<ol>
        <li> Country: Names of countries/territories </li>
        <li> Commodity...Transaction: Installed or generating capacity of different types of electric power plants or pwer sources </li>
        <li>Year: Ranges from 1990 to 2013</li>
        <li>Year: Ranges from 1990 to 2013</li>
        <li>Unit: power unit in Kilowatts (KWs)</li>
        <li>Quantity: Total power installed or generated in a specific year in KWs</li>
</ol>

--- .class #s4 
## Data visualization

### Total net installed capacity of electric power plants of G20 countries 


##### Graph generation code



```r
countries <- c("Argentina", "Australia", "Brazil", "Canada", "China", "France", "Germany", "India", "Indonesia", "Italy", 
                         "Japan", "Mexico", "Russian Federation", "Saudi Arabia", "South Africa", "Korea, Republic of", "Turkey", "United Kingdom", 
                         "United States")

results <- d %>%
        filter(Year > 2002) %>%
        filter(code == "I") %>%
        filter(Country %in%  countries) %>%
        group_by(Country, Year) %>%
        summarise(ttl = sum(Quantity)/1000)

p <- ggplot(data = results, aes(x = factor(Year), y = ttl, color = Country))
p <- p + geom_point() + aes(group = Country) + geom_line() 
p <- p + labs(x = "Year", y = "Total Installed Capacity (MW)", title = "G20 Countries")

ggsave(file.path(figureDir, "plot1.png"), width=9.0, height=5.4, dpi=100)
```

--- .class #s5
## Data visualization

### Total net installed capacity of electric power plants of G20 countriess 

![](figure/plot1.png)

--- .class #s6
## Learn More

Visit my shiny app: [https://trieutn.shinyapps.io/data_products_course_project/](https://trieutn.shinyapps.io/data_products_course_project/)





