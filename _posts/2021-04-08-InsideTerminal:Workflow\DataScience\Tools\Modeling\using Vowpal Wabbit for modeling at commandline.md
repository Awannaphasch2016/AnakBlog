---
layout: post
title: "InsideTerminal:Workflow\\DataScience\\Tools\\Modeling\\using Vowpal Wabbit for modeling at commandline.md"
date: 2021-04-08 10:02:26
categories: inside-terminal/ workflow/ data-science/ tools/  modeling/ vowpa-wabbit/
---

# References
* youtube 
    * https://www.youtube.com/watch?v=gyCjancgR9U&ab_channel=YuryKashnitsky
* documentation
    * https://github.com/VowpalWabbit/vowpal_wabbit/wiki
* tutorial 
    * basic
        * basic vowpal wabbit commandline 
            * https://vowpalwabbit.org/tutorials/cmd_first_steps.html
        * Vowpal Wabbit Linear Regssion Tutorial
            * https://vowpalwabbit.org/tutorials/getting_started.html
    * advance 
        * Deep Dive Into Logistic Regression: Part 3
            * http://www.philippeadjiman.com/blog/2018/04/03/deep-dive-into-logistic-regression-part-3/
# Tools
# What you will learn
* basic usecase of vowpal wabbit
# Content
* what is vowpal wabbit?
    * Vowpal Wabbit provides fast, efficient, and flexible online machine learning techniques for 
        reinforcement learning, supervised learning, and more. It is influenced by an ecosystem of 
        community contributions, academic research, and proven algorithms. Microsoft Research is a major 
        contributor to Vowpal Wabbit.
* what are vowpal wabbit's alternative?
    * vowpal wabbit
        * general purposed ml tools
            * however, main focus is on reinforcement learning 
        * support 
            * cmd 
            * programming language library
    * sklearn 
        * general purposed ml tools
        * support 
            * programming language library
    * XGBoost
        * gradient boosted decision trees
        * support 
            * programming language library
    * Weka
        * general purposed tools 
        * support
            * cmd 
            * application 

* why vowpal wabbit?
    * faster than competitors by design.
    * online learning

* terminology 
    * Data Syntax explaination
        * ref 
            * https://vowpalwabbit.org/tutorials/getting_started.html
        * `[LABEL] [OPTIONS]: FEATURES:VALUE`
            * note
                * this syntax apply to every row 
                    * see ref link for example 
            * full syntax 
                * `[LABEL] [IMPORTANCE-WEIGHT] [INITIAL-PREDICTION] [TAG]: FEATURES:VALUE` 
            * syntax 
                * LABEL
                * IMPORTANT-WEIGHT 
                    * this implies that this esxample counts twice.
                    * default = 1
                * INITIAL-PREDICTION
                    * sometimes you have mutiple interaction learning systems and want to be able to predict an offset rather than an absolute value
                        * [[validate]] I don't get it 
                * TAG
                    * name of row
* usecase
    * example 
        * train a model
        `vw -d train.txt -f model.vw`
        * predict
            * `vw -d test.txt -i model.vw -p predictions.txt`
            * test with no prediction 
                * `vw -i house.model -t house_dataset -p /dev/stdout --quiet`
        * adjusting validation set
            * `vw house_dataset -l 10 -c --passes 25 --holdout_off`
        * save your model into a file
            * `vw house_dataset -l 10 -c --passes 25 --holdout_off -f house.model`
        * debugging using --audit
            * note 
                * helpful for debuggin a machine learning application
            * `vw house_dataset --audit --quiet` 
* data preperation
    * csv to vowpal wabbit txt input
        * ref 
            * How to convert CSV columns into Vowpal Wabbit txt input file?
                * https://stackoverflow.com/questions/65385962/how-to-convert-csv-columns-into-vowpal-wabbit-txt-input-file 
