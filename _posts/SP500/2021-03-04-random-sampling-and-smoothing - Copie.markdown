---
layout: post
title:  "Random sampling and noise smoothing"
date:   2021-03-04 12:55:23 +0100
categories: SP500 
author: "Davide Coldebella"
permalink: SP500/Random-sampling-and-noise-smoothing
---

This post is the second of a series dedicated to extract covariance/correlation matrices from the daily returns. Here I will present how correlation and covariance matrices were extracted from the data.

##### **Summary**
~25k subsamples were extracted from the return data. Each subsample contains daily returns for ~252 days with starting date chosen uniformly at random and for 80 stocks chosen at random without repetition. From each subsample we compute the correlation and covariance following 2 procedures: the second one involves smoothing the noise. 

---
---
### Random sampling
The goal is to sample uniformly from all dates available and, for each fixed date, to sample 80 stocks without repetition. It is necessary to be careful to include only stocks that have no missing data. \
The length of the time window is chosen to be 252 + K days (where K is a small integer).

##### 1st method
For each subsample we compute its correlation and covariance matrix. 

##### 2nd method: Riemannian average
For each subsample we consider a rolling window of 252 days and compute a list of K+1 covariance matrices. Indexing the matrix with the suffix {0, 1, .. K} we have that the most "recent" is the K-th one. \
Each covariance matrix lives on the Riemannian manifold thus we cannot simply average them since the space is now curved.
Imagine two points A and B connected by a line of length 1: then we can interpolate between them by indicating a value in [0,1] where P(0)=A and P(1)=B. In the same way we can specify a value in [0,1] than interpolates between the most "recent" matrix and each of the others. We assign exponentially decaying weights to each of them (0.9, 0.99, etc). In the end we have K+1 matrices: the K-th one and the K interpolated matrices; we Riemann average them. 
\ \
The difference, for each matrix component, between this averaging method and the classical method applied above is about 1%. We believe that this method allows for smoothing noise.

### Onion matrices

We sample ~25k matrices using the [onion method](https://gmarti.gitlab.io/stats/2018/10/05/onion-method.html). These matrices are sampled uniformly over the space of correlation matrices and will act as a comparison against the empirical matrices extracted from market data.