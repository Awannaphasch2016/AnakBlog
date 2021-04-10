---
layout: post
title: "Survey\\TimeSeries\\Classification\\list of time series classification algorithms"
date: 2021-04-08 21:28:41

categories: survey/ time-series/ classification/ algorithms/ 
---

# Toc
<!-- vim-markdown-toc Marked -->

* [References](#references)
* [Terminology](#terminology)
* [Content](#content)

<!-- vim-markdown-toc -->

# References
* article 
    * A Brief Survey of Time Series Classification Algorithms
        * https://towardsdatascience.com/a-brief-introduction-to-time-series-classification-algorithms-7b4284d31b97
# Terminology
* Contracting 
    * contracting limits the run time of an algorithm
# Content

* On time series data, time series classification performs better than tabular classifier

* foundation concepts of time series  classification
    * features extractions 
        * categorization
            1. globally
            2. locally
    * data preprocessing
        * series can be transformed into the following
            * primitive 
                * eg
                    * mean
                    * standard
            * series 
                * eg
                    * fourier transform
                    * series of fitted auto-regressive coefficients
* baseline model
    * KNN with DTW
* list of time series classifcaiton algorithms
    * note
        * for details see 
    * Distance-based (KNN with dynamic time warping)
    * Interval-based (TimeSeriesForest)
    * Dictionary-based (BOSS, cBOSS)
    * Frequency-based (RISE — like TimeSeriesForest but with other features)
    * Shapelet-based (Shapelet Transform Classifier)
        * note
            * subsequences or small sub-shapes of times seris that are representative of a class
            * they can be used to detect "phase-independent localised similarity between series within the same class
