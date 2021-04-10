---
layout: post
title: "InsideTerminal:Tools\\Python\\Visualizations\\Implmentations\\feedgnuplot"
date: 2021-04-10 14:04:04
categories: inside-terminal/ tools/ python/ visualization/ implementations/ feednuplot/
---

# Code

## line + dot plot
```sh
seq 5 | awk '{print 2*$1, $1*$1}' | \
    feedgnuplot --lines --points --legend 0 "data 0" --title "Test plot" --y2 1 
     --unset grid --terminal 'dumb 80,40' --exit
```

## send plot to stdout
```sh
seq 5 | awk '{print 2*$1, $1*$1}' | feedgnuplot --line --terminal "dumb"
```

## select column for x-axis with --domain
```sh
seq 5 | awk '{print 2*$1, $1*$1}' | feedgnuplot --domain
```

## basic example
```sh
seq 5 | awk '{print 2*$1, $1*$1}' | feedgnuplot --unset grid
```

## using vd with feedgnuplot: vd doesn't work as expected.
```sh
seq 5 | awk 'BEGIN{print "col1,col2"}{print 2*$1","$1*$1}' | vd --delimiter=',' | feedgnuplot
```

## plot with error bar.
```sh
echo '  1 2 1.7 
        2 3 2.6 
        3 4 3.5 ' | feedgnuplot --domain --rangesizeall 3 --with 'yerrorbars'
```

## 3D plot
```sh
echo '1 2 1.7 2.3
        2 3 2.6 3.4
        3 4 3.5 4.5' | feedgnuplot --domain --rangesizeall 2 --3d

## plot stream data and + datetime format
sar 1 -1 |
  awk '$1 ~ /..:..:../ && $8 ~/^[0-9\.]*$/ {print $1,$8; fflush()}' |
  feedgnuplot --stream --domain
               --lines --timefmt '%H:%M:%S'
               --set 'format x "%H:%M:%S"'
```

## bar plot
```sh
echo "# x label a b
       5  aaa   2 1
       6  bbb   3 2
      10  ccc   5 4
      11  ddd   2 1" | \
vnl-filter -p label,a,b | \
feedgnuplot --vnl \
            --xticlabels \
            --set 'style data histogram' \
            --set 'style histogram rowstacked' \
            --set 'boxwidth 0.8' \
            --set 'style fill solid border lt -1' \
            --autolegend \
            --ymin 0 --unset grid
```

##  histogram

### histogram 1
```sh
 N=20000;
 Nsum=10;
 binwidth=.1;
 seq $N | \
 perl -nE '$Nsum = '$Nsum';
           $var  = '$Nsum' / 3.;
           $s = 0; for $i (1..$Nsum) { $s += rand()*2-1; }
           say $s/sqrt($var);' | \
 feedgnuplot --histo 0 --binwidth $binwidth \
             --equation "($N * sqrt(2.*pi) * erf($binwidth/(2.*sqrt(2.)))) * \
                               exp(-(x*x)/(2.)) / \
                               sqrt(2.*pi) title \"Limit gaussian\" with lines lw 2"

```
### historgram 2 

```sh
 N=20000; 
 binwidth=.1; 
 for Nsum in 1 2 3; do
   seq $N | \
   perl -nE '$, = " ";
             $Nsum = '$Nsum';
             $var  = '$Nsum' / 3.;
             $s = 0; for $i (1..$Nsum) { $s += rand()*2-1; }
             say $Nsum,$s/sqrt($var);';
 done | \
 feedgnuplot --dataid --histo 1,2,3 --binwidth $binwidth \
             --autolegend \
             --style 1  'with boxes fill transparent solid 0.3 border lt -1' \
             --style 2  'with boxes fill transparent pattern 4 border lt -1' \
             --style 3  'with boxes fill transparent pattern 5 border lt -1' \
             --equation "($N * sqrt(2.*pi) * erf($binwidth/(2.*sqrt(2.)))) * \
                               exp(-(x*x)/(2.)) / \
                               sqrt(2.*pi) title \"Limit gaussian\" with lines lw 2"

