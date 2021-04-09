---
layout: post
title: Notes\Best Practices\Refactoring\how to refactor terraform
date: 2021-04-03 11:04:23
categories: example/ automation/ terraform/ best_practices/
---

# References
* article
    * [Refactorign Terraform, the right way](https://blog.doit-intl.com/refactor-terraform-into-modules-the-right-way-7bce4d57d66a)
    * [5 lessons Learned From Writing Over 300,00 Lines of Infrastructure Code](https://blog.gruntwork.io/5-lessons-learned-from-writing-over-300-000-lines-of-infrastructure-code-36ba7fadeac1)
    * [7 tips to start your terraform project the righ tway](https://medium.com/@simon.so/7-tips-to-start-your-terraform-project-the-right-way-93d9b890721a)
        * status
            * in progress
# Terminology
# Content
*  Refactorign Terraform, the right way
    * every module shoudl have the followign structure
        * ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FAdaptiveGraphStucture%2FPOCb_qN3Gk.png?alt=media&token=682cd094-55c2-47a3-a370-f8d7e2bfb24c)

    * no hard-code, each hard-coded value becomes a deafulat vairable and aevery module attribute is a variable
        ( some required, some are defualt).
    * The idea is to place elements where they belong. If the main .tf file is larger than 30 lines, break it into logical files i.e., ec2.tf, autoscaling.tf, etc.
    * A good practice is to have the ‘examples’ folder to be used for the development of the module and also serve as a usage example for future reference
    * example of starting script 

    ```
    ➜ export module_name="sample"
    ➜ mkdir -p $module_name/examples $module_name/test
    ➜ cd $module_name && touch \
         main.tf \
         versions.tf \
         default-variables.tf \ 
         required-variables.tf \
         outputs.tf \
         data.tf
    ```

    * 3-tier modules structure
        * building block                               = terraform-resources
        * bulindg services from these primitives block = terraform-service
        * deploy end-to-end enviornments from servies  = terraform-live-envs
        * example
            * ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FAdaptiveGraphStucture%2F1rX4_c1rsu.png?alt=media&token=719a3e02-b50b-4d8c-8606-a4cf024f6f59)

* 7 tips to start your terraform project the righ tway
    * Remote State
    * Separate Your Environments
    * Use Modules
    * Keep it DRY
    * Conditionals
        * it support syntax of a ternary opertaor 
            * `CONDITION ? VAL_IF_TURE : VAL_IF_FALSE`
    * The null_resources
    * Other Useful Functions
        * note
            * the concept that the article mentioned is outdated at the time of writing 
                * [Interpolation Syntax](https://www.terraform.io/docs/configuration-0-11/interpolation.html)
            * new concepts is "Expression" and "Built-in Functions"
                * expreesions are used to refer to or compute rvalues iwthin a configuration
                *

