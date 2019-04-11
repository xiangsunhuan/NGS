This exercise is designed to provide the basic skills required for working in the UNIX environment, using plenty of relevant examples, specifically for biologists.

## 准备数据  
```
cd ~
ln -s /data/lab/ngs/linux/WORKSHOP_FILES ./
cd WORKSHOP_FILES
ls
```
## Navigation  

```
pwd
cd ..
```
## Directories and files  
```
mkdir FirstDirectory
cp SOURCE DESTINATION
cp -r WORKSHOP_FILES BACKUP_WORKSHOP
mv SOURCE DESTINATION
mv OLDNAME NEWNAME
ls DIRECTORY
ls –l #Lists all the files in lengthy or detailed view
ls –t #Lists all the files, sorted based on creation time
ls –S #Lists all the files, sorted based on size
touch firstfile
nano firstfile
less AT_cDNA.fa
more AT_cDNA.fa
cat AT_cDNA.fa
head AT_cDNA.fa
rmdir DIRECTORY
rm FILE

```
## Compression/Decompression  
```
zip OUTFILE.zip INFILE.txt
zip -r OUTDIR.zip DIRECTORY
zip -r OUTFILE.zip . -i *.txt
unzip SOMEFILE.zip
tar -cvf OUTFILE.tar INFILE
tar -czvf OUTFILE.tar.gz INFILE
tar -czvf OUTFILE.tar.gz DIRECTORY
tar -czvf OUTFILE.tar.gz *.txt
tar -tvf SOMEFILE.tar
tar -xvf SOMEFILE.tar
tar -xzvf SOMEFILE.tar.gz
gzip SOMEFILE
gunzip SOMEFILE.gz
gzip AT_genes.gff
ls -lh
gunzip AT_genes.gff.gz
ls –lh
```
