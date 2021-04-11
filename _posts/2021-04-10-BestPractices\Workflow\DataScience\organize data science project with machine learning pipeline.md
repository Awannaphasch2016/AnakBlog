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
    * yaml
        * theory
            * [5 Reasons To Use YAML Files In Your Machine Learning Projects](https://towardsdatascience.com/5-reasons-to-use-yaml-files-in-your-machine-learning-projects-d4c7b9650f27)
        * implementation
            * [How to Write Configuration Files in Your Machine Learning Project.](https://medium.com/analytics-vidhya/how-to-write-configuration-files-in-your-machine-learning-project-47bc840acc19)

# Goal 
* established bast practices to organize/manage/track/deploy machine learning experiment for reproducibility.

# Take Away 
* learn best practice to organize configuration file with yaml file
    * Importance of using a configuration file.
    * Introduction to YAML file.
    * Basics syntax of the YAML file.
    * Rules for creating a YAML file.
    * How to write your first YAML file.
    * How to load the YAML file in python.
    * How to use YAML file (as a configuration file) in your Machine Learning Project.

# Tools
* Weight and Biases
    * for experiment tracking
* DVC
    * data version control
* Docker
    * for deployment

# Content
* Best practices to organize/manage/track/deploy a machine learning project.
    * note 
        * step by step below is for running 1 experiments
        * for running multiple experiments using variuos combination of parameters, yaml file should have
            dedicated key-value for hyper parameter tuning that contains list of parameters to be iterate over.
    1. set up project with pip3 or conda (using pip3 or conda with Docker if you need it to be more portible)
    2. load data 
    3. set up git
    4. set up dvc 
        * use dvc for the following reason
            * always use dvc to do data version control
            * use `dvc run` and commit to git with with comment that describe what is this experiment
                snapshot is about. (why is it so important that you want to take a snap shot of it)
                * so far, I don't see the need of creating new branch because all attemp were 'experiment'
                    there is no 'main experiment' (main level) and 'side experiment.'(dev branch) All of them
                    are experiments, we just have to focus on emphasizing experiments that are important.
                * the only reason to have a new branch is when there is a new experiment direction 
                    * such as 
                        * trying model on the different 'dataset'.
    5. set up configuration file with yaml. 
        * this decouple paramters from code.
        * benefit 
            * easy to read
            * easy to use
            * easy to parse via command line
        * example 
            * ymal file for machine learning parameters configuration 
            ```yaml
            dataset:
              script_path: ../datasets/cifar10_keras.py
            model:
              script_path: ../models/optimized.py
            optimizer:
              script_path: ../optimizers/adam_keras.py
              initial_lr: 0.0001
            train:
              script_path: ../train/train_keras.py
              artifacts_path: ../artifacts/cifar10_opt/
              batch_size: 64
              epochs: 1000
              data_augmentation:
                samplewise_center: False
                samplewise_std_normalization: False
                rotation_range: 0
                width_shift_range: 0.1
                height_shift_range: 0.1
                horizontal_flip: True
                vertical_flip: False
                zoom_range: 0
                shear_range: 0
                channel_shift_range: 0
                featurewise_center: False
                zca_whitening: False
            evaluate:
              batch_size: 1000
              augmentation_factor: 32
              data_augmentation:
                samplewise_center: False
                samplewise_std_normalization: False
                rotation_range: 0
                width_shift_range: 0.15
                height_shift_range: 0.15
                horizontal_flip: True
                vertical_flip: False
                zoom_range: 0
                shear_range: 0
                channel_shift_range: 0
                featurewise_center: False
                zca_whitening: False
            ```
                * list of keys are 
                    * dataset
                    * model
                    * optimizer
                    * train (train model paramters)
                    * evaluate 
        * compare
            * yaml vs passing argument via commandline.
                * using yaml is best because yaml decouple parameters from code.
                    Therefore, using yaml encorage coding best pracitice.
    5. implement preperation file to prep data
    6. implement multiple models file separately
    7. implement train.py to train certain model
    8. track model performance with Weight and Biases 
    9. output and store model performance 
    10. you can use log to take a snapshot of important finding.
    11. write report to present certain aspect with the following expection.
        * getting optimal feedback toward final goal.
        * emphasis important finding.

        
