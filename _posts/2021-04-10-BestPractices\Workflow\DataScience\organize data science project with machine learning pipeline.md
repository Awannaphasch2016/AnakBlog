---
layout: post
title: "BestPractices\\Workflow\\DataScience\\organize data science project with machine learning pipeline"
date: 2021-04-10 19:16:05

categories: best-practices/ workflows/ data-sciences/ pipelines/ examples/ in-progress/
---

# References 
* documentation
    * [Get Started: Data Versioning](https://dvc.org/doc/start/data-and-model-versioning)
* article
    * [How to Manage Your Machine Learning Workflow with DVC, Weights & Biases, and
        Docker](https://towardsdatascience.com/how-to-manage-your-machine-learning-workflow-with-dvc-weights-biases-and-docker-5529ea4e59e0)

# Goal 
* established bast practices to organize/manage/track/deploy machine learning experiment for reproducibility.

# Tools
* Weight and Biases
    * for experiment tracking
* DVC
    * data version control
* Docker
    * for deployment

# Content
* Best practices to organize/manage/track/deploy a machine learning project.
    1. set up project with pip3 or conda (Docker if you need it to be more portible)
    2. set up git
    3. load data 
    4. set up dvc 
    5. load data -> prep data -> build model -> produce model performance
    6. track model performance with Weight and Biases 
    7. you can use log to take a snapshot of important finding.
    8. write report to present certain aspect with the following expection.
        * getting optimal feedback toward final goal.
        * emphasis important finding.

