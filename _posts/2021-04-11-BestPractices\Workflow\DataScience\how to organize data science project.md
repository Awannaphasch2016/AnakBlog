---
layout: post
title: "BestPractices\Workflow\DataScience\how to organize data science project"
date: 2021-04-11 21:50:34

categories: best-practices/ workflows/ data-sciences/ organizations/ 
---

# Terminology
    * [[Exploratory data analysis (EDA)]]
    * [[Exploratory Model Analysis (EMA)]]
        * I named it model exploration.
    * [[data science pipeline]]
    * [[DRY Principle]]

# Requirement 
    * self-contained code should be in separated folder.
        * Example of self-contained code are the following.
            * components of data science pipeline including 
                the following
                1. evaluation
                2. data preparation
                3. featurization
                4. modelling
                5. evaluation 
                6. outputs
            * experiments folder
                * experiments should have separate folder because each experiments have different goal.
                * experiments folder simply connects class/function/parameters from machine learning
                    pipeline to achieve a certain goal.
                * eg
                    * exploration 
                        * EDA. 
                        * EMA.
                    * optimization 
                        * hyperparameter tuning.
                        * model performance optimization.
            * example folder.
                * This is used when learning about new library/services which will be used in the 
                    project. 
                * This allow you to make a quick example of how things works to help with recalling 
                    process.
            * documentation folder
                * planning should be maintained here planning.
                * documentation about code/references etc. 
            * Experimental logs folder 
                * this is to keep record of important findings.
    * There should be keyword representation for each self-contained folder. I purposed the following
        name convention.
        * Data/
            * Raw/
            * Process/
            * Scratch/
        * Docs/
        * Examples/
        * Experiments/
            * ExperimentN/
                * Exploration/
                    * EDA/
                    * EMA/
                        * note 
                            * I exploratory model analysis
                * Optimization/
                    * ParamTuning/
                    * ModelTuning/
        * Featurization/
        * Data Preparation/
        * Models/
        * Scripts/
            * note
                * script related to the whole project (not just toward certains experiments)
        * TMP/
            * note
                * contain files that are frequently changed.
                * contain files that will be removed later on. 
        * Utils/


