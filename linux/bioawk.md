## BioAWK 基础  
Bioawk is an extension of the UNIX core utility command `awk`. It provides several features for biological data manipulation in a similar way as that of `awk`. This tutorial will give a brief introduction and examples for some common tasks that can be done with this command.

You can download and install it from the [Git repository](https://github.com/lh3/bioawk).
### Features  
* It can automatically recognize some popular formats and will parse different features associated with those formats. The format option is passed to `bioawk` using `-c` arg flag. Here arg can be `bed`, `sam`, `vcf`, `gff` or `fastx` (for both `fastq` and `FASTA`). It can also deal with other types of table formats using the `-c header` option. When `header` is specified, the field names will used for variable names, thus greatly expanding the utility.  
* There are several builtin functions (other than the standard `awk` built-ins), that are specific to biological file formats. When a format is read with `bioawk`, the fields get automatically parsed. You can apply several functions on these variables to get the desired output. Let’s say, we read `fasta` format, now we have `$name` and `$seq` that holds sequence name and sequence respectively. You can use the `print` function (`awk` builtin) to print `$name` and `$seq`. You can also use `bioawk` built-in with the `print` function to get length, reverse complement etc by just using `'{print length($seq)}'`. Other functions include `reverse`, `revcomp`, `trimq`, and, `or`, `xor` etc.  
* It can automatically read gzipped/compressed files  
### Options  
* `-t` to set input and output filed separator as tab  
* `-c fmt` to read and parse the file in desired format  
* `-v var=value` initialize a variable and value [std to awk as well]  
* `-H` retain header in the output file (for files like SAM)  
* And all standard awk flags will work with bioawk  
### Variables for each format  
For the `-c` you can either specify `bed`, `sam`, `vcf`, `gff`, `fastx` or `header`. Bioawk will parse these variables for the respective format  
bed |	sam	| vcf |	gff	| fastx
--- | --- | --- | --- | ---
chrom |	qname |	chrom |	seqname |	name
start |	flag |	pos |	source |	seq
end |	rname |	id |	feature |	qual
name |	pos |	ref |	start |	comment
score |	mapq |	alt |	end	 | 
strand | 	cigar |	qual |	score |	 
thickstart |	rnext |	filter |	filter	|   
thickend |	pnext |	info |	strand |	 
rgb |	tlen |	group |	 	|   
blockcount | seq |	attribute |	 |  	 
blocksizes |	qual |  |   |   	 	 	 
blockstarts |  |	 |	 |	 

