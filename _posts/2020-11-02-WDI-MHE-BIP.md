---
layout: post
title: "Downloading, cleaning and analyzing, WDI indicators in R with codes and examples"
date: 2020-11-02
categories: R
status: publish
published: true
#status: development
#published: false
---

# **What’s in this blog?**

This blog is about performing all the following tasks using [R programming language](https://www.r-project.org/about.html) with expamples, codes and step by step explanation.

- How to search your variable(s) of interest, in the [World Bank](http://www.worldbank.org/), from [International Debt Statistics](https://data.worldbank.org/products/ids)  to the [World Development Indicators (WDI)](http://datatopics.worldbank.org/world-development-indicators/)?

<img src="/assets/img/2020-11-02-WDI-MHE-BIP.Rmd/wdithemes.png" title="plot of wdithemes" alt="plot of wdithemes" style="display: block; margin: auto;" />

- How to download data for the variable(s), ranging from 1960 to the latest?

- How to clean the data and readying it for your analysis?

- How to visualize your statistic?


# **Example for explaining the above tasks**

## **Variables/Indicators**

1. Military expenditure (% of GDP)

2. Government expenditure on education, total (% of GDP)

3. Current health expenditure (% of GDP)

## **Countries**

1. Bangladesh.

2. India

3. Pakistan


# **1. Getting Data on required Indicators**

First, we need to search indicators and get codes for these. I am searching these one by one. You may do these at once.

## 1.1 Searching indicators and get codes

### 1.1.1 Search for military expenditure

{% highlight r %}
library(WDI)

WDIsearch(string="military expenditure",
          short = TRUE)

{% endhighlight %}

 {% highlight text %}

     indicator           name                                                        
[1,] "MS.MIL.XPND.CD"    "Military expenditure (current USD)"                        
[2,] "MS.MIL.XPND.CN"    "Military expenditure (current LCU)"                        
[3,] "MS.MIL.XPND.GD.ZS" "Military expenditure (% of GDP)"                           
[4,] "MS.MIL.XPND.GN.ZS" "Military expenditure (% of GNI)"                           
[5,] "MS.MIL.XPND.ZS"    "Military expenditure (% of general government expenditure)"

{% endhighlight %}

From the first search result I found ***Military expenditure (% of GDP)*** and its code ***MS.MIL.XPND.GD.ZS***

### 1.1.2 Search for health expenditure

{% highlight r %}

WDIsearch(string="current health expenditure",
          short = TRUE)

{% endhighlight %}

{% highlight text %}

     indicator           name                                                                              
[1,] "SH.XPD.CHEX.GD.ZS" "Current health expenditure (% of GDP)"                                           
[2,] "SH.XPD.CHEX.PC.CD" "Current health expenditure per capita (current US$)"                             
[3,] "SH.XPD.CHEX.PP.CD" "Current health expenditure per capita, PPP (current international $)"            
[4,] "SH.XPD.EHEX.CH.ZS" "External health expenditure (% of current health expenditure)"                   
[5,] "SH.XPD.GHED.CH.ZS" "Domestic general government health expenditure (% of current health expenditure)"
[6,] "SH.XPD.OOPC.CH.ZS" "Out-of-pocket expenditure (% of current health expenditure)"                     
[7,] "SH.XPD.PVTD.CH.ZS" "Domestic private health expenditure (% of current health expenditure)"   

{% endhighlight %}

From the second search result I found ***Current health expenditure (% of GDP)*** and its code ***SH.XPD.CHEX.GD.ZS***

### 1.1.3 Search for expenditure on education

{% highlight r %}

WDIsearch(string="government expenditure on education",
          short = TRUE)

{% endhighlight %}


{% highlight text %}

      indicator                
 [1,] "SE.XPD.EDUC.ZS"         
 [2,] "SE.XPD.PRIM.ZS"         
 [3,] "SE.XPD.SECO.ZS"         
 [4,] "SE.XPD.TERT.ZS"         
 [5,] "SE.XPD.TOTL.GB.ZS"      
 [6,] "SE.XPD.TOTL.GD.ZS"      
 [7,] "UIS.X.PPP.FSGOV"        
 [8,] "UIS.X.PPP.UK.FSGOV"     
 [9,] "UIS.X.PPPCONST.FSGOV"   
[10,] "UIS.X.PPPCONST.UK.FSGOV"
      name                                                                                                                 
 [1,] "Public Expenditure on Education  (% GDP)"                                                                           
 [2,] "Expenditure on primary education (% of government expenditure on education)"                                        
 [3,] "Expenditure on secondary education (% of government expenditure on education)"                                      
 [4,] "Expenditure on tertiary education (% of government expenditure on education)"                                       
 [5,] "Government expenditure on education, total (% of government expenditure)"                                           
 [6,] "Government expenditure on education, total (% of GDP)"                                                              
 [7,] "Government expenditure on education, PPP$ (millions)"                                                               
 [8,] "Government expenditure on education not specified by level, PPP$ (millions)"                                        
 [9,] "Government expenditure on education, constant PPP$ (millions)"                                                      
[10,] "Government expenditure on education not specified by level, constant PPP$ (millions)"    

{% endhighlight %}

From the third search result I found ***Government expenditure on education, total (% of GDP)*** and its code ***SE.XPD.TOTL.GD.ZS***

## 1.2 Getting data for selected indicators

{% highlight r %}

DHEexp_data<- WDI(country = c("BGD","IND","PAK"),
    indicator = c('Military_expenditure' = 'MS.MIL.XPND.GD.ZS',
                  'Health_expenditure' = 'SH.XPD.CHEX.GD.ZS',
                  'Education_expenditure' = 'SE.XPD.TOTL.GD.ZS'),
    start=1960, end=2020)

{% endhighlight %}

Now let's have a look at downloaded data

{% highlight r %}

library(tibble)

as_tibble(DHEexp_data)

{% endhighlight %}

{% highlight text %}

# A tibble: 183 x 6
   iso2c country     year Military_expenditure Health_expenditure Education_expenditure
   <chr> <chr>      <int>                <dbl>              <dbl>                 <dbl>
 1 BD    Bangladesh  1960                   NA                 NA                    NA
 2 BD    Bangladesh  1961                   NA                 NA                    NA
 3 BD    Bangladesh  1962                   NA                 NA                    NA
 4 BD    Bangladesh  1963                   NA                 NA                    NA
 5 BD    Bangladesh  1964                   NA                 NA                    NA
 6 BD    Bangladesh  1965                   NA                 NA                    NA
 7 BD    Bangladesh  1966                   NA                 NA                    NA
 8 BD    Bangladesh  1967                   NA                 NA                    NA
 9 BD    Bangladesh  1968                   NA                 NA                    NA
10 BD    Bangladesh  1969                   NA                 NA                    NA
# ... with 173 more rows

{% endhighlight %}

# **2. Cleaning the Data**

After downloading, the next stage is to clean data. From the glimpse of the data. As I am concerned only with years for which data is available. Therefore, I want to remove observations with NAs.

{% highlight r %}

library(tidyr)
library(dplyr)

DHEexp_data <- drop_na(DHEexp_data)

as_tibble(DHEexp_data)

{% endhighlight %}

{% highlight text %}

# A tibble: 38 x 6
   iso2c country     year Military_expenditure Health_expenditure Education_expenditure
   <chr> <chr>      <int>                <dbl>              <dbl>                 <dbl>
 1 BD    Bangladesh  2000                 1.36               2.00                  2.13
 2 BD    Bangladesh  2001                 1.29               1.99                  2.17
 3 BD    Bangladesh  2002                 1.19               2.15                  2.02
 4 BD    Bangladesh  2003                 1.14               2.19                  2.07
 5 BD    Bangladesh  2004                 1.12               2.21                  1.94
 6 BD    Bangladesh  2006                 1.11               2.32                  2.13
 7 BD    Bangladesh  2007                 1.11               2.39                  2.20
 8 BD    Bangladesh  2008                 1.06               2.35                  2.05
 9 BD    Bangladesh  2009                 1.16               2.40                  1.94
10 BD    Bangladesh  2011                 1.36               2.57                  2.13
# ... with 28 more rows

{% endhighlight %}

As there are three countries, so lets filter years which are repeated 3 times, then join it with original data. While removed remaining. There are seven observations left for each country now.

{% highlight r %}

yr3 <- count(DHEexp_data,year, sort = TRUE)

DHEexp_data <-left_join(DHEexp_data,yr3, by="year")

DHEexp_data <- filter(DHEexp_data, n==3)

DHEexp_data <- select(DHEexp_data,1:6)

as_tibble(DHEexp_data)

{% endhighlight %}

{% highlight text %}

# A tibble: 21 x 6
   iso2c country     year Military_expenditure Health_expenditure Education_expenditure
   <chr> <chr>      <int>                <dbl>              <dbl>                 <dbl>
 1 BD    Bangladesh  2000                 1.36               2.00                  2.13
 2 BD    Bangladesh  2004                 1.12               2.21                  1.94
 3 BD    Bangladesh  2006                 1.11               2.32                  2.13
 4 BD    Bangladesh  2009                 1.16               2.40                  1.94
 5 BD    Bangladesh  2011                 1.36               2.57                  2.13
 6 BD    Bangladesh  2012                 1.32               2.57                  2.18
 7 BD    Bangladesh  2013                 1.26               2.50                  1.97
 8 IN    India       2000                 2.95               4.03                  4.32
 9 IN    India       2004                 2.83               3.96                  3.35
10 IN    India       2006                 2.53               3.63                  3.14
# ... with 11 more rows

{% endhighlight %}

To get the final data for visualization, data is reshaped. Subsequently rounded and selected only three intervals i.e. $2000$, $2006$ and $2012$

{% highlight r %}

DHEexp_data<- pivot_longer(DHEexp_data,
                           !c("iso2c","country","year"),
                           names_to = "expenditures",
                           values_to = "values")

DHEexp_data <- DHEexp_data %>% mutate_if(is.numeric,
                                         round, digits=2)

plotdata <- filter(DHEexp_data,year==2000 |
                     year==2006|
                     year==2012)

as_tibble(plotdata)

{% endhighlight %}

{% highlight text %}

# A tibble: 27 x 5
   iso2c country     year expenditures          values
   <chr> <chr>      <dbl> <chr>                  <dbl>
 1 BD    Bangladesh  2000 Military_expenditure    1.36
 2 BD    Bangladesh  2000 Health_expenditure      2   
 3 BD    Bangladesh  2000 Education_expenditure   2.13
 4 BD    Bangladesh  2006 Military_expenditure    1.11
 5 BD    Bangladesh  2006 Health_expenditure      2.32
 6 BD    Bangladesh  2006 Education_expenditure   2.13
 7 BD    Bangladesh  2012 Military_expenditure    1.32
 8 BD    Bangladesh  2012 Health_expenditure      2.57
 9 BD    Bangladesh  2012 Education_expenditure   2.18
10 IN    India       2000 Military_expenditure    2.95
# ... with 17 more rows

{% endhighlight %}

# **3. Data visualizations**

## **3.1 Military expenditure (% of GDP)**

{% highlight r %}

library(ggplot2)

ggplot(data = filter(plotdata,expenditures=="Military_expenditure"),
       mapping = myplot) + mygeom + mytheme + myguides +
  labs(x="", y="",
       caption = mycaption,
       title = "Military expenditure (% of GDP)")
{% endhighlight %}

<img src="/assets/img/2020-11-02-WDI-MHE-BIP.Rmd/mexp.png" title="plot of mexp" alt="plot of mexp" style="display: block; margin: auto;" />

## **3.2 Current health expenditure (% of GDP)**

{% highlight r %}

ggplot(data = filter(plotdata,expenditures=="Health_expenditure"),
        mapping = myplot) + mygeom + mytheme + myguides +
        labs(x="", y="",
        caption = mycaption,
        title = "Current health expenditure (% of GDP)")

{% endhighlight %}

<img src="/assets/img/2020-11-02-WDI-MHE-BIP.Rmd/hexp.png" title="plot of hexp" alt="plot of hexp" style="display: block; margin: auto;" />

## **3.3 Government expenditure on education, total (% of GDP)**

{% highlight r %}

ggplot(data = filter(plotdata,expenditures=="Education_expenditure"),
       mapping = myplot) + mygeom + mytheme + myguides +
      labs(x="", y="",
       caption = mycaption,
       title = "Government expenditure on education, total (% of GDP)")

{% endhighlight %}

<img src="/assets/img/2020-11-02-WDI-MHE-BIP.Rmd/eexp.png" title="plot of eexp" alt="plot of eexp" style="display: block; margin: auto;" />


## **3.4 Combined graph**

{% highlight r %}
ggplot(data = plotdata,
       mapping = aes(x = year, y = values,
                     fill = country)) +
  geom_col(position = "dodge", width = 3) +
  facet_grid(~year~expenditures) +
  mytheme1 + myguides +
  labs(x="", y="",
       caption = mycaption,
       title = "Expenditures (% of GDP)")

{% endhighlight %}

<img src="/assets/img/2020-11-02-WDI-MHE-BIP.Rmd/combinedgraph.png" title="plot of combinedgraph" alt="plot of combinedgraph" style="display: block; margin: auto;" />
