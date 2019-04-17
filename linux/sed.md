## 流编辑器sed  

The `s`treamline `ed`itor or sed command is a stream editor that reads one or more text files, makes changes or edits according to editing script, and writes the results to standard output. First, we will discuss `sed` command with respect to search and replace function. Other uses for the `sed` can also be found in this official guide, but we will discuss them briefly in this chapter as well.

### 1. Find and replace  
查找并替换，语法如下：  

```
sed 'OPERATION/REGEXP/REPLACEMENT/FLAGS' FILENAME
```
* Here, / is the delimiter (you can also use _ (underscore), | (pipe) or : (colon) as delimiter as well)  
* OPERATION specifies the action to be performed (sometimes if a condition is satisfied). The most common and widely used operation is s which does the substitution operation (other useful operators include y for transformation, i for insertion, d for deletion etc.).  
* REGEXP and REPLACEMENT specify search term and the substitution term respectively for the operation that is being performed.  
* FLAGS are additional parameters that control the operation. Some common FLAGS include:  
** g	replace all the instances of REGEXP with REPLACEMENT (globally)  
** N where N is any number, to replace Nth instance of the REGEXP with REPLACEMENT  
** p if substitution was made, then prints the new pattern space   
** i ignores case for matching REGEXP  
** w file If substitution was made, write out the result to the given file  
** d when specified without REPLACEMENT, deletes the found REGEXP  

