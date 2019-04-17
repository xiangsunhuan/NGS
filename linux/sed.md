## 流编辑器sed  

The `s`treamline `ed`itor or sed command is a stream editor that reads one or more text files, makes changes or edits according to editing script, and writes the results to standard output. First, we will discuss `sed` command with respect to search and replace function. Other uses for the `sed` can also be found in this official guide, but we will discuss them briefly in this chapter as well.

### 1. Find and replace  
查找并替换，语法如下：  

```
sed 'OPERATION/REGEXP/REPLACEMENT/FLAGS' FILENAME
```
* Here, / is the delimiter (you can also use _ (underscore), | (pipe) or : (colon) as delimiter as well)  
* `OPERATION` specifies the action to be performed (sometimes if a condition is satisfied). The most common and widely used operation is s which does the substitution operation (other useful operators include y for transformation, i for insertion, d for deletion etc.).  
* `REGEXP` and `REPLACEMENT` specify search term and the substitution term respectively for the operation that is being performed.  
* `FLAGS` are additional parameters that control the operation. Some common FLAGS include:  
  * `g`	replace all the instances of REGEXP with REPLACEMENT (globally)  
  * `N` where `N` is any number, to replace Nth instance of the REGEXP with REPLACEMENT  
  * `p` if substitution was made, then prints the new pattern space   
  * `i` ignores case for matching REGEXP  
  * `w` file If substitution was made, write out the result to the given file  
  * `d` when specified without REPLACEMENT, deletes the found REGEXP  

一些例子：  

```
# 1. find and replace all chr to chromosome in the file替换所有的  
sed 's/chr/chromosome/g' FILENAME > NEWFILE
# 2. find and replace, but only the one instance per line (first occurrence of chr will be changed to chromosome)只替换第一个
sed 's/chr/chromosome/1' FILENAME > NEWFILE
# 3. find and replace, but do it directly on the original file直接编辑原文件
sed -i 's/chr/chromosome/g' FILENAME
# 4. find and replace directly, but save a old version too直接编辑原文件，但保存副本
sed -i.old 's/chr/chromosome/g' FILENAME
# 5. find and replace, only if you also find MTF1 in the line有条件的替换
sed '/MTF1/s/chr/chromosome/g' FILENAME > NEWFILE
```

### 2. Print specific lines of the file  
To print a specific line, you can use the address function, note that by deafault, `sed` will stream the entire file, so when you are interested in specific lines only, you will have to suppress this feature using the option `-n`.  
Some examples:  
```
# 1. print 10th line
sed -n '10p' FILENAME
# 2. You can provide any number of additional lines to print using -e option (you can add any number of lines like this)
# print 10th and 15th line
sed -n -e '10p' -e '15p' FILENAME
# 3. It also accepts range, using ,
sed -n '10,50p' FILENAME
# 4. or you can create specific pattern, like multiple of a number using ~
# Every tenth line starting from 10, 20, 30.. to end of the file
sed -n '10~10p' FILENAME
# 5. print odd-numbered lines
sed -n '1~2p' FILENAME
# 6. Most powerful feature is that you can combine these ranges or multiples in any fashion. Example: fastq files have header on first line and sequence in second, next two lines will have the quality and a blank extra line (four lines make one read). Sometimes you will only need the sequence and header
# to print 1,2,5,6,9,10 so on you can use
sed -n '1~4p;2~4p' FASTQ_FILE
# 7. pipe this to make a fasta file
sed -n '1~4p;2~4p' FASTQ_FILE | sed 's/^@/>/g' > FASTA_FILE
# 8. print 1 to 10, and then multiples of 10
sed -n '1,10~10p'  FILENAME
```
