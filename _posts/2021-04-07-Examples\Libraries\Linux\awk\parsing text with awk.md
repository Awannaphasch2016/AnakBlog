---
layout: post
title: "Examples\\Libraries\\Linux\\awk\\parsing text with awk"
date: 2021-04-07 10:18:44
categories: examples/ libraries/ linux/  awk/ nlp/ parsing/ usecase/
---

# References
* ref
    * https://stackoverflow.com/questions/6284560/how-to-split-a-variable-by-a-special-character/6284596
# Requirements
* pipelining in linux 

# What you will learn
* you will learn simple use case of awk.

# CODE

## Terminology
### Syntax

* `awk '(PATTERN1){...print something..} (PATTERN2){..print something..}`
* `awk 'PATTERN1{...print something..} PATTERN2{..print something..}`
    * awk:terminology:example:
    * note
        * for each line, if PATTERNN is matched, command in {} will be executed.
    * terminology 
        * syntax 
            * `awk 'NR==1{print}' [FILE]` 
            * `awk 'NR==1' [FILE]` 
                * note
                    * for line 1, print whole line 
            * `awk 'NR==1{}' [FILE]`
                * note
                    * for line 1, {} = don't do anything 
            * `awk 'NR==1{print} {print}' [FILE]` 
                * note
                    * {} without condition is the same as condition always set to True.
                    * for eaech line, each condition will be read 1 time
                        * so this example line 1 will be printed 2 times while the rest of the line 
                            will be printed 1 time.
            * `awk '($0 ~ /e$/){print $0}' [FILE]`
            * `awk '$0 ~ /e$/{print $0}' [FILE]`
            * `awk '/e$/{print $0}' [FILE]`
                * :awk:regex:example:terminology
                * note 
                    * print line if first value ends with e.
                    * ~ indicate that if statement of the rigth is matched, condition will be true.
                    * /\<\>/ is regex

## USECASE

* split input text by 'x'
    * `echo 1920x1080 | awk -F"x" '{print $1, $2}'`
* split input text from a line 
    * `echo '$2 = 1920x1080' | awk -F"x" 'sub(/\$[0-9] += +/, "", $1){print $1, $2}'`
* writing function in .awk extension file
    * example 1 
        * Goal
            * rounding number using awk 
        1. create 'test.awk'
        ```
        func round(n){
            n = n + 0.5 
            n = int(n)
            return  n
            }
        /^w/ && $2 9000 (print $1, $2/1024, round($2/1024) "K")
        ```
        2. run `awk -f test.awk [FILE]`
    * example 2 
        * Goal
            * print number that is less than the current line number (line number start from 1)
            * expected output 
                ```
                1
                1 2
                1 2 3
                1 2 3 4
                1 2 3 4 5
                1 2 3 4 5 6
                1 2 3 4 5 6 7
                1 2 3 4 5 6 7 8
                1 2 3 4 5 6 7 8 9
                1 2 3 4 5 6 7 8 9 10
                ```
        1. create loop.awk

    ```
        func printloop(n){
            for(i=1;i<=n;i++){
                printf("%d ", i)
                }
            printf("
        ")
        }

        {printloop($1)}

    ```
        2. run `seq 10 | awk -f loop.awk`



