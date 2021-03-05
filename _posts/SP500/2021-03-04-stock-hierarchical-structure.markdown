---
layout: post
title:  "Stock hierarchical structure"
date:   2021-03-04 12:55:23 +0100
categories: SP500 
author: "Davide Coldebella"
permalink: SP500/Stock-hierarchical-structure
---

This post is the third of a series dedicated to extract covariance/correlation matrices from the daily returns. Here I will present how we sorted the empirical correlation/covariance matrices.

##### **Summary**
Each correlation matrix has an underlying hierarchical cluster structure representing the sectors in the market. We highlight it by converting each correlation matrix into a distance matrix and using the ward sorting algorithm.

---
---
### Hierachical structure
A stylized fact of stock returns is the presence of an underlying hierarchical structure: stocks belonging to the similar industries behave more similarly. 

Our goal is to highlight this hierarchical structure and we will do so using Ward's method, which by desing aims to minimize the internal variance of each cluster. In our case the variance is computed over the correlation distances: given a correlation matrix M, we define
<p align="center">
    <img src="http://latex.codecogs.com/svg.latex?d(M)&space;=&space;(1-M)/2" title="http://latex.codecogs.com/svg.latex?d(M) = (1-M)/2" />
</p>
If we want to find the hierarchical structure of a covariance matrix C instead we first convert it to a correlation matrix, compute its distance with the above formula, and convert the matrix d(M) back to a covariance matrix.
<p align="center">
    <img src="http://latex.codecogs.com/svg.latex?\begin{align}&\Lambda&space;=&space;diag(C)&space;\nonumber\\&M&space;=&space;\Lambda^{-\frac{1}{2}}&space;C&space;\Lambda^{-\frac{1}{2}}&space;\nonumber\\&d(M)&space;=&space;(1-M)/2&space;\nonumber\\&d(C)&space;=&space;\Lambda^{\frac{1}{2}}&space;d(M)&space;\Lambda^{\frac{1}{2}}&space;\nonumber\end{align}" title="http://latex.codecogs.com/svg.latex?\begin{align}&\Lambda = diag(C) \nonumber\\&M = \Lambda^{-\frac{1}{2}} C \Lambda^{-\frac{1}{2}} \nonumber\\&d(M) = (1-M)/2 \nonumber\\&d(C) = \Lambda^{\frac{1}{2}} d(M) \Lambda^{\frac{1}{2}} \nonumber\end{align}" />
</p>

### Results
Given a set of data, we can extract a covariance and a correlation matrix. If we apply Ward's method on the distance matrix obtained from a correlation or a covariance matrix we get drastically different clusters, as can be seen in the images below.

##### **Hierarchical structure of the correlation matrix**
The matrix clearly has a number of clusters (to be determined!) of various sizes.
{% include Corr_sorted.html %}
##### **Hierarchical structure of the covariance matrix**
There are two images:
*   the first one represents the covariance matrix sorted as its respective correlation matrix (notice the same dendrogram as the image above). Clusters are not as evident as before.
*   the second one represents the covariance matrix sorted as explained before. Cluster structure is absent, with 4 outliers at the left and right edge of the dendrogram.
{% include Cov_sorted_as_corr.html %}
{% include Cov_sorted.html %}


