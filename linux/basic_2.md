This exercise will provide you details about some administrative commands with examples. Here, you can learn how to change permissions for files and folders to modify its accessibility and commands to obtain information about the system you are using.
## Changing permissions  
All files in the UNIX system will have a set of permissions which define what can be done with that file and by whom. Here, what refers to read (view contents), write (modify) and execute (run as a script) and whom refers to user (owner), group (collection of users that the user belongs to) and others (everyone else).  

| Permissions |	Symbol |
| --- | --- |
| read | r |
| write |	w |
| execute |	x |
| all users |	a |  

| Relations |	Symbol |
| --- | --- |
| owner |	u |
| group |	g |
| others |	o |  

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
理解各列的含义  

To set/modify a file’s permissions you need to use the `chmod` command (`ch`ange `mod`e). Only the owner of a file can alter a file’s permissions. The syntax:  
```
chmod [OPTIONS] RELATIONS[+ or -]PERMISSIONS FILE
# 1. Adding permissions
chmod RELATIONS+PERMISSIONS FILENAME
chmod g+rwx FILENAME
chmod g+r FILENAME
# 2. Removing permissions
chmod g-wx FILENAME
chmod g-rwx FILENAME
chmod a-rwx FILENAME
chmod a-x FILENAME
```
OPTIONS include -R recursively (the permissions are applied to all the files, directories present inside the directory)  
## Check system properties  
In this section, you will learn how to check system resources (space, memory, disk usage, storage properties), system properties (operating system, Linux version, kernel version) and commands to access other information (CPU type, memory type, variables available etc ) about the environment  
```
# 1. Directory size
du -sh DIRECTORY
# 2. File size
ls -lh FILENAME

# 3. Available storage and mounts
df -h

# 4. Available memory
free 
free -g
free -m

# 5. System properties
cat /etc/system-release
uname -a
uname -s # kernel name
uname -n # node
uname -v # version
uname -r # release version date
uname -i # platform
uname -m # machine type
uname -p # processor type
uname -o # OS type

# 6. Processor and Memory information
cat /proc/meminfo
cat /proc/cpuinfo

# 7. IP address
ifconfig

# 8. Other information
env
For getting more information about the environment, you can type env, which lists all the variables currently set. If you want to know specifically about a variable, you can do:
echo $VARIABLE
```
