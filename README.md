# ChineseNames

Chinese Name Database 1930-2008

![](https://img.shields.io/badge/R-package-success)
![](https://img.shields.io/badge/Version-0.4.0-success)
![](https://img.shields.io/github/license/psychbruce/ChineseNames?label=License&color=success)
[![](https://img.shields.io/badge/lifecycle-maturing-blue.svg)](https://www.tidyverse.org/lifecycle/#maturing)
[![](https://img.shields.io/github/stars/psychbruce/ChineseNames?style=social)](https://github.com/psychbruce/ChineseNames/stargazers)

[![](https://img.shields.io/badge/Follow%20me%20on-Zhihu-blue)](https://www.zhihu.com/people/psychbruce/ "Personal profile on Zhihu.com")


## Citation

Please cite the following two references if you use this database.

- Bao, H.-W.-S. (2020). ChineseNames: Chinese Name Database 1930-2008 [R package]. https://github.com/psychbruce/ChineseNames

- Bao, H.-W.-S., Cai, H., DeWall, C. N., Gu, R., Chen, J., & Luo, Y. L. L. (2020). Name uniqueness predicts career choice and career achievement. *PsyArXiv*. https://doi.org/10.31234/osf.io/53j86
  + This manuscript has been submitted to a journal and posted on a preprint server (*PsyArXiv*). I will update the reference information once it is accepted and published.


## Install
```r
install.packages("devtools")
# devtools::install_github("psychbruce/bruceR")
devtools::install_github("psychbruce/ChineseNames")
```
*Note*. To use the function `compute_name_index()` in `ChineseNames`, you should also install the package `bruceR`. For an installation guide of `bruceR`, please see: https://github.com/psychbruce/bruceR


## Description
### Data Source
This Chinese name database was provided by *Beijing Meiming Science and Technology Company* and originally obtained from the National Citizen Identity Information Center (NCIIC) of China in 2008.

It consists of nationwide statistics for almost all surnames and given-name characters and covers **1.2 billion Han Chinese population** (96.8% of the Han Chinese population born from 1930 to 2008 and still alive in 2008, i.e., the *living household-registered population*). To our knowledge, this is the most comprehensive and accurate Chinese name database up to now.

The `ChineseNames` package includes five datasets (`data.frame` in R):
- **`familyname`**: 1,806 Chinese surnames with their usage in the Han Chinese population
  + overall frequencies and proportions regardless of gender and birth cohort
- **`givenname`**: 2,614 characters used in Chinese given names with their usage in the Han Chinese population
  + separate frequencies and proportions for each gender and each birth cohort (i.e., pre-1960s, 1960-1969, 1970-1979, 1980-1989, 1990-1999, and 2000-2008)
  + involving all situations of their usage in either single-character or multi-character given names (e.g., the character “伟” in “张伟”, “张伟\*”, “张\*伟”, “王伟”, “王伟\*”, “王\*伟”, …)
- **`top1000name.prov`**: Top 1,000 given names (character combinations) for 31 Chinese mainland provinces
- **`top100name.year`**: Top 100 given names (character combinations) for 6 birth cohorts
- **`top50char.year`**: Top 50 given-name characters for 6 birth cohorts

*Note*. The “ppm” in variable names of these datasets means “parts per million (百万分率)” (e.g., ppm = 1 means a proportion of 1/10<sup>6</sup>).


### Name Variables
- **NLen: full-name length**
  + 2~4
  + A Chinese given name can be any Chinese character or any combination of two characters (rarely three characters).
  + A Chinese surname usually consists of one character (rarely two characters [“compound surname”, 复姓]).
- **NU: given-name uniqueness (character level)**
  + 1~6
  + NU = –log<sub>10</sub>(P<sub>given-name</sub> + 10<sup>–6</sup>)
    + P<sub>given-name</sub> = percentage of a character used in either single-character or multi-character given names among the Han Chinese population within a specific birth cohort
    + The distribution of P<sub>given-name</sub> is highly skewed, so we log-transform and reverse it to get an index of uniqueness easy to be interpreted.
    + As the Chinese given-name database does not include some extremely rare characters, a small constant (10<sup>–6</sup>) is added to adjust for zero percentage (P<sub>given-name</sub> = 0) and limit the maximum of NU to 6.00.
    + NU ranges from 1.18 to 6.00, with a higher value indicating a more unique character. This index can be directly interpreted. For instance, NU = 2 means that 1% of people use this character in given names within their birth cohort; and NU = 3 means that 1‰ of people use this character in given names within their birth cohort.
    + For data without birth-year information, you can just use the averaged percentage across all six birth cohorts to estimate NU (see the help page of the function `compute_name_index()`).
- **CCU: character uniqueness in daily Chinese corpus**
  + 1~6
  + CCU = –log<sub>10</sub>(P<sub>character</sub> + 10<sup>–6</sup>)
    + P<sub>character</sub> = percentage of a character appearing in daily Chinese corpus (http://www.cncorpus.org)
    + CCU should be distinguished from NU because daily language usage is quite different from naming practices. For instance, some characters rarely used in personal names may instead be frequently used in daily language (and vice versa).
    + CCU ranges from 1.31 to 6.00. For example, CCU = 2 and 3 mean that the frequency of a character used in written and/or spoken Chinese texts equals to 1% and 1‰, respectively.
- **NV: given-name valence (positivity of character meaning)**
  + 1~5
  + Six raters evaluated the valence (1 = *strongly negative*, 5 = *strongly positive*) of all the 2,614 characters in the Chinese given-name list (interrater reliability ICC = 0.884).
- **NG: given-name gender (difference in proportions of a character used by males vs. females)**
  + –1~1
  + NG = (*N*<sub>male</sub> – *N*<sub>female</sub>) / (*N*<sub>male</sub> + *N*<sub>female</sub>)
    + NG ranges from –1 (completely feminine; 100% used by females) through 0 (gender-neutral; half by females and half by males) to 1 (completely masculine; 100% used by males).
- **SNU: surname uniqueness**
  + 1~6
  + SNU = –log<sub>10</sub>(P<sub>surname</sub> + 10<sup>–6</sup>)
    + SNU ranges from 1.13 to 6.00. Likewise, SNU = 2 and 3 mean that 1% and 1‰ of people possess this surname, respectively.
    + Note that the diversity of surnames is rather limited in China: the top 25 popular Chinese surnames have covered about 60% (0.7 billion) of the Han Chinese population (1.2 billion).
- **SNI: surname initial (alphabetical order)**
  + 1~26
  + As Chinese names are always sorted by surname initials, we include such an index according to the alphabetical order of *Pinyin* initial of each surname.


### Functions in `ChineseNames`
- **`compute_name_index()`**
  + With this function, users can easily compute variables of given names and surnames ready for scientific research. Just input a data frame and it will output a new data frame with all name variables appended.
  + It can handle millions of cases in seconds.
  + We strongly recommend using this function given its convenience and optimized computation efficiency. Otherwise, users have to spend much time on basic work such as transforming and merging different datasets.
  + Example:
```r
library(ChineseNames)  # "bruceR" package should also be installed
?compute_name_index  # see the help page to learn how to use it

demodata  # a data frame with two variables "name" and "birth"
newdata=compute_name_index(demodata,
                           var.fullname="name",  # full name
                           var.birthyear="birth",  # adjust for birth cohort
                           return.all=FALSE)  # or TRUE (return all temporary variables in the computing process)
newdata
```
```
      name birth name0 name1 name2 name3 NLen       NU      CCU       NV         NG      SNU SNI
1 包寒吴霜  1995    包    寒    吴    霜    4 3.604170 4.117764 3.444444 -0.2187045 3.059540   2
2   陈俊霖  1995    陈    俊    霖  <NA>    3 2.461936 4.768781 4.250000  0.4080962 1.341518   3
3     张伟  1985    张    伟  <NA>  <NA>    2 1.661054 3.886456 4.000000  0.6859337 1.152858  26
4     张炜  1988    张    炜  <NA>  <NA>    2 3.166530 5.858278 3.833333  0.6025298 1.152858  26
5   欧阳修  1968  欧阳    修  <NA>  <NA>    3 2.946245 3.550976 2.833333  0.5047172 3.164511  15
6     欧阳  2010    欧    阳  <NA>  <NA>    2 1.950870 3.457427 4.000000  0.5102738 2.969432  15
7 易烊千玺  2000    易    烊    千    玺    4 3.744914 4.894362 2.611111  0.4619253 2.868858  25
8   张艺谋  1950    张    艺    谋  <NA>    3 3.880830 3.661088 3.250000  0.3183426 1.152858  26
9     王的  2005    王    的  <NA>  <NA>    2 5.189320 1.310983 1.666667 -0.5325489 1.125734  23
```


### A Note on Multi-Character Given Names
For a Chinese given name with multiple characters, name variables (NU, CCU, NV, and NG) are averaged across characters. In other words, we target (and recommend targeting) ***characters*** rather than ***character combinations*** in Chinese given names. Here we summarize the reasons for doing so.
1. This practice has been accepted by academic community of psychology (for related previous research, see [Cai et al., 2018](https://doi.org/10.3389/fpsyg.2018.00554)).
2. Analyses based on characters are more practical and allow for more specific examination targeting characters used at different locations in a given name.
3. In computing the percentage of a character used among the Han Chinese population, the Chinese name database has added up all kinds of its usage in either single-character or multi-character given names. Therefore, the percentages of characters indeed reflect their all possible usage in naming practices.
4. Our research has shown that the NU computed by averaging NU across multiple characters (objective NU) is positively correlated with people’s perception (subjective NU) (*r*<sub>obj–subj</sub> = 0.32, *p* < 0.001, *N* = 672, [Study 1](https://doi.org/10.31234/osf.io/53j86)), suggesting an objective–subjective correspondence.
5. For name variables other than NU, it is the only feasible approach to compute them in a large sample.

For details, please see the *SI Appendix* (`Bao_2020_Preprint_SI_Unique-name holders are more likely to choose and succeed in unique jobs.pdf`) posted on our OSF Project (https://osf.io/8syrc/).

We recommend future researchers to follow this practice in processing Chinese given names.


## Author
[Han-Wu-Shuang (Bruce) Bao - 包寒吴霜](https://www.zhihu.com/people/psychbruce/ "Personal profile on Zhihu.com")

E-mail: baohws@psych.ac.cn or psychbruce@qq.com
