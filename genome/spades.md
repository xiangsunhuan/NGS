# SPAdes使用基础
本章主要介绍二代测序序列组装应用。常用的组装软件有：velvet, soap-denovo, idba, ABySS等。
## Introduction to SPAdes
SPAdes包含了以下几个组装软件，适合不同场合的组装任务。
* spades - 基因组组装
* metaSPAdes – a pipeline for metagenomic data sets
* plasmidSPAdes – a pipeline for extracting and assembling plasmids from WGS data sets
* rnaSPAdes – a de novo transcriptome assembler from RNA-Seq data
* truSPAdes – a module for TruSeq barcode assembly

SPAdes主要用于小基因组组装，如细菌基因组，大基因组可以考虑使用soap-denovo等。

## Running spades
> 输入，SPAdes input  

SPAdes takes as input paired-end reads, mate-pairs and single (unpaired) reads in FASTA and FASTQ. For IonTorrent data SPAdes also supports unpaired reads in unmapped BAM format (like the one produced by Torrent Server). However, in order to run read error correction, reads should be in FASTQ or BAM format. Sanger, Oxford Nanopore and PacBio CLR reads can be provided in both formats since SPAdes does not run error correction for these types of data.

To run SPAdes 3.13.0 you need at least one library of the following types:

* Illumina paired-end/high-quality mate-pairs/unpaired reads
* IonTorrent paired-end/high-quality mate-pairs/unpaired reads
* PacBio CCS reads
* Illumina and IonTorrent libraries should not be assembled together. All other types of input data are compatible. SPAdes should not be used if only PacBio CLR, Oxford Nanopore, Sanger reads or additional contigs are available.

SPAdes supports mate-pair only assembly. However, we recommend to use only high-quality mate-pair libraries in this case (e.g. that do not have a paired-end part).

Notes:

* It is strongly suggested to provide multiple paired-end and mate-pair libraries according to their insert size (from smallest to longest).
* It is not recommended to run SPAdes on PacBio reads with low coverage (less than 5).
* We suggest not to run SPAdes on PacBio reads for large genomes.
* SPAdes accepts gzip-compressed files.

## SPAdes运行示例
> 说明：用到的数据存放在：`/data/lab/ngs/spades`，有两个序列文件：`s_6_1.fastq.gz, s_6_2.fastq.gz`。

```
spades.py -1 /data/lab/ngs/spades/s_6_1.fastq.gz -2 /data/lab/ngs/spades/s_6_2.fastq.gz -o ecoli
```

## SPAdes输出
SPAdes stores all output files in <output_dir> , which is set by the user.

* `<output_dir>/corrected/` directory contains reads corrected by BayesHammer in \*.fastq.gz files; if compression is disabled, reads are stored in uncompressed \*.fastq files
* `<output_dir>/scaffolds.fasta` contains resulting scaffolds (recommended for use as resulting sequences)
* `<output_dir>/contigs.fasta` contains resulting contigs
* `<output_dir>/assembly_graph.gfa` contains SPAdes assembly graph and scaffolds paths in [GFA 1.0 format](https://github.com/GFA-spec/GFA-spec/blob/master/GFA1.md)
* `<output_dir>/assembly_graph.fastg` contains SPAdes assembly graph in [FASTG format](http://fastg.sourceforge.net/)
* `<output_dir>/contigs.paths` contains paths in the assembly graph corresponding to contigs.fasta (see details below)
* `<output_dir>/scaffolds.paths` contains paths in the assembly graph corresponding to scaffolds.fasta (see details below)

Contigs/scaffolds names in SPAdes output FASTA files have the following format:
`>NODE_3_length_237403_cov_243.207`
Here 3 is the number of the contig/scaffold, 237403 is the sequence length in nucleotides and 243.207 is the k-mer coverage for the last (largest) k value used. Note that the k-mer coverage is always lower than the read (per-base) coverage.

In general, SPAdes uses two techniques for joining contigs into scaffolds. First one relies on read pairs and tries to estimate the size of the gap separating contigs. The second one relies on the assembly graph: e.g. if two contigs are separated by a complex tandem repeat, that cannot be resolved exactly, contigs are joined into scaffold with a fixed gap size of 100 bp. Contigs produced by SPAdes do not contain N symbols.

## 图形化查看组装结果
To view FASTG and GFA files we recommend to use [Bandage visualization tool](http://rrwick.github.io/Bandage/). Note that sequences stored in assembly_graph.fastg correspond to contigs before repeat resolution (edges of the assembly graph). Paths corresponding to contigs after repeat resolution (scaffolding) are stored in contigs.paths (scaffolds.paths) in the format accepted by Bandage (see Bandage wiki for details). The example is given below.

## 组装结果评估
[QUAST](http://cab.spbu.ru/software/quast/) may be used to generate summary statistics (N50, maximum contig length, GC %, # genes found in a reference list or with built-in gene finding tools, etc.) for a single assembly. It may also be used to compare statistics for multiple assemblies of the same data set (e.g., SPAdes run with different parameters, or several different assemblers). 
