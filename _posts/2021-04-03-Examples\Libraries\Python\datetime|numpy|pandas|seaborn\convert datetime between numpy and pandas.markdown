---
layout: post
title: Examples\Libraries\Python\datetime|numpy|pandas|seaborn\convert datetime between numpy and pandas
date:  2021-04-03 09:44:22
categories: examples/ libraries/ datetime/  python/ numpy/ pandas/ seaborn/ plot/
---
# TODO
* use data_path to access data -> upload data to S3, and download data to local computer.
* simply file graph. 
    1. (optional) create new blog to folow on plotting correlation across multiple nodes per time step for 
        multiple time step
    2. simply graph to simple graph such as line, box plot.
# Goal
* plot graph where x-axis is date. 
## expected output
![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FAdaptiveGraphStucture%2FFXhHw7bNd8.png?alt=media&token=c93fca9a-9f84-4e3a-ba07-980a698307b6)
# Note
* numpy with more than 1 types will be automatically convert types of all values to 'object' type
    * therefore, you must remember to convert type of row/colum of numpy array after convering from numpy to 
        pandas.
# What you will learn
* how to use plot graph with datetime as x-axis?
* how to convert numpy datetime to datetime (datetime library)?
* how to convert datetime to string datetime?
* how to convert string datetime to pandas datetime?
# Terminology
# Code 
## Setup
* note
    * copy and paste this section for initial setup before the main code.
```
"""Correlation of intra-temporal dependencies"""

from Models.Preprocessing import *
from scipy.stats import  pearsonr
from itertools import product
from itertools import permutations
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


data_path = '/home/awannaphasch2016/Documents/Working/COVID19TrendPredictionData/Raw/COVID19Cases/StateLevels/us-states.csv'

n_input = 5
n_features = 1

data = pd.read_csv(
    str(BASEPATH / pathlib.Path(data_path))
)  

df_by_date = pd.DataFrame(
    data.fillna("NA")
    .groupby(["state", "date"])["cases"]
    .sum()
    .sort_values()
    .reset_index()
)

df_by_date['date'] = pd.to_datetime(df_by_date['date'], format='%Y-%m-%d')
tmp = df_by_date.groupby([ pd.Grouper(key="date", freq="1W"), 'state'])["cases"].apply(np.array)
tmp1 = pd.Series.to_frame(tmp,name='node')
tmp2 = tmp1[tmp1['node'].map(len) == 7 ]
date_indices = np.unique(tmp2.index.get_level_values('date'))

weekly_inter_node = []
for d in date_indices:
    tmp = np.array([i for i in tmp2.iloc[tmp2.index.get_level_values('date') == d]['node'].sort_index().values])
    weekly_inter_node.append(tmp)

def corr_plot():
    week_1 = weekly_inter_node[10]
    x = week_1
    clique_edges = list(product(range(x.shape[0]), range(x.shape[0])))
    clique_edges_ps_corr = []
    for i,j in clique_edges:
        clique_edges_ps_corr.append(pearsonr(x[i, :],x[j, :])[0])
    clique_edges_ps_corr_np = np.array(clique_edges_ps_corr).reshape(x.shape[0], x.shape[0])
    clique_edges_ps_corr_df = pd.DataFrame(clique_edges_ps_corr_np)
    plt.matshow(clique_edges_ps_corr_df)
    cb = plt.colorbar()
    cb.ax.tick_params(labelsize=14)
    plt.title('clique pearson matrix')
    plt.show()

week_1 = weekly_inter_node[10]
x = week_1
nodes_permutation_index = list(permutations(range(x.shape[0]), r=2))

```
## Core
```
from datetime import datetime

weekly_inter_node_ps_corr = []
for i_, week in enumerate(weekly_inter_node):
    # print(date_indices[i_])
    utc = date_indices[i_].astype('<M8[s]').astype(int)
    utc = datetime.utcfromtimestamp(utc)
    utc_str = utc.strftime("%m-%d-%y")
    print(f'week = {i_}: {utc_str}')
    if week.shape[0] == 55:
        for n_1,n_2 in nodes_permutation_index:
            tmp = pearsonr(week[n_1,:], week[n_2,:])[0]
            # weekly_inter_node_ps_corr.append((utc_str,tmp))
            weekly_inter_node_ps_corr.append((i_, utc_str, tmp))
            print(tmp)

weekly_inter_node_ps_corr_np = np.array(weekly_inter_node_ps_corr)
weekly_inter_node_ps_corr_df = pd.DataFrame(weekly_inter_node_ps_corr_np, columns=['Index','Date', 'Corr'])
weekly_inter_node_ps_corr_df['DateOfYear'] = pd.to_datetime(weekly_inter_node_ps_corr_df['Date'], format='%m-%d-%y')
weekly_inter_node_ps_corr_df.set_index('DateOfYear', inplace=True)
weekly_inter_node_ps_corr_df.index = weekly_inter_node_ps_corr_df.index.dayofyear

import pandas as pd
import numpy as np
import seaborn
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=(12,5))
chart = seaborn.boxplot(weekly_inter_node_ps_corr_df['Date'], weekly_inter_node_ps_corr_df['Corr'].values.astype(float), ax=ax)
chart.set_xticklabels(chart.get_xticklabels(), rotation=45, horizontalalignment='right')
plt.show()

```

