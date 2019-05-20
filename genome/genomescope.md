# 基因组大小估计与复杂性评估
一般在做基因组项目之初，会做一个survey，主要用于评估目标基因组大小，重复序列及杂合度。这里我们介绍genomescope的用法。

Genomescope uses k-mer frequencies generated from raw read data to estimate the genome size, abundance of repetitive elements and rate of heterozygosity.

## 首先了解下什么是k-mer
A K-mer is a substring of length K in a string of DNA bases. For example: All 2-mers of the sequence `AATTGGCCG` are `AA`, `AT`, `TT`, `TG`, `GG`, `GC`, `CC`, `CG`. Similarly, all 3-mers of the sequence `AATTGGCCG` are `AAT`, `ATT`, `TTG`, `TGG`, `GGC`, `GCC`, `CCG`. There are an exponentially increasing number of possible K-mers for increasing numbers of `K`. There are 16 possible 2-mers for DNA if we assume there are only 4 types of bases (A,T,G,C). Similarly, there are 64 possible 3-mers for DNA if we assume there are only 4 types of bases (A,T,G,C). The general rule for the number of possible K-mers given a sequence with 4 possible bases is the following. The number of bases (B) raised to the power of the size (length) of the k-mer (k).`B^k`

Bases	K-mer | size |	Total possible kmers
--- | --- | ---
4	| 1	| 4
4	| 2	| 16
4	| 3	| 64
4	| 4	| 256
4	| 5	| 1,024
4	| 6	| 4,096
4	| 7	| 16,384
4	| 8	| 65,536
4	| 9	| 262,144
4	| 10 |	1,048,576
4	| …	| …
4	| 20 |	1,099,511,627,776

As you can see, there are 64 possibilities for a 3-mer and over a Trillion possibilities for a 20-mer!

下面让我们来看下一个实际的例子，

![](https://isugenomics.github.io/bioinformatics-workbook/assets/images/genomescope/coveragexfrequency_0.png)
The peak around 25 in the plot above is the coverage with the highest number of different 21-mers. Another way to put it is that there were 5e^7 unique 21-mers (frequency) that were observed 25 times (coverage). The normal-like distribution is due to the fact that we don’t get perfect coverage of the genome. There are some regions with a little less coverage and some regions with a little more coverage but the average coverage depth is around 25.

The large number of unique K-mers that have a frequency of 1 right on the left side of the graph is due to PCR errors and works like this. General Rule: For a given sequence, a single PCR error will result in K unique and incorrect K-mers

## How GenomeScope works
GenomeScope extended this idea by exploring how the K-mer graph changes with increasing heterozygosity, PCR errors and PCR duplicates. They determined that the idealized K-mer graph that you understand above is the extreme case where there is low heterozygosity, low PCR errors and low rates of PCR duplicates.

![](https://isugenomics.github.io/bioinformatics-workbook/assets/images/genomescope/screen_shot_2017-02-16_at_7.31.20_am.png)

The big peak at 25 in the graph above is in fact the homozygous portions of the genome that account for the identical 21-mers from both strands of the DNA. The dotted line corresponds to the predicted center of that peak. The small shoulder to the left of the peak corresponds to the heterozygous portions of the genome that accounts for different 21-mers from each strand of the DNA. The two dotted lines to the right of the main peak (at coverage = 25) are the duplicated heterozygous regions and duplicated homozygous regions and correspond to two smaller peaks. The shape of these peaks are affected by the PCR errors and PCR duplicates. The authors were able to come up with an equation that accurately models the shape and size of the K-mer graph using four negative binomial peaks which shape and size are determined by `% heterozygosity`, `% PCR duplication`, `% PCR Error`. All very useful pieces of information to learn about your genome from your raw data.

## 实例操作

1. count

```
jellyfish count -C -m 21 -s 1000000000 -t 10  -o reads.jf <(zcat /data/lab/ngs/spades/*.fastq.gz)
```
2. 计算coverage分布
```
jellyfish histo -t 10 reads.jf > reads.histo
```
3. GenomeScope计算
  * 在线计算：http://qb.cshl.edu/genomescope/
  * 本地计算
    * 下载R代码
    ```
    wget https://raw.githubusercontent.com/schatzlab/genomescope/master/genomescope.R
    ```
    * 运行程序
    
```
Rscript genomescope.R reads.histo 21 100 gs 1000
```
4. 查看结果

结果保存在`gs`文件夹下  
