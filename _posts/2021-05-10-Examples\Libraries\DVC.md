---
layout: post
title: "BestPractices\\Workflow\\DataScience\\organize data science project with machine learning pipeline"
date: 2021-04-10 19:16:05

categories: best-practices/ workflows/ data-sciences/ pipelines/ examples/
---
# References
* Youtube
    * [Versioning Data with DVC (Hands-On
        Tutorial!)](https://www.youtube.com/watch?v=kLKBcPonMYw&ab_channel=DVCorg)
    * [Sharing Data and Models with DVC (Hands-On Data Science
        Tutorial!)](https://www.youtube.com/watch?v=EE7Gk84OZY8&ab_channel=DVCorg)
    * [Machine Learning Pipelines with DVC (Hands-On Tutorial!)](https://www.youtube.com/watch?v=71IGzyH95UY&ab_channel=DVCorg) 

# Content
## using commandline 
* list content that is being version control by dvc.
    *  `dvc list https://github.com/iterative/dataset-registry get-started`
* get data fron repo that is version controled by dvc .
    * without metadata of where data is from.
        * `dvc get https://github.com/iterative/dataset-registry use-cases/cats-dogs`
    * with metadata of where data is from.
        * `dvc import https://github.com/iterative/dataset-registry use-cases/cats-dogs`
* check update 
    * `dvc update data/data.xml.dvc`

## using python api
```python
import dvc.api

with dvc.api.open( "get-started/data.xml", repo="https://github.com/iterative/dataset-registry") as fd:
    fd.read()
```

