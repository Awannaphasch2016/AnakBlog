---
layout: post
title: "Workflow\\Python\\Python environment for Time Series Forecasting"
date: 2021-04-08 20:05:01
categories: workflow/ python/ tools/ time-series/
---

# References
* Python environment for Time Series Forecasting
    * https://machinelearningmastery.com/python-environment-time-series-forecasting/#:~:text=There%20are%20three%20higher%2Dlevel,modeling%2C%20and%20machine%20learning%20respectively.

# Notes
* this doesn't include my inside-terminal/ tools

# Content
* dataset
    * time series dataset
        * https://www.sktime.org/en/latest/related_software.html
* collection of time series models 
    * https://www.sktime.org/en/latest/related_software.html
* list of python libraries for time series analysis
    * core
        * Pandas 
        * statsmodels
            * statistical test for stationarity.
                * eg
                    * Augmented Dickey-Fuller unit root test.
            * Time series analysis plots 
                * eg
                    * autocorrelation function (ACF) and partial autocorrelation function (PACF). 
                    * Linear time series models such as autoregression (AR), moving average (MA), autoregressive moving average (ARMA), and autoregressive integrated moving average (ARIMA). 
        * scikit-learn
            * data preparation  
            * machine learning algorithm
            * resampling methods for TimeSeriesSplit
    * options 
        * machine larning 
            * sktime 
                * more star and more active than tslearn.
            * tslearn
                * only time series machine learning library that provide time series clustering.
            * Darts  
                * newest one, seem to be the most promising.
                * its goal is to make the library to unify time-series machin learning.
        * deep learning 
            * sktime-dl 
                * [2021-04-08 21:35:16] it is not currently maintained

