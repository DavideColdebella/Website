---
layout: post
title:  "Introduction"
date:   2021-03-03 13:13:23 +0100
categories: SP500 
author: "Davide Coldebella"
permalink: SP500/Introduction
---

This post is the first of a series dedicated to extract covariance/correlation matrices from the daily returns. Here I will present the raw data and perform a basic exploration to assess the presence of missing values and outliers. In the next post we will see how to post process the data.

##### **Summary**
The data contains daily closure prices for 400 stocks over the years 2000/2016. Almost 12% of data is missing but, after deleting 90 stocks, it is reduced to 1% but it is not filled. We compute the simple returns and see that outliers are indeed present.

---
---
### S&P500 Data

This whole analysis is part of a project, called Pi², started from the [ESILV](https://www.esilv.fr/) school in Paris. The school put us in contact with [G. Marti](https://www.linkedin.com/in/gautier-marti-344b565a/) who supplied the dataset.

This dataset is a .csv file containing daily closure prices for ~400 stocks tracked from early 2000 to late 2016. From the graph below we can see that 12% of data is missing. To be precise, 133 stocks have at least one missing entry, 90 have more than 30% missing entries and 62 have more than half missing entries. We discard those 90 stocks and end up with a dataset having only 1% missing data; moreover all stocks are time series of at least 10 years thus, when we will extrapolate the correlation/covariance matrices, for each single stock we will have a more heterogeneous history.
{% include Missing_values_before.html %}
{% include Missing_values_after.html %}

### Simple returns

After the above step we compute the simple returns by the formula
<p align="center">
    <img src="http://latex.codecogs.com/svg.latex?r_i=\frac{P_i-P_{i-1}}{P_{i-1}}" title="http://latex.codecogs.com/svg.latex?r_i=\frac{P_i-P_{i-1}}{P_{i-1}}" />
</p>



|       |      SPX Index |   AA UN Equity |   LYB UN Equity |   AXP UN Equity |   VZ UN Equity |  
|:------|---------------:|---------------:|----------------:|----------------:|---------------:|
| count | 3973           | 3973           |  1457           |  3973           | 3973           | 
| mean  |    0.000195529 |    0.000126167 |     0.000963509 |     0.00034642  |    0.000189777 |     
| std   |    0.0125155   |    0.0269544   |     0.0227345   |     0.0233133   |    0.0153848   |   
| min   |   -0.0903498   |   -0.160539    |    -0.140139    |    -0.175949    |   -0.118461    |   
| 25%   |   -0.00526341  |   -0.0131417   |    -0.00972566  |    -0.00884017  |   -0.00747935  |    
| 50%   |    0.0005749   |    0           |     0.00160831  |     0.000178723 |    0.000213038 |   
| 75%   |    0.00587121  |    0.0128355   |     0.0125745   |     0.00975548  |    0.00780166  |       
| max   |    0.1158      |    0.232117    |     0.13253     |     0.206485    |    0.146326    |    


