---
layout: post
title: "Learning\\TimeSeries\\Implementation\\Dynamic Time Warping Distance (DTW).md"
date: 2021-04-08 20:26:07

categories: learning/ time-series/ implementation/ algorithm/ DTW/
---

# CODE

## Core

```
import pandas as pd
import numpy as np
import matplotlib.pylab as plt
from math import sqrt

x=np.linspace(0,50,100)
ts1=pd.Series(3.1*np.sin(x/1.5)+3.5)
ts2=pd.Series(2.2*np.sin(x/3.5+2.4)+3.2)
ts3=pd.Series(0.04*x+3.0)

# ts1.plot()
# ts2.plot()
# ts3.plot()

# plt.ylim(-2,10)
# plt.legend(['ts1','ts2','ts3'])
# plt.show()
# exit()

def euclid_dist(t1,t2):
    return sqrt(sum((t1-t2)**2))

def DTWDistance(s1, s2):
    DTW={}
    for i in range(len(s1)):
        DTW[(i, -1)] = float('inf')
    for i in range(len(s2)):
        DTW[(-1, i)] = float('inf')
    DTW[(-1, -1)] = 0
    for i in range(len(s1)):
        for j in range(len(s2)):
            dist= (s1[i]-s2[j])**2
            # print(i-1,j)
            # print(i,j-1)
            # print(i-1,j-1)
            # print('=====')
            # print(DTW[(i-1, j)],DTW[(i, j-1)], DTW[(i-1, j-1)])
            # print(min(DTW[(i-1, j)],DTW[(i, j-1)], DTW[(i-1, j-1)]))
            DTW[(i, j)] = dist + min(DTW[(i-1, j)],DTW[(i, j-1)], DTW[(i-1, j-1)])

    return sqrt(DTW[len(s1)-1, len(s2)-1])

# print(euclid_dist(ts1,ts2))
# print(euclid_dist(ts1,ts3))
print(DTWDistance(ts1,ts2))
print(DTWDistance(ts1,ts3))

```

