---
title: Simple frequency analysis
weight: 10
chapter: false
draft: false
---


```r
require(quanteda)
require(quanteda.corpora)
require(ggplot2)
```

Unlike `topfeatures()`, `textstat_frequency()` shows both term and document frequencies. You can also use the function to find the most frequent features within groups.


```r
tweet_corp <- download(url = 'https://www.dropbox.com/s/846skn1i5elbnd2/data_corpus_sampletweets.rds?dl=1')
```




```r
tweet_toks <- tokens(tweet_corp, remove_punct = TRUE) 
tweet_dfm <- dfm(tweet_toks, select = "#*")
freq <- textstat_frequency(tweet_dfm, n = 5, groups = docvars(tweet_dfm, 'lang'))
head(freq, 20)
```

```
##              feature frequency rank docfreq     group
## 1           #twitter         1    1       1    Basque
## 2     #canviemeuropa         1    2       1    Basque
## 3             #prest         1    3       1    Basque
## 4           #psifizo         1    4       1    Basque
## 5     #ekloges2014gr         1    5       1    Basque
## 6            #ep2014         1    1       1 Bulgarian
## 7         #yourvoice         1    2       1 Bulgarian
## 8      #eudebate2014         1    3       1 Bulgarian
## 9            #велико         1    4       1 Bulgarian
## 10 #savedonbaspeople         1    1       1  Croatian
## 11   #vitoriagasteiz         1    2       1  Croatian
## 12           #ep14dk        31    1      31    Danish
## 13            #dkpol        18    2      18    Danish
## 14            #eupol         7    3       7    Danish
## 15        #vindtilep         6    4       6    Danish
## 16    #patentdomstol         4    5       4    Danish
## 17           #ep2014        34    1      34     Dutch
## 18              #vvd        10    2      10     Dutch
## 19               #eu         8    3       6     Dutch
## 20              #pvv         8    4       8     Dutch
```

You can also plot the frequencies easily using `ggplot()`.


```r
tweet_dfm %>% 
  textstat_frequency(n = 15) %>% 
  ggplot(aes(x = reorder(feature, frequency), y = frequency)) +
  geom_point() +
  coord_flip() +
  labs(x = NULL, y = "Frequency") +
  theme_minimal()
```

<img src="/statistical-analysis/frequency_files/figure-html/unnamed-chunk-5-1.svg" width="768" />

