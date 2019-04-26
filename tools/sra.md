# 如何从SRA下载序列文件

## Using SRAtoolkit
SRA toolkit has been configured to connect to NCBI SRA and download via FTP. The simple command to fetch a SRA file you can use this command:

### 下载前10条reads，输出到屏幕

```
fastq-dump -Z -X 10 SRR6656085
```
### 下载到文件
```
fastq-dump SRR6656085
```
This will download the SRA file (in sra format) and then convert them to fastq file for you. If your SRA file is paired, you will still end up with a single fastq file, since, fastq-dump, by default writes them as interleaved file. To change this, you can provide `--split-files` argument.
```
fastq-dump --split-files SRR6656085
```
The downloaded fastq files will have sra number suffixed on all header lines of fastq file

下载的序列文件压缩保存。
```
fastq-dump --split-files --gzip SRR6656085
```

下载fasta序列  
```
fastq-dump --split-files --fasta SRR6656085
```
