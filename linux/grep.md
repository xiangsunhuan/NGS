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
Now let’s use grep command to do some simple jobs with the sequences:
