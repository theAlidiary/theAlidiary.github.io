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

# What can you expect from this blog?

This is my first blog. And I hope it would be of great interest to those, who are planning to write their dissertations or for anyone aiming to analyze statistics such as socioeconomic development etc. within or across the countries. In this regard, [World Development Indicators (WDI)](http://datatopics.worldbank.org/world-development-indicators/), which is one leading open data source, from the [World Bank](http://www.worldbank.org/). It offers statistics on more than 1500 indicators, ranging from 1960 to the latest date, and covering around 200 plus countries. With such an importance, still, for majority of investigators, it is such a daunting process to download data, then clean it and make it ready for the question to be answered. 
However, in this blog I am going to explain it in step by step, how to download, clean, visualize and analyze these statistics within [
R (programming language)] (https://www.r-project.org/about.html). Where you don’t need to visit any external site, or open Excel etc.

# Indicators and countries to be investigated in the blog

To make it more interactive, I have tried to explain all these steps, with three example indicators: Military expenditure (% of GDP); Government expenditure on education, total (% of GDP) and Current health expenditure (% of GDP). The countries selected are India, Pakistan and Bangladesh.

# Package

I will use the “WDI-package”, to search and download statistics on these indicators. 


# **1. Getting Data on required Indicators**

First, we need to search indicators and get codes for these. I am searching these one by one. You may do these at once.

## 1.1 Searching indicators and get codes

### 1.1.1 Search for military expenditure

From the first search result I found *Military expenditure (% of GDP)* and its code *MS.MIL.XPND.GD.ZS*

### 1.1.2 Search for health expenditure

From the second search result I found *Current health expenditure (% of GDP)* and its code *SH.XPD.CHEX.GD.ZS*

### 1.1.3 Search for expenditure on education

From the third search result I found *Government expenditure on education, total (% of GDP)* and its code *SE.XPD.TOTL.GD.ZS*

## 1.2 Getting data for selected indicators

Now let's have a look at downloaded data


# **2. Cleaning the Data**

After downloading, the next stage is to clean data. From the glimpse of the data. As I am concerned only with years for which data is available. Therefore, I want to remove observations with NAs.

As there are three countries, so lets filter years which are repeated 3 times, then join it with original data. While removed remaining. There are seven observations left for each country now. 

To get the final data for visualization, data is reshaped. Subsequently rounded and selected only three intervals i.e. $2000$, $2006$ and $2012$


# **3. Data visualizations**

## **3.1 Military expenditure (% of GDP)**

## **3.2 Current health expenditure (% of GDP)**

## **3.3 Government expenditure on education, total (% of GDP)**


