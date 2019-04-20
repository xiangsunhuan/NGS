## Diamond 基本用法
Diamond比BLAST快500以上！

DIAMOND is a sequence aligner for protein and translated DNA searches, designed for high performance analysis of big sequence data. The key features are:

* Pairwise alignment of proteins and translated DNA at 500x-20,000x speed of BLAST.
* Frameshift alignments for long read analysis.
* Low resource requirements and suitable for running on standard desktops or laptops.
* Various output formats, including BLAST pairwise, tabular and XML, as well as taxonomic classification.

下面我们分别用diamond和BLAST将稻瘟菌的蛋白序列比对到swissprot蛋白库
>swissprot蛋白库和稻瘟菌蛋白序列已经下载在服务器上，位置：/data/lab/ngs/diamond

### diamond比对
```
diamond makedb --in uniprot_sprot.fasta -d swissprot
diamond blastp -d swissprot -q Magnaporthe_oryzae.MG8.pep.all.fa -o mory.dm
```
注意：`diamond`建完索引后新产生了一个文件，以`.dmnd`为后缀名。比对结果文件默认格式为blast表格格式。
### blast比对
```
makeblastdb -in uniprot_sprot.fasta -dbtype prot
blastp -db uniprot_sprot.fasta -query Magnaporthe_oryzae.MG8.pep.all.fa -out mory.blast -outfmt 6
```
makeblastdb建索引后会产生3新的文件。

diamond比对只花了8.26秒！！！blast 跑了2个小时还没完成！！！

### 比较下diamond和blast比对的结果

## More Information
* [blast output format 6](http://www.metagenomics.wiki/tools/blast/blastn-output-format-6)
* [diamond](https://github.com/bbuchfink/diamond)
