以正则表达式方式查找文件内容  
`grep` (`g`lobally search a `r`egular `e`xpression and `p`rint) 是Linux最常用的一个命令，常用来对文件/输入进行过滤。匹配方式是每次取一行，如果匹配上了，则输出该行。
```
grep PATTERN FILENAME
```
常见参数：  

| Argument |	Function |
| --- | --- |
| -v |	inverts the match or finds lines NOT containing the pattern. |
| --color	| colors the matched text for easy visualization |
| -F	| interprets the pattern as a literal string. |
| -H,-h	| print, don’t print the matched filename |
| -i	| ignore case for the pattern matching. |
| -l	| lists the file names containing the pattern (instead of match). |
| -n	| prints the line number containing the pattern (instead of match). |
| -c	| counts the number of matches for a pattern |
| -o	| only print the matching pattern |
| -w	| forces the pattern to match an entire word. |
| -x	| forces patterns to match the whole line. |

Some typical scenarios to use `grep`:  

* Counting number of sequences in a multi-fasta sequence file
* Get the header lines of fasta sequence file
* Find a matching motif in a sequence file
* Find restriction sites in sequence(s)
* Get all the Gene IDs from a multi-fasta sequence files and many more.  

Now let’s use `grep` command to do some simple jobs with the sequences:  
### 1. Counting sequences:  
```
grep -c ">" AT_cDNA.fa
grep -c ">" RefSeq.faa
```
### 2. Looking for genes or features:  
```
grep ">" AT_cDNA.fa
grep ">" AT_cDNA.fa | less
```
### 3. Subtracting one list from another:
If there is a small list of genes that you want to remove from a larger list, you can use the grep function with these options:  
```
grep -Fvw -f sub_list.txt full_list.txt
```
here -F and -w will make sure that the full word is used as literal string, -v will NOT print the matching patterns and -f filename.txt is to say that the input patterns are in the file.  
### 4. Count a word:  
```
grep -oP "AT1G\d+" AT_cDNA.fa | sort | uniq -c 
grep -oPn "Cysteine.+" AT_cDNA.fa | less
grep -i "transcription factor" AT_cDNA.fa
grep -i "TFIIIA" AT_cDNA.fa
```
### 5. Search a motif:  
```
grep --color "GAATTC" ./Sequences/NT21.fa
grep --color "C..C............H...H" RefSeq.faa
```
### 6. Finding patterns that DOES NOT match:  
```
grep -i "transcription factor" AT_cDNA.fa| grep -v "chr1"
grep -i "transcription factor" AT_cDNA.fa| grep "chr1"
```
### 7. Searching for more than one pattern:  
```
grep 'pattern1|pattern2|pattern3' FILENAME
grep 'pattern1' FILENAME | grep 'pattern2' | grep 'pattern3'
```
理解下列命令的功能：  
```
grep -c -w "ATP" RefSeq.faa
grep -c CGT[CA]GTG AT_cDNA.fa
grep -l "ATG" ./Sequences/*.fa
grep -l "ATGTTTT" ./Sequences/*.fa
```
### 8. Finding blank lines  
```
grep "^$" FILENAME
grep -v "^$" FILENAME
```
### 9. Finding all the files that contain a term  
```
grep -rl "PATTERN" .
grep -rL "PATTERN" .
```
### 10. Print lines before or after the matching term  
```
grep -B 10 "YP_665686" RefSeq.faa
grep -A 10 "YP_665686" RefSeq.faa
grep -B 10 -A 10 "YP_665686" RefSeq.faa
```
