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

# Content

## How to use these folders?
    * Always initilize the project with core folders. As the experiments grows overtime, you want to 
        add new folder only if you need it.
    * when you start working on coding, you have 2 options
        1. no clear goal on what you want to do 
            * you should create a scratch file in TMP/ then refactor code into
                appropriate folder as your code evolve.
        2. have clear goal
            * create Experiments folders and initialized expriments folder with just scratch file.
    * core folders for the whole repo are the following.
        * note 
            * you might notice that none of the model pipeline components are involved
                * This is because you should start of the project in TMP folder as mentioned eariler
                    this is to ovide 'Premature organization.' 
                    Instead, you want to refactor code as you code (DRY Principle)
                    * Premature organization is where you have to refactor code inside 
                    files match to its current folder. 
        * Data/
        * Docs/
        * Featurization/
        * Data Preparation/
        * Models/
        * Utils/



