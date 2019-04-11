This exercise will provide you details about some administrative commands with examples. Here, you can learn how to change permissions for files and folders to modify its accessibility and commands to obtain information about the system you are using.
## Changing permissions  
All files in the UNIX system will have a set of permissions which define what can be done with that file and by whom. Here, what refers to read (view contents), write (modify) and execute (run as a script) and whom refers to user (owner), group (collection of users that the user belongs to) and others (everyone else).  
To look at the permissions for any file, you can list the files with `l` option (`ls –l`). Permissions User	Group	Size	Date modified	Name.  
It looks something like this:   
```
total 452948
-rwxr-xr-x 1 wangys wangys  71717780 Aug 29  2013 AT_cDNA.fa
-rwxr-xr-x 1 wangys wangys  44139005 Aug 29  2013 AT_genes.gff
drwxr-xr-x 2 wangys wangys      4096 Aug 29  2013 delete_me
-rwxr-xr-x 1 wangys wangys      2053 Aug 29  2013 genes_a.gff
-rwxr-xr-x 1 wangys wangys      2667 Aug 29  2013 genes_b.gff
-rwxr-xr-x 1 wangys wangys       350 Aug 29  2013 ids_a.txt
-rwxr-xr-x 1 wangys wangys       350 Aug 29  2013 ids_b.txt
-rwxr-xr-x 1 wangys wangys       500 Aug 29  2013 ids.txt
-rwxr-xr-x 1 wangys wangys      1183 Jun 23  2014 jobfile.sub
-rwxr-xr-x 1 wangys wangys 172857623 Aug 29  2013 R1.fastq
-rwxr-xr-x 1 wangys wangys 175047333 Aug 29  2013 R2.fastq
-rwxr-xr-x 1 wangys wangys      6055 Aug 29  2013 RefSeq.faa
drwxr-xr-x 2 wangys wangys      4096 Aug 29  2013 Sequences
-rwxr-xr-x 1 wangys wangys      1196 Jun 23  2014 template_jobfile.sub
```
To set/modify a file’s permissions you need to use the `chmod` command (`ch`ange `mod`e). Only the owner of a file can alter a file’s permissions. The syntax:  
```

```
