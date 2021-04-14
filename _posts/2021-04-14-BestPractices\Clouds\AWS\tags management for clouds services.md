---
layout: post
title: "BestPractices\Clouds\AWS\tags management for clouds services"
date: 2021-04-14 12:10:25

categories: best-practices/ clouds/ tags/ AWS/ 
---

# References
* AWs documentation
    * tagging AWS resources
        * https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html

# Terminology
* aws tags

# Content
* what is tags?
    * tags is key-value system for managing aws resources.

* what is the benefit of tags?
    * tags can help you manage, identify, organize search for, and filter resources.

* how to use tags?
    * You can create tags to categorized resources by purposed, owner, environment, or other criteria.

* What are common usecase of tags?
    * tags for resource organization
        * this is what I focus on in this blog.
    * tags for automation
    * tags for access control

* My best practices for managing tags.
    * all value are separated by _ and are all written in lowercase.
    * For all of my cloud services, I fill out the following tags keys.
        * 'owner'
            * description
                * name of owner of the resources..
        * 'project_type' 
            * project_type key has the following value option
                * learning
                * side
                * self_branding
                * <work>
                    * description 
                        * <work> can be changed based on the name of the current work
                            that you are doing, for example phd, fiverr etc.
        * 'project_name' 
            * description 
                * name of the project. 
        * 'Environment'
            * description
                * 'develop', 'production'
        * 'Department'
            * description 
                * this can be use for cost management for each department in your business
                * if there is project you work on is small and have no department, assign value to 'none'

* other tags managerment system 
    * https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html
