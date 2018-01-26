---
title: Relative frequency analysis (keyness)
weight: 40
chapter: false
draft: false
---


```r
require(quanteda)
require(lubridate)
```

`textstat_keyness()` compares frequencies of words between two groups of documents by the kyeness statistics. This statistical measure was originally implemented in [WordSmith](http://www.lexically.net/wordsmith/) to discover frequent words in target documents. Kyeness is essentially a signed chi-square, where words more frequent than expected are given positive sign. 


```r
news_corp <- quanteda.corpora::download('data_corpus_guardian')
news_toks <- tokens(news_corp, remove_punct = TRUE) 
news_dfm <- dfm(news_toks)
key <- textstat_keyness(news_dfm, 2016 <= year(docvars(news_dfm, 'date'))) 
head(key, 20)
```

```
##           feature      chi2 p n_target n_reference
## 1           trump 3357.8703 0     2886         383
## 2            2016 1978.8983 0     1762         261
## 3         clinton 1919.2093 0     1695         245
## 4         sanders 1591.1874 0     1206          93
## 5            cruz 1326.3063 0      967          58
## 6              eu 1259.6693 0     2256        1005
## 7          brexit 1142.7441 0      767          18
## 8          donald 1142.1275 0      985         132
## 9             gmt  863.3412 0     2105        1193
## 10        hillary  712.4467 0      626          89
## 11     block-time  682.8614 0     3240        2591
## 12       campaign  637.1807 0     1816        1135
## 13         bernie  635.8215 0      466          29
## 14            ted  580.7457 0      448          38
## 15       february  573.2721 0      901         353
## 16        trump's  537.2018 0      520          96
## 17 published-time  515.3862 0     2446        1956
## 18        related  505.5657 0     1996        1476
## 19     republican  504.5048 0      909         407
## 20         kasich  459.9745 0      323          14
```

```r
textplot_keyness(key)
```

<img src="/statistical-analysis/keyness_files/figure-html/unnamed-chunk-2-1.svg" width="768" />

