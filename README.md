# ChineseNames

Chinese Names Database 1930-2008

![](https://img.shields.io/badge/R-package-success)
![](https://img.shields.io/badge/Version-0.2.0-success)
![](https://img.shields.io/github/license/psychbruce/ChineseNames?label=License&color=success)
[![](https://img.shields.io/badge/lifecycle-maturing-blue.svg)](https://www.tidyverse.org/lifecycle/#maturing)
[![](https://img.shields.io/github/stars/psychbruce/ChineseNames?style=social)](https://github.com/psychbruce/ChineseNames/stargazers)

[![](https://img.shields.io/badge/Follow%20me%20on-Zhihu-blue)](https://www.zhihu.com/people/psychbruce/ "Personal profile on Zhihu.com")


## Citation
Bao, H.-W.-S. (2020). ChineseNames: Chinese Names Database 1930-2008 (R package). Retrieved from https://github.com/psychbruce/ChineseNames


## User Guide
### Install
NOTE: To use the function `compute_name_index()` in `ChineseNames`, you should also install the package `bruceR`. For an installation guide of `bruceR`, please see: https://github.com/psychbruce/bruceR
```r
install.packages("devtools")
# devtools::install_github("psychbruce/bruceR")
devtools::install_github("psychbruce/ChineseNames")
```


### Data Source
This Chinese name database, consisting of nationwide statistics for almost all surnames and given-name characters and covering 1.2 billion Han Chinese population, was obtained from the National Citizen Identity Information Center (NCIIC) of China and provided by *Beijing Meiming Science and Technology Company*.

To our knowledge, this is the most comprehensive and accurate Chinese name database up to now.

The database includes:
1.	a list of 1,806 Chinese surnames with their proportions in the Chinese population;
2.	a list of 2,614 characters used in Chinese given names with their proportions in the Chinese population.

These two lists cover 96.8% of Han Chinese population born from 1930 to 2008 and still alive in 2008 (i.e., the living household-registered population). The given-name list documents the proportions of given-name characters separately for each gender and each birth cohort (i.e., pre-1960s, 1960-1969, 1970-1979, 1980-1989, 1990-1999, and 2000-2008). The surname list records the overall proportions of surnames across gender and birth cohorts.


### Name Variables
- NLen: full-name length
  + 2~4
- NU: given-name uniqueness
  + 1~6
- CCU: character uniqueness in daily corpus
  + 1~6
- NV: given-name valence
  + 1~5
- NG: given-name gender
  + -1~1
- SNU: surname uniqueness
  + 1~6
- SNI: surname initial (alphabetical order)
  + 1~26


### Functions in `ChineseNames`
- `compute_name_index()`
  + Compute variables of given names and surnames for scientific research


## Author
[Han-Wu-Shuang (Bruce) Bao - 包寒吴霜](https://www.zhihu.com/people/psychbruce/ "Personal profile on Zhihu.com")

E-mail: baohws@psych.ac.cn or psychbruce@qq.com
