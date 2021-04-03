---
layout: post
title: Example\Libraries\Pandas\Sliding multilevel index with list as value
date:  2021-03-30 17:41:10 
categories: examples/ libraries/ pandas/ python/
---

# Goal
* Given the dataset, you must filter multilevel index namely 'state' and 'date', whose cells list value have length equal to 7.

# What you will learn
1. understand how to filter with pandas that have list as cell value.
2. understand how to filter with multilevel index pandas.
3. understand how to use pd.Grouper

# Terminology
* dataframe
    * pd.DataFrame.groupby
    * pd.Grouper
    * pd.Series.apply
    * pd.Series.map


# Code

{% highlight python %}

import pandas as pd
import pathlib

data_path = '/home/awannaphasch2016/Documents/Working/COVID19TrendPrediction/Data/Raw/COVID19Cases/StateLevels/us-states.csv'

data = pd.read_csv(
    data_path 
)  

df_by_date = pd.DataFrame(
    data.fillna("NA")
    .groupby(["state", "date"])["cases"]
    .sum()
    .sort_values()
    .reset_index()
)

df_by_date['date'] = pd.to_datetime(df_by_date['date'], format='%Y-%m-%d')
tmp = df_by_date.groupby(['state', pd.Grouper(key="date", freq="1W")])["cases"].apply(list)
tmp1 = pd.Series.to_frame(tmp,name='node')
tmp1[tmp1['node'].map(len) == 7 ]
weekly_inter_node = np.array([i for i in tmp2.iloc[tmp2.index.get_level_values('date') == d]['node'].sort_index().values])

{% endhighlight %}
